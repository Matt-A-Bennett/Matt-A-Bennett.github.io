<div style="text-align: justify">
<p>We create a matrix, call the sum method twice with a different axis as an
argument and print the results:</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[1, 2, 3],
            [-2, 1, 4],
            [0, 1, 2],
            [3, 6, 1]])

result = la.stats.sum(A)
la.print_mat(result)

result = la.stats.sum(A, axis=1)
la.print_mat(result)

Outputs:

{% endhighlight %}

{% highlight console %}
>>> la.print_mat(result)
[2, 10, 10]

>>> la.print_mat(result)
[6, 3, 3, 10]

{% endhighlight %}
