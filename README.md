<!-- nodus:readme — structure du README produit (starter de Nodus). Rempli et tenu à jour par le skill
     `presenter` depuis docs/PRD.md, le code et le CHANGELOG ; `npm run release-check` vérifie les
     sections et les « À compléter ». Les outils de développement sont dans docs/developpement.md.
     presenter : PRD à la décision « 2026-11-16 (D32) », rédigé le 2026-11-16 -->

# Kroma

> Construire un système de couleurs à partir de quelques courbes réglables, le vérifier, et le
> livrer au format standard des design tokens. Kroma s'adresse aux designers et aux développeurs
> front-end qui tiennent un design system.

**Statut** : prototype · **Version** : 0.9.0, voir [CHANGELOG.md](CHANGELOG.md) · **Démo** : À
compléter

## Le problème

Un système de couleurs compte des dizaines de nuances. Elles doivent rester cohérentes entre elles,
fonctionner en thème sombre et offrir assez de contraste pour être lisibles. Les outils courants
font régler chaque couleur, ou chaque palette, à la main : une retouche de la progression se répète
partout, et le contraste se vérifie couleur par couleur.

Un système ne vaut aussi que s'il circule. Il doit pouvoir **entrer** depuis ce qui existe déjà
(fichier de tokens, variables CSS) et **sortir** dans un format que lisent le code, les outils de
design et les agents, avec l'usage de chaque couleur écrit et ses combinaisons vérifiées.

## Pour qui

Le **Design Engineer** : designer ou développeur front-end confirmé, à l'aise en CSS et en
JavaScript, qui connaît l'espace de couleur OKLCH et tient à l'accessibilité. Il veut tout régler,
voir l'effet aussitôt et repartir avec des fichiers propres. Il travaille sur un ordinateur
portable. Kroma ne vise ni les designers non techniques ni les développeurs débutants.

Les outils (Style Dictionary, Tokens Studio) et les agents IA lisent ce que Kroma exporte ; ils ne
se servent pas de l'application.

## Ce que ça permet

