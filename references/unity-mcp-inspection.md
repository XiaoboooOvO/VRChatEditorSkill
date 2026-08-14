# Unity MCP inspection requirements

Use this reference whenever an Avatar conclusion or action depends on Unity
Editor state. Unity MCP is required for Editor-resolved inspection and for all
Unity-managed mutations in this workflow.

## Connection gate

Before Editor work:

1. Confirm that the Unity MCP server and the required read or mutation tools are
   callable.
2. Rediscover the available Unity instances. Do not reuse an instance ID from a
   previous session.
3. Associate exactly one instance with the requested project. Verify the project
   path, Unity version, active scene, and named Avatar target.
4. Read the dirty, compilation, update, and Play Mode state plus a Console
   baseline.
5. Stop on zero matches, multiple plausible instances, an unproven scene, a
   compiling/updating editor, or an ambiguous Avatar root.

Do not select an instance by recency, active-window status, scene name alone, or
a previous task's connection.

## Static work when MCP is unavailable

Static source inspection may still establish package versions, GUID/fileID
chains, literal serialized values, and likely menu or asset routes. Label those
findings `STATIC_SOURCE`.

Without a usable exact Unity MCP instance:

- do not claim `UNITY_RESOLVED` evidence;
- do not inspect or mutate scene, prefab, import, preview, build, or runtime
  state;
- do not create a temporary Editor script or launch Unity batch mode as a silent
  fallback;
- mark the missing layer `MCP_REQUIRED` or `BLOCKED` and state what remains
  unverified.

## Read-only MCP inspection

For inspection, prefer narrow queries tied to the exact target:

- exact hierarchy path and active state;
- component types and task-relevant serialized fields;
- source prefab and instance overrides;
- asset paths, GUIDs, fileIDs, controllers, menus, parameters, materials, and
  animation bindings;
- relevant Console entries after the recorded baseline;
- provider preview or generated state only when that explicit layer is
  authorized and available.

Do not dump the entire project when a focused object, asset, or menu chain can
answer the question.

## Mutation gate and single ownership

Before a mutation, confirm that the request authorizes the exact action and
target. Keep one agent or operator as the sole Unity owner for scene, prefab,
import, compilation, preview, test, build, and upload work.

Recheck the selected instance immediately before a consequential action. Do not
save scenes or prefabs, Apply overrides, refresh/import, enter Play Mode, build,
or upload merely because the MCP exposes that command.

## Failure and retry behavior

After a timeout or unclear response, inspect durable evidence first: Editor
state, Console, source changes, scene dirty state, and produced artifacts. Do
not blindly repeat a mutation that may already have succeeded.

Stop after two materially identical failures. Report the exact attempted layer,
the last proven state, and the smallest user or environment action needed to
continue.

## Evidence acceptance

Accept `UNITY_RESOLVED` only when the selected instance, project, scene, and
target are proven and the MCP query returned the requested state. A clean
Console or successful static parse alone is not Unity-resolved proof.

Keep provider preview, NDMF build, SDK build, client runtime, VR, multiplayer,
and upload as separate evidence layers. Name every layer that was not run.
