---
name: warpx-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in warpx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# warpx: Examples and Tutorials

## High-Signal Playbook

### Route conditions
- Use this skill for selecting, running, and adapting existing WarpX examples/tests.
- Route low-level parameter semantics to `warpx-inputs-and-modeling`.
- Route launch/restart mechanics to `warpx-simulation-workflows`.
- Route analysis/output tooling questions to `warpx-analysis-and-output`.

### Triage questions
- Is the goal a minimal regression-backed example or a physics application showcase?
- Do you need input-file (`warpx.<dim> inputs_*`) or PICMI Python script workflows?
- What dimension/backends are required for the first runnable case?
- Is quick validation enough, or do you need benchmark-style analysis plots/checksums?

### Canonical workflow
1. Pick a nearby example with README + analysis script.
2. Run the smallest variant first (few steps).
3. Execute provided analysis/checksum script.
4. Modify one parameter at a time and re-validate.
5. Promote to larger physics applications after baseline behavior is stable.

### Minimal working example
```bash
# regression-backed starter case
cd Examples/Tests/langmuir
mpirun -np 4 ../../../build/bin/warpx.2d inputs_base_2d max_step=40
python3 ../../../Examples/analysis_default_regression.py --path diags/diag1000040
```

### Pitfalls and fixes
- Copying an example without its analysis script: keep analysis/checksum companion files in the run workflow.
- Choosing an example requiring unavailable optional features (e.g., QED/openPMD): verify build options first.
- Jumping straight to large production settings: keep `max_step` short while validating changes.
- Interpreting failed checksums as guaranteed physics regression: first rule out platform/library differences.

### Convergence and validation checks
- Example run completes and writes expected `diags/` outputs.
- Default or example-specific analysis script passes.
- After edits, key observable trends remain consistent with baseline.
- For new studies, perform resolution/time-step scans before claiming physical conclusions.

## Primary documentation references
- `Docs/source/tutorials.rst`
- `Docs/source/usage/examples.rst`
- `Docs/source/usage/workflows.rst`
- `Docs/source/dataanalysis/paraview.rst`
- `Examples/Tests/langmuir/README.rst`
- `Examples/Tests/restart/CMakeLists.txt`
- `Examples/Physics_applications/plasma_acceleration/README.rst`
- `Examples/Physics_applications/pierce_diode/README.rst`

## Source entry points for unresolved issues
- `Examples/CMakeLists.txt`
- `Examples/analysis_default_regression.py`
- `Examples/analysis_default_restart.py`
- `Examples/Tests/langmuir/analysis_2d.py`
- `Examples/Tests/langmuir/analysis_3d.py`
- `Source/main.cpp`
- `Source/WarpX.cpp`
- `Python/pywarpx/picmi.py`

## Deep references
- `references/doc_map.md`
- `references/source_map.md`
