# MalVizNet

CNN-based malware family classification via grayscale image visualization of malware binaries.

A comparative replication and extension of the 12-CNN-architecture framework proposed in Pinhero et al. (2021), *"Malware detection employed by visualization and deep neural network"* (Computers & Security, 105, 102247), applied to the 25-class Malimg family classification task.

## Overview

This project implements and benchmarks 12 CNN architectures (M1–M12) — ranging from shallow custom CNNs to VGG3 variants and ResNet-50 — on the Malimg dataset (9,339 grayscale malware images, 25 families). All models are trained from scratch under a unified data pipeline, with every deviation from the source paper's specification documented and justified.

**Best result (Phase 1, 128×128):** M4 (shallow 4-layer CNN) — 82.48% test accuracy, 16.79M params.

**Key finding:** shallow CNNs outperformed all VGG3/ResNet-50 variants — contrary to the source paper's own conclusions. Attributed primarily to smaller training set size (6,537 vs. the source paper's 15,617 combined samples) and no transfer learning for the deep models.

## Repository structure

```
malviznet/
├── phase1_128x128/              # Original study: 12 models at 128×128, full results + deviations
├── phase2_resolution_ablation/  # Extension: same 12 models re-tested at 32×32 and 64×64
├── scripts/                     # Shared preprocessing / data-loading code reused across phases
└── README.md
```

## Dataset

- **Source:** Malimg dataset (Nataraj et al., 2011), 9,339 samples, 25 malware families
- **Format used:** `malimg.npz`, single `arr` key, (9339, 2) object array of image + integer label pairs
- **Split:** Stratified 70/30 (scikit-learn, `random_state=42`) → 6,537 train / 2,802 test, all classes represented in both

## Reference

Pinhero, A., Anupama, M.L., Vinod, P., Visaggio, C.A., Aneesh, N., Abhijith, S., AnanthaKrishnan, S. (2021). Malware detection employed by visualization and deep neural network. *Computers & Security*, 105, 102247.

## Status

- ✅ Phase 1 (128×128, all 12 models): complete
- 🚧 Phase 2 (resolution ablation, 32×32 / 64×64): in progress

## Author

Sapna Samariya — 7th semester academic project
