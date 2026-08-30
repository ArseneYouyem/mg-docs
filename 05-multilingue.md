---
id: multilingue
title: Multilingue
sidebar_position: 6
---

# Multilingue

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

On lève des **clés**, jamais des phrases.

## La distinction qui commande tout

| Nature | Exemples | Traitement |
|---|---|---|
| **Donnée de l'utilisateur** | Libellé d'opération, note, nom de compte | Stockée **brute**, jamais traduite |
| **Texte système** | Erreur, validation, notification, catégorie par défaut | Stocké comme **clé + paramètres**, rendu à la lecture |

« Loyer » reste « Loyer » quand l'utilisateur passe en anglais. Ce n'est pas une
limite technique : c'est **sa** donnée, et la traduire la lui prendrait.

## Ce que ça impose

- Toute clé ajoutée l'est **dans les deux langues**, français et anglais.
- ⚠️ Une clé manquante **ne lève rien** : elle s'affiche telle quelle à
  l'utilisateur, qui lit `errors.account.not_found` en pleine interface. Seul un
  test de parité la détecte.
- Un message non traduisible est **remplacé** par le message générique de son
  statut : aucun texte de bibliothèque n'atteint l'utilisateur.

```ts
// ❌ La phrase est figée dans une langue
throw new NotFoundException('Ce compte est introuvable.');

// ✅ La clé est traduite au moment de répondre
throw new NotFoundException('errors.account.not_found');
```

## Les deux points de schéma qui en découlent

### `categories.system_key`

Une catégorie par défaut porte une clé (`category.food`) et pas de libellé ; son
nom est résolu à la lecture. Dès que l'utilisateur la renomme, `system_key`
passe à `null` et le nom devient sa donnée — définitivement.

### `notifications.template_key`

Une notification stocke son gabarit et ses variables, jamais sa phrase. Une
notification écrite il y a six mois s'affiche donc dans la langue d'aujourd'hui.
