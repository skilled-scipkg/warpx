---
name: warpx-getting-started
description: This skill should be used when users ask about getting started in warpx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# warpx: Getting Started

## High-Signal Playbook

### Route conditions
- Use this skill for first-run setup, selecting an install path, and running a first validated example.
- Route detailed build matrix questions to `warpx-build-and-install`.
- Route physics model design to `warpx-inputs-and-modeling`.
- Route post-processing/diagnostics interpretation to `warpx-analysis-and-output`.

### Triage questions
- Do you want package-manager install (`conda`/`spack`) or source build? (`Docs/source/install/users.rst`)
- Workstation or HPC system with scheduler scripts? (`Docs/source/install/hpc.rst`)
- Executable input-file run or Python PICMI run? (`Docs/source/usage/how_to_run.rst`)
- Which geometry/dimensionality is needed for first test? (`Docs/source/usage/how_to_run.rst`)
- Is the goal a quick smoke test or a physically meaningful benchmark?

### Canonical workflow
1. Pick one install route and complete dependencies.
2. Build/install WarpX (or install package).
3. Select a tested starter case (Langmuir is minimal and portable).
4. Launch with a short run (`max_step` override acceptable).
5. Confirm diagnostics output and archived `warpx_used_inputs`.
6. Expand from the starter case to physics-application examples.

### Minimal working example
```bash
# from repo root after a successful build
cd Examples/Tests/langmuir
mpirun -np 4 ../../../build/bin/warpx.2d inputs_base_2d max_step=40
```

```bash
# equivalent Python route for the same test family
cd Examples/Tests/langmuir
python3 inputs_test_2d_langmuir_multi_picmi.py
```

### Pitfalls and fixes
- Running without matching executable/input dimensions: pick `warpx.1d`, `warpx.2d`, `warpx.3d`, or `warpx.rz` that matches `geometry.dims`.
- Mixing dependency managers in one environment: use one stack per build (`Docs/source/install/cmake.rst`).
- First run too large/slow: start from `Examples/Tests` and cap with `max_step`.
- Missing reproducibility record: keep `warpx_used_inputs` with output artifacts.
- HPC launch failures: start from machine docs indexed in `Docs/source/install/hpc.rst` and the `Docs/source/install/hpc/` directory.

### Convergence and validation checks
- Simulation starts and advances without runtime aborts.
- `diags/` and `warpx_used_inputs` are produced.
- Starter example analysis scripts run successfully when provided.
- For production transitions, perform mesh/time-step scans and compare key observables.

## Primary documentation references
- `Docs/source/index.rst`
- `Docs/source/install/users.rst`
- `Docs/source/install/cmake.rst`
- `Docs/source/install/hpc.rst`
- `Docs/source/usage/how_to_run.rst`
- `Docs/source/usage/examples.rst`
- `Examples/Tests/langmuir/README.rst`

## Source entry points for unresolved issues
- `Source/main.cpp`
- `Source/WarpX.H`
- `Source/WarpX.cpp`
- `Python/pywarpx/__init__.py`
- `Source/Python/WarpX.cpp`
- `Source/Utils/WarpXVersion.cpp`
- `Source/Diagnostics/WarpXIO.cpp`
- `Source/Utils/WarpXUtil.cpp`

## Deep references
- `references/doc_map.md`
- `references/source_map.md`
