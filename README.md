## DATA ANALYSIS PROJECT
# MIGRATION PATTERNS BETWEEN ARGENTINA AND EUROPE

# 1. Introduction
## 1.1. Project background
Migration has been a defining element in shaping societies globally, with historical movements significantly influencing contemporary patterns. Argentina, in particular, experienced a profound wave of European immigration during the 19th and early 20th centuries. This period, often referred to as the Great Immigration, saw millions of Europeans—primarily from Italy, Spain, and other European nations—migrate to Argentina. This influx was driven by factors such as economic hardship, political instability, and the promise of new opportunities in the Americas. The immigrants contributed substantially to Argentina’s cultural, social, and economic landscape, leaving a lasting legacy in the country's demographic composition and national identity.

In recent decades, a reverse migration trend has emerged, with increased flows of Argentinians moving to Europe, particularly Spain and Italy. This shift reflects a complex interplay of factors including economic challenges, political developments, and the evolving global context. As Argentina navigates economic difficulties and high poverty rates, the historical connection with European countries, once destinations for Argentine immigrants, now becomes a poignant aspect of contemporary migration dynamics. Understanding this reversal not only sheds light on current migration trends but also highlights the enduring links between Argentina and Europe, shaped by a shared historical narrative of migration.

In the current global context, understanding migration patterns is crucial for policymakers, researchers, and institutions. This project focuses on analyzing migration flows from Argentina to Europe, particularly to Spain and Italy, over the past 30 years. This period is selected to observe recent trends and compare them with historical migrations, reflecting on the historical and cultural connections between these countries.

## 1.2. Objectives

### General objectives

To analyze the relationship between poverty levels, employment, and other relevant indicators that may trigger migration from Argentina to Europe over the past 30 years, with a focus on Spain and Italy. These countries are chosen due to their historical, cultural, and ancestral connections with Argentina, stemming from significant European immigration in the 19th and 20th centuries.

### Specific objectives

- To evaluate how variations in GDP per capita among Argentina, Italy, and Spain influence migration patterns.
- To investigate the correlation between poverty rates in Argentina and migration trends towards Europe.
- To compare economic conditions in Argentina with those in Italy and Spain, focusing on key indicators such as GDP per capita and poverty levels.
- To assess migration exchanges between Argentina and Europe based on existing data.
- To analyze the demographic composition of migrants, including age, education level, and professional background, and how these factors impact migration decisions.

## 1.3. Research questions

- **How has the poverty rate in Argentina changed over the past 30 years, and how has this impacted migration flows to Italy and Spain?**

    Hypothesis: Increased poverty rates in Argentina are positively correlated with higher migration rates to Italy and Spain.

- **What differences exist in GDP per capita among Argentina, Italy, and Spain, and how do these differences relate to migration decisions?**

    **Hypothesis:** Lower GDP per capita in Argentina relative to Italy and Spain is associated with higher migration rates, as individuals seek better economic opportunities in countries with higher GDP per capita.

- **Is there a significant correlation between poverty in Argentina and migration to Europe?**

    **Hypothesis:** There is a significant correlation between higher poverty levels in Argentina and increased migration to Europe, with more severe poverty leading to higher migration rates.

- **What other economic factors (such as income inequality) might be influencing migration patterns?**

    **Hypothesis:** Besides poverty, high levels of income inequality in Argentina may also contribute to increased migration, as individuals from lower-income brackets seek more equitable opportunities in Europe.

- **What are the demographic characteristics of migrants from Argentina to Europe, and how do these characteristics influence migration trends?**

    **Hypothesis:** The demographic profile of migrants (including age, education, and occupation) affects migration trends, with younger, more educated individuals being more likely to migrate to Europe for better job prospects.

# 2. Methodology

## 2.1. Data sources and information

The sources listed below were selected for the analysis and were included and imported into the initial database: [dap1.0.sql](data/processed/dap1.0.sql).

### United Nations: Population Division

