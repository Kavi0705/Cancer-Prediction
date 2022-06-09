# FinalProject_050322

## Topic and Reason

Breast Cancer Data diagnostics:

- Cancer is the second leading cause of death worldwide. According to Breastcancer.org, women in the United States suffer from higher death rates due to breast cancer than most types of cancers.
- About 1 in 8 U.S. women (~13%) will develop invasive breast cancer over the course of her lifetime.
- b. In 2022, an estimated 287,850 new cases of invasive breast cancer are expected to be diagnosed in women, along with 51,400 new cases of non-invasive (in situ) breast cancer.
- About 2,710 new cases of invasive breast cancer are expected to be diagnosed in men in 2022. A man’s lifetime risk of breast cancer is about 1 in 833.
- About 43,250 women in the U.S. are expected to die in 2022 from breast cancer. Death rates have been steady in women under 50 since 2007, but have continued to drop in women over 50. The overall death rate from breast cancer decreased by 1% per year from 2013 to 2018. These decreases are thought to be the result of treatment advances and earlier detection through screening.

## Data Source

[Breast Cancer Wisconsin Diagnostic Data Set](https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data)

This dataset from Kaggle shows the Wisconsin breast cancer diagnostic data set for predictive analysis. Ten values were evaluated for each cell nucleus of the breast mass. The variables in this dataset focus on the size and the texture to categorize the cancer into benign or malignant cancer.

#### Size Measures:
- Radius: mean of distances from the center to points on the perimeter
- Radius worst: "worst" or largest mean value for mean of distances from center to points on the perimeter
- Perimeter: size of the core tumor
- Fractal dimension: mean for coastline approximation -1
- Radius se: standard error for the mean of distances from center to points on the perimeter
- Fractal dimension: mean for "coastline approximation" – 1

#### Texture Measures:
1.	Smoothness: Local variation in radius lengths
2.	Compactness: Mean of Perimeter ^2/area – 1.0
3.	Concavity: mean of severity of concave portions of the contour
4.	Concave Points: mean of number of concave portions of the contour
5.	Texture: standard deviation of gray scale values
6.	Texture se: standard error for standard deviation of gray-scale values
7.	Smoothness se: standard error for local variation in radius lengths
8.	Compactness se: standard error for perimeter^2 / area - 1.0
9.	Texture worst: "worst" or largest mean value for standard deviation of gray-scale values


### Diagnosis:
- Benign: growth that is not considered cancer. It will not invade nearby tissue or spread to other parts of the body.
- Malignant: cancerous cells that invade nearby tissue and spread to other parts of the body.
•	The stage of a breast cancer is determined by the cancer’s characteristics. For instance, the size and the presence or absence of hormone receptors. 
•	Why is the stage important?
- Determine the prognosis
- Determine best treatment option 
•	How is breast cancer staged?
- Stage of 0 through IV.
- Stage 0: non-invasive (in original location) to Stage IV: invasive and invaded other parts of the body.


•	Size of Tumors:
- Primary breast tumors vary in shape and size. The smallest lesion that can be felt by hand is typically 1.5 to 2 centimeters (about 1/2 to 3/4 inch) in diameter. Sometimes tumors that are 5 centimeters (about 2 inches) — or even larger — can be found in the breast.

Source: This information is provided by Breastcancer.org.


## Question to Answer
- Which features have the greatest impact on breast cancer diagnosis?
- Which classification model has the greatest accuracy of predicting breast cancer diagnosis?

## Data Exploration

Descriptive statistics was used to calculate the mean, standard deviation, min/max, and percintiles of the ten values. This dataset includes the mean, the standard error, and "worst" (defined as the mean of the three largest values). Histograms, scatterplots, and bar charts were used to compare values of the diagnosis groups (M: malignant, B: benign). 

Examples below:

