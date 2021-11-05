<div style="text-align: justify">
<p>Addition and subtraction is valid between two same-shaped matrices and is
done element-wise:</p>
</div>

$$
A + B =%
  \begin{bmatrix}
    1 & 2 & 3 \\
    4 & 5 & 6
  \end{bmatrix}+%

  \begin{bmatrix}
    2 & 1 & 4 \\
    0 & 3 & 1
  \end{bmatrix}=%

  \begin{bmatrix}
    3 & 3 & 7 \\
    4 & 8 & 7
  \end{bmatrix}
$$

<div style="text-align: justify">
<p>Although not a strictly legal operation, adding/subtracting a scalar to/from
a matrix is a useful thing to do (and can be achieved by subtracting an 'all
ones' matrix that itself has been multiplied by a scalar)</p>
</div>

$$
  \begin{bmatrix}
    1 & 2 & 3 \\
    4 & 5 & 6
  \end{bmatrix} ``+ 2" =%
$$

$$
  \begin{bmatrix}
    1 & 2 & 3 \\
    4 & 5 & 6
  \end{bmatrix}+ 2%

  \begin{bmatrix}
    1 & 1 & 1 \\
    1 & 1 & 1
  \end{bmatrix}=%

  \begin{bmatrix}
    3 & 4 & 5 \\
    6 & 7 & 8
  \end{bmatrix}
$$
