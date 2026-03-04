---
name: warpx-index
description: This skill should be used when users ask how to use warpx and the correct generated documentation skill must be selected before going deeper into source code.
---

# warpx Skills Index

## Docs-first routing rules
- Route to one topic skill first; do not jump into source code until that skill's primary docs are checked.
- Prefer test-backed examples for behavior claims.
- Escalate to source only when docs are ambiguous, outdated, or missing behavior-critical details.

## Topic skills
- `warpx-getting-started`: first install/run path, smoke tests, and onboarding.
- `warpx-build-and-install`: dependency setup, CMake/pip flows, backend+dims flags, build failures.
- `warpx-simulation-workflows`: launch lifecycle, runtime controls, checkpoint/restart.
- `warpx-inputs-and-modeling`: grid/domain/boundaries/species/laser/solver parameterization.
- `warpx-analysis-and-output`: diagnostics formats, post-processing, and regression-style validation.
- `warpx-api-and-scripting`: Python/pywarpx/PICMI scripting and callbacks.
- `warpx-parallel-hpc`: MPI/OpenMP/GPU launch, decomposition, scaling, profiling.
- `warpx-examples-and-tutorials`: worked examples and tutorial-first run patterns.
- `warpx-theory-and-methods`: algorithm/model interpretation and numerical-method choices.
- `warpx-developer-guide`: contribution workflow, architecture entry points, tests/docs expectations.
- `warpx-advanced-topics`: governance, conduct, acknowledgements, glossary, regression utilities.

## Canonical directory roots
- Docs: `Docs/source`, plus top-level docs (`CONTRIBUTING.rst`, `CODE_OF_CONDUCT.rst`, `GOVERNANCE.rst`).
- Examples/tests: `Examples/Physics_applications`, `Examples/Tests`.
- Regression utilities: `Regression`, `Examples/analysis_default_regression.py`.
- Source roots: `Source`, `Python`, `cmake`.

## Fast start route
1. Use `warpx-getting-started` to run a short Langmuir case.
2. Use `warpx-inputs-and-modeling` to adapt physics/mesh/solver parameters.
3. Use `warpx-simulation-workflows` for restart/checkpoint and production run controls.
4. Use `warpx-analysis-and-output` to validate outputs and compare observables.

## Escalation workflow
1. Read the target skill's primary documentation references.
2. If needed, inspect the target skill's doc map.
3. If still unresolved, inspect the target skill's source map and follow function-level entry points.
4. Use targeted symbol search: `rg -n "<symbol_or_keyword>" Source Python Examples Regression cmake`.
