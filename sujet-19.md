# info sujet 19

## Q1

```python
def est_en_penurie(liste_reservoirs, nom_reservoir):
    for reservoir in liste_reservoirs:
        if reservoir['nom'] == nom_reservoir: #on vérifie si c'est bien le réservoir choisi
            taux = reservoir['volume'] / reservoir['capacite'] # on calcule le taux de remplissage
            return taux < 0.2 #on renvoie un booléen True ou False
```

## Q2

"volume_par_district qui prend en paramètres
une liste de réservoirs et qui renvoie un dictionnaire ayant pour clés chaque nom différent de
district associés au volume total d’eau, en litres, disponible dans ce district."

```python
def volume_par_district(reservoirs):
    dico_districts = {}
    for reservoir in reservoirs:
        nom_district = reservoir['district']
        if nom_district in dico_districts:
            dico_districts[nom_district] += reservoir['volume']
        else:
            dico_districts[nom_district] = reservoir['volume']
    return dico_districts
```
## Q3

encore une moyenne mais ici faut corriger le code + attention à gérer la division par 0 en mettant une condition si 0 homme / 0 femme

## Q4

On doit modifier la fonction distance et mettre en commentaire la ligne qui rajoute de la distance en fonction du sexe 