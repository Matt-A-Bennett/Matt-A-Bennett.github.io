<div style="text-align: justify">
<p>We then define a function that can zero center each column, each row, or
that matrix as a whole (if axis=2). If the matrix is square, then we use the
centering matrix approach above. Otherwise, after taking the mean across the
relevant axis (columns, rows, or all elements), we make a matrix of the same
size but filled with the mean of each axis and subtract it off the original
matrix:</p>
</div>

{% highlight python %}

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
{% endhighlight %}
