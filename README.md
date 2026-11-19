# Smart Agriculture Predictor

A notebook that trains a decision tree classifier to predict a crop label from soil nutrients and weather measurements. The implementation is in [`genesis.ipynb`](genesis.ipynb).

[![Open in Google Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/danyl-dnl/Smart-Agriculture-Predictor/blob/main/genesis.ipynb)

## How it works

1. Upload a CSV file named `Crop_recommendation.csv` in the notebook.
2. Read it into a pandas DataFrame and inspect the crop labels.
3. Encode the `label` column as numeric class IDs with scikit-learn's `LabelEncoder`.
4. Use the following seven columns as model features:

   | Feature | Description in the notebook |
   | --- | --- |
   | `N` | Nitrogen value |
   | `P` | Phosphorus value |
   | `K` | Potassium value |
   | `temperature` | Temperature measurement |
   | `humidity` | Humidity measurement |
   | `ph` | Soil pH value |
   | `rainfall` | Rainfall measurement |

5. Split the rows into training and test sets with an 80/20 split and `random_state=42`.
6. Train a `DecisionTreeClassifier` with `random_state=42` and map predicted class IDs back to crop labels.

The notebook also defines `predict_crop(N, P, K, temperature, humidity, ph, rainfall)` for predicting a crop from one set of measurements after the model has been trained.

## Dataset requirements

The CSV is not included in this repository. Upload a `Crop_recommendation.csv` containing these columns:

```text
N, P, K, temperature, humidity, ph, rainfall, label
```

Each row should contain numeric values for the seven features and a crop name in `label`. The notebook expects the exact column names shown above. Use a labeled dataset appropriate for your intended region and application.

## Run in Google Colab

1. Open `genesis.ipynb` using the Colab badge above.
2. Run the notebook cells in order.
3. When the upload dialog appears, select your `Crop_recommendation.csv` file.
4. Continue through the cells to train the model and print example predictions.

The notebook imports `google.colab.files` for file upload, so that upload cell is Colab-specific. To run locally, install `pandas` and `scikit-learn`, replace the Colab upload cell with a local file path, and make the CSV available in the working directory.

## Current scope and limitations

- The notebook trains a basic decision tree using scikit-learn's default tree settings.
- It creates an 80/20 split but does not calculate accuracy, precision, recall, a confusion matrix, or cross-validation results. It only prints the predicted labels for the first ten test rows.
- `predict_crop` returns a class label; it does not return confidence, validate input ranges, or handle missing or malformed values.
- The trained model and label encoder are not saved to disk, and the repository does not include an API or user interface.
- This is a machine-learning demonstration, not agronomic advice. Predictions depend on the training data and should be validated by qualified local agricultural guidance before use in real planting decisions.

## Repository contents

| File | Description |
| --- | --- |
| `genesis.ipynb` | Data upload, label encoding, train/test split, decision tree training, and crop prediction function |
| `README.md` | Project overview, dataset format, run instructions, and limitations |
