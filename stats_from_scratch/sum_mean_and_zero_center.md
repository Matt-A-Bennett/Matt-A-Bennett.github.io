# Sum, mean and zero-center
## Sum
<div style="text-align: justify">
<p>Summing all the values in each column, or in each row, of a matrix is a
common operation. We can achieve it my multiplying the matrix with a vector of
ones: multiplying on the left side will sum the columns, multiplying on the
right will sum the rows.</p>

<p>In our function, we will always multiply on the left, and therefore
transpose the matrix in the case that we want the sum the rows. If a vector is
passed, we always sum the elements:</p>
</div>

{% highlight python %}

def sum(A, axis=0):
    # if we have a vector, we sum along it's length
    if min(la.size(A)) == 1:
        axis = la.size(A).index(max(la.size(A)))
    if axis == 1:
        A = A.transpose()
    ones = la.gen_mat([1,la.size(A)[0]],1)
    A_sum = ones.multiply(A)
    return A_sum

{% endhighlight %}

### Demo

<div style="text-align: justify">
<p>We create a matrix, call the sum method twice with a different axis as an
argument and print the results:</p>
</div>

{% highlight python %}

import linalg as la
import stats as st
A = la.Mat([[1, 2, 3],
            [-2, 1, 4],
            [0, 1, 2],
            [3, 6, 1]])

result = st.sum(A)
la.print_mat(result)

result = st.sum(A, axis=1)
la.print_mat(result)

Outputs:

{% endhighlight %}

{% highlight console %}
>>> la.print_mat(result)
[2, 10, 10]

>>> la.print_mat(result)
[6, 3, 3, 10]

{% endhighlight %}

## Mean
<div style="text-align: justify">
<p>Now that we have a function to sum, we can divide the result by the number
of elements that went into the sum to obtain the mean:</p>
</div>

{% highlight python %}

def mean(A, axis=0):
    # if we have a vector, we take the mean along it's length
    if min(la.size(A)) == 1:
        axis = la.size(A).index(max(la.size(A)))
    A_sum = sum(A, axis)
    A_mean = A_sum.scale(1/la.size(A)[axis])
    return A_mean

{% endhighlight %}

### Demo

<div style="text-align: justify">
<p>We create a matrix, call the mean method twice with a different axis as an
argument and print the results (we only print 2 decimal places in one case to
make it look pretty):</p>
</div>

{% highlight python %}

import linalg as la
import stats as st
A = la.Mat([[1, 2, 3],
            [-2, 1, 4],
            [0, 1, 2],
            [3, 6, 1]])

result = st.mean(A)
la.print_mat(result)

result = st.mean(A, axis=1)
la.print_mat(result, 2)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(result)
[0.5, 2.5, 2.5]

>>> la.print_mat(result, 2)
[2.0, 1.0, 1.0, 3.33]

{% endhighlight %}

<div style="text-align: justify">
<p>It is often useful to normalise data. One type of normalisation is to 'zero
center' the data by subtracting it's mean. This will yield data with a new mean
of zero.</p>

<p>Here we define a function that can zero center each column, each row, or
that matrix as a whole (if axis=2). After taking the mean across the relevant
axis (columns, rows, or all elements), we make a matrix of the same size but
filled with the mean of each axis and subtract it off the original matrix:</p>
</div>

{% highlight python %}

def zero_center(A, axis=0):
    if axis == 2 or min(la.size(A))==1:
        A_mean = mean(mean(A)).data[0][0]
        A_mean_mat = la.gen_mat(la.size(A),A_mean)
    else:
        A_mean = mean(A, axis)
        ones = la.gen_mat([la.size(A)[0],1],1)
        A_mean_mat = ones.multiply(A_mean)
        if axis == 1:
            A_mean_mat = A_mean_mat.transpose()
    A = A.subtract(A_mean_mat)
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
import stats as st

A = la.Mat([[1, 2, 3],
            [-2, 1, 4],
            [0, 1, 2],
            [3, 6, 1]])

result = st.zero_center(A)
la.print_mat(result)

result = st.zero_center(A, axis=1)
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

{% endhighlight %}

[< Element-wise matrix manipulations](./element_wise_matrix.md)\
[Variance, covariance, standard deviation and standard error >](./var_covar_stddev_stderr.md)

[back to project main page](./stats_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/stats_from_scratch/sum_mean_and_zero_center.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

