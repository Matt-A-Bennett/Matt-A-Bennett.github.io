# A = QR
<div style="text-align: justify">
<p>There are many benefits to working with set of vectors that span some space
and are all 'orthonormal' - meaning each vector has a dot product of zero with
every other and a dot product of one with itself. It's common to denote such
matrices with: $Q$. Multiplying this matrix $Q$ with it's transpose $Q^T$ gives
$I$ - therefore $Q^T = Q^{-1}$. This makes projection, and many other
calculations easy. For instance, the projection matrix $A(A^TA)^{-1}A^T$
becomes $Q(Q^TQ)^{-1}Q^T = QQ^T$ and so we don't need to do any
elimination!</p>

<p>Thus, it is useful to be able to express a matrix $A$ in terms of $QR$. We
do that by 'orthogonalising' the columns of $A$. The 'Gram-Schmidt' procedure
involves projecting columns of $A$ onto the nullspace of other columns of
$A$.</p>

<p>Projecting onto $N(A^T)$, will yield a vector that we called the 'error' in
the last post. It was the difference between an initial vector $b$ and the
projection (\(A\hat x\)), encoded in the projection matrix $P$ onto $C(A)$:
</p>
</div>

$$
b - Pb
$$

We can rewrite that as:

$$
Ib - Pb
$$

And factor out the vector $b$:

$$
b(I - P)
$$

<p>So to project onto the nullspace, we use the projection matrix $I - P$. We
start by projecting the 2nd column onto the nullspace of the 1st. This new
vector is orthogonal to the 1st, which is what we want. We do the same with the
rest of the columns, so that now the 1st column is orthogonal to every other
column.</p>

<p>Next we repeat the procedure with our partially orthogonalised matrix,
aiming to make the 3rd, 4th... nth columns orthogonal to the <i>2nd column</i>
(in addition to the 1st). We repeat this procedure for the 3rd column... and
onwards until every column is orthogonal to every other.</p>

<p>The matrix that reassembles $A$ from $Q$ is upper triangular and denoted
$R$. The reason for $R$ being upper triangular is that the more rightward
columns of $A$ have undergone more projections and so are represented by a
combination of more columns of $Q$ and so need more non-zero rows of $R$ to
provide the combining weights. Since $A = QR$, we can recover $R = Q^TA$ (since
$Q^{-1} = Q^T$ at the end of the Gram-Schmidt procedure.</p>
</div>

## Code implementation
<div style="text-align: justify">
<p>We already have the method to give us a projection matrix. So here we take
$I - P$ as our projection matrix. After transposing $A$ (to make accessing the
columns easier) we loop over each columns and make the others orthogonal. Then
we move onto the next column and repeat:</p>
</div>

{% highlight python %}

def qr(self):
    A = copy.deepcopy(self)

    if A.is_singular():
        print('Matrix is singular!')
        return None

    A = A.transpose()
    Q = copy.deepcopy(A)
    I = eye([len(A.data),len(A.data[0])])
    # projection orthogonal to column
    for col in range(len(Q.data)-1):
        Col = copy.deepcopy(Q.data[col])
        Col = Mat([Col])
        Col = Col.transpose()
        P, _ = Col.projection()
        P = I.subtract(P)
        # project and put into matrix Q
        for col2 in range(col+1, len(Q.data)):
            Col = copy.deepcopy(Q.data[col2])
            Col = Mat([Col])
            Col = Col.transpose()
            q = P.multiply(Col)
            q = q.transpose()
            Q.data[col2] = q.data[0]

{% endhighlight %}

<div style="text-align: justify">
<p>The next step is to make the length of each column 1. Which we do by
dividing by it's current length:</p>
</div>

{% highlight python %}

# normalise to unit length
    for x, q in enumerate(Q.data):
        q = Mat([q])
        qn = q.length()
        q = q.scale(1/qn)
        Q.data[x] = q.data[0]

{% endhighlight %}

<div style="text-align: justify">
<p>The last step is transpose $A$ back to how it was originally, and to
generate $R$ by multiplying $Q^TA$. Note that because we worked from $A^T$ from
the beginning, our $Q$ is already transposed, so we just multiply this with $A$
and then transpose $Q$ before returning:</p>
</div>

{% highlight python %}
    A = A.transpose()
    R = Q.multiply(A)
    Q = Q.transpose()
    A = Q.multiply(R)

    return A, Q, R

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create a matrix, call the qr method and print the results. Note that we
print the $A$ computed from $QR$ at two levels of rounding precision. We begin
to see rounding errors beyond 13 decimal places:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
         [2, 4, 12],
         [2, 8, 0]])

A, Q, R = A.qr()
print_mat(Q, 2)
print_mat(R, 2)
print_mat(A, 13)
print_mat(A, 16)

{% endhighlight %}

Outputs:

{% highlight shell %}

>>> print_mat(Q, 2)
[0.33, -0.3, -0.89]
[0.67, -0.6, 0.45]
[0.67, 0.75, 0.0]

>>> print_mat(R, 2)
[3.0, 8.67, 9.0]
[0.0, 2.98, -8.05]
[0.0, 0.0, 2.68]

>>> print_mat(A, 13)
[1.0, 2.0, 3.0]
[2.0, 4.0, 12.0]
[2.0, 8.0, 0.0]

>>> print_mat(A, 20)
[0.9999999999999989, 1.9999999999999973, 2.9999999999999956]
[2.0000000000000004, 4.0, 12.000000000000004]
[2.0, 8.0, 0.0]

{% endhighlight %}

[< Projection and regression](./projection_and_regression.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/qr_factorisation.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

