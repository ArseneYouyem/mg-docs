---
id: produit-accueil
title: Accueil, navigation et statistiques
sidebar_position: 1
---

# Accueil, navigation et statistiques

> ## ⛔ Règle ultime — la doc produit suit l'écran
>
> **Ce dossier `produit/` se modifie depuis `mg-mobile`**, et lui seul — c'est
> l'exception au sens unique qui gouverne le reste de ce dépôt, où la source est
> `mg-backend`. L'interface décrite ici vit dans le mobile : la documenter
> ailleurs garantirait qu'elle prenne du retard.
>
> **Toute modification de l'interface ou d'une règle d'affichage met à jour cette
> page dans le même commit.** Un écran qui change sans sa page laisse une
> description que le support et l'assistant croiront — et une doc fausse coûte
> plus cher qu'une doc absente.

## Conteneur principal à quatre onglets

Le point d'entrée : la navigation principale, les réglages rapides et l'accès
aux grands modules.

**Comment y arriver** — dès l'ouverture de l'application, une fois la session
ouverte. L'application exige un compte : il n'y a pas de consultation sans
connexion.

### Ce qu'on y voit

- **Barre du haut** — le logo MoneyGes, le nom de l'utilisateur, un bouton de
  bascule clair/sombre (icône lune), une cloche portant une pastille du nombre
  de notifications non lues, et un avatar rond.
- **Zone de contenu** — quatre onglets : Accueil, Dépenses, Modules, Menu. On
  passe de l'un à l'autre par la barre basse ou en glissant horizontalement.
- **Barre de navigation basse** — les quatre icônes ; l'onglet actif est mis en
  évidence.
- **Bouton central flottant** — un « + » ancré au centre de la barre basse.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Changer d'onglet | Toucher une icône de la barre basse, ou glisser | La page correspondante s'affiche |
| Basculer le thème | Toucher l'icône lune | Toute l'application passe du clair au sombre, ou l'inverse |
| Ouvrir les notifications | Toucher la cloche | L'écran des notifications s'ouvre |
| Enregistrer une opération | Toucher le « + » | Une feuille d'action rapide propose le type d'opération |

### Ce qui est pris en compte

- La pastille de la cloche n'apparaît que s'il existe au moins une notification
  non lue ; elle en affiche le nombre exact.
- Le bouton de thème et la cloche restent accessibles depuis les quatre onglets.
- Le nom affiché vient du profil ; tant qu'il n'est pas chargé, l'application
  affiche « Invité » — c'est un repli d'affichage, pas un mode d'utilisation.

### Quand il n'y a rien, ou que ça charge

L'ossature s'affiche immédiatement ; chaque onglet charge ses données pour son
propre compte.

---

## Tableau de bord

La synthèse : appel de l'assistant, épargne, comptes, dernières opérations,
dettes et budget en cours.

**Comment y arriver** — premier onglet, icône maison. C'est l'écran par défaut.

### Ce qu'on y voit

Dans l'ordre d'affichage :

1. **Bannière de fermeture de compte**, si une fermeture a été confirmée. Elle
   reste **48 heures**, puis la fermeture devient irréversible.
2. **Barre Leo** — un champ stylisé qui invite à poser une question. Ce n'est pas
   un champ de saisie : le toucher ouvre la conversation.
3. **Bloc statistique** — un encart en dégradé avec un titre, un message de
   synthèse, le libellé « View Details » ⚠️ et une jauge circulaire portant un
   montant sous l'étiquette « Saved » ⚠️. Il synthétise l'épargne — revenus moins
   dépenses — sur la période retenue par le serveur.
4. **Comptes** — titre « Comptes », lien « Voir tout », puis une rangée
   horizontale de cartes portant chacune un compte et son solde, dans la devise
   du compte. Une carte « + » ferme la rangée.
5. **Dernières opérations** — titre « Last operations » ⚠️, lien « See All » ⚠️,
   puis trois onglets « All » / « Spending » / « Income » ⚠️. Les opérations sont
   groupées par date ; **seuls les deux premiers groupes** sont affichés.
6. **Dettes et créances** — la carte de synthèse, identique à celle de l'onglet
   Modules.
7. **Budgets** — titre « Budgets », lien « Voir tout », puis la carte du budget
   actif le plus consommé, avec un bouton « Détails ».

