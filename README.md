## Cryptocurrency Market Analysis and Price Movement Prediction

## Project Overview

This project involves a comprehensive analysis of cryptocurrency market data to predict 24-hour price movements (Up or Down). It covers data loading, cleaning, exploratory data analysis (EDA), feature engineering, and the training and evaluation of machine learning models to classify price trends.

## Dataset

The dataset `top_500_metadata.csv` contains metadata for the top 500 cryptocurrencies, including:

*   `id`, `symbol`, `name`
*   `current_price`, `market_cap`, `total_volume`
*   `high_24h`, `low_24h`, `price_change_24h`, `price_change_percentage_24h`
*   `ath` (All-Time High), `atl` (All-Time Low), `ath_date`, `atl_date`
*   `circulating_supply`, `total_supply`, `max_supply`
*   `roi`, `last_updated`

### Initial Observations:
*   The dataset initially contained 500 rows and 26 columns.
*   Missing values were identified in `high_24h`, `low_24h`, `price_change_24h`, `price_change_percentage_24h`, `market_cap_change_24h`, `market_cap_change_percentage_24h`, `max_supply`, and `roi`.
*   The `roi` column had a significant number of missing values (459 out of 500), leading to its removal.

## Methodology

1.  **Data Loading & Initial Inspection**: The data was loaded into a pandas DataFrame, and initial checks were performed using `df.head()`, `df.info()`, `df.describe()`, and `df.columns.tolist()` to understand its structure, data types, and basic statistics.

2.  **Data Cleaning**: Missing values were addressed by dropping the `roi` column due to high cardinality of nulls and then removing remaining rows with any null values. The DataFrame was reset, resulting in 254 cleaned entries.

3.  **Exploratory Data Analysis (EDA)**:
    *   **Price Distribution**: Analyzed the distribution of current crypto prices, revealing a heavily skewed distribution with a few high-priced cryptocurrencies.
    *   **Market Capitalization**: Identified the top 10 cryptocurrencies by market cap, highlighting Bitcoin's dominance.
    *   **24-hour Price Change**: Explored the distribution of 24-hour price change percentages to understand market sentiment (gainers vs. losers).
    *   **Top Gainers & Losers**: Visualized the top 10 cryptocurrencies with the highest gains and losses over 24 hours.
    *   **Market Cap vs. Total Volume**: Investigated the relationship between market capitalization and total trading volume.
    *   **Correlation Heatmap**: Generated a heatmap to visualize correlations between numerical features.
    *   **Circulating Supply**: Examined the top 10 cryptocurrencies by circulating supply and its potential impact on price.

4.  **Feature Engineering**: Several new features were created to enhance the model's predictive capability:
    *   `Target`: A binary variable (1 for price UP, 0 for price DOWN) based on `price_change_percentage_24h`.
    *   `ath_drop_pct`: Percentage drop from All-Time High.
    *   `atl_rise_pct`: Percentage rise from All-Time Low.
    *   `volume_to_mcap`: Ratio of total volume to market capitalization (a liquidity indicator).

5.  **Model Training**: The data was split into training (80%) and testing (20%) sets. Features were scaled using `StandardScaler` to ensure all features contribute equally to the model. Three classification models were trained:
    *   Logistic Regression
    *   Decision Tree Classifier
    *   Random Forest Classifier

6.  **Model Evaluation**: Model performance was evaluated using:
    *   **Accuracy Score**: A comparison of accuracy across all three models.
    *   **Classification Report**: Detailed metrics (precision, recall, F1-score) for the best-performing model.
    *   **Confusion Matrix**: A visual representation of true positives, true negatives, false positives, and false negatives.
    *   **Feature Importance**: Analyzed the importance of each feature in the Random Forest model's predictions.


## Key Findings

*   **Data Imbalance**: The `Target` variable (price UP/DOWN) showed a slight imbalance, with more cryptocurrencies experiencing a price decrease (168 DOWN vs. 86 UP) in the 24-hour period captured by the dataset.
*   **Bitcoin Dominance**: Bitcoin consistently appeared as a significant outlier in terms of market cap and volume, far surpassing other cryptocurrencies.
*   **Feature Importance**: The engineered features `atl_rise_pct` and `ath_drop_pct` were identified as the most important predictors for price movement, highlighting the significance of historical price extremes in predicting short-term trends.
*   **Model Performance**: Among the trained models, **Logistic Regression** achieved the highest accuracy of approximately 82.35%, followed by Random Forest (68.63%) and Decision Tree (60.78%). This suggests that a simpler linear model captured the underlying relationships in this dataset effectively for the chosen features.

## Conclusion

This project successfully demonstrated a pipeline for analyzing cryptocurrency market data and predicting short-term price movements. The cleaned dataset and engineered features allowed for a meaningful EDA and the development of predictive models. While Logistic Regression provided the best overall accuracy, further optimization and exploration of more advanced models or larger datasets could yield even better results. The final predictions were exported to a CSV file, ready for visualization in tools like Power BI or Tableau.  
