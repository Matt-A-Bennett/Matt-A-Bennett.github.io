<div style="text-align: justify">
<p>To do this we can make use of the transpose and dot product methods we
already defined: We transpose the second matrix, then for each row of the first
matrix we take the dot product with every 'row' of the transposed second matrix
(the rows in the transposed matrix were formerly columns):</p>
</div>

{% highlight python %}

def multiply(self, new_mat):
    # preallocate empty matrix
    multiplied = gen_mat([self.size(0), new_mat.size(1)])
    # transpose one matrix, take a bunch of dot products
    new_mat = new_mat.transpose()
    for i, row in enumerate(self.data):
        tmp_row = Mat([row])
        for j, col in enumerate(new_mat.data):
            # enter the dot product into our final matrix
            multiplied.data[i][j] = tmp_row.dot(Mat([col]))
    return multiplied

{% endhighlight %}
