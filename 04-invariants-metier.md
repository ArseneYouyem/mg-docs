---
id: invariants-metier
title: Invariants métier
sidebar_position: 5
---

# Invariants métier

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

Ces règles ne sont pas des préférences de style. Chacune, inversée, produit une
erreur **qui ne lève aucune exception** — elle s'affiche.

## Un solde n'est jamais stocké

Il est recalculé depuis le solde d'ouverture et les opérations.

⚠️ Une colonne dénormalisée diverge **dès la première opération modifiée ou
supprimée**. L'écart ne déclenche rien : l'utilisateur voit un solde faux, le
croit, et prend des décisions dessus. C'est la panne la plus coûteuse que cette
application puisse produire, et la plus discrète.

## Les échéances de cotisation sont dérivées

Elles se calculent depuis la périodicité et la date de départ. Seuls les
**faits** — un encaissement, une pénalité — sont des lignes en base.

⚠️ Matérialiser les échéances crée des lignes qui se désynchronisent au premier
changement de périodicité, et il faut alors décider quoi faire du passé déjà
généré. Le calcul, lui, reste juste sans intervention.

## Aucune phrase traduite n'est stockée

Soit c'est la **donnée de l'utilisateur** — intouchable —, soit c'est un
**texte système** stocké comme clé et rendu à la lecture. Jamais une phrase
figée dans une langue.

⚠️ Une phrase en base ne suit pas le changement de langue et ne se corrige que
par migration. Détail dans [`05-multilingue.md`](05-multilingue.md).

## L'appartenance se vérifie dans le `where`

`where: { id, userId }`, pas un `findUnique` suivi d'une comparaison.

⚠️ Vérifier après coup marche jusqu'au jour où un chemin d'appel oublie la
vérification. Dans le `where`, l'oubli est impossible : la requête ne rend rien.
C'est la même logique que la portée de l'assistant — une clé étrangère, pas une
intention.

## Un `where` vide ne filtre pas, il vide

⚠️ `{ OR: [] }` ou `{ in: [] }` laissé dans une clause **ne renvoie aucune
ligne**. Les fabriques de filtres rendent `{}` quand le critère est absent,
précisément pour ça. Un écran vide sans erreur est presque toujours ce piège.
