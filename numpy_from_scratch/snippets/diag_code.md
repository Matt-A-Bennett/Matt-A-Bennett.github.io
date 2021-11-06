<div style="text-align: justify">
<p>This function works along the diagonal of the matrix, starting in the top
left and stopping after running out of rows or columns.</p>
</div>

{% highlight python %}

def diag(self):
    diag_vals = []
    for idx in range(min(self.size())):
        diag_vals.append(self.ind(idx,idx))
    return diag_vals

{% endhighlight %}
