# Modular Avatar playbook

Use only when Modular Avatar is selected in `TOOLCHAIN_PROFILE`, required by the
asset, or already owns a task-relevant feature on the exact target. Resolve the
installed version and component types from the project; do not assume that a
field or inspector label from another version still exists.

## Establish the MA build graph

Treat MA components and source prefabs as declarations. Treat NDMF preview,
manual bake, build clones, merged controllers, and generated assets as outputs.
Never repair an output when the supported source component can be repaired.

For the exact Avatar, record this graph before diagnosing or changing anything:

```text
player entry or passive feature
-> source prefab and MA component
-> declared menu, parameter, Animator, armature, mesh, or object responsibility
-> NDMF pass and ordering relationship
-> remapped or merged build result
-> exact model or runtime effect
```

Inventory the installed version's equivalents of:

- Menu Installer, Menu Item, and Menu Group;
- Parameters and parameter remaps;
- Merge Animator and Merge Motion;
- Merge Armature, Bone Proxy, constraints, and path remaps;
- Mesh Settings and BlendShape synchronization;
- Object Toggle or reactive-object components;
- Contacts, PhysBones, platform filters, and other NDMF providers that share the
  same objects, parameters, menus, or build phase.

Record component hierarchy path, enabled state, source prefab, target reference,
merge or install destination, parameter names and defaults, Animator layer or
motion source, attachment root, path remaps, and shared consumers. Package
presence alone is not feature ownership.

## Read-only inspection sequence

1. Lock the exact Avatar and Unity MCP instance. Record scene dirty/compile state
   and the task-relevant Console baseline.
2. Start from the player-visible menu path or named passive feature. Locate the
   closest MA declaration that contributes it.
3. Walk upward to the source prefab or stable scene configuration. Distinguish
   prefab source values from scene-instance overrides.
4. Walk sideways to every other provider contributing the same parameter,
   Animator layer, armature path, object, mesh, or menu destination.
5. Walk forward to provider preview or NDMF output. Resolve generated names,
   deduplicated parameters, merged menu placement, Animator ordering, armature
   remaps, and final component ownership.
6. Compare source intent with build output. Report the first layer where the
   chain diverges; do not skip directly from a source component to runtime.

Stop at `UNITY_RESOLVED` when preview/build is not authorized. Mark merged
behavior `BUILD_REQUIRED` rather than guessing how NDMF will resolve it.

## Common task: missing or misplaced menu item

Check in this order:

1. Confirm the source menu control exists and is reachable from the intended
   menu asset or generated provider entry.
2. Confirm the Menu Installer/Item/Group component is enabled on an active build
   source and targets the intended menu destination.
3. Confirm no scene override removed the component, changed its target, or left
   a stale menu asset reference.
4. Confirm the provider owns the parameter and control value used by the item.
5. Inspect NDMF output for final placement, page limits, deduplication, provider
   ordering, and conflicts with another menu owner.
6. Validate the final player path in the authorized preview/build layer.

Repair the stable source component or menu asset. Do not paste a generated menu
item back into the source tree. Do not merge leaves from unrelated providers
merely to save a page.

## Common task: parameter exists but the feature does nothing

Trace one exact chain:

```text
menu control and value
-> declared MA parameter, type, default, saved, and sync settings
-> final deduplicated/remapped parameter
-> Animator or reactive consumer
-> state, transition, motion, or object toggle
-> exact model binding
```

Compare all declarations of the same parameter name. A same-name declaration is
not automatically compatible: type, default, saved, sync, and local-only intent
can disagree. Inspect the built parameter result before claiming a conflict is
resolved. Use installed SDK/provider APIs for final cost; do not calculate the
256-bit budget by counting names.

## Common task: merged Animator is missing, reordered, or overridden

1. Identify the source controller or motion, target playable layer, path mode,
   layer-order setting, masks, defaults, and parameter dependencies.
