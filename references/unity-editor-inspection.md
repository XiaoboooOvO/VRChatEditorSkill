# Unity Editor inspection pattern

Use this reference only when static file inspection cannot answer the question reliably.

## Two-pass batch workflow

Place a uniquely named inspector in `Assets/Editor/`, then run Unity twice:

```powershell
$project = 'E:\path\to\project'
$unity = 'D:\path\to\matching\Editor\Unity.exe'

& $unity -batchmode -quit `
  -projectPath $project `
  -logFile "$project\Temp\CodexReports\import.log"
if ($LASTEXITCODE -ne 0) { throw 'Unity import or compilation failed.' }

& $unity -batchmode -quit `
  -projectPath $project `
  -executeMethod CodexVrcInspector.Run `
  -codexScene 'Assets/Avatar/Avatar.unity' `
  -codexReport 'Temp/CodexReports/avatar.json' `
  -logFile "$project\Temp\CodexReports\inspect.log"
if ($LASTEXITCODE -ne 0) { throw 'Unity inspection failed.' }
```

Create the report directory before launching Unity. Keep the inspector in place until both processes exit.

## Minimal inspector skeleton

Adapt the output fields to the user's question. Prefer a focused report over dumping every serialized property.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using UnityEditor;
using UnityEditor.SceneManagement;
using UnityEngine;
using VRC.SDK3.Avatars.Components;

public static class CodexVrcInspector
{
    [Serializable]
    private sealed class Report
    {
        public string unityVersion;
        public string scene;
        public List<AvatarRecord> avatars = new List<AvatarRecord>();
    }

    [Serializable]
    private sealed class AvatarRecord
    {
        public string path;
        public bool activeSelf;
        public string expressionsMenu;
        public string expressionParameters;
        public List<ObjectRecord> objects = new List<ObjectRecord>();
    }

    [Serializable]
    private sealed class ObjectRecord
    {
        public string path;
        public bool activeSelf;
        public bool activeInHierarchy;
        public string[] components;
    }

    public static void Run()
    {
        var scenePath = Argument("-codexScene");
        var reportPath = Argument("-codexReport") ??
            "Temp/CodexReports/avatar.json";

        if (String.IsNullOrWhiteSpace(scenePath))
            throw new ArgumentException("Missing -codexScene.");

        var scene = EditorSceneManager.OpenScene(scenePath);
        var report = new Report {
            unityVersion = Application.unityVersion,
            scene = scene.path
        };

        var descriptors = scene.GetRootGameObjects()
            .SelectMany(root =>
                root.GetComponentsInChildren<VRCAvatarDescriptor>(true));

        foreach (var descriptor in descriptors)
        {
            var avatar = new AvatarRecord {
                path = HierarchyPath(descriptor.transform),
                activeSelf = descriptor.gameObject.activeSelf,
                expressionsMenu = AssetDatabase.GetAssetPath(
                    descriptor.expressionsMenu),
                expressionParameters = AssetDatabase.GetAssetPath(
                    descriptor.expressionParameters)
            };

            foreach (var transform in
                     descriptor.GetComponentsInChildren<Transform>(true))
            {
                avatar.objects.Add(new ObjectRecord {
                    path = HierarchyPath(transform),
                    activeSelf = transform.gameObject.activeSelf,
                    activeInHierarchy = transform.gameObject.activeInHierarchy,
                    components = transform.GetComponents<Component>()
                        .Select(component => component == null
                            ? "<missing-script>"
                            : component.GetType().FullName)
                        .ToArray()
                });
            }

            report.avatars.Add(avatar);
        }

        var absoluteReportPath = Path.IsPathRooted(reportPath)
            ? reportPath
            : Path.Combine(Directory.GetCurrentDirectory(), reportPath);
        Directory.CreateDirectory(Path.GetDirectoryName(absoluteReportPath));
        File.WriteAllText(absoluteReportPath,
            JsonUtility.ToJson(report, true));

        Debug.Log("CODEX_VRC_INSPECTION_COMPLETE | " + absoluteReportPath);
    }

    private static string Argument(string name)
    {
        var args = Environment.GetCommandLineArgs();
        for (var index = 0; index + 1 < args.Length; index++)
            if (String.Equals(args[index], name,
                    StringComparison.OrdinalIgnoreCase))
                return args[index + 1];
        return null;
    }

    private static string HierarchyPath(Transform transform)
    {
        var names = new List<string>();
        while (transform != null)
        {
            names.Add(transform.name);
            transform = transform.parent;
        }
        names.Reverse();
        return String.Join("/", names);
    }
}
```

## Targeted extensions

- Inspect a private or version-sensitive field with `new SerializedObject(component)` and `FindProperty`. Check for a null property before reading it.
- Resolve any loaded object with `AssetDatabase.GetAssetPath`. Resolve an asset path to GUID with `AssetDatabase.AssetPathToGUID`.
- Inspect `descriptor.baseAnimationLayers` and `descriptor.specialAnimationLayers` for controller paths, but tolerate SDK-version field differences.
- Load an `AnimatorController` through `AssetDatabase.LoadAssetAtPath<AnimatorController>` when states, transitions, blend trees, or behaviours matter.
- Record Prefab origin through `PrefabUtility.GetCorrespondingObjectFromSource` and `PrefabUtility.GetPrefabAssetPathOfNearestInstanceRoot`.
- Identify missing scripts when `GetComponents<Component>()` contains null.

## Failure interpretation

- Treat compiler errors as blocking. Fix or remove the new inspector without changing unrelated project scripts.
- Treat a project-lock message as blocking. Close the interactive editor or use an intentional copy.
- Treat the absence of the completion marker or JSON report as failure even if Unity exits with code zero.
- Do not classify isolated licensing, package update, curl shutdown, or thread-abort messages as task failure when compilation succeeded, the report exists, the completion marker is present, and Unity exited successfully.
- Preserve the full Unity log path in the final report when inspection is incomplete.
