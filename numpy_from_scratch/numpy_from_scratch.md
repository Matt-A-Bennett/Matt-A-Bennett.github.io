# Building a Python 3 Numpy-like module from scratch
<div style="text-align: justify">
I want to improve my knowledge of classes, objects, functions and methods in
Python 3 and to gain a better understanding of the 'standard practices'
associated with writing them. So I've decided to try and build a Python library
that allows me to do linear algebra operations - something like the popular
Numpy module, but of course much smaller in scope. As a bonus, it will allow me
to consolidate my recent studies of linear algebra. I will attempt to implement
all the linear algebra operations, methods and algorithms covered in Gilbert
Strang's Introduction to linear algebra. As much as possible, I will use
Python's standard library.
</div><br/>

The full code I've written so far can be found [here](./full_code.md).

## The Mat(rix) class and standalone functions
<div style="text-align: justify">
First off, we need a class 'Mat' (as in 'matrix'). Matrix like data will be
passed to the Mat class in the form of a list of lists, with each sub-list
acting as a row. We will gradually build up a suit of methods to do all the
needed operations. 
</div>

{% highlight python %}

class Mat:
    def __init__(self, data):
        self.data = data

# define a 2x3 matrix
Mat([[1, 2, 3], [4, 5, 6]])

{% endhighlight %}

<div style="text-align: justify">
We also define a standalone function to generate a matrix of a given size and
uniformly populated with a particular value (if supplied)
</div>

{% highlight python %}

def gen_mat(size, value=0):
    generated_mat = []
    for i in range(size[0]):
        generated_mat.append([value for j in range(size[1])])
    return Mat(generated_mat)

{% endhighlight %}

## Methods to implement
<div style="text-align: justify">
Below is a list of the topics I've covered in my studies so far, and which I
will attempt to realise in my library.
</div><br/>

### Fundamental Methods
- [Transpose](./transpose.md)
- [Scalar Multiplication](./scalar_multiplication.md)
- [Addition/Subtraction](./addition_subtraction.md)
- [u' * u = dot product](./dot_prod_and_mat_multiply.md)
- [Matrix Multiplication](./dot_prod_and_mat_multiply.md)

### Secondary Methods 
- [EA = U](./elimination.md)
- A = LU
- A = QR
- Rank
- Pivot Columns
- Inverse
- Four fundamental subspaces
- Bases for fundamental subspaces
- Determinant
- Projection
- Orthogonalisation
- Orthonormal basis
- Eigenvalues and Eigenvectors

[back to home](../README.md)

