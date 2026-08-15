# Avatar feature routing

Use the smallest route that answers the question. Keep the exact avatar root,
scene or prefab path, requested feature, package versions, and authorization
scope in the record. Names are not unique; preserve hierarchy paths, GUIDs, and
fileIDs where they matter.

Use the evidence labels and authorization boundaries defined by the main skill
and `evidence-and-authorization.md`. A source chain can locate a feature, but it
cannot prove final reachability or player behavior when a build-time provider
participates.

## Common entry gate

1. Confirm the exact project, Unity version, active scene, target root, and
   whether the scene is dirty, compiling, or in Play Mode.
2. Classify every relevant item as a scene override, shared asset, editable
   provider source, generated output, build clone, or cache. See
   `generated-and-shared-assets.md` before changing an ownership boundary.
3. Follow the route below only through task-relevant assets. Resolve external
   references by both GUID and fileID and scene-local references by document
   anchor and prefab modification.
4. Stop at the first unsupported claim. Say `BUILD_REQUIRED`, `NOT_RUN`,
   `BLOCKED`, `STALE`, or `AMBIGUOUS_TARGET` rather than filling the gap from a
   similar avatar, old cache, or object name.

## Menu or player-visible function

Minimum read chain:

`exact root -> complete player menu path -> descriptor menu and every provider
Menu Installer/Menu Item -> control type and value -> Expression Parameter
declaration (type, default, sync, saved) -> controller/layer/state/driver ->
clip binding -> exact model object or property`

Audit the complete root page before following one leaf. Prefer a single flat
root page. Add pagination or a submenu only when the installed SDK's hard
per-page limit is actually exceeded and the required functions cannot be
balanced without obscuring their semantics. Preserve each provider's complete
menu ownership; never split or merge leaves from different plugins as an
optimization strategy. Near-capacity is normal and does not trigger an
optimization prompt.

Only when explicitly authorized and needed, escalate to provider preview or
`NDMF_BUILT` when a provider injects a menu,
when multiple menu sources merge, when menu reachability or pagination matters,
or when parameter collisions are possible. Add `CLIENT_RUNTIME` in the named
environment for actual input, visual, audio, Contact, or synchronization claims.
Use `SDK_BUILD` only for the exact authorized build or upload-preflight claim.
Otherwise record `BUILD_REQUIRED` or `NOT_RUN` and stop.

Stop if the root is missing or duplicated, a menu source cannot be assigned to
one owner, a referenced asset is unresolved, or the conclusion depends on a
generated menu that was not built. A dirty scene or shared source also stops a
mutation until the user chooses the target and recovery boundary.

Common errors: opening only the descriptor menu and missing injected items;
treating a source Menu Installer as the final menu; using names instead of full
paths; changing a shared menu for one avatar; mixing leaves from different
providers to avoid a page; prompting for optimization while within the hard
limit; and calling source reachability "works in VRChat" without runtime
evidence.

After any menu or player-function change, update the project menu tree,
menu-to-function map, parameter index, provider inventory, and evidence status.

## Facial expression or gesture

Minimum read chain:

`exact root -> FaceEmo or gesture source/config -> pattern and condition
 (gesture, weight, viseme, voice, Contact, or AFK) -> stable animation clip and
 additional object references -> Blink, eye tracking, Lip Sync, and mouth
 cancellation settings -> generated FX/menu/parameters -> merged FX state and
 exact blendshape, transform, material, or object binding`

For continuous gesture input, include the weight parameter and BlendTree
thresholds. For Contact input, include sender/receiver and lock or override
settings. Keep built-in VRChat input parameters read-only; do not invent menu
controls for them.

Only when explicitly authorized and needed, escalate when FaceEmo Apply or
regeneration is involved, when a clip or prefab
is shared by multiple groups, when a generated controller is queried, or when
Blink, Lip Sync, tracking, Contact, or gesture blending can override one
another. Use `PROVIDER_PREVIEW`/`NDMF_BUILT` for merged output and the named
`CLIENT_RUNTIME` layer for gesture, blink, mouth, eye, and network behavior.
Otherwise record `BUILD_REQUIRED`/`NOT_RUN` and stop.

