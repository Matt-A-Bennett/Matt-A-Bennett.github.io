<div style="text-align: justify">
<p>Here we return the number of rows, or columns, or both depending on the axis
argument:</p>
</div>

{% highlight python %}

def size(self, axis=2):
    if axis == 0:
        return len(self.data)
    elif axis == 1:
        return len(self.data[0])
    elif axis == 2:
        return [len(self.data), len(self.data[0])]

{% endhighlight %}
