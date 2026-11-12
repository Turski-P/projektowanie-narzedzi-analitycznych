# Zadania 3 — Wykresy, funkcje, testy diagnostyczne

## Wykresy

**Zadanie 1**

Za pomocą polecenia `curve` narysować wykresy funkcji określonych poniższymi wzorami:

a) $y=2x-4$,

b) $y=x^3-2x^2+x-6$ dla $x\in[0,1]$,

c) $y=\sin\left(\frac{10\pi}{3}x\right)$ dla $x\in[0,2\pi]$.

**Zadanie 2**

Za pomocą polecenia `read.csv` wczytać dane z pliku {download}`EngScoResults.csv <dane/EngScoResults.csv>`. Sporządzić wykresy rozproszenia dla:

a) liczby zdobytych goli przez Anglików,

b) liczby zdobytych goli przez Szkotów w meczach w Szkocji.

## QQ-plot

- W statystyce wykres kwantyl-kwantyl (Q-Q) jest wykresem probabilistycznym, który jest graficzną metodą porównywania dwóch rozkładów prawdopodobieństwa poprzez wykreślenie ich kwantyli względem siebie.
- Wybiera się zestaw przedziałów dla kwantyli. Punkt $(x,y)$ na wykresie odpowiada jednemu z kwantyli drugiego rozkładu (współrzędna y) skreślonemu z tym samym kwantylem pierwszego rozkładu (współrzędna x).
- Jeśli porównywane rozkłady są podobne, punkty na wykresie Q-Q będą leżeć w przybliżeniu na linii $y=x$. Jeśli rozkłady są liniowo powiązane, punkty będą leżeć w przybliżeniu na linii, ale nie musi to być $y=x$.
- Wykresy Q-Q można wykorzystać także do graficznego szacowania parametrów w rodzinie rozkładów typu położenie-skala.

*(Źródło: Wikipedia, „Q–Q plot”.)*

**Zadanie 3**

Sporządzić samodzielnie wykres kwantylowy dla zmiennej zapisanej w pliku {download}`PNA_Z03.csv <dane/PNA_Z03.csv>`, zakładając rozkład normalny zmiennej.

**Zadanie 4**

Wygenerować zmienną `tSt` zawierającą 1000 obserwacji z rozkładu t-Studenta z 3 stopniami swobody. Sporządzić wykres kwantylowy zmiennej z kwantylami z rozkładu:

a) normalnego,

b) t-Studenta z 3 stopniami swobody.

**Zadanie 5**

Wygenerować zmienną `wyk` zawierającą 10000 obserwacji z rozkładu wykładniczego z parametrem $\lambda=1$. Sporządzić wykres kwantylowy zmiennej z kwantylami teoretycznymi z rozkładu Gamma(1,1).

## Funkcje w R

**Zadanie 6**

Napisać funkcję *silnia*, która dla podanej liczby całkowitej zwróci wartość jej silni.

**Zadanie 7**

Napisać funkcję *ProcentZer*, która dla podanej macierzy zawierającej 0 i 1 zwróci udział liczby zer w liczbie elementów macierzy.

**Zadanie 8**

Napisać funkcję *PoleProstokata*, która dla podanych długości boków wylicza pole prostokąta. Jeżeli długość drugiego boku nie będzie podana, to domyślnie ma być przyjmowana wartość:

a) 10,

b) długości pierwszego boku.

## Test Jarque-Bera

Statystyka testowa JB dana jest wzorem

$$JB=\frac{n}{6}\left(S^{2}+\frac{1}{4}(C-3)^{2}\right)$$

gdzie $n$ to liczba obserwacji, $S$ — skośność próby, $C$ — kurtoza próby, a $k$ — liczba regresorów:

$$S=\frac{\hat{\mu}_{3}}{\hat{\sigma}^{3}}=\frac{\frac{1}{n}\sum_{i=1}^{n}(x_{i}-\bar{x})^{3}}{\left(\frac{1}{n}\sum_{i=1}^{n}(x_{i}-\bar{x})^{2}\right)^{3/2}}, \qquad
C=\frac{\hat{\mu}_{4}}{\hat{\sigma}^{4}}=\frac{\frac{1}{n}\sum_{i=1}^{n}(x_{i}-\bar{x})^{4}}{\left(\frac{1}{n}\sum_{i=1}^{n}(x_{i}-\bar{x})^{2}\right)^{2}}$$

