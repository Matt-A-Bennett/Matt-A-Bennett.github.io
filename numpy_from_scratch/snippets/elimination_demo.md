<div style="text-align: justify">
<p>We create a matrix, call the elimination method and print the result:</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 2, 3],
         [4, 8, 6],
         [7, 8, 9]])

P, E, A, U, singular, row_exchange_count = A.elimination()

print(singular)
print()
print(row_exchange_count)
print()
la.print_mat(P)
la.print_mat(E)
la.print_mat(A)
la.print_mat(U)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(singular)
0
>>> print(row_exchange_count)
1
>>> la.print_mat(P)
[1, 0, 0]
[0, 0, 1]
[0, 1, 0]

>>> la.print_mat(E)
[1.0, 0.0, 0.0]
[-4.0, 1.0, 0.0]
[-7.0, 0.0, 1.0]

>>> la.print_mat(A)
[1, 2, 3]
[4, 8, 6]
[7, 8, 9]

>>> la.print_mat(U)
[1.0, 2.0, 3.0]
[0.0, -6.0, -12.0]
[0.0, 0.0, -6.0]

{% endhighlight %}
