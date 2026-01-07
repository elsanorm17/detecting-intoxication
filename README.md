# Detecting Intoxication

This project uses a dataset from the UC Irvine Machine Learning Repository at https://archive.ics.uci.edu/dataset/515/bar+crawl+detecting+heavy+drinking. The dataset contains smartphone accelerometer data and TAC measurements for 13 subjects while participating in the Ohio State University Annual Senior Bar Crawl. This project investigates whether smartphone accelerometer data can be used to detect intoxication for the 13 subjects in this study.

Using this labeled dataset, we trained and evaluated several supervised learning models, namely Logistic Regression, Classification Trees, Random Forests, Bagging, Boosting, Support Vector Machines, and K-Nearest Neighbors, and one unsupervised method, Hierarchical Clustering. Model performance was assessed using accuracy, precision, recall, and F1-score, focusing on how often intoxicated periods were correctly identified. Bagging provided the best overall performance, with 76.94% accuracy.
