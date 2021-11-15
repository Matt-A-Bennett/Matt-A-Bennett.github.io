<script>
MathJax = {
tex: {
tags: 'ams'  // should be 'ams', 'none', or 'all'
     }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>

# Pivots, rank, singularity, determinant, positive definiteness
## Pivots
{% include_relative snippets/pivots_code.md %}
### Demo
{% include_relative snippets/pivots_demo.md %}

## Rank
{% include_relative snippets/rank_code.md %}
### Demo
{% include_relative snippets/rank_demo.md %}

## Singularity
{% include_relative snippets/is_singular_code.md %}
### Demo
{% include_relative snippets/is_singular_demo.md %}

## Determinant
{% include_relative snippets/determinant_code.md %}
### Demo
{% include_relative snippets/determinant_demo.md %}

## Is matrix positive definite?
{% include_relative snippets/posdef_para.md %}
### Code implementation
{% include_relative snippets/pivot_sign_code_code.md %}
### Demo
{% include_relative snippets/pivot_sign_code_demo.md %}

[< Back substitution](./backsub.md)

<div style="text-align: right">
<a href="https://matt-a-bennett.github.io/numpy_from_scratch/inverse.html">Inverse ></a>
</div>

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/rank_piv_sing_det.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

