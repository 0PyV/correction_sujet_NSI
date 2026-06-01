# info sujet 2

## Q1
 
On s'aperçoit que la fonction recupere_donnees_fichier_csv(nom_fichier) renvoie :

```python 
 return altitudes, temperatures, longitudes, latitudes
 
```

on doit juste faire l'appel suivant pour stocker les quatre listes sortantes (attention à ne pas oublier les virgules)

```python 
altitudes, temperatures, longitudes, latitudes = recupere_donnees_fichier_csv('releves_ballon_sonde.csv')
```

## Q2

" La température en kelvins correspond à la température en degrés celsius à laquelle on ajoute la
valeur 273,15" : On doit donc retirer 273.15 à chaque température qu'on obtient grâce à une boucle
(le round() est indiqué sur le sujet)

```python 

def conversion_K_en_C(liste_temperatures):
    lst = []
    for temp_K in liste_temperatures:
        temp_C = round(temp_K - 273.15, 1)
        lst.append(temp_C)
    return lst

conversion_K_en_C(recupere_donnees_fichier_csv('releves_ballon_sonde.csv')[1]) #ne pas oublier de faire l'appel test, ici on ne veut que la liste temperatures donc [1]

```

## Q3

"On souhaite disposer d’une fonction nommée altitude_la_plus_froide qui prend en
paramètres une liste d’altitudes, ainsi qu’une liste des températures en degrés Celsius. Cette
fonction doit renvoyer la température la plus froide, ainsi qu’une liste contenant la ou les altitudes
correspondantes"

```python 

def altitude_la_plus_froide(liste_altitudes, liste_temperatures):
    plus_froid=float('inf')
    liste_froid = []
    for temperature_rang in range(len(liste_temperatures)):
        if plus_froid > liste_temperatures[temperature_rang] :
            plus_froid = liste_temperatures[temperature_rang] #ON PEUT DIRECTEMENT FAIRE min(liste_temperatures) au lieu de la boucle

    for altitude_rang in range(len(liste_altitudes)):
        if liste_temperatures[altitude_rang] == plus_froid : 
            liste_froid.append(liste_altitudes[altitude_rang])
    return plus_froid,liste_froid

```

ATTENTION on peut utilser la fonction min() de python mais l'examinateur vous demandera probablement de reformuler votre programme ainsi vaut-il mieux connaitre cette méthode
pour trouver la minimale

## Q4

il suffit de rajouter une insertion dans la fonction demandée au début de elle-ci

```python 
def genere_kml(liste_longitudes, liste_latitudes):
    """ Fonction qui génère un fichier de données géographiques au format standard international KML
        Ce fichier est visionnable ensuite dans différents logiciels
    """
    assert len(liste_longitudes) == len(liste_latitudes) #ICI
    fichier_kml = open( ......

```

## Q5

```python 
altitudes, temperatures, longitudes, latitudes = recupere_donnees_fichier_csv('releves_ballon_sonde.csv') #la question 1
genere_kml(longitudes, latitudes) #appel de la fonction avec les listes récupérées de la Q1
```

## Q6

On doit rajouter une balise "</kml>" , en suivant la même structure des autres balises :

```python 

def genere_kml(liste_longitudes, liste_latitudes):
    """ Fonction qui génère un fichier de données géographiques au format standard international KML
        Ce fichier est visionnable ensuite dans différents logiciels
    """
    fichier_kml = open(
        'ballon sonde.kml', 'w')    # Création et ouverture du fichier kml en mode "write"
    entete_fichier = '<?xml version="1.0" encoding="UTF-8"?>\n'
    entete_fichier += '<kml xmlns="http://www.opengis.net/kml/2.2">\n'
    entete_fichier += '<Document>\n'
    entete_fichier += '<name>Trajectoire ballon sonde</name>\n'
    # Ecriture du contenu de la variable entete_fichier dans le fichier kml
    fichier_kml.write(entete_fichier)
    for i in range(len(liste_longitudes)):
        corps_fichier = '<Placemark>\n'
        corps_fichier += f'<name>Point {i}</name>\n'
        corps_fichier += '<Point>\n'
        corps_fichier += f'<coordinates>{liste_longitudes[i]},{liste_latitudes[i]}</coordinates>\n'
        corps_fichier += '</Point>\n'
        corps_fichier += '</Placemark>\n'
        fichier_kml.write(corps_fichier)
    bas_fichier = '</Document>\n'
    bas_fichier+= '</kml>\n' #ICI, le retour à la ligne n'est pas obligatoire mais conseillé \n
    fichier_kml.write(bas_fichier)
    fichier_kml.close()                         # Fermeture du fichier kml

```