<div style="text-align: justify">
<p>We create a matrix, call the transpose method and print the result:</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 2, 3],
            [4, 5, 6]])

transposed = A.tr()

la.print_mat(transposed)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(transposed)
[1, 4]
[2, 5]
[3, 6]

{% endhighlight %}
