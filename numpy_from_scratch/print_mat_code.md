{% highlight python %}

def print_mat(A, round_dp=99):
    for row in A.data:
        rounded = [round(i,round_dp) for i in row]
        print(rounded)
    print()

{% endhighlight %}
