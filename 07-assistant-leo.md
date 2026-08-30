---
id: assistant-leo
title: Assistant Leo
sidebar_position: 8
---

# Assistant Leo

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

Leo existe en **deux exemplaires**, qui ne partagent ni code ni portée :

| | Leo de l'application | Leo de la vitrine |
|---|---|---|
| Interlocuteur | Utilisateur authentifié | Visiteur anonyme |
| Où il tourne | `mg-backend` | `mg-vitrine` |
| Savoir | Catalogue d'outils | Index lexical de la documentation produit |
| Peut écrire | Oui, après confirmation | Non |

Ce fichier décrit **le premier**. Le second ne parle à personne : il est entier
dans la vitrine.

## Les quatre routes

| Méthode | Route | Effet |
|---|---|---|
| GET | `/assistant/sessions` | Lister ses conversations, paginé |
| GET | `/assistant/sessions/:id/messages` | Relire un fil |
| DELETE | `/assistant/sessions/:id` | Supprimer une conversation |
| POST | `/assistant/messages` | Parler — **flux SSE** |

## Les six événements

| Événement | Ce que le client en fait |
|---|---|
| `session` | Retient l'identifiant du fil que le serveur vient d'ouvrir |
| `tool` | Annonce l'action en cours — « je regarde vos comptes… » |
| `confirmation` | Affiche l'écriture proposée et attend un accord |
| `message` | Pose la réponse et la liste des actions **menées** |
| `done` | Fin de tour |
| `error` | Message affichable |

## La garde bilatérale

C'est le point le plus important du contrat, et **le seul qui repose sur les
deux côtés à la fois**.

Un outil d'écriture n'est pas exécuté quand le modèle le demande : il est
**proposé**. Le serveur émet `confirmation` et s'arrête. Le client affiche les
valeurs **telles qu'elles partiront**, et ne renvoie le même message avec
`confirm: true` qu'après validation explicite.

⚠️ **Si un seul des deux côtés change, la garde ne casse pas : elle
disparaît.** Un serveur qui exécuterait sans attendre, ou un client qui
renverrait `confirm` d'office, enregistre une opération que personne n'a vue.
Aucune exception, aucun test rouge — l'écart se découvre au relevé.

⚠️ **Le client n'envoie jamais `confirm` par défaut.** L'omettre est la position
sûre ; le poser doit être un geste de l'utilisateur.

## Le flux se recolle

`POST /assistant/messages` répond en `text/event-stream`. Une lecture réseau
n'apporte pas des trames entières : elle peut en livrer plusieurs d'un coup, ou
**couper la dernière en deux**.

⚠️ Un client qui décode chaque morceau isolément perd des messages, au hasard
de la découpe réseau — donc rarement en développement, et régulièrement en
production. Le tampon se conserve d'une lecture à l'autre, et une trame
illisible s'ignore plutôt que d'interrompre l'échange.

## La portée est une clé étrangère

Chaque exécution d'outil reçoit le `userId` de la session et le passe aux
services, qui filtrent déjà dessus.

⚠️ Écrire « ne réponds que sur les données de l'utilisateur courant » dans le
prompt aurait confié cette limite à un système qu'on ne contrôle pas : une
phrase bien tournée dans une question suffirait à la lever. Le prompt façonne le
**comportement** — le ton, la prudence, les questions posées — jamais les droits.

## Débit

Trente échanges par heure et par personne. Chaque message déclenche plusieurs
appels au modèle — un par tour d'outil — et se paie.
