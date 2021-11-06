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

print('Inverting matrix A...')
A_inverse = A.inverse()

if A_inverse:
    la.print_mat(A_inverse)

print('Inverting matrix B...')
B_inverse = B.inverse()

if B_inverse:
    la.print_mat(B_inverse)

{% endhighlight %}

Outputs:

{% highlight console %}

Inverting matrix A...
[-0.5, 1.0, -0.5]
[-1.0, -1.0, 1.0]
[1.1667, 0.3333, -0.5]

Inverting matrix B...
Matrix is singular!

{% endhighlight %}
