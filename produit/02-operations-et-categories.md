---
id: produit-operations
title: Opérations, catégories et paiements programmés
sidebar_position: 2
---

# Opérations, catégories et paiements programmés

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

## Liste des opérations

Toutes les opérations enregistrées, avec recherche, filtres et une synthèse
portant sur la sélection.

**Comment y arriver** — depuis le tableau de bord, « See All » sous « Last
operations ». Depuis le détail d'un compte ou d'une catégorie, l'écran s'ouvre
**déjà filtré** sur cet élément.

### Ce qu'on y voit

1. Un champ « Rechercher une transaction » et, à droite, une icône de filtre.
2. Si des filtres sont actifs, une rangée de puces — une par filtre — chacune
   avec une croix pour la retirer.
3. **Une carte de synthèse** portant, selon le signe : « Solde de la sélection »
   ou « Déficit de la sélection ». Elle donne le montant net, le nombre
   d'opérations, puis deux sous-totaux « Revenus » et « Dépenses ».
4. Les opérations **groupées par date**, de la plus récente à la plus ancienne.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Rechercher | Saisir dans le champ | La liste se recharge après une courte pause, environ une demi-seconde |
| Filtrer | Toucher l'icône de filtre | Une feuille propose Période (Jour, Mois, Plage), Type (Tous, Dépense, Revenu, Transfert), Compte et Catégorie |
| Retirer un filtre | Toucher la croix de sa puce | Le filtre part et la liste se recharge |
| Exporter le relevé | Toucher l'icône de partage, visible s'il y a des opérations | « Exporter le relevé » propose : partager ou enregistrer, enregistrer dans l'application, imprimer |
| Ouvrir une opération | Toucher sa carte | Le détail s'ouvre |

### Ce qui est pris en compte

- **Aucun filtre n'est actif par défaut** quand on arrive depuis le tableau de
  bord. En revanche, arriver depuis un compte ou une catégorie **pose un filtre**
  — c'est voulu, mais il faut le savoir pour comprendre un total inattendu.
- Les filtres **se combinent** : une opération doit satisfaire tous les critères.
- La période « Jour » couvre la journée entière, jusqu'à 23 h 59 min 59 s ; la
  période « Mois » couvre le mois civil ; la plage libre accepte un début et une
  fin indépendants, chacun effaçable.
- ⚠️ **La synthèse ne porte que sur la sélection affichée**, pas sur le solde de
  vos comptes. Un filtre actif change le montant : c'est normal.
- **Les filtres persistent** quand on quitte l'écran et qu'on y revient. Ouvrir
  la liste depuis une catégorie efface d'abord les filtres précédents, puis pose
  le sien.
- L'export reprend exactement les groupes et les totaux affichés.

### Quand il n'y a rien, ou que ça charge

- Chargement : un indicateur remplace la liste.
- Aucun résultat : « Aucune opération ne correspond à ces filtres. »

---

## Saisie d'une opération

Enregistrer une dépense, un revenu ou un transfert.

**Comment y arriver** — le bouton « + » central, ou une action rapide du détail
d'un compte. **Le type se choisit avant d'arriver ici** et ne peut plus être
changé sur cet écran.

### Ce qu'on y voit

Le titre suit le type : « Nouvelle dépense », « Nouveau revenu » ou « Transfert
de fonds ».

**Dépense ou revenu** — Montant · Montant attendu (optionnel) · Catégorie, ou
« Catégorie/provenance » pour un revenu · Compte de paiement, ou Compte de dépôt
· Membre concerné, ou « Membre à l'origine du revenu » · Date, préremplie à
« maintenant » · Note · bouton « Enregistrer ».

**Transfert** — Compte de retrait · Compte de dépôt · Montant · Date · Note ·
bouton « Enregistrer ».

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Saisir un montant attendu | Facultatif, supérieur ou égal au montant versé | L'opération devient un **règlement partiel** : « Avance : il restera … à régler. » |
| Choisir une catégorie | Toucher le champ | La liste du type correspondant s'ouvre ; « Créer » permet d'en ajouter une sans quitter la saisie |
| Rattacher un membre | Toucher le champ, s'il apparaît | L'opération est rattachée à ce membre |
| Enregistrer | Toucher « Enregistrer » | L'opération part, puis soldes, budgets, statistiques et notifications sont recalculés |

### Ce qui est pris en compte

- **Champs obligatoires.** Dépense ou revenu : un montant strictement positif,
  une catégorie, un compte. Transfert : un montant strictement positif, un compte
  de retrait et un compte de dépôt. ⚠️ Tant qu'il en manque un, le bouton
  « Enregistrer » reste **grisé sans message** — rien n'indique lequel manque.
