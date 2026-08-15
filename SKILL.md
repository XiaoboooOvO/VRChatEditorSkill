---
name: inspect-vrchat-avatar-project
description: Inspect, diagnose, document, and explain VRChat Avatar SDK Unity projects with a toolchain-confirmation gate, player-menu-first baseline audit, durable project documentation, and evidence-led scope control across serialized source assets, Unity-resolved state, provider or NDMF output, SDK builds, and runtime validation. Use only for VRChat Avatar work when Codex receives a new avatar, must confirm expression, clothing, prop, preview, or optimization tools, trace a player-visible feature, inspect parameters, Animator layers, FaceEmo, lilycalInventory, Modular Avatar, DressingTools, Gesture Manager, Avatar Optimizer, PhysBones, Contacts, materials, textures, meshes, prefab overrides, build size, or maintain the audit after a relevant change. Do not use for VRChat World or Udon projects.
---

# Inspect VRChat Avatar Project

Inspect the smallest authoritative scope and label every conclusion by evidence layer. Treat project-local coordination documents and inventories as routing indexes, not as timeless proof.

Apply this workflow only to VRChat Avatars. Route VRChat Worlds, Udon, world scenes, and world runtime systems to a dedicated World workflow instead.

## Preserve intent and existing work

- Treat inspect, explain, review, audit, compare, and diagnose requests as read-only. Do not implement a fix unless the user asks for a change.
- Do not save scenes or prefabs, Apply overrides, refresh/import assets, enter Play Mode, build, upload, or publish unless the request authorizes that action.
- Inspect workspace status before changes. Preserve unrelated work and do not assume Git recovery exists.
- Keep upload as a separate authorization boundary. Permission to inspect, preview, test, or build does not imply permission to upload.
- For feature imports and visual-asset updates, record source footprint and the current size-evidence status. Run fresh SDK size reports, probe new build caches, or initiate size builds only when size/build validation is explicitly authorized.

## Orient from project-local knowledge

1. Find and read applicable `AGENTS.md` files and the project's documented entrypoint, such as `PROJECT_CONTEXT.md`.
2. Reuse task-relevant maintained-avatar inventories, menu maps, expression guides, parameter reports, and size guides when present.
3. Treat dated inventories as navigation. Cheaply recheck facts that can drift: Unity version, package versions, exact editor instance, active scene, target root, dirty/compile/play state, and relevant asset references.
4. Honor documented inactive, historical, generated, recovery, or out-of-scope boundaries.
5. Rescan broadly only when no usable inventory exists or a documented refresh trigger applies.

Do not encode project-specific avatar names, GUIDs, package versions, or grouping assumptions into this reusable workflow.

## Confirm the toolchain first

Unity MCP is required for every Editor-resolved query and every Unity-managed
action in this workflow. Before a complete baseline audit, confirm that the MCP
toolset is available and that an exact instance can be associated with the
target project. Static package and source detection may proceed without MCP,
but it cannot complete the menu-to-model audit or authorize Editor work.

Before a new Avatar baseline audit, read or create the project's
`TOOLCHAIN_PROFILE`. Detect installed packages and the target Avatar's actual
provider components without importing anything, then let the user confirm the
tool roles before the menu audit or any mutation.

Recommend this default profile when compatible:

- clothing and wardrobe: lilycalInventory;
- facial expressions: FaceEmo;
- props and reusable feature prefabs: the asset-declared provider, otherwise
  Modular Avatar;
- Unity preview: Gesture Manager only when requested;
- optimization: Avatar Optimizer only when requested or required by a measured
  target.

Support an existing DressingTools workflow without forcing migration. Treat an
unknown or asset-specific plugin through the generic provider route rather than
inventing specialized experience.

User selection and package presence are separate facts. Load a tool-specific
playbook only when the user selected that role and the exact tool is installed.
If the user selects a missing tool, stop before import until installation is
explicitly authorized. Read [references/toolchain-selection.md](references/toolchain-selection.md)
for the selection record and reuse rules.

## Maintain a durable audit index

For a newly received avatar, perform a read-only baseline audit and create or update project-owned documentation before proposing changes. Start from the player menu and trace each reachable function to its parameter, provider, controller or driver, exact model binding, and source files. Record passive systems separately; do not invent menu entries for PhysBones, automatic Contacts, or internal generator parameters.

Maintain documentation that covers:

