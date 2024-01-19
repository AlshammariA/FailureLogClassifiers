# Failure Logs Classifiers
This is the artifact of our paper title **230,439 Test Failures Later: An Empirical Evaluation of Flaky Failure Classifiers**. The preprint will be available soon. 
Authors: Abdulrahman Alshammari, Paul Ammann, Michael Hilton, Jonathan Bell


# How to replicate our experiment? 

## Step 1) Preprocess the Dataset

In this step, we demonstrate how to process the dataset (Flaky and True Failures logs) and prepare the logs to be used as an input for the de-duplication approaches as discussed in our paper. For comprehensive guidelines on this step, please refer [Here](https://github.com/AlshammariA/FailureLogClassifiers/tree/main/processing-dataset).

## Step 2) De-duplication Approaches

In this step, we show how do we apply/implmenet the three approaches we discuss in our paper: **1)text-baed matching**, **2)Failure Log Classifier**, and **1)TF-IDF**. Please refer [Here](https://github.com/AlshammariA/FailureLogClassifiers/tree/main/de-duplication-approaches) for complete guidelines. 