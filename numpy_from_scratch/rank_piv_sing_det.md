# Rank, pivots, singularity, determinant
<div style="text-align: justify">
<p>Now that we have the method of elimination, we can get a lot of information
about a matrix easily. The pivots of a matrix are the non-zero numbers sitting
along the diagonal of U after elimination. Here we return those pivots along
with the columns in which they were found:</p>
</div>

{% highlight python %}

def pivots(self):
    # find U
    _, _, U, _, _ = self.elimination()
    # extract the non-zeros on the diagonal
    diag_vals = U.diag()
    pivot_info = [(i, val) for i, val in enumerate(diag_vals) if val]
    return pivot_info

{% endhighlight %}

<div style="text-align: justify">
<p>The rank of a matrix tells us a huge amount, and is simply the number of
pivots:</p>
</div>

{% highlight python %}

def rank(self):
    pivot_info = self.pivots()
    return len(pivot_info)

{% endhighlight %}

<div style="text-align: justify">
<p>The matrix is singular if during elimination row exchanges can't avoid a
zero in a pivot position. Our elimination method already returns a variable
indicating singularity, and so this next method just provides a cleaner way of
accessing that variable:</p>
</div>

{% highlight python %}

def is_singular(self):
    _, _, _, singular, _ = self.elimination()
    return singular

{% endhighlight %}

<div style="text-align: justify">
<p>The determinant of a matrix is simply the product of the pivots, with a
negative sign if there were an odd number of row exchanges. Here we don't use
the pivot method we wrote, as we also need the number of row exchanges:</p>
</div>

{% highlight python %}

def determinant(self):
    # find U
    _, _, U, _, row_exchange_count = self.elimination()
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

[< EA = U](./elimination.md)\
[Inverse >](./inverse.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
