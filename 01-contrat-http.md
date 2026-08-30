---
id: contrat-http
title: Contrat HTTP
sidebar_position: 2
---

# Contrat HTTP

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

Ce contrat est **déjà consommé** par le code Dart du mobile. Chaque règle
correspond à une ligne qui casserait si on s'en écartait.

## Préfixe

Toutes les routes vivent sous `/api/v1`. Côté mobile, `ApiPaths.baseUrl` vaut
`<serveur>/api/v1` ; côté serveur, le préfixe est posé une fois dans `main.ts`.
Il n'est jamais écrit dans un chemin.

## Enveloppe

Toute réponse est enveloppée :

```json
{ "data": { "id": "…", "name": "…" } }
```

Les listes paginées ajoutent `meta`. L'enveloppe est posée par un intercepteur —
aucun contrôleur ne l'écrit à la main.

### La seule exception

`POST /auth/refresh-token` répond **à plat** :

```json
{ "access_token": "…", "refresh_token": "…" }
```

Le `TokenInterceptor` du mobile lit `response.data['access_token']` à la racine.
La route porte `@NoEnvelope()`. C'est l'unique dérogation, et elle ne se
négocie pas : l'envelopper déconnecterait toutes les applications installées à
la première expiration de jeton.

## Format d'erreur

Toute erreur, quel que soit son code, porte une clé **`message`** :

```json
{
  "statusCode": 422,
  "message": "Adresse email invalide.",
  "errors": { "email": ["Adresse email invalide."] },
  "path": "/api/v1/auth/verify-code",
  "timestamp": "2026-08-12T10:00:00.000Z"
}
```

`message` est **en français et affichable tel quel** : il arrive dans une
snackbar sans retraitement. ⚠️ Sans elle, l'utilisateur voit « Une erreur est
survenue » — le serveur a expliqué le problème, et personne ne l'a lu.

## Codes HTTP

| Code | Ce qu'il signifie | Ce que le mobile en fait |
|---|---|---|
| 400 | Requête malformée | Affiche `message` |
| 401 | **Défaut d'authentification, et rien d'autre** | Tente un refresh, puis **purge la session** |
| 403 | Droits insuffisants | Affiche `message` |
| 404 | Ressource introuvable, ou existence masquée | Affiche `message` |
| 422 | Validation métier | Affiche `message` |
| 429 | Débit dépassé | Affiche `message` |

⚠️ **Un 401 renvoyé pour un défaut de droits déconnecte l'utilisateur.** Le
mobile ne distingue pas « jeton invalide » de « accès refusé » : il tente un
refresh, échoue, et purge la session. Un manque de droits est un **403**.

⚠️ **404 plutôt que 403 quand l'existence même de la ressource est une
information.** Répondre 403 sur un compte qui ne vous appartient pas confirme
qu'il existe.

## Langue

Le français et l'anglais, portés par `Accept-Language`, avec repli sur la
préférence enregistrée puis le français. Les variantes régionales retombent sur
leur langue de base.

⚠️ **Les données de l'utilisateur ne sont jamais traduites.** Un libellé saisi
« Loyer » reste « Loyer » en anglais : c'est sa donnée, pas un texte système.
Détail dans [`05-multilingue.md`](05-multilingue.md).

## Les trois choses qui cassent les applications déjà installées

1. Changer le préfixe `/api/v1`.
2. Envelopper `POST /auth/refresh-token`.
3. Renvoyer une erreur sans clé `message`.

Une application installée ne se met pas à jour d'elle-même. Ces trois points
n'ont pas de période de transition : ils cassent le parc au moment du déploiement.