**International Migrant Stock**

Source: [International Migrant Stock](https://www.un.org/development/desa/pd/content/international-migrant-stock)

Description: This dataset includes processed graphs and original databases detailing immigration and emigration statistics for various countries. The dataset presents estimates of international migrants disaggregated by age, sex, and country of origin. These estimates are based on national statistics, primarily obtained from population censuses, population registers, and representative surveys. Data are available for the years 1990, 1995, 2000, 2005, 2010, 2015, and 2020, covering 232 countries and areas worldwide.

### World Bank Group: indicators

- **GDP per Capita (current US$)**

    Indicator ID: NY.GDP.PCAP.CD

    Source: [World Bank | GDP per Capita](https://data.worldbank.org/indicator/NY.GDP.PCAP.CD)

    This indicator measures the total value of goods and services produced in a country divided by its population, expressed in current US dollars. It is commonly used to assess the standard of living and economic performance of a country. Comparing GDP per capita between Argentina, Italy, and Spain helps contextualize Argentina's economic standing relative to these European countries, offering insights into why migration trends might occur.

- **Net Migration**

    Indicator ID: SM.POP.NETM

    Source: [World Bank | Net Migration](https://data.worldbank.org/indicator/SM.POP.NETM)

    This indicator measures the net number of migrants (immigrants minus emigrants) in a country. It provides a direct view of migration trends and patterns.

- **Poverty Headcount Ratio at National Poverty Lines (% of Population)**

    Indicator ID: SI.POV.NAHC

    Source: [World Bank | Poverty Headcount Ratio](https://data.worldbank.org/indicator/SI.POV.NAHC)

    This indicator measures the percentage of the population living below the national poverty line. It is a key measure for understanding local poverty conditions and is crucial for correlating poverty with migration trends. It provides a precise view of how many people are living under conditions deemed inadequate by national standards.

- **Unemployment, Total (% of Total Labor Force) (modeled ILO estimate)**

    Indicator ID: SL.UEM.TOTL.ZS

    Source: [World Bank | Unemployment Rate](https://data.worldbank.org/indicator/SL.UEM.TOTL.ZS?end=2023&start=1991&view=chart)

    This indicator represents the share of the labor force that is unemployed but actively seeking employment. It is used as an alternative measure in the absence of sufficient data for the poverty headcount ratio. Understanding unemployment rates helps provide additional context to migration trends and economic conditions.

## 2.2. Data processing

### 2.2.1. Data research, collection and initial data exploration

In this phase, data was collected from various sources, including the World Bank and the United Nations. The datasets were initially downloaded in multiple formats, such as **.csv** and **.xlsx**, and were processed using **Navicat**, a database management software. This step involved examining the data structure and content, especially focusing on the data contained in Excel files. Data was edited directly in Excel to ensure proper formatting and structure before importing it into the database.

Raw data: [data/raw](data/raw)

### 2.2.2. Database design

In this phase, the database structure was designed to ensure consistency and scalability of the data. Additionally, normalization techniques were applied to reduce data redundancy and enhance data integrity.

An Entity-Relationship (ER) diagram was created to model how data elements relate to each other. This involved defining tables, fields, and data types, establishing primary and foreign keys for relational integrity, and applying normalization, ensuring scalability and data consistency.

This involved defining the schema, an **entity-relationship diagram** for the databases, including the creation of tables, relationships, and keys, in order to facilitate a scalable and consistent data models, maintaining data integrity.
_____
**World Bank Indicators**

- **Handling countries, areas and regions:** the raw data from the World Bank included regional and aggregated data that was not relevant for this analysis. We filtered out these regions and kept only the country-level data. This was necessary as the regional data was often ambiguous and not suitable for detailed country-specific analysis.

- **Database schema design:** the transformed data was imported into a relational database with a schema that includes a parent table (**wb_indicators**) which holds all indicators by country. Two secondary tables were created: one for countries (**wb_countries**) and another for indicators (**wb_indicators**). Each country and indicator is assigned a unique **id**.

Raw data: [data/raw/wb_indicators](data/raw/wb_indicators)  
Database schema: [wb_indicators_schema](data/processed/[wb_indicators_schema.jpg)

_____
**United Nations Population Division**

- **Handling countries, areas and regions:** as well as the World Bank data, the UN Population Division data included regions and areas, which were retained for this analysis. Each location, whether a country, region or area, was assigned a unique **id** to ensure data consistency.

- **Data processing:** the data was extracted from the original Excel file, containing migration stocks with detailed origin and destination information. We cleaned the data by removing elements that could hinder proper importation into the database while retaining **id**s for locations and migration records. Each record in the parent table (**un_migration_stock**) includes both the origin and destination locations.

 - **Schema design:** a logical and physical schema was designed organizing data in the database, including a parent table (**un_migration_stock**) and one secondary table (**un_locations**). The **un_locations** holds information related to each location: 

Raw data:   
[undesa_pd_2020_ims_stock_by_sex_destination_and_origin_modif](data/raw/un_international_migration_stock/undesa_pd_2020_ims_stock_by_sex_destination_and_origin_modif.xlsx)  
[aggregates_correspondence_table_2020_1_modif](data/raw/un_international_migration_stock/aggregates_correspondence_table_2020_1_modif.xlsx)

Database schema: [un_migration_schema](data/processed/un_migration_schema.jpg)
  
_____

### 2.2.3. Data preparation, configuration and data import

The database environment was set up using **MySQL** in **Navicat**. The table structures defined during the data modeling phase were implemented, and the data was validated to ensure consistency with the original sources.

During this phase, I utilized SQL queries to validate the accuracy of the imported data by cross-referencing the tables with the original datasets. I performed basic exploratory queries to check relationships between tables and fields.

➡️ Jupyter notebook: [2.2.3. Data preparation, configuration and data import](https://github.com/jsruano/migration_analysis/blob/main/notebooks/2.2.3.%20Data%20preparation,%20configuration%20and%20data%20import.ipynb)

_____
### 2.2.4. Initial data cleaning

In the data cleaning phase, both the United Nations and World Bank tables underwent basic transformations. Blank spaces were removed, and certain expressions were modified in the **wb_countries** and **un_locations**.

➡️ Jupyter notebook: [2.2.4. Initial data cleaning](https://github.com/jsruano/migration_analysis/blob/51caebd4ad22ffc99726e6c31c046143b6cd600b/notebooks/2.2.4.%20Initial%20data%20cleaning.ipynb)

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

## 2.3. Analytical Techniques
Description of statistical and analytical techniques used (correlation, mean comparison, etc.).

# 3. Data Analysis

## 3.1. GDP per Capita Analysis
Comparison between Argentina, Italy, and Spain.
Impact of GDP per capita on migration patterns.

## 3.2. Poverty Rate Analysis
Trends in poverty rates in Argentina.
Correlation between poverty rates and migration to Europe.

## 3.3. Comparison of Economic Conditions
Comparison of key indicators (GDP per capita, poverty, income inequality) between Argentina, Italy, and Spain.

## 3.4. Evaluation of Migration Flows
Analysis of migration flows between Argentina and Europe.
Identification of trends and patterns.

4. Results
4.1. Summary of Findings
Key discoveries from the analysis.
4.2. Interpretation of Results
Explanation of how results address the research questions.
4.3. Implications for Migration
Discussion on the implications of findings for understanding migration patterns.

5. Conclusions and Recommendations
5.1. Conclusions
Summary of key conclusions based on data analysis.
5.2. Recommendations
Suggestions for migration policies and future research.

6. Appendices
6.1. Additional Data
Tables and charts supporting the analysis.
6.2. Technical Documentation
Details on data processing and analytical techniques used.

7. References
7.1. Sources Consulted
Citations of datasets, articles, and other resources used in the report.