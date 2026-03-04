# warpx documentation map: Build and Install

Use these docs first for dependency setup, CMake configuration, and Python binding installation.

## Core references
- `Docs/source/install/users.rst` | user-facing install paths (conda, spack, source).
- `Docs/source/install/cmake.rst` | canonical CMake/source build instructions and options.
- `Docs/source/install/dependencies.rst` | dependency matrix and optional components.
- `Docs/source/install/hpc.rst` | machine-specific notes and launcher patterns.
- `Docs/source/install/batch/slurm.rst` | Slurm batch template guidance.
- `Docs/source/install/batch/pbs.rst` | PBS batch template guidance.
- `Docs/source/install/batch/flux.rst` | Flux batch template guidance.
- `Docs/source/developers/how_to_compile_locally.rst` | fast local development compile loops.
- `Docs/source/developers/dimensionality.rst` | dimensionality build implications.
- `Docs/source/developers/faq.rst` | common build/runtime environment issues.

## Build/test anchors in repo
- `CMakeLists.txt` | top-level build options and dependency toggles.
- `setup.py` | Python packaging/build workflow.
- `Examples/CMakeLists.txt` | test registration (`add_warpx_test`) and run-analysis-checksum wiring.
