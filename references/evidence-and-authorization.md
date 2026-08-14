# Evidence and authorization boundaries

Use this reference when a conclusion may cross from source inspection into previews, builds, runtime tests, size checks, or upload.

## Evidence matrix

| Label | What it can prove | What it cannot prove |
| --- | --- | --- |
| `STATIC_SOURCE` | Serialized references, literal values, asset identity, declared configuration | Imported semantics, prefab-instance resolution, merged output, runtime behavior |
| `UNITY_RESOLVED` | Current imported objects, component fields, active state, prefab overrides, and exact hierarchy observed through the selected Unity MCP instance | Final NDMF output or VRChat runtime behavior |
| `PROVIDER_PREVIEW` | Provider-visible source inventory or virtual/preview state | Final SDK artifact when later passes can still transform it |
| `NDMF_BUILT` | Merged/generated avatar, menu, parameters, controllers, meshes, and components after registered passes | SDK bundle limits or client behavior unless those layers were also run |
| `SDK_BUILD` | SDK validation and the exact generated bundle or final parameter asset | Desktop, VR, multiplayer, or upload behavior |
| `CLIENT_RUNTIME` | Behavior in the named test environment | Other clients, hardware modes, networking, or upload unless separately tested |
| `UPLOAD_CONFIRMED` | Observed behavior of the explicitly authorized uploaded avatar | Unobserved clients or later edits |

Use the narrowest label supported by current evidence. A newer lower-layer result does not replace an older higher-layer result, and an older higher-layer result does not prove the current source.

## Authorization matrix

| Request wording | Normally authorized | Not automatically authorized |
| --- | --- | --- |
| Inspect, explain, audit, compare, diagnose | Read files, inspect live state, perform non-mutating diagnostics | Save, Apply, import/refresh, Play Mode, build, upload |
| Fix, change, remove, migrate | Narrow source edits, affected audit-document updates, and proportional import/compile validation | Build & Test, fresh size probes/builds, publish/upload |
| Add or import a feature/plugin | Narrow installation, source edits, import/compile validation, and documentation of menu, parameters, source footprint, size-evidence status, and model responsibilities | Fresh SDK size build, Build & Test, publish/upload unless separately authorized |
| Update texture/material/shader/mesh/visual animation | Narrow asset/source edits, importer validation, shared-consumer audit, visual-map update, source-footprint record, and invalidation of stale build-size evidence | Fresh SDK size build, client visual acceptance, publish/upload unless separately authorized |
| Preview or test | The named preview/runtime layer and its normal reversible setup | Upload or unrelated project cleanup |
| Build | The named build for the exact target | Upload; destructive source changes; assuming Build & Test enforces upload limits |
| Check avatar size | Read relevant size guide, run the needed report/cache probe or exact size build for the named target | Upload or applying the result to a different avatar |
| Upload or publish | Only the exact confirmed avatar and platform after preflight | Selecting a target by guess or uploading another active descriptor |

When the requested action can overwrite unsaved scene work, modify a shared source, or affect multiple consumers beyond the named target, stop and obtain the missing decision.

## Failure and status language

- Use `PASS` only for an executed layer whose acceptance criteria were met.
- Use `NOT_RUN` when a layer was not attempted.
- Use `BUILD_REQUIRED` when source evidence cannot answer a generated-state question.
- Use `MCP_REQUIRED` when the claim or action requires Unity Editor state but no exact usable Unity MCP instance is connected.
- Use `BLOCKED` when an attempted layer could not produce reliable evidence.
- Use `STALE` for dated evidence invalidated by a refresh trigger.
- Use `AMBIGUOUS_TARGET` when a build, cache, Pipeline Manager identity, or duplicate object cannot be associated with exactly one avatar.

Name blockers precisely: unavailable or ambiguous Unity MCP instance, dirty scene, project lock, compile failure, missing Unity license, tool exception, missing completion marker, ambiguous target, or absent authorization.

## Claim examples

Good:

- `UNITY_RESOLVED`: The selected avatar instance contains the component and its referenced controller resolves to this asset.
- `PROVIDER_PREVIEW`: The parameter provider estimates 228 bits; final SDK cost is `NOT_RUN`.
- `NDMF_BUILT`: The generated menu contains the item; desktop, VR, and multiplayer behavior are `NOT_RUN`.
- `SDK_BUILD`: The named PC avatar build is below both bundle limits; upload is `NOT_RUN`.

Avoid:

- "The feature works in VRChat" from YAML or an Animator clip.
- "The avatar is under the size limit" from project asset sizes or an ambiguous old cache.
- "All similar avatars have the same parameter cost" from hierarchy similarity.
- "Upload passed" when only Build & Test or a local preview ran.
