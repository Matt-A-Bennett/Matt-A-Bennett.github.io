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
<p>I loop over the rows and columns of the input matrix, keeping a record of
the row and column subscript indices. The transposed matrix is built up
gradually with a set of new rows (each row being the values found in the
corresponding column):</p>
</div>

{% highlight python %}

def transpose(self):
    transposed = []
    for row_idx, row in enumerate(self.data):
        for col_idx, col in enumerate(row):
            # first time through, make new row for each old column
            if row_idx == 0:
                transposed.append([col])
            else:
                # append to newly created rows
                transposed[col_idx].append(col)
        self.data = transposed
    return self

{% endhighlight %}

[< The Mat(rix) Class and standalone functions](./class_and_standalone_functions.md)\
[Scalar Multiplication >](./scalar_multiplication.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
