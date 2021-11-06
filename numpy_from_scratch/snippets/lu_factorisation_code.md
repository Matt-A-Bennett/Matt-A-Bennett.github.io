<div style="text-align: justify">
<p>The method I use here is needlessly inefficient since we call the
elimination method 3 times (since our inverse method calls it twice!), when it
is easy to simply inject the multiplying values into $L$ as we do a single pass
of elimination. However, at the moment this project is only about learning how
to write classes and methods and secondarily to solidify my grasp of linear
algebra. In the code we account for row exchanges by multiplying $E$ with $P$
(i.e. the permutation matrix), then taking the inverse of $E$ to get $L$.
Similarly, we ensure $L$ is lower triangular using $P$:</p>
</div>

{% highlight python %}

def lu(self):
    P, E, A, U, _, _ = A.elimination()
    E = P.multiply(E)
    L = P.multiply(E.inverse())
    return A, P, L, U

{% endhighlight %}
