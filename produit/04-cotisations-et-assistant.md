---
id: produit-cotisations
title: Cotisations, assistant Leo et première ouverture
sidebar_position: 4
---

# Cotisations, assistant Leo et première ouverture

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

## Programmer une cotisation

Une **cotisation** — une tontine — est une somme demandée à chaque membre d'un
compte partagé, à une date ou à un rythme donné.

**Comment y arriver** — détail du compte → onglet Cotisations → « Programmer une
cotisation ».

### Ce qu'on y voit

1. **La cotisation** — Nom · **Montant par membre** · Description · Icône ·
   Couleur.
2. **Rythme** — ponctuelle ou récurrente.
   - Ponctuelle : une **Date d'échéance**.
   - Récurrente : **Fréquence** · **Répéter tous les** · **Première échéance** ·
     **Fin de la série** (optionnel) · **Nombre d'échéances** (optionnel).
3. **Membres concernés** — « Seuls les membres ayant rejoint le compte peuvent
   cotiser. Une invitation en attente n'est pas sélectionnable. » Un bouton
   « Choisir les participants », puis les pastilles des membres retenus.
4. **Pénalité de retard** — un interrupteur. Désactivé : « Sans pénalité, une
   échéance en retard reste simplement due. » Activé : mode de calcul (montant
   fixe ou pourcentage), valeur, **délai de tolérance en jours** (« 0 = pénalité
   dès le lendemain de l'échéance »), option **« La pénalité augmente avec le
   retard »**, et alors une fréquence de réapplication et un plafond.
   Un encadré **« Règle appliquée : »** résume la configuration en direct.
5. Le bouton **« Programmer la cotisation »**.

### Ce qui est pris en compte

- **Obligatoires** : un nom, un montant strictement positif, au moins un membre.
  Si une pénalité est activée, sa valeur doit être strictement positive.
- **Tous les membres rattachés sont présélectionnés** à l'ouverture. ⚠️ Les
  membres seulement *invités* ne sont pas proposés : ils n'ont pas encore
  rejoint le compte.
- **Ponctuelle** : une seule échéance, à la date choisie. **Récurrente** : une
  série depuis la première échéance, qui s'arrête à la fin de série ou après le
  nombre d'échéances. ⚠️ **Sans l'un ni l'autre, la série est illimitée.**
- La pénalité court après le délai de tolérance ; avec « augmente avec le
  retard », elle est réappliquée jusqu'au plafond éventuel.

### Quand il n'y a rien

- « Aucun compte sélectionné. »
- « Ce compte n'a aucun membre. Ajoutez-en depuis l'onglet "Membres". »

---

## Détail d'une cotisation

Le suivi complet : échéances, membres, pénalités.

**Comment y arriver** — toucher une cotisation dans l'onglet Cotisations d'un
compte.

### Ce qu'on y voit

Un en-tête : icône, montant par membre, rythme suivi de « • par membre », la
description, puis des badges — le statut, **« Pénalité : … »** ou **« Sans
pénalité »**, et **« Prochaine : … »**.

Puis trois onglets.

**Suivi** — six indicateurs : Membres à jour · Membres pas à jour · Total cotisé
avec sa progression · **Total de dette** (« cotisations restant dues ») ·
Pénalités encaissées · Pénalités à encaisser. Ensuite **Historique des
cotisations**, son bouton de filtre, les pastilles de filtres actifs, et la liste
des échéances.

**Membres** — le bouton « Ajouter des membres à la cotisation » si la permission
existe, puis les membres inscrits.

**Pénalités** — un filtre Membre, un filtre Statut, puis la liste.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Encaisser une échéance | Toucher l'échéance → « Encaisser » → montant → « Valider l'encaissement » | « Encaissement enregistré. » |
| Suspendre ou réactiver un membre | Toucher le membre → « Suspendre des cotisations » / « Réactiver le membre » | La génération de nouvelles échéances s'arrête ou reprend |
| Solder toutes les dettes d'un membre | Feuille du membre → « Solder toutes les dettes (montant) » | Cotisations **et** pénalités dues sont encaissées en une fois |
| Annuler une pénalité | Onglet Pénalités → « Annuler la pénalité » | La part restante est annulée |
| Voir la configuration | Menu ⋮ → « Paramètres de la cotisation » | Une feuille en lecture seule |
| Supprimer | Menu ⋮ → « Supprimer la cotisation » | Confirmation, puis suppression de la cotisation et de ses échéances |

### Ce qui est pris en compte

- Les actions sont gardées par les permissions du compte ; sinon : **« Action non
  autorisée — Vous n'avez pas la permission d'effectuer cette action sur ce
  compte. »**
- **Un encaissement peut être partiel.** Le champ est prérempli avec le reste à
  payer et ne peut pas le dépasser : au-delà, l'aperçu affiche « Le montant
  dépasse le reste à payer. »
- ⚠️ **Un encaissement partiel sert d'abord la cotisation, puis la pénalité.**
  C'est ce qui explique qu'une pénalité reste due alors qu'un versement a été
  fait.
- ⚠️ **Suspendre un membre n'efface pas ses dettes.** Le bandeau le dit :
  « Membre suspendu : aucune nouvelle cotisation ne lui est imputée. Ses dettes
  existantes restent dues. »
- ⚠️ **Une cotisation ne peut plus être supprimée dès qu'un encaissement a eu
  lieu.** La confirmation l'indique. Une suppression validée est irréversible.
- ⚠️ **Annuler une pénalité n'annule que la part restante** : ce qui a déjà été
  encaissé reste acquis, et l'annulation elle-même ne se défait pas.
- L'ajout de membres ne propose que ceux qui ne participent pas encore ; sinon :
  « Rien à ajouter — Tous les membres du compte participent déjà à cette
  cotisation. »

### Quand il n'y a rien

« Aucune cotisation sélectionnée. » · « Aucune cotisation ne correspond à ces
filtres. » · « Aucun membre inscrit à cette cotisation. » · « Aucune pénalité
appliquée pour ces filtres. » · « Ce membre est à jour. Rien à encaisser. »

---

## Conversation avec Leo

**Leo** est l'assistant de MoneyGes. Il répond aux questions, analyse les
finances de la personne qui lui parle, et **exécute des tâches pour elle**.

**Comment y arriver** — la barre d'appel en tête du tableau de bord.

### Ce qu'on y voit

- Dans la barre du haut : l'avatar de Leo, son nom, et le sous-titre **« Assistant
  MoneyGes »** ou **« en train d'écrire… »**.
- Deux icônes à droite : **Nouvelle conversation** et **Mes conversations**.
- Au premier lancement, un accueil et quatre suggestions : « Enregistre 2 500 F
  de taxi aujourd'hui », « Où est passé mon argent ce mois-ci ? », « Combien
  me reste-t-il sur mes budgets ? », « Qui me doit encore de l'argent ? ».
- Le fil, du plus ancien au plus récent.
- Le champ de saisie **« Écrivez à Leo… »** et un bouton d'envoi.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Envoyer un message | Écrire, puis toucher la flèche | Leo répond dans le fil |
| Utiliser une suggestion | La toucher | Elle part immédiatement |
| Nouvelle conversation | Icône dédiée | Le fil se vide ; **l'ancien reste dans l'historique** |
| Ouvrir l'historique | Icône dédiée | La liste des conversations s'ouvre |

### La validation avant écriture

⚠️ **C'est le point le plus important de cet écran.**

Quand Leo veut enregistrer quelque chose — une dépense, une catégorie, un
budget — **il ne le fait pas** : il le **propose**. Une carte affiche alors les
valeurs **exactement telles qu'elles partiront**, et rien n'est enregistré tant
que l'utilisateur n'a pas validé.

Refuser **n'envoie rien du tout**. Leo répond : « Très bien, je n'enregistre
rien. Dites-moi ce qu'il faut corriger. »

Un montant mal compris se corrige donc **avant** l'écriture, pas dans un relevé
où l'opération est déjà passée.

### Ce qui est pris en compte

- **Le premier message ouvre la conversation** : rien à créer au préalable.
- Leo n'agit que sur **le compte de la personne qui lui parle**. Il n'a aucun
  accès aux données de quelqu'un d'autre, et le dit simplement si on le lui
  demande.
- Pendant qu'il répond, le champ est verrouillé et le bouton d'envoi inactif. Un
  message vide ne part pas.
- Quand une écriture est confirmée, **les soldes affichés ailleurs sont
  actualisés** dans la foulée.
- ⚠️ Le message d'erreur s'affiche sous le titre **« Oups!!! »** — trois points
  d'exclamation, à revoir.

### Quand il n'y a rien, ou que ça charge

- Fil vide : l'accueil et les quatre suggestions.
- Chargement : des silhouettes de messages.
- Pendant que Leo travaille, l'écran annonce l'action en cours plutôt qu'une
  simple attente — « je regarde vos comptes… », « j'analyse vos dépenses… ».

---

## Mes conversations

**Comment y arriver** — l'icône d'historique, en haut de la conversation.

### Ce qu'on y voit

Une feuille **« Mes conversations »**, puis les fils, **du plus récent au plus
ancien** : titre, date de dernière activité — « Aujourd'hui à HH:MM », « Hier »,
« Il y a X jours », ou une date — et une icône de suppression. La conversation
ouverte est mise en évidence.

### Ce qui est pris en compte

- ⚠️ **La suppression est irréversible** : la conversation et tous ses messages
  sont effacés. Une confirmation le rappelle.
- Supprimer la conversation ouverte ramène à un fil vierge.

### Quand il n'y a rien

« Aucune conversation. Votre premier message ouvrira un fil. »

---

## Première ouverture

Cinq écrans de présentation, au tout premier lancement.

**Comment y arriver** — lancer l'application pour la première fois.

### Ce qu'on y voit

La marque au centre, le lien **« Passer »** en haut à droite, puis cinq
diapositives — capture de l'application, surtitre, icône, titre, texte — un
indicateur de progression, et le bouton **« Suivant »**, remplacé par
**« Commencer »** sur la dernière. Dessous : « Vous pourrez créer un compte ou
vous connecter à l'étape suivante. »

### Les cinq écrans

| # | Surtitre | Titre |
|---|---|---|
| 1 | Vue d'ensemble | Vos finances, d'un coup d'œil |
| 2 | Budgets | Des budgets qui préviennent |
| 3 | Tontines | Les tontines, enfin tenues |
| 4 | Parrainage | Gagnez de l'argent en recommandant MoneyGes |
| 5 | C'est parti | Commencez |

### Ce qui est pris en compte

- ⚠️ **Cette présentation ne se rejoue jamais.** « Passer » vaut l'avoir vue :
  il n'existe aucun moyen de la revoir depuis l'application.
- À la sortie, il faut **créer un compte ou se connecter** : MoneyGes ne propose
  pas de consultation sans compte.
