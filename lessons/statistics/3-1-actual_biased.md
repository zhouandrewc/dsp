[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

Our problem:

> Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.
Use the NSFG respondent variable NUMKDHH to construct the actual distribution for the number of children under 18 in the household.

> Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.

> Plot the actual and biased distributions, and compute their means. 

We compute and plot the two distributions:

```python
children_actual = thinkstats2.Pmf(resp.numkdhh, "actual")
children_biased = BiasPmf(children_actual, "observed")

thinkplot.PrePlot(2)
thinkplot.Pmfs([children_actual, children_biased])
thinkplot.Config(xlabel='Number of children', ylabel='PMF')
```

![image info](./img/chap03-img1.png)

We can see that the biased distribution is more top-heavy than the actual distribution, since larger families are weighted more heavily.

We calculate the means, and see as expected that the biased distribution has a larger mean.

```python
children_actual.Mean(), children_biased.Mean()
> (1.024205155043831, 2.403679100664282)
```