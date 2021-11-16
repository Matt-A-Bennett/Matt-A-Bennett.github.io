<div style="text-align: justify">
<p>Picking up from the last post on elimination, we represented a system of
equations in matrix form as $Ax = b$:</p>

$$
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

<p>We converted this to an equivalent system of equations $Ux = \hat b$ (Note
that the same elimination steps applied to $A$ are also applied to the rows of
$b$):</p>

$$
\begin{equation}
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
  = 
  \begin{bmatrix}
    0 \\
    -2 \\
    8
  \end{bmatrix}
\end{equation}
$$

<p>Now we can systematically solve for the components of $x$ with ease.
Clearly, $x_3$ must be $\frac{8}{-6} = -1.33$.</p>

<p>Solving for $x_2$ is easy in this example, since there is no $x_3$
coefficient, but if there was we could multiply $x_3$ by the coefficient to
arrive at the equation:</p>

$$
\begin{equation}
0 - 2x_2 + (z \times -1.33) = -2
\end{equation}
$$

<p>Where $z$ stands for some non-zero coefficient.</p>

<p>Rearranging:</p>

$$
\begin{equation}
0 - 2x_2 = -2 - (z \times -1.33)
\end{equation}
$$

<p>We then have $-2x_2 = something$ and can solve for $x_2$ easily. In our
actual case, we have $-2x_2 = -2$ and so clearly $x_2 = 1$.</p>

<p>The last row is more interesting:</p>

$$
\begin{equation}
x_1 + 2x_2 + 3x_3 = 0
\end{equation}
$$

<p>Substituting what we know already:</p>

$$
\begin{equation}
x_1 + 2 - 4 = 0
\end{equation}
$$

<p>And so:</p>

$$
\begin{equation}
x_1 = 2
\end{equation}
$$

<p>We see that our solutions work for the original system of equations:</p>

$$
\begin{equation}
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 2 & 6 \\
    4 & 5 & 6
  \end{bmatrix}
  %
  \begin{bmatrix}
    2 \\
    1 \\
    -1.33 
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

</div>
\begin{equation}
