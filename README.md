# 🏥 MedVision India
### Offline AI-Powered Diagnostic Assistant for Rural India

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/Platform-Android%208%2B-green)](https://android.com)
[![Status](https://img.shields.io/badge/Status-In%20Development-blue)]()
[![Made in India](https://img.shields.io/badge/Made%20in-India%20🇮🇳-orange)]()

> **Empowering frontline health workers with AI — no internet required.**

MedVision India is a compact, offline-first mobile AI system that helps ASHA workers, ANMs, and rural clinicians screen for **Tuberculosis**, **Skin Lesions**, and **Ophthalmic Diseases** using both camera images and patient symptom data. All inference runs on-device. No data ever leaves the phone.

---

## 🌍 The Problem

Over **600 million Indians** live in rural areas with limited access to specialist doctors.

- **TB**: India accounts for 27% of global TB cases. Most go undetected until late stages.
- **Skin Disease**: Dermatologists are concentrated in cities; rural patients travel 100–200 km for a consultation.
- **Eye Disease**: Diabetic Retinopathy affects 18 million Indians; 90% of blindness is preventable if caught early.

A frontline health worker with a smartphone and this app can screen patients and flag high-risk cases for referral — closing the gap between rural populations and specialist care.

---

## 🎯 What This App Does

| Module | Input | Output |
|---|---|---|
| 🫁 **TB Screener** | Chest X-ray photo + symptoms | TB risk score + Grad-CAM heatmap |
| 🔬 **Skin Lesion Identifier** | Skin photo + lesion description | Lesion class + malignancy risk |
| 👁️ **Ophthalmic Finder** | Fundus/eye photo + vision symptoms | DR grade + condition flag |

All three modules work **fully offline** on any Android 8+ phone with 2 GB RAM.

---

## 🏗️ Project Structure

```
MedVisionIndia/
│
├── 📁 data/
│   ├── README.md                  # Dataset download instructions
│   ├── tb/                        # TB dataset preprocessing scripts
│   ├── skin/                      # Skin lesion preprocessing scripts
│   └── ophthalmic/                # Eye disease preprocessing scripts
│
├── 📁 models/
│   ├── tb_model/                  # MobileNetV3 for TB detection
│   ├── skin_model/                # EfficientNet-Lite0 for skin lesions
│   ├── ophthalmic_model/          # EfficientNet-Lite0 for eye disease
│   └── fusion/                    # Multimodal fusion logic (image + symptoms)
│
├── 📁 training/
│   ├── train_tb.py                # TB model training script
│   ├── train_skin.py              # Skin model training script
│   ├── train_ophthalmic.py        # Eye model training script
│   ├── convert_to_tflite.py       # TFLite INT8 quantization converter
│   └── evaluate_models.py         # Accuracy, AUC, confusion matrix
│
├── 📁 app/                        # Flutter mobile application
│   ├── lib/
│   │   ├── screens/               # UI screens per disease module
│   │   ├── models/                # TFLite model inference classes
│   │   ├── widgets/               # Reusable UI components
│   │   └── utils/                 # Image preprocessing, Grad-CAM overlay
│   └── assets/
│       └── tflite/                # Bundled .tflite model files
│
├── 📁 docs/
│   ├── architecture.md            # System architecture deep-dive
│   ├── datasets.md                # Full dataset descriptions and sources
│   ├── model_cards/               # Model cards (accuracy, bias, limitations)
│   │   ├── tb_model_card.md
│   │   ├── skin_model_card.md
│   │   └── ophthalmic_model_card.md
│   └── funding_proposal.md        # Draft funding proposal for BIRAC/IndiaAI
│
├── 📁 notebooks/
│   ├── 01_tb_data_exploration.ipynb
│   ├── 02_skin_data_exploration.ipynb
│   ├── 03_ophthalmic_data_exploration.ipynb
│   ├── 04_model_training_demo.ipynb
│   └── 05_gradcam_visualization.ipynb
│
├── 📁 results/
│   ├── tb_results.md              # TB model performance report
│   ├── skin_results.md            # Skin model performance report
│   └── ophthalmic_results.md      # Eye model performance report
│
├── requirements.txt               # Python dependencies
├── LICENSE                        # MIT License
└── README.md                      # This file
```

---

## 🧠 Model Architecture

### Why These Models?

| Disease | Model | Size (INT8) | Target Accuracy |
|---|---|---|---|
| Tuberculosis | MobileNetV3-Small | ~4 MB | >90% AUC |
| Skin Lesion | EfficientNet-Lite0 | ~5 MB | >88% accuracy |
| Ophthalmic | EfficientNet-Lite0 | ~5 MB | >85% accuracy |
| **Total App** | All 3 + Flutter UI | **~25 MB** | — |

All models use **INT8 post-training quantization** via TensorFlow Lite, which reduces model size by ~4× while maintaining near-identical accuracy on medical images.

### Multimodal Fusion

```
[Camera Image] ──► [CNN Branch] ──► [Disease Probabilities]
                                              │
                                         [Fusion MLP] ──► [Final Risk Score]
                                              │
[Symptom Form] ──► [Rule Engine] ──► [Symptom Scores]
```

The symptom branch captures structured clinical inputs (fever duration, cough type, lesion color/texture, vision blur level) and combines them with image-based predictions without requiring any large language model.

---

## 📦 Datasets Used

| Dataset | Disease | Size | Source |
|---|---|---|---|
| Shenzhen + Montgomery | TB | 662 images | [NIH NLM](https://lhncbc.nlm.nih.gov/LHC-downloads/downloads.html#tuberculosis-image-data-sets) |
| Tawsifur Rahman TB Dataset | TB | 700 images | [Kaggle](https://www.kaggle.com/datasets/tawsifurrahman/tuberculosis-tb-chest-xray-dataset) |
| HAM10000 | Skin Lesions | 10,000 images | [ISIC Archive](https://www.isic-archive.com) |
| ISIC 2024 SLICE-3D | Skin Lesions | 400,000 images | [Kaggle](https://www.kaggle.com/competitions/isic-2024-challenge) |
| APTOS 2019 | Diabetic Retinopathy | 5,590 images | [Kaggle](https://www.kaggle.com/c/aptos2019-blindness-detection) |
| IDRiD | Diabetic Retinopathy | 516 images | [IEEE DataPort](https://ieee-dataport.org/open-access/indian-diabetic-retinopathy-image-dataset-idrid) |
| ODIR | Multi-eye Disease | 8,000 images | [ODIR Challenge](https://odir2019.grand-challenge.org) |

> Full dataset descriptions, preprocessing steps, and license notes are in [`docs/datasets.md`](docs/datasets.md)

---

## 🚀 Roadmap

- [x] Repository structure & documentation
- [ ] Dataset download + preprocessing scripts (TB)
- [ ] Dataset download + preprocessing scripts (Skin, Eye)
- [ ] MobileNetV3 TB model training
- [ ] EfficientNet-Lite0 Skin model training
- [ ] EfficientNet-Lite0 Ophthalmic model training
- [ ] TFLite INT8 conversion for all models
- [ ] Grad-CAM explainability overlay
- [ ] Flutter app with all 3 modules
- [ ] Multilingual UI (Tamil, Hindi, Telugu)
- [ ] PHC pilot study (target: 100 patients)
- [ ] BIRAC / IndiaAI grant application

---

## 🤝 Relevance to Indian Government Initiatives

This project directly aligns with:

- **IndiaAI Mission (MeitY, 2024)** — democratisation of AI for rural and underserved populations
- **IndiaAI Application Development Initiative (IADI)** — explicitly lists TB X-ray screening and DR detection as priority use cases
- **Department of Biotechnology (DBT)** — funds AI-based diagnostics for TB, DR, and cancer
- **BIRAC-India Health Fund** — co-funding pool for TB screening tools for resource-limited settings
- **National Digital Health Mission (NDHM)** — digital health records and diagnostics at PHC level

---

## 🛡️ Privacy & Ethics

- ✅ All AI inference is **on-device** — no images or patient data ever leave the phone
- ✅ No internet connection required for diagnosis
- ✅ Compliant with India's **DPDP Act 2023** (Digital Personal Data Protection)
- ✅ App is a **screening and referral aid** — not a replacement for clinical diagnosis
- ✅ Every result includes a "Refer to Doctor" recommendation for high-risk findings

---

## 👨‍💻 Getting Started (For Developers)

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/MedVisionIndia.git
cd MedVisionIndia

# Install Python dependencies
pip install -r requirements.txt

# Download TB dataset (instructions in data/tb/README.md)
cd data/tb
python download_tb_data.py

# Run the TB preprocessing pipeline
python preprocess_tb.py
```

> Step-by-step guides for each module are in the [`docs/`](docs/) folder and Jupyter notebooks in [`notebooks/`](notebooks/).

---

## 📄 License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for details.

---

## 📬 Contact & Collaboration

Built with the goal of making specialist-level screening accessible to every Indian, regardless of where they live.

If you are a clinician, researcher, NGO, or government body interested in collaborating or piloting this tool — please open an issue or reach out directly.

---

*"The best doctor is the one who can reach the patient." — MedVision India exists to close that gap.*
