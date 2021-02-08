# A = LU
<div style="text-align: justify">
<p>Having the inverse method allows to revisit EA = U and move to a better
formulation of the same idea: A = LU. The matrix L is lower triangular and
takes U back to A by applying the elimination steps in the reverse order. The
improvement of this formulation is that the elimination steps <i>don't mix</i>.
</p>

<p>L is just the inverse of E (hence why it reverses the elimination steps). We
also have to reverse any row exchanges that we made in creating E. This is
achieved by multiplying L by the inverse of P (i.e. the permutation
matrix):</p>
</div>

{% highlight python %}

def lu(self):
    P, E, self, U, _, _ = self.elimination()
    L = E.inverse()
    P.transpose()
    L = P.multiply(L)
    return P, self, L, U

{% endhighlight %}

[< Inverse](./inverse.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)