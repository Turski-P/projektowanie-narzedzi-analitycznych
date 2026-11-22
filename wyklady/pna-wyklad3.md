# Wykład 3 — Wykresy w R, funkcje, testy diagnostyczne


## Wykresy w R

Wybrane funkcje do tworzenia wykresów:

- `plot` — tworzy wykresy: liniowe lub rozproszenia,
- `hist` — histogram,
- `barplot` — wykres słupkowy,
- `boxplot` — wykres pudełkowy,
- `qqnorm` — wykres kwantylowy,
- `curve(x^2, from=0, to=2)` — tworzy wykres krzywej określonej wzorem, argumentem jest x.

## QQ-plot (wykres kwantylowy)

Wykres kwantyl-kwantyl (Q-Q plot) to graficzna metoda porównywania dwóch rozkładów prawdopodobieństwa poprzez wykreślenie ich kwantyli względem siebie.

- Wybiera się zestaw przedziałów dla kwantyli. Punkt $(x,y)$ na wykresie odpowiada jednemu z kwantyli drugiego rozkładu (współrzędna y) skreślonemu z tym samym kwantylem pierwszego rozkładu (współrzędna x).
- Jeśli porównywane rozkłady są podobne, punkty na wykresie Q-Q będą leżeć w przybliżeniu na linii $y=x$. Jeśli rozkłady są liniowo powiązane, punkty będą leżeć w przybliżeniu na linii, ale nie musi to być $y=x$.
- Wykresy Q-Q można wykorzystać także do graficznego szacowania parametrów w rodzinie rozkładów typu położenie-skala.

*(Źródło: Wikipedia, „Q–Q plot”.)*

## Test Jarque-Bera

Test Jarque-Bera jest testem zgodności sprawdzającym, czy skośność i kurtoza próby odpowiadają rozkładowi normalnemu. Statystyka testowa JB dana jest wzorem

$$JB = \frac{n}{6}\left(S^2 + \frac{1}{4}(C-3)^2\right)$$

gdzie $n$ to liczba obserwacji, $S$ jest skośnością próby, a $C$ jest kurtozą próby:

$$S = \frac{\hat{\mu}_3}{\hat{\sigma}^3} = \frac{\frac{1}{n}\sum_{i=1}^n (x_i - \bar{x})^3}{\left(\frac{1}{n}\sum_{i=1}^n (x_i-\bar{x})^2\right)^{3/2}}, \qquad C = \frac{\hat{\mu}_4}{\hat{\sigma}^4} = \frac{\frac{1}{n}\sum_{i=1}^n (x_i-\bar{x})^4}{\left(\frac{1}{n}\sum_{i=1}^n (x_i-\bar{x})^2\right)^2}$$

gdzie $\hat{\mu}_3$ i $\hat{\mu}_4$ są odpowiednio oszacowaniami trzeciego i czwartego momentu centralnego, $\bar{x}$ jest średnią z próby, a $\hat{\sigma}^2$ jest oszacowaniem wariancji.

Jeśli dane pochodzą z rozkładu normalnego, statystyka JB asymptotycznie ma rozkład chi-kwadrat z dwoma stopniami swobody, więc może być wykorzystana do testowania hipotezy o normalności rozkładu danych.

```{admonition} Własności testu JB
:class: note
- Hipoteza zerowa jest łączną hipotezą o zerowej skośności i zerowej nadwyżkowej kurtozie.
- Próby z rozkładu normalnego mają oczekiwaną skośność 0 i oczekiwaną nadwyżkową kurtozę 0 (czyli kurtozę równą 3). Każde odchylenie od tego zwiększa statystykę JB.
- Dla małych prób przybliżenie chi-kwadrat jest nadmiernie czułe i często odrzuca prawdziwą $H_0$.
- Rozkład p-wartości odbiega od jednostajnego i staje się prawoskośnym rozkładem jednomodalnym, szczególnie dla małych p-wartości — co prowadzi do dużego błędu I rodzaju.
```

*(Źródło: Wikipedia, „Jarque–Bera test”.)*

## Różnica między skryptami a funkcjami

Skrypt (*script*) — każde jego wykonanie zapisuje wynik w zmiennej znajdującej się w globalnej przestrzeni roboczej (workspace). Funkcja (*function*) — ma własną, odrębną przestrzeń roboczą; wywołania funkcji nie nadpisują wartości zmiennych o tych samych nazwach w globalnym workspace.

*(Źródło: MathWorks, dokumentacja MATLAB — koncepcja analogiczna dotyczy R.)*

## Składnia funkcji w R

```r
y = function(arg) {
  wyrazenie
}
```

Przykład:

```r
norm <- function(x) {
  if (is.vector(x) == FALSE) {
    stop("x nie jest wektorem")
  }
  norm = sqrt(x %*% x)
  return(norm)
}
```

Wywołanie:

```r
norm(1:4)
```

## Pętla `for`

```r
for (var in seq) {
  wyrazenie
}
```

Przykład:

```r
for (v in 1:10) {
  print(v)
}
```

## Pętla `while`

```r
while (cond) {
  wyrazenie
}
```

Przykład:

```r
n = 1
while (n < 10) {
  print(n)
  n = n + 1
}
```

## Wyrażenie `if`

```r
if (test_expression1) {
  statement1
} else if (test_expression2) {
  statement2
} else {
  statement4
}
```

Przykład:

```r
if (x < 0) {
  print("x jest ujemny")
} else if (x == 0) {
  print("x jest równy zero")
} else {
  print("x jest dodatni")
}
```

```{admonition} Do samodzielnego przećwiczenia
:class: tip
Napisanie procedur realizujących testy diagnostyczne (Durbina-Watsona, Ljunga-Boxa, chi-kwadrat niezależności) — patrz Jupyter Book z zadaniami, tydzień 3.
```
