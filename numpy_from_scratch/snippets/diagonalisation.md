<div style="text-align: justify">
<p>A very important factorisation of a square non-singular matrix $A$ is:</p>

$$
A = X\Lambda X^{-1}
$$

<p>Where $X$ contains the eigenvectors of $A$ and $\Lambda$ is a diagonal
matrix containing the eigenvalues. This can be seen from:</p>

$$
AX = X\Lambda
$$

<p>Since when $A$ multiplies any eigenvector $x_1$ (any column of $X$) we get
the original vector scaled by some number:</p>

$$
x_1\lambda
$$

<p>Therefore 'move' the $X$ to the right hand side like so:</p>

$$
AX = X\Lambda\\
AXX^{-1} = X\Lambda X^{-1}\\
A = X\Lambda X^{-1}\\
$$

<p> This shows why $A$ must be square and non-singular - the eigenvectors must
be independent for $X^{-1}$ to exist.</p>
</div>