- the confirmed toolchain profile and installed-provider evidence;
- exact avatar identity, versions, shared consumers, and evidence status;
- the complete player menu tree and menu-to-function chains;
- parameters in both directions: menu to parameter to consumer, and parameter back to owner and menu;
- one provider inventory record per plugin or project-owned feature;
- renderer, material, shader-property, texture, importer, animation-binding, and shared-consumer routes for visual assets;
- size evidence, including whether only source footprint or an exact SDK build is available.

Treat these documents as dated routing indexes. At the end of every relevant change, refresh the affected records and mark stale or unrun evidence explicitly. Read [references/audit-documentation-workflow.md](references/audit-documentation-workflow.md) for the required audit, menu architecture, change-delta, and update contracts.

## Lock the target before deep inspection

Record the exact:

- project path and Unity version;
- exact selected Unity MCP instance;
- active scene and whether it is saved or dirty;
- avatar hierarchy path, including whitespace and duplicate-name risks;
- requested feature or failure;
- intended evidence level and whether any mutation is authorized.

Do not infer the target from object recency, active state, a Pipeline Manager ID, structural similarity, or a previous session's editor instance.

## Use the evidence ladder

Classify findings with one of these labels:

1. `STATIC_SOURCE` - serialized files, GUID/fileID chains, literal values, and package metadata.
2. `UNITY_RESOLVED` - imported assets, prefab instances, component types, private serialized fields, and resolved hierarchy observed through the selected Unity MCP instance.
3. `PROVIDER_PREVIEW` - a tool's source/provider preview or introspection, before final transformation.
4. `NDMF_BUILT` - the generated avatar after NDMF, Modular Avatar, FaceEmo, Avatar Optimizer, or equivalent build passes.
5. `SDK_BUILD` - VRChat SDK validation and the exact built bundle or parameter result.
6. `CLIENT_RUNTIME` - behavior observed in Gesture Manager, Play Mode, Build & Test, desktop, VR, or multiplayer. Name the exact runtime layer.
7. `UPLOAD_CONFIRMED` - the explicitly authorized uploaded avatar and its observed result.

Read [references/evidence-and-authorization.md](references/evidence-and-authorization.md) whenever the requested conclusion may require preview, build, runtime, size, or upload evidence.

Never promote one layer into another. In particular, do not describe raw YAML, provider previews, or an old build cache as final player behavior.

## Route from the user's question

Choose the narrowest relevant route:

- Player-visible menu or feature: start at the complete player menu path, then follow control and value to parameter, provider/controller, state or clip, exact model binding, and built menu when final reachability matters.
- Facial expression or gesture: trace the editable source, generated ownership, Blink/Lip Sync/eye tracking interaction, and final merged FX behavior.
- Parameter addition, removal, or conflict: use installed SDK or provider APIs; calculate each target avatar independently and inspect type/default/sync conflicts.
- Clothing, accessory, or generated feature: identify the real provider chain and every responsibility it contributes, including menu, parameters, armature, mesh, blendshape, and object toggles.
- PhysBone or Contact: inspect exact transforms, roots, colliders, senders/receivers, allow-self/others settings, parameters, and runtime-dependent behavior.
- Material, texture, animation, or mesh: trace renderer path, material slot, material, shader property, texture/importer or clip binding, full GUID/fileID lineage, shared consumers, and platform import settings.
- Size or upload readiness: require explicit size-check authorization, distinguish compressed download size from uncompressed AssetBundle size, and associate results with one exact target and build.

Read [references/avatar-feature-routing.md](references/avatar-feature-routing.md) for the detailed route and stop conditions.

Use the selected tool route only when its `TOOLCHAIN_PROFILE` entry is confirmed:

- FaceEmo: read [references/faceemo-playbook.md](references/faceemo-playbook.md).
- lilycalInventory: read [references/lilycal-inventory-playbook.md](references/lilycal-inventory-playbook.md).
- Modular Avatar: read [references/modular-avatar-playbook.md](references/modular-avatar-playbook.md).
- DressingTools, Gesture Manager, or Avatar Optimizer: read
  [references/extended-tool-support.md](references/extended-tool-support.md).
- Any other provider: read [references/generic-provider.md](references/generic-provider.md).

For FaceEmo, lilycalInventory, or Modular Avatar work, use the selected playbook
as an execution checklist rather than a background description. Build its source
and ownership record before mutation, follow the task-specific diagnostic order,
edit only the identified stable source, and satisfy the playbook's acceptance
matrix before reporting success. If the installed version lacks an expected
component or field, stop and resolve the version's supported equivalent instead
of inventing or copying a schema.

