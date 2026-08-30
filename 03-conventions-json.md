---
id: conventions-json
title: Conventions JSON
sidebar_position: 4
---

# Conventions JSON

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

## Clés

Toutes les clés sont en **`snake_case`** : `created_at`, `per_page`,
`country_code`. Le mobile est en Dart, l'admin et la vitrine en TypeScript —
tous trois convertissent chez eux. Le fil est en `snake_case`, sans exception.

## Dates

**ISO 8601 UTC** : `2026-08-12T10:00:00.000Z`. `created_at` et `updated_at`
accompagnent les entités.

## Montants

Des **nombres**, jamais des chaînes formatées : `12500.5`, pas `"12 500,50 F"`.
Ni séparateur de milliers, ni symbole monétaire. ⚠️ Le formatage appartient au
client, qui seul connaît la locale d'affichage — un montant formaté par le
serveur arriverait faux dans la moitié des cas.

## Téléphone

Un numéro est **toujours un objet à trois clés**, ou `null` :

```json
{ "phone": { "country_code": "CM", "phone_code": "+237", "phone_number": "657112897" } }
```

| Clé | Contenu |
|---|---|
| `country_code` | ISO 3166-1 alpha-2, en majuscules |
| `phone_code` | Indicatif international, `+` compris |
| `phone_number` | Numéro national, sans indicatif |

⚠️ **Absence de numéro = `null`**, jamais un objet aux trois champs vides. Un
objet vide passe les vérifications de présence et casse plus loin.

## Icône

`icon` est un **chemin d'asset du client**. Le serveur ne connaît pas les assets
du mobile : il ne valide pas la valeur, il borne sa longueur et rogne les
espaces.

⚠️ **`icon` survit au renommage** — c'est la donnée de l'utilisateur. Ne pas la
confondre avec `system_key`, qui appartient au serveur et tombe à `null` dès que
l'utilisateur renomme la ressource.

## Pagination

Paramètres d'URL `page` et `per_page`. `page` commence à 1, `per_page` est
**plafonné à 100** : sans plafond, un client pourrait demander la table entière.

La réponse porte `meta` :

```json
{
  "data": [ … ],
  "meta": {
    "page": 1,
    "per_page": 20,
    "total": 57,
    "total_pages": 3,
    "has_next_page": true
  }
}
```

⚠️ **Les cinq clés sont exactement celles-là.** Un client qui lit `last_page`
n'obtient rien, retombe sur sa valeur par défaut, et conclut qu'il n'y a pas de
page suivante — sans qu'aucune erreur ne soit levée. La liste s'arrête à la
première page et personne ne le remarque avant qu'un utilisateur ne signale des
données manquantes.

## Identifiants

Des UUID, transportés en chaîne.
