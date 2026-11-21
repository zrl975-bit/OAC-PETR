# OAC-PETR: Orientation Ambiguity Modeling and Query Reliability Calibration for Sparse-Query Camera-Only 3D Object Detection

This is the official repository for **OAC-PETR**, a training and score-calibration framework built upon [StreamPETR](https://github.com/exiawsh/StreamPETR) without altering its backbone or transformer decoder architecture.

> **Status:** The manuscript is currently under review. The training and evaluation code, stage configuration files, evaluation logs, and final single-checkpoint weights will be publicly released here upon acceptance.

## Overview

OAC-PETR addresses two key limitations in sparse-query camera-only 3D object detection:
1. **Ambiguity-Aware Query Training:** Combines origin-centered ray-aware denoising with category-conditioned bimodal supervision on matched main queries and symmetry-aware Hungarian assignment to accommodate front–back heading ambiguity.
2. **Object-Centric Teacher-Guided Refinement & Checkpoint Averaging:** Selectively transfers directed yaw evidence using ground-truth association and teacher–student error filtering during full-head refinement, then consolidates refined checkpoints into a single model.
3. **Query Reliability Calibration (QRC):** Trains a lightweight branch on the frozen detector to estimate geometric box quality and calibrate detection scores before top-300 ranking, without modifying box coordinates or introducing extra teacher/ensemble overhead at inference.

## Main Results on nuScenes Validation Set

All results below use ResNet-50 (ImageNet pretraining), $256 \times 704$ input resolution, 900 queries, and single-checkpoint inference (without CBGS, EMA, or future-frame inputs).

| Method | mAP ↑ | mATE ↓ | mASE ↓ | mAOE ↓ | mAVE ↓ | mAAE ↓ | NDS ↑ |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| StreamPETR (R50, 24e baseline) | 0.3745 | 0.6799 | 0.2762 | 0.6456 | 0.3001 | 0.2088 | 0.4762 |
| **OAC-PETR (Single-Checkpoint)** | **0.4012** | **0.6438** | 0.2784 | **0.6068** | **0.2872** | **0.2038** | **0.4986** |
| *Improvement* | *+0.0267* | *-0.0361* | *+0.0022* | *-0.0388* | *-0.0129* | *-0.0050* | *+0.0224* |

## Release Plan (Upon Acceptance)

- [ ] Training and evaluation code (built on the StreamPETR codebase)
- [ ] Stage configuration files (ambiguity-aware base training, teacher-guided refinement, checkpoint averaging, and QRC)
- [ ] Final single-checkpoint model weights
- [ ] Official nuScenes validation evaluation logs and reproduction scripts

## Acknowledgements

This project builds upon the open-source [StreamPETR](https://github.com/exiawsh/StreamPETR) and [MMDetection3D](https://github.com/open-mmlab/mmdetection3d) codebases. We thank the authors for making their implementations publicly available.

## Citation

If you find this work useful in your research, please consider citing our paper (BibTeX will be updated upon publication).
