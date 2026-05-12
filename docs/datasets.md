# 📦 Datasets Used in MedVision India

This document describes every dataset used in this project — its source, license, size, and how to download it.

---

## 1. Tuberculosis Datasets

### 1a. Shenzhen Chest X-ray Set
- **Source**: National Library of Medicine (NLM), USA
- **Images**: 336 TB-positive + 326 normal = 662 total
- **Format**: PNG, greyscale chest X-rays
- **Clinical Data**: Age, gender, lung abnormality notes per image
- **License**: Public domain (US Government)
- **Download**: https://lhncbc.nlm.nih.gov/LHC-downloads/downloads.html#tuberculosis-image-data-sets

### 1b. Montgomery County X-ray Set
- **Source**: National Library of Medicine (NLM), USA
- **Images**: 138 total (58 TB, 80 normal)
- **Format**: PNG
- **License**: Public domain
- **Download**: Same link as Shenzhen above

### 1c. Tawsifur Rahman TB Dataset (Kaggle)
- **Source**: Compiled from multiple public sources
- **Images**: 700 TB-positive images
- **Format**: JPEG/PNG
- **License**: CC BY 4.0
- **Download**: https://www.kaggle.com/datasets/tawsifurrahman/tuberculosis-tb-chest-xray-dataset

---

## 2. Skin Lesion Datasets

### 2a. HAM10000
- **Source**: ISIC Archive / Harvard Dataverse
- **Images**: 10,015 dermoscopic images
- **Classes**: 7 (melanoma, melanocytic nevi, BCC, AKIEC, BKL, DF, vascular)
- **Format**: JPEG, 600×450 px
- **License**: CC BY-NC 4.0
- **Download**: https://www.isic-archive.com/#!/topWithHeader/onlyHeaderTop/gallery

### 2b. ISIC 2024 SLICE-3D
- **Source**: 7 international dermatologic centers
- **Images**: 400,000+ skin lesion images
- **Format**: JPEG, smartphone-comparable resolution
- **License**: CC BY-NC 4.0
- **Download**: https://www.kaggle.com/competitions/isic-2024-challenge

---

## 3. Ophthalmic Datasets

### 3a. APTOS 2019 (Indian Dataset)
- **Source**: Aravind Eye Hospital, India + Kaggle competition
- **Images**: 5,590 retinal fundus images
- **Classes**: 5 (No DR, Mild, Moderate, Severe, Proliferative DR)
- **Format**: JPEG, variable resolution
- **License**: Competition rules (non-commercial research use)
- **Download**: https://www.kaggle.com/c/aptos2019-blindness-detection

### 3b. IDRiD (Indian Diabetic Retinopathy Image Dataset)
- **Source**: Eye clinic, Nanded, Maharashtra, India
- **Images**: 516 images at 50° FOV (Kowa camera)
- **Classes**: ICDR DR grades + lesion segmentation masks
- **License**: CC BY 4.0
- **Download**: https://ieee-dataport.org/open-access/indian-diabetic-retinopathy-image-dataset-idrid

### 3c. ODIR (Ocular Disease Intelligent Recognition)
- **Source**: Shanggong Medical Technology, China
- **Images**: 8,000 fundus images (left + right eye per patient)
- **Classes**: 8 (Normal, DR, Glaucoma, Cataract, AMD, Hypertension, Myopia, Other)
- **License**: CC BY-NC-SA 4.0
- **Download**: https://odir2019.grand-challenge.org

### 3d. EyePACS
- **Source**: Originally captured by Aravind Eye Hospital technicians
- **Images**: 35,126 fundus images
- **Classes**: 0–4 DR severity scale
- **License**: Kaggle competition (research use)
- **Download**: https://www.kaggle.com/c/diabetic-retinopathy-detection

---

## Preprocessing Notes

All images are resized to **224×224 pixels** before training.

- **Chest X-rays (TB)**: Apply CLAHE (Contrast Limited Adaptive Histogram Equalization) to enhance lung structures
- **Skin images**: Normalize RGB channels to ImageNet mean/std; apply hair removal filter
- **Fundus images**: Apply Ben Graham's preprocessing (subtract local average color, clip edges)

Preprocessing scripts are in the `data/` folder for each module.
