# info sujet 15

## Q1

On cherche à nettoyer le numero de téléphone de tout symbole parasite comme les . () ou encore ,
```python
def normalisation_tel(num):
    clean_num = ''
    for c in num:
        if c.isdigit(): #vérifie si c'est bien un chiffre
            clean_num += c
    return clean_num #on renvoie une chaîne de caractères composée uniquement de chiffres
```

## Q2

```python
def test_validation_tel():
    '''
    Inventer des assert à partir des conditions qui constituent la fonction validation_tel()
    '''
    assert validation_tel('0612999012') == True
    assert validation_tel('0712999012') == True
    assert validation_tel('02.12.99.90.12') == False
    assert validation_tel('1612999012') == False
    assert validation_tel('12999012') == False
    assert validation_tel('0512999012') == False
    assert validation_tel('1612999012') == False
    print('Les tests de la fonction validation_tel sont passés')
```
## Q3

```python

def consultation_vaccination_chat(date):
    '''
    Renvoie les consultations de vaccination de chats dont la date
    est supérieure à la date `date`.

    :param: date: date minimale
    :return: liste [(id_animal, nom_animal, tel_proprietaire, date_consultation)]


    on selectionne l'id le nom le num de telephone et la date de la base de données animal
    on va partir de la base de données proprietaire (renommée p)
    on fusionne les deux bases de données d'après leur id (clé primaire et clé étrangère) (animal renommée a)
    on y rajoute la base de données consultation (renommée c) d'après leur id 
    Enfin on selectionne les 4 infos de la première ligne SI la date > date en argument et si c'est bien un chat pour vaccination
    on trie d'après les infos du sujet par id et par date (ordre croissant tous les deux) on peut rajouter ASC à la fin même si c'est déjà 
    dans l'ordre croissant par défaut
    '''
    conn = sqlite3.connect(DB_PATH)
    cursor = conn.cursor()
    resultat = cursor.execute(
    '''
    SELECT a.id, a.nom , telephone, c.date 
    FROM proprietaire as p
    JOIN  animal as a ON p.id = a.id_proprietaire
    JOIN  consultation as c ON c.id_animal = a.id
    WHERE c.date > ? and  a.espece = 'chat' and c.motif ='vaccination'
    ORDER BY a.id, c.date;
    ''',
        (date,),
    )
    return list(resultat)
```

ATTENTION gardez les guillemets pour que le execute() renvoie du texte
## Q4

```python
def derniere_vaccination(consultations):
    '''
    Renvoie un dictionnaire ayant pour clef l'identifiant de l'animal,
    et dont la valeur associée est la dernière consultation de cet animal.

    Chaque consultation est un tuple :

    (id_animal, nom_animal, tel_proprietaire, date_consultation)
    '''
    derniere = {}
    for consult in consultations:
        id_animal = consult[0]
        date = consult[3]
        if id_animal not in derniere:
            derniere[id_animal] = consult
        elif date > derniere[id_animal][3]: #ICI la date la plus récente est + grande cependant on avait date < derniere...
            derniere[id_animal] = consult #ce qui fait qu'on gardait toujours la date la plus ancienne au lieu de la plus récente
    return derniere
```