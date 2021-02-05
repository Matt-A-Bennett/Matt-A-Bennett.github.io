# Inverse
<div style="text-align: justify">
<p>The inverse of a square matrix A is that matrix which multiples A (on either
side) to give the identity matrix. Not all matrices have inverses. A good way
to find the inverse of a matrix is through elimination. Once we have reached EA
= U, we carry on eliminating the upper triangular region of U to get to a
diagonal matrix. This diagonal matrix is more similar to I, and by dividing
each row appropriately it <i>is</i> I. That means that there were some sequence
of elimination steps which brought A to I. If we had applied those steps to I
we would have ended up at the inverse of A!</p>

<p>So to compute the inverse of A, we do elimination, but we apply the
operations to the matrix I. We already have a library method for doing
elimination, so we will call that method twice (to clear out the lower, and the
the uppper triangular regions of A). Beyond that we only need to do some
division of each row at the end.</p>

</div>

{% highlight python %}

def inverse(self):
    size = [len(self.data), len(self.data[0])]

    # create [A I]
    I = eye(size)
    augmented = Mat([rows[0]+rows[1]  for rows in zip(self.data, I.data)])

    # perform elimination to get to [U ~inv]
    E, A, U = augmented.elimination()

    # creae anti-diag I
    antiI = gen_mat(size)
    for i, j in enumerate(reversed(range(size[1]))):
        antiI.data[i][j] = 1

    # seperate augmented into U and ~inv
    tmp_fU = Mat([Urow[0:size[1]] for Urow in U.data])
    tmp_inv = Mat([Urow[size[1]:] for Urow in U.data])

    # multiply U and ~inv on both sides by anti-diag I
    fU = antiI.multiply(tmp_fU)
    fU = fU.multiply(antiI)
    f_tmp_inv = antiI.multiply(tmp_inv)
    f_tmp_inv.multiply(antiI)

    # put fU back into [fU  f~inv]
    augmented = Mat([rows[0]+rows[1] for rows in zip(fU.data, f_tmp_inv.data)])

    # perform elimination again to get to [cI cA^-1]
    _, _, U = augmented.elimination()

    # divide each row by c to get [I A^-1]
    div = gen_mat(size)
    for i in range(size[0]):
        div.data[i][i] = 1/U.data[i][i]
    inv = div.multiply(U)

    # flip back
    inv = antiI.multiply(inv)
    for i in range(size[1]):
        inv.data[i] = inv.data[i][size[1]:]
    return inv

{% endhighlight %}


[< EA = U](./elimination.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
