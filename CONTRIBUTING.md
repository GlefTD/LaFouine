# Contribuer

LaFouine 0.2.2 est une page unique et un jeu de données. Une contribution utile est presque toujours une correction de montant, de lien ou de libellé, avec la pièce officielle à l’appui.

Ce dépôt est la distribution : `LaFouine_v0.2.2.html` et la compilation `dataset/lafouine_dataset.js`. Le code original est sous [LICENCE](LICENCE) MIT. La compilation suit [NOTICE.md](NOTICE.md). Les PDF et l’atelier d’extraction ne sont pas dans ce dépôt.

## Signaler une erreur

Une issue suffit. Y mettre :

- la version : 0.2.2;
- le ministère, l’exercice et le type de document;
- l’URL du PDF ou de la page officielle;
- le montant lu sur la pièce, et le montant affiché par LaFouine;
- l’identifiant de fiche, s’il est visible;
- la recherche utilisée, si le total change selon les mots.

Une capture de la grille aide. Le PDF reste la preuve.

Exemples déjà tranchés dans cette version, à ne pas rouvrir sans un PDF qui dit le contraire :

- un téléphone ou un télécopieur d’en-tête (514 873-6191, 418 380-2364) n’est pas un frais;
- `445 $ 210 $ 764 $` reste plusieurs montants;
- un numéro de dossier (`210994185`, `CT506051`) n’est pas un montant;
- une ligne d’engagement de rôle total ou en-tête n’entre pas dans le total;
- un montant au-delà de 1 000 000 000 000 $ n’entre pas dans le total LAI;
- les milliards du cadre et des comptes publics n’entrent pas dans le total LAI;
- la recherche `voxco` vaut 227 367 $ sur quatre lignes, pas le total des fiches parentes;
- Batteries vaut 1 877 295 149 $ déboursés (VGQ), et les huit filières ensemble 3 263 862 244 $.

## Ce qui se corrige volontiers

- un lien officiel cassé;
- un libellé français ou anglais de l’interface;
- un poste de l’Assemblée mal nommé;
- une fiche de filière dont la source publique contredit le montant ou la note;
- une règle d’affichage qui contredit le journal des révisions en tête du HTML.

## Interface

La page publiée est `LaFouine_v0.2.2.html`. Une modification qui change le comportement crée une nouvelle copie `LaFouine_vX.Y.Z.html`. Dans cette copie :

- le titre, le `h1`, la ligne d’état et le nom du CSV portent la même version;
- une entrée en français est ajoutée en tête du journal des révisions, datée, sans effacer les entrées précédentes;
- les libellés nouveaux existent en français et en anglais.

La console reste dense : police IBM Plex Mono, coins droits, lignes serrées. Le mode S doit continuer d’ouvrir la page sur un écran étroit. Les boutons S, E et D restent.

Les textes visibles sont en français. L’anglais est la deuxième langue du bouton FR/EN, pas la langue du journal.

## Compilation

Le fichier que la page charge est `dataset/lafouine_dataset.js`. Une correction de données remplace ce fichier, entier. Après remplacement, la page ouverte depuis ce dossier affiche 9 667 lignes, le total LAI 12 529 858 060 411 $ et Batteries 1 877 295 149 $.

## Demandes de fusion

Petite, liée à une pièce, et limitée à la page, à la compilation ou à ces documents. Une demande qui ajoute des PDF, une clé, ou un total LAI mélangé avec le cadre financier ne sera pas reprise telle quelle.

Le ton des descriptions : ce que la pièce dit, puis ce que la page devrait afficher.
