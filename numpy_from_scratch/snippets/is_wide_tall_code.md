<div style="text-align: jusitifed">
<p>If the matrix is not square, then it must either have more columns than rows
(wide) or have more rows than columns (tall). We make a couple of methods to
test those cases too:</p>
</div>

{% highlight python %}

def is_wide(self):
    return self.size(0) < self.size(1)

def is_tall(self):
    return self.size(0) > self.size(1)

{% endhighlight %}
