<div style="text-align: justify">
<p>Below, we define a helper function and try this method out on a small
sample. We fit a straight line, a 2nd degree polynomial, and a 7th degree
polynomial:</p>
</div>

{% highlight python %}
import linalg as la

# regression
def quick_plot(b, orders=[1]):
    fig = plt.figure()
    Xs = [i/10 for i in range(len(b.data[0])*10)]
    for idx, order in enumerate(orders):
        fit = b.tr().polyfit(order=order)
        Ys = []
        for x in Xs:
            y = 0
            for exponent in range(order+1):
                y += fit.data[exponent][0]*x**exponent
            Ys.append(y)

        ax = plt.subplot(1,len(orders),idx+1)
        d = ax.plot(Xs[0::10], b.data[0], '.k')
        f = ax.plot(Xs, Ys, '-r')
        ax.set_ylim([0, max(b.data[0])+1])
    return fig

import matplotlib.pyplot as plt
b = la.Mat([[2,1,3,5,1,4,6,3,4,7,7,8,7,6,5,7,8,7,9,7,6,6,9]])

fig = quick_plot(b, orders=[1, 2, 7])
plt.show()

{% endhighlight %}

![regression plot](./images/regression.png)

