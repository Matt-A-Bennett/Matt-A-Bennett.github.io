<div style="text-align: justify">
<p>Just what it sounds like. We will use $\odot$ and $\oslash$ to denote these
two operations:</p>
</div>

$$
A \odot B = 
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 0 & 0 \\
    4 & -2 & -1
  \end{bmatrix}
  \odot
  \begin{bmatrix}
    2 & 2 & 3 \\
    4 & 2 & 1 \\
    1 & 3 & 2
  \end{bmatrix} =
  \begin{bmatrix}
    2 & 4 & 9 \\
    8 & 0 & 0 \\
    8 & -6 & -2
  \end{bmatrix}
\end{equation}
$$

$$
\begin{equation}
A \oslash B = 
  \begin{bmatrix}
    1 & 2 & 3 \\[5pt]
    2 & 0 & 0 \\[5pt]
    4 & -2 & -1
  \end{bmatrix}
  \oslash
  \begin{bmatrix}
    2 & 2 & 3 \\[5pt]
    4 & 2 & 1 \\[5pt]
    1 & 3 & 2
  \end{bmatrix} =
  \begin{bmatrix}
    \frac{1}{2} & 1 & 1 \\[5pt]
    \frac{1}{2} & 0 & 0 \\[5pt]
    4 & -\frac{2}{3} & -\frac{1}{2}
  \end{bmatrix}
\end{equation}
$$

<div style="text-align: justify">
<p>Scalar multiplication, which <i>is</i> a legal operation in linear algebra,
is a simple matter of taking some matrix (or vector) and
multiplying all of its elements by some number (the scalar):</p>
</div>

$$
\begin{equation}
2A = 2
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 2 & 6 \\
    4 & 5 & 6
  \end{bmatrix}
  =
  \begin{bmatrix}
    2 & 4 & 6 \\
    4 & 4 & 12 \\
    8 & 10 & 12
  \end{bmatrix}
\end{equation}
$$
\begin{equation}
