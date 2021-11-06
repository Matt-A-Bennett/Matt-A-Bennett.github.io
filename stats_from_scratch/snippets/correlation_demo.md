<div style="text-align: justify">
<p>We create a matrix, call the corr method and print the result:</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[1, 2, 3],
            [2, 3, 1],
            [3, 3, 0],
            [4, 5, 1],
            [5, 6, -1]])

la.print_mat(la.stats.corr(A), 2)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.stats.corr(A), 2)
[1.0, 0.96, -0.85]
[0.96, 1.0, -0.74]
[-0.85, -0.74, 1.0]

{% endhighlight %}
