<div style="text-align: justify">
<p>We create a vector, call the norm method and print the result. We also
confirm that the length of the normalised vector is 1 (ignoring rounding errors
after 15 decimal places):</p>
</div>

{% highlight python %}

u = la.Mat([[1, 0, 1]])

u_normalised = u.norm()

print_mat(u_normalised)

print(round(u_normalised.length(),15))

{% endhighlight %}

Outputs:

{% highlight shell %}

>>> print(u_length)
>>> print_mat(u_normalised)
[0.7071067811865475, 0.0, 0.7071067811865475]

>>> print(round(u_normalised.length(),15))
1.0

{% endhighlight %}
