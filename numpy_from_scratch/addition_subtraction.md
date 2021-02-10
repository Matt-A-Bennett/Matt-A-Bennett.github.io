# Addition/Subtraction
<div style="text-align: justify">
<p>Addition and subtraction is valid between two same-shaped matrices and is
done element-wise:</p>
</div>

$$
A + B =%
  \begin{bmatrix}
    1 & 2 & 3 \\
    4 & 5 & 6
  \end{bmatrix}+%

  \begin{bmatrix}
    2 & 1 & 4 \\
    0 & 3 & 1
  \end{bmatrix}=%

  \begin{bmatrix}
    3 & 3 & 7 \\
    4 & 8 & 7
  \end{bmatrix}
$$
   
## Code implementation
<div style="text-align: justify">
<p>Here, the method is called from an initial matrix, with the second
matrix supplied as an argument. Then I simply loop over the rows of each
matrix, each time looping over the elements of those rows (i.e. the columns),
summing them and appending them to an added_rows variable.</p>
</div>

{% highlight python %}

def add(self, new_mat):
    A = copy.deepcopy(self)
    B = copy.deepcopy(new_mat)
    added_rows = []
    for rows in zip(A.data, B.data):
        added_cols = []
        for cols in zip(rows[0],rows[1]):
            added_cols.append(sum(list(cols)))
        added_rows.append(added_cols)
    A.data = added_rows
    return A

{% endhighlight %}

<div style="text-align: justify">
<p>In the case of the subtraction, we can simply reverse the signs for the second
matrix by applying a scalar multiplication with -1 and then call the add
method, thus achieving a subtraction.</p>
</div>

{% highlight python %}

def subtract(self, new_mat):
    A = copy.deepcopy(self)
    B = copy.deepcopy(new_mat)
    # reverse sign of second matrix
    B = B.scale(-1)
    # use add function
    A = A.add(B)
    return A

{% endhighlight %}

## Demo

<div style="text-align: justify">
<p>We create two matrices, call the add method and print the result:</p>
</div>

{% highlight python %}

A = Mat([[1, 2, 3],
         [4, 5, 6]])

B = Mat([[0, 2, 1],
         [3, 6, -1]])

C = A.add(B)

print_mat(C)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> print_mat(C)
[1, 4, 4]
[7, 11, 5]

{% endhighlight %}

[< Scalar Multiplication](./scalar_multiplication.md)\
[Dot Product and Matrix Multiplication >](./dot_prod_length_and_mat_multiply.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/addition_subtraction.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

