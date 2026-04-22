# Business Case Analysis - Promotion Effectiveness
--------------------------------------------------------------------------------------------------------
# B1 - Problem Formulation

# B1 (a) ML problem formulation
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



