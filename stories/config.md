# CGF - Configuration du restaurant

En tant que propriétaire du restaurant, je veux configurer les tables de mon restaurant.

## CoS

| # | CoS                                                                                   |
|---|---------------------------------------------------------------------------------------|
| 1 | Je peux changer les tables du restaurant                                              |
| 2 | Toutes les tables ont un nombre de places divisible par 2                             |
| 3 | Chaque table doit avoir un numéro unique, plus grand ou égal à 1                      |
| 4 | Je peux changer la stratégie d'assignation des tables (fallback par défaut sur WHOLE) |
| 5 | Chaque appel à l'API de configurate écrase la configuration actuelle (si présente)    |
| 6 | Chaque appel à l'API de configuration "reset" toutes les données                      |
| 7 | Tous les autres appels au système échouent s'il n'y a pas de configuration            |

_NOTE_: Les valeurs possible pour l'assignation sont "WHOLE", "SKIP" et "MERGE". Par contre, celles-ci seront implémentés
au fur et à mesure du projet. Si une stratégie est valide, mais non implémentée, on utilise WHOLE par défaut

## API

**Requête**

POST /configuration

```
{
  "tables": [
    {
      "numéro": 1::number
      "places": 4::number
    }
  ],
  "assignation": "WHOLE | SKIP | MERGE"::enum
}
```

**Réponse**

200 OK

Contenu vide

**Exceptions**

```
{
  "message": "Message de l'erreur"::string
}
```

* Nombre de places invalide : 400 Bad Request
* Numéro de table invalide : 400 Bad Request
* La stratégie est invalide : 400 Bad Request
* Pour tous les autres appels du système, s'il n'y a pas de configuration: 500 Server Error
