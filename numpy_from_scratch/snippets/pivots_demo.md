<div style="text-align: justify">
<p>We create two matrices, call the pivots method and print the results:</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 2, 3],
            [4, 5, 6],
            [5, 8, 9]])

B = la.Mat([[1, 2, 3],
            [4, 5, 6],
            [5, 7, 9]])

A_pivots = A.pivots()

B_pivots = B.pivots()

print(A_pivots)
print()
print(B_pivots)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(A_pivots)
{0: 1.0, 1: -3.0, 2: -2.0}

>>> print(B_pivots)
{0: 1.0, 1: -3.0}

{% endhighlight %}
