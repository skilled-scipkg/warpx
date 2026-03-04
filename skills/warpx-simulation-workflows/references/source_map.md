# warpx source map: Simulation Workflows

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "main\(|WarpX::Evolve|ComputeDt|InitFromCheckpoint|WriteToFile|WriteUsedInputsFile" Source`
- `rg -n "step\(|evolve\(|check_restart" Python/pywarpx Examples`

## Function-level entry points
- `Source/main.cpp` | symbols: `main` | check: executable startup and finalization order.
- `Source/Evolve/WarpXEvolve.cpp` | symbols: `WarpX::Evolve` | check: step loop, diagnostics triggers, end-of-run conditions.
- `Source/Evolve/WarpXComputeDt.cpp` | symbols: `WarpX::ComputeDt`, `WarpX::UpdateDtFromParticleSpeeds` | check: runtime dt control path.
- `Source/Diagnostics/MultiDiagnostics.cpp` | symbols: `DoComputeAndPack`, `FilterComputePackFlush` | check: when diagnostics are computed/flushed.
- `Source/Diagnostics/WarpXIO.cpp` | symbols: `InitFromCheckpoint`, `GetRestartDMap` | check: restart read path and DMap behavior.
- `Source/Diagnostics/FlushFormats/FlushFormatCheckpoint.cpp` | symbols: `WriteToFile` | check: checkpoint write semantics.
- `Source/Initialization/WarpXInitData.cpp` | symbols: `WriteUsedInputsFile` | check: persisted effective inputs after overrides.
- `Python/pywarpx/WarpX.py` | symbols: `step`, `evolve`, `finalize` | check: Python workflow runtime control.
- `Examples/analysis_default_restart.py` | symbols: `check_restart` | check: restart output equivalence validation.

## Practical verification
```bash
# inspect run/restart control points
rg -n "WarpX::Evolve|InitFromCheckpoint|WriteToFile|WriteUsedInputsFile" Source
```
