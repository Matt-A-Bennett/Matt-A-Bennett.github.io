<div style="text-align: justify">
<p>To do this we can make use of the transpose and dot product methods we
already defined: We transpose the second matrix, then for each row of the first
matrix we take the dot product with every 'row' of the transposed second matrix
(the rows in the transposed matrix were formerly columns):</p>
</div>

{% highlight python %}

def multiply(self, new_mat):
    A = dc(self)
    B = dc(new_mat)
    # preallocate empty matrix
    multiplied = gen_mat([size(A)[0], size(B)[1]])
    # transpose one matrix, take a bunch of dot products
    B = B.transpose()
    for row_idx, row in enumerate(A.data):
        tmp_row = Mat([row])
        for col_idx, col in enumerate(B.data):
            # enter the dot product into our final matrix
            multiplied.data[row_idx][col_idx] = tmp_row.dot(Mat([col]))
    return multiplied

{% endhighlight %}
