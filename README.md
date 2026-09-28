# Kawiarnia „Pod Gałęzią” — ćwiczenia z Gita

Na dzisiejszych zajęciach zajmiemy się dokumentami małej kawiarni: menu, przepisami
i godzinami otwarcia. Przy okazji przećwiczycie podstawowe polecenia Gita:
`init`, `clone`, `add`, `commit`, `branch`, `checkout` i `merge`.

Mamy na to mniej więcej półtorej godziny. Róbcie zadania po kolei — kolejne części
korzystają z tego, co zrobiliście wcześniej.

Dwie rady na start:

- Jeśli nie pamiętacie jakiegoś polecenia, zajrzyjcie do pliku `SCIAGA.md`.
- Po każdym zadaniu wpisujcie `git status` i `git log --oneline --graph --all`.
  Dzięki temu widać, co się właściwie stało, i łatwiej zrozumieć, co robi dane polecenie.

Przy niektórych zadaniach są pytania. Nie musicie nigdzie zapisywać odpowiedzi, ale
zastanówcie się nad nimi — wrócimy do nich na koniec zajęć.

---

## 0. Przygotowanie (ok. 5 min)

Otwórzcie terminal (na Windowsie **Git Bash**) i sprawdźcie, czy Git jest zainstalowany:

```bash
git --version
```

Git musi wiedzieć, kto robi zmiany — te dane pojawią się przy każdym waszym commicie:

```bash
git config --global user.name "Imię Nazwisko"
git config --global user.email "twoj@email.pl"
git config --global init.defaultBranch main
```

Ostatnia linijka sprawia, że główna gałąź w nowych repozytoriach będzie się nazywać `main`.
Sprawdźcie, czy wszystko się zapisało: `git config --global --list`.

---

## 1. Własne repozytorium od zera (ok. 20 min)

Zanim zaczniecie pracować w kawiarni, założycie własny mały projekt — pamiętnik baristy.

**1.1** Utwórzcie folder na projekt i zamieńcie go w repozytorium:

```bash
cd ~/Desktop
mkdir pamietnik-baristy
cd pamietnik-baristy
git init
```

Wpiszcie `ls -a`. Pojawił się ukryty folder `.git` — tam Git przechowuje całą historię
projektu. Wpiszcie też `git status` i przeczytajcie, co Git wam odpowiada.

*Pytanie: co by się stało, gdybyście usunęli folder `.git`?*

**1.2** Utwórzcie plik `o-mnie.txt` i wpiszcie do niego dwie linijki: jak macie na imię
i jaką kawę (albo herbatę) lubicie. Możecie to zrobić w edytorze albo z terminala:

```bash
echo "Nazywam się ..." > o-mnie.txt
echo "Najbardziej lubię ..." >> o-mnie.txt
```

Teraz po kolei:

1. `git status` — plik jest oznaczony jako *untracked*, czyli Git go jeszcze nie śledzi.
2. `git add o-mnie.txt` — dodajecie plik do poczekalni (*staging area*).
3. Jeszcze raz `git status` — porównajcie z poprzednim wynikiem.
4. `git commit -m "Dodaj plik o mnie"` — zapisujecie zmianę w historii.
5. `git log`, a potem `git log --oneline` — oglądacie historię.

**1.3** Zróbcie trzy kolejne commity, każdy z sensownym opisem:

- dodajcie plik `dzien1.txt` z jednym zdaniem o dzisiejszym dniu,
- dopiszcie do `o-mnie.txt` trzecią linijkę, np. ulubione ciasto
  (zanim zrobicie `git add`, wpiszcie `git diff` — zobaczycie dokładnie, co się zmieniło),
- utwórzcie naraz dwa pliki, `dzien2.txt` i `dzien3.txt`, i dodajcie oba jednym poleceniem `git add .`

**1.4** Zmieńcie coś zarówno w `dzien1.txt`, jak i w `dzien2.txt`. Dodajcie do poczekalni
**tylko** `dzien1.txt` i zróbcie commit. Potem `git status` — zmiana w `dzien2.txt` nadal
czeka. Zróbcie dla niej osobny commit.

*Pytanie: po co w ogóle jest poczekalnia? Czy nie prościej byłoby od razu zapisywać wszystkiego?*

Na koniec tej części `git log --oneline` powinien pokazywać co najmniej 6 commitów,
a `git status` — komunikat `nothing to commit, working tree clean`.

---

## 2. Klonowanie repozytorium (ok. 10 min)

Teraz dołączacie do zespołu kawiarni. Jej repozytorium już istnieje, więc nie zakładacie
nowego, tylko pobieracie gotowe.

**2.1** Wyjdźcie z folderu pamiętnika i sklonujcie repozytorium kawiarni (adres podam na zajęciach):

```bash
cd ..
git clone <adres-repozytorium> kawiarnia
cd kawiarnia
```

