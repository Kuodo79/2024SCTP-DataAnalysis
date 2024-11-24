![Neuro Compass Foundation Logo](https://imgur.com/Dgselim.png)
# Global Mental Health Insights
### A Data-Driven Analysis by Neuro Compass Foundation

---

##### Date: 11 Nov 2024
##### Prepared by: Kuodo Cheok, Data Analyst
---
![Screenshot of dashboard](https://imgur.com/eaa3XuB.jpg)

---

## Project Overview

As a data analyst with the research team at Neuro Compass Foundation, my objective is to conduct an in-depth analysis of five key mental health disorders: Anxiety, Bipolar Disorder, Depression, Eating Disorder, and Schizophrenia. This analysis aims to provide data-driven insights into the global distribution, prevalence, and trends of these disorders. It also examines correlations between mental health metrics, socioeconomic factors such as GDP per capita, and suicide rates, highlighting significant regional disparities.

The findings will support the foundation’s mission by informing advocacy efforts, guiding resource allocation, shaping policymaking, and enabling targeted mental health interventions globally.

---

## Table of Contents

- [Description of Datasets](#description-of-datasets)
- [Data Understanding and Preparation](#data-understanding-and-preparation)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

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
#### Dataset 1:
- **`Code`** contains null. The reason behind that is that the Entity covers several countries and can't be represented with a single code. As there are valuable data within these countries, I have decided to remove the **`Code`** column entire instead of removing records with null **`Code`**.
- **`Entity`** shall be changed to **`Country`** instead for better clarity and to prepare for data join.
- All the disorders column titles are too long. I shall use shorter name.
- This dataset is clean otherwise and requires no further transformation.

Dataset 1 after cleaning:
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

Dataset 2 after initial cleaning:
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

#### Merge Datasets into a Complete Dataset
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
- There is also a **`World`** data under **`Country`** which I wish to save into a separate .CSV.
- I need to perform Comparative Trend Analysis on the key disorders. Therefore, I need the metrics to be **`Scaled`** and saved as a separate.CSV.

#### Merged Dataset
![Screenshot of dataset](https://imgur.com/1OExWI6.jpg)

#### Scaled Merged Dataset
![Screenshot of dataset](https://imgur.com/udQBQ3G.jpg)

---
Examples of potential clients could include:
A healthcare provider seeking to improve patient outcomes
A retail company aiming to optimize inventory
A financial institution working to enhance fraud detection
Or any other problem in any other field you prefer



Project Objective:

Your task is to develop a data analysis pipeline that adds value to the client’s operations. This involves creating an end-to-end solution, from data preparation to visualization, to effectively address the client’s challenges. 




---

#### Exploratory Data Analysis (EDA)
Have you articulated the size and shape of the dataset?
Have you assessed data quality, including null values or missing data?
Have you documented the data types of all features?
Have you selected a target column for analysis?
Have you provided descriptive statistics for the dataset?
Have you identified and commented on outliers within the dataset?
Have you created plots for each categorical column to show feature distributions?
Have you generated appropriate charts for numerical features, both individually and in relation to the target column?
Have you calculated and displayed correlations between numerical features and the target column?
Have you summarized key insights and implications from the EDA process?

--- 
#### Data Visualization
Have you created at least five visualizations relevant to the project objectives?
Have you used Python libraries (e.g., matplotlib, seaborn, plotly) or Power BI to develop visualizations?
Have you explained the choice of visualization type and tool for each?

---

#### Analytical Pipeline Development
Have you designed and implemented an analytical or BI pipeline to address the client’s challenges using cleaned and processed data?

---
#### Model Development and Performance Evaluation
Have you built a model suited to the project’s needs (e.g., regression, classification)?
Have you employed at least 3 metrics appropriate to either a classification or a regression task (as appropriate to your situation)?
Have you mentioned if certain metrics are sub-optimal but required?
Have you explained why the chosen metric(s) are ideal for the project and drawn distinctions if applicable?

---

Documentation and Recommendations
Have you summarized findings from the analysis and EDA process?
Have you provided clear, actionable recommendations tailored to the client’s needs?

---
Material Preparation
Have you prepared your project materials in one of the following formats:
Power BI: At least three pages, including a summary dashboard.
Jupyter Notebook: At least five graphics and 300 words of markdown text.
Have you presented the data insights in a storytelling format tailored to the target audience?
Have you optionally used presentation or slide-sharing software if preferred?

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