![radius](https://github.com/Copperminer02/FinalProject_050322/blob/d8491831c5da54cb9a1564146c964e6eb69d77d5/avg_radius.png)
![smooth](https://github.com/Copperminer02/FinalProject_050322/blob/d8491831c5da54cb9a1564146c964e6eb69d77d5/avg_smooth.png)


## Data Analysis


### Create a Training and Test Set of Data
- accuracy, recall, F1 score and precision. 
- The F1 score will be used to measure the model’s accuracy and it’s a mean of precision and recall. 
- F1 scores closer to 1 indicate lower false positives and lower false negatives.
- The recall score measures the extent to which the model can correctly identify true positives. 
- The accuracy score is the relationship between the number of correct predictions and total number of predictions. 
- The precision score represents the relationship between the true positives and all positives. 

### Model Classification: 
- Build classification models to evaluate performance on the training data 
- Supervised ML Models: random forest, decision trees, logistic regression, random forest, support vector mechanisms. 
- The ML models robust against overfitting and consistent with the ML algorithms used in biomedical research.

Supervised Models Classification Report
Logistic Regression Models: Using Logistic Regression to Predict Breast Cancer Diagnosis:
   precision    recall  f1-score   support

           0       0.95      0.97      0.96        90
           1       0.94      0.91      0.92        53

    accuracy                           0.94       143
   macro avg       0.94      0.94      0.94       143
weighted avg       0.94      0.94      0.94       143

Support Vector Mechanisms Using All Features
precision    recall  f1-score   support

           0       0.95      0.99      0.97        90
           1       0.98      0.91      0.94        53

    accuracy                           0.96       143
   macro avg       0.96      0.95      0.95       143
weighted avg       0.96      0.96      0.96       143

Decision Trees Using All Features
Accuracy Score : 0.9090909090909091
Classification Report
              precision    recall  f1-score   support

           0       0.97      0.87      0.92        84
           1       0.84      0.97      0.90        59

    accuracy                           0.91       143
   macro avg       0.91      0.92      0.91       143
weighted avg       0.92      0.91      0.91       143

Random Forest Using All Features
Accuracy Score : 0.965034965034965
Classification Report
              precision    recall  f1-score   support

           0       0.98      0.96      0.97        84
           1       0.95      0.97      0.96        59

    accuracy                           0.97       143
   macro avg       0.96      0.97      0.96       143
weighted avg       0.97      0.97      0.97       143

Features by Importance:

[(0.14880270244945648, 'concave points_worst'),

(0.11373771437548913, 'perimeter_worst'),

(0.09863784160265764, 'concave points_mean'),

(0.08812880462600081, 'radius_worst'),

(0.07912421470226502, 'area_worst'),

(0.07183289243373002, 'concavity_mean'),

(0.07112163118155258, 'concavity_worst'),

(0.04697855582757448, 'area_se'),

(0.046698351295552526, 'perimeter_mean'),

(0.04013201279677222, 'area_mean'),

(0.02980723922949247, 'radius_mean'),

(0.01811650137649341, 'radius_se'),

(0.017829553286640487, 'compactness_mean'),

(0.017667815814524805, 'smoothness_worst'),

(0.015370654621446754, 'compactness_worst'),

(0.014609224606356414, 'texture_mean'),

(0.013653600343979147, 'texture_worst'),

(0.008432478543931065, 'perimeter_se'),

(0.007305341598365188, 'fractal_dimension_worst'),

(0.007211764698972296, 'concave points_se'),

(0.006938417964144726, 'symmetry_worst'),

(0.006881960462587396, 'concavity_se'),

(0.004915601279205796, 'smoothness_mean'),

(0.004379183625492492, 'texture_se'),

(0.004298387111451206, 'symmetry_se'),

(0.00393214080195755, 'symmetry_mean'),

(0.0035555755555820986, 'fractal_dimension_se'),

(0.003525656418915917, 'compactness_se'),

(0.003288730557037211, 'fractal_dimension_mean'),

(0.0030854508123727437, 'smoothness_se')]


# Conclusion:
 The best model to be used for diagnosing breast cancer as found in this analysis is Random Forest.
 
 The features with the greatest impact included: concave points, perimeter, radius and area.

# Tableau

[Tableau Link](https://public.tableau.com/shared/GS52HRHB8?:display_count=n&:origin=viz_share_link)

- The tableau visualizations represent the 569 samples of the breast cancer diagnosis dataset with 357(63%) of the samples being benign and 212(37%) being malignant. Relationships between the means of all ten values are visualized in the pair plot. This helps us understand the relationship between the individual features and how they are distributed between diagnosis types. 

![tableau](https://github.com/Copperminer02/FinalProject_050322/blob/1c4cdafdbe71f52a3d50910eacbc744e0d84b1d1/tableau1.png)

![tableau](https://github.com/Copperminer02/FinalProject_050322/blob/1c4cdafdbe71f52a3d50910eacbc744e0d84b1d1/tableau2.png)

## Future Analysis/Future Changes

Future Analysis would include other clinical characteristics: lymph node involvement and metastasis to determine which clinical characteristic had the greatest impact on breast cancer diagnosis.
