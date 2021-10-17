# Class, standalone functions and miscellaneous methods (1/3)
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

## Standalone functions

### Printing matrices
<div style="text-align: justify">
<p>Here is a function to print a matrix, one row beneath the other. This is
helpful for debugging. We also include an option to round the values to a
specified precision, which is useful to ignore very tiny rounding errors on
what would otherwise be integer numbers:</p>
</div>

#### Code implementation
{% highlight python %}

def print_mat(self, round_dp=99):
    A = dc(self)
    for row in A.data:
        rounded = [round(i,round_dp) for i in row]
        print(rounded)
    print()

{% endhighlight %}

### Generate matrices
<div style="text-align: justify">
<p>We make a method to generate a matrix of a given size, populated with a
particular set of values (default all zeros) and of a particular type (full by
default, or optionally diagonal, upper, lower):</p>

<p>First, we ensure that we won't run out of values when populating the matrix. If
a single value is passed, then we repeat that value. If more than one value is
passed, but is less than the largest row/column dimension of the matrix, then
we pad the value list with zeros. This scheme will allow us to make some quite
useful types of matrices such as tri-diagonal etc.</p>

{% highlight python %}

def gen_mat(size, values=[0], type='full'):
    if len(values) == 1:
        values = [values[0] for val in range(max(size))]
    elif len(values) < max(size):
        values += [0 for val in range(max(size)-len(values))]

{% endhighlight %}

<p>Now that we have our list of values, we loop over each row/column of the
matrix and decide whether to put a value from the list of a zero (in the case
of diagonal/upper/lower matrices, we know some parts of the matrix will be
zero).</p>

<p>If the matrix is to have a single diagonal, we place a value from the list
once per row, in the jth column.</p> 

<p>An interesting case is when we provide more than one value with type='full'.
In this case we check which diagonal we're on (i.e. main, 1st off-diagonal, 2nd
off-diagonal etc.) and pull the corresponding item (0th, 1st, 2nd) from the
value list. If the original value list contained more than one value it will
have been padded with zeros, and the result will be a matrix with some
recurring number along each diagonal (see demos below). If only a single value
was supplied then this value will have been repeated and the result will be a
uniformly populated matrix</p>

{% highlight python %}

generated_mat = []
for i in range(size[0]):
    row = []
    for j in range(size[1]):
        if (type == 'diag' and j!=i) or (type == 'upper' and j<=i) or (type == 'lower' and j>=i):
            row.append(0)
        elif type == 'diag':
            row.append(values[j])
        elif j>=i:
            row.append(values[j-i])
        elif j<i:
            row.append(values[i-j])
    generated_mat.append(row)
return Mat(generated_mat)

{% endhighlight %}

### Demo

{% highlight python %}

print_mat(gen_mat([7,7], values=[1], type='full'))
print_mat(gen_mat([7,7], values=[1], type='upper'))
print_mat(gen_mat([7,7], values=[1,2,0,4,5], type='diag'))
print_mat(gen_mat([7,7], values=[2,-1], type='full'))

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print_mat(gen_mat([7,7], values=[1], type='full'))
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]

>>> print_mat(gen_mat([7,7], values=[1], type='upper'))

[0, 1, 1, 1, 1, 1, 1]
[0, 0, 1, 1, 1, 1, 1]
[0, 0, 0, 1, 1, 1, 1]
[0, 0, 0, 0, 1, 1, 1]
[0, 0, 0, 0, 0, 1, 1]
[0, 0, 0, 0, 0, 0, 1]
[0, 0, 0, 0, 0, 0, 0]

>>> print_mat(gen_mat([7,7], values=[1,2,0,4,5], type='diag'))

[1, 0, 0, 0, 0, 0, 0]
[0, 2, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 4, 0, 0, 0]
[0, 0, 0, 0, 5, 0, 0]
[0, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 0, 0]

>>> print_mat(gen_mat([7,7], values=[2,-1], type='full'))

[2, -1, 0, 0, 0, 0, 0]
[-1, 2, -1, 0, 0, 0, 0]
[0, -1, 2, -1, 0, 0, 0]
[0, 0, -1, 2, -1, 0, 0]
[0, 0, 0, -1, 2, -1, 0]
[0, 0, 0, 0, -1, 2, -1]
[0, 0, 0, 0, 0, -1, 2]

{% endhighlight %}

<p>A very common matrix to generate immediately is the identity matrix. We use
the previous function and populate the diagonal with 1's.</p>

{% highlight python %}

def eye(size):
    return gen_mat(size, values=[1], type='diag')

{% endhighlight %}

</div>

[Is matrix triangular, diagonal, symmetric? >](./class_and_standalone_functions_-_tri_diag_sym.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/class_and_standalone_functions.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

