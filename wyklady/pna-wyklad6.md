# Wykład 6 — MNW: metoda Newtona i algorytm BHHH


## Przypomnienie: metoda Newtona (jedna zmienna)

$$y-y_0 = f'(x)(x-x_0), \qquad f'(x_0) = \frac{f(x_0)-0}{x-x_0}, \qquad x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}$$

W maksymalizacji funkcji metodą Newtona znajduje się miejsce zerowe pochodnej:

$$x_{n+1} = x_n - \frac{f'(x_n)}{f''(x_n)}$$

## Metoda Newtona — maksymalizacja funkcji wielu zmiennych

Niech $\ln L(\theta)$ będzie funkcją log-wiarygodności od argumentu $\theta$, który jest $(K\times 1)$ wektorem parametrów. Iteracja metody Newtona ma postać:

$$\theta_{n+1} = \theta_n - H_n^{-1}G_n$$

gdzie $G_n$ (gradient) i $H_n$ (hesjan) liczone są w punkcie $\theta_n$:

$$G_n = \frac{\partial \ln L(\theta)}{\partial \theta}\bigg|_{\theta_n}, \qquad H_n = \frac{\partial^2 \ln L(\theta)}{\partial \theta \partial \theta'}\bigg|_{\theta_n}$$

$$G_n = \left[\begin{array}{c} \frac{\partial \ln L(\theta)}{\partial \theta_1} \\ \frac{\partial \ln L(\theta)}{\partial \theta_2} \\ \vdots \\ \frac{\partial \ln L(\theta)}{\partial \theta_K}\end{array}\right], \qquad
H_n = \left[\begin{array}{cccc}
\frac{\partial^2 \ln L(\theta)}{\partial \theta_1\partial \theta_1} & \frac{\partial^2 \ln L(\theta)}{\partial \theta_1\partial \theta_2} & \ldots & \frac{\partial^2 \ln L(\theta)}{\partial \theta_1\partial \theta_K}\\
\frac{\partial^2 \ln L(\theta)}{\partial \theta_2\partial \theta_1} & \frac{\partial^2 \ln L(\theta)}{\partial \theta_2\partial \theta_2} & \ldots & \frac{\partial^2 \ln L(\theta)}{\partial \theta_2\partial \theta_K}\\
\vdots & \vdots & \vdots & \vdots \\
\frac{\partial^2 \ln L(\theta)}{\partial \theta_K\partial \theta_1} & \frac{\partial^2 \ln L(\theta)}{\partial \theta_K\partial \theta_2} & \ldots & \frac{\partial^2 \ln L(\theta)}{\partial \theta_K\partial \theta_K}
\end{array}\right]$$

### Przykład — rozkład normalny

Dla $\ln L(x;\mu,\sigma) = -\frac{1}{2}N\ln(2\pi) - N\ln(\sigma) - \frac{1}{2}\sum_{i=1}^N \frac{(x_i-\mu)^2}{\sigma^2}$:

$$\frac{\partial}{\partial \mu}\ln L = \sum_{i=1}^N \frac{x_i-\mu}{\sigma^2}, \qquad
\frac{\partial}{\partial \sigma}\ln L = -\frac{N}{\sigma} + \sum_{i=1}^N \frac{(x_i-\mu)^2}{\sigma^3}$$

$$\frac{\partial^2 \ln L}{(\partial \mu)^2} = -\frac{N}{\sigma^2}, \qquad
\frac{\partial^2 \ln L}{\partial \mu \partial \sigma} = -2\sum_{i=1}^N \frac{x_i-\mu}{\sigma^3}, \qquad
\frac{\partial^2 \ln L}{(\partial \sigma)^2} = \frac{N}{\sigma^3} - 3\sum_{i=1}^N \frac{(x_i-\mu)^2}{\sigma^4}$$

*(Źródło przykładu: Martin, Hurn, Harris, Econometric Modelling with Time Series, [2].)*

## Algorytm BHHH (Berndt-Hall-Hall-Hausman)

```{admonition} Referencja
:class: note
Berndt, E.; Hall, B.; Hall, R.; Hausman, J. (1974). *Estimation and Inference in Nonlinear Structural Models*, Annals of Economic and Social Measurement, 3: 653–665.
```

Algorytm BHHH jest wariantem metody Newtona, w którym hesjan zastępuje się przybliżeniem opartym na iloczynie gradientów indywidualnych obserwacji — nie wymaga to liczenia drugich pochodnych:

$$\theta_{n+1} = \theta_n - J_n^{-1}G_n$$

gdzie

$$G_n = \left[\begin{array}{cccc}
\frac{\partial \ln L_1(\theta_n)}{\partial \theta_1} & \frac{\partial \ln L_1(\theta_n)}{\partial \theta_2} & \ldots & \frac{\partial \ln L_1(\theta_n)}{\partial \theta_K} \\
\frac{\partial \ln L_2(\theta_n)}{\partial \theta_1} & \frac{\partial \ln L_2(\theta_n)}{\partial \theta_2} & \ldots & \frac{\partial \ln L_2(\theta_n)}{\partial \theta_K} \\
\vdots & \vdots & \vdots & \vdots \\
\frac{\partial \ln L_N(\theta_n)}{\partial \theta_1} & \frac{\partial \ln L_N(\theta_n)}{\partial \theta_2} & \ldots & \frac{\partial \ln L_N(\theta_n)}{\partial \theta_K}
\end{array}\right], \qquad J_n = G_n'G_n$$

($G_n$ w tym zapisie jest macierzą $N\times K$ gradientów indywidualnych, w odróżnieniu od gradientu sumarycznego z metody Newtona.)

### Przykład — rozkład Weibulla

$$f(x;k,\lambda) = \frac{k}{\lambda^k}x^{k-1}e^{-(x/\lambda)^k}, \qquad x \geq 0$$

$$\ln L_i(\theta) = \ln(k) - k\ln(\lambda) + (k-1)\ln(x_i) - \left(\frac{x_i}{\lambda}\right)^k$$

Dla $\theta = \left[\begin{array}{c}k \\ \lambda\end{array}\right]$:

$$G_n(\theta) = \left[\begin{array}{cc}
\frac{\partial \ln L_1(\theta_n)}{\partial k} & \frac{\partial \ln L_1(\theta_n)}{\partial \lambda} \\
\frac{\partial \ln L_2(\theta_n)}{\partial k} & \frac{\partial \ln L_2(\theta_n)}{\partial \lambda} \\
\vdots & \vdots \\
\frac{\partial \ln L_N(\theta_n)}{\partial k} & \frac{\partial \ln L_N(\theta_n)}{\partial \lambda}
\end{array}\right]$$

$$J_n = \left[\begin{array}{cc}
\sum_{i=1}^N \left(\frac{\partial \ln L_i(\theta_n)}{\partial k}\right)^2 & \sum_{i=1}^N \left(\frac{\partial \ln L_i(\theta_n)}{\partial k}\right)\left(\frac{\partial \ln L_i(\theta_n)}{\partial \lambda}\right) \\
\sum_{i=1}^N \left(\frac{\partial \ln L_i(\theta_n)}{\partial k}\right)\left(\frac{\partial \ln L_i(\theta_n)}{\partial \lambda}\right) & \sum_{i=1}^N \left(\frac{\partial \ln L_i(\theta_n)}{\partial \lambda}\right)^2
\end{array}\right]$$

### Interpretacja BHHH jako regresji pomocniczej

Przydatny sposób myślenia o strukturze algorytmu BHHH: niech $(N\times K)$ macierz $X$ oraz $(N\times 1)$ wektor $Y$ będą dane przez

$$X = \left[\begin{array}{cc}
\frac{\partial \ln L_1(\theta_n)}{\partial k} & \frac{\partial \ln L_1(\theta_n)}{\partial \lambda} \\
\frac{\partial \ln L_2(\theta_n)}{\partial k} & \frac{\partial \ln L_2(\theta_n)}{\partial \lambda} \\
\vdots & \vdots \\
\frac{\partial \ln L_N(\theta_n)}{\partial k} & \frac{\partial \ln L_N(\theta_n)}{\partial \lambda}
\end{array}\right], \qquad Y = \left[\begin{array}{c}1\\1\\1\\ \vdots \\ 1\end{array}\right]$$

Iterację algorytmu BHHH można zatem zapisać jako:

$$\theta_{n+1} = \theta_n + \left(X_n'X_n\right)^{-1}X_n'Y$$

gdzie $J_n = X_n'X_n$, $G_n = X_n'Y$ — czyli krok BHHH odpowiada wykonaniu regresji MNK jedynek $Y$ na macierzy gradientów indywidualnych $X$.

```{admonition} W R
:class: tip
Pakiet `maxLik` implementuje m.in. algorytm BHHH (`method="BHHH"`) oraz metodę Newtona-Raphsona (`method="NR"`) do maksymalizacji funkcji wiarygodności — patrz Henningsen, Toomet (2011), *maxLik: A package for maximum likelihood estimation in R*.
```

## Literatura

1. V.L. Martin, A.S. Hurn, D. Harris, *Econometric Modelling with Time Series: Specification, Estimation and Testing*, Cambridge University Press, 2012.
2. Henningsen, Arne and Toomet, Ott (2011). *maxLik: A package for maximum likelihood estimation in R*, Computational Statistics 26(3), 443–458.
