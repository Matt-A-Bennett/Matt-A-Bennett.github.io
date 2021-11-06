<div style="text-align: justify">
<p>First we create a few matrices which we'll use later on. The first is the
identity matrix $I$, which will become our matrix $E$, but which could have
more columns than rows (this allows us to find the inverse, described in a
later post). The second is a permutation matrix $P$, which allows us to
exchange the rows of a matrix through multiplication:</p>
</div>

{% highlight python %}

def elimination(self):
    # we assume the matrix is invertible
    singular = False

    # size of elimination and perumtation matrices
    mat_size = [self.size(0)]*2

    # create identity matrix which we'll turn into an E matrix
    E = eye(mat_size)

    # create a permutation matrix for row exchanges
    P = eye(mat_size)

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

U = dc(self)
pivot_count = 0
row_exchange_count = 0
for idx in range(U.size(0)-1):
    for sub_row in range(idx+1, U.size(0)):
        # create elimination mat
        nextE = eye(mat_size)
        nextP = eye(mat_size)

        # handle a zero in the pivot position
        if U.data[idx][pivot_count] == 0:
            row_exchange_count += 1
            # look for a non-zero value to use as the pivot
            options = [row[pivot_count] for row in U.data[sub_row:]]
            exchange = sub_row + options.index(max(options, key=abs))

            # build and apply a purmutation matrix
            nextP.data[idx][pivot_count] = 0
            nextP.data[idx][exchange] = 1
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
if U.data[idx][idx] == 0:
    singular = True
    # undo the row exchanges that failed
    row_exchange_count -= 1
    U = nextP.transpose().multiply(U)
    P = nextP.transpose().multiply(P)
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
    ratio = U.data[sub_row][pivot_count]/U.data[idx][pivot_count]
    # create the elimination matrix for this step
    nextE.data[sub_row][idx] = -ratio
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

# If self was a 1x1 matrix, the above loops didn't happen. Take the
# reciprocal of the number:
if U.size(0) == 1 and U.size(1) == 2:
    if U.ind(0,0) != 0:
        U.data[0] = [1/U.ind(0,0), 1]
    i = -1

# check if the matrix is square
if U.size(1) == U.size(0):
    # check if the permutation avoided a zero in the pivot position
    if U.data[idx+1][idx+1] == 0:
        singular = True

return P, E, self, U, singular, row_exchange_count

{% endhighlight %}
