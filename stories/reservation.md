# RES - Réservation de places

En tant que client, je veux pouvoir réserver une table

## CoS

| # | CoS                                                                                                                  |
|---|----------------------------------------------------------------------------------------------------------------------|
| 1 | S'il reste de la place dans le restaurant, je peux réserver une place                                                |
| 2 | Les tables sont réservés dans leur ordre de numéro (les numéros ne sont pas forcément séquentiel)                    |
| 3 | Si le nombre de places demandé n'est pas possible avec une seule table, la/les table/s suivantes sont aussi réservés |
| 4 | Chaque réservation a un numéro unique (GUID)                                                                         |
| 5 | Le nombre minimal de personnes est de 2                                                                              |
| 6 | Il est possible d'avoir les détails d'une réservation                                                                |
| 7 | La bonne stratégie d'assignation est utilisée selon la configuration (note: MERGE n'est pas supporté pour l'instant) |

**Stratégies**

`WHOLE`

Les tables sont réservées au complet, sans en sauter. Si la réservation est pour 2 et que la prochaine table est 4, on la prend au complet

`SKIP`

On conserve l'ordre séquentiel, mais on prend la plus petite table suivante disponible qui peut accommoder 
la réservation. On commence également par la table la plus grande possible pour la réservation, tant qu'on peut
garder le groupe ensemble (il n'est pas nécessaire de minimiser le nombre de tables).

Attention: On ne peut pas séparer les groupes. 

Exemple 1: les tables disponibles ont les places suivantes : `4, 2, 4, 4`. On a une réservation pour 8, on prend 
les tables #1, #2 et #3. On ne peut pas "sauter" la table 2, afin de garder le groupe ensemble.

Exemple 2 : les tables disponibles ont les places suivantes : `4, 2, 8, 4`. On a une réservation pour 2, on prend 
la table #2. On a ensuite une réservation pour 7, alors on prend la table #3.

Exemple 3 : les tables disponibles ont les places suivantes : `4, 4, 6`. On a une réservation pour 7, on prend 
les tables #1 et #2. On ne peut pas prendre la table de 6, puisqu'on n'a pas de table suivante.

Exemple 4 : les tables disponibles ont les places suivantes : `4, 6, 4, 6, 4, 6`. On a une réservation pour 7, on prend
les tables #2 et #3. 

`MERGE`

Pas supporté pour l'instant (on fallback par défaut sur `WHOLE`)


## API - Création

**Requête**

POST /reservations

```
{
  "personnes": 4::number
  "nom": "Herménégilde"::string
}
```

**Réponse**

201 Created
Location: <url>/reservations/{numeroReservation::guid}

Contenu vide

**Exceptions**

```
{
  "message": "Message de l'erreur"::string
}
```

* Il ne reste plus de place : 400 Bad Request
* Le nombre de personnes est invalide : 400 Bad Request

## API - Obtenir

**Requête**

GET /reservations/{numeroReservation::guid}

**Réponse**

```
{
  "numeroReservation": "numero"::guid,
  "tables": []::number[]
}
```

**Exceptions**

```
{
  "message": "Message de l'erreur"::string
}
```

* Si le numéro de réservation n'existe pas: 404 Not Found
