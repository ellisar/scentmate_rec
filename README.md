# ScentMate
###### Capstone Project Final Proposal &bull; g45 &bull; Yuwei(Kelly) Peng &bull; 09/2017

---
#### Check out the final product:
Web app IP address: 34.212.206.24

---

## Motivation

Fragrance is not only about scent, it tells your personality, or the impression you want to leave on people. People with different personality types will like different scents. In addition to personality, mood, environment, season all affects people's choice of fragrances.

Among 30,000 fragrance products in the world, do you know which fragrance is your perfect match? What's people's impression of the fragrance you like? Is that the way you want people to think about you? That's what ScentMate is all about.

ScentMate, find your perfect match.

&nbsp;
## Recommendation Systems

Think about Pandora, Netflix, Youtube, Amazon...One common characteristic of them is that they personalize what each user receives based on user preferences, and this is what recommendation systems are about. Recommendation systems have become increasingly more popular in recent years as a way for companies to provide better service and increase profit. In a broad sense, recommendation systems predict the level of interest a user has in a new item.

Different architectures for a recommender system:
1. **Popularity Based Recommender** Make the same recommendation to every user, based on the popularity of an item.
2. **Content-Based Recommender** focus on properties of items. Similarity of items is determined by measuring the similarity in their properties. Different types of content-based systems:
   1. Classification/Regression
   2. Item content similarity (Jaccard similarity, cosine similarity)
   3. Word2Vec
   4. Non-Negative Matrix Factorization (NMF)
3. **Collaborative Filtering Recommender** focus on the relationship between users and items. Similarity of items is determined by the similarity of the ratings of those items by the users who have rated both items.
   1. Item-item similarity
   2. User-user similarity
   3. Matrix Factorization

For this project, I will implement different approaches. For cold start problem, I will use content based models, for users with rating history, I will implement item-item similarity collaborative filtering model and matrix factorization model.

It is also possible to combine the collaborative and content-based approaches into one model and create a hybrid recommendation system.

&nbsp;
## Workflow

**Step 1**. Parallel scrape data from website using 6 AWS EC2 instances
**Step 2**. Store scraped data in MongoDB on AWS EC2 instance
**Step 3**. Data analysis, feature engineering, modeling, cross validation
**Step 4**. Develop a web app using Flask, Bootstrap, HTML, CSS
**Step 5**. Deploy everything onto AWS EC2 instance, run flask on AWS

&nbsp;
## Data

The data I scraped from website are two tables. One table is perfume data, which includes features such as:

* Number of Perfumes: 20k
* Brand: 1,824
* Gender: 3
* Note: 653
* Theme: 30

Another table is user rating data:

* Number of Ratings: 40k
* Perfume ID
* User ID
* Rating Score: Range 2 - 10
* User Comment

&nbsp;
## Models

1. Model 1: Content-Based Recommender
In order to gather more meaningful features for each perfume, such as people's feeling about each perfume, I applied NMF and LDA to user comments for topic modeling. After comparing the topics from both methods, I chose 12 topics generated by LDA, and then combined LDA keywords together with other perfume features, built perfume matrix, then built content-based similarity model based on Jaccard similarity.

2. Model 2: Collaborative Filtering Recommender

||Base Model|Item-item Similarity|Funk SVD (UV decomposition)|
------|------|------|-----|
Methodology|Predict mean for everything|Recommend based on the most similar items found by user ratings|Decompose utility matrix into two matrices with 14 latent factors, added regularization
Performance on Test Set|RMSE: 2.20|RMSE: 7.32|RMSE: 1.95|
Reason||Utility matrix too sparse lead to little information going into each prediction|Should perform better if more data available

&nbsp;
## Limitations
1. No price data, which has a big impact on content-based recommender's performance
2. Some fragrance products have no reviews at all, the reason can be they are too old/new/unpopular, these perfumes are not included in dataset

&nbsp;
## Tools Used
- Data processing and EDA: Numpy, Pandas, Matplotlib, Plotly, Seaborn
- Machine learning and stats: Numpy, Pandas, Graphlab, Scikit-learn, Scipy
- Web Scaping: BeautifulSoup, urllib2
- Data Storage: pymongo, MongoDB
- Cloud Computing: AWS S3, EC2
- Web App: Flask, Bootstrap, HTML, CSS


---
&nbsp;
