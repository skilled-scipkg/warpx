# warpx source map: Parallel and HPC

Use this map only after exhausting `doc_map.md`.

## Fast source navigation
- `rg -n "mpi_init|MPI_Init_thread|check_mpi_thread_level|FillBoundary|SumBoundary|GuardCell" Source`
- `rg -n "LoadBalance|MoveWindow|ComputeDt|UpdateAuxilaryData" Source`

## Function-level entry points
- `Source/ablastr/parallelization/MPIInitHelpers.cpp` | symbols: `mpi_init`, `mpi_finalize`, `check_mpi_thread_level` | check: MPI startup and thread-level diagnostics.
- `Source/ablastr/parallelization/MPIInitHelpers.H` | symbols: `mpi_thread_required` | check: required thread mode policy.
- `Source/Parallelization/GuardCellManager.cpp` | symbols: `guardCellManager::Init` | check: guard-cell counts from solver/deposition settings.
- `Source/Parallelization/WarpXComm.cpp` | symbols: `WarpX::UpdateAuxilaryData`, `FillBoundaryE`, `FillBoundaryB` | check: boundary exchange and staggered/nodal communication paths.
- `Source/Parallelization/WarpXSumGuardCells.cpp` | symbols: guard-cell summation wrappers | check: overlap summation behavior.
- `Source/Utils/WarpXMovingWindow.cpp` | symbols: `WarpX::MoveWindow` | check: moving-window shifts and communication implications.
- `Source/Evolve/WarpXComputeDt.cpp` | symbols: `WarpX::ComputeDt`, `WarpX::UpdateDtFromParticleSpeeds` | check: timestep constraints relevant for scaling stability.
- `Source/Diagnostics/ReducedDiags/LoadBalanceCosts.cpp` | symbols: `LoadBalanceCosts::ComputeDiags`, `WriteToFile` | check: cost diagnostics generated for scaling analysis.
- `Source/Diagnostics/ReducedDiags/LoadBalanceEfficiency.cpp` | symbols: `LoadBalanceEfficiency::ComputeDiags` | check: load-balance efficiency diagnostics.

## Practical verification
```bash
# validate MPI/parallelization hooks in source
rg -n "mpi_init|MPI_Init_thread|FillBoundary|GuardCell|LoadBalance" Source
```
