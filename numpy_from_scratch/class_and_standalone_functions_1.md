<script>
MathJax = {
tex: {
tags: 'ams'  // should be 'ams', 'none', or 'all'
     }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>

# Class, standalone functions and miscellaneous methods (1/3)
## The Mat(rix) Class
{% include_relative snippets/Mat.md %}

## Standalone functions
### Printing matrices
{% include_relative snippets/print_mat.md %}
#### Code implementation
{% include_relative snippets/print_mat_code.md %}

### Generate matrices
{% include_relative snippets/gen_mat.md %}
{% include_relative snippets/eye.md %}
#### Demo
{% include_relative snippets/gen_mat_demo.md %}
#### The vandamonde matrix
{% include_relative snippets/vandermonde_code.md %}
#### Demo
{% include_relative snippets/vandermonde_demo.md %}

## Miscellaneous methods 
### Size of a matrix
{% include_relative snippets/size.md %}
#### Code implementation
{% include_relative snippets/size_code.md %}

### Transpose of a matrix
{% include_relative snippets/transpose.md %}
#### Code implementation
{% include_relative snippets/transpose_code.md %}
#### Demo
{% include_relative snippets/transpose_demo.md %}

### Indexing a matrix
{% include_relative snippets/ind.md %}
#### Code implementation
{% include_relative snippets/ind_code.md %}
### Make 1x1 matrix a scalar
{% include_relative snippets/make_scalar_code.md %}
### Get the diagonal of a matrix
{% include_relative snippets/diag_code.md %}

#### Demo
{% include_relative snippets/ind_demo.md %}

<div style="text-align: right">
<a href="https://matt-a-bennett.github.io/numpy_from_scratch/class_and_standalone_functions_2.html">Is matrix triangular, diagonal, symmetric? ></a>
</div>

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/class_and_standalone_functions_1.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

