<div style="text-align: justify">
<p>The second method gives the parameters for an nth degree polynomial curve
through a set of data points in $b$. To do so, we create a matrix $A$ with as
many rows as $b$ and one column per term of the polynomial - the 1st column is
all ones, and is the basis for the intercept ($x^0 = 1$); The second
incrementally increases and forms the basis for the slope ($x^1 = x$); The
third column is for the squared terms ($x^2 = x^2$) and so on:</p>
</div>

{% highlight python %}

def polyfit(self, order=1):
    # create a model
    A = gen_mat([size(b)[0], 1])
    for i in range(size(b)[0]):
        orders = []
        for exponent in range(order+1):
            orders.append(i**exponent)
        A.data[i] = orders
    # fit model to b
    _, for_x = A.projection()
    fit = for_x.multiply(b)
    return fit

{% endhighlight %}

<div style="text-align: justify">
<p>Then we define a method to fit a straight line. This is the default of the
polyfit method, but fitting a straight line is so common that it's nice to have
a more descriptive method to call:</p>
</div>
{% highlight python %}

def linfit(self):
    return self.polyfit()

{% endhighlight %}
