# Class, standalone functions and miscellaneous methods (2/3)
## Miscellaneous methods 
### Is matrix lower triangular?
<div style="text-align: justify">
<p>A matrix is 'lower triangular' if all the entries with column indices greater
than row indices are zero:</p>

$$
  \begin{bmatrix}
  1 & 0 & 0 \\
  0 & 5 & 0 \\
  7 & 8 & 0
  \end{bmatrix}
$$

</div>

#### Code implementation
<div style="text-align: justify">
<p>We loop over each element in the upper triangular region and if we find a
non-zero we return False, otherwise we return True:</p>
</div>

{% highlight python %}

def is_lower_tri(self):
    A = dc(self)
    for idx, row in enumerate(A.data):
        for col in range(idx+1,len(row)):
            if row[col] != 0:
                return = False
    else:
        return True

{% endhighlight %}

### Is matrix upper triangular?
<div style="text-align: justify">
<p>Similary, a matrix is 'upper triangular' if all the entries with row
indices greater than column indices are zero:</p>

$$
  \begin{bmatrix}
  1 & 3 & 0 \\
  0 & 5 & -4 \\
  0 & 0 & 1 
  \end{bmatrix}
$$

</div>

#### Code implementation
<div style="text-align: justify">
<p>Here we simply call the is_lower_tri method on the transposed matrix:</p>
</div>

{% highlight python %}

def is_upper_tri(self):
    A = dc(self)
    return A.transpose().is_lower_tri()

{% endhighlight %}

### Is matrix diagonal?
<div style="text-align: justify">
<p>If a matrix has zeros wherever the row and column indices are not equal,
then the matrix is 'diagonal':</p>

$$
  \begin{bmatrix}
  1 & 0 & 0 \\
  0 & 5 & 0 \\
  0 & 0 & 1
  \end{bmatrix}
$$

</div>

#### Code implementation
<div style="text-align: justify">
<p>If the matrix qualifies as both lower and upper, then it must be diagonal.
Therefore we use the previous two methods like so:</p>
</div>

{% highlight python %}

def is_diag(self):
    A = dc(self)
    if A.is_lower_tri() and A.is_upper_tri():
        return True
    else:
        return False

{% endhighlight %}

### Is matrix symmetric?
<div style="text-align: justify">
<p>If a matrix has the same values for every entry in $a_{ij}$ as in $a_{ji}$,
then that matrix is symmetric:</p>

$$
  \begin{bmatrix}
  2 & 9 & 3 \\
  9 & 5 & -2 \\
  3 & -2 & 1
  \end{bmatrix}
$$

</div>

#### Code implementation
<div style="text-align: justify">
<p>We loop over two ranges - one being the number of rows/columns, and the
other being one less than that (since we don't need to check diagonal entries).
If we find any $a_{ij} \neq a_{ji}$, we return False, otherwise we return
True:</p>
</div>

{% highlight python %}

def is_symmetric(self):
    A = dc(self)
    for i in range(size(A)[0]):
        for j in range(i+1, size(A)[0]):
            if A.data[i][j] != A.data[j][i]:
                return False
    else:
        return True

{% endhighlight %}

[< The Mat(rix) Class, generation, and printing](./class_and_standalone_functions_-_class_gen_print.md)\
[Combining matrices and getting the diagonal >](./class_and_standalone_functions_-_comb_diag.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/class_and_standalone_functions.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

