{% highlight python %}
import linalg as la

la.print_mat(la.gen_mat([7,7], values=[1], kind='full'))
la.print_mat(la.gen_mat([7,7], values=[1], kind='upper'))
la.print_mat(la.gen_mat([7,7], values=[1,2,0,4,5], kind='diag'))
la.print_mat(la.gen_mat([7,7], values=[2,-1], kind='full'))

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.gen_mat([7,7], values=[1], kind='full'))
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]

>>> la.print_mat(la.gen_mat([7,7], values=[1], kind='upper'))

[0, 1, 1, 1, 1, 1, 1]
[0, 0, 1, 1, 1, 1, 1]
[0, 0, 0, 1, 1, 1, 1]
[0, 0, 0, 0, 1, 1, 1]
[0, 0, 0, 0, 0, 1, 1]
[0, 0, 0, 0, 0, 0, 1]
[0, 0, 0, 0, 0, 0, 0]

>>> la.print_mat(la.gen_mat([7,7], values=[1,2,0,4,5], kind='diag'))

[1, 0, 0, 0, 0, 0, 0]
[0, 2, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 4, 0, 0, 0]
[0, 0, 0, 0, 5, 0, 0]
[0, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 0, 0]

>>> la.print_mat(la.gen_mat([7,7], values=[2,-1], kind='full'))

[2, -1, 0, 0, 0, 0, 0]
[-1, 2, -1, 0, 0, 0, 0]
[0, -1, 2, -1, 0, 0, 0]
[0, 0, -1, 2, -1, 0, 0]
[0, 0, 0, -1, 2, -1, 0]
[0, 0, 0, 0, -1, 2, -1]
[0, 0, 0, 0, 0, -1, 2]

{% endhighlight %}

