<div style="text-align: justify">
<p>We make both vectors row vectors and then carry out the multiplication and
sum operations.</p>
</div>

{% highlight python %}

def dot(self, new_mat):
    A = dc(self)
    B = dc(new_mat)
    # make both vectors rows with transpose
    if size(A)[0] != 1:
        A = A.transpose()
    if size(B)[0] != 1:
        B = B.transpose()
    # compute dot product
    dot_prod = []
    for cols in zip(A.data[0], B.data[0]):
        dot_prod.append(cols[0]*cols[1])
    dot_prod = sum(dot_prod)
    return dot_prod

{% endhighlight %}
