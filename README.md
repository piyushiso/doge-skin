# DogeSkin: Dog Skin Disease Image Classification

## Project Overview

DogeSkin is a machine learning project for dog skin disease image classification. The goal of this project is to compare different machine learning and deep learning-based approaches for classifying dog skin disease images.

This project focuses on evaluating whether CNN-based feature extraction can improve image classification performance compared to raw pixel-based features.

This system is designed for preliminary image-based screening support only. It is not a replacement for professional veterinary diagnosis.

## Research Question

Do pretrained CNN-extracted features improve dog skin disease image classification performance compared to raw pixel features across traditional machine learning algorithms?

## Dataset

The project uses a public dog skin disease image dataset from Kaggle.

The dataset is organized into training, validation, and testing folders. Each folder contains class-specific subfolders for different dog skin disease categories.

The main disease classes used in this project include:

```text
Demodicosis
Dermatitis
Fungal Infections
Healthy
Hypersensitivity
Ringworm
```

## Project Folder Structure

```text
doge-skin/
├── datasets/
│   ├── feed/
│   │   ├── train/
│   │   ├── valid/
│   │   └── test/
│   └── real/
|       ├── labelled/
│       └── unlabelled/
├── notebooks/
│   └── doge_skin.ipynb
├── lightweight/
│   ├── doge_skin.html
│   └── doge_skin.pdf
├── outputs/
│   ├── features/
│   ├── results/
│   ├── models/
│   └── figures/
└── README.md
```

## Lightweight Viewing Files

The full notebook contains many outputs, charts, confusion matrices, prediction images, and model evaluation results. Because of this, the notebook file may be too large to preview directly on GitHub or nbviewer.

To make the project easier to review, exported lightweight viewing files are provided inside the `lightweight/` folder.

```text
doge-skin/
├── lightweight/
│   ├── doge_skin.html
│   └── doge_skin.pdf
```

## How to Review the Project

For the best viewing experience, open:

```text
lightweight/doge_skin.html
```