---
id: produit-readme
title: Documentation produit
sidebar_position: 0
---

# Documentation produit

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

Chaque page métier de l'application mobile : ce qu'on y voit, ce qu'on peut y
faire, et **ce qui décide de ce qui s'affiche**.

## Pour qui

| Lecteur | Ce qu'il y cherche |
|---|---|
| Le **support** | Répondre à « pourquoi je ne vois pas… », « pourquoi je ne peux pas… » |
| **Leo**, l'assistant | Expliquer le fonctionnement de l'application à un utilisateur |
| Un **nouveau venu** dans l'équipe | Comprendre le produit avant d'ouvrir le code |

⚠️ **Ce n'est pas de la documentation technique.** Aucun nom de fichier, de
classe ni de route n'y figure — et ne doit y figurer. Les contrats techniques
sont à la racine de ce dépôt.

## Les pages

| Page | Ce qu'elle couvre |
|---|---|
| [Accueil et statistiques](01-accueil-et-statistiques.md) | Les quatre onglets, le tableau de bord, les deux écrans de statistiques, les notifications |
| [Opérations et catégories](02-operations-et-categories.md) | Saisie, détail, filtres, catégories, paiements programmés |
| [Comptes, budgets, dettes](03-comptes-budgets-dettes.md) | Comptes partagés et permissions, enveloppes, dettes et créances |
| [Cotisations et assistant](04-cotisations-et-assistant.md) | Tontines, pénalités, Leo et la validation avant écriture, première ouverture |
| [Connexion, profil, réglages](05-connexion-profil-reglages.md) | Code à usage unique, profil, parrainage, thème, langue, fermeture de compte |

## Le gabarit

Chaque écran suit la même structure, et **« Ce qui est pris en compte » est la
section qui compte** : c'est celle qui explique pourquoi un chiffre n'est pas
celui qu'on attendait, ou pourquoi un bouton refuse.

```
## <Nom de l'écran, tel que l'utilisateur le voit>
**Comment y arriver** — …
### Ce qu'on y voit          → les blocs, dans l'ordre d'affichage
### Ce qu'on peut y faire    → un tableau Action / Comment / Ce qui se passe
### Ce qui est pris en compte → les règles, et ce qui surprend
### Quand il n'y a rien, ou que ça charge → les messages exacts
```

## Défauts relevés en écrivant ces pages

Ils sont signalés par ⚠️ à l'endroit où ils se voient. Les principaux :

- **Des libellés anglais dans une application française** : « View Details »,
  « Saved », « Last operations », « See All », « All / Spending / Income »,
  « Scheduled payments », « Mark all as read », « Today / days ago »,
  « Active / Closed », « Add new budget », « See Details », « Save »,
  « Transaction History », « Paid », « Scan a code », « Barcode Type », « no
  Permission », « Balance ».
- **Des fautes visibles** : « Version de l'application instalée », « Detail de la
  dette », « Revenue » pour « Revenu », « Oups!!! ».
- **Le symbole `$` écrit en dur** dans les libellés de montant des dettes et
  créances, quelle que soit la devise réelle du compte.
- **Le solde global affiché dans la devise du premier compte**, sans conversion.
- **Les conditions du parrainage absentes de l'application** alors que le site
  les publie.
- **La durée de validité du code de connexion, nulle part indiquée.**

Ce sont des constats, pas des tâches : cette page les enregistre, elle ne les
corrige pas.
