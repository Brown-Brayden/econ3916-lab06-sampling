# econ3916-lab06-sampling
# Sampling for Machine Learning — Train-Test Splits

## Objective
I used the Titanic dataset and a simulated 1936 election to show how the way a sample is drawn, whether for a train-test split or a poll, decides how far its results can be trusted.

## Methodology
- Explored the Titanic dataset (891 passengers) with survival as the target, and compared survival rates by passenger class.
- Compared a naive 80/20 split with a split stratified on survival, checking the survival rate and class shares in each half.
- Stratified on passenger class and survival together so both shares stayed the same in train and test.
- Found and fixed data leakage in a StandardScaler step and a SimpleImputer step by splitting first and fitting on the training rows only.
- Wrote split_by_share(), a function that splits a table by a test share and a seed, and checked that it reproduces the lab's own split.
- Simulated the 1936 Literary Digest poll on 10 million voters and compared it with a random sample of 50,000.
- Computed Meng's data defect correlation and used his formula to predict the biased sample's error.
- Ran 100 replications of both samples to compare their bias and spread.

## Key Findings
- Stratifying kept the survival rate the same in the training and test sets; a naive split left them apart by chance.
- Fitting a scaler or imputer before splitting lets the test rows shape the training data. The fix is to split first, fit on the training rows, and only transform the test rows.
- A biased sample of 4,382,503 responses was less accurate than a random sample of 50,000.
- Sample design beats sample size: a data defect correlation of 0.1475 produced an error of 8.3 percentage points.
- Across 100 replications, the biased estimates were tightly grouped but all wrong by the same amount, while the random estimates were more spread out but centred on the truth.
