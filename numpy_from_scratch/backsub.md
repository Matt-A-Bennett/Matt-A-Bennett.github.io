# Back substitution
<div style="text-align: justify">
<p>Picking up from the last post on elimination, we represented a system of
equations in matrix form as $Ax = b$:</p>
</div>

$$
Ax = b =%
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 2 & 6 \\
    4 & 5 & 6
  \end{bmatrix}
  %
  \begin{bmatrix}
    x_1 \\
    x_2 \\
    x_3
  \end{bmatrix}
  %
  =%
  \begin{bmatrix}
    0 \\
    -2 \\
    5
  \end{bmatrix}
$$

<div style="text-align: justify">
<p>We converted this to an equivalent system of equations $Ux = \hat b$ (Note
that the same elimination steps applied to $A$ are also applied to the rows of
$b$):</p>
</div>

$$
  \begin{bmatrix}
    1 & 2 & 3 \\
    0 & -2 & 0 \\
    0 & 0 & -6
  \end{bmatrix}
  %
  \begin{bmatrix}
    x_1 \\
    x_2 \\
    x_3
  \end{bmatrix}
  %
  = 
  \begin{bmatrix}
    0 \\
    -2 \\
    8
  \end{bmatrix}
$$

<div style="text-align: justify">
<p>Now we can systematically solve for the components of $x$ with ease.
Clearly, x_3 must be $8/-6 = -1.33$.</p>

<p>Solving for $x_2$ is easy for this example, since there is no $x_3$
coefficient, but if there was we could multiply $x_3$ by the coefficient to
arrive at the equation:</p>
</div>

$$
0 - 2x_2 + (z \times -1.33) = -2
$$

<div style="text-align: justify">
<p>Where $z$ stands for some non-zero coefficient.</p>

<p>Rearranging:</p>
</div>

$$
0 - 2x_2 = -2 - (z \times -1.33)
$$

<div style="text-align: justify">
<p>We then have $-2x_2 = some number$ and can solve for $x_2$ easily. In our
actual case, we have $-2x_2 = -2$ and so clearly $x_2 = 1$.</p>

<p>the last row is more interesting:</p>
</div>

$$
x_1 + 2x_2 + 3x_3 = 0
$$

<div style="text-align: justify">
<p>Substituting what we know already:</p>
</div>

$$
x_1 + 2 - 4 = 0
$$

<div style="text-align: justify">
<p>And so:</p>
</div>

$$
x_1 = 2
$$

<div style="text-align: justify">
<p>We see that our solutions work for the original system of equations:</p>
</div>

$$
  \begin{bmatrix}
    1 & 2 & 3 \\
    2 & 2 & 6 \\
    4 & 5 & 6
  \end{bmatrix}
  %
  \begin{bmatrix}
    2 \\
    1 \\
    -1.33 
  \end{bmatrix}
  %
  =%
  \begin{bmatrix}
    0 \\
    -2 \\
    5
  \end{bmatrix}
$$

## Code implementation
<div style="text-align: justify">
<p>First we to run elimination on the augmented matrix $[A | b]$:</p>
</div>

{% highlight python %}

def backsub(self, b):
    A = copy.deepcopy(self)
    b = copy.deepcopy(b)
    augmented = cat(A, b)
    _, _, _, U, _, _ = augmented.elimination()

{% endhighlight %}

<div style="text-align: justify">
<p>Next we create a row or zeros for comparison purposes later in the code. We
also initiate a list that will contain the coefficients as they are solved.</p>
</div>

{% highlight python %}

zero_U_row = gen_mat([1,size(U)[1]-1]).data[0]
coeff = []

{% endhighlight %}

<div style="text-align: justify">
<p>We loop of the row indices in reverse order. For each step (apart from the
first), we take the previous coefficient and multiply the corresponding column
of U, then subtract the result from the current $b$. To do this, we use an
elimination matrix on the <i>right side</i> of $U$ (to manipulate the columns
rather than the rows):</p>
</div>

{% highlight python %}

for idx in range(-1, -(size(U)[0]+1), -1):
    if idx < -1:
        E = eye([size(U)[0]+1, size(U)[1]])
        E.data[idx][size(U)[1]-1] = -1*(coeff[-1])
        U = U.multiply(E)

{% endhighlight %}

<div style="text-align: justify">
<p>With the rearranged row we can attempt to solve for the unknown. There are a
number of possibilities. If we have a singular matrix, elimination will have
produced a row of zeros and in this case we can't solve for a non-zero in $b$.
If $b$ happens to contain a zero at this position, then any coefficient will
multiply to produce a zero and we have an infinite number of solutions. We
default to picking a coefficient of $1$ in this case. Otherwise, We solve for
the coefficient by dividing the $b$ term with term in the row:</p>
</div>

{% highlight python %}

row = U.data[idx]
# check solution possibilities
if row[:-1] == zero_U_row and row[-1] != 0:
   print('No solution!')
   return None
elif row[:-1] == zero_U_row and row[-1] == 0:
   print('Infinite solutions!')
   coeff.append(1)
else:
    coeff.append(row[-1]/row[idx-1])

{% endhighlight %}

<div style="text-align: justify">
<p>Since we solved for the coefficients in reverse order, we reverse our list,
and return a column vector of the coefficients:</p>
</div>

{% highlight python %}

coeffs = list(reversed(coeff))
return Mat([coeffs]).transpose()

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create a matrix, call the backsub method and print the result. We also
print the result of the multiplication $Ax$ to confirm that we get $b$:</p>
</div>

{% highlight python %}

A = la.Mat([[1, 2, 3],
            [2, 2, 6],
            [4, 5, 6]])

b = la.Mat([[0],[-2],[5]])

x = A.backsub(b)

print_mat(x, 2)
print_mat(A.multiply(x))

{% endhighlight %}

Outputs:

{% highlight shell %}

>>> print_mat(x, 2)
[2.0]
[1.0]
[-1.33]

>>> print_mat(A.multiply(x))
[0.0]
[-2.0]
[5.0]

{% endhighlight %}

[< EA = U](./elimination.md)
[Rank, pivots, singularity, determinant >](./rank_piv_sing_det.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/template.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
