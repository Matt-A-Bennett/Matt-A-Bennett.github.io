<div style="text-align: justify">
<p>We create a matrix with three columns - the third being more variable. We
then store the each column separately as u, v and z, and extend z by
concatenating it with v. We call the various ttest methods and print the
results:</p>
</div>

{% highlight python %}

import linalg as la

A = la.Mat([[85, 84, 81],
            [86, 83, 92],
            [88, 93, 103],
            [75, 99, 85],
            [78, 97, 97],
            [94, 90, 84],
            [98, 88, 52],
            [79, 90, 88],
            [71, 87, 105],
            [80, 86, 86],
                       ])

u = A.ind('',0)
v = A.ind('',1)
z = A.ind('',2)
z = la.cat(v, z)

ts, df = la.stats.ttest_one_sample(A, H=80)
print(df); la.print_mat(ts, 2)

t, df = la.stats.ttest_paired(u, v)
print(df); print(round(t, 2))

t, df = la.stats.ttest_unpaired(u, z, assume_equal_vars=True)
print(df); print(round(t, 2))

t, df = la.stats.ttest_welchs(u, z)
print(round(df, 2)); print(round(t, 2))

{% endhighlight %}

Outputs:

{% highlight console %}

>>> ts, df = la.stats.ttest_one_sample(A, H=80)
>>> print(df); la.print_mat(ts, 2)
9
[1.27, 5.8, 1.56]

>>> t, df = la.stats.ttest_paired(u, v)
>>> print(df); print(round(t, 2))
9
-1.8

>>> t, df = la.stats.ttest_unpaired(u, z, assume_equal_vars=True)
>>> print(df); print(round(t, 2))
28
-1.45

>>> t, df = la.stats.ttest_welchs(u, z)
>>> print(round(df, 2)); print(round(t, 2))
22.79
-1.41

{% endhighlight %}