Stop if the editable expression owner is unknown, a timestamped generated
folder is the only available source, a shared clip's consumers are unmapped, or
the test would require Apply in Play Mode. Do not edit generated FaceEmo
controllers or menus; change the source and regenerate.

Common errors: treating every generated `CN_*` or `EM_*` parameter as a public
expression selector; forgetting Blink/Lip Sync/eye tracking interaction;
adding a blend tree to a generated controller; assuming a gesture clip creates
new animation content; and inferring facial behavior from a static blendshape
binding alone.

## Expression parameter or conflict

Minimum read chain:

`exact root -> descriptor Expression Parameters -> every relevant provider
 parameter source (for example Modular Avatar, FaceEmo, inventory, wardrobe, or
 gesture provider) -> name/type/default/saved/sync and remapping -> provider
 introspection or source estimate -> NDMF merged list -> SDK
 expression-parameter cost`

Calculate each target root independently with the installed SDK/provider API;
do not hand-add scene components or copy a value from a structurally similar
root. A non-synced or animator-only parameter has zero sync bits but still counts
toward the parameter-entry limit. A parameter explicitly written to the
descriptor asset can be charged even when its name resembles a built-in input.

Only when explicitly authorized and needed, escalate to `PROVIDER_PREVIEW` for
provider introspection, to `NDMF_BUILT` for
deduplication, remapping, generated names, and type conflicts, and to
`SDK_BUILD` for the final cost and platform list. Use `CLIENT_RUNTIME` only when
the question is synchronization or saved-value behavior. Otherwise record
`BUILD_REQUIRED`/`NOT_RUN` and stop.

Stop if the target root is ambiguous, the same name has incompatible types, a
provider version or introspection result is unavailable, or the result is an
old source estimate. Report the estimate as provisional and leave final cost
`BUILD_REQUIRED`.

Common errors: counting parameters instead of bits; assuming non-synced means
it does not count at all; ignoring remaps and duplicate-name rules; copying
budget values across avatars; and calling a source report an upload proof.

## Clothing or provider migration

Minimum read chain:

`exact root -> old provider source and new provider source -> menu injection and
 parameter ownership -> armature/bone mapping and constraints -> mesh/renderers,
 material slots, blendshape sync, and object toggles -> PhysBones/Contacts,
 audio/particles, and saved or sync behavior -> provider preview -> NDMF clone`

A migration is complete only when every old responsibility has a new owner. Map
the old and new menu paths, parameters, Animator layers and clips, armature
paths, mesh and material assignments, blendshapes, toggles, constraints,
PhysBones, Contacts, and non-visual effects. Dressing Tools, lilycalInventory,
Modular Avatar, and other systems may each contribute different
parts of that chain.

Only when explicitly authorized and needed, escalate to provider preview before
deleting the old provider, to `NDMF_BUILT`
for merged ownership, collisions, and optimized output, and to the named
`CLIENT_RUNTIME` layer for visual, audio, PhysBone, Contact, or multiplayer
acceptance. Use `SDK_BUILD` only for an authorized build claim; otherwise record
the unrun layer and stop before destructive removal.

Stop if any responsibility has no mapped replacement, the target clothing or
provider asset is shared by unlisted consumers, two providers both claim the
same menu/parameter/Animator role, or the only evidence is an old generated
output. Do not remove the old source until the new chain is inspected and the
consumer map is updated.

Common errors: preserving a toggle but losing bone merge or blendshape sync;
assuming a wardrobe menu proves wearable behavior; deleting Dressing Tools
before validating an inventory replacement; editing an optimized clone; and
using another avatar's armature path or budget as a template.

For a newly imported feature or plugin, also record its menu contribution,
parameter delta, imported/source footprint, current build-size evidence status,
and every non-menu responsibility. Measure marginal bundle size only from
authorized comparable before/after builds; otherwise mark it `NOT_MEASURED`.
If the result is within all hard limits, report the delta and stop without an
optimization prompt.

## PhysBone or Contact

Minimum read chain:

`exact root and hierarchy path -> transform/root and active state -> PhysBone
 settings, colliders, and constraints -> Contact sender/receiver settings,
 parameter, allow-self/allow-others, and shape -> Animator/provider bindings ->
 NDMF generated components -> named runtime`

