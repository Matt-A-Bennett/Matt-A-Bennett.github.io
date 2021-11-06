
<div style="text-align: justify">
<p>We loop over each element in the upper triangular region and if we find a
non-zero we return False, otherwise we return True:</p>
</div>

{% highlight python %}

def is_lower_tri(self):
    for i, row in enumerate(self.data):
        for col in range(i+1,len(row)):
            if row[col] != 0:
                return False
    else:
        return True

{% endhighlight %}
