# DSI15-web-scraping-project

The goal of this project was to compile information and use it to train a machine learning model to accurately predict the salaries of data-related jobs in the UK market.

To do this, we scraped data from the aggregator Indeed.co.uk. We conducted four main searches, looking at roles for Data Scientists, engineers in Machine Learning , Data Analysts, and experts in Artificial Intelligence. We didn’t search simply for ‘Data’, on the basis that this would return many entries for ‘Data Entry’ which would skew our results. Each search was conducted on fifteen major UK cities, and an area within 25 miles of each. For each listing, we extracted data on the job’s Company/Employer, Salary, Title, Location and Description.

Many of the results were duplicated (ie one job showing up in multiple search categories). Strangely there were also a few jobs which showed up in more than one geographic location. There was a handful of jobs from other industries (mainly law) and many job listings which either didn’t include any salary information or included temporary jobs that paid daily or weekly. Once all the unsuitable listings had been dropped, the dataset was left with just over 1500 rows. The next task was to process the salary data into a usable format, and to rationalise the location data.

We could have built a model to predict the actual salary for each job (regression), but instead were asked to split salaries into multiple categories (high vs low) and predict which would apply for each job (a ‘classification’ problem). We began the modelling process by looking only at ‘Location’ as a predictor. We tried out a couple of different models, and achieved a best accuracy score of slightly over 0.66. This means that the model correctly classified about 66.2% of all jobs as having either ‘high’ or ‘low’ salaries. This is significantly better than the baseline score of about 52% that would have been achieved by simply guessing the majority class for all jobs (ie by guessing that they all had ‘low’ salaries).

The next step was to create some new features for the model to work with. We did this by extracting information from the ‘Company’ (whether the employer was an academic institution), and the ‘Title’ column (whether there were any indicators of seniority or junior status). Including these new features gave our models a big boost, improving the best one to an accuracy score of over 78.8%.

After this, we created new features by vectorizing the text in the ‘Description’ column. This involved mapping the words and phrases in the text to specific numbers, to look for patterns that could be used to improve our model’s predictions. Unfortunately this didn’t work, so we dropped these new features and reverted back to the previous set. Up to this point we had tried two algorithms on this dataset, LogisticRegression and RandomForest. We then tried two more types, KNearestNeighbors and XGBoost. Of the four, LogisticRegression remained the most successful, with a score of 0.788.

Finally we were asked to look at what would happen if we needed to prioritise the avoidance of False Positives (ie if it was very important to avoid predicting a high salary when this wasn’t actually the case). We recalibrated the model with this in mind, and saw that this could be achieved at the cost of overall accuracy (because minimising False Positives would mean accepting more False Negatives).

Without data concerning the true costs of False Positives and False Negatives, it is impossible to know the best trade-off. However we looked how we could optimise for this once good cost data becomes available.
