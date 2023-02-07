# Feedback sur le parcours S06



### #2 Lister tous les profs

La liste des professeurs est correctement récupérée.

-----

### #3 Lister tous les étudiants

La liste des étudiants est correctement récupérée.

-----

### #4 Ajout d'un prof

L'ajout d'un prof n'est pas terminé.

----

La suite des questions et les bonus n'ont pas été faits.
Est-ce par incompréhension ou par manque de temps ?
Je te contacterai pour faire le point avec toi car il est vraiment dommage de ne pas avoir pu faire l'exercice entièrement, ne serait-ce que les premières questions sans les bonus.

La mise en pratique est la meilleure façon d'apprendre et il est fort probable que des morceaux de code que tu vas créer dans ces exercices te reserviront plus tard, dans d'autres exercices ou dans tes projets professionnels.

---

------

## Conseils supplémentaires

##### index.php

Pour plus de clarté, je te conseille de définir toutes tes routes dans un fichier à part.
Dans la correction, il s'agit du fichier *routes.php*.
Cela permettra de rendre le code du fichier *index.php* plus lisible.

Ça applique en fait à tous les cas. Si tu commences à avoir un gros morceau de code pour une fonction ou la définition d'éléments par exemple, il vaut mieux le faire dans un fichier à part.

---

##### err404

La page d'erreur 404 n'a pas été créée.
Pourtant, elle est utilisée dans le *Dispatcher*, ce qui va entraîner des erreurs.
Elle devrait se trouver dans */app/views/error/*.

Le fait de créer cette page pourra entraîner la suppression de l'erreur et te permettra de tester tes fonctions en naviguant sans les différentes pages.



