# lilycalInventory playbook

Use only when lilycalInventory is selected in `TOOLCHAIN_PROFILE` and the exact
installed package, target Avatar, and task-relevant components are present.
Discover the installed version's component and field names through Unity MCP;
do not copy host references, menu folders, parameters, or generated objects from
another Avatar.

## Establish the wardrobe provider chain

Trace the installed version's equivalent of:

```text
wearable source or prop
-> inventory host/settings and provider component
-> generated CostumeChanger, ItemToggler, or equivalent owner
-> menu generator and menu placement
-> parameters and Animator
-> armature, renderer, material, and object responsibilities
-> NDMF merged Avatar
-> named runtime behavior
```

Treat the wearable, provider component, inventory settings, stable presets, and
user-authored assets as editable sources. Treat generated menu assets,
controllers, parameters, build clones, and NDMF results as outputs unless the
installed provider explicitly documents otherwise.

Before diagnosis or mutation, record:

- exact Avatar and wearable hierarchy paths;
- package version and installed component types;
- inventory host/settings and whether the required host is unique and active;
- wearable source prefab, scene overrides, active/default state, and provider
  enabled state;
- menu folder/placement, generated control name, parameter name/type/default,
  saved/sync behavior, and remaps;
- object toggles, presets, materials, armature, meshes, BlendShapes, constraints,
  PhysBones, Contacts, and non-visual effects;
- every Avatar, prefab, menu, parameter asset, material, mesh, and clip consumer.

An inactive clothing object can still participate in a build when its provider
component is enabled. Do not classify source inactivity as failure until the
installed provider semantics and built result are checked.

## Build a clothing responsibility map

For each wearable or item, record one owner for every applicable responsibility:

| Responsibility | Required record |
| --- | --- |
| Player entry | Complete menu path, control type/value, icon, and placement owner |
| Parameter | Name, type, default, saved/sync intent, remap, and final consumer |
| Visibility | Source active state, generated toggle, Animator state, and platform filters |
| Fit | Armature/root, bone mapping, renderer root bone/bones, constraints, and scale |
| Mesh | Renderer, mesh, material slots, BlendShapes, and BlendShape synchronization |
| Physics | PhysBone/Contact roots, colliders, filters, parameters, and runtime dependency |
| Preset | Included items, exclusivity, defaults, and interaction with individual toggles |
| Generated result | Final menu, parameters, Animator, hierarchy, and NDMF ownership |

A visible wardrobe menu proves only menu reachability. It does not prove fit,
clipping, motion, saved state, synchronization, or correct physics.

## Read-only inspection sequence

1. Lock the exact Avatar and Unity MCP instance; record scene, compile, and
   Console state.
2. Start from the player wardrobe menu or named wearable and locate the exact
   provider source.
3. Resolve inventory host/settings, provider components, wearable source,
   prefab overrides, and shared consumers.
4. Build the responsibility map, including responsibilities owned by another
   provider rather than lilycalInventory.
5. Inspect provider preview or NDMF output for generated menus, parameters,
   Animator layers, object toggles, armature, and hierarchy changes.
6. Compare the source record with the generated result and identify the first
   divergence.

Without authorized preview/build, stop before final generated claims and mark
them `BUILD_REQUIRED` or `NOT_RUN`.

## Common task: add one wearable or item

1. Confirm the asset author's supported installation path and required provider.
2. Record the wearable's source prefab, armature/mesh requirements, menus,
   parameters, materials, physics, presets, and non-visual effects.
3. Confirm the target inventory host and intended menu placement. Do not create
   a second host when the installed version requires one shared host.
4. Add or configure the smallest provider-supported source component.
5. Choose parameter/default/saved/sync behavior deliberately; do not inherit a
   sibling wearable's values without checking intent and final budget.
6. Preserve source active-state semantics required by the provider.
7. Preview/build and inspect the final menu, parameter, Animator, hierarchy,
   armature, renderer, and toggle result.
8. Run the authorized fit/visibility/runtime checks before calling the wearable
   complete.

Record the imported source footprint. Leave marginal SDK bundle size
`NOT_MEASURED` unless an exact comparable size build was explicitly authorized.

## Common task: menu item is missing or in the wrong folder

Check in this order:

