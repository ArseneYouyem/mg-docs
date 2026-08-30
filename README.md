---
id: readme
title: Documentation partagée MoneyGes
sidebar_position: 1
---

# Documentation partagée MoneyGes

> ## ⛔ Règle ultime — sens unique
>
> **Cette documentation ne se modifie que depuis `mg-backend`.**
>
> `mg-mobile`, `mg-admin` et `mg-vitrine` la reçoivent en **lecture seule** : ils
> mettent à jour le pointeur du sous-module, jamais son contenu. Une correction
> écrite depuis un projet client part dans un commit que le prochain
> `git submodule update` écrase sans un mot — le travail est perdu et la
> divergence revient.
>
> Un écart constaté depuis un projet client se **signale**, il ne se corrige pas
> sur place.

Les contrats, invariants et conventions qui **lient** les quatre projets
MoneyGes. Rien d'autre.

## Ce qu'il ne contient pas

La documentation propre à un projet reste chez lui : les controllers GetX du
mobile, les modules NestJS du backend, les composants Next.js de l'admin et de
la vitrine. Les rapatrier ici gonflerait le contexte de chaque agent sans rien
apprendre à personne — un développeur Flutter n'a que faire des files BullMQ.

La frontière est simple : **ce fichier a-t-il deux projets qui en dépendent ?**
Si non, il n'a rien à faire ici.

## Contenu

| Fichier | Ce qu'il fige |
|---|---|
| [`01-contrat-http.md`](01-contrat-http.md) | Enveloppe, format d'erreur, codes HTTP, langue |
| [`02-chemins-api.md`](02-chemins-api.md) | Les 66 chemins figés par le mobile |
| [`03-conventions-json.md`](03-conventions-json.md) | Clés, dates, montants, téléphone, icône, pagination |
| [`04-invariants-metier.md`](04-invariants-metier.md) | Les règles qui cassent silencieusement quand on les inverse |
| [`05-multilingue.md`](05-multilingue.md) | Clés plutôt que phrases, et les deux points de schéma |
| [`06-roles-et-acces.md`](06-roles-et-acces.md) | La hiérarchie des rôles et qui accède à quoi |
| [`07-assistant-leo.md`](07-assistant-leo.md) | Routes, événements SSE, et la garde bilatérale |
| [`08-carte-des-liens.md`](08-carte-des-liens.md) | Qui appelle qui, et ce qui casse |
| [`produit/`](produit/README.md) | **La documentation produit** — chaque écran de l'application mobile, pour le support et pour Leo |

## Montage dans un projet

```bash
git submodule add https://github.com/ArseneYouyem/mg-docs.git docs/shared
git commit -m "Rattacher la documentation partagée"
```

Et pour récupérer un projet qui en porte un :

```bash
git clone --recurse-submodules <url-du-projet>
```

## Deux propriétaires, et un seul par dossier

| Dossier | Qui l'écrit | Pourquoi |
|---|---|---|
| La racine — contrats techniques | **`mg-backend`** | C'est lui qui sert l'API que les trois autres consomment |
| **`produit/`** | **`mg-mobile`** | L'interface décrite y vit ; la documenter ailleurs garantirait qu'elle prenne du retard |

Partout ailleurs, la règle est le sens unique : on lit, on signale, on ne
corrige pas sur place.

⚠️ **`produit/` ne contient aucun terme technique** — ni fichier, ni classe, ni
route. Il est écrit pour le support et pour l'assistant, qui n'ouvriront jamais
le code. Les contrats techniques restent à la racine, et ne doivent pas se
mélanger : un assistant public qui indexerait la racine restituerait la
structure de la base et les noms de variables d'environnement à un visiteur
anonyme.

## Mise à jour

Depuis `mg-backend` pour la racine, depuis `mg-mobile` pour `produit/` : modifier, commiter, pousser dans
`mg-shared-docs`. Puis, dans chaque projet client :

```bash
git submodule update --remote docs/shared
git add docs/shared && git commit -m "Suivre la documentation partagée"
```

Le pointeur part **dans le commit du code** qui en dépend. C'est ce qui rend la
mise à jour atomique côté projet : un commit référence une version précise du
contrat.

## Les deux pièges

⚠️ **`git clone` sans `--recurse-submodules` laisse `docs/shared/` vide**, sans
un mot. L'agent ou le développeur qui arrive conclut « pas de documentation » et
écrit la sienne — exactement le contraire du but. Posez
`git config --global submodule.recurse true` une fois pour toutes.

⚠️ **Un sous-module se cloné en `detached HEAD`.** Un commit écrit là n'est sur
aucune branche : le prochain `git submodule update` l'écrase et le travail
disparaît. C'est la raison mécanique de la règle ultime en tête de ce fichier.
