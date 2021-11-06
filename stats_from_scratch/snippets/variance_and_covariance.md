<div style="text-align: justify">
<p>The variance of a set of values $x$ is the sum of the squared deviation of
each value from the mean of all the values $\bar x$, divided by one less than
the number of observations (this gives the 'sample variance', whereas omitting
the $-1$ would instead give the 'population variance'. When $n$ is large, it
doesn't particularly matter). In essence it's the average squared deviation
from the mean in the data:</p>
</div>

$$ \sigma^2 = \frac{1}{n-1}\sum_{i=1}^n (x_i - \bar x)(x_i - \bar x) $$

<div style="text-align: justify">
<p>In matrix notation:</p>
</div>

$$ \text{covariance} = \frac{1}{m-1}(x - \bar x)^T (x - \bar x)$$

<div style="text-align: justify">
<p>We can compare the variation between two different variables and see if they
'covary' or not. This is called the covariance and is computed just like the
variance, only it's between two sets of observations $x$ and $y$. In essence
this is the average 'agreement' in the deviations from each variable's
mean:</p>
</div>

$$ \text{covariance} = \frac{1}{n-1}\sum_{i=1}^n (x_i - \bar x)(y_i - \bar y) $$

<div style="text-align: justify">
<p>In matrix notation:</p>
</div>

$$ \text{covariance} = \frac{1}{m-1}(x - \bar x)^T (y - \bar x) $$

<div style="text-align: justify">
<p>If we have observations of several variables, with each set of observations
forming a column of a matrix $A$, then computing all of the dot products
between each column is just what happens with $A^T A$. So if we use the
centering matrix to remove the mean of each set of observations with</p>
</div>

$$ (CA)^T C A = A^T C^T C A = A^T C A $$

<div style="text-align: justify">
<p>(since C is symmetric and idempotent) and
divide this by one less than the number of observations we get the 'covariance
matrix':</p>
</div>

$$ \text{covariance matrix} = \frac{1}{m-1} A^T CA $$ 

$$
\frac{1}{3}
  \begin{bmatrix}
    1 & 0 & 4 & 2 \\
    2 & -1 & 0 & 5 \\
    3  & 6 & 2  & 1
  \end{bmatrix}
  %
  \frac{1}{4}
  \begin{bmatrix}
    3, -1, -1, -1 \\
    -1, 3, -1, -1 \\
    -1, -1, 3, -1 \\
    -1, -1, -1, 3
  \end{bmatrix}
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & -1 & 6 \\
    4 & 0 & 2 \\
    2 & 5 & 1
  \end{bmatrix}
  =%
$$

$$
  \frac{1}{3}
  \begin{bmatrix}
    8.75 & 1.5 & -8 \\
    1.5 & 21 & -13 \\
    -8 & -13 & 14
  \end{bmatrix}
  =%
  \begin{bmatrix}
    2.1875 & 0.375 & -2 \\
    0.375 & 5.25 & -3.25 \\
    -2 & -3.25 & 3.5
  \end{bmatrix}
$$

<div style="text-align: justify">
<p>Note the variance $\sigma^2$ of each column sitting along the diagonal.</p>
</div>
