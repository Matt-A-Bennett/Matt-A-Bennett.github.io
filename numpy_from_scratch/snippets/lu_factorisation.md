<div style="text-align: justify">
<p>Having the inverse method allows to revisit $EA = U$ and move to a better
formulation of the same idea: $A = LU$. The matrix $L$ is lower triangular and
takes $U$ back to $A$ by applying the elimination steps in the reverse order.
The improvement of this formulation is that the elimination steps <i>don't
mix</i>. In $EA = U$ we see a $-10$ sitting in the (3,1) position of $E$:</p>
</div>

$$
  \begin{bmatrix}
    1 & 0 & 0 \\
    -2 & 1 & 0 \\
    -10 & 3 & 1
  \end{bmatrix}
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 5 & 5 \\
    4 & 5 & 6
  \end{bmatrix} =%
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & 1 & -1 \\
    0 & 0 & -9
  \end{bmatrix}
$$

<div style="text-align: justify">
<p>That $-10$ comes from the fact that we subtracted 4 of the 1st row from the
3rd, and subtracted 2 of 1st row from the 2nd, then added 3 of this <i>new 2nd
row</i> (effectively subtracting 6 of the 2nd row) from the 3rd: so overall $3
\times -2 -4 = -10$. When we reverse the order of those steps, applying them to
$U$ to get back to $A$, there is no such interference - all the multiples we
used during elimination show up in $L$:</p>
<p></p>
</div>

$$
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 5 & 5 \\
    4 & 5 & 6
  \end{bmatrix} =%
  \begin{bmatrix}
    1 & 0 & 0 \\
    2 & 1 & 0 \\
    4 & -3 & 1
  \end{bmatrix}
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & 1 & -1 \\
    0 & 0 & -9
  \end{bmatrix}
$$

<div style="text-align: justify">
<p>$L$ is just the inverse of $E$ (hence why it reverses the elimination
steps). We also have to reverse any row exchanges that we made in creating
$E$:</p>
</div>

$$
PEA = P\hat U
$$

$$
  \begin{bmatrix}
    1 & 0 & 0 \\
    0 & 0 & 1 \\
    0 & 1 & 0
  \end{bmatrix}
  \begin{bmatrix}
    1 & 0 & 0 \\
    -2 & 1 & 0 \\
    -4 & 0 & 1
  \end{bmatrix}
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 4 & 5 \\
    4 & 5 & 6
  \end{bmatrix} =%
  \begin{bmatrix}
    1 & 0 & 0 \\
    0 & 0 & 1 \\
    0 & 1 & 0
  \end{bmatrix}
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & 0 & -1 \\
    0 & 1 & 0
  \end{bmatrix}
$$

$$
PEA = U
$$

$$
  \begin{bmatrix}
    1 & 0 & 0 \\
    0 & 0 & 1 \\
    0 & 1 & 0
  \end{bmatrix}
  \begin{bmatrix}
    1 & 0 & 0 \\
    -2 & 1 & 0 \\
    -4 & 0 & 1
  \end{bmatrix}
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 4 & 5 \\
    4 & 5 & 6
  \end{bmatrix} =%
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & 1 & 0 \\
    0 & 0 & -1
  \end{bmatrix}
$$

$$
A = (PE)^{-1}U = \hat LU
$$

$$
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 4 & 5 \\
    4 & 5 & 6
  \end{bmatrix} =%
  \begin{bmatrix}
    1 & 0 & 0 \\
    2 & 0 & 1 \\
    4 & 1 & 0
  \end{bmatrix}
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & 1 & 0 \\
    0 & 0 & -1
  \end{bmatrix}
$$

$$
A = PLU
$$

$$
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 4 & 5 \\
    4 & 5 & 6
  \end{bmatrix} =%
  \begin{bmatrix}
    1 & 0 & 0 \\
    0 & 0 & 1 \\
    0 & 1 & 0
  \end{bmatrix}
  \begin{bmatrix}
    1 & 0 & 0 \\
    4 & 1 & 0 \\
    2 & 0 & 1
  \end{bmatrix}
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & 1 & 0 \\
    0 & 0 & -1
  \end{bmatrix}
$$
