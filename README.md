# NN-Interest Prediction. Reccomendation System

This project was a university assesment packaged with a kaggle competition. Data and tasks were provided by BIP Solutions a glasgow based consultancy firm. 

The task for this project was to predict each instance of a document being loaded as relevant ornot to the customer. We beleive that this model would have the cabability to in turn create a reccomender system for their tender database. 

Below are the summary sections from the python file and report that are key to the learning outcomes and results. 

**Data processing**

The following attributes were removed:
* New-Sub - little face value relevance based on initial EDA
* Premium Pack - little face value relevance based on initial EDA * Session Id - values are nearly
all unique, therfore was removed * Query Id - values are nearly all unique, therfore was removed
* Day - Found not to improve model, removed to reduce dimensionality * Hour - Found not to
improve model, removed to reduce dimensionality
Users were tokenised using the keras tokenizer function. This was used so that models could
distinguish the same user from other users. Cpvs columns were also tokenised using the keras
tokenizer function and then padded. This transformation essentially treats the cpvs codes as text
in which relationships between the values can be formed. Cpvs were dropped for non embedding
models as the cardinality with one hot encoding was far too large for only marginal gain. To keep
dimensionality to a minimum, the number of categories for Dwell, Month, and Nature was reduced
by respectively introducing the class ‘Other’ for categories found non significant in differerentiating
between relevant and irrelevant

**Results and Discussion**
See pyhton File for Results table.

**Findings**

* As can be seen within the table, models perform better when they are trained on more data.
Using limited categorical data, the dense 3-layer model (model 2) achieved validation f1 scores
of 0.2, however when submitting to Kaggle, the score obtained on the testing data was of
0.09.
* The dense deep model (model 3) performed comparatively poor to the previous model, scoring
at best 0.19 on validation data and 0.086 in Kaggle. Perhaps being a deeper network training
was not as efficient due to unstable gradients.
115
* The final model, with a alternate architecture (model 4), scores validation f1 scores circa 0.40
when trained. We attribute this to the embedding layers using complex data, and the skip
layers assisting consistant learning throughout all layers.
* Models do not tend to overfit but rather converge.
We note that the additonal architecture doesnt perform well on non augmented data suggesting
that it is very data hungry, but this should not be a problem for the client.


**Summary and Recommendation**
* We found that best models always embed user and CPVS data in order to accurately extract
the relationships contained. Adding embedding layers gives a significant jump of circa 0.15.
Using the correct architecture with embedding layers in addition to data augmentation allowed
us to reach a score of .1975 on kaggle. We believe embedding input layers and skip layers to
be the most effienct tactic available (META) for this task.
* The non-user-Id-data is important and can give a reasonable predictor of relevance but applying them to each customer is key. We did not find session Id to be impactful with embedding
layers.
* We would emplore the client to use embedding layers going forward to act as a recommender
system. It is computationally expensive but unless the profit margin is low then we believe
that implementation of embeddings with cloud computing services would be the appropriate
way for the client to take their recommender system to production and implementation.
* Avoid shallow NN’s and Shallow ML methods as they are not able to capure the complexity
within the dataset. With embedding layers, layers with as little as 3 nuerons pefrom excellently. We would suggest investigation into much deeper neural networks when applied to
the whole data set.


