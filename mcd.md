# MCD



### Cardinalités

La cardinalité *USER has ADDRESS* devrait être à *(1,n)* car on peut créer une ou plusieurs adresses de livraison pour un utilisateur.
Un utilisateur sans adresse n'a pas lieu d'être.

La cardinalité *USER like PRODUCT* devrait être à *(0,n)* car un utilisateur n'est pas obligé de liker un produit.
À l'inverse, il doit avoir la possibilité d'en liker plusieurs.

La cardinalité *PRODUCT like USER* devrait également être à *(0,n)* car un produit pourrait être liké par aucun ou plusieurs utilisateurs.

----

### Mise en forme

###### Clés primaires

Il y a bien un identifiant pour chaque entité.
Néanmoins, les clés primaires des entités doivent se distinguer soit en les précédant d'un dièse (#), soit en les soulignant.

###### Relations

Les relations sont normalement symbolisées avec des ovales.

---

### Ajouts

J'ajouterais une propriété *quantity* dans la relation *contain* afin de gérer le cas où une commande contient plusieurs exemplaires d'un même produit.
Il faudra alors renseigner cette valeur mais elle ne peut être stockée ni dans *ORDER*, ni dans *PRODUCT* car elle est liée à la fois à un produit et une commande.

Enfin, j'ajouterais une propriété *image* dans *PRODUCT* afin de pouvoir associer une image à un mug.
S'il y a besoin de plusieurs images pour un mug, on pourra alors créer une nouvelle entité *IMAGE* avec un identifiant et une propriété *chemin* par exemple.
On pourrait ensuite créer une relation *looks like* avec les cardinalités suivantes :

```
PRODUCT (0, n) looks like (1, 1) IMAGE
```

-----

### Outils gratuits

Voici quelques outils gratuits pour réaliser des MCD.

##### AnalyseSI

https://launchpad.net/analysesi

Peut-être un peu déroutant pour le prendre en main au début mais il permet de créer assez facilement des MCD.

----

##### DBConcept

https://dbconcept.tuxfamily.org/online/index.html

Outil en ligne mais un peu particulier car on ne crée pas directement les entités et les relations mais on écrit une sorte de code source qui créera les éléments automatiquement.

----

##### Looping

https://www.looping-mcd.fr/

Cet outil est assez connu mais il ne fonctionne que sur Windows donc je n'ai pas pu le tester.