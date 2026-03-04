# warpx source map: Getting Started

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "main\(|initialize_external_libraries|check_dims|Evolve|WriteUsedInputsFile" Source`
- `rg -n "initialize|finalize|step|evolve" Python/pywarpx`

## Function-level entry points
- `Source/main.cpp` | symbols: `main` | check: top-level startup/teardown flow.
- `Source/Initialization/WarpXInit.cpp` | symbols: `initialize_external_libraries`, `check_dims`, `initialize_warning_manager` | check: startup environment/dimension validation.
- `Source/Evolve/WarpXEvolve.cpp` | symbols: `WarpX::Evolve` | check: timestep loop behavior.
- `Source/Initialization/WarpXInitData.cpp` | symbols: `WriteUsedInputsFile` | check: run-of-record input capture.
- `Source/Diagnostics/Diagnostics.cpp` | symbols: `BaseReadParameters` | check: initial diagnostic parameter parsing.
- `Source/Diagnostics/WarpXIO.cpp` | symbols: `InitFromCheckpoint` | check: restart bootstrap path.
- `Source/Utils/WarpXVersion.cpp` | symbols: `WarpX::Version` | check: version/build identity access.
- `Python/pywarpx/_libwarpx.py` | symbols: `LibWarpX.initialize`, `LibWarpX.finalize` | check: Python runtime lifecycle.

## Practical verification
```bash
# quick startup trace points
rg -n "main\(|initialize_external_libraries|WarpX::Evolve|WriteUsedInputsFile" Source
```
