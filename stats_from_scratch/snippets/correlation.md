<div style="text-align: justify">
<p> Pearson's correlation coefficient is closely related to the covariance - it
is normalised to fall between 1 and -1 by dividing by the product of the
standard deviations of the two variables being correlated. Thus, correlation
tells us how two variables tend to covary, but in 'standard', rather than
absolute, units. This is similar to how a z-score abstracts away from the
absolute scale of the raw scores. </p>

<p> In order to divide each value in the covariance matrix by the product of
the standard deviations of the two variables, we can multiply the covariance
matrix on the left and also on the right by a diagonal matrix containing the
reciprocal of the standard deviations:</p>
</div>

$$
\begin{equation}
\begin{bmatrix}
    \frac{1}{\sigma_1} & 0 & 0 \\
    0 & \frac{1}{\sigma_2} & 0 \\
    0 & 0 & \frac{1}{\sigma_3}
\end{bmatrix}
%
\begin{bmatrix}
    v_{1,1} & v_{1,2} & v_{1,3} \\
    v_{2,1} & v_{2,2} & v_{2,3} \\
    v_{3,1} & v_{3,2} & v_{3,3}
\end{bmatrix}
%
\begin{bmatrix}
    \frac{1}{\sigma_1} & 0 & 0 \\
    0 & \frac{1}{\sigma_2} & 0 \\
    0 & 0 & \frac{1}{\sigma_3}
\end{bmatrix}
=%
\begin{bmatrix}
    \rho_{1,1} & \rho_{1,2} & \rho_{1,3} \\
    \rho_{2,1} & \rho_{2,2} & \rho_{2,3} \\
    \rho_{3,1} & \rho_{3,2} & \rho_{3,3}
\end{bmatrix}
\end{equation}
$$

<div style="text-align: justify">
<p> For instance, with the matrix $A$ containing observations of 3 variables,
we can see by eye that the first column increases row by row, and so does the
2nd column. These two variables are positively correlated. The third column
<i>decreases</i> as we descend the rows, although not as linearly. This column
is therefore negatively correlated with the other two, though slightly less
strongly: </p>
</div>

$$
\begin{equation}
A =%
\begin{bmatrix}
    1 & 2 & 3 \\
    2 & 3 & 1 \\
    3 & 3 & 0 \\
    4 & 5 & 1 \\
    5 & 6 & -1
\end{bmatrix}
\end{equation}
$$

<div style="text-align: justify">
<p>Doing the computations, we see that this is indeed the case:</p>
</div>

$$
\begin{equation}
\begin{bmatrix}
    0.63 & 0 & 0 \\
    0 & 0.61 & 0 \\
    0 & 0 & 0.67
\end{bmatrix}
%
\begin{bmatrix}
    2.5 & 2.5 & -2.0 \\
    2.5 & 2.7 & -1.8 \\
    -2.0 & -1.8 & 2.2
\end{bmatrix}
%
\begin{bmatrix}
    0.63 & 0 & 0 \\
    0 & 0.61 & 0 \\
    0 & 0 & 0.67
\end{bmatrix}
=%
\begin{bmatrix}
    1.0 & 0.96 & -0.85 \\
    0.96 & 1.0 & -0.74 \\
    -0.85 & -0.74 & 1.0
\end{bmatrix}
\end{equation}
$$

<div style="text-align: justify">
<p>In matrix notation, we have:</p>
</div>

$$
\begin{equation}
K^{-\frac{1}{2}} V K^{-\frac{1}{2}} = \text{correlation matrix}
\end{equation}
$$

<div style="text-align: justify">
<p>Where $V$ is the covariance matrix, and $K$ is a diagonal matrix containing
the variance of each variable (thus $K^{-\frac{1}{2}}$ takes the reciprocal of
the square root of each element on the diagonal, yielding the reciprocal of the
standard deviation).</p>
</div>
