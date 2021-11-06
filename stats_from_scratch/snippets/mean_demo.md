<div style="text-align: justify">
<p>We create a matrix, call the mean method twice with a different axis as an
argument and print the results (we only print 2 decimal places in one case to
make it look pretty):</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[1, 2, 3],
            [-2, 1, 4],
            [0, 1, 2],
            [3, 6, 1]])

la.print_mat(la.stats.mean(A))

la.print_mat(la.stats.mean(A, axis=1), 2)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.stats.mean(A))
[0.5, 2.5, 2.5]

>>> la.print_mat(la.stats.mean(A, axis=1), 2)
[2.0]
[1.0]
[1.0]
[3.33]

{% endhighlight %}
