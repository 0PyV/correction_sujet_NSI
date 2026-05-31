# info sujet 10

## Q1

```python
def total_conso(donnees, jour):
    tot=0
    test = False
    for i in donnees:
        if i["jour"] == jour:
            test= True
            tot+= i["chaude"]+i['froide']
    if test == False: return None
    return tot
```
attention à bien mettre un booléen pour vérifier si on a bien une mesure présente (renvoyer si total =0 est trompeur si chaud et froid s'annule, le jour existe bien simplement que la conso vaut 0)

## Q2

```python
def fuite_possible(donnees, jour):
    suite=0
    for i in donnees:
        if i['jour'] == jour and 0 <= int(i['heure'][:2]) <= 5:
            if i['chaude']+i['froide'] != 0:
                suite+=1
                if suite >= 3: return True
            else:
                suite=0
    return False
```
Ici utilisation du slicing pour transformer l'heure en int mais on peut utiliser mesure["heure"] <= "05:00" en comparant d'après la table ASCII 

## Q3

On veut faire une moyenne sauf que dans le else on divise une somme de 3 éléments par 2 : il faut donc changer le 2 en 3

```python

def lissage_conso(valeurs):
    '''
    Calcule une moyenne glissante sur les valeurs.
    Pour chaque valeur, on calcule la moyenne avec ses voisins.
    '''

    lisse = []
    for i in range(len(valeurs)):
        if i == 0:
            m = (valeurs[i] + valeurs[i+1]) / 2
        elif i == len(valeurs)-1:
            m = (valeurs[i-1] + valeurs[i]) / 2
        else:
            m = (valeurs[i-1] + valeurs[i] + valeurs[i+1]) / 3 #ici
        
lisse.append(m)

    return lisse

```

## Q4

Vu qu'on doit renvoyer une liste qui a la même taille que celle d'origine sans erreur, on doit gérer certaines limites (modifié dans lissage_conso()):
    - liste à 2 valeurs déjà gérée
    - si liste vide: 
```python
        if len(valeurs) == 0:
        return None

```
    - si liste à 1 élément: 
```python
        if len(valeurs) == 1:
        return valeurs

```

```python
def test_lissage():
    assert lissage_conso([]) == None
    assert lissage_conso([4]) == [4]
    assert lissage_conso([4, 10, 10]) == [7, 8, 10]

 ```