---
name: warpx-analysis-and-output
description: This skill should be used when users ask about analysis and output in warpx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# warpx: Analysis and Output

## High-Signal Playbook

### Route conditions
- Use this skill for diagnostics configuration, output formats, and post-processing/validation flows.
- Route run-launch/restart orchestration to `warpx-simulation-workflows`.
- Route physics model setup to `warpx-inputs-and-modeling`.
- Route build-time I/O dependency issues (openPMD/ascent/sensei) to `warpx-build-and-install`.

### Triage questions
- Which output type is needed: `plotfile`, `openpmd`, `checkpoint`, reduced diagnostics?
- Is this offline post-processing or in-situ workflow (`ascent`/`sensei`/`catalyst`)?
- Are you validating a regression test or doing exploratory analysis?
- Which toolchain is intended: `yt`, `openpmd-viewer`, `openPMD-api`, custom scripts?
- Do you need particle outputs, field outputs, or both?

### Canonical workflow
1. Define diagnostics in the input deck (`diagnostics.diags_names`, intervals, format).
2. Run a short case to confirm output directories and file format.
3. Load plotfiles with `yt` or openPMD with `openpmd-viewer`/`openPMD-api`.
4. For CI-like validation, run default regression analysis scripts/checksum tools.
5. Interpret quantities with staggering awareness before comparing time slices.

### Minimal working example
```text
diagnostics.diags_names = diag1
diag1.diag_type = Full
diag1.format = plotfile
diag1.intervals = 10
diag1.fields_to_plot = Ex Ey Ez Bx By Bz rho
```

```python
import yt

ds = yt.load("./diags/plotfiles/plt00000/")
print(ds.field_list)
```

```bash
# regression-style checksum (run from a test output directory)
python ../../../Examples/analysis_default_regression.py --path diags/diag1000010
```

### Pitfalls and fixes
- Comparing mixed-time quantities naively: account for temporal staggering (`Docs/source/dataanalysis/formats.rst`).
- Expecting checkpoint from non-checkpoint format: set `<diag_name>.format = checkpoint`.
- openPMD backend confusion: choose backend (`bp5`, `bp4`, `h5`, `json`) consistent with runtime and rank count (`Docs/source/usage/parameters.rst`).
- Asynchronous plotfile I/O on many ranks without MPI thread support: enable `WarpX_MPI_THREAD_MULTIPLE` when needed (`Docs/source/dataanalysis/formats.rst`).
- `json` openPMD backend used in parallel runs: keep it to serial/debug usage.

### Convergence and validation checks
- Verify outputs load cleanly (`yt.load` or `OpenPMDTimeSeries`).
- Confirm diagnostics cadence and last-step dump behavior match intent.
- Cross-check selected observables using reduced diagnostics where possible.
- For regression workflows, run checksum scripts and compare against expected tolerances.

## Primary documentation references
- `Docs/source/dataanalysis/formats.rst`
- `Docs/source/dataanalysis/openpmd.rst`
- `Docs/source/dataanalysis/yt.rst`
- `Docs/source/dataanalysis/advanced.rst`
- `Docs/source/dataanalysis/insitu.rst`
- `Docs/source/usage/parameters.rst`
- `Examples/analysis_default_regression.py`

## Source entry points for unresolved issues
- `Source/Diagnostics/Diagnostics.cpp`
- `Source/Diagnostics/WarpXIO.cpp`
- `Source/Diagnostics/FlushFormats/FlushFormatPlotfile.cpp`
- `Source/Diagnostics/FlushFormats/FlushFormatOpenPMD.cpp`
- `Source/Diagnostics/FlushFormats/FlushFormatCheckpoint.cpp`
- `Source/Diagnostics/WarpXOpenPMD.cpp`
- `Regression/PostProcessingUtils/post_processing_utils.py`
- `Regression/Checksum/checksumAPI.py`

## Deep references
- `references/doc_map.md`
- `references/source_map.md`
