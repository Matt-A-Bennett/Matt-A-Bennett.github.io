{% highlight python %}

def eigvalues(self, epsilon = 0.0001, max_its=100):
    if not (self.is_symmetric() or self.is_lower_tri() or self.is_upper_tri()):
        print('Matrix is not symmetric or triangular and may therefore have complex eigenvalues which this method cannot handle. Interpret results with care!')

    if self.is_upper_tri() or self.is_lower_tri():
        return Mat([self.diag()])
    if self.is_singular():
        print('Matrix is singular!')
        return None

    old_eig = 0
    final_eigs = []
    for its in range(max_its):

        # obtain off diagonal zeros
        _, E, _, _, _, _ = self.elimination()
        Einv = E.inverse()
        A = E.multiply(self).multiply(Einv)

        # shift A by -cI, where c is last diag
        shift = eye(A.size()).multiply_elwise(old_eig)

        # QR factorisation
        A = A.subtract(shift)
        _, Q, R = A.qr()
        A = R.multiply(Q)
        A = A.add(shift)

        current_eig = A.diag()[-1]
        diff = old_eig - current_eig
        old_eig = current_eig
        if abs(diff) < epsilon:
            if min(A.size()) == 2:
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
