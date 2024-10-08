# datavisenchiffres

### Description

Reproduction d'une sélection de graphiques du [VS en chiffres](https://www.vs.ch/documents/21539585/21539740/Das+Wallis+in+Zahlen+2023.pdf/ca9c4eaf-6956-3b40-8610-a7d40faea27e?t=1707999971763), publication papier annuelle.

![Capture d'écran de la page d'accueil menant aux différentes visualisations](imgs/homepage.png)

L'idée est de tester quelques possibilités d'interactivité afin d'"augmenter" le contenu de la brochure dans le futur. Les différentes reproductions sont ainsi plutôt sobres et orientées sur l'apprentissage et l'expérimentation des fonctionnalités. Les différents choix et améliorations sont détaillés ci-dessous dans les rubriques dédiées. Chaque visualisation reprend le commentaire ainsi que quelques potentiels d'amélioration.

![Capture vidéo de la visualisation du temps de trajet quotidien](imgs/temps_trajet.gif)

#### Données

Les données sont issues majoritairement d'enquêtes de l'OFS (notamment STATPOP, HESTA, le microrecensement mobilité et transports, etc.) et sont, à priori, de bonne qualité.

Les données cartographiques sont © OFS, Themakart, 2024

### Choix des visualisations

Le Valais en chiffres est une publication annuelle qui essaie de dresser le portrait statistique du Canton lors de l'année écoulée (les données datant généralement de l'année précédente). Ce choix est déjà restrictif, car il exclut d'emblée les séries temporelles (sur plusieurs années). La publication étant (vraiment) destinée au grand public (ainsi qu'aux écoles du canton), les graphiques "trop complexes" sont également évités. On peut penser qu'avec la plus large diffusion de visualisations et l'amélioration de la littératie des données, cette barrière pourra être levée dans un futur proche.

Le panel de graphiques à choix devient vite réduit si l'on souhaite visualiser principalement des relations de type "magnitude", "part relative à un ensemble", "classement" et "spatial" pour reprendre le _[visual vocabulary](https://raw.githubusercontent.com/Financial-Times/chart-doctor/main/visual-vocabulary/poster.png)_ du _Financial Times_. Il faut pourtant essayer de rendre la publication la plus attractive possible.

Les cartes de [densité](./carte_densite.html) et d'[évolution de la population](./carte_evol_pop.html), le graphique en barres [le nombre de logements selon la source d'énergie](./chauffage_logements.html) et celui en lignes du nombre de [nuitées selon la provenance des hôtes](./nuitees_provenance.html) sont des grands classiques et devraient facilement parler au public. L'ajout de l'interactivité les rend encore plus informatifs avec la possibilité de connaître la valeur précise pour une certaine commune ou un mois donné. Pour les barres, l'interactivité est uniquement cosmétique (animation du début).

La "pyramide" des âges est un type de graphique moins fréquent et a été incluse pour montrer le résultat de la projection démographique réalisée pour le canton du Valais. Là aussi l'interactivité permet de connaître, pour chaque tranche d'âge, les valeurs exactes. On pourrait également penser inclure dans la même visualisation la différence entre la projection et l'état actuel (ou d'autres différences), animer l'évolution sur plusieurs années et ainsi voir la pyramide onduler.

Le graphique de l'[utilisation du sol](./oc_sol.html) est une petite évolution avec l'utilisation d'un _treemap_ plutôt que d'un _pie chart_. Ici l'interactivité permet d'inclure les données de l'agriculture directement dans un "sous-treemap" qui pourrait être étendu aux autres grandes catégories (ce que le format A6 de la publication ne permet pas). On se heurte toutefois au même problème que la publication physique pour l'inclusion de labels hors _tooltip_. De plus, la visualisation paraît un peu vide vu qu'il n'y a qu'un sous-domaine qui est détaillé et que c'est un des plus petits. Le résultat final n'est donc pas très convaincant dans sa forme actuelle.

Le graphique des [exportations](./exportations.html) permet de voir les partenaires privilégiés au niveau des exportations. Un graphique alternatif aurait été de faire un graphique "de Sankey"/alluvial pour montrer comment se répartissent les plus gros secteurs d'exportations dans les plus grosses destinations d'export. Toutefois, le graphique est vite encombré et les symboles proportionnels sont assez intuitifs (même s'ils demandent de connaître les drapeaux représentés). Là encore, l'interactivité permet d'apporter cette information ainsi qu'un peu d'animation, mais le type de graphique pourrait être intégralement repensé.

Finalement, le graphique du [temps de trajet journalier moyen](./temps_trajet.html) est une façon plus originale de représenter une quantité qu'un simple graphique en barre. Ici l'animation est un grand plus (mais a fait remonter pas mal de mauvais souvenirs liés au cercle trigonométrique), car elle permet de mieux comprendre que la grande horloge représente le total et qu'il est supérieur à une heure (un tour de cadran). Il serait également intéressant d'y coupler la distance moyenne par type de transport (qui a dû être abandonnée faute de place).

### Technologies

Le travail est réalisé à l'aide de [D3.js](https://d3js.org/), une librairie destinée à la visualisation pour le web.

### Sources et ressources

L'idée de la page d'accueil vient de la "galerie" D3 visible sur [Observable](https://observablehq.com/@d3/gallery).

Une partie du code pour le graphique des exportations a été reprise et adaptée du projet d3-country-bubble-chart
de jeffreymorganio (https://github.com/jeffreymorganio/d3-country-bubble-chart/)

Les drapeaux pour les exportations sont issus du repo suivant : [https://github.com/fonttools/region-flags](https://github.com/fonttools/region-flags). Les informations complémentaires sont disponibles dans le dossier `/flags`.

Pour comprendre l'animation des lignes : https://jakearchibald.com/2013/animated-line-drawing-svg/

Pour les horloges, https://observablehq.com/@d3/simple-clock et https://observablehq.com/@drio/lets-build-an-analog-clock

### Améliorations potentielles

- Cartes : Ajouter une échelle
- Pyramides des âges :
  - L'axe à zéro est décalé (valeur en milieu d'axe)
  - La transition pour se faire de manière à ce que les barres des années montent pour passer de 2022 à 2050 (une sorte d'ondulation vers le haut)
- Treemap :
  - Insérer des labels dans les rectangles (pas optimal)
  - Ajouter des autres informations sur les types de surfaces
- Drapeaux/Exportations : 
  - Il faudrait standardiser l'aspect ratio des drapeaux pour éviter d'avoir des cas comme le Japon qui ressemble plus à l'oeil de Sauron qu'à un drapeau ou le Canada qui n'est plus qu'une feuille d'érable.
  - Résoudre le problème des drapeaux blancs (DK, SK, SE)
  - Ajouter le nom court des pays plutôt que le code ISO
- Barres / Sources du chauffage : Insérer le label en bout de barre à l'exemple de la publication physique
- Lignes / Nuitées : 
  - Labellisation directe
  - Formater les axes avec une espace fine pour les milliers
- Horloges : Organiser la page de façon plus complète (texte explicatif, sources, etc.)

### Contexte de développement

Ce projet a été développé dans le cadre du cours _Visualisation de données_ (SP24) dispensé par Isaac Pante (SLI, Lettres, UNIL).