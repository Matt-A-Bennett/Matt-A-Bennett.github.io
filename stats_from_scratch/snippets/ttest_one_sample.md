<div style="text-align: justify">
<p>A common task is to check if the value of a population parameter as
estimated from a random sample of that population differs meaningfully from
zero (or some other number). We can form the null hypothesis that any deviation
of our estimate from zero is the result of measurement error - and then see if
that deviation is large enough to reject the null hypothesis. To do this, we
could assume that such measurement errors are normally distributed around zero
(this is often the case for samples greater that ~30, thanks to the central
limit theorem). Then we could calculate the number of standard deviations our
estimate is away from zero - rejecting the null hypothesis at some critical
value (often set at about 2). This would be a <i>z</z> test.</p>

<p>However, it's uncommon to <i>know</i> the population standard deviation of
the estimate in advance, and so it must be estimated from the sample (this is
the standard error):</p>
</div>

$$
t = \frac{\bar x - \mu_0}{SE}
$$

<div style="text-align: justify">
<p>In addition, if the sample is smaller than we'd like (say 10-20) then a
<i>z</i> the distribution of the measurement errors are likely not well
approximated by a normal distribution. Instead, the measurement errors would
have more extreme values - that is, the distribution would have heavier tails -
and better approximated by the Student's <i>t</i> distribution. This aspect of
the shape of the t-distribution varies with the sample size (becoming closer to
the normal distribution as the sample size increases) and thus so does the
critical value of <i>t</i> that we would require to reject the null
hypothesis.</p>
</div>

