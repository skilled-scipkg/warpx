# warpx documentation map: Analysis and Output

Use these docs first for diagnostics configuration, output formats, and post-processing.

## Core references
- `Docs/source/dataanalysis/formats.rst` | output format behavior, staggering caveats, async I/O notes.
- `Docs/source/dataanalysis/openpmd.rst` | reading openPMD outputs.
- `Docs/source/dataanalysis/openpmdapi.rst` | direct openPMD-api workflows.
- `Docs/source/dataanalysis/openpmdviewer.rst` | openPMD-viewer tooling.
- `Docs/source/dataanalysis/yt.rst` | loading AMReX plotfiles with yt.
- `Docs/source/dataanalysis/advanced.rst` | low-level/advanced plotfile handling.
- `Docs/source/dataanalysis/insitu.rst` | in-situ output stack (Ascent/SENSEI/Catalyst references).
- `Docs/source/developers/diagnostics.rst` | diagnostics implementation-level concepts.
- `Docs/source/usage/parameters.rst` | diagnostics parameter syntax and runtime options.

## Regression and validation references
- `Examples/analysis_default_regression.py` | default checksum-based validation entry point.
- `Examples/analysis_default_restart.py` | restart consistency checks.
- `Regression/Checksum/checksumAPI.py` | checksum API used by CI analysis scripts.
- `Regression/PostProcessingUtils/post_processing_utils.py` | shared post-processing helpers.
