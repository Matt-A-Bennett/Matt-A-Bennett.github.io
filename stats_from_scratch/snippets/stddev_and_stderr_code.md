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
