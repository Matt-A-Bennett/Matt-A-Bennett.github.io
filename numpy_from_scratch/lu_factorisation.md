# A = LU
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

## Code implementation
<div style="text-align: justify">
<p>The method I use here is needlessly inefficient since we call the
elimination method 3 times (since our inverse method calls it twice!), when it
is easy to simply inject the multiplying values into $L$ as we do a single pass
of elimination. However, at the moment this project is only about learning how
to write classes and methods and secondarily to solidify my grasp of linear
algebra. In the code we account for row exchanges by multiplying $E$ with $P$
(i.e. the permutation matrix), then taking the inverse of $E$ to get $L$.
Similarly, we ensure $L$ is lower triangular using $P$:</p>
</div>

{% highlight python %}

def lu(self):
    A = copy.deepcopy(self)
    P, E, A, U, _, _ = A.elimination()
    E = P.multiply(E)
    L = E.inverse()
    L = P.multiply(L)
    return A, P, L, U

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create a matrix, call the lu method and print the result:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
         [4, 8, 6],
         [7, 8, 9]])

A, P, L, U = A.lu()
print_mat(A)
print_mat(P)
print_mat(L)
print_mat(U)
PL = P.multiply(L)
PLU = PL.multiply(U)
print_mat(PL)
print_mat(PLU)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print_mat(A)
[1, 2, 3]
[4, 8, 6]
[7, 8, 9]

>>> print_mat(P)
[1, 0, 0]
[0, 0, 1]
[0, 1, 0]

>>> print_mat(L)
[1.0, 0.0, 0.0]
[7.0, 1.0, 0.0]
[4.0, 0.0, 1.0]

>>> print_mat(U)
[1.0, 2.0, 3.0]
[0.0, -6.0, -12.0]
[0.0, 0.0, -6.0]

>>> print_mat(PL)
[1.0, 0.0, 0.0]
[4.0, 0.0, 1.0]
[7.0, 1.0, 0.0]

>>> print_mat(PLU)
[1.0, 2.0, 3.0]
[4.0, 8.0, 6.0]
[7.0, 8.0, 9.0]

{% endhighlight %}

[< Inverse](./inverse.md)\
[Projection and regression >](./projection_and_regression.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/lu_factorisation.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

