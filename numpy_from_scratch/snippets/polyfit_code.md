<div style="text-align: justify">
<p>Next we define a method to give the parameters for an nth degree polynomial
curve through a set of data points in $b$. Here we use the vandermonde matrix
$V$, we defined earlier and project onto it to give \(\hat b\):</p>
</div>

{% highlight python %}

def polyfit(self, order=1):
    V = vandermonde(self.size(0), order=order)
    # fit model to b
    return self.project_onto_V(V)

{% endhighlight %}

<div style="text-align: justify">
<p>Then we define a method to fit a straight line. This is the default of the
polyfit method, but fitting a straight line is so common that it's nice to have
a more descriptive method to call:</p>
</div>
{% highlight python %}

def linfit(self):
    return self.polyfit()

{% endhighlight %}
