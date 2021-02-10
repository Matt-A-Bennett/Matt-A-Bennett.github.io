# Transpose
<div style="text-align: justify">
<p>To transpose a matrix, we need a new matrix in which the rows are the former
columns and the columns are the former rows:</p>
</div>

$$
A =%
  \begin{bmatrix}
    1 & 2 & 3 \\
    4 & 5 & 6
  \end{bmatrix};
   
A^T =%
  \begin{bmatrix}
    1 & 4 \\
    2 & 5 \\
    3 & 6
  \end{bmatrix}
$$

## Code implementation
<div style="text-align: justify">
<p>We loop over the rows and columns of the input matrix, keeping a record of
the row and column subscript indices. The transposed matrix is built up
gradually with a set of new rows (each row being the values found in the
corresponding column):</p>
</div>

{% highlight python %}

def transpose(self):
    A = copy.deepcopy(self)
    transposed = []
    for row_idx, row in enumerate(A.data):
        for col_idx, col in enumerate(row):
            # first time through, make new row for each old column
            if row_idx == 0:
                transposed.append([col])
            else:
                # append to newly created rows
                transposed[col_idx].append(col)
        A.data = transposed
    return A

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create a matrix, call the transpose method and print the result:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
         [4, 5, 6]])

transposed = A.transpose()

print_mat(transposed)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print_mat(transposed)
[1, 4]
[2, 5]
[3, 6]

{% endhighlight %}

[< The Mat(rix) Class and standalone functions](./class_and_standalone_functions.md)\
[Scalar Multiplication >](./scalar_multiplication.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/transpose.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

