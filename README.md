<div align="center">

# ♻️ PolyNex

### Towards Robust Waste Recognition: An Object-Level Annotated Multiclass Waste Image Dataset for Comprehensive Deep Learning-Based Detection Benchmarking and Performance Analysis Across Diverse Real-World Waste Categories

**Object-level annotations · Seven waste categories · Bangladesh field imagery**

[![Task](https://img.shields.io/badge/Task-Object%20Detection-2563eb?style=for-the-badge)](#)
[![Classes](https://img.shields.io/badge/Classes-7-0f766e?style=for-the-badge)](#)
[![Images](https://img.shields.io/badge/Original%20Images-3%2C154-7c3aed?style=for-the-badge)](#)
[![Annotations](https://img.shields.io/badge/Instances-4%2C022-d97706?style=for-the-badge)](#)

**PolyNex** is a real-world, object-level annotated waste image dataset designed to support the development, evaluation, and benchmarking of deep-learning-based waste detection systems under diverse environmental conditions.

[Dataset & Code Repository](https://github.com/tarekrahamn/PolyNex) · [Report an Issue](https://github.com/tarekrahamn/PolyNex/issues)

</div>

---

## ✨ Overview

Waste objects in real environments vary in appearance, scale, orientation, illumination, and background. PolyNex addresses this challenge with field-collected images from urban and semi-urban locations across Bangladesh. Each target object is annotated with a bounding box, making the dataset suitable for object detection rather than image-level classification alone.

The dataset contains **3,154 original images** and **4,022 object-level annotations** across seven waste categories. Images were captured using seven smartphone models and include natural variation in scene composition, camera characteristics, object scale, and lighting.

## 📊 Dataset at a Glance

| Attribute | Description |
|---|---|
| Dataset name | PolyNex |
| Task | Multiclass object detection |
| Original images | **3,154** |
| Annotated instances | **4,022** |
| Number of classes | **7** |
| Annotation format | YOLO bounding-box format |
| Image size | 640 × 640 pixels |
| Collection setting | Real-world urban and semi-urban environments |
| Collection country | Bangladesh |
| Capture devices | Seven smartphone models |
| Dataset split | 70% / 20% / 10% (train / validation / test) |

### Dataset partitions

| Split | Original images | Annotated instances |
|---|---:|---:|
| Train | 2,208 | 2,834 |
| Validation | 631 | 791 |
| Test | 315 | 397 |
| **Total** | **3,154** | **4,022** |

> **Note:** The released dataset version described in the paper contains 7,495 images after training-set augmentation: 6,549 training, 631 validation, and 315 test images. The original-image counts above are reported before augmentation. Only the training subset was augmented.

## 🗂️ Waste Categories

PolyNex includes seven waste categories:

| Class | Category | Images | Instances |
|---:|---|---:|---:|
| 1 | Food and Organic Waste | 698 | 1,024 |
| 2 | Metal Scrap Waste | 582 | 688 |
| 3 | Polythene Waste | 500 | 562 |
| 4 | Aluminium Waste | 309 | 515 |
| 5 | Plastic Waste | 500 | 497 |
| 6 | Electrical Waste | 319 | 433 |
| 7 | Construction Waste | 249 | 303 |
| | **Total** | **3,154** | **4,022** |

The category numbering in this summary follows the presentation order in the paper. For model training, use the class mapping defined in the distributed `data.yaml` file.

## 🌍 Real-World Data Collection

Images were collected at multiple locations across Bangladesh, including areas in Dhaka, Cumilla, Madaripur, Faridpur, Jashore, and Mymensingh.

The collection process was designed to capture natural variation in:

- Illumination and time of capture
- Object orientation, scale, and camera distance
- Background complexity and scene composition
- Camera resolution and colour reproduction
- Single-object and multi-object scenes

Images were acquired using the following smartphone models:

- Vivo Y51 (2020)
- Samsung Galaxy A06
- Samsung Galaxy S24 Ultra
- HONOR X9d
- Samsung Galaxy F13
- Google Pixel 6a
- Samsung Galaxy S23

The approximate camera-to-object distance was 30–60 cm.

## 🏷️ Annotation & Preprocessing

All target objects were annotated with bounding boxes using **Roboflow**. The dataset follows the YOLO annotation convention, with normalized bounding-box coordinates.

The preparation workflow described in the paper includes:

1. Manual inspection and quality screening.
2. Duplicate and low-quality image removal.
3. EXIF-based orientation correction.
4. Resizing to **640 × 640** pixels.
5. Bounding-box annotation and class assignment.
6. A class-wise train/validation/test split.
7. Training-only rotation augmentation between **−10° and +10°**, with corresponding bounding-box updates.

The split was performed before augmentation to prevent augmented training images from entering the validation or test subsets.

## 📁 Dataset Structure

The released dataset is organized in a YOLO-style directory layout:

```text
PolyNex/
├── train/
│   ├── images/
│   └── labels/
├── valid/
│   ├── images/
│   └── labels/
├── test/
│   ├── images/
│   └── labels/
├── data.yaml
└── metadata.csv
```

| File / directory | Purpose |
|---|---|
| `train/images/` | Training images |
| `train/labels/` | YOLO-format training annotations |
| `valid/images/` | Validation images |
| `valid/labels/` | YOLO-format validation annotations |
| `test/images/` | Test images |
| `test/labels/` | YOLO-format test annotations |
| `data.yaml` | Dataset paths and class mapping |
| `metadata.csv` | Image, split, class, and normalized bounding-box metadata |

Each YOLO label line represents an object in the form:

```text
class_id x_center y_center width height
```

The bounding-box values are normalized to the image dimensions and lie in the range `[0, 1]`.

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/tarekrahamn/PolyNex.git
cd PolyNex
```

### 2. Obtain the dataset

Use the dataset archive or download location linked by the project maintainers. After extraction, place the dataset in the expected directory structure and check the paths and class mapping in `data.yaml`.

> The paper identifies a separate **PolyNex Dataset Repository**, but does not specify its direct URL in the manuscript text. Add the verified dataset-download URL here when it is available.

### 3. Set up an environment

The experiments use YOLO-family object detectors. Install the framework and dependencies required by the implementation you intend to run. For an Ultralytics-based workflow:

```bash
python -m venv .venv
```

Activate the environment:

```bash
# Linux / macOS
source .venv/bin/activate

# Windows PowerShell
.venv\Scripts\Activate.ps1
```

Install the relevant package:

```bash
pip install ultralytics
```

> **Reproducibility:** Exact training commands, package versions, hardware specifications, and model-specific configuration should be taken from the corresponding implementation files. Confirm compatibility with the selected YOLO architecture before running experiments.

## 🧪 Benchmark Results

Three YOLO-family detectors were evaluated using the PolyNex dataset: YOLOv11s, YOLOv12s, and YOLO26s. The following results are from the **test split** reported in the paper.

| Model | Precision | Recall | F1-score | mAP@50 | mAP@50–95 | Inference (ms/image) |
|---|---:|---:|---:|---:|---:|---:|
| YOLOv11s | 0.8801 | 0.7991 | 0.8330 | 0.8606 | 0.6232 | 12.2104 |
| YOLOv12s | **0.9113** | 0.7724 | 0.8313 | 0.8565 | 0.6339 | 16.6833 |
| YOLO26s | 0.8951 | **0.8555** | **0.8734** | **0.8792** | **0.6438** | **12.1574** |

YOLO26s achieved the strongest test-set recall, F1-score, mAP@50, and mAP@50–95, while also recording the lowest inference time among the evaluated models. YOLOv12s achieved the highest precision.

### YOLO26s class-wise test performance

| Category | Precision | Recall | F1-score | mAP@50 |
|---|---:|---:|---:|---:|
| Construction Waste | 0.9317 | 0.8929 | 0.9119 | 0.8950 |
| Food and Organic Waste | 0.7510 | 0.5763 | 0.6521 | 0.6181 |
| Metal Scrap Waste | 0.8550 | 0.8043 | 0.8289 | 0.8456 |
| Plastic Waste | 0.9046 | 0.9074 | 0.9060 | 0.9487 |
| Polythene Waste | 0.8955 | 0.9344 | 0.9145 | 0.9139 |
| Aluminium Waste | 0.9457 | 0.9024 | 0.9236 | 0.9484 |
| Electrical Waste | 0.9825 | 0.9706 | 0.9765 | 0.9846 |
| **Overall** | **0.8951** | **0.8555** | **0.8734** | **0.8792** |

**Observation:** Food and Organic Waste was the most challenging category in the reported YOLO26s evaluation, while Electrical Waste achieved the highest class-wise mAP@50.

## 🔬 Potential Research Applications

PolyNex can support research on:

- Multiclass waste object detection and localization
- Benchmarking YOLO, CNN-based, and Transformer-based detectors
- Class imbalance and data augmentation
- Robustness to illumination, viewpoint, and background variation
- Domain generalization and transfer learning
- Automated waste monitoring and intelligent recycling
- Smart-city environmental assessment and waste mapping

## 📚 Repository & Resources

| Resource | Link |
|---|---|
| Code and implementation | [github.com/tarekrahamn/PolyNex](https://github.com/tarekrahamn/PolyNex) |
| Dataset archive | Add the verified dataset repository/download URL |
| Research manuscript | Add the paper URL when publicly available |

## 📝 Citation

If you use PolyNex in your research, please cite the associated paper. The manuscript title and author list are provided below; add the final publication details or DOI when available.

```text
Rahman, T., Roy, A., Ghosh, B., & Morol, M. K.
Towards Robust Waste Recognition: An Object-Level Annotated
Multiclass Waste Image Dataset for Comprehensive Deep
Learning-Based Detection Benchmarking and Performance Analysis
Across Diverse Real-World Waste Categories.
```

## ⚖️ License & Usage

Please refer to the dataset repository for the applicable dataset license and usage conditions. The manuscript does not specify a license, so no reuse or redistribution license is asserted here.

For research use, retain the dataset attribution and cite the associated work. Do not redistribute the dataset unless its license or the maintainers explicitly permit redistribution.

## 🤝 Acknowledgements

PolyNex was developed through collaborative field data collection, image screening, annotation, and model evaluation. We acknowledge the contributors involved in collecting and preparing the dataset.

## 👥 Authors

- **Tarek Rahman** — Corresponding Author
- Akash Roy
- Badhan Ghosh
- Md Kishor Morol

For questions about the dataset or implementation, please open an issue in the [GitHub repository](https://github.com/tarekrahamn/PolyNex).

---

<div align="center">

**PolyNex — Supporting research toward more robust, data-driven waste recognition.**

</div>
