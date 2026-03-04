# warpx source map: Developer Guide

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "WarpX::Evolve|WMRecordWarning|WarnManager|MoveWindow|add_warpx_test" Source Examples`
- `rg -n "warning|portability|development|contrib" Docs/source/developers CONTRIBUTING.rst`

## Function-level entry points
- `Source/Evolve/WarpXEvolve.cpp` | symbols: `WarpX::Evolve`, `checkEarlyUnusedParams` | check: main timestep orchestration and warning emission point.
- `Source/WarpX.cpp` | symbols: class-level runtime state and parameter defaults | check: core runtime behavior switches.
- `Source/Initialization/WarpXInit.cpp` | symbols: `initialize_warning_manager`, `check_dims` | check: startup warnings and dimensionality guardrails.
- `Source/ablastr/warn_manager/WarnManager.cpp` | symbols: `RecordWarning`, `PrintGlobalWarnings`, `SetAbortThreshold` | check: warning aggregation/abort policy.
- `Source/ablastr/warn_manager/WarnManager.H` | symbols: warning manager API | check: call sites and priorities.
- `Source/ablastr/utils/msg_logger/MsgLogger.cpp` | symbols: message formatting helpers | check: warning/info text formatting behavior.
- `Source/Utils/WarpXMovingWindow.cpp` | symbols: `WarpX::MoveWindow` | check: moving-window evolution path.
- `Examples/CMakeLists.txt` | symbols: `add_warpx_test` | check: how to add run/analysis/checksum regression tests.
- `Examples/analysis_default_regression.py` | symbols: `main` | check: default analysis/checksum invocation pattern.

## Practical verification
```bash
# run one targeted regression test after code changes
ctest --test-dir build -R "test_3d_langmuir_multi\..*" --output-on-failure
```
