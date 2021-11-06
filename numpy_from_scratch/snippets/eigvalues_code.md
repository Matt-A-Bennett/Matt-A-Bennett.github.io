{% highlight python %}

def eigvalues(self, epsilon = 0.0001, max_its=100):
    A = dc(self)
    if not (A.is_symmetric() or A.is_lower_tri() or A.is_upper_tri()):
        print('Matrix is not symmetric or triangular and may therefore have complex eigenvalues which this method cannot handle. Interpret results with care!')

    if A.is_upper_tri() or A.is_lower_tri():
        return Mat([A.diag()])
    if A.is_singular():
        print('Matrix is singular!')
        return None

    old_eig = 0
    final_eigs = []
    for its in range(max_its):

        # obtain off diagonal zeros
        _, E, _, _, _, _ = A.elimination()
        Einv = E.inverse()
        A = E.multiply(A).multiply(Einv)

        # shift A by -cI, where c is last diag
        shift = eye(size(A)).scale(old_eig)

        # QR factorisation
        A = A.subtract(shift)
        _, Q, R = A.qr()
        A = R.multiply(Q)
        A = A.add(shift)

        current_eig = A.diag()[-1]
        diff = old_eig - current_eig
        old_eig = current_eig
        if abs(diff) < epsilon:
            if min(size(A)) == 2:
                final_eigs += A.diag()
                return Mat([final_eigs])
            else:
                final_eigs.append(current_eig)
                A = A.data[:-1]
                A = [row[:-1] for row in A]
                A = Mat(A)
                old_eig = A.diag()[-1]
    else:
        print('Did not converge!')
        return None

{% endhighlight %}
