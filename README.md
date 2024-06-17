# u2u-collaborative-filtering

## Overview
Created a reccomendation system using user-to-user collaborative filtering to suggest new movies to users. 

## Data
user_reviews.csv
- rows represent users of the system 
- columns represent products 
- cells represent a numerical rating from 1 to 5 of a product given by a user.
- value of 0 represents a missing rating—a movie the user hasn't rated yet.

movie_genres.csv
- rows represent the movies in the columns of  user_reviews.csv. 
- each row represents genre features of a single movie. 

## Description
The algorithm predicts the user’s preferences based on the preferences and behaviour of similar users, under the assumption that users who have similar preferences in the past are likely to have similar preferences in the future. Items with higher predicted ratings are deemed more likely to be of interest to the user and thus, are recommended to the user. The predicted ratings are calculated as a weighted average of the ratings given by similar users (neighbours) to the movies (items), with weights determined by similarity scores. 

Cosine similarity is used to calculate the similarity between users based on their interaction with movies. Each user in the system is represented as a vector in the movie space. The vector contains the user’s preferences by assigning values to movies based on user ratings. If the user has not interacted with the movie, the entry in the vector is set to 0. Cosine similarity is calculated between pairs of user vectors to measure the similarity of their movie preferences.

Based on the cosine similarity scores, a set of users (neighbours) with highest similarity to the target user is selected, forming the “neighbourhood” of users.

For movies that are not seen and rated by users, the algorithm takes a weighted average of ratings given by users in the neighbourhood (weights determined by cosine similarity scores) and users with higher similarity contribute more to the ratings. Finally, the movies with the highest predicted scores are recommended to the user. 

## Methodology
1. The user_reviews.csv file was used to create a user-item matrix, where rows represent users, columns represent items (movies). The User column was set as the dataframe index. 
2. Find neighbours (similar users) using cosine similarity 
3. Filter out unseen movies (movies with rating 0.0) by creating a boolean mask 
4. Loop through all unseen movies and for each movie, assign a predicted rating

The predicted rating is calculated by:
 1. Calculate the user’s baseline rating for the specific movie
 2. Loop through all neighbours 
 - Calculate neighbour’s baseline rating for the movie 
 - Adjust rating by subtracting the baseline and multiplying the similarity between the user and the neighbour 
 - Sum the adjusted and weighted ratings 
3. Sort the predicted ratings in descending order and select the first 5 movies

## Evaluation
Strengths
- Reccomendations are specific to each user using the behaviour of users
- Less data needed to generate recommendations (only the user_reviews.csv file was used as collaborative filtering solely relies on the user’s behaviour to make recommendations)

Weaknesses 
- User’s who are new to the platform/ have not watched many movies may receive a lower quality of recommendations as less data is available to calculate the user’s baseline rating for a movie and consequently the cosine similarity between target user and neighbours.
- Data privacy concerns may arise as the algorithm requires access to individual user data (movies watched by the user), and users may not be comfortable sharing their watch history.

