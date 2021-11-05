<div style="text-align: justify">
<p>Just as with the case in the add and subtract methods, we check if the B
argument is of class matrix and decide whether to use a function of one or of
two variables:</p>
</div>

{% highlight python %}

def multiply_elwise(self, B):
    return self.function_choice(B, [lambda x: x*B, lambda x, y: x*y])

def div_elwise(self, B):
    return self.function_choice(B, [lambda x: x/B, lambda x, y: x/y])

{% endhighlight %}

