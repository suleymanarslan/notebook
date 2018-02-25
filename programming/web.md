# Web

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
