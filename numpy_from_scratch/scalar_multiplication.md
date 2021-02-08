# Scalar Multiplication
<div style="text-align: justify">
<p>Scalar multiplication is a simple matter of taking some matrix (or vector) and
multiplying all of its element: by some number (the scalar):</p>
</div>

$$
2A = 2
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 2 & 6 \\
    4 & 5 & 6
  \end{bmatrix}
  =
  \begin{bmatrix}
    2 & 4 & 6 \\
    4 & 4 & 12 \\
    8 & 10 & 12
  \end{bmatrix}
$$

## Code implementation
<div style="text-align: justify">
<p>To do this we iterate over the subscript indices of the matrix and apply the
multiplication to each element:</p>
</div>

{% highlight python %}

def scale(self, scalar):
    for row_idx, row in enumerate(self.data):
        for col_idx in range(len(row)):
            self.data[row_idx][col_idx] *= scalar
    return self

{% endhighlight %}

[< Transpose](./transpose.md)\
[Addition/Subtraction >](./addition_subtraction.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/scalar_multiplication.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

