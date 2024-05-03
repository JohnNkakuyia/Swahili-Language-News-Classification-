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

