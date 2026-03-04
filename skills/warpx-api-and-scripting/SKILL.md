---
name: warpx-api-and-scripting
description: This skill should be used when users ask about api and scripting in warpx; it prioritizes documentation references and then source inspection only for unresolved details.
---

# warpx: API and Scripting

## High-Signal Playbook

### Route conditions
- Use this skill for Python/pywarpx/PICMI scripting, callback hooks, and runtime data access from Python.
- Route CMake/compilation failures for bindings to `warpx-build-and-install`.
- Route physics parameter semantics to `warpx-inputs-and-modeling`.
- Route diagnostics interpretation and output tooling to `warpx-analysis-and-output`.

### Triage questions
- Are you running a PICMI script or extending an input-file workflow with Python callbacks?
- Do you need field access, particle access, or both at runtime?
- Is this single-rank development or MPI-distributed execution?
- Do you need callback timing order guarantees (`beforestep`, `afterstep`, etc.)?
- Is the target CPU-only, GPU-enabled, or portable across both?

### Canonical workflow
1. Ensure WarpX Python bindings are installed (`WarpX_PYTHON=ON`, `pip_install`).
2. Start from an existing PICMI example and keep dimensions/solver simple first.
3. Add callbacks and verify callback execution ordering on a short run.
4. Read fields/particles through pywarpx wrappers and validate shapes/units.
5. Scale to MPI/GPU only after single-rank behavior is validated.

### Minimal working example
```bash
# run a tested PICMI script
cd Examples/Tests/langmuir
python3 inputs_test_2d_langmuir_multi_picmi.py
```

```python
from pywarpx import callbacks

@callbacks.callfromafterstep
def report_step():
    print("afterstep callback fired")
```

### Pitfalls and fixes
- Accessing `libwarpx.warpx` before initialization: initialize via `WarpX.init(...)` or `libwarpx.initialize(...)` first.
- Callback appears ignored: verify callback name matches supported hook names in `Python/pywarpx/callbacks.py`.
- Particle array confusion in RZ/3D: use geometry-aware accessors (`get_particle_r`, `get_particle_theta`) and check dimension-specific behavior.
- Mixed C++/Python environment issues: use one consistent environment for build and runtime.
- GPU portability regressions: use portable Python workflow guidance (`Docs/source/usage/workflows/python_portable.rst`).

### Convergence and validation checks
- Script runs with no callback exceptions and expected callback counts.
- Retrieved field/particle arrays have expected sizes and non-trivial values.
- For MPI runs, verify rank-dependent operations are deterministic where required.
- Compare one observable against a known test analysis baseline.

## Primary documentation references
- `Docs/source/usage/python.rst`
- `Docs/source/usage/workflows/python_warpx.rst`
- `Docs/source/usage/workflows/python_callbacks.rst`
- `Docs/source/usage/workflows/python_field_data.rst`
- `Docs/source/usage/workflows/python_particle_data.rst`
- `Docs/source/usage/workflows/python_portable.rst`
- `Docs/source/developers/python.rst`
- `Docs/source/dataanalysis/openpmdapi.rst`

## Source entry points for unresolved issues
- `Python/pywarpx/picmi.py`
- `Python/pywarpx/WarpX.py`
- `Python/pywarpx/_libwarpx.py`
- `Python/pywarpx/callbacks.py`
- `Python/pywarpx/particle_containers.py`
- `Source/Python/pyWarpX.cpp`
- `Source/Python/WarpX.cpp`
- `Source/Python/callbacks.cpp`
- `Source/Python/Particles/WarpXParticleContainer.cpp`

## Deep references
- `references/doc_map.md`
- `references/source_map.md`
