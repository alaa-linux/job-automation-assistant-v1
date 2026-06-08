
# Job Automation Assistant

## Présentation

Job Automation Assistant est une plateforme d'automatisation développée avec n8n, PostgreSQL et Docker permettant de récupérer automatiquement des offres d'emploi depuis l'API France Travail, de les filtrer selon des critères DevOps/Cloud, de les stocker dans une base PostgreSQL puis d'envoyer automatiquement les meilleures offres par email.

---

## Objectifs

* Automatiser la recherche d'offres
* Filtrer les offres pertinentes
* Éliminer les doublons
* Stocker les offres en base
* Notifier automatiquement par email
* Conserver un historique d'exécution

---

## Technologies utilisées

### Automatisation

* n8n

### Base de données

* PostgreSQL 16

### Conteneurisation

* Docker
* Docker Compose

### API

* France Travail API

### Notifications

* Gmail SMTP

---

## Architecture

```text
Schedule Trigger
        ↓
HTTP Request
        ↓
France Travail - Offres
        ↓
Suppression Doublons
        ↓
Tri Offres
        ↓
Top Offres
        ↓
Préparer Insertion SQL
        ↓
PostgreSQL : offres
        ↓
Analyse Résultats
        ↓
Structure Simplifiée
        ↓
Moteur Mots Clés
        ↓
Score Pertinence
        ↓
Send an Email
        ↓
PostgreSQL : workflow_logs
```

### Gestion des erreurs

```text
Schedule Trigger
        ↓
Email Erreur
```

---

## Structure du projet

```text
job-automation-assistant/
│
├── database/
├── docker/
├── docs/
│   └── architecture/
├── exports/
├── n8n/
│   └── workflows/
├── scripts/
└── README.md
```

---

## Installation

### Cloner le projet

```bash
git clone <repository>
cd job-automation-assistant
```

### Démarrer PostgreSQL

```bash
docker compose up -d
```

### Vérifier les conteneurs

```bash
docker ps
```

---

## Base PostgreSQL

Base :

```text
jobdb
```

Utilisateur :

```text
jobuser
```

Tables :

```text
offres
workflow_logs
```

---

## Configuration France Travail

Configurer :

* Client ID
* Client Secret
* OAuth2
* Bearer Token

Node concerné :

```text
France Travail - Offres
```

---

## Configuration Gmail

Créer un mot de passe d'application Gmail.

Configurer :

```text
smtp.gmail.com
Port 465
SSL/TLS
```

Node concerné :

```text
Send an Email
```

---

## Exécution

### Mode manuel

Exécuter depuis n8n :

```text
Execute Workflow
```

### Mode automatique

Schedule Trigger :

```text
Tous les jours à 08h00
```

---

## Fonctionnement

1. Déclenchement automatique
2. Appel API France Travail
3. Récupération des offres
4. Suppression des doublons
5. Calcul du score
6. Sélection Top Offres
7. Insertion PostgreSQL
8. Envoi email HTML
9. Enregistrement des logs

---

## Journalisation

Table :

```text
workflow_logs
```

Informations enregistrées :

* Date d'exécution
* Nombre d'offres
* Nombre d'offres retenues
* Statut
* Durée

---

## Notifications

### Succès

Email :

```text
Top offres DevOps détectées
```

### Erreur

Email :

```text
ERREUR - Workflow France Travail
```

---

## Auteur

Alaa Kaid Ahmed

Projet pédagogique DevOps / Automatisation / Data Engineering.
