<div style="text-align: justify">
<p>We already have a library method for doing elimination, so we will call that
method twice (to clear out the lower and upper triangular regions of $A$).
Beyond that we only need to do some division of each row at the end.</p>

<p>We take in the matrix $A$ to invert and 'augment' it by concatenating the
identity matrix $I$ to it's right side and run the elimination procedure to
take $A$ to $U$, and apply the same steps to $I$. If elimination produces a
zero row, then $A$ is singular and has no inverse:</p>
</div>

{% highlight python %}

def inverse(self):
    mat_size = size(A)

    # create [A I]
    I = eye(size)
    augmented = cat(A, I, axis=1)

    # perform elimination to get to [U ~inv]
    _, _, _, U, singular, _ = augmented.elimination()

    if singular:
        print('Matrix is singular!')
        return None

{% endhighlight %}

<div style="text-align: justify">
<p>Now we want to do another round of elimination, only this time working
upwards to clear out the upper triangular region of $U$ (and apply the same
steps to the right half, formerly $I$). In order to do this using our method
'elimination', which is only capable of eliminating the lower triangular
region, we have to rearrange both the matrix $U$ and the right half such that
the rows are flipped upside down, and the columns are flipped left to right. We
do this rearrangement by separately multiplying $U$ on the right half with an
anti-diagonal identity matrix on the left and right sides:</p>
</div>

{% highlight python %}

# seperate augmented into U and ~inv
tmp_fU = Mat([Urow[0:size[1]] for Urow in U.data])
tmp_inv = Mat([Urow[size[1]:] for Urow in U.data])

# create anti-diag I
antiI = gen_mat(size)
for i, j in enumerate(reversed(range(size[1]))):
    antiI.data[i][j] = 1

# multiply U and ~inv on both sides by anti-diag I
fU = antiI.multiply(tmp_fU).multiply(antiI)
f_tmp_inv = antiI.multiply(tmp_inv).multiply(antiI)

{% endhighlight %}

<div style="text-align: justify">
<p>Now we reassemble the matrix and run elimination again to achieve a diagonal
matrix on the left half and a full matrix on the right:</p>
</div>

{% highlight python %}

# put fU back into [fU  f~inv]
augmented = cat(fU, f_tmp_inv, axis=1)

# perform elimination again to get to [cI cA^-1]
_, _, U, _, _ = augmented.elimination()

{% endhighlight %}

<div style="text-align: justify">
<p>To complete the calculation and achieve the matrix $I$ on the left we divide
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
inv = inv.multiply(antiI)

return inv

{% endhighlight %}
