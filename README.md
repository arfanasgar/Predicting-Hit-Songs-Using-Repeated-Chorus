# Predicting Hit Songs Using Repeated Chorus

## Project Overview

This project explores whether audio features extracted from a song's repeated chorus can help classify the song as a hit or non-hit. It uses precomputed chorus-based audio features and machine-learning classifiers to compare predictive performance.

## Objective

The project investigates whether repeated-chorus audio characteristics can help distinguish hit songs from non-hit songs.

The workflow covered by the current notebook includes:
- Loading a dataset of chorus-based audio features.
- Exploring the feature space and performing PCA-based feature selection.
- Splitting the data into training and test sets.
- Training and evaluating multiple classification models.
- Comparing accuracy, precision, recall, and F1 score.

## Dataset

The working dataset used in the notebook is `feature_extract_04.csv`.

The current file contains:
- **756 songs**
- **518 numerical audio features**
- A binary `Label` target, where `1` represents a hit and `0` represents a non-hit.

The dataset also includes metadata columns such as artist and title, along with audio-file path fields. The path fields and non-numeric metadata are not used as model inputs.

> Dataset note: these figures describe the dataset currently used by this notebook. They may differ from datasets used in other versions of the project.

## Audio Features

The feature set contains numerical descriptors of audio characteristics, including groups such as:
- Chroma features
- Mel-frequency cepstral coefficients (MFCCs)
- Root-mean-square (RMS) energy
- Spectral centroid, bandwidth, contrast, and rolloff
- Tonnetz features
- Zero-crossing rate

The notebook uses precomputed features; it does not currently reproduce the full audio collection and chorus-extraction pipeline from raw songs.

## Modelling Workflow

1. **Load data:** Read the feature dataset and separate the target label from metadata and file-path columns.
2. **Feature selection:** Use the notebook's PCA-based exploratory workflow to select features.
3. **Train/test split:** Use an 80/20 split with `random_state=2022`.
4. **Model training:** Evaluate the following six classifiers:
   - Logistic Regression
   - Linear Discriminant Analysis (LDA)
   - Support Vector Machine (SVM) with an RBF kernel
   - Random Forest
   - Gradient Boosting
   - Multi-Layer Perceptron (MLP) neural network
5. **Evaluation:** Compare training and test accuracy, precision, recall, and F1 score.

## Results

In the current recorded run:
- **SVM** achieved the highest test accuracy, approximately **59.2%**.
- **MLP** achieved the highest test F1 score, approximately **0.630**.
- Random Forest and Gradient Boosting showed large training-to-test performance gaps, suggesting possible overfitting.

These results come from one train/test split and should be treated as preliminary rather than definitive.

## Limitations and Future Improvements

- The current dataset contains 756 songs and may differ from datasets used in other experiments.
- Feature selection is performed before the train/test split in the current workflow, which can introduce data leakage.
- The evaluation uses one split rather than stratified cross-validation.
- Model hyperparameters have not been comprehensively tuned.
- The raw audio collection and chorus-extraction pipeline has not been independently rerun as part of this notebook.

Recommended next steps:
- Move feature selection and preprocessing inside a training-only pipeline.
- Evaluate models with stratified cross-validation.
- Tune model hyperparameters and report mean performance and variability.
- Keep notebook outputs and exported result files synchronized.

## Repository Contents

The repository may include the notebook, dataset files, and generated result files. File availability depends on what has been included in the local project folder.

## Running the Notebook

1. Open `Chorus_Model.ipynb` in Jupyter Notebook or Google Colab.
2. Upload or place `feature_extract_04.csv` where the notebook expects it.
3. Run the notebook cells in order.
4. Review the model comparison table and evaluation plots.

Make sure the dataset filename and file paths in the notebook match your environment before running it.
