# SUB - Substitutions de repas

En tant que propriétaire, je veux éviter le plus possible les soirées échouées par manque de repas

## CoS

| # | CoS                                                                                                        |
|---|------------------------------------------------------------------------------------------------------------|
| 1 | Les repas peuvent être substitués selon les règles ci-bas                                                  |
| 2 | On doit toujours en priorité servir le repas demandé                                                       |
| 3 | Les premières commandes (dans l'ordre du POST) ont priorités                                               |
| 4 | On ne peut pas substituer une substitution                                                                 |
| 5 | Si le repas ne pas être servit ni substitué, alors on revient à un échec tel que décrit [ici](./souper.md) |

Règles (pour rappel, voir le [menu](./pre.md)) : 

1. Le repas 1 peut être substitué par le 2
2. Le repas 2 peut être substitué par le 1
3. Le repas 3 n'a pas de substitution, vu qu'il est vegan

## API

Aucun changement