2. Confirm the MA component is active and targets the selected Avatar rather
   than a sibling or inactive historical root.
3. Inventory other Merge Animator components and generators targeting the same
   playable layer. Record their ordering constraints and shared layer names.
4. Inspect NDMF output for renamed layers, path remaps, deduplication, and the
   final order.
5. For a behavior conflict, compare conditions, transition duration, Write
   Defaults, masks, and clips that bind the same property.

Do not repair a generated controller directly. Change the source controller,
MA declaration, or explicit ordering relationship, then regenerate and compare
the built result.

## Common task: armature, attachment, or mesh result is wrong

Check the source wearable or prop independently from the merge declaration:

- exact source and target armature roots;
- humanoid or transform paths after remapping;
- Bone Proxy or constraint destination;
- renderer root bone and bones array;
- mesh, material slots, BlendShapes, and BlendShape Sync mapping;
- object scale, activation, and prefab overrides;
- PhysBone and Contact roots, colliders, and shared consumers.

Inspect NDMF output for the final transform paths and renderer bindings. A
visible source hierarchy is not proof that Merge Armature succeeded. Do not copy
bone paths, mesh assignments, or proxy targets from a structurally similar
Avatar. When one source FBX or prefab is shared, isolate an Avatar-specific
override unless a shared change is explicitly intended.

## Common task: object toggle has the wrong default or visibility

Resolve source active state, MA toggle declaration, parameter default, Animator
default state, saved behavior, and platform filters as separate inputs. Compare
the result before and after NDMF. If two providers write the same object state,
assign one explicit owner or document the intended ordering; do not leave both
as accidental competing authorities.

Use a named runtime layer to validate persistence, local/remote visibility,
Contact behavior, or synchronization. An Editor hierarchy checkbox alone proves
only the inspected source state.

## Props and feature prefabs

Prefer an asset's declared provider. When MA is the selected owner, record the
attachment transform, Bone Proxy or constraint, menu, parameters, Animator,
toggles, materials, audio, particles, Contacts, PhysBones, defaults, platform
filters, and shared consumers. Do not assign a second provider the same
responsibility without an explicit integration map.

Before migrating an existing feature to MA:

1. List every responsibility owned by the old provider.
2. Map each responsibility to one MA source component or deliberate manual
   owner.
3. Preserve a recoverable copy or version-control checkpoint.
4. Build and validate the replacement before removing the old provider.
5. Remove old ownership only after the new menu, parameters, model bindings, and
   required runtime behavior pass.

## Mutation guardrails

Before editing, record the exact source component, affected prefab or scene
instance, shared consumers, authorized action, and required validation layer.
Prefer the smallest provider-supported edit. Recheck the Unity instance before
Apply, prefab changes, refresh, preview, or build.

After editing:

1. Save only the explicitly authorized source asset or scene.
2. Wait for import/compile completion and inspect new Console entries.
3. Regenerate through MA/NDMF rather than editing generated assets.
4. Compare the intended source declaration with the built menu, parameters,
   Animator, hierarchy, meshes, and components.
5. Refresh the toolchain profile, menu map, parameter index, provider inventory,
   generated-source record, and acceptance status.

## Acceptance matrix

| Claim | Minimum evidence |
| --- | --- |
| MA component is configured on the target | `UNITY_RESOLVED` exact component, target, and source references |
| Menu or parameter is present after merging | `NDMF_BUILT` or provider preview showing the final merged result |
| Animator layer or armature path survives remapping | `NDMF_BUILT` exact final layer/path and binding |
| Prop, clothing, or toggle behaves correctly | Named authorized runtime layer for the claimed behavior |
| Synced or saved behavior works for players | Named client/multiplayer test; source defaults are insufficient |

Report every unrun layer as `NOT_RUN`, `BUILD_REQUIRED`, or `BLOCKED`. A clean
source inspector and a clean Console do not prove the final MA result.
