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

As a data analyst with the research team at Neuro Compass Foundation, my objective is to conduct an in-depth analysis of five key mental health disorders: Anxiety, Bipolar Disorder, Depression, Eating Disorder, and Schizophrenia. This analysis aims to provide data-driven insights into the global distribution, prevalence, and trends of these disorders. It also examines correlations between mental health metrics, socioeconomic factors such as GDP per capita, and suicide rates, highlighting significant regional disparities.

The findings will support the foundation’s mission by informing advocacy efforts, guiding resource allocation, shaping policymaking, and enabling targeted mental health interventions globally.

---

## Table of Contents

- [Description of Datasets](#description-of-datasets)
- [Data Understanding and Preparation](#data-understanding-and-preparation)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Data Visualization in MS Power BI](#data-visualization-in-ms-power-bi)
- [Contributing](#contributing)
- [License](#license)

---

Project Objective:

Your task is to develop a data analysis pipeline that adds value to the client’s operations. This involves creating an end-to-end solution, from data preparation to visualization, to effectively address the client’s challenges. 

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
- **`incomeLevel`** needs to be encoded to **`Income Level Encoded`**.
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
- I need to perform Comparative Trend Analysis on the key disorders. Therefore, I need the metrics to be **`Scaled`** (0 to 1) and saved as **``Scaled Mental Disorder Suicides and GDP.csv`**.

#### Merged Dataset:
#### Mental Disorder Suicides and GDP.csv

![Screenshot of dataset](https://imgur.com/1OExWI6.jpg)

#### Scaled Merged Dataset:
#### Scaled Mental Disorder Suicides and GDP.csv
![Screenshot of dataset](https://imgur.com/udQBQ3G.jpg)

---

## Exploratory Data Analysis (EDA)
- There are a total of **`3149 records`** across **`12 columns`**.
- All data types are in order and there are **`no nulls`**.

#### Statistical Description:
![Screenshot of description](https://imgur.com/UetZwqC.jpg)

- Schizophrenia Disorder (%):
    - Mean: 0.26%, with a narrow range (0.19% to 0.46%).
    - Relatively low prevalence with little variation across countries.
- Depressive Disorder (%):
    - Mean: 3.76%, with a range from 1.94% to 7.65%.
    - More common than schizophrenia, with moderate variability.
- Anxiety Disorder (%):
    - Mean: 4.12%, range from 1.88% to 8.62%.
    - Similar to depression, indicating widespread prevalence and considerable variation.
- Bipolar Disorder (%):
    - Mean: 0.66%, with a narrower range (0.18% to 1.51%).
    - Less prevalent, with low variation.
- Eating Disorder (%):
    - Mean: 0.66%, range from 0.18% to 1.51%.
    - Similar to bipolar, less prevalent with low variation.
- Suicide Rate Per 100k:
    - Mean: 10.69, with a wide range from 0 to 92.6.
    - High variability, with a few countries having extremely high suicide rates.
- GDP Per Capita, PPP:
    - Mean: $16,711, range from $478 to $141,635.
    - Shows significant inequality in economic well-being globally.

Skewness Indication:
Many of the variables, such as GDP per capita, suicide rate, and disorder prevalence, show signs of positive skew (right-skewed), where a few outliers (extreme values) are pulling the mean higher than the median.


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
- Both **`Merged`** and **`Scaled`** datasets are sorted by **`Country`** and **`Year`**, and there are many parameters to choose from. I have chosen Power BI for its dynamic chart functions. 
- Both datasets are transformed by unpivoting the various disorders columns into **`Disorders`** and **`Percentage`**
- **`Year`** is being converted to actual Year-date using **`Year Date = YEAR(DATE([Year],1,1))`**
- The charts that will be filtered by slicers **`Mental Disorders`**, **`Country`**, and **`Year Date`**.

#### Report 1:
![Screenshot of report1](https://imgur.com/r19cMRt.jpg)

- **`Bubble Map`**: Displays the prevalence of Mental Disorder(s) in the world map.
- **`Line and Clustered Column Chart`**: Ranks the countries based on highest prevalence of selected Mental Disorder(s).
- **`Cards`**: Indicates countries with **`Highest Median %`** and **`Lowest Median %`** of Mental Disorder(s) based on the following measures (DAX).

![Screenshot of DAX1](https://imgur.com/oqLO86E.jpg)
![Screenshot of DAX2](https://imgur.com/EVc3ZyR.jpg)
![Screenshot of DAX3](https://imgur.com/ARR2Boi.jpg)

#### Report 2:
![Screenshot of report2a](https://imgur.com/W2T0Ic9.jpg)
![Screenshot of report2b](https://imgur.com/CrhkEUJ.jpg)
- **`Pie Chart`**: Displays the distribution of Mental Disorder(s) % by Country.
- **`Line and Stacked Column Chart`**: Plots the prevalence of Mental Disorder(s) across GDP Per Capita, PPP.
- **`Boxplot Chart (Python)`**: Displays the distribution of Mental Disorder(s) Values (%) in boxplot to visualize the spread, central tendency, and variability of the dataset. 

As I do not have ready Boxplot chart in my Power BI, I had to create one using Python.

![Screenshot of python boxplot](https://imgur.com/J78PSom.jpg)

#### Report 3:
![Screenshot of report3](https://imgur.com/hRGNQkH.jpg)
- **`Line Chart A`**: Plots Yearly Scaled Mental Disorder Trend(s) to see correlation between selection.
- **`Line Chart B`**: Plots Suicide Rate by Income Level over Income Level Encoded to see if there is correlation.
- **`Line Chart C`**: Plots Scaled Mental Disorder Trend(s) over Income Level Encoded to see if there is correlation.

---

## Model Development and Performance Evaluation
#### Use observation to build the following models:
- For **`Simple Linear Regression`**, I shall use **`GDP Per Capita, PPP`** column.
- For **`Multiple Linear Regression (Correlated Selection)`**, I shall use only those columns which correlation is more than 0.5 as shown above.
- Lastly, I shall use all columns of the dataframe for **`Multiple Linear Regression (All)`**.


Have you built a model suited to the project’s needs (e.g., regression, classification)?
Have you employed at least 3 metrics appropriate to either a classification or a regression task (as appropriate to your situation)?
Have you mentioned if certain metrics are sub-optimal but required?
Have you explained why the chosen metric(s) are ideal for the project and drawn distinctions if applicable?

---

Documentation and Recommendations
Have you provided clear, actionable recommendations tailored to the client’s needs?

---
Have you presented the data insights in a storytelling format tailored to the target audience?

---

Submission Guidelines
Have you ensured all minimum criteria are met to avoid an incomplete assessment?
Have you double-checked that:
Dataset(s) meet the size and quality requirements.
All EDA, visualizations, and models are documented clearly.
The report aligns with storytelling and client-focused objectives?

--- 
Report Preparation
Have you drafted and scripted a 10-12 minute report on your findings?
Have you rehearsed and timed it?
And re-rehearsed it?
Are you prepared to receive questions about the report?
Did you include a significant section regarding challenges you encountered and new material you learned or discovered?
Have you mentioned what you would do with additional time or resources?
Do you have your project repo up on Github with a full README.md including screenshots and writeup and did you link from Github to your LinkedIn in the README.md?

[Link to your LinkedIn](https://www.linkedin.com/in/kuodo/)
