# info sujet 3

## Q1

pour bissextile mettre des if dans des if ou sinon elif attention ne pas oublier des return True ou False
```python 
def est_bissextile(n):
    if n % 400 == 0:
        return True
    elif n % 4 == 0 and n % 100 != 0:
        return True
    else:
        return False

```
(https://glassus.github.io/terminale_nsi/T6_6_Epreuve_pratique/BNS_2026/#:~:text=Sujet%204)

## Q2

refaire des if attention d'abord > ou <  puis le égal si besoin

## Q3

faire des assert  changement de mois, de jour, annee bissextile etc...

## Q4

rajouter dans while jours ecoule de fonction calendrier SI mois < 10 alors faut combler avec "0"+str(mois) pareil pour jour pour respecter format date AAAA MM JJ 