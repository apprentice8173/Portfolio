# Portfolio
## My projects
### Executive Summary
This project uses logistic regression to predict if a pit stop will be fast or slow based on race data such as lap time, circuit, and race progression. This analysis merges two open, Formula 1 datasets from 2022 to 2025.  

This model gave an accuracy score of 67%, precision of 63%, and recall of 59%. All the metrics are above the 50% random guess threshold, but the model need improvements to increase reliability. The model’s precision of 63% means that 37% of predicted true results were slow, this could negatively impact the drivers position and result in a change of strategy. 

Gathering more race data, along with data from different sources, would improve this model as more conditions would be imported, diversifying the model. By adding more features, new insights that impact the speed of a pit stop may be revealed. Different circuits have varying pit lengths so building a circuit specific model would improve usefulness to a strategist but lower the evaluation metrics due to circuit having the most influence with a coefficient of 0.77.

Formula 1’s unpredictable nature, with numerous variables affecting pit stops, a model with an accuracy score of at least 85% would be more reliable for strategic decision making while also being a realistic goal. 

![Histogram](/images/histogram-example.png)
### Data Engineering & Data Infrastructure and Tools
Two open Formula 1 datasets were attained from Kaggle, an online community for data scientists (“What is Kaggle?,” 2025). The first document, f1_strategy_dataset, was a single CSV file containing tire, lap, and race information. This file did not include any laps completed under safety car, pitstop information or driver details. A second dataset, Race Data, was obtained to provide additional variables necessary to create a versatile analysis. This dataset contained multiple CSV files comprising of driver demographics, pit stop records, and complete lap time information.

Before merging, the datasets required transformations and cleaning. Power Query was chosen to perform these alterations as it connects directly to Excel, shows clear transformation steps, and has a user-friendly interface. Python was considered as it is being used for the analysis and it also had data cleaning capabilities, but Excel was chosen so that the data could easily be seen in spreadsheets format, making it easier to visualise, and the apprentice felt stronger in Power Query than Python. 

As f1_strategy_dataset only contained data from 2022 to 2025, Race Data was filtered to match this period. F1_strategy_dataset included laps completed in pre-season testing, these were removed to avoid skewing the data.

From pit_stops in Race Data, pit stops over 2 minutes was removed as retirements and red flags were recorded as pitting. A test group was selected at random and manually checked for retirement or red flag, none were actual pit stops. Removing the extreme values may cause bias as it would be impossible to check them all, so a handful may be actual stops. However, including these records would have caused more issues as they are not actual pit stops and would skew the data. 

While exploring f1_strategy_dataset it was discovered that any laps completed under safety car was not in the dataset. The prediction required completeness to ensure an accurate and consistent model, so every lap of the race was needed. To merge the two tables together a primary key was created by using the circuit, driver, lap, and year to make a unique column. The table lap_times from Race Data contained all the laps, so a left merge was performed, keeping all the rows in Race Data and only matching from f1_strategy_dataset. 

The age of the drivers was added using their date of birth. This meant that it can be used for analysis, as dates are harder to use in logistic regression than numbers. This also made the data easier to understand as stakeholders can comprehend age. 

By merging two index columns, one starting at 0 and one at 1, a pit_next_lap column was created from offsetting the pit_stop column.

Race_progressed, stint, and position_change are all DAX calculated columns. Although f1_strategy_dataset already had these columns, the left merge meant there were missing values. These columns were calculated only using columns in the lap_times file to ensure that there were no blank values, helping with the completeness of the dataset. 

Once the data was loaded into Excel a correlation chart was created. This highlighted that there was some very high correlation between some columns. Date and quali_date had a correlation of 1 indicating a perfect positive relationship. Other date and time columns were showing a high positive correlation like year and race_start_time with quali_time. To avoid overfitting and resolve the multicollinearity only one date feature will be used, broken up by day, week, and year. 

For this analysis, the pit duration was categorised into a fast or slow stop. A fast stop was under 23.5 seconds as this was the average duration in the cleaned data. This gave a binary outcome that could be used for logistic regression. 

### Analysis
The supervised learning technique, logistic regression was chosen because it supports binary classification and produces interpretable outputs. Google Colab was used to build the model, as it is free, supports easy sharing and collaboration, simple to learn, and can handle large datasets. 
Google Colab is a cloud service and would not be suitable for personal or sensitive data. As the datasets are publicly available and no confidential information, Google Colab was acceptable to use.

A correlation chart, figure, was created from the data. Columns with a high correlation score indicates a strong relationship with fast_stop making it useful for prediction. Fast_stop has the highest correlation with circuit_id. This positive correlation suggests that the leading impacting factor for pit speed is the circuit. Race_progressed, nationality_id, and tyre_life all have a correlation under 0.01 suggesting there is a weak relationship and may not be useful in the prediction. 

![Histogram](/images/confusion_martix.png)
