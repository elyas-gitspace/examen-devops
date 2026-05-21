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
