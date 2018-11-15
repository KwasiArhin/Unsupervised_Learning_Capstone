# Unsupervised_Learning_Capstone. Poetry Analysis. :book:

#### Introduction: :european_castle:
Poetry is a cultural treasure of a country and its trademark. It's not unheard of people to learn a new language specifically in order to be able to read poems of their favorite authors in the original. Meter, rhythm, imagery, symbolism, references to other authors and contemporary events. How can a computer understand it?

#### In this project, I attempt to reach the following tangible goals:  
* Prediction of a poem's time period (Renaissance vs. Modern) based on features generated through TF IDF scores and subsequent Latent Semantic Analysis (LSA).
* Prediction of a poem's time period (Renaissance vs. Modern) based on word2vec features.
* Prediction of a poem's type (love vs. non-love) using tf idf scores and LSA.
* Clustering of the Texts using MeanShift, KMeans, and Spectral clustering algorithms.

#### Data:
The corpus of English poetry which is available at: https://www.kaggle.com/ultrajack/poetry-analysis-using-ai-machine-learning/data.

#### Metrics:
For this project, we will use roc_auc score (area under the receiver operating characteristic curve) as the measure of the classifiers' performance. It allows us to estimate the ratio of true positives to false positives regardless of our probability threshold.

## Task One. Time Period Prediction (Renaissance vs. Modern) :clock1:

**FEATURES:** tf idf matrix with dimensionality reduced by applying Latent Semantic Analysis (LSA).

#### Results: :bar_chart:
Models | Training Set Roc_Auc Scores |Test Set Roc_Auc Scores
------------ | ------------- |-------------
Logistic Regression (Ridge)|	0.9825|	0.9726
Random Forest	|0.9621|	0.9526
Gradient Boosting	|0.9391|	0.9332
XGB	|0.9541|	0.9243
SVM	|0.980|	0.9779

**ALTERNATIVE FEATURE GENERATION:** document vectors (Word2Vec)

#### Results: :bar_chart:
Models | Training Set Roc_Auc Scores |Test Set Roc_Auc Scores
------------ | ------------- |-------------
Logistic Regression (Lasso)|	0.9277|	0.9576
SVM	|0.893|	0.8691

Our word2vec model did not perform the best which was to be expected. For this kind of model to work well, we would need a much larger corpus of texts: in our case we only had 573 samples. Using a pretrained model, e.g. Google's, might not be the greatest idea since our corpus contains a very specific vocabulary with a large portion of works dating back to the Renaissance.

## Task Two. Identification of "Love" Poems :cupid:
**FEATURES:** tf idf matrix with dimensionality reduced by applying Latent Semantic Analysis (LSA).

Models | Training Set Roc_Auc Scores |Test Set Roc_Auc Scores
------------ | ------------- |-------------
Logistic Regression (Lasso)|	0.7493|	0.812
SVM|	0.76|	0.815

## Task Three. Clustering of The Texts

We experimented with different clustering algorithms, but the best results were produced by K-Means Clustering and Spectral Clustering. K-Means was able to produce stable two-cluster and four-cluster solutions.

#### Four-Cluster Solution
The thematic difference between the clusters is intriguing. 

* For the first cluster, the following semantic components are relevant: "celebration of love and beauty", and "death." At the same time, "farewell to love" is more pertinent to this cluster than to other clusters.

* For the second cluster, "celebration of love and beauty" is important. However, the unique semantic component "weak man" is also very significant. "Farewell to love" is relevant.

* The third cluster seems to be comprised of starkingly "happy" and "light" poems. The only relevant semantic component is "celebration of love and beauty."

* The last cluster is a mix: "celebration of love and beauty" is more pertinent to this cluster than to any other clusters. However, the same is true of the semantic component of "fading." 

#### Conclusion::clipboard:
With the help of modelling, we were able to achieve some tangible results: we trained algorithms that could predict the time period when a poem was written and could identify "love" poems. In our case, we were dealing with a labeled dataset and pure categories. However, in reality there are many borderline cases, for example, undated works, imitations of Renaissance poems as well as poems with varying degree of "love" theme expressed. The models we trained will still be able to tackle these problems: they will be able to give us probabilities of a poem belonging to a particular time period as well as probabilities of a poem related to the topic of "love." In fact, we could even arrange poems as more typical of Renaissance or more "love-heavy" based on these probabilities. This is a useful strategy for poetry analysis: it is not impressionistic but quantifiable and objective.

Additionally, in this project, we were able discover thematic groups (clusters) in our corpus. While the corpus of the poems used for this analysis was within the established literary cannon, a similar analysis could be applied to a vast corpus of "the great unread" or any other body of texts which had not been previously studied or even read by a human.
