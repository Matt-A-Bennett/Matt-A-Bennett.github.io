<div style="text-align: justify">
<p>We create two matrices, call the pivots method and print the results:</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[4, 2, 4],
            [0, 3, 3],
            [0, 1, 2]])

B = la.Mat([[1, 2, 3],
            [4, 5, 6],
            [5, 7, 9]])

print(A.pivots())

print(B.pivots())

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(A_pivots)
{0: 4.0, 1: 3.0, 2: 1.0}

>>> print(B_pivots)
{0: 1.0, 1: -3.0}

{% endhighlight %}
