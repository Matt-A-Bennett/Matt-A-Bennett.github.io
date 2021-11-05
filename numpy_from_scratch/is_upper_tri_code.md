<div style="text-align: justify">
<p>Here we simply call the is_lower_tri method on the transposed matrix:</p>
</div>

{% highlight python %}

def is_upper_tri(self):
    return self.transpose().is_lower_tri()

{% endhighlight %}
