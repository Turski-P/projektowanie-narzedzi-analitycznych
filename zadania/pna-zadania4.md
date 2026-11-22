# Zadania 4 — Test Jarque-Bera i Metoda Najmniejszych Kwadratów

## Test Jarque-Bera

**Zadanie 1**

Sprawdzić normalność rozkładu zmiennej:

a) {download}`vec1 <dane/vec1.csv>`,

b) {download}`vec2 <dane/vec2.csv>`,

c) {download}`vec3 <dane/vec3.csv>`,

d) {download}`vec4 <dane/vec4.csv>`.

**Zadanie 2**

Przeprowadzić eksperyment składający się z 10 tysięcy powtórzeń wygenerowania zmiennej o 100 obserwacjach z rozkładu t-Studenta z 12 stopniami swobody i przeprowadzeniu testu JB. W każdym powtórzeniu zapisujemy wynik (statystykę testową lub wynik zero-jedynkowy). Sprawdzić, w jakim procencie przypadków test wskazuje prawidłowy wynik.

**Zadanie 3**

Wygenerować zmienną o 30 obserwacjach z rozkładu normalnego ze średnią 4 i odchyleniem standardowym 2. Sprawdzić normalność rozkładu za pomocą testu JB. Zadanie powtórzyć 10000 razy. Sprawdzić, w jakim procencie przypadków test wskazuje prawidłowy wynik.

## Metoda Najmniejszych Kwadratów

**Zadanie 4**

Oszacować model ekonometryczny dla danych o samochodach postaci $cena_i=\beta_0+\beta_1 lpg_i+\varepsilon_i$:

1. cena=1, instalacja gazowa = nie,
2. cena=2, instalacja gazowa = tak,
3. cena=3, instalacja gazowa = nie.

**Zadanie 5**

Dla zbioru obserwacji $(x;y)\in\{(1;1);(2;2);(3;1)\}$ dla modelu empirycznego postaci

$$y_{i}=\beta_{0}+\beta_{1}x_{i}+\varepsilon_{i}$$

wyznaczyć $Cov(\widehat{\beta}_{0},\widehat{\beta}_{1})$.

**Zadanie 6**

Wykorzystując dane z pliku {download}`vacation.csv <dane/vacation.csv>` dla modelu liniowego postaci:

$$MILES_{i}=\beta_{0}+\beta_{1}INCOME_{i}+\beta_{2}AGE_{i}+\beta_{3}KIDS_{i}+\varepsilon_{i}$$

wyznaczyć:

1. estymatory parametrów $\beta$,
2. wartość wariancji reszt,
3. współczynniki determinacji $R^2$ oraz $\bar{R}^2$,
4. $Cov(\widehat{\beta}_1,\widehat{\beta}_2)$ oraz $Cov(\widehat{\beta}_2,\widehat{\beta}_2)$.

Dane pochodzą z zadania 8.4 z podręcznika *Principles of Econometrics*, Third Edition.

**Zadanie 7**

Wykorzystując dane z pliku {download}`vacation.csv <dane/vacation.csv>` dla modelu liniowego postaci:

$$MILES_{i}=\beta_{0}+\beta_{1}INCOME_{i}+\beta_{2}AGE_{i}+\beta_{3}KIDS_{i}+\varepsilon_{i}$$

oszacować model przy ograniczeniu $\beta_2=10$.

## Bibliografia

[1] Krysicki W., Bartos J., Dyczka W., Królikowska K., Wasilewski M., *Rachunek prawdopodobieństwa i statystyka matematyczna w zadaniach*, tom I i II, Wydawnictwo Naukowe PWN, Warszawa 2010.

[2] Boratyńska A., *Zadania na ćwiczenia ze statystyki matematycznej*.

[3] R. Carter Hill, William E. Griffiths, Guay C. Lim, *Principles of Econometrics*, Third Edition, John Wiley & Sons.