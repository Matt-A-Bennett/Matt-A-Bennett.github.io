<div style="text-align: justify">
<p>Here we define a method that performs a one sample <i>t</i> test on the
samples in each column (or row) of a matrix. We compute the mean and standard
error of each column (or row) and perform an element wise division. The vector
of <i>t</i> values is returned along with the degrees of freedom:</p>
</div>

{% highlight python %}

def ttest_one_sample(A, axis=0, H=0):
    A_diff = mean(A, axis).subtract(H)
    A_se = se(A, axis, sample=True)
    ts = A_diff.div_elwise(A_se)
    df = A.size(axis)-1
    return ts, df

{% endhighlight %}
