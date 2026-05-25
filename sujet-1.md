# Correction du Sujet 1 de NSI

Dans cet exercice, on nous demande de chercher un élément dans un tableau.

## 1. Explication de l'algorithme
Nous allons utiliser une boucle `for` pour parcourir les indices du tableau. Si l'élément est trouvé, on renvoie son indice immédiatement.

## 2. Le Code Python
Voici le script complet à exécuter :

```python
def recherche(elt, tab):
    # On parcourt le tableau de gauche à droite
    for i in range(len(tab)):
        if tab[i] == elt:
            return i # Élément trouvé !
    return -1 # L'élément n'est pas dans le tableau
