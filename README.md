# Introduction
Dans ce tutoriel, nous allons vous guider pas à pas dans la création d'une application web en réalité augmentée (AR) simple. 

Nous utiliserons A-Frame, un framework web open-source pour créer des expériences VR/AR, et AR.js, une bibliothèque JavaScript qui permet d'intégrer des fonctionnalités AR dans les applications web. 

Notre objectif sera d'afficher le texte "Hello" sur un marqueur AR de type code-barres. Puis de customiser le contenu.

Ce petit projet comprend aussi la réalisation d'une "étiquette" / "porte clé".
<p style="align:center; width: 100%;"> 
  <img src="ressources/markup_1000019121.png" alt="text disaplyed in ar" width="45%"/>
  <img src="ressources/markup_1000019122.png" alt="3d model displayed in ar" width="45%"/>
</p>

# Prérequis
- Un ordinateur
- Un éditeur de code notre outil sera : [projectIDX](https://idx.dev/)
- Un navigateur web (Chrome, Firefox ...)
- Un smartphone avec un navigateur web (Chrome, Firefox ...)

# Matériel à votre disposition
- un petit carré de carton bois au bords arrondis
- un sticker découpé sur vynile mat
- un petit cordon métallique avec une attache
- une petite puce rfid

<p style="align:center; width: 100%;"> 
  <img src="ressources/PXL_20240912_065600761.jpg" alt="photo of all the elemtns" width="75%" />
</p>

Pour l'assemblage, rien de plus simple :
- coller le sticker sur le carré en carton bois sur l'emplacement délimité par la gravure.
- coller la puce RFID, centrée, au dos de ce carré.
- dévisser l'attache et faite la passer dans le trou.

et voilà ! on est prêts à passer sur la partie numérique !

Si vous voulez plus d'infos sur cette partie là
- [Explications de la découpe stickers](https://github.com/LucieMrc/SilhouetteCameo_2spi)
- [Explications sur la découpe laser](https://github.com/b2renger/Introduction_Laser_Beambox)

# Étape 1 : Créer un compte GitHub et un dépôt
- Créer un compte GitHub : Si vous n'en avez pas déjà un, rendez-vous sur https://github.com/signup?source=login et créez un compte.

**☢️ Le nom d'utilisateur que vous choisissez sera utilisé pour l'adresse qu'il faudra tapper pour voir votre projet. <u>Choisissez un nom court ! sans espaces, sans caractères spéciaux (accents etc.)</u>**

<div style="display: flex; justify-content: space-around; width: 100%;"> 
  <img src="ressources/Capture_signup_github.png" alt="signup github page" width="49%" />
  <img src="ressources/Capture_login_github.png" alt="login github page" width="49%" />
</div>

- Créer un nouveau dépôt : Une fois connecté, cliquez sur le bouton "New repository". Donnez un nom à votre dépôt (par exemple, "microProjetAr"), ajoutez une description facultative, et cliquez sur "Create repository".

<div style="display: flex; justify-content: space-around; width: 100%;"> 
<img src="ressources/Capture_github_newRepo.png" alt="menu to create new repo" width="75%" />
</div>
</br>
<div style="display: flex; justify-content: space-around; width: 100%;">
<img src="ressources/Capture_github_newRepoCreation.png" alt="menu to create new repo" width="75%" />
</div>



# Étape 2 : Activer GitHub Pages
Nous allons maintenant configurer GitHub Pages, pour permettre à notre projet d'être servi par les serveurs de github lorsque l'on rentre l'adresse : https://[votre-nom-utilisateur].github.io/[votre-depot]


- Accéder aux paramètres : Dans votre dépôt, cliquez sur l'onglet "Settings", puis sur l'onglet "Pages"

<div style="display: flex; justify-content: space-around; width: 100%;"> 
<img src="ressources/Capture_github_settings.png" alt="menu to access gh-pages settings" width="75%" />
</div>
</br>
<div style="display: flex; justify-content: space-around; width: 100%;"> 
<img src="ressources/Capture_github_settings_pages.png" alt="Pages menu to access gh-pages settings" width="75%" />
</div>

- Sélectionner la branche : Dans la section "GitHub Pages", sélectionnez la branche main (ou la branche principale de votre dépôt).
- Enregistrer les modifications : Cliquez sur le bouton "Save". Votre site GitHub Pages sera maintenant accessible à l'adresse https://[votre-nom-utilisateur].github.io/[microprojetAr].

<div style="display: flex; justify-content: space-around; width: 100%;"> 
<img src="ressources/Capture_github_settings_pages_activate.png" alt="choose branch and save" width="75%" />
</div>

Si vous revenez sur la page d'accueil de votre projet, vous remarquerez au bout de quelques minutes, que certains éléments ont changé. Un déploiement est maintenant disponible !

<div style="display: flex; justify-content: space-around; width: 100%;"> 
<img src="ressources/Capture_github_settings_pages_done.png" alt="choose branch and save" width="75%" />
</div>

Toute l'infrastructure nécessaire pour héberger votre projet est donc bien en place, il suffit maintenant d'ajouter du contenu.


# Étape 3 : Utiliser Project IDX

Ouvrir Project IDX et créez un nouveau projet.

Importer le dépôt : Utilisez l'option pour importer votre dépôt GitHub dans Project IDX.

Choisir un environnement : Sélectionnez un environnement de développement adapté (par exemple, Node.js).

# Étape 4 : Créer la page HTML

Créer un fichier index.html : Dans votre projet IDX, créez un fichier nommé index.html.

Ajouter le code HTML : Copiez et collez le code HTML suivant dans votre fichier index.html :

```HTML
<!DOCTYPE html>
<html>
<head>
  <title>Ma première app AR</title>
  <script src="https://aframe.io/releases/1.3.0/aframe.min.js"></script>
  <script src="https://raw.githubusercontent.com/jeromeetienne/AR.js/master/aframe/build/aframe-ar.js"></script>   

</head>
<body>
    <a-scene embedded
    arjs="sourceType: webcam; detectionMode: mono_and_matrix; matrixCodeType: 3x3; trackingMethod: best ; changeMatrixMode: modelViewMatrix;"
    renderer="sortObjects: true; antialias: true; colorManagement: true; physicallyCorrectLights; logarithmicDepthBuffer: true;"

    vr-mode-ui="enabled: false"

    smooth=" true" smoothCount="5" smoothTolerance=".05" smoothThreshold="5"
    
    sourceWidth="800" sourceHeight="600" displayWidth="1280" displayHeight="720">

      
        <a-marker type='barcode' value='2'>
   
            <a-text value="Hello !" 
            side="double" position = "0 0 -1" rotation="270 0 0" 
            width="8"
            color="red" align="center" >
            </a-text>

        </a-marker>

        <a-entity camera></a-entity>
  </a-scene>
</body>
</html>
```


# Étape 5 : Comprendre le code
Ce code crée une expérience simple de réalité augmentée (RA) en utilisant A-Frame et AR.js. Décomposons ce que fait chaque partie :

Si vous n'êtes pas à l'aise et ne connaissez pas du tout la manière dont du code html fonctionne cliquez sur le petit triangle pour déplier une explication des bases de la syntaxe html

<details > <summary> <b>&#128161 les bases html</b> </summary>

Une page HTML est comme un sandwich. Elle a besoin d'un pain du haut et d'un pain du bas pour contenir la garniture !

Le pain du haut et du bas, ce sont les balises ```<html>``` et ```</html>```. Elles indiquent au navigateur que le contenu entre ces balises est du code HTML.

Deux parties principales : À l'intérieur du "sandwich HTML", on trouve deux parties :

**La tête** (```<head>``` et ```</head>```) : C'est comme les informations sur l'emballage du sandwich. On y met des informations importantes pour le navigateur, mais qui ne sont pas affichées directement à l'utilisateur. 

Par exemple :
- Le titre de la page ```<title>```

- Des liens vers des fichiers CSS pour le style

- Des liens vers des fichiers JavaScript pour les fonctionnalités interactives

**Le corps** (```<body>``` et ```</body>```) : C'est la garniture du sandwich ! C'est le contenu visible de la page web : texte, images, vidéos, etc.

La syntaxe et donc l'interprétation par le navigateur du code html repose sur des balises ouvrantes et fermantes :

- La balise **ouvrante** (par exemple ```<p>```)  dit au navigateur : "Attention, on commence un paragraphe !"
- La balise fermante (par exemple ```</p>```) dit : "Voilà, le paragraphe est terminé."

Tout le contenu entre la balise ouvrante et la balise fermante est considéré comme faisant partie de cet élément.

Exemple :
```html
<html>
<head>
  <title>Ma page web</title>
</head>
<body>
  <h1>Bienvenue !</h1>
  <p>Ceci est un paragraphe de texte.</p>
</body>
</html>
```
Dans cet exemple :

- ```<html>``` ouvre la page HTML et ```</html>``` la ferme.
- ```<head>``` ouvre la section d'en-tête et ```</head>``` la ferme.
- ```<title>``` ouvre le titre de la page et ```</title>``` le ferme.
- ```<body>``` ouvre le corps de la page et ```</body>``` le ferme.
- ```<h1>``` ouvre un titre de niveau 1 et ```</h1>``` le ferme.
- ```<p>``` ouvre un paragraphe et ```</p>``` le ferme.

</details>
</br>

Ici nous avons une structure HTML classique : Le code met en place une page HTML basique avec les sections <head> et <body>.


Dans la partie ```<head>```, nous ajoutons : 

- le titre de l'expérience

```html
<title>Ma première app AR</title>
```

- la *Bibliothèque A-Frame* : Il inclut la bibliothèque A-Frame (aframe.min.js) qui est un framework JavaScript permettant de créer des expériences de réalité virtuelle (RV) et de RA en utilisant du HTML.
```html
<script src="https://aframe.io/releases/1.3.0/aframe.min.js"></script>
``` 

- la *Bibliothèque AR.js* : Il inclut la bibliothèque AR.js (aframe-ar.js) qui ajoute des capacités de RA à A-Frame.
```html
  <script src="https://raw.githubusercontent.com/jeromeetienne/AR.js/master/aframe/build/aframe-ar.js"></script>  
```

Dans la partie ```<body>```, et c'est ici que tout ce joue pour le contenu visible par l'utilisateur. Nous ajoutons : 

- la *scène RA* : L'élément ```<a-scene>``` crée la scène de RA.
  ```html
  <a-scene embedded
    arjs="sourceType: webcam; detectionMode: mono_and_matrix; matrixCodeType: 3x3; trackingMethod: best ; changeMatrixMode: modelViewMatrix;"
    renderer="sortObjects: true; antialias: true; colorManagement: true; physicallyCorrectLights; logarithmicDepthBuffer: true;"

    vr-mode-ui="enabled: false"

    smooth=" true" smoothCount="5" smoothTolerance=".05" smoothThreshold="5"
    
    sourceWidth="800" sourceHeight="600" displayWidth="1280" displayHeight="720">

        <!-- contenu de l'expérience AR avec d'autres balises -->

        </a-scene>
  ```
  Remarquez qu'avant le chevron fermant '>' de la balise ```<a-scene>``` nous ajoutons beaucoup d'options (qui s'appellent attributs en html)  pour configuer la manière dont la scène va s'afficher.

  <details > <summary> <b>&#128161 les détails des options de configuration de l'attribut arjs</b> </summary>
  - *embedded* : Cet attribut indique à A-Frame d'intégrer la scène dans la page HTML.

  - *arjs* : Cet attribut configure AR.js 
    - *sourceType: webcam* : Utilise la webcam de l'appareil comme source vidéo.
    - *detectionMode: mono_and_matrix* : Détecte à la fois les images cibles et les marqueurs de type code-barres.
    - *matrixCodeType: 3x3* : Spécifie que le type de code-barres utilisé est un code-barres matriciel 3x3.
    - *trackingMethod: best* : Utilise la meilleure méthode de suivi disponible.
    - *changeMatrixMode: modelViewMatrix* : Mode de changement de matrice pour le suivi.
    - *vr-mode-ui="enabled: false"* : Désactive l'interface utilisateur du mode VR.
    - *renderer*. Configure le rendu de la scène avec des options pour le tri des objets, l'antialiasing, la gestion des couleurs, etc.
    - *smooth* : Active le lissage du mouvement de la caméra.
  </details>
  </br>

- Le *marqueur* : L'élément ```<a-marker>``` définit un marqueur de type code-barres avec la valeur '2'. Lorsque la caméra détecte ce marqueur, le contenu à l'intérieur de la balise sera affiché en RA.
  ```html
  <a-marker type='barcode' value='2'>
    <!-- ajouter du contenu qui sera visible par l'utilisateur et donc ancré sur notre marqueur -->
  </a-marker>
  ```
  Ici la valeur 2 correspond à un motif précis qui a été prédécoupé pour vous à la [découpeuse de stickers](https://github.com/LucieMrc/SilhouetteCameo_2spi). Avec la technique que nous utilisons [il existe 64 motifs différents](https://github.com/b2renger/Introduction_A-frame/blob/main/markers/barcodes/2.png) qui peuvent être détectés en même temps par arjs.

- Un texte : L'élément <a-text> crée un texte en 3D qui sera affiché au-dessus du marqueur. Le texte est "Hello !", de couleur rouge et centré.
  ```html
  <a-text value="Hello !" 
            side="double" position = "0 0 -1" rotation="270 0 0" 
            width="8"
            color="red" align="center" >
  </a-text>
  ```
  - *value* : Le texte à afficher.
  - *side=double* : permet d'afficher le texte quelque soit l'angle sous lequel on le regarde.
  - *position="0 0 -1" : la position xyz du centre du texte par rapport au centre du marqueur.
  - *rotation="270 0 0"* :
  - *width="8"* : la largeur du texte.
  - *color="red"* : la couleur du texte.
  - *align="center"* : l'alignement du texte.

- Caméra : L'élément <a-entity camera> définit la caméra de la scène.

En résumé, ce code crée une expérience de RA où un texte en 3D apparaît lorsqu'un marqueur de code-barres spécifique est détecté par la caméra.

A-Frame : Le tag <a-scene> définit la scène 3D. L'attribut arjs indique que la scène est une scène AR.

AR.js : Le tag <a-marker> définit un marqueur AR. L'attribut preset="barcode" indique que le marqueur est un code-barres. L'attribut value spécifie l'image du code-barres.

A-text : Le tag <a-text> affiche du texte dans la scène 3D.


# Étape 6 : Enregistrer les modifications et les commiter sur GitHub
Enregistrer les modifications : Enregistrez votre fichier index.html.

Commiter les modifications : Utilisez les outils de versioning de Project IDX pour commiter vos changements et les pousser sur votre dépôt GitHub.

# Étape 7 : Tester l'application
Accéder à l'URL de votre GitHub Pages : Ouvrez l'URL de votre site GitHub Pages dans votre navigateur.

Ouvrir la caméra : Autorisez l'accès à votre caméra lorsque vous y êtes invité.

Pointer la caméra sur le marker code-barres 

**Félicitations !**  Vous avez créé votre première application AR. Vous pouvez maintenant personnaliser votre application en modifiant le texte, en ajoutant des modèles 3D, et en expérimentant avec différentes fonctionnalités d'A-Frame et AR.js.

Note : Ce tutoriel est une introduction de base. Pour approfondir vos connaissances, consultez la documentation officielle d'A-Frame et AR.js.

# Pour aller plus loin ...

Un cours entier en anglais est disponible sur [le site de l'ateliernum](http://ateliernum.github.io) à cette adresse : https://github.com/b2renger/Introduction_A-frame#introduction_a-frame

Personnaliser l'apparence : Ajouter d'autres éléments, modifier les couleurs, les tailles et les positions des éléments.

Ajouter des modèles 3D : Importer des modèles 3D dans votre scène.

Utiliser d'autres types de marqueurs : Explorer les différents types de marqueurs AR.

Créer des interactions : Ajouter des événements et des interactions à votre application.
