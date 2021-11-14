<div style="text-align: justify">
<p>We make a method to generate a matrix of a given size, populated with a
particular set of values (default all zeros) and of a particular type (full by
default, or optionally diagonal, upper, lower):</p>

<p>First, we ensure that we won't run out of values when populating the matrix. If
a single value is passed, then we repeat that value. If more than one value is
passed, but is less than the largest row/column dimension of the matrix, then
we pad the value list with zeros. This scheme will allow us to make some quite
useful types of matrices such as tri-diagonal etc.</p>
</div>

{% highlight python %}

def gen_mat(size, values=[0], kind='full'):
    if type(size) is int:
        size = [size, size]
    if len(values) == 1:
        values = [values[0] for val in range(max(size))]
    elif len(values) < max(size):
        values += [0 for val in range(max(size)-len(values))]

{% endhighlight %}

<div style="text-align: justify">
<p>Now that we have our list of values, we loop over each row/column of the
matrix and decide whether to put a value from the list or a zero (in the case
of diagonal/upper/lower matrices, we know some parts of the matrix will be
zero).</p>

<p>If the matrix is to have a single diagonal, we place a value from the list
once per row, in the jth column.</p> 

<p>An interesting case is when we provide more than one value with kind='full'.
In this case we check which diagonal we're on (i.e. main, 1st off-diagonal, 2nd
off-diagonal etc.) and pull the corresponding item (0th, 1st, 2nd) from the
value list. If the original value list contained more than one value it will
have been padded with zeros, and the result will be a matrix with some
recurring number along each diagonal (see demos below). If only a single value
was supplied then this value will have been repeated and the result will be a
uniformly populated matrix</p>
</div>

{% highlight python %}

generated_mat = []
for i in range(size[0]):
    row = []
    for j in range(size[1]):
        if (kind == 'diag' and j!=i) or (kind == 'upper' and j<=i) or (kind == 'lower' and j>=i):
            row.append(0)
        elif kind == 'diag':
            row.append(values[j])
        elif j>=i:
            row.append(values[j-i])
        elif j<i:
            row.append(values[i-j])
    generated_mat.append(row)
return Mat(generated_mat)

{% endhighlight %}

