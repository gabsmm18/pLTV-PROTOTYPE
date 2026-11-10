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

See the **Summary of results** section at the end of the notebook.

## Limitations

- One retailer, mostly UK, many wholesale buyers: not a typical consumer e-commerce business.
- No acquisition-channel or ad data: the project predicts value, but cannot simulate how ad platforms react to the signal.
- Simple features and models, with no tuning or causal methods.
- Good ranking on historical data is not proof of incremental revenue: that needs the experiment in step 4.

## How to run

Click **Open in Colab** above, then **Runtime → Run all**. No installation needed.

## Author

Mattia Mariani, MSc Applied Economics and Finance, Copenhagen Business School.