Jeśli dane pochodzą z rozkładu normalnego, statystyka JB asymptotycznie ma rozkład chi-kwadrat z dwoma stopniami swobody.

*(Źródło: Wikipedia, „Jarque–Bera test”.)*

**Zadanie 9**

Napisać program/procedurę realizującą test Jarque-Bera. Program powinien zwracać wartość statystyki testowej, p-value oraz zmienną zero-jedynkową z wynikiem testu (odrzucenie/nieodrzucenie $H_0$).

**Zadanie 10**

Wykorzystać program z zadania 9 do sprawdzenia normalności rozkładu zmiennej z zadania 3.

**Zadanie 11**

Przeprowadzić eksperyment składający się z 10 tysięcy powtórzeń wygenerowania zmiennej o 100 obserwacjach z rozkładu t-Studenta z 12 stopniami swobody i przeprowadzeniu testu JB. W każdym powtórzeniu zapisujemy wynik (statystykę testową lub wynik zero-jedynkowy). Sprawdzić, w jakim procencie przypadków test wskazuje prawidłowy wynik.

**Zadanie 12**

Wygenerować zmienną o 30 obserwacjach z rozkładu normalnego ze średnią 4 i odchyleniem standardowym 2. Sprawdzić normalność rozkładu za pomocą testu JB.

## Test Durbina-Watsona

Najpopularniejszym testem służącym do weryfikacji hipotezy o braku autokorelacji czynników losowych jest test Durbina-Watsona. Hipotezy zerową i alternatywną formułujemy jako:

$$H_{0}: \ Cov(\varepsilon_{t}, \varepsilon_{t-1}) = 0, \qquad H_{1}: \ Cov(\varepsilon_{t}, \varepsilon_{t-1}) \neq 0 \quad \text{dla } t=1,\ldots,T$$

Hipoteza zerowa mówi o braku autokorelacji pierwszego rzędu, czyli braku korelacji między $\varepsilon_t$ a $\varepsilon_{t-1}$. Ogólniej, o autokorelacji rzędu $s$ mówimy, gdy występuje autokorelacja między $\varepsilon_t$ a $\varepsilon_{t-s}$, gdzie $s\geq 1$.

Statystykę DW liczymy ze wzoru:

$$DW = \frac{\sum_{t=2}^{T}(e_{t}-e_{t-1})^{2}}{\sum_{t=2}^{T}e_{t}^{2}} = \frac{2\sum_{t=1}^{T}e_{t}^{2}-2\sum_{t=1}^{T}e_{t}e_{t-1}-e_{1}^{2}-e_{T}^{2}+2e_{1}e_{0}}{\sum_{t=1}^{T}e_{t}^{2}} = 2(1-\hat{\rho}_{\varepsilon_{t},\varepsilon_{t-1}})-\frac{e_{1}^{2}+e_{T}^{2}-2e_{1}e_{0}}{\sum_{t=1}^{T}e_{t}^{2}}$$

gdzie $e_t$ są resztami z regresji, a $\hat{\rho}$ jest współczynnikiem korelacji empirycznej między $e_t$ i $e_{t-1}$:

$$\hat{\rho}_{e_{t},e_{t-1}}=\frac{\sum_{t=1}^{T}e_{t}e_{t-1}}{\sum_{t=1}^{T}e_{t}^{2}}$$

Wnioskowanie na podstawie wyliczonej statystyki DW:

1. Jeśli $DW<2$:
   a) $DW<d_L$: odrzucamy $H_0$, przyjmujemy hipotezę o dodatniej autokorelacji;
   b) $d_L<DW<d_U$: brak konkluzji;
   c) $DW>d_U$: nie ma podstaw do odrzucenia $H_0$ o braku autokorelacji.
2. Jeśli $DW>2$:
   a) $DW>4-d_L$: odrzucamy $H_0$, przyjmujemy hipotezę o ujemnej autokorelacji;
   b) $4-d_U<DW<4-d_L$: brak konkluzji;
   c) $DW<4-d_U$: nie ma podstaw do odrzucenia $H_0$ o braku autokorelacji.