1. Confirm the provider source and inventory host are enabled and associated
   with the selected Avatar.
2. Confirm the item is registered in the intended inventory/settings source.
3. Confirm menu folder/placement references are valid and not stale scene
   overrides.
4. Confirm the generated control has a compatible parameter and value.
5. Inspect NDMF output for final placement, page capacity, ordering, and
   ownership conflicts with another menu provider.
6. Validate the complete player path in the authorized preview/build layer.

Repair the provider source or placement declaration. Do not hand-add the item to
a generated menu that regeneration will replace.

## Common task: wrong default, saved state, or exclusivity

Resolve these inputs separately:

- source object active state;
- provider item default;
- generated Animator default state;
- parameter default, saved, synced, or local behavior;
- preset membership and exclusive-group rules;
- another provider or manual FX state writing the same object.

Inspect the built parameter and Animator result. Use a fresh runtime state when
testing defaults, and a second launch or explicit reset when testing persistence.
Use a named multiplayer test for remote synchronization; local preview is not
proof of network behavior.

## Common task: wearable appears but fit or motion is wrong

Check exact source and built values for:

- source/target armature roots and bone mapping;
- renderer root bone, bones array, and mesh binding;
- transforms, scale, constraints, and Bone Proxy or Merge Armature providers;
- BlendShapes and BlendShape synchronization;
- material slots, clipping masks, and body-hiding responsibilities;
- PhysBone and Contact roots, colliders, and filters;
- shared FBX, mesh, material, and prefab consumers.

Do not use a successful menu toggle as fit evidence. Do not copy bones, meshes,
or body references from a structurally similar Avatar. Isolate a target-specific
override when a shared source should not change for every consumer.

## Common task: migrate from another wardrobe provider

1. Snapshot the old provider and preserve a recovery point.
2. Complete the responsibility map for every menu, parameter, preset, armature,
   mesh, BlendShape, material, physics, Contact, audio, and object responsibility.
3. Assign each responsibility to lilycalInventory, another provider, or a
   deliberate manual owner. Leave no accidental dual ownership.
4. Build and validate the new provider while the old source remains recoverable.
5. Compare menu path, defaults, parameter cost, fit, saved/sync behavior, and
   runtime effects.
6. Remove the old provider only after the replacement passes the required
   evidence layers and the user authorized removal.

Do not migrate merely to standardize a project that already has a deliberate,
working provider.

## Parameter and limit checks

Calculate the exact selected Avatar independently. Inventory descriptor
parameters plus every provider contribution, then use installed SDK/provider
APIs or a project-owned report for the final built cost. Do not estimate the
256-bit budget by counting parameter names or copy a result from a similar root.

Near-capacity is normal. Enter optimization only after a confirmed hard overflow,
when a requested feature cannot fit, or when the user explicitly asks.

## Mutation guardrails

Before editing, state the exact item, source component, target Avatar, menu
destination, shared consumers, authorized operation, and required validation
layer. Recheck the Unity instance before prefab changes, Apply, refresh,
preview, or build.

After editing:

1. Wait for import/compile completion and inspect task-caused Console changes.
2. Regenerate through the provider/NDMF path.
3. Compare the source responsibility map with generated menus, parameters,
   Animator, hierarchy, armature, meshes, and toggles.
4. Run only the authorized runtime and size layers.
5. Update the toolchain profile, menu map, parameter index, provider inventory,
   clothing responsibility map, generated-source record, source footprint,
   size-evidence status, and acceptance record.

## Acceptance matrix

| Claim | Minimum evidence |
| --- | --- |
| Item is configured for the target | `UNITY_RESOLVED` exact host, source, provider, and target |
| Menu/parameter/Animator is generated | Provider preview or `NDMF_BUILT` final result |
| Armature, renderer, and toggles are correctly bound | `NDMF_BUILT` exact paths and bindings |
| Fit, clipping, motion, or visibility is correct | Named authorized runtime layer |
| Saved or synced state works | Fresh persistence test or named multiplayer test as applicable |
| Bundle size impact is acceptable | Exact authorized SDK build comparison; otherwise `NOT_MEASURED` |

Report every unrun layer explicitly. A visible source object, successful provider
preview, or clean Console is not final player proof.
