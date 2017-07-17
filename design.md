# DESIGN

> Perfection is finally attained not when there is no longer anything to add, but when there is no longer anything to take away.
— Antoine de Saint-Exupery:

Index of Contents

* [Philosophy](#philosophy)
* [Get Inspired](#get-inspired)
* [Fonts](#fonts)
* [CSS](#css)

## Philosophy

* [Wabi Sabi](https://www.brainpickings.org/2010/11/11/wabi-sabi/)

## Get Inspired

Tools & Products:
* [Tumpline](https://en.wikipedia.org/wiki/Tumpline)
* [Bogarde BMX](http://www.bogarde.fr/)
* [Masahiro Kikuno](http://watchesbysjx.com/2017/05/portrait-masahiro-kikuno-japanese-watchmaker.html)

Websites:

* [freelance.tv](http://freelance.tv/)
* [bench.li](http://bench.li/)
* [minimal.gallery](http://minimal.gallery/)
* [julie.design](http://julie.design/)
* [semplice](https://www.semplice.com/) | [features](https://www.semplice.com/features) | [pricing](https://www.semplice.com/get-semplice)
* [bumpers.fm](https://bumpers.fm/)
* [betalist](https://betalist.com/) | [startup](https://betalist.com/startups/httpulse)
* [u+d](http://design.u.plus/)
* [aj](https://aj.lkn.io/)
* [carrd.co](https://carrd.co)
* [pixelarity](https://pixelarity.com/)
* [dropbox paper](https://www.dropbox.com/paper)
* [notion.so](https://www.notion.so/)
* [fly](https://fly.io/)
* [e-flux](http://www.e-flux.com/) | [article](http://www.e-flux.com/architecture/artificial-labor/)
* [nautiulus](https://nautil.us/) | [issue](http://nautil.us/issue/49/the-absurd) | [article](http://nautil.us/issue/49/the-absurd/chaos-makes-the-multiverse-unnecessary)
* [99percentinvisible](http://99percentinvisible.org/article/color-sphere-professors-pivotal-color-space-numbering-system/)
* [ugmonk](https://ugmonk.com/) | [blog](https://ugmonk.com/blog/)
* [c-reel](http://c-reel.com) | [tokyo](http://www.c-reel.com/tokyo/)
* [brainpickings](http://brainpickings.org/2017/05/18/beethoven-emilie-letter)
* [persona](https://persona.co/)
* [the gallery](http://thegallery.io/)
* [the intercept](https://theintercept.com/)
* [cargo collectie](http://cargocollective.com/) | [morocco](http://cargocollective.com/ninakeinrath/)
* [lonelyplanet.com](http://www.lonelyplanet.com/) | [cambodia](https://www.lonelyplanet.com/cambodia)
* [helen tran](http://helentran.com/) | [two habits](http://helentran.com/twohabits)
* [crew.co](https://crew.co/)
* [pudding](https://pudding.cool/)
* [the book of life](http://www.thebookoflife.org/)

## Fonts

### Useful

* [Beautiful Web Type](http://hellohappy.org/beautiful-web-type)
* [Typewolf](https://www.typewolf.com/): A collection of inspirational sites with fonts listed
* [Google Web Fonts Helper](http://google-webfonts-helper.herokuapp.com/fonts): Lets you download the fonts you like, so you can host your fonts.
* [The Pattern Library](http://thepatternlibrary.com)

### Fonts I Use

#### At [GetKozmos.com](https://getkozmos.com)

Following are the fonts I use at [getkozmos.com](https://getkozmos.com);

* Sans Serif: [Open Sans](https://fonts.google.com/specimen/Open+Sans)
* Serif: [Gentium Book Basic](https://fonts.google.com/specimen/Gentium+Book+Basic)
* Monospace: [PT Mono](https://fonts.google.com/specimen/PT+Mono)
* Display: [Lobster](https://fonts.google.com/specimen/Lobster)

#### At [azer.bike](http://azer.bike)

* Sans Serif: [Open Sans](https://fonts.google.com/specimen/Open+Sans)
* Serif: [Gentium Book Basic](https://fonts.google.com/specimen/Gentium+Book+Basic) and [Merriweather](https://fonts.google.com/specimen/Merriweather)

## CSS

#### Reset & Make Fonts Look Better

```css
* {
  font-weight: normal;
  -webkit-font-smoothing: antialiased !important;
  -moz-font-smoothing: antialiased !important;
  -moz-osx-font-smoothing: grayscale;
  speak: none;
  font-style: normal;
  font-weight: normal;
  font-variant: normal;
  text-transform: none;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
}
```

#### transition

Add transform property ease-in effect;

```css
-webkit-transition: -webkit-transform 0.3s ease-in;
-moz-transition: -moz-transform 0.3s ease-in;
-o-transition: -o-transform 0.3s ease-in;
transition: transform 0.3s ease-in;
```

Specify `all` instead of transform if effect should impact all properties.

#### not()
Apply rules to all except last one;

```
section:not(:last-child) { margin-bottom:1em; }
```

#### nth-child()

Keywords available: `even`, `odd`

Example: Select every 3rd element
```
ul li:nth-child(3n+3)
```

#### Masonry Layout

```html
<article>
  <section>foo</section>
  <section>bar</section>
</article>
```

```css
article {
 -moz-column-width: 13em;
 -webkit-column-width: 13em;
 -moz-column-gap: 1em;
 -webkit-column-gap: 1em;
}

section {
 display: inline-block;
 margin:  0.25rem;
 padding:  1rem;
 width:  100%;
 background:  #efefef;
}
```

### Rainbow Text Animation

```css
.rainbow {
   /* Chrome, Safari, Opera */
  -webkit-animation: rainbow 1s infinite;

  /* Internet Explorer */
  -ms-animation: rainbow 1s infinite;

  /* Standard Syntax */
  animation: rainbow 1s infinite;
}

/* Chrome, Safari, Opera */
@-webkit-keyframes rainbow{
  20%{ color: rgb(225, 45, 0); }
  40%{ color: rgb(255, 175, 0); }
  60%{ color: rgb(0, 200, 100); }
  80%{ color: rgb(0, 175, 200); }
  100%{ color: rgb(200, 100, 150); }
}

/* Internet Explorer */
@-ms-keyframes rainbow{
  20%{ color: rgb(225, 45, 0); }
  40%{ color: rgb(255, 175, 0); }
  60%{ color: rgb(0, 200, 100); }
  80%{ color: rgb(0, 175, 200); }
  100%{ color: rgb(200, 100, 150); }
}

/* Standard Syntax */
@keyframes rainbow{
  20%{ color: rgb(225, 45, 0); }
  40%{ color: rgb(255, 175, 0); }
  60%{ color: rgb(0, 200, 100); }
  80%{ color: rgb(0, 175, 200); }
  100%{ color: rgb(200, 100, 150); }
}
```

#### Shaking Effect

```css
/* also need keyframes and -moz-keyframes */
@-webkit-keyframes shake {
  8%, 41% {
    -webkit-transform: translateX(-10px);
  }
  25%, 58% {
    -webkit-transform: translateX(10px);
  }
  75% {
    -webkit-transform: translateX(-5px);
  }
  92% {
    -webkit-transform: translateX(5px);
  }
  0%, 100% {
    -webkit-transform: translateX(0);
  }
}
```

