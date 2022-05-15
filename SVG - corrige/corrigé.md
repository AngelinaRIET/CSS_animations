### 1. Barre de chargement

Pour créer cette barre de chargement, nous avons ajouté un rectangle dans le SVG d'une hauteur de 10px. Ce rectangle a d'abord une largeur de 0px puis s'élargi jusqu'à atteindre 100% de la largeur. C'est la balise animate, à l'intérieur du `rect` qui permet de réaliser une animation sur le rectangle.

```html
<svg>
  <rect height="10" fill="cadetblue">
    <animate
      attributeType="CSS"
      attributeName="width"
      from="1"
      to="100%"
      dur="10s"
      fill="freeze"
    />
  </rect>
</svg>
```

- `attributeName` : permet d'indiquer la propriété à animer, ici la largeur de l'élément
- `from` : valeur au départ de l'animation
- `to` : valeur à la fin de l'animation
- `dur` : durée de l'animation
- `fill` : même si cette propriété a le même nom que la propriété qui permet de renseigner la couleur de remplissage d'un élément, celle-ci permet d'indiquer à l'élément dans quel état rester à la fin de l'animation. `freeze` permet à l'élément de rester dans l'état de la fin de l'animation. `remove` permet au contraire de revenir à l'état du début de l'animation

#### 1.bonus Texte dans le SVG

```html
<svg>
  <rect>...</rect>
  <text font-family="sans-serif" y="30" x="10" fill="cadetblue">
    En cours de chargement
    <animate
      attributeType="CSS"
      attributeName="opacity"
      from="1"
      to="0"
      dur="10s"
      values="1; 1; 0"
      keyTimes="0; 0.9; 1"
      fill="freeze"
    />
  </text>
</svg>
```

On ajoute une balise `<text>` dans le SVG que l'on vient animer à l'aide de breackpoints (values et keyTimes) :

- `values` : les différentes valeurs que prendra l'animation
- `keyTimes` : les moments où les valeurs de l'animation changent

Ici, le texte apparait à une opacité de 1 (=100%) au départ de l'animation. A 90% de l'animation (=9s), il est toujours à 100% d'opacité mais décroit jusqu'à 0 dans la seconde qui suit. Cela nous permet d'éviter que le texte s'efface peu à peu dès le départ mais uniquement sur la dernière seconde.

### 2. Animer un cercle au clic

```html
<circle cx="40" cy="60" r="20">
  <animate
    attributeName="cx"
    from="40"
    to="calc(100% - 40px)"
    dur="3s"
    begin="click"
  />
</circle>
```

Dans l'attribut `to`, on utilise la fonction `calc()` de CSS qui permet de venir placer à droite l'élément à même distance du bord gauche où il était initialement.

C'est l'attribut `begin` qui permet de démarrer l'animation au click !

#### 3.bonus - Répéter l'animation

```html
<circle cx="40" cy="60" r="20">
  <animate
    attributeName="cx"
    from="40"
    to="calc(100% - 40px)"
    dur="3s"
    begin="click"
    repeatCount="indefinite"
  />
</circle>
```

Il suffit de rajouter `repeatCount="indefinite"` afin de répéter indéfiniment l'animation.

### 3. Battement de coeur

```html
<svg class="" height="150">
  <g>
    <path
      transform-origin="33px 30px"
      fill="#870707"
      d="M50.286,30.124C57.379,17.378 71.566,17.378 78.659,23.751C85.753,30.124 85.753,42.87 78.659,55.616C73.694,65.175 60.926,74.735 50.286,81.108C39.645,74.735 26.877,65.175 21.912,55.616C14.818,42.87 14.818,30.124 21.912,23.751C29.005,17.378 43.192,17.378 50.286,30.124Z"
    >
      <animateTransform
        attributeName="transform"
        type="scale"
        dur="1s"
        values="1.5;1.3; 1.35; 1.20;1.5; 1.5"
        keyTimes="0;0.2;0.35;0.5;0.75;1"
        repeatCount="indefinite"
      />
    </path>
  </g>
</svg>
```

