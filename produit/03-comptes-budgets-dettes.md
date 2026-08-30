---
id: produit-comptes
title: Comptes, budgets, dettes et créances
sidebar_position: 3
---

# Comptes, budgets, dettes et créances

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

## Liste des comptes

Le solde global et tous les comptes.

**Comment y arriver** — depuis le tableau de bord, « Voir tout » à côté de
« Comptes ».

### Ce qu'on y voit

Le libellé **« Balance »** ⚠️ (en anglais) suivi du total, puis une grille de
cartes — icône, nom, solde — fermée par une carte d'ajout.

### Ce qui est pris en compte

- Le total est la somme des soldes de tous les comptes.
- ⚠️ **Le total s'affiche dans la devise du premier compte.** Quelqu'un qui tient
  un compte en francs et un autre en euros voit une somme dans une seule devise,
  sans conversion : le chiffre n'a alors pas de sens économique.
- Les données sont rechargées en arrière-plan si la liste est déjà remplie.

---

## Détail d'un compte

Solde, actions rapides, références, et trois onglets.

**Comment y arriver** — toucher une carte dans la liste des comptes.

### Ce qu'on y voit

1. Une carte colorée : icône, nom, la mention **« Compte personnel »** ou
   **« Partagé · X membres »**, le **Solde disponible**, une barre de répartition
   et les cumuls **Revenus** / **Dépenses**.
2. Trois actions rapides : **Transfert de fonds**, **Enregistrer un revenu**,
   **Enregistrer une dépense**.
3. **Références du compte** — les numéros enregistrés (Orange Money, UBA…), avec
   un bouton d'ajout.
4. Trois onglets : **Opérations**, **Cotisations**, **Membres**.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Enregistrer une opération | Une des trois actions rapides | Le formulaire s'ouvre avec **le type et le compte déjà choisis** |
| Modifier le compte | Icône crayon, si elle est visible | Le formulaire de modification s'ouvre |
| Gérer les références | Boutons d'ajout, de modification, de suppression | Une feuille de saisie s'ouvre ; la suppression demande confirmation |
| Ajouter un membre | Bouton **Ajouter un membre**, s'il est visible | La feuille d'invitation s'ouvre |
| Rechercher un membre | Champ **Rechercher un membre** | Filtre sur le nom, le téléphone ou le code client |
| Voir un membre | Toucher sa ligne | Une feuille montre ses permissions |

⚠️ Une action tentée sans le droit correspondant affiche **« Action non
autorisée »** en nommant la permission manquante. Le bouton n'est pas caché : il
refuse.

### Ce qui est pris en compte

- **Les permissions gardent chaque action** : modifier le compte, transférer des
  fonds, enregistrer une opération, gérer les cotisations, gérer les membres.
- **Le créateur détient tous les droits.** Un membre autorisé à gérer les membres
  peut inviter, retirer et ajuster les droits des autres — ⚠️ **jamais ceux du
  créateur**.
- **Trois états de membre** :

  | État | Ce que ça veut dire | Ce qu'il peut faire |
  |---|---|---|
  | **Actif** | A accepté l'invitation | Tout ce que ses permissions autorisent |
  | **Invité** | L'invitation est partie, pas encore acceptée | Rien : l'accès n'existe qu'après acceptation |
  | **Non rattaché** | Saisi à la main, sans compte MoneyGes | Rien ; il peut être rattaché plus tard par son code client, **en conservant tout son historique** |

- ⚠️ **Le compte personnel créé à l'inscription n'accueille personne.** L'onglet
  Membres affiche alors un avis et propose de créer un compte partagé — ce n'est
  pas une panne.
- Le champ de recherche de membre n'apparaît **qu'à partir de quatre membres**.
  La recherche par téléphone ne considère que les chiffres, indicatif compris.

### Quand il n'y a rien, ou que ça charge

- Aucun compte sélectionné : « Aucun compte sélectionné. »
- « Aucune opération sur ce compte. » · « Aucune cotisation programmée sur ce
  compte. » · « Ce compte n'est partagé avec personne. »
- Recherche infructueuse : « Aucun membre ne correspond à « … » »

---

## Création et modification d'un compte

**Comment y arriver** — la carte d'ajout de la liste ; ou l'icône crayon du
détail, si la permission est accordée.

### Ce qu'on y voit

Titre **« Nouveau compte »** ou **« Modifier le compte »**.

