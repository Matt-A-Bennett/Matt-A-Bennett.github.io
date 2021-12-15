{% highlight python %}
import linalg as la

la.print_mat(la.gen_mat([7,7], values=[1], family='full'))
la.print_mat(la.gen_mat([7,7], values=[1], family='upper'))
la.print_mat(la.gen_mat([7,7], values=[1,2,0,4,5], family='diag'))
la.print_mat(la.gen_mat([7,7], values=[2,-1], family='full'))

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.gen_mat([7,7], values=[1], family='full'))
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]

>>> la.print_mat(la.gen_mat([7,7], values=[1], family='upper'))

[0, 1, 1, 1, 1, 1, 1]
[0, 0, 1, 1, 1, 1, 1]
[0, 0, 0, 1, 1, 1, 1]
[0, 0, 0, 0, 1, 1, 1]
[0, 0, 0, 0, 0, 1, 1]
[0, 0, 0, 0, 0, 0, 1]
[0, 0, 0, 0, 0, 0, 0]

>>> la.print_mat(la.gen_mat([7,7], values=[1,2,0,4,5], family='diag'))

[1, 0, 0, 0, 0, 0, 0]
[0, 2, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 4, 0, 0, 0]
[0, 0, 0, 0, 5, 0, 0]
[0, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 0, 0]

>>> la.print_mat(la.gen_mat([7,7], values=[2,-1], family='full'))

[2, -1, 0, 0, 0, 0, 0]
[-1, 2, -1, 0, 0, 0, 0]
[0, -1, 2, -1, 0, 0, 0]
[0, 0, -1, 2, -1, 0, 0]
[0, 0, 0, -1, 2, -1, 0]
[0, 0, 0, 0, -1, 2, -1]
[0, 0, 0, 0, 0, -1, 2]

{% endhighlight %}

