<div style="text-align: justify">
<p>The determinant of a matrix is simply the product of the pivots, with a
negative sign if there were an odd number of row exchanges. Here we don't use
the pivot method we wrote, as we also need the number of row exchanges:</p>
</div>

{% highlight python %}

def determinant(self):
    # find U
    _, _, _, U, _, row_exchange_count = self.elimination()
    # muliply the pivots
    det = 1
    diag_vals = U.diag()
    for val in diag_vals:
        det *= val
    # if an odd number of row exchanges, multiply determinant by minus one
    if row_exchange_count % 2:
        det *= -1
    return det

{% endhighlight %}
