# warpx source map: Theory and Methods

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "EvolveE|EvolveB|SpectralSolver|HybridPICSolveE|UpdateMomentum|doGatherShapeN|doDepositionShapeN" Source`
- `rg -n "solver|pusher|PICMI" Python/pywarpx/picmi.py`

## Function-level entry points
- `Source/FieldSolver/FiniteDifferenceSolver/EvolveE.cpp` | symbols: `FiniteDifferenceSolver::EvolveE`, `EvolveECartesian`, `EvolveECylindrical` | check: explicit E-field update equations by geometry.
- `Source/FieldSolver/FiniteDifferenceSolver/EvolveB.cpp` | symbols: `FiniteDifferenceSolver::EvolveB`, `EvolveBCartesian` | check: B-field advance variants.
- `Source/FieldSolver/SpectralSolver/SpectralSolver.cpp` | symbols: `ForwardTransform`, `pushSpectralFields`, `CurrentCorrection` | check: PSATD spectral update path.
- `Source/FieldSolver/SpectralSolver/SpectralSolverRZ.cpp` | symbols: `pushSpectralFields`, `CurrentCorrection`, `VayDeposition` | check: RZ spectral-specific behavior.
- `Source/FieldSolver/FiniteDifferenceSolver/HybridPICModel/HybridPICModel.cpp` | symbols: `ReadParameters`, `HybridPICSolveE`, `FieldPush` | check: hybrid kinetic-fluid coupling algorithm path.
- `Source/Particles/Pusher/PushSelector.H` | symbols: `doParticleMomentumPush` | check: selection among Boris/Vay/Higuera-Cary pushers.
- `Source/Particles/Pusher/UpdateMomentumBoris.H` | symbols: `UpdateMomentumBoris` | check: Boris momentum update equations.
- `Source/Particles/Pusher/UpdateMomentumVay.H` | symbols: `UpdateMomentumVay` | check: Vay momentum update equations.
- `Source/Particles/Deposition/CurrentDeposition.H` | symbols: `doDepositionShapeN`, `doDepositionShapeNImplicit` | check: current deposition implementation details.
- `Source/Particles/Gather/FieldGather.H` | symbols: `doGatherShapeN`, `doDirectGatherVectorField` | check: field gather interpolation semantics.

## Practical verification
```bash
# inspect method implementation anchors quickly
rg -n "EvolveE|EvolveB|pushSpectralFields|UpdateMomentum|doDepositionShapeN|doGatherShapeN" Source
```
