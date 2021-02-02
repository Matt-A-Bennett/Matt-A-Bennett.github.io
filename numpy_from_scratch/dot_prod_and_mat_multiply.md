# Dot Product and Matrix Multiplication
## Dot Product
<div style="text-align: justify">
The dot product is only valid for two vectors (with the same number of
entries). You simply match up each element between the vectors, multiply them
and add the results. The current implementation will only work for two row
vectors.
</div><br/>

{% highlight python %}

def dot(self, new_mat):
    # only works for 2 row vectors at the moment...
    if len(self.data) != 1 and len(new_mat.data) != 1:
        print('error: dot product is only valid for 2 vectors')
    else:
        dotted = []
        for cols in zip(self.data[0], new_mat.data[0]):
            dotted.append(cols[0]*cols[1])
        dotted = sum(dotted)
        return Mat(dotted)

{% endhighlight %}

## Matrix Multiplication
<div style="text-align: justify">
At a low level, matrix multiplication can be seen as a series of dot products
between the rows of one matrix and the columns of another. For example, the
(2,3) entry of a matrix C produced through the multiplication of two other
matrices A and B, would be the dot product of the 2nd row of A with the 3rd row
of B. To do this we can make use of the transpose and dot product methods we
already defined: We transpose the second matrix, then for each row of the first
matrix we take the dot product with every 'row' of the transposed second matrix
(the rows in the transposed matrix were formerly columns).
</div><br/>

{% highlight python %}

def multiply(self, new_mat):
    multiplied = []
    # transpose one matrix, take a bunch of dot products
    transposed = new_mat.transpose()
    for row_idx, row in enumerate(self.data):
        tmp_row = Mat([row])
        for col_idx, col in enumerate(transposed.data):
            tmp_col = Mat([col])
            tmp_dot = tmp_row.dot(tmp_col)
            # first time through, make new row for each old column
            if row_idx == 0:
                multiplied.append([tmp_dot.data])
            else:
                # append to newly created rows
                multiplied[col_idx].append(tmp_dot.data)
    return Mat(multiplied)

{% endhighlight %}

[< Addition/Subtraction](./addition_subtraction.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)