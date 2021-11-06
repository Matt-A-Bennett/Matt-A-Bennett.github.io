<div style="text-align: justify">
<p>We use the same matrices as in the 
<a href="https://matt-a-bennett.github.io/numpy_from_scratch/rank_piv_sing_det.html">Pivots section above</a>
, and call the pivots method and check if they positive definite:</p>
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
A.is_posdef()

print(B.pivots())
B.is_posdef()

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(A_pivots)
{0: 4.0, 1: 3.0, 2: 1.0}

>>> A.is_posdef()
True

>>> print(B_pivots)
{0: 1.0, 1: -3.0}

>>> B.is_posdef()
False

{% endhighlight %}
