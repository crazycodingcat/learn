## Imbalanced dataset
- collect more samples?
- change performance metric: precision, recall, confusion matrix, Kappa, ROC curve
- Resampling:
	- over-sampling
	- under-sampling
- generate synthetic samples:
	- SMOTE (Synthetic Minority Over-sampling Technique)
- try different algo: decision trees often perform well on imbalanced datasets.
- try penalized models: additional cost for making mistakes on minority class during training.
- Change perspective: anomaly detection, change detection.
- get creative:
	- decompose larger class into smaller ones
	- use a one class classifier (e.g. treat like outlier detection)
	- resampling the unbalanced training set into several balanced set, build a classifier for each and ensemble.


## Categorical data encoding:
- mean response per category
- Leabe-One-Out encoding: for each row, use all the other row's mean response, add some noise (more robust to outliers)


## Association rule mining
- just counting..
- Lift: P(x, y) / (P(x)*P(y)) observed frequency of co-occurence / expected f of co-occurance. Expected f is assuming statistical independence between the products. 

## ML in practice - steps:
- Problem definition: meeting w/ stakeholders, identify pain-points, evaluating ML opportunities
- Evaluation strategy: evaluation metric, to have both:
	- business-friendly metric for stakeholder reporting and communication
	- a scientific scoring metric for internal model-optimizing
- Baseline model: e.g. simple rolling avg. 
	- to see if it is worth investing more time into building a full flidged ML model
	- setting the target and a sense-check for the actual ML model
- Data validation: remove outliers from data before model building
- Building model