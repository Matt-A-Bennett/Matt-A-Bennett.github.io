<div style="text-align: justify">
<p>We also define a method to choose which of a list of supplied
functions to apply, given the argument B. If the argument B was not an instance
of the class 'Mat' we assume an integer or float was passed and that the user
wants to use the first listed function, and otherwise wants to apply the second
function. Thus the appropriate function is passed, along with the argument B
into function_elwise:</p>
</div>

{% highlight python %}

def function_choice(self, B, functions):
    if isinstance(B, Mat) == False:
        return self.function_elwise(functions[0])
    return self.function_elwise(functions[1], B)

{% endhighlight %}
