# CI/Git Examen Cheat Sheet

De labo's zijn **90% Git** en **10% CI**. Begrijp de Git-flow, want CI is de automatisering daarvan.

---

## 🚀 Deel 1: De Basis Git Workflow (Labo 1-2)

Dit is de fundamentele cyclus. Je moet de 3 stadia kennen:

1.  **Working Directory:** De map waarin je werkt.
    * `git status` (Controleer altijd hiermee!)
2.  **Staging Area:** Bestanden die klaarstaan voor een "snapshot".
    * `git add .` (Voeg *alle* gewijzigde bestanden toe aan de staging area)
    * `git add pad/naar/bestand.md` (Voeg één specifiek bestand toe)
3.  **Local Repo:** De "opgeslagen" geschiedenis op jouw pc.
    * `git commit -m "Duidelijke commit boodschap"`
    * `git log` (Bekijk de geschiedenis)

**Commando's om te kennen:**
* `git init`: Maakt een nieuwe, lege repository.
* `git config --global user.name "Naam"`: Stelt je naam in.
* `.gitignore`: Een bestand waarin je bestanden/mappen zet die Git moet negeren (bv. `*.tmp` of `node_modules/`).

---

## 🌐 Deel 2: Werken met Remotes (GitHub)

Dit gaat over het synchroniseren van je lokale repo met de server (GitHub).

* `git clone <url>`: Kopieert een remote repo naar jouw pc.
* `git remote add origin <url>`: Linkt je lokale repo aan een remote (als je lokaal begon).
* `git pull origin main`: Haalt de laatste versie van de server **en** voegt deze samen met jouw werk.
* `git push origin main`: Stuurt jouw commits naar de server.
* `git push -u origin main`: De `-u` (upstream) gebruik je de *allereerste keer* dat je pusht om de lokale `main` aan de remote `main` te koppelen.

---

## 🌿 Deel 3: De Branching Workflow (Gitflow) (Labo 3-4)

Dit is de **belangrijkste workflow** die je moet kennen. Je werkt *nooit* direct op `main` of `dev`.

1.  **Start een nieuwe taak:**
    * Ga naar de basisbranch: `git checkout dev`
    * Haal de laatste versie: `git pull`
    * Maak je taak-branch: `git checkout -b feature/nieuwe-functionaliteit`
2.  **Doe je werk:**
    * (Programmeer, wijzig bestanden...)
    * `git add .`
    * `git commit -m "Nieuwe feature toegevoegd"`
3.  **Deel je werk:**
    * Push je *feature branch* naar de server: `git push origin feature/nieuwe-functionaliteit`
4.  **Vraag om te mergen:**
    * Ga naar GitHub en maak een **Pull Request (PR)**.
    * Je vraagt om `feature/nieuwe-functionaliteit` te mergen in `dev`.
5.  **Opruimen (na merge op GitHub):**
    * `git checkout dev` (Terug naar `dev`)
    * `git pull` (Haal de net gemergede code binnen)
    * `git branch -d feature/nieuwe-functionaliteit` (Verwijder de lokale branch)

---

## ⚠️ Deel 4: Merge Conflict Oplossen (Labo 4)

Dit gebeurt als twee branches **hetzelfde bestand op dezelfde lijn** hebben aangepast.

**Scenario:** Je bent op `feature/mijn-taak` en je doet `git merge dev`.
1.  Git stopt: **"CONFLICT!"**
2.  Open het bestand met het conflict in je editor (bv. VSCode).
3.  Je ziet de markers:
    ```
    <<<<<<< HEAD
    (Jouw code op de feature branch)
    =======
    (Code die van 'dev' komt)
    >>>>>>> dev
    ```
4.  **Oplossing:** Verwijder álle markers (`<<<`, `===`, `>>>`) en zorg dat de code 100% klopt (soms wil je beide stukken code, soms maar één).
5.  Sla het bestand op.
6.  Markeer het conflict als opgelost: `git add .`
7.  Maak de merge-commit af: `git commit` (je hoeft geen `-m` te typen, de editor opent vanzelf).

