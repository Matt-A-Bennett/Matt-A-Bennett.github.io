<div style="text-align: justify">
<p>Here we call the function_choice method with a list of two lambda functions.
In the case that B was not a matrix, we assume that the user wants to
add/subtract the same scaler to each element. This is a simple function of each
element and is reflected in the first lambda function in the list. On the other
hand, if the B argument was a matrix, the second lambda function of two
variables (x and y: the $i,j$ elements from the original matrix and matrix B)
will be applied:</p>
</div>

{% highlight python %}

def add(self, B):
    return self.function_choice(B, [lambda x: x+B, lambda x, y: x+y])

def subtract(self, B):
    return self.function_choice(B, [lambda x: x-B, lambda x, y: x-y])

{% endhighlight %}
