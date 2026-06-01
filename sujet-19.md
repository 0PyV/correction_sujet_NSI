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

def volume_par_district(reservoirs):
    dico={}
    for reservoir in reservoirs:
        if reservoir['district'] not in dico:
            dico[reservoir['district']] = 0 #si on connaît pas déjà le district on le rajoute au dico
        
        dico[reservoir['district']] += reservoir['volume'] #dans tous les cas on rajoute le volume au district correspondant
    return dico
```
## Q3

```python


test_meme_vol = [
    {"nom": "Nuiavai", "capacite": 100000, "volume": 50000, "district": "Tepua"},
    {"nom": "Farepape", "capacite": 120000, "volume": 50000, "district": "Fare"}
]

assert len(reservoirs) > 0 #au moins un réservoir


max_capa = 0
for reservoir in test_meme_vol: 
    if max_capa < reservoir['capacite']:  #vérifier qu’une moyenne doit être inférieure ou égale à la plus grande valeur de capacité parmi les réservoirs de la liste
        max_capa = reservoir['capacite']

assert volume_moyen(test_meme_vol) <= max_capa


assert volume_moyen(test_meme_vol) == 50000

def volume_moyen(reservoirs):
    '''
    Renvoie le volume moyen d'eau disponible dans les réservoirs.
    '''
    if len(reservoirs) == 0:
        return 0
    somme_totale = 0
    for r in reservoirs:
        somme_totale += r['volume']
    moyenne = somme_totale / len(reservoirs) #ICI on doit enlever le -1 pour diviser par le bon nombre de réservoirs
    return moyenne
```

## Q4

"À l’aide des fonctions précédentes et des fonctions liste_districts et reser-
voirs_par_district, écrire une fonction districts_vulnerables permettant
d’identifier les districts dont le volume moyen est inférieur à 80 % du volume moyen global."

```python

def districts_vulnerables(reservoirs):
    if len(reservoirs) == 0: #si aucun réservoir
        return []             
    
    moy_global = volume_moyen(reservoirs)
    seuil = 0.8 * moy_global
    
    liste_vulnerables = []
    
    dico_districts = reservoirs_par_district(reservoirs) #dico avec clé (nom du district) et valeur une liste de dico(les réservoirs)
    
    for district, les_reservoirs in dico_districts.items():# .items() permet de récupérer proprement le nom ET la liste des réservoirs
        
        moy_district = volume_moyen(les_reservoirs)
        
        if moy_district < seuil: # si inférieur au global*0.8
            liste_vulnerables.append(district) # on rajoute au vulnérable
            
    return liste_vulnerables
```