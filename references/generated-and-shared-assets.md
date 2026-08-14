# Generated and shared assets

Use this reference before changing an avatar feature that crosses a scene,
prefab, provider, or build boundary. The editable source is the place where a
tool expects the user to make a change. A generated result, build clone, or
cache is evidence or a disposable product, not automatically an edit target.

## Ownership boundaries

| Boundary | Source of truth | Typical contents | Safe default |
| --- | --- | --- | --- |
| Scene override (instance) | The exact scene instance and its prefab modifications | Active state, local transform, added or removed component, overridden reference | Edit only the named instance after mapping its prefab and consumers. Do not assume the prefab asset changes. |
| Shared asset | The referenced asset file | Prefab, menu, parameters, controller, animation clip, material, mesh, or texture used by multiple roots | Map every consumer first. A change is a multi-consumer change unless isolation is proven. |
| Editable generator source | The provider component, source prefab, configuration asset, or stable user clip | FaceEmo expressions, Modular Avatar components, inventory or wardrobe settings, generic feature providers, optimizer settings | Edit the source supported by that provider, then use its documented preview or regeneration path. |
| Generated output | The provider's generated controller, menu, parameter asset, merged component, or optimized result | Timestamped tool output, NDMF result, merged Animator, optimized mesh/material | Inspect or diff it, but do not edit it as the source of truth. Regenerate from source. |
| Build clone | A temporary avatar clone made for preview or SDK build | NDMF preview clone, SDK build copy, test-only hierarchy | Treat as disposable. Record the exact source fingerprint and target; never copy changes back by guessing. |
| Cache | A tool or editor cache | Library, Temp, SDK build cache, provider cache, stale report | Diagnostic only. It may be stale or match more than one avatar and cannot prove current source or upload state. |

Prefab overrides, added/removed components, inactive objects, and asset GUIDs
belong to the boundary where they are stored. A scene override can still point
at a shared clip or material. A generated output can still reveal a missing
source reference. Ownership follows the write path, not the object name.

## Provider ownership notes

These rules are generic; confirm the installed version's documented source and
build behavior before acting.

### FaceEmo

- Editable source is the FaceEmo configuration or source prefab: patterns,
  conditions, expression clips, Blink/Lip Sync settings, and Additional Object
  references.
- `Apply` or regeneration may write a FaceEmo prefab plus generated menu and FX
  assets. The generated assets are outputs and may be replaced or cleaned on a
  later run.
- A copied menu can have separate configuration while still sharing an
  animation clip. Map both prefab and clip consumers before editing.
- For a change, edit the source, keep custom clips in a stable user-owned
  directory, and regenerate. Inspect provider output, then NDMF output; do not
  hand-patch the generated controller or menu.

### Modular Avatar and NDMF providers

- Editable source is the component or source prefab that declares menu items,
  parameters, merge Animators, bone proxies, armature or object changes, and
  other provider settings.
- NDMF resolves order, remapping, deduplication, and generated names during
  preview/build. The merged clone is not a replacement for the source
  component.
- Changes to a shared source prefab or menu can affect every avatar that
  consumes it. Isolate the source before making a one-avatar change.
- Use provider preview for the source inventory and `NDMF_BUILT` for final merged
  menu, parameter, Animator, mesh, and component claims.

### lilycalInventory

- Editable source is the inventory item, AutoDresser or wardrobe configuration,
  menu placement, parameter mapping, and any linked wearable source.
- Its build pass may inject menus, parameters, toggles, object state, and
  Animator behavior. The generated menu or controller is not the edit entry.
- A migration must preserve item ownership, default active state, saved/sync
  semantics, menu path, and all wearable responsibilities, not only the visible
  clothing toggle.
- Validate inventory source, then provider preview/NDMF output and the target
  runtime layer for actual wardrobe behavior.

### Dressing Tools

- Editable source is the wardrobe or wearable configuration, including armature
  mapping, mesh settings, BlendShape sync, object toggles, constraints, and menu
  settings.
- A replacement by inventory, Modular Avatar, or another provider must recreate
  each responsibility before the Dressing Tools source is removed.
- Do not infer success from a menu item or an active wearable alone. Check bone
  paths, blendshape bindings, renderers, materials, PhysBones, Contacts, and
  defaults in the target root.

