<div style="text-align: justify">
<p>Solving a set of simultaneous equations (when there is an unique solution)
can be done by subtracting multiples of one from another such that an unknown
is 'eliminated'. By repeating this procedure, we can eliminate all but one
unknown from an equation, leaving a trivially easy solution of the remaining
unknown. Having found the value of that unknown, we can move to trivially
solving any equation involving two unknowns provided one of them is the one we
have previously solved. Continuing this procedure of 'back substitution' will
systematically solve for all the unknowns.</p>

For example, the equations:

$$
x_1 + 2x_2 + 3x_3 = 0 \\
2x_1 + 2x_2 + 6x_3 = -2 \\
4x_1 + 5x_2 + 6x_3 = 5
\end{equation}
$$

can be translated, after elimination, into:

$$
\begin{equation}
x_1 + 2x_2 + 3x_3 = 0 \\
0 - 2x_2 + 0 = -2 \\
0 + 0 - 6x_3 = 8
\end{equation}
$$

<p>In linear algebra, the procedure of elimination can be carried out by
multiplying a matrix $A$ of coefficients with an elimination matrix $E$. The
result is an upper triangular matrix $U$.</p>

The initial problem looks like:

$$
\begin{equation}
Ax = b =%
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 2 & 6 \\
    4 & 5 & 6
  \end{bmatrix}
  %
  \begin{bmatrix}
    x_1 \\
    x_2 \\
    x_3
  \end{bmatrix}
  %
  =%
  \begin{bmatrix}
    0 \\
    -2 \\
    5
  \end{bmatrix}
\end{equation}
$$

The elimination procedure looks like:

$$
\begin{equation}
Ux = EAx = Eb
\end{equation}
$$

$$
\begin{equation}
Ux = %
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & -2 & 0 \\
    0 & 0 & -6
  \end{bmatrix}
  %
  \begin{bmatrix}
    x_1 \\
    x_2 \\
    x_3
  \end{bmatrix}
  %
  = %
  \begin{bmatrix}
    0 \\
    -2 \\
    8
  \end{bmatrix}
\end{equation}
$$

<p>In the case that we find a zero sitting in a column above an unknown that we
want to eliminate, we can exchange the row with the zero with some row below
that doesn't have a zero in that column.</p>

<p>What we would like to do is encode the results of each elimination step in
the matrix $E$ and to have the result $U$ coming from the multiplication of $E$
with $A$.</p>
</div>
\begin{equation}
