# Classifying Salaries of Data-Related Jobs

### Introduction

One of my projects for the General Assembly Data Science Immersive course was to scrape job listings from a job aggregation website and apply machine learning algorithms to predict salaries for Data Science related roles in the United Kingdom.
This project was completed in January 2022.

### Goals

The goals of the project are summarized as follows:
1. Determine the factors that are most important in predicting salary for the roles chosen.
2. Scrape data from a job aggregation tool in order to obtain necessary data.
3. To predict salary the most appropriate approach would be a regression model. Here, instead, we just want to estimate which factors lead to high or low salary and work with a classification model.

As we only have two classes (whether the salary is 'low' or 'high'), the baseline model accuracy is 50% (Guessing whether the salary is in either category without any modeling would ensure you are correct half the time, on average).

### Scraping the Data

Job aggregation website Indeed.com was scraped using BeautifulSoup as the website is a simple text page where you can easily find relevant entries. It was possible to identify a number of key tags for information which might be helpful to scrape such as job location, company name, job title, and salary.

I limited my search to job postings in the UK only, including cities across England, Scotland, Wales and Northern Ireland.

### Data Cleaning and EDA

Once the data was collected, it was cleaned using various techniques learned throughout the course. Although I was initially able to scrape nearly 60,000 data points, after cleaning I was left with just more than 1,300. This was largely due to many duplicated data points, and entries with missing or irrelevant information among other factors. The number of useable data points was deemed sufficient to build predictive models to complete the project.

<br>
<p align="center" width="100%">
<kbd><img src="images/01 Salary Distribution Histogram.png" width="700"  /></kbd>
</p>

<p align="center"><i><sub>Salary Distribution of Data-Related Jobs. UK. January 2022.</sub></i></p>
<br>
<br>
<p align="center" width="100%">
<kbd><img src="images/02 City Count.png" width="700"  /></kbd>
</p>

<p align="center"><i><sub>Top 10 Locations of Data-Related Jobs. UK. January 2022.</sub></i></p>
<br>

Summary of the data cleaning steps:
* Only a small number of the scraped results had salary information - only these were used for modeling.
* Not all of the salaries were yearly but hourly or weekly, and these were removed.
* Text and unicode characters were removed from the scraped salary information.
* Where a salary range was provided, the average was computed and substituted.
* The median salary was determined, and a new binary variable was created based on the median (below median = 'low' assigned 0, above median = 'high' assigned 1).

### Classification Models

I built three separate classification models in order to compare the results between models, and also to use my best performing model to investigate the data further to obtain additional insights. My best performing model obtained a mean cross-validated accuracy score around 68%, which is a significant improvement from the baseline accuracy.
The models evaluated include:
* Logistic Regression (0.68)
* Random Forest Classifier (0.67)
* Decision Tree Classifier (0.66)

### Model Evaluation

I was able to obtain the most important features that can allow the salary to be predicted, which included:
- job level = Senior, Graduate, Junior, and
- job position = Data Engineer, Data Scientist, and Data Analyst
- The location of the job was not a particularly useful predictor, although there did seem to be a small effect whether the job was based in London or not.

<br>
<p align="center" width="100%">
<kbd><img src="images/03 Feature Importance.png" width="300"  /></kbd>
</p>

<p align="center"><i><sub>Most Important Features Predicting Salary of Data-Related Jobs. UK. January 2022.</sub></i></p>
<br>

We were also required to tune our models so that we would have higher confidence in telling someone incorrectly that they would get a lower salary job over telling them incorrectly that they would get a high salary job. The tradeoff with this is that ‘peace-of-mind’ is gained at the expense of precision.

<br>
<p align="center" width="100%">
<kbd><img src="images/04 Confusion Matrix - original.png" width="400"  /></kbd>
</p>

<p align="center"><i><sub>Confusion Matrix (Train Data). Classification threshold of 0.5 used.</sub></i></p>
<br>
<br>
<p align="center" width="100%">
<kbd><img src="images/05 PR-AUROC Curvers - original.png" width="500"  /></kbd>
</p>

<p align="center"><i><sub>Precision-Recall and AUC-ROC curves for classification thresholds between 0 and 1. The dotted black line represents baseline performance.</sub></i></p>
<br>

`Precision = TP / (TP + FP)`

`Recall = TP / (TP + FN)`

The tradeoff with telling a client incorrectly that they would get a lower salary job over telling a client incorrectly that they would get a high salary job, is that the model recall (The ability of the classifier to correctly identify the current class) increases at the expense of the model precision (The ability of the classifier to avoid labeling a class as a member of another class).

If the number of FN values decreases (and the value of FP increases), model recall increases while model precision decreases.

<br>
<p align="center" width="100%">
<kbd><img src="images/06 Confusion Matrix - threshold.png" width="400"  /></kbd>
</p>

<p align="center"><i><sub>Confusion Matrix (Train Data). Classification threshold of 0.8 used.</sub></i></p>
<br>
<br>
<p align="center" width="100%">
<kbd><img src="images/07 PR-AUROC Curvers - threshold.png" width="500"  /></kbd>
</p>

<p align="center"><i><sub>Precision-Recall and AUC-ROC curves. Now we can see Class 1 is predicted at the expense of Class 0.</sub></i></p>
<br>

### Conclusion

Overall, the project was challenging but allowed me to work on my data science skills. There are two key things I would have done differently if I had the opportunity:
1.	I would take the job summary/description into account, using NLP to analyze different keywords and perhaps obtain additional features to predict salary,
2.	I should have paid more attention to the different cities and job titles my web-scraper included and filtered as there were too many unique cities and titles to provide meaningful insights to be obtained. 

Finally, and for those interested, as of January 2022 the median UK salary for data-related roles was slightly higher than £36,000 considering all factors affecting salary (location, experience, position etc.). The minimum advertised salary was £7,800 and the maximum was £121,800.
