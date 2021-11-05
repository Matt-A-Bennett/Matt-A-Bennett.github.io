<div style="text-align: justify">
<p>We loop over the rows and columns of the input matrix, keeping a record of
the row and column subscript indices. The transposed matrix is built up
gradually with a set of new rows (each row being the values found in the
corresponding column):</p>
</div>

{% highlight python %}

def transpose(self):
    transposed = []
    for i, row in enumerate(self.data):
        for j, col in enumerate(row):
            # first time through, make new row for each old column
            if i == 0:
                transposed.append([col])
            else:
                # append to newly created rows
                transposed[j].append(col)
    return Mat(transposed)

{% endhighlight %}
