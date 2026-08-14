# Extended general-purpose tool support

Use only for a tool selected in `TOOLCHAIN_PROFILE` and detected on the exact
target. These tools are supported but are not all default recommendations.

## DressingTools

Preserve an existing DressingTools workflow unless the user requests migration.
Map wardrobe/cabinet source, wearable configuration, armature and bone mapping,
mesh settings, BlendShape synchronization, object toggles, constraints, menu,
parameters, defaults, and shared consumers.

Do not infer correct fitting from a cabinet entry or visible object. Before a
migration, give every old responsibility a new owner and verify the required
provider/NDMF layer before removing the old components.

## Gesture Manager

Treat Gesture Manager as Unity editor preview and diagnostics, not an authoring
provider. Record whether the run used Play Mode, a clone, radial menu/parameter
emulation, clickable Contacts, gesture weights, Animator debugging, or OSC.

Label the result `CLIENT_RUNTIME` only with the exact qualifier
`Unity/Gesture Manager preview`; never promote it to VRChat desktop, VR,
multiplayer, SDK build, or upload proof.

## Avatar Optimizer

Treat optimizer settings and original assets as sources. Treat optimized meshes,
materials, components, paths, and clones as NDMF/build outputs. Check any menu,
animation, BlendShape, PhysBone, Contact, material, or renderer route against the
optimized result when the claim depends on it.

Do not recommend optimization merely because the package is installed or a
metric is near a limit. Enter optimization only on user request, confirmed hard
overflow, or a measured performance target. Preserve exact before/after build
evidence and do not edit optimized output as the durable fix.
