<div style="text-align: justify">
<p>This method concatenates two matrices along a dimension.</p>
</div>

{% highlight python %}

def cat(A, B, axis=0):
    if axis == 0:
        concatenated = Mat(A.data + B.data)
    elif axis == 1:
        concatenated = Mat([rows[0]+rows[1] for rows in zip(A.data, B.data)])
    return concatenated

{% endhighlight %}
