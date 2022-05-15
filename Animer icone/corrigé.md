# Animer une partie d'icône SVG

On vient manipuler le code du SVG pour lui ajouter une classe afin d'animer l'élément en CSS avec une animation.

## Corrigé

### 1. Icone de souris

Une fois la classe .move-y ajoutée dans le HTML, on crée la keyframe dans le CSS.

```css
.move-y {
  animation: moveY 1s infinite;
}

/* Déplace de haut en bas */
@keyframes moveY {
  from {
    transform: translateY(0);
  }
  20% {
    transform: translateY(-1px);
  }
  90% {
    transform: translateY(6px);
  }
  to {
    transform: translateY(0);
  }
}
```

Le translateY permet de modifier la position de l'élément verticalement. Ici, il monte de 1px puis descend de 6 avant de revenir à sa position de départ.

Cette animation dure 1 seconde et est répétée à l'infini grâce au `infinite`.

### 2. Les vagues

On crée un mouvement de vague sur les vagues du bas de l'icône.

```css
.distortion-y {
  transform-origin: center 90%;
  animation: distortionY 3s infinite;
}

/* Déforme sur l'axe Y */
@keyframes distortionY {
  from {
    transform: scaleY(0.6);
  }
  65% {
    transform: scaleY(1.2);
  }
  to {
    transform: scaleY(0.6);
  }
}
```

Le scaleY déplace également l'élément sur toute la hauteur du SVG, c'est pour quoi on vient changer son point d'origine. De cette façon, la distortion se fait, mais en laissant bien la ligne de vagues au même point d'horizon.

### 3. Ballon de volley

On souhaite faire tourner le ballon sur lui même de façon linéaire. On applique la classe sur la balise `<g>`

```css
.rotate-360 {
  transform-origin: center;
  animation: rotate360 3s linear infinite;
}

/* Rotation de 360deg */
@keyframes rotate360 {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
```

Le rotate déplace notre ballon, on doit donc changer l'origine de sa zone de travail pour qu'elle soit au centre et non dans l'angle en haut à gauche comme c'est le cas par défaut.
Pour éviter d'avoir un effet de ralenti-accélération dans l'animation, nous allons renseigner la valeur pour l'animation-timing-function que nous souhaitons linéaire (et non pas ease qui augmente puis ralenti à la fin).

### 4. Baseball

On souhaite animer les lignes derrière la balle afin de donner l'illusion d'un mouvement.

```css
.compress-x {
  transform-origin: 35%;
  animation: compressX 1s infinite;
}

.delay-03 {
  animation-delay: 0.3s;
}

/* Retréci sur l'axe horizontal */
@keyframes compressX {
  from {
    transform: scaleX(0.2);
  }

  70% {
    transform: scaleX(1);
  }

  to {
    transform: scaleX(0.2);
  }
}
```

Pour donner un départ différé à une ligne, on ajoute une classe delay-03 qui servira à rajouter un délai de 0.3s avant le démarrage de l'animation. On applique cette classe à la ligne du milieu.

### 5. Badminton

Nous souhaitons animer le volant de façon lineaire pour simuler un service.

```css
.badminton {
  transform-origin: center;
  animation: serve 1s linear infinite;
}

/* Service de volant badminton */
@keyframes serve {
  from {
    transform: translate(50%, 100%) rotate(120deg) scale(0.4);
  }

  70% {
    transform: translate(20%, 0) scale(0.6) rotate(30deg);
  }

  75% {
    transform: translate(15%, 0) scale(0.65) rotate(25deg);
  }

  80% {
    transform: translate(10%, 0) scale(0.7) rotate(20deg);
  }

  to {
    transform: translate(0, 0) rotate(0) scale(0.8);
  }
}
```

On modifie l'angle, la taille et la position de l'icône pour simuler le mouvement d'un service.
