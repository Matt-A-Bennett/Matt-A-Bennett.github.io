<div style="text-align: justify">
<p>The Vandamonde matrix stores the components of an nth degree polynomial
curve. It has as many rows as points on the curve and one column per term of
the polynomial - the 1st column is all ones, and is the basis for the intercept
($x^0 = 1$); The second incrementally increases and forms the basis for the
slope ($x^1 = x$); The third column is for the squared terms ($x^2 = x^2$) and
so on. When a vector $b$ is [projected onto](../projection_and_regression.md)
the column space of this matrix, the resulting projection is the 'best fitting'
polynomial curve through the points $b$:</p>
</div>

{% highlight python %}

def vandermonde(n_rows, order=1):
    A = gen_mat([n_rows, 1])
    for i in range(n_rows):
        orders = []
        for exponent in range(order+1):
            orders.append(i**exponent)
        A.data[i] = orders
    return A

{% endhighlight %}
