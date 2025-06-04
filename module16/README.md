# Module 16: Comparing Classifiers

Nathan Oyama's Workspace for UC Berkeley Machine Learning &amp; Artificial Intelligence 2025

June 4, 2025

* Notebook: [./prompt_III.ipynb](./prompt_III.ipynb)

There is a data set of the marketing campaigns of a banking institution in Portugal. Each record corresponds to a customer who has participated in the campaign, and there are several profile fields: his or her age, job status, martial status, whether or not he or she subscribed a term deposit.

In this data analysis, you predict how likely someone starts subscribing a term deposit based on those profile features. 

The following table summarizes the machine learning models used, their training time, and accuracies. The decision tree with maximum depth of 15 performed the best in unforseen data, while K nearest neighbors with 7 neighbors performed fast and a decent accuracy. All models outperformed *"simply assming no one starts subscribing the term deposit"*.

| Model (scikit-learn)   | Parameters              | Train Time [s] | Train Accuracy | Test Accuracy |
| :--------------------- | :-----------------------| -------------: | -------------: | ------------: |
| Baseline (all "no")    |                         |                | 0.8871         | 0.8880        |
| LogisticRegression     | C= 0.1                  |   0.0746       | 0.9071         | 0.9076        |
| LogisticRegression     | C= 1.0                  |   0.0265       | 0.9073         | 0.9076        |
| LogisticRegression     | C=10.0                  |   0.0268       | 0.9073         | 0.9077        |
| KNeighborsClassifier   | n_neighbors=3           |   0.0104       | 0.9310         | 0.8922        |
| KNeighborsClassifier   | n_neighbors=5           |   0.0107       | 0.9180         | 0.8978        |
| KNeighborsClassifier   | n_neighbors=7           |   0.0100       | 0.9114         | 0.9005        |
| DecisionTreeClassifier | max_depth= 5            |   0.0434       | 0.9112         | 0.9108        |
| DecisionTreeClassifier | max_depth=10            |   0.0760       | 0.9309         | 0.9070        |
| DecisionTreeClassifier | max_depth=15            |   0.1062       | 0.9590         | 0.8948        |
| SVC                    | C= 0.1, kernel='rbf')   |   6.2822       | 0.8979         | 0.8974        |
| SVC                    | C= 1.0, kernel='rbf')   |   7.2931       | 0.9203         | 0.9064        |
| SVC                    | C=10.0, kernel='rbf')   |  15.4600       | 0.9576         | 0.9019        |
| SVC                    | C= 0.1, kernel='linear' |  27.4683       | 0.8978         | 0.8966        |
| SVC                    | C= 1.0, kernel='linear' | 292.6501       | 0.8978         | 0.8966        |

