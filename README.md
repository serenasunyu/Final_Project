# Beauty Product Recommendation System

Product Recommendation System is a machine learning-based project that provides personalized product recommendations to users based on their purchase history. The system utilizes popularity based filtering and collaborative filtering algorithms to analyze user behavior and generate relevant recommendations. This project aims to improve the overall shopping experience for users, increase sales for e-commerce businesses.

## Dataset

Amazon beauty product dataset.

* You can find the [dataset](https://cseweb.ucsd.edu/~jmcauley/datasets.html#amazon_reviews)


## Approach

### Popularity Based Product Recommendation
Objective:
* Recommend products with highest number of ratings.
* Target new customers with most popular products.
* Solve the Cold Start Problem

Outputs:
* Recommend top 5 products

Approach:
* Use IMDB weighted rating system and the number of ratings into account.
* Calculate average rating for each product.
* Calculate total number of ratings for each product.
* Calculate the minimum number of ratings required to be listed.
* Calculate the mean number of ratings across the whole dataset
* Calculate popularity score.
* Create a DataFrame using these values and sort it by popularity score.
* Write a function to get 'n' top products with specified minimum number of interactions.

### Collaborative filtering
Objective:
* Provide personalized recommendations to users based on their past behavior and preferences, while also addressing the challenges of sparsity and scalability that can arise in other collaborative filtering techniques.

Outputs:
* Recommend top 5 products for a particular user.

Approach:
* Taking the matrix of product ratings and converting it to a CSR(compressed sparse row) matrix. This is done to save memory and computational time, since only the non-zero values need to be stored.
* Performing singular value decomposition (SVD) on the sparse or csr matrix. SVD is a matrix decomposition technique that can be used to reduce the dimensionality of a matrix. In this case, the SVD is used to reduce the dimensionality of the matrix of product ratings to 15 latent features.
* Calculating the predicted ratings for all users using SVD. The predicted ratings are calculated by multiplying the U matrix, the sigma matrix, and the Vt matrix.
* Storing the predicted ratings in a DataFrame. The DataFrame has the same columns as the original matrix of product ratings. The rows of the DataFrame correspond to the users. The values in the DataFrame are the predicted ratings for each user.

### Model Evaluation
* Use Top N Recommendation to generate recommendations for a subset of users in the testset.
* Use Recall@5 and Recall@10 to evaluate the recommendations.

### Result:
* Popularity based filtering:
  - recall@5: 0.48853211009174313 
  - recall@10: 0.5359327217125383
* Collaborative filtering
  - recall@5: 0.4602446483180428
  - recall@10: 0.47897553516819574

### Analysis
* From the evaluation, it becomes evident that the popularity-based filtering model outperforms the collaborative filtering model. This outcome can be primarily attributed to the dataset used in this project. The beauty product dataset initially comprised approximately 320,000 data points but was subsequently reduced to around 8,000 after undergoing data cleaning and filtering. 
* Specifically, we retained only those users who had engaged with more than 4 products. If we raise this threshold to more than 5 interactions, the dataset further shrinks to about 4,000 data points. This indicates that a significant portion of users provided ratings for fewer than 5 products, resulting in a dearth of personalized recommendations for the majority of users.
* One potential explanation for this phenomenon could be related to user behavior and habits. Some individuals may simply refrain from leaving ratings or comments for their purchases. In light of this situation, it becomes imperative to incorporate additional features into the recommendation system to enhance its performance. For instance, we might consider integrating metrics such as the amount of time these users spend browsing product pages or the number of related products present in their search history. By doing so, we can augment the system's ability to cater to users who may not actively engage in traditional rating and review behaviors, thereby improving the overall quality of personalized recommendations.
     
