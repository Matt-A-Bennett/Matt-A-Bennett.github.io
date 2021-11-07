<div style="text-align: justify">
<p>We create a matrix and tile it:</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 2],
            [0, 5],
            [0, 0]])

la.print_mat(la.tile(A, [2, 5]))

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.tile(A, [2, 5]))
[1, 2, 1, 2, 1, 2, 1, 2, 1, 2]
[0, 5, 0, 5, 0, 5, 0, 5, 0, 5]
[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
[1, 2, 1, 2, 1, 2, 1, 2, 1, 2]
[0, 5, 0, 5, 0, 5, 0, 5, 0, 5]
[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

{% endhighlight %}