### Avatar Optimizer

- Editable source is the optimizer setting or component and the original mesh,
  material, and avatar configuration.
- Optimization can remove, merge, or rewrite meshes, materials, and components
  in the build clone. The optimized result is not a stable source asset.
- Any animation, material, blendshape, PhysBone, or Contact route that depends
  on a pre-optimized path must be checked against the `NDMF_BUILT` result.

## Pre-change consumer mapping

Complete this map before editing a shared asset, applying a provider, migrating
between providers, or deleting an old source. Keep the map scoped to the exact
target root, scene, or prefab, but include every known consumer of shared files.

1. Record the exact target hierarchy path, scene or prefab path, active state,
   dirty state, Unity and provider versions, and requested outcome.
2. Identify the write owner: scene override, shared asset, editable generator
   source, generated output, build clone, or cache. Record the GUID/fileID and
   prefab origin where relevant.
3. Enumerate direct and indirect consumers through GUID/fileID links and
   provider references. Include descriptor menus and parameters, menu
   installers/items, merge Animators, expression clips, controllers, meshes,
   materials, textures, constraints, PhysBones, Contacts, audio, and particles
   that the feature can reach.
4. Separate shared consumers from isolated copies. Do not use hierarchy
   similarity, root names, active state, or an old Pipeline Manager ID as proof
   of isolation.
5. Record the baseline evidence layer for each claim and the exact generated or
   build artifact, if one exists. Mark previews, builds, runtime tests, and
   uploads independently.
6. List the expected blast radius: which roots, prefabs, menus, parameters,
   clips, materials, or generated outputs can change after Apply, regeneration,
   preview, or build.
7. Define the recovery point and the smallest acceptance check before any
   destructive removal. A dirty scene, unsaved override, or ambiguous target
   is a stop condition, not a reason to guess.

## Migration responsibility checklist

When replacing one clothing, expression, or feature provider with another, mark
each responsibility as mapped, rebuilt, and verified for the exact target.

- [ ] Menu path, control type, default, page placement, and reachability.
- [ ] Parameter names, types, defaults, saved flags, sync mode, remaps, and
      per-avatar budget impact.
- [ ] Animator layers, states, transitions, drivers, clips, and layer order.
- [ ] Armature merge, bone proxies, constraints, root paths, and scale.
- [ ] Mesh renderers, submeshes, material slots, shader properties, textures,
      and platform importer settings.
- [ ] BlendShape names, weights, sync rules, and animation binding paths.
- [ ] Object toggles, active defaults, visibility, and fallback state.
- [ ] PhysBones, colliders, Contacts, senders/receivers, self/other filters,
      and local versus synced parameters.
- [ ] Audio, particles, lights, constraints, and other non-visual effects.
- [ ] Provider ordering, generated ownership, and duplicate menu/parameter
      claims after merge.
- [ ] NDMF/provider output diff against the mapped responsibilities.
- [ ] The named desktop, VR, multiplayer, or other runtime layer, when required.
- [ ] SDK build and upload readiness only when separately authorized.

Remove or disable the old provider only after the replacement has an inspected
source chain, a successful provider/NDMF check at the required layer, and a
consumer map that records what was intentionally retired. Update the map after
cleanup so a later audit does not mistake stale output for an active source.

## Generated-output editing policy

Do not edit timestamped or tool-owned generated output from FaceEmo, Modular
Avatar/NDMF, lilycalInventory, Dressing Tools, Avatar Optimizer, another provider, or an
SDK build. This includes generated menus, controllers, parameter assets,
merged components, optimized meshes/materials, build clones, and cache files.
Generated output may be regenerated, renamed, cleaned, or replaced, and a hand
edit is not a durable fix.

The narrow exception is an explicit, documented tool handoff that declares a
particular export user-editable and non-regenerated, with all of these
conditions: the exact artifact is isolated from shared consumers, the user has
authorized the edit, the regeneration and ownership behavior is recorded, and
the result is saved as a stable source or documented input for the next build.
If any condition is missing, inspect or diff the output and change the editable
source instead. Reading, diffing, and reporting generated output are always
distinct from editing it.
