<div style="text-align: justify">
<p>We generate a vandermonde matrix with terms up to cubic and print the
result:</p>
</div>

{% highlight python %}

V = la.vandermonde(5, order=3)

la.print_mat(V)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(V)
[1, 0, 0, 0]
[1, 1, 1, 1]
[1, 2, 4, 8]
[1, 3, 9, 27]
[1, 4, 16, 64]

{% endhighlight %}
