# Eigenvalues and eigenvectors
## Eigenvalues
<div style="text-align: justify">
<p>At this point in my studies, I have learned about eigenvalues and how to
discover them in the context of the determinant (reviewed below) but this
method is not practical for size >3 matrices. Therefore, I had to skip ahead to
quickly implement the algorithms for finding eigenvalues (and the corresponding
eigenvectors). This means I don't have a deep understanding of how these
algorithms work so I'll postpone the usual description of how the code works
until later, and instead focus on what I understand theoretically.</p>

<p>Thinking of a matrix $A$ as encoding a linear transformation of a vector
space, any vector $x$ that points in the same direction after the
transformation (i.e. after the multiplication $Ax$) as before it are called
eigenvectors. The amount by which their length is changed is called the
eigenvalue (typically denoted with $\lambda$). Typically we think of the
eigenvalues and eigenvectors as properties of the matrix $A$. You can also look
at eigenvalues as the roots of a polynomial, which comes from the determinant.
We have 2 unknowns to find: $x$ and $\lambda$:</p>
</div>

$$
Ax = \lambda x
$$

<p>The first thing we do is rewrite the equation:</p>
</div>

$$
Ax = \lambda Ix
$$

<div style="text-align: justify">
<p>Then rearrange:</p>
</div>

$$
Ax - \lambda Ix = 0
$$

<div style="text-align: justify">
<p>Factoring out the $x$:</p>
</div>

$$ 
(A - \lambda I)x = 0
$$

<div style="text-align: justify">
<p>This tells us that the matrix $(A - \lambda I)$ is singular, which means its
determinant is zero.</p>
</div>


<div style="text-align: justify">
<p>In the 2 by 2 case we have:</p>
</div>

$$ 
  \begin{bmatrix}
    a - \lambda & b \\
    c & d - \lambda
  \end{bmatrix}
$$

<div style="text-align: justify">
<p>The determinant of that matrix is:</p>
</div>

$$
(a - \lambda)(d - \lambda) - (bc) = 0
$$

<div style="text-align: justify">
<p>Expanding, we see the familiar polynomial form:</p>
</div>

$$
\lambda^2 -(a + d)\lambda + (ad - bc) = 0
$$

<div style="text-align: justify">
<p>Notice the trace and the determinant appearing in the above equation:</p>
</div>

$$
\lambda^2 -(trace)\lambda + (determinant) = 0
$$

<div style="text-align: justify">
<p>We refactor that equation:</p>
</div>

$$
(\lambda - z_1)(\lambda - z_2) = 0
$$
 
<div style="text-align: justify">
<p>Where $z_1$ and $z_2$ are those numbers which bring about the trace and
determinant in the previous equation. Whatever $z_1$ and $z_2$ are, they must
be equal to $\lambda$ and therefore are the eigenvalues of the matrix.</p>
</div>

### Code implementation

{% highlight python %}

def eigvalues(self, epsilon = 0.0001, max_its=100):
    A = copy.deepcopy(self)
    if not (A.is_symmetric() or A.is_lower_tri() or A.is_upper_tri()):
        print('Matrix is not symmetric or triangular and may therefore have complex eigenvalues which this method cannot handle. Interpret results with care!')

    if A.is_upper_tri() or A.is_lower_tri():
        return Mat([A.diag()])
    if A.is_singular():
        print('Matrix is singular!')
        return None

    old_eig = 0
    final_eigs = []
    for its in range(max_its):

        # obtain off diagonal zeros
        _, E, _, _, _, _ = A.elimination()
        Einv = E.inverse()
        A = E.multiply(A).multiply(Einv)

        # shift A by -cI, where c is last diag
        shift = eye(size(A)).scale(old_eig)

        # QR factorisation
        A = A.subtract(shift)
        _, Q, R = A.qr()
        A = R.multiply(Q)
        A = A.add(shift)

        current_eig = A.diag()[-1]
        diff = old_eig - current_eig
        old_eig = current_eig
        if abs(diff) < epsilon:
            if min(size(A)) == 2:
                final_eigs += A.diag()
                return Mat([final_eigs])
            else:
                final_eigs.append(current_eig)
                A = A.data[:-1]
                A = [row[:-1] for row in A]
                A = Mat(A)
                old_eig = A.diag()[-1]
    else:
        print('Did not converge!')
        return None

{% endhighlight %}

### Demo

<div style="text-align: justify">
<p>We create a matrix, call the eigvalues method and print the result:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
         [2, 4, 4],
         [3, 4, 5]])

evals = A.eigvalues()

print_mat(evals,2)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print_mat(evals, 2)
[-0.61, 9.95, 0.65]

{% endhighlight %}

## Eigenvectors

### Code implementation

{% highlight python %}

def eig(self, epsilon=0.0001, max_its=100):
    A = copy.deepcopy(self)
    if A.is_singular():
        print('Matrix is singular!')
        return None, None
    evals = A.eigvalues()
    evects = []
    for evalue in evals.data[0]:
        # ensure we don't destroy the diagonal completely
        if evalue in A.diag():
            evalue -= 1e-12
        A_shifted = A.subtract(eye(size(A)).scale(evalue))
        # A_shifted_inv = A_shifted.inverse()
        b = gen_mat([size(A)[0],1],1)
        b = b.norm()
        for its in range(max_its):
            old_b = copy.deepcopy(b)
            b = A_shifted.backsub(b)
            # b = A_shifted_inv.multiply(b)
            b = b.norm()
            diff1 = b.subtract(old_b)
            diff2 = b.subtract(old_b.scale(-1))
            if diff2.length() or diff2.length() < epsilon:
                evects.append(b.transpose().data[0])
                break
    evects = Mat(evects).transpose()
    return evects, evals

{% endhighlight %}

### Demo

<div style="text-align: justify">
<p>We create a matrix, call the eig method and print the results. Then we check
that an eigenvector multiplied by $A$ gives the same result as the eigenvector
scaled by the eigenvalue:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
         [2, 4, 4],
         [3, 4, 5]])

evects, evals = A.eig()

print_mat(evals, 2)
print_mat(evects,2)

# extract the first eigenvector
evect = la.Mat([evects.transpose().data[0]]).transpose()
# multiply eigenvector by A and print result
print_mat(A.multiply(evect),2)
# scale eigenvector by eigenvalue and print result
print_mat(evect.scale(evals.data[0][0]),2)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print_mat(evals, 2)
[-0.61, 9.95, 0.65]

>>> print_mat(evects,2)
[-0.86, 0.37, 0.35]
[-0.07, 0.6, -0.8]
[0.51, 0.71, 0.49]

>>> print_mat(A.multiply(evect),2)
[0.53]
[0.04]
[-0.31]

>>> print_mat(evect.scale(evals.data[0][0]),2)
[0.53]
[0.04]
[-0.31]

{% endhighlight %}

[< A = QR](./qr_factorisation.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/eigen.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

