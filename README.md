# LaFouine

Explorateur local des dépenses publiques du Québec. Distribution **0.2.2** (5 octobre 2026).

Ce dépôt est cette distribution. Il contient la page et la compilation des données, rien de l’atelier qui a servi à la produire.

```text
LaFouine_v0.2.2.html
dataset/lafouine_dataset.js
README.md
NOTICE.md
SECURITY.md
CONTRIBUTING.md
LICENCE
```

`dataset/lafouine_dataset.js` (7 934 562 octets) est la compilation : divulgations des ministères, rapports de dépenses de l’Assemblée nationale, filière batteries et filières stratégiques. Le gzip de cette compilation est encodé en base64 dans le script `window.__LAFOUINE_B64`.

LaFouine met ces pièces dans une seule page, avec le catalogue Données Québec en lecture directe. On filtre, on cherche dans le texte des pièces, et chaque montant garde un lien vers sa source.

La page est une lecture des documents publics. En cas d’écart, le PDF ou le jeu de données de l’éditeur fait foi.

## Ouvrir

Ouvrir `LaFouine_v0.2.2.html` depuis ce dossier, celui qui contient `dataset/`. Chrome et Firefox chargent la compilation au premier lancement, y compris par un double-clic (`file://`). Après un remplacement du fichier, actualiser avec Ctrl+F5.

Aucun serveur, aucun compte, aucune clé. La grille, la recherche et les totaux fonctionnent hors ligne. Les boutons **CKAN** et **RSS** ont besoin d’Internet.

Le bouton **JEU** (en-tête, bureau), le panneau de filtres, ou un glisser-déposer acceptent un autre jeu : gzip brut (octets `1F 8B`) ou le script `window.__LAFOUINE_B64`. Un fichier illisible ne remplace pas un corpus déjà affiché.

## À quoi sert l’outil

Les ministères publient, pièce par pièce, des PDF de frais, de contrats et de salaires. L’Assemblée nationale publie un rapport annuel par député et par cabinet. Le ministère des Finances publie des séries ouvertes (comptes publics, dette, cadre). Ces documents sont exacts à la source et difficiles à croiser.

LaFouine les rend interrogeables ensemble :

- une ligne de la grille est une fiche (un document, une personne, un poste ou une aide);
- une recherche peut descendre dans les lignes du PDF, pas seulement dans le titre;
- le total suit le filtre actif, avec une règle d’argent différente selon qu’on regarde les divulgations, l’Assemblée ou une filière;
- la fiche rappelle l’organisme, la période, le type de document et l’URL officielle.

L’outil sert à préparer une question, un article ou une vérification. Il ne remplace ni les comptes publics, ni une pièce signée, ni le rapport du Vérificateur général.

## Fonctions

### Corpus et filtres

Trois périmètres : Exécutif, Assemblée nationale, Données Québec.

