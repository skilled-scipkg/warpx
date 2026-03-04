# warpx documentation map: Inputs and Modeling

Use these docs first for simulation parameterization and model selection.

## Core parameter references
- `Docs/source/usage/parameters.rst` | full input parameter reference.
- `Docs/source/usage/how_to_run.rst` | input-file and CLI override behavior.
- `Docs/source/usage/workflows/domain_decomposition.rst` | rank decomposition and load partitioning.
- `Docs/source/usage/faq.rst` | common modeling/runtime pitfalls.

## Physics/modeling references
- `Docs/source/theory/boundary_conditions.rst` | boundary condition behavior and constraints.
- `Docs/source/theory/models_algorithms/electromagnetic_pic.rst` | electromagnetic PIC model.
- `Docs/source/theory/models_algorithms/electrostatic_pic.rst` | electrostatic model details.
- `Docs/source/theory/models_algorithms/implicit_em_pic.rst` | implicit EM method context.
- `Docs/source/theory/models_algorithms/kinetic_fluid_hybrid_model.rst` | hybrid PIC model assumptions.
- `Docs/source/theory/boosted_frame/input_output.rst` | boosted-frame input/output semantics.

## Practical input examples
- `Examples/Tests/langmuir/inputs_base_2d` | compact, editable baseline input.
- `Examples/Physics_applications/pierce_diode/README.rst` | practical model setup walkthrough.
