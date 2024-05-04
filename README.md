# Swahili-Language-News-Classification
<img src="News.gif" alt="News GIF" style="max-height: 2630px;">


## Project Overview

## Business Problem

Swahili serves as a vital language for communication, education, and cultural expression in Tanzania and across East Africa. With the increasing dominance of English in online spaces, there's a risk of losing the representation of Swahili, especially in digital media such as news platforms. We strive to address this challenge by developing a multi-class classification model to automatically categorize Swahili news articles into specific categories. By doing so, online news platforms can enhance user experience by providing readers with easy access to news content relevant to their interests, while also contributing to the preservation and promotion of the Swahili language in the digital age.
## Objectives
* To Develop a Multi-Class Classification Model that utilizes machine learning techniques to categorize Swahili News.
* To Enhance User Experience by improving the accessibility of Swahili news content by enabling automated categorization on online news platforms.
* To Promote Swahili Language by contributing to the representation and preservation of Swahili in digital media by ensuring its inclusion and visibility in online products and services.
## Data
The data used is from [Zindi Africa's platform]( https://zindi.africa/hackathons/swahili-news-classification-challenge/data.) and has 5151 Swahili articles and 3 features.

## Data Preparation
During this process, we checked for null values, and the shape of the dataset, and investigated the distribution of the Swahili news categories. we find out that we have an imbalance distribution.




![Target dist](https://github.com/JohnNkakuyia/Swahili-Language-News-Classification-/blob/main/images/target_dist.jpg) 
| category  | count |
|-----------|-------|
| Kitaifa   | 2000  |
| michezo   | 1720  |
| Biashara  | 1360  |
| Kimataifa | 54    |
| Burudani  | 17    |

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

|    Model                   | Accuracy | Log Loss |
|---------------------------|----------|----------|
| Logistic Regression       | 0.847050 | 0.450319 |
| Decision Tree Classifier  | 0.722826 | 9.963229 |
| RandomForestClassifier    | 0.825311 | 0.580609 |
| MultinomialNB             | 0.801242 | 0.514762 |
| XGBClassifier             | 0.843168 | 0.468921 |
| LGBMClassifier            | 0.853261 | 0.487481 |
| CatBoostClassifier        | 0.839286 | 0.437096 |


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

| Metric    | LogisticRegression | MultinomialNB | CatBoostClassifier |
|-----------|--------------------|---------------|--------------------|
| Precision | 0.852504           | 0.828837      | 0.850330           |
| Recall    | 0.847050           | 0.801242      | 0.839286           |
| F1-Score  | 0.849144           | 0.806635      | 0.843752           |
| Accuracy  | 0.847050           | 0.801242      | 0.839286           |



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
On the stacking model, we achieved an accuracy of 0.8524, implying that approximately 85.24% of the model's predictions were correct. Additionally, with a log loss of 0.3984, it suggests that the model's predictions are closely aligned with the actual probabilities.

Upon examining the confusion matrix, the model exhibits robustness in its predictions, effectively capturing the underlying patterns and features of the data. There are no instances of mislabeled posts, indicating consistent and precise predictions across all classes. This reliability suggests that the model can be trusted for accurate classifications. Given its strong performance, the model may be suitable for deployment in real-world applications where accurate classification is crucial.

## findings
* **Challenges with Rare Classes:** The model faces difficulties in correctly classifying instances belonging to rare classes such as "Burudani" and "Kimataifa." This is evident from the lower true positive values for these classes in the confusion matrix.
* **Model Performance:** The stacking model achieved a commendable accuracy of 85.24%, indicating that approximately 85.24% of the predictions were correct. The low log loss of 0.3984 further suggests that the model's predictions closely align with actual probabilities.
* **Robust Predictions:** The confusion matrix reveals that the model exhibits robustness in its predictions, effectively capturing underlying patterns and features of the data. There are no instances of mislabeled posts, indicating consistent and precise predictions across all classes.

## Conclusion
* **Reliable Model:** The model demonstrates reliability in its predictions, as evidenced by its strong performance and consistent accuracy across various classes. This reliability instills confidence in the model's capability for accurate classifications.
* **Suitability for Deployment:** Given its robust performance, the model appears suitable for deployment in real-world applications where accurate classification of Swahili news articles is crucial.
  
## Recommendations 
* **Addressing Rare Class Challenge:** To improve classification performance for rare classes like "Burudani" and "Kimataifa," consider strategies such as collecting more data specific to these classes 
* Investigate domain adaptation techniques to address language variations and improve model robustness across different text genres.
* Collaborate with linguists and domain experts to develop specialized resources and tools for Swahili language processing tasks.

## Next Step

* further analysis is warranted to ensure the model's robustness across diverse datasets or conditions and to identify any potential biases or limitations.

