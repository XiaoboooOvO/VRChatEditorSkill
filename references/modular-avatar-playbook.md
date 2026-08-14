# Modular Avatar playbook

Use only when Modular Avatar is selected in `TOOLCHAIN_PROFILE`, required by the
asset, or already owns a task-relevant feature on the exact target.

## Declare, then inspect the build result

Treat Modular Avatar components and source prefabs as declarations. Trace Menu
Installer/Item/Group, Parameters, Merge Animator/Motion, Merge Armature, Bone
Proxy, Mesh Settings, BlendShape Sync, Object Toggle/reactive components,
constraints, Contacts, PhysBones, and platform filters that participate.

Preserve exact armature roots, transform paths, remaps, defaults, and shared
prefab consumers. Do not copy bone paths or parameter results from a structurally
similar Avatar.

NDMF resolves ordering, path remapping, generated names, deduplication, menu
merge, and final component ownership. Treat preview/manual-bake/build clones and
their generated assets as outputs, not editing sources.

## Props and feature prefabs

Prefer an asset's declared provider. When Modular Avatar is the selected owner,
record attachment transform, Bone Proxy/constraint, menu, parameters, Animator,
toggles, materials, audio, particles, Contacts, PhysBones, defaults, and shared
consumers. Do not assign a second provider the same responsibility without an
explicit integration map.

## Validation

Use source inspection for declarations, provider preview/NDMF output for merged
menus, parameters, Animators, meshes, bones, and components, and a named runtime
layer for visible, physical, audio, Contact, or synchronized behavior.

Update the toolchain profile and every affected menu, parameter, provider,
visual, size-evidence, and acceptance record after a change.
