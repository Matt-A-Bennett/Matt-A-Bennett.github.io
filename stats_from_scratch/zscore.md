# Z-score
<div style="text-align: justify">
<p>Z-scores are a way of transforming a set of observations such that each
represents the number of standard deviations above or below the mean. This is
useful since it allows you to compare sets of observations measured on
different scales - when fitting models, using standardised scores can aid the
interpretation of how much different variables are contributing to the
model.</p>
</div>

## Code implementation
<div style="text-align: justify">
<p>The Z-score is computed in two steps: zero centering the columns (or rows),
followed by dividing each value by the standard deviation of the column (or
row). For the division step, use the tile method to produce a matrix the same
size as the input, with the standard deviation of each column (or row) repeated
for each row (or column) and perform a element-wise division:</p>
</div>

{% highlight python %}

def zscore(A, axis=0, sample=False):
    A_zc = zero_center(A, axis)
    A_sd = sd(A_zc, axis, sample)
    if axis == 1:
        A_sd_rep = la.tile(A_sd, axes=[1, la.size(A)[1]])
    else:
        A_sd_rep = la.tile(A_sd, axes=[la.size(A)[0], 1])
    return A_zc.div_elwise(A_sd_rep)

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create a matrix, call the zscore method and print the result:</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[1, 2, 3],
            [2, 1, 4],
            [3, 0, 4],
            [4, 2, 2]])

la.print_mat(la.stats.zscore(A, axis=0), 3)

la.print_mat(la.stats.zscore(A, axis=1), 3)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.stats.zscore(A, axis=0), 3)
[-1.342, 0.905, -0.302]
[-0.447, -0.302, 0.905]
[0.447, -1.508, 0.905]
[1.342, 0.905, -1.508]

>>> la.print_mat(la.stats.zscore(A, axis=1), 3)
[-1.225, 0.0, 1.225]
[-0.267, -1.069, 1.336]
[0.392, -1.373, 0.981]
[1.414, -0.707, -0.707]

{% endhighlight %}

<div style="text-align: left">
<a href="https://matt-a-bennett.github.io/stats_from_scratch/var_covar_stddev_stderr.html">< Variance, covariance, standard deviation and standard error</a>
</div>

<div style="text-align: right">
<a href="https://matt-a-bennett.github.io/stats_from_scratch/correlation.html">Pearson correlation ></a>
</div>

[back to project main page](./stats_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/stats_from_scratch/Z-score.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

