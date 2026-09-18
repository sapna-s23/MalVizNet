# \# Phase 2 — Resolution Ablation

# 

# Extension of Phase 1: the same 12 architectures, same dataset and split, re-tested at two additional resolutions to test whether the "shallow beats deep" finding is resolution-dependent, and to reduce/eliminate the interpolation-related deviation present at 128×128.

# 

# \## Resolutions tested

# 

# \- \*\*32×32\*\* — native Malimg resolution, no resizing/interpolation involved (complete)

# \- \*\*64×64\*\* — light upscale from native resolution (not started)

# 

# \## Approach

# 

# \- Two separate Kaggle notebooks (`malviznet-32x32`, `malviznet-64x64`), each with its own checkpoint/recovery workflow

# \- Starting point: literal architecture specification from Pinhero et al. (2021), Table 2 — no corrections applied up front

# \- Corrections (optimizer, pooling, dense-layer sizing, etc.) applied only if/when a specific model fails to train, same empirical approach used in Phase 1

# \- Same stratified 70/30 split (`random\_state=42`) reused from Phase 1 for direct comparability

# \- Batch size 64 used for all 12 models at 32×32 (Phase 1 used 32 for M1–M8), documented as a simplification deviation

# 

# \## Status

# 

# ✅ 32×32: complete — all 12 models trained and evaluated

# 🚧 64×64: not yet started

# 

# \## 32×32 Results

# 

# | Model | Params | Accuracy | Weighted F1 | Macro F1 | Latency (ms) |

# |---|---|---|---|---|---|

# | M7 | 275,065 | 86.76% | 0.866 | 0.864 | 0.09 |

# | M4 | 1,061,497 | 86.51% | 0.864 | 0.872 | 0.09 |

# | M3 | 1,070,745 | 85.72% | 0.854 | 0.856 | 0.11 |

# | M9 | 327,065 | 84.19% | 0.843 | 0.853 | 0.10 |

# | M10 | 327,065 | 83.62% | 0.841 | 0.859 | 0.10 |

# | M11 | 327,065 | 82.80% | 0.829 | 0.858 | 0.10 |

# | M8 | 87,705 | 79.51% | 0.795 | 0.825 | 0.10 |

# | M12 | 26,348,441 | 66.88% | 0.671 | 0.756 | 0.33 |

# | M6 | 17,017 | 65.77% | 0.674 | 0.681 | 0.09 |

# | M1 | 1,061,497 | 61.24% | 0.602 | 0.579 | 0.09 |

# | M5 | 7,769 | 58.07% | 0.583 | 0.478 | 0.09 |

# | M2 | 1,052,249 | 22.13% | 0.190 | 0.271 | 0.10 |

# 

# \*\*Best: M7\*\* — highest accuracy and weighted-F1, with 96× fewer parameters than M4 for near-identical performance.

# \*\*Worst: M2\*\* — literal-spec learning rate (0.00001) does not converge at this resolution even at 200 epochs.

# 

# \## Key findings vs. Phase 1 (128×128)

# 

# \- \*\*GlobalPooling models (M5, M6) and BatchNorm/VGG3 models (M9, M10, M11) show the largest gains at lower resolution\*\* — up to +50pp accuracy for M6. Likely because GlobalPooling discards less useful spatial information when there's less spatial information to begin with.

# \- \*\*M12 (ResNet-50) underperforms its Phase 1 result\*\* (66.88% vs 68.42%) — at 32×32, `conv5\_block1–3` (\~8M of 26.35M params) operate on a degenerate 1×1 feature map, meaning \~30% of the network does no meaningful spatial computation. Documented as a limitation, not a training failure — the model builds and trains without error.

# \- \*\*M2 fails to converge\*\* regardless of epoch budget (tested up to 200 epochs) — its literal paper-specified LR (0.00001) appears too conservative for this resolution/batch-size combination.

# \- \*\*M3, M4, M7 improve moderately\*\* over their Phase 1 results, continuing to be strong performers.

# \- Confusion matrix analysis (M7, M4) replicates Phase 1's finding: the same class-confusion clusters (\~2–3, 6–8, 16, 20–21) recur across architecturally different models, reinforcing that these reflect genuine visual similarity between malware families rather than a model-specific weakness.

# 

# \## Contents

# 

# \- `malviznet-32x32.ipynb` — full training/evaluation notebook

# \- `phase2\_32x32\_results.csv` — full metrics table (accuracy, F1, params, latency)

# \- `confusion\_matrices\_32x32.png` — confusion matrices for M7, M4, M10, M2

# \- `malviznet-64x64.ipynb` — not yet created

