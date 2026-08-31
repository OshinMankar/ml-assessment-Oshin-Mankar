# Machine Learning for Retail & Customer Analytics

An end-to-end machine learning project applying supervised learning, unsupervised learning, feature engineering, regression modeling, and business-focused ML problem solving.

The project demonstrates how machine learning techniques can be used to solve classification, customer segmentation, and retail prediction problems while connecting technical model development with real-world business decisions.

---

## Project Overview

This project consists of multiple machine learning workflows designed to explore different stages of the machine learning lifecycle.

The work includes:

- Classification modeling for prediction problems
- Customer segmentation using unsupervised learning
- Feature engineering and regression pipelines
- Model evaluation and hyperparameter tuning
- PCA-based dimensionality reduction and visualization
- Business-focused machine learning strategy and deployment planning

---

# Project Components

## 1. Supervised Learning: Heart Disease Classification

Built and evaluated multiple classification models to predict whether heart disease is present based on patient attributes.

### Key Activities

- Performed exploratory data analysis and visualizations
- Handled missing values
- Applied categorical encoding and feature scaling
- Trained Decision Tree, Random Forest, and Gradient Boosting models
- Evaluated models using precision, recall, F1-score, and confusion matrices
- Applied GridSearchCV for hyperparameter tuning

### Key Learning

The project focused on selecting models using multiple evaluation metrics rather than relying only on accuracy.

---

## 2. Customer Segmentation using K-Means

Applied unsupervised machine learning to identify customer groups based on spending and purchasing behaviour.

### Key Activities

- Scaled customer features using StandardScaler
- Used the Elbow Method to identify an appropriate number of clusters
- Applied K-Means clustering
- Analyzed cluster centroids
- Interpreted customer groups from a business perspective
- Applied PCA to reduce dimensionality
- Visualized customer segments using principal components

### Business Value

Customer segmentation can support targeted marketing, personalized campaigns, and improved customer engagement strategies.

---

## 3. Retail Sales Prediction Pipeline

Developed a reproducible machine learning pipeline to predict retail store sales volume.

### Key Activities

- Engineered date-based features from transaction data
- Used a temporal train-test split to preserve time order
- Built preprocessing pipelines using ColumnTransformer
- Applied one-hot encoding and feature scaling
- Trained Linear Regression and Random Forest models
- Evaluated models using RMSE and MAE
- Created predicted vs actual parity plots
- Identified the most influential features using feature importance

### Business Value

The model can help understand the factors influencing sales volume and support data-driven retail planning.

---

## 4. Promotion Effectiveness Business Analysis

Designed a machine learning strategy for identifying suitable promotions across different retail stores.

The analysis focused on:

- Machine learning problem formulation
- Target variable selection
- Store-level and location-based modelling strategies
- Data integration and modelling dataset design
- Exploratory data analysis strategy
- Promotion imbalance considerations
- Time-based model evaluation
- Feature importance and model explainability
- Model deployment and performance monitoring

### Business Objective

Develop a data-driven approach to support promotion decisions across stores while accounting for differences in store characteristics and seasonal behaviour.

---

# Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- Jupyter Notebook

---

# Machine Learning Techniques

### Supervised Learning
- Decision Tree Classifier
- Random Forest Classifier
- Gradient Boosting Classifier

### Unsupervised Learning
- K-Means Clustering
- Principal Component Analysis (PCA)

### Regression
- Linear Regression
- Random Forest Regressor

### Machine Learning Techniques
- Feature Engineering
- One-Hot Encoding
- StandardScaler
- Pipeline
- ColumnTransformer
- GridSearchCV
- Temporal Train-Test Split
- Feature Importance Analysis

---
