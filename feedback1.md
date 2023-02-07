# Feedback sur le parcours S06



### #2 Lister tous les profs

La liste des professeurs est correctement récupérée.

-----

### #3 Lister tous les étudiants

La liste des étudiants est correctement récupérée.

-----

### #4 Ajout d'un prof

L'ajout d'un prof est correctement réalisé.

----

### #5 Ajout d'un étudiant

À la fin de la fonction *studentAddPost*, il faut faire attention à bien récupérer la liste des professeurs pour la réutiliser dans la méthode *show* en cas d'erreur.

En effet, si tu ne le fais pas, lorsque la page va se rafraîchir avec les messages d'erreur, la liste des professeurs sera vide, donc impossible d'en sélectionner un et donc impossible de faire un ajout.

Rien de grave non plus mais, dans le morceau de code suivant, le message d'erreur ne correspond pas.
C'est en fait le professeur qui est manquant et non le statut :

```php
if(empty($teacher_id)) {
	$errorList[] = "Le status est vide ou invalide !";
}
```

-----

### #6 Restreindre l'accès aux utilisateurs

##### UserController

Par rapport au nommage de tes fichiers, si tu crées un modèle *AppUser*, il vaut mieux nommer le controller de la même façon, soit *AppUserController*.

Ça facilitera la compréhension et te permettra de rapidement retrouver le lien entre modèle et controller.

Il faut aussi se demander si c'est compréhensible pour quelqu'un d'autre qui lit ou travaille sur ton code (par exemple ton prof 😊) ou même toi si tu reviens dessus dans quelques temps.

##### Modèle AppUser

Les setters (*setEmail*, *setName*, ...) n'ont pas besoin de return à la fin car ils ne sont pas censés retourner de valeur.

-----

### #7 Mettre en place les permissions

##### CoreController

Pour plus de clarté, tu pourrais définir toutes les autorisations (*$acl*) dans un fichier à part.
Il suffit ensuite d'importer ce fichier dans ton *CoreController*.
Cela te permettra de retrouver tes autorisations plus rapidement si tu dois les modifier et le fichier *CoreController* sera plus lisible.

Enfin, selon la consigne, les personnes ayant un rôle *user* doivent pouvoir accéder à la liste des professeurs, ce qui n'est pas le cas ici car tu as défini *teacher_list* seulement pour les *admin*.

-----

## Bonus

### Validation des données

Les données sont bien validées lors de l'ajout d'un professeur ou d'un étudiant.
En cas de données incorrectes, tu ne réalises pas l'ajout et tu affiches bien les messages d'erreurs.

Il te manque juste la partie pour vérifier si le statut est bien égal à 1 ou 2.

----

### Mise à jour d'un prof

Il y a une erreur lors de la validation du formulaire de mise à jour d'un professeur. On tombe sur une page 404.
Tu n'as pas besoin de préciser d'action pour le form. En effet, en cliquant sur *Valider*, la page appelée par défaut sera la page de mise à jour d'un professeur. Et grâce au routeur, ce sera bien la fonction *teacherUpdatePost* de ton controller qui sera appelée.

Ensuite, lors de la fin du traitement, la consigne précise de rediriger vers la page de modification du professeur.
Dans ton cas, on est redirigé vers la liste des professeurs lorsque le traitement ne comporte pas d'erreur.

----

### Mise à jour d'un étudiant

Pour cette partie, il s'agit des mêmes remarques que pour la mise à jour d'un professeur.

----

### Suppression d'un prof

La suppression d'un professeur est correctement effectuée.
Néanmoins, par sécurité, il vaut mieux toujours vérifier que l'élément existe avant de le supprimer, afin d'éviter d'éventuelles erreurs.

----

### Suppression d'un étudiant

Pour cette partie, il s'agit des mêmes remarques que pour la suppression d'un professeur.

---

## Mega Bonus

Tu as bien géré l'accès à la page des utilisateurs seulement pour les administrateurs.

Je vois que tu n'as pu finir le méga bonus mais c'est déjà très bien d'être arrivé jusque là.

N'hésite pas à revenir vers moi si tu as besoin d'aide ou de précisions sur les dernières questions que tu n'as pas pu faire.

---

---

## Conseils supplémentaires

##### index.php

Comme pour les autorisations (*$acl*), pour plus de clarté, je te conseille de définir toutes tes routes dans un fichier à part.
Dans la correction, il s'agit du fichier *routes.php*.
Cela permettra de rendre le code du fichier *index.php* plus lisible.

Ça applique en fait à tous les cas. Si tu commences à avoir un gros morceau de code pour une fonction ou la définition d'éléments par exemple, il vaut mieux le faire dans un fichier à part.

---

##### .htaccess

Comme tu as sans doute pu le constater, les pages de ton site ne fonctionnent pas.
En fait, il te manque le fichier *.htaccess* dans le dossier *public*. Il te permettra d'activer la réécriture d'URL pour que ton router fonctionne.

Sans ce fichier, le navigateur ne pourra jamais faire la correspondance entre l'URL saisie et la méthode du controller correspondante.

Par exemple, quand tu vas vouloir accéder à */public/teachers*, le navigateur va rechercher un dossier *teachers* dans le dossier *public* et ouvrir sa page d'index.

Avec le *.htaccess*, le router pourra fonctionner et le navigateur saura que pour l'URL */public/teachers*, il faut aller chercher la méthode *teacher* de ton *TeacherController*.

J'imagine que cela a dû être problématique car tu n'as pas pu tester le rendu de tes pages.

N'hésite pas à revenir vers moi si tu souhaites plus d'explications.

---

##### Commentaires

N'hésite pas à commenter ton code pour bien décrire tout ce que tu fais.

Je sais que ça peut être ennuyeux et un peu long à faire mais crois moi, quand tu reviendras dans ton code dans quelques jours ou quelques semaines, tu seras bien content d'avoir une explication pour te remettre dans ce que tu as fait 😁.

Un autre truc tout bête mais qui peut aider est de bien nommer les variables.
Si par exemple tu récupères une liste de professeurs dans une variable, il vaut mieux l'appeler $*teachers* plutôt que *$teacher*.

Il y a juste une lettre de différence mais quand tu utiliseras cette variable dans un autre fichier, tu sauras tout de suite ce que tu peux trouver à l'intérieur, une liste de professeurs et non pas un professeur unique.

-----

##### self

Dans tes fonctions static, tu peux utiliser *self::class* pour récupérer directement le nom de la classe dans laquelle tu es.
Cela t'évitera de devoir retaper par exemple *App\Models\AppUser* à chaque fois.

De plus, tu pourras copier-coller ces morceaux de code dans d'autres classes sans avoir à les modifier.

Enfin, si jamais tu changes le nom de la classe (ce qui est très rare mais on ne sait jamais), tu n'auras pas à renommer tous tes appels à cette classe.

---

Ce sont vraiment des petits plus, ce n'est pas grave si tu ne retiens pas tout maintenant. Mais tu pourras y revenir et tester tout ça quand tu seras plus à l'aise.