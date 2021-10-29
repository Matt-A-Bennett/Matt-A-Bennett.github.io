# Element-wise functions of one or more matrices
<div style="text-align: justify">
<p>We define a useful method for applying any function to each element of a
matrix (e.g. scaling, raising to any power) and for applying any function to
the elements in two matrices to produce a third matrix (e.g. adding, Hadamard
products). The 'function_elwise' method forms the basis for several
operations.</p>
</div>

## Code implemetation

<div style="text-align: justify">
<p> The method requires an arbitrary function as an argument, and can also take
an optional second matrix, B. If B is supplied, then the function must be a
function of two variables (these will be the elements in the $i,j$ positions of
the two matrices).</p>

<p>We loop over the row and column indices of the matrix and, depending on the
if a second matrix, B, was supplied, apply the function to yield the new
element:</p>
</div>

{% highlight python %}

def function_elwise(self, function, B=None):
    C = gen_mat(size(self))
    for i in range(size(self)[0]):
        for j in range(size(self)[1]):
            if B:
                C.data[i][j] = function(self.data[i][j], B.data[i][j])
            else:
                C.data[i][j] = function(self.data[i][j])
    return C

{% endhighlight %}

<div style="text-align: justify">
<p>We also define a method to choose which of a list of supplied
functions to apply, given the argument B. If the argument B was not an instance
of the class 'Mat' we assume an integer or float was passed and that the user
wants to use the first listed function, and otherwise wants to apply the second
function. Thus the appropriate function is passed, along with the argument B
into function_elwise:</p>
</div>

{% highlight python %}

def function_choice(self, B, functions):
    if isinstance(B, Mat) == False:
        return self.function_elwise(functions[0])
    return self.function_elwise(functions[1], B)

{% endhighlight %}

# Addition and subtraction
<div style="text-align: justify">
<p>Addition and subtraction is valid between two same-shaped matrices and is
done element-wise:</p>
</div>

$$
A + B =%
  \begin{bmatrix}
    1 & 2 & 3 \\
    4 & 5 & 6
  \end{bmatrix}+%

  \begin{bmatrix}
    2 & 1 & 4 \\
    0 & 3 & 1
  \end{bmatrix}=%

  \begin{bmatrix}
    3 & 3 & 7 \\
    4 & 8 & 7
  \end{bmatrix}
$$

<div style="text-align: justify">
<p>Although not a strictly legal operation, adding/subtracting a scalar to/from
a matrix is a useful thing to do (and can be achieved by subtracting an 'all
ones' matrix that itself has been multiplied by a scalar)</p>
</div>

$$
  \begin{bmatrix}
    1 & 2 & 3 \\
    4 & 5 & 6
  \end{bmatrix} ``+ 2" =%
$$

$$
  \begin{bmatrix}
    1 & 2 & 3 \\
    4 & 5 & 6
  \end{bmatrix}+ 2%

  \begin{bmatrix}
    1 & 1 & 1 \\
    1 & 1 & 1
  \end{bmatrix}=%

  \begin{bmatrix}
    3 & 4 & 5 \\
    6 & 7 & 8
  \end{bmatrix}
$$

## Code implemetation

<div style="text-align: justify">
<p>Here we call the function_choice method with a list of two lambda functions.
In the case that B was not a matrix, we assume that the user wants to
add/subtract the same scaler from each element. This is a simple function of
each element and is reflected in the first lambda function in the list. On the
other hand, if the B argument was a matrix, the second lambda function of two
variables (x and y: the $i,j$ elements from the original matrix and matrix B)
will be applied:</p>
</div>

{% highlight python %}

def add(self, B):
    return self.function_choice(B, [lambda x: x+B, lambda x, y: x+y])

def subtract(self, B):
    return self.function_choice(B, [lambda x: x-B, lambda x, y: x-y])

{% endhighlight %}

# Element-wise multiplication/division and scalar multiplication
<div style="text-align: justify">
<p>Just what it sounds like. We will use $\odot$ and $\oslash$ to denote these
two operations:</p>
</div>

$$
A \odot B = 
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 0 & 0 \\
    4 & -2 & -1
  \end{bmatrix}
  \odot
  \begin{bmatrix}
    2 & 2 & 3 \\
    4 & 2 & 1 \\
    1 & 3 & 2
  \end{bmatrix} =
  \begin{bmatrix}
    2 & 4 & 9 \\
    8 & 0 & 0 \\
    8 & -6 & -2
  \end{bmatrix}
$$

$$
A \oslash B = 
  \begin{bmatrix}
    1 & 2 & 3 \\[5pt]
    2 & 0 & 0 \\[5pt]
    4 & -2 & -1
  \end{bmatrix}
  \oslash
  \begin{bmatrix}
    2 & 2 & 3 \\[5pt]
    4 & 2 & 1 \\[5pt]
    1 & 3 & 2
  \end{bmatrix} =
  \begin{bmatrix}
    \frac{1}{2} & 1 & 1 \\[5pt]
    \frac{1}{2} & 0 & 0 \\[5pt]
    4 & -\frac{2}{3} & -\frac{1}{2}
  \end{bmatrix}
$$

<div style="text-align: justify">
<p>Scalar multiplication, which <i>is</i> a legal operation in linear algebra,
is a simple matter of taking some matrix (or vector) and
multiplying all of its elements by some number (the scalar):</p>
</div>

$$
2A = 2
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 2 & 6 \\
    4 & 5 & 6
  \end{bmatrix}
  =
  \begin{bmatrix}
    2 & 4 & 6 \\
    4 & 4 & 12 \\
    8 & 10 & 12
  \end{bmatrix}
$$

## Code implemetation
<div style="text-align: justify">
<p>Just as with the case in the add and subtract methods, we check if the B
argument is of class matrix and decide whether to use a function of one or of
two variables:</p>
</div>

{% highlight python %}

def multiply_elwise(self, B):
    return self.function_choice(B, [lambda x: x*B, lambda x, y: x*y])

def div_elwise(self, B):
    return self.function_choice(B, [lambda x: x/B, lambda x, y: x/y])

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create two matrices, call a subset of the methods and print the
results:</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 2, 3],
         [4, 5, 6]])

B = la.Mat([[0, 2, 1],
         [3, 6, -1]])

la.print_mat(A.add(B))

la.print_mat(A.subtract(2))

la.print_mat(A.multiply_elwise(B))

la.print_mat(A.div_elwise(2))

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(A.add(B))
[1, 4, 4]
[7, 11, 5]

>>> la.print_mat(A.subtract(2))
[-1, 0, 1]
[2, 3, 4]

>>> la.print_mat(A.multiply_elwise(B))
[0, 4, 3]
[12, 30, -6]

>>> la.print_mat(A.div_elwise(2))
[0.5, 1.0, 1.5]
[2.0, 2.5, 3.0]

{% endhighlight %}

[< Transpose](./transpose.md) \
[Dot Product >](./dot_prod_length_and_mat_multiply.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/elwise_function.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

