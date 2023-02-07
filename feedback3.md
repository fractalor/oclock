# Feedback sur le parcours S06



### #2 Lister tous les profs

La liste des professeurs est correctement récupérée.

Attention en recopiant les morceaux de code fournis car certains éléments ne servent pas.

C'est le cas par exemple dans *teacher_list.tpl.php* pour la balise 

```html
<link rel="stylesheet" href="./css/style.css">
```

Le fichier *style.css* n'est pas accessible depuis cet endroit.
De plus, les éléments de style dans ce fichier ne s'appliquent à aucun élément du projet, ça ne sert donc à rien de l'utiliser.

-----

### #3 Lister tous les étudiants

La liste des étudiants est correctement récupérée.

Attention car il n'y a pas de menu dans les pages listant les professeurs et les étudiants, ce qui n'est pas pratique pour naviguer dans le site.
Je vois que tu as voulu recréer le menu dans chacune des pages, probablement car c'était fait de cette façon dans les pages d'intégration html/css fournies.

Ce n'est malheureusement pas la meilleure façon de faire.

En effet, tu vas devoir le faire dans chacune des pages du site, ce qui peut provoquer des oublis, comme c'est le cas dans ton projet. 

De plus, si tu as besoin d'ajouter une entrée supplémentaire dans le menu, tu vas devoir repasser sur toutes les pages pour faire la modification.

La meilleure façon de faire est de créer ton menu dans un fichier à part. Tu importes ensuite ce fichier lors de la création d'une page. Dans ton cas, il faudrait importer ce fichier à l'aide d'un *require_once* dans la fonction *show* de ton *MainController*.

Ainsi, le menu sera automatiquement ajouté dans toutes les pages et si tu as besoin de le modifier, tu le feras seulement une fois dans le fichier que tu as créé spécialement pour ton menu.

-----

### #4 Ajout d'un prof

La fonction d'ajout dans *TeacherController* se nomme *studentAdd*, ce qui peut prêter à confusion.
Il est important de bien nommer les éléments pour mieux s'y retrouver dans le code et éviter les erreurs.
Il s'agit certainement d'un copier-coller. Il faut être très vigilant lors de cette manipulation et bien revérifier les données collées.

De plus, le bouton d'ajout dans la page des professeurs appelle la fonction d'ajout d'un étudiant.

----

### #5 Ajout d'un étudiant

Attention car dans la page d'ajout, la liste des professeurs est mise "en dur".
Les professeurs étant stockés dans la base de données, il faut aller les récupérer pour les afficher dans la liste et ainsi faire la liaison avec l'étudiant lors de l'ajout.

Ensuite, il y a une erreur dans la requête SQL lors de l'ajout car on attend l'identifiant du professeur, qui est une valeur qui ne peut pas être nulle dans la table.

En récupérant la liste des professeurs et en utilisant l'identifiant du professeur sélectionné dans la requête d'insertion, cela corrigera le problème.

-----

### #6 Restreindre l'accès aux utilisateurs

Cette partie n'a pas été réalisée.

Dans cette partie, on cherche en fait à masquer l'accès aux différentes pages.
Seule la page de connexion doit être visible par défaut afin de forcer les utilisateurs à se connecter.

Il faudra également créer une méthode pour vérifier les données saisies par l'utilisateur au moment de la connexion et les comparer aux valeurs de la base de données.

-----

### #7 Mettre en place les permissions

Cette partie n'a pas été réalisée.

Pour cette partie, l'idée est de vérifier le rôle de l'utilisateur actuellement connecté afin de lui autoriser ou non l'accès à la page.

-----

## Bonus

### Validation des données

Tu as bien vérifié que le prénom et le nom de l'étudiant n'étaient pas vides lors de l'ajout.

Néanmoins, il faut également le faire pour le *status* car cette valeur ne peut pas être nulle.
Tu n'as pas non plus vérifié si le *status* était à 1 ou 2.

Attention à ne pas laisser de commentaires inutiles comme cette partie dans *StudentController* :

```php
// Si jamais vous avez par exemple, un NULL autorisé dans la base de données
// sur le champs subtitle de la tableau Category =>
// l'erreur ci-dessous n'est pas vraiment une erreur, on ne la gère pas !
/*if(empty($subtitle)) {
	$errorList[] = "Le sous-titre est vide !";
}*/
```

Ensuite, le traitement si les données sont incorrectes est bon mais il te manque l'affichage des erreurs une fois que l'on revient sur le formulaire.

En effet, il te faut afficher les erreurs si ton tableau *$errorList* n'est pas vide. Sinon, l'utilisateur ne peut pas comprendre ce qui n'a pas fonctionné.

Comme pour le menu, comme il s'agit d'un traitement générique qui peut s'appliquer à plusieurs pages, le mieux est de le créer dans un fichier à part. Tu trouveras un exemple dans la correction. Il s'agit du fichier */app/views/partials/errors.tpl.php*.

Tu n'as plus qu'à importer ce fichier dans tes pages suscpetibles d'afficher des messages.

----

Le reste du bonus, modification et suppression des étudiants et des professeurs n'a pas été réalisé.

La modification des données va ressembler à un ajout donc ça devrait être possible pour toi de coder ces parties avec un peu plus de temps.
Pour la suppression, ce sera plus simple à gérer car il n'y a pas de formulaire pour cette partie.

N'hésite pas à revenir vers moi si tu souhaites des précisions pour terminer cette partie. Cela te permettra d'aller un peu plus loin et d'apprendre encore plus efficacement en codant ces fonctionnalités.
Ça te servira forcément par la suite.

----

------

## Conseils supplémentaires

##### index.php

Pour plus de clarté, je te conseille de définir toutes tes routes dans un fichier à part.
Dans la correction, il s'agit du fichier *routes.php*.
Cela permettra de rendre le code du fichier *index.php* plus lisible.

Ça applique en fait à tous les cas. Si tu commences à avoir un gros morceau de code pour une fonction ou la définition d'éléments par exemple, il vaut mieux le faire dans un fichier à part.

---

##### .htaccess

Comme tu as sans doute pu le constater, les pages de ton site ne fonctionnent pas.
En fait, il te manque le fichier *.htaccess* dans le dossier *public*. Il te permettra d'activer la réécriture d'URL pour que ton router fonctionne.

Sans ce fichier, le navigateur ne pourra jamais faire la correspondance entre l'URL saisie et la méthode du controller correspondante.

Par exemple, quand tu vas vouloir accéder à */public/teacher_list*, le navigateur va rechercher un dossier *teacher_list* dans le dossier *public* et ouvrir sa page d'index.

Avec le *.htaccess*, le router pourra fonctionner et le navigateur saura que pour l'URL */public/teacher_list*, il faut aller chercher la méthode *teachers* de ton *TeacherController*.

J'imagine que cela a dû être problématique car tu n'as pas pu tester le rendu de tes pages.

N'hésite pas à revenir vers moi si tu souhaites plus d'explications.

-----

##### self

Dans tes fonctions static, tu peux utiliser *self::class* pour récupérer directement le nom de la classe dans laquelle tu es.

Cela t'évitera de devoir retaper par exemple *App\Models\Teacher* à chaque fois.

De plus, tu pourras copier-coller ces morceaux de code dans d'autres classes sans avoir rien à changer.

Enfin, si jamais tu changes le nom de la classe (ce qui est très rare mais on ne sait jamais), tu n'auras pas à renommer tous tes appels à cette classe.

-----

Ce sont vraiment des petits plus, ce n'est pas grave si tu ne retiens pas tout maintenant. Mais tu pourras y revenir et tester tout ça quand tu seras plus à l'aise