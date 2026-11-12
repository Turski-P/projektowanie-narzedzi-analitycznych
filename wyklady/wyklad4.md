# Wykład 4 — Metoda Najmniejszych Kwadratów


## Model regresji liniowej

Model regresji liniowej ma postać:

$$y_i = \beta_0 + \beta_1 x_{1,i} + \beta_2 x_{2,i} + \ldots + \beta_K x_{K,i} + \varepsilon_i$$

Estymator wektora parametrów $\beta$:

$$\hat{\beta} = (\mathbb{X}'\mathbb{X})^{-1}\mathbb{X}'y$$

gdzie

$$\beta = \left[\begin{array}{c} \beta_0 \\ \beta_1 \\ \beta_2 \\ \vdots \\ \beta_K \end{array}\right], \qquad
\mathbb{X} = \left[\begin{array}{ccccc}
1 & x_{1,1} & x_{2,1} & \ldots & x_{K,1} \\
1 & x_{1,2} & x_{2,2} & \ldots & x_{K,2} \\
\vdots & \vdots & \vdots & \ldots & \vdots \\
1 & x_{1,N} & x_{2,N} & \ldots & x_{K,N}
\end{array}\right], \qquad
y = \left[\begin{array}{c} y_1 \\ y_2 \\ y_3 \\ \vdots \\ y_N \end{array}\right]$$

### Ćwiczenie

Dla modelu regresji liniowej postaci $y_i = \beta_0 + \beta_1 x_i + \varepsilon_i$ podać:

a) wzór na $\beta = (\mathbb{X}'\mathbb{X})^{-1}\mathbb{X}'y$,

b) postać macierzy $\mathbb{X}$,

c) macierz $\mathbb{X}'\mathbb{X}$,

d) macierz $(\mathbb{X}'\mathbb{X})^{-1}$,

e) macierz $\mathbb{X}'y$,

f) postać funkcji regresji.

## Miary dopasowania i macierz wariancji-kowariancji

Współczynnik determinacji liniowej $R^2$:

$$R^2 = 1 - \frac{RSS}{TSS} = 1 - \frac{\sum_{i=1}^N (y_i - \hat{y}_i)^2}{\sum_{i=1}^N (y_i - \bar{y})^2}$$

Skorygowany współczynnik determinacji liniowej $\bar{R}^2$:

$$\bar{R}^2 = 1 - \frac{N-1}{N-K}\left(1-R^2\right)$$

Estymator macierzy wariancji-kowariancji parametrów:

$$\widehat{\Sigma} = s^2 \left(\mathbb{X}'\mathbb{X}\right)^{-1}, \qquad
\widehat{\Sigma} = \left[\begin{array}{cccc}
Cov(\beta_0,\beta_0) & Cov(\beta_0,\beta_1) & \ldots & Cov(\beta_0,\beta_K) \\
Cov(\beta_1,\beta_0) & Cov(\beta_1,\beta_1) & \ldots & Cov(\beta_1,\beta_K) \\
Cov(\beta_2,\beta_0) & Cov(\beta_2,\beta_1) & \ldots & Cov(\beta_2,\beta_K) \\
\vdots & \vdots & \ldots & \vdots \\
Cov(\beta_K,\beta_0) & Cov(\beta_K,\beta_1) & \ldots & Cov(\beta_K,\beta_K)
\end{array}\right]$$

```{admonition} Do zaprogramowania samodzielnie
:class: note
Powyższe wzory — estymator $\hat{\beta}$, $R^2$, $\bar{R}^2$ oraz $\widehat{\Sigma}$ — mają zostać zaprogramowane "od podstaw" (przy użyciu operacji na macierzach: `t()`, `%*%`, `solve()`), a nie za pomocą gotowej funkcji `lm()`. Pozwala to zrozumieć mechanikę estymacji MNK, zanim skorzysta się z funkcji wbudowanych w R.
```

Przydatne operacje w R przy programowaniu MNK:

```r
X <- cbind(1, x1, x2)     # dodanie kolumny jedynek (stała) do macierzy regresorów
beta_hat <- solve(t(X) %*% X) %*% t(X) %*% y
y_hat <- X %*% beta_hat
resid <- y - y_hat
RSS <- sum(resid^2)
TSS <- sum((y - mean(y))^2)
R2 <- 1 - RSS / TSS
N <- length(y)
K <- ncol(X)
R2_adj <- 1 - (N - 1) / (N - K) * (1 - R2)
s2 <- RSS / (N - K)
Sigma_hat <- s2 * solve(t(X) %*% X)
```