<!-- source : docs/PRD.md › Jobs to be done (MVP d'abord). État d'après le code, jamais d'après le
     PRD : ✅ livré (ses critères d'acceptation ont leurs tests) · 🚧 en cours · ○ prévu -->

| | Quand… | je veux… | pour… | État |
|---|---|---|---|---|
| J1 | je définis les règles de mes palettes | régler des courbes de luminosité et de chroma partagées par toutes les teintes d'une catégorie (colorée ou neutre), en OKLCH ou OKHSL | garder une progression cohérente | 🚧 en cours · le glisser des poignées n'a pas encore de test de geste |
| J2 | je modifie un paramètre | voir toutes les palettes se mettre à jour, les couleurs hors gamut signalées | juger l'effet de mes choix | 🚧 en cours · fluidité (16 ms par image) non mesurée |
| J3 | une teinte demande un traitement particulier | changer sa valeur et son nom, en ajouter ou en retirer | adapter le système à mon identité visuelle | ✅ livré · décalage de teinte ○ prévu (V1) |
| J4 | je vérifie l'accessibilité | voir le contraste d'une couleur avec les autres, et la matrice d'une rampe, en APCA ou WCAG 2, classé par usage | vérifier les combinaisons une à une et d'ensemble | ✅ livré · raccourcis clavier ○ prévus (V1) |
| J5 | mon thème clair est prêt | nommer des tokens qui désignent une couleur en clair et une en sombre | obtenir un thème sombre cohérent et nommé | ✅ livré · aperçu clair / sombre ○ prévu (V1) |
| J6 | mes palettes sont prêtes | exporter des variables CSS, clair et sombre | les utiliser dans un projet | ✅ livré · sortie `light-dark()` ○ prévue (V1) |
| J7 | je reviens sur le projet | retrouver mes réglages et ma langue | reprendre où j'en étais | ✅ livré |
| J9 | j'ai un système enregistré par Kroma | le rouvrir à l'identique | le reprendre ou le partager | ✅ livré |
| J11 | mon système est prêt | l'exporter au format W3C Design Tokens (DTCG 2025.10), clair et sombre, descriptions et paires comprises | le livrer aux outils, au code et aux agents | ✅ livré |
| J12 | mes tokens sémantiques sont nommés | écrire l'intention de chacun, et déclarer les paires fond / texte avec l'usage qu'elles doivent tenir | livrer un thème dont l'accessibilité est écrite et vérifiée | ✅ livré |
| J13 | j'ai un système hors de Kroma (fichier DTCG, Tokens Studio compris ; variables CSS) | l'importer : Kroma retrouve des teintes et des courbes qui le reproduisent et dit l'écart de chaque couleur | le reprendre dans Kroma, réglable | ✅ livré |
| J8 | je commence un système | partir d'un preset qui montre ce que Kroma sait faire | avoir un point de départ et des exemples de structure de tokens | ✅ livré (V1) |
| J10 | je suis sur mobile | consulter les palettes et exporter | y accéder hors du poste de travail | ○ prévu (V2) |

## Comment ça marche

1. **Partir d'un preset, ou d'un système existant** : un système complet est chargé au premier
   lancement. Huit presets montrent ce que font les courbes, dont quatre design systems connus
   repris dans Kroma (téléchargés au moment de les charger). On peut aussi importer un fichier DTCG ou des variables CSS : Kroma propose des
   rampes, on les corrige, puis il calcule teintes et courbes et montre l'écart de chaque couleur.
2. **Régler les courbes** : dans le panneau de paramètres, choisir la forme de la courbe de
   luminosité et de chroma d'une catégorie (linéaire, parabolique, Bézier…) ou en glisser les
   points ; toutes les palettes de la catégorie suivent. Les poignées d'une courbe de Bézier
   peuvent sortir du cadre, comme dans les outils de dessin, et les couleurs suivent exactement la
   courbe dessinée.
3. **Vérifier les contrastes** : sélectionner une couleur pour la voir en texte sur sa rampe et sur
   les neutres, ou ouvrir la matrice d'une rampe. Chaque paire dit l'usage qu'elle permet (corps de
   texte, gros texte, bordure…).
4. **Nommer et déclarer** : dans l'écran Tokens, chaque token sémantique désigne une couleur en clair
   et une en sombre, avec son intention écrite ; dans l'écran Contrastes, les paires fond / texte
   déclarées sont vérifiées dans les deux thèmes.
5. **Exporter** : un fichier DTCG 2025.10 (un seul `.resolver.json`, qui se rouvre à l'identique)
   ou des variables CSS. Chaque couleur exportée porte sa recette : la courbe de sa rampe, sa
   position sur cette courbe et les valeurs qui en sortent. Un export DTCG défectueux est refusé, ses défauts affichés. Tout est
   enregistré dans le navigateur, sans compte.

Captures : À compléter (`docs/captures/`).

## Ce qu'on cherche à apprendre

<!-- source : docs/PRD.md › Hypothèses à valider — publié avec l'accord du porteur du projet -->

| Ce qu'on suppose | Comment on le saura |
|---|---|
| Les outils et les agents n'ont besoin de rien d'autre que d'un fichier DTCG valide et décrit | en livrant l'export à Style Dictionary, Tokens Studio et à un agent |
| L'import retrouve un système venu d'un autre outil avec un écart acceptable | en important de vrais fichiers (Tokens Studio, Style Dictionary) : seuls des fichiers écrits pour les tests l'ont été |

Restent aussi des questions de la spécification d'origine : la forme de la consultation sur
mobile, les raccourcis clavier par défaut et leur présentation.

## Choix de conception

<!-- source : docs/PRD.md › Décisions — publié avec l'accord du porteur du projet -->

- **Des courbes partagées par catégorie** : une courbe règle toutes les teintes colorées, une autre
  les neutres. La cohérence vient de la règle, pas de la retouche. C'est ce qui distingue Kroma.
- **La norme d'abord** : en sortie comme en entrée, le format W3C Design Tokens (DTCG 2025.10). Le
  thème sombre y est un contexte du même système, pas une copie ; les courbes et les paires, que la
  norme ne décrit pas, voyagent dans une extension que les autres outils ignorent sans perte.
- **Importer, c'est ajuster des courbes** : un système venu d'ailleurs devient réglable, et l'écart
  avec l'original est dit couleur par couleur, plutôt que copié tel quel.
- **Une couleur dit d'où elle vient** : dans l'export, chaque couleur porte sa recette (courbe,
  position, valeurs), lisible token par token, sans relire tout le système.
- **Le thème sombre se construit par tokens nommés**, choisis à la main, plutôt que par un calcul
  automatique : le designer garde la main, et chaque token dit à quoi il sert.
- **Une échelle de contraste fixe, des exigences déclarées par paire** : régler les seuils ferait
  dire « conforme » à ce qui ne l'est pas ; chaque paire fond / texte déclare l'usage qu'elle doit
  tenir, vérifié en clair et en sombre, sur la couleur réellement affichée.
- **Tout reste dans le navigateur** : ni serveur ni compte ; le fichier DTCG sert à sauvegarder et
  à partager un système.

## Ce que l'application ne fait pas

Par choix :

- pas d'annulation / rétablissement, ni d'historique des versions (l'export en tient lieu) ;
- un seul système à la fois ; pas de compte, pas de collaboration ;
- pas d'espace de couleur autre qu'OKLCH et OKHSL ;
- pas de plugin ni d'import Figma ou Sketch ;
- pas d'aperçu de composants, pas de génération d'images, pas de serveur pour les agents ;
- pas de rôle sémantique déduit automatiquement : chaque token est choisi par l'utilisateur ;
- les exports SCSS, JavaScript, Tailwind v3 et l'ancien JSON sont retirés (l'ancien JSON reste
  lisible) : ils se déduisent du DTCG ou du CSS.

Limites connues de la version 0.9.0 :

- un système importé garde une seule courbe de luminosité et une de chroma par catégorie : des
  rampes dont les courbes diffèrent beaucoup d'une teinte à l'autre gardent un écart visible ;
- l'import n'a pas encore été essayé sur un vrai fichier Tokens Studio ou Style Dictionary ;
- un système en courbe de Bézier ouvert avec une version antérieure change légèrement à la
  réouverture (jusqu'à 0,02 de luminosité), les couleurs suivant désormais la courbe dessinée ;
- l'éditeur de courbe et la grille ne sont pas encore utilisables entièrement au clavier ;
- sur un téléphone, l'application s'affiche mais l'édition n'y est pas prévue.

## Où on en est

**0.9.0** (2026-11-16) : la recette de chaque couleur, des courbes de Bézier libres.

- L'export DTCG dit, pour chaque couleur, la courbe dont elle vient, sa position et ses valeurs.
- Les poignées de Bézier sortent du cadre, et les couleurs suivent exactement la courbe dessinée.
- 0.8.0 : des presets qui montrent l'outil (OKLCH et OKHSL, modes de courbe, nombres de paliers).
- 0.7.0 : importer un système existant (fichier DTCG d'un autre outil, variables CSS).

**Prochain lot** : À compléter (non décidé).

## Développer

```bash
npm install
npm run dev     # http://localhost:5226
npm test
```

Commandes, structure, publication, mise à jour de Nodus : [docs/developpement.md](docs/developpement.md).
Le produit voulu en détail : [docs/PRD.md](docs/PRD.md).

## Crédits et licences

Kroma — © 2026 benoit poulain — tous droits réservés ([COPYRIGHT](COPYRIGHT)). Composants tiers et
leurs licences (Reef.js, Nodus, MadeMark, Lucide, Geist, Color.js) : [THIRD-PARTY.md](THIRD-PARTY.md).

