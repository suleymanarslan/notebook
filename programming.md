# programming

I find myself Googling same stuff every time I'm making something. This is for remembering programming tips/snippets that I learn and forget easily.

* [CSS](#css)
* [Bash](#bash)
* [Makefiles](#makefiles)
* [systemd](#systemd)
* [Upstart](#upstart)
* [Codesign](#codesign)
* [Scraping Wikipedia](#scraping-wikipedia)
* [HTTP Status Codes](#http-status-codes)

## CSS

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

#### Check if a command exists

Definition:
```bash
  command_exists () {
      type "$1" &> /dev/null ;
  }
```

Usage:

```
  if command_exists foo ; then
      echo "yo"
  fi
```

### loops

#### Iterate Files

```bash
for i in *; do echo $i; done
```

#### iterating input by line and columns

```bash
lsblk | awk '{print $1,$4}' > input.txt

while read col1 col2 ; do
  echo "$col1 $col2"
done < input.txt
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

## systemd

#### Basic commands:

* `service myapp start|stop|restart|status`
* Reload service config: `systemctl daemon-reload`
* See logs: `journalctl -u {myapp}`

## upstart

* Logs are saved to /var/log/{app}

#### Commands:

* `initctl list`
* `initctl status myapp`
* `initctl start myapp`

Service can be used, too;

* `sudo service goweb status`
* `sudo service goweb start`

Syntax Check:
* `init-checkconf /etc/init/goweb.conf`

#### Example script:

```
description "A stupid golang http listener"

start on filesystem or runlevel [2345]
stop on runlevel [!2345]

setuid www-data
setgid www-data

env API_KEY=abcdefgh

respawn
respawn limit 5 2

chdir /opt

pre-start script
    # Source File
    . /path/to/env/file
end script

script
    # Start Listener
    /opt/listen
end script
```

## Codesign

A command-line tool for signing OSX apps. e.g

```
codesign --verbose=4 -s "<Signature Key>" --deep --strict Foo.app
```

Verify if an app was signed;

```
codesign -dvvv --strict --deep-verify Foo.app
```

Verify if it'll be allowed to be executed;

```
spctl -a -t exec -vv Foo.app
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

## HTTP Status Codes

#### 1xx Informatial Responses
* **100** Continue
* **101** Switching Protocols
* **102** Processing (WebDAV; RFC 2518)

#### 2xx Success
* **200** OK
* **201** Created
* **202** Accepted
* **203** Non-Authoritative Information (since HTTP/1.1)
* **204** No Content
* **205** Reset Content
* **206** Partial Content (RFC 7233)
* **207** Multi-Status (WebDAV; RFC 4918)
* **208** Already Reported (WebDAV; RFC 5842)
* **226** IM Used (RFC 3229)

#### 3xx Redirection
* **300** Multiple Choices
* **301** Moved Permanently
* **302** Found
* **303** See Other (since HTTP/1.1)
* **304** Not Modified (RFC 7232)
* **305** Use Proxy (since HTTP/1.1)
* **306** Switch Proxy
* **307** Temporary Redirect (since HTTP/1.1)
* **308** Permanent Redirect (RFC 7538)

#### 4xx Client Errors
* **400** Bad Request
* **401** Unauthorized (RFC 7235)
* **402** Payment Required
* **403** Forbidden
* **404** Not Found
* **405** Method Not Allowed
* **406** Not Acceptable
* **407** Proxy Authentication Required (RFC 7235)
* **408** Request Timeout
* **409** Conflict
* **410** Gone
* **411** Length Required
* **412** Precondition Failed (RFC 7232)
* **413** Payload Too Large (RFC 7231)
* **414** URI Too Long (RFC 7231)
* **415** Unsupported Media Type
* **416** Range Not Satisfiable (RFC 7233)
* **417** Expectation Failed
* **418** I'm a teapot (RFC 2324)
* **421** Misdirected Request (RFC 7540)
* **422** Unprocessable Entity (WebDAV; RFC 4918)
* **423** Locked (WebDAV; RFC 4918)
* **424** Failed Dependency (WebDAV; RFC 4918)
* **426** Upgrade Required
* **428** Precondition Required (RFC 6585)
* **429** Too Many Requests (RFC 6585)
* **431** Request Header Fields Too Large (RFC 6585)
* **451** Unavailable For Legal Reasons (RFC 7725)

#### 5xx Server Errors
* **500** Internal Server Error
* **501** Not Implemented
* **502** Bad Gateway
* **503** Service Unavailable
* **504** Gateway Time-out
* **505** HTTP Version Not Supported
* **506** Variant Also Negotiates (RFC 2295)
* **507** Insufficient Storage (WebDAV; RFC 4918)
* **508** Loop Detected (WebDAV; RFC 5842)
* **510** Not Extended (RFC 2774)
* **511** Network Authentication Required (RFC 6585)

#### Unofficial Codes
* **103** Checkpoint
* **103** Early Hints
* **420** Method Failure (Spring Framework)
* **420** Enhance Your Calm (Twitter)
* **450** Blocked by Windows Parental Controls (Microsoft)
* **498** Invalid Token (Esri)
* **499** Token Required (Esri)
* **509** Bandwidth Limit Exceeded (Apache Web Server/cPanel)
* **530** Site is frozen
* **598** (Informal convention) Network read timeout error
* **599** (Informal convention) Network connect timeout error
* **440** Login Time-out
* **449** Retry With
* **451** Redirect
* **444** No Response
* **495** SSL Certificate Error
* **496** SSL Certificate Required
* **497** HTTP Request Sent to HTTPS Port
* **499** Client Closed Request
* **520** Unknown Error
* **521** Web Server Is Down
* **522** Connection Timed Out
* **523** Origin Is Unreachable
* **524** A Timeout Occurred
* **525** SSL Handshake Failed
* **526** Invalid SSL Certificate
* **527** Railgun Error
