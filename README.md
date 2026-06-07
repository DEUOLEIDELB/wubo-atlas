# Wubo Atlas (widget lecture / mise en page A4)

Widget Grist générique : transforme **n'importe quelle table de la Bible Wubo** en page A4 propre, à la charte Wubo, imprimable en PDF. Pose le widget dans chaque table, il s'auto-configure et garde la mise en page que tu fais.

Live : `https://deuoleidelb.github.io/wubo-atlas/`

## Ce qu'il fait

- **Lecture A4 propre** : layout dédié par table (fiche pour les tables de type Rubrique/Contenu, carte pour les tables de type catalogue). Notes / colonnes système masquées automatiquement.
- **Édition inline** : tu cliques sur n'importe quel texte affiché, tu modifies, tu sors → la modification part directement dans la cellule Grist source. Une seule vérité.
- **Drag & drop façon Tally** :
  - poignée `⋮⋮` à gauche de chaque ligne pour la monter / descendre,
  - attrape un bloc et dépose-le à côté d'un autre pour les mettre **côte à côte (50/50)**,
  - dépose un bloc dans la zone pointillée en bas pour créer une **nouvelle ligne**.
- **Masquer un bloc** : croix `×` en haut à droite. Le bloc disparaît du A4 sans toucher la donnée Grist. Bouton **Réinitialiser** pour tout remettre.
- **Insérer une image** : bouton `+ Image` en haut. L'image est **uploadée comme pièce jointe dans le doc Grist** : aucune dépendance externe, tout le monde voit la même mise en page avec les mêmes images.
- **Impression A4** : bouton `Imprimer / PDF A4` (Ctrl+P enregistre en PDF).
- **Persistance** : la mise en page (ordre, masquages, splits, images insérées) est stockée dans les options du widget Grist (`setOptions`). Tu rouvres le doc dans 6 mois, tu retrouves ton A4.

## Mapping par table

Les 13 tables de la Bible ont chacune un layout pré-câblé (titre, sous-titre, colonnes affichées, ordre).

| Table | Layout | Colonne titre |
|---|---|---|
| T01_identite | fiche | Rubrique |
| T02_ecosysteme_produit | carte | Pilier |
| T03_univers_narratif | carte | Élément / Type |
| T04_blocs_modulaires | carte | Bloc / Audience |
| T05_pitchs | carte | Type de pitch / Durée |
| T06_business_model | fiche | Rubrique (+ sidebar Chiffres clés) |
| T07_concurrence | carte | Concurrent / Type |
| T08_equipe_legal | fiche | Rubrique (+ sidebar Rôle / Statut) |
| T09_audiences | carte | Audience / Sous-segment |
| T10_kits_roadmap | carte | Kit / Nom capsule |
| T11_traction_metriques | carte | Métrique / Catégorie |
| T12_canvas_frameworks | carte | Framework / Bloc |
| T13_risques | carte | Risque / Catégorie |

Pour une table inconnue, fallback en layout auto (titre = 1ère colonne, attributs = autres).

## Utilisation dans Grist

Dans la table voulue : **Add Widget to Page > Custom**, colle l'URL `https://deuoleidelb.github.io/wubo-atlas/`, puis règle **Access level** sur **Full document access** (indispensable : sans ça, pas d'édition inline, pas d'upload d'image, pas d'attachements).

Le bandeau du haut affiche en permanence :
- la table reconnue + nombre de lignes visibles / total,
- les erreurs éventuelles (édition refusée, upload bloqué, etc.).

## Notes techniques

- Un seul `index.html`. Dépendances chargées via CDN : `grist-plugin-api.js` (Grist) + `Sortable.min.js` (drag & drop).
- Stockage de la mise en page : `grist.setOptions({rows: [...]})` par instance de widget.
- Stockage des images : `grist.docApi.uploadAttachment(file)` → ID référencé dans la config.
- Édition : `grist.docApi.applyUserActions([["UpdateRecord", tableId, recId, {colId: value}]])`.
- Charte : violet `#5914D0`, jaune `#FFDD0B`, format A4 (`@page { size: A4 }`).
