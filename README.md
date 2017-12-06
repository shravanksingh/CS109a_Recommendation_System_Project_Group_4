# Recommendation System for Restaurants using Yelp dataset
Group # 4

1. Shravan Kumar Singh 
2. Gurjeet Singh
3. Deepika Sinha 

(Website link:https://shravanksingh.github.io/CS109a_Recommendation_System_Project_Group_4/)


**Problem Statement and Motivation:**

Restaurants is one of the major industry that has close ties with humans’ necessity & offers a variety of experiences and food from specialty cuisines (e.g. Mexican, Italian etc.) to taste, décor & services. Yelp users give rating to the restaurant based on their preferences so one rating for a restaurant that all users see. Yelp has a single star rating which is not enough to address different user preferences. Customized rankings are imperatives to any business and people will benefit more from this service. So, we can build a recommendation system that can identify a user’s preferences and provide customized rankings for each individual user. 

This recommender system focuses on predicting the rating that a user would have given to a certain restaurant, which is used to rank all the restaurants including those that have not been rated by the user. 

**Introduction and Description of Data:**

The academic dataset (https://www.yelp.com/dataset/challenge) from yelp was downloaded and untarred.

Description of revenant knowledge about Yelp data:
1. business.json: Contains business data including location, attributes, and categories. 
2. review.json: Contains full review text data including the user_id that wrote the review and the business_id the review is written for and the review stars and usefulness. 
3. user.json: Contains the user's friend mapping and all the metadata associated with the user. 

Recommendation systems are important for increasing business revenue and giving users the ability to find desired restaurants of their taste. The system is challenging because many users don't give ratings and we have new restaurants and users added to the system every day. In order to improve Yelp restaurant rating system, we need to predict the rating for the restaurant which are not rated.From our EDA via distribution charts we found many restaurants were not rated and some restaurants were rated by large number of people.So it is important to build recommendation system for sparse rated restaurants.

**Literature Review/Related Work:**
We referred to the some of the libraries below for building the model namely Python Surprise library, Library for SVD, Library for accessing Similarity references to these libraries are given at the end.
we also referred to some of the papers to broaden our understanding of the recommender system like Matrix factorization for recommender systems and Netflix prize related details on Kaggle (references at the end).
Some of them has used SVD and similarity collaborative filtering, we also did that and then we extended that with Meta Classifier approach and got some decent results.  

**Modeling Approach and Project Trajectory:**

The following steps are used in preparing data for analysis & prediction:
 	
1. Large Dataset: As the dataset is huge, we only took 100K samples of the observations from each dataset (businesses, users and reviews) to perform the initial EDA.
2. Combining Data: The sample data was observed to be clean and we merged the dataset based on unique keys.
3. Filtering: We filtered it down to the restaurants by selecting businesses based on category ‘Food’; for reviews/users we only included the data which was for the restaurants in the sample.
4. Visualization: We used bar charts, histograms, scatter plots and distribution plots to explore the data and understand the data patterns for the restaurants’ reviews.
5. Ratings are integers ranging between 1 and 5. The loss function to compare various methods is measured by the root mean squared error (RMSE).

Baseline Models:
We used Surprise library for Baseline models. Surprise is a Python scikit for building, and analyzing (collaborative-filtering) recommender systems. Various algorithms are built-in, with a focus on rating prediction. 
BaselineOnly is an algorithm predicting the baseline estimate for given user and item 
	Ym = μ + su + sm
where the unknown parameters su and sm indicate the deviations, or biases, of user u and item m respectively from some intercept parameter.

KNNBaseline is a basic collaborative filtering algorithm taking into account a baseline rating.

Memory Based Collaborative filtering:
We used Collaborative filtering. The two primary areas of collaborative filtering are the neighborhood methods and latent factor models. 

Neighborhood methods are centered on computing the relationships between items or, alternatively, between users. The item oriented approach evaluates a user’s preference for an item based on ratings of “neighboring” items by the same user. A product’s neighbors are other products that tend to get similar ratings when rated by the same user. 

Latent factor models (aka SVD) are an alternative approach that tries to explain the ratings by characterizing both items and users on number of factors inferred from the ratings patterns. Latent factor models are based on matrix factorization which characterizes both items and users by vectors of factors inferred from item rating patterns. High correspondence between item and user factors leads to a recommendation. From the results, we can see that prediction accuracy has improved by considering also implicit feedback, which provides an additional indication of user preferences.

**Results, Conclusions, and Future Work:**

We can see below that testing and training RMSE's for various models are not much different but when we used Meta Classifier we are able to improve the RMSE.

RMSE scores(training/testing) for various models are given below
Meta Classifier training/testing: 0.161929/0.396512
SVD Collaborative Flittering training/testing: 3.371695/5.000000	
Memory Based User Collaborative Filtering training/testing: 3.920374/4.989627	
Memory Based Restaurant Collaborative Filtering training/testing: 3.924467/5.000000

Due to paucity of time we are not able to add features in our models and we did matrix factorization with k=10, we also tried to change the number of latent factors but our scores did improve so we kept the value of k to be 10.
In future we would like to add all the features of the restaurant so that we can further improve the accuracy of our models.

**References:**

1. How the Netflix prize was won, http://blog.echen.me/2011/10/24/winning-the-netflix-prize-a-summary/
2. Matrix factorization for recommender systems, https://datajobs.com/data-science-repo/Recommender-Systems-[Netflix].pdf
3. Ensembling for the Netflix Prize, http://web.stanford.edu/~lmackey/papers/netflix_story-nas11-slides.pdf
4. Reviews on methods for netflix prize, http://arxiv.org/abs/1202.1112andhttp://www.grouplens.org/system/files/FnT%20CF%20Recsys%20Survey.pdf
5. Advances in Collaborative Filtering from the Netflix prize, https://datajobs.com/data-science-repo/Collaborative-Filtering-%5BKoren-and-Bell%5D.pdf
6. Python Surprise library for models, https://pypi.python.org/pypi/scikit-surprise.
7. Library for SVD, https://docs.scipy.org/doc/scipy/reference/generated/scipy.linalg.svd.html
8. Library for accessing Similarity, http://scikit-learn.org/stable/modules/generated/sklearn.metrics.pairwise.pairwise_distances.html

