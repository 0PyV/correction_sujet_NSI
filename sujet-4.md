# info sujet 4
ATTENTION ETRE SOLIDE EN MANIPULATION DICO ET LISTE
## Q1

faut faire gaffe au orienté objet dans fichier plante donc faut faire .croissance pour la moyenne et géré si liste vide

## Q2

attention y a un code a faire mais aussi des assert (j'ai mis en dessous un code pour montrer qu'on doit utiliser
la correspondance entre le nom de plante qui est en VALEUR dans mesures ET le nom de la plante qui est en ATTRIBUT de l'objet)
```python
def dictionnaire_mesure(plantes, mesures):
    dico={}
    for i in plantes:
        dico[i.nom]=[]
    for j in mesures:
        dico[j['plante']].append(j)
    return dico
```

## Q3

le probleme c'est qu'on modifie avec remove une liste en décalant les indices donc dès qu'on efface un élément i on saute le i+1 etc...

## Q4

on peut faire nouvelle_liste  = ma_liste.copy() pour faire une copie détachée de l'ancienne (car nouvelle_liste = ma_liste si on change l'une ca change l'autre)
le probleme c est que ca fait un peu suspect alors on peut toujours faire une liste vide et on la remplit avec une boucle 

```python
def purger_mesures_extremes(liste_mesures):
    """
    Supprime de la liste toutes les mesures dont la température 
    n'est pas comprise entre 20 et 25°C inclus.
    """
    copie=[]
    for i in liste_mesures:
        copie.append(i)
    for mesure in copie:
        if mesure['temperature'] < 20 or mesure['temperature'] > 25:
            liste_mesures.remove(mesure)

```