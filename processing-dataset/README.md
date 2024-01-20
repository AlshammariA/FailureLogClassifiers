# Preprocess the Dataset

Our dataset is publicly available on [Zenodo](https://zenodo.org/records/10531160) contains two main parts:
- **Flaky Failures**: These failures collected originally from the [FlakeFlagger](https://github.com/AlshammariA/FlakeFlagger) dataset
- **True Failures**: These failures are collected using PIT by running each studied flaky test against project-related-mutations.


## The Content of the dataset
The dataset contains the following files:
1. **project_name.tgz**

-   The 22 projects folders where each one includes subfolders, each representing a flaky test.
-   Each subfolder, named after a test, contains the following files:
    -   **pit-report(s).xml:**  A set of files which is a result of running a test on mutations. If the file name contains 5X, it indicates the report's result from 5 runs (reported once). If it contains 1X, it reports the result of a single run against all mutants. Total runs per test are 20X.
    -   **test_name.xml:**  Contains sets of all flaky and true failures of a particular test. Flaky Failures are reported in `<test>` blocks and True Failures are reported in `<mutant>` blocks.
    -   **summary-of-test_name.xml:**  A simplified version of the test_name.xml file used as the final shape to be used in our paper (See our repo below for more details).
    - **FeaturesPerTest.csv**: Each failure is converted into a set of features that are discussed in Table 1 in our paper.

2. **FlakeFlagger-testCode-CUT-reports.tgz:**
-   List of Code-Under-Test files names and test code files names used to collect classifier features (refer to Table 1 in the paper).

3. **pit-indexes-per-test.tgz:**

-   JSON file with test names as keys and mutation indexes in pit reports indicating killed, survived, or flaky mutants. This file can be reproduced (will be discussed later).

### test_name.xml structure:
There are two main blocks in each test_name.xml file:
- `<tests>` : contains a list of `<test>` block (each one represent one type of flaky failure reported in FlakeFlagger dataset. Each `<test>` has the following:
	- `<test_name>`: which have these main attributes as follow:
		- ***frequency***: The number of times this failure has been detected 
		- ***project***: The name of the project where this test belongs to
		- ***source***: The source of flaky failure (in our dataset is FlakeFlagger)
		- ***status***: The status of this failure. In this case, the status is FLAKY
	- `<test_exception>`: reports the failure message
	- `test_stackTrace`: Full stactraces of the failure
- `<mutants>` : contains a list of `<mutant>` block (each one represent one mutant that was killed by the test. Each `<mutant>` has the following attributes:
	- `<mutant_name>`: which have these main attributes as follow:
		- ***mutant_id***: refers to the index of the pit report 
		- ***source***: The source where we collect the mutant. In our case, we collect them using PIT
		- ***status***: The status of the mutant. If a test kills this mutant every time it runs, it is KILLED. If the test sometime kills the mutant and sometimes not, then it is FLAKY.  
		- ***numberOfKills***: The number of times the mutant was killed by the test. 

### summary-of-test_name.xml structure:
This is a simplified version of the test_name.xml by considering the following:
1. We consider only the exception type (e.g. AssertionError) in `<test_exception>`
2. We consider only the top lines of the stack traces as discussed in our paper. 
Then, we group the failures based on these steps.

## Prepare the dataset
The script `prepare-dataset.ipynb`will generate two main files:
- **summary-of-test_name.xml**
- **FeaturesPerTest.csv**

The `prepare-dataset.ipynb` has many sections as follow:
- ***Funcitons***: All defined functions that starts from parsing the log, collecting failure exception and stacktraces, till generate the two mentioned files.
- ***Step 0)*** :This is optional. The outcome of this step is **pit-indexes-per-test.json** file which is used to parse mutations. This can be reproduced by running this step. It is worthy to mentioned that this takes 1.5 day to run and collect which mutation per test has either killed, survived, and flaky result. 
- ***Step 1)*** This parse the mutation files to collect True failure and merge them to **test_name.xml** file. 
- ***Step 2)*** This parse the **test_name.xml** to generate **summary-of-test_name.xml**. 
- ***Step 3)*** Generate the **FeaturesPerTest.csv** based on the given **summary-of-test_name.xml**. 

