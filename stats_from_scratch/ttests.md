<script>
MathJax = {
tex: {
tags: 'ams'  // should be 'ams', 'none', or 'all'
     }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>

# Student's <i>t</i>
## One sample t-test
{% include_relative snippets/ttest_one_sample.md %}

### Code implementation
{% include_relative snippets/ttest_one_sample_code.md %}

## Paired samples t-test
{% include_relative snippets/ttest_paired_code.md %}

## Unpaired samples t-test
{% include_relative snippets/ttest_unpaired.md %}

### Code implementation
{% include_relative snippets/ttest_unpaired_code.md %}

## Welch's unpaired samples t-test
{% include_relative snippets/ttest_welchs.md %}

### Code implementation
{% include_relative snippets/ttest_welchs_code.md %}

## Demo
{% include_relative snippets/ttest_demo.md %}


[< Pearson's correlation](./correlation.md)

[back to project main page](./stats_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/stats_from_scratch/ttests.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

