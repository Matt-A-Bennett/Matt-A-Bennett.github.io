# EA = U
<div style="text-align: justify">
<p>Solving a set of simultaneous equations (when there is an unique solution)
can be done by subtracting multiples of one from another such that an unknown
is 'eliminated'. By repeating this procedure, we can eliminate all but one
unknown from an equation, leaving a trivially easy solution of the remaining
unknown. Having found the value of that unknown, we can move to trivially
solving any equation involving two unknowns provided one of them is the one we
have previously solved. Continuing this procedure of 'back substitution' will
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
multiplying a matrix $A$ of coefficients with an elimination matrix $E$. The
result of is an upper triangular matrix $U$.</p>
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
Ux = %
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
<p>In the case that we find a zero sitting in a column above an unknown that we
want to eliminate, we can exchange the row with the zero with some row below
that doesn't have a zero in that column.</p>

<p>What we would like to do is encode the results of each elimination step in
the matrix $E$ and to have the result $U$ coming from the multiplication of $E$
with $A$.</p>
</div>

## Code implementation
<div style="text-align: justify">
<p>First we create a few matrices which we'll use later on. The first is the
identity matrix $I$, which will become our matrix $E$, but which could have
more columns than rows (this allows us to find the inverse, described in a
later post). The second is a permutation matrix $P$, which allows us to
exchange the rows of a matrix through multiplication:</p>
</div>

{% highlight python %}

def elimination(self):
    A = copy.deepcopy(self)
    # should do some row exchanges for numerical stability...

    # we assume the matrix is invertible
    singular = 0

    # create identity matrix which we'll turn into an E matrix
    tmpE = eye([size(A)[0], size(A)[1]])

    # create a permutation matrix for row exchanges
    tmpP = eye(size(A))

{% endhighlight %}

<div style="text-align: justify">
<p>Each iteration of elimination will produce an $E$ matrix for that step. We
continually multiply those $E$'s together to keep track of the overall $E$. The
input matrix is copied to $U$, and will become the upper triangular matrix. We
also produce a permutation matrix P, that encodes any row exchanges needed.</p>

<p>For each entry on the diagonal of the matrix (the 'pivot positions'), we
carry out a row exchange if we find a zero:</p>
</div>

{% highlight python %}

E = copy.deepcopy(tmpE)
P = copy.deepcopy(tmpP)
U = copy.deepcopy(A)
pivot_count = 0
row_exchange_count = 0
for row_idx in range(size(U)[0]-1):
    for sub_row in range(row_idx+1, size(U)[0]):
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
the matrix is singular and we flag that fact. We also undo the failed
permutation and carry on with elimination in the next column.</p>
</div>

{% highlight python %}

# check if the permutation avoided a zero in the pivot position
if U.data[row_idx][row_idx] == 0:
    singular = 1
    # undo the row exchanges that failed
    row_exchange_count -= 1
    nextP = nextP.transpose()
    U = nextP.multiply(U)
    P = nextP.multiply(P)
    # move on to the next column
    break

{% endhighlight %}

<div style="text-align: justify">
<p>If we have avoided a zero pivot, we determine what multiple of the higher
row to subtract from the lower row so as to eliminate the unknown. This
multiple goes into our nextE matrix and is applied to $U$:</p>
</div>

{% highlight python %}

# determine how much to subtract to create a zero
ratio = U.data[sub_row][pivot_count]/U.data[row_idx][pivot_count]
# create the elimination matrix for this step
nextE.data[sub_row][row_idx] = -ratio
# apply the elimination step to U
U = nextE.multiply(U)

{% endhighlight %}

<div style="text-align: justify">
<p>We update the overall $E$ by multiplying it with nextE:</p>
</div>

{% highlight python %}

    # update the overall E
    E = nextE.multiply(E)
pivot_count += 1
{% endhighlight %}

<div style="text-align: justify">
<p>In the case of a 1x1 matrix, the loops in the code above won't happen, and
we just take the reciprocal of the number, if it's not zero, to be the pivot.
After the final pivot has been placed into $U$, we just check if it was zero,
and if so indicate that with a flag on returning the results:</p>
</div>

{% highlight python %}

# If A was a 1x1 matrix, the above loops didn't happen. Take the
# reciprocal of the number:
if size(U)[0] == 1 and size(U)[1] == 2:
    if U.data[0][0] != 0:
        U.data[0] = [1/U.data[0][0], 1]
    row_idx = -1

# check if the permutation avoided a zero in the pivot position
elif U.data[row_idx+1][row_idx+1] == 0:
    singular = 1

return P, E, self, U, singular, row_exchange_count

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create a matrix, call the elimination method and print the result:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
         [4, 8, 6],
         [7, 8, 9]])

P, E, A, U, singular, row_exchange_count = A.elimination()

print(singular)
print()
print(row_exchange_count)
print()
print_mat(P)
print_mat(E)
print_mat(A)
print_mat(U)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(singular)
0
>>> print(row_exchange_count)
1
>>> print_mat(P)
[1, 0, 0]
[0, 0, 1]
[0, 1, 0]

>>> print_mat(E)
[1.0, 0.0, 0.0]
[-4.0, 1.0, 0.0]
[-7.0, 0.0, 1.0]

>>> print_mat(A)
[1, 2, 3]
[4, 8, 6]
[7, 8, 9]

>>> print_mat(U)
[1.0, 2.0, 3.0]
[0.0, -6.0, -12.0]
[0.0, 0.0, -6.0]

{% endhighlight %}

[< Dot product, length and matrix multiplication](./dot_prod_length_and_mat_multiply.md)\
[Rank, pivots, singularity, determinant >](./rank_piv_sing_det.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/elimination.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

