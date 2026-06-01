# info sujet 21

## Q1

```python
def traiter_reponse(self, succes):
    if succes: #s’il répond correctement, la carte passe au niveau supérieur (sans dépasser le niveau 4 maximum)
        self.niveau = min(4, self.niveau+1)
    else:
        self.niveau = 0 #s’il se trompe, lacarte retombe immédiatement au niveau 0, quel que soit son niveau précédent
    self.date_prochaine = date_future(DELAIS[self.niveau]) # La prochaine date de révision est ensuite calculée en ajoutant le délai du nouveau niveau à la date du jour.
```
## Q2

```python
def extraire_cartes_du_jour(paquet, date_jour):
    lst = []
    for carte in paquet:
        if carte.date_prochaine <= date_jour: #on ne garde que les cartes avec une date inférieure ou égale à celle choisie
            lst.append(carte)
    return lst
```
## Q3

```python
def extraire_cartes_a_renforcer(paquet):
    '''
    Parcourt le paquet et renvoie la liste des cartes ayant le 
    niveau d'avancement le plus faible.
    '''
    if len(paquet) == 0:
        return []

    niveau_min = paquet[0].niveau #on prend un niveau de référence, celle de la premiere carte
    a_renforcer = []

    for carte in paquet:
        if carte.niveau < niveau_min: #si on trouve une carte avec un niveau encore plus bas
            niveau_min = carte.niveau #on redéfinit le niveau le plus bas
            a_renforcer = [carte]  # ICI on change le append par la suppression de toutes les anciennes cartes
        elif carte.niveau == niveau_min: #dans le cas ou on a 2 cartes niveau 1, le code gardera les niveaux 1 dans la liste même si elle trouve des niveaux 0 après
            a_renforcer.append(carte) # on doit donc recommencer la liste des a_renforcer avec la nouvelle carte la plus bas niveau

    return a_renforcer


```