⚠️ Les libellés « View Details », « Saved », « Last operations », « See All »,
« All », « Spending » et « Income » sont **en anglais dans une application
française** : ce sont des défauts de traduction à corriger.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Rafraîchir | Tirer l'écran vers le bas | Comptes, opérations, budgets, statistiques, notifications et dettes sont rechargés |
| Ouvrir l'assistant | Toucher la barre Leo | La conversation s'ouvre |
| Voir les statistiques | Toucher le bloc statistique | L'écran Statistiques s'ouvre |
| Voir tous les comptes | Toucher « Voir tout » | La liste des comptes s'ouvre |
| Ajouter un compte | Toucher la carte « + » | Le formulaire de création s'ouvre |
| Voir toutes les opérations | Toucher « See All » | La liste s'ouvre, **filtres réinitialisés** |
| Filtrer les opérations récentes | Toucher « All », « Spending » ou « Income » | La liste se restreint au type choisi |
| Ouvrir le budget mis en avant | Toucher « Détails » | Le détail du budget s'ouvre |
| Planifier un budget | Toucher « Planifier un budget » | Le formulaire de création s'ouvre |

### Ce qui est pris en compte

- **Le bloc statistique ne dit pas sa période.** Le montant est l'épargne nette
  calculée par le serveur ; il ne se recoupe donc pas nécessairement avec ce que
  montre l'écran Statistiques, dont la période se choisit à la main.
- **Les soldes sont dans la devise de chaque compte** — pas dans une devise
  unique. Un utilisateur qui tient un compte en francs et un autre en euros voit
  deux devises côte à côte.
- **Les dernières opérations s'arrêtent à deux groupes de dates**, pas à un
  nombre d'opérations : une journée chargée peut remplir l'écran à elle seule.
  Le filtre par type s'applique **avant** le groupement.
- **Le budget mis en avant est le plus consommé** parmi les budgets actifs, pas
  le plus récent ni le plus gros. ⚠️ Les autres ne sont accessibles que par
  « Voir tout ».
- **La bannière de fermeture ne propose aucune action** : l'annulation se fait
  depuis les réglages.

### Quand il n'y a rien, ou que ça charge

- Au chargement, chaque bloc affiche un squelette qui épouse la forme de ce qui
  va s'afficher — rangée de cartes pour les comptes, liste pour les opérations.
- Aucune opération récente : « Aucune opération pour l'instant. »
- Aucun budget actif : « Aucun budget actif. Planifiez-en un pour suivre vos
  dépenses. », suivi du bouton « Planifier un budget ».
- Le bloc Comptes n'a pas de message vide : la carte « + » tient lieu d'invite.

---

## Onglet Dépenses

Le suivi des dépenses : courbe revenus/dépenses, répartition par catégorie, et
paiements programmés.

**Comment y arriver** — deuxième onglet.

### Ce qu'on y voit

1. **Bloc Dépenses** — titre et lien « Détails ». La carte porte deux onglets de
   granularité, « Mensuel » (par défaut) et « Annuel » ; un bouton calendrier à
   droite affichant la fenêtre analysée ; une courbe à deux lignes, Revenu et
   Dépenses, avec sa légende.
2. **Catégories** — titre et lien « Tout afficher ». Une rangée horizontale des
   **six premières** catégories avec leur montant, fermée par une carte
   « Nouvelle catégorie ».
3. **Paiements programmés** — titre « Scheduled payments » ⚠️ et lien « Voir
   tout ». Les **trois prochains** paiements, puis un bouton « Programmer un
   paiement ».

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Rafraîchir | Tirer vers le bas | Courbe, catégories et paiements sont rechargés |
| Changer la granularité | Toucher « Mensuel » ou « Annuel » | La courbe se recharge, et **la fenêtre revient à la période en cours** |
| Changer la fenêtre | Toucher le bouton calendrier | Une grille de mois (en Mensuel) ou d'années (en Annuel) s'ouvre |
| Voir le détail des dépenses | Toucher « Détails » | L'écran Statistiques des dépenses s'ouvre |
| Voir toutes les catégories | Toucher « Tout afficher » | La liste des catégories s'ouvre |
| Créer une catégorie | Toucher « Nouvelle catégorie » | Le formulaire s'ouvre, type « dépense » présélectionné |
| Programmer un paiement | Toucher « Programmer un paiement » | Le formulaire de programmation s'ouvre |

### Ce qui est pris en compte

- ⚠️ **Changer de granularité remet la fenêtre à aujourd'hui.** Quelqu'un qui
  analyse mars 2026 en mensuel, puis bascule en annuel, se retrouve sur l'année
  en cours — pas sur 2026 si l'on est en 2027.
- La rangée de catégories s'arrête à **six** : ce n'est pas un classement
  complet, et une petite catégorie peut être absente sans avoir disparu.
