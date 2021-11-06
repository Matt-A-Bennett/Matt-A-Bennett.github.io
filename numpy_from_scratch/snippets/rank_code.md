<div style="text-align: justify">
<p>The rank of a matrix tells us a huge amount, and is simply the number of
pivots:</p>
</div>

{% highlight python %}

def rank(self):
    return len(self.pivots())

{% endhighlight %}
