# lilycalInventory playbook

Use only when lilycalInventory is selected in `TOOLCHAIN_PROFILE` and the exact
package and target components are present.

## Provider chain

Trace the installed version's equivalent of:

`AutoDresser or Prop -> generated CostumeChanger or ItemToggler -> menu generator
and MenuFolder/placement -> parameters and Animator -> NDMF merged Avatar`

Record inventory host/settings, wearable source, active/default state, menu
placement, parameter names and remaps, saved/sync behavior, object toggles,
materials, presets, and every linked Avatar consumer.

An inactive clothing object can still participate in a build when its provider
component is enabled. Do not classify a disabled source object as broken without
checking provider semantics. Required settings or host components must be unique,
enabled, and attached to active objects when the installed version requires it.

## Clothing responsibilities

A visible wardrobe menu does not prove a complete wearable. Inspect armature and
bone mapping, mesh/root bone, BlendShape sync, material slots, constraints,
PhysBones/Contacts, defaults, and non-visual effects separately. Calculate
parameters for the exact Avatar rather than copying another root's cost.

When migrating from another provider, map every old responsibility to a new owner
before removing the old source. Preserve a recovery point and leave final NDMF,
SDK, and runtime layers unclaimed when they were not run.

## Validation and documentation

Use provider preview for source inventory and NDMF output for generated menus,
parameters, Animators, armature, and toggles. Use the named runtime layer for fit,
clipping, motion, visibility, saved state, Contact, or multiplayer claims.

Update the toolchain profile, menu map, parameter index, provider inventory,
clothing responsibility map, source footprint, size-evidence status, and
acceptance record after import, configuration, or migration.
