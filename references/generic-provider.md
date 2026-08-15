# Generic provider route

Use this route for any tool, plugin, prefab system, or generator without a
dedicated public playbook. Do not present project-specific familiarity as a
general recommendation.

## Inspect generically

1. Verify official package identity, installed version, asset-declared
   dependency, target components, and current documentation.
2. Identify the editable source, scene overrides, shared assets, generated
   output, build clones, caches, and every known consumer.
3. Inventory menu, parameters, Animator, model bindings, armature, meshes,
   materials, BlendShapes, toggles, constraints, PhysBones, Contacts, audio,
   particles, defaults, and platform behavior contributed by the provider.
4. Record provider execution order and the exact preview/build artifact needed
   to establish final ownership.
5. Stop before import, Apply, regeneration, migration, deletion, build, runtime,
   or upload unless that action is explicitly authorized.

Use the provider's supported editing entry and upstream instructions. Do not
hand-edit generated output or infer compatibility from a similarly named tool.

## Report boundaries

Record unknown behavior as `SOURCE_ONLY`, `BUILD_REQUIRED`, `NOT_RUN`, or
`BLOCKED`. A detected package is not proof that the target Avatar uses it. A
provider preview is not client runtime proof.

If repeated real tasks establish stable, project-independent rules, add a public
playbook in a later Skill revision. Until then, keep the provider generic.
