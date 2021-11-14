<div style="text-align: justify">
<p>In the case that we have a two samples of observations where each
observation in one sample is 'paired' with an observation in the other sample
(e.g. if a set of measurements is repeated at two times), then we can compute
these paired differences and run same test as above:</p>
</div>

{% highlight python %}

def ttest_paired(u, v):
    A_diff = u.subtract(v)
    return ttest_one_sample(A_diff)

{% endhighlight %}
