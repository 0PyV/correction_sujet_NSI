# info sujet 23

## Q1

"• les 12 bits suivants trame[16:28] encodent la température. Pour l’obtenir en °C, il faut
convertir cette valeur binaire en décimal, lui soustraire 900, puis diviser le tout par 10. Par
exemple, 010010001100 vaut 1164 en décimal, ce qui donne (1164 - 900) / 10 = 26.4 °C. Une
température inférieure à -10 °C est considérée comme une erreur de mesure ;

• les 8 bits suivants trame[28:36] encodent l’humidité en pourcentage. Attention, elle est
codée en Décimal Codé Binaire (BCD) : chaque chiffre décimal est codé séparément sur 4 bits.
Par exemple, 01100010 se sépare en 0110 (6) et 0010 (2), ce qui donne 62 %. Exception : 100%
est codé 10100000 ;"

```python

def decoder_temperature(self): #ce sont des méthodes
    temp_binaire=int(self._trame[16:28], 2)
    self._temperature = (temp_binaire - 900) / 10

def decoder_humidite(self):
    humidite_dcb = self._trame[28:36]
    self._humidite = int(humidite_dcb[:4], 2)*10 + int(humidite_dcb[4:], 2)


t = Transmission('0010101011001000010010001100011000101101')
assert t.get_temperature() == 26.4
assert t.get_humidite() == 62
```

## Q2

```python
def est_valide(self):
    blocs_trame = [self._trame[0:8], self._trame[8:16], self._trame[16:28], self._trame[28:36]] #on découpe la trame chaîne de caractères dans une liste
    bits_controle = self._trame[36:40]
    for i in range(4):
        nombre_de_1 = 0
        for bit in blocs_trame[i]:
            if bit == '1':
                nombre_de_1 += 1
        if nombre_de_1 % 2 != int(bits_controle[i]):
            return False #ici False si le reste par la division par 2  n'est pas égal au bit de contrôle correspondant (0 ou 1)
    return True # sinon ça correspond forcément
```
## Q3

encore une moyenne mais ici faut corriger le code + attention à gérer la division par 0 en mettant une condition si 0 homme / 0 femme

## Q4

On doit modifier la fonction distance et mettre en commentaire la ligne qui rajoute de la distance en fonction du sexe 