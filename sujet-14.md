# info sujet 2

## Q1

On doit parcourir une liste de liste donc il est nécessaire d'utiliser une double boucle.

```python
def nb_occupants_restants(self) -> int:
    ''' renvoie le nombre d'occupants restants dans la pièce.
    '''
    nb_occ = 0
    for lst in self.grille:
        for nb in lst:
            nb_occ += nb
    return nb_occ
```

## Q2

```python
def evacuation(p: Piece, silencieux: bool = True) -> int:
    nb_tours = 0
    while p.nb_occupants_restants() > 0: # on continue l'évacuation tant qu'il reste des individus
        nb_tours += 1
        if not p.alerter(silencieux): # la condition appelle alerter() 
            print(p) # on affiche la piece si not False == True (rappel : si silencieux == False alors on print(p))
    return nb_tours
```

## Q3

En s'inspirant du code pour les sorties Nord et Ouest, on en déduit le reste:
```python
def ajouter_sortie(self, direction: str, position: int):
    ''' permet d'ajouter des sorties à la pièce.
    '''
    if direction == 'N':
        self.sorties.append((0, position))
    elif direction == 'O':
        self.sorties.append((position, 0))
    elif direction == 'S':
        self.sorties.append((self.i_max, position)) #i_max renvoie la longueur du tableau soit la dernière liste tout en bas et position est une variable 'libre'
    elif direction == 'E':
        self.sorties.append((position, self.j_max)) #j_max renvoie la longueur d'une liste du tableau soit la largeur 
```

position est un indice qui nous laisse choisir librement sur quelle colonne ou ligne on souhaite rajouter la sortie

ATTENTION PROBLEME DANS LE SUJET CERTAINES SORTIES NOTAMMENT DANS LES COINS POUR DES RAISONS DE PRIORITE DANS LA FONCTION CLIQUE_GAUCHE():
le candidat ne doit pas régler ce problème cependant éviter de mettre des sorties dans les coins devant l'examinateur ou bien il faudra expliquer 
que le code donné est par défaut erroné.

## Q4

La variable non définie à relever est 
```python
    def choix_sortie(self, i: int, j: int) -> tuple:
        """Renvoie la sortie la plus proche (distance de Manhattan) pour la case (i, j)."""
        def distance_de_manhattan(destination): 
            return abs(i - destination[0]) + abs(j - destination[1])

        assert len(self.sorties) > 0, "Aucune sortie"
        choix = self.sorties[0]
        distance_min = distance_de_manhattan(choix)  # FACULTATIF : variable renommée distance_min au lieu de distance
        for k in range(1, len(self.sorties)):
            autre_sortie = self.sorties[k]
            d2 = distance_de_manhattan(autre_sortie)  # CORRECTION : d2 était non défini donc on rajoute cette ligne pour attribuer d2 à la distance de la sortie à comparer
            if d2 < distance_min:                     # CORRECTION : condition était k < 0 ,cependant k commence à 1 d'après la boucle donc la condition
                choix = autre_sortie                  # pour trouver la meilleure sortie n'était jamais vérifiée
                distance_min = d2
        return choix
```
ATTENTION dans le nouveau sujet la fonction distance_de_manhattan() est remplacée en faisant directement le calcul dans distance = distance_de_manhattan()... 