[![DOI](https://zenodo.org/badge/1229260484.svg)](https://doi.org/10.5281/zenodo.20089015)

# Bone-Loss Segmentation

> **Status — code accompanying research articles currently under peer review.**
> This repository is released for methodological transparency and
> reproducibility while the companion article(s) are under review for
> publication.

## Overview

A two-notebook pipeline for automated assessment of periodontal bone loss from
intraoral panoramic radiographs. The pipeline localizes the mouth region,
segments individual teeth, segments dental crowns and the alveolar ridge, and
quantifies per-tooth bone loss as a percentage from the resulting geometry.

| Notebook | Purpose |
| --- | --- |
| `Bone_Loss_Segmentation_(Training).ipynb` | Trains the crown and alveolar-ridge segmentation models. Two architectures are compared — SegFormer-B5 (PyTorch Lightning) and YOLOv11x-seg (Ultralytics). A Detectron2 RetinaNet provides a preprocessing mouth crop. |
| `Bone_Loss_Segmentation_(Inference).ipynb` | Runs the full pipeline on a panoramic radiograph: mouth detection → tooth instance segmentation (Detectron2 Mask R-CNN) → crown and alveolar-ridge segmentation (YOLOv11) → geometric bone-loss measurement → LabelMe-compatible JSON export. Includes a Gradio interface for single-image analysis. |

## Repository layout

```
boneloss_inference/
├── Bone_Loss_Segmentation_(Training).ipynb
├── Bone_Loss_Segmentation_(Inference).ipynb
├── .gitignore
└── README.md
```

Datasets, model weights, and trained checkpoints are intentionally not stored
in this repository — see *Data and model availability* below.

## Data and model availability

The pretrained model weights and trained checkpoints referenced in these
notebooks are property of [InReDD](https://inredd.com.br/en) and are **not
publicly available**, nor distributed with this repository.

The clinical dataset is also property of InReDD. It may be requested for
non-commercial academic use through the
[InReDD Open Data portal](https://inredd.com.br/en/solutions/open-data).

## Reproducibility

- Tested on a local workstation with an NVIDIA RTX 5070 (12 GB).
- Pinned dependencies are declared in the install cell of each notebook —
  `pytorch-lightning==2.4.0`, `transformers==4.46.2`, `ultralytics`, plus
  Detectron2 built from source.
- Random seeds, image sizes, batch sizes, and other hyperparameters are
  surfaced as named constants at the top of each section.
- Drive identifiers and credentials in the install cells are masked with
  placeholders; obtain the corresponding artefacts from InReDD before running.

## Citation

A citation entry will be added once the companion article is published. Please
contact the corresponding author for the current preprint reference.

## License

License terms will be defined upon publication. Until then, the code is shared
for peer-review and academic-discussion purposes only; please do not
redistribute or use it for commercial applications without the corresponding
author's written consent.
