<div style="text-align: justify">
<p>We check to see if a row index 'i' and if a column index 'j' were passed. If
only a row index was passed, we return that entire row. If only a column index
was passed, we return the entire column (by transposing the matrix to make
indexing a column easy) and if both were passed we return the value in the
'ith' and 'jth' column (as an integer):</p>
</div>

{% highlight python %}

def ind(self, i=None, j=None):
    if isinstance(i, int) and not isinstance(j, int):
        return Mat([self.data[i]])
    elif isinstance(j, int) and not isinstance(i, int):
        return Mat([self.tr().data[j]]).tr()
    elif isinstance(i, int) and isinstance(j, int):
        return self.data[i][j]

{% endhighlight %}