- **Le montant attendu ne peut pas être inférieur au montant versé** : « Le
  montant attendu ne peut pas être inférieur au montant versé. » S'il est
  supérieur, le reste à régler est calculé et affiché.
- ⚠️ **Le champ Membre n'apparaît que si le compte choisi a des membres.**
  Changer de compte **remet le membre à zéro** : une saisie longue peut perdre ce
  rattachement sans prévenir.
- **Le membre concerné n'est pas l'auteur de la saisie.** Le premier dit *pour
  qui* ou *de qui* vient l'argent ; le second, qui a tapé l'opération. Le détail
  les affiche séparément.
- **Effet en cascade, immédiat** : une dépense diminue le solde du compte, un
  revenu l'augmente, un transfert débite l'un et crédite l'autre. Si la catégorie
  est suivie par un budget de la période, l'enveloppe est consommée et le budget
  peut basculer en alerte. Les statistiques et les notifications suivent.
- Un transfert n'accepte pas de montant attendu.

---

## Détail d'une opération

Tout ce qui a été enregistré, le reçu, et l'annulation.

**Comment y arriver** — toucher une opération dans la liste.

### Ce qu'on y voit

- Un menu « ⋮ » en haut à droite.
- Si l'opération est un règlement partiel, un bandeau « Règlement partiel » avec
  la progression et trois montants : « Attendu », « Versé », « Reste à régler ».
- Une carte d'informations : Type · Catégorie · Compte · Compte de dépôt pour un
  transfert · Membre concerné · **Enregistré par** · Montant, ou Montant versé ·
  Montant attendu et Reste à régler le cas échéant · État · Date · Note.
- Un bouton « Reçu PDF », **uniquement si l'opération peut en produire un**.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Obtenir un reçu | Toucher « Reçu PDF » | Partager, enregistrer dans l'application, ou imprimer |
| Annuler l'opération | Menu « ⋮ » → « Annuler l'opération » | Confirmation : « Les soldes et budgets impactés seront recalculés. Continuer ? » |

### Ce qui est pris en compte

- ⚠️ **La suppression est définitive.** Soldes, budgets et statistiques sont
  recalculés dans la foulée, sans retour arrière possible.
- Le reçu n'est pas proposé pour toutes les opérations.
- Le bandeau de règlement partiel n'apparaît que si le montant attendu dépasse le
  montant versé.

### Quand il n'y a rien

Après une suppression : « Aucune opération sélectionnée. »

---

## Liste des catégories

Les catégories de dépense et les provenances de revenu, avec leurs cumuls.

**Comment y arriver** — depuis l'onglet Dépenses, « Tout afficher » à côté de
« Catégories ».

### Ce qu'on y voit

Un champ « Rechercher une catégorie », deux onglets « Dépenses » et « Revenus »,
puis une grille de tuiles — icône sur fond coloré, nom, montant cumulé. La grille
se termine par une tuile en pointillés : « Nouvelle catégorie » ou « Nouvelle
provenance » selon l'onglet.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Rechercher | Saisir dans le champ | La grille se filtre **immédiatement**, sans appel au serveur |
| Changer d'onglet | Toucher « Dépenses » ou « Revenus » | La grille change de type |
| Ouvrir une catégorie | Toucher une tuile | Le détail s'ouvre |
| Créer | Toucher la tuile en pointillés | Le formulaire s'ouvre, type présélectionné |

### Ce qui est pris en compte

- La recherche porte sur le **nom et la description**, sans tenir compte des
  majuscules, et s'applique localement : elle est instantanée.
- Le cumul de chaque catégorie est chargé avec la liste ; s'il n'a pas pu être
  récupéré, il s'affiche à zéro.
- La tuile de création reste visible même quand la recherche ne rend rien.
- Trois tuiles par ligne sur téléphone, quatre sur tablette.

### Quand il n'y a rien, ou que ça charge

Recherche infructueuse : « Aucune catégorie ne correspond à « … ». »

---

## Détail d'une catégorie

Les indicateurs d'une catégorie, et sa suppression.

**Comment y arriver** — toucher une tuile dans la liste des catégories.

### Ce qu'on y voit

1. Une carte d'identité teintée : icône, nom, et le type — « Catégorie de
   dépense » ou « Provenance de revenu » — puis la description éventuelle.
2. **Cumul depuis le début** : le total, le cumul du mois en cours, et la
   variation par rapport au mois précédent.
3. Quatre tuiles : « Opérations » (nombre), « Montant moyen », « Part sur 12
   mois » avec la mention « de vos dépenses » ou « de vos revenus », et
   « Dernière fois ».
4. **Évolution sur 12 mois** — une courbe.
5. Un bouton « Voir les N opérations », désactivé et affichant « Aucune
   opération » s'il n'y en a pas.
