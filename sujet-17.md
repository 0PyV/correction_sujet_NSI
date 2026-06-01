# info sujet 17

## Q1

Elle permet de faire la somme soit des dépenses soit des recettes
```python
def total_par_type(mouvements, type_mouvement):
    total = 0
    for mv in mouvements:
        if mv['type'] == type_mouvement:
            total += mv['montant']
    return total

def test_total():
    assert total_par_type(mouvements_test, 'dépense') == 2150.0 
    assert total_par_type(mouvements_test, 'recette') == 2300.0
    #assert total_par_type(mouvements_test, 'cotisations') == 0
    print('tests passés avec succès')
```

## Q2

```python
def test_solde_annuel():
    assert solde_annuel(mouvements_test) == 150 #CALCUL A LA MAIN 2300 - 2150 = 150
```
l'assert doit renvoyer une erreur

## Q3

```python
def solde_annuel(mouvements):
    '''
    Calcule le solde annuel en additionnant les soldes de chaque mois.
    '''
    total = 0
    # Parcourt les mois de l'année pour cumuler le bilan
    for m in range(1, 13): #ICI on doit remplacer le 12 par un 13 car le range exclut la borne de fin mais il faut ajouter les dépenses ou recettes du 12ème mois
        total = total + solde_mensuel(mouvements, m)

    return total

#ENLEVER LES HASHTAGS POUR EXECUTER LE CODE ET NON L'AVOIR EN COMMENTAIRE

mouvements_complets = lire_mouvements_depuis_csv("budget_complet.csv")
print("Le solde annuel sur le fichier complet est de :", solde_annuel(mouvements_complets))

```

