# OsteoVision: Dental X-ray Osteoporosis Screening

A machine learning research repository documenting a pipeline from segmentation to ROI extraction and the next stage of osteoporosis prediction.

## Why this matters

Osteoporosis screening currently relies on DXA scanners, which are expensive and not always available. This project explores whether panoramic dental X-rays can support a lower-cost screening workflow by extracting the mandible region and using it for model development.

## Project overview

This repository has a two-phase pipeline:

- training and comparing segmentation models on annotated dental X-rays
- selecting the best segmentation backbone for mandible ROI extraction
- applying the chosen segmentation output to crop dental X-rays
- preparing for the next phase: osteoporosis classification on cropped images

Current repository highlights:

- `models/deeplabv3plus_efficientb4.ipynb`: the top-performing segmentation notebook
- `models/unet++_efficientb4.ipynb` and `models/unet_efficientb4.ipynb`: additional segmentation experiments
- `models/unet_resnet50.ipynb`: backbone comparison with a ResNet variant
- `cropping/segment_and_crop.ipynb`: the pipeline that segments and crops the mandible ROI
- `Osteo_PR_Dataset_Cropped/`: generated cropped ROI images for the next osteoporosis model
- `models/`: saved segmentation checkpoints and experiment notebooks
- `data_prep_DatasetNinja/`: dataset preparation and annotation conversion

> Note: `Osteo_PR_Dataset/`, `Osteo_PR_Dataset_Cropped/`, and `masks/` contain large data and are not tracked in Git.

## What has been done so far

- Trained multiple segmentation architectures, including UNet, UNet++, DeepLabV3+, and ResNet50-backed variants
- Identified `deeplabv3plus_efficientb4` as the best-performing segmentation model for this dataset
- Built a reproducible cropping pipeline to convert segmented masks into focused ROI images
- Generated the cropped image folder `Osteo_PR_Dataset_Cropped/` for downstream osteoporosis model training
- Saved the best segmentation checkpoint in `models/deeplabv3plus_efficientb4.pth`
- Established a clean training workflow with `splits.json` for reproducibility

## Next phase: osteoporosis prediction

The best segmentation model has been selected and the cropped mandible ROI is ready. The next step is to use the cropped X-rays for a classification model that predicts osteoporosis risk from the segmented mandible region.

Planned steps:

- design or fine-tune a classification network on cropped ROI images
- use the segmented mandible region instead of raw panoramic X-rays
- compare performance with and without ROI cropping
- document the final osteoporosis prediction approach and results

## Quick start

1. Create a clean Python environment:

```bash
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

2. Explore the best segmentation model notebook:

- `models/deeplabv3plus_efficientb4.ipynb`

3. Run the cropping workflow to generate focused mandible images:

- `cropping/segment_and_crop.ipynb`

4. Use the cropped image outputs as the input dataset for the next osteoporosis classification model.

## Dependencies

- Python 3.11+
- PyTorch
- `torchvision`
- `segmentation-models-pytorch`
- `albumentations`
- `opencv-python`
- `numpy`
- `pandas`
- `scikit-learn`
- `matplotlib`
- `jupyter`
- `notebook`
- `Pillow`



