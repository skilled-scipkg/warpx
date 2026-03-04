# warpx source/script map: Advanced Topics

Use this map after reading `doc_map.md`.
For governance/conduct/citation questions, docs are authoritative; source inspection is mainly for regression tooling behavior.

## Fast navigation
- `rg -n "conduct|governance|acknowledge|glossary" CODE_OF_CONDUCT.rst GOVERNANCE.rst Docs/source`
- `rg -n "checksum|restart|plotfile|openpmd" Examples Regression`

## Function-level entry points
- `Examples/analysis_default_regression.py` | symbols: `main` | check: auto-detects format and calls checksum evaluation.
- `Examples/analysis_default_restart.py` | symbols: `check_restart` | check: compares restart output against benchmark plotfile data.
- `Regression/Checksum/checksumAPI.py` | symbols: `evaluate_checksum`, `reset_benchmark`, `reset_all_benchmarks` | check: benchmark compare/reset logic.
- `Regression/PostProcessingUtils/post_processing_utils.py` | symbols: `check_particle_filter`, `check_random_filter`, `check_array_sum` | check: reusable analysis assertions across tests.
- `Examples/CMakeLists.txt` | symbols: `function(add_warpx_test ...)` | check: how run/analysis/checksum steps are wired in CI-style tests.

## Practical verification
```bash
# run one regression-style post-check on existing output
python3 Examples/analysis_default_regression.py --path <diag_path>
```
