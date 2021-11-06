<div style="text-align: justify">
<p>We create a matrix, call the 'eigdiag' method and print the results. We also
'reconstruct' the matrix $A$ from $X\Lambda X^{-1}$ (note there are some
rounding errors):</p>
</div>

{% highlight python %}
import linalg as la

A = la.Mat([[1, 1, 3],
            [2, 2, 4],
            [5, 2, 6]])

evec, eigval, evecinv = A.eigdiag()
la.print_mat(evec,4)
la.print_mat(eigval,4)
la.print_mat(evecinv,4)
la.print_mat(evec.multiply(eigval).multiply(evecinv),5)

{% endhighlight %}

Outputs:

{% highlight console %}
 
>>> evec, eigval, evecinv = A.eigdiag()
Matrix is not symmetric or triangular and may therefore have complex
eigenvalues which this method cannot handle. Interpret results with care!

>>> la.print_mat(evec,4)
[-0.7299, -0.34, 0.0443]
[-0.3156, -0.5135, -0.9495]
[0.6063, -0.7878, 0.3106]

>>> la.print_mat(eigval,4)
[-1.0598, 0, 0]
[0, 9.4614, 0]
[0, 0, 0.5984]

>>> la.print_mat(evecinv,4)
[-1.0682, 0.0833, 0.4067]
[-0.5622, -0.2984, -0.8321]
[0.6591, -0.9195, 0.3148]

>>> la.print_mat(evec.multiply(eigval).multiply(evecinv),4)
[0.99994, 1.00009, 2.99997]
[1.99994, 2.00009, 3.99997]
[4.99994, 2.00009, 5.99997]

{% endhighlight %}