6. Un bouton « Supprimer la catégorie », **ou** un encart expliquant pourquoi
   c'est impossible.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Voir les opérations | Toucher « Voir les N opérations » | La liste s'ouvre : **les filtres précédents sont effacés**, puis le filtre de catégorie est posé |
| Supprimer | Toucher « Supprimer la catégorie » | « « Nom » sera définitivement supprimée. Cette action est irréversible. » |

### Ce qui est pris en compte

- ⚠️ **La suppression n'est possible que si la catégorie ne porte aucune
  opération.** Sinon le bouton laisse place à : « Suppression impossible : cette
  catégorie porte N opérations. » Ce n'est pas une panne, c'est la protection de
  l'historique.
- Les indicateurs portent sur **toute** l'histoire de la catégorie, sans filtre
  de période — contrairement aux écrans de statistiques.
- La part sur 12 mois se rapporte à l'ensemble des dépenses, ou des revenus,
  selon le type de la catégorie.

---

## Création d'une catégorie

**Comment y arriver** — la tuile en pointillés de la liste, ou « Créer » depuis
un sélecteur de catégorie pendant une saisie.

### Ce qu'on y voit

Titre « Nouvelle catégorie ». Champs : « Type de la catégorie » (« Dépense » ou
« Revenus »), « Nom de la catégorie », « Icône de la catégorie », « Couleur de la
catégorie », puis un aperçu en direct — l'icône blanche sur la couleur choisie —
et le bouton **« Save »** ⚠️, resté en anglais.

### Ce qui est pris en compte

- **Le nom et l'icône sont obligatoires.** La couleur a une valeur par défaut et
  ne bloque pas.
- Le type reste modifiable ici, même s'il était présélectionné.
- La création recharge la liste des catégories et leurs cumuls.
- ⚠️ Tant que le formulaire est incomplet, le bouton reste grisé **sans message**.

---

## Liste des paiements programmés

Les prélèvements et versements récurrents, avec leur prochaine échéance.

**Comment y arriver** — depuis l'onglet Dépenses, « Voir tout » à côté de
« Scheduled payments » ⚠️.

### Ce qu'on y voit

Un champ « Rechercher un paiement », un bouton « Programmer un paiement », puis
la liste. Chaque carte porte le nom, la fréquence, le montant précédé de « − »
pour une dépense ou « + » pour un revenu, le compte, la prochaine échéance et son
statut.

### Ce qui est pris en compte

- La liste est triée par **échéance la plus proche**.
- La recherche interroge le serveur, après une courte pause.
- Le statut signale un **retard** quand l'échéance est passée sans prélèvement.

### Quand il n'y a rien

- Aucun paiement : « Aucun paiement programmé. »
- Recherche infructueuse : « Aucun résultat pour cette recherche. »

---

## Détail d'un paiement programmé

**Comment y arriver** — toucher une carte dans la liste.

### Ce qu'on y voit

Un menu « ⋮ », une carte de synthèse — nom, fréquence, montant signé, Compte,
Prochaine échéance, Statut — puis une section **« Transaction History »** ⚠️
listant les exécutions passées : date d'échéance, statut (« Paid … » ⚠️ ou « En
attente de prélèvement ») et montant.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Supprimer | Menu « ⋮ » → « Supprimer le paiement » | « « Nom » ne sera plus prélevé automatiquement. » |

⚠️ **La suppression est irréversible** : le prélèvement automatique cesse.

### Quand il n'y a rien

Historique vide : « Aucun prélèvement pour l'instant. »

---

## Programmation d'un paiement

Un formulaire en **deux étapes**.

**Comment y arriver** — « Programmer un paiement », depuis l'onglet Dépenses ou
la liste des paiements.

### Ce qu'on y voit

**Étape 1 — « Informations du paiement »** : Nom du paiement · Montant · Compte
de paiement · Type (« Dépense » ou **« Revenue »** ⚠️, graphie fautive : lire
« Revenu ») · Catégorie de la dépense, ou Provenance du revenu. Bouton
« Suivant ».

**Étape 2 — « Programme de paiement »** : Fréquence de paiement · « Répéter tous
les X » · Date du premier paiement. Boutons « Précédent » et « Programmer ».

### Ce qui est pris en compte

- Pour passer à l'étape 2 : un nom, un montant strictement positif et un compte.
  **La catégorie n'est pas obligatoire.**
- Pour programmer : la répétition doit valoir au moins 1. **La date du premier
  paiement est facultative.**
- ⚠️ **Changer la fréquence remet la répétition à 1.** Quelqu'un qui règle
  « tous les 3 » puis change de rythme repart de 1 sans que rien ne le signale.
- L'enregistrement recharge la liste des paiements et les notifications.