*(Na podstawie: J. Mycielski, Skrypt do ekonometrii, str. 204–205.)*

**Zadanie 13**

Napisać program/procedurę realizującą test Durbina-Watsona. Program powinien zwracać wartość statystyki testowej.

## Test Ljunga-Boxa

Model powinien się charakteryzować oszacowaniami $\varepsilon_t$ (resztami $e_t$), które są nieskorelowane w czasie. Testem diagnostycznym badającym hipotezę o nieskorelowaniu $\varepsilon_t$ jest test Ljunga-Boxa postaci:

$$Q = n(n+2)\sum_{k=1}^{m}\frac{\hat{\rho}_{k}^{2}}{n-k} \rightarrow \chi^{2}_{m}$$

gdzie

$$\hat{\rho}_{k}=\frac{(T-k)\sum_{t=k+1}^{T}(y_{t}-\bar{y})(y_{t-k}-\bar{y})}{T^{-1}\sum_{t=1}^{T}(y_{t}-\bar{y})^{2}}$$

jest empirycznym współczynnikiem korelacji rzędu $k$, a $m$ jest liczbą współczynników korelacji uwzględnionych przy liczeniu statystyki.

$H_0: \rho_1=\rho_2=\ldots=\rho_m=0$.

Test Q Ljunga-Pierce'a ma bardzo podobną statystykę testową:

$$Q_{BP}=n\sum_{k=1}^{h}\hat{\rho}_{k}^{2}$$

i wykorzystuje ten sam zbiór krytyczny co test Ljunga-Boxa. Za pomocą symulacji można pokazać, że statystyka Ljunga-Boxa jest lepsza dla wszystkich liczności próbek, również małych. *(Na podstawie: Wikipedia, „Ljung–Box test”.)*

**Zadanie 14**

Napisać program/procedurę realizującą test Ljunga-Boxa. Program powinien zwracać wartość statystyki testowej, p-value oraz zmienną zero-jedynkową z wynikiem testu (odrzucenie/nieodrzucenie $H_0$).

## Test chi-kwadrat niezależności

$(X,Y)$ — dwuwymiarowa zmienna losowa o rozkładzie dyskretnym, tzn. $(X,Y)\in\{1,2,\ldots,r\}\times\{1,2,\ldots,s\}$. Niech

$$p_{i,j}=P(X=i \land Y=j), \qquad p_{i\bullet}=P(X=i)=\sum_{j=1}^{s}p_{i,j}, \qquad p_{\bullet j}=P(Y=j)=\sum_{i=1}^{r}p_{i,j}$$

$(X_1,Y_1),\ldots,(X_n,Y_n)$ — próba losowa, $N_{i,j}=\sum \mathbb{1}(X_l=i \land Y_l=j)$, $N_{i\bullet}=\sum_{j=1}^s N_{i,j}$, $N_{\bullet j}=\sum_{i=1}^r N_{i,j}$.

Dane przedstawiamy w tablicy kontyngencji:

| $x\backslash y$ | 1 | 2 | $\ldots$ | $s$ | $N_{i,\bullet}$ |
|---|---|---|---|---|---|
| 1 | $N_{1,1}$ | $N_{1,2}$ | $\ldots$ | $N_{1,s}$ | $N_{1,\bullet}$ |
| 2 | $N_{2,1}$ | $N_{2,2}$ | $\ldots$ | $N_{2,s}$ | $N_{2,\bullet}$ |
| $\ldots$ | $\ldots$ | $\ldots$ | $\ldots$ | $\ldots$ | $\ldots$ |
| $r$ | $N_{r,1}$ | $N_{r,2}$ | $\ldots$ | $N_{r,s}$ | $N_{r,\bullet}$ |
| $N_{\bullet,j}$ | $N_{\bullet,1}$ | $N_{\bullet,2}$ | $\ldots$ | $N_{\bullet,s}$ | $N$ |

Hipoteza zerowa: $H_0:$ $X$ i $Y$ są niezależne, tj. $H_0: p_{i,j}=p_{i,\bullet}\cdot p_{\bullet,j}$ dla $i=1,\ldots,r$, $j=1,\ldots,s$.

