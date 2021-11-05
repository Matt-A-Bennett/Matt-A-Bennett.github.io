<div style="text-align: justify">
<p>We create two matrices, call the multiply method and print the result:</p>
</div>

{% highlight python %}

A = la.Mat([[1, 1, 3],
         [2, 5, 4]])

B = la.Mat([[1, 1],
         [1, 3],
         [-1, 3]])

C = A.multiply(B)

la.print_mat(C)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(C)
[-1, 13]
[3, 29]

{% endhighlight %}
