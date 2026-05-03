# AGENTS.md — simplegrad examples repo

A collection of Jupyter notebooks demonstrating [simplegrad](https://github.com/simplegrad/simplegrad) (`sg`).

## Goal

Show clean, working deep learning workflows built with simplegrad.
Maximize `sg` usage — keep everything else minimal.

## Rules

### Imports
- Only import what is actually used. No unused imports.
- Prefer the standard library and numpy over third-party packages.
- If a third-party package is needed, use the simplest one that does the job.

### Dependencies
Allowed third-party packages beyond `simplegrad` and `numpy`:
- `tqdm` — wrap the epoch loop with `tqdm(range(NUM_EPOCHS), desc="training")`
- `matplotlib` — sanity checks and inline plots only

### numpy → sg.Tensor handoff
Use numpy only for I/O and dataset-level preprocessing (reading files, splitting, one-hot encoding).
Convert to `sg.Tensor` at the earliest point where the data enters the model pipeline.
Never pass raw numpy arrays into model calls.

### No single-use functions
If a function is called exactly once, inline it as a block of code.
Only define a function when it is called in two or more places.

### One cell = one step
Cells must be short and focused on a single logical step.
Never mix data loading, model definition, and training in the same cell.

### Comments
Only where the logic is non-obvious. Do not narrate what the code already says.

## Notebook cell order

1. Imports
2. Config — hyperparameters as `ALL_CAPS`, paths as `lowercase`
3. Dataset download — commented-out shell commands
4. Data loading — numpy/PIL, print shapes
5. Sanity check — visualize one sample
6. Preprocessing + convert to `sg.Tensor`
7. Model — `sg.nn.Sequential(…)` + `model.summary()`
8. Optimizer, loss, tracker
9. Training loop
10. Plot — `sg.vis.plot(...)`
11. Evaluation
12. Computation graph — `sg.vis.graph(...)` + `tracker.save_comp_graph(...)`
