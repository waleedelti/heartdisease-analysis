# Heart Disease Analysis

According to the CDC, in 2020, Heart Disease was the leading cause of death in the USA for most races. How do we go about tackling this issue as a society? Investigating what the **key correlations** were that played a role in Heart Disease diagnoses was a good place to start. Once we could understand the factors correlated with Heart Disease, we would be able to determine which preventative measures were needed to minimize future diagnoses by using predictive models that calculated who might be at risk. Through my analysis, I aimed to answer:

- What was the impact Age and Sex had on the likelihood of being diagnosed with Heart Disease?  
- **Hypothesis**: Age played an influential role in the likelihood of Heart Disease diagnosis, but Sex was not an influential factor in the likelihood of Heart Disease.

## Objectives

There were many factors that could influence someone developing Heart Disease, but my goal was to specifically investigate the correlation between one's age, their sex, and the likelihood of being diagnosed with Heart Disease. I wrangled the dataset using **tidyverse** to mutate the categorical columns into numerical ones, renamed the columns, and manipulated the data for investigation. After that, I used the **ggplot2** package to create a variety of plots and correlation figures to analyze the relationship of age and sex with heart disease, as well as their impact relative to other variables. I utilized the **DT** and **gt** packages to create interactive tables. Because Heart Disease is binary, I decided to conduct a **logistic regression analysis**. The logistic regression model helped determine the relationship between Age/Sex and Heart Disease in my dataset. For missing data handling, I used the **Amelia** package.

## Data

The dataset used for this project came from an annual survey the CDC conducted in the USA with more than 400,000 respondents. A Kaggle user, Kamil Pytlak, took the most relevant factors that influenced heart disease (directly or indirectly) from the original dataset and constructed a new condensed dataset. The **Indicators of Heart Disease 2020** dataset contains 319,795 observations of 18 variables. I used **tidyverse** to rename columns and create variations of the dataset where the values were numeric for correlation analysis and factors for missing data handling. The 'Age' column values were converted from range values to the midpoint of the ranges for analysis (e.g., 55-59 to 57). There was no missing data in the original dataset, so I randomly deleted 7% of the data using the **prodNA** function in the **missFOREST** package.

## Results

To begin my analysis, I created exploratory graphs to investigate the relationships within the data. My first figure was a summary table of the dataset to get initial insights on the structure and details of each variable. The dataset included various types of variables, including genetic, health history, and personal health opinions.

I created various graphs using **ggplot2** to analyze the relationship between age and sex and the likelihood of being diagnosed with heart disease. The analysis showed that although male responses accounted for 47.52% of the survey, 58.97% of heart disease diagnoses in the dataset were among males. Both graphs skewed left, indicating a significant increase in positive diagnoses after age 50.

Due to the binary nature of the Heart Disease variable, I chose to use logistic regression to explore the relationship further. The logistic regression model results indicated that each additional year of age increased the odds of heart disease by 0.07, while males had a 0.67 higher log odds than females. The p-values were statistically significant (all < 0.05).

To assess the model's performance, I plotted an ROC curve. The AUC (Area Under the Curve) was 0.7461, indicating that the model performed better than random guessing (0.5) but was not perfect (1.0). 

A correlation heat map visually conveyed the strength of associations between variables related to heart disease. The heat map highlighted that Sex had a low positive correlation (0.02) with heart disease, whereas Age had a moderate positive correlation (0.23).

## Missing Data

This dataset was initially clean with no missing values, so I generated missing data using the **prodNA** function from the **missForest** package, introducing 7% missing values. After generating the missing data, I performed multiple imputation to fill in the gaps. Using the **Amelia** package, I created five new imputed datasets. The consistency of the results reinforced that Age was a significant predictor of heart disease.

Finally, I applied **Rubin’s Rules** to combine the imputed datasets using the **mi.mield** function. 

## Limitations

This dataset relied on survey responses, which may have introduced bias due to inaccurate self-reporting. The way questions were phrased could also have influenced responses. Additionally, there may have been unmeasured variables that affected the relationship between age, sex, and heart disease.

## Conclusion

Based on the results and visualizations, Age was indeed an influential factor in heart disease likelihood, leading to a failure to reject this part of the null hypothesis. Although the correlation heatmap indicated that Age was the strongest predictor, the logistic regression models supported the influence of Sex as well. This nuanced analysis highlighted the importance of both variables in understanding heart disease diagnosis.
