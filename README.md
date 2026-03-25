# Heart Disease Prediction Using Machine Learning

A machine learning project that predicts whether a patient has heart disease based on clinical health records. Built as part of the CSC 5800 Intelligent Systems course at Wayne State University (April 2025).

## What This Project Does

Heart disease is one of the leading causes of death worldwide. Early detection through patient health data can help doctors intervene sooner and save lives. This project takes routinely collected clinical data like age, blood pressure, cholesterol levels, and chest pain type, and uses it to predict the presence of heart disease.

Two models were trained and compared: **Logistic Regression** as a simple, interpretable baseline and **Random Forest** as a more powerful ensemble approach. After tuning, the Random Forest model came out on top with **87% test accuracy** and an **AUC of 0.90**.

## Dataset

The dataset is a refined version of the [UCI Heart Disease dataset](https://archive.ics.uci.edu/ml/datasets/heart+Disease), compiled from multiple medical sources and made publicly available on Kaggle. It contains **920 patient records** with the following features:

| Feature    | Description                                      |
|------------|--------------------------------------------------|
| age        | Age of the patient in years                      |
| sex        | 1 = male, 0 = female                             |
| cp         | Chest pain type (4 categories)                   |
| trestbps   | Resting blood pressure (mm Hg)                   |
| chol       | Serum cholesterol (mg/dl)                         |
| fbs        | Fasting blood sugar > 120 mg/dl (1 = yes, 0 = no)|
| restecg    | Resting electrocardiographic results              |
| thalach    | Maximum heart rate achieved                       |
| exang      | Exercise induced angina (1 = yes, 0 = no)         |
| oldpeak    | ST depression induced by exercise                 |
| slope      | Slope of the peak exercise ST segment             |

The target variable (`num`) was converted to binary: **0** means no heart disease, **1** means heart disease is present.

## How It Works

### Data Cleaning and Preprocessing

Before training any models, the data went through a careful preprocessing pipeline:

1. **Dropped columns with too many missing values** (`ca`, `thal`) and redundant metadata columns (`id`, `dataset`)
2. **Filled remaining missing values** using median for numeric columns and mode for categorical columns
3. **Converted the target variable** from multiclass severity levels to a simple binary (0 or 1)
4. **One hot encoded** categorical features like chest pain type, resting ECG, and exercise induced angina
5. **Standardized numeric features** (age, blood pressure, cholesterol, max heart rate, oldpeak) using `StandardScaler` so that scale sensitive algorithms perform correctly

### Exploratory Data Analysis

Several visualizations were created to understand the data before modeling:

**Target distribution** showed a slight class imbalance, with more heart disease cases than healthy ones, but not severe enough to require oversampling.

**Histograms** of age and cholesterol revealed that age follows a roughly normal distribution centered around 50 to 60 years, while cholesterol is positively skewed with most values between 200 and 250 mg/dl.

**Boxplots** comparing features across the two classes showed that `oldpeak` (ST depression) tends to be higher in heart disease patients, and `thalach` (max heart rate) tends to be lower. Meanwhile, age, cholesterol, and resting blood pressure didn't show strong separation on their own.

**Correlation heatmap** confirmed that `thalach` has the strongest negative correlation with the target, and `oldpeak` has the strongest positive correlation. No multicollinearity issues were found among the predictors.

### Model Training

Two classifiers were trained using an 80/20 train test split:

**Logistic Regression** with `max_iter=1000` to ensure convergence after scaling.

**Random Forest Classifier** with tuned hyperparameters:
  * `n_estimators=100` (number of trees)
  * `max_depth=5` (prevents overfitting)
  * `min_samples_leaf=5` (ensures robustness at leaf nodes)

The initial Random Forest model had near perfect training accuracy, which was a clear sign of overfitting. After applying the hyperparameter constraints above, the gap between training and test performance narrowed significantly.

## Results

| Metric           | Logistic Regression | Random Forest |
|------------------|---------------------|---------------|
| Train Accuracy   | 82%                 | 84%           |
| Test Accuracy    | 80%                 | 87%           |
| Train AUC        | 0.89                | 0.92          |
| Test AUC         | 0.88                | 0.90          |
| Train F1 (class 1) | 0.83              | 0.86          |
| Test F1 (class 1)  | 0.83              | 0.89          |
| Error Rate       | 0.2011              | 0.1304        |

The ROC curve comparison showed that Random Forest consistently achieved a higher true positive rate across all thresholds.

**Bottom line:** The tuned Random Forest model outperformed Logistic Regression on every metric. It strikes a solid balance between bias and variance, making it well suited for real world health screening applications.

## Tech Stack

* **Language:** Python
* **Libraries:** pandas, NumPy, scikit learn, seaborn, matplotlib
* **Environment:** Google Colab
* **Dataset source:** UCI Heart Disease dataset via Kaggle

## Project Structure

```
.
├── Final_Heart_disease_prediction.ipynb   # Full notebook with code and outputs
├── Poornesh_IS_Project_report.pdf         # Detailed project report
├── README.md                              # You're reading it
```

## How to Run

1. Open `Final_Heart_disease_prediction.ipynb` in Google Colab (or any Jupyter environment)
2. Upload the heart disease CSV dataset when prompted
3. Run all cells sequentially

The notebook handles everything from data loading and cleaning through model training, evaluation, and visualization.

## Key Takeaways

* Random Forest significantly outperforms Logistic Regression for this task after proper tuning
* `thalach` (max heart rate) and `oldpeak` (ST depression) are the most predictive features
* Overfitting in tree based models can be effectively controlled through depth limits and leaf size constraints
* Even with a relatively small dataset (920 records), meaningful predictive power is achievable

## References

1. Detrano, R., et al. (1989). *International application of a new probability algorithm for the diagnosis of coronary artery disease.* American Journal of Cardiology, 64, 304–310.
2. Aha, D.W. & Kibler, D. *Instance based prediction of heart disease presence with the Cleveland database.*
3. Gennari, J.H., Langley, P., & Fisher, D. (1989). *Models of incremental concept formation.* Artificial Intelligence, 40, 11–61.

## Author

**Poornesh Muppalam**
MS in Computer Science, Wayne State University
