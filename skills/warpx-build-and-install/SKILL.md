---
name: warpx-build-and-install
description: This skill should be used when users ask about build and install in warpx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# warpx: Build and Install

## High-Signal Playbook

### Route conditions
- Use this skill for dependency setup, CMake configuration, backend/dims flags, and build/install failures.
- Route Python/PICMI runtime usage to `warpx-api-and-scripting` after build is complete.
- Route simulation setup/runtime behavior to `warpx-simulation-workflows` and physics parameter choices to `warpx-inputs-and-modeling`.

### Triage questions
- Are you installing from source, conda-forge package, or Spack? (`Docs/source/install/users.rst`)
- Which backend is needed: `NOACC`, `OMP`, `CUDA`, `SYCL`, `HIP`? (`Docs/source/install/cmake.rst`)
- Which dimensions are needed: `1`, `2`, `3`, `RZ` (or multi-dim build)? (`Docs/source/install/cmake.rst`)
- Is MPI required (`WarpX_MPI=ON` / `WARPX_MPI=ON`)? (`Docs/source/install/cmake.rst`)
- Are Python bindings required (`WarpX_PYTHON=ON` + `pip_install`)? (`Docs/source/install/cmake.rst`)
- Are optional features required (`WarpX_OPENPMD`, `WarpX_FFT`, `WarpX_QED`)? (`Docs/source/install/cmake.rst`)

### Canonical workflow
1. Activate one dependency environment and avoid mixing package managers (`Docs/source/install/cmake.rst`).
2. Configure CMake with explicit dims/backend/options.
3. Build binaries and run a smoke test executable.
4. If Python is needed, configure `WarpX_PYTHON=ON` and run the `pip_install` target.
5. Keep build directories separate for app-only and Python builds.
6. If config changed materially (compiler/deps/options), re-run `cmake -S . -B <build>`.

### Minimal working example
```bash
# app build (MPI + OpenMP example)
conda activate warpx-cpu-mpich-dev
cmake -S . -B build -DWarpX_DIMS=3 -DWarpX_COMPUTE=OMP -DWarpX_MPI=ON
cmake --build build -j 8

# python bindings build/install
cmake -S . -B build_py -DWarpX_DIMS="1;2;3;RZ" -DWarpX_PYTHON=ON
cmake --build build_py -j 8 --target pip_install
# faster repeat install while developing:
cmake --build build_py -j 8 --target pip_install_nodeps
```

### Pitfalls and fixes
- `cmake`/`ctest` not found: activate `warpx-cpu-mpich-dev` first.
- MPI mismatch between environment and build: set `WarpX_MPI`/`WARPX_MPI` consistently for CMake vs pip workflows (`Docs/source/install/cmake.rst`).
- Python install fails due to permissions outside virtual env: add `-DPY_PIP_INSTALL_OPTIONS="--user"` or use a venv (`Docs/source/install/cmake.rst`).
- Slow Python link times with IPO: set `-DWarpX_PYTHON_IPO=OFF -DpyAMReX_IPO=OFF` for dev iterations.
- GPU build failure: verify driver/toolkit alignment and backend-specific dependencies (`Docs/source/install/cmake.rst`).

### Convergence and validation checks
- Confirm CMake summary matches intended `COMPUTE`, `DIMS`, `MPI`, `PYTHON`, `OPENPMD`, `FFT`, `QED`.
- Verify binaries exist under `build/bin/` with expected suffixes (e.g., `warpx.2d`, `warpx.3d`).
- Run `ctest --test-dir build -N` to ensure tests are discovered.
- Run one short example/test (e.g., Langmuir) before scaling to production.

## Primary documentation references
- `Docs/source/install/users.rst`
- `Docs/source/install/cmake.rst`
- `Docs/source/install/hpc.rst`
- `Docs/source/index.rst`
- `Docs/source/developers/faq.rst`

## Source entry points for unresolved issues
- `CMakeLists.txt`
- `cmake/WarpXFunctions.cmake`
- `cmake/dependencies/AMReX.cmake`
- `cmake/dependencies/FFT.cmake`
- `cmake/dependencies/openPMD.cmake`
- `cmake/dependencies/PICSAR.cmake`
- `Source/Python/WarpX.cpp`
- `setup.py`

## Deep references
- `references/doc_map.md`
- `references/source_map.md`
