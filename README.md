# Exercice 1 — Conception Logicielle

## 1. Diagramme de contexte

Ce schéma montre les 3 acteurs externes qui interagissent avec DevOpsGPT, comme une carte des contacts du système.

```
+------------------+       Question        +-------------------+
|                  | --------------------> |                   |
|   Utilisateur    |                       |    DevOpsGPT      |
|                  | <-------------------- |    (système)      |
+------------------+       Réponse         +-------------------+
                                                |        |
                                    Envoi msg   |        |  Sauvegarde
                                                v        v
                                    +----------+   +----------+
                                    | API GPT-4|   | Base de  |
                                    |          |   | données  |
                                    +----------+   +----------+
```

## 2. Flowchart — Traitement d'un message

Ce schéma représente le chemin complet d'un message depuis l'envoi jusqu'à l'affichage de la réponse, avec un filtre de modération au milieu.

```
        [Réception du message utilisateur]
                       |
                       v
        [Le message contient des insultes ?]
               /                 \
             OUI                 NON
              |                   |
              v                   v
        [Refuser le         [Envoi du message
         message]            à l'API GPT-4]
                                  |
                                  v
                       [Sauvegarde de la réponse
                          en base de données]
                                  |
                                  v
                       [Affichage de la réponse
                          à l'utilisateur]
```

## 3. Dictionnaire de données — Message

Ce tableau liste tous les attributs qu'on doit stocker en base de données pour chaque message, comme une fiche d'identité obligatoire.

| Nom de la donnée | Type       | Description                                          |
|------------------|------------|------------------------------------------------------|
| `id`             | INT        | Identifiant unique du message                        |
| `contenu`        | STRING     | Le texte du message envoyé                           |
| `date_envoi`     | DATETIME   | Horodatage de l'envoi du message                     |
| `auteur`         | STRING     | Expéditeur du message (utilisateur ou IA)            |
| `session_id`     | INT        | Regroupe les messages d'une même conversation        |



# Exercice 2 — Git & Docker

## Question 1A — User Story : Abonnement Premium

En tant qu'utilisateur, je veux souscrire à un abonnement premium, afin d'accéder à des fonctionnalités avancées de DevOpsGPT sans limitations.

## Question 1B — Commandes Git

**1. Créer la branche et faire un commit :**
```bash
git checkout -b feature-premium-subscription
git add .
git commit -m "feat: ajout de l'abonnement premium"
```

**2. Fusionner sur main et créer le tag :**
```bash
git checkout main
git merge feature-premium-subscription
git tag v1.0.0
```

**3. Pousser le tag sur GitHub :**
```bash
git push origin v1.0.0
```


## Question 2 & Question 3


(Voir les fichiers de mon repo)


## Exercice 3 - Le pipeline CI/CD et sécurité/secrets


## Question 1 

(voir le fichier dans le dossier .github/workflows de mon repo)

## Question 2/A

Pour enregistrer une clé secrète de facon sécurisée, je vais sur mon repo en question (donc elyas-gitspace/examen-devops
dans mon cas, dans -> Settings -> Secrets et variables -> Actions -> New repository secret. Arrivé ici je saisi le nom
 du secret ainsi que le secret en question

## Question 2/B

Pour intégrer le le secret dans mon workflow, cela se passe au moment du CD, après avoir désigné le trigger du pipeline (ici lorsque un push avec tag est détecté dans mon repo) :
```yaml
      - name: Déploiement
        if: startsWith(github.ref, 'refs/tags/v')
        run: echo "Déploiement en cours..."
        env:
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
```



