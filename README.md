![Neuro Compass Foundation Logo](https://imgur.com/Dgselim.png)
# Global Mental Health Insights
### A Data-Driven Analysis by Neuro Compass Foundation

---

##### Date: 11 Nov 2024
##### Prepared by: Kuodo Cheok, Data Analyst
---

![Screenshot of dashboard](https://imgur.com/r19cMRt.jpg)

---

## Project Overview

As part of the Neuro Compass Foundation’s research team, my goal as a data analyst is to conduct a comprehensive analysis of five major disorders: Anxiety, Bipolar Disorder, Depression, Eating Disorder, and Schizophrenia.

This analysis will uncover patterns and trends in how these disorders are distributed globally and how they connect to socioeconomic indicators such as GDP, income levels, and suicide rates. We looked closely at geographical and temporal distributions to highlight disparities that need attention.

These findings will advance our foundation’s mission by raising awareness of the critical connections between mental health and socioeconomic factors. They will inform advocacy efforts, shape policy decisions, optimize resource distribution, and drive impactful, targeted mental health interventions globally.

---

## Table of Contents

- [Project Objectives](#project-objectives)
- [Description of Datasets](#description-of-datasets)
- [Data Understanding and Preparation](#data-understanding-and-preparation)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Data Visualization in MS Power BI](#data-visualization-in-ms-power-bi)
- [Model Development and Performance Evaluation](#model-development-and-performance-evaluation)
- [Tools and Resources](#tools-and-resources)
- [Actionable Recommendations](#actionable-recommendations)
- [Retrospective: Buds, Roses and Thorns](#retrospective-buds-roses-and-thorns)
- [Conclusion](#conclusion)

---

## Project Objectives
- Explore the prevalence and distribution of different mental disorders globally, such as Anxiety, Bipolar, Depression, Eating Disorders and Schizophrenia.
- Investigate the relationship between disorder prevalence, Suicide Rates and other socialeconomics indicators such as GDP Per Capita and Income levels.
- Identify correlations between variables and select primary target for further analysis and prediction.
- Analyse measurable insights through visuals such as trends, correlations, geographical and temporal distributions, and relevant charts.
- Examine regional disparities, highlighting outliers and significant deviations, highlighting countries with the highest and lowest disorder prevalence.
- Predict targeted mental health outcomes using machine learning models based on socioeconomic and temporal features.
- Deliver a comprehensive report and presentation, showcasing analytical skills and advocating for data-driven interventions.

---

## Description of Datasets

I have sourced a total of 4 datasets to be used for this analysis.

#### Dataset 1:
#### 1- mental-illnesses-prevalence.csv
This dataset contains information about the prevalence of mental health disorders in countries across the globe.

source: https://www.kaggle.com/datasets/imtkaggleteam/mental-health

![Screenshot of dashboard](https://imgur.com/7aW6zQ2.jpg)


**`Entity:`** Unique identifier for each country or region included in the data set. (String)

**`Code:`** Unique code associated with an Entity/Country or region included in the data set. (String)

**`Year:`** Year that the data about that particular Entity/Country was collected. (Integer)

**`Schizophrenia disorders (share of population) - Sex: Both - Age: Age-standardized:`** Percentage of people with schizophrenia in that country/region during that year. (Float)

**`Depressive disorders (share of population) - Sex: Both - Age: Age-standardized:`** Percentage of people with depression in that country/region during that year. (Float)

**`Anxiety disorders (share of population) - Sex: Both - Age: Age-standardized:`** Percentage of people with anxiety disorders in that country/region during that year. (Float)

**`Bipolar disorders (share of population) - Sex: Both - Age: Age-standardized:`** Percentage of people with bipolar Disorder in that country/region during that year. (Float)

**`Eating disorders (share of population) - Sex: Both - Age: Age-standardized:`** Percentage of people with eating disorders in that country/region during that year. (Float)

#### Dataset 2:
#### suicide homicide gdp.csv
This dataset contains information about the homicide, suicide, GDP and income level of different countries.

source: https://www.kaggle.com/datasets/prasertk/homicide-suicide-rate-and-gdp

![Screenshot of dashboard](https://imgur.com/GUIs6s1.jpg)


**`country:`** Unique identifier for each country included in the data set. (String)

**`iso3c:`** Unique code associated with a Country included in the data set. (String)

**`iso2c:`** Unique code associated with a Country included in the data set. (String)

**`year:`** Year that the data about that particular Country was collected. (Integer)

**`Intentional homicides (per 100,000 people):`** Intentional homicide rate per 100k people. (Float)

**`Suicide mortality rate (per 100,000 population):`** Suicide rate per 100k people. (Float)

**`GDP (current US$):`** Gross Domestic Product of each Country in that year was collected. (Float)

**`GDP per capita, PPP (current international $):`** Gross Domestic Product per person of each Country in that year was collected. (Float)

**`adminregion:`** World Bank region in the world. (String)

**`incomeLevel:`** World Bank income level. (String)

#### Dataset 3:
#### master.csv
This dataset was originally considered but it contained too many missing data. However, it does contain data of **`Puerto Rico`** to serve as supplementary support for missing data of dataset 2, which is useful. For both dataset 3 and 4, I require only the country, year and suicides/100k pop.

source: https://www.kaggle.com/datasets/russellyates88/suicide-rates-overview-1985-to-2016

![Screenshot of dataset](https://imgur.com/B7eAsq5.jpg)

#### Dataset 4:
#### who_suicide_statistics.csv
This dataset contain data to serve as supplementary support for missing data of dataset 2, **`Dominica`**.

source: https://www.kaggle.com/datasets/szamil/who-suicide-statistics

![Screenshot of dataset](https://imgur.com/B7eAsq5.jpg)

---

## Data Understanding and Preparation
Here is a summary of the steps performed using jupyter notebook.
The working file can be found here:
[Link to .IPYNB file](https://github.com/Kuodo79/2024SCTP-DataAnalysis-Capstone-NCF/blob/main/Global%20Mental%20Health%20Insights.ipynb)

#### Dataset 1:
- **`Code`** contains null. The reason behind that is that the Entity covers several countries and can't be represented with a single code. As there are valuable data within these countries, I have decided to remove the **`Code`** column entire instead of removing records with null **`Code`**.
- **`Entity`** shall be changed to **`Country`** instead for better clarity and to prepare for data join.
- All the disorders column titles are too long. I shall use shorter name.
- This dataset is clean otherwise and requires no further transformation.

#### Dataset 1 after cleaning:

![Screenshot of dataset](https://imgur.com/yrLGOVv.jpg)

#### Dataset 2:
- **`country`** and **`year`** shall be capitalised to match with other datasets.
- **`iso3c`**, **`iso2c`** and **`adminregion`** to be removed since I do not need them.
- **`GDP (current US$)`** needs to be renamed to **`GDP For Year`**, 2 decimals.
- **`GDP per capita, PPP (current international $)`** needs to be renamed to **`GDP Per Capita, PPP`**, 2 decimals.
- **`incomeLevel`** needs to be renamed to **`Income Level`**.
- **`incomeLevel`** needs to be label encoded to **`Income Level Encoded`**.
- As I am only interested in the suicide and GDP data, **`Intentional homicides (per 100,000 people)`** shall be dropped.
- Ensure that all data in **`Suicide Rate Per 100k`** are in 1 decimal.
- This dataset has several missing data and should be transformed, dropped, and join with dataset 3 when required.

#### Dataset 2 after initial cleaning:

![Screenshot of dataset](https://imgur.com/joHJDwB.jpg)

#### Dataset 3:
**`Puerto Rico`** from dataset 2 contains missing data from **`Suicide Rate Per 100k`** that can be joined by dataset 3.

I only need to the following data from this dataset, and the columns shall be renamed:
- Capitalise **`country`** -> **`Country`**.
- Capitalise **`year`** -> **`Year`**.
- Current data is segregated by gender and age group, I need to transform the data and combine all the records in order to compute **`Suicide Rate Per 100k`** based on overall combined data
- **`country-year`** is useful key for combining the data but I won't need it in the final merger dataframe.

![Screenshot of dataset](https://imgur.com/hvpXAtq.jpg)

#### Dataset 4:
**`Dominica`** from dataset 2 contains missing data from **`Suicide Rate Per 100k`** that can be joined by dataset 4.

I only need to the following data from this dataset, and the columns shall be renamed:
- Capitalise **`country`** -> **`Country`**.
- Capitalise **`year`** -> **`Year`**.
- Current data is segregated by gender and age group, I need to transform the data and combine all the records in order to compute **`Suicide Rate Per 100k`** based on overall combined data. For that, I need to fetch **`Population`** data from the internet.

![Screenshot of dataset](https://imgur.com/lPwHCI6.jpg)

#### Merge Datasets into together:
- Datasets 2's missing **`Suicide Rate Per 100k`** data from **`Puerto Rico`** and **`Dominica`** has been replaced by those in dataset 3 and 4 respectively.
- Now that both dataset 1 and 2 are ready and clean, I shall perform a left join on them with matching **`Country`** and **`Year`**.
- Data should be between **`Year`** 2000 to 2019 as these are the years that contain the most complete data required.
- Drop all duplicates.

#### Observation of merged data:
- **`Cuba`** and **`Djibouti`** contains do not have sufficient **`GDP Per Capita, PPP`**. Initial decision was to keep them and update them using (https://data.worldbank.org/) and (https://statisticstimes.com/). But I failed to find the proper data for them. Therefore, I have decided to drop them both.
- Missing **`GDP Per Capita, PPP`** data from **`Afghanistan`** in **`Year`** 2000 and 2001. Drop only those 2 years.
- Missing **`GDP Per Capita, PPP`** data from **`Sao Tome and Principe`** in **`Year`** 2000. Drop that year.
- Missing **`Suicide Rate Per 100k`** data from **`Puerto Rico`** in **`Year`** 2016 to 2019. Drop those years.
- Missing **`Suicide Rate Per 100k`** data from **`Dominica in`** **`Year`** 2016 to 2019. Drop those years.
- Save the merged dataset as **`Mental Disorder Suicides and GDP.csv`**.
- There is also a **`World`** data under **`Country`** which I wish to save into a **`World Mental Disorder Suicides and GDP.csv`**.
- I need to perform Comparative Trend Analysis on the key disorders. Therefore, I need the metrics to be normalised and **`Scaled`** (0 to 1) to be saved as **`Scaled Mental Disorder Suicides and GDP.csv`**.

#### Merged Dataset:
#### Mental Disorder Suicides and GDP.csv
[Link to .CSV File](https://github.com/Kuodo79/2024SCTP-DataAnalysis/raw/refs/heads/main/Mental%20Disorder%20Suicides%20and%20GDP.csv)
![Screenshot of dataset](https://imgur.com/1OExWI6.jpg)

#### Scaled Merged Dataset:
#### Scaled Mental Disorder Suicides and GDP.csv
[Link to .CSV File](https://github.com/Kuodo79/2024SCTP-DataAnalysis/raw/refs/heads/main/Scaled%20Mental%20Disorder%20Suicides%20and%20GDP.csv)

![Screenshot of dataset](https://imgur.com/udQBQ3G.jpg)

---

## Exploratory Data Analysis (EDA)
- There are a total of **`3149 records`** across **`12 columns`**.
- All data types are in order and there are **`no nulls`**.

#### Statistical Description:
![Screenshot of description](https://imgur.com/UetZwqC.jpg)

- **`Schizophrenia Disorder (%)`**:
    - Mean: **`0.26%`**, with a narrow range **`0.19% to 0.46%`**.
    - Relatively low prevalence with little variation across countries.
- **`Depressive Disorder (%)`**:
    - Mean: **`3.76%`**, with a range from **`1.94% to 7.65%`**.
    - More common than Schizophrenia Order, with moderate variability.
- **`Anxiety Disorder (%)`**:
    - Mean: **`4.12%`**, range from **`1.88% to 8.62%`**.
    - Similar to Depressive Order, indicating widespread prevalence and considerable variation.
- **`Bipolar Disorder (%)`**:
    - Mean: **`0.66%`**, with a narrower range **`0.18% to 1.51%`**.
    - Less prevalent, with low variation.
- **`Eating Disorder (%)`**:
    - Mean: **`0.66%`**, range from **`0.18% to 1.51%`**.
    - Similar to Bipolar Disorder, less prevalent with low variation.
- **`Suicide Rate Per 100k`**:
    - Mean: **`10.69`**, with a wide range from **`0 to 92.6`**.
    - High variability, with a few countries having extremely high Suicide Rates Per 100k.
- **`GDP Per Capita, PPP`**:
    - Mean: **`$16,711`**, range from **`$478 to $141,635`**.
    - Shows significant inequality in economic well-being globally.
- **`Skewness Indication`**:
    - With the exception of Schizophrenia Disorder, many of the variables show signs of positive skew (right-skewed), where a few outliers (extreme values) are pulling the mean higher than the median. I need a Box Plot Chart to further this analysis.


#### Correlation Analysis:

![Screenshot of correlation1](https://imgur.com/9LRbojg.jpg)
![Screenshot of correlation2](https://imgur.com/0pCSGag.jpg)
![Screenshot of correlation3](https://imgur.com/l7dRvDd.jpg)

- **`Eating Disorder (%)`** is strongly positive correlated to **`GDP Per Capita, PPP`** followed by **`Income Level Encoded`** and **`Bipolar Disorder (%)`**.
- **`Eating Disorder (%)`** is borderline positive correlated to **`Schizophrenia Disorder (%)`**
- **`Anxiety Disorder (%)`** is equally highly positive correlated to both **`Eating Disorder (%)`** and **`Bipolar Disorder (%)`**.
- I am quite surprised that **`Suicide Rate Per 100k`** is not significantly correlated to any of the other values. I was quite certain at least **`Depressive Disorder (%)`** should be correlated. This might be due to aggregation of suicide data despite their age group and genders. Also, the 2 dataset are from different sources.
- **`Eating Disorder (%)`** has the most correlation with the entire dataset. It should be the primary target column for analysis.

#### Pairplot:

![Screenshot of pairplot](https://imgur.com/jJALBaW.jpg)

--- 

## Data Visualization in MS Power BI
[Link to .PBIX file](https://github.com/Kuodo79/2024SCTP-DataAnalysis/raw/refs/heads/main/Capstone_NCF_v01.pbix)
- Both **`Merged`** and **`Scaled`** datasets are sorted by **`Country`** and **`Year`**, and there are many parameters to choose from. I have chosen Power BI for its dynamic chart functions. 
- Both datasets are transformed by unpivoting the various disorders columns into **`Disorders`** and **`Percentage`**
- **`Year`** is being converted to actual Year-date using **`Year Date = YEAR(DATE([Year],1,1))`**
- The charts that will be filtered by slicers **`Mental Disorders`**, **`Country`**, and **`Year Date`**.

#### Report 1:
#### Global Prevalence of Mental Disorder(s)

![Screenshot of report1](https://imgur.com/r19cMRt.jpg)

- **`Bubble Map`**: Displays the prevalence of Mental Disorder(s) in the world map.
- **`Line and Clustered Column Chart`**: Ranks the countries based on highest prevalence of selected Mental Disorder(s).
- **`Cards`**: Indicates countries with **`Highest Median %`** and **`Lowest Median %`** of Mental Disorder(s) based on the following measures (DAX).

Observations:
- **`Portugal`** has the **`Highest Median %`** of overall Mental Disorder(s).
- **`Vietnam`** has the **`Lowest Median %`** of overall Mental Disorder(s).
- **`Australia`** has the **`Highest Median %`** of Eating Disorder (%).

![Screenshot of DAX1](https://imgur.com/oqLO86E.jpg)
![Screenshot of DAX2](https://imgur.com/EVc3ZyR.jpg)
![Screenshot of DAX3](https://imgur.com/ARR2Boi.jpg)

#### Report 2:
#### Comparative Analysis and Distribution

![Screenshot of report2a](https://imgur.com/W2T0Ic9.jpg)
![Screenshot of report2b](https://imgur.com/CrhkEUJ.jpg)

- **`Pie Chart`**: Displays the distribution of Mental Disorder(s) % by Country.
- **`Line and Stacked Column Chart`**: Plots the prevalence of Mental Disorder(s) across GDP Per Capita, PPP.
- **`Box Plot Chart (Python)`**: Displays the distribution of Mental Disorder(s) Values (%) in box plot to visualize the spread, central tendency, and variability of the dataset. 

Observations:
- At **`Australia`** where Eating Disorder has highest prevalence, the **`Line and Stacked Column Chart`** indicates **`strong correlation`** between **`GDP Per Capita, PPP`** with **`Eating Disorder (%)`**.
- **`The Pie Chart`** shows that **`Depressive Disorder`** and **`Anxiety Disorder`** has highest overall prevalence globally.
- **`The Box Plot Chart`** shows that most of the mental disorders are either somewhat normally distributed or **`slightly positively skewed`**, except for **`Schizophrenia Disorder`**.

As I do not have ready Box Plot Chart in my Power BI, I had to create one using Python.

![Screenshot of python box plot](https://imgur.com/J78PSom.jpg)

#### Report 3:
#### Scaled Mental Disorders Trends

![Screenshot of report3](https://imgur.com/hRGNQkH.jpg)

- **`Line Chart A`**: Plots Yearly Scaled Mental Disorder Trend(s) to see correlation between selection.
- **`Line Chart B`**: Plots Suicide Rate by Income Level over Income Level Encoded to see if there is correlation.
- **`Line Chart C`**: Plots Scaled Mental Disorder Trend(s) over Income Level Encoded to see if there is correlation.- 

Observations:
- The **`Yearly Scaled Mental Disorder Trend(s) Chart`** presents the temporal trends of individual **'Mental Disorder(s)`**.
- **`Bipolar Disorder`** seems to have some correlation with the **`Income Level Encoded`** but it is only **`0.47`**.
- **`Suicide Rate`** has very mild correlation with the **`Income Level Encoded`** at only **`0.15`**.
- **`Eating Disorder`** and **`Schizophrenia Disorder`** have the most correlation with **`Income Level Encoded`**.
- **`Depressive Disorder`** seems to drop as **`Income Level`** increases. But the correlation is only at **`-0.33`**.
- There is a spike for **`Depressiive Disorder`** around year **`2008`** and the trend moves up for couple of years. This might have something to do with the Global Financial Crisis.


---

## Model Development and Performance Evaluation
Based on the correlation identified earlier and the trends evaluation, it might be useful to perform prediction upon the target feature **`Eating Disorder (%)`** based on **`Linear Regression model`**.

#### Build the following models:
- For **`Simple Linear Regression`**, I used **`GDP Per Capita, PPP`** column.
- For **`Multiple Linear Regression (Correlated Selection)`**, I used only those columns which correlation is more than 0.5 as shown above.
- Lastly, I used all columns of the dataframe for **`Multiple Linear Regression (All)`**.

#### Metrics used for Model Evaluation:
After the model is created, the following metrics are used to test the model's performance:
1. **`Mean Absolute Error (MAE)`**
    - Provides a straightforward average error.
2. **`Root Mean Squared Error (RMSE)`**
    - Emphasizes large error.
3. **`R-squared (R²)`**
    - Evaluates overall model performance and variance explained.

#### Simple Linear Regression
In Simple Linear Regression, I predicted a dependent variable **`Eating disorders (%)`** based on the values in an independent variable **`GDP Per Capita, PPP`**.
 
 Feature Selection:
- y = **target/output/dependent variable** which will be **`Eating disorders (%)`** which is to be predicted.<br>
- X = **predictor/input/independent variable** which will be **`GDP Per Capita, PPP`** which has the highest correlation with Eating disorders (%).
- c/b = Constant value or y-intercept
- m/w = slope or coefficient of X
- e = error

![Screenshot of simple linear regression chart](https://imgur.com/v77pdST.jpg)

Model Prediction
- Call the function to train the data and predict the the values
- Compare the predictions with actual output from testing data.

![Screenshot of simple linear regression predict](https://imgur.com/BLtfM2q.jpg)
![Screenshot of simple linear regression statistics](https://imgur.com/FodNbS7.jpg)

![Screenshot of simple linear regression metrics](https://imgur.com/ScTsmsU.jpg)

As the **`Accuracy is only around 50%`**, I felt that the prediction is not good enough. **`Eating Disorder (%)`** has high correlation with several other disorders as well. Taking that into consideration, I shall perform **`Multiple Linear Regression`** later.

#### Multiple Linear Regression (Correlated Selection):
In Multiple Linear Regression, I shall predict a dependent variable **`Eating Disorder (%)`** based on the values in all 5 highly correlated variables.
 Features Selection:
- Y = **target/output/dependent variable** which will be **`Eating Disorder (%)`** which is to be predicted.<br>
- Xs = **predictor/input/independent variables**. For the model building, I used 5 highly correlated variables:
    - **`GDP Per Capita, PPP`**
    - **`Income Level Encoded`**
    - **`Bipolar Disorder (%)`**
    - **`Anxiety Disorder (%)`**
    - **`Schizophrenia Disorder (%)`**

Model Prediction
- Call the function to train the data and predict the the values
- Compare the predictions with actual output from testing data.

![Screenshot of simple linear regression chart](https://imgur.com/PDGlLLy.jpg)
![Screenshot of simple linear regression predict](https://imgur.com/6NVqVKM.jpg)

![Screenshot of simple linear regression statistics](https://imgur.com/GnmjcNH.jpg)

Now the Accuracy is close to **`80%`**. It is a significant improvement from the Single Regression.

#### Multiple Linear Regression (All):

In Multiple Linear Regression, I shall predict a dependent variable **`Eating Disorder (%)`** based on all variables within the dataset.
 
 Features Selection:
- Y = **target/output/dependent variable** which will be **`Eating Disorder (%)`** which is to be predicted.<br>
- Xs = **predictor/input/independent variables**. For the model building, I shall take all variables of the dataframe.

To use all the values in numericals, I applied One-Hot Encoding to **`Country`** with get_dummies().

Model Prediction
- Call the function to train the data and predict the the values
- Compare the predictions with actual output from testing data.

![Screenshot of simple linear regression chart](https://imgur.com/vDGSIRa.jpg)
![Screenshot of simple linear regression predict](https://imgur.com/SPdj2nf.jpg)

![Screenshot of simple linear regression statistics](https://imgur.com/Fipy7NW.jpg)

Finally the Accuracy is close to **`100%`**!

---

## Tools and Resources
#### Tools:
- Python 3 (numpy, pandas, matplotlib, seaborn, scikit-learn)
- Jupyter Notebook
- Microsoft Power BI Desktop
- Microsoft Excel

#### Resources:
- [Kaggle Datasets](https://www.kaggle.com/datasets)
- [Github](https://github.com/)
- [Statistics Times](https://statisticstimes.com/)
- [World Bank Group](https://data.worldbank.org/)
- [World Health Organization (WHO) Data](https://data.who.int/countries)
- [ChatGPT](https://chatgpt.com/)
- Bishmer Sekaran, Senior Machine Learning Engineer at Xaltius, Trainer at NTUC

---

## Actionable Recommendations
Based on my findings and reflections, I recommend the following actionable plans for Neuro Compass Foundation:

#### 1. Support Enhanced Data Acquisition:
- Facilitate partnerships with organizations like WHO and national health bodies to acquire granular, high-quality datasets (segregated data by age, gender and region)
- Invest in datasets with richer demographic and socioeconomic details to deepen insights.
- Allocate resources for obtaining longitudinal data to uncover trends over larger temporal distribution.

#### 2. Targeted Awareness Campaigns:
- Focus on regions and populations where socioeconomic factors like income disparities correlate with mental health challenges, such as Eating Disorders.
- Raise awareness about the nuanced connections between Income Levels, Anxiety, Bipolar Disorder, and Suicide Rates.

#### 3. Research-Driven Advocacy:
- Utilize data insights to shape public health policies focusing on mental health education and early intervention in vulnerable socioeconomic groups.
- Promote programs targeting the interplay of Anxiety, Bipolar, and Eating Disorders in high-income countries.
- Advocate for suicide prevention programs tailored to high-risk groups based on demographic and regional analysis.

#### 4. Future Projects:
- Conduct studies focused on identifying subtle relationships between Income Levels and Suicide Rates using refined datasets.
- Encourage multidisciplinary research combining mental health, socioeconomic indicators, and cultural contexts.

---

## Retrospective: Buds, Roses and Thorns
#### 🌱 Buds (Opportunities for Growth)
- **`Enhanced Data Modeling`**:
    - I got comfortable with extracting data from various sources and remodel them into a single coherent dataset. This strengthens my ability to conceptualise and perform comparative data analysis.
- **`Advanced Visualizations`**:
    - Improved Power BI skills, especially in creating complex measures using DAX and integrating Python scripts, has broadened my visualization capabilities.
- **`Potential for Deeper Insights`**:
    - If better datasets were available, I could explore correlations more granularly (e.g., segregating by age group and gender) to refine insights, particularly on Suicide Rates and Mental Disorders.
- **`Technical Skills Advancement`**:
    - Gained significant understanding of Python and relevant libraries.
    - Improved knowledge of statistical concepts like standard deviation, box plots, and regression metrics.
    - Learned normalization techniques (scaled to 0 to 1) for comparative trend analysis.
    - Acquired Markdown and GitHub skills for collaborative reporting.
- **`Future Aspirations`**:
    - Explore SQL datasets in future projects for structured queries and integration.
    - Experiment with Python-based interactive charts to rival Power BI's interactivity.

#### 🌹 Roses (What Went Well)
- **`Insightful Findings`**:
    - Discovered that Eating Disorders have strong correlations with socioeconomic indicators such as GDP Per Capita and Income Level, suggesting it may be more prevalent in higher-income countries.
    - Identified a mild relationship between Suicide Rates and Income Levels, despite no significant correlation with mental disorders like Depression.
- **`Improved Tool Utilization`**:
    - Used Power BI effectively for interactive visualizations like bubble maps and slicers.
    - Leveraged Python scripts for additional data handling and visualizations.
- **`Holistic Application of Knowledge`**:
    - Applied various course topics, including data transformation, normalization and statistical analysis, to the project, ensuring a comprehensive approach to problem-solving.

#### 🌵 Thorns (Challenges and Limitations)
- **`Dataset Limitations`**:
    - The aggregated dataset lacked granularity (age and gender details), potentially masking correlations between Suicide Rates and Mental Disorders.
    - Limited access to detailed Suicide Rate data from WHO—possibly due to social restrictions or data availability policies.
- **`Missed Opportunities`**:
    - Could not incorporate SQL significantly due to the convenience of Python for .CSV files.
- **`Disappointment in Findings`**:
    - Surprised and disappointed by the lack of significant correlation between Suicide Rates and Depression, likely due to aggregation of data, which warrants deeper investigation.

---

## Conclusion
In conclusion, this analysis reveals important connections between mental health disorders and socioeconomic factors. These insights can help shape global policies, raise awareness, and better allocate resources where they’re needed most.

However, I am dissatisfied with the aggregated nature of the data, which likely led to inaccuracies, particularly in the correlation between Suicide Rates and mental disorders. The lack of detailed data, such as age and gender breakdowns, limited the depth of our analysis. There is also limited access to detailed suicide rate data online.

Despite the challenges, this project has laid the groundwork for deeper exploration. I recommend improving data acquisition, focusing awareness campaigns on vulnerable regions, and using these insights to influence public health policies.

This analysis is a call to action, guiding us toward more effective, targeted, and impactful mental health interventions worldwide.

---

[Link to your LinkedIn](https://www.linkedin.com/in/kuodo/)