Champs communs : Nom du compte · Icône du compte · Couleur du compte.
**En création seulement** : Pays du compte · Devise du compte · Numéros de
référence (facultatif) · un aperçu. Bouton **« Save »** ⚠️ en création,
**« Mettre à jour »** en modification.

### Ce qui est pris en compte

- **Obligatoires** : un nom non vide et une icône. En création, le pays et la
  devise le sont aussi.
- Le pays est proposé d'après le profil, et reste modifiable.
- Les devises offertes pour un pays sont : **sa devise locale, puis l'euro et le
  dollar**.
- ⚠️ **Le pays et la devise ne se modifient plus après la création** — ils
  disparaissent même du formulaire. Une erreur à la création se corrige en
  ouvrant un autre compte.
- Formulaire incomplet : « Renseignez un nom et choisissez une icône. » ou
  « Choisissez le pays et la devise du compte. »

---

## Scanner de code client

Lire le code d'un utilisateur pour l'inviter sur un compte.

**Comment y arriver** — depuis la feuille d'ajout de membre, choisir de scanner.

### Ce qu'on y voit

La caméra, un cadre de visée rouge, et le texte **« Scan a code »** ⚠️. Après
lecture : **« Barcode Type: … Data: … »** ⚠️ — libellés techniques en anglais,
visibles par l'utilisateur.

### Ce qui est pris en compte

- L'accès à la caméra est requis ; s'il est refusé, l'écran affiche **« no
  Permission »** ⚠️.
- Le code attendu est un **code client à 7 chiffres**.
- L'écran se referme dès le premier code lu.

---

## Liste des budgets

**Comment y arriver** — depuis le tableau de bord, « Voir tout » à côté de
« Budgets ».

### Ce qu'on y voit

Deux onglets, **« Active »** et **« Closed »** ⚠️ (en anglais). Une grande carte
**« Add new budget »** ⚠️. Puis la liste, chaque bloc portant un lien **« See
Details »** ⚠️.

### Ce qui est pris en compte

- L'onglet **Active** est actif par défaut ; le filtre s'applique localement.
- Un budget est **actif** ou **clôturé**, la clôture étant une action volontaire.

### Quand il n'y a rien

« Aucun budget actif. » · « Aucun budget clôturé. »

---

## Détail d'un budget

La consommation de l'enveloppe.

**Comment y arriver** — toucher un budget dans la liste.

### Ce qu'on y voit

1. La plage de dates — avec une date de fin seulement si le budget en a une.
2. Une ligne **« Spend: … / … »** ⚠️ et le pourcentage consommé.
3. Une barre de progression dont la couleur suit l'état.
4. **« Reste … sur l'enveloppe. »** ou **« Dépassement de … »**
5. Une courbe comparant l'enveloppe aux dépenses dans le temps.
6. Un camembert de répartition par catégorie, puis le détail par catégorie.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Clôturer | Menu ⋮ → « Clôturer le budget » | Le budget bascule dans l'onglet **Closed** |
| Supprimer | Menu ⋮ → « Supprimer le budget » | Confirmation, puis suppression définitive |

⚠️ **La clôture ne se défait pas depuis l'application** : aucun bouton ne
rouvre un budget clôturé.

### Ce qui est pris en compte

- **L'enveloppe ne suit que les catégories choisies à la création.** Si aucune
  n'a été choisie, elle suit **toutes** les dépenses. ⚠️ C'est la première cause
  d'un budget qui « ne bouge pas » : la dépense enregistrée n'appartient pas aux
  catégories suivies.
- Un budget est **à durée fixe** — début et fin affichés — ou **récurrent**, et
  n'affiche alors que sa date de début.
- Le pourcentage rapporte le dépensé au montant de l'enveloppe.

### Quand il n'y a rien

« Aucun budget sélectionné. » · « Aucune dépense sur ce budget pour l'instant. »

---

## Création d'un budget

**Comment y arriver** — « Add new budget » depuis la liste, ou « Planifier un
budget » depuis le tableau de bord.

### Ce qu'on y voit

Titre **« Planifier un budget »**. Champs : Montant · Nom du budget ·
Périodicité — durée fixe ou récurrente · une plage de dates **ou** une fréquence
selon le choix · **Catégories concernées**. Bouton **« Planifier »**.

### Ce qui est pris en compte

- **Obligatoires** : un nom, un montant strictement positif, et en durée fixe les
  deux dates.