## Trace Unity serialization narrowly

- Search `.unity`, `.prefab`, `.asset`, `.controller`, `.overrideController`, `.anim`, `.mat`, `.meta`, and task-relevant importer files.
- Resolve external references through both GUID and fileID. Resolve scene-local references through document anchors and prefab modifications.
- Include Prefab Instance overrides, removed components, added components, inactive objects, and duplicate names before concluding that a source prefab matches the scene instance.
- Do not feed the whole project to a generic YAML parser. Unity serialization uses tagged multi-document YAML, large anchors, prefab overrides, and engine-specific sub-assets.
- Treat `Library/`, `Temp/`, `Logs/`, `Obj/`, generated project files, previews, and caches as diagnostics unless the installed tool explicitly defines a particular artifact as evidence.

Static inspection is for routing and literal facts. Escalate when the answer depends on resolved or generated state.

## Require Unity MCP for Editor work

Before any Unity-resolved inspection, preview, import, refresh, scene or prefab
change, compilation, test, build, or upload:

1. Confirm that the Unity MCP server and required tools are callable.
2. Rediscover available instances; do not reuse an old instance identifier.
3. Select the exact project instance and prove its project path and Unity version.
4. Read editor state, active scene, dirty state, Play Mode, compilation/update state, and Console baseline before action.
5. Keep one owner for scene, prefab, import, compile, preview, test, build, and upload operations.
6. Stop and report if the selected instance, project, target, or scene cannot be proven.

If no usable Unity MCP connection exists, continue only with claims that static
source evidence can support. Mark Editor-dependent work `MCP_REQUIRED` or
`BLOCKED` and ask the user to connect the correct instance. This skill does not
use batch-mode Unity or a temporary Editor script as a silent substitute for
MCP. Read [references/unity-mcp-inspection.md](references/unity-mcp-inspection.md)
for the connection, ownership, retry, and evidence requirements.

## Respect shared and generated ownership

Before a change, classify the target as one of:

- scene-instance override;
- shared prefab, material, menu, parameters, controller, animation, or model asset;
- tool-owned editable source configuration;
- generated output;
- build clone or cache.

Map all known consumers before modifying shared assets. Do not edit timestamped or tool-owned generated output unless the tool explicitly documents it as the supported source of truth. Apply, regeneration, and build operations can affect more avatars than the selected scene object.

Read [references/generated-and-shared-assets.md](references/generated-and-shared-assets.md) when FaceEmo, Modular Avatar, lilycalInventory, DressingTools, Avatar Optimizer, or another generator participates.

## Validate in proportion to the claim

- For a literal serialized change, use static diff plus Unity import/compile when import occurred.
- For a resolved component or prefab claim, use the selected Unity MCP instance.
- For merged menus, parameters, Animator layers, optimized meshes, or generated components, inspect the NDMF/provider build output.
- For visual, audio, gesture, Contact, PhysBone, Blink, Lip Sync, eye tracking, or synchronization behavior, run the exact authorized runtime layer.
- For parameter limits, prefer SDK/provider APIs over hand arithmetic. Keep source estimates separate from final built cost.
- For bundle limits, use the exact current build. Do not infer size from scenes, FBX files, textures, or a structurally similar avatar.
- Treat values close to a hard platform limit as ordinary within-limit results. Do not prompt for optimization unless a hard limit is exceeded or the user explicitly requests optimization.
- Preserve provider ownership during menu work. Do not merge or interleave different plugins' menu leaves as an optimization strategy.
- Do not call an unrun layer `PASS`. Report it as `NOT_RUN`, `BLOCKED`, or `BUILD_REQUIRED`.

## Report compact evidence

Lead with the answer, then include:

- exact project, scene, and avatar root;
- affected feature and ownership boundary;
- evidence label for every material conclusion;
- key asset paths and GUID/fileID resolutions;
- live-state checks or build/runtime layer actually run;
- shared consumers and generated-source boundary;
- unresolved risks, unrelated pre-existing errors, and unrun layers;
- audit documents created or refreshed, and any affected record intentionally left unchanged;
- smallest safe next step.

Keep unrelated Console errors separate from task-caused failures. A process exit code alone is insufficient when a tool requires a completion marker or output artifact.
