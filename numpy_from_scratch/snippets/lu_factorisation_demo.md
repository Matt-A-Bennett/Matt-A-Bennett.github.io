<div style="text-align: justify">
<p>We create a matrix, call the lu method and print the result:</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 2, 3],
            [4, 8, 6],
            [7, 8, 9]])

A, P, L, U = A.lu()
la.print_mat(A)
la.print_mat(P)
la.print_mat(L)
la.print_mat(U)
PL = P.multiply(L)
PLU = PL.multiply(U)
la.print_mat(PL)
la.print_mat(PLU)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(A)
[1, 2, 3]
[4, 8, 6]
[7, 8, 9]

>>> la.print_mat(P)
[1, 0, 0]
[0, 0, 1]
[0, 1, 0]

>>> la.print_mat(L)
[1.0, 0.0, 0.0]
[7.0, 1.0, 0.0]
[4.0, 0.0, 1.0]

>>> la.print_mat(U)
[1.0, 2.0, 3.0]
[0.0, -6.0, -12.0]
[0.0, 0.0, -6.0]

>>> la.print_mat(PL)
[1.0, 0.0, 0.0]
[4.0, 0.0, 1.0]
[7.0, 1.0, 0.0]

>>> la.print_mat(PLU)
[1.0, 2.0, 3.0]
[4.0, 8.0, 6.0]
[7.0, 8.0, 9.0]

{% endhighlight %}