Nieznanymi parametrami są $p_{i,\bullet}$ i $p_{\bullet,j}$. Ich estymatory największej wiarogodności to $\hat{p}_{i,\bullet}=\frac{N_{i,\bullet}}{N}$, $\hat{p}_{\bullet,j}=\frac{N_{\bullet,j}}{N}$. Estymatory parametrów $p_{i,j}$ są postaci $\hat{p}_{i,j}=\hat{p}_{i,\bullet}\hat{p}_{\bullet,j}=\frac{N_{i,\bullet}}{N}\frac{N_{\bullet,j}}{N}$.

Statystyka testu chi-kwadrat ma postać

$$\chi^{2}_{test}=\sum_{i=1}^{r}\sum_{j=1}^{s}\frac{\left(N_{i,j}-\frac{N_{i,\bullet}N_{\bullet,j}}{N}\right)^{2}}{\frac{N_{i,\bullet}N_{\bullet,j}}{N}}$$

Jeżeli $n\to\infty$, to rozkład statystyki $\chi^2_{test}$ zbiega do rozkładu $\chi^2\left((r-1)(s-1)\right)$. Hipotezę $H_0$ odrzucamy, gdy $\chi^2_{test}>\chi^2(\alpha,(r-1)(s-1))$.

*(Za: Boratyńska A., Wykłady ze statystyki matematycznej, II rok WNE.)*

**Zadanie 15** (zadanie 11.2 z [2])

W celu zbadania zależności pomiędzy płcią klientów i ich preferencjami wylosowano próbę 200 kobiet i mężczyzn i zadano im pytanie: czy uważasz za lepszy produkt firmy A czy B? Wyniki:

| Wybrany produkt | kobiety | mężczyźni |
|---|---|---|
| wolę A | 20 | 45 |
| wolę B | 60 | 15 |
| nie widzę różnicy | 40 | 20 |

Zweryfikować hipotezę mówiącą, że preferencje klientów nie zależą od płci, na poziomie istotności 0,10.

**Zadanie 16** (zadanie 11.5 z [2])

Badano związek pomiędzy wykształceniem a zarobkami. Wykształcenie każdej z badanych osób sklasyfikowano jako podstawowe, średnie lub wyższe. Zarobki zostały sklasyfikowane na trzech poziomach:

| | podstawowe | średnie | wyższe |
|---|---|---|---|
| < 1000 | 54 | 78 | 128 |
| 1000–2000 | 75 | 122 | 73 |
| > 2000 | 71 | 40 | 49 |

Zweryfikować hipotezę o niezależności obu cech na poziomie istotności 0,025.

**Zadanie 17** (zadanie 11.6 z [2])

Pewien produkt można wytwarzać trzema metodami produkcji. Wysunięto hipotezę, że wadliwość nie zależy od metody produkcji. Wylosowano niezależnie od metody produkcji próbę 270 sztuk i otrzymano wyniki:

| Metoda produkcji | jakość dobra | jakość zła |
|---|---|---|
| metoda I | 40 | 10 |
| metoda II | 80 | 60 |
| metoda III | 60 | 20 |

Zweryfikować hipotezę o niezależności wadliwości od metody produkcji.

## Zadania dodatkowe

**Zadanie 18** (pasma ufności dla wykresu kwantylowego)

Ocena „na oko”, czy punkty wykresu Q-Q leżą blisko prostej, jest subiektywna. Napisać funkcję
`qq_pasmo(x, R = 1000, poziom = 0.95)`, która:

a) rysuje wykres kwantylowy zmiennej `x` względem rozkładu normalnego wraz z prostą
   o wyrazie wolnym $\bar x$ i nachyleniu $S$;

b) generuje $R$ prób o liczności `length(x)` z rozkładu $N(\bar x, S^2)$, porządkuje każdą z nich
   rosnąco i dla każdej statystyki pozycyjnej $X_{(i)}$ wyznacza kwantyle empiryczne rzędu
   $\frac{1-\text{poziom}}{2}$ i $\frac{1+\text{poziom}}{2}$; otrzymane pasmo dorysować na wykresie.
   Rozwiązanie nie powinno zawierać pętli po replikacjach (wskazówka: macierz $R\times n$
   i funkcje `apply(..., 1, sort)` lub `matrixStats::rowSorts`, `matrixStats::colQuantiles`);

