<div style="text-align: justify">
<p>The matrix is singular if during elimination row exchanges can't avoid a
zero in a pivot position. Our elimination method already returns a variable
indicating singularity, and so this next method just provides a cleaner way of
accessing that variable:</p>
</div>

{% highlight python %}

def is_singular(self):
    _, _, _, _, singular, _ = self.elimination()
    return singular

{% endhighlight %}
