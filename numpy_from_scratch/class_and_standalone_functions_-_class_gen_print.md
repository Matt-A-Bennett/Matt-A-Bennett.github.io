# Class, standalone functions and miscellaneous methods (1/3)
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
### Generate matrices
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

### Printing matrices
<div style="text-align: justify">
<p>Here is a function to print a matrix, one row beneath the other. This is
helpful for debugging. We also include an option to round the values to a
specified precision, which is useful to ignore very tiny rounding errors on
what would otherwise be integer numbers:</p>
</div>

#### Code implementation
{% highlight python %}

def print_mat(self, round_dp=99):
    A = copy.deepcopy(self)
    for row in A.data:
        rounded = [round(i,round_dp) for i in row]
        print(rounded)
    print()

{% endhighlight %}

[Is matrix triangular, diagonal, symmetric? >](./class_and_standalone_functions_-_tri_diag_sym.md)

[back to project main page](./numpy_from_scratch.md)\
[back to home](../index.md)

---
<script src="https://utteranc.es/client.js"
        repo="Matt-A-Bennett/Matt-A-Bennett.github.io"
        issue-term="https://matt-a-bennett.github.io/numpy_from_scratch/class_and_standalone_functions.html"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

