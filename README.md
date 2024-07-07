# Date Night Movie Recommender

For this recommender system project, I chose to implement Funk SVD, which is used in major recommendation engines such as Netflix's, and apply it to the [MovieLens 1M](https://grouplens.org/datasets/movielens/1m/) dataset.

### Why Funk SVD?

SVD (Singular Value Decomposition) is a popular collaborative filtering technique for recommender systems. It's a matrix factorisation technique which decomposes the problem into two lower-dimensional matrices: a user matrix and an item matrix.

Here are the main reasons why I chose to use Funk SVD for this project:

- **Efficiency and Accuracy**: Funk SVD being a matrix factorisation technique, it reduces the dimensionality of user-item matrices, allowing it to capture latent relationships between users and movies effectively.

- **Sparse matrix**: Funk SVD works particularly better than SVD on sparse matrices, which is the case of our dataset, because users only rate some movies and most squares in our user-item interaction matrix are empty.

- **Simplicity**: This technique is straightforward to implement compared to more complex models such as deep neural networks, yet it can deliver comparable performance. Since it's one of the techniques we implemented in class, it was also easier to apply to similar use cases than other techniques.

- **Popularity**: Successfully used by Netflix in its recommendation system, Funk SVD has demonstrated its ability to provide accurate recommendations.

### Implementation choices in the project

1. **Data collection and preprocessing**:
   - **Dataset download**:
	   - The MovieLens 1M dataset was downloaded. Experimentation with bigger MovieLens datasets showed that they were just to heavy and kept crashing, so 1M was selected. The dataset contains information about movies, users and ratings.
	   - IMDb datasets containing movie information, as well as cast and crew information, were downloaded.
   - **Datasets merging**: Data was merged to include movie ratings, genres and other movie features into one single dataframe. *This was done prior to selecting Funk SVD as the recommendation algorithm, so it was not used in the end.*

2. **Feature extraction**:
   - **User-Item interaction matrix**: A matrix of movie ratings by users was created.

3. **Funk SVD implementation**:
   - **Train-validation split**: The data was split into a training and a validation set.
   - **Normalization**: Before being fitted into the model, the data was normalized by subtracting the mean rating for each item. After inference, the predictions are multiplicated back into the [0, 5] range.
   - **Model implementation**: Funk SVD was used to factorize the user-item interaction matrix into latent feature matrices for users and items. The model was created following the implementation seen in class.
   - **Inference**: After the model is succesfully fitted, a function allows to get all predicted movie ratings for one specified user.

4. **Development of the recommendation algorithm**:
   - **Couple score**: A "couple score" was defined to combine the predictions for two specified users. The score consists of multilplying the two scores and dividing them by 5. This method ensures that both users have an equal influence on the prediction and normalizes the score in the [0, 5] range.
   - **Movie ranking**: Movies were ranked based on the couple score, recommending those with the highest scores.

5. **Evaluation**:
   - **Data splitting**: Data was split into training and validation sets.
   - **Evaluation**: Predictions were generated for 1000 user-item pairs from the validation set, where actual ratings were available for comparison.
   - **Metrics**: Root Mean Squared Error and R-squared score were used to evaluate prediction accuracy. While RMSE allows to measure the average distance between the predicted and the actual ratings, R2 score indicates how the predicted ratings compared to using naively the mean rating.

### Conclusion

This date night movie recommender system for couples was implemented using Funk SVD, a powerful matrix factorization technique widely used in recommendation engines. Utilizing the MovieLens 1M dataset, we implemented and evaluated the model to suggest movie pairs based on user ratings.

Funk SVD was selected for its straightforward implementation and efficiency in handling sparse user-item interactions. While our approach brought valuable insights, the results in terms of prediction accuracy, as measured by RMSE and R2 score, were not optimal and highlighted areas for improvement.

Some ideas to improve the recommendation algorithm include:
-   **Add additional features**: adding movie features such as duration, genres, casts to enrich the algorithm.
-   **Explore more advanced algorithms**: consider more sophisticated algorithms such as neural networks and deep learning models.

This project highlights the importance of exploring diverse approaches to achieve optimal performance in recommendation systems.