# Variance, covariance, standard deviation and standard error
<div style="text-align: justify">
<p>The study of statistics and data is the study of variation. The general
situation is that we are interested in estimating a parameter of a population
based on a sample drawn from that population.</p>

<p>Here we introduce some of the key basic measures.</p>
</div>

## Variance and covariance

<div style="text-align: justify">
<p>The variance of a set of values $x$ is the sum of the squared deviation of
each value from the mean of all the values $\bar x$, divided by one less than
the number of observations (this gives the 'sample variance', whereas omitting
the $-1$ would instead give the 'population variance'. When $n$ is large, it
doesn't particularly matter). In essence it's the average squared deviation
from the mean in the data:</p>
</div>

$$ \sigma^2 = \frac{1}{n-1}\sum_{i=1}^n (x_i - \bar x)(x_i - \bar x) $$

<div style="text-align: justify">
<p>In matrix notation:</p>
</div>

$$ \text{covariance} = \frac{1}{m-1}(x - \bar x)^T (x - \bar x)$$

<div style="text-align: justify">
<p>We can compare the variation between two different variables and see if they
'covary' or not. This is called the covariance and is computed just like the
variance, only it's between two sets of observations $x$ and $y$. In essence
this is the average 'agreement' in the deviations from each variable's
mean:</p>
</div>

$$ \text{covariance} = \frac{1}{n-1}\sum_{i=1}^n (x_i - \bar x)(y_i - \bar y) $$

<div style="text-align: justify">
<p>In matrix notation:</p>
</div>

$$ \text{covariance} = \frac{1}{m-1}(x - \bar x)^T (y - \bar x) $$

<div style="text-align: justify">
<p>If we have observations of several variables, with each set of observations
forming a column of a matrix $A$, then computing all of the dot products
between each column is just what happens with $A^T A$. So if we use the
centering matrix to remove the mean of each set of observations with</p>
</div>

$$ (CA)^T C A = A^T C^T C A = A^T C A $$

<div style="text-align: justify">
<p>(since C is symmetric and idempotent) and
divide this by one less than the number of observations we get the 'covariance
matrix':</p>
</div>

$$ \text{covariance matrix} = \frac{1}{m-1} A^T CA $$ 

$$
\frac{1}{3}
  \begin{bmatrix}
    1 & 0 & 4 & 2 \\
    2 & -1 & 0 & 5 \\
    3  & 6 & 2  & 1
  \end{bmatrix}
  %
  \frac{1}{4}
  \begin{bmatrix}
    3, -1, -1, -1 \\
    -1, 3, -1, -1 \\
    -1, -1, 3, -1 \\
    -1, -1, -1, 3
  \end{bmatrix}
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & -1 & 6 \\
    4 & 0 & 2 \\
    2 & 5 & 1
  \end{bmatrix}
  =%
$$

$$
  \frac{1}{3}
  \begin{bmatrix}
    8.75 & 1.5 & -8 \\
    1.5 & 21 & -13 \\
    -8 & -13 & 14
  \end{bmatrix}
  =%
  \begin{bmatrix}
    2.1875 & 0.375 & -2 \\
    0.375 & 5.25 & -3.25 \\
    -2 & -3.25 & 3.5
  \end{bmatrix}
$$

<div style="text-align: justify">
<p>Note the variance $\sigma^2$ of each column sitting along the diagonal.</p>
</div>

## Code implementation
<div style="text-align: justify">
<p>We define a method that by default computes the covariance among the columns
of an input matrix A, yielding the sample covariance (i.e. using the $n-1$
correction).</p>

<p>First we transpose the matrix if the user wants to take rows as variables.
Then we zero center the matrix, perform the $A^T A$ step and normalise by the
number of observations (subtracting 1 by default, unless sample is False):</p>
</div>

{% highlight python %}

def covar(A, axis=0, sample=True):
    if axis == 1:
        A = A.transpose()
    A_zc = zero_center(A)
    A_cov = A_zc.transpose().multiply(A_zc)
    N = la.size(A)[0]
    if sample:
        N -= 1
    A_cov = A_cov.div_elwise(N)
    return A_cov

{% endhighlight %}

<div style="text-align: justify">
<p>A method for the variances of the columns of a matrix, rather than the full
covariance matrix, is achieved by extracting the values from the diagonal of
the covariance matrix. We transpose the vector from a row to a column in the
case that we computed the variance across the rows of the matrix:</p>
</div>

{% highlight python %}

def var(A, axis=0, sample=True):
    A_covar = covar(A, axis, sample)
    A_var = la.Mat([A_covar.diag()])
    if axis == 1:
        return A_var.transpose()
    return A_var

{% endhighlight %}

## Standard deviation and standard error
<div style="text-align: justify">
<p>While the variance of, and covariance between, a set of variables is useful,
they are squared values and as such not on the same scale as the measured data.
Therefore a useful measure when reasoning about the data is the square root of
the variance. This is called the standard deviation:</p>
</div>

$$ \sigma = \sqrt{\sigma^2} $$

<div style="text-align: justify">
<p>If we divide the standard deviation by the square root of the number of
observations, we have the standard error of the mean. This indicates the
uncertainty around the sample mean as an estimate of the population mean (since
the sample mean will not match the population mean exactly). The $\sqrt{n}$
term is like a 'penalty' incurred for making the 'leap' of inference to the
population and this penalty decreases as your sample size increases:</p>
</div>

$$ SE = \frac{\sigma}{\sqrt{n}} $$

## Code implementation
<div style="text-align: justify">
<p>It is simple to convert from the variance to the standard deviation and from
the standard deviation to the standard error:</p>
</div>

{% highlight python %}

def sd(A, axis=0, sample=True):
    A_var = var(A, axis, sample)
    stddevs = A_var.function_elwise(sqrt)
    return stddevs

def se(A, axis=0, sample=True):
    stddevs = stddev(A, axis, sample)
    N = la.size(A)[axis]
    stderrs = stddevs.div_elwise(sqrt(N))
    return stderrs

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create a matrix, call the methods and print the results (notice when we
use the population covariance by setting the sample argument to 'False' the
values are a bit smaller):</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[1, 2, 3],
            [0, -1, 6],
            [4, 0, 2],
            [2, 5, 1]])

la.print_mat(la.stats.covar(A), 2)

la.print_mat(la.stats.covar(A, sample=False), 2)

la.print_mat(la.stats.sd(A), 2)

la.print_mat(la.stats.se(A), 2)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.stats.covar(A), 2)
[2.92, 0.5, -2.67]
[0.5, 7.0, -4.33]
[-2.67, -4.33, 4.67]

>>> la.print_mat(la.stats.covar(A, sample=False), 2)
[2.19, 0.38, -2.0]
[0.38, 5.25, -3.25]
[-2.0, -3.25, 3.5]

>>> la.print_mat(la.stats.sd(A), 2)
[1.71, 2.65, 2.16]

>>> la.print_mat(la.stats.se(A), 2)
[0.85, 1.32, 1.08]
{% endhighlight %}



[< Zero center](./zero_center.md)

<div style="text-align: right">
<a href="https://matt-a-bennett.github.io/stats_from_scratch/zscore.html">Z-score ></a>
</div>

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

