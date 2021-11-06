<div style="text-align: justify">
<p>We create two matrices, call the determinant method and print the results:</p>
</div>

{% highlight python %}

A = la.Mat([[1, 2, 3],
            [4, 5, 6],
            [5, 8, 9]])

B = la.Mat([[1, 2, 3],
            [4, 5, 6],
            [5, 7, 9]])

A_determinant = A.determinant()

B_determinant = B.determinant()

print(A_determinant)
print()
print(B_determinant)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(A_determinant)
6.0

>>> print(B_determinant)
-0.0

{% endhighlight %}
