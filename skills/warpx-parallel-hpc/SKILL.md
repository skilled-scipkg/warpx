---
name: warpx-parallel-hpc
description: This skill should be used when users ask about parallel and hpc in warpx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# warpx: Parallel and HPC

## High-Signal Playbook

### Route conditions
- Use this skill for MPI/OpenMP/GPU execution, decomposition choices, scaling behavior, and scheduler launch patterns.
- Route build dependency/toolchain setup to `warpx-build-and-install`.
- Route physics model setup to `warpx-inputs-and-modeling`.
- Route diagnostics/post-processing interpretation to `warpx-analysis-and-output`.

### Triage questions
- Backend and node layout: CPU/OpenMP, CUDA, HIP, or SYCL?
- Launcher and scheduler: `mpirun`, `srun`, `flux`, PBS/LSF/PJM?
- Is domain decomposition explicit (`warpx.numprocs`) or auto-managed by AMReX?
- Are you debugging startup failures, communication overhead, or load imbalance?
- Do you need profiling output for per-step timing and load-balance diagnostics?

### Canonical workflow
1. Build with explicit backend and MPI settings.
2. Start with a small tested case and fixed rank/thread layout.
3. Validate decomposition and guard-cell communication correctness.
4. Add reduced diagnostics for load-balance/timestep duration when scaling.
5. Scale ranks/threads/GPUs incrementally and compare throughput trends.

### Minimal working example
```bash
# CPU+MPI smoke scaling case
cmake -S . -B build -DWarpX_DIMS=3 -DWarpX_COMPUTE=OMP -DWarpX_MPI=ON
cmake --build build -j 8

srun -n 4 build/bin/warpx.3d Examples/Tests/langmuir/inputs_base_3d max_step=40
```

```text
# optional explicit decomposition (product must equal MPI ranks)
warpx.numprocs = 2 2 1
```

### Pitfalls and fixes
- `warpx.numprocs` product not equal to rank count: run abort or incorrect decomposition.
- MPI thread support mismatch with async I/O: check `WarpX_MPI_THREAD_MULTIPLE` settings.
- Too many tiny boxes per rank or too few boxes: revisit `amr.max_grid_size`, blocking factor, and load-balance settings.
- Guard-cell exchange overhead dominates: inspect guard-cell requirements and solver/deposition order.
- Poor scaling with diagnostics-heavy runs: reduce diagnostic cadence for scaling studies.

### Convergence and validation checks
- Decomposition is stable (no rank-local failures) at target rank count.
- `warpx_used_inputs` records the exact parallel settings used.
- Step-time trends improve or remain flat as resources scale (for fixed global problem size, expect limits).
- Load-balance reduced diagnostics indicate no severe outliers across ranks.

## Primary documentation references
- `Docs/source/install/hpc.rst`
- `Docs/source/install/batch/slurm.rst`
- `Docs/source/install/batch/flux.rst`
- `Docs/source/install/batch/pbs.rst`
- `Docs/source/usage/how_to_run.rst`
- `Docs/source/usage/workflows/domain_decomposition.rst`
- `Docs/source/developers/how_to_profile.rst`
- `Docs/source/usage/workflows/plot_timestep_duration.rst`
- `Docs/source/usage/workflows/plot_distribution_mapping.rst`

## Source entry points for unresolved issues
- `Source/ablastr/parallelization/MPIInitHelpers.H`
- `Source/ablastr/parallelization/MPIInitHelpers.cpp`
- `Source/Parallelization/GuardCellManager.cpp`
- `Source/Parallelization/WarpXComm.cpp`
- `Source/Parallelization/WarpXSumGuardCells.cpp`
- `Source/Utils/WarpXMovingWindow.cpp`
- `Source/Evolve/WarpXComputeDt.cpp`
- `Source/Diagnostics/ReducedDiags/LoadBalanceCosts.cpp`
- `Source/Diagnostics/ReducedDiags/LoadBalanceEfficiency.cpp`

## Deep references
- `references/doc_map.md`
- `references/source_map.md`
