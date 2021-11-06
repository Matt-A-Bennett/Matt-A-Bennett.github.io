<div style="text-align: justify">
<p>We compute the covariance matrix, take the variance values from the diagonal
and take the reciprocal of the square root and store them on a diagonal matrix
K. Then we do the multiplications before returning the correlation matrix:</p>
</div>

{% highlight python %}

def corr(A, axis=0):
    V = covar(A, axis)
    sds=[1/sqrt(x) for x in V.diag()]
    K_sqrt = la.gen_mat([len(sds)]*2, values=sds, type='diag')
    correlations = K_sqrt.multiply(K).multiply(K_sqrt)
    return correlations

{% endhighlight %}
