<div style="text-align: justify">
<p>We create a matrix, call the methods and print the results (notice when we
use the population covariance by setting the sample argument to 'False' the
values are a bit smaller):</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[1, 2, 3],
            [0, -1, 6],
            [4, 0, 2],
            [2, 5, 1]])

la.print_mat(la.stats.covar(A), 2)

la.print_mat(la.stats.covar(A, sample=False), 2)

la.print_mat(la.stats.sd(A), 2)

la.print_mat(la.stats.se(A), 2)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.stats.covar(A), 2)
[2.92, 0.5, -2.67]
[0.5, 7.0, -4.33]
[-2.67, -4.33, 4.67]

>>> la.print_mat(la.stats.covar(A, sample=False), 2)
[2.19, 0.38, -2.0]
[0.38, 5.25, -3.25]
[-2.0, -3.25, 3.5]

>>> la.print_mat(la.stats.sd(A), 2)
[1.71, 2.65, 2.16]

>>> la.print_mat(la.stats.se(A), 2)
[0.85, 1.32, 1.08]

{% endhighlight %}
