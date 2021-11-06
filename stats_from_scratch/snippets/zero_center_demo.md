<div style="text-align: justify">
<p>We create a matrix, call the zero center method twice with a different axis
as an argument and print the results (we only print 2 decimal places in one
case to make it look pretty):</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[1, 2, 3],
            [-2, 1, 4],
            [0, 1, 2],
            [3, 6, 1]])

B = la.Mat([[1, 1, 1],
            [0, 2, 0],
            [0, 3, -4]])

result = la.stats.zero_center(A)
la.print_mat(result)

result = la.stats.zero_center(A, axis=1)
la.print_mat(result, 2)

result = la.stats.zero_center(B)
la.print_mat(result, 2)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(result)
[0.5, -0.5, 0.5]
[-2.5, -1.5, 1.5]
[-0.5, -1.5, -0.5]
[2.5, 3.5, -1.5]

>>> la.print_mat(result, 2)
[-1.0, 0.0, 1.0]
[-3.0, 0.0, 3.0]
[-1.0, 0.0, 1.0]
[-0.33, 2.67, -2.33]

>>> la.print_mat(result, 2)
[0.67, -1.0, 2.0]
[-0.33, 0.0, 1.0]
[-0.33, 1.0, -3.0]

{% endhighlight %}
