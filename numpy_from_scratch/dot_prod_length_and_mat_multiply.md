# Dot product, length and matrix multiplication
## Dot product
<div style="text-align: justify">
<p>The dot product is only valid for pairs of vectors (with the same number of
entries). You simply match up each element between the vectors, multiply them
and add the results:</p>

$$
u \cdot v =%
  \begin{bmatrix}
    1 \\
    2 \\
    3
  \end{bmatrix} \cdot
   
  \begin{bmatrix}
    4 \\
    5 \\
    6
  \end{bmatrix} = 32
$$

</div>

### Code implementation
<div style="text-align: justify">
<p>We make both vectors row vectors and then carry out the multiplication and
sum operations.</p>
</div>

{% highlight python %}

def dot(self, new_mat):
    A = dc(self)
    B = dc(new_mat)
    # make both vectors rows with transpose
    if size(A)[0] != 1:
        A = A.transpose()
    if size(B)[0] != 1:
        B = B.transpose()
    # compute dot product
    dot_prod = []
    for cols in zip(A.data[0], B.data[0]):
        dot_prod.append(cols[0]*cols[1])
    dot_prod = sum(dot_prod)
    return dot_prod

{% endhighlight %}

### Demo

<div style="text-align: justify">
<p>We create two vectors, call the dot method and print the result:</p>
</div>

{% highlight python %}
import linalg as la

u = la.Mat([[1, 2, 2]])

v = la.Mat([[1, 1, 3]])

dotted = u.dot(v)

print(dotted)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(dotted)
9

{% endhighlight %}

## Length
<div style="text-align: justify">
<p>The length of a vector $u$ is defined as the square root of the dot product
of the vector with itself: \(\sqrt{u \cdot u}\).</p>
</div>

### Code implementation

{% highlight python %}

def length(self):
    A = dc(self)
    v_length = sqrt(A.dot(A))
    return v_length

{% endhighlight %}

### Demo
<div style="text-align: justify">
<p>We create a vector, call the length method and print the result:</p>
</div>

{% highlight python %}

u = la.Mat([[1, 1, 3]])

u_length = u.length()

print(u_length)

{% endhighlight %}

Outputs:

{% highlight shell %}

>>> print(u_length)
3.3166247903554

{% endhighlight %}

## Norm
<div style="text-align: justify">
<p>To normalise a vector we just divide by the length:</p>
</div>

### Code implementation

{% highlight python %}

def norm(self):
    A = dc(self)
    A_norm = A.scale(1/A.length())
    return A_norm

{% endhighlight %}

### Demo
<div style="text-align: justify">
<p>We create a vector, call the norm method and print the result. We also
confirm that the length of the normalised vector is 1 (ignoring rounding errors
after 15 decimal places):</p>
</div>

{% highlight python %}

u = la.Mat([[1, 0, 1]])

u_normalised = u.norm()

print_mat(u_normalised)

print(round(u_normalised.length(),15))

{% endhighlight %}

Outputs:

{% highlight shell %}

>>> print(u_length)
>>> print_mat(u_normalised)
[0.7071067811865475, 0.0, 0.7071067811865475]

>>> print(round(u_normalised.length(),15))
1.0

{% endhighlight %}

## Matrix multiplication
<div style="text-align: justify">
<p>At a low level, matrix multiplication can be seen as a series of dot
products between the rows of one matrix and the columns of another. For
example, the (2,3) entry of a matrix $C$ produced through the multiplication of
two other matrices $A$ and $B$, would be the dot product of the 2nd row of $A$
with the 3rd row of $B$</p>
</div>

$$
AB =%
  \begin{bmatrix}
    1 & 2 & 3 \\
    4 & 5 & 6
  \end{bmatrix}
   
  \begin{bmatrix}
    1 & 2 \\
    1 & 1 \\
    3 & 2
  \end{bmatrix} =%

  \begin{bmatrix}
    12 & 10 \\
    27 & 25
  \end{bmatrix}
$$

### Code implementation
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

### Demo

<div style="text-align: justify">
<p>We create two matrices, call the multiply method and print the result:</p>
</div>

{% highlight python %}

A = la.Mat([[1, 1, 3],
         [2, 5, 4]])

B = la.Mat([[1, 1],
         [1, 3],
         [-1, 3]])

C = A.multiply(B)

la.print_mat(C)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(C)
[-1, 13]
[3, 29]

{% endhighlight %}

[< Element-wise functions of one or more matrices >](./elwise_function.md)\
[EA = U >](./elimination.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/dot_prod_and_mat_multiply.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

