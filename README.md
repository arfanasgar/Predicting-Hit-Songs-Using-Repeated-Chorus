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

The main files used for this experiment are:

- `README.md` — project overview, setup, and usage instructions.
- `Chorus_Model.ipynb` — notebook containing feature preparation, model training, evaluation, and plots.
- `feature_extract_04.csv` — precomputed dataset used by the notebook.
- `model_results.csv` — exported model metrics from the current six-model run, if present.
- `PES1UG24AM163_PES1UG25AM807.pdf` — project report, if included in the submission.
- `PES1UG24AM163_PES1UG25AM807.pptx` — project presentation, if included in the submission.

Intermediate CSVs and the data-scraping notebook may be included for documenting earlier processing steps, but they are not required to run the main modelling notebook if `feature_extract_04.csv` is available.

## Setup

### Option A: Run in Google Colab

1. Open `Chorus_Model.ipynb` in Google Colab.
2. Upload `feature_extract_04.csv` to the Colab session, or mount Google Drive and place the CSV at the path expected by the notebook.
3. Check the notebook's data-loading cell and make sure its path points to `feature_extract_04.csv`.
4. Run the cells from top to bottom.

If a cell reports that a Python package is missing, install the package named in the error in a Colab cell using `!pip install package-name`, then rerun the failed cell and subsequent cells.

### Option B: Run locally with Jupyter

Requirements:
- Python 3.10 or a compatible Python version supported by the installed packages
- Jupyter Notebook or JupyterLab
- The dataset file `feature_extract_04.csv`

From the project directory, create and activate a virtual environment if desired.

**Windows (PowerShell):**

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install jupyter pandas numpy matplotlib seaborn scikit-learn pca
jupyter notebook
```

**macOS / Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install jupyter pandas numpy matplotlib seaborn scikit-learn pca
jupyter notebook
```

Open `Chorus_Model.ipynb` in the Jupyter interface. Keep `feature_extract_04.csv` in the directory expected by the notebook, or update the file path in the data-loading cell.

> Package versions may affect execution. If the notebook reports a missing dependency, install that dependency in the active environment and restart the kernel if necessary.

## Usage

1. Ensure `feature_extract_04.csv` is available at the path used by the notebook.
2. Open `Chorus_Model.ipynb`.
3. Run all cells in order. The notebook prepares the features, creates the train/test split, trains six classifiers, and calculates evaluation metrics.
4. Review the result table and plots for training and test accuracy, precision, recall, and F1 score.
5. The main results cell exports the current six-model table to `model_results_6_models.csv`. If your repository uses the filename `model_results.csv`, ensure it is generated from the same current six-model results rather than an older run.

### Models evaluated

- Logistic Regression
- Linear Discriminant Analysis (LDA)
- Support Vector Machine (SVM, RBF kernel)
- Random Forest
- Gradient Boosting
- Multi-Layer Perceptron (MLP) neural network

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
- Tune model hyperparameters and report mean scores and variability.
- Keep notebook outputs, plots, and exported result files synchronized.
