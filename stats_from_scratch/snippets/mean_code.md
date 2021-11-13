<div style="text-align: justify">
<p>Now that we have a function to sum, we can divide the result by the number
of elements that went into the sum to obtain the mean. We transpose the vector
from a row to a column in the case that we computed the mean across the rows of
the matrix:</p>
</div>

{% highlight python %}

def mean(A, axis=0):
    # if we have a vector, we take the mean along it's length
    if min(la.size(A)) == 1:
        axis = la.size(A).index(max(la.size(A)))
    A_sum = sum(A, axis)
    A_mean = A_sum.div_elwise(la.size(A)[axis])
    if axis == 1:
        A_mean = A_mean.tr()
    return A_mean

{% endhighlight %}
