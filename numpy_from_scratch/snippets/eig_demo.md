<div style="text-align: justify">
<p>We create a matrix, call the eig method and print the results. Then we check
that an eigenvector multiplied by $A$ gives the same result as the eigenvector
scaled by the eigenvalue:</p>
</div>

{% highlight python %}

A = la.Mat([[1, 2, 3],
            [2, 4, 4],
            [3, 4, 5]])

evects, evals = A.eig()

la.print_mat(evals, 2)
la.print_mat(evects,2)

# extract the first eigenvector
evect = Mat([evects.tr().data[0]]).tr()
# multiply eigenvector by A and print result
la.print_mat(A.multiply(evect),2)
# scale eigenvector by eigenvalue and print result
la.print_mat(evect.scale(evals.data[0][0]),2)

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(evals, 2)
[-0.61, 9.95, 0.65]

>>> la.print_mat(evects,2)
[-0.86, 0.37, 0.35]
[-0.07, 0.6, -0.8]
[0.51, 0.71, 0.49]

>>> la.print_mat(A.multiply(evect),2)
[0.53]
[0.04]
[-0.31]

>>> la.print_mat(evect.scale(evals.data[0][0]),2)
[0.53]
[0.04]
[-0.31]

{% endhighlight %}
