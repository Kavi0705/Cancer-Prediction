# Cancer Death Rates predictions from Country Sustainability data

## Topic and Reason
- Analyzing Global Cancer Death Rates for trends to Socioeconomic Factors.
#### Reason?
- Cancer is the second leading cause of death worldwide, with over 100 different types. The data collected from cancer death rates can be used to track the progression of cancer while also contrasting those rates to the sustainability of countries around the world. Our purpose in this project is to better understand these socioeconomical trends of 149 countries and explore whether those traits have any relation to with cancer mortality. 

## Description of Data Source
[Link to Cancer Death Rates](https://www.kaggle.com/datasets/bahadirumutiscimen/cancer-death-rates-in-the-world-19902019)

- This dataset from Kaggle shows the total cancer deaths by type of cancer by country. 

[Link to Global Sustainability](https://www.kaggle.com/datasets/truecue/worldsustainabilitydataset?select=WorldSustainabilityDataset.csv)

- This dataset, also pulled from Kaggle, tracks sustainability metrics in 173 countries. We initially evaluated utiliozed all factors 
### Factors Defined for World Data

- Total Natural Resource Rents ($ of GDP) : sum of oil, natural gas, coal, mineral, forest rents

- Particulate Emission Damage: damage due to exposure of a population to air pollution

- Renewable Energy Consumption: the sum of the gross inland consumption of energy from renewable sources

- Natural Resource Depletion (% of GNI): sum of net forest depletion, energy depletion, mineral depletion

- Carbon Dioxide Damage (% of GNI): cost of damage due to Co2 emissions from fossil fuel use & manufacture of cement

- Production-Based Emissions of CO2: calculates emissions generated from domestic production of goods and services

- GDP: gross domestic product, measures monetary value of goods and services produced in a country

- Net Forest Depletion (% of GNI): calculated as product of unit resource rents & the excess of roundwood harvest over natural growth

- Life Expectancy

- Population

- % Population living in rural area

- % Population living in urban area


## Question to answer
- Can socioeconomic factors be used as a predictive tool to predict the rates of death by different cancers?
- Which factors regression weights will be the most predictive of each cancer?


## Data exploration

Both datasets were pulled from Kaggle as CSV's and imported into Jupyter Noetbook.  We selected the the 13 most common types of cancer to explore as our dependent variables. This simplified the amount of data to handle. Column names for the independant sustainibility variables were also changed to simplify data handling. 

Using a for loop statement, each variable was checked to see the percentage of null values. Items with greater than 10% null values were explored further to determine if there were enough values to include in the dataset.

![image](https://user-images.githubusercontent.com/91850824/169675699-713be0c8-fb34-4e36-b431-e16db9daabd0.png)

![image](https://user-images.githubusercontent.com/91850824/169675750-c2834f20-a0e8-4988-b8b9-0875d82478b4.png)

Our personal judgement in the applicability of each features potential to contribute to cancer deaths was also used to determine the final feature list:

![image](https://user-images.githubusercontent.com/91850824/169675790-347f369f-46ae-4aad-8be7-b54484e9d179.png)

Remaining null values were dropped as were the year and the continent.

Because each dataset contained information by year for each country, all values were averaged via groupby and a composite of the like years merged were used for each country.  From this dataframe each country's population was divide by 100,000 to limit the influence of the larger value to the rest of the dataset and the cancer deaths were divided by the countries population to create an equal standard deaths per 100,000 person capita for each cancer. Likewise GDP was standardized by subtracting each GDP by $100,000,000. 

## Analysis 

### Machine Learning

#### K-Means

To explore possible relationships to each country based solely on sustainability data PCA was used to reduce the data to 4 components (4 components were chosen due to a resultant 81.6% data retention using PCA after standarizing the data.  An Elbow curve indicated that 4 clusters were appropriate for unsupervised k-means analysis. 

![image](https://user-images.githubusercontent.com/91850824/169676071-89db1aa1-d552-44e0-97cb-404147348305.png)

Each identified class was added back to the dataset to be used in regression analysis.

#### Regression Analysis

Since our identified dependant variables are continuos data points, regression was the best option for prediction.  Three regression models were ran: Multiple Linear Regression, Random Forest regression, and Decision Tree Regression.

To process all cancer types more efficiently, each cancer was looped and set as the key value for a resulting dataframe that included the specific cancer chosen and the cleaned sustainability features.
![image](https://user-images.githubusercontent.com/91850824/169676225-287190a2-79cb-4232-8233-11e4775a3533.png)

Utilizing the dictionary of dataframes, each cancer was looped and ran against each regression model.  The training and testing scores were printed above a scatter plot comparing predicted to actual death rates.

![image](https://user-images.githubusercontent.com/91850824/169676300-de1db9da-6d12-45e0-942e-1fe724cc8b01.png)

The predicted values for each cancer, the model weights/coefficients, and the training and testing scores were saved in a new dataframe with each cancer as the column header and the features as the index.  

The results for each model were then exported to postgressql to be merged for our Tableau dashboard.  Also, a copy of the feature data (with the country names included) and the predicted values for each regression was combined into a single dataframe and exported to postgres.

![image](https://user-images.githubusercontent.com/91850824/169676403-3274c573-ee47-40c5-8256-5c8d51e80826.png)

### SQL Mockup Data Flow

- An eco_cancer_data database was created in postgressql.
- Within the database the following tables were imported.
     - cancer_world - all used feature data and predictions
     - decision_tree_regression - model results and wieghts by cancer type for decision tree regression
     - linear_regression - model results and wieghts by cancer type for linear regression
     - random_forest_regressor - model results and wieghts by cancer type for random forest regression

- The cancer_ml_regressions table was created via joins of the regression model results to create 1 simple table for the tableau dashboard
- cancer_ml_regressions  and cancer_world exported to csv for import into tableau.

## Dashboard
Final result Dahsboard and visualization performed with Tableau. Basic visualization include examination of successful regression model results, further looks into the heaviest weighted features compared to each cancer type, and an overview of the countries with the highest death rate based on the highest weighted features.

[Dashboard click here](https://public.tableau.com/app/profile/josh.shutey/viz/Cancer_eco_data/CancerDeathRatePredictionsBasedonSustainabilityData)

![image](https://user-images.githubusercontent.com/91850824/170844640-2c0a487e-1c80-4e2e-90d9-d08e33d4b143.png)

![image](https://user-images.githubusercontent.com/91850824/170844632-3db41667-abf8-41d1-bda1-5324ef9c1549.png)

![image](https://user-images.githubusercontent.com/91850824/170844642-68bbfa49-0686-4f43-9acc-338473e1200b.png)

![image](https://user-images.githubusercontent.com/91850824/170844648-ec2f11d8-2782-46f4-a400-1ad9599e5655.png)

![image](https://user-images.githubusercontent.com/91850824/170844652-0cb42fbb-e136-44e6-aef0-ee71955f22ad.png)

![image](https://user-images.githubusercontent.com/91850824/170844658-51626360-a67f-40e6-b52a-a4692e1ad3fb.png)

## Results and Summary

As can be seen from the dashboard images, we were able to create models with training and testing scores above 80.  Given the nature of this analysis, the independant variables could in no way encompass every factor for each of these cancers and model accuracy over 60 are deemed successful enough to conclude *some* common statistical trending.  Of all models ran, the Random Forest regressor was teh most successful.  

All of the independant variables chosen represent a measure of each countries wealth.  The kmeans analysis results can be seen below.

![image](https://user-images.githubusercontent.com/91850824/170844866-4e7247d8-cc0e-466c-9a3f-1373a8a30df0.png)

The interesting result is that 3 variables continually had a vast majority of weights in the model: **Particulate Emssion Damage, Life Expectancy, and Natural Resoureces Rent**.  Some logical inferences can be made, especially with life expectancy, that the longer one lives the more likely one will die of cancer; however, using this analysis to conclude any relationship concretely would be in error.  Overall, the cancer death rates appeared to generally trend higher to more wealthy countries.  This could be the result of many factors: cancer identification, early deaths to other causes, etc.   

## Future Analysis/Changes

Further more meaningful analysis could be to explore the 3 top features by weight and look at the range where cancer death rates are the highest. (See image below)

![image](https://user-images.githubusercontent.com/91850824/170845098-b8d5aeea-74ff-4418-880f-479e67236afa.png)

Many of these cancers show a wide spread amongst countries with similar economic indicators.  Conversly, as cancer deaths decrease, the poorer countries show less range in cancer deaths.  The question remains why do the more economically advanced countries trend to higher cancer deaths and what makes some of these countries more successful against different cancers.  
