# Variance, covariance, standard deviation and standard error
<div style="text-align: justify">
<p>The study of statistics and data is the study of variation. The general
situation is that we are interested in estimating a parameter of a population
based on a sample drawn from that population. Therefore, we often distinguish
between e.g. the 'population standard deviation' and the 'sample standard
deviation'. The calculation values of these are often different. In calculating
the sample statistics, with the aim of producing an estimate of the population
parameter, there is the notion of a 'biased' and an 'unbiased' estimate.

Here we introduce some of the key basic measures.</p>
</div>

## Variance and covariance

<div style="text-align: justify">
<p>We can compare the variation between two different variables and see if they
covary or not. This is called the covariance and is measured by subtracting the
mean of each set of points and multiplying the leftover deviations:</p>
</div>

$$ \text{covariance} = \sum_{i=1}^n (x_i - \bar x)(y_i - \bar y)$$

<div style="text-align: justify">
<p>In matrix notation:</p>
</div>

$$ \text{covariance} = (x - \bar x) \cdot (y - \bar y)$$

<div style="text-align: justify">
<p>The population variance is a measure of the deviation of a set of points
from their mean. We measure that by first subtracting the mean of and then
squaring all the leftover deviations:</p>
</div>

$$ \text{variance} = \sum_{i=1}^n (x_i - \bar x)^2 $$

<div style="text-align: justify">
<p>In matrix notation:</p>
</div>

$$ \text{variance} = (x - \bar x) \cdot (x - \bar x) = \|(x - \bar x)\|^2 $$

<div style="text-align: justify">
<p>When we want an estimate the population variance from a sample drawn from
that population, we divide the sample variance by one less than the number of
data points:</p>
</div>

$$ \text{sample variance} = \frac{1}{N-1} \sum_{i=1}^n (x_i - \bar x)^2 $$

<div style="text-align: justify">
<p>In matrix notation:</p>
</div>

$$ \text{sample variance} = \frac{1}{N-1}(x - \bar x) \cdot (x - \bar x) 
= \frac{1}{N-1}\|(x - \bar x)\|^2 $$

{% highlight python %}

def covar(A):
    A = zero_center(A,0)
    A = A.transpose().multiply(A)
    return A

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create a matrix, call the <METHOD> method and print the result:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]])

A = Mat([[1, 2, 3],
        [4, 5, 6]])

A = Mat([[1, 2],
        [3, 4],
        [5, 6]])

<METHODED> = A.<METHOD>()

print_mat(<METHOD>)

{% endhighlight %}

Outputs:

{% highlight shell %}

{% endhighlight %}

[< Zero center and z-scoring](./zero_center_and_zscore.md)

[back to project main page](./stats_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/stats_from_scratch/var_covar_stddev_stderr.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

