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
        A = A.tr()
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
        A = A.tr()
    if A.is_square():
        A = gen_centering(la.size(A)).multiply(A)
    else:
        A_mean = mean(A)
        ones = la.gen_mat([la.size(A)[0], 1], values=[1])
        A_mean_mat = ones.multiply(A_mean)
        A = A.subtract(A_mean_mat)
    if axis == 1:
        A = A.tr()
    return A

def covar(A, axis=0, sample=True):
    if axis == 1:
        A = A.tr()
    A_zc = zero_center(A)
    A_cov = A_zc.tr().multiply(A_zc)
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

def zscore(A, axis=0, sample=False):
    A_zc = zero_center(A, axis)
    A_sd = sd(A_zc, axis, sample)
    if axis == 1:
        A_sd_rep = la.tile(A_sd, axes=[1, la.size(A)[1]])
    else:
        A_sd_rep = la.tile(A_sd, axes=[la.size(A)[0], 1])
    return A_zc.div_elwise(A_sd_rep)

def corr(A, axis=0):
    K = covar(A, axis)
    sds=[1/sqrt(x) for x in K.diag()]
    K_sqrt = la.gen_mat([len(sds)]*2, values=sds, type='diag')
    correlations = K_sqrt.multiply(K).multiply(K_sqrt)
    return correlations

def ttest_one_sample(A, axis=0, H=0):
    A_diff = mean(A, axis).subtract(H)
    A_se = se(A, axis, sample=True)
    ts = A_diff.div_elwise(A_se)
    df = A.size(axis)-1
    return ts, df

def ttest_paired(u, v):
    A_diff = u.subtract(v)
    t, df = ttest_one_sample(A_diff)
    return t.make_scalar(), df

def ttest_welchs(u, v):
    diff = mean(u).subtract(mean(v)).make_scalar()
    u_se, v_se = se(u).make_scalar(), se(v).make_scalar()
    t = diff / sqrt(u_se**2 + v_se**2)

    # compute degrees of freedom by Welch–Satterthwaite equation
    Nu, Nv = u.size(0), v.size(0)
    u_sd, v_sd = sd(u).make_scalar(), sd(v).make_scalar()

    df =          ( (u_sd**2/Nu + v_sd**2/Nv)**2 /
    (u_sd**4 / (Nu**2 * (Nu-1)) + v_sd**4 / (Nv**2 * (Nv-1))) )

    return t, df

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

