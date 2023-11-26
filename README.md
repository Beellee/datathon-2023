# Daily Sales Datathon

## Overview
This repository contains the code that my team and I created for the [Novartis 2023 Daily Sales Datathon](https://godatathon.com/challenge/). The challenge was to predict the daily sales patterns for different brands in various countries throughout 2022, using historical data from 2013 to 2021.

## Problem Description
Our main goal was to break down monthly sales into daily patterns, considering the unique sales behaviors in different countries and for different brands. The dataset provided includes daily-level details for Novartis brands, covering various features like identifiers, calendar-related information, business-related details, and target/auxiliary variables.

## Approach
### Seasonal AutoRegressive Integrated Moving Average (SARIMA) Model
The script for this model is in the Rmd file and involves the following steps:

1. **Loading Data:** Reading time series data from a Parquet file named "train_data.parquet."
2. **Data Preprocessing:** Converting date variables and exploring data using a correlation plot for selected variables.
3. **Data Splitting:** Dividing the dataset by country and selecting data for a specific country (e.g., "Zamunda").
4. **Data Cleaning:** Handling missing values and removing outliers using a function (`remove_outliers`).
5. **SARIMA Modeling:** Splitting the time series data into training and validation sets, fitting a SARIMA model using `auto.arima`, and evaluating the model's performance with forecasting and accuracy metrics.

### Decision Tree Model
**Decision Tree Model**
The script for this model is in the py file, and you can also access the Colab notebook [here](https://colab.research.google.com/drive/1FJ0Ni8w3DW7mBTM36N4Prh6SRA0ijhpz?usp=drive_link). The script involves the following steps:

1. **Imports:** Loading necessary libraries, mounting Google Drive, and reading the time series data from a Parquet file.
2. **Decision Tree Model:** Preparing data and implementing a Decision Tree Regressor to predict the 'phase' variable.
3. **Brand-based Model:** Creating and evaluating a Decision Tree model for a specific brand, showcasing the model's Mean Absolute Error (MAE).
4. **Month-based Model:** Similar to the brand-based model, training and evaluating the model for a specific month.
5. **Feature Importance:** Displaying the importance of each feature in the Decision Tree model.
6. **Submission Data & Template:** Reading submission data and template, encoding categorical variables, making predictions, and creating a submission file.
7. **Normalization of Predictions:** Ensuring predictions sum to one for each year-month-country-brand combination.

## Problems Encountered

**Model Understanding**
Understanding the data's complexity posed challenges in developing models that accurately captured daily sales patterns. Despite using advanced techniques like SARIMA and Decision Tree models, grasping the intricate patterns within the data was challenging.

**Feature Engineering**
Creating meaningful features to enhance model performance proved difficult. The variety of variables, including identifiers, calendar-related features, and business-related details, required innovative feature engineering. Unfortunately, despite our best efforts, we couldn't generate features that substantially improved predictive capabilities.

**Data Complexity**
The dataset's intricate structure across multiple countries, brands, and dates added complexity to our modeling efforts. Understanding unique sales patterns for each Country, Brand, and Month combination demanded a deep exploration, and achieving a comprehensive understanding remained challenging.

### Collaboration and Communication
Effective collaboration and communication within the team were crucial as we faced these challenges. Aligning diverse perspectives on model selection, feature engineering, and problem-solving required continuous dialogue and shared insights.

## Data Structure
- **Identifiers:**
  - Brand: Identifies the brand associated with the data.
  - Country: Represents the country associated with the brand.
  - Date: Specifies the date of the recorded data.

- **Calendar-Related Features:**
  - Day of the Week: Indicates the day of the week for a given date.
  - Working Date Number: Represents the number of the working date within the month.

- **Business-Related Features:**
  - Therapeutic Area: Provides information about the therapeutic area to which the country-brand belongs.
  - Distribution Channel: Specifies the main distribution channel for the country-brand.
  - Percentage of Sales to Hospitals: Represents the percentage of sales made to hospitals.

- **Target and Auxiliary Variables:**
  - Phasing (Target): The proportion of sales for a specific day relative to the total sales in the month. The sum of phases for the same month and country-brand combination should be equal to one.
  - Monthly Sales (Auxiliary): The sum of sales in a month for a particular country-brand, after being scaled non-linearly. This variable will be used as a weight when evaluating performance.

## Evaluation Metric
The evaluation metric employed in this datathon was the Weighted Root Mean Squared Error (WRMSE). This metric offers a thorough evaluation of model performance by considering the nuanced significance of various combinations involving Country, Brand, and Month. It adjusts to the challenge presented by the scarcity of recent data in later quarters, ensuring a more adaptive assessment of predictive accuracy over time.

### Instructions for Use
1. Clone this repository to your local machine.
2. Install the required dependencies.
3. Execute the provided scripts for predicting the daily phasing of sales for each brand in each country.
