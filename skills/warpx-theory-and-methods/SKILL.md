---
name: warpx-theory-and-methods
description: This skill should be used when users ask about theory and methods in warpx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# warpx: Theory and Methods

## High-Signal Playbook

### Route conditions
- Use this skill for method selection and interpretation: FDTD vs PSATD vs electrostatic/implicit/hybrid formulations, particle pusher choices, and model assumptions.
- Route concrete run setup to `warpx-inputs-and-modeling`.
- Route launch/restart/runtime control to `warpx-simulation-workflows`.
- Route diagnostics/post-processing questions to `warpx-analysis-and-output`.

### Triage questions
- Which equations/model family is required: electromagnetic, electrostatic, implicit EM, or hybrid PIC?
- Is the method question about stability, accuracy, or performance tradeoffs?
- Are boosted-frame, AMR, or multiphysics effects required?
- Which particle pusher/deposition/gathering behavior is under scrutiny?

### Canonical workflow
1. Anchor interpretation in the relevant theory docs.
2. Map the method to the corresponding implementation file and function.
3. Build a minimal test case that isolates the claimed behavior.
4. Validate against known analytical/benchmark expectations.
5. Only then tune performance options.

### Minimal working example
```bash
# compare numerical behavior on a short, known test
cd Examples/Tests/langmuir
mpirun -np 4 ../../../build/bin/warpx.2d inputs_test_2d_langmuir_multi max_step=80
python3 analysis_2d.py
```

### Pitfalls and fixes
- Treating theory docs as runtime defaults: confirm active solver/pusher in actual input/CMake config.
- Comparing methods without consistent resolution/timestep: match numerical settings first.
- Inferring implementation details without checking source function paths.
- Drawing conclusions from one short run only: run controlled scans.

### Convergence and validation checks
- Observable trends remain consistent under mesh/timestep refinement.
- Method-specific constraints (stability/BC assumptions) are respected.
- Cross-method comparisons use matched physics and diagnostics.
- At least one regression-backed example supports the interpretation.

## Primary documentation references
- `Docs/source/theory/intro.rst`
- `Docs/source/theory/models_algorithms/electromagnetic_pic.rst`
- `Docs/source/theory/models_algorithms/explicit_em_pic.rst`
- `Docs/source/theory/models_algorithms/electrostatic_pic.rst`
- `Docs/source/theory/models_algorithms/implicit_em_pic.rst`
- `Docs/source/theory/models_algorithms/kinetic_fluid_hybrid_model.rst`
- `Docs/source/theory/kinetic_particles.rst`
- `Docs/source/theory/boosted_frame.rst`
- `Docs/source/theory/amr.rst`
- `Docs/source/theory/multiphysics_extensions.rst`

## Source entry points for unresolved issues
- `Source/FieldSolver/FiniteDifferenceSolver/EvolveE.cpp`
- `Source/FieldSolver/FiniteDifferenceSolver/EvolveB.cpp`
- `Source/FieldSolver/SpectralSolver/SpectralSolver.cpp`
- `Source/FieldSolver/SpectralSolver/SpectralSolverRZ.cpp`
- `Source/FieldSolver/FiniteDifferenceSolver/HybridPICModel/HybridPICModel.cpp`
- `Source/Particles/Pusher/PushSelector.H`
- `Source/Particles/Pusher/UpdateMomentumBoris.H`
- `Source/Particles/Pusher/UpdateMomentumVay.H`
- `Source/Particles/Deposition/CurrentDeposition.H`
- `Source/Particles/Gather/FieldGather.H`

## Deep references
- `references/doc_map.md`
- `references/source_map.md`
