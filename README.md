# Spaceship Titanic (Kaggle Competition)

## Objective
Predict which passengers were "transported to an alternate dimension" during the Spaceship Titanic's collision with a spacetime anomaly — a binary classification problem (`Transported`: True/False).

## Dataset
- **Source:** [Kaggle — Spaceship Titanic](https://www.kaggle.com/competitions/spaceship-titanic)
- **Train set:** 8,693 passengers × 14 columns.
- **Test set:** 4,277 passengers × 13 columns (no `Transported` label — used for the Kaggle submission).
- **Features:** `HomePlanet`, `CryoSleep`, `Cabin` (deck/number/side), `Destination`, `Age`, `VIP`, spending across 5 onboard services (`RoomService`, `FoodCourt`, `ShoppingMall`, `Spa`, `VRDeck`), and `Name`.

## Data Cleaning & Preparation
- **Missing values**, handled by column type:
  - **Mean** — used for the 5 spending columns (financial values), after converting them from `int` to `float`.
  - **Median** — used for `Age`, more appropriate than the mean given its distribution.
  - **Mode** — used for columns with only a few possible categories.
- **Encoding:**
  - `OneHotEncoder` for binary/low-cardinality categorical columns.
  - Custom function mapping Boolean columns to 0/1.
  - `LabelEncoder` for higher-cardinality columns (e.g. `Cab_Num`), where One-Hot would have been too costly and less clear.
- **Feature engineering:** `Cabin` was split into 3 new columns (deck, number, side) using `str.split()`, since the original combined field mixed three different pieces of information.
- **Scaling:** the 5 spending columns were on a very different scale from the rest of the data — `StandardScaler` was applied to correct this before modelling.

## Key Visualisations
- Correlation heatmap across all processed features — built to check for strong relationships worth exploring further; **no strong correlations were found**, meaning no single feature stands out as an obvious predictor on its own.
- Distribution/scale plots (matplotlib/seaborn) used to confirm the spending columns needed scaling before modelling.

## Modelling & Results
Three algorithms were tried first with a standard train/test split, then re-tuned using `KFold` cross-validation + `GridSearchCV`. Accuracy is the **actual Kaggle leaderboard score** for each submission:

| Model | Kaggle Score (baseline) | Kaggle Score (with GridSearchCV) |
|---|---|---|
| Logistic Regression | 0.79424 | 0.79448 |
| Random Forest | 0.79237 | **0.79869** |
| MLP Classifier | 0.78559 | 0.79611 |

**Best model: Random Forest with GridSearchCV — 0.79869.**

## Results & Limitations
- All three algorithms landed within a narrow band (~0.785–0.799) — this dataset doesn't have one standout "easy" signal, consistent with the heatmap showing no strong individual correlations.
- Hyperparameter tuning via GridSearchCV improved every model, most notably Random Forest (+0.63 points) and MLP (+1.05 points), confirming the baseline configurations were leaving accuracy on the table.
- Since no feature showed a strong individual correlation with the target, further gains would likely come from feature interactions or additional feature engineering (e.g. total spend, group size from `PassengerId`) rather than more hyperparameter tuning alone.

## Conclusion
With no single dominant predictor in the data, model choice and tuning mattered more than feature selection here — Random Forest with proper hyperparameter search was the most effective approach, edging out both Logistic Regression and a Neural Network (MLP).

## Files in this repository

| File | Description |
|---|---|
| [`Space_Titanic.ipynb`](./Space_Titanic.ipynb) | Full analysis notebook — cleaning, encoding, scaling, modelling and GridSearchCV tuning |
| [`train.csv`](./train.csv) | Training set (8,693 passengers, labelled) |
| [`test.csv`](./test.csv) | Test set (4,277 passengers, for Kaggle submission) |
