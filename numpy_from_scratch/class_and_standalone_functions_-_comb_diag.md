# Class, standalone functions and miscellaneous methods (3/3)
## Standalone functions
### Combining matrices
<div style="text-align: justify">
<p>This method concatenates two matrices along a dimension.</p>
</div>

{% highlight python %}

def cat(A, B, axis=0):
    if axis == 0:
        concatenated = Mat(A.data + B.data)
    elif axis == 1:
        concatenated = Mat([rows[0]+rows[1] for rows in zip(A.data, B.data)])
    return concatenated

{% endhighlight %}

### Tiling matrices
<div style="text-align: justify">
<p>We can easily make a large matrix by repeated 'tiling' a smaller matrix by a
repeated series of concatenations. We make a copy of the original matrix, and
in two loops concatenate it to the appropriate axis (starting by adding more
columns, and then replicating this 'row of matrices' downwards.</p>
</div>

{% highlight python %}

def tile(A, axes=[1,1]):
    B = dc(A)
    for j in range(axes[1]-1):
        A = cat(A, B, axis=1)
    B = dc(A)
    for i in range(axes[0]-1):
        A = cat(A, B, axis=0)
    return A

{% endhighlight %}

### Demo
<div style="text-align: justify">
<p>We create a matrix and tile it:</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 2],
            [0, 5],
            [0, 0]])

la.print_mat(la.tile(A, [2, 5]))

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.tile(A, [3, 4]))
[1, 2, 1, 2, 1, 2, 1, 2, 1, 2]
[0, 5, 0, 5, 0, 5, 0, 5, 0, 5]
[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
[1, 2, 1, 2, 1, 2, 1, 2, 1, 2]
[0, 5, 0, 5, 0, 5, 0, 5, 0, 5]
[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

{% endhighlight %}

## Miscellaneous methods
### Get the diagonal of a matrix
<div style="text-align: justify">
<p>This function works along the diagonal of the matrix, starting in the top
left and stopping after running out of rows or columns.</p>
</div>

{% highlight python %}

def diag(self):
    A = dc(self)
    diag_vals = []
    for i in range(min(size(A))):
        diag_vals.append(A.data[i][i])
    return diag_vals

{% endhighlight %}

[< Is matrix triangular, diagonal, symmetric?](./class_and_standalone_functions_-_sq_tri_diag_sym.md)\
[Transpose >](./transpose.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/class_and_standalone_functions.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

