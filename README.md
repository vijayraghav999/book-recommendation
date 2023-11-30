# [Book Recommendation Engine](https://github.com/Saipavan790/Recommender-Systems)
Recommender systems is a sub-class of information filtering system that provide suggestions for items that are most pertinent to a particular user. Typically, the suggestions refer to various decision-making processes, such as what product to purchase, what music to listen to, or what online news to read. Recommender systems are particularly useful when an individual needs to choose an item from a potentially overwhelming number of items that a service may offer.

## There are two ways to build a recommendation system:-

> ### Content-based Recommendation system :
>> One popular technique of recommendation systems is **content-based filtering**. Content here refers to the content or attributes of the products you like. So, the idea in content-based filtering is to tag products using certain keywords, understand what the user likes, look up those keywords in the database and recommend different products with the same attributes.

>> It is based on the idea of recommending the item to user K which is similar to previous item highly rated by K. Basic concept in content based filtering is TF-IDF (Term frequency — inverse document frequency), which is used to determine the importance of document/word/movie etc. Content based filtering shows transparency in recommendation but unlike collaborative filtering it can’t able to work efficiently for large data. Content-based approach requires a good amount of information of items’ own features, rather than using users’ interactions and feedbacks. For example, it can be movie attributes such as genre, year, director, actor etc., or textual content of articles that can extracted by applying Natural Language Processing.

> ### Collaborative Filtering based Recommendation system:
>> Collaborative methods for recommender systems are methods that are based solely on the past interactions recorded between users and items in order to produce new recommendations. These interactions are stored in the so-called “user-item interactions matrix”.

>> **The class of collaborative filtering algorithms is divided into two sub-categories that are generally called memory based and model based approaches.**

>> Memory based approaches directly works with values of recorded interactions, assuming no model, and are essentially based on nearest neighbours search (for example, find the closest users from a user of interest and suggest the most popular items among these neighbours). Model based approaches assume an underlying “generative” model that explains the user-item interactions and try to discover it in order to make new predictions.

>> The main advantage of collaborative approaches is that they require no information about users or items and, so, they can be used in many situations. Moreover, the more users interact with items the more new recommendations become accurate: for a fixed set of users and items, new interactions recorded over time bring new information and make the system more and more effective. However it only consider past interactions for making recommendations.

**The method I used for this project is collaborative filtering**.

The steps I followed to implement this project

## Collaborative Filtering using K-Nearest Neighbors (KNN)

kNN is a machine learning algorithm to find clusters of similar users based on common book ratings, and make predictions using the average rating of top-k nearest neighbors.

### Load the data  
You can get the data from this [link](http://www2.informatik.uni-freiburg.de/~cziegler/BX/)  
From this link you have to download three files.  
![](https://github.com/Saipavan790/Recommender-Systems/blob/main/load_data1.png)

I only selected relevent columns from the dataset. Note that file encoding is not 'utf-8'.  
**To ensure statistical significance, we will be only looking at the popular books.**

### Data Preprocessing

![](https://github.com/Saipavan790/Recommender-Systems/blob/main/extract_users.png)  
As you can see I've explained clearly how I extracted users who have rated at least 200 books.

![](https://github.com/Saipavan790/Recommender-Systems/blob/main/extract_books.png)

I have extracted books that have received at least 30 ratings. It's because we cannot recommend books based on less ratings. After that merge your book and ratings dataframe.

### Implement the KNN model  
We convert our table to a 2D matrix, and fill the missing values with zeros (since we will calculate distances between rating vectors). We then transform the values(ratings) of the matrix dataframe into a scipy sparse matrix for more efficient calculations.

![](https://github.com/Saipavan790/Recommender-Systems/blob/main/build_model.png)
We then generate a pivot table with the values as the ratings, the book titles as the rows and the user IDs as the columns. They are lot of null values in our pivot table so we convert those values to zeroes before feeding it to the model. Since our dataset is fairly large. For better computations we convert our pivot table to sparse matrix.

![](https://github.com/Saipavan790/Recommender-Systems/blob/main/trained_model.png)
We use unsupervised algorithms with sklearn.neighbors. The algorithm we use to compute the nearest neighbors is “brute”, and we specify “metric=euclidean” so that the algorithm will calculate the distance between rating vectors. Finally, we fit the model.

### Make Predictions 
I defined a function which would take book name and returns a list of 5 recommendations.

![](https://github.com/Saipavan790/Recommender-Systems/blob/main/predictions.png)

These predictions are based on euclidean distance. We can also build this same model using cosine similarity.
