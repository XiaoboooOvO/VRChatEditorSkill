# FaceEmo playbook

Use only when FaceEmo is selected in `TOOLCHAIN_PROFILE` and the exact package and
target configuration are present.

## Source and ownership

Trace this chain:

`target Avatar -> FaceEmo scene configuration -> editable source prefab/config ->
stable user clips and additional objects -> Apply/regeneration -> generated menu,
parameters, and FX -> NDMF merged Avatar`

- Treat the configuration or source prefab as the editing entry.
- Treat timestamped/generated controllers, menus, parameters, and backup output
  as outputs, not durable editing sources.
- Distinguish a scene-instance override from a shared prefab edit. Map every
  Avatar and clip consumer before Apply or regeneration.
- Keep custom expression clips in a stable user-owned directory.

## Expression audit

For each expression, record gesture, GestureWeight, viseme, Contact, AFK, menu,
or other condition; pattern/threshold; clip; and exact BlendShape, transform,
material, particle, audio, or object binding.

Check Blink, eye tracking, Lip Sync, mouth cancellation, transitions, layer
order, Write Defaults, and generated parameter ownership. A large facial clip
can explicitly zero many unrelated curves; copy the intended non-zero expression
rather than blindly reusing a full-face replacement clip.

## Validation

Use provider preview or NDMF output for generated menu, parameter, and FX claims.
Use a named desktop, VR, or multiplayer runtime layer for player behavior. Do not
call a static clip or FaceEmo Apply result final runtime proof.

After a change, refresh the toolchain profile, expression/provider inventory,
menu-to-function map, parameter index, generated-source record, and evidence
status. Mark replaced generated paths `STALE`.
