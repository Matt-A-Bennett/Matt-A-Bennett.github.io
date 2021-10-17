# Diagonalisation of a matrix
<div style="text-align: justify">
<p>A very important factorisation of a square non-singular matrix $A$:</p>

$$
A = X\Lambda X^{-1}
$$

<p>where $X$ contains the eigenvectors and $\Lambda$ is a diagonal matrix
containing the eigenvalues. This can be seen from:</p>

$$
AX = X\Lambda
$$

<p>When $A$ multiplies any eigenvector $x_1$ (any column of $X$) we get the
original vector scaled by some number:</p>

$$
x_1\lambda
$$

<p>So we can 'move' the $X$ to the right hand side like so:</p>

$$
AX = X\Lambda\\
AXX^{-1} = X\Lambda X^{-1}\\
A = X\Lambda X^{-1}\\
$$

<p> This shows why $A$ must be square and non-singular - the eigenvectors must
be independent to allow $X^{-1}$ to exist.</p>
</div>

## Code implementation

<div style="text-align: justify">
<p>We compute the eigenvalues and eigenvectors of $A$, and store the
eigenvalues on the diagonal of a matrix 'eigval_mat' (the matrix $\Lambda$
above). Next, we need to compute the inverse of the eigenvector matrix. If the
matrix $A$ is symmetric, then we know that the eigenvectors will be orthogonal,
and the inverse is simply the transpose. If not, then we have to compute the
inverse from scratch.</p>
</div>

{% highlight python %}

def eigdiag(self):
    A = dc(self)
    evects, evals = A.eig()
    eigval_mat = gen_mat(size(A), values=evals.data[0], type='diag')
    if A.is_symmetric():
        evectsinv = evects.transpose()
    else:
        evectsinv = evects.inverse()
    return evects, eigval_mat, evectsinv

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create a matrix, call the 'eigdiag' method and print the results. We also
'reconstruct' the matrix $A$ from $X\Lambda X^{-1}$ (note there are some
rounding errors):</p>
</div>

{% highlight python %}

A = Mat([[1, 1, 3],
        [2, 2, 4],
        [5, 2, 6]])

evec, eigval, evecinv = A.eigdiag()
print_mat(evec,4)
print_mat(eigval,4)
print_mat(evecinv,4)
print_mat(evec.multiply(eigval).multiply(evecinv),5)

{% endhighlight %}

Outputs:

{% highlight console %}
 
>>> evec, eigval, evecinv = A.eigdiag()
Matrix is not symmetric or triangular and may therefore have complex
eigenvalues which this method cannot handle. Interpret results with care!

>>> print_mat(evec,4)
[-0.7299, -0.34, 0.0443]
[-0.3156, -0.5135, -0.9495]
[0.6063, -0.7878, 0.3106]

>>> print_mat(eigval,4)
[-1.0598, 0, 0]
[0, 9.4614, 0]
[0, 0, 0.5984]

>>> print_mat(evecinv,4)
[-1.0682, 0.0833, 0.4067]
[-0.5622, -0.2984, -0.8321]
[0.6591, -0.9195, 0.3148]

>>> print_mat(evec.multiply(eigval).multiply(evecinv),4)
[0.99994, 1.00009, 2.99997]
[1.99994, 2.00009, 3.99997]
[4.99994, 2.00009, 5.99997]

{% endhighlight %}

[< Eigenvalues and eigenvectors](./eigen.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/diagonalisation.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

