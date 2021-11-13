<div style="text-align: justify">
<p>First we run elimination on the augmented matrix $[A | b]$:</p>
</div>

{% highlight python %}

def backsub(self, b):
    augmented = cat(self, b, axis=1)
    _, _, _, U, _, _ = augmented.elimination()

{% endhighlight %}

<div style="text-align: justify">
<p>Next we initiate a list where we will store the coefficients as they are
solved. We loop over the row indices in reverse order. For each step (apart
from the first), we take the previous coefficient and multiply the
corresponding column of U, then subtract the result from the current $b$. To do
this, we use an elimination matrix on the <i>right side</i> of $U$ (to
manipulate the columns rather than the rows):</p>
</div>

{% highlight python %}

coeff = []
for idx in range(-1, -(U.size(0)+1), -1):
    if idx < -1:
        E = eye([U.size(0)+1, U.size(1)])
        E.data[idx][U.size(1)-1] = -1*(coeff[-1])
        U = U.multiply(E)

{% endhighlight %}

<div style="text-align: justify">
<p>With the rearranged row we can attempt to solve for the unknown. There are a
number of possibilities. If we have a singular matrix, elimination will have
produced a row of zeros and in this case we can't solve for a non-zero in $b$.
If $b$ happens to also contain a zero at this position, then any coefficient
will multiply to produce a zero and we have an infinite number of solutions. We
default to picking a coefficient of $1$ in this case. Otherwise, we solve for
the coefficient by dividing the $b$ term with term in the row:</p>
</div>

{% highlight python %}

row = U.data[idx]
# check solution possibilities
if row[idx-1] == 0 and row[-1] != 0:
   print('No solution!')
   return None
elif row[idx-1] == 0 and row[-1] == 0:
   print('Infinite solutions!')
   coeff.append(1)
else:
    coeff.append(row[-1]/row[idx-1])

{% endhighlight %}

<div style="text-align: justify">
<p>Since we solved for the coefficients in reverse order, we reverse our
coefficient list, and return them as a column vector:</p>
</div>

{% highlight python %}

coeffs = list(reversed(coeff))
return Mat([coeffs]).tr()

{% endhighlight %}
