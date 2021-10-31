## Zero-center

<div style="text-align: justify">
<p>It is often useful to normalise data. One type of normalisation is to 'zero
center' the data by subtracting it's mean. This will yield data with a new mean
of zero. Often we want to do this separately for each column or row of a
matrix. Also it's often the case that we want to perform this operation on a
square matrix. In that case, we can multiply by a 'centering matrix':</p> 
</div>

$$ C = I - \frac{1}{N} $$

$$
C = %
  \begin{bmatrix}
    1 & 0 & 0 \\[5pt]
    0 & 1 & 0 \\[5pt]
    0 & 0 & 1 \\
  \end{bmatrix}
    %
    -%
  \begin{bmatrix}
    -\frac{1}{3} & -\frac{1}{3} & -\frac{1}{3} \\[5pt]
    -\frac{1}{3} & -\frac{1}{3} & -\frac{1}{3} \\[5pt]
    -\frac{1}{3} & -\frac{1}{3} & -\frac{1}{3}
  \end{bmatrix}
  %
  =%
  \begin{bmatrix}
    \frac{2}{3} & -\frac{1}{3} & -\frac{1}{3} \\[5pt]
    -\frac{1}{3} & \frac{2}{3} & -\frac{1}{3} \\[5pt]
    -\frac{1}{3} & -\frac{1}{3} & \frac{2}{3}
  \end{bmatrix}
$$
$$
CA =%
  \begin{bmatrix}
    \frac{2}{3} & -\frac{1}{3} & -\frac{1}{3} \\[5pt]
    -\frac{1}{3} & \frac{2}{3} & -\frac{1}{3} \\[5pt]
    -\frac{1}{3} & -\frac{1}{3} & \frac{2}{3}
  \end{bmatrix}
  \begin{bmatrix}
    1 & 1 & 1\\[5pt]
    0 & 2 & 0\\[5pt]
    0 & 3 & -4
  \end{bmatrix}
  %
  =%
  \begin{bmatrix}
     \frac{2}{3} & -1 & 2 \\[5pt]
    -\frac{1}{3} & 0 & 1 \\[5pt]
    -\frac{1}{3} & 1 & -3
  \end{bmatrix}
$$

<div style="text-align: justify">
<p>Here the matrix $C$ had the effect of subtracting $1/3$ from the first
column, subtracting $2/3$ from the second column, and adding $1$ to the last
column - ensuring that all columns sum to zero.</p>

We create a function to build the centering matrix:
</div>

{% highlight python %}

def gen_centering(size):
    size_mat = la.gen_mat(size, values=[1/size[0]])
    return la.eye(size).subtract(size_mat)

{% endhighlight %}

<div style="text-align: justify">
<p>We then define a function that can zero center each column, each row, or
that matrix as a whole (if axis=2). If the matrix is square, then we use the
centering matrix approach above. Otherwise, after taking the mean across the
relevant axis (columns, rows, or all elements), we make a matrix of the same
size but filled with the mean of each axis and subtract it off the original
matrix:</p>
</div>

{% highlight python %}

def zero_center(A, axis=0):
    if axis == 2:
        global_mean = mean(mean(A)).data[0][0]
        return A.subtract(global_mean)
    elif axis == 1:
        A = A.transpose()
    if A.is_square():
        A = gen_centering(la.size(A)).multiply(A)
    else:
        A_mean = mean(A)
        ones = la.gen_mat([la.size(A)[0], 1], values=[1])
        A_mean_mat = ones.multiply(A_mean)
        A = A.subtract(A_mean_mat)
    if axis == 1:
        A = A.transpose()
    return A
{% endhighlight %}

### Demo

<div style="text-align: justify">
<p>We create a matrix, call the zero center method twice with a different axis
as an argument and print the results (we only print 2 decimal places in one
case to make it look pretty):</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[1, 2, 3],
            [-2, 1, 4],
            [0, 1, 2],
            [3, 6, 1]])

B = la.Mat([[1, 1, 1],
            [0, 2, 0],
            [0, 3, -4]])

result = la.stats.zero_center(A)
la.print_mat(result)

result = la.stats.zero_center(A, axis=1)
la.print_mat(result, 2)

result = la.stats.zero_center(B)
la.print_mat(result, 2)

{% endhighlight %}

Outputs:

{% highlight shell %}

>>> la.print_mat(result)
[0.5, -0.5, 0.5]
[-2.5, -1.5, 1.5]
[-0.5, -1.5, -0.5]
[2.5, 3.5, -1.5]

>>> la.print_mat(result, 2)
[-1.0, 0.0, 1.0]
[-3.0, 0.0, 3.0]
[-1.0, 0.0, 1.0]
[-0.33, 2.67, -2.33]

>>> la.print_mat(result, 2)
[0.67, -1.0, 2.0]
[-0.33, 0.0, 1.0]
[-0.33, 1.0, -3.0]

{% endhighlight %}

[< Sum and mean](./sum_and_mean.md)\
[Variance, covariance, standard deviation and standard error >](./var_covar_stddev_stderr.md)

[back to project main page](./stats_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/stats_from_scratch/zero_center_and_zscore.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

