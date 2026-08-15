# Avatar audit and documentation workflow

Use this reference for a newly received avatar and after any feature, plugin,
menu, parameter, controller, texture, material, mesh, audio, importer, provider,
or build-evidence change.

## Contents

- Baseline audit contract
- Menu architecture contract
- Limit and optimization policy
- Feature or plugin addition
- Visual-asset update
- End-of-task documentation gate

## Baseline audit contract

Start with the read-only toolchain gate. Record the user's selected tool roles,
installed-package evidence, missing selections, and authorized actions in a
`TOOLCHAIN_PROFILE`. Then lock the exact avatar root, scene or prefab,
Unity/SDK/provider versions, shared consumers, and evidence scope. Use the player
menu as the primary feature directory only after the profile is confirmed:

`menu path -> control/value -> parameter -> owner/provider -> controller,
driver, or generated source -> clip/binding -> exact model effect -> source
files and GUID/fileID`

Record passive systems outside the menu tree. PhysBones, automatic Contacts,
constraints, internal parameters, and build helpers do not need player menu
entries unless they expose a player control.

The first audit must create durable project-owned documents. A project may use
one consolidated report or several files, but it must cover:

1. Toolchain profile with clothing, expression, prop, preview, and optimization
   roles; selected tool, installed status, version source, and authorization.
2. Avatar identity, exact target, versions, shared boundaries, and evidence
   status.
3. Complete menu tree, every reachable player function, and every unresolved or
   build-required path.
4. Parameter index in both directions, with type, default, saved, sync mode,
   remapping, cost, owner, menu path, and consumers.
5. Provider inventory with one independent record per plugin or project-owned
   feature, including editable source, menu, parameters, Animator, generated
   output, model responsibilities, and affected avatars.
6. Visual-asset map from renderer path and material slot through material,
   shader property, texture/importer or animation binding, plus shared
   consumers and platform overrides.
7. Size evidence that distinguishes imported/source footprint, total built
   avatar size, and measured before/after build delta.
8. Evidence status and refresh triggers for every section.

Documents are routing indexes, not permanent proof. Recheck the exact target
files and cheap live facts before relying on a dated record.

## Menu architecture contract

- Prefer one flat root page. Read the installed SDK's current per-page control
  limit from its API/editor instead of hardcoding a remembered value, and keep
  important player controls directly reachable while they fit.
- Introduce pagination or a submenu only after the page actually exceeds the
  hard limit and cannot be balanced without removing or obscuring required
  function semantics.
- Preserve provider ownership. Treat a plugin's complete menu as one owned
  unit. Do not split, interleave, or merge leaves from different plugins to
  make a page fit.
- Optimize only within project-owned controls or within one plugin when that
  plugin explicitly supports the change.
- If preserving provider boundaries causes a hard overflow, accept a clear
  page or submenu instead of a cross-provider merge.
- Do not prompt the user to optimize a within-limit menu. Near-capacity is a
  normal result.

Report menu records with the full path, owner/provider, source menu or
installer, control type/value, parameter, final function, evidence layer, and
reachability status. Useful statuses include `REACHABLE`, `ORPHAN`,
`DUPLICATE_INSTALL`, `OWNER_PRESERVED`, `CROSS_PROVIDER_MERGE`, `OVER_LIMIT`,
`SOURCE_ONLY`, and `BUILD_REQUIRED`.

## Limit and optimization policy

Record actual usage and remaining capacity without interpreting proximity to a
limit as a defect. Use neutral results such as `WITHIN_LIMIT`, `AT_LIMIT`,
`OVER_LIMIT`, `NOT_MEASURED`, `BUILD_REQUIRED`, and `AMBIGUOUS_TARGET` in the
user-facing conclusion.

Do not ask whether the user wants optimization unless:

- a hard platform limit is exceeded;
- the current feature cannot be added without exceeding a hard limit; or
- the user explicitly requests optimization.

When a hard limit is exceeded, inventory costs per provider without crossing
provider ownership. Separate menu controls, synced parameter bits, Animator
and component counts, source assets, total build size, and measured marginal
build size. Do not use folder size as bundle contribution.

## Feature or plugin addition

After import or installation, always document the delta:

1. Identify the exact provider and editable source.
2. Determine whether it contributes a menu, where it is installed, how many
   controls/pages it contributes, and whether final reachability needs a build.
3. Record every added, remapped, or conflicting parameter and calculate the
   target avatar independently.
4. Record imported/source footprint and invalidate stale build-size evidence.
5. If exact before/after SDK builds are authorized and available, record both
   compressed and uncompressed deltas. Otherwise mark marginal build size
   `NOT_MEASURED`.
6. Trace its non-menu responsibilities: Animator, armature, meshes, materials,
   blendshapes, toggles, PhysBones, Contacts, audio, particles, and constraints.
7. Update the menu map, parameter index, provider inventory, size record, and
   evidence status before closing the task.

If the result remains within hard limits, report it and stop. Do not introduce
an optimization prompt.

## Visual-asset update

Use this route for textures, materials, shaders, meshes, and visual animation:

`exact avatar -> renderer path -> material slot -> material GUID -> shader and
property -> texture GUID/importer or animation binding -> shared consumers ->
provider/optimizer output`

Distinguish:

- replacing file content while preserving the texture GUID;
- assigning a different texture to a material property;
- creating an isolated material/texture branch for one avatar;
- changing only import settings or platform overrides;
- changing a shader or animated material property.

Record before/after hashes, dimensions, format/type, color space, alpha,
normal-map mode, mipmaps, max size, compression, Crunch, and platform overrides
when relevant. Map all material and avatar consumers before changing a shared
asset. Check animation clips that can replace the material or drive the same
property.

Update the visual-asset map and avatar change/evidence record. Update the menu,
parameter, or provider documents only when their chain changed. Record source
footprint and mark previous build-size evidence stale when import settings or
included visual assets changed; do not infer final bundle delta without an
exact build.

## End-of-task documentation gate

Before closing any avatar change:

1. Recheck the exact changed files, target root, ownership boundary, and
   evidence layer actually run.
2. Update every affected audit document in the same task.
3. Leave unaffected documents unchanged, but state that they were reviewed and
   why no update was required when the task could plausibly affect them.
4. Mark old measurements or generated paths `STALE` when the change invalidates
   them.
5. Record `NOT_RUN` or `BUILD_REQUIRED` instead of carrying forward an old
   higher-layer result.
6. Make the next lookup possible from the menu/function or visual-asset record
   without rescanning the entire project.