Le coeur est fait sous Affinity Designer. Sa taille par défaut est de 67px\*61px. On utilise `transform-origin="33px 30px"` afin que l'animation se fasse depuis le centre du cercle et non pas son angle haut gauche. Ces chiffres correspondent respectivement à la moitié de sa largeur et la moitié de sa hauteur.

On utilise ici `values` et `keyTimes` dans la mesure où il y a différentes transformations à appliquer durant l'animation et non pas une transformation linéaire.

Pour produire l'effet d'aller-retour de l'animation, il faut que la valeur de départ et de fin soient les mêmes.

### 4. Chemin

```html
<svg class="border auto" height="200" width="500">
  <path
    d="M0,195 h495 V5 H10,5 l0,195"
    stroke="black"
    stroke-width="10px"
    fill="none"
    stroke-dasharray="1400"
    stroke-dashoffset="1400"
  >
    <animate
      attributeName="stroke-dashoffset"
      from="1400"
      to="0"
      dur="5s"
      repeatCount="indefinite"
    />
  </path>
</svg>
```

On utilise le contour du tracé grâce à `stroke-width` et `stroke`. `fill="none"` permet de supprimer la couleur de remplissage du rectangle.

Pour créer l'animation, on va tricher sur le contour du tracé en jouant sur un effet de pointillé.

On utilise les propriétés `stroke-dasharray` pour déterminer l'espace entre les pointillés et
`stroke-dashoffset` permet de déterminer la position du premier pointillé. Les 2 contiennent pour valeur un nombre correspondant à la longueur du tracé (idéalement il faudrait utiliser du JavaScript afin de déterminer avec exactitude et de façon dynamique cette longueur). Ici, nous faisons à vu de nez (et de calcul) : en effet, le SGV fait : 500px de large _ 2 = 1000px + 200px de hauteur _ 2 = 400px + 1000px = 1400px !

On vient ensuite animer `stroke-dashoffset` pour modifier cette fameuse position de départ du pointillé. C'est l'animation de cette propriété qui nous permet de générer l'apparition du tracé.

### 5. Positionner du texte sur un tracé

Le tracé utilisé a été généré sous Affinity Designer à l'aide de la Plume.

```html
<svg height="250">
  <path
    id="ligne"
    d="M29.729,199.463C29.729,199.463 67.895,136.425 138.002,134.207C208.109,131.989 242.419,191.404 342.662,195.04C442.904,198.676 462.374,160.534 462.374,160.534"
    fill="none"
    stroke="lightgrey"
  />
  <text>
    <textpath xlink:href="#ligne" font-size="20px">
      Ne rêve pas ta vie mais vis tes rêves. — Bernard Asleyr
    </textpath>
  </text>
</svg>
```

On renseigne un `id` au `path` qui a un contour (ici pour l'exercice). On utilise ensuite une balise `text` pour ajouter notre phrase qui lui-même contiendra un `textpath`. C'est cette balise qui permet de créer un lien entre le tracé et le texte grâce à la propriété `xlink:href` qui permet de faire le lien avec l'id du `path`.

> ⚠️ Le texte doit absolument se trouver à l'intérieur même de `textpath`.

#### 5.bonus - Animer le texte

```html
<textpath xlink:href="#ligne" font-size="20px">
  Ne rêve pas ta vie mais vis tes rêves. — Bernard Asleyr
  <animate
    attributeName="startOffset"
    from="0%"
    to="100%"
    dur="5s"
    repeatCount="indefinite"
  />
</textpath>
```

Pour animer le texte sur le tracé, on vient animer l'attribut startOffset, qui indique à partir de quel endroit commence à apparaitre le texte.

0% correspond donc au tout début du tracé et on anime jusqu'à 100% de façon à décaler petit à petit le texte vers la fin du tracé.
