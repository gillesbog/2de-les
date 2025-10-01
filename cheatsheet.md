Zeker, hier is het volledige `cheatsheet.md` bestand. Je kan de volledige inhoud hieronder kopiëren en rechtstreeks in een `.md` bestand plakken.

````markdown
# Git Bash Cheatsheet 🚀

Dit is een overzicht van de basiscommando's voor Git, gebaseerd op een typische eerste workflow.

---

## 📂 Project Opzetten

### `git init`
Initialiseert een **nieuw Git-repository** in de huidige map. Dit commando maakt een verborgen `.git` submap aan, die alle benodigde repository-bestanden bevat.

```bash
git init
````

-----

## ⚙️ De Basis Workflow

De kern van Git draait om het wijzigen, stagen en committen van je bestanden.

### `git status`

Toont de **status van de werkmap**. Hiermee zie je welke bestanden zijn gewijzigd, welke klaarstaan om gecommit te worden (gestaged), en welke nog niet worden gevolgd door Git (untracked).

```bash
git status
```

### `git add <bestandsnaam>`

Voegt een specifiek bestand toe aan de **staging area**. Bestanden in de staging area worden opgenomen in de volgende commit.

```bash
# Voegt één specifiek bestand toe
git add tasks.md
```

### `git add .`

Voegt **alle gewijzigde en nieuwe bestanden** in de huidige map en submappen toe aan de staging area. De `.` staat voor de huidige directory.

```bash
# Voegt alles in de huidige map toe
git add .
```

### `git commit -m "Jouw boodschap"`

Slaat een **snapshot** van de gestagede wijzigingen definitief op in de projectgeschiedenis. De `-m` (message) vlag is verplicht en dient om een duidelijke beschrijving van de wijziging te geven.

```bash
git commit -m "Takenlijst voor het project toegevoegd"
```

-----

## 📚 Geschiedenis Bekijken

### `git log`

Toont de **commit-geschiedenis** van de huidige branch. Je ziet details zoals de commit-hash (een unieke ID), de auteur, de datum en de commit-boodschap.

```bash
git log
```

### `git shortlog`

Geeft een **beknopte samenvatting** van de `git log`, gegroepeerd per auteur. Handig om snel te zien wie wat heeft bijgedragen.

```bash
git shortlog
```

-----

## 🌐 Werken met Remote Repositories (GitHub)

Een "remote" is een versie van je repository die op een server wordt gehost, zoals GitHub.

### `git remote add <naam> <url>`

Verbindt je lokale repository met een **remote repository**. De standaardnaam voor de primaire remote is `origin`.

```bash
git remote add origin [https://github.com/gebruikersnaam/repositorynaam.git](https://github.com/gebruikersnaam/repositorynaam.git)
```

### `git remote -v`

Toont een lijst van alle geconfigureerde **remote connecties** met hun URLs. De `-v` staat voor "verbose".

```bash
git remote -v
```

### `git push`

**Uploadt** je lokale commits naar de verbonden remote repository.

```bash
git push
```

### `git push --set-upstream origin main`

Dit commando gebruik je de **allereerste keer** dat je een nieuwe branch naar de remote pusht. Het koppelt je lokale `main` branch aan de `main` branch op `origin`, zodat je in de toekomst simpelweg `git push` kunt gebruiken.

```bash
git push --set-upstream origin main
```

### `git pull`

**Downloadt** wijzigingen van de remote repository en voegt deze samen (merget) met je huidige lokale branch. Dit is essentieel om up-to-date te blijven met werk van anderen.

```bash
git pull
```

-----

## 🖥️ Terminal Commando's

Dit zijn geen Git-commando's, maar basis Bash-commando's die vaak worden gebruikt.

### `mkdir <mapnaam>`

Maakt een **nieuwe map** (directory) aan.

```bash
mkdir bestanden
```

### `cd <mapnaam>`

**Navigeert** naar een andere map (Change Directory).

```bash
cd bestanden
```

### `code <bestandsnaam>`

Opent een bestand of map in **Visual Studio Code** (als dit correct is ingesteld in je PATH).

```bash
code cheatsheet.md
```


````markdown
# Git Workflow Cheatsheet 🚀

Dit overzicht beschrijft een standaard Git-workflow, van een lokaal project tot samenwerken via GitHub.

---

## 🏛️ Lokale Repository & Basis Commando's

Alles begint op je eigen computer.

- **Nieuwe repository starten**
  ```bash
  # Maakt een nieuwe Git repository aan in de huidige map
  git init
````

  - **Wijzigingen opslaan (Commit)**

    ```bash
    # 1. Voeg bestanden toe aan de 'staging area' (klaarzetten voor commit)
    git add <bestandsnaam>
    # of voeg alle gewijzigde bestanden toe
    git add .

    # 2. Sla de klaargezette bestanden op met een beschrijvend bericht
    git commit -m "Dit is wat ik heb veranderd"
    ```

  - **Status bekijken**

    ```bash
    # Controleer de status van je bestanden en branch
    git status
    ```

-----

## 🌿 Werken met Branches

Branches zijn aparte tijdlijnen waar je nieuwe features kunt ontwikkelen zonder de hoofdlijn (`main`) te beïnvloeden.

  - **Aanmaken en wisselen**

    ```bash
    # Maak een nieuwe branch aan
    git branch <nieuwe-branch-naam>

    # Wissel naar een andere branch
    git checkout <branch-naam>

    # Maak én wissel naar een nieuwe branch in één commando
    git checkout -b <nieuwe-branch-naam>
    ```

  - **Samenvoegen (Mergen)**
    Nadat je werk op een feature branch af is, voeg je het samen met `main`.

    ```bash
    # 1. Ga terug naar de hoofdbranch
    git checkout main

    # 2. Voeg de wijzigingen van de feature branch samen in main
    git merge <feature-branch-naam>
    ```

  - **Soorten Merges**

      - **Fast-Forward**: Simpele merge waarbij `main` "doorspoelt" naar de nieuwste commit van je feature branch. Gebeurt als `main` zelf niet is veranderd.
      - **Merge Commit**: Als beide branches unieke commits hebben, maakt Git een nieuwe commit aan die de twee geschiedenissen samenbrengt.

-----

## ☁️ Samenwerken met een Remote Repository (GitHub)

Om je code te back-uppen, te delen of om samen te werken, koppel je je lokale repository aan een remote.

  - **Verbinding leggen**

    ```bash
    # Koppel je lokale repo aan een remote URL (meestal van GitHub)
    # 'origin' is de standaardnaam voor deze verbinding.
    git remote add origin [https://github.com/gebruiker/repo.git](https://github.com/gebruiker/repo.git)
    ```

  - **Wijzigingen synchroniseren**

      - **Push**: Lokale commits naar de remote **sturen**.
        ```bash
        # Stuur commits van je huidige lokale branch naar de remote 'origin'
        git push

        # De allereerste keer dat je een nieuwe branch pusht:
        git push --set-upstream origin <branch-naam>
        ```
      - **Pull**: Wijzigingen van de remote **ophalen** en mergen.
        ```bash
        # Update je lokale branch met de laatste versie van de remote
        git pull
        ```

-----

## 🧹 Branches Opruimen

Houd je repository overzichtelijk door afgewerkte branches te verwijderen.

  - **Lokale branch verwijderen**
    ```bash
    # Verwijder een branch die al volledig is samengevoegd
    git branch -d <branch-naam>

    # Forceer de verwijdering van een branch (ook als hij niet gemerged is)
    git branch -D <branch-naam>
    ```
  - **Remote branch verwijderen**
    ```bash
    # Verwijder een branch van de remote 'origin'
    git push origin --delete <branch-naam>
    ```

<!-- end list -->

```
```
