# info sujet 16

## Q1

```python
def ecart_temperature(datas,annee):
    for i in datas:
        if i['année'] == annee:
            return i['écart']
    return None #on renvoie None si l'année n'est pas présente dans les datas

def test_ecart_temperature():
    assert ecart_temperature(datas_temperature, 2025) == 1.29
    assert ecart_temperature(datas_temperature, 2030) == None
```

## Q2

```python
print(derniere_annee_ecart_negatif(datas_temperature))
```
On doit avoir en sortie 1977
## Q3

```python
def moyenne_ecarts(annee_debut, annee_fin, datas):
    """
    Renvoie la moyenne des écarts de température pour la période comprise 
    entre annee_debut et annee_fin (incluses).
    """
    somme = 0
    compteur = 0
    for dico in datas:
        if annee_debut <= dico["année"] and dico["année"] <= annee_fin:
            somme = somme + dico["écart"] #ICI, il faut remplacer le moins par un +, sinon ca revient à inverser les écarts négatifs et positifs
            compteur += 1
    return somme / compteur
```

## Q4

```python
def graphique(datas):
    """
    Représente visuellement les warming stripes.
    """
    fig, ax = plt.subplots(figsize=(10, 2))

    # Création d'une palette de couleurs basée sur l'amplitude thermique
    cmap = plt.get_cmap("seismic")
    temperatures = [dico["écart"] for dico in datas]
    max_val = max(max(temperatures), -min(temperatures))
    norm = plt.Normalize(-max_val, max_val)

    # A COMPLETER
    # Création de la liste annees et de la liste ordonnees
    annees=[]
    ordonnees = []
    # pour les abscisses et ordonnées
    for i in datas:
        annees.append(i['année'])
        ordonnees.append(1) #ATTENTION i['écart']

    # Génération du graphique
    ax.bar(annees, ordonnees, width=1.0, color=cmap(norm(temperatures)))
    ax.set_title("Warming Stripes mondiales - Base 1901-2000")
    plt.yticks([], [])  # Masque l'axe Y car seule la couleur compte
    ax.set_xlabel("Année")

    plt.tight_layout()
    plt.show()
```

REMARQUE : la représentation des warming stripes (“bandes de réchauffement”) se doit de respecter des bandes qui vont de "haut en bas" donc
           il faut définir l'abscisse par une liste de 1 (voir 1.png)
           Cependant définir l'abscisse par une liste qui comporte l'écart de l'année montre en plus du ton de rouge/bleu les écarts des 
           températures par sa hauteur (voir i['écart'])
           il est préférable de tout de même rester sur ordonnees.append(1)