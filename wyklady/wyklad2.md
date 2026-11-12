# Wykład 2 — Testowanie hipotez statystycznych


## Schemat testowania hipotez statystycznych

1. Policzyć statystykę testową $t_{test}$.
2. Przy prawdziwości $H_0$ statystyka testowa ma pewien znany rozkład.
3. Obszar krytyczny $K$ zależny od hipotezy alternatywnej $H_1$.
4. Jeżeli $t_{test} \in K$, to dane są mało prawdopodobne.
5. Mało prawdopodobne dane mogą być podstawą do odrzucenia $H_0$.

## Testowanie hipotez — przykład

- $X_1, X_2, \ldots, X_n$ jest próbą losową z rozkładu normalnego $N(\mu, 1^2)$.
- Hipoteza zerowa: $H_0: \mu = \mu_0$.
- Statystyka testowa: $U = \dfrac{\bar{X}-\mu_0}{\sigma}\sqrt{n}$, przy prawdziwej $H_0$ ma rozkład $N(0,1)$.
- Alternatywa: $H_1: \mu \neq \mu_0 \Rightarrow K_1 = \left(-\infty, -u(1-\frac{\alpha}{2})\right) \cup \left(u(1-\frac{\alpha}{2}), +\infty\right)$.
- $\{X_1,\ldots,X_5\} = \{-0.6256417;\ -2.3999373;\ -0.2979613;\ -1.5966765;\ 1.3804601\}$.
- $H_0: \mu = 0$, $U_{test} = -1.583027$.
- $K = (-\infty, -1.96) \cup (1.96, +\infty)$.
- $U_{test} \notin K$ — nie ma podstaw do odrzucenia $H_0$.

## Wartości krytyczne

Wartości krytyczne można odczytać z tablic statystycznych albo wyznaczyć funkcjami programu R. Przydatna jest ogólna tabela funkcji kwantylowych i gęstości dla popularnych rozkładów:

| Rozkład | Kwantyl | Gęstość |
|---|---|---|
| Normalny | `qnorm(p, mean, sd)` | `dnorm(x, mean, sd)` |
| Beta | `qbeta(p, s1, s2)` | `dbeta(x, s1, s2)` |
| $\chi^2_n$ | `qchisq(p, df)` | `dchisq(x, df)` |
| Wykładniczy | `qexp(p, rate)` | `dexp(x, rate)` |
| t-Studenta | `qt(p, df)` | `dt(x, df)` |
| Jednostajny(0,1) | `qunif(p, min, max)` | `dunif(x, min, max)` |
| Gamma | `qgamma(p, s, r)` | `dgamma(x, s, r)` |
| F-Snedecora | `qf(p, df1, df2)` | `df(x, df1, df2)` |
| Dwumianowy | `qbinom(p, s, p)` | `dbinom(x, s, p)` |
| Poissona | `qpois(p, lambda)` | `dpois(x, lambda)` |

## p-value (p-wartość)

- $H_0: \theta = \theta_0$, $\alpha$ jest poziomem istotności.
- Obszar krytyczny $K = \{T(X) > c_\alpha\}$.
- p-wartość jest równa $\mathbb{P}_{\theta_0}(T(X) > t_{test})$.

Wnioskowanie:

- Jeśli p-wartość $< \alpha$, to $H_0$ odrzucamy.
- Jeśli p-wartość $> \alpha$, to nie ma podstaw do odrzucenia $H_0$.

p-wartość w zależności od hipotezy alternatywnej:

- $H_1: \theta \neq \theta_0 \Rightarrow \text{p-value} = \mathbb{P}_{\theta_0}(T(X) > |t_{test}|)$
- $H_1: \theta < \theta_0 \Rightarrow \text{p-value} = \mathbb{P}_{\theta_0}(T(X) < t_{test})$
- $H_1: \theta > \theta_0 \Rightarrow \text{p-value} = \mathbb{P}_{\theta_0}(T(X) > t_{test})$

*(Za: A. Boratyńska, Wykłady ze statystyki matematycznej, II rok WNE, str. 84.)*

## Programowanie w R

Osoby, które nie miały wcześniej programowania, powinny zapoznać się i spróbować uruchomić kody wprowadzające do R — np. z materiałów Przemysława Biecka, *Przewodnik po pakiecie R* (2014, str. 37–45), lub Mikołaja Rybińskiego, *Krótkie wprowadzenie do R dla programistów* (str. 30–34).

```{admonition} Cel zajęć
:class: note
Podstawowe testy są zaprogramowane w R (np. w pakiecie bazowym czy w pakietach takich jak `stats`). Część zagadnień trzeba zapisać samemu — poniższe zadania koncentrują się właśnie na samodzielnym zaprogramowaniu procedury testu, a nie na użyciu gotowej funkcji.
```

## Zadania ilustrujące (do samodzielnego zaprogramowania)

**Zadanie 1*** (zadanie 6.12). Niech $X_1, X_2, \ldots, X_n$, $n>1$, będą niezależnymi zmiennymi losowymi o tym samym rozkładzie wykładniczym o gęstości

$$p_\lambda(x) = \lambda e^{\lambda x}\mathds{1}_{[0,\infty)}(x), \qquad \lambda>0.$$

Wiedząc, że zmienna losowa $T = 2\lambda\sum_{i=1}^{n}X_i \sim \chi^2_{2n}$, wyznaczyć $a$, $b$ tak, aby

$$P\{T<a\} = P\{T>b\} = \frac{\alpha}{2}.$$

Wyznaczyć na tej podstawie przedział ufności dla parametru $\lambda$ na poziomie ufności $1-\alpha$.

**Zadanie 2** (modyfikacja zadania 7.5). Niech $x_1, x_2, \ldots, x_n$ będą wynikami $n$-elementowej próby losowej pobranej z populacji, w której cecha $X$ ma rozkład jednostajny na przedziale $(0, \theta)$. Do weryfikacji hipotezy $H: \theta=\theta_0$ przy alternatywie $K: \theta>\theta_0$ zaproponowano test: gdy $\max(x_1,\ldots,x_n) = x_{n:n} \geq c$, hipotezę $H$ odrzucamy na korzyść $K$. Wykorzystując fakt, że statystyka $X_{n:n}$ ma rozkład o gęstości

$$f(z) = \begin{cases} \dfrac{n}{\theta^n}z^{n-1} & \text{gdy } z\in(0,\theta) \\ 0 & \text{w p.p.} \end{cases}$$

a) wyznaczyć stałą $c$ tak, aby rozmiar testu był równy 0,1;

b) dla realizacji $0.08436747,\ 1.04285094,\ 0.04980488,\ 1.19777030,\ 1.05726010$ zweryfikować hipotezę $H: \theta = \sqrt{2}$.
