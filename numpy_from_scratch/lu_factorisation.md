# A = LU
<div style="text-align: justify">
<p>Having the inverse method allows to revisit EA = U and move to a better
formulation of the same idea: A = LU. The matrix L is lower triangular and
takes U back to A by applying the elimination steps in the reverse order. The
improvement of this formulation is that the elimination steps <i>don't mix</i>.
</p>

<p>L is just the inverse of E (hence why it reverses the elimination steps). We
also have to reverse any row exchanges that we made in creating E:</p>
</div>

$$
PEA = PV
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
A = (PE)^{-1}U = DU
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

## Code implementation
<div style="text-align: justify">
<p>This is achieved by taking the inverse of E to get L, and ensuring L is
lower triangular by accounting for row exchanges via a multiplication with P
(i.e. the permutation matrix):</p>
</div>

{% highlight python %}

def lu(self):
    P, E, self, U, _, _ = self.elimination()
    L = E.inverse()
    L = P.multiply(L)
    return self, P, L, U

{% endhighlight %}

[< Inverse](./inverse.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
