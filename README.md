# Movie Recommendation System

## Overview
The primary objective of this project is to develop an efficient and accurate movie recommendation system (a collaborative filtering Machine Learning model) using SVD. The system aims to predict movie ratings for users and generate a list of top movie recommendations for each user.

## Dataset
The project uses two datasets, one containing movie titles and movie id's (check inside data folder) and another dataset containing movie id's, user id's and movie ratings by the user.  
[Get that latter dataset here](https://drive.google.com/file/d/1LsAMPUQRHtLqlAn6YHYEmoxMAy4rdfrC/view?usp=sharing)

## EDA & Data Cleaning Key Steps
- Initially the movie ratings dataset did not contain any headers. The first column contains IDs, the second column contains ratings, and the third column contains dates.
- The dataset is re-imported with appropriate headers ('UserID', 'Rating') and without the date column.
- There was 4499 null values present in this dataset. Upon observation it was found that these rows cotaining null values in ratings and values from 1 to 4499 in order inside UserID's are acutually our movie ID's.
- Accordingly created a 'MovieID' column where the 'Rating' is NaN, extracting the number from 'UserID'.
- Since all the UserID and ratings for each MovieID was ascending order in the dataset, fillna() was used with forward fill method to fill NaN values in 'MovieID' with the preceding value.
- Finally dropped the rows with NaN values in 'Rating' to get the cleaned dataset.

## Data Preprocessing
- The goal is to prepare a dataset for training a recommendation model, ensuring high-quality training data by excluding movies with very few ratings and users who have rated only a few movies.
- By focusing on items and users with sufficient data, the model can learn more meaningful patterns and preferences.
- To ensure sufficient data quality, we set a benchmark where only the top 70% of movies (by the number of ratings) and the top 70% of users (by the number of ratings given) will be considered.
- After preprocessing steps the final number of ratings were 17337458 (rather than the initial 24053764) from 43458 unique users and 1350 unique movies.

## Model Building
- The collaborative filtering model was trained using Singular Value Decomposition (SVD) algorithm from the Scikit-Surprise library
