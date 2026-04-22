# Business Case Analysis - Promotion Effectiveness
-----------------------------------------------------------------------------------------------------
# B1 - Problem Formulation

# B1 (a) 
This can be turned into a **supervised machine learning problem** whose purpose is to predict, for each store in each month, which of the 5 promotion will generate the highest number of items sold.

**Target Variable:**
The number of **items sold** in a store during a given month under a specific promotion. 

**Candidate input features:**
1) Store-level: store size, location type(urban/semi-urban/rural), average monthly footfall, local competition density, and customer demographics.
2) Promotion-level: promotion type, discount depth, minimum spend requirement, and duration.
3) Time-level: month, quarter, festival flags, and weekend indicators.
4) Historical behaviour: past monthly sales volumes and how the store responded to each promotion in previous months.

**Type of ML problem and justification:**
This is best framed as regression problem(predicting items sold) or promotion-ranking problem where the model scores promotion and selects the top one. Regression is useful because it lets us compare the expected volume uplift from different promotions rather than treating them as equally distant categories.

# B1 (b) 
The company currently uses total sales revenue to measure performance, but that can be misleading. Revenue depends on both how many items are sold and how much each item is priced. A promotion that gives a deep discount might increase volume but reduce average revenue per item, or loyalty bonus might increase revenue without moving more units.

**Using items sold instead:**
1) Directly reflects the stated business goal: maximising the number of units shifted.
2) Is less sensitive to price changes or product-mix effects, so the model can focus on promotion effectiveness rather than being distorted by pricing or margin decisions.

**Broader Principle:**
The target variable should be directly related as possible to the actual business decision. If the goal is to clear more stock or increase footfall conversions, then a volume-based metric is usually more appropriate than a financially derived metric like revenue.

# B1 (c) 
 A junior analyst suggests training a single global model for all 50 stores, but this assumes that every store reacts to promotions in the same way, which is unlikely given the differences in location, footfall, competition, and customer base.

 **Better alternatives:**
 1) Store-cluster models: Group stores into clusters and fit separate models for each cluster. This way, similar stores share learning, but local differences are still captured.
 2) Hierarchical models: Build a model where baseline sales and promotion effects can vary by store, but are practically pooled under a common structure. This borrows strength from data-rich stores while still allowing for store-specific responses.

These strategies are more realistic because they recognise the same Flat Discount might work extremely well in a busy urban mall but underperform in a small rural outlet with different customer expectations.

-----------------------------------------------------------------------------------------------------

# B2 - Data and EDA Strategy

# B1 (a) 

**Data:**
1) transactions
2) store_attributes
3) promotion_details
4) calendar

**Joining logic:**
1) First, join transactions with calendar on date to attach time flags(weekend, festival, etc.)
2) Then join with promotion_details on store_id and month (or date range) to label each transaction with the active promotion.
3) Finally, attach store_attributes via store_id so each transactions also carries store-level information.

**Grain of the final modelling dataset:**
1) One row = one store-month-promotion combination.
2) For that combination, we'll compute metrics like: total items sold, average items per transaction, number of transactions, average revenue per item, and any relevant store-level features.

**Aggregations before modelling:**
1) Aggregate transaction-level data up to the store-month-promotion level.
2) Compute averages for store-level features (e.g., average footfall per month) and encode time effects (month, quarter, festival month). This makes the dataset ready for regression or ranking-style modelling.

# B1 (b) 

Key EDA analyses I would run:

1) Promotion performance by store-type:
   a) Plot: average items sold per store-month, grouped by promotion type and location type.
   b) Look for which promotions consistently boost volume in urban vs rural stores
   c) This informs whether interactions features are useful or if separate models per cluster are warranted.

2) Seasonality and time-trends:
   a) Plot: time-series of monthly items sold across all stores, with lines coloured by promotion type.
   b) Check for peaks around festivals or specific months.
   c) This supports the inclusion of month-of-year, quarter, and festival flags as features, and helps identify whether some months should be treated as special cases.

3) Store-level heterogeneity:
   a) Plot: box-plots of items sold per store under each promotion, grouped by store size or footfall.
   b) Identify "outlier" stores that respond very strongly or very weakly to promotions.
   c) This supports hierarchical or cluster-based modelling, and may flag stores that need special handling.

4) Feature correlations and multicollinearity:
   a) Plot: a correlation matrix or heatmap of numeric features
   b) Check for highly correlated variables that might cause instability.
   c) This guides feature selection and the choice of regularised models (like Ridge/Lasso or tree-based models).

# B1 (c)

If 80% of transactions happen without any promotion, the data is heavily skewed toward the "no promotion" condition, which might bias the model to treat "no promotion" as the default and under-estimate the value of running promotions.

**Potential issues:**
1) The model may not learn robust patterns for less-frequent promotions.
2) Promotion-month effects can be noisy or hard to estimate due to small sample size.

**How to Address this:**
1) Stratified sampling by promotion status: ensure that each promotion (including "no promotion") is adequately represented in training and validation.
2) Weighting or oversampling: assign higher weights to promotion-month observations, or synthetically increase the number of promotion-month samples.
3) Baseline and increment model: model baseline demand (no promotion) separately and then model the incremental uplift from each promotion. This isolates the promotion effect and makes better use of the relatively rare promotion-only-data.

# B3: Model Evaluation and Deployment:

# B3 (a) Train-test split and metrics:

Using a random split across rows is inappropriate here because the data is time-dependent and store-specific. Randomly mixing early and late months would let the model "see" future patterns during training, which would artificially inflate performance.

**Better approach:**
  a) Use a time-based split: train on the first 24-30 months and hold out the last 6-12 months for testing.
  b) Ensure each store's history is kept clean in either training or test, not split across both.

**Metrics and their interpretation:**
| Metric | What it tells us in the context |
|---|---|
| MAE (Mean Absolute Error) | How far off, on average, the model's predicted items sold are from the actual number.|
| RMSE (Root Mean Squared Error) | Penalises large mistakes more heavily, useful if big-over or under-predictions are costly.|
| R-squared | How much of the variation in items sold the model explains, helps compare different model designs.|
| Promotion-choice accuracy | The percentage of times the model's recommended promotion actually was the best-performing one in the test set.|

In practice, lower MAE/RMSE and higher promotion-choice accuracy mean the model is likely to give more reliable guidance about which promotion to run.

# B3 (b) 
If the model recommends Loyalty Points Bonus in December and Flat Discount in March for Store 12, the explanation usually lies in different underlying conditions between those two months.

Using feature importance:
1) Examine how features like month, is_festival, footfall, and promo_type contribute to the predicted items sold in December vs. March
2) For example, in December, the festival effect combined with the loyalty-bonus structure might generate a strong uplift, while in March that effect disappears and a straightforward Flat Discount works better.

Communicating this to the marketing team:
1) Show a side-by-side visual comparing the two months for store 12.
2) Explain simply: "In the festive month, customers respond more to loyalty-style rewards, so the model picks Loyalty Points Bonus. In a quieter month like March, a sample discount drives more volume, so the model switches to Flat Discount."





























