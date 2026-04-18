Part B: Business Case Analysis
B1. Problem Formulation
(a) This is a Supervised Learning problem, specifically Regression. The target variable is items_sold. We are predicting a numerical value based on features like location, promotion type, and store size.
(b) "Items sold" (volume) is a more reliable target than sales revenue because revenue can be skewed by the price of products. Volume directly shows how many customers reacted to a promotion, illustrating the principle of choosing a stable target proxy that isn't affected by external price inflation.
(c) Instead of one global model, I propose a Segmented Modeling strategy. We should group stores by location_type (Urban vs. Rural) because customers in different areas respond differently to the same discounts.

B2. Data and EDA Strategy

(a) I would join the tables using store_id and date. The final grain would be one row per store, per day. I would aggregate total footfall and average competition density for each store.
(b) EDA Plan:
Bar Chart: Promotion Type vs. Items Sold (to see which offer is generally strongest).

Line Chart: Sales over time (to find seasonal spikes).

Scatter Plot: Competition Density vs. Sales (to see if rivals impact our success).

Correlation Heatmap: To see which features (like is_festival) relate most to sales.
(c) Since 80% of data has no promotion, the model might become biased. I would handle this by oversampling the "promotion" days or using a weighted loss function to make the model pay more attention to the days when deals were active.

B3. Model Evaluation and Deployment

(a) I would use a Temporal Split (the most recent months as the test set). A random split is wrong because it would let the model "cheat" by seeing future data. I would use RMSE (Root Mean Squared Error) to see how many units off our predictions are.

(b) I would use Feature Importance to show that in December, "Holiday flags" drove the recommendation, while in March, "Price discount" was the main driver for that specific store.

(c) Deployment: Save the model using joblib. I would set up an automated script to feed in new store data every month. I would monitor for Model Drift—if the prediction accuracy drops significantly, it’s time to retrain the model with newer data.
