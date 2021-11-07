<div style="text-align: justified">
<p>In case we end up with a 1x1 matrix, we probably want to use it as a scalar
(that's all a 1x1 matrix is...) and so we make a method that indexes the
element for us (since the intent is more understandable than indexing
directly):</p>
</div>

{% highlight python %}

def make_scalar(self):
    if max(self.size()) == 1:
        return self.ind(0,0)

{% endhighlight %}
