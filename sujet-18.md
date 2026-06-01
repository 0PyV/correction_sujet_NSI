# info sujet 18

## Q1

On doit faire une moyenne selon la zone choisie
Pensez à mettre la condition ==> None si aucune mesure
```python
def temperature_moyenne(zone, donnees):
    somme_temperatures = 0
    n = 0
    for d in donnees:
        if d['zone'] == zone:
            somme_temperatures += d['temperature']
            n += 1
    if n == 0:
        return None
    else:
        return somme_temperatures / n

```
## Q2
```python
def detecter_anomalies(zone, seuil, donnees):
    t = temperature_moyenne(zone, donnees) # on récupère la température de référence qui est la moyenne de la zone
    liste_dates = []
    for d in donnees:
        if d['zone'] == zone and abs(d['temperature'] - t) > seuil: #la fonction abs() est donnée dans le sujet et pensez à cibler la zone choisie
            liste_dates.append(d['date']) #si c'est une valeur aberrante on l'ajoute 
    return liste_dates
```
## Q3

```python
def test_zone_inexistante():
    '''
    Test 1 : Tester une zone qui n'existe pas

    À compléter:
    1. Appeler evolution_par_decennie avec une zone inexistante
    2. Vérifier que le résultat est un dictionnaire vide
    '''
    assert evolution_par_decennie('Tahiti', donnees_test) == {}

def test_une_seule_decennie():
    '''
    Test 2: Tester une zone avec données sur une seule décennie

    À compléter:
    1. Appeler evolution_par_decennie avec la zone appropriée
    2. Vérifier que le résultat ne contient qu'une seule décennie (2020)
    3. Vérifier la température moyenne
    '''
    assert len(evolution_par_decennie('Marquises', donnees_test)) == 1
    assert evolution_par_decennie('Marquises', donnees_test)[2020] == 26.0

def test_plusieurs_decennies():
    '''
    Test 3 : Tester une zone avec données sur plusieurs décennies

    À compléter:
    1. Appeler evolution_par_decennie avec la zone appropriée
    2. Vérifier que le résultat contient bien les clés 2010 et 2020
    3. Vérifier que les températures moyennes sont cohérentes
    '''
    resultat = evolution_par_decennie('Societe', donnees_test)
    assert 2010 in resultat and 2020 in resultat
    assert resultat[2010] == 27.0 and resultat[2020] == 28.5
```

On remarque l'assert sur plusieurs décennies ne marche car:
On s'attend à avoir {2010: 27.0, 2020: 28.5} mais on obtient {201: 27.0, 202: 28.5}

Le problème vient du calcul de la décennie

```python
 # Calcul de la décennie
decennie = (annee // 10)
```
Ici, on voit que l'année est standardisée/arrondi à l'inférieur (ex: 2019 c'est 10*201 +9 et la division euclédienne // supprime le reste 9)
Cependant, on oublie de remultiplier par 10 pour changer le 201  en 2010= 201*10

## Q4

Grâce aux observations de la Q3, on a:

```python
def evolution_par_decennie(zone, donnees):
    '''
    Calcule l'évolution des températures moyennes par décennie pour une zone.

    ATTENTION: Cette fonction contient un bug volontaire à détecter et corriger.

    Arguments:
        zone (str): Nom de l'archipel (ex: 'Societe', 'Tuamotu')
        donnees (list): Liste de dictionnaires de relevés

    Renvoie:
        dict: Dictionnaire {décennie : température_moyenne}
            ex: {2010: 27.5, 2020: 28.3}
            Renvoie un dictionnaire vide si la zone n'existe pas
    '''
    # Filtrage des relevés pour la zone
    releves_zone = [r for r in donnees if r['zone'] == zone]

    if not releves_zone:
        return {}

    # Regroupement par décennie
    temperatures_par_decennie = {}

    for releve in releves_zone:
        # Extraction de l'année de la date (format: 'YYYY-MM-DD')
        annee = int(releve['date'].split('-')[0])

        # Calcul de la décennie
        decennie = (annee // 10) * 10 #ICI RAJOUTEZ  *10 

        if decennie not in temperatures_par_decennie:
            temperatures_par_decennie[decennie] = []

        temperatures_par_decennie[decennie].append(releve['temperature'])

    # Calcul des moyennes
    moyennes = {}
    for decennie, temperatures in temperatures_par_decennie.items():
        moyennes[decennie] = round(sum(temperatures) / len(temperatures), 2)

    return moyennes
```