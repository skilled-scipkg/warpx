---
name: warpx-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in warpx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# warpx: Inputs and Modeling

## High-Signal Playbook

### Route conditions
- Use this skill for domain/grid/boundary setup, species/laser definitions, solver and numerical-physics parameterization.
- Route launch/restart mechanics to `warpx-simulation-workflows`.
- Route build flags and optional dependency enablement to `warpx-build-and-install`.
- Route diagnostic interpretation to `warpx-analysis-and-output`.

### Triage questions
- What geometry/dimensions and physical box are required (`geometry.dims`, `geometry.prob_lo/hi`)?
- What mesh/decomposition is intended (`amr.n_cell`, `amr.max_grid_size`, `amr.blocking_factor`, optional `warpx.numprocs`)?
- Which field solver is required (`yee`, `ckc`, `psatd`, `hybrid`, electrostatic variants)?
- Which field and particle boundary conditions are physically valid for the case?
- Which species are present and how are they injected (`injection_style`, density/momentum models)?
- Are lasers/external fields/boosted-frame parameters needed?

### Canonical workflow
1. Define `geometry.*` and `amr.*` first.
2. Set consistent field/particle boundary conditions.
3. Choose solver and time-step controls (`warpx.cfl`, solver-specific knobs).
4. Define species list and per-species injection, charge, mass, density, momentum model.
5. Add laser(s) or external fields if needed.
6. Add diagnostics and run a short sanity case before long runs.
7. Iterate with convergence scans (resolution + timestep + particles-per-cell).

### Minimal working example
```text
max_step = 80
amr.n_cell = 128 128
amr.max_grid_size = 64
geometry.dims = 2
geometry.prob_lo = -20.e-6 -20.e-6
geometry.prob_hi =  20.e-6  20.e-6
boundary.field_lo = periodic periodic
boundary.field_hi = periodic periodic
warpx.cfl = 1.0

particles.species_names = electrons positrons
electrons.species_type = electron
electrons.injection_style = "NUniformPerCell"
electrons.num_particles_per_cell_each_dim = 2 2
electrons.profile = constant
electrons.density = 2.e24
```

### Pitfalls and fixes
- Domain decomposition invalid: `warpx.numprocs` product must equal MPI ranks; otherwise use AMReX decomposition (`Docs/source/usage/workflows/domain_decomposition.rst`).
- Unphysical BC combinations: periodic fields require paired periodic boundaries; solver-specific BC constraints apply (`Docs/source/usage/parameters.rst`, `Docs/source/theory/boundary_conditions.rst`).
- PSATD convergence assumptions misapplied: exact energy convergence caveat depends on single-box FFT setup (`Docs/source/usage/parameters.rst`).
- Density parser near-zero regions causing null-weight particles: use density thresholds (e.g., `density_min`) where supported (`Docs/source/usage/parameters.rst`).
- Stability/performance mismatch: re-tune `warpx.cfl`, guard cells, and particles-per-cell via scans.

### Convergence and validation checks
- Mesh/time-step refinement scan: increase `amr.n_cell`, decrease effective `dt` (via CFL or explicit dt controls).
- Particle statistics scan: increase particles-per-cell until key observables stabilize.
- Charge/field sanity: monitor diagnostics for divergence and conservation trends.
- Benchmark against a nearby tested case (`Examples/Tests` or a physics application README).

## Primary documentation references
- `Docs/source/usage/parameters.rst`
- `Docs/source/usage/how_to_run.rst`
- `Docs/source/usage/workflows/domain_decomposition.rst`
- `Docs/source/theory/boundary_conditions.rst`
- `Docs/source/usage/faq.rst`
- `Examples/Tests/langmuir/inputs_base_2d`
- `Examples/Physics_applications/pierce_diode/README.rst`

## Source entry points for unresolved issues
- `Source/Initialization/WarpXInit.cpp`
- `Source/Initialization/WarpXInitData.cpp`
- `Source/Initialization/PlasmaInjector.cpp`
- `Source/BoundaryConditions/WarpXFieldBoundaries.cpp`
- `Source/FieldSolver/WarpXPushFieldsEM.cpp`
- `Source/FieldSolver/WarpXSolveFieldsES.cpp`
- `Source/Laser/LaserProfiles.H`
- `Source/Particles/MultiParticleContainer.cpp`

## Deep references
- `references/doc_map.md`
- `references/source_map.md`
