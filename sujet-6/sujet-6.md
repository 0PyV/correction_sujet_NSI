# info sujet 6

## Q1

Une boutique est représentée par un objet qui a en attribut un dico universel de recette et sa liste perso de fruits dispo
Donc il suffit de vérifier si tous les fruits nécessaires sont présent  
(voir le readme pour la source du code)

```python

def smoothie_possible(self, nom_smoothie):
    '''Retourne True si le smoothie peut être préparé avec les fruits disponibles, False sinon.'''
    for fruit in self.db_smoothies[nom_smoothie]:
        if fruit not in self.liste_fruits_disponibles:
            return False
    return True

```
## Q2

on veut faire une liste des smoothies réalisables donc il suffit de parcourir db_smoothies et réutiliser la METHODE _possible et si ca renvoie true alors on rajoute dans une liste  

## Q3

faire différents assert avec des smoothies + ou - proches (oubliez pas de créer une boutique avec sa liste de str)
```python

def test_score_proximité():
    b = Boutique_smoothie(['Mangue', 'Ananas', 'Banane', 'Fraise'])
    assert b.score_proximité('Tropical', 'Rouge') == 0
    assert b.score_proximité('Agrume', 'Tropical citron') == 1
    assert b.score_proximité('Tropical', 'Tropical citron') == 2
    assert boutique.score_proximité('Tropical', 'Tropical') == 3

```

## Q4

On parcourt tous les smoothies , le probleme c est que le smoothie le plus proche (dans sa composition) du tropical par exemple ca sera lui-meme on doit donc sauter le smoothie sélectionné + VERIFIER QUE CEUX REALISABLES PAS TOUS
 
```python

    def plus_proche_possible(self, nom_smoothie_ref):
        """Retourne le nom du smoothie le plus proche de nom_smoothie_ref en termes de fruits communs parmi les smoothies possibles.
        En cas d'égalité, retourne le premier trouvé.
        """
        max_communs = 0
        smoothie_proche = None
        for nom_smoothie in self.db_smoothies:
            #rajoutez ce if 
            if nom_smoothie != nom_smoothie_ref and self.smoothie_possible(nom_smoothie): #si les deux smoothies sont différents et si le smoothie comparé est bien faisable
                nb_communs = self.score_proximité(nom_smoothie_ref, nom_smoothie)
                if nb_communs > max_communs:
                    max_communs = nb_communs
                    smoothie_proche = nom_smoothie
        return smoothie_proche

```

ATTENTION : le sujet indique qu'il y a un probleme alors qu'il y en a 2 (comparé le même smoothie ET vérifier si le smoothie est faisable dans la boutique)

## Q5

creer objet et afficher avec la méthode

boutique = Boutique_smoothie(['Mangue', 'Ananas', 'Banane', 'Fraise', 'Citron', 'Kiwi', 'Pomme verte'])
boutique.affichage_possibles()