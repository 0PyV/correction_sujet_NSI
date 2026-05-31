# info sujet 7

## Q1

creer la pop qui est une liste d'objet et ensuite une boucle qui appelle la fonction évolution()

```python
c1 = Coccinelle('femelle', 10, 2)
c2 = Coccinelle('femelle', 10, 2)
c3 = Coccinelle('male', 10, 2)
cocci = [c1, c2, c3]
proies = 200 #initialiser la pop de pucerons car la class coccinelle ne s'occupe que des coccinelles pas des pucerons
for k in range(5):
    cocci, proies = evolution(cocci, proies) #pensez à stocker ce qui va changer chaque jour donc la nouvelle pop de cocci et la nouvelle pop de proie (soit les pucerons) 
    print('jour : ', k+1)
    print('nombre de coccinelles :', len(cocci)) 
    print('nombre de proies :', proies)
    print('-------------') #pour un joli affichage 

```
ATTENTION on demande le nombre de coccinelles DONC LEN() ; NE PAS PRINT DIRECTEMENT LA LISTE

## Q2

on s'inspire de la q1 pour faire une fonction simulation sur 30 j max :

```python
def simulation_simple(population, nb_proies):
    """
    Automatise la simulation de l'écosystème sur une durée maximale de 30 jours.
    S'arrête avant si la population de coccinelles ou le nombre de pucerons tombe à 0.
    Retourne un tuple (nb_coccinelles_final, nb_pucerons_final, jours_simules).
    """
    nb_jours = 0                                # compteur de jours simulés
    for jour in range(30):                      # au maximum 30 jours
        population, nb_proies = evolution(population, nb_proies)    # on simule une journée
        nb_jours += 1                           # on incrémente le compteur de jours
        if len(population) == 0 or nb_proies == 0:  # si plus de coccinelles ou plus de pucerons... LES DEUX CONDITIONS D ARRET DEMANDEES
            break                               # ...on arrête la simulation
    return (len(population), nb_proies, nb_jours)   # on retourne le triplet (tuple)
```
Ici on peut supprimer nb_jours et renvoyer jour directement mais ATTENTION JOUR+1 CAR ON COMMENCE A 0

## Q3

la documentation : -en début de fonction
                    - entre 3 guillemets
                    -en 3 parties : - rapide résumé du but de la fonction  (à quoi ca sert?)
                                    - les entrées (types de donnees (str,int,dict,list,...) + ce que ca représente contexte de l'exo) 
                                    - les sorties (faire pareil que pour les entrées)
```python           
    def chasser(self, nb_proies, nb_coccinelles):
        """
            Simule la chasse d'une coccinelle en fonction du nmb de pucerons et du nombre de coccinelles présents.
            De plus elle permet de simuler la faim de la coccinelle

            Entrées : - self (méthode de Coccinelle)
                      - nb_proies : nombre de pucerons (int)
                      - nb_coccinelles : nombre de coccinelles (int)
            
            Sortie : - nb_proies - consomme : la population restante après consommation 

        """
        if nb_coccinelles == 0: #si aucun prédateur alors pas de proies mangées 
            return nb_proies    #donc on renvoie la même population de pucerons

        proies_par_cocci = nb_proies / nb_coccinelles # on calcule le rapport entre les proies et les prédateurs

        #dans ce bloc du code on utilise l'aléatoire (librairie random) pour renvoyer le nmb de puces mangées par coccinelle
        if proies_par_cocci > 20:
            consomme = random.randint(12, 20) #renvoie un entier entre 12 et 20 compris
        elif proies_par_cocci > 10:
            consomme = random.randint(8, 15)
        else:
            consomme = random.randint(3, 8)

        consomme = min(consomme, nb_proies) #dans le cas où on a une coccinelle qui mange 8 pucerons (random.randint(3, 8)) alors qu'il n'y en a que 3 
        #on force la consommation à ne pas dépasser la pop réelle de proie (sinon on aurait 3-8=-5 pucerons)

        if consomme >= 10: # il faut que la coccinelle mange au moins 10 pucerons pour être rassasiée
            self.niv_nutrition += 1
        else:
            self.niv_nutrition = max(0, self.niv_nutrition - 1) #sinon on diminue sa nutrition qui impacte sa survie et sa reproduction

        return nb_proies - consomme #on renvoie la nouvelle population après la consommation de la coccinelle

```
ATTENTION ICI ON SIMULE LA CHASSE D UNE COCCINELLE ET NON LA CHASSE DE TOUTE LA POPULATION

## Q4

```python  
    def reproduction(self):
        """
        Une femelle avec un niveau de nutrition >= 2 engendre exactement
        deux descendants : un mâle et une femelle.
        """
        descendants = []
        if self.sexe == "femelle" and self.niv_nutrition >= 2 and age >= 20: # on rajoute la condition qu'elle doit avoir au moins 20 jours de survie
            descendants.append(Coccinelle("male", 0, 0))
            descendants.append(Coccinelle("femelle", 0, 0))
            self.niv_nutrition = 0

        return descendants

    def a_survecu(self):
        """
        Met à jour l'âge de la coccinelle et indique si elle est encore en vie. (False = mort et True = vivant)
        """
        self.age = self.age + 1
        if self.niv_nutrition == 0: # CONDITION A RAJOUTER
            r = random.randint(1,3)
            if r == 1: #1 chance sur 3 de mourir
                return False
        return self.age < self.esperance_de_vie #rappel: l'espérance de vie est un int aléatoire qui détermine l'âge limite avant la mort en jour

```