# Class, standalone functions and miscellaneous methods (2/3)
## Miscellaneous methods 
### Is matrix square?
<div style="text-align: justify">
<p>A matrix is 'square' if it has the same number of rows as it does columns:</p>

$$
  \begin{bmatrix}
  1 & 2 & 3 \\
  4 & 5 & 6 \\
  7 & 8 & 9
  \end{bmatrix}
$$

</div>

#### Code implementation
<div style="text-align: justify">
<p>This is extremely simple:</p>
</div>

{% highlight python %}

def is_square(self):
    sizes = size(self)
    return sizes[0] == sizes[1]


{% endhighlight %}

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
    for idx, row in enumerate(self.data):
        for col in range(idx+1,len(row)):
            if row[col] != 0:
                return False
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
    return self.transpose().is_lower_tri()

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
    if self.is_lower_tri() and self.is_upper_tri():
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
    for i in range(size(self)[0]):
        for j in range(i+1, size(self)[0]):
            if self.data[i][j] != self.data[j][i]:
                return False
    else:
        return True

{% endhighlight %}

### Is matrix positive definite?
<div style="text-align: justify">
<p>If all the pivots of a matrix are strictly greater than zero, then the
matrix is positive definite. If they are greater than or equal to zero, then
the matrix is positive semi-definite. Similary, strictly less than zero means
the matrix is negative definite and if there are also some zeros then the
matrix is negative semi-definite.</p>
</div>

#### Code implementation
<div style="text-align: justify">
<p>We create a method that returns the base-10 integer representation of a
base-2 (i.e. binary) number. The binary number is constructed from the
TRUE/FALSE answers to 3 queries: whether the matrix contains any negative,
zero, or positive pivots. The answers to these 3 queries uniquely determine
what kind of 'definiteness' (if any) we can call the matrix. Thus the method
returns a number (between 0 and 7: since $2^3 = 8$ possibilities) which can be
used as a unique identifier of the 'definiteness':</p>
</div>

{% highlight python %}

def pivot_sign_code(self):
    ''' Returns number between 0 and 7 according to signs of pivots. We do
    this by constructing a 3-bit binary number, where each bit represents
    the presence/absence of negative, zero, or positive pivots, and then
    converting from binary to a base 10 integer.'''
    pivot_info = self.pivots().items()

    neg = int(any(piv[1] < 0 for piv in pivot_info))
    semi = int(any(piv[1] == 0 for piv in pivot_info))
    pos = int(any(piv[1] > 0 for piv in pivot_info))

    return int(str(neg) + str(semi) + str(pos), 2)

def is_negdef(self):
    return self.pivot_sign_code() == 4

def is_negsemidef(self):
    return self.pivot_sign_code() == 6

def is_possemidef(self):
    return self.pivot_sign_code() == 3

def is_posdef(self):
    return self.pivot_sign_code() == 1

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

