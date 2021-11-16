<div style="text-align: justify">
<p>The inverse of a square matrix $A$ is that matrix which multiples $A$ (on
either side) to give the identity matrix (not all matrices have inverses):</p>
</div>

$$
AA^{-1} = I
\end{equation}
$$

<div style="text-align: justify">
<p>A good way to find the inverse of a matrix is through elimination. Once we
have reached $EA = U$, we do a second round of elimination but 'upwards' to
clear out the upper triangular region of $U$, reaching a diagonal matrix. This
diagonal matrix is more similar to $I$, and by dividing each row appropriately
(using a matrix \(\hat D\)) it <i>is</i> $I$:</p>
</div>

$$ 
\begin{equation}
\hat EEA = \hat EU = D\hat D
\end{equation}
$$

<div style="text-align: justify">
<p>Below we just track the matrices $A$, $U$, and $D$ as we go from $A$ to
$I$:</p>
</div>
$$
\begin{equation}
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 5 & 4 \\
    3 & 8 & 9
  \end{bmatrix} \to %
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & 1 & -2 \\
    0 & 0 & -2
  \end{bmatrix} \to %
  \begin{bmatrix}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & -2
  \end{bmatrix} \to %
  \begin{bmatrix}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & 1
  \end{bmatrix}
\end{equation}
$$

<div style="text-align: justify">
<p>This means that there was some sequence of elimination steps which took $A$
to $I$. If we had applied those steps to $I$ we would have ended up at the
inverse of $A$!</p>

<p>So to compute the inverse of $A$, we do elimination on $A$, but we 'augment'
the matrix with $I$. This means that all row operations applied based on the
$A$ side of the matrix will also be applied to the $I$ side:</p>
</div>

$$ \left[
\begin{equation}
  \begin{array}{ccc|ccc}
    1 & 2 & 3 & 1 & 0 & 0 \\
    2 & 5 & 4 & 0 & 1 & 0 \\
    3 & 8 & 9 & 0 & 0 & 1  
  \end{array} 
  \right] \to%
  \left[
  \begin{array}{ccc|ccc}
    1 & 0 & 0 & 3.25 & 1.5 & -1.75 \\
    0 & 1 & 0 & -1.5 & 0 & 0.5 \\
    0 & 0 & 1 & 0.25 & -0.5 & 0.25
  \end{array} 
  \right]
\end{equation}
$$
\begin{equation}
