# Movie Recommendation System

## Overview
The primary objective of this project is to develop an efficient and accurate movie recommendation system (a collaborative filtering machine learning model) using SVD. The system aims to predict movie ratings for users and generate a list of top movie recommendations for each user.

## Dataset
The project uses two datasets: one containing movie titles and movie IDs (check inside the data folder), and another containing movie IDs, user IDs, and movie ratings by the users.  
[Get that latter dataset here](https://drive.google.com/file/d/1LsAMPUQRHtLqlAn6YHYEmoxMAy4rdfrC/view?usp=sharing)

## EDA & Data Cleaning Key Steps
- Initially, the movie ratings dataset did not contain any headers. The first column contains IDs, the second column contains ratings, and the third column contains dates.
- The dataset is re-imported with appropriate headers ('UserID', 'Rating') and without the date column.
- There were 4499 null values present in this dataset. Upon observation, it was found that these rows containing null values in ratings and values from 1 to 4499 in order inside 'UserID' are actually our movie IDs.
- Accordingly, a 'MovieID' column was created where the 'Rating' is NaN, extracting the number from 'UserID'.
- Since all the UserID and ratings for each MovieID were in ascending order in the dataset, fillna() was used with the forward fill method to fill NaN values in 'MovieID' with the preceding value.
- Finally, the rows with NaN values in 'Rating' were dropped to get the cleaned dataset.

## Data Preprocessing
- The goal is to prepare a dataset for training a recommendation model, ensuring high-quality training data by excluding movies with very few ratings and users who have rated only a few movies.
- By focusing on items and users with sufficient data, the model can learn more meaningful patterns and preferences.
- To ensure sufficient data quality, we set a benchmark where only the top 70% of movies (by the number of ratings) and the top 70% of users (by the number of ratings given) will be considered.
- After preprocessing, the final number of ratings was 17,337,458 (rather than the initial 24,053,764) from 43,458 unique users and 1,350 unique movies.

## Model Building
- The collaborative filtering model was trained using the Singular Value Decomposition (SVD) algorithm from the Scikit-Surprise library.
- The dataset is loaded into a format suitable for training models using the Dataset class, and the Reader class ensures the dataset is compatible with the SVD model.
- An SVD model is initialized and K-fold cross-validation (5-fold) is performed using the initialized SVD model. This involves splitting the data into 5 subsets and evaluating the model on each subset. The performance is measured using RMSE and MAE, with results indicating good performance due to low error values.
- The model is then trained on the entire dataset to ensure it has learned from all available data.
- Predictions are made for the unseen movies for a particular user, resulting in a list of predicted ratings. These predictions are organized into a DataFrame and sorted by estimated ratings to identify the top recommended movies for the user.
- For a given user, the model identifies other users who are similar based on their historical interactions with the movies. The model then predicts the rating that the current user might give to an unrated item by considering the ratings given by similar users to that item.
- The resultant DataFrame is merged with the movies titles table to display movie names alongside the predicted ratings for better interpretability.
