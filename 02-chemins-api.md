---
id: chemins-api
title: Chemins d’API
sidebar_position: 3
---

# Chemins d’API

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

`mg-mobile/lib/shared/network/api_path.dart` est la **source** de ce catalogue.
Ce fichier en est le reflet, jamais l'inverse : **ajouter un chemin commence par
le mobile**, le backend le transcrit ensuite.

Les paramètres sont notés `:id` quelle que soit leur position réelle dans le
code Dart.

## Les 66 chemins figés

Tous sont préfixés par `/api/v1` (posé par `ApiPaths.baseUrl` côté client, par
`setGlobalPrefix` côté serveur) : le préfixe n'est jamais écrit dans un chemin.

### Authentification

- `/auth/logout`
- `/auth/me`
- `/auth/refresh-token` — ⚠️ **servie à plat**, sans enveloppe
- `/auth/request-code`
- `/auth/social`
- `/auth/verify-code`

### Identités de connexion

- `/auth/identities`
- `/auth/identities/:id`
- `/auth/identities/request-code`
- `/auth/identities/social`
- `/auth/identities/verify-code`

### Fermeture de compte

- `/auth/me/deletion`
- `/auth/me/deletion/confirm`
- `/auth/me/deletion/request-code`

### Parrainage

- `/auth/referral-code/available`
- `/auth/referral-countries`
- `/auth/referrals`

### Utilisateurs

- `/users/lookup`

### Comptes

- `/accounts`
- `/accounts/:id`
- `/accounts/:id/invitations`
- `/accounts/:id/invitations/:id/accept`
- `/accounts/:id/members`
- `/accounts/:id/members/:id`
- `/accounts/:id/members/:id/link`
- `/accounts/:id/members/:id/permissions`
- `/accounts/:id/references`
- `/accounts/:id/references/:id`

### Cotisations

- `/accounts/:id/contributions`
- `/contribution-entries/:id/collect`
- `/contribution-entries/:id/penalty`
- `/contributions/:id`
- `/contributions/:id/entries`
- `/contributions/:id/members`
- `/contributions/:id/members/:id`
- `/contributions/:id/members/:id/settle`
- `/contributions/:id/penalties`

### Catégories

- `/categories`
- `/categories/:id`

### Opérations

- `/operations`
- `/operations/:id`
- `/operations/:id/evolution`

### Budgets

- `/budgets`
- `/budgets/:id`
- `/budgets/:id/breakdown`
- `/budgets/:id/series`

### Dettes & créances

- `/debts`
- `/debts/:id`
- `/debts/:id/operations`
- `/debts/summary`

### Paiements programmés

- `/scheduled-payments`
- `/scheduled-payments/:id`
- `/scheduled-payments/:id/settle`

### Notifications

- `/notifications`
- `/notifications/:id`
- `/notifications/preferences`
- `/notifications/read-all`
- `/notifications/unread-count`

### Statistiques

- `/statistics`
- `/statistics/categories`
- `/statistics/dashboard`

### Assistant

- `/assistant/messages` — ⚠️ **flux `text/event-stream`**, pas du JSON
- `/assistant/sessions`
- `/assistant/sessions/:id`
- `/assistant/sessions/:id/messages`

### Contact

- `/contact` — publique, aucun jeton

## Ce que le backend expose en plus

Le serveur sert **78 routes** : les 66 ci-dessus, plus douze qui ne
concernent pas l'application mobile — `/campaigns/*` et `/contact/messages*`
pour le back-office, `/health` pour la supervision, et quelques routes de
lecture non encore consommées.

⚠️ **La réciproque est vérifiée : aucun chemin figé par le mobile n'est absent
du backend.** C'est le sens qui compte — une route manquante côté serveur ne se
voit qu'au moment où un utilisateur touche l'écran concerné.

## Ce que ce fichier ne dit pas

Les **méthodes HTTP** ne figurent pas ici. `api_path.dart` fige les chemins,
pas les verbes : les affirmer demanderait un audit route par route qui n'a pas
été mené. Chaque repository du mobile porte le verbe qu'il emploie, et c'est
lui qui fait foi.
