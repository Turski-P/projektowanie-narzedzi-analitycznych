# Wykład 5 — Metoda Największej Wiarygodności (wprowadzenie)


## Funkcja wiarygodności — zmienna dyskretna

Niech $f(x;\theta)$ będzie rozkładem prawdopodobieństwa **dyskretnej** zmiennej losowej z parametrem $\theta$. Załóżmy, że $X_1, X_2, \ldots, X_n$ są niezależną próbą losową z tego rozkładu, a $x_1, x_2, \ldots, x_n$ są zaobserwowanymi wartościami tych zmiennych losowych.

Wówczas funkcją wiarygodności dla parametru $\theta$ jest

$$L(\theta|x_1,x_2,\ldots,x_n) = P(X_1=x_1,X_2=x_2,\ldots,X_n=x_n) = P(X_1=x_1)P(X_2=x_2)\cdots P(X_n=x_n) = f(x_1;\theta)f(x_2;\theta)\cdots f(x_n;\theta) = \prod_{i=1}^n f(x_i;\theta)$$

Funkcja wiarygodności jest funkcją $\theta$; bywa oznaczana $L(\theta) = L(\theta|x_1,x_2,\ldots,x_n)$.

*(Źródło: Chihara, Hesterberg, Mathematical Statistics with Resampling and R, str. 137.)*

## Funkcja wiarygodności — zmienna ciągła

Niech $f(x;\theta)$ będzie rozkładem prawdopodobieństwa **ciągłej** zmiennej losowej z parametrem $\theta$. Analogicznie:

$$L(\theta|x_1,\ldots,x_n) = f(x_1;\theta)f(x_2;\theta)\cdots f(x_n;\theta)$$

Oszacowaniem największej wiarygodności (MNW) parametru $\theta$ jest statystyka $\hat{\theta}$, która maksymalizuje funkcję wiarygodności $L(\theta)$:

$$L(\hat{\theta}) \geq L(\theta) \quad \text{dla każdego } \theta$$

*(Źródło: tamże, str. 139.)*

## Przykład — rzut monetą

Załóżmy, że kupiliśmy monetę w sklepie z magicznymi rekwizytami. Moneta wygląda na symetryczną, ale nie koniecznie taka jest. Rzuciliśmy monetą 8 razy i otrzymaliśmy OOOROROR. Jaka wartość będzie dobrym oszacowaniem $p$, prawdopodobieństwa orła?

Niech $X_i \sim Bern(p)$, gdzie $X_i$ oznacza orła. Zakładając niezależność wyników rzutów:

$$P(X_1=1,X_2=1,X_3=1,X_4=0,X_5=1,X_6=0,X_7=1,X_8=0) = P(X_1=1)\cdots P(X_8=0) = p^5(1-p)^3$$

Estymator MNW: $\hat{p}_{MNW} = 5/8$.

*(Źródło: tamże, str. 136.)*

## Metoda Newtona-Raphsona

Do znajdowania maksimum funkcji wiarygodności (kiedy nie da się go wyznaczyć analitycznie) wykorzystuje się metody numeryczne, z których najbardziej klasyczna to metoda Newtona (Newtona-Raphsona).

```{admonition} Dobre omówienie z przykładami
:class: note
Włodzimierz Krysicki, Lech Włodarski, *Analiza matematyczna w zadaniach*, tom I, rozdział XIV: *Przybliżone rozwiązywanie równań i układów*, Wydawnictwo Naukowe PWN.
```

### Metoda — idea

1. Zaczynamy od jakiegoś punktu startowego $\theta_0$.
2. Jeżeli wartość funkcji w tym punkcie jest różna od zera, wyznaczamy styczną do funkcji w tym punkcie i wyliczamy jej punkt przecięcia z osią X — otrzymujemy nowy punkt $\theta_1$.
3. Powtarzamy punkty (1) i (2), dopóki nie uzyskamy zbieżności, czyli dopóki nie otrzymamy takiego $\theta_n$, że w następnym kroku daje on siebie samego.

### Przykład (zadanie 14.2, Krysicki-Włodarski)

Za pomocą metody Newtona znaleźć miejsce zerowe funkcji

$$f(x) = x^3 - 2x^2 - 4x - 7$$

w przedziale $(3; 4)$.

$$f(3) = 27-18-12-7 = -10 < 0, \qquad f(4) = 64-32-16-7 = 9 > 0$$

Wyjdźmy z punktu $\theta_0 = x_0 = 4$. Styczna do funkcji $f(x)$ w $x_0$:

$$y - y_0 = f'(x)(x-x_0)$$

Pochodna $f(x)$ to $f'(x) = 3x^2 - 4x - 4$, a $f'(x_0=4) = 48-16-4 = 28$. Styczna do $f(x)$ w punkcie $x_0=4$:

$$y - 9 = 28(x-4) \implies y = 28x - 103$$

Styczna przecina się z osią X w punkcie $y=0$, czyli dla $x_1 = \frac{103}{28} = 3.678$.

Następny krok: wyznaczamy wartość funkcji $f(x)$ w punkcie $x_1 = 3.678$ i jeśli jest różna od zera, wyznaczamy styczną itd.

## Metoda Newtona — wzór ogólny

Metoda Newtona do znajdowania miejsca zerowego:

$$y - y_0 = f'(x)(x-x_0), \qquad f'(x_0) = \frac{f(x_0)-0}{x-x_0}, \qquad x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}$$

W maksymalizacji funkcji metodą Newtona znajduje się miejsce zerowe pochodnej:

$$x_{n+1} = x_n - \frac{f'(x_n)}{f''(x_n)}$$

To właśnie ten wariant wykorzystuje się do numerycznego wyznaczania estymatorów MNW, gdy warunki pierwszego rzędu (zerowanie się pochodnej log-wiarygodności) nie mają rozwiązania analitycznego — rozwinięcie tego podejścia na przypadek wielowymiarowy (kilka parametrów jednocześnie) omówione jest na następnym wykładzie.

## Literatura

1. Krysicki W., Bartos J., Dyczka W., Królikowska K., Wasilewski M., *Rachunek prawdopodobieństwa i statystyka matematyczna w zadaniach*, tom I i II, Wydawnictwo Naukowe PWN, Warszawa 2010.
2. Boratyńska A., *Zadania na ćwiczenia ze statystyki matematycznej*.
3. Laura Chihara, Tim Hesterberg, *Mathematical Statistics with Resampling and R*, John Wiley & Sons, 2011.
