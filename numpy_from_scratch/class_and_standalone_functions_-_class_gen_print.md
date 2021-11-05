# Class, standalone functions and miscellaneous methods (1/3)
## The Mat(rix) Class
{% include_relative Mat.md %}

## Standalone functions

### Printing matrices
{% include_relative print_mat.md %}
#### Code implementation
{% include_relative print_mat_code.md %}

### Generate matrices
{% include_relative gen_mat.md %}
{% include_relative eye.md %}
#### Demo
{% include_relative gen_mat_demo.md %}

## Miscellaneous methods 
###  Size of a matrix
<div style="text-align: justify">
<p>The size of a matrix is simply its number of rows and columns.</p>
</div>

#### Code implementation
<div style="text-align: justify">
<p>Here we return the number of rows, or columns, or both depending on the axis
argument:</p>
</div>

{% highlight python %}

def size(self, axis=2):
    if axis == 0:
        return len(self.data)
    elif axis == 1:
        return len(self.data[0])
    elif axis == 2:
        return [len(self.data), len(self.data[0])]

{% endhighlight %}

<div style="text-align: right">
<a href="https://matt-a-bennett.github.io/numpy_from_scratch/class_and_standalone_functions_-_sq_tri_diag_sym.html">Is matrix triangular, diagonal, symmetric? ></a>
</div>

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

