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
involves projecting columns of $A$ onto the nullspace of columns of $A^T$.</p>

<p>Projecting onto $N(A^T)$, will yield a vector that we called the 'error' in
the last post. It was the difference between an initial vector $b$ and the
projection (\(A\hat x\)) encoded in the projection matrix $P$ onto $C(A)$:
</p>
</div>

$$
\begin{equation}
b - Pb
\end{equation}
$$

We can rewrite that as:

$$
\begin{equation}
Ib - Pb
\end{equation}
$$

And factor out the vector $b$:

$$
\begin{equation}
b(I - P)
\end{equation}
$$

<div style="text-align: justify">
<p>So to project onto $N(A^T)$, we use the projection matrix $I - P$. We start
by projecting the 2nd column onto $N(A^T)$ of the 1st. This new vector is
orthogonal to the 1st, which is what we want. We do the same with the rest of
the columns, so that now the 1st column is orthogonal to every other
column.</p>

<p>Next we repeat the procedure with our partially orthogonalised matrix,
aiming to make the 3rd, 4th... nth columns orthogonal to the <i>2nd column</i>
(in addition to the 1st). We repeat this procedure for the 3rd column... and
onwards until every column is orthogonal to every other.</p>

<p>The matrix that reassembles $A$ from $Q$ is upper triangular and denoted
$R$. The reason for $R$ being upper triangular is that the more rightward
columns of $A$ have undergone more projections. This means they are represented
by a combination of more columns of $Q$ and so need more non-zero rows of $R$
to provide the combining weights. Since $A = QR$, we can recover $R = Q^TA$
(since $Q^{-1} = Q^T$) at the end of the Gram-Schmidt procedure.</p>
</div>
\begin{equation}
