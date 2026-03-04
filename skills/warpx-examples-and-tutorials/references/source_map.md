# warpx source map: Examples and Tutorials

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "add_warpx_test|analysis|checksum" Examples/CMakeLists.txt Examples/Tests Examples/Physics_applications`
- `rg -n "def main|check_restart|get_theoretical_field" Examples/*.py Examples/Tests/*/analysis_*.py`

## Function-level entry points
- `Examples/CMakeLists.txt` | symbols: `function(add_warpx_test ...)` | check: run + analysis + checksum orchestration.
- `Examples/analysis_default_regression.py` | symbols: `main` | check: common post-run validation path.
- `Examples/analysis_default_restart.py` | symbols: `check_restart` | check: restart correctness comparison.
- `Examples/Tests/langmuir/analysis_2d.py` | symbols: `get_contribution`, `get_theoretical_field` | check: analytical comparison pattern in tests.
- `Examples/Tests/langmuir/analysis_3d.py` | symbols: `get_contribution`, `get_theoretical_field` | check: 3D analysis validation pattern.
- `Source/main.cpp` | symbols: `main` | check: executable startup path used by input-file examples.
- `Python/pywarpx/picmi.py` | symbols: PICMI classes used by Python examples | check: script option mapping behavior.

## Practical verification
```bash
# list and inspect test/example wrappers quickly
ctest --test-dir build -N
rg -n "add_warpx_test\(" Examples/Tests Examples/Physics_applications
```
