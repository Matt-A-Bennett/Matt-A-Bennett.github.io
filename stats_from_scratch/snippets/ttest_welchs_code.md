<div style="text-align: justify">
<p>Paragraph</p>
</div>

{% highlight python %}

def ttest_welchs(u, v):
    diff = mean(u).subtract(mean(v)).make_scalar()
    u_se, v_se = se(u).make_scalar(), se(v).make_scalar()
    t = diff / sqrt(u_se**2 + v_se**2)

    # compute degrees of freedom by Welch–Satterthwaite equation
    Nu, Nv = u.size(0), v.size(0)
    u_sd, v_sd = sd(u).make_scalar(), sd(v).make_scalar()

    df =          ( (u_sd**2/Nu + v_sd**2/Nv)**2 /
    (u_sd**4 / (Nu**2 * (Nu-1)) + v_sd**4 / (Nv**2 * (Nv-1))) )

    return t, df

{% endhighlight %}
