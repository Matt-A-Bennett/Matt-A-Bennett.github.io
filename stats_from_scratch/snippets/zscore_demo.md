<div style="text-align: justify">
<p>We create a matrix, call the zscore method and print the result:</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[1, 2, 3],
            [2, 1, 4],
            [3, 0, 4],
            [4, 2, 2]])

la.print_mat(la.stats.zscore(A, axis=0), 3)

la.print_mat(la.stats.zscore(A, axis=1), 3)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.stats.zscore(A, axis=0), 3)
[-1.342, 0.905, -0.302]
[-0.447, -0.302, 0.905]
[0.447, -1.508, 0.905]
[1.342, 0.905, -1.508]

>>> la.print_mat(la.stats.zscore(A, axis=1), 3)
[-1.225, 0.0, 1.225]
[-0.267, -1.069, 1.336]
[0.392, -1.373, 0.981]
[1.414, -0.707, -0.707]

{% endhighlight %}
