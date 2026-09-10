# **A Ruff Case of Classification**

## **Raw Pixels vs. Deep CNN Features for Dog Skin Conditions**

DogeSkin is an academic machine-learning project that compares raw image pixels with pretrained CNN features for multiclass dog skin-condition image classification.

The central question is:

> Do pretrained MobileNetV2 features provide a stronger representation than low-resolution raw pixels when the same conventional classifiers are used?

The project is intended for comparative experimentation and preliminary screening research. It is not a veterinary diagnostic tool.

## **Target Classes**

The main dataset contains six classes:

- Demodicosis
- Dermatitis
- Fungal Infections
- Healthy
- Hypersensitivity
- Ringworm

## **Experiments**

| Experiment | Image representation | Classifier stage |
|---|---|---|
| 1. Raw-pixel baseline | 64 x 64 grayscale images flattened into 4,096 normalized values | Logistic Regression, k-NN, Decision Tree, Random Forest, SVM, and MLP |
| 2. Fixed CNN features | 224 x 224 RGB images transformed into 1,280-dimensional MobileNetV2 embeddings | The same six conventional classifiers |
| 3. Frozen-backbone transfer learning | 224 x 224 RGB images processed by a frozen MobileNetV2 backbone | Trainable dense head with dropout and six-class softmax output |

Experiments 1 and 2 used stratified five-fold cross-validation for model comparison. Selected models were then evaluated on the held-out test set.

## **Main Results**

| Approach | Test accuracy | Macro precision | Macro recall | Macro F1-score |
|---|---:|---:|---:|---:|
| Raw pixels with Random Forest | 0.6328 | 0.6566 | 0.5583 | 0.5642 |
| MobileNetV2 features with MLP | **0.9169** | **0.9002** | **0.8837** | **0.8904** |
| Frozen MobileNetV2 with dense head | 0.8822 | 0.8613 | 0.8547 | 0.8570 |

MobileNetV2 features followed by MLP produced the strongest completed result, correctly classifying 397 of 433 held-out test images.

These values describe performance on the available project datasets only. They do not establish clinical reliability.

## **Repository Structure**

```text
doge-skin/
├── datasets/
│   ├── feed/                     # Main dataset, downloaded separately
│   │   ├── train/
│   │   ├── valid/
│   │   └── test/
│   └── real/
│       ├── labelled/             # Secondary dataset, downloaded separately
│       └── unlabelled/           # Author-collected phone images
├── lightweight/
│   ├── doge_skin.html
│   └── doge_skin.pdf
├── notebooks/
│   └── doge_skin.ipynb
├── outputs/
│   ├── features/
│   ├── figures/
│   ├── models/
│   └── results/
├── report/                       # Final paper stored in the private submission
├── compressed/                   # Private coursework package, ignored by Git
├── .gitignore
└── README.md
```

The public repository intentionally excludes the complete labelled datasets, final submission package, final report PDF, large feature arrays, trained models, and local copies of referenced publications.

## **Datasets**

### **Main labelled dataset**

