# Personalised Fashion Recommendation System

## Project Overview
This project is to build and test a personalized fashion recommendation system for an online fashion company. To enhance product discovery and engagement, by creating personalized product recommendations derived from historical interactions with products and product attributes.

Three methods for the recommendations were carried out:
1. Collaborative Filtering (SVD matrix factorization)
2. TF-IDF + cosine similarity
3. Hybrid Recommendation System (weighted combination of both)

The project is based on an end-to-end machine learning process that covers exploratory data analysis, processing of data, training the model, fine-tuning the hyperparameters, cross-validation, evaluation, and interpretation for business.

## Abstract
This work discusses the development of fashion recommendation system based on collaborative filtering, content-based filtering and hybrid modeling approaches. The data comprises 1,000 customer--product interactions from 100 customers and 1,000 products, along with their attributes like brand, category, color, size, price, and customer ratings.

The goal of the business is to improve the aspect of customized product suggestions in an e-commerce setting. Data preprocessing involved encoding of user and product identifiers, building of product metadata features and TF-IDF based vectorization of categorical attributes. The exploratory analysis showed that it was very sparse, only 1% of the possible number of user-item interactions was actually observed, significantly limiting the effectiveness of the collaborative filtering system.

Various models were tested such as baseline predictors (Global Mean, User Mean, Item Mean), a matrix factorization model with SVD, a content-based recommender system and a hybrid of the latter two. For rating prediction, the RMSE and MAE were used, while for the quality of the rankings, the Precision@K, Recall@K and the NDCG@K were used.

Results indicated that the tuned SVD model achieved the minimum RMSE (1.2068), which was slightly better than the Global Mean baseline (1.2075). Results were still low in terms of ranking for all models because of the high sparsity in the data, which did not allow the models to learn the user preference ordering reliably. These results show that the performance of the recommendation systems also critically relies on the interaction density, and that no algorithm outperforms the others in the absence of enough interactions.

## Business Problem
Product overload is a common problem on e-commerce platforms that can make it hard for users to find the relevant products. This negatively impacts engagement and conversion rates.

The business question being asked is:
> Given the history of limited interaction with the product and product attributes, how can we suggest to the user the proper fashion products?

As a result of this extreme sparsity, the vast majority of user-product interactions are unknown and these are the cases where collaborative filtering is most effective.

## Data Preparation
Key preprocessing steps included:
- Converting user and product IDs into contiguous numerical indices
- Train-test split (80/20)
- Construction of product metadata features
- TF-IDF vectorization of product attributes
- Cosine similarity computation for content-based modeling

This suggests that with this data set, content-based features are more reliable than collaborative signals because of extreme sparsity.

## Modeling Approach (Summary)

### Baseline Models
- Global Mean
- User Mean
- Item Mean

These were used as reference benchmarks.

### Collaborative Filtering (SVD)
A matrix factorization model was used to learn:
- User latent factors
- Item latent factors
- User biases
- Item biases

**Cross-Validation Results**
- Mean RMSE: 1.1779
- Standard deviation: 0.0388

This shows stable performance but limited improvement due to sparse interaction data.

### Hyperparameter Tuning
Best configuration:
- Factors: 100
- Learning rate: 0.002
- Regularization: 0.05

Best RMSE: 1.2068

The tuned SVD model performed best in terms of RMSE, but improvements over the baseline were not significant.

### Content-Based Filtering
TF-IDF was used to vectorize product attributes, and cosine similarity was applied to compute similarity between products.

This method does not depend on user interaction history and is therefore more robust under sparse conditions.

### Hybrid Recommendation System
The hybrid model combines collaborative and content-based signals:

`Hybrid Score = α(Collaborative) + (1 − α)(Content)`

Best α = 0.3

This indicates that content-based features were more reliable than collaborative signals due to extreme sparsity.

## Evaluation Strategy
Two categories of metrics were used:

**Rating Prediction Metrics**
- RMSE
- MAE

