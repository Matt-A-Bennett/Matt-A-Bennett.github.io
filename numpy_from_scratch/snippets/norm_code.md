{% highlight python %}

def norm(self):
    if self.length() != 0:
        self = self.div_elwise(self.length())
    return self

{% endhighlight %}
