# Module 11: What drives the price of a car?

Nathan Oyama's Workspace for UC Berkeley Machine Learning &amp; Artificial Intelligence 2025

April 15, 2025

---

To use this data analysis based on the given data set, your customers need to select models _elsewhere_ because the data set does not include sufficient information to distinguish one model or variant from another. For example, assume that someone is looking for a pickup truck with two rows of seats to sit six passengers such as some kind of Ford F-150. But Ford F-150 used to have a variant for a single-row seat configuration which is not what he is looking for. The data set put all kinds of Ford F-150 into the same model, and there is no "seat count" field. He would also prefer Chevy Silverado over Ford F-150 when it comes to the grill design.

After your cusotmers choose the model(s), you can help them select the right car from the inventory within their budget.


## Goal: Making models to predict the price of a car


## Factors of the pricing model

**Condition**

**Model year**



## Cleaning Data

The original data set contains some invalid records such as the most expensive car being priced at $3.7bn, and those few samples with extremely unusual values can affect the data analysis and modeling. In this data analysis, I removed the following samples:

* Cars with unreasonable model names.

* Top 0.1% cars (> $95,000)

* Odometer mileage of 300,000 miles or greater

**Expensive cars (> $95,000)**


---

Nathan Oyama. nathan.oyama[&alpha;&tau;]berkeley.edu.

