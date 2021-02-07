# Inverse
<div style="text-align: justify">
<p>The inverse of a square matrix A is that matrix which multiples A (on either
side) to give the identity matrix. Not all matrices have inverses. A good way
to find the inverse of a matrix is through elimination. Once we have reached EA
= U, we carry on eliminating the upper triangular region of U to get to a
diagonal matrix. This diagonal matrix is more similar to I, and by dividing
each row appropriately it <i>is</i> I. That means that there was some sequence
of elimination steps which brought A to I. If we had applied those steps to I
we would have ended up at the inverse of A!</p>

<p>So to compute the inverse of A, we do elimination, but we apply the
operations to the matrix I. We already have a library method for doing
elimination, so we will call that method twice (to clear out the lower, and the
upper triangular regions of A). Beyond that we only need to do some division of
each row at the end.</p>

<p>We take in the matrix A to invert and 'augment' it by concatenating the
identity matrix I to it's right side and run the elimination procedure to take A
to U, and apply the same steps to I. If elimination produces a zero row, A is
singular and has no inverse:</p>
</div>

{% highlight python %}

def inverse(self):
     size = [len(self.data), len(self.data[0])]

    # create [A I]
    I = eye(size)
    augmented = cat(self, I)

    # perform elimination to get to [U ~inv]
    _, _, U, singular, _ = augmented.elimination()

    if singular:
        print('Matrix is singular!')
        return None

{% endhighlight %}

<div style="text-align: justify">
<p>Now we want to do another round of elimination, only this time working
upwards to clear out the upper triangular region of U (and apply the same steps
to the right half, formerly I). In order to do this using our method
'elimination', which is only capable of eliminating the lower triangular
region, we have to rearrange both the matrix U and the right half such that the
rows are flipped upside down, and the columns are flipped left to right. We do
this rearrangement by separately multiplying U and the right half with an
anti-diagonal identity matrix on the left and right sides:</p>
</div>

{% highlight python %}

# seperate augmented into U and ~inv
tmp_fU = Mat([Urow[0:size[1]] for Urow in U.data])
tmp_inv = Mat([Urow[size[1]:] for Urow in U.data])

# creae anti-diag I
antiI = gen_mat(size)
for i, j in enumerate(reversed(range(size[1]))):
    antiI.data[i][j] = 1

# multiply U and ~inv on both sides by anti-diag I
fU = antiI.multiply(tmp_fU)
fU = fU.multiply(antiI)
f_tmp_inv = antiI.multiply(tmp_inv)
f_tmp_inv.multiply(antiI)

{% endhighlight %}

<div style="text-align: justify">
<p>Now we reassemble the matrix and run elimination again to achieve a diagonal
matrix on the left half and a full matrix on the right:</p>
</div>

{% highlight python %}

# put fU back into [fU  f~inv]
augmented = cat(fU, f_tmp_inv)

# perform elimination again to get to [cI cA^-1]
_, _, U, _, _ = augmented.elimination()

{% endhighlight %}

<div style="text-align: justify">
<p>To complete the calculation and achieve the matrix I on the left we divide
each row by whatever number appears on the diagonal. Lastly we re-exchange the
rows of the right side and we have the inverse:</p>
</div>

{% highlight python %}

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

[< Rank, pivots, singularity, determinants](./rank_piv_sing_det.md)\
[A = LU >](./lu_factorisation.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
