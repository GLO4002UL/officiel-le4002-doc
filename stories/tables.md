# TAB - Gestion des tables

En tant que client, je voudrais être assis avec les personnes de ma réservation

## CoS

| # | CoS                                                                                  |
|---|--------------------------------------------------------------------------------------|
| 1 | Dans le mode MERGE, on peut coller ou décoller des tables                            |
| 2 | Toutes les tables peuvent être défaites en "blocs" de 2 uniquement                   |
| 3 | Les numéros de tables restent inchangés. Une table peut être dans 2 réservation      |
| 4 | Les tables peuvent être défaites plusieurs fois au besoin.                           |
| 5 | On ne saute pas de tables (i.e. on ne fait pas comme dans SKIP)                      |
| 6 | Après le souper, les tables reviennent à leur [configuration originale](./config.md) |

Exemple, le restaurant est configuré comme suit : 3 tables de 6 (numérotées 1 à 6).

On reçoit une commande #1 pour 2. On prend la table 1 (avec 2 places). On reçoit une autre commande #2 pour 2, on prend la
table 1 (avec 2 places). On reçoit ensuite une commande #3 pour 5, on prend donc la table 1 (les 2 places restantes) +
la table 2 (avec 4 places) : 

* table 1, divisée (2 pour #1, 2 pour #2, 2 pour #3)
* table 2 (4 pour #3, 2 places restantes)
* table 3 (6 places, libre)
 
## API

Aucun changement
