# Pivots, rank, singularity, determinant
## Pivots
<div style="text-align: justify">
<p>Now that we have the method of elimination, we can get a lot of information
about a matrix easily. The pivots of a matrix are the non-zero numbers sitting
along the diagonal of $U$ after elimination. Here we return those pivots along
with the columns in which they were found:</p>
</div>

{% highlight python %}

def pivots(self):
    A = copy.deepcopy(self)
    # find U
    _, _, _, U, _, _ = A.elimination()
    # extract the non-zeros on the diagonal
    diag_vals = U.diag()
    pivot_info = [(i, val) for i, val in enumerate(diag_vals) if val]
    return pivot_info


{% endhighlight %}

### Demo
<div style="text-align: justify">
<p>We create two matrices, call the pivots method and print the results:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
         [4, 5, 6],
         [5, 8, 9]])

B = Mat([[1, 2, 3],
         [4, 5, 6],
         [5, 7, 9]])

A_pivots = A.pivots()

B_pivots = B.pivots()

print(A_pivots)
print()
print(B_pivots)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(A_pivots)
[(0, 1), (1, -3.0), (2, -2.0)]

>>> print(B_pivots)
[(0, 1), (1, -3.0)]

{% endhighlight %}

## Rank
<div style="text-align: justify">
<p>The rank of a matrix tells us a huge amount, and is simply the number of
pivots:</p>
</div>

{% highlight python %}

def rank(self):
    A = copy.deepcopy(self)
    return len(A.pivots())

{% endhighlight %}

### Demo
<div style="text-align: justify">
<p>We create two matrices, call the rank method and print the results:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
         [4, 5, 6],
         [5, 8, 9]])

B = Mat([[1, 2, 3],
         [4, 5, 6],
         [5, 7, 9]])

A_rank = A.rank()

B_rank = B.rank()

print(A_rank)
print()
print(B_rank)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(A_rank)
3

>>> print(B_rank)
2

{% endhighlight %}

### Singularity
<div style="text-align: justify">
<p>The matrix is singular if during elimination row exchanges can't avoid a
zero in a pivot position. Our elimination method already returns a variable
indicating singularity, and so this next method just provides a cleaner way of
accessing that variable:</p>
</div>

{% highlight python %}

def is_singular(self):
    A = copy.deepcopy(self)
    _, _, _, _, singular, _ = A.elimination()
    return singular

{% endhighlight %}

### Demo
<div style="text-align: justify">
<p>We create two matrices, call the is_singular method and print the results:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
         [4, 5, 6],
         [5, 8, 9]])

B = Mat([[1, 2, 3],
         [4, 5, 6],
         [5, 7, 9]])

A_sing = A.is_singular()

B_sing = B.is_singular()

print(A_sing)
print()
print(B_sing)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(A_sing)
0
>>> print(B_sing)
1

{% endhighlight %}

### Determinant
<div style="text-align: justify">
<p>The determinant of a matrix is simply the product of the pivots, with a
negative sign if there were an odd number of row exchanges. Here we don't use
the pivot method we wrote, as we also need the number of row exchanges:</p>
</div>

{% highlight python %}

def determinant(self):
    A = copy.deepcopy(self)
    # find U
    _, _, _, U, _, row_exchange_count = A.elimination()
    # muliply the pivots
    det = 1
    diag_vals = U.diag()
    for val in diag_vals:
        det *= val
    # if an odd number of row exchanges, multiply determinant by minus one
    if row_exchange_count % 2:
        det *= -1
    return det

{% endhighlight %}

### Demo
<div style="text-align: justify">
<p>We create two matrices, call the determinant method and print the results:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
         [4, 5, 6],
         [5, 8, 9]])

B = Mat([[1, 2, 3],
         [4, 5, 6],
         [5, 7, 9]])

A_determinant = A.determinant()

B_determinant = B.determinant()

print(A_determinant)
print()
print(B_determinant)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print(A_determinant)
6.0

>>> print(B_determinant)
-0.0

{% endhighlight %}

[< Back substitution](./backsub.md)\
[Inverse >](./inverse.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/rank_piv_sing_det.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