- Les paiements affichés sont les **trois prochains**, dans l'ordre des
  échéances.

### Quand il n'y a rien, ou que ça charge

- Chargement : squelettes pour la courbe, les catégories et les paiements.
- Aucune donnée sur la période : « Pas encore de données sur cette période. »
- Aucun paiement : « Aucun paiement programmé. »

---

## Onglet Modules

Les modules disponibles, et ceux annoncés.

**Comment y arriver** — troisième onglet.

### Ce qu'on y voit

- La carte de synthèse **Dettes et créances**, la même que sur le tableau de bord.
- Une section « Modules à venir », avec la phrase « Ces modules arrivent dans une
  prochaine version. »
- Deux cartes en pointillés, estompées, portant un badge « Bientôt » :
  **Tontine** et **Epargne**.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Rafraîchir | Tirer vers le bas | Les totaux de dettes et créances sont rechargés |
| Ouvrir les dettes et créances | Toucher la carte de synthèse | L'écran de gestion s'ouvre |

⚠️ Les cartes « Tontine » et « Epargne » ne réagissent pas au toucher : ces
modules ne sont pas encore livrés.

### Ce qui est pris en compte

La carte de dettes est **partagée** avec le tableau de bord : une retouche vaut
pour les deux écrans, et un rafraîchissement de l'un met l'autre à jour.

---

## Menu

Profil, code client, parrainage, réglages et version.

**Comment y arriver** — quatrième onglet.

### Ce qu'on y voit

Une grille de cartes — deux colonnes sur téléphone, trois sur tablette :

| Carte | Sous-titre |
|---|---|
| **Profil** | « Identité, coordonnées, code client » |
| **Code client** | Carte plus haute : un QR code, puis le code formaté et une icône de copie |
| **Parrainage** | « Inviter des proches, gagner de l'argent » |
| **Paramètres** | « Compte, préférences, aide et mentions » |
| **V 1.0.0** | « Version de l'application instalée » ⚠️ — faute d'orthographe, lire « installée » |

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Ouvrir le profil | Toucher « Profil » | L'écran de profil s'ouvre |
| Copier le code client | Toucher le code sous le QR | Le code part dans le presse-papiers, avec une confirmation |
| Ouvrir le parrainage | Toucher « Parrainage » | L'écran de parrainage s'ouvre |
| Ouvrir les réglages | Toucher « Paramètres » | Les réglages s'ouvrent |

⚠️ **Le menu ne propose pas de déconnexion.** Elle se trouve dans les réglages.

### Ce qui est pris en compte

Le QR encode le code client de l'utilisateur : c'est lui que le scanner d'un
autre utilisateur lit pour l'inviter sur un compte partagé.

### Quand il n'y a rien, ou que ça charge

Tant que le code client n'est pas chargé, un squelette remplace le QR et le code
affiche « — ».

---

## Statistiques

L'analyse détaillée : filtres, indicateurs, évolution et tableau période par
période.

**Comment y arriver** — depuis le tableau de bord, toucher le bloc statistique.

### Ce qu'on y voit

1. **Barre de titre** « Statistiques ». À droite, un bouton « Réinitialiser »
   **qui n'apparaît que si** un filtre catégorie ou compte est actif.
2. **Trois pastilles de filtre** : la période, « Catégorie » et « Compte ». Une
   pastille active porte une croix pour retirer son filtre.
3. **Bloc principal** : le montant net sous l'étiquette « Épargné sur la
   période » ou « Déficit », le pourcentage du revenu épargné, et la portée —
   période, catégorie et compte séparés par « · ».
4. **Deux tuiles** : « Revenus » et « Dépenses », chacune avec son total et sa
   variation.
5. **Courbe d'évolution** — revenus et dépenses par sous-période.
6. **Tableau de détail** — une ligne par sous-période avec Revenus, Dépenses,
   Solde, et une ligne de total.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Changer la période | Toucher la pastille de période | Une feuille propose la granularité — Journalier, Hebdomadaire, Mensuel, Annuel — puis la fenêtre |
| Filtrer par catégorie ou par compte | Toucher la pastille correspondante | Le filtre s'applique **à la fois** au montant net, à la courbe et au tableau |
| Retirer un filtre | Toucher la croix de sa pastille | Le filtre part et l'écran se recharge |
| Tout réinitialiser | Toucher « Réinitialiser » | Catégorie et compte sont effacés ; **la période est conservée** |
| Surligner une ligne | Toucher une ligne du tableau | La ligne se surligne ; un second toucher l'éteint |

