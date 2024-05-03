# Swahili-Language-News-Classification-
<img src="News.gif" alt="News GIF" style="max-width: 100%;">

## Project Overview

## Business Problem

Swahili serves as a vital language for communication, education, and cultural expression in Tanzania and across East Africa. With the increasing dominance of English in online spaces, there's a risk of losing the representation of Swahili, especially in digital media such as news platforms. We strive to address this challenge by developing a multi-class classification model to automatically categorize Swahili news articles into specific categories. By doing so, online news platforms can enhance user experience by providing readers with easy access to news content relevant to their interests, while also contributing to the preservation and promotion of the Swahili language in the digital age.
## Objectives
* To Develop a Multi-Class Classification Model that utilizes machine learning techniques to categorize Swahili News.
* To Enhance User Experience by improving the accessibility of Swahili news content by enabling automated categorization on online news platforms.
* To Promote Swahili Language by contributing to the representation and preservation of Swahili in digital media by ensuring its inclusion and visibility in online products and services.
## Data
The data used is from Zindi Africa and has 5151 Swahili articles and 3 features.

## Data Preparation
During this process, we checked for null values, and the shape of the dataset, and investigated the distribution of the Swahili news categories. we find out that we have an imbalance distribution.

![Target dist](https://github.com/JohnNkakuyia/Swahili-Language-News-Classification-/blob/main/images/target_dist.jpg)

## Exploratory Data Analysis
we label-encoded the categories, corrected punctuations where necessary, tokenized our dataset, and created subplots for our tokens, after which we noted we could distinguish categories as displayed. 

![Removing stopwords](https://github.com/JohnNkakuyia/Swahili-Language-News-Classification-/blob/main/images/No_stopwords.jpg)

## Baseline Model
We performed a baseline model without balancing the categories. The baseline performance of the Multinomial Naive Bayes classifier, evaluated using cross-validation, yields an average accuracy of approximately 39.2%. This indicates that the classifier's predictive ability is slightly better than random chance. However, it's essential to consider the class balance within the dataset, as it significantly influences the interpretation of the results

To effectively mitigate the effects of class imbalance in our dataset and improve the
performance of the predictive model, we apply the Oversampling technique which Increases the
number of instances in the minority class by generating synthetic samples or duplicating
existing ones. we noted that when balancing categories our model performed exemplary well with a mean cross-validated accuracy score of about 0.91

**Distributions of Sentence Counts by Category**

We find that our model has a good distribution in content when it comes to 'kitaifa', 'biashara',
and 'michezo'. However, this might also treat the class with skewed content distribution as a
rare class, which could affect our predictions.

![sentence tokenized](https://github.com/JohnNkakuyia/Swahili-Language-News-Classification-/blob/main/images/Sentence_token.jpg)

We iteratively ran seven models for us to examine which models performed the best in terms of accuracy and log loss.

**MultinomialNB**: This model has an accuracy of 0.821429 and log loss of 0.482447. 

**Logistic Regression**: The logistic regression model has an accuracy of 0.836957 and a log loss of 0.438784.

**Decision Tree Classifier**: The Decision Tree Classifier has an accuracy of 0.712733 and log loss of	10.354155.

**RandomForestClassifier**: The RandomForest Classifier has an accuracy of 0.840839 and log loss of	0.575659.

**XGBClassifier**: The XGBClassifier has an accuracy of 0.856366	and log loss of 0.457004.

**LGBMClassifier**: The LGBMClassifier has an accuracy of 0.858696 and log loss of 0.464706.

**CatBoostClassifier**: The CatBoostClassifier has an accuracy of 0.847826 and log loss of 0.420255.

**visualizing models performance , accuracy and log loss**

![model comparison](https://github.com/JohnNkakuyia/Swahili-Language-News-Classification-/blob/main/images/model_comparison.jpg)

Accuracy: The accuracy of the model on the test data, measuring the proportion of correctly
classified instances. Log Loss: The logarithmic loss (log loss) of the model on the test data,
assessing the performance of a classification model where the prediction output is a probability
value between 0 and 1. According to the results, the LGBMClassifier achieved the highest
accuracy of 0.859, closely followed by the CatBoostClassifier with an accuracy of 0.848. However,considering both accuracy and log loss, it's noteworthy that the CatBoostClassifier attained the
lowest log loss of 0.420 among all models.
Hence, based on both accuracy and log loss, the CatBoostClassifier appears to have performed
the best in this scenario.

**Model with CatBoostClassifier, LogisticRegression and MultinomialNB**

The observed range of evaluation metrics across the three selected classifiers highlights varying
strengths and weaknesses in their performance. While MultinomialNB exhibits a lower recall,
indicating potential limitations in capturing all positive instances, CatBoostClassifier stands out
with its high precision, showcasing its proficiency in making accurate positive predictions while
minimizing false positives.

![CatBoostClassifier](https://github.com/JohnNkakuyia/Swahili-Language-News-Classification-/blob/main/images/catboost_matrix.jpg)

## Final Model with StackingClassifier 
Stacking is a method that combines multiple classification or regression models via a meta-classifier or meta-regressor. The basic idea is to use the predictions of base models as input features to a higher-level model. Here we apply stacking ensembling to CatBoostClassifier, LogisticRegression and MultinomialNB

![StackingClassifier confusion matrix](https://github.com/JohnNkakuyia/Swahili-Language-News-Classification-/blob/main/images/final_confusion_matrix.jpg)

**Interpreting Results**

Rare classes like Burudani and Kimataifa in the dataset pose challenges for the model in
correctly classifying instances belonging to these classes. Consequently, the confusion matrix
shows lower values for true positives for these rare classes.
On the stacking model, we achieved an accuracy of 0.8524, implying that approximately 85.24%
of the model's predictions were correct. Additionally, with a log loss of 0.3984, it suggests that
the model's predictions are closely aligned with the actual probabilities.
Upon examining the confusion matrix, the model exhibits robustness in its predictions,
effectively capturing the underlying patterns and features of the data. There are no instances of
mislabeled posts, indicating consistent and precise predictions across all classes. This reliability
suggests that the model can be trusted for accurate classifications. Given its strong
performance, the model may be suitable for deployment in real-world applications where
accurate classification is crucial

## Conclusion 
While the absence of mislabeled posts is encouraging, further analysis is warranted to ensure
the model's robustness across diverse datasets or conditions and to identify any potential biases
or limitations.




