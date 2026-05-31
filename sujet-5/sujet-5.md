# info sujet 5

## Q1

attention a pas oublier de faire une deuxieme fonction qui affiche le resultat de total_simple() et se souvenir que dans les json on a des dico

## Q2

fonction récursive pour faire le total des valeurs qui peuvent se trouver dans un dico d'un dico etc... en sachant que certaines valeurs
sont + profondes à chercher que d'autres 
ex: {'Alimentation': {'Repas': {'Viande': {'Blanche': 296, ====> on a 4 dico à parcourir pour choper le 296
     'Déchets': 152 ===> ici on a qu'à rentrer dans le grand dico et on a déchets (ALLEZ CHECKER DANS LES JSON DIRECTEMENT POUR VOIR CLAIREMENT LA PROFONDEUR)

```python 

def total_rec(empreinte):

    tot = 0
    for clé in empreinte:
        if not est_dictionnaire(empreinte[clé]): #SI LA VALEUR DE MA CLE C EST UN DICO ALORS ON DOIT ALLEZ CHERCHER + PROFONDEMENT
            tot += empreinte[clé]
        else:
            tot += total_rec(empreinte[clé]) #SI C EST PAS UN DICO ALORS FORCEMENT UNE VALEUR A RAJOUTER AU TOTAL
    return tot

```
## Q3

l'appel a faire alerte_valeur_aberrante(chargement_json('empreinte_ada.json'), 1000)
le code de base 

```python 
def alerte_valeur_aberrante(empreinte, limite):
    """
    Fonction censée déterminer si au moins une valeur du dictionnaire
    dépasse strictement la limite donnée.
    """
    for categorie, valeur in empreinte.items():
        if est_dictionnaire(valeur): #SI C EST UN DICO ON VA EN PROFONDEUR AUTREMENT DIT ON RAPPELLE LA FONCTION en checkant dans une boucle cle valeur du sous dico
            return alerte_valeur_aberrante(valeur, limite) # ERREUR CAR LE RETURN ANNULE LE PARCOURS DU GRAND DICO DES QU ON TOMBE SUR UN SOUS DICO
        else: #autrement dit on s'enfonce dans un sous dico sans terminer de vérifier l'ensemble du grand dico d'abord 
            if valeur > limite: #si la valeur abberante se trouve à la fin du grand dico elle ne sera jamais trouvée par exemple à cause d'un sous dico au début qui coupe la boucle
                return True
    return False
```

LE CORRIGE

```python 
def alerte_valeur_aberrante(empreinte, limite):
    """
    Fonction censée déterminer si au moins une valeur du dictionnaire
    dépasse strictement la limite donnée.
    """
    for categorie, valeur in empreinte.items():
        if est_dictionnaire(valeur):
            if alerte_valeur_aberrante(valeur, limite) == True: # ici on rappelle la fonction simplement en vérifiant si on a pas un True qui ressort de cet appel
                return True # # si oui alors on alerte en renvoyant True on peut stopper le programme ici
        else:
            if valeur > limite:
                return True
    return False
```

## Q4

question formulée de manière confuse mais qui est simple : on doit juste faire plusieurs test ( en assert ca peut être mieux)
exemple de la correction de dev malin
```python


# Cas 1 : dictionnaire simple, valeur AU-DESSUS du seuil → doit retourner True
# Vérifie le cas le plus simple : un seul niveau, une valeur aberrante évidente.
print(alerte_valeur_aberrante({"Transport": 1500}, 1000))   # True attendu

# Cas 2 : dictionnaire simple, toutes les valeurs EN-DESSOUS du seuil → doit retourner False
# Vérifie que la fonction ne déclenche pas d'alerte à tort.
print(alerte_valeur_aberrante({"Transport": 800}, 1000))   # False attendu

# Cas 3 : dictionnaire simple, valeur EXACTEMENT égale au seuil → doit retourner False (condition strictement supérieure)
# Vérifie la rigueur de la condition : ">" et non ">=".
print(alerte_valeur_aberrante({"Transport": 1000}, 1000))   # False attendu

# Cas 4 : dictionnaire imbriqué, valeur dans un sous-dictionnaire AU-DESSUS du seuil → doit retourner True
# C'est le cas typique qui posait problème : on vérifie que la récursion fonctionne bien.
print(alerte_valeur_aberrante({"Logement": {"Chauffage individuel": 1500}}, 1000))   # True attendu

# Cas 5 : dictionnaire imbriqué, valeur AU-DESSUS du seuil n'est PAS dans le premier sous-dictionnaire parcouru → doit retourner True
# Ce cas était particulièrement mal géré par la version buguée.
print(alerte_valeur_aberrante({"Alimentation": {"Viande": 800}, "Transport": {"Avion": 1500}}, 1000))   # True attendu

# Cas 6 : dictionnaire imbriqué, valeur dans un sous-dictionnaire EN-DESSOUS du seuil → doit retourner False
# C'est le cas typique qui posait problème : on vérifie que la récursion fonctionne bien.
print(alerte_valeur_aberrante({"Logement": {"Chauffage individuel": 800}}, 1000))   # False attendu

# Cas 7 : dictionnaire imbriqué, valeur EXACTEMENT égale au seuil → doit retourner False (condition strictement supérieure)
# Vérifie la rigueur de la condition : ">" et non ">=".
print(alerte_valeur_aberrante({"Logement": {"Chauffage individuel": 1000}}, 1000))   # False attendu

```