## Zero-center and z-scoring

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

def gen_centering(size):
    size_mat = la.gen_mat(size, values=[1/size[0]])
    return la.eye(size).subtract(size_mat)

def zero_center(A, axis=0):
    if axis == 1 or la.size(A)[0]==1:
        return A.multiply(gen_centering(la.size(A)))
    else:
        return gen_centering(la.size(A)).multiply(A)
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

[< Sum and mean](./sum_and_mean.md)\
[Variance, covariance, standard deviation and standard error >](./var_covar_stddev_stderr.md)

[back to project main page](./stats_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/stats_from_scratch/template.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

