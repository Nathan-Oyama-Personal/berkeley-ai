### Capstone Project: the best and worst US cities to build solar plants

* Nathan Oyama (Group C)
* July 30, 2025
* Source: [Capstone (Jupyter Notebook)](./eda.ipynb)


Suppose that you want to build a new solar power plant somewhere in the United States. Which city or region would you choose? There are several factors to consider: 

* Climates (sunshine durations)
* Land values
* Proximity to large cities

#### Rationale

There should be specific locations and conditions where building solar power plants make sense. For example, you would want to build solar power plants near Las Vegas, where land values are very low, many sunny days, and close to the large city&mdash;more than Barrow, Alaska, which is the northernmost small city.



#### Data Sources and Exploratory Data Analysis (EDA)

Check the existing solar power plants in the United States, their sunshine durations, the land values, and city profiles:

* Kaggle: "Percent Sunshine by US City". 18 Jan 2023. kaggle.com/datasets/thedevastator/annual-percent-of-possible-sunshine-by-us-city.

* US Geological Survey: "The United States Large-Scale Solar Photovoltaic Database (USPVDB)". 28 Apr 2025. US Department of the Interior. energy.usgs.gov/uspvdb/data.

* landvalue: "ZHVI 3-Bedroom Time Series($) - City". 25 Jun 2025. landvalue.com/research/data.

* Pareto Software: "United States Cities Database - Basic". 9 Jun 2025. simplemaps.com/data/us-cities.


In Section 4 (_"Combining Four DataFrames into One"_), you will combine the four DataFrames from the previous section into one: `df_solar`: 


Table 1: The columns in the sample data set

| Column       | Example         | Data Sets                                |
| :------------| :-------------- | :--------------------------------------- |
| City name    | ALAMEDA, CA     | City, Sunshine, Land Value, Photovoltaic |
| Longitude    | -149.789413     | City, Photovoltaic                       |
| Latitude     | 61.587349       | City, Photovoltaic                       |
| Population   | 25,824          | City                                     |
| Density      | 1780.7          | City                                     |
| Jan ... Dec  | 58              | Sunshine                                 |
| Current      | 14.4            | Photovoltaic                             |
| Land Value   | $840,048.91...  | Land Value                               |

In the machine learning process, use the logarithm of the currents instead of the original currents to increase the model accuracy.


#### Methodology

Split the `df_solar` DataFrame into two groups: the rows which have values in the Current column and the other rows which do not. Note that all rows have values in any other columns. You can use the first group of the DataFrame to build a machine learning model and figure out what algorithm and hyperparameters you should use for this problem. Then rebuild a machine learning model with the same algorithm and hyperparameters by using the first group of DataFrame for the training data set and predict the missing Current fields in the second group of the DataFrame.

For the first group of DataFrame which has values in the Current column, shuffle the rows by using the random seed 42, assign 75% of those rows to a training data set and the remaining 25% a test data set. Split each data set again into the feature DataSet $X$ and the prediction value $y$. Now you have four data sets: $X_{\textrm{train}}$, $y_{\textrm{train}}$, $X_{\textrm{test}}$, and $y_{\textrm{test}}$.

To find the best algorithm and hyperparameters, apply cross validation for the first group of the DataFrame. That is, train the model $X_{\textrm{train}}$ and $y_{\textrm{train}}$ by using the following algorithms and hyperparameters: 

