<div style="text-align: justify">
<p>Now that we have the method of elimination, we can get a lot of information
about a matrix easily. The pivots of a matrix are the first non-zero numbers
sitting in each row of U after elimination. Here we return those pivots along
with the columns in which they were found:</p>
</div>

{% highlight python %}

def pivots(self):
    _, _, _, U, _, _ = self.elimination()
    # extract the first non-zero from each row - track the column number
    U = U.transpose()
    pivots = {}
    found = []
    for j, col in enumerate(U.data):
        piv_pos = sum(list(map(bool, col)))
        if piv_pos not in found:
            found.append(piv_pos)
            pivots[j] = col[piv_pos-1]
    return pivots

{% endhighlight %}
