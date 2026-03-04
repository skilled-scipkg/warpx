# warpx documentation map: Simulation Workflows

Use these docs first for run lifecycle, checkpoint/restart, and validated execution patterns.

## Core run lifecycle references
- `Docs/source/usage/how_to_run.rst` | executable/PICMI launch patterns.
- `Docs/source/usage/parameters.rst` | runtime control and diagnostics parameters.
- `Docs/source/usage/workflows/domain_decomposition.rst` | decomposition controls and constraints.
- `Docs/source/usage/workflows/debugging.rst` | structured runtime debugging workflow.
- `Docs/source/usage/workflows/archiving.rst` | preserving simulation outputs.

## Test-backed workflow examples
- `Examples/Tests/langmuir/README.rst` | standard short-run workflow with analysis.
- `Examples/Tests/restart/CMakeLists.txt` | restart test matrix and checks.
- `Examples/Tests/gaussian_beam/README.rst` | electromagnetic test run flow.
- `Examples/Tests/field_ionization/README.rst` | multiphysics test run flow.

## Physics-application workflows
- `Examples/Physics_applications/plasma_acceleration/README.rst` | application-grade run pattern.
- `Examples/Physics_applications/laser_acceleration/README.rst` | laser-acceleration workflow.
- `Examples/Physics_applications/pierce_diode/README.rst` | electrostatic application workflow.
