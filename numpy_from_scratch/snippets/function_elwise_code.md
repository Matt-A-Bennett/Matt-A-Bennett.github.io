<div style="text-align: justify">
<p> The method requires an arbitrary function as an argument, and can also take
an optional second matrix, B. If B is supplied, then the function must be a
function of two variables (these will be the elements in the $i,j$ positions of
the two matrices).</p>

<p>We loop over the row and column indices of the matrix and, depending on if a
second matrix, B, was supplied, apply the function to yield the new
element:</p>
</div>

{% highlight python %}

def function_elwise(self, function, B=None):
    C = gen_mat(size(self))
    for i in range(size(self)[0]):
        for j in range(size(self)[1]):
            if B:
                C.data[i][j] = function(self.data[i][j], B.data[i][j])
            else:
                C.data[i][j] = function(self.data[i][j])
    return C

{% endhighlight %}
