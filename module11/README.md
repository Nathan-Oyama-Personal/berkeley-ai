# Module 11: What drives the price of a car?

Nathan Oyama's Workspace for UC Berkeley Machine Learning &amp; Artificial Intelligence 2025

April 15, 2025

---

To use this data analysis based on the given data set, your customers need to select models _elsewhere_ because the data set does not include sufficient information to distinguish one model or variant from another. For example, assume that someone is looking for a pickup truck with two rows of seats to sit six passengers such as some kind of Ford F-150. But Ford F-150 used to have a variant for a single-row seat configuration which is not what he is looking for. The data set put all kinds of Ford F-150 into the same model, and there is no "seat count" field. He would also prefer Chevy Silverado over Ford F-150 when it comes to the grill design.

After your cusotmers choose the model(s), you can help them select the right car from the inventory within their budget.


## Goal: Making models to predict the price of a car

**The price models differ across car models.** For example, you cannot use the same price model with VW Beatle and Mercedes-Benz S-Class. In this data analysis, I selected the three most popular car models--Ford F-150 (truck), Toyota Camry (sedan), and Jeep Wrangler (SUV)--to make three pricing models.

Decide the following parameters to predict the price of a car:


**Condition** There are six condition grades: "New", "Like new", "Excellent", "Good", "Fair", and "Salvage". Most cars have either condition grade, but some records do not ("Unknown").

**Odometer mileage** Most cars have the odometer mileage reading between 0 mile and 299,999 miles. I discarded other cars which drove 300,000 miles or even more as instructed in the next section.

**Model year** Most records contain one of the model years ranging betwen 1900 and 2022.



## Cleaning Data

The original data set contains some invalid records such as the most expensive car being priced at $3.7bn, and those few samples with extremely unusual values can affect the data analysis and modeling. In this data analysis, I removed the following cars from the data set:

* Cars with unreasonable model names (e.g. "SPECIAL FINANCE PROGRAM 2021")

* Cars with top 0.1% price tags (> $95,000)

* Cars with odometer mileage of 300,000 miles or greater


The following cars are intentionally kept:

* Cars of unknown conditions

* Cars with no VIN


## Classifying cars into price tiers

Price tier     | Minimum price | Maximum price | Percentile |
---------------|---------------|---------------|------------|
Cheap cars     | $0            | $999          | 10.3%      |
Typical cars   | $1,000        | $69,000       | 99.2%      |
Expensive cars | $70,000       | $94,999       | 99.8%      |


## Modeling (polynomial, k-fold cross validation)

Use the _k_-fold cross validation method to get the following polynomial model:

$$\hat{y} = \sum_{j=1}^{d} \theta_{j} \phi_{j} + \alpha$$

where 

* $\hat{y}$ : the predicted price
* $\theta_{j}$ : the coefficients
* $\phi_{j}$ : The input values
* $d$ : the number of features/parameters
* $\alpha$ : the intercept term


Sample model  | Condition | Mileage $([\theta]_{j}, \alpha)$ | Model Year $([\theta]_{j}, \alpha)$ |
--------------|-----------|----------------------------------|-------------------------------------|
Ford F-150    | Good      | ([0,0,0], 0)                     | ([0,0,0], 0)                        |
Toyota Camry  | Good      | ([0,0,0], 0)                     | ([0,0,0], 0)                        |
Jeep Wrangler | Good      | ([0,0,0], 0)                     | ([0,0,0], 0)                        |


---

Nathan Oyama. nathan.oyama[&alpha;&tau;]berkeley.edu.

