# pLTV prototype: does the first order predict long-term customer value?

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/gabsmm18/pLTV-PROTOTYPE/blob/main/pltv_prototype.ipynb)

Ad platforms like Meta and Google usually value a new customer by their **first purchase**. But two customers with the same first order can be worth very different amounts over time. This project tests, on real e-commerce data, whether early signals predict a customer's future value better than the first order alone, and how you would prove the impact in a real experiment.

## Data

[Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii) (UCI Machine Learning Repository): real transactions of a UK online gift retailer, December 2009 to December 2011, about one million rows. The notebook downloads it automatically.

## What the notebook does

| Step | What it does |
| --- | --- |
| 1. Data cleaning | Audits data quality, cleans it with a logged step for each decision, keeps returns as negative events, builds one row per order |
| 2. Features and target | For each new customer: 12 features from the first 30 days, and net value over the following 180 days as the target |
| 3. Model | Compares the first-order value (naive signal) with linear regression and gradient boosting, using an out-of-time split; evaluates ranking (deciles, value captured by the top 20%) and calibration |
| 4. Measurement | Designs a geo experiment with difference-in-differences and runs a power calculation: how many customers are needed to detect a lift |

## Results

1. Data quality. Only 74.4% of raw rows were usable for LTV; the main loss is missing customer IDs (22.8% of rows). 4.2% of purchased value was returned, so ignoring returns would overstate customer value.

2. Repeat behaviour. 72.4% of customers buy at least twice; the median gap between the 1st and 2nd purchase is 56 days.

3. Target. In the cohort of 3,085 new customers, 48.5% bring no value in the following 180 days, while the top 10% bring 60.0% of all future value.

4. Naive signal vs model. Ranking customers by first-order value, the top 20% hold 44.7% of future value. With gradient boosting, the top 20% hold 54.5% (Spearman 0.32 vs 0.18 for the first order). The model beats the naive signal.

5. Key signals. The model relies most on revenue_30d and first_month.

6. Measurement. Customer value is very noisy (coefficient of variation 2.9). Detecting a +10% lift with 80% power needs about 25,536 new customers in total (522 weeks at this retailer's acquisition rate); a +20% lift needs 6,384 (130 weeks). Recommended design: a geo experiment estimated with difference-in-differences.
## Limitations

- One retailer, mostly UK, many wholesale buyers: not a typical consumer e-commerce business.
- No acquisition-channel or ad data: the project predicts value, but cannot simulate how ad platforms react to the signal.
- Simple features and models, with no tuning or causal methods.
- Good ranking on historical data is not proof of incremental revenue: that needs the experiment in step 4.

## How to run

Click **Open in Colab** above, then **Runtime → Run all**. No installation needed.

## Author

Mattia Mariani, MSc Applied Economics and Finance, Copenhagen Business School.
