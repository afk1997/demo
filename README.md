---
title: "KPI-Based Reward Calculation"
---

# KPI-Based Reward Calculation

Metrom’s KPI-based incentive model distributes rewards in direct proportion to the performance of a liquidity pool, as measured by a key performance indicator (KPI) such as Total Value Locked (TVL). Rewards are scaled according to the KPI achievement and distributed continuously over the campaign duration.

## Key Parameters

- **Total Reward Pool (R):** Total amount of reward tokens allocated for the campaign.
- **KPI Goal (U):** Upper bound for the KPI (e.g., a TVL target) at which 100% of rewards are distributed.
- **Lower Bound (L):** The minimum KPI threshold below which no rewards are unlocked.
- **Achieved KPI (A):** The current measured KPI value (e.g., current TVL).
- **Campaign Duration (D):** Length of the campaign (in days).
- **Measurement Interval:** The frequency at which rewards are computed (e.g., hourly).

## Scaling Factor Calculation

The rewards are scaled based on the KPI achievement using the following rules:

- **If \(A < L\):**  
  $$ M = 0 $$
- **If \(L \leq A \leq U\):** (linear scaling)
  $$ M = \frac{A - L}{U - L} $$
- **If \(A > U\):**
  $$ M = 1 $$

Thus, the total distributed rewards are:

$$ R_{\text{distributed}} = R \times M $$

## Time-Based Distribution

To ensure rewards are issued continuously, the reward pool is also divided over time.

- **Daily Reward Rate:**

  $$ R_{\text{daily}} = \frac{R}{D} $$

- **Hourly Reward Rate:**

  $$ R_{\text{hourly}} = \frac{R_{\text{daily}}}{24} = \frac{R}{24 \times D} $$

At each measurement interval (e.g., every hour), the current KPI achievement percentage is determined as:

$$ \text{KPI Fraction} = \frac{\text{Current KPI Value}}{U} $$

Then, the effective reward distributed for that hour is:

$$ R_{\text{effective, hourly}} = R_{\text{hourly}} \times \text{KPI Fraction} $$

This ensures that if the KPI is only partially met, only the corresponding fraction of the hourly reward is distributed among liquidity providers.

## Example Calculation

Assume the following:
- **Total Reward Pool:** \( R = 5500 \) UNI  
- **Campaign Duration:** \( D = 7 \) days  
- **KPI Goal:** \( U = \$2.5\text{M} \) TVL  

Then, the daily reward is:

$$ R_{\text{daily}} = \frac{5500}{7} \approx 785.71\ \text{UNI/day} $$

and the hourly reward is:

$$ R_{\text{hourly}} \approx \frac{785.71}{24} \approx 32.74\ \text{UNI/hour} $$

If at a given hour the current KPI (TVL) is 38.28% of the goal, then:

$$ \text{KPI Fraction} = 0.3828 $$

and the effective reward distributed for that hour is:

$$ R_{\text{effective, hourly}} = 32.74 \times 0.3828 \approx 12.53\ \text{UNI/hour} $$

This method ensures that rewards are continuously aligned with actual liquidity performance, minimizing wastage and promoting efficient incentive spending.
