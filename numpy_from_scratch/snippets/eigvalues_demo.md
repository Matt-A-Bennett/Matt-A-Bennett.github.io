<div style="text-align: justify">
<p>We create a matrix, call the eigvalues method and print the result:</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 2, 3],
            [2, 4, 4],
            [3, 4, 5]])

evals = A.eigvalues()

la.print_mat(evals,2)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(evals, 2)
[-0.61, 9.95, 0.65]

{% endhighlight %}