Zwróćcie uwagę, że tym razem nie było `git init` — `git clone` zrobił to za was
i od razu pobrał całą historię.

**2.2** Rozejrzyjcie się po repozytorium i spróbujcie odpowiedzieć na pytania:

- Ile commitów jest na gałęzi `main`? (`git log --oneline`)
- Kto i kiedy dodał przepis na latte? (`git log -- przepisy/latte.md`)
- Jakie gałęzie są w repozytorium? (`git branch`, a potem `git branch -a`)
- Co zmienił pierwszy commit? (`git show <hash>`)

*Pytanie: dlaczego `git branch` pokazuje tylko `main`, a `git branch -a` więcej gałęzi?*

**2.3** W folderze `goscie/` utwórzcie plik ze swoim imieniem i nazwiskiem, np.
`goscie/anna-kowalska.txt`, i wpiszcie do niego zamówienie, np. „Poproszę latte i sernik”.
Zróbcie commit z opisem w stylu `Dodaj zamówienie: Anna Kowalska`.

**2.4** Klonować można nie tylko z internetu, ale też z dysku. Spróbujcie:

```bash
cd ..
git clone pamietnik-baristy pamietnik-kopia
cd pamietnik-kopia
git log --oneline
```

Historia jest taka sama jak w oryginale. Potem wróćcie do folderu `kawiarnia`.

---

## 3. Gałęzie (ok. 15 min)

Gałąź to osobna linia pracy. Można na niej spokojnie eksperymentować i nie psuć
głównej wersji projektu, czyli `main`.

**3.1** Sprawdźcie, na której gałęzi jesteście: `git branch` (bieżąca jest oznaczona gwiazdką).
Utwórzcie nową gałąź i przełączcie się na nią:

```bash
git branch nowa-kawa
git branch
git checkout nowa-kawa
```

Zauważcie, że samo `git branch nowa-kawa` tworzy gałąź, ale was na nią nie przenosi.
Dopiero `git checkout` zmienia bieżącą gałąź.

**3.2** Kawiarnia chce wprowadzić flat white. Na gałęzi `nowa-kawa`:

1. utwórzcie plik `przepisy/flat-white.md` z krótkim przepisem (wzorujcie się na `espresso.md`),
2. dopiszcie do `menu.txt` w sekcji KAWA, zaraz pod latte, linijkę `Flat white ......... 14 zł`,
3. zróbcie commit.

Teraz wróćcie na główną gałąź (`git checkout main`) i obejrzyjcie `ls przepisy/` oraz `cat menu.txt`.
Gdzie się podział flat white? Przełączcie się znowu na `nowa-kawa` i sprawdźcie jeszcze raz.

*Pytanie: co dzieje się z plikami w folderze, kiedy przełączacie gałąź?*

**3.3** Gałąź można też utworzyć i od razu się na nią przełączyć jednym poleceniem:

```bash
git checkout main
git checkout -b eksperyment
```

Na gałęzi `eksperyment` zmieńcie cokolwiek w `godziny.txt`, zróbcie commit i wróćcie na `main`.
Tej gałęzi nie będziemy nigdzie scalać — niech zostanie jako nieudany eksperyment.

**3.4** W repozytorium są też gałęzie przygotowane przez innych pracowników kawiarni:
`ciasta`, `godziny-otwarcia` i `promocja`. Przełączcie się na każdą z nich i zobaczcie, co zawiera, np.:

```bash
git checkout ciasta
git log --oneline -3
```

Przy pierwszym przełączeniu Git sam utworzy lokalną gałąź na podstawie tej z serwera.
Na koniec wróćcie na `main` i obejrzyjcie wszystko naraz: `git log --oneline --graph --all`.

---

## 4. Scalanie gałęzi (ok. 15 min)

Scalanie (*merge*) to przeniesienie zmian z jednej gałęzi do drugiej. Najpierw przełączacie się
na gałąź, **do której** chcecie dołączyć zmiany, a potem podajecie gałąź, **z której** je bierzecie.

**4.1** Flat white jest gotowy, więc trafia do głównego menu:

```bash
git checkout main
git merge nowa-kawa
```

W komunikacie pojawi się słowo *Fast-forward*. Obejrzyjcie `git log --oneline --graph`.

*Pytanie: dlaczego tym razem nie powstał żaden nowy commit?*

**4.2** Teraz gałąź z ciastami. Ona odbiła od `main` wcześniej, jeszcze przed waszym zamówieniem
i flat white, więc historie się rozeszły.

```bash
git merge ciasta
```

Git otworzy edytor z gotowym opisem `Merge branch 'ciasta'`. Wystarczy go zapisać i zamknąć —
w vimie: `:wq` i Enter, w nano: `Ctrl+O`, Enter, `Ctrl+X`.

Obejrzyjcie graf (`git log --oneline --graph`) — tym razem powstał commit, który ma dwóch rodziców.
Zajrzyjcie też do `menu.txt`: Git sam połączył flat white z nową sekcją ciast, bo zmiany były
w różnych miejscach pliku.

