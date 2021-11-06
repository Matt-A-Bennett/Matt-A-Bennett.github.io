<div style="text-align: justify">
<p>We make both vectors row vectors and then carry out the multiplication and
sum operations.</p>
</div>

{% highlight python %}

def dot(self, new_mat):
    # make both vectors rows with transpose
    if self.size(0) != 1:
        self = self.transpose()
    if new_mat.size(0) != 1:
        new_mat = new_mat.transpose()
    dot_prod = []
    for cols in zip(self.data[0], new_mat.data[0]):
        dot_prod.append(cols[0]*cols[1])
    dot_prod = sum(dot_prod)
    return dot_prod

{% endhighlight %}
