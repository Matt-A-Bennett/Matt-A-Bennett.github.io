<div style="text-align: justify">
<p>If the matrix qualifies as both lower and upper, then it must be diagonal.
Therefore we use the previous two methods like so:</p>
</div>

{% highlight python %}

def is_diag(self):
    if self.is_lower_tri() and self.is_upper_tri():
        return True
    else:
        return False

{% endhighlight %}
