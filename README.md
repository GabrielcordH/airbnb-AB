# **AB Tests Simulation in New York City Airbnb Data**

![Static Badge](https://img.shields.io/badge/In_Progress-Purple?style=flat)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)

---

## Context
AB tests can be used to make data-driven decisions by comparing two versions of something, like a web page or email, to determine which performs better, ultimately improving conversion rates, user experience, and profitability. That said, I am using data available on Kaggle (https://www.kaggle.com/datasets/arianazmoudeh/airbnbopendata) to simulate some AB tests following a statistically rigorous process. 

My goal here is to find the most important variables that can positively and negatively impact the pricing and valuation of Airbnbs through AB tests using the data avaliable and doing some feature engineering

---  

## Methodology
The preprocessing was made by removing some duplicate entrys and filling the NMAR missing occurrences, specially in the review section where hosts with zero reviews in which listed as missing data, and the same for house rules. I also removed some non-helpful features like country and license.

The feature engineering was made by in three steps:
- Used sklearn to find the most common terms in the house rules feature, ignoring stop words, then used re to search the hous_rules feature for keywords such as pet friendly, no smoking, no parties, etc., thus creating a list of dummy variables
- Used Geopandas to calculate the minimum absolute distance from each airbnb to the Central Park, one of the most expensive areas in NYC. The GEOJSON of Central Park was acquired from data.gov (https://catalog.data.gov/dataset/national-parks-c0904/resource/3ddcf942-ddf1-4e3d-9d70-0432b6029f45)
- Used GeoPandas to calculate the minimum absolute distance to the nearest subway station The GEOJSON of subway stations was acquired from data.gov (https://catalog.data.gov/dataset/mta-subway-stations)

The AB tests were done using this parameters 
- Statistical Power ($\beta$) -> 80%
- $\alpha$ -> 5%
- Minimum sample size: N = $\frac{(\sigma^2_{con} + \sigma^2_{exp})(z_{1-\frac{\alpha}{2}} + z_{1-\beta})^2}{\delta^2}$
