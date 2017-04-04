# programming

I find myself Googling same stuff every time I'm making something. This is for remembering programming tips/snippets that I learn and forget easily.

* [Bash](#bash)
* [Makefiles](#makefiles)

## CSS

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

## Bash

### Conditions

#### Check if a variable is empty:

```bash
if [[ -z "${foobar// }" ]]; then
fi
```

#### Check if a variable is not empty:

```bash
[[ -n "${foobar// }" ]]
```

#### Check if a file exists:

```bash
if [ -f $FILE ];
then
   echo "File $FILE exists."
else
   echo "File $FILE does not exist."
fi
```

#### Check if a string contains another string

```bash
string='My long string'
if [[ $string == *"My long"* ]]; then
  echo "It's there!"
fi
```

### loops

#### Iterate Files

```bash
for i in *; do echo $i; done
```

### dialogs

#### opening a menu with bunch of lines

```bash
regionsArray=()

while read i name; do
  regionsArray+=($i "$name")
done <<< "$regions"

selected=$(dialog --stdout \
                  --title "Timezones" \
                  --backtitle "Happy Hacking Linux" \
                  --ok-label "Next" \
                  --no-cancel \
                  --menu "Select a continent or ocean from the menu:" \
                  20 50 30 \
                  "${regionsArray[@]}")
```

## Makefiles

#### multiline strings

It's possible as long as the variable is exported

```make
export COMPONENT_HTML
create-component:
  define COMPONENT_HTML
import html from "choo/html"

const view = (state, prev, send) => html`
$(name)
`

export default view
```
  endef

  @echo "$$COMPONENT_HTML" > ui/components/${name}.js

## Scraping Wikipedia

* [Request JSON Output of an Article](https://en.wikipedia.org/w/api.php?format=json&action=query&prop=extracts&explaintext=1&titles=Michelangelo)
