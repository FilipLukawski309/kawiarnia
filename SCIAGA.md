# Ściąga — najważniejsze polecenia Gita

## Na początek (raz na komputer)

    git config --global user.name "Imię Nazwisko"
    git config --global user.email "twoj@email.pl"

## Repozytorium

    git init                  zamienia bieżący folder w repozytorium
    git clone <adres>         pobiera istniejące repozytorium razem z historią

## Zapisywanie zmian

    git status                co się zmieniło, co jest w poczekalni
    git diff                  zmiany, których jeszcze nie dodano do poczekalni
    git add <plik>            dodaje plik do poczekalni
    git add .                 dodaje wszystkie zmiany z bieżącego folderu
    git commit -m "opis"      zapisuje zawartość poczekalni w historii

## Historia

    git log                   pełna historia
    git log --oneline         historia w skrócie
    git log --oneline --graph --all     graf wszystkich gałęzi
    git show <hash>           szczegóły jednego commita

## Gałęzie

    git branch                lista gałęzi (gwiazdka = bieżąca)
    git branch -a             wszystkie gałęzie, także te z serwera
    git branch <nazwa>        tworzy gałąź, ale się na nią nie przełącza
    git checkout <nazwa>      przełącza na gałąź
    git checkout -b <nazwa>   tworzy gałąź i od razu się na nią przełącza
    git branch -d <nazwa>     usuwa gałąź (tylko jeśli jest scalona)

## Scalanie

    git merge <gałąź>         dołącza zmiany z <gałąź> do gałęzi, na której jesteś
    git merge --abort         przerywa scalanie z konfliktem

Jak rozwiązać konflikt:

1. `git status` pokaże, w których plikach jest konflikt.
2. Otwórz plik, znajdź fragmenty między `<<<<<<<` a `>>>>>>>` i zostaw właściwą treść.
3. Usuń znaczniki `<<<<<<<`, `=======` i `>>>>>>>`.
4. `git add <plik>`, a potem `git commit`.

## Git otworzył edytor i nie wiem, jak wyjść

- vim: `Esc`, potem `:wq` i Enter
- nano: `Ctrl+O`, Enter, `Ctrl+X`
