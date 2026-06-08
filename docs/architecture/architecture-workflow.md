# Architecture — Workflow France Travail

## Schéma global

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
PostgreSQL : table offres
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
PostgreSQL : table workflow_logs
```

## Branche notification erreur

```text
Schedule Trigger
        ↓
Email Erreur
```

## Composants

* Schedule Trigger : déclenche automatiquement le workflow.
* HTTP Request : initialise le workflow.
* France Travail - Offres : interroge l’API France Travail.
* Suppression Doublons : élimine les doublons.
* Tri Offres : calcule le score des offres.
* Top Offres : conserve les meilleures offres.
* Préparer Insertion SQL : prépare les données PostgreSQL.
* PostgreSQL (offres) : stocke les offres.
* Send an Email : envoie les résultats par Gmail SMTP.
* PostgreSQL (workflow_logs) : stocke les journaux d’exécution.
* Email Erreur : envoie une notification en cas d’échec.

## Flux

1. Déclenchement automatique.
2. Appel API France Travail.
3. Suppression des doublons.
4. Calcul du score.
5. Sélection des meilleures offres.
6. Insertion dans PostgreSQL.
7. Envoi de l’email de résultats.
8. Insertion d’un log d’exécution.
9. Notification email en cas d’erreur.

## Dépendances

* Docker
* PostgreSQL
* n8n
* API France Travail
* OAuth2 France Travail
* Gmail SMTP
* Mot de passe d’application Gmail

## Validation

Document enregistré dans :

```text
docs/architecture/architecture-workflow.md
```
