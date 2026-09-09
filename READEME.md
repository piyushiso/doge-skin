# DogeSkin: Dog Skin Disease Image Classification

## Project Overview

DogeSkin is a machine learning project for dog skin disease image classification. The goal of this project is to compare different machine learning and deep learning-based approaches for classifying dog skin disease images.

This system is designed for preliminary image-based screening support only. It is not a replacement for professional veterinary diagnosis.

## Research Question

Do pretrained CNN-extracted features improve dog skin disease image classification performance compared to raw pixel features across traditional machine learning algorithms?

## Dataset

The project uses a public dog skin disease image dataset from Kaggle.

The dataset contains dog skin images organized into train, validation, and test folders. Each folder contains class-specific subfolders.

## Project Folder Structure

```text
doge-skin/
├── datasets/
│   ├── feed/
│   │   ├── train/
│   │   ├── valid/
│   │   └── test/
│   └── real/
│       └── unlabelled/
├── notebooks/
│   └── doge_skin.ipynb
├── outputs/
│   ├── features/
│   ├── results/
│   ├── models/
│   └── figures/
└── README.md