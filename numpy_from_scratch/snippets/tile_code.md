<div style="text-align: justify">
<p>We can easily make a large matrix by 'tiling' a smaller matrix by a repeated
series of concatenations. We make a copy of the original matrix, and in two
loops concatenate it to the appropriate axis (starting by adding more columns,
and then replicating this 'row of matrices' downwards. (The two loops are
identical apart from the axis being specified, and so it's tempting to delete
one of them and then loop over the remaining one two times. While this saves 2
lines of code and avoids replicating the loop, it's just a little harder to
grasp what's going on. So we go for clarity/readability over brevity):</p>
</div>

{% highlight python %}

def tile(self, axes=[1,1]):
    B = dc(self)
    for j in range(axes[1]-1):
        self = cat(self, B, axis=1)
    B = dc(self)
    for i in range(axes[0]-1):
        self = cat(self, B, axis=0)
    return self

{% endhighlight %}
