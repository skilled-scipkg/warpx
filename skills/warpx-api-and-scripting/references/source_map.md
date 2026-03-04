# warpx source map: API and Scripting

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "class |def |initialize|finalize|callback|PICMI" Python/pywarpx Source/Python`
- `rg -n "installcallback|execute_python_callback|add_python_callback" Python/pywarpx Source/Python`

## Function-level entry points
- `Python/pywarpx/picmi.py` | symbols: `Species`, `Cartesian2DGrid`, `ElectromagneticSolver`, `Simulation` classes | check: PICMI-to-WarpX option mapping.
- `Python/pywarpx/WarpX.py` | symbols: `init`, `step`, `evolve`, `finalize` | check: high-level Python runtime control.
- `Python/pywarpx/_libwarpx.py` | symbols: `LibWarpX.initialize`, `LibWarpX.finalize` | check: binding bootstrap and lifecycle.
- `Python/pywarpx/callbacks.py` | symbols: `installcallback`, `uninstallcallback`, `CallbackFunctions` | check: callback registration and dispatch.
- `Python/pywarpx/particle_containers.py` | symbols: `ParticleContainerWrapper.add_particles`, `get_particle_*` | check: runtime particle access semantics.
- `Source/Python/pyWarpX.cpp` | symbols: `amrex_init`, `amrex_finalize`, `execute_python_callback` exports | check: pybind module-level API.
- `Source/Python/WarpX.cpp` | symbols: `init_WarpX` | check: bound WarpX methods/attributes.
- `Source/Python/callbacks.cpp` | symbols: `InstallPythonCallback`, `ExecutePythonCallback`, `ClearPythonCallback` | check: C++ callback bridge.
- `Source/Python/Particles/WarpXParticleContainer.cpp` | symbols: pybind particle container wrappers | check: Python-accessible particle container behavior.

## Practical verification
```bash
# locate callback hooks and their C++ bridge
rg -n "callback|ExecutePythonCallback|installcallback" Python/pywarpx Source/Python
```