**Ranking Metrics**
- Precision@K
- Recall@K
- NDCG@K

These evaluate both prediction accuracy and recommendation usefulness.

## Results
| Model | RMSE | MAE |
|-------|------|-----|
| Global Mean | 1.2075 | 1.0521 |
| User Mean | 1.3053 | 1.1012 |
| Item Mean | 1.2075 | 1.0521 |
| Tuned SVD | 1.2068 | 1.0554 |

The tuned SVD model achieved the lowest RMSE, but the improvement over the baseline was marginal.

Ranking metrics were near zero across all models due to extreme sparsity in the dataset.

## Interpretation of Findings
This project's most important conclusion is that data sparsity is the primary factor that affects the performance of a recommendation system.

Even with the use of advanced models (SVD, TF-IDF, hybrid systems), the amount of observed interactions in the dataset was only 1%, too little to learn reliable user preference structures.

As a result:
- Simple baseline models did not significantly outperform complex models
- The quality of the ranking was not consistent for any method
- Personalization could NOT be done by collaborative filtering (CF) alone

It illustrates an important real-life lesson: data quality and quantity is more important in a recommendation system than model complexity.

## Business Recommendations

### 1. Collect More User Interaction Data (Highest Priority)
The most important improvement is reducing sparsity by collecting behavioral signals such as:
- Product clicks
- Add-to-cart actions
- Purchase history
- Wishlist activity
- Browsing time and engagement signals

These implicit feedback signals would significantly improve collaborative filtering performance.

### 2. Expand Dataset Coverage
The current dataset is insufficient for meaningful personalization. Increasing both:
- Number of users
- Number of interactions per user

is essential for improving recommendation quality.

### 3. Strengthen Content-Based Features
In sparse cases, content-based filtering was relatively more successful, so metadata of products should be enhanced with:
- Material type
- Seasonality
- Style descriptors
- Customer reviews
- Product embeddings

This improves cold-start performance and recommendation diversity.

### 4. Deploy Hybrid Recommendation Systems
Hybrid systems are the most practical solution under sparse conditions because they:
- Reduce reliance on interaction data
- Improve cold-start recommendations
- Combine behavioral and attribute-based signals

Even though ranking performance was limited here, hybrid approaches remain the most scalable real-world solution.

### 5. Evaluate Using Real-World Feedback
Offline metrics such as RMSE and Precision@K are limited under sparse datasets. A production system should also include:
- A/B testing
- Click-through rate (CTR)
- Conversion rate tracking

These are more appropriate measures of the success of recommendations.

## 6. Tableau VIsualization
To support the analysis of machine learning, an interactive Tableau dashboard was created to allow visualizing both product characteristics and business performance. The dashboard offers dynamic visualisation and filtering options for important metrics on brands, categories, sizes, colour, price, rating, and profitability. The dashboard suggests that pricing is fairly uniform among brands, more profitable for items like jeans, shoes, and more uniform customer ratings by product size. The category–colour distribution also shows buying pattern which can be used for merchandising and recommending strategies. The dashboard provides descriptive business intelligence and predictive recommendation models to enable stakeholders to have a clearer understanding of the product performance and customer preferences, which helps in informed business decisions. The dashboard can be accessed at [Tableau Fashion Products Analysis Dashboard](https://public.tableau.com/app/profile/sonia.cherop/viz/FashionDashboard_17803116244790/FashionProductsAnalysisDashboard?publish=yes&utm_source=chatgpt.com).


## Conclusion
In this project, an end-to-end pipeline of recommendation system is applied to collaborative filtering, content-based filtering and hybrid approaches. All models were implemented and worked, but it was not the model but the sparseness of the datasets that caused limited performance.

What's important to note is that recommendation systems are more likely to be effective when there is more interaction data available, rather than when there are more algorithms employed. Focusing on better data collection processes and the addition of implicit feedback signals has a greater impact in practice than additional model optimizations in isolation.