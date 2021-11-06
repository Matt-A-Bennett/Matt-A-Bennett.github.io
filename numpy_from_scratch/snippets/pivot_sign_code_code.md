<div style="text-align: justify">
<p>We also create a method that returns the base-10 integer representation of a
base-2 (i.e. binary) number. The binary number is constructed from the
TRUE/FALSE answers to 3 queries: whether the matrix contains any negative,
zero, or positive pivots. The answers to these 3 queries uniquely determine
what kind of 'definiteness' (if any) we can call the matrix. Thus the method
returns a number (between 0 and 7: since $2^3 = 8$ possibilities) which can be
used as a unique identifier of the 'definiteness':</p>
</div>

{% highlight python %}

def pivot_sign_code(self):
    '''Returns number between 0 and 7 according to signs of pivots. We do
    this by constructing a 3-bit binary number, where each bit represents
    the presence/absence of negative, zero, or positive pivots, and then
    converting from binary to a base 10 integer.'''
    pivot_info = self.pivots().items()

    neg = int(any(piv[1] < 0 for piv in pivot_info))
    semi = int(any(piv[1] == 0 for piv in pivot_info))
    pos = int(any(piv[1] > 0 for piv in pivot_info))

    return int(str(neg) + str(semi) + str(pos), 2)

def is_negdef(self):
    return self.pivot_sign_code() == 4

def is_negsemidef(self):
    return self.pivot_sign_code() == 6

def is_possemidef(self):
    return self.pivot_sign_code() == 3

def is_posdef(self):
    return self.pivot_sign_code() == 1

{% endhighlight %}

