{% highlight python %}
import linalg as la

la.print_mat(la.gen_mat([7,7], values=[1], type='full'))
la.print_mat(la.gen_mat([7,7], values=[1], type='upper'))
la.print_mat(la.gen_mat([7,7], values=[1,2,0,4,5], type='diag'))
la.print_mat(la.gen_mat([7,7], values=[2,-1], type='full'))

{% endhighlight %}

Outputs:

{% highlight console %}

>>> la.print_mat(la.gen_mat([7,7], values=[1], type='full'))
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]
[1, 1, 1, 1, 1, 1, 1]

>>> la.print_mat(la.gen_mat([7,7], values=[1], type='upper'))

[0, 1, 1, 1, 1, 1, 1]
[0, 0, 1, 1, 1, 1, 1]
[0, 0, 0, 1, 1, 1, 1]
[0, 0, 0, 0, 1, 1, 1]
[0, 0, 0, 0, 0, 1, 1]
[0, 0, 0, 0, 0, 0, 1]
[0, 0, 0, 0, 0, 0, 0]

>>> la.print_mat(la.gen_mat([7,7], values=[1,2,0,4,5], type='diag'))

[1, 0, 0, 0, 0, 0, 0]
[0, 2, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 4, 0, 0, 0]
[0, 0, 0, 0, 5, 0, 0]
[0, 0, 0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 0, 0]

>>> la.print_mat(la.gen_mat([7,7], values=[2,-1], type='full'))

[2, -1, 0, 0, 0, 0, 0]
[-1, 2, -1, 0, 0, 0, 0]
[0, -1, 2, -1, 0, 0, 0]
[0, 0, -1, 2, -1, 0, 0]
[0, 0, 0, -1, 2, -1, 0]
[0, 0, 0, 0, -1, 2, -1]
[0, 0, 0, 0, 0, -1, 2]

{% endhighlight %}

