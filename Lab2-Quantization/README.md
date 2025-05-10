## K-Means Quantization
### How to get a K-Means results
We ues **KMeans** class in order to divide n numbers into **n_clusters** clusters. If we want to get a result which is a Q bits-Quantization result, we must ensure $2^Q==n\\_clusters$.

And then we input the X tensor, we can get **label** indicates which center the float belongs to, and **centroid** is the floating point value of the center.

The result is as follow. The number {0.09, -0.04, -0.16, -0.08, 0.06, -0.11} on origin grid are clustered to the **green** label which centroid value is **-0.02**

<img width="746" alt="image" src="https://github.com/user-attachments/assets/8d82b831-b83b-4544-8a2d-deabd89ba784" />

## Linear Quantization
### How to get Linear results
From $r=S(q-Z)$, we have $q = \mathrm{int}(\mathrm{round}(r/S)) + Z$.

Supposed we want to get a result which is a Q bits-Quantization, we can get $q_{max} = 2^{Q-1} - 1$ and $q_{min} = 2^{Q-1}$.

For each element r in a given X tensor, we can get $S$ and $Z$ according to formula 
$S=\frac{r_{max}-r_{min}}{q_{max}-q_{min}}$ and $Z=\mathrm{int}(\mathrm{round}(q_{min}-\frac{r_{min}}{S}))$.

Finially, we can use **clamp** function fix $q = \mathrm{int}(\mathrm{round}(r/S)) + Z$ into the range of $[-2^{Q-1}, 2^{Q-1})$.
