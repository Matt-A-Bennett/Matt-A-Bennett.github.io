{% highlight python %}

def print_mat(A, round_dp=99):
    for row in A.data:
        rounded = [round(j,round_dp) for j in row]
        print(rounded)
    print()

{% endhighlight %}
