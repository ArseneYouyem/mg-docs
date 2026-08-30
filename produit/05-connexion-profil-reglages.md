---
id: produit-reglages
title: Connexion, profil, parrainage et réglages
sidebar_position: 5
---

# Connexion, profil, parrainage et réglages

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

## Connexion

**MoneyGes n'a pas de mot de passe.** On s'identifie avec un numéro ou une
adresse, on reçoit un code, on le saisit. La première connexion crée le compte —
il n'y a pas de formulaire d'inscription séparé.

**Comment y arriver** — au lancement, ou après l'expiration d'une session.

### Ce qu'on y voit

1. Le logo et la phrase « Vos comptes, vos budgets, vos tontines. » — remplacée
   par un texte contextuel si la session a expiré.
2. Un panneau **« Se connecter »** : une bascule **Téléphone / Courriel**, le
   champ correspondant, et le bouton **« Recevoir un code »**.
3. Après l'envoi, le panneau devient **« Votre code »** : un champ à six
   chiffres, le bouton **« Continuer »**, et le lien **« Je n'ai rien reçu —
   renvoyer »**.
4. Sous le panneau, deux boutons : **Google** et **Apple**.
5. En bas : « En continuant, vous acceptez nos conditions d'utilisation et notre
   politique de confidentialité. »

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Choisir le canal | La bascule Téléphone / Courriel | Le champ change |
| Demander un code | « Recevoir un code » | Un code part par SMS/WhatsApp ou par courriel |
| Corriger l'identifiant | « Modifier », à l'étape du code | Retour à la saisie ; ⚠️ **le code déjà envoyé devient inutilisable** |
| Valider | Saisir les six chiffres, puis « Continuer » | Accès à l'application, ou complétion du profil si le compte est neuf |
| Renvoyer | « Je n'ai rien reçu — renvoyer » | Un nouveau code part au même endroit |
| Passer par Google ou Apple | Le bouton correspondant | Identité validée par le service ; **aucun code n'est demandé** |

### Ce qui est pris en compte

- Le code fait **six chiffres**. ⚠️ **Sa durée de validité n'est indiquée nulle
  part à l'écran** — une personne qui revient plus tard ne sait pas si son code
  tient encore.
- « Continuer » reste inactif tant que les six chiffres ne sont pas saisis.
- ⚠️ **Les boutons Google et Apple disparaissent** une fois le code demandé. Ils
  reviennent si l'on revient à l'étape précédente.

---

## Bienvenue — complétion du profil

Les dernières informations avant d'entrer. **Cette étape ne se saute pas.**

**Comment y arriver** — automatiquement, après une première connexion réussie.

### Ce qu'on y voit

Une barre de progression sur deux étapes, puis le panneau **« Bienvenue »** —
« Encore deux informations et votre compte est prêt. »

**Étape 1** — le champ **« Votre nom »** (absent si le nom est déjà connu, par
exemple via Google ou Apple), le champ **« Code de parrainage (facultatif) »**,
et le bouton **« Continuer »**.

**Étape 2** — **« Gagnez en recommandant »**, **« Votre code »** affiché en
grand, la note « Vous pouvez le personnaliser, tant qu'il n'est pas déjà pris. »,
un encart **Pays / Éligibilité**, et le bouton **« Entrer dans MoneyGes »**.

### Ce qui est pris en compte

- **Le nom est obligatoire** quand il est demandé : au moins deux caractères.
- **Le code de parrainage est facultatif.** Saisir le sien affiche : « Vous ne
  pouvez pas saisir votre propre code. »
- Un code personnel fait **6 à 8 caractères**, lettres majuscules et chiffres,
  sans espace ni accent.
- L'encart d'éligibilité dit si le **retrait** des gains est possible dans le
  pays du compte. ⚠️ **Sans pays renseigné, le retrait est considéré comme
  indisponible** — le parrainage reste possible, c'est le versement qui ne l'est
  pas.

---

## Paramètres

**Comment y arriver** — depuis le Menu, carte « Paramètres ».

### Ce qu'on y voit

En tête, **un bandeau rouge si une suppression de compte est programmée**, avec
son échéance et un bouton d'annulation. Puis :

| Section | Lignes |
|---|---|
| **Mon compte** | Profil · Moyens de connexion · Parrainage |
| **Préférences** | Apparence · Langue · Notifications |
| **Aide** | Nous contacter · Questions fréquentes · Partager MoneyGes |
| **Légal** | Politique de confidentialité · Conditions d'utilisation · Licences open source |
| **Zone sensible** | Se déconnecter · Supprimer mon compte |

Chaque ligne affiche sa valeur courante à droite : le nom, le nombre de moyens de
connexion, le code de parrainage, le thème, la langue.

⚠️ **C'est ici que se trouve la déconnexion** — le Menu n'en propose pas.

### Ce qui est pris en compte

- « Questions fréquentes », « Politique de confidentialité » et « Conditions
  d'utilisation » **ouvrent le navigateur** sur le site moneyges.com.
- « Partager MoneyGes » ouvre la feuille de partage du téléphone avec : « Je gère
  mon argent avec MoneyGes. Essaie : [lien] ».

---

## Profil

**Comment y arriver** — Paramètres → Profil, ou Menu → Profil.

### Ce qu'on y voit

Un en-tête avec les initiales, le nom — ou **« Profil incomplet »** — et le code
client. Puis :

- **Identité** — Nom affiché · Pays, avec « Non renseigné » à défaut et le
  sous-titre « Enregistré définitivement ».
- **Coordonnées** — Téléphone · Adresse email · Moyens de connexion, chacun
  affichant « — » s'il est vide.
- **Code client** — « Copier mon code client ».

