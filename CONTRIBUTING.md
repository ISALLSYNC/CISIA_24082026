# Travailler sur le dépôt pendant le Sprint 3

## Une branche par apprenant ou binôme

Dans VS Code, ouvrez **Terminal > Nouveau terminal** puis saisissez, depuis le dossier du dépôt :

```powershell
git switch main
git pull --ff-only
git switch -c prenom-nom
git status --short
```

Remplacez `prenom-nom` par un nom court sans espace, par exemple `lea-samir`.

## Boucle de travail

Avant chaque commit :

```powershell
uv run python -m black --check --no-cache .
uv run ruff check --no-cache .
uv run python -m pytest -q
git status --short
```

Ajoutez uniquement les fichiers voulus, puis contrôlez-les :

```powershell
git add -- chemin\du\fichier.py tests\test_concerne.py
git diff --cached --check
git diff --cached
git commit -m "M25: ajouter la preuve de sécurité"
git push -u origin prenom-nom
```

Créez ensuite une pull request vers `main`. Une pull request ne remplace pas la preuve locale :
conservez la sortie des tests et le résultat métier demandé dans le support.

## Garde-fous

- ne commitez jamais `.env`, `.venv/`, une clé personnelle, un jeton ou un mot de passe ;
- n'utilisez pas `git add -A` pendant le Sprint : ajoutez une liste fermée de fichiers ;
- ne forcez pas un push et ne réécrivez pas l'historique partagé ;
- ne travaillez pas sur `J6-gameday` avant le signal du formateur ;
- si votre dossier contient déjà du travail, ne lancez ni `git reset --hard` ni `git clean`.

## Revenir à l'état sain sans perdre son travail

Commencez par sauvegarder votre branche :

```powershell
git status --short
git switch -c sauvegarde-prenom-nom
git push -u origin sauvegarde-prenom-nom
```

Demandez ensuite au formateur avant toute restauration. Le tag `v1.0-sain` sert de référence de
comparaison pour le Game Day :

```powershell
git diff v1.0-sain
```