[Dogs Skin Diseases Image Dataset](https://www.kaggle.com/datasets/youssefmohmmed/dogs-skin-diseases-image-dataset/data)

After downloading, place the split folders directly under `datasets/feed/`:

```text
datasets/feed/train/
datasets/feed/valid/
datasets/feed/test/
```

Each split must contain these folder names:

```text
Dermatitis/
Fungal Infections/
Healthy/
Hypersensitivity/
demodicosis/
ringworm/
```

Do not leave another directory between `feed/` and the three split folders.

The original collection contained 4,315 images. Exact MD5 duplicate inspection identified 4,233 unique files. Experiments 1 and 2 used a cleaned development set of 3,800 images and a held-out test set of 433 images.

### **Secondary labelled dataset**

[Dogs Skin Disease Dataset](https://www.kaggle.com/datasets/yashmotiani/dogs-skin-disease-dataset)

Only the relevant classes were retained for the external check. Arrange them using these exact paths:

```text
datasets/real/labelled/Dermatitis/
datasets/real/labelled/Fungal Infections/
datasets/real/labelled/Healthy/
datasets/real/labelled/Hypersensitivity/
```

This collection does not contain actual examples for all six target classes. Its result is therefore an exploratory external check, not complete six-class validation.

### **Author-collected unlabelled images**

The phone images are available at:

```text
datasets/real/unlabelled/
```

These images do not have veterinarian-confirmed labels. They are used only to inspect predictions and confidence behaviour. Classification accuracy cannot be calculated without ground-truth labels.

## **Installation**

Python 3.10 or 3.11 is recommended. Create and activate a virtual environment before installing the dependencies.

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install jupyter tensorflow numpy pandas pillow matplotlib seaborn scikit-learn joblib
```

On Windows, activate the environment with:

```powershell
.venv\Scripts\activate
```

TensorFlow compatibility varies by operating system, Python version, and hardware. The first MobileNetV2 run may require internet access to download ImageNet weights.

## **Running the Notebook**

Clone the repository:

```bash
git clone https://github.com/piyushiso/doge-skin.git
cd doge-skin
```

Download and arrange both labelled datasets using the paths above. Start Jupyter from the notebook directory so that relative paths such as `../datasets/feed` and `../outputs` resolve correctly:

```bash
cd notebooks
jupyter notebook doge_skin.ipynb
```

Run the notebook cells from top to bottom. A full execution can take substantial time because it includes duplicate inspection, image preprocessing, feature generation, five-fold cross-validation, final model fitting, transfer-learning training, and external-image prediction.

## **Viewing the Completed Outputs**

The checked notebook has its outputs cleared to keep the repository and submission manageable. The original visual outputs are preserved in:

```text
lightweight/doge_skin.pdf
```

This PDF contains the recorded tables, figures, confusion matrices, training history, and prediction examples. The HTML export may provide a more interactive local view but is considerably larger.

## **Reproducibility Notes**

- Experiments 1 and 2 use exact-duplicate-cleaned development data.
- Experiment 3 reloads the original folder splits, so it is not a perfectly controlled comparison with Experiments 1 and 2.
- The MobileNetV2 backbone in Experiment 3 is frozen. Only the added classification head is trained.
- The 20-epoch value is a resource-aware training limit, not a proven optimal epoch count.
- The secondary labelled dataset contains only four target classes.
- The phone-image collection is unlabelled and cannot provide an accuracy measurement.
- The public dataset labels were not independently confirmed by veterinary specialists.

## **Project Resources**

- [Main DogeSkin repository](https://github.com/piyushiso/doge-skin)
- [Notebook](https://github.com/piyushiso/doge-skin/blob/master/notebooks/doge_skin.ipynb)
- [Visual-output PDF](https://github.com/piyushiso/doge-skin/blob/master/lightweight/doge_skin.pdf)
- [Unlabelled phone images](https://github.com/piyushiso/doge-skin/tree/master/datasets/real/unlabelled)

## **Previous Project Attempt**

The earlier [pest-classifier repository](https://github.com/piyushiso/pest-classifier) documents the initial project direction. That attempt was discontinued because the available pest dataset was unsuitable for the intended evaluation and appropriate real-world test images were difficult to obtain.

The pest-classifier data, models, and results are not used in DogeSkin.

## **Coursework Submission**

The private coursework archive contains the final paper, output-cleared notebook, visual-output PDF, author-collected images, selected reference papers, and a short submission README.

The required filename format is:

```text
ML_Project_StudentID_Name.zip
```

The `compressed/` directory is ignored by Git and should be uploaded only through the institution's submission system.

## **Ethical Notice**

Dog skin conditions can appear visually similar, and a photograph does not contain clinical history, laboratory findings, microscopy, culture results, or other information used by veterinarians. Predictions from this project must not be interpreted as medical diagnoses or treatment recommendations.
