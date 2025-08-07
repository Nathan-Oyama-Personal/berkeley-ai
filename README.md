# Nathan Oyama's Workspace for UC Berkeley Machine Learning &amp; Artificial Intelligence (January 2025)

I have created this Git repository for my assignment work of the online bootcamp at University of California, Berkeley: ["the Professional Certificate in Machine Learning and Artificial Intelligence"](https://em-executive.berkeley.edu/professional-certificate-machine-learning-artificial-intelligence) ([Web Archive of January 2025](https://web.archive.org/web/20241119023126/https://em-executive.berkeley.edu/professional-certificate-machine-learning-artificial-intelligence)). I enrolled in the course on January 15, 2025 and completed it on August 4.

As the course name suggests, this course focused on machine learning (ML) and artificial intelligence (AI) designing&ndash;more precisely, the course covered the following topics: 

* Major algorithms for numerical prediction, time-series analysis, (non-)linear classification, and clustering: logistic regression, ridge regression with L1/L2 regularization, k-nearest neighbors, decision trees, and support vector classification (SVC)
* Ensemble techniques: bagging, boosting like AdaBoost, voting regression and gradient-boosted trees
* Recommendation systems using the Simon Funk SVD gradient descent algorithm and the SURPRISE library
* Natural language processing (NLP) using the natural language toolkit (NLTK) library
* Convolutional/deep neural network (DNN) using Keras for TensorFlow
* Generative AI using Groq
* Mathematical interpretation
* Model implementation using pandas, scikit-learn, and SciPy for Python
* Data visualization using matplotlib and Plotly

I'd like to thank Professor Amit Jambhekar, Aravind Reddy, and all other faculty staff for their incredible support during the course. I would also like to thank my _"classmates"_ who helped me facilitate discussion and shared insightful ideas.


## Assignment 5: Will the Customer Accept the Coupon?

FEBRUARY 26, 2025. In this assignment, I analyzed the coupon usage dataset (probably by OnStar) and checked what kind of drivers claim or discard coupons for bars, coffee shops, restaurants, and so on. For example, frequent bar visitors tend to use the bar coupons. Every record corresponds to a driver who took this survey, and there is the column or the field to enter whether this driver is using the coupon. I divided the number of drivers who entered 1 (for "yes") in this field by the total sample population to yield the *"acceptance rate*. I got several sample groups of drivers and calculated the acceptance rate for each group to see the likeliness of using the coupons.

  - Jupyter Notebook: [./module05/module05-nathan-oyama.ipynb](./module05/module05-nathan-oyama.ipynb)
  - Dataset: [./module05/coupons.csv](./module05/coupons.csv)



## Assignment 11: What drives the price of a car?

APRIL 15, 2025. I analyzed the given data set of various cars on the US market. The sample model I created was made only works within a particular type of vehicle: Ford F-150. You can remake similar models for other types of cars such as Toyota Camry and Jeep Wrangler, but you cannot create a one-size-fits-all model due to low correlations in different car models.

![image](./module11/fig-example.png "The built year vs. price: Ford F-150")

The model takes the built year and odometer mileage as input features and returns a predicted price.

Mileage  | Year | Price (predict)
---------|------|----------------
50,000   | 2015 | $32,300
100,000  | 2015 | $28,132
100,000  | 2005 | $12,148

![image](./module11/images/model-3d.png "The built year vs. price: Ford F-150")

See [./module11/README.md](./module11/README.md) and [./module11/prompt_II.ipynb](./module11/prompt_II.ipynb).


## Assignment 16: Comparing Classifiers

JUNE 4, 2025. So far I have learned various algorithms for numerical prediction models. In this assignment, I apply those algorithms with various hyperparameters to the same problem and compare the accuracy scores.

![image](./module16/fig-example.png "The built year vs. price: Ford F-150")

 See [./module16/README.md](./module16/README.md) and [./module16/prompt_III.ipynb](./module16/prompt_III.ipynb).


## Capstone Project: "The best and worst US cities to build solar power plants"

JULY 30, 2025. This is my Capstone project: building a numerical prediction model for solar power plant output of every US city and applying this model to other US cities where no solar power plant is in service. Then you can tell which cities should have solar power plants which may imply that you should build ones in those new cities.

![image](./module20/usmap-predicted.png "Predicted solar power output")

See [./module20/README.md](./module20/README.md) and [./module20/eda.ipynb](./module20/eda.ipynb).


---

**Disclaimer:** This Git repository is solely used for this online course. Any contents in this repository do not necessarily reflect my views or positions.

Nathan Oyama. nathan.oyama[&alpha;&tau;]berkeley.edu. linkedin.com/in/nathanoyama.

