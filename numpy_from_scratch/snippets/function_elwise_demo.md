<div style="text-align: justify">
<p>We create two matrices, call a subset of the methods and print the
results:</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 2, 3],
            [4, 5, 6]])

B = la.Mat([[0, 2, 1],
            [3, 6, -1]])

la.print_mat(A.add(B))

la.print_mat(A.subtract(2))

la.print_mat(A.multiply_elwise(B))

la.print_mat(A.div_elwise(2))

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(A.add(B))
[1, 4, 4]
[7, 11, 5]

>>> la.print_mat(A.subtract(2))
[-1, 0, 1]
[2, 3, 4]

>>> la.print_mat(A.multiply_elwise(B))
[0, 4, 3]
[12, 30, -6]

>>> la.print_mat(A.div_elwise(2))
[0.5, 1.0, 1.5]
[2.0, 2.5, 3.0]

{% endhighlight %}
<p>Just as with the case in the add and subtract methods, we check if the B
argument is of class matrix and decide whether to use a function of one or of
two variables:</p>
</div>

{% highlight python %}

def multiply_elwise(self, B):
    return self.function_choice(B, [lambda x: x*B, lambda x, y: x*y])

def div_elwise(self, B):
    return self.function_choice(B, [lambda x: x/B, lambda x, y: x/y])

{% endhighlight %}
