<div style="text-align: justify">
<p>We create a matrix, call the qr method and print the results. Note that we
print the $A$ computed from $QR$ at two levels of rounding precision. We begin
to see rounding errors beyond 13 decimal places:</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 2, 3],
            [2, 4, 12],
            [2, 8, 0]])

A, Q, R = A.qr()
la.print_mat(Q, 2)
la.print_mat(R, 2)
la.print_mat(A, 13)
la.print_mat(A, 20)

{% endhighlight %}

Outputs:

{% highlight shell %}

>>> la.print_mat(Q, 2)
[0.33, -0.3, -0.89]
[0.67, -0.6, 0.45]
[0.67, 0.75, 0.0]

>>> la.print_mat(R, 2)
[3.0, 8.67, 9.0]
[0.0, 2.98, -8.05]
[0.0, 0.0, 2.68]

>>> la.print_mat(A, 13)
[1.0, 2.0, 3.0]
[2.0, 4.0, 12.0]
[2.0, 8.0, 0.0]

>>> la.print_mat(A, 20)
[0.9999999999999989, 1.9999999999999973, 2.9999999999999956]
[2.0000000000000004, 4.0, 12.000000000000004]
[2.0, 8.0, 0.0]

{% endhighlight %}
