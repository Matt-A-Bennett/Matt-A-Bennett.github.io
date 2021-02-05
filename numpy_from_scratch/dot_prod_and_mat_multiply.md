# Dot Product and Matrix Multiplication
## Dot Product
<div style="text-align: justify">
<p>The dot product is only valid for two vectors (with the same number of
entries). You simply match up each element between the vectors, multiply them
and add the results. We make both vectors row vectors and then carry out the
multiplication and sum operations.</p>
</div>

{% highlight python %}

def dot(self, new_mat):
    # make both vectors rows with transpose
    if len(self.data) != 1:
        self.transpose()
    if len(new_mat.data) != 1:
        new_mat.transpose()
    # compute dot product
    dot_prod = []
    for cols in zip(self.data[0], new_mat.data[0]):
        dot_prod.append(cols[0]*cols[1])
    dot_prod = sum(dot_prod)
    return dot_prod

{% endhighlight %}

## Matrix Multiplication
<div style="text-align: justify">
<p>At a low level, matrix multiplication can be seen as a series of dot products
between the rows of one matrix and the columns of another. For example, the
(2,3) entry of a matrix C produced through the multiplication of two other
matrices A and B, would be the dot product of the 2nd row of A with the 3rd row
of B. To do this we can make use of the transpose and dot product methods we
already defined: We transpose the second matrix, then for each row of the first
matrix we take the dot product with every 'row' of the transposed second matrix
(the rows in the transposed matrix were formerly columns).</p>
</div>

{% highlight python %}

    def multiply(self, new_mat):
        # preallocate empty matrix
        multiplied = gen_mat([len(self.data), len(new_mat.data[0])])
        # transpose one matrix, take a bunch of dot products
        transposed = new_mat.transpose()
        for row_idx, row in enumerate(self.data):
            tmp_row = Mat([row])
            for col_idx, col in enumerate(transposed.data):
                tmp_col = Mat([col])
                tmp_dot = tmp_row.dot(tmp_col)
                # enter the dot product into our final matrix
                multiplied.data[row_idx][col_idx] = tmp_dot
        return multiplied

{% endhighlight %}

[< Addition/Subtraction](./addition_subtraction.md)\
[EA = U >](./elimination.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
