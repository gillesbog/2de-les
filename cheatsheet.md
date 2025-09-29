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

