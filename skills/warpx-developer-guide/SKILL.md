---
name: warpx-developer-guide
description: This skill should be used when users ask about developer guide in warpx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# warpx: Developer Guide

## High-Signal Playbook

### Route conditions
- Use this skill for contribution workflow, architecture entry points, coding conventions, and test/doc integration for code changes.
- Route end-user run setup to `warpx-simulation-workflows`.
- Route build environment/toolchain details to `warpx-build-and-install`.
- Route diagnostics interpretation to `warpx-analysis-and-output`.

### Triage questions
- Is this a bug fix, feature, refactor, or portability work?
- Which subsystem is touched (fields, particles, diagnostics, Python bindings, boundary conditions)?
- Does the change add/modify runtime parameters (thus requiring docs updates)?
- What minimal regression test can protect the behavior?
- Does the change affect GPU/MPI/OpenMP behavior?

### Canonical workflow
1. Create a branch from up-to-date `development` (`CONTRIBUTING.rst`).
2. Implement focused changes with WarpX style conventions.
3. Build locally and run targeted tests first (`ctest -R ...`).
4. Add/adjust regression test coverage (`add_warpx_test`, checksum flow).
5. Update docs when user-facing behavior changes.
6. Run formatting/lint hooks and submit a small, descriptive PR.

### Minimal working example
```bash
git checkout development
git pull mainline development
git checkout -b fix-<topic>

# after coding
ctest --test-dir build -R "test_3d_langmuir_multi\..*" --output-on-failure
```

```cpp
// warning logger usage for grouped runtime warnings
ablastr::warn_manager::WMRecordWarning(
    "Particles",
    "Both mass and species_type were set; explicit mass takes precedence.",
    ablastr::warn_manager::WarnPriority::medium);
```

### Pitfalls and fixes
- Large PRs slow review and increase regression risk: split by feature/fix (`CONTRIBUTING.rst`).
- Code changes without tests/docs: include both in the same PR.
- Style-only changes mixed with behavior changes: separate them (`CONTRIBUTING.rst`).
- Runtime warning behavior unclear in parallel: use warning logger instead of ad-hoc prints (`Docs/source/developers/warning_logger.rst`).
- New params undocumented: update docs under `Docs/source/usage/` or relevant developer sections.

### Convergence and validation checks
- Targeted tests pass locally for touched components.
- At least one integration/regression test guards the new behavior.
- Documentation compiles and reflects new user-facing options.
- For performance-sensitive changes, compare before/after timings on a representative case.

## Primary documentation references
- `CONTRIBUTING.rst`
- `Docs/source/developers/developers.rst`
- `Docs/source/developers/warning_logger.rst`
- `Docs/source/developers/portability.rst`
- `Docs/source/developers/moving_window.rst`

## Source entry points for unresolved issues
- `Source/WarpX.cpp`
- `Source/Evolve/WarpXEvolve.cpp`
- `Source/ablastr/warn_manager/WarnManager.H`
- `Source/ablastr/warn_manager/WarnManager.cpp`
- `Source/ablastr/utils/msg_logger/MsgLogger.H`
- `Source/Utils/WarpXMovingWindow.cpp`
- `Examples/Tests/restart/CMakeLists.txt`
- `Examples/analysis_default_regression.py`

## Deep references
- `references/doc_map.md`
- `references/source_map.md`