- **Ministères** : 23 organismes, cases ouvertes. La liste est dans [Sources](#sources).
- **Types de documents** : sous-catégories des divulgations (déplacements, engagements, salaires, subventions, et les autres types du règlement).
- **Exercices** et **familles** (dépense LAI, rémunération, AssNat, filière, CKAN, et les autres familles présentes dans le jeu).
- **Filières stratégiques** : huit cases. Batteries, aérospatiale, technologies de pointe, minéraux critiques et stratégiques, défense et sécurité, bioalimentaire, bois d’œuvre, aluminium.
- **Postes** de l’Assemblée (logement, voyages, loyer, contrats de service, et les autres postes du rapport).
- Filtres actifs en pastilles, retirables une à une. **Réinitialiser** vide la recherche et les filtres. Les favoris étoilés et les vues enregistrées restent.

### Recherche

Les accents sont ignorés. Les guillemets, les parenthèses et les crochets marquent une phrase exacte. `AND` / `ET` est implicite. `OR` / `OU` et `NOT` / `SAUF` sont disponibles.

```text
"Christine Fréchette" OR "Fréchette, Christine"
(levio conseils inc)
conseil AND (informatique OR logiciel)
```

Le bouton **E** cherche aussi dans le détail des fiches et surligne les passages. Sans E, la grille filtre quand même sur ce texte : E change le surlignage, pas le périmètre de la recherche.

### Grille, fiche, totaux

Console dense, colonnes redimensionnables, réordonnables, masquables. Un clic sur un en-tête trie. Le mode **S** passe à une liste simple, prévue pour un écran étroit.

Le mode **D** déplie la grille : une ligne par bénéficiaire dans les engagements, sans les lignes de sommaire. **D ne change pas le total.** Le plafond d’affichage (1 500 lignes, puis « Afficher plus ») ne le change pas non plus. Le total porte sur tout le filtre.

Règle d’argent des divulgations :

- si la recherche tombe dans le titre de la fiche, le montant de la fiche est pris;
- si elle tombe seulement dans une ligne, seules les lignes trouvées sont additionnées, et l’étiquette devient « lignes »;
- les lignes de rôle total ou en-tête ne sont pas additionnées;
- un montant au-delà de 1 000 000 000 000 $ est écarté.

La fiche est une grille de propriétés (identité, source, lignes). Les lignes qui correspondent à la recherche s’ouvrent. Le lien mène au PDF et à la page de divulgation.

**STATS** reprend les filtres actifs comme titre. Sur un filtre de filière, le chiffre du haut est le relevé de filière. Sur un filtre limité à l’Assemblée, le total suit les rapports de dépenses. Dans les autres vues qui contiennent des divulgations, le total LAI est celui qui s’affiche.

**FIL** relie une même personne et les contreparties partagées. Les libellés génériques et les contreparties présentes sur plus de 40 fiches sont écartés. Un clic isole les fiches liées.

**Favoris** : étoiles locales. **Vues** : jusqu’à 24 recherches enregistrées (requête, filtres, tri, état de E). Une vue ne mémorise ni le mode D ni les étoiles.

**Export CSV** : le fichier se nomme `LaFouine_v0.2.2_filtre.csv`. En mode D, les lignes dépliées partent dans le CSV.

**FR / EN** traduit les libellés de l’interface. Le texte extrait des PDF reste dans la langue du document.

Tout cela reste dans le navigateur (`localStorage`, et IndexedDB sous le nom `lafouine`, clé `gzip`, pour le dernier jeu chargé à la main).

### Filières stratégiques

Relevé séparé des divulgations. Il n’entre pas dans le total LAI.

| Filière | Ce que le total retient |
| --- | --- |
| Batteries | Déboursé retenu par le Vérificateur général : **1 877 295 149 $** |
| Aérospatiale | Plafond québécois autorisé en dollars canadiens. Les plafonds en dollars US restent affichés, hors somme |
| Technologies de pointe | Annonces du budget 2025-2026 retenues dans le relevé |
| Minéraux | Plafonds québécois du relevé. Les autres leviers cités à part restent hors somme |
| Défense et sécurité | Plafonds québécois du relevé. Les annonces fédérales restent hors somme |
| Bioalimentaire | Plafonds québécois du relevé |
| Bois d’œuvre | Plafond autorisé du relevé. L’aide déjà consentie, marquée historique, reste hors somme |
| Aluminium | Plafond québécois. L’annonce fédérale reste hors somme |

Les huit cases ensemble affichent **3 263 862 244 $**, étiquette « déboursé + autorisé ».

Dès qu’une filière a des montants marqués VGQ, la somme prend ces montants en dollars canadiens. Sinon elle prend les plafonds québécois autorisés en dollars canadiens. Les devises autres que le dollar canadien, et les sommes marquées fédéral, Caisse ou historique, restent visibles et hors somme.

### Données Québec (CKAN)

Le bouton **CKAN** interroge le portail en direct. La base est :

```text
https://www.donneesquebec.ca/recherche/api/3/action/
```

LaFouine appelle, en lecture et sans clé :

- `package_search` pour le catalogue (texte, organisme, groupe, étiquette, format, tri);
- `datastore_search` pour la table d’une ressource CSV déjà versée dans le DataStore.

La recherche du haut de page sert aussi de recherche CKAN quand cette vue est ouverte. On ouvre un jeu, puis une ressource, puis la table, avec tri de colonnes. Des jeux du ministère des Finances sont épinglés pour entrer plus vite : comptes publics volume 2, cadre financier, rapport préélectoral, dette brute, déficits cumulés, statistiques fiscales des sociétés.

Cette vue ne télécharge pas le portail dans le jeu local. Elle ne crée, ne modifie et ne supprime aucun jeu. L’écriture CKAN exigerait une clé d’un diffuseur : ce programme ne la demande pas.

Chaque jeu porte sa propre variante de Creative Commons 4.0 sur sa fiche Données Québec. La variante par défaut du portail est CC BY 4.0. Le crédit se fait au jeu utilisé, pas au portail en bloc. Voir [NOTICE.md](NOTICE.md).

### Fils RSS de l’Assemblée nationale

Le bouton **RSS** lit des fils publics de l’Assemblée. Le navigateur ne peut pas les lire directement (`file://` et les règles CORS). La page essaie donc, dans l’ordre, des relais : rss2json, allorigins, corsproxy.io, codetabs, puis r.jina.ai. L’adresse du fil leur est transmise.

Fils proposés :

| Fil | Adresse |
| --- | --- |
| Actualités | `https://www.assnat.qc.ca/fr/rss/SyndicationRSS-214.html` |
| Dépôts du jour | `https://www.assnat.qc.ca/fr/rss/depots-du-jour.html` |
| Projets de loi | `https://www.assnat.qc.ca/fr/rss/SyndicationRSS-210.html` |
| Commission des finances publiques, horaire | `https://www.assnat.qc.ca/fr/rss/SyndicationRSS-182.html` |
| Commission des finances publiques, mandats | `https://www.assnat.qc.ca/fr/rss/SyndicationRSS-202.html` |
| Conférences et points de presse | `https://www.assnat.qc.ca/fr/rss/SyndicationRSS-212.html` |
| Transcriptions des points de presse | `https://www.assnat.qc.ca/fr/rss/SyndicationRSS-18.html` |
| Commission de l’administration publique, horaire | `https://www.assnat.qc.ca/fr/rss/SyndicationRSS-176.html` |
| Commission des institutions, horaire | `https://www.assnat.qc.ca/fr/rss/SyndicationRSS-184.html` |

Le lecteur affiche titre, lien, date et un court extrait. Il ne réécrit pas le fil.

### Repères de budget dans la page

Quelques fiches de cadre, de portefeuille et d’infrastructure sont écrites dans le HTML, avec leur URL (budget, comptes publics, stratégie de gestion des dépenses, plan québécois des infrastructures). Elles servent de point d’entrée. Leurs milliards ne sont pas additionnés au total des divulgations.

## Sources

La page, une fois ouverte, charge le jeu puis les repères du HTML. Le compteur affiche **9 667** lignes et la mention du jeu `2026-10-05`. Ce compteur mélange les divulgations, l’Assemblée, les filières et les repères. Le total d’argent LAI, lui, ne mélange pas ces familles.

### Divulgations ministérielles

Texte juridique : *Loi sur l’accès aux documents des organismes publics et sur la protection des renseignements personnels*, et *Règlement sur la diffusion de l’information et sur la protection des renseignements personnels*. Les pièces visées ici sont surtout les articles 16 à 27 du règlement (déplacements, réceptions, formation, contrats de formation, de publicité et de télécoms, subventions, baux, véhicules, dépenses de fonction) plus les salaires et la liste des engagements financiers de 25 000 $ et plus.

Les PDF sont ceux que les ministères publient sur Québec.ca et `cdn-contenu.quebec.ca`, sous les pages « accès à l’information » / « cadre légal et transparence ». LaFouine 0.2.2 ne rappelle pas ces pages au démarrage : le jeu a été constitué à l’avance. Chaque fiche garde l’URL du PDF et, quand elle est connue, celle de la page ministère.

Organismes présents :

- Affaires municipales et Habitation
- Agriculture, Pêcheries et Alimentation
- Conseil exécutif
- Culture et Communications
- Cybersécurité et Numérique
- Économie, Innovation et Énergie
- Éducation
- Emploi et Solidarité sociale
- Enseignement supérieur
- Environnement, Lutte contre les changements climatiques, Faune et Parcs
- Famille
- Finances
- Immigration, Francisation et Intégration
- Justice
- Langue française
- Relations internationales et Francophonie
- Ressources naturelles et Forêts
- Santé et Services sociaux
- Secrétariat du Conseil du trésor
- Sécurité intérieure
- Tourisme
- Transports et Mobilité durable
- Travail

Couverture utile : les exercices encore en ligne, surtout 2023-2024 et les suivants, plus une reprise partielle 2018-2022 là où le fichier répond encore (Économie, engagements d’Éducation et d’Enseignement supérieur, archives du Conseil du trésor, salaires du Conseil exécutif). La plupart des pages annuelles 2018-2021 ont été retirées des menus. Un fichier connu sur le CDN peut encore répondre ; il n’y a pas de liste publique complète pour ces années.

Le jeu de cette version retient **8 379** fiches LAI. Le total LAI sans filtre s’affiche **12 529 858 060 411 $**. Trois fiches d’engagement dont le montant extrait dépasse 1 000 000 000 000 $ restent dans le corpus et hors de cette somme.

Types suivis : déplacements du personnel, au Québec, hors Québec et à l’étranger ; véhicules et dépenses de fonction ; réception ; formation, colloques et congrès ; contrats de formation, de publicité et de télécoms ; subventions discrétionnaires ; baux ; salaires des titulaires, des ministres et des directeurs ; rapports de mission ; engagements financiers ; autre.

Les salaires des titulaires d’un emploi supérieur sont publiés par le Conseil exécutif. La colonne ministère de la personne est dans le tableau, pas dans le dossier du fichier. Pour les ministres, la fiche sépare l’indemnité de député, l’indemnité de ministre et les frais de fonction mensuels. Le total annuel ajoute les deux indemnités et douze fois les frais de fonction.

### Assemblée nationale

Rapports annuels de dépenses des députés, des cabinets et du service de recherche, publiés à [Rapports de dépenses](https://www.assnat.qc.ca/fr/deputes/rapports-des-depenses/deputes-cabinets.html). L’exercice va du 1er avril au 31 mars. Le jeu contient les rapports extraits pour les exercices couverts par les PDF déjà lus (les fichiers sources vont de 2020-2021 aux rapports présents dans l’atelier au moment de la compilation).

La fiche renvoie vers la page de dépenses du député sur assnat.qc.ca quand l’identifiant est connu, sinon vers le sommaire du rapport.

Les feuilles de poste (logement, loyer, contrats, et les autres) sont dans la page quand on filtre un poste. Le fichier `dataset/lafouine_dataset.js` porte les totaux de fiche ; le détail de poste suit la même extraction.

Conditions de réutilisation : [NOTICE.md](NOTICE.md). Source à citer : Assemblée nationale du Québec.

### Données Québec

Portail CKAN, lecture anonyme. Documentation : [page API de Données Québec](https://www.donneesquebec.ca/page-api/) et [API CKAN](https://docs.ckan.org/en/2.9/api/).

Les séries épinglées viennent du ministère des Finances. Leur licence est celle de la fiche du jeu, en pratique une Creative Commons 4.0, le plus souvent CC BY 4.0. Exemple de crédit :

```text
Comptes publics du gouvernement — volume 2, Ministère des Finances,
Données Québec, licence indiquée sur la fiche du jeu, consulté le 7 octobre 2026.
https://www.donneesquebec.ca/recherche/dataset/comptes-publics-du-gouvernement-volume-2
```

LaFouine ne copie pas ces CSV dans le jeu local. Qui réutilise un tableau doit citer le jeu précis et respecter la variante écrite sur sa fiche, y compris l’article 5 (absence de garantie).

### Vérificateur général et filières

Le total Batteries vient du rapport du Vérificateur général du Québec rendu public le 5 juin 2026 (couverture du 1er avril 2020 au 30 septembre 2025, avec un paiement Nemaska jusqu’au 15 octobre 2025) : 29 dossiers, **2 204 454 778 $** autorisés, **1 877 295 149 $** déboursés. Le rapport lui-même n’est pas redistribué. Les autres filières sont un relevé d’annonces et de crédits officiels, avec la source sur la ligne. Ce relevé n’est pas un inventaire exhaustif des aides.

### Ce que la compilation ne contient pas

La compilation porte les fiches extraites, pas les PDF. Les comptes publics en milliards, le cadre financier et les fonds spéciaux ne sont pas versés dans le total LAI. Une cellule « Transports » du volume 2 des comptes publics est le fonds général seulement : elle ne comprend pas, à elle seule, les fonds spéciaux de transport.

## Limites

- **Extraction.** Les montants viennent d’une lecture automatique des PDF. Des téléphones d’en-tête, des numéros de dossier et des colonnes collées ont été écartés dans cette version. Des lignes restent des extraits mal coupés. Le nom d’un fournisseur est souvent au milieu d’une ligne d’engagement, pas dans un champ « entreprise ».
- **Sommes.** Additionner une fiche et ses lignes, ou un sommaire et les établissements, double le chiffre. LaFouine écarte les rôles total et en-tête, et les montants déraisonnables. Un reste d’erreur est possible. Le PDF tranche.
- **Périmètre LAI.** Le total LAI n’est pas le budget de l’État, ni le volume 1 des comptes publics, ni le volume 2, ni les fonds spéciaux. Les engagements de 25 000 $ et plus sont des engagements publiés, parfois des enveloppes annuelles répétées d’un mois à l’autre.
- **Années manquantes.** Avant 2023, le corpus est troué. L’absence d’une dépense dans la grille signifie souvent que le PDF n’est plus au menu, pas que la dépense n’a pas existé.
- **Filières.** Plafonds et déboursés ne se comparent pas tels quels. Un plafond fédéral, un montant en dollars US ou une participation de la Caisse n’entre pas dans la somme. ÉcoPro (322 M$ hors Québec) reste hors du total Batteries, parce que cette filière a déjà des montants VGQ.
- **CKAN.** Dépend du portail et du DataStore. Une ressource qui n’est pas dans le DataStore s’ouvre par son lien de fichier, sans table intégrée. Le réseau peut refuser la requête selon le navigateur.
- **RSS.** Dépend d’un relais tiers. Le contenu du fil et l’adresse IP du poste sont vus par ce relais. Détail dans [SECURITY.md](SECURITY.md).
- **Police.** IBM Plex Mono est demandée à Google Fonts. Hors ligne, le navigateur prend une police monospace de repli.
- **Poste de travail.** La page tient dans le navigateur. Elle n’a pas de compte multi-utilisateurs et ne synchronise rien.

## Distribution publiée

Le dépôt s’arrête à la liste du début de ce fichier. La compilation est `dataset/lafouine_dataset.js`. Les PDF, les XML d’atelier et l’outil d’extraction restent hors de cette distribution. Les conditions qui accompagnent la compilation sont dans [NOTICE.md](NOTICE.md).

## Licence

Le code original de cette version est sous [licence MIT](LICENCE). Les documents, données et marques des éditeurs publics restent les leurs. Le détail, les crédits et ce que la MIT ne couvre pas sont dans [NOTICE.md](NOTICE.md).

## Contribuer

Une erreur de montant se signale avec l’URL du PDF. Voir [CONTRIBUTING.md](CONTRIBUTING.md). Une question de sécurité se traite selon [SECURITY.md](SECURITY.md).
