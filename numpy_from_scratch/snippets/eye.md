<div style="text-align: justify">
<p> A useful matrix to generate immediately is the identity matrix. We use the
previous function and populate the diagonal with 1's.</p>
</div>

{% highlight python %}

def eye(size):
    return gen_mat(size, values=[1], family='diag')

{% endhighlight %}


