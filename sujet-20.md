# info sujet 20

## Q1

```python
def calculer_empreinte(utilisateur):
    empreinte = 0
    for activite in utilisateur:
        empreinte += EMISSIONS[activite] * utilisateur[activite] #on multiplie la pollution/unité * le nombre d'unité 
    return empreinte

assert calculer_empreinte(utilisateur1) == 7490
```
## Q2

On doit classer en 3 niveaux les activités d'un utilisateur (envoyer un email serait dans faible mais si l'utilisateur envoie beaucoup d'emails
alors cette activité peut passer dans fort)

```python
def classer_par_impact(utilisateur):
    dict_impact = {'fort': [], 'moyen': [], 'faible': []}
    for activite in utilisateur: #on peut recopier la boucle de la Q1
        emissions = EMISSIONS[activite] * utilisateur[activite]
        if emissions >= 1000: #on vérifie dans quelle catégorie on doit placer l'activité
            dict_impact['fort'].append(activite)
        elif emissions >= 200:
            dict_impact['moyen'].append(activite)
        else:
            dict_impact['faible'].append(activite)
    return dict_impact

assert classer_par_impact(utilisateur2) == {'fort': ['streaming_hd'],
                                            'moyen': ['emails_simples'],
                                            'faible': ['recherches']}
```

## Q3

```python
def test_comparer():
    diff = comparer(utilisateur4, utilisateur5)
    assert diff['emails_simples'] == -200  # (50-100) * 4
    assert diff['recherches'] == 350     # (100-50) * 7

    # Ajouter vos tests ci-dessous avec justifications
    assert diff['streaming_hd'] == 0  # activité absente chez les deux utilisateurs
    diff = comparer(utilisateur2, utilisateur4)
    assert diff['streaming_hd'] == -500  # (0-5) * 100; activité absente chez un utilisateur
```
## Q4
```python
def comparer_v2(u1, u2):
    '''Compare les émissions de deux utilisateurs pour toutes les activités.
    Renvoie un dictionnaire avec, pour chaque activité, l'écart des émissions
    sous forme de pourcentage, en proportion de la première émission.'''
    ecarts = {}
    for activite in EMISSIONS:
        quantite1 = 0
        quantite2 = 0
        if activite in u1:
            quantite1 = u1[activite]
        if activite in u2:
            quantite2 = u2[activite]
        emission1 = quantite1 * EMISSIONS[activite]
        emission2 = quantite2 * EMISSIONS[activite]
        if emission1 == 0: #ICI, on doit s'apercevoir que la fonction retourne une erreur lorsqu'on divise par 0 (= pas d'activité de l'utilisateur)
            ecarts[activite] = None # on peut alors renvoyer None pour éviter la division par 0
        else:
            ecarts[activite] = (emission2 - emission1)/emission1 * 100
    return ecarts
```