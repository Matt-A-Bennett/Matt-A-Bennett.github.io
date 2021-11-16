<div style="text-align: justify">
<p>At this point in my studies, I have learned about eigenvalues and how to
discover them in the context of the determinant (reviewed below) but this
method is not practical for size >3 matrices. Therefore, I had to skip ahead to
quickly implement the algorithms for finding eigenvalues (and the corresponding
eigenvectors). At present the methods cannot handle complex numbers, and so
should be used for symmetric and triangular real matrices (since they always
have real eigenvalues). This means I don't have a deep understanding of how
these algorithms work so I'll postpone the usual description of how the code
works until later, and instead focus on what I understand theoretically.</p>

<p>Thinking of a matrix $A$ as encoding a linear transformation of a vector
space, any vector $x$ that points in the same direction after the
transformation (i.e. after the multiplication $Ax$) as before it is called an
eigenvector. The amount by which their length is changed is called the
eigenvalue (typically denoted with $\lambda$). Typically we think of the
eigenvalues and eigenvectors as properties of the matrix $A$. You can also view
eigenvalues as the roots of a polynomial, which comes from the determinant. We
have 2 unknowns to find: $x$ and $\lambda$:</p>

$$
\begin{equation}
Ax = \lambda x
\end{equation}
$$

<p>The first thing we do is rewrite the equation:</p>

$$
\begin{equation}
Ax = \lambda Ix
\end{equation}
$$

<p>Then rearrange:</p>

$$
\begin{equation}
Ax - \lambda Ix = 0
\end{equation}
$$

<p>Factoring out the $x$:</p>

$$ 
\begin{equation}
(A - \lambda I)x = 0
\end{equation}
$$

<p>This tells us that the matrix $(A - \lambda I)$ is singular, which means its
determinant is zero.</p>


<p>In the 2 by 2 case we have:</p>

$$ 
\begin{equation}
  \begin{bmatrix}
    a - \lambda & b \\
    c & d - \lambda
  \end{bmatrix}
\end{equation}
$$

<p>The determinant of that matrix is:</p>

$$
\begin{equation}
(a - \lambda)(d - \lambda) - (bc) = 0
\end{equation}
$$

<p>Expanding, we see the familiar polynomial form:</p>

$$
\begin{equation}
\lambda^2 -(a + dlambda + (ad - bc) = 0
\end{equation}
$$

<p>Notice the trace and the determinant appearing in the above equation:</p>

$$
\begin{equation}
\lambda^2 -(tracelambda + (determinant) = 0
\end{equation}
$$

<p>We refactor that equation:</p>

$$
\begin{equation}
(\lambda - z_1)(\lambda - z_2) = 0
\end{equation}
$$
\begin{equation}
 
<p>Where $z_1$ and $z_2$ are those numbers which bring about the trace and
determinant in the previous equation. Whatever $z_1$ and $z_2$ are, they must
be equal to $\lambda$ and therefore are the eigenvalues of the matrix.</p>
</div>
