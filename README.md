# OsteoVision: Dental X-ray Osteoporosis Detection

A work-in-progress machine learning research repository focused on building a low-cost osteoporosis screening pipeline from panoramic dental X-ray images.

## Why this matters

Osteoporosis is typically diagnosed using DXA machines, which are expensive and not widely available in many clinics. This project explores a new direction, using routine panoramic dental X-rays to predict osteoporosis risk through mandible segmentation and radiographic analysis.

> The goal is to make an osteoporosis screening solution available at every dental visit, enabling earlier referral and better preventive care.

## Project overview

This repository captures the initial phases of a broader pipeline:

- Data preparation using the DatasetNinja annotated dental X-ray dataset
- Mandible segmentation and ROI extraction
- Training of multiple segmentation-based models
- Ongoing work toward a final osteoporosis classification model

Current repository contents:

- `panoramic-dental-x-rays-DatasetNinja/`: annotated panoramic dental images used for segmentation training
- `models/`: trained model weights and notebooks with model training code
- `data_prep_DatasetNinja/`: notebook for dataset preparation and annotation processing

> Note: `Osteo_PR_Dataset/` and `masks/` are large data folders and are intentionally excluded from version control. They are generated or downloaded outside the repository to keep the Git history lightweight.

## What has been done so far

- Collected and curated a dental X-ray dataset for mandible segmentation
- Implemented a segmentation training pipeline with UNet++ and EfficientNet-B4
- Established a reproducible train/validation split using `splits.json`
- Saved model checkpoints for iterative improvement and comparison

## What is still in progress

This repository intentionally remains incomplete in the clinical prediction stage. The current focus is on building the best segmentation backbone before finalizing the osteoporosis detection model.

### Next steps

- Evaluate segmentation models across multiple backbones
- Select the best-performing architecture for final retraining
- Build the osteoporosis classification head using segmented mandible features
- Validate predictions against clinical DXA labels or proxy measures

## Quick start

1. Create a clean Python environment:

```bash
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

2. Open the main model notebook:

- `models/unet++_efficientb4.ipynb`

3. Run the data preparation notebook to generate masks and `splits.json`:

- `data_prep_DatasetNinja/data_prep_DatasetNinja.ipynb`

4. The notebook creates the required `masks/` folder and `splits.json` for training.

5. Track experiments using the saved model files in `models/`.

## Dependencies

- Python 3.11+
- PyTorch
- `segmentation-models-pytorch`
- `albumentations`
- OpenCV
- NumPy
- scikit-learn
- Matplotlib

## Vision and impact

This project is designed to impress by combining real-world medical imaging, modern deep learning architectures, and a compelling clinical narrative:

- dental X-rays are already common in dental clinics
- osteoporosis screening could be offered without adding a second specialized appointment
- a successful pipeline would make early detection more accessible and affordable

> The final product will connect dental radiology to osteoporosis risk prediction, making this a potentially revolutionary addition to preventive healthcare.



