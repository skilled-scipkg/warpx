# warpx documentation map: API and Scripting

Use these docs first for Python/PICMI/pywarpx interfaces and callback-driven scripting.

## Core references
- `Docs/source/usage/python.rst` | PICMI Python input workflow.
- `Docs/source/developers/python.rst` | conversion of PICMI options into WarpX runtime parameters.
- `Docs/source/usage/workflows/python_warpx.rst` | global WarpX Python interface usage.
- `Docs/source/usage/workflows/python_callbacks.rst` | callback lifecycle and hook usage.
- `Docs/source/usage/workflows/python_field_data.rst` | field data access from Python.
- `Docs/source/usage/workflows/python_particle_data.rst` | particle data access from Python.
- `Docs/source/usage/workflows/python_particle_boundary_data.rst` | boundary-hit particle access patterns.
- `Docs/source/usage/workflows/python_portable.rst` | CPU/GPU-portable Python coding patterns.
- `Docs/source/dataanalysis/openpmdapi.rst` | scripted openPMD analysis.

## Examples
- `Examples/Tests/langmuir/inputs_test_2d_langmuir_multi_picmi.py` | minimal PICMI run script.
- `Examples/Physics_applications/plasma_acceleration/inputs_test_1d_plasma_acceleration_picmi.py` | physics-application PICMI example.
