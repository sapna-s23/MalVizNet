# Phase 2 — Resolution Ablation

Extension of Phase 1: the same 12 architectures, same dataset and split, re-tested at two additional resolutions to test whether the "shallow beats deep" finding is resolution-dependent, and to reduce/eliminate the interpolation-related deviation present at 128×128.

## Resolutions tested

- **32×32** — native Malimg resolution, no resizing/interpolation involved
- **64×64** — light upscale from native resolution

## Approach

- Two separate Kaggle notebooks (`malviznet-32x32`, `malviznet-64x64`), each with its own checkpoint/recovery workflow
- Starting point: literal architecture specification from Pinhero et al. (2021), Table 2 — no corrections applied up front
- Corrections (optimizer, pooling, dense-layer sizing, etc.) applied only if/when a specific model fails to train, same empirical approach used in Phase 1
- Same stratified 70/30 split (`random_state=42`) reused from Phase 1 for direct comparability

## Status

🚧 In progress — architecture implementation and initial training runs not yet started.

## Contents (to be added)

- `malviznet-32x32.ipynb`
- `malviznet-64x64.ipynb`
- Results comparison table (32×32 vs 64×64 vs Phase 1's 128×128)