- Seules les **catégories de dépense** sont proposées.
- ⚠️ **Aucune catégorie sélectionnée signifie « toutes »**, pas « aucune ». Le
  formulaire l'annonce : « Aucune catégorie : le budget suivra toutes les
  dépenses. »
- Formulaire incomplet : « Renseignez un nom, un montant et la plage de dates. »
  ou « Renseignez un nom et un montant. »

---

## Liste des dettes et créances

**Comment y arriver** — depuis l'onglet Modules ou le bas du tableau de bord,
toucher la carte de synthèse.

### Ce qu'on y voit

Un bandeau de synthèse, un champ **« Rechercher un tiers »**, trois filtres —
**Tout**, **Dettes**, **Créances** — portant chacun leur nombre d'entrées, puis
la liste. **Orange pour les dettes, bleu pour les créances.** Un bouton flottant
**« Nouvelle entrée »** reste visible en permanence.

### Ce qui est pris en compte

- **Dette** : ce que vous devez. **Créance** : ce qu'on vous doit.
- ⚠️ **Le montant affiché est le RESTE DÛ**, recalculé depuis l'historique des
  mouvements — **pas le montant emprunté à l'origine**. Un prêt de 100 000
  remboursé de moitié affiche 50 000.
- Le filtre s'applique localement, sans appel réseau ; la recherche, elle,
  interroge le serveur après 400 millisecondes.

### Quand il n'y a rien

- Recherche infructueuse : « Aucun résultat pour cette recherche. »
- Filtre vide : « Aucune entrée dans cette catégorie. »
- Aucune entrée du tout : un bloc « Suivez ce qu'on vous doit, et ce que vous
  devez » avec un bouton « Enregistrer la première ».

---

## Détail d'une dette ou d'une créance

**Comment y arriver** — toucher une carte dans la liste.

### Ce qu'on y voit

Titre **« Detail de la dette »** ⚠️ ou **« Detail de la créance »** ⚠️ — accent
manquant sur « Détail ».

1. Une carte colorée : **« Je dois à »** ou **« On me doit — »** ⚠️, le nom du
   tiers, un badge de statut, puis le **Reste à rembourser** ou **Reste à
   recevoir**.
2. Si un total a été engagé, une jauge : « … remboursé sur … » avec son
   pourcentage.
3. **Créée le** · **Échéance** (ou « Aucune ») · **Compte** · **Note**.
4. Deux boutons : **« J'emprunte plus »** ou **« Je prête plus »**, et
   **« Remboursement »**.
5. L'**Historique**, du plus récent au plus ancien : chaque mouvement porte une
   flèche, un montant signé, une date et sa note.

### Ce qui est pris en compte

- ⚠️ **Un remboursement ne peut pas dépasser le reste dû** : le serveur refuse
  un montant supérieur.
- La jauge n'apparaît que si un montant a été engagé.
- ⚠️ **Le bouton « Remboursement » garde ce libellé même pour une créance**, où
  il s'agit en réalité d'un encaissement. La feuille qui s'ouvre rétablit le sens
  avec « … me rembourse ».
- ⚠️ **Les champs de montant affichent « ($) » en dur** — « Montant à ajouter
  ($) », « Montant remboursé ($) » — alors que la devise réelle est celle du
  compte. Défaut d'affichage à corriger.
- La suppression efface l'entrée **et tout son historique**, définitivement.

### Quand il n'y a rien

« Aucune entrée sélectionnée. » · « Aucun mouvement enregistré. »

---

## Création d'une dette ou d'une créance

**Comment y arriver** — le bouton flottant « Nouvelle entrée », qui demande
d'abord le sens.

### Ce qu'on y voit

Titre **« Nouvelle dette »** ou **« Nouvelle créance »**. Un bandeau rappelle le
sens choisi et offre un bouton **« Changer »**.

Champs : **Créancier** (dette) ou **Débiteur** (créance) · **Montant ($)** ⚠️ ·
Compte concerné · **« Quand as-tu emprunté ? »** ou **« Quand as-tu prêté ? »** ·
Échéance de remboursement · Rappel · Description. Bouton **« Enregistrer »**.

### Ce qui est pris en compte

- **Obligatoires** : le sens, un tiers non vide, un montant strictement positif.
- Le premier compte est présélectionné ; la date est « Maintenant » ; l'échéance
  est « Aucune échéance » ; le rappel est mensuel.
- Formulaire incomplet : « Indiquez le sens, le tiers concerné et un montant. »
- ⚠️ Ici encore, le libellé du montant porte **« ($) »** quelle que soit la
  devise du compte.
