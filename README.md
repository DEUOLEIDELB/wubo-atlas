# Wubo Atlas (widget de lecture A4)

Widget Grist générique : transforme **n'importe quelle table** en page A4 propre, à la charte Wubo, imprimable en PDF. Conçu pour **fabriquer des documents à présenter aux équipes** (golden circle, business model, structure de coût, certifications, etc.) à partir des données qui vivent déjà dans Grist.

## Ce qu'il fait

- Tu **choisis les lignes** à afficher (cases à cocher), ou tu affiches toute la table, ou la ligne active.
- Tu donnes un **titre** et une **phrase d'intro** au document.
- Rendu en feuille A4 (en-tête WUBO, sections, pied de page), **bouton Imprimer / PDF A4**.
- Affiche les **images** des colonnes pièces jointes (accès complet au document requis).
- Le widget **retient** ton titre, ton intro et ta sélection (stockés dans les options de la section Grist) : configure une fois un document "Golden Circle", il reste tel quel.

## Exemples d'usage

- **Golden Circle** : pose le widget sur la table identité, mode Sélection, coche les lignes Golden Circle WHY/HOW/WHAT, titre "Golden Circle Wubo".
- **Business model** : sur la table business model, coche les rubriques voulues, titre "Modèle économique".
- **Structure de coût** : coche la rubrique coûts, titre "Structure de coût de l'appareil".
- **Certifications** : coche les lignes concernées (risques/roadmap), titre "Certifications à réaliser".

## Déploiement GitHub Pages (~5 min)

1. Sur github.com, crée un repo vide `wubo-atlas` (org DEUOLEIDELB).
2. Sur ton ordinateur, dans ce dossier :
   ```bash
   git init && git add . && git commit -m "Widget lecture A4"
   git branch -M main
   git remote add origin git@github.com:DEUOLEIDELB/wubo-atlas.git
   git push -u origin main
   ```
   (ou glisse simplement `index.html` et `README.md` dans le repo via l'interface web GitHub)
3. Settings > Pages > Source : `main` / root. URL :
   `https://deuoleidelb.github.io/wubo-atlas/`

## Utilisation dans Grist

Dans la table voulue : **Ajouter une section > Custom**, colle l'URL, puis règle **Access level** sur **Full document access** (sinon pas d'images). Tu peux poser plusieurs sections Atlas, une par document type.

## Notes techniques

- Un seul fichier `index.html`, dépend uniquement de `grist-plugin-api.js`.
- Charte : violet `#5914D0`, jaune `#FFDD0B`, fond blanc, format A4.
- Images via colonnes pièces jointes Grist. Si la version self-hosted (`grist.playwubo.com`) expose l'API d'attachement différemment, une zone de repli s'affiche : me prévenir pour câbler l'URL exacte.
