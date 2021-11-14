<div style="text-align: justify">
<p>Since we allow for different sample sizes, we require two vectors, u and v.
Unless explicitly told to assume equal variances, we perform Welch's unpaired
<i>t</i> test (see below). Otherwise, we compute a few preliminaries, then
proceed to the pooled variance and pooled standard deviation. Finally, we
compute and return the <i>t</i> statistic (along with the degrees of
freedom):</p>
</div>

{% highlight python %}

def ttest_unpaired(u, v, assume_equal_vars=False):
    if not assume_equal_vars:
        return ttest_welchs(u, v)

    diff = mean(u).subtract(mean(v)).make_scalar()
    Nu, Nv = u.size(0), v.size(0)
    u_df, v_df = Nu-1, Nv-1
    df = u_df + v_df
    u_var, v_var = var(u).make_scalar(), var(v).make_scalar()

    pooled_var = (( (u_var * u_df) / (u_df + v_df) ) +
                  ( (v_var * v_df) / (v_df + v_df) ))

    pooled_sd = sqrt(pooled_var)

    t = diff / (pooled_sd * sqrt(1/Nu + 1/Nv))

    return t, df

{% endhighlight %}
