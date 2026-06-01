# info sujet 22

## Q1

```python
def bin2dec(tuple_binaire):
    valeur = 0
    for bit in tuple_binaire:
        valeur = valeur * 2 + bit #on calcule depuis la gauche donc on utilise pas d'exposant 2
    return valeur

# implémentation du QR Code de la figure 1:
qrcode_fig1 = ascii.figure1

sol = ''
for lst in qrcode_fig1: #on prend ligne par ligne
    sol += ascii.dict_ascii[bin2dec(lst)] #on ajoute le caractère ASCII avec le décimal
print(sol) #on a M.Hara
```
## Q2

```python
def qrcode2dec(qrcode):
    '''
    renvoie une liste d’entiers décimaux correspondant à chacune des lignes du qrcode
    parametre en entrée:
        qrcode:list de tuples
    paramètre en sortie
        liste d'entiers
    '''
    liste_resultat = []                           # On initialise une liste vide d'entiers 
    for ligne in qrcode:                        # Pour chaque ligne dans le qrcode
        liste_resultat.append(bin2dec(ligne))   # on ajoute à liste_resultat la conversion de la ligne en entier
    return liste_resultat                       # On renvoie la liste des résultats


qrcode2dec(ascii.figure1)
#on a [77, 46, 72, 97, 114, 97]
```

## Q3

```python
def dec2str(liste_dec):
    ''' entrée: liste d'entiers décimaux
        sortie: chaine de caractère formée des caractères correspondant
        de la table ascii '''
    table_ascii = ascii.dict_ascii
    chaine = ''
    for entier in liste_dec:
        if 0 <= entier <= 127: #ICI on rajoute une condition pour trier les erreurs des bons entiers
            chaine += table_ascii[entier]     # Si oui, on ajoute le caractère
        else:                                 # Sinon,
            chaine += '?'                     # On met un caractère d'erreur
    return chaine
```
## Q4

```python
def str2qrcode(message):
    '''
    Convertit une chaine de caractères en liste de tuples binaires.
    '''
    qrcode = []
    table_inverse = {valeur: cle for cle, valeur in ascii.dict_ascii.items()}

    for caractere in message:
        entier = table_inverse.get(caractere, 63)
        binaire_str = bin(entier)[2:] #pour enlever le 0b qu'on a devant chaque nmb binaire avec bin()
        if len(binaire_str) < 8:    # ICI, condition pour rajouter des éléments si on n'a pas les 8 bits
            binaire_str = '0'*(8-len(binaire_str)) + binaire_str  # ICI, ATTENTION bien compléter par la gauche et non par la droite (sinon la valeur devient + grande)
        ligne = tuple(int(bit) for bit in binaire_str) # 1010 == 0000 1010 mais != 1010 0000
        qrcode.append(ligne)
    return qrcode
```