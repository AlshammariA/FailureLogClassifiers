# De-duplication Approaches

We show how the three approaches that we discuss in our paper have been implemented. 
### Text-Based-Matching Approach
>TextBasedMatching.ipynb

This script has the following main parts:
1. Generate the row result per failure per test by applying this approach. The outcome is saved in `Result/PerFailureResult.csv` 
2. Find which failure is repetitive. This generate the outcome per project as shown in Table II in our paper. The outcome is saved in `Result/RepetitiveFlakyFailure.csv`
3. Find how the text-based-matching approach works as shown in Table III. The correspond result is saved in `Result/TextBasedMatchingResult.csv`
4. Get top most exceptions in Flaky and True Failures (Table IV in our paper). The result is saved in `Result/TopMostExceptions.csv`

### Failure Log Classifier
>FailureLogClassifier.ipynb

This script will train the data (from *FeaturePerTest.csv*) and the result is saved in `Result/DT_FinalClassifierResult.csv` for Decision Tree model and `Result/NB_FinalClassifierResult.csv` for the Naive baise model. 
### TF-IDF
>TFIDF.ipynb

The script aims to train the data using the tf-idf (based on the exception type and stack traces). The result is saved as `Result/TFIDF.csv`

To combine the Failure Log Classifier and TF-IDF (as shown in Table V), you can run the following script
>ClassifiersAnalysis.ipynb