| Algorithm           | Method of scikit-learn     | Hyperparameter |
|---------------------|----------------------------|-----------------------------|
| Linear regression   | `LinearRegression()`       | None                         |
| K-nearest neighbors | `KNeighborsRegressor()`    | Number of neighbors: 3, 5, 7 |
| Decision tree       | `DecisionTreeRegressor()`  | Maximum depth: 3, 5, 7       |
| Ridge regression    | `Ridge()`                  | Constant that multiplies the L2 term $\alpha$: 0.1, 1.0, 10.0 |
| Support vector regression (SVR) | `SVR()` | $C$ (an inverse of the strength of regularization: 0.1, 1.0, 10.0;<br>$\gamma$ (gamma): scale or auto |
| Ensemble voting regression | `VotingRegressor()` | Use all  the other algorithms.<br>CV 2;<br>scoring: the negative mean squared error |

For the SVR algorithm, there are two types of the $\gamma$ values: 

* $\gamma$ scale: 

$$\frac{1}{n_{\textrm{features}} X.\textrm{var()}}$$

* $\gamma$ auto: 

$$\frac{1}{n_{\textrm{features}}}$$

For each algorithm, train a model by using the training set $X_{\textrm{train}}$ and $y_{\textrm{train}}$, apply this model to $X_{\textrm{test}}$ to predict the current field, and get the mean square error (MSE) of the predicd current values with the actual values in $y_{\textrm{test}}$. Perform this operation for each hyperparameter to get the MSEs.


Algorithm with best hyperparameters | Lowest MSE score
------------------------------------|-----------------
Linear regression                   | 4.1537
K-nearest neighbors                 | 3.0855
Decision tree                       | 4.432
Ridge regression                    | 3.991
SVR                                 | 3.6409
Ensemble voting regression          | 3.2892

As you can see, the k-nearest neighbors returned the lowest MSE score which means that the model using this algorithm with a certain hyperparameter was the most accurate. Manually repeat this model assessment and find the best hyperparameter, and you can find the model with 5 neighbors returned the same lowest MSE score.

Apply the same algorithm and the hyper parameter, that is, the k-nearest neighbors with 5 neighbors to the entire first group to train a new model which may be more accurate because of the larger sample data set. For the second group of the DataFrame which did not have a valid value in the Current field, drop the column to make a feature DataFrame $X_\textrm{predict}$. Apply the new model to the feature DataFrame $X_\textrm{predict}$ and you can get the predicted Current values for the 49 cities listed in the second group of the data set.

**Note:** The codes used in this task are mostly based on the worksheet of Module 20 for this program: _"Comparing Aggregate Models for Regression"_ (try_it_20_1.ipynb). 7 May 2025.


#### Results

Sort the second group of data set by the predicted current. The cities with the high predicted current have features that are similar to the other cities in which solar power plants are already built. 

**The most favorable cities to build solar power plants** with the highest predicted current are listed as follows:

US City     | Land Value | Population | Density | Latitude | June | November | Current (MWh)
------------|------------|------------|---------|----------|------|----------|--------------
Key West, FL | $1,285,405 | 25,824 | 1780.7 | 24.6 | 77 | 71 | 361.9
Jackson, MS | $85,274 | 331,332 | 518.0 | 32.3 | 70 | 55 | 161.2
Flagstaff, AZ | $650,010 | 77,868 | 446.4 | 35.2 | 88 | 72 | 129.6
Amarillo, TX | $211,068 | 205,100 | 748.8 | 35.2 | 79 | 67 | 108.2
Ely, NV | $255,374 | 3,941 | 199.5 | 39.3 | 81 | 65 | 108.2


**The least favorable cities to build solar power plants** with the lowest predicted current are listed as follows:

US City     | Land Value | Population | Density | Latitude | June | November | Current (MWh)
------------|------------|------------|---------|----------|------|----------|--------------
Omaha, NE | $278,435 | 826,161 | 1318.9 | 41.3 | 72 | 49 | 8.6
Dodge City, KS | $237,736 | 27,652 | 711.1 | 37.8 | 77 | 63 | 10.1
Concordia, KS | $143,484 | 5,067 | 434.4 | 39.6 | 78 | 59 | 10.1
Tulsa, OK | $217,766 | 740,620 | 805.1 | 36.1 | 66 | 50 | 10.8
Des Moines, IA | $227,345 | 560,170 | 930.5 | 41.6 | 69 | 45 | 11.6

Again, the values in the "Land Value" column is the average price of a 3-bedroom house in the city, the values in the "November" and "June" columns are the number of sunshine hours in these months.

The following is a list of features, sorted by the importance score, you can get while training and assessing the models by using the first group: 

Feature | Importance Score
--------|-----------------
lat | 0.059882
NOV | 0.032363
JUL | 0.031565
Land Value | 0.027916
MAY | 0.024683
density | 0.024294
FEB | 0.016571
JAN | 0.012489
population | 0.009800
APR | 0.005774
AUG | 0.003775
MAR | 0.001454
DEC | -0.006241
JUN | -0.009242
OCT | -0.010082
lng | -0.010163
SEP | -0.012938

That is, the latitude is the most important factor to determine the predicted current of each city. Other important features are the sunshine hours of November and July; November ends 20 days prior to the winter solstice, and July starts 10 days after the summer solstice. Interestingly enough, the sunshine hours of December and June have relatively low important scores. The other important features are the land value which is the average price of the 3-bedroom houses and the population density. The population of the city has the moderate importance score. The least important features are the sunshine hours of September and October, and the longitude which might not be very relevant to the economy or climate of the cities.

The results look reasonable. The most favorable city to build a new solar power plant is Key West, Florida, which is the southernmost city of Florida, observes many sunshine hours in summer and winter. Note that the land value of Key West is very high which might imply that people there should be wealthy enough to invest, build, and operate solar power plants. The least favorable city to build a new solar power plant was Omaha, Nebraska. Omaha rarely observes sunshine hours in winter, and the land value is relatively low despite the large population and high population density.


#### Further analysis

The models and predicted currents they made could have questionable accuracies due to the small sample data set. The original data set for the sunshine hours only contains 158 city records. Merging other data sets reduces this number to even lower: 133 city records. In the 133 city records, 84 city records have the current values whereas the other 49 records do not. With this small sample set, you built the model based on the 84 city records and predicted the currents of 49 cities.

The original city data set contains as many as 31,254 city records although it might not be meaningful to compare between two adjacent small cities such as Berkeley and Oakland. You may want to have a greater data set of sunshine hours for every US city&mdash;or every US county. There are 3,242 counties in the United States, and this number is still much greater than 133, and such a decent data set will make the model even more accurate. In that case, you may need to assess the algorithms and hyperparameters to rebuild a new, better model.

You used 17 features, and these features might be quite relevant to predict the current of solar power plants&mdash;except the longitude. You may want to add more relevant features such as the distance from the sea, political factors such as the renewable energy policies in the local government, as well as "susipcious features" such as the elevation of the cities or counties.
