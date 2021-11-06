We use the same matrices as in the [Pivots
section](./class_and_standalone_functions_2.md#pivots), and call the pivots
method and check if they're positive definite:

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
