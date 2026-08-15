# FaceEmo playbook

Use only when FaceEmo is selected in `TOOLCHAIN_PROFILE` and the exact installed
package, target Avatar, and target configuration are present. Discover the
installed version's actual fields and generated paths through Unity MCP; do not
copy another project's Launcher target, prefab GUID, clip path, or generated
directory.

## Establish source and generated ownership

Trace and record this chain before diagnosing or changing an expression:

```text
exact target Avatar
-> FaceEmo scene configuration or Launcher target
-> editable source prefab/configuration
-> stable user clips and additional objects
-> provider Apply or regeneration
-> generated menu, parameters, and FX
-> NDMF merged Avatar
-> named runtime behavior
```

Treat the configuration or source prefab as the editing entry. Treat timestamped
controllers, menus, parameters, backups, previews, and build clones as generated
outputs unless the installed provider explicitly documents otherwise. Keep
custom clips in a stable user-owned directory that regeneration will not replace.

Before Apply or regeneration, record:

- exact Avatar hierarchy path and descriptor;
- configuration/Launcher component and direct target reference;
- editable prefab/config asset and whether the scene instance has overrides;
- current generated directory and assets referenced by the Avatar;
- every Avatar sharing the source prefab, controller, menu, parameters, or clip;
- package version, scene dirty state, Console baseline, and authorized action.

Do not use a blank target-path string as proof that no Avatar is assigned. The
provider may use an object reference or another version-specific target field.

## Build an expression responsibility record

For each expression or facial feature, record:

```text
display name and player entry
-> gesture, GestureWeight, viseme, Contact, AFK, menu, or other condition
-> pattern, threshold, and transition rules
-> stable source clip or generated motion
-> exact BlendShape, transform, material, particle, audio, or object bindings
-> Blink, eye tracking, Lip Sync, and mouth-cancellation interaction
-> generated layer/state and final NDMF ownership
```

List every curve in a task-relevant clip, including curves with a zero value. A
full-face clip can reset unrelated eyes, mouth, ears, tail, materials, or props
even when only one visible expression appears intentional.

## Read-only inspection sequence

1. Lock the target Avatar and exact Unity MCP instance.
2. Resolve the active FaceEmo configuration and its editable source.
3. Inventory expression definitions, conditions, source clips, additional
   objects, and direct/shared consumers.
4. Inspect Blink, eye tracking, Lip Sync, gesture, viseme, Contact, AFK, and menu
   ownership for overlapping bindings or conditions.
5. Inspect the current generated menu, parameters, and FX only as output evidence.
6. Compare provider preview or NDMF output with the source responsibility record.
7. Identify the first layer where the intended chain diverges.

Without authorized preview/build, stop below the generated conclusion and mark
it `BUILD_REQUIRED` or `NOT_RUN`.

## Common task: add or edit one expression

1. Snapshot the current source configuration, generated references, and all
   shared consumers.
2. Choose the exact expression entry and condition. Do not reuse another entry
   merely because the visible face looks similar.
3. Edit or create a stable source clip. Include only intended bindings; review
   every inherited or copied zero curve.
4. Check the expression against Blink, eye tracking, Lip Sync, mouth
   cancellation, gesture weight, layer order, masks, transitions, and Write
   Defaults.
5. Apply or regenerate only through the provider-supported path after the target
   and shared impact are confirmed.
6. Inspect the new generated menu, parameter, layer/state, motion, and exact
   model bindings.
7. Run the authorized preview/runtime layer for the behavior being claimed.

Do not copy a full generated state or timestamped clip into a user source folder
as a shortcut. Rebuild the intended expression from stable source bindings.

## Common task: gesture or menu expression does not trigger

Check in this order:

1. Confirm the player entry or gesture pattern and the expected parameter value.
2. Confirm GestureWeight thresholds, transition conditions, and left/right or
   combined gesture semantics.
3. Confirm the generated parameter type/default and the final FX consumer.
4. Inspect state transitions, interruption, layer weight, masks, Write Defaults,
   and higher-priority states that can immediately replace the expression.
5. Resolve every clip binding path against the built Avatar hierarchy.
6. Check whether another expression owner or custom FX layer writes the same
   BlendShape, transform, material, or object.

Fix the editable condition, clip, or source configuration. Do not patch the
generated controller; regeneration would erase that change.

## Common task: Blink, Lip Sync, or eye tracking breaks

Inventory the exact overlapping curves first. Separate these failure classes:

- expression clip explicitly writes eye or mouth curves;
- cancellation or protection settings are missing or too broad;
- a transition or Write Defaults state resets the curve;
- another provider or custom FX layer has later ownership;
- a copied full-face clip contains unintended zero curves;
- the built binding path no longer resolves after hierarchy remapping.

Change the smallest stable source that owns the conflict. Preserve intentional
asymmetry and non-face bindings. Validate Blink, Lip Sync, and eye tracking
independently; one passing behavior does not prove the other two.

## Common task: wrong Avatar, shared prefab, or cross-avatar contamination

Resolve target object references, source prefab GUID, scene overrides, and every
consumer before Apply. If multiple Avatars share the source, decide explicitly
whether the edit is shared or isolated. Prefer an Avatar-specific source prefab
or stable clip when only one target should change.

After regeneration, verify that unrelated Avatars retain their previous source
references and generated ownership. Do not compare by hierarchy similarity or
copy another Avatar's target path.

## Common task: generated assets are missing, stale, or duplicated

1. Confirm the exact provider configuration and currently referenced generated
   assets.
2. Confirm package import/compile state and isolate unrelated Console errors.
3. Check whether generation completed and whether the Avatar now references the
   new output rather than an older timestamped directory.
4. Inspect duplicate configurations, stale scene overrides, shared source
   prefabs, and provider ordering.
5. Regenerate through the supported path only after the source and target are
   proven.

Mark replaced generated paths `STALE`; do not delete them unless cleanup is
explicitly authorized and every consumer has been mapped.

## Mutation guardrails

Before editing, state the exact expression, source asset, target Avatar, shared
consumers, authorized operation, and validation layer. Keep one Unity owner for
Apply, import, compilation, preview, and build. Recheck the target immediately
before Apply or regeneration.

After editing:

1. Wait for import/compile completion and inspect task-caused Console changes.
2. Inspect the generated menu, parameters, FX layer/state, motion, and bindings.
3. Compare the new output with the pre-change responsibility record.
4. Validate only the authorized runtime layers.
5. Refresh the toolchain profile, expression/provider inventory,
   menu-to-function map, parameter index, generated-source record, visual map,
   and evidence status.

## Acceptance matrix

| Claim | Minimum evidence |
| --- | --- |
| Source expression is configured | `UNITY_RESOLVED` exact configuration, condition, clip, and target |
| Generated menu/parameter/FX contains the expression | Provider preview or `NDMF_BUILT` generated output |
| Clip binds to the intended model properties | Resolved built bindings, not clip names alone |
| Blink, Lip Sync, or eye tracking is preserved | Named preview/runtime test for each claimed behavior |
| Expression works for players | Named desktop, VR, or multiplayer layer as appropriate |

Do not call a static clip, successful Apply, clean Console, or generated
controller final runtime proof. Report unrun layers explicitly.
