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
    evects, evals = self.eig()
    eigval_mat = gen_mat(self.size(), values=evals.data[0], family='diag')
    if self.is_symmetric():
        evectsinv = evects.tr()
    else:
        evectsinv = evects.inverse()
    return evects, eigval_mat, evectsinv

{% endhighlight %}
