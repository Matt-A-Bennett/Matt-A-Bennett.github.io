<script>
MathJax = {
tex: {
tags: 'ams'  // should be 'ams', 'none', or 'all'
     }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>

# Variance, covariance, standard deviation and standard error
<div style="text-align: justify">
<p>The study of statistics and data is the study of variation. The general
situation is that we are interested in estimating a parameter of a population
based on a sample drawn from that population.</p>

<p>Here we introduce some of the key basic measures.</p>
</div>

## Variance and covariance
{% include_relative snippets/variance_and_covariance.md %}

## Code implementation
{% include_relative snippets/variance_and_covariance_code.md %}

## Standard deviation and standard error
{% include_relative snippets/stddev_and_stderr.md %}

## Code implementation
{% include_relative snippets/stddev_and_stderr_code.md %}

## Demo
{% include_relative snippets/var_cov_sd_se_demo.md %}


[< Zero center](./zero_center.md)

<div style="text-align: right">
<a href="https://matt-a-bennett.github.io/stats_from_scratch/zscore.html">Z-score ></a>
</div>

[back to project main page](./stats_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/stats_from_scratch/var_covar_stddev_stderr.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

