# Architecture du projet

## Architecture en trois tiers
- **Présentation (client)** : pages HTML/CSS affichées dans le navigateur (Accueil, Compétences, Projets, Parcours, Contact).
- **Applicative (serveur)** : reçoit les requêtes HTTP du navigateur, interroge la base de données et renvoie les résultats.
- **Données (SGBD)** : base de données MySQL / MariaDB qui stocke les compétences, les projets, le parcours et les messages.

## Schéma relationnel

```
COMPETENCE(id_competence, nom, domaine, niveau, origine)
PROJET(id_projet, titre, description, annee, type, image, lien_github)
UTILISER(#id_projet, #id_competence)
PARCOURS(id_parcours, categorie, titre, etablissement, date_debut, date_fin, description)
MESSAGE(id_message, nom, email, objet, contenu, date_envoi)
```

- Clés primaires : id_competence, id_projet, (id_projet, id_competence), id_parcours, id_message
- Clés étrangères : dans UTILISER, id_projet référence PROJET et id_competence référence COMPETENCE

## Rôle des tables
- **COMPETENCE** : compétences affichées sur la page Compétences (domaine pour le filtre, niveau de 1 à 5 pour le graphique, origine IUT ou hors IUT).
- **PROJET** : projets affichés sur la page Projets (année et type SAE / personnel pour les filtres).
- **UTILISER** : relie chaque projet aux compétences utilisées (relation plusieurs à plusieurs).
- **PARCOURS** : formations et expériences de la page Parcours (categorie = formation ou expérience).
- **MESSAGE** : messages envoyés depuis le formulaire de la page Contact.

## Routes prévues
| Méthode | Route | Rôle |
|---|---|---|
| GET | /competences | Lister les compétences |
| GET | /competences?domaine=web | Filtrer par domaine |
| GET | /competences/{id} | Détail d'une compétence et projets liés |
| GET | /projets | Lister les projets |
| GET | /projets?annee=2026&type=SAE | Filtrer les projets |
| GET | /projets/{id} | Détail d'un projet |
| GET | /parcours | Afficher le parcours |
| POST | /messages | Envoyer un message de contact |
