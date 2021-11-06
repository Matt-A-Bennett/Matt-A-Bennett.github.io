<div style="text-align: justify">
<p>Often there is no solution to $Ax = b$. Usually in practical applications we
have a large set of data points $b$ that we want to fit with a model - the
columns of $A$ - with only a few parameters - stored in $x$ - much fewer
parameters than we have data points. Our model matrix $A$ is tall and thin, and
so has no inverse! $x = A^{-1}b$ is not an option to find the parameters in
$x$.</p>

<p>The data points contain some measurement error or 'noise' and we don't want
our model to fit this noise. We want our model to capture informative trends,
that will generalise to new data with different noise. Therefore we have to
accept some discrepancy between our fitted model and the data. We want to
minimise this 'model error' when we fit.</p>

<p>Since we can't find an $x$ that satisfies $Ax = b$, we look for a 'best $x$'
that comes close: \(\hat x\). The $b$ doesn't fall into the column space of $A$
(henceforth $C(A)$) whereas \(A\hat x\) does, so we project $b$ to the closest
point in $C(A)$. This implies that the 'error' is the shortest vector $e$
needed to 'bridge the gap' from $b$ to $C(A)$:</p>
</div>

$$
e = b - A\hat x
$$

<div style="text-align: justify">
<p>The vector $e$ is perpendicular to $C(A)$ and so is in the nullspace of
$A^T$ (henceforth $N(A^T)$):</p>
</div>

$$
A^T(b - A\hat x) = 0
$$

<div style="text-align: justify">
<p>The equation can be expanded to:</p>
</div>

$$
A^Tb - A^TA\hat x = 0
$$


<div style="text-align: justify">
<p>Rearranging::</p>
</div>

$$
A^TA\hat x = A^Tb
$$

<div style="text-align: justify">
<p>Therefore, our best estimate of the parameters of the model is:</p>
</div>

$$
\hat x = (A^TA)^{-1}A^Tb
$$

<div style="text-align: justify">
<p>And the vector that will be in the $C(A)$ (that is the 'predicted values' of
our model) is:</p>
</div>

$$
A\hat x = A(A^TA)^{-1}A^Tb
$$

<div style="text-align: justify">
<p>Thus we arrive at a matrix to 'project' some vector into $C(A)$:</p>
</div>

$$
P = A(A^TA)^{-1}A^T
$$
