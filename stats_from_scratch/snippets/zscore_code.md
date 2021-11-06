<div style="text-align: justify">
<p>The Z-score is computed in two steps: zero centering the columns (or rows),
followed by dividing each value by the standard deviation of the column (or
row). For the division step, use the tile method to produce a matrix the same
size as the input, with the standard deviation of each column (or row) repeated
for each row (or column) and perform a element-wise division:</p>
</div>

{% highlight python %}

def zscore(A, axis=0, sample=False):
    A_zc = zero_center(A, axis)
    A_sd = sd(A_zc, axis, sample)
    if axis == 1:
        A_sd_rep = la.tile(A_sd, axes=[1, la.size(A)[1]])
    else:
        A_sd_rep = la.tile(A_sd, axes=[la.size(A)[0], 1])
    return A_zc.div_elwise(A_sd_rep)

{% endhighlight %}
