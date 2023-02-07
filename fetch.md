# Fetch



### Qu'est-ce que c'est ?

La méthode *fetch* va nous permettre d'échanger des données avec le serveur de manière asynchrone. 
C'est-à-dire qu'il n'y aura pas besoin de recharger la page.

----

### Comment ça fonctionne ?

Il s'agit d'une fonction Javascript qui prend une URL en paramètre.
On peut également lui préciser la méthode (GET ou POST) et un objet à transférer.

Il est possible d'utiliser beaucoup d'autres paramètres mais nous n'allons pas rentrer dans le détail maintenant.

-----

### Exemple

Prenons l'exemple de ta page de mise à jour d'un professeur.
Après le traitement de la mise à jour, on souhaite ensuite revenir sur la même page.

On va pouvoir utiliser la méthode fetch pour lancer la mise à jour sans recharger la page.

Commençons d'abord par ajouter un identifiant à notre formulaire, pour récupérer ses informations plus facilement :  

```html
<form action="" method="POST" class="mt-5" id="form_update">
```



Ensuite, on va modifier le bouton de type submit en un bouton normal qui appellera notre fonction javascript :

```html
<button type="button" onclick="return save();" class="btn btn-primary btn-block mt-5">Valider</button>
```



Enfin, voici le contenu de la fonction javascript :


```javascript
function save() {
	// Récupération de l'identifiant du professeur
	// Il s'agit du dernier élément de l'URL
	let id = window.location.pathname.split("/").pop();

	// Récupération des données du formulaire
	var form = new FormData(form_update);

	// Lancement de la mise à jour des données grâce à la méthode fetch
	fetch('/public/teacher/' + id, {
		method: 'POST',
		body: form
	});
}
```
On récupère tout d'abord l'identifiant du professeur qui est dans l'URL.
On en aura besoin pour appeler la bonne route.

On utilise ensuite *FormData* pour récupérer les champs du formulaire afin de les envoyer avec la méthode *fetch*.

Enfin, on appelle la méthode *fetch* en lui passant en paramètre l'URL correspondant à la mise à jour d'un professeur.
On précise également qu'il s'agit de la méthode POST et on utilise *body* pour envoyer les champs du formulaire.

Cet exemple est très sommaire.
On peut normalement gérer des messages de retour et les éventuelles erreurs.
Il serait par exemple possible de faire un traitement pour afficher un message de confirmation si la modification a bien été faite ou un message d'erreur dans le cas contraire.

Si tu veux en savoir plus, n'hésite pas à revenir vers moi.