### Ce qui est pris en compte

- **Période par défaut** : mensuelle, sur le mois en cours. Aucun filtre de
  catégorie ni de compte n'est actif au départ.
- ⚠️ **La courbe disparaît en granularité Journalier.** Ce n'est pas une panne :
  une journée n'a pas de sous-périodes à tracer.
- ⚠️ **Le tableau masque les lignes sans mouvement.** Un mois à zéro ne s'affiche
  pas — il ne manque pas, il est vide. Le total ne porte donc que sur les lignes
  visibles, ce qui revient au même.
- **Les variations comparent à la période précédente de même durée.** La couleur
  suit le sens métier : une hausse de revenus est verte, une hausse de dépenses
  est rouge. En deçà de 0,5 %, l'écran affiche « Stable vs période précédente »
  plutôt qu'un pourcentage trompeur.
- Le pourcentage du revenu épargné est arrondi à l'entier.

### Quand il n'y a rien, ou que ça charge

- Chargement : squelettes pour les indicateurs, la courbe et le tableau.
- Aucune opération sur le périmètre : « Aucune opération sur ce périmètre. », et
  le tableau ne s'affiche pas.

---

## Statistiques des dépenses

La répartition par catégorie, en camembert et en liste.

**Comment y arriver** — depuis l'onglet Dépenses, toucher « Détails ».

### Ce qu'on y voit

1. **Barre de titre** « Statistiques des dépenses ».
2. **Deux pastilles** : la fréquence et le compte.
3. **Un bouton pleine largeur** affichant la fenêtre exacte et son statut,
   « Période en cours » ou « Période close ». Un bouton « Aujourd'hui »
   apparaît dès qu'on s'éloigne de la période courante.
4. **Deux onglets** : « Dépenses » (par défaut) et « Revenus ».
5. **Un camembert** portant en son centre le type et le total de la période,
   avec une légende par catégorie.
6. **Un bouton** « Nouvelle catégorie de dépense » ou « Nouvelle provenance de
   revenu », selon l'onglet.
7. **La liste des catégories** : nom, montant et part.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Changer la fréquence | Toucher la pastille | Journalier, Hebdomadaire, Mensuel ou Annuel |
| Changer la fenêtre | Toucher le bouton de période | Une grille adaptée à la fréquence s'ouvre |
| Revenir au présent | Toucher « Aujourd'hui » | La fenêtre revient à la période contenant aujourd'hui |
| Filtrer par compte | Toucher la pastille Compte | La répartition ne porte plus que sur ce compte |
| Basculer Dépenses / Revenus | Toucher l'autre onglet | Camembert, liste **et libellé du bouton de création** changent |

### Ce qui est pris en compte

- Fréquence mensuelle par défaut, sur le mois en cours ; aucun filtre de compte.
- Les parts du camembert sont arrondies à l'entier : ⚠️ leur somme peut donner
  99 % ou 101 %.
- Le bouton de création ouvre le formulaire avec **le type de l'onglet actif**
  déjà choisi.

### Quand il n'y a rien, ou que ça charge

- Chargement : squelettes pour le camembert et la liste.
- Aucun mouvement : le camembert disparaît et la liste affiche « Aucun mouvement
  sur cette période. »

---

## Notifications

Les notifications reçues, et leur lecture.

**Comment y arriver** — toucher la cloche dans la barre du haut.

### Ce qu'on y voit

- **Barre de titre** « Notifications », avec à droite un bouton « Mark all as
  read » ⚠️, grisé s'il n'y a rien à marquer.
- **La liste** : chaque notification porte une icône ronde, son titre, sa date
  relative — « Today | 8:25 », « 1 day ago | 14:25 », « 3 days ago | 14:25 » ⚠️ —
  et son message. Une non-lue se distingue par une pastille et une bordure
  colorée.

⚠️ Le bouton et les dates relatives sont **en anglais** : défauts de traduction
à corriger.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Marquer comme lue | Toucher une notification non lue | La pastille et la bordure partent, le compteur de la cloche diminue |
| Tout marquer comme lu | Toucher « Mark all as read » | Le compteur passe à zéro |
| Rafraîchir | Tirer vers le bas | La liste se recharge |

### Ce qui est pris en compte

- Les titres et messages arrivent **traduits par le serveur**, dans la langue de
  la requête. Ils ne sont pas retraduits par l'application.
- Une notification déjà lue ne réagit pas au toucher.

### Quand il n'y a rien, ou que ça charge

- Chargement : squelettes de lignes.
- Liste vide : « Aucune notification pour le moment. »
