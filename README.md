# ML-music-popularity-predictor
Kaggle Prediction Competition - Spotify Past Decades Songs (September 2020) 

## Introduction / project context
This project comes from a Kaggle competition with purposes to find the secret sauce to make a song popular. 
Two questions have been raised by this project: Why do we like some songs more than others? Is there something about a song that pleases out subconscious, making us listening to it on repeat? 
To understand this, the project instructor collected various attributes from a selection of songs available in the Spotify's playlist "All out ..s" starting from the 50s up to the newly ended 10s. We present a model that can predict how likely a song will be a hit, defined by making it on Billboard’s Top 100, with over 68% accuracy for popular songs and 74% for non-popular songs.

# Data collection and preprocessing : Acquiring the data
This data repo contains 7 datasets (.csv files) Those playlists collect the most popular/iconic songs from the decade. For each song, a set of attributes have been reported in order to perform some data analysis.
Every song in the dataset contains 14 features categorized by audio analysis, artist information, and song related features.
Audio analysis features: Beat per minute, duration_ms, energy, danceability, liveness, valence, acousticness, speechiness, loudness (dB)
Artist related features: artist name
Song related features: releases_year, title, genre, popularity
The dataset has been provided on Kaggle for the competition purpose, The attributes have been scraped from this amazing website : http://organizeyourmusic.playlistmachinery.com/

# Data collection and preprocessing : cleaning dataset
Dropping some features : ‘Number’, ‘Title’,’Artist’
Transform ‘year’ into a categorical variable with seven values : fifty’s, sixty’s, seventy’s, eighty’s, ninety’s, twenty’s
Transform ‘top genre’ from 101 distinct values to 4 distinct values :
Transform ‘popularity into 2 classes’ based on conditionality : if pop >= 66 class 1, else class 0. After this transform we get 330 instances for class 0 and 337 events for class 1
Missing values imputation:
The following features had respectively 10 missing values: title, artist, bpm, nrgy, dnce, dB, live, val, dur, acous, spch, pop
Data missing imputation use TransformerMixin:
def __init__(self):
"""Impute missing values.
        Columns of dtype object are imputed with the most frequent value 
        in column.
        Columns of other types are imputed with mean of column.
        
# Data scaling and transform
Data scaling using Normal scaler through RobustScaler for the numeric features and OneHotEncoding for the categorical ones.
# Define which columns should be encoded vs scaled
columns_to_encode = ['top genre']
columns_to_scale  = ['bpm', 'nrgy','dnce','dB','live','val','dur','acous','spch’]
This step has been done separately on Training and test dataset.

# Data exploration : Feature engineering
Split out validation dataset: transform our data separately from training and test
Feature importance: random forest for feature importance on a classification problem
RFE for Feature Selection
In order to select the most relevant feature in predicting our target variable 'popularity', we will use the Recursive Feature Elimination. As we aim to automatically select the number of Features chosen by RFE, we will perform cross-validation evaluation of different numbers of features, and automatically selecting the number of features that resulted in the best mean score. We will refer to the RFECV class.

# Model Selection and Tuning
Spot-check classification algorithms:
Spot-checking is a way of discovering which algorithms perform well on your machine learning, as we cannot know which algorithms are best suited to the problem beforehand. What algorithms should I spot-check on my dataset?
Evaluate Algorithms : Baseline
Let's design our test harness. We will use 10-fold cross-validation. The dataset is not too small and this is a good standard test harness configuration. We will evaluate algorithms using the accuracy metric. This is a gross metric that will give a quick idea of how correct a given model is.

