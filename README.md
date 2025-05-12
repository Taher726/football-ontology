# README - Ontologie du Domaine du Football

## 🌟 Description du Projet

Cette ontologie modélise le domaine du football (soccer) en utilisant les technologies du Web Sémantique. Elle fournit une structure formelle pour représenter les joueurs, équipes, matchs, stades et autres concepts liés au football, permettant l'inférence automatique et la classification à l'aide de règles SWRL.

## 📋 Table des Matières

- [Aperçu](#aperçu)
- [Structure de l'Ontologie](#structure-de-lontologie)
- [Classes Principales](#classes-principales)
- [Propriétés](#propriétés)
- [Règles SWRL](#règles-swrl)
- [Installation](#installation)
- [Utilisation](#utilisation)
- [Exemples de Requêtes SPARQL](#exemples-de-requêtes-sparql)
- [Exemples](#exemples)
- [Licence](#licence)
- [Contact](#contact)

## 🔍 Aperçu

Cette ontologie du football a été développée pour:
- Modéliser la taxonomie des entités du football (joueurs, équipes, stades, etc.)
- Établir des relations explicites entre ces entités
- Permettre l'inférence de nouvelles connaissances à l'aide de règles
- Servir de base pour des applications analytiques dans le domaine sportif

L'ontologie est écrite en RDF/XML et utilise le langage OWL 2 pour la modélisation des classes et des propriétés, ainsi que SWRL pour les règles d'inférence.

## 🏗️ Structure de l'Ontologie

L'ontologie est organisée selon une hiérarchie de classes avec des relations spécifiques au domaine du football. Elle s'appuie sur des ontologies externes comme FOAF pour les concepts de base, tout en développant des concepts spécifiques au domaine du football.

## 📊 Classes Principales

### Personnes
- **Person**: Classe de base pour tous les individus
  - **Player**: Joueurs de football
    - **Forward**: Attaquants
      - **Striker**: Avant-centres
    - **Midfielder**: Milieux de terrain
    - **Defender**: Défenseurs
    - **Goalkeeper**: Gardiens de but
  - **Coach**: Entraîneurs
  - **Referee**: Arbitres
  - **TeamStaff**: Personnel d'équipe

### Équipes
- **Team**: Équipes de football
  - **ClubTeam**: Équipes de club
  - **NationalTeam**: Équipes nationales
  - **ProfessionalTeam**: Équipes professionnelles (avec contrainte min. 11 joueurs)

### Événements
- **Event**: Événements liés au football
  - **Match**: Matchs de football
  - **Tournament**: Tournois et compétitions
  - **Training**: Sessions d'entraînement

### Lieux
- **Place**: Emplacements pertinents pour le football
  - **Stadium**: Stades de football
    - **LargeStadium**: Stades de grande capacité (>90,000)
  - **TrainingGround**: Terrains d'entraînement

### Objets
- **FootballObject**: Objets utilisés dans le football
  - **Ball**: Ballons
  - **Goal**: Buts
  - **Card**: Cartons
    - **YellowCard**: Cartons jaunes
    - **RedCard**: Cartons rouges

## 🔗 Propriétés

### Propriétés d'Objet
- **playsFor**: Relie un joueur à son équipe
- **hasPlayer**: Relie une équipe à ses joueurs
- **homeStadium**: Stade principal d'une équipe (fonctionnelle)
- **isRivalOf**: Relation de rivalité entre équipes (symétrique)
- **participatesIn**: Équipe participant à un tournoi
- **coaches**: Relation entre entraîneur et équipe
- **playedAt**: Match joué dans un stade
- **refereesMatch**: Arbitre officiant un match
- **receivesCard**: Joueur recevant un carton

### Propriétés de Données
- **playerName**: Nom du joueur
- **playerPosition**: Position du joueur sur le terrain
- **birthDate**: Date de naissance
- **goalsScored**: Nombre de buts marqués
- **matchesPlayed**: Nombre de matchs joués
- **contractEndsIn**: Année d'expiration du contrat
- **nationality**: Nationalité
- **stadiumCapacity**: Capacité du stade
- **teamName**: Nom de l'équipe

## ⚙️ Règles SWRL

L'ontologie comprend plusieurs règles SWRL qui permettent d'inférer automatiquement de nouvelles connaissances:

### Code des Règles SWRL

1. **Règle S1**: Classifie les joueurs avec plus de 500 matchs comme `ExperiencedPlayer`
