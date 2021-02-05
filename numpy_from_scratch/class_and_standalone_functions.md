# The Mat(rix) Class and standalone functions
## The Mat(rix) Class
<div style="text-align: justify">
<p>First off, we need a class 'Mat' (as in 'matrix'). Matrix like data will be
passed to the Mat class in the form of a list of lists, with each sub-list
acting as a row. We will gradually build up a suit of methods to do all the
needed operations.</p> 
</div>

{% highlight python %}

class Mat:
    def __init__(self, data):
        self.data = data

# define a 2x3 matrix
Mat([[1, 2, 3], [4, 5, 6]])

{% endhighlight %}

## Standalone functions

<div style="text-align: justify">
<p>We make a method to generate a matrix of a given size, uniformly populated
with a particular value (default 0):</p>
</div>

{% highlight python %}

def gen_mat(size, value=0):
    generated_mat = []
    for i in range(size[0]):
        generated_mat.append([value for j in range(size[1])])
    return Mat(generated_mat)

{% endhighlight %}

<div style="text-align: justify">
<p>Another useful matrix to generate immediately is the identity matrix. We
use the previous function and populate the diagonal with 1's.</p>
</div>

{% highlight python %}

def eye(size):
    eye = gen_mat(size)
    for i in range(size[0]):
        eye.data[i][i] = 1
    return eye

{% endhighlight %}

<div style="text-align: justify">
<p>Here is a function to print a matrix, one row beneath the other. This is
helpful for debugging.</p>
</div>

{% highlight python %}

def print_mat(self):
    for row in self.data:
        print(row)
    print()

{% endhighlight %}

[Transpose >](./transpose.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../README.md)
