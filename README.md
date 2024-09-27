## DATA ANALYSIS PROJECT
# MIGRATION PATTERNS BETWEEN ARGENTINA AND EUROPE

# 1. Introduction
## 1.1. Project background
Migration has been a defining element in shaping societies globally, with historical movements significantly influencing contemporary patterns. Argentina, in particular, experienced a profound wave of European immigration during the 19th and early 20th centuries. This period, often referred to as the Great Immigration, saw millions of Europeans—primarily from Italy, Spain, and other European nations—migrate to Argentina. This influx was driven by factors such as economic hardship, political instability, and the promise of new opportunities in the Americas. The immigrants contributed substantially to Argentina’s cultural, social, and economic landscape, leaving a lasting legacy in the country's demographic composition and national identity.

In recent decades, a reverse migration trend has emerged, with increased flows of Argentinians moving to Europe, particularly Spain and Italy. This shift reflects a complex interplay of factors including economic challenges, political developments, and the evolving global context. As Argentina navigates economic difficulties and high poverty rates, the historical connection with European countries, once destinations for Argentine immigrants, now becomes a poignant aspect of contemporary migration dynamics. Understanding this reversal not only sheds light on current migration trends but also highlights the enduring links between Argentina and Europe, shaped by a shared historical narrative of migration.

In the current global context, understanding migration patterns is crucial for policymakers, researchers, and institutions. This project focuses on analyzing migration flows from Argentina to Europe, particularly to Spain and Italy, over the past 30 years. This period is selected to observe recent trends and compare them with historical migrations, reflecting on the historical and cultural connections between these countries.

## 1.2. General objectives

To explore migration trends between Latin America and Europe over the past 30 years, with a specific focus on how migration stock data reflects cultural and historical ties, particularly between South America (Argentina) and Europe (Spain and Italy). Additionally, to analyze the correlations between key economic indicators such as poverty rates, GDP per capita, unemployment, and net migration.

## 1.3. Research and analysis questions

- Where do Latin America and Europe stand in terms of permanent migration flows?
- What is the impact of historical and cultural connections on migration between these regions?
- Are there significant correlations between economic indicators (poverty, GDP per capita, unemployment) and migration patterns?

# 2. Methodologycal process

## 2.1. Data sources and information

The sources listed below were selected for the analysis and were included and imported into the initial database: [dap1.2.sql](data/processed/dap1.2.sql).

### United Nations: Population Division

**International Migrant Stock**

