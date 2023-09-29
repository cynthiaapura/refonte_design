# **Refont web : développement** 🚀

[Lien vers la page](https://cynthiaapura.github.io/refonte_design/)
![cover](./asset/cover.PNG)


Dans le cadre de cette refonte, nous devons corriger les erreurs qui se sont glissées dans le projet, le HTML et la CSS.


### Première étape: corriger les erreurs et l'organisation au sein des fichiers du projet.
- Nous pouvons remarquer que l'image **cover** qui sert d'image de présentation pour le readme ne se trouve pas dans le dossier **asset**. Pour une question d'organisation il faut que cette image soit placée dans le fichier **asset**. Après avoir déplacé le fichier cover dans le bon dossier, il faut modifier les chemins dans lequel était appelé l'image.


- Nous pouvons aussi voir que les packages **Javascript** nécessaire à la compilation, ne sont pas présents dans le dossier. Le dossier **src** également est absent ainsi que le fichier **app.js** qui permet d'injecter du JS dans le projet. De ce fait, toutes les modifications apportées aux JavaScript ne seront pas compilées. Il faut créer le dossier src et le fichier app.js ensuite il faut installer et lancer le compilateur dans le projet afin d'avoir les **packages.json** et **node_modules**.


- Le **site.webmanifest** n'est pas configuré et n'est pas lié au HTML. Par conséquent les icônes ne seront pas prises en compte par le navigateur. Il faut donc formater le Json qui se trouve dans le fichier afin de le configurer correctement et ensuite l'ajouter dans une balise link dans le **head** du HTML.
```HTML
<link rel="manifest" href="favicon/site.webmanifest">
```


### Deuxième étape: vérifier les erreurs dans la console navigateur lors de l'inspection de la page web.


Nous allons vérifier en particulier l'onglet accessibilité afin de voir si les bonnes pratiques liées à l'accessibilité sont respectées.


Capture d'écran du rapport d'erreur dans l'onglet accessibilité :
![console_accessibilite](./asset/console_accessibilite.png)


Nous allons passer en revu chacune des erreurs remontés dans la console.


- **heading / entry / password text : étiquette de texte**
Cela signifie que les balises de titre ```<h1> <h2> <h3>``` etc... sont utilisées incorrectement ou hors de leur contexte. Les titres devraient être utilisés pour structurer hiérarchiquement le contenu de la page, et ils doivent être étiquetés correctement en tant que label. Un label est utilisé pour associer un texte descriptif à un élément interactif, tel qu'un champ de formulaire, un bouton, une case à cocher ou un bouton radio. Dans notre cas les erreurs **entry** et **password text** sont liées au fait que les champ de formulaire sont sans étiquette appropriée et ne comportent pas de label.
Concernant l'erreur du **heading** Celle-ci est surement liée au fait que les balises de titre ne sont pas utilisées de manière hiérarchique.


- **texte leaf : contraste**
Cette erreur signifie que le contraste de couleur n'est pas optimal pour l'accessibiité. Elles ne sont pas conformes aux normes WCAG pour l'accessibilité des textes.


### Troisième étape: nous allons corriger les erreurs dans le code HTML.


Lors d'une première lecture du code HTML, on s'aperçoit que la balise lang est a "en", il faut la modifier en "fr" afin que notre site soit référencé correctement en France et que les outils d'assistance puissent fournir la prononciation et le formatage appropriés pour le texte. Cette balise est un élément important pour indiquer la langue principale de la page web, ce qui contribue à améliorer l'accessibilité, la recherche, le traitement du texte et la compatibilité internationale de notre site.


```html
<html lang="fr">
```
Ensuite, nous pouvons voir que le head est incomplet et qu'il manque énormément de balises, notamment :

- pour la compatibilité sur les différents supports et ancienne version de navigateur
```html
<meta http-equiv=”X-UA-Compatible” content=”IE=edge”>
<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
```
- la balise meta d'encodage de caractères 
```html
<meta charset="UTF-8"> 
```
- les meta description pour le référencement naturel
```html
 <meta name="description" content="web design and developpment">
 ```
- les links favicons
```html
<link rel="apple-touch-icon" sizes="180x180" href="favicon/apple-touch-icon.png">
<link rel="icon" type="image/png" sizes="32x32" href="favicon/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="favicon/favicon-16x16.png">
```
- le link pour le chemin du manifest
```html
<link rel="manifest" href="favicon/site.webmanifest">
```
- le link pour le chemin pour le css
```html
<link rel="stylesheet" href="./css/screen.css">
```

Une fois que le head est complet, on passe le code HTML au W3C afin de connaître les erreurs rencontrées.
![erreur w3c](./asset/erreur_w3c.png)


#### Erreur #1
```From line 13, column 17; to line 13, column 33```
Le logo est absent. Lors du passage du lecteur d'écran, l'utilisateur sera alerté de la présence d'un titre mais il ne lira aucun texte car celui-ci est inéxistant. 

#### Erreur #2
```From line 27, column 17; to line 27, column 85```
La balise name ne peut pas être vide, j'ai donc rempli l'argument avec "search".

#### Erreur #3
```From line 28, column 30; to line 28, column 49```
Une balise **a** ne peut pas contenir une balise **button**, j'ai modifié en metant juste une balise **button** avec un **aria-label** 
```html 
<button class="btn" aria-label="link">Search</button>
```

#### Erreur #4
```From line 38, column 36; to line 38, column 47```
Une balise **a** ne peut pas contenir une balise **button**, j'ai modifié en metant juste une balise **button** avec un **aria-label** 
```html 
<button class="btn" aria-label="link">Search</button>
```

#### Erreur #5
```From line 43, column 21; to line 43, column 85```
La balise name ne peut pas être vide, j'ai donc rempli l'argument avec "password".

#### Erreur #6
```From line 44, column 42; to line 44, column 53```
Une balise **a** ne peut pas contenir une balise **button**, j'ai modifié en metant juste une balise **button** avec un **aria-label** 
```html
<button class="cn" aria-label="link">Login</button>
```

#### Erreur #7
```From line 47, column 50; to line 47, column 53```
Une balise **p** ne peut contenir une balise **a**, en revenche l'inverse est possible

#### Erreur #8
```From line 61, column 9; to line 61, column 14```
C'était une erreur de sémantique la balise n'était associé a aucune autre.

#### Erreur #9
```From line 62, column 5; to line 62, column 10```
C'était une erreur de sémantique la balise n'était associé a aucune autre.

Après toutes les modifications, on repasse le code html au W3C. Tout est validé.
![w3c](./asset/w3c.png)