# TryHackMe — Challenge "Neighbour"

> **Catégorie :** Web Security  
> **Difficulté :** Easy  
> **Plateforme :** TryHackMe  
> **Statut :** Terminé  
> **Compétences travaillées :** reconnaissance web, inspection du code source, HTTP, contrôle d'accès, IDOR

---

## 1. Objectif du challenge

Le challenge présente une application web appelée *Authentication Anywhere*, qui permet aux utilisateurs de se connecter avec un nom d'utilisateur et un mot de passe.

L'objectif est d'examiner l'application et de déterminer si un utilisateur authentifié peut accéder aux informations d'un autre utilisateur.

L'indice principal de l'énoncé concerne les secrets présents dans les profils des utilisateurs.

## 2. Reconnaissance et exploration

### Page de connexion

La première page observée est une page de connexion contenant deux champs :

- `username`
- `password`

Le formulaire envoie les informations vers `/login.php` avec la méthode HTTP `POST`.

```html
<form action="/login.php" method="post">
    <input type="text" name="username">
    <input type="password" name="password">
</form>
```

### Inspection du code source

L'inspection du code source HTML avec `Ctrl + U` révèle un commentaire contenant des identifiants de test :

```html
<!-- use guest:guest credentials until registration is fixed -->
```

Les identifiants Guest sont donc :

- **Username :** `guest`
- **Password :** `guest`

Cette découverte illustre un problème de divulgation d'informations : les commentaires HTML sont transmis au navigateur et peuvent être consultés par les utilisateurs.

### Connexion au compte Guest

Après connexion avec les identifiants découverts, l'application donne accès au profil Guest.

L'URL observée est :

```text
/profile.php?user=guest
```

Le paramètre `user` semble indiquer quel profil l'application doit afficher.

## 3. Identification et exploitation de la vulnérabilité

### Hypothèse : IDOR

Une IDOR (*Insecure Direct Object Reference*) est une vulnérabilité de contrôle d'accès. Elle apparaît lorsqu'une application permet à un utilisateur d'accéder à une ressource en manipulant un identifiant ou un paramètre, sans vérifier correctement ses autorisations.

Dans ce challenge, le nom d'utilisateur est transmis directement dans le paramètre GET `user`.

### Test effectué

URL initiale :

```text
/profile.php?user=guest
```

En remplaçant `guest` par `admin`, l'application affiche le profil administrateur :

```text
/profile.php?user=admin
```

Le compte Guest a ainsi pu accéder au profil Admin sans disposer des autorisations nécessaires.

**Résultat :** le contrôle d'accès côté serveur est insuffisant. La modification d'un paramètre contrôlé par l'utilisateur permet d'accéder à une ressource appartenant à un autre compte.

> Le flag a été récupéré dans le cadre du challenge. Il n'est pas reproduit dans cette fiche.

## 4. Analyse des problèmes de sécurité

### A. Divulgation d'informations — Information Disclosure

Les identifiants Guest étaient présents dans un commentaire HTML.

**Risque :**
- Des informations internes ou sensibles peuvent être découvertes par les utilisateurs.
- Des identifiants exposés peuvent faciliter un accès non autorisé, notamment s'ils sont encore valides.

**Mesures correctives :**
- Ne jamais placer de mots de passe, secrets ou clés API dans le code source côté client.
- Supprimer les commentaires de développement qui exposent des informations internes.
- Utiliser une gestion sécurisée des secrets et des identifiants.
- Éviter les identifiants par défaut ou les modifier avant la mise en production.

### B. IDOR — Insecure Direct Object Reference

L'application semble utiliser directement le paramètre `user` pour sélectionner le profil à afficher, sans vérifier suffisamment les droits de l'utilisateur connecté.

**Risque :**
- Consultation de profils ou de données appartenant à d'autres utilisateurs.
- Exposition d'informations confidentielles.
- Selon les fonctionnalités disponibles, modification ou suppression non autorisée de données.

**Mesures correctives :**
- Vérifier côté serveur les autorisations à chaque requête portant sur une ressource.
- Associer les ressources à l'identité de l'utilisateur authentifié.
- Ne jamais considérer un identifiant fourni par le navigateur comme une preuve d'autorisation.
- Appliquer le principe du moindre privilège.
- Tester les contrôles d'accès avec différents rôles et comptes.

## 5. Notions techniques à retenir

| Notion | Définition / point clé |
|---|---|
| HTTP GET | Les paramètres peuvent être transmis dans l'URL, par exemple `?user=guest`. |
| HTTP POST | Les données du formulaire sont transmises dans le corps de la requête. |
| Code source HTML | Le code envoyé au navigateur est consultable côté client. |
| Information Disclosure | Exposition involontaire d'informations sensibles ou internes. |
| IDOR | Accès à une ressource sans contrôle d'autorisation approprié. |
| Authentication | Processus permettant de vérifier l'identité d'un utilisateur. |
| Authorization | Processus permettant de déterminer ce qu'un utilisateur est autorisé à consulter ou effectuer. |
| Principe du moindre privilège | Un utilisateur ne doit disposer que des permissions nécessaires à ses fonctions. |

### Authentication vs Authorization

Cette distinction est essentielle :

- **Authentication :** « Qui es-tu ? »
- **Authorization :** « Qu'as-tu le droit de faire ? »

Dans ce challenge, l'application a accepté l'authentification du compte Guest, mais n'a pas correctement limité l'accès aux profils. L'identité de l'utilisateur était connue ; ses permissions n'ont pas été correctement vérifiées.

## 6. Méthodologie utilisée

1. Examiner la page de connexion et les fonctionnalités visibles.
2. Inspecter le code source HTML à la recherche d'informations exposées.
3. Identifier les identifiants Guest fournis dans un commentaire HTML.
4. Se connecter avec le compte Guest.
5. Observer l'URL et repérer le paramètre `user`.
6. Formuler l'hypothèse d'un défaut de contrôle d'accès de type IDOR.
7. Modifier la valeur du paramètre dans le cadre du laboratoire.
8. Observer l'accès au profil Admin et récupérer le flag.

## 7. Bilan et apprentissages

Ce challenge m'a permis de mettre en pratique plusieurs notions de sécurité web :

- L'inspection du code source HTML peut révéler des informations que l'interface ne montre pas.
- Les commentaires HTML ne sont pas un emplacement sécurisé pour stocker des informations sensibles.
- Les paramètres GET transmis dans une URL peuvent révéler la manière dont une application sélectionne une ressource.
- Une authentification réussie ne garantit pas que les autorisations soient correctement appliquées.
- Les contrôles d'accès doivent être effectués côté serveur, pour chaque ressource et chaque requête.

**Point essentiel à retenir :** il ne faut jamais faire confiance à un paramètre contrôlé par l'utilisateur pour décider seul de l'accès à une ressource.
