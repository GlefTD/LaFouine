# Notice

LaFouine 0.2.2 rassemble du code original et des documents produits par d’autres. Cette notice dit qui détient quoi, et sous quelle condition chaque bloc peut être repris. La [LICENCE](LICENCE) MIT ne s’applique qu’au code original désigné plus bas.

Date de cette notice : 7 octobre 2026. Les pages citées peuvent changer. En cas d’écart, la page de l’éditeur fait foi.

## Code original

Copyright © 2026 GlefTD.

Sous la licence MIT, pour la version 0.2.2 :

- `LaFouine_v0.2.2.html`, à l’exclusion des tableaux de données, des URL de documents officiels et des extraits de pièces qui y sont collés;
- la logique qui lit le jeu, filtre, cherche, calcule les totaux et dessine la console.

Cette distribution inclut `dataset/lafouine_dataset.js`. C’est la compilation du corpus : une ligne `window.__LAFOUINE_B64` dont le gzip contient les fiches extraites. La licence MIT couvre le contenant. Elle ne couvre pas la compilation qui est à l’intérieur. Les conditions de cette compilation sont celles des sections suivantes.

## Polices et librairies

| Élément | Provenance | Condition |
| --- | --- | --- |
| IBM Plex Mono | Demandée au chargement à `fonts.googleapis.com`. Non incluse dans le dépôt | [SIL Open Font License 1.1](https://github.com/IBM/plex/blob/master/LICENSE.txt). Le dessin de la police reste à IBM |
| pdfplumber | Utilisé seulement dans l’atelier local d’extraction des PDF, s’il est conservé à part | Licence MIT du projet pdfplumber. Absente de la page HTML |

CKAN n’est pas embarqué. La page parle au CKAN déjà en ligne sur Données Québec.

## Données Québec

Le bouton CKAN lit le portail en direct. Les CSV ne sont pas copiés dans le jeu de LaFouine.

- Portail : [donneesquebec.ca](https://www.donneesquebec.ca/)
- API de lecture : `https://www.donneesquebec.ca/recherche/api/3/action/`
- Documentation : [Utiliser les données](https://www.donneesquebec.ca/exploiter/utiliser-les-donnees/) et [Licence Creative Commons 4.0](https://www.donneesquebec.ca/licence/)

Chaque jeu porte une des six variantes Creative Commons 4.0. La variante est écrite sur sa fiche. La variante assignée par défaut sur le portail est **CC BY 4.0** : partage, y compris commercial, à condition de citer l’œuvre originale. CC0, quand elle est indiquée, ne demande pas de crédit. Les autres variantes ajoutent des conditions (pas d’utilisation commerciale, pas d’œuvre dérivée, partage à l’identique). Il faut lire la fiche du jeu avant de republier un CSV.

Toutes les variantes CC 4.0 incluent une absence de garantie (article 5 du code juridique). Un tableau CKAN ouvert dans LaFouine n’est pas certifié par le ministère des Finances ni par Données Québec.

Crédit minimal, à adapter au jeu réel :

```text
[Titre du jeu], [organisme producteur], Données Québec,
[variante de licence indiquée sur la fiche], consulté le [date].
[URL de la fiche]
```

Exemple pour un jeu épinglé par la page :

```text
Comptes publics du gouvernement — volume 2, Ministère des Finances,
Données Québec, licence indiquée sur la fiche, consulté le 7 octobre 2026.
https://www.donneesquebec.ca/recherche/dataset/comptes-publics-du-gouvernement-volume-2
```

Jeux épinglés dans l’interface, à citer chacun selon sa fiche :

- `comptes-publics-du-gouvernement-volume-2`
- `http-www-budget-finances-gouv-qc-ca-budget-en-chiffres`
- `cadre-financier-pluriannuel-du-gouvernement-du-quebec-publie-dans-le-rapport-preelectoral`
- `dette-du-gouvernement-du-quebec`
- `dette-representant-les-deficits-cumules`
- `statistiques-fiscales-des-societes-sommaire-des-statistiques-fiscales-des-societes`

La lecture (`package_search`, `datastore_search`) est anonyme. LaFouine n’écrit rien sur le portail.

## Assemblée nationale du Québec

Les rapports de dépenses des députés et des titulaires de cabinet, les pages de dépenses, et les fils RSS proviennent de l’Assemblée nationale du Québec.

Conditions publiées le 20 avril 2009, relues le 7 octobre 2026 :

[Conditions d’utilisation des contenus](https://www.assnat.qc.ca/fr/propos-site/droits-propriete-intellectuelle.html)

L’Assemblée autorise la reproduction sans frais lorsque, ensemble :

- l’utilisation est raisonnable, équitable, et non commerciale ou lucrative;
- les contenus ne sont pas modifiés ou altérés;
- l’utilisation ne porte pas atteinte à l’honneur ou à la réputation de l’Assemblée ou des personnes concernées;
- la source « Assemblée nationale du Québec » est indiquée.

Une utilisation commerciale ou publicitaire demande une autorisation préalable : [renseignements@assnat.qc.ca](mailto:renseignements@assnat.qc.ca). Le logo de l’Assemblée ne figure pas dans LaFouine et ne doit pas être ajouté sans autorisation.

L’Assemblée garantit l’intégrité de l’information au moment de sa mise en ligne. Elle ne garantit pas un document modifié ensuite. Le texte officiel a préséance sur le site, et le site a préséance sur l’extraction de LaFouine.

La compilation livrée dans `dataset/lafouine_dataset.js` reprend ces rapports sous forme de fiches : montants isolés, postes nommés, texte découpé. C’est une transformation, au-delà de la reproduction à l’identique visée par l’autorisation sans frais. La source à indiquer reste « Assemblée nationale du Québec ».

Hub à citer :

```text
Assemblée nationale du Québec, Rapports de dépenses des députés et des cabinets.
https://www.assnat.qc.ca/fr/deputes/rapports-des-depenses/deputes-cabinets.html
```

Les fils RSS restent la propriété de l’Assemblée. Les relais (rss2json, allorigins, corsproxy.io, codetabs, r.jina.ai) sont des services tiers, utilisés parce que le navigateur bloque la lecture directe. Leurs conditions sont les leurs.

## Gouvernement du Québec — divulgations et pages budgétaires

Les PDF de frais, de contrats, de subventions et de salaires sont produits par les ministères et organismes. Ils sont diffusés sur Québec.ca et `cdn-contenu.quebec.ca` au titre de la diffusion proactive.

Le gouvernement du Québec écrit, sur [Québec.ca/droit-auteur](https://www.quebec.ca/droit-auteur), qu’il détient les droits sur les documents, données et compilations qu’il produit, et que leur reproduction, leur stockage, leur adaptation et leur publication demandent une autorisation préalable. Le formulaire de demande est sur cette page.

La mise en ligne d’une divulgation permet au public de la consulter. Elle n’est pas, à elle seule, une licence Creative Commons de rediffusion.

Cette distribution inclut le texte extrait, dans `dataset/lafouine_dataset.js`. Elle n’inclut pas les PDF. Le gouvernement du Québec reste titulaire des documents d’origine. Chaque fiche garde l’URL de la page et du PDF.

Repères budgétaires collés dans le HTML (cadre, comptes publics, plan québécois des infrastructures, stratégie de gestion des dépenses) : mêmes titulaires, mêmes réserves. Leurs URL pointent vers Finances, le Conseil du trésor ou Québec.ca. Les chiffres de ces repères ne sont pas des données ouvertes du seul fait qu’ils apparaissent dans LaFouine.

## Vérificateur général du Québec

Les montants Batteries marqués VGQ sont une transcription du rapport publié le 5 juin 2026 (autorisation 2 204 454 778 $, déboursé 1 877 295 149 $, couverture jusqu’au 30 septembre 2025). Le rapport PDF n’est pas inclus. Le Vérificateur général reste l’auteur du rapport. La transcription peut être incomplète par rapport au texte intégral : le rapport fait foi.

## Marques

« LaFouine » désigne cet explorateur. Québec.ca, Données Québec, CKAN, Assemblée nationale du Québec, Vérificateur général du Québec, IBM Plex et les noms des ministères restent les signes de leurs titulaires. Aucune de ces institutions n’a mandaté ce projet.

## Absence de garantie

Les éditeurs publics excluent déjà leur responsabilité sur l’usage qui est fait de leurs sites. La licence MIT ajoute la sienne sur le code. Un total affiché par LaFouine est une somme de lectures. Il ne constitue ni un compte public, ni une opinion du Vérificateur général, ni une décision d’un ministère.
