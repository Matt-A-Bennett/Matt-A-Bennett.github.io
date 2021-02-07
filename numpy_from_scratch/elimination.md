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

<p>What we would like to do is encode the results of each elimination step in
the matrix E and to have the result U coming from the multiplication of E with
A.</p>

<p>First we create a few matrices which we'll use later on. The first is the
identity matrix I, which will become our matrix E, but which could have more
columns than rows (this allows us to find the inverse, described in a later
post). The second is a permutation matrix P, which allows us to exchange the
rows of a matrix through multiplication:</p>
</div>

{% highlight python %}

def elimination(self):
    # should do some row exchanges for numerical stability...

    # we assume the matrix is invertible
    singular = 0

    # create identity matrix which we'll turn into an E matrix
    tmpE = eye([len(self.data),len(self.data[0])])

    # create a permutation matrix for row exchanges
    tmpP = eye([len(self.data),len(self.data)])

{% endhighlight %}

<div style="text-align: justify">
<p>Each iteration of elimination will produce an E matrix for that step. We
continually multiply those E's together to keep track of the overall E. The
input matrix is copied to U, and will become the upper triangular matrix. We
also produce a permutation matrix P, that encodes any row exchanges needed.</p>

<p>For each entry on the diagonal of the matrix (the 'pivot positions'), we
carry out a row exchange if we find a zero:</p>
</div>

{% highlight python %}

E = copy.deepcopy(tmpE)
P = copy.deepcopy(tmpP)
U = copy.deepcopy(self)
pivot_count = 0
row_exchange_count = 0
for row_idx in range(len(U.data)-1):
    for sub_row in range(row_idx+1, len(U.data)):
        # create elimination mat
        nextE = copy.deepcopy(tmpE)
        nextP = copy.deepcopy(tmpP)

        # handle a zero in the pivot position
        if U.data[row_idx][pivot_count] == 0:
            row_exchange_count += 1
            # look for a non-zero value to use as the pivot
            options = [row[pivot_count] for row in U.data[sub_row:]]
            exchange = sub_row + options.index(max(options, key=abs))

            # build and apply a purmutation matrix
            nextP.data[row_idx][pivot_count] = 0
            nextP.data[row_idx][exchange] = 1
            nextP.data[exchange][exchange] = 0
            nextP.data[exchange][pivot_count] = 1
            U = nextP.multiply(U)
            P = nextP.multiply(P)

{% endhighlight %}

<div style="text-align: justify">
<p>If after a possible row exchange we have a zero in the pivot position then
the matrix is singular and we return our results and a flag indicating
singularity. Otherwise, we copy the two rows we're doing elimination on and
determine what multiple of the higher row to subtract from the lower row so as
to eliminate the unknown. After carrying out the subtraction we update U with
the eliminated row:</p>
</div>

{% highlight python %}

# check if the permutation avoided a zero in the pivot position
if U.data[row_idx][row_idx] == 0:
    singular = 1
    return P, E, self, U, singular, row_exchange_count

# get copies of the rows
row_above = copy.deepcopy(Mat([U.data[row_idx]]))
row_below = copy.deepcopy(Mat([U.data[sub_row]]))

# determine how much to subtract to create a zero
ratio = row_below.data[0][pivot_count]/row_above.data[0][pivot_count]
# do the subtraction
row_above.scale(ratio)
row_below = row_below.subtract(row_above)
# add to our U
U.data[sub_row] = row_below.data[0]

{% endhighlight %}

<div style="text-align: justify">
<p>We create a nextE matrix for the previous step and update the overall E by
multiplying it:</p>
</div>

{% highlight python %}

    # add to our E
    nextE.data[sub_row][row_idx] = -ratio
    # update the overall E
    E = nextE.multiply(E)
pivot_count += 1

{% endhighlight %}

<div style="text-align: justify">
<p>After the final pivot has been placed into U, we just check if it was zero,
and if so indicate that with a flag on returning the results:</p>
</div>

{% highlight python %}

# check if the permutation avoided a zero in the pivot position
if U.data[row_idx+1][row_idx+1] == 0:
    singular = 1

return P, E, self, U, singular, row_exchange_count

{% endhighlight %}


[< Matrix Multiplication](./dot_prod_and_mat_multiply.md)\
[Rank, pivots, singularity, determinant >](./rank_piv_sing_det.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
