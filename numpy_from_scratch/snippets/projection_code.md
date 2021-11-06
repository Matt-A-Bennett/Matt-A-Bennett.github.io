<div style="text-align: justify">
<p>We define two methods, one that gives both the general projection matrix $P$
and the matrix that multiplies $b$ to give \(\hat x\):</p>
</div>

{% highlight python %}

def projection(self):
    # P = A((A'A)^-1)A'
    AtA_inv = (self.transpose().multiply(self)).inverse()
    for_x = AtA_inv.multiply(self.transpose())
    Projection = self.multiply(for_x)
    return Projection, for_x

{% endhighlight %}
