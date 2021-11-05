<div style="text-align: justify">
<p>This function works along the diagonal of the matrix, starting in the top
left and stopping after running out of rows or columns.</p>
</div>

{% highlight python %}

def diag(self):
    A = dc(self)
    diag_vals = []
    for i in range(min(size(A))):
        diag_vals.append(A.data[i][i])
    return diag_vals

{% endhighlight %}
