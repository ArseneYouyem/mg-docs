---
id: roles-et-acces
title: Rôles et accès
sidebar_position: 7
---

# Rôles et accès

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

La hiérarchie, telle que `mg-backend/src/auth/roles.guard.ts` l'ordonne :

| Rang | Rôle | Ce qu'il désigne |
|---|---|---|
| 0 | `member` | Tout utilisateur de l'application |
| 1 | `viewer` | Lecture du back-office |
| 2 | `support` | Traitement des messages de contact |
| 3 | `admin` | Administration, campagnes |
| 4 | `superadmin` | Tout, y compris la gestion des rôles |

## C'est un ordre, pas un ensemble

`hasMinRole` compare des **positions** dans ce tableau. `@MinRole(support)`
autorise donc `support`, `admin` **et** `superadmin` : tout rôle supérieur
hérite des droits inférieurs.

⚠️ Traiter les rôles comme une liste d'appartenance ferait qu'un `superadmin`
se verrait refuser une route ouverte au `support`. L'ordre est ce qui rend
l'ajout d'un rang intermédiaire sans conséquence sur l'existant.

## Le rôle est lu en base, pas dans le jeton

`JwtStrategy` charge le rôle **à chaque requête**. ⚠️ Le porter dans le jeton
aurait fait qu'un rôle retiré reste actif jusqu'à l'expiration de l'access
token — une révocation qui n'en est pas une.

## Qui accède à quoi

| Projet | Accès |
|---|---|
| `mg-mobile` | Tout utilisateur authentifié, sur **ses propres données** |
| `mg-admin` | `support` pour les messages de contact, `admin` pour les campagnes |
| `mg-vitrine` | Routes publiques uniquement — aujourd'hui `POST /contact` |

## Il n'y a pas de clé d'API pour le back-office

`mg-admin` s'authentifie comme n'importe qui : **email + code OTP**. Les rôles
décident ensuite.

⚠️ Une clé partagée aurait donné un secret unique, non révocable
individuellement, sans trace de qui a agi — et sur un back-office qui lit des
messages d'utilisateurs, l'imputabilité fait partie du produit.

⚠️ **Le premier compte doit être promu à la main en base.** Sans cela, toutes
les routes du back-office répondent 403 et personne ne peut ouvrir la porte de
l'intérieur.
