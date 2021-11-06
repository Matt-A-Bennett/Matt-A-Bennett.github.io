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
