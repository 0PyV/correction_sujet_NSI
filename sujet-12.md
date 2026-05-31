# info sujet 12

## Q1

Retranscrire tout en attribut

```python
def __init__(self, identifiant, nom, poids, date_arrivee):
    self.identifiant = identifiant
    self.nom = nom
    self.poids = poids
    self.date_arrivee = date_arrivee
```

## Q2

On doit respecter la contrainte d'un affichage tel que "Renard ID [id] - [Nom] (Arrivé le [date_arrivee])"

```python

    def __str__(self):
    
        return 'Renard ID '+str(self.identifiant)+' - '+self.nom+' (Arrivé le '+self.date_arrivee+')'

renard1 = Renard(200, 'Oscar', 5.1, '2026-01-01')
print(renard1)
```

## Q3

Ici, les données qu'on récupère du CSV sont par défaut en str, il faut penser à convertir le type de la variable

```python
def importer_donnees(self, nom_fichier):
    '''
    Fonction qui importe les données des renards à partir d'un fichier CSV.
    '''
    print(f"Tentative d'importation depuis {nom_fichier}...")
    with open(nom_fichier, 'r', encoding='utf-8') as f:
        lignes = csv.DictReader(f, delimiter=';')
        for ligne in lignes:
            renard = Renard(int(ligne['id']), ligne['nom'], float(ligne['poids']), ligne['date_arrivee']) #ICI rajoutez float() et int() respectivement pour poids et int
            self.recueillir(renard)

refuge1 = Refuge('SOS Goupil', '2 rue du Renard 63150 Renardville') 
refuge1.importer_donnees('donnees_renards.csv')

```

## Q4

```python
''' les deux méthodes d'analyse (mettre len() pour la longueur de laliste de peu corpulents) '''

print(len(refuge1.lister_peu_corpulents()))
print(refuge1.pourcentage_peu_corpulents())

print(len(refuge1.liste_renards))
``` 

On obtient respectivement les valeurs suivantes :
                                                - 15 peu corpulents
                                                - 50% de peu corpulents
                                                - 30 renards au total
                                                
15/30 = 50% Ainsi les méthodes sont fonctionnelles et le pourcentage est valide.
                                                   