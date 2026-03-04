---
name: warpx-simulation-workflows
description: This skill should be used when users ask about simulation workflows in warpx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# warpx: Simulation Workflows

## High-Signal Playbook

### Route conditions
- Use this skill for input-file/PICMI run lifecycle, launch patterns, restarts/checkpoints, and runtime controls.
- Route build/toolchain issues to `warpx-build-and-install`.
- Route physics parameter design to `warpx-inputs-and-modeling`.
- Route output interpretation/post-processing to `warpx-analysis-and-output`.

### Triage questions
- Executable inputs file or Python PICMI script? (`Docs/source/usage/how_to_run.rst`)
- New run or restart from checkpoint (`amr.restart`)? (`Docs/source/usage/parameters.rst`)
- What dimensional executable is being used (`warpx.1d`, `warpx.2d`, `warpx.3d`, `warpx.rz`)? (`Docs/source/usage/how_to_run.rst`)
- Which launch mode is needed: `mpirun`, `srun`, or scheduler script? (`Docs/source/usage/how_to_run.rst`)
- Are diagnostics/checkpoint outputs configured before launch? (`Docs/source/usage/parameters.rst`)
- Is domain decomposition explicit (`warpx.numprocs`) or AMReX-managed (`amr.max_grid_size`/`blocking_factor`)? (`Docs/source/usage/workflows/domain_decomposition.rst`)

### Canonical workflow
1. Start from a known example/test case (`Examples/Tests` or `Examples/Physics_applications`).
2. Copy executable and input/script into a clean run directory.
3. Launch with MPI or scheduler script.
4. Verify `warpx_used_inputs` and diagnostics directories are produced.
5. Enable checkpoint diagnostics for restart-capable runs.
6. Restart by setting `amr.restart=<chk_path>`.
7. Compare fresh vs restarted behavior with regression analysis scripts.

### Minimal working example
```bash
# fresh run (input-file workflow)
mkdir -p run_langmuir && cd run_langmuir
cp ../build/bin/warpx.2d ./warpx
cp ../Examples/Tests/langmuir/inputs_base_2d .
mpirun -np 4 ./warpx inputs_base_2d max_step=80
```

```text
# checkpoint + restart parameters
# in original run input:
diagnostics.diags_names = diag1 chk
chk.diag_type = Full
chk.format = checkpoint
chk.intervals = 10

# in restart run input or CLI override:
amr.restart = "./diags/chk000010"
warpx.write_diagnostics_on_restart = 1
```

### Pitfalls and fixes
- Restart fails: checkpoint path missing/invalid; `amr.restart` requires a valid checkpoint directory (`Docs/source/usage/parameters.rst`).
- No checkpoint generated: diagnostic format not set to `checkpoint`.
- Wrong executable dimensionality for the input deck: use matching `warpx.<dim>` binary.
- `warpx.numprocs` mismatch with MPI ranks: product must equal rank count (`Docs/source/usage/workflows/domain_decomposition.rst`).
- Output confusion after command-line overrides: rely on `warpx_used_inputs` as run-of-record (`Docs/source/usage/how_to_run.rst`).

### Convergence and validation checks
- Confirm `warpx_used_inputs` exists and includes any CLI overrides.
- Confirm expected diagnostics/checkpoints appear in `diags/`.
- For restart workflows, run `Examples/analysis_default_restart.py` when available.
- Perform resolution/time-step scans for production studies, not single-run acceptance.

## Primary documentation references
- `Docs/source/usage/how_to_run.rst`
- `Docs/source/usage/parameters.rst`
- `Docs/source/usage/workflows/domain_decomposition.rst`
- `Examples/Tests/langmuir/README.rst`
- `Examples/Tests/restart/CMakeLists.txt`

## Source entry points for unresolved issues
- `Source/main.cpp`
- `Source/WarpX.cpp`
- `Source/Evolve/WarpXEvolve.cpp`
- `Source/Evolve/WarpXComputeDt.cpp`
- `Source/Diagnostics/WarpXIO.cpp`
- `Source/Diagnostics/Diagnostics.cpp`
- `Source/Diagnostics/FlushFormats/FlushFormatCheckpoint.cpp`
- `Source/Diagnostics/MultiDiagnostics.cpp`

## Deep references
- `references/doc_map.md`
- `references/source_map.md`
