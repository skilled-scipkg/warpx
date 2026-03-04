# warpx source map: Inputs and Modeling

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "queryWithParser|getWithParser|injection_style|boundary|solver|ComputeSpaceChargeField" Source`
- `rg -n "class .*Grid|class .*Solver|class Species" Python/pywarpx/picmi.py`

## Function-level entry points
- `Source/Initialization/WarpXInitData.cpp` | symbols: `CheckGuardCells`, `PostProcessBaseGrids`, `WriteUsedInputsFile` | check: mesh/decomposition guards and run-input persistence.
- `Source/Initialization/PlasmaInjector.cpp` | symbols: `PlasmaInjector::PlasmaInjector`, `setupSingleParticle` | check: species injection-style parsing and bounds behavior.
- `Source/Particles/MultiParticleContainer.cpp` | symbols: `ReadParameters` | check: species/global particle configuration parsing.
- `Source/Particles/WarpXParticleContainer.cpp` | symbols: `ReadParameters`, `AddNParticles` | check: per-species runtime behavior and particle insertion.
- `Source/BoundaryConditions/WarpXFieldBoundaries.cpp` | symbols: `ApplyEfieldBoundary`, `ApplyBfieldBoundary`, `ApplyJfieldBoundary` | check: BC implementation semantics.
- `Source/FieldSolver/WarpXPushFieldsEM.cpp` | symbols: `PSATDForwardTransformF`, `PSATDBackwardTransformF` and related transforms | check: spectral update path hooks.
- `Source/FieldSolver/WarpXSolveFieldsES.cpp` | symbols: `ComputeSpaceChargeField` | check: electrostatic field solve path.
- `Source/FieldSolver/FiniteDifferenceSolver/HybridPICModel/HybridPICModel.cpp` | symbols: `ReadParameters`, `HybridPICSolveE`, `FieldPush` | check: hybrid model update sequence.
- `Source/Laser/LaserProfiles.H` | symbols: `ILaserProfile`, `GaussianLaserProfile` | check: laser profile parameter and amplitude logic.
- `Python/pywarpx/picmi.py` | symbols: grid/species/solver classes | check: user-level Python model declarations.

## Practical verification
```bash
# inspect parser-driven parameter handling quickly
rg -n "queryWithParser|getWithParser|injection_style|boundary" Source/Initialization Source/Particles Source/BoundaryConditions
```
