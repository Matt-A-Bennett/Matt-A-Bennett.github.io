<div style="text-align: justify">
<p>We define two methods, the first gives both the general projection matrix
$P$ and the matrix 'for_x' that multiplies $b$ by the $P$ to give \(\hat x\).
The second projects the column(s) of a vector/matrix $B$ and projects them onto
$A$ to yield \(\hat x\):</p>
</div>

{% highlight python %}

def projection(self):
    # P = A((A'A)^-1)A'
    AtA_inv = (self.tr().multiply(self)).inverse()
    for_x = AtA_inv.multiply(self.tr())
    Projection = self.multiply(for_x)
    return Projection, for_x

def project_onto_A(self, A):
    _, for_x = A.projection()
    projected = for_x.multiply(self)
    return projected

{% endhighlight %}
