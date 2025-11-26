# Project-Pitch-Classification-Model
For this project, we are using publicly available Major League Baseball pitch-tracking data from the Baseball Savant Statcast database, provided by MLB. It is accessible at: https://baseballsavant.mlb.com/statcast_searchnd the label represents the corresponding pitch type which we use to train the classification model.
Overview

This project builds several pitch type classifiers using MLB Statcast data. The workflow includes data cleaning, normalization, ANN and KNN models, PCA analysis, an ensemble model, and data analysis and visualization.

Data Preparation

Eight pitch types are used, with each one having a CSV file which is loaded and processed. Exactly 5000 clean rows are collected from each pitch type. Any row containing missing or invalid values is removed. The datasets are combined into one 40,000 row file saved as merged_pitch_data.csv.

Normalization

StandardScaler (z-scale) is applied to all numeric pitch features. This produces a fully normalized dataset saved as normalized_pitch_data.csv. Pitch types are encoded using LabelEncoder and one-hot encoding. The dataset is then split into training and testing sets with stratification so each pitch type is evenly represented.

ANN Model

The ANN captures non-linear interactions between pitch features. A three layer neural network is used with BatchNormalization and Dropout to stabilize training and reduce overfitting. This model reaches ~83% accuracy on the test set after being hyperparametrized.

KNN Model

A KNN classifier handles tight pitch clusters effectively using distance weighting. It performs well due to the natural clustering present in pitch physics. This model also reaches ~83% accuracy but performs better on average than the ANN.

PCA Section

PCA reduces the five primary features to two principal components. A PCA scatter plot is included to show how pitch types overlap in the reduced space. ANN and KNN models trained on PCA transformed data both drop to around 68% accuracy, showing that PCA removes important information needed to separate similar pitch types.

Ensemble Model

The ensemble combines ANN and KNN prediction probabilities using a weighted formula. The best performance uses a weight of alpha = 0.66, giving more influence to KNN. The ensemble reaches approximately 84% accuracy, with the consistently highest accuracy achieved among models. The model improves decisions on borderline predictions where ANN and KNN disagree.

Feature Engineering

The project includes correlation heatmaps, pitch movement plots, and spin-axis distribution visuals. These visualizations help explain pitch behavior and highlight where many pitch types overlap.

Clustering

KMeans clustering is used with PCA to identify natural pitch groupings without labels. The clusters match known pitch families based on movement and spin. This also explains why classifying certain pitch pairs is more challenging.

How to Run

Run the data preparation script to create merged_pitch_data.csv. Run the normalization steps to create normalized_pitch_data.csv. Open the main Jupyter notebook. Run preprocessing, then train the ANN, KNN, and PCA models. Run the ensemble model for best accuracy. Use the feature engineering sections for analysis and visualizations.
