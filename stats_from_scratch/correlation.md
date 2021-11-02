# Pearson's correlation 
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
standard deviations:</p>
</div>

$$
\begin{bmatrix}
    \sigma_1 & 0 & 0 \\
    0 & \sigma_2 & 0 \\
    0 & 0 & \sigma_3
\end{bmatrix}
%
\begin{bmatrix}
    v_{1,1} & v_{1,2} & v_{1,3} \\
    v_{2,1} & v_{2,2} & v_{2,3} \\
    v_{3,1} & v_{3,2} & v_{3,3}
\end{bmatrix}
%
\begin{bmatrix}
    \sigma_1 & 0 & 0 \\
    0 & \sigma_2 & 0 \\
    0 & 0 & \sigma_3
\end{bmatrix}
=%
\begin{bmatrix}
    \rho_{1,1} & \rho_{1,2} & \rho_{1,3} \\
    \rho_{2,1} & \rho_{2,2} & \rho_{2,3} \\
    \rho_{3,1} & \rho_{3,2} & \rho_{3,3}
\end{bmatrix}
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
A =%
\begin{bmatrix}
    1 & 2 & 3 \\
    2 & 3 & 1 \\
    3 & 3 & 0 \\
    4 & 5 & 1 \\
    5 & 6 & -1
\end{bmatrix}
$$

<div style="text-align: justify">
<p>Doing the computations, we see that this is indeed the case:</p>
</div>

$$
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
$$

<div style="text-align: justify">
<p>In matrix notation, we have:</p>
</div>

$$
K^{-\frac{1}{2}} V K^{-\frac{1}{2}} = \text{correlation matrix}
$$

<div style="text-align: justify">
<p>Where $V$ is the covariance matrix, and $K$ is a diagonal matrix containing
the variance of each variable (thus $K^{-\frac{1}{2}}$ takes the reciprocal of
the square root of each element on the diagonal, yielding the reciprocal of the
standard deviation).</p>
</div>

## Code implementation
<div style="text-align: justify">
<p>We compute the covariance matrix, take the variance values from the diagonal
and take the reciprocal of the square root and store them on a diagonal matrix
K. Then we do the multiplications before returning the correlation matrix:</p>
</div>

{% highlight python %}

def corr(A, axis=0):
    V = covar(A, axis)
    sds=[1/sqrt(x) for x in V.diag()]
    K_sqrt = la.gen_mat([len(sds)]*2, values=sds, type='diag')
    correlations = K_sqrt.multiply(K).multiply(K_sqrt)
    return correlations

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create a matrix, call the corr method and print the result:</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[1, 2, 3],
            [2, 3, 1],
            [3, 3, 0],
            [4, 5, 1],
            [5, 6, -1]])

la.print_mat(la.stats.corr(A), 2)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.stats.corr(A), 2)
[1.0, 0.96, -0.85]
[0.96, 1.0, -0.74]
[-0.85, -0.74, 1.0]

{% endhighlight %}


[< Z-score](./zscore.md)

[back to project main page](./stats_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/stats_from_scratch/correlation.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

