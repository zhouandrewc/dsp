[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

> The distribution of income is famously skewed to the right. In this exercise, we’ll measure how strong that skew is.

> The Current Population Survey (CPS) is a joint effort of the Bureau of Labor Statistics and the Census Bureau to study income and related variables. Data collected in 2013 is available from http://www.census.gov/hhes/www/cpstables/032013/hhinc/toc.htm. I downloaded hinc06.xls, which is an Excel spreadsheet with information about household income, and converted it to hinc06.csv, a CSV file you will find in the repository for this book. You will also find hinc2.py, which reads this file and transforms the data.

> The dataset is in the form of a series of income ranges and the number of respondents who fell in each range. The lowest range includes respondents who reported annual household income “Under $5000.” The highest range includes respondents who made “$250,000 or more.”

> To estimate mean and other statistics from these data, we have to make some assumptions about the lower and upper bounds, and how the values are distributed in each range. hinc2.py provides InterpolateSample, which shows one way to model this data. It takes a DataFrame with a column, income, that contains the upper bound of each range, and freq, which contains the number of respondents in each frame.

> It also takes log_upper, which is an assumed upper bound on the highest range, expressed in log10 dollars. The default value, log_upper=6.0 represents the assumption that the largest income among the respondents is 106, or one million dollars.

> InterpolateSample generates a pseudo-sample; that is, a sample of household incomes that yields the same number of respondents in each range as the actual data. It assumes that incomes in each range are equally spaced on a log10 scale.

> Compute the median, mean, skewness and Pearson’s skewness of the resulting sample. What fraction of households reports a taxable income below the mean? How do the results depend on the assumed upper bound?


```python
log_sample = InterpolateSample(income_df, log_upper=6.0)
sample = np.power(10, log_sample)
np.median(sample), np.mean(sample), Skewness(sample), sum(sample < np.mean(sample))/sample.size
> (51226.93306562372, 74278.7075311872, 4.949920244429583, 0.660005879566872)
```

```python
log_sample = InterpolateSample(income_df, log_upper=7.0)
sample = np.power(10, log_sample)
np.median(sample), np.mean(sample), Skewness(sample), sum(sample < np.mean(sample))/sample.size
> (51226.93306562372, 124267.39722164697, 11.603690267537793, 0.8565630665207663)
```


```python
log_sample = InterpolateSample(income_df, log_upper=8.0)
sample = np.power(10, log_sample)
np.median(sample), np.mean(sample), Skewness(sample), sum(sample < np.mean(sample))/sample.size
>> (51226.93306562372, 457453.4872473685, 14.892459804414136, 0.9786294076336377)
```

We see that as the assumed upper bound increases from $1 million to $10 million to $100 million, the median stays the same, while the mean, skewness, and percentage of households below the mean increase, reflecting very different results depending on our assumption of the maxmimum income. We see here the limitations of a dataset that doesn't specify the precise amount of money made by the topmost tier, as our results will vary significantly depending on that assumption.
