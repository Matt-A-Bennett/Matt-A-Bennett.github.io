<p>In our function, we will always multiply on the left, and therefore
transpose the matrix in the case that we want the sum the rows. If a vector is
passed, we always sum the elements:</p>
</div>

{% highlight python %}

def sum(A, axis=0):
    # if we have a vector, we sum along it's length
    if min(la.size(A)) == 1:
        axis = la.size(A).index(max(la.size(A)))
    if axis == 1:
        A = A.tr()
    ones = la.gen_mat([1,la.size(A)[0]],1)
    A_sum = ones.multiply(A)
    return A_sum

{% endhighlight %}
