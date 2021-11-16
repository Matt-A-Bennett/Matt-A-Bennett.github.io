<div style="text-align: justify">
<p>It is often useful to normalise data. One type of normalisation is to 'zero
center' the data by subtracting it's mean. This will yield data with a new mean
of zero. Often we want to do this separately for each column or row of a
matrix. Also it's often the case that we want to perform this operation on a
square matrix. In that case, we can multiply by a 'centering matrix':</p> 
</div>

$$
\begin{equation}
C = I - \frac{1}{N}
\end{equation}
$$

$$
\begin{equation}
C = %
  \begin{bmatrix}
    1 & 0 & 0 \\[5pt]
    0 & 1 & 0 \\[5pt]
    0 & 0 & 1 \\
  \end{bmatrix}
    %
    -%
  \begin{bmatrix}
    \frac{1}{3} & \frac{1}{3} & \frac{1}{3} \\[5pt]
    \frac{1}{3} & \frac{1}{3} & \frac{1}{3} \\[5pt]
    \frac{1}{3} & \frac{1}{3} & \frac{1}{3}
  \end{bmatrix}
  %
  =%
  \begin{bmatrix}
    \frac{2}{3} & -\frac{1}{3} & -\frac{1}{3} \\[5pt]
    -\frac{1}{3} & \frac{2}{3} & -\frac{1}{3} \\[5pt]
    -\frac{1}{3} & -\frac{1}{3} & \frac{2}{3}
  \end{bmatrix}
\end{equation}
$$

$$
\begin{equation}
CA =%
  \begin{bmatrix}
    \frac{2}{3} & -\frac{1}{3} & -\frac{1}{3} \\[5pt]
    -\frac{1}{3} & \frac{2}{3} & -\frac{1}{3} \\[5pt]
    -\frac{1}{3} & -\frac{1}{3} & \frac{2}{3}
  \end{bmatrix}
  \begin{bmatrix}
    1 & 1 & 1\\[5pt]
    0 & 2 & 0\\[5pt]
    0 & 3 & -4
  \end{bmatrix}
  %
  =%
  \begin{bmatrix}
     \frac{2}{3} & -1 & 2 \\[5pt]
    -\frac{1}{3} & 0 & 1 \\[5pt]
    -\frac{1}{3} & 1 & -3
  \end{bmatrix}
\end{equation}
$$

<div style="text-align: justify">
<p>Here the matrix $C$ had the effect of subtracting $1/3$ from the first
column, subtracting $2/3$ from the second column, and adding $1$ to the last
column - ensuring that all columns sum to zero.</p>

We create a function to build the centering matrix:
</div>

{% highlight python %}

def gen_centering(size):
    if type(size) is int:
        size = [size, size]
    return la.eye(size).subtract(1/size[0])

{% endhighlight %}