Source: [International Migrant Stock](https://www.un.org/development/desa/pd/content/international-migrant-stock)

The International Migrant Stock dataset provides detailed estimates of the number of international migrants residing in various countries, disaggregated by age, sex, and country of origin. These estimates are based on national statistics, primarily derived from population censuses, population registers, and representative surveys. The dataset includes information for the years 1990, 1995, 2000, 2005, 2010, 2015, and 2020, covering a total of 232 countries and areas worldwide.

_____

**Key points for data interpretation:**

**Data units:** The figures represent the total number of international migrants living in a given country who were born in another country. These numbers reflect the migrant stock (total count of migrants) rather than migration flows (annual movements). The data provides a snapshot of the migrant population at specific points in time.

**Origin and destination:** The dataset is organized by both the country of origin (where the migrants were born) and the country of destination (where the migrants currently reside). This means the data shows how many people born in a specific country are living in another country at a given time.

**Annual columns:** The dataset includes columns for specific years (e.g., 1990, 2000). These columns represent the total number of international migrants in those years, not cumulative flows over previous years. For example, if the dataset shows 50,000 migrants from Country B (origin) residing in Country A (destination) in 1990, it reflects the number present in that year, not how many arrived or left over a period.

**Positive values:** The values are always positive, representing the count of people residing in a different country from their country of birth. The data does not separate entries and exits but provides a total count of migrants in each year.

_____

**Migration stock vs. migration flow:**

**Migration stock:** represents the total number of immigrants residing in a country at a specific point in time. It is a static snapshot of the migrant population for the years provided.

**Migration Flows:** refers to the number of people moving into or out of a country over a specific period (typically annually), showing dynamic movement rather than a snapshot.

_____

### World Bank Group: indicators

- **GDP per capita (current US$)**

    Indicator ID: NY.GDP.PCAP.CD

    Source: [World Bank | GDP per Capita](https://data.worldbank.org/indicator/NY.GDP.PCAP.CD)

    This indicator measures the total value of goods and services produced in a country divided by its population, expressed in current US dollars. It is commonly used to assess the standard of living and economic performance of a country. Comparing GDP per capita between Argentina, Italy, and Spain helps contextualize Argentina's economic standing relative to these European countries, offering insights into why migration trends might occur.

- **Net migration**

    Indicator ID: SM.POP.NETM

    Source: [World Bank | Net Migration](https://data.worldbank.org/indicator/SM.POP.NETM)

    This indicator measures the net number of migrants (immigrants minus emigrants) in a country. It provides a direct view of migration trends and patterns.

- **Poverty headcount ratio at national poverty lines (% of population)**

    Indicator ID: SI.POV.NAHC

    Source: [World Bank | Poverty Headcount Ratio](https://data.worldbank.org/indicator/SI.POV.NAHC)

    This indicator measures the percentage of the population living below the national poverty line. It is a key measure for understanding local poverty conditions and is crucial for correlating poverty with migration trends. It provides a precise view of how many people are living under conditions deemed inadequate by national standards.

- **Total unemployment (% of total labor force) (modeled ILO estimate)**

    Indicator ID: SL.UEM.TOTL.ZS

    Source: [World Bank | Unemployment Rate](https://data.worldbank.org/indicator/SL.UEM.TOTL.ZS?end=2023&start=1991&view=chart)

    This indicator represents the share of the labor force that is unemployed but actively seeking employment. It is used as an alternative measure in the absence of sufficient data for the poverty headcount ratio. Understanding unemployment rates helps provide additional context to migration trends and economic conditions.

## 2.2. Data processing

### 2.2.1. Data research, collection and initial data exploration

In this phase, data was collected from various sources, including the World Bank and the United Nations. The datasets were initially downloaded in multiple formats, such as **.csv** and **.xlsx**, and were processed using **Navicat**, a database management software. This step involved examining the data structure and content, especially focusing on the data contained in Excel files. Data was edited directly in Excel to ensure proper formatting and structure before importing it into the database.

Raw data: [raw data files]([data/raw](https://github.com/jsruano/migration_analysis/tree/865d412dbe98d2bba75209ec1e8e0e07aaa08e70/data/raw))

### 2.2.2. Database design

In this phase, the database structure was designed to ensure consistency and scalability of the data. Additionally, normalization techniques were applied to reduce data redundancy and enhance data integrity.

An Entity-Relationship (ER) diagram was created to model how data elements relate to each other. This involved defining tables, fields, and data types, establishing primary and foreign keys for relational integrity, and applying normalization, ensuring scalability and data consistency.

This involved defining the schema, an **entity-relationship diagram** for the databases, including the creation of tables, relationships, and keys, in order to facilitate a scalable and consistent data models, maintaining data integrity.
_____

**World Bank Indicators**

- **Handling countries, areas and regions:** the raw data from the World Bank included regional and aggregated data that was not relevant for this analysis. We filtered out these regions and kept only the country-level data. This was necessary as the regional data was often ambiguous and not suitable for detailed country-specific analysis.

- **Database Schema Design**: The transformed data was imported into a relational database with a schema designed to follow normalization principles. The schema includes a primary table, **wb_indicators**, which stores all indicators by country. Additionally, four secondary tables were created: **wb_countries**, **wb_regions**, **wb_income_groups**, and **wb_indicators**. Each country, region, income group, and indicator is assigned a unique ID, ensuring proper data organization and integrity.

Raw data: [wb_indicators files]([data/raw/wb_indicators](https://github.com/jsruano/migration_analysis/tree/865d412dbe98d2bba75209ec1e8e0e07aaa08e70/data/raw/wb_indicators))  
Database schema: [wb_database_schema](https://github.com/jsruano/migration_analysis/blob/865d412dbe98d2bba75209ec1e8e0e07aaa08e70/data/processed/wb_database_schema.jpg)

_____

**United Nations | Population Division**

- **Handling countries, areas and regions:** as well as the World Bank data, the UN Population Division data included regions and areas, which were retained for this analysis. Each location, whether a country, region or area, was assigned a unique **id** to ensure data consistency.

- **Data processing:** the data was extracted from the original Excel file, containing migration stocks with detailed origin and destination information. We cleaned the data by removing elements that could hinder proper importation into the database while retaining **id**s for locations and migration records. Each record in the parent table (**un_migration_stock**) includes both the origin and destination locations.

 - **Schema design:** a logical and physical schema was designed organizing data in the database, including a parent table (**un_migration_stock**) and three secondary tables (**un_countries**, **un_subregion** and **un_region**).

Raw data:   
[undesa_pd_2020_ims_stock_by_sex_destination_and_origin_modif](https://github.com/jsruano/migration_analysis/blob/865d412dbe98d2bba75209ec1e8e0e07aaa08e70/data/raw/un_international_migration_stock/undesa_pd_2020_ims_stock_by_sex_destination_and_origin_modif.xlsx)  
[aggregates_correspondence_table_2020_1_modif](https://github.com/jsruano/migration_analysis/blob/865d412dbe98d2bba75209ec1e8e0e07aaa08e70/data/raw/un_international_migration_stock/aggregates_correspondence_table_2020_1_modif.xlsx)

Database schema: [un_database_schema](https://github.com/jsruano/migration_analysis/blob/865d412dbe98d2bba75209ec1e8e0e07aaa08e70/data/processed/un_database_schema.jpg)
  
_____

### 2.2.3. Data preparation, configuration and data import

The database environment was set up using **MySQL** in **Navicat**. The table structures defined during the data modeling phase were implemented, and the data was validated to ensure consistency with the original sources.

During this phase, I utilized SQL queries to validate the accuracy of the imported data by cross-referencing the tables with the original datasets. I performed basic exploratory queries to check relationships between tables and fields.

➡️ Jupyter notebook: [2.2.3. Data preparation, configuration and data import](https://github.com/jsruano/migration_analysis/blob/main/notebooks/2.2.3.%20Data%20preparation,%20configuration%20and%20data%20import.ipynb)

_____

## 2.3. Initial data cleaning

In the data cleaning phase, both the United Nations and World Bank tables underwent basic transformations. Blank spaces were removed, and certain expressions were modified in the **wb_countries** and **un_locations**.

➡️ Jupyter notebook: [2.3. Initial data cleaning](https://github.com/jsruano/migration_analysis/blob/0de88f5b2f4375efaf9da9e522daab54c3094006/notebooks/2.3.%20Initial%20data%20cleaning.ipynb)

## 2.4. Exploratory analysis

### 2.4.1. United Nations | Population Division

The initial phase of the analysis involved exploring the United Nations databases using MySQL queries via Navicat. This exploration aimed to understand the structure and nature of the data within the tables. Given the objective was not only to produce descriptive statistics but also to utilize the data in visualization software, specifically Power BI, it was crucial to ensure the tables were in a compatible format for import.

The first step focused on a global exploratory analysis of migration stock data across various years, examining migration trends at a global and interregional (intercontinental) level. This broader contextual analysis was essential for understanding worldwide migration patterns before narrowing the scope to specific regions. Subsequently, the focus shifted to regional dynamics, particularly the migration flows between Latin America and Europe, providing a more detailed and localized insight into the migration context.

➡️ Jupyter notebook: [2.4.1. UN data exploratory analysis](https://github.com/jsruano/migration_analysis/blob/057e2d221eea4e00fd052dd2ee49d8bb1cf58595/notebooks/2.4.1.%20UN%20data%20exploratory%20analysis.ipynb)

______

### 2.4.2. World Bank Indicators

After unpivoting the data for easier manipulation in Power BI, visualizations revealed inconsistencies, leading to the exclusion of the poverty headcount ratio indicator. Correlations between indicators were generally weak, suggesting a multifactorial nature not fully captured by the chosen data. A deeper study would require broader data and sources for more precise insights.

➡️ Jupyter notebook: [2.4.2. WB data exploratory analysis](https://github.com/jsruano/migration_analysis/blob/31f9995232956c3947698941dedb2e23de0773c7/notebooks/2.4.2.%20WB%20data%20exploratory%20analysis.ipynb)

## 2.5. Data visualization

The PDF version of this report provides a static representation of the visualizations and does not capture the full interactive capabilities offered by the various graphs.

To experience the complete functionality and interact with the data, the .pbix file must be downloaded and explored in Power BI Desktop.

➡️ Visualization report (Microsoft Power BI): [dap1.pbix](https://github.com/jsruano/migration_analysis/blob/5feab804ff185e75f92ae31656c13a55e97ed2e7/visualizations/dap1.pbix)  
➡️ Visualization report (.pdf):[dap1.pdf](https://github.com/jsruano/migration_analysis/blob/d3e6eacaef7f393e2cc8096755808b2c9167f84d/visualizations/dap1.pdf)  
➡️ Data files: [visualizations data files](https://github.com/jsruano/migration_analysis/tree/d3e6eacaef7f393e2cc8096755808b2c9167f84d/data/processed/visualizations)