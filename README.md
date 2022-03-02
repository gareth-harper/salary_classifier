# Classifying Salaries of Data-Related Jobs

### Introduction

One of my projects for the General Assembly Data Science Immersive course was to scrape job listings from a job aggregation website and apply machine learning algorithms to predict salaries for Data Science related roles in the United Kingdom.
This project was completed in Jnuary 2022.

### Goals

The goals of the project are summarized as follows:
1. Determine the factors that are most important in predicting salary for the roles chosen.
2. Scrape your own data from a job aggregation tool in order to obtain necessary data.
3. To predict salary the most appropriate approach would be a regression model. Here, instead, we just want to estimate which factors lead to high or low salary and work with a classification model.

As we only have two classes (whether the salary is 'low' or 'high'), the baseline model accuracy is 50% (Guessing whether the salary is in either category without any modeling would ensure you are correct half the time, on average).

### Scraping the Data

Job aggregation website Indeed.com was scraped using BeautifulSoup as the website is a simple text page where you can easily find relevant entries. It was possible to identify a number of key tags for information which might be helpful to scrape such as job location, company name, job title, and salary.

I limited my search to job postings in the UK only, including cities across England, Scotland, Wales and Northern Ireland.

### Data Cleaning and EDA

Once the data was collected, it was cleaned using various techniques learned throughout the course. Although I was initially able to scrape nearly 60,000 data points, after cleaning I was left with just more than 1,300. This was largely due to many duplicated data points, and entries with missing or irrelevant information among other factors. The number of useable data points was deemed sufficient to build predictive models to complete the project.
