# Déployer le widget de lecture A4 (wubo-atlas)

Guide pas à pas pour mettre le widget en ligne et l'utiliser dans Grist. Tout est déjà prêt dans le dossier `outils/wubo-atlas/` (`index.html` + `WUBO-logo.png` + `README.md`). Compter 5 à 10 minutes.

---

## Étape 0 : ménage préalable

Dans l'Explorateur Windows, va dans `C:\Users\takih\Desktop\Playground\outils\` et **supprime le dossier `wubo-atlas-widget`** (un `git init` raté l'a laissé cassé : index.html tronqué + `.git` verrouillé). Le bon dossier, celui à utiliser, est **`wubo-atlas`**.

---

## Étape 1 : créer le repo sur GitHub

1. Va sur https://github.com/new (connecté au compte DEUOLEIDELB).
2. Repository name : `wubo-atlas`
3. Visibilité : **Public** (obligatoire pour GitHub Pages en offre gratuite).
4. Ne coche rien d'autre (pas de README, pas de .gitignore : les fichiers existent déjà).
5. Clique **Create repository**.

---

## Étape 2 : mettre les fichiers en ligne

### Option A : interface web (le plus simple, sans Git)

1. Sur la page du repo vide, clique le lien **uploading an existing file**.
2. Ouvre `C:\Users\takih\Desktop\Playground\outils\wubo-atlas\` dans l'Explorateur.
3. Glisse-dépose les 4 fichiers : `index.html`, `WUBO-logo.png`, `README.md`, `DEPLOIEMENT.md`.
4. En bas, clique **Commit changes**.

### Option B : ligne de commande (Git Bash ou PowerShell)

```bash
cd "C:/Users/takih/Desktop/Playground/outils/wubo-atlas"
git init
git add .
git commit -m "Widget lecture A4 v2"
git branch -M main
git remote add origin https://github.com/DEUOLEIDELB/wubo-atlas.git
git push -u origin main
```

Si Git demande une authentification : utilise ton nom d'utilisateur GitHub et un **token personnel** (Settings > Developer settings > Personal access tokens) comme mot de passe.

---

## Étape 3 : activer GitHub Pages

1. Dans le repo : **Settings** (onglet en haut) > **Pages** (menu de gauche).
2. Sous "Build and deployment", Source : **Deploy from a branch**.
3. Branch : `main`, dossier `/ (root)`. Clique **Save**.
4. Attends 1 à 2 minutes. La page affichera l'URL en ligne :

```
https://deuoleidelb.github.io/wubo-atlas/
```

Pour vérifier : ouvre cette URL dans un onglet. Tu dois voir une page qui dit "Ouvre cette page comme widget personnalisé dans Grist". C'est normal : le widget ne s'anime que dans Grist.

---

## Étape 4 : ajouter le widget dans chaque table

Pour chaque table que tu veux pouvoir présenter en A4 :

1. Ouvre la **table** dans Grist.
2. Bouton **Add New** (ou le "+") > **Add Widget to Page**.
3. Type de widget : **Custom**.
4. Dans le panneau de droite, champ **URL** : colle `https://deuoleidelb.github.io/wubo-atlas/`
5. Juste en dessous, **Access level** : choisis **Full document access** (indispensable, sinon pas d'images et accès données bloqué).
6. Valide. Le widget s'affiche en page A4 avec toutes les lignes de la table.

Le widget n'a que deux boutons :

- **Rafraîchir** : recharge la page après une modif dans la table.
- **Imprimer / PDF A4** : ouvre le dialogue système pour imprimer ou enregistrer en PDF A4 propre.

---

## À savoir

- **Images** : le widget affiche les images des colonnes "pièces jointes" de Grist. Si une zone de repli grise apparaît au lieu de l'image, c'est que l'API d'attachement de ton Grist self-hosted (`grist.playwubo.com`) diffère : dis-le-moi, c'est deux lignes à ajuster dans `index.html`.
- **Mettre à jour le widget** plus tard : il suffit de remplacer `index.html` dans le repo (re-upload ou `git push`). Grist recharge la nouvelle version automatiquement.
- **Charte** : violet `#5914D0`, jaune `#FFDD0B`, format A4. Modifiable en haut de `index.html` (bloc `:root`).
