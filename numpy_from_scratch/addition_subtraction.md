# Addition/Subtraction
<div style="text-align: justify">
Here, the method is called from an initial matrix, with the second
matrix supplied as an argument. Then I simply loop over the rows of each
matrix, each time looping over the elements of those rows (i.e. the columns),
summing them and appending them to an added_rows variable.
</div>

{% highlight python %}

def add(self, new_mat):
    added_rows = []
    for rows in zip(self.data, new_mat.data):
        added_cols = []
        for cols in zip(rows[0],rows[1]):
            added_cols.append(sum(list(cols)))
        added_rows.append(added_cols)
    return Mat(added_rows)

{% endhighlight %}

<div style="text-align: justify">
In the case of the subtraction, we can simply reverse the signs for the second
matrix by applying a scalar multiplication with -1 and then call the add
method, thus achieving a subtraction. 
</div>

{% highlight python %}

def subtract(self, new_mat):
    # reverse sign of second matrix
    new_mat.scale(-1)
    # use add function
    return self.add(new_mat)

{% endhighlight %}

[< Scalar Multiplication](./scalar_multiplication.md)\
[Dot Product and Matrix Multiplication >](./dot_prod_and_mat_multiply.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
