# Page Title
<div style="text-align: justify">
Solving a set of simultaneous equations (when there is an unique solution) can
be done by subtracting multiples of one from another such that an unknown is
'eliminated'. By repeating this procedure, we can eliminate all but one unknown
from an equation, leaving a trivially easy solution of the value of the
remaining unknown. Having found the value of that unknown, we can move to
trivially solving any equation involving two unknown provided one of them is
the one we have previously solved. Continuing this procedure of 'back
substitution' will systematically deliver all the unknowns. 

In linear algebra, the procedure of elimination can be carried out with by
multiplying a matrix A of coefficients with and elimination matrix E. The
result of the multiplication is an upper triangular matrix U.

For example, the equations:

$$
x + 2y + 3z = 0 \\
2x + 2y + 6z = -2 \\
4x + 5y + 6z = 5
$$

can be translated, after elimination, into:

$$
x + 2y + 3z = 0 \\
0 - 2y + 0 = -2 \\
0 + 0 - 6z = 8
$$

The same procedure in matrix looks like this:

$$
Ax = b =%
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 2 & 6 \\
    4 & 5 & 6
  \end{bmatrix}
  %
  \begin{bmatrix}
    x \\
    y \\
    z
  \end{bmatrix}
  %
  =%
  \begin{bmatrix}
    0 \\
    -2 \\
    5
  \end{bmatrix}
$$

$$
EAx = Eb = E%
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & -2 & 0 \\
    0 & 0 & -6
  \end{bmatrix}
  %
  \begin{bmatrix}
    x \\
    y \\
    z
  \end{bmatrix}
  %
  = E%
  \begin{bmatrix}
    0 \\
    -2 \\
    8
  \end{bmatrix}
$$

What we would like to do is encode the results of each elimination step in the
matrix E.

</div><br/>

{% highlight python %}

def elimination(self):
    # need to handle cases where a zero is already below the pivot
    # should do some row exchanges for numerical stability...

    # create identity matrix which we'll turn into an E matrix
    tmpE = gen_mat([len(self.data),len(self.data[0])])
    for row_idx in range(len(tmpE.data)):
        tmpE.data[row_idx][row_idx] = 1

    currentE = copy.deepcopy(tmpE)
    U = copy.deepcopy(self)
    pivot_count = 0
    for row_idx in range(len(U.data)-1):
        for sub_row in range(row_idx+1, len(U.data)):
            # create elimination mat
            nextE = copy.deepcopy(tmpE)
            # get copies of the rows
            row_above = copy.deepcopy(Mat([U.data[row_idx]]))
            row_below = copy.deepcopy(Mat([U.data[sub_row]]))
            # determine how much to subtract to create a zero
            ratio = row_below.data[0][pivot_count]/row_above.data[0][pivot_count]
            # do the subtraction
            row_above.scale(ratio)
            row_below = row_below.subtract(row_above)
            # add to our E
            nextE.data[sub_row][row_idx] = -ratio
            # add to our U
            U.data[sub_row] = row_below.data[0]
            # update the overall E
            currentE = nextE.multiply(currentE)
        pivot_count += 1
    return currentE, self, U

{% endhighlight %}


[< Matrix Multiplication](./dot_prod_and_mat_multiply.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
