# EA = U
<div style="text-align: justify">
<p>Solving a set of simultaneous equations (when there is an unique solution) can
be done by subtracting multiples of one from another such that an unknown is
'eliminated'. By repeating this procedure, we can eliminate all but one unknown
from an equation, leaving a trivially easy solution of the remaining unknown.
Having found the value of that unknown, we can move to trivially solving any
equation involving two unknowns provided one of them is the one we have
previously solved. Continuing this procedure of 'back substitution' will
systematically solve for all the unknowns.</p>
</div>

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

<div style="text-align: justify">
<p>In linear algebra, the procedure of elimination can be carried out by
multiplying a matrix A of coefficients with an elimination matrix E. The result
of is an upper triangular matrix U.</p>
</div>

The initial problem looks like:

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

The elimination procedure looks like:

$$
Ux = EAx = Eb
$$

$$
= Ux = %
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

<div style="text-align: justify">
<p>In the case that we find a zero sitting in a column above an unknown that we want to
eliminate, we can exchange the row with the zero with some row below that
doesn't have a zero in that column.</p>

<p>What we would like to do is encode the results of each elimination step in the
matrix E.</p>
</div>

{% highlight python %}

    def elimination(self):
        # should do some row exchanges for numerical stability...

        # we assume the matrix is invertible
        singular = 0

        # create identity matrix which we'll turn into an E matrix
        tmpE = gen_mat([len(self.data),len(self.data[0])])
        for row_idx in range(len(tmpE.data)):
            tmpE.data[row_idx][row_idx] = 1

        # create a permutation matrix for row exchanges
        P = gen_mat([len(self.data),len(self.data)])
        for row_idx in range(len(tmpE.data)):
            P.data[row_idx][row_idx] = 1

        currentE = copy.deepcopy(tmpE)
        U = copy.deepcopy(self)
        pivot_count = 0
        row_exchange_count = 0
        for row_idx in range(len(U.data)-1):
            for sub_row in range(row_idx+1, len(U.data)):
                # create elimination mat
                nextE = copy.deepcopy(tmpE)

                # handle a zero in the pivot position
                if U.data[row_idx][pivot_count] == 0:
                    row_exchange_count += 1
                    # look for a non-zero value to use as the pivot
                    options = [row[pivot_count] for row in U.data[sub_row:]]
                    exchange = sub_row + options.index(max(options, key=abs))

                    # build and apply a purmutation matrix
                    P = copy.deepcopy(P)
                    P.data[row_idx][pivot_count] = 0
                    P.data[row_idx][exchange] = 1
                    P.data[exchange][exchange] = 0
                    P.data[exchange][pivot_count] = 1
                    U = P.multiply(U)

                # get copies of the rows
                row_above = copy.deepcopy(Mat([U.data[row_idx]]))
                row_below = copy.deepcopy(Mat([U.data[sub_row]]))

                # check if the permutation avoided a zero in the pivot position
                if U.data[sub_row][sub_row] == 0:
                    singular = 1
                    return currentE, self, U, singular, row_exchange_count

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
        return currentE, self, U, singular, row_exchange_count

{% endhighlight %}


[< Matrix Multiplication](./dot_prod_and_mat_multiply.md)\
[Rank, pivots, singularity, determinant >](./rank_piv_sing_det.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
