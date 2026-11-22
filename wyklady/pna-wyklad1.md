# Wykład 1 — Wstęp do kursu, R i R Markdown, wektory i macierze

## Wprowadzenie do programu R

Zanim przejdziemy do konkretnych obliczeń, poniżej znajduje się krótki przewodnik po R i R Markdown — jak pisać w R oraz jak tworzyć dokumenty R Markdown. Ta część nie pochodzi z oryginalnych materiałów prowadzącego zajęcia; została dodana jako uzupełnienie na potrzeby tego kursu.

### Czym jest R?

R jest językiem programowania i środowiskiem do obliczeń statystycznych oraz tworzenia wykresów. Kod R uruchamia się w konsoli R (bezpośrednio) albo zapisuje w plikach `.R` (skrypty) i wykonuje fragment po fragmencie lub w całości.

Podstawowa składnia:

```r
# Komentarz zaczyna się od znaku #
x <- 5          # przypisanie wartości do zmiennej (operator <- jest standardem w R)
y = 3           # znak = też działa jako przypisanie, ale <- jest bardziej idiomatyczny
x + y           # wyświetla wynik: 8
print(x + y)    # to samo, ale explicite
```

Podstawowe typy danych: liczby (`numeric`), wektory tekstowe (`character`), wartości logiczne (`logical`: `TRUE`/`FALSE`), wektory (`vector`), macierze (`matrix`), ramki danych (`data.frame`), listy (`list`).

```{admonition} Wskazówka
:class: tip
Operator `<-` można wpisać szybko w RStudio kombinacją klawiszy `Alt` + `-` (Windows/Linux) lub `Option` + `-` (Mac).
```

### Instalacja i wczytywanie pakietów

R ma bogaty ekosystem dodatkowych pakietów (bibliotek):

```r
install.packages("nazwa_pakietu")   # instalacja (jednorazowo)
library(nazwa_pakietu)              # wczytanie pakietu w danej sesji
```

### Podstawowe operacje

```r
# Operacje arytmetyczne
2 + 2
3 * 4
10 / 3
2^3          # potęgowanie
sqrt(16)     # pierwiastek kwadratowy

# Wektory
v <- c(1, 2, 3, 4, 5)   # funkcja c() (combine) tworzy wektor
v[2]                     # drugi element wektora
length(v)                # długość wektora
sum(v)                   # suma elementów
mean(v)                  # średnia

# Funkcje własne
kwadrat <- function(x) {
  return(x^2)
}
kwadrat(5)   # 25

# Pętle i warunki
for (i in 1:5) {
  print(i)
}

if (x > 0) {
  print("dodatnie")
} else {
  print("niedodatnie")
}
```

### Czym jest R Markdown?

R Markdown to format dokumentów, który łączy **tekst sformatowany w Markdown** z **kodem R, który jest wykonywany, a jego wyniki (tekst, tabele, wykresy) automatycznie wstawiane do dokumentu**. Plik R Markdown ma rozszerzenie `.Rmd`. Jest to szczególnie przydatne przy pisaniu raportów, prac zaliczeniowych czy projektów, w których chcemy pokazać zarówno kod, jak i jego wyniki, w jednym gotowym dokumencie (HTML, PDF, Word).

#### Struktura pliku `.Rmd`

Każdy dokument R Markdown zaczyna się nagłówkiem YAML, po którym następują fragmenty tekstu Markdown przeplatane blokami kodu R (tzw. *chunki*):

```markdown
---
title: "Mój raport"
author: "Imię Nazwisko"
date: "2024-01-01"
output: html_document
---

## Wprowadzenie

To jest zwykły tekst w formacie Markdown. Można używać **pogrubienia**,
*kursywy* oraz list:

- punkt pierwszy
- punkt drugi

## Analiza danych

Poniższy fragment kodu (tzw. *code chunk*) zostanie wykonany, a jego
wynik pojawi się w wygenerowanym dokumencie:

\`\`\`{r}
x <- rnorm(100)
mean(x)
hist(x)
\`\`\`
```

Elementy składni:

- **Nagłówek YAML** (między `---`): określa tytuł, autora, datę oraz format wyjściowy (`html_document`, `pdf_document`, `word_document`).
- **Tekst Markdown**: `#`, `##`, `###` — nagłówki różnych poziomów; `**tekst**` — pogrubienie; `*tekst*` — kursywa; `-` lub `*` na początku linii — lista wypunktowana.
- **Bloki kodu (chunki)**: zaczynają się od ```` ```{r} ```` i kończą ```` ``` ````. Wewnątrz nawiasów klamrowych można podać nazwę chunka i opcje, np. ```` ```{r nazwa-chunka, echo=FALSE, fig.width=6} ````.

#### Najważniejsze opcje chunków

| Opcja | Działanie |
|---|---|
| `echo=FALSE` | nie pokazuje kodu, tylko wynik jego działania |
| `eval=FALSE` | pokazuje kod, ale nie wykonuje go |
| `include=FALSE` | wykonuje kod, ale nie pokazuje ani kodu, ani wyniku |
| `warning=FALSE` | ukrywa ostrzeżenia |
| `message=FALSE` | ukrywa komunikaty (np. przy wczytywaniu pakietów) |
| `fig.width`, `fig.height` | rozmiar generowanych wykresów |

#### Wzory matematyczne w R Markdown

R Markdown wspiera LaTeX-owy zapis matematyczny (przez MathJax/KaTeX). Wzór w linii tekstu otacza się jednym znakiem dolara: `$\hat{\beta} = (X'X)^{-1}X'y$`, co daje $\hat{\beta} = (X'X)^{-1}X'y$. Wzór wyśrodkowany, na osobnej linii, otacza się dwoma znakami dolara:

```markdown
$$
\bar{X} = \frac{1}{n}\sum_{i=1}^{n} X_i
$$
```

#### Kompilacja (renderowanie) dokumentu

Aby przekształcić plik `.Rmd` w gotowy dokument HTML/PDF/Word, potrzebny jest pakiet `rmarkdown` (oraz `knitr`, od którego zależy):

```r
install.packages("rmarkdown")
```

Renderowanie można wykonać dwoma sposobami:

1. **W RStudio**: kliknięcie przycisku **Knit** nad edytorem otwartego pliku `.Rmd`.
2. **Z konsoli R**:

```r
rmarkdown::render("moj_raport.Rmd")
```

Domyślny format wyjściowy określa pole `output` w nagłówku YAML; można też wymusić inny format, np.:

```r
rmarkdown::render("moj_raport.Rmd", output_format = "pdf_document")
```

```{admonition} Uwaga dotycząca PDF
:class: warning
Renderowanie do PDF wymaga zainstalowanej dystrybucji LaTeX (np. TinyTeX, instalowanej pakietem `tinytex::install_tinytex()`, albo pełnego MiKTeX/TeX Live).
```

#### Krótki przykład kompletnego dokumentu R Markdown

```markdown
---
title: "Analiza przykładowych danych"
author: "Jan Kowalski"
output: html_document
---

## Cel analizy

W tym raporcie analizujemy 100 obserwacji wygenerowanych z rozkładu
normalnego standardowego.

\`\`\`{r generowanie-danych}
set.seed(123)
x <- rnorm(100, mean = 0, sd = 1)
summary(x)
\`\`\`

Histogram rozkładu:

\`\`\`{r histogram, fig.width=6, fig.height=4}
hist(x, main = "Histogram próbki", xlab = "wartość")
\`\`\`

Średnia z próby wynosi $\bar{x} = `r round(mean(x), 3)`$.
```

Zwróć uwagę na ostatnią linijkę — zapis `` `r kod` `` (tzw. *inline code*) pozwala wstawić wynik obliczenia R prosto w tekst, bez tworzenia osobnego chunka.

---

## Okno programu R

Podstawowe okno programu R (lub środowiska RStudio) składa się zazwyczaj z konsoli (do wpisywania i wykonywania poleceń), edytora skryptów, panelu ze zmiennymi w danej sesji (*Environment*) oraz panelu z wykresami, plikami i pomocą.

## Działania matematyczne

Przykładowe podstawowe operacje do przećwiczenia w konsoli R:

```r
1 + 1
2 + 2 * 2
8 * 6
8 * 6 - 40
3 * 2^3 - 100^0
sqrt(49)
(5 - 3) / (2 - 1)
2^(3 - 1)
8^1.5
```

```{admonition} Polecenia
:class: tip
Strzałka **↑** w konsoli R przywołuje poprzednio wykonane polecenie — bardzo przydatne przy poprawianiu drobnych błędów.
```

## Generowanie wektorów

Trzy podstawowe sposoby generowania wektorów w R:

1. **Operator `:`** (dwukropek) — generuje wektor liczb całkowitych z określonego przedziału. Zapis `1:10` jest równoważny `c(1,2,3,4,5,6,7,8,9,10)`.
2. **Funkcja `seq`** — pozwala na generowanie wartości od jednej granicy do drugiej, z krokiem innym niż 1. Np. `seq(-5, 5, by=0.2)` jest równoważne `c(-5, -4.8, -4.6, ..., 4.6, 4.8, 5)`. To samo można osiągnąć podając liczbę elementów ciągu (równomierny krok dobiera się sam): `seq(-5, 5, length=51)`.
3. **Funkcja `rep`** — pozwala na powtórzenie wektora określoną liczbę razy, np. `rep(c(1,2), 2)` jest równoważne `c(1,2,1,2)`. Jeśli drugi argument jest wektorem o długości takiej samej jak pierwszy, każdy z elementów pierwszego wektora jest powtarzany tyle razy, ile wynosi odpowiadająca mu wartość w drugim wektorze.

Do tworzenia wektorów bez szczególnego wzorca służy funkcja `c()` (*combine*):

```r
c(1, 4, 8, 2, 9)
```

### Ćwiczenie: utwórz wektory

$$\left[\begin{array}{c}0\\0\\0\\0\\0\end{array}\right] \quad \left[\begin{array}{c}17\\17\\17\\17\end{array}\right] \quad \left[\begin{array}{c}1\\2\\3\\\vdots\\10\end{array}\right] \quad \left[\begin{array}{c}8\\6\\4\\2\\0\end{array}\right]$$

### Odwołanie się do elementów wektora

Do wybrania fragmentu wektora służy notacja `wektor[indeks]`:

```r
z <- c(8, 3, 0, 9, 9, 2, 1, 3)

z[4]              # czwarty element z
z[c(1, 3, 4)]     # pierwszy, trzeci i czwarty element
z[-c(1, 3, 4)]    # wszystkie elementy oprócz pierwszego, trzeciego i czwartego

which(z < 4)        # które pozycje mają wartość z < 4?
index <- which(z < 4)
z[index]            # zwraca z[c(2, 3, 6, 7)]
```

### Ćwiczenie 1

- Utwórz wektor $z=\left[\begin{array}{cccccccccc}0&-1&2&-3&4&-5&6&-7&8&-9\end{array}\right]^{T}$.
- Utwórz 10-elementowy wektor `z2` zawierający 0 dla dodatnich elementów wektora `z` oraz 1 dla elementów ujemnych i zerowych.
- Utwórz wektor `z3` zawierający tylko ujemne elementy wektora `z`.
- Utwórz wektor `y` równy wektorowi `z`.
- Zamień ujemne elementy wektora `y` na wartości 999.

## Generowanie macierzy

Podstawowa funkcja do tworzenia macierzy:

```r
matrix(data = NA, nrow = 1, ncol = 1, byrow = FALSE, dimnames = NULL)
```

| Argument | Znaczenie |
|---|---|
| `data` | opcjonalny wektor danych (może być listą albo wektorem wyrażeń) |
| `nrow` | żądana liczba wierszy |
| `ncol` | żądana liczba kolumn |
| `byrow` | logiczne; jeśli `FALSE` (domyślnie), macierz jest wypełniana kolumnami, w przeciwnym razie wierszami |

### Ćwiczenie: utwórz macierze

$$A=\left[\begin{array}{cc}0&0\\0&0\end{array}\right] \quad B=\left[\begin{array}{cc}1&2\\3&4\end{array}\right] \quad C=\left[\begin{array}{cc}1&1\\1&1\end{array}\right] \quad D=\left[\begin{array}{rr}5&-5\\-5&10\end{array}\right]$$

## Łączenie macierzy

Funkcje `cbind` i `rbind` formują tablice z podanych wektorów, umieszczając je odpowiednio kolumnami lub wierszami w nowo tworzonej tabeli.

### Ćwiczenie: utwórz macierz blokową

$$K=\left[\begin{array}{rrcrrcrr}1&1&\phantom{a}&0&0&\phantom{a}&0&0\\
1&1&&0&0&&0&0\\
&&&&&&&\\
0&0&&1&2&&0&0\\
0&0&&3&4&&0&0\\
&&&&&&&\\
5&-5&&0&0&&1&1\\
-5&10&&0&0&&1&1\end{array}\right]$$

Wskazówka: macierz $K$ jest macierzą blokową, złożoną z czterech mniejszych macierzy $2\times 2$ (odpowiadających macierzom $C$, zerowej, $B$ i $D$ z poprzedniego ćwiczenia) — najprościej ją zbudować, łącząc te bloki za pomocą `cbind` i `rbind`.
