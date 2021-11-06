<div style="text-align: justify">
<p>We create a matrix, call the backsub method and print the result. We also
print the result of the multiplication $Ax$ to confirm that we get $b$:</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 2, 3],
            [2, 2, 6],
            [4, 5, 6]])

b = la.Mat([[0],
            [-2],
            [5]])

x = A.backsub(b)

la.print_mat(x, 2)
la.print_mat(A.multiply(x))

{% endhighlight %}

Outputs:

{% highlight shell %}

>>> la.print_mat(x, 2)
[2.0]
[1.0]
[-1.33]

>>> la.print_mat(A.multiply(x))
[0.0]
[-2.0]
[5.0]

{% endhighlight %}
