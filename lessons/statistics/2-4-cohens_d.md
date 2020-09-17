[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

Our problem:

> *Using the variable totalwgt_lb, investigate whether first babies are lighter or heavier than others. Compute Cohen’s* d *to quantify the difference between the groups. How does it compare to the difference in pregnancy length?*

```python
firsts.totalwgt_lb.mean(), others.totalwgt_lb.mean()
> 7.201094430437772 7.325855614973262
```

We see that first babies are generally lighter than others. Compute Cohen's *d*:

```python
CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)
> -0.08867292707260174
```

The effect size, indicating the difference in means between first and other pregnanices, is about -0.0887 standard deviations. The negative indicating a generally lower weight for first pregnancies. We see this effect is larger in magnitude than the effect size for pregnancy length, \~0.0289.

A Jupyter Notebook containing my work can be found at <https://github.com/zhouandrewc/ThinkStats2>.


