{% highlight python %}

def eig(self, epsilon=0.0001, max_its=100):
    if self.is_singular():
        print('Matrix is singular!')
        return None, None
    evals = self.eigvalues()
    evects = []
    for evalue in evals.data[0]:
        # ensure we don't destroy the diagonal completely
        if evalue in self.diag():
            evalue -= 1e-12
        A_shifted = self.subtract(eye(self.size()).multiply_elwise(evalue))
        # A_shifted_inv = A_shifted.inverse()
        b = gen_mat([self.size(0),1], values=[1])
        b = b.norm()
        for its in range(max_its):
            old_b = dc(b)
            b = A_shifted.backsub(b)
            # b = A_shifted_inv.multiply(b)
            b = b.norm()
            diff1 = b.subtract(old_b)
            diff2 = b.subtract(old_b.multiply_elwise(-1))
            if diff2.length() or diff2.length() < epsilon:
                evects.append(b.transpose().data[0])
                break
    evects = Mat(evects).transpose()
    return evects, evals

{% endhighlight %}
