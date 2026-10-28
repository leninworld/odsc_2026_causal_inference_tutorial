 ## Dataset

# Candy Campaign Dataset

## Overview

This dataset collection supports analysis of a candy marketing campaign.
It combines historical purchasing behavior, customer-level campaign
outcomes, and simulation ground truth for studying campaign impact and
customer response.

## Dataset Files

### `candy_purchase_history.csv`

Contains purchase records from the three months before the campaign.
Each row represents a user's purchasing activity for a pre-campaign
month.

**Key fields:** - `user_id`: Customer identifier. -
`month_before_campaign`: Month relative to the campaign, represented by
negative values. - `item_price`, `quantity`, `total_spend`: Price,
quantity purchased, and total spending for that record. - `age`,
`gender`, `income`: Customer demographic and income information.

**Purpose:** Understand pre-campaign buying patterns and establish a
baseline for customer behavior.

### `candy_users_600.csv`

Contains one row per customer, combining customer characteristics,
summarized purchase history, campaign exposure, and campaign-period
outcomes.

**Key fields:** - `user_id`: Customer identifier. - `age`, `gender`,
`income`: Customer attributes. - `history_item_price`,
`history_quantity`, `history_total_spend`: Summary measures of
pre-campaign purchasing. - `exposed`: Indicates whether the customer was
exposed to the campaign. - `conversion`: Indicates whether the customer
converted during the campaign. - `campaign_item_price`,
`campaign_quantity`, `campaign_total_spend`: Campaign-period purchase
measures.

**Purpose:** Analyze campaign performance and explore how customer
characteristics and prior purchasing behavior relate to conversion and
spending.

### `candy_simulation_truth.csv`

Contains simulated ground-truth response values for each customer.

**Key fields:** - `user_id`: Customer identifier. - `p0`, `p1`:
Simulated outcome probabilities under two campaign conditions, typically
interpreted as no campaign and campaign exposure. - `true_cate`: The
simulated conditional average treatment effect for the customer,
represented here by the difference between `p1` and `p0`.

**Purpose:** Evaluate whether analytical or causal-inference methods can
recover the campaign's simulated customer-level effects. These
ground-truth fields are simulation-specific and may not be available in
real-world campaign data.

## How the Files Relate

The files can be linked using `user_id`. The purchase-history file
provides monthly pre-campaign records; the customer-level file
summarizes history and records campaign exposure and outcomes; and the
simulation-truth file provides reference probabilities and treatment
effects for evaluation.

## Potential Use Cases

-   Explore customer purchasing patterns before a campaign.
-   Measure campaign conversion and spending outcomes.
-   Compare outcomes across exposed and unexposed customers.
-   Build customer-response or uplift models.
-   Evaluate estimated treatment effects against simulated ground truth.

## Notes

-   These files appear to be structured for a simulated
    campaign-analysis task.
-   `candy_purchase_history.csv` contains multiple monthly records per
    customer, while the other two files contain one row per customer.
-   Treat `candy_simulation_truth.csv` as evaluation/reference data
    rather than ordinary customer features when training a model, to
    avoid target leakage.
-   Confirm the data-generation assumptions before drawing causal
    conclusions from exposure and conversion comparisons.