c) zwraca liczbę punktów leżących poza pasmem.

Zastosować funkcję do: zmiennej z pliku {download}`PNA_Z03.csv <dane/PNA_Z03.csv>`, zmiennej `tSt` z Zadania 4 oraz 50 obserwacji
z rozkładu $\chi^2_5$. Wyjaśnić, dlaczego pasmo jest najszersze na końcach. Czy pasmo punktowe
na poziomie 95% gwarantuje, że przy prawdziwej $H_0$ *wszystkie* punkty znajdą się w nim
z prawdopodobieństwem 0,95? Sprawdzić symulacyjnie.

**Zadanie 19** (test JB w małych próbach)

Statystyka JB ma rozkład $\chi^2_2$ tylko asymptotycznie.

a) Dla $n\in\{10, 20, 50, 100, 500, 2000\}$ wyznaczyć symulacyjnie (10 000 powtórzeń) rzeczywisty
   rozmiar testu JB z Zadania 9 przy $\alpha=0{,}05$ dla danych z rozkładu normalnego.
   Czy test jest liberalny, czy konserwatywny?

b) Wyznaczyć symulacyjne wartości krytyczne $c_n$ (kwantyl rzędu 0,95 statystyki JB przy $H_0$)
   i porównać je z $\chi^2_{2;\,0{,}95}\approx 5{,}99$.

c) Wykorzystując wartości $c_n$, porównać moc testu JB z mocą testu Shapiro-Wilka (`shapiro.test`)
   dla $n\in\{20, 50, 100\}$ przy alternatywach: $t_5$, $t_{12}$ (por. Zadanie 11), $\chi^2_{10}$,
   $U(0,1)$. Który test jest lepszy dla rozkładów symetrycznych o grubych ogonach, a który dla
   rozkładów o lekkich ogonach (np. jednostajnego)?

d) Wykazać, że przy $H_0$ zachodzi $E(S)=0$ oraz $\mathrm{Var}(S)\approx 6/n$,
   $E(C)\approx 3$, $\mathrm{Var}(C)\approx 24/n$, i zweryfikować te przybliżenia symulacyjnie.
   Wyjaśnić na tej podstawie postać statystyki JB.

**Zadanie 20** (test Durbina-Watsona: rozkład dokładny i moc)

Rozważmy model $y_t=\beta_0+\beta_1x_t+\varepsilon_t$, $t=1,\ldots,T$, w którym
$\varepsilon_t=\rho\,\varepsilon_{t-1}+u_t$, $u_t\sim N(0,1)$ i.i.d.

a) Ustalić $T=40$ i $x_t=t$. Przy $\rho=0$ wyznaczyć symulacyjnie rozkład statystyki DW
   (funkcja z Zadania 13) i jej kwantyl rzędu 0,05. Porównać go z tablicowymi wartościami
   $d_L$ i $d_U$ dla $T=40$, $k=1$.

b) Powtórzyć punkt a) dla $x_t\sim N(0,1)$ (wylosowanych raz i ustalonych) oraz dla
   $x_t=\sin(2\pi t/T)$. Wyjaśnić, dlaczego rozkład DW zależy od macierzy $X$ i skąd wobec
   tego bierze się w teście „obszar braku konkluzji”.

c) Wyznaczyć funkcję mocy testu (symulacyjna wartość krytyczna z punktu a), alternatywa
   $\rho>0$) dla $\rho\in\{0; 0{,}1; \ldots; 0{,}9\}$ i $T\in\{20, 40, 100\}$; wyniki przedstawić
   na jednym wykresie.

d) Pokazać symulacyjnie, że $DW\approx 2(1-\hat\rho_1)$, gdzie $\hat\rho_1$ jest autokorelacją
   reszt rzędu 1. Kiedy przybliżenie jest najgorsze?

