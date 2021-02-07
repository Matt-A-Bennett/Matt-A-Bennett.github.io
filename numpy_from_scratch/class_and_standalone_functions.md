# Classes, miscellaneous methods and standalone functions
## The Mat(rix) Class
<div style="text-align: justify">
<p>First off, we need a class 'Mat' (as in 'matrix'). Matrix like data will be
passed to the Mat class in the form of a list of lists, with each sub-list
acting as a row. We will gradually build up a suit of methods to do all the
needed operations.</p> 
</div>

{% highlight python %}

class Mat:
    def __init__(self, data):
        self.data = data

# define a 2x3 matrix
Mat([[1, 2, 3], [4, 5, 6]])

{% endhighlight %}

## Miscellaneous methods
### Get the diagonal of a matrix
<div style="text-align: justify">
<p>This function works along the diagonal of the matrix, starting in the top
left and stopping after running out of rows or columns.</p>
</div>

{% highlight python %}

def diag(self):
    diag_vals = []
    for i in range(min(len(self.data), len(self.data[0]))):
        diag_vals.append(self.data[i][i])
    return diag_vals

{% endhighlight %}

## Standalone functions
### Generate matrices
<div style="text-align: justify">
<p>We make a method to generate a matrix of a given size, uniformly populated
with a particular value (default 0):</p>
</div>

{% highlight python %}

def gen_mat(size, value=0):
    generated_mat = []
    for i in range(size[0]):
        generated_mat.append([value for j in range(size[1])])
    return Mat(generated_mat)

{% endhighlight %}

<div style="text-align: justify">
<p>Another useful matrix to generate immediately is the identity matrix. We
use the previous function and populate the diagonal with 1's.</p>
</div>

{% highlight python %}

def eye(size):
    eye = gen_mat(size)
    for i in range(size[0]):
        eye.data[i][i] = 1
    return eye

{% endhighlight %}

### Combining matrices

{% highlight python %}

<div style="text-align: justify">
<p>This method concatenates two matrices along a dimension.</p>
</div>

def cat(A, B, axis=0):
    if axis == 0:
        concatenated = Mat([rows[0]+rows[1] for rows in zip(A.data, B.data)])
    if axis == 1:
        print(A, B)
        concatenated = Mat(A.data + B.data)
    return concatenated

{% endhighlight %}

### Printing matrices
<div style="text-align: justify">
<p>Here is a function to print a matrix, one row beneath the other. This is
helpful for debugging.</p>
</div>

{% highlight python %}

def print_mat(self):
    for row in self.data:
        print(row)
    print()

{% endhighlight %}

[Transpose >](./transpose.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