Include inactive objects, prefab additions/removals, scale and parent changes,
and exact collider or receiver references. A Contact parameter can be local or
synced; record that choice rather than inferring it from the name.

Only when explicitly authorized and needed, escalate to `UNITY_RESOLVED` when
prefab overrides or imported component fields
matter, to `NDMF_BUILT` when a provider adds, removes, or merges components, and
to `CLIENT_RUNTIME` for motion, collision, self/other filtering, timing, or
network behavior. Otherwise record the higher layer `NOT_RUN`. A static cycle
or missing reference is a diagnostic finding,
not proof of an intended runtime effect.

Stop on an ambiguous root/transform, missing collider or receiver reference,
unresolved prefab modification, circular dependency whose intent is unknown,
or a requested runtime claim without an authorized runtime layer.

Common errors: searching by component name only; ignoring inactive or removed
components; confusing a Contact sender with a receiver; ignoring self/others
filters, scale, or update order; and calling a serialized field a working
interaction.

## Material, texture, mesh, or visual animation

Minimum read chain:

`exact avatar root -> renderer or animated object path -> mesh/submesh and
material slot -> material asset/GUID and shader property -> texture GUID plus
importer/platform settings or animation binding path/property -> prefab
overrides and shared consumers -> provider/optimizer output`

Classify the update before editing: in-place texture-content replacement,
material property reassignment, isolated material/texture branch, importer-only
change, shader change, or animated visual property. Record relevant before and
after hashes, dimensions, texture type, color space, alpha, normal-map mode,
mipmaps, max size, compression, Crunch, and platform overrides. Check clips
that replace the material or animate the same property.

Preserve the complete GUID/fileID lineage. For an animation, check whether the
binding targets a local path, a prefab source path, a blendshape, a material
property, or an object active flag. For a visual claim, also check the target
platform's shader and texture import result.

Only when explicitly authorized and needed, escalate to `UNITY_RESOLVED` for
imported mesh/material semantics and prefab
overrides, to `NDMF_BUILT` when Avatar Optimizer or another provider combines,
removes, or rewrites meshes/materials, to `SDK_BUILD` for platform bundle
inclusion, and to `CLIENT_RUNTIME` for actual appearance or animation. Otherwise
record `BUILD_REQUIRED`/`NOT_RUN` and stop.

Stop if any GUID/fileID or binding path is unresolved, duplicate hierarchy names
make the path ambiguous, a shared material/clip assignment has unknown
consumers, or the only inspected asset is a generated/optimized clone.

Common errors: editing a shared material to fix one instance; changing a texture
before proving the material branch; assuming an animation clip targets a
similarly named object; ignoring platform importer overrides; and using source
file size as bundle-size evidence.

Update the visual-asset map and evidence/change record. Update menu, parameter,
or provider documents only when their chain changed. Mark previous build-size
evidence stale when included assets or import settings changed, but do not
infer final bundle delta without an exact current build.

## Size or upload readiness

Minimum read chain:

`explicitly named avatar root and platform -> current source/package/build state
 -> provider/NDMF build for that target -> SDK build artifact -> compressed
 download size and uncompressed AssetBundle size -> SDK validation -> optional
 named Build & Test/runtime -> separately authorized upload`

Read the current platform limits from the installed SDK or official docs. Both
compressed and uncompressed figures require the exact current build. Build &
Test can demonstrate a runtime path but does not replace SDK size validation.

Escalate only after the user explicitly asks for a size check or build-readiness
check, and only for the named avatar and platform. Use `SDK_BUILD` for the two
bundle measurements and keep `UPLOAD_CONFIRMED` separate. Runtime evidence is
needed only for the requested behavior, not to derive size.

Stop when no exact target is selected, a Pipeline/cache result matches multiple
avatars, the build is old or its source fingerprint is stale, the platform is
unknown, or the user did not authorize a size/build operation. Leave the result
`NOT_RUN`, `STALE`, or `AMBIGUOUS_TARGET` as appropriate.

Common errors: inferring bundle size from scenes, FBX files, textures, or project
directories; confusing compressed and uncompressed values; transferring a size
result between similar avatars; treating Build & Test as an upload-limit check;
and treating build permission as upload permission.
