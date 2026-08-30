---
id: carte-des-liens
title: Carte des liens
sidebar_position: 9
---

# Carte des liens

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

Qui appelle qui, dans quel sens, et **ce qui casse** quand le contrat bouge.

```
┌──────────────┐   HTTP /api/v1    ┌──────────────┐    Prisma     ┌──────────┐
│  mg-mobile   │──────────────────▶│              │──────────────▶│ Supabase │
│  (Flutter)   │◀──────────────────│  mg-backend  │               │ Postgres │
└──────────────┘   { data } JSON   │   (NestJS)   │               └──────────┘
┌──────────────┐                   │              │
│   mg-admin   │──────────────────▶│   78 routes  │
│   (Next.js)  │   authentifié     │              │
└──────────────┘                   │              │
┌──────────────┐                   │              │
│  mg-vitrine  │──────────────────▶│              │
│   (Next.js)  │   POST /contact   └──────────────┘
└──────────────┘
```

## Les liens

| Depuis | Vers | Contrat | Ce qui casse |
|---|---|---|---|
| `mg-mobile` | `mg-backend` | 66 chemins figés par `api_path.dart`, préfixe `/api/v1`, enveloppe `{data}`, `Accept-Language` | Les applications **déjà installées**, qui ne se mettent pas à jour d'elles-mêmes |
| `mg-mobile` | `mg-backend` | `POST /assistant/messages`, flux SSE, garde de confirmation | Une écriture comptable que personne n'a validée — silencieusement |
| `mg-vitrine` | `mg-backend` | `POST /contact`, publique | Le formulaire de contact ne dépose plus rien ; le visiteur croit avoir écrit |
| `mg-admin` | `mg-backend` | `/contact/messages*`, rôle `support` minimum | La boîte de réception se ferme ; les messages arrivent en base et personne ne les lit |
| `mg-admin` | `mg-backend` | `/campaigns/*`, rôle `admin` minimum | — |
| `mg-backend` | Supabase | Deux URL distinctes, voir ci-dessous | Migrations bloquées sans message |

## Le sens du contrat, et il surprend

`mg-mobile` **n'est pas** un consommateur passif de l'API : c'est sa
**spécification**. `api_path.dart` fige les chemins, `lib/data/models/` fixe le
nom et le type de chaque clé JSON, et `lib/data/fake/` en donne une
implémentation de référence exécutable.

Devant un doute sur un comportement du backend, **on lit la fake API du mobile
avant d'inventer une règle**.

⚠️ Vérifié au moment d'écrire ce fichier : **aucun des 66 chemins figés par le
mobile n'est absent du backend**. Le serveur en expose douze de plus, réservés
au back-office et à la supervision.

## Les deux URL de la base

| Variable | Point d'entrée | Port | Qui l'utilise |
|---|---|---|---|
| `DATABASE_URL` | Transaction pooler | 6543 | L'application, à l'exécution |
| `DIRECT_URL` | **Session pooler** | 5432 | Le CLI Prisma, pour les migrations |

⚠️ `DIRECT_URL` pointe sur le **Session pooler**, pas sur la « Direct connection
string » du tableau de bord : `db.<ref>.supabase.co` ne résout qu'en IPv6 sur
les projets récents, et `prisma migrate` reste alors bloqué **sans message
d'erreur**. C'est une attente infinie, pas un échec.

⚠️ Depuis Prisma 7, le champ `url` de `prisma.config.ts` reçoit **`DIRECT_URL`**
— son nom prête à confusion.
