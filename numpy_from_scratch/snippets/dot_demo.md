<div style="text-align: justify">
<p>We create two vectors, call the dot method and print the result:</p>
</div>

{% highlight python %}
import linalg as la

u = la.Mat([[1, 2, 2]])

v = la.Mat([[1, 1, 3]])

dotted = u.dot(v)

print(dotted)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(dotted)
9

{% endhighlight %}
