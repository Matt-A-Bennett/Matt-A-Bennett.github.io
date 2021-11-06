<div style="text-align: justify">
<p>While coding other functions in this library, I noticed I was often
extracting a single row, column, or particular value from the matrix by doing:</p>
</div>

{% highlight python %}

my_value = A.data[0][0]

{% endhighlight %}

<div style="text-align: justify">
<p>This seemed a bit clunky so I defined a method with a more readable
interface to do it:</p>
</div>


