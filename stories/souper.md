# SOU - L'heure du souper

En tant que propriétaire de restaurant, je veux servir mes clients lors du souper afin de faire du ca$H.

## CoS

| # | CoS                                                                                                                               |
|---|-----------------------------------------------------------------------------------------------------------------------------------|
| 1 | Le souper se produit en 1 seule étape, où tout le monde commande et est servit en même temps                                      |
| 2 | S'il n'y a pas assez d'ingrédients pour servir tout le monde, la soirée est un échec au complet et aucun ingrédient n'est utilisé |
| 3 | S'il y a assez d'ingrédients pour servir tout le monde, les ingrédients sont retirés de la cuisine                                |
| 4 | Dans tous les cas, toutes les réservations sont considérées comme terminées (et peuvent être supprimées)                          |
| 5 | Il est possible que certaines personnes ne se présentent pas                                                                      |
| 6 | Les ingrédients restants sont conservés (on ne considère pas de date de péremption ou autre)                                      |

On commande par numéro de réservation. Pour chaque commande, on a la liste de repas. Il doit y avoir au maximum le même
nombre de repas que de personne dans la réservation. S'il y en a moins, ou si une réservation n'est pas dans la liste
des commandes, on assume que ces personnes ne se sont pas présentées.


## API

**Requête**

POST /souper

```
{
  "commandes": [
    {
      "numeroReservation": "numero"::guid,
      "repas": [1, 1, 2, 3]::number[]
    }
  ]
}
```

**Réponse**

200 OK

Contenu vide

**Exceptions**

_Rappel_: Dans tous les cas d'erreur, aucun ingrédient n'est utilisé et les réservations sont terminées.

```
{
  "message": "Message de l'erreur"::string
}
```

* Si le nombre de repas est plus grand que le nombre de personnes dans la réservation : 400 Bad Request
* Si une réservation n'existe pas : 404 Not Found
* S'il manque d'ingrédients : 400 Bad Request
