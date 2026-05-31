# info sujet 9

## Q1

reproduire la formule de distance dans la fonction distance()
    √((𝑥𝐴 − 𝑥𝐵)2 + (𝑦𝐴 − 𝑦𝐵)2 + (𝑧𝐴 − 𝑧𝐵))
```python 

def distance(self, sommet):
    '''
    renvoie la distance de l'objet à sommet
    '''
    return math.sqrt((self.x-sommet.x)**2 + (self.y-sommet.y)**2 + (self.y-sommet.y)**2)
```

ATTENTION méthode déjà écrite dans le code d'origine. (erreur du sujet)

## Q2

ATTENTION Objet3D a comme attribut Faces
Faces est une liste d'objet Face
chaque objet face 

```python

    def sommets_adjacents(self, s1, s2):
        for face in self.faces:
            
            L = face.sommets #on récupère l'attribut de l'objet face
            n = len(L)
            
            for rang_sommet in range(0, n - 1): #on vérifie si s1 et s2 (ou s2 puis s1) se suivent , si oui alors adjacent
                if L[rang_sommet] == s1 and L[rang_sommet + 1] == s2:
                    return True
                if L[rang_sommet] == s2 and L[rang_sommet + 1] == s1:
                    return True
            
            # LE DERNIER SOMMET DE LA FACE (n-1) est traité ici car on doit le mettre en relation avec le premier de la boucle qui le suivant du dernier
            if (L[n - 1] == s1 and L[0] == s2) or (L[n - 1] == s2 and L[0] == s1):
                return True
                
        return False

```
## Q3

### 1.

"On dispose d’une méthode volume_cube_englobant dans la classe Objet3D qui utilise la
fonction précédente pour estimer le volume d’un objet 3D." 

### 2.

"Dans un premier temps, il faut calculer le volume d’impression de l’objet, c’est-à-dire
en multipliant le volume réel par le taux de remplissage." 

### 3.

"Dans un second temps, il faut calculer le temps d’impression en secondes. On rappelle
que le temps s’obtient en divisant le volume d’impression de l’objet par la vitesse
d’extrusion de l’imprimante. 

```python

    def estimation_impression(self, objet):
        """
        Estime le temps d'impression en secondes d'un objet 3D.
        """
        # 1.
        volume_reel = objet.volume_cube_englobant()

        #ATTENTION "l’attribut remplissage précise le taux de remplissage, flottant entre 0.0 et 1.0, du plastique lors de l’impression."
        taux = float(self.remplissage / 100) #MAIS DANS LE CODE imprimante = Imprimante3D(20, 1.2) avec 20 comme remplissage
        #pour régler l'incohérence du sujet on transforme le 20 en 0.2 pour respecter le sujet
        # 2.
        volume_impression = volume_reel * taux
        
        # 3.
        temps = volume_impression / self.vitesse_extrusion

        return temps
```
## Q4

Ici, il faut savoir que lorsqu'on crée une face, l'appel cube.ajouter_face([0, 1, 2, 3]) va piocher grâce à une liste d'indices les sommets dans la liste self.sommets
de cube pour attribuer ces sommets lors de la création de l'objet face

Ainsi self.faces contiendra des objets faces.
Cependant, si REMPLACE les sommets de self.sommets du cube, il n'y aura aucune modification sur les sommets (attributs de l'objet face) car ils se réfèrent toujours
aux ANCIENS sommets qui ne sont donc PLUS présents dans self.sommets du cube

Autrement dit, il faudrait soit recréer les faces ou bien simplement multiplier les coordonnées des sommets utilisés par les faces

```python

    def afficher(self): "PAS A MODIFIER"
        """
        Affiche l'objet 3D à l'aide de matplotlib.
        """
        fig = plt.figure()
        ax = fig.add_subplot(111, projection='3d')

        f = []
        for face in self.faces:
            x = [(s.x, s.y, s.z) for s in face.sommets] #ICI ON UTILISE LES SOMMETS DES FACES QUI NE SONT PAS MODIFIES PAR TRANSFORMER()
            f.append(x)
        mesh = Poly3DCollection(f, alpha=0.4, edgecolor='black')
        ax.add_collection3d(mesh)
        plt.show()


    def transformer_corrigé(self, rapport):
            # On modifie les attributs des objets existants sur place
            for sommet in self.sommets: #self.sommets nous renvoie sur les sommets qui sont présents parmi les attributs des objets faces
                sommet.x = sommet.x * rapport
                sommet.y = sommet.y * rapport
                sommet.z = sommet.z * rapport

    def transformer_erroné(self, rapport):
        """
        Applique une transformation d'échelle à l'objet 3D en modifiant directement ses sommets.
        """
        sommets = []
        for sommet in self.sommets:
            sommets.append(
                Sommet(sommet.x * rapport,
                       sommet.y * rapport, sommet.z * rapport))
        self.sommets = sommets

```