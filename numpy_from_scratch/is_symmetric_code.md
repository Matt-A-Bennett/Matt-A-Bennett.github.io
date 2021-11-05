<div style="text-align: justify">
<p>We loop over two ranges - one being the number of rows/columns, and the
other being one less than that (since we don't need to check diagonal entries).
If we find any $a_{ij} \neq a_{ji}$, we return False, otherwise we return
True:</p>
</div>

{% highlight python %}

def is_symmetric(self):
    for i in range(size(self)[0]):
        for j in range(i+1, size(self)[0]):
            if self.data[i][j] != self.data[j][i]:
                return False
    else:
        return True

{% endhighlight %}