### Ce qui est pris en compte

- **Le nom se modifie** ici, au minimum deux caractères.
- ⚠️ **Le pays est définitif.** Il ne se change plus une fois enregistré.
- ⚠️ **Le code client ne change jamais** : c'est lui que les autres saisissent ou
  scannent pour vous inviter sur un compte partagé.
- Le téléphone et l'adresse ne se modifient **pas** ici : ils viennent des
  moyens de connexion vérifiés.

---

## Parrainage

**Comment y arriver** — Paramètres → Parrainage, ou Menu → Parrainage.

### Ce qu'on y voit

1. Une grande carte colorée : **« Votre code de parrainage »**, le code en gros,
   et deux boutons **Copier** et **Partager**.
2. Un bandeau d'information **si le pays ne permet pas le retrait**.
3. **Mon code** — la ligne « Personnaliser mon code ».
4. **Mes filleuls (n)** — la liste : nom et date d'inscription.

### Ce qu'on peut y faire

| Action | Comment | Ce qui se passe |
|---|---|---|
| Copier | Bouton « Copier » | Le code part dans le presse-papiers |
| Partager | Bouton « Partager » | « Rejoins-moi sur MoneyGes pour gérer ton argent. Utilise mon code de parrainage [code] à l'inscription : [lien] » |
| Personnaliser | « Personnaliser mon code » | Un champ de 6 à 8 caractères, avec vérification de disponibilité pendant la frappe |

### Ce qui est pris en compte

- La disponibilité s'affiche en direct : « Ce code est disponible. », « Ce code
  est déjà pris. », « Disponibilité non vérifiée. »
- Le parrain touche **10 % de chaque paiement de ses filleuls pendant 6 mois** ;
  le filleul obtient **l'accès gratuit aux fonctionnalités premium**.
- ⚠️ **Ces conditions ne sont écrites nulle part dans l'application.** Le site
  moneyges.com les détaille, l'écran de parrainage non : quelqu'un qui partage
  son code ne sait pas ce qu'il gagne. À corriger.
- Le pays inéligible n'empêche pas de parrainer — il empêche de **retirer**.
- Les filleuls n'apparaissent qu'avec leur nom et leur date d'inscription.

### Quand il n'y a rien

« **Personne pour l'instant** — Partagez votre code : chaque inscription avec ce
code apparaîtra ici. »

---

## Apparence

**Comment y arriver** — Paramètres → Apparence.

Trois cartes : **Automatique**, **Clair**, **Sombre**, sous la phrase
« Choisissez l'aspect de l'application. Le réglage est retenu sur cet appareil. »

### Ce qui est pris en compte

- Le choix s'applique **immédiatement**, sans redémarrage, et reste sur
  l'appareil.
- En **Automatique**, l'écran indique le thème effectif : « Actuellement :
  clair » ou « Actuellement : sombre ».
- Le thème se bascule aussi d'un geste depuis la barre du haut, partout dans
  l'application.

---

## Langue

**Comment y arriver** — Paramètres → Langue.

Trois options : **Automatique**, **Français**, **English**.

### Ce qui est pris en compte

⚠️ **Ce réglage ne traduit pas l'interface.** L'écran le dit lui-même :

> « L'interface de l'application reste en français pour l'instant : ce réglage
> change la langue des messages et des données servis par le serveur (erreurs,
> catégories par défaut, notifications). »

C'est la première source de confusion sur cet écran : choisir « English » ne
change rien à ce qui est écrit sur les boutons.

- Le choix s'applique immédiatement et reste sur l'appareil ; il est aussi
  transmis au compte, pour les notifications reçues hors de l'application.
- **Automatique** ramène la langue du téléphone à l'une des deux langues
  servies : un téléphone en espagnol obtient le français.

---

## Supprimer mon compte

Un parcours en trois étapes, avec un **délai de rétractation**.

**Comment y arriver** — Paramètres → Zone sensible → Supprimer mon compte.

### Les trois étapes

**1 — Explication.** Un texte, cinq points — l'envoi d'un code, le délai,
l'archivage, le sort des comptes partagés, la possibilité de recommencer — et un
encart d'avertissement. Puis le bouton **« Recevoir le code de suppression »**.

**2 — Code.** Un champ à six chiffres, un rappel du délai, les boutons
**« Confirmer la suppression »** et **« Annuler »**.

**3 — Suppression en cours.** La date d'archivage, le temps restant, et le bouton
**« Annuler la suppression »**.

### Ce qui est pris en compte

- ⚠️ **La suppression n'est pas immédiate : 48 heures de rétractation.** Pendant
  ce délai, le compte fonctionne normalement, un bandeau apparaît sur le tableau
  de bord et dans les réglages, et l'annulation ne demande **aucun code**.
- ⚠️ **Passé le délai, l'accès est définitivement perdu.**
- ⚠️ **Les opérations des comptes partagés ne sont pas effacées** : elles restent
  visibles pour les autres membres. C'est voulu — effacer sa part trouerait la
  comptabilité de tout le monde.
- Le numéro et l'adresse sont **libérés** après archivage : les réutiliser crée un
  **nouveau** compte, sans aucun lien avec l'ancien.
- ⚠️ **Un compte qui n'a que Google ou Apple ne peut pas recevoir le code.**
  L'écran invite alors à ajouter d'abord un numéro ou une adresse.
- Si une suppression est déjà programmée, l'écran s'ouvre directement à l'étape 3.

---

## Écrans non encore documentés

Deux écrans des réglages restent à couvrir dans une prochaine passe :
**Moyens de connexion** (ajouter, vérifier ou retirer un téléphone, une adresse,
un compte Google ou Apple), **Notifications** (les préférences), et **Nous
contacter**.
