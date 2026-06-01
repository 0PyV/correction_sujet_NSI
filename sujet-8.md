# info sujet 8

## Q1

```python
def calcul_recettes():
    recette = 0
    for k in range(1000): #on répète pour les 1000 resto
        for j in range(500): # 500 menus par jour
            recette += 2.27 + 5.19 + 1.81 # un menu c'est entrée + plat + dessert
    return recette
``` 
On obtient 4634999.999986519 au lieu de 4635000 car arrondi de la représentation d'un nombre à virgule en binaire
rappel binaire pour flottant : 

1 en décimal est égal à 1 en binaire.

On multiplie le reste par 2.

On note la partie entière obtenue (0 ou 1), qui sera notre prochain bit binaire.

On ne garde que la nouvelle partie fractionnaire pour l'étape suivante.

0.81×2=1.62→ On note 1

0.62×2=1.24→ On note 1

0.24×2=0.48→ On note 0

0.48×2=0.96→ On note 0

0.96×2=1.92→ On note 1 ...... (on a pour l'instant 1. 11001...)

ON NE VA JAMAIS TOMBER SUR 1.00 donc arrondi qui s'accumule ==> différence entre le 4634999 ET LE 4635000

## Q2

en gardant à l'esprit que  (['0001', '0011', '0101', '0110']) == 13.56 ( ne pas oublier l'assert)

```python
def convertir_BCD_vers_decimal(liste_quartets):
    nombre=""
    for quartet in liste_quartets:
        nombre+=str(int(quartet,2)) #int("1101",2) transforme le binaire en base 2
    part_deci=nombre[-2:] #on commence à prendre à partir de l'avant dernier
    part_ent=nombre[:-2] #commence au début et on arrête de prendre à l'avant dernier
    
    return float(part_ent +"."+ part_deci) # ca fait float("13"+"."+"56") 13.56
    
``` 
 
## Q3

```python

def additionner_nombres_format_BCD(a, b):
    """
    Additionne deux nombres au format BCD, quartet par quartet.
    """
    liste_quartets1 = convertir_dec_vers_BCD(a)
    liste_quartets2 = convertir_dec_vers_BCD(b)

    # Ajustement de la longueur
    liste_quartets1, liste_quartets2 = aligner_quartets(
        liste_quartets1, liste_quartets2)

    retenue = 0
    resultat = []
    longueur_max = max(len(liste_quartets1), len(liste_quartets2))

    for i in range(longueur_max):
        index = longueur_max - i - 1

        # Addition binaire simple des quartets
        somme, retenue = additionner_binaire_quartets(
            liste_quartets1[index], liste_quartets2[index], retenue)

        somme, retenue = corriger_BCD(somme, retenue) #juste après l'addition, on corrige si besoin pour respecter le format BCD
        resultat.insert(0, somme)

    # Gestion de la dernière retenue éventuelle
    if retenue == 1:
        resultat.insert(0, '0001')

    return resultat
```
## Q4

on rajoute des quartets vide ( = 0 ) pour corriger le décalage 
```python

def aligner_quartets(q1: list, q2: list) -> tuple:
    """
    Doit équilibrer les deux listes en ajoutant des '0000' à gauche 
    de la liste la plus courte.
    """
    if len(q1) > len(q2):
        diff= len(q1)-len(q2)
        q2 = ['0000']*diff + q2
    elif len(q2) > len(q1):
        diff= len(q2)-len(q1)
        q1 = ['0000']*diff + q1
    return q1,q2


```