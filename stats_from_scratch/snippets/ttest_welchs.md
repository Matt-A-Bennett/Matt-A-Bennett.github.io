<div style="text-align: justify">
<p>The unpaired <i>t</i> test above pooled the variances, taking into account
the unequal sample sizes but assuming that the magnitude of the variation did
not differ between the two samples. If the variance <i>does</i> differ, we
can't pool them. A method for dealing with this situation is Welch's unpaired
<i>t</i> test. The method is robust and gives very similar results to the
pooling method above when variances are equal. For this reason, many
statistical software packages default to this method whenever doing unpaired
<i>t</i> tests.</p>

<p>Conceptually simple, Welch's <i>t</i> is calculated by dividing the mean
difference between the two samples by the square root of the sum of the squared
standard errors:</p>
</div>

$$
t = \frac{\bar u - \bar v}{\sqrt{SE_u^2 + SE_v^2}}
$$

<div style="text-align: justify">
<p>To calculate the degrees of freedom, we can use the Welch–Satterthwaite
equation:</p>
</div>

$$
df = \frac{\Big(\frac{\sigma_u^2}{n_u} + \frac{\sigma_v^2}{n_v}\Big)^2}{\frac{\sigma_u^4}{n_u^2(n_u-1)}\frac{\sigma_v^4}{n_v^2(n_v-1)}}
$$

