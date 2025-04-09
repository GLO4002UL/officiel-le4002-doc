# PRE - Pré-commande d'ingrédients

En tant que propriétaire du restaurant, je veux pré-commander des ingrédients afin de pouvoir servir le souper

## CoS

| # | CoS                                                                                                                         |
|---|-----------------------------------------------------------------------------------------------------------------------------|
| 1 | Pour chaque personne dans une réservation, les ingrédients d'un des repas est commandé en cuisine                           |
| 2 | Le repas commandé est cyclique. Si on a 2 réservation de 2 personnes, on commande les ingrédients pour les repas 1, 2, 3, 1 |
| 3 | On assume que les ingrédients sont immédiatement disponibles en cuisine                                                     |
| 4 | Il est possible de voir l'inventaire de la cuisine                                                                          |
| 5 | Si un ingrédient n'est pas présent (on en a 0), on ne l'affiche pas dans l'inventaire                                       |
| 6 | Le menu est fixe pour le moment, mais un jour on voudrait peut-être le changer facilement                                   |

## Menu

_Note_: Les "ingrédients" sont simplifiés pour facilité le projet. Je sais qu'on ne peut pas commander "500 riz", mais c'est comme ça ici.

| Numéro du repas | Nom                         | Ingrédients                                              |
|-----------------|-----------------------------|----------------------------------------------------------|
| 1               | Poulet à l'orange-ish       | 1x poulet, 1x sauce soya, 4x orange, 500x riz            |
| 2               | Genre de steak              | 1x boeuf angus, 1x sauce au poivre, 2x patates           |
| 3               | Falafels à la sauce mystère | 3x pois chiche, 2x persil, 1x couscous, 2x sauce mystère |

## API

_Note_: L'API de réservation est inchangée.

**Requête**

GET /cuisine

```
{
  "cuisine": {
    "ingredients": [
      {
        "nom": "nom"::string,
        "quantite": 1::number
      }
    ]
  }
}
```
