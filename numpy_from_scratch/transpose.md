# Transpose
<div style="text-align: justify">
First off, we need a class 'Mat' (as in 'matrix'). We will gradually build up a
suit of methods to do all the needed operations. 

To transpose a matrix, we need a new matrix in which the rows are the former
columns and the columns are the former rows. I loop of the rows and columns of
the input matrix, keeping a record of the row and column subscript indices. The
transposed matrix is built up gradually with a set of new rows (each row being
the values found in the corresponding column.
</div>

{% highlight python %}

class Mat:
    def __init__(self, data):
        self.data = data

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
        return Mat(transposed)

{% endhighlight %}

[Addition/Subtraction >](./addition_subtraction.md)<br/>
[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
