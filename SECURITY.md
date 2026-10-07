# Politique de sécurité

S’applique à LaFouine **0.2.2**, la page statique `LaFouine_v0.2.2.html` et le jeu `dataset/lafouine_dataset.js`.

Cette version n’a pas de serveur, pas de compte et pas de clé. Le risque principal est ce que le navigateur envoie à des tiers, et la confiance accordée à un chiffre extrait d’un PDF.

## Ce qui reste sur le poste

- le HTML et le jeu de données, une fois téléchargés;
- les favoris, les vues, la langue, les largeurs de colonnes et l’état des boutons S, E et D, dans `localStorage`;
- le dernier jeu chargé à la main, dans IndexedDB, base `lafouine`, magasin `kv`, clé `gzip`.

Rien de tout cela n’est envoyé à un serveur LaFouine, parce qu’il n’y en a pas.

## Ce qui quitte le poste

Seulement si l’on s’en sert, et seulement vers le service nommé.

| Action | Destination | Ce qui part |
| --- | --- | --- |
| Ouvrir la page | `fonts.googleapis.com`, `fonts.gstatic.com` | Demande de la police IBM Plex Mono. L’adresse IP du poste est vue par Google |
| Bouton CKAN, recherche, ouverture d’une table | `www.donneesquebec.ca` | Requête GET `package_search` ou `datastore_search`. Le texte cherché, les filtres et l’identifiant de ressource partent. Pas de clé |
| Bouton RSS | rss2json, allorigins, corsproxy.io, codetabs, puis `r.jina.ai`, dans cet ordre, jusqu’au premier qui répond | L’URL complète du fil de l’Assemblée. Le relais voit cette URL et l’adresse IP du poste. Le fil lui-même est public |
| Lien « source » d’une fiche | Québec.ca, `cdn-contenu.quebec.ca`, assnat.qc.ca, finances.gouv.qc.ca, ou un autre hôte écrit sur la fiche | Navigation ordinaire vers le document officiel |

La lecture CKAN est anonyme. LaFouine n’appelle aucune action d’écriture (`package_create`, `resource_update`, `datastore_upsert`, et les autres). Une clé d’API Données Québec n’a pas sa place dans cette page : ne pas en coller une dans le HTML, dans une issue ou dans un jeu de données.

Les relais RSS ne sont pas des services de l’Assemblée nationale ni de LaFouine. Qui veut éviter ce transit n’ouvre pas la vue RSS et lit les fils depuis le site de l’Assemblée.

## Jeu de données chargé à la main

Le bouton JEU et le glisser-déposer lisent un fichier local. Le fichier est décompressé dans le navigateur. Il n’est pas téléversé. Un jeu reçu d’un tiers peut contenir n’importe quel texte : le traiter comme une page web non fiable. La compilation livrée avec cette distribution est `dataset/lafouine_dataset.js`.

## Renseignements personnels

Les divulgations et les rapports de dépenses nomment des titulaires de charges publiques, des fournisseurs et des montants déjà publiés par l’État. LaFouine ne crée pas de dossier sur un particulier au-delà de cette republication.

Ne pas ajouter, dans une issue ou une demande de fusion, un renseignement qui n’est pas déjà dans une pièce publique : coordonnées privées, numéro d’assurance sociale, dossier médical, document obtenu par une demande d’accès et non rediffusable.

## Intégrité des chiffres

Un montant faux est un défaut d’extraction, pas une porte d’entrée. Il se corrige en comparant la fiche au PDF, selon [CONTRIBUTING.md](CONTRIBUTING.md). En attendant, le PDF ou le jeu ouvert de l’éditeur fait foi. Ne pas utiliser un total de LaFouine comme seule pièce d’une accusation.

## Signaler un problème de sécurité

Ouvrir une issue si le problème peut être décrit en public sans mode d’emploi d’un abus : un lien trop permissif, un fichier inattendu chargé par la page, une requête vers un hôte qui n’est pas dans le tableau ci-dessus.

Si le détail aiderait à exploiter la page chez quelqu’un d’autre, décrire le symptôme sans le pas à pas, et attendre un correctif avant de publier la recette.

Ne pas déposer dans l’issue de clé, de cookie, de jeton, ou le contenu d’un document qui n’est pas déjà public.

Cette version n’a pas d’adresse de sécurité dédiée. Quand le dépôt GitHub existe, l’onglet Security du dépôt est l’endroit prévu pour cette politique.

## Versions suivantes

Une version qui ajouterait un serveur, un modèle, ou une clé devra réécrire cette page avant d’être publiée. La 0.2.2 ne le fait pas.
