<div style="text-align: justify">
<p>We create two matrices, call the rank method and print the results:</p>
</div>

{% highlight python %}

A = la.Mat([[1, 2, 3],
         [4, 5, 6],
         [5, 8, 9]])

B = la.Mat([[1, 2, 3],
         [4, 5, 6],
         [5, 7, 9]])

A_rank = A.rank()

B_rank = B.rank()

print(A_rank)
print()
print(B_rank)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(A_rank)
3

>>> print(B_rank)
2

{% endhighlight %}