---

## 🔧 Deel 5: Fouten Herstellen (Geavanceerd Git) (Labo 6)

Dit zijn de "fix" commando's. Heel belangrijk voor het examen.

| Commando | Wat het doet | Wanneer te gebruiken |
| :--- | :--- | :--- |
| **`git revert <hash>`** | Maakt een **nieuwe commit** die een oude commit ongedaan maakt. | **De veilige manier.** Je wilt een fout herstellen die al gepusht is, zonder de geschiedenis te herschrijven. De foute commit blijft bestaan, maar de wijziging is weg. |
| **`git reset --hard <hash>`** | **Verwijdert commits.** Het zet de `HEAD` terug naar een vorig punt. | **Gevaarlijk.** Je wilt commits *echt* laten verdwijnen (bv. een paswoord). Je *moet* `git push --force` gebruiken. Gevraagd als: "zonder sporen na te laten". |
| **`git cherry-pick <hash>`** | **Kopieert** één specifieke commit van een andere branch naar je huidige branch. | Labo 6: Je wilt één commit (de 'airspeed' vraag) van een foute branch overzetten naar de juiste branch. |

---

## 🔥 Deel 6: De Hotfix Procedure (Scenario) (Labo 6)

**Probleem:** De build op `master` faalt (bv. de vergeten `;`).

**Procedure:**
1.  `git checkout master`
2.  `git pull`
3.  `git checkout -b hotfix/compile-error` (Cruciaal: aftakken van **master**!)
4.  (Fix de bug, sla op)
5.  `git add .`
6.  `git commit -m "Hotfix: compile error"`
7.  `git checkout master`
8.  `git merge hotfix/compile-error` (Merge de fix in `master`)
9.  `git push origin master` (De CI op `master` zal nu slagen)
10. **NIET VERGETEN:** De fix moet ook in `dev`!
11. `git checkout dev`
12. `git merge master` (Haal de hotfix van `master` naar `dev`)
13. `git push origin dev`

---

## ⚙️ Deel 7: GitHub Ecosysteem (Labo 5)

* **Issues:** Taken, bugs, of vragen. Hebben een nummer (bv. `#12`).
* **Labels:** Categorieën voor Issues/PRs (bv. `bug`, `docs`, `fix`).
* **Milestones:** Groeperen van Issues voor een deadline (bv. `v2.0`).
* **Issues Automatisch Sluiten:** Gebruik keywords in je **commit message** (NIET de PR titel).
    * `git commit -m "Fixes #12: typo in de docs opgelost"`
    * **Keywords:** `Closes`, `Fixes`, `Resolves`

---

## 🤖 Deel 8: Continuous Integration (CI) - GitHub Actions (Labo 6)

Dit is de "CI Basic". Het is een bestand dat in je repo woont op `.github/workflows/naam.yml`.

**Anatomie van een `.yml` bestand:**

```yml
# Naam van de workflow
name: .NET Build Workflow

# WANNEER moet dit draaien?
on:
  push:
    branches: [ main ]  # Als iemand naar 'main' pusht
  pull_request:
    branches: [ main ]  # Als iemand een PR naar 'main' maakt

# WAT moet het doen?
jobs:
  build: # Naam van de job
    # Op welke machine moet dit draaien?
    runs-on: ubuntu-latest

    steps:
      # Stap 1: Download de code
      - name: Checkout code
        uses: actions/checkout@v3

      # Stap 2: Installeer de .NET omgeving
      - name: Setup .NET
        uses: actions/setup-dotnet@v2
        with:
          # VRAAG LABO 6: Je moest dit aanpassen!
          dotnet-version: 6.0.x 

      # Stap 3: Voer de build uit
      - name: Build
        run: dotnet build --configuration Release