e) Zbudować model z opóźnioną zmienną objaśnianą $y_t=\beta_0+\gamma y_{t-1}+\varepsilon_t$
   ($\gamma=0{,}5$) z autokorelacją $\varepsilon_t$ przy $\rho=0{,}4$. Sprawdzić symulacyjnie moc
   testu DW i wyjaśnić, dlaczego test ten nie powinien być stosowany w takich modelach.

**Zadanie 21** (Ljung-Box czy Box-Pierce, liczba stopni swobody)

a) Dla białego szumu gaussowskiego o długości $n\in\{30, 100, 500\}$ wyznaczyć symulacyjnie
   rzeczywisty rozmiar testów Ljunga-Boxa (funkcja z Zadania 14) i Boxa-Pierce'a dla
   $m\in\{5, 10, 20\}$, $\alpha=0{,}05$. Porównać wyniki z funkcją `Box.test`. Który test lepiej
   trzyma rozmiar i dlaczego? (Wskazówka: porównać $E(\hat\rho_k^2)$ z $1/n$.)

b) Wygenerować szereg AR(1) z $\phi=0{,}6$ o długości $n=200$, dopasować model AR(1)
   (`arima(x, order = c(1, 0, 0))`) i przeprowadzić test Ljunga-Boxa dla reszt przy $m=10$.
   Powtórzyć to 5 000 razy i wyznaczyć rozmiar testu, przyjmując rozkład $\chi^2_{10}$ oraz
   $\chi^2_{9}$ (argument `fitdf` w `Box.test`). Który wybór jest poprawny?

c) Sprawdzić symulacyjnie moc testu Ljunga-Boxa przeciwko alternatywie MA(1)
   $x_t=u_t+\theta u_{t-1}$, $\theta\in\{0{,}1; 0{,}2; 0{,}3\}$, dla $m=1$ oraz $m=20$, $n=100$.
   Skomentować wpływ wyboru $m$ na moc.

**Zadanie 22** (test chi-kwadrat przy małych licznościach)

Przybliżenie rozkładem $\chi^2$ wymaga dostatecznie dużych liczności oczekiwanych
(zwykle $N_{i\bullet}N_{\bullet j}/N\ge 5$).

a) Rozważmy tablicę $3\times 3$ o ustalonych sumach brzegowych: wierszowych $(5, 10, 15)$
   i kolumnowych $(4, 8, 18)$. Za pomocą funkcji `r2dtable` wygenerować 10 000 tablic zgodnych
   z $H_0$ (warunkowo względem sum brzegowych) i wyznaczyć rzeczywisty rozmiar testu
   chi-kwadrat przy $\alpha\in\{0{,}01; 0{,}05; 0{,}10\}$. Ile komórek ma liczność oczekiwaną
   mniejszą niż 5?

b) Na podstawie tych samych tablic wyznaczyć warunkowy (permutacyjny) p-value dla tablicy

   |   | 1 | 2 | 3 |
   |---|---|---|---|
   | 1 | 3 | 1 | 1 |
   | 2 | 1 | 5 | 4 |
   | 3 | 0 | 2 | 13 |

   i porównać go z p-value z `chisq.test(...)`, `chisq.test(..., simulate.p.value = TRUE, B = 1e4)`
   oraz `fisher.test(...)`. Wyjaśnić, dlaczego test permutacyjny z punktu b) i test Fishera
   odpowiadają tej samej hipotezie warunkowej.

c) Dla danych z Zadania 15 (produkty A/B a płeć) zbadać symulacyjnie moc testu chi-kwadrat:
   przyjmując za rozkład prawdziwy empiryczne częstości z tablicy, losować tablice o liczności
   $N\in\{30, 60, 100, 200\}$ (`rmultinom`) i wyznaczyć częstość odrzuceń $H_0$ przy $\alpha=0{,}10$.
   Jakie $N$ wystarcza, aby moc przekroczyła 0,9?

## Bibliografia

[1] Krysicki W., Bartos J., Dyczka W., Królikowska K., Wasilewski M., *Rachunek prawdopodobieństwa i statystyka matematyczna w zadaniach*, tom I i II, Wydawnictwo Naukowe PWN, Warszawa 2010.

[2] Boratyńska A., *Zadania na ćwiczenia ze statystyki matematycznej*.