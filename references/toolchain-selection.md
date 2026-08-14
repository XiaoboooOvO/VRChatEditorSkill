# Toolchain selection gate

Use this gate before the first menu audit for a new Avatar and whenever a tool,
provider, or asset-declared dependency changes. Tool selection is a user decision;
package detection is read-only evidence. Neither implies permission to install or
mutate a project.

Unity MCP is the required Editor transport for this workflow. Confirm the MCP
toolset and exact target-project instance before treating any component,
prefab-instance, scene, Console, preview, generated-state, or mutation claim as
Editor evidence. Without it, tool detection may continue from static source,
but the complete audit remains `MCP_REQUIRED`.

## Detect before recommending

Record the exact target Avatar and inspect:

1. Unity and VRChat SDK versions.
2. VPM and Unity package manifests.
3. Provider components on the Avatar and task-relevant prefabs.
4. Menu installers, parameter components, merge Animators, wardrobe sources,
   expression generators, preview helpers, and optimizer settings.
5. The asset author's declared dependencies and supported installation path.

Do not infer provider ownership from folder names or package presence alone. A
package can be installed but unused by the selected Avatar.

## Recommended roles

Present one decision per relevant category:

| Category | Default recommendation | Preserve instead when |
| --- | --- | --- |
| Clothing/wardrobe | lilycalInventory | The clothing declares another supported provider or the existing workflow is intentionally retained |
| Facial expressions | FaceEmo | The Avatar has a deliberate custom expression owner the user wants to keep |
| Props/features | Asset-declared provider, otherwise Modular Avatar | The prefab already has a supported provider configuration |
| Unity preview | Gesture Manager only when requested | No editor simulation is needed |
| Optimization | Avatar Optimizer only when requested or measured need exists | No optimization goal or hard-limit problem exists |

DressingTools is supported when already present. Do not recommend migration to
lilycalInventory only to standardize the project.

For a multi-category request, let the user choose each role independently, then
check the combined result for overlapping menu, parameter, Animator, armature,
mesh, toggle, Contact, PhysBone, and generated-output ownership.

## Record `TOOLCHAIN_PROFILE`

Store the profile in project-owned documentation using this minimum schema:

```text
target_avatar: <exact hierarchy or prefab path>
unity_mcp: <server/toolset and exact instance or unavailable>
clothing: <selected tool or manual>
expression: <selected tool or custom owner>
props: <selected provider rule>
preview: <tool or none>
optimization: <tool or none>
installed_evidence: <manifest/component/version sources>
missing_tools: <selected but absent tools>
shared_consumers: <known roots or prefabs>
authorized_actions: <inspect/import/configure/preview/build/runtime/upload>
status: CONFIRMED | NEEDS_USER_CHOICE | MISSING_TOOL | MCP_REQUIRED | STALE
```

User selection plus installed evidence activates a tool playbook. If either is
missing, use only the generic source audit and stop before provider mutation.

## Reuse and refresh

Reuse a confirmed profile on later tasks. Cheaply recheck package manifests,
target components, asset dependencies, and requested authorization. Ask again
only when the target Avatar changes, a provider is added/removed, a tool version
changes materially, an imported asset declares another provider, or the user
wants a different workflow.

Mark the old profile `STALE` rather than silently rewriting the user's choices.
