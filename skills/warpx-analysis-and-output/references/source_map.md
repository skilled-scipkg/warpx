# warpx source map: Analysis and Output

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "diag|checkpoint|openpmd|plotfile|WriteToFile" Source/Diagnostics`
- `rg -n "evaluate_checksum|check_restart|OpenPMDTimeSeries|yt.load" Examples Regression`

## Function-level entry points
- `Source/Diagnostics/MultiDiagnostics.cpp` | symbols: `ReadParameters`, `DoComputeAndPack`, `FilterComputePackFlush` | check: diagnostics scheduling and flush conditions.
- `Source/Diagnostics/Diagnostics.cpp` | symbols: `BaseReadParameters`, `InitDataBeforeRestart` | check: parameter parsing and restart initialization behavior.
- `Source/Diagnostics/WarpXIO.cpp` | symbols: `GetRestartDMap`, `InitFromCheckpoint` | check: restart mapping and checkpoint restore path.
- `Source/Diagnostics/FlushFormats/FlushFormatPlotfile.cpp` | symbols: `WriteToFile`, `WriteWarpXHeader` | check: plotfile output naming/content.
- `Source/Diagnostics/FlushFormats/FlushFormatOpenPMD.cpp` | symbols: `FlushFormatOpenPMD(...)`, `WriteToFile` | check: backend option parsing and openPMD writes.
- `Source/Diagnostics/FlushFormats/FlushFormatCheckpoint.cpp` | symbols: `WriteToFile` | check: checkpoint serialization of fields/particles.
- `Source/Diagnostics/WarpXOpenPMD.cpp` | symbols: `getSeriesOptions`, `name2openPMD`, `WarpXOpenPMDPlot::WarpXOpenPMDPlot` | check: openPMD metadata/series conventions.
- `Source/Diagnostics/OpenPMDHelpFunction.cpp` | symbols: `WarpXOpenPMDFileType` | check: backend/file-extension resolution.
- `Examples/analysis_default_regression.py` | symbols: `main` | check: default checksum post-processing path.
- `Regression/Checksum/checksumAPI.py` | symbols: `evaluate_checksum` | check: tolerances and benchmark comparison logic.

## Practical verification
```bash
# inspect diagnostics-related symbols quickly
rg -n "WriteToFile|DoComputeAndPack|InitFromCheckpoint" Source/Diagnostics
```
