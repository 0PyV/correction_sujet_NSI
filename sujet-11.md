# info sujet 11

## Q1

math déjà import et puissance soit avec pow(,) ou avec **2

```python

def distance(habitat_1, habitat_2):
    '''
    Calcule la distance euclidienne entre deux habitats.
    entrée : 
        - habitat_1 : dictionnaire représentant un habitat.
        - habitat_2 : dictionnaire représentant un autre habitat.
    sortie : 
        - float : distance euclidienne entre habitat_1 et habitat_2.
    '''
    v1,v2 = habitat_1['vegetation'] ,habitat_2['vegetation']
    p1,p2 = habitat_1['proximite_eau'] ,habitat_2['proximite_eau']
    u1,u2 = habitat_1['densite_urbaine'] ,habitat_2['densite_urbaine']
    d1,d2 = habitat_1['disponibilite_proies'] ,habitat_2['disponibilite_proies']
    return sqrt((v1-v2)**2+(p1-p2)**2+(u1-u2)**2+(d1-d2)**2)

```

## Q2

On fait une boucle pour rajouter des tuples (dist,hab) à la liste

```python
def distance_d_un_habitat(habitat, habitats):
    '''
    Calcule la distance entre un habitat et chaque habitat de la liste.
    entrée : 
        - habitat : dictionnaire représentant un habitat.
        - habitats : liste de dictionnaires représentant des habitats.
    sortie : 
        - list[tuple] : liste de tuples (distance, habitat) où distance est la distance entre habitat et chaque habitat de la liste.
    '''
    liste=[]
    for habit in habitats:
        liste.append((distance(habit, habitat),habit))
    return liste
```

## Q3

On utilise le slicing

```python
distance_d_un_habitat(nouveau, zones_connues)[:3]
```

## Q4

```python
def presence_renard(k, habitat, habitats):
    '''
    Vérifie si l'habitat donné a plus de k/2 voisins avec des renards.
    entrée : 
        - k : entier représentant le nombre d'habitats à considérer.
        - habitat : dictionnaire représentant un habitat.
        - habitats : liste de dictionnaires représentant des habitats.
    sortie : 
        - bool : True si l'habitat a plus de k/2 voisins avec des renards, False sinon.
    '''
    habitats = k_plus_proches(k, habitat, habitats)
    n_renards = 0
    for habitat in habitats:
        distance = habitat[0]
        caracteristiques = habitat[1]
        if caracteristiques['presence_renard']: #remplacez distance['presence_renard'] par caracteristiques['presence_renard']
            n_renards += 1
    return n_renards > k/2
```

k plus proche renvoie une liste de 3 tuples (distance,habitat) qui représentent les 3 habitats voisins (les + proches) de l'habitat choisi 
dans le but d'affirmer "si il y a des renards dans au moins la moitié des habitats voisins, alors l'habitat choisi a des renards".
La correction nécessaire permet de voir la clé 'présence_renard' de l'habitat voisin stocké dans caractéristique (alors que distance est un float)