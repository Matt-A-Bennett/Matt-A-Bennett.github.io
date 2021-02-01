# Addition/Subtraction
<div style="text-align: justify">
First off, we need a class 'Mat' (as in 'matrix'). We will gradually build up a
suit of methods to do all the needed operations. 

Below is what I've come up with as an initial implementation for adding one
matrix to another. The method is called from an initial matrix, with the second
matrix supplied as an argument. Then I simply loop over the rows of each
matrix, each time looping of the elements of those rows (i.e. the columns),
summing them and appending them to a added_rows variable.
</div>

{% highlight python %}

class Mat:
    def __init__(self, data):
        self.data = data

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
In the case of the subtraction, I simply reverse the signs for the second
matrix and the call the add method, thus achieving a subtraction. Now that I
look at it, I realise that once I have a method for scalar multiplication of a
matrix I can simply use that method to achieve the sign reversal, rather than
the loops I have here.
</div>

{% highlight python %}

    def subtract(self, new_mat):
        # reverse sign of second matrix
        tmp = []
        for row in new_mat.data:
            tmp_col = []
            for col in row:
                tmp_col.append(-col)
            tmp.append(tmp_col)
        # use add method
        return self.add(Mat(tmp))

{% endhighlight %}


[back to project overview](./numpy_from_scratch.md)\
[back to home](../README.md)
