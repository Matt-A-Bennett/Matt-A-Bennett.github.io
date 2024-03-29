<div style="text-align: justify"> 
<p>If on the other hand we have two samples which do not have a simple pairing,
then the variation of the two samples cannot be considered 'shared' and used to
normalise the observed difference as before.</p>

<p>Instead, we have to normalise by the 'pooled' standard deviation (which
itself gives rise to a family of 'pooled' standard error). If the number of
observations in each sample were equal, we could just average the two
variances:</p>
</div>

$$ 
\begin{equation}
s = \sqrt{\frac{\sigma_u^2}{2} + \frac{\sigma_v^2}{2}}
\end{equation}
$$

<div style="text-align: justify">
<p> And then instead of obtaining the standard error by using $\sqrt{n}$, we
would use $\sqrt{2/n}$ (because we have one less degree of freedom due to the
second sample):</p>
</div>

$$ 
\begin{equation}
t = \frac{\bar u - \bar v}{s \sqrt{\frac{1}{n} + \frac{1}{n}}}
\end{equation}
$$

<div style="text-align: justify">
<p>When the sample sizes are different, we can take a family of 'weighted'
average of the variances - weighted, that is, by the proportion of total
degrees of freedom each sample accounts for. Thus the 'pooled' standard
deviation in that case is:</p>
</div>

$$ 
\begin{equation}
s = \sqrt{\frac{\sigma_u^2(n_1-1)}{(n_1 - 1) + (n_2 - 1)} + \frac{\sigma_v^2(n_2 - 1)}{(n_1 - 1) + (n_2 - 1)}}
\end{equation}
$$

$$
\begin{equation}
  = \sqrt{\frac{\sigma_u^2(n_1-1) + \sigma_v^2(n_2 - 1)}{(n_1 - 1) + (n_2 - 1)}}
\end{equation}
$$

<div style="text-align: justify">
<p>Just like in equation $(3)$ above, we account for having one less degree of
freedom when converting our pooled standard deviation to a pooled standard
error:</p>
</div>

$$ 
\begin{equation}
t = \frac{\bar u - \bar v}{s \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}}
\end{equation}
$$

