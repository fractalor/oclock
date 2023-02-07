# Feedback sur le parcours S06



### #2 Lister tous les profs

##### TeachersController

Attention aux noms des variables.
Par exemple *$teachers**d**Model* dans la fonction *teachers* de *TeachersController*.

Il y a également un souci avec ce morceau de code, le *teachers* est en trop :

```php
$teachersModel = new Teachers
       teachers();
```

Attention également aux noms des méthodes dans les routes.
Par exemple, la méthode *products* n'existe pas dans *TeachersController*.
Un mauvais copier-coller du projet oShop ?

Dans certaines pages, l'appel à la route *teachers_update* ne peut pas fonctionner car la route se nomme en fait *teachers_edit*.

Mises à part ces erreurs de nommage, le listing des professeurs est bon.

-----

### #3 Lister tous les étudiants

Attention aux noms des controllers.
Tu appelles parfois le controller *StudentController* et parfois *Student**s**Controller*.

Comme pour les professeurs, il y a un souci avec ce morceau de code, le *students* est en trop :

```php
$studentsModel = new Students
        students();
```

Attention également aux minuscules et aux majuscules.
Tu as par exemple nommé l'une de tes routes ***S**tudents_update* mais tu l'appelles ensuite en la nommant *students_update*, ce qui ne fonctionnera pas car les noms des routes sont sensibles à la casse.

Mises à part ces erreurs de nommage, le listing des étudiants est bon.

-----

### #4 Ajout d'un prof

Pour cette partie, il y a plusieurs choses à revoir.

Tout d'abord, la page *teachers_add.tpl.php* ne permettra pas de réaliser un ajout car il semblerait qu'il s'agisse d'un copier-coller de la page de listing des professeurs.

De plus, d'après les consignes, il est nécessaire de séparer les traitements GET et POST de cette page.
Il te faudrait donc, dans ton controller, créer une fonction permettant de gérer l'affichage de la page d'ajout et qui soit indépendante de la fonction de traitement des données du formulaire.

----

### #5 Ajout d'un étudiant

Attention lors de la création d'une nouvelle instance de la classe *Students* à bien utiliser le bon nom de classe.

Dans la page *students_add.tpl.php*, tu essayes d'y afficher les valeurs d'un étudiant.
Or, aucun étudiant ne sera passé en paramètre dans cette page, ce qui risque de provoquer des erreurs.

Attention aux noms des labels, ils ne correspondent pas toujours à l'input correspondant ou sont parfois incompréhensibles.

Attention également aux noms des tables dans les requêtes SQL. La table est parfois appelée *student* et parfois *student**s***.

Enfin, attention à la valeur de *status*. 
Il s'agit d'un entier donc il faut restreindre la saisie de cette valeur à des nombres entiers afin d'éviter les erreurs lors de l'ajout en base de données.

-----

### #6 Restreindre l'accès aux utilisateurs

Encore des soucis avec le nommage des éléments.

L'appel de *show("user/login")* ne fonctionnera pas car la page est stockée dans le dossier *appuser* et non *user*.
Le mieux pour éviter ce genre de problème est de garder le même nom pour le modèle, la vue et le controller.
Si ton modèle s'appelle *AppUser*, alors ton controller devrait s'appeler *AppUserController* et le dossier pour stocker tes vues s'appellera *appuser*.
Ça permettra d'éviter les erreurs et le code sera plus facile à comprendre.

Attention à ne pas mettre de valeurs par défaut dans les zones de saisie de l'e-mail et du mot de passe.
C'est dangereux s'il s'agit de vraies valeurs de connexion.
De plus, c'est perturbant pour l'utilisateur qui pourrait penser qu'il s'agit de ses identifiants précédemment enregistrés.

Sinon, l'accès grâce aux identifiants et mots de passe est bien géré.

-----

### #7 Mettre en place les permissions

La gestion des permissions n'a pas été mise en place.
Il s'agit de vérifier, pour chaque appel à une route, le statut de l'utilisateur actuellement connecté.
En fonction de ce statut, on lui permettra ou pas d'accéder à la route.

-----

## Bonus

### Validation des données

Tu as bien commencé à vérifier que les données n'étaient pas vides avant de les ajouter en base de données.
Néanmoins, il faut le faire pour chaque élément et pas seulement pour le nom.

----

### Mise à jour d'un prof et d'un étudiant

Les mises à jour sont presque fonctionnelles.
Il reste seulement des incohérences dans les noms des variables et des méthodes utilisées.

Je t'invite à bien revérifier qu'il n'y a pas de faute dans le nom des variables et également vérifier si les méthodes appelées existent bien.

Il faut enfin faire attention en copiant-collant des éléments de *TeachersController* dans *StudentsController* à bien remplacer tous les éléments faisant référence à *Teacher* par *Student*.

----

### Suppression d'un prof et d'un étudiant

Ces parties n'ont pas été réalisées mais le raisonnement est le même que pour l'ajout ou la modification.
Ce sera même plus simple car il n'y a pas de formulaire à gérer pour cette partie.
Un simple lien permettra de lancer la suppression.

---

## Mega Bonus

Cette partie n'a pas été réalisée mais c'est déjà bien d'être arrivé jusque là.

N'hésite pas à revenir vers moi si tu as des interrogations sur les dernières questions que tu n'as pas pu faire.

---

---

## Conseils supplémentaires

##### Fichiers

Il manque de nombreux fichiers pour que le site puisse fonctionner :

- .htaccess
- ErrorController
- MainController
- CoreController

Il n'est donc pas possible de le tester.
Lorsque l'on ouvre l'index de ton projet, on tombe sur une page blanche.

Tu peux facilement te rendre compte des éventuels fichiers manquants en consultant les logs d'erreur.

-----

##### index.php

Pour plus de clarté, je te conseille de définir toutes tes routes dans un fichier à part.
Dans la correction, il s'agit du fichier *routes.php*.
Cela permettra de rendre le code du fichier *index.php* plus lisible.

Ça applique en fait à tous les cas. Si tu commences à avoir un gros morceau de code pour une fonction ou la définition d'éléments par exemple, il vaut mieux le faire dans un fichier à part.

---

##### self

Dans tes fonctions static, tu peux utiliser *self::class* pour récupérer directement le nom de la classe dans laquelle tu es.

Cela t'évitera de devoir retaper par exemple *App\Models\AppUser* à chaque fois.

De plus, tu pourras copier-coller ces morceaux de code dans d'autres classes sans avoir rien à changer.

Enfin, si jamais tu changes le nom de la classe (ce qui est très rare mais on ne sait jamais), tu n'auras pas à renommer tous tes appels à cette classe.

---

Ce sont vraiment des petits plus, ce n'est pas grave si tu ne retiens pas tout maintenant. Mais tu pourras y revenir et tester tout ça quand tu seras plus à l'aise.









