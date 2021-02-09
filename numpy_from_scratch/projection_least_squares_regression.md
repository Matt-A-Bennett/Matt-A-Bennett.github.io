# Projection, least squares and regression
<div style="text-align: justify">
<p>Often there is no solution to $Ax = b$. Usually in practical applications we
have a large set data points $b$ that we want to fit with a model - the columns
of $A$ - with only a few parameters - stored in $x$ - much fewer parameters than
we have data points. Our model matrix $A$ is tall and thin, and so has no
inverse! $x = A^{-1}b$ is not an option to find the parameters in $x$.</p>

<p>The data points contain some measurement error or 'noise' and we don't want
our model to fit this noise. We want out model to capture informative trends,
that will generalise to new data with different that will generalise to new
data with different noise. Therefore we have to accept some discrepancy between
our fitted model and the data. We want to minimise this 'model error' when we
fit.</p>

<p>Since we can't find an $x$ that satisfies $Ax = b$, we look for a 'best $x$'
that comes close: \(\hat x\). The $b$ doesn't fall into the column space of $A$
(henceforth $C(A)$) so we project $b$ to the closest point in that space. This
implies that the 'error' is the shortest vector $e$ needed to 'bridge the gap'
from $b$ to $C(A)$:</p>
</div>

$$
e = b - A\hat x
$$

<div style="text-align: justify">
<p>The vector $e$ is perpendicular to $C(A)$ and so is in the nullspace of
$A^T$ (henceforth $N(A^T)$):</p>
</div>

$$
A^T(b - A\hat x) = 0
$$

<div style="text-align: justify">
<p>The equation can be rearranged to:</p>
</div>

$$
A^Tb - A^TA\hat x = 0\\
= A^TA\hat x = A^Tb
$$

<div style="text-align: justify">
<p>This our best estimate of the parameters of the models:</p>
</div>

$$
\hat x = (A^TA)^{-1}A^Tb
$$

<div style="text-align: justify">
<p>And the vector that will be in the $C(A)$ (that is the 'predicted values' of
our model) is:</p>
</div>

$$
A\hat x = A(A^TA)^{-1}A^Tb
$$

<div style="text-align: justify">
<p>Thus we arrive at a matrix to 'project' some vector into $C(A)$:</p>
</div>

$$
P = A(A^TA)^{-1}A^T
$$

## Code implementation

<div style="text-align: justify">
<p>We define two methods, one that gives both the general projection matrix $P$
and the matrix that multiplies $b$ to give \(\hat x\):</p>
</div>

{% highlight python %}

def projection(self):
    # P = A((A'A)^-1)A'
    A = copy.deepcopy(self)
    At = self.transpose()
    AtA = At.multiply(A)
    AtAinv = AtA.inverse()
    AtAinvAt = AtAinv.multiply(At)
    for_x = copy.deepcopy(AtAinvAt)
    Projection = A.multiply(AtAinvAt)
    return Projection, for_x

{% endhighlight %}

<div style="text-align: justify">
<p>The second method gives the parameters for a straight line through a set of
data points in $b$. To do so, we create a matrix $A$ with as many rows as $b$
and two columns - the 1st column is all ones, and is the basis for the
intercept. The second incrementally increases and forms the basis for the
slope:</p>
</div>

{% highlight python %}

def linfit(self):
    # create a model
    A = gen_mat([len(self.data), 1])
    for i in range(len(self.data)):
        A.data[i] = [1, i]
    # project self onto model with least squares
    _, for_x = A.projection()
    fit = for_x.multiply(self)
    return fit

{% endhighlight %}

## Demo
<div style="text-align: justify">
<p>Below we try this method out on a small sample and plot the line:</p>
<p></p>
</div>

{% highlight python %}

import matplotlib.pyplot as plt
import numpy as np

b = Mat([[1,3,3,5,6,3,4,6,7,5,7,8,9]])
b = b.transpose()

fit = b.linfit()

print_mat(fit)

x = np.linspace(min(b.data[0])-2,len(b.data[0])+1,100)
y = fit.data[1]*x+fit.data[0]
plt.plot(x, y, '-r')
Xs = [i for i in range(len(b.data[0]))]
plt.plot(Xs, b.data[0], '.k')
plt.xlim([min(b.data[0])-2,len(b.data[0])])
plt.show()

{% endhighlight %}

_*

![regression plot)(./images/regression.png)

[< A = LU](./lu_factorisation.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/projection_least_squares_linfit.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

