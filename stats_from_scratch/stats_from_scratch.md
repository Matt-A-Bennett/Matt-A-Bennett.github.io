<script>
MathJax = {
tex: {
tags: 'ams'  // should be 'ams', 'none', or 'all'
     }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>

# Adding a statistics sub-package

The full code I've written so far can be found [here](./full_code.md).

<div style="text-align: justify">
<p>Now that I've learned the basics of linear algebra and implemented a few of
the methods in my <a href="https://matt-a-bennett.github.io/numpy_from_scratch/numpy_from_scratch.html">linalg</a>
package, I'm going back over my understanding of statistics and model building
to see it from a linear algebra perspective. Therefore I'm going to add a
sub-package called 'stats' to the 'linalg' package, in order to learn about how
packages work in Python 3 and to help cement my understanding as I go.
Everything I do here will be implemented using the existing methods in the
'linalg' package. Here is what I've done so far:</p>
</div>

## Fundamental building blocks
- [Sum and mean](./sum_and_mean.md)
- [Zero-center](./zero_center.md)
- [Variance, covariance, standard deviation and standard error](./var_covar_stddev_stderr.md)
- [Z-score](./zscore.md)

## Statistical tests
- [Pearson's correlation](./correlation.md#pearsons-correlation)
- [One sample t-test](./ttests.md#one-sample-t-test)
- [Paired samples t-test](./ttests.md#paired-samples-t-test)
- [Unpaired samples t-test](./ttests.md#unpaired-samples-t-test)
- [Welch's unpaired samples t-test](./ttests.md#welchs-unpaired-samples-t-test)

[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/stats_from_scratch/stats_from_scratch.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

