# Correction du Sujet 1 de NSI

## Q1

Non car le système de  tuples (répétition,valeur) peut rallonger l'écriture d'un pixel dans le cas où il n'y a pas de répétition.

Exemple : [52] ==> [1,52] 
Ici la longueur de la liste est doublée
DONC RLE EFFICACE SI REPETITION.
## Q2

```python
def decodage_rle(liste_rle):
    '''Renvoie la liste d'octets obtenue à partir de la liste liste_rle obtenue
    par compression RLE'''
    liste_octets = []              # liste résultat qu'on va reconstruire

    # On parcourt la liste RLE deux éléments par deux : (compte, valeur)
    i = 0
    while i < len(liste_rle):
        k = liste_rle[i]           # nombre de répétitions
        c = liste_rle[i + 1]       # valeur à répéter
        # on remet k fois la valeur c dans la liste résultat
        for _ in range(k):
            liste_octets.append(c)
        i += 2                     # on passe au prochain couple (compte, valeur)

    return liste_octets