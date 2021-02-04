# Scalar Multiplication
<div style="text-align: justify">
<p>Scalar multiplication is a simple matter of taking some matrix (or vector) and
multiplying all of its elements by some number (the scalar). To do this we
iterate over the subscript indices of the matrix and apply the multiplication
to each element.</p>
</div><br/>

{% highlight python %}

def scale(self, scalar):
    for row_idx, row in enumerate(self.data):
        for col_idx in range(len(row)):
            self.data[row_idx][col_idx] *= scalar
    return self

{% endhighlight %}


[< Transpose](./transpose.md)\
[Addition/Subtraction >](./addition_subtraction.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
