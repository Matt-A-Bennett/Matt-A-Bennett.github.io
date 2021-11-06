<div style="text-align: justify"> <p>We already have the
method to give us a projection matrix. So here we take $I - P$ as our
projection matrix. After transposing $A$ (to make accessing the columns easier)
we loop over each column and make the others columns orthogonal. Then we move
onto the next column and repeat:</p> 
</div>

{% highlight python %}

def qr(self):
    if self.is_singular():
        print('Matrix is singular!')
        return self, None, None

    A = self.transpose()
    Q = dc(A)
    I = eye(A.size())
    # projection orthogonal to column
    for col in range(Q.size(0)-1):
        Col = dc(Mat([Q.data[col]]))
        P, _ = Col.transpose().projection()
        P = I.subtract(P)
        # project and put into matrix Q
        for col2 in range(col+1, Q.size(0)):
            Col = dc(Mat([Q.data[col2]]))
            q = P.multiply(Col.transpose()).transpose()
            Q.data[col2] = q.data[0]

{% endhighlight %}

<div style="text-align: justify">
<p>The next step is to make the length of each column 1. Which we do by
dividing by it's current length:</p>
</div>

{% highlight python %}

# normalise to unit length
for x, q in enumerate(Q.data):
    q = Mat([q])
    q = q.norm()
    Q.data[x] = q.data[0]

{% endhighlight %}

<div style="text-align: justify">
<p>The last step is to transpose $A$ back to how it was originally, and to
generate $R$ by multiplying $Q^TA$. Note that because we worked from $A^T$ from
the beginning, our $Q$ is already transposed, so we just multiply this with $A$
and then transpose $Q$ before returning:</p>
</div>

{% highlight python %}

    A = A.transpose()
    R = Q.multiply(A)
    Q = Q.transpose()
    A = Q.multiply(R)

    return A, Q, R

{% endhighlight %}