**4.3** Scalcie do `main` gałąź `godziny-otwarcia`. Porównajcie `cat godziny.txt` przed scaleniem i po nim.

**4.4** Scalonych gałęzi już nie potrzebujemy. Ich commity zostają w historii `main`, więc można je usunąć:

```bash
git branch -d nowa-kawa
git branch -d ciasta
```

Spróbujcie tak samo usunąć `eksperyment`. Co odpowiada Git i dlaczego?
(Nie usuwajcie jej na siłę — chodzi tylko o to, żeby zrozumieć komunikat.)

---

## 5. Konflikty (ok. 15 min)

Konflikt pojawia się wtedy, gdy dwie gałęzie zmieniły te same linijki tego samego pliku.
Git nie wie, która wersja jest dobra, więc decyzję zostawia wam.

**5.1** Na gałęzi `promocja` ktoś obniżył ceny kawy, a w tym samym czasie na `main` ktoś inny je
podniósł. Spróbujcie to scalić:

```bash
git merge promocja
```

Git zgłosi konflikt w `menu.txt`. Spokojnie, nic się nie zepsuło. Wpiszcie `git status` — plik
jest oznaczony jako *both modified*. Otwórzcie `menu.txt` w edytorze. Zobaczycie mniej więcej coś takiego:

```
<<<<<<< HEAD
(wersja z main, czyli z gałęzi, na której jesteście)
=======
(wersja z gałęzi promocja)
>>>>>>> promocja
```

Szef kawiarni zdecydował: promocja obowiązuje na espresso i cappuccino, ale latte zostaje w cenie
z `main`. Poprawcie plik tak, żeby to się zgadzało, i usuńcie wszystkie znaczniki
(`<<<<<<<`, `=======`, `>>>>>>>`). Uważajcie, żeby przy okazji nie zgubić flat white!

Potem zakończcie scalanie:

```bash
git add menu.txt
git commit -m "Scal promocję: tańsze espresso i cappuccino"
```

Gdyby w trakcie konfliktu coś poszło bardzo nie tak, `git merge --abort` przywraca stan
sprzed scalania i można zacząć od nowa.

**5.2** Teraz wywołacie konflikt sami:

1. Utwórzcie gałąź `herbata-a` i zmieńcie na niej cenę zielonej herbaty na 10 zł. Commit.
2. Wróćcie na `main`, utwórzcie gałąź `herbata-b` i zmieńcie tę samą cenę na 12 zł. Commit.
3. Wróćcie na `main` i scalcie `herbata-a`.
4. Scalcie `herbata-b`. Tu powinien pojawić się konflikt — rozwiążcie go, ustawiając cenę na 11 zł.

*Pytanie: dlaczego pierwsze scalenie przeszło bez problemu, a drugie nie?*

Na koniec `git status` powinien być czysty, a w `menu.txt` nie powinno być żadnych znaczników konfliktu.

---

## 6. Zadanie na koniec (ok. 10 min)

Wróćcie do swojego pamiętnika baristy z pierwszej części i spróbujcie zrobić to samodzielnie,
bez zaglądania wyżej:

1. Utwórzcie gałąź `wakacje` i dodajcie na niej plik `wakacje.txt`.
2. Wróćcie na `main` i dodajcie plik `dzien4.txt`.
3. Scalcie `wakacje` do `main`.
4. Utwórzcie gałąź `poprawki` i zmieńcie na niej pierwszą linijkę `o-mnie.txt`. Na `main` zmieńcie
   tę samą linijkę, ale inaczej. Scalcie `poprawki` i rozwiążcie konflikt.

Pokażcie mi potem wynik `git log --oneline --graph --all` — powinny być na nim widoczne dwa
rozgałęzienia, które wracają do `main`.

---

## Dla chętnych

Jeśli skończyliście wcześniej, spróbujcie jeszcze tego:

- **`.gitignore`** — w pamiętniku utwórzcie plik `notatki-prywatne.txt` i sprawcie, żeby Git go
  ignorował (nie powinien pojawiać się w `git status`). Sam plik `.gitignore` dodajcie do repozytorium.
- **Podróż w czasie** — `git checkout <hash pierwszego commita>`. Przeczytajcie komunikat o *detached HEAD*
  i zobaczcie, jak wyglądają pliki. Wracacie poleceniem `git checkout main`.
- **Kto to napisał?** — `git blame menu.txt`. Co pokazuje każda linijka?
- **Przywracanie pliku** — usuńcie połowę `menu.txt`, a potem przywróćcie ostatnią zapisaną wersję:
  `git checkout -- menu.txt` (albo `git restore menu.txt`).
- **Nowsze polecenia** — zamiast `git checkout` do przełączania gałęzi można używać `git switch`.
  Powtórzcie zadanie 3.1 z `git switch`.
