# Full Code
Below is all the code that we have written to date.

[back to project main page](./stats_from_scratch.md)\
[back to home](../index.md)

{% highlight python %}

import linalg.linalg as la
from math import sqrt

def sum(A, axis=0):
    # if we have a vector, we sum along it's length
    if min(la.size(A)) == 1:
        axis = la.size(A).index(max(la.size(A)))
    if axis == 1:
        A = A.transpose()
    ones = la.gen_mat([1,la.size(A)[0]],values=[1])
    A_sum = ones.multiply(A)
    return A_sum

def mean(A, axis=0):
    # if we have a vector, we take the mean along it's length
    if min(la.size(A)) == 1:
        axis = la.size(A).index(max(la.size(A)))
    A_sum = sum(A, axis)
    A_mean = A_sum.div_elwise(la.size(A)[axis])
    return A_mean

def gen_centering(size):
    if type(size) is int:
        size = [size, size]
    return la.eye(size).subtract(1/size[0])

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

def covar(A, axis=0, sample=True):
    if axis == 1:
        A = A.transpose()
    A_zc = zero_center(A)
    A_cov = A_zc.transpose().multiply(A_zc)
    N = la.size(A)[0] - sample
    A_cov = A_cov.div_elwise(N)
    return A_cov

def var(A, axis=0, sample=True):
    A_covar = covar(A, axis, sample)
    A_var = la.Mat([A_covar.diag()])
    return A_var

def sd(A, axis=0, sample=True):
    A_var = var(A, axis, sample)
    sds = A_var.function_elwise(sqrt)
    return sds

def se(A, axis=0, sample=True):
    sds = sd(A, axis, sample)
    N = la.size(A)[axis]
    ses = sds.div_elwise(sqrt(N))
    return ses

{% endhighlight %}

[back to project main page](./stats_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/stats_from_scratch/full_code.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

