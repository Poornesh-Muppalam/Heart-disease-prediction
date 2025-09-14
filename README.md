# Heart Disease Prediction

## Project Description

This project provides a **machine learning workflow** for predicting the presence of heart disease based on clinical patient data. Using structured medical records, it demonstrates end-to-end data science: **data cleaning, exploratory analysis, feature engineering, modeling, and evaluation**. The goal is to identify patients at risk for heart disease using accessible clinical features.

## Features

- **Data Preprocessing**:  
  Handles missing values, drops irrelevant columns, and encodes categorical features.
- **Exploratory Data Analysis**:  
  Visualizes target distribution, variable correlations, and feature relationships.
- **Feature Engineering**:  
  Normalizes numeric features and one-hot encodes categorical variables for modeling.
- **Model Training**:  
  Implements **logistic regression** and **random forest** classifiers.
- **Model Evaluation**:  
  Provides detailed metrics: accuracy, precision, recall, F1-score, AUC-ROC, and error rate.
- **Visualization**:  
  Generates histograms, boxplots, and correlation heatmaps for deeper insights.

## Dataset

The dataset used includes **demographic, symptomatic, and diagnostic features** such as age, sex, chest pain type, blood pressure, cholesterol, ECG results, exercise-induced angina, and more. The target is a binary indicator where `1` indicates the presence of heart disease, `0` its absence.

## Requirements

To run this project, you need:

- Python 3.x
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- Google Colab (for `.ipynb` execution; optional for local use)

Install dependencies with:

