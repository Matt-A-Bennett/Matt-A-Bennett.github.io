<div style="text-align: justify">
<p>We create two matrices, call the is_singular method and print the results:</p>
</div>

{% highlight python %}

A = la.Mat([[1, 2, 3],
            [4, 5, 6],
            [5, 8, 9]])

B = la.Mat([[1, 2, 3],
            [4, 5, 6],
            [5, 7, 9]])

A_sing = A.is_singular()

B_sing = B.is_singular()

print(A_sing)
print()
print(B_sing)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(A_sing)
0
>>> print(B_sing)
1

{% endhighlight %}
