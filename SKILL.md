---
name: read-vrc-unity-project
description: Inspect and explain VRC SDK Unity avatar projects by combining static Unity serialization and GUID indexing, Unity Editor batch-mode inspection, and optional NDMF or Modular Avatar build-output verification. Use when Codex needs to locate avatar scenes or descriptors, trace GUID and fileID references, inspect hierarchies, components, expression menus, parameters, Animator layers, PhysBones, Contacts, materials, or Modular Avatar configuration, diagnose avatar behavior, or distinguish source-scene state from the avatar produced for VRChat.
---

# Read VRC Unity Project

Read the project in three layers: static files for fast discovery, Unity APIs for resolved object state, and the build pipeline for final generated state.

## Preserve the project

- Treat read, inspect, explain, review, and diagnose requests as read-only. Do not save scenes, prefabs, assets, or generated controllers unless the user asks for a change.
- Check workspace status and existing user changes before creating inspection files. Never revert unrelated work.
- Treat `Assets/`, `Packages/`, and `ProjectSettings/` as project sources. Treat `Library/`, `Temp/`, `Logs/`, `Obj/`, and generated `.csproj` files as caches or diagnostics, not source of truth.
- Put reports under `Temp/CodexReports/` by default. Do not place generated reports under `Assets/`.
- Do not upload an avatar or invoke a VRChat SDK publish action during inspection.

## Establish the baseline

1. Confirm the directory contains `Assets/`, `Packages/`, and `ProjectSettings/`.
2. Read `ProjectSettings/ProjectVersion.txt` and use the exact Unity editor version.
3. Read `Packages/manifest.json`, `Packages/packages-lock.json`, and `Packages/vpm-manifest.json` when present.
4. Record the VRC SDK, Modular Avatar, NDMF, Avatar Optimizer, VRCFury, shader, and other build-affecting package versions.
5. Enumerate every `.unity` file under `Assets/`. Do not assume `EditorBuildSettings.asset` identifies the avatar scene; avatar projects commonly leave its scene list empty.
6. Locate likely avatar scenes by searching for `VRCAvatarDescriptor` serialization, `customExpressions`, `expressionParameters`, `baseAnimationLayers`, and known avatar root names.

## Read static Unity serialization

Use fast text inspection first for targeted questions.

- Search `.unity`, `.prefab`, `.asset`, `.controller`, `.overrideController`, `.anim`, `.mat`, and `.meta` files.
- Trace an external reference by copying its `guid`, finding the `.meta` file containing that GUID, and then opening the adjacent asset.
- Interpret `fileID` as the object or sub-asset identity inside the referenced file. Preserve both GUID and fileID when reporting evidence.
- Follow scene-local links through Unity document anchors such as `--- !u!1 &12345` and references such as `{fileID: 12345}`.
- Inspect Prefab Instance modifications and removed or added components before concluding that a source prefab matches its scene instance.
- Use exact object paths when possible. Names are not unique, and inactive duplicates are common.
- Do not feed the complete project to a generic YAML parser. Unity serialization uses tagged multi-document YAML, large integer anchors, prefab overrides, and engine-specific object references.

Static inspection is sufficient for locating assets, checking literal values, tracing references, and narrowing the semantic inspection target.

## Escalate to Unity semantic inspection

Use Unity Editor APIs when the answer depends on resolved prefab instances, imported models, component types, private serialized fields, inactive objects, Animator sub-assets, or exact object hierarchy.

Read [references/unity-editor-inspection.md](references/unity-editor-inspection.md) before writing or running an inspector.

Follow these rules:

1. Locate the Unity executable matching `ProjectVersion.txt`; do not silently use a different version.
2. Ensure no other Unity process has the same project open, or inspect a deliberate copy. Unity normally permits one editor process per project.
3. Create a uniquely named temporary editor script under `Assets/Editor/`. Do not overwrite an existing file.
4. Launch Unity once in batch mode to import and compile the script.
5. Launch Unity a second time with `-executeMethod` to run it. A newly added method is not reliably available in the same launch that first imports it.
6. Open the intended scene explicitly with `EditorSceneManager.OpenScene`.
7. Include inactive objects with `GetComponentsInChildren<T>(true)`.
8. Report full hierarchy paths, active state, component type, asset path, GUID, and relevant values.
9. Use `AssetDatabase.GetAssetPath` for object references and `SerializedObject` for targeted serialized fields not exposed by a stable public API.
10. Emit a machine-readable JSON report plus a unique completion marker. Treat arbitrary `Error` text in Unity package or licensing logs as diagnostic noise unless the process exit code, compilation status, or completion marker also indicates failure.
11. Do not call `SaveScene`, `SaveAssets`, or prefab save APIs during a read-only inspection.
12. Remove a temporary inspector only after all Unity processes have exited. Remove its `.meta` with it and allow a final refresh; otherwise stale compilation state can reference a deleted source file.

## Distinguish source state from built state

Check the installed packages before interpreting the raw scene.

- Treat Modular Avatar, NDMF plugins, Avatar Optimizer, VRCFury, and similar systems as build-time transformations.
- Describe raw-scene findings as source configuration, not as the guaranteed uploaded avatar.
- When the question asks whether a menu, parameter, Animator, mesh, or component exists in the final avatar, run the installed version's supported preview or build pipeline and inspect the generated clone or build artifact.
- Keep preview and upload separate. Never infer permission to publish from permission to inspect.
- State clearly whether each conclusion comes from static source, Unity-resolved source state, or generated build state.

## Inspection checklist

Inspect only the categories relevant to the request:

- Avatar Descriptor and avatar root
- Expression Menu and Expression Parameters
- Base and special animation layers, controllers, states, transitions, and parameter drivers
- Modular Avatar menu installers, menu items, object toggles, bone proxies, merge components, and parameter components
- PhysBones, colliders, Contacts, stations, and constraints
- Skinned meshes, blendshapes, materials, shaders, and missing references
- Active state, transforms, duplicate names, missing scripts, and prefab overrides
- NDMF or optimizer changes when final behavior matters

## Report the result

Lead with the answer, then provide:

- Unity and VRC SDK versions
- Scene and avatar root inspected
- Evidence paths and GUID resolutions
- Whether the finding is static, Unity-resolved, or build-resolved
- Unresolved references, compilation failures, or version mismatches
- The smallest safe next step when more certainty is required

Do not claim final VRChat behavior from raw YAML alone when a build-time system participates.
