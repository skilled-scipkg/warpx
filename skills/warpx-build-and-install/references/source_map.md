# warpx source map: Build and Install

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "option\(WarpX_|WarpX_DIMS|WarpX_COMPUTE|include\(.*dependencies" CMakeLists.txt`
- `rg -n "function\(|set_warpx_binary_name|warpx_print_summary|configure_mpiexec" cmake/WarpXFunctions.cmake`
- `rg -n "find_package|FetchContent|WarpX_.*internal" cmake/dependencies/*.cmake`

## Function-level entry points
- `CMakeLists.txt` | symbols: `option(WarpX_...)`, `WarpX_DIMS`, `WarpX_COMPUTE` handling | check: global build option gates.
- `cmake/WarpXFunctions.cmake` | symbols: `set_warpx_binary_name`, `configure_mpiexec`, `warpx_print_summary` | check: binary naming, MPI test launcher, config summary.
- `cmake/dependencies/AMReX.cmake` | symbols: AMReX option forwarding and `FetchContent` logic | check: backend/MPI/precision propagation.
- `cmake/dependencies/openPMD.cmake` | symbols: `find_openpmd` | check: openPMD internal/external resolution.
- `cmake/dependencies/FFT.cmake` | symbols: `fftw_check_omp`, backend-dependent FFT setup | check: FFT backend and OpenMP FFTW behavior.
- `cmake/dependencies/PICSAR.cmake` | symbols: `find_picsar` | check: QED dependency path and table-generation toggles.
- `setup.py` | symbols: `CMakeBuild.build_extension`, `CopyPreBuild.run` | check: pip-driven CMake build/install flow.
- `Source/Python/CMakeLists.txt` | symbols: pybind target wiring | check: Python module build target composition.
- `Source/Python/pyWarpX.cpp` | symbols: module init exports | check: runtime symbols available in installed Python package.

## Practical verification
```bash
# inspect final CMake config summary after configure
cmake -S . -B build -DWarpX_DIMS=3 -DWarpX_COMPUTE=OMP -DWarpX_MPI=ON
cmake --build build -j 8
```
