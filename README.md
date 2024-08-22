# Predicting the Quality of White Wine

## Overview
The goal of this project is to analyze the white wine dataset and build a predictive model that can offer insights to CVRVV (The Viticulture Commission of the Vinho Verde Region), a wine certification agency, to gain a deeper understanding of factors that affect white wine quality and to aid wine experts during sensory analysis. 

Various algorithms like Multiple Logistic Regression, K-Nearest Neighbors, Support Vector Machine, Random Forest, and Extreme Gradient Boosting (XGBoost) were combined with data preprocessing techniques to come up with the final model. The XGBoost with SMOTE outperforms the other models, with a weighted f1 score of 77% during testing, making the model useful in predicting the category of quality where a wine belongs. 


## Business Understanding
In Portugal’s wine industry, a crucial aspect of quality assurance is the certification and evaluation of wines. During the certification phase, analytical tests are utilized to measure the physicochemical components of the wine, and the wine quality is evaluated using sensory analysis by a panel of experts.  

This project aims to develop a machine learning model to predict white wine quality based on objective analytical test results with the goal of reducing the inherent subjectivity present in human sensory analysis. The insights from this project will help the CVRVV (The Viticulture Commission of the Vinho Verde Region) to gain a deeper understanding of the factors that affect wine quality and to aid wine experts during sensory analysis. The CVRVV is a wine certification agency with the goal of improving the quality and marketing of Vinho Verde wines. 

**Deliverables:**
1. [One-page executive summary that would be presented to stakeholders.](https://docs.google.com/presentation/d/1oDFPnfKkoBjCuXTg55KydqY83c-4uBwVb0ZATAKvQlY/edit?usp=sharing)
2. [Complete code Python notebook](https://github.com/je-marco/Wine-Quality-Prediction/blob/cc927f5e9b527f70a71bb0c84fea4cc1d8a1e180/wine_quality_prediction.ipynb)

**Scope and Limitation:**  
Due to the constraint of data imbalance, the classes of wine that will be predicted in this modeling effort are the following: 
1. **low** (quality score of 0-4)
2. **medium** (quality score of 5-6)
3. **high** (quality score of 7-10)


## Data Understanding
The dataset was taken from [University of California Irvine Machine Learning Repository](https://archive.ics.uci.edu/dataset/186/wine+quality). Each entry in the dataset is the result of a given test (analytical or sensory). The type of wine represented in this dataset is the white variant of the  Portuguese "Vinho Verde" wine.

It contains 4,898 rows&mdash;each representing all test results of a unique white wine sample. It has 12 columns which are listed below: 

  Variable  |Description |
-----|-----|
fixed_acidity|Most acids involved with wine are fixed or nonvolatile (*do not evaporate easily*) [3.8&ndash;15.9]|
volatile_acidity|The amount of acetic acid in wine, which at too high of levels can lead to an unpleasant vinegar taste [0.1&ndash;1.6]|
citric_acid|Found in small quantities, citric acid can add 'freshness' and flavor to wines [0.0&ndash;1.7]|
residual sugar|The amount of sugar remaining after fermentation stops [0.6&ndash;65.8]|
chlorides|The amount of salt in the wine [0.01&ndash;0.61]|
free_sulfur_dioxide|The free form of SO2 exists in equilibrium between molecular SO2 (*as a dissolved gas*) and bisulfite ion [1&ndash;289]|
total_sulfur_dioxide|Amount of free and bound forms of sulfur dioxide gas (SO2) [6&ndash;440]|
density|[0.987&ndash;1.039]|
pH|Describes how acidic or basic a wine is [2.7&ndash;4.0]|
sulphates|A wine additive which can contribute to sulfur dioxide gas (SO2) levels, which acts as an antimicrobial and antioxidant [0.2&ndash;2.0]|
alcohol|[8.0&ndash;14.9]|
quality|Based on sensory data [0&ndash;10]|


**Note:** The wine samples came from different manufacturers from the northwest region of Portugal and were tested at the official certification entity called CVRVV. Therefore, expect a different range of results for each given test. 


## Modeling and Evaluation

**Modeling results:**
Algorithm&ndash;Preprocessing Technique|Modeling Process|f1 score
-----|-----|----|
XGBoost&ndash;Baseline model| Evaluation| 0.762480	
XGBoost&ndash;Baseline model| Testing| 0.777840	
XGBoost&ndash;With feature engineering| Evaluation| 0.771266	
XGBoost&ndash;With feature engineering| Testing| 0.752879
XGBoost&ndash;With SMOTE| Evaluation| 0.764714
XGBoost&ndash;With SMOTE| Testing| 0.768106	
SVM&ndash;With PCA| Evaluation| 0.740807
SVM&ndash;With PCA| Testing| 0.765861
XGBoost&ndash;With SMOTE & PCA| Evaluation| 0.744526	
XGBoost&ndash;With SMOTE & PCA| Testing| 0.719466	

* During model selection, the evaluation results of the baseline model are very close to the results of the model with SMOTE. Still, the baseline model scored higher during the prediction of the test set. However, the model with SMOTE has more consistent f1 score results during evaluation and testing.
* Because of the class imbalance, the Baseline model is more effective in classifying medium-class wines, decreasing its ability to predict low and high-quality wine; a wine sample was even classified as high-quality when in reality, it is of low quality. To eliminate the bias towards the majority class, oversampling was done to balance the classes in the training set using SMOTE.

**Feature Importance:**

![feature_importance_plot](https://github.com/je-marco/Wine-Quality-Prediction/blob/cc927f5e9b527f70a71bb0c84fea4cc1d8a1e180/Feature%20Importance%20for%20XGBoost%20model%20with%20SMOTE%20final.png)

The feature importance graph confirms that key predictors identified during exploratory data analysis closely align with the top features. The modeling effort confirms that `free sulfur dioxide`, `alcohol`, `volatile acidity`, and `total sulfur dioxide` are key factors in predicting wine quality. 

**Confusion Matrix:**

![confusion_matrix](https://github.com/je-marco/Wine-Quality-Prediction/blob/cc080a5adb3ac80718d09fa92e06b5e2a2503587/Confusion%20Matrix%20for%20XGBoost%20model%20with%20SMOTE.png)

The XGBoost with SMOTE outperforms the other models. From the confusion matrix, the model accurately classifies 88% of medium-quality wines (519/593), struggles with low-quality wines (10/35, 29%), and moderately performs well with high-quality ones (85/165, 52%). It exhibits bias towards medium-quality wines, misclassifying 25 low-quality and 80 high-quality wines as medium-quality wines. Despite this, the model still performs reasonably well, with a weighted f1 score of 77%, making it helpful in predicting wine quality.


## Conclusion and Recommendation
* The modeling effort demonstrates that physicochemical indicators can reliably reflect white wine quality, thus serving as a valuable tool for improving both the quality evaluation and the wine itself.
  
* Integrate the model into a decision support system during wine tasting to improve the speed and consistency of quality evaluations. For instance, the wine expert could only repeat the tasting if the quality score does not belong to the class predicted by the model.

* Improve the effectiveness of the model by adding new features such as grape variety or combination of grape varieties, wine selling price, color, phenolic compounds, and glycerol levels.

* Share the findings of this project with wine manufacturers, particularly the variables that can be controlled during the production process, such as alcohol content, volatile acidity, free sulfur dioxide levels and pH,  and residual sugars. 
 
## Note
Throughout this project, you'll see references to the problem-solving framework, PACE. The Python notebook components are labeled with the respective PACE stages: Plan, Analyze, Construct, and Execute.

  
