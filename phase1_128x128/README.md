# Phase 1 — 128×128, Original Study

Full implementation and benchmarking of all 12 CNN architectures (M1–M12) from Pinhero et al. (2021), Table 2, on the Malimg dataset at 128×128 resolution.

## Contents

- Kaggle notebook (`.ipynb`) — data loading, preprocessing, all 12 model definitions, training loops, evaluation
- Results summary (see main repo README for headline numbers)

## Key details

- Resolution: 32×32 native → resized to 128×128 via `cv2.INTER_CUBIC` (deviation from source paper's `INTER_AREA`, documented as a deliberate upscale correction)
- Optimizer corrections: Adam (LR=0.001) in place of literal SGD for M9–M11 (SGD failed to converge — loss stuck at ln(25))
- Architecture corrections: 2×2 stride-2 pooling (literal 1×1 spec is a spatial no-op); GlobalAveragePooling2D + reduced Dense widths in place of literal Flatten+Dense(4096→2048→1024) for M9–M11 (literal spec produced ~280M params)

Full deviation table and rationale are documented in the final report (submitted separately, not tracked in this repo).

## Best result

M4 (Conv+Pool+Conv+Dense+Dense, shallow) — **82.48% test accuracy**, 16.79M params.

Full results table for all 12 models is in the notebook output / final report.
