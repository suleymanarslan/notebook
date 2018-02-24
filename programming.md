# programming

I find myself Googling same stuff every time I'm making something. This is for remembering programming tips/snippets that I learn and forget easily.

* [CSS](#css)
* [Bash](#bash)
* [SQL](#sql)
* [Makefiles](#makefiles)
* [systemd](#systemd)
* [Upstart](#upstart)
* [Codesign](#codesign)
* [Scraping Wikipedia](#scraping-wikipedia)
* [HTTP Status Codes](#http-status-codes)
* [Decimal & Binary Conversion](#decimal-binary-conversion)
* [Bitwise Operations](#bitwise-operations)

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

#### Rename bunch of files

```bash
for name in *
do
    newname=new-"$(echo "$name" | cut -c7-)" # cuts first 6 characters
    mv "$name" "$newname"
done
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

## SQL

### Profiling

```sql
SET profiling = 1;
```

Execute your query, then list profiled queries;

```sql
SHOW PROFILES;
```

Choose which profile you'd like to see in detail, then:

```sql
SHOW PROFILE FOR QUERY 1;
```

### Indexes:

Create an index:

```sql
CREATE INDEX idx_will_be_indexed ON page (will_be_indexed);
```

[Create a partial index:](https://www.databasejournal.com/features/mysql/article.php/3840606/Maximizing-Query-Performance-through-Column-Indexing-in-MySQL.htm)

```sql
CREATE INDEX index_name ON table_name (field_name(prefix_length));
```

Create a [unique](https://stackoverflow.com/questions/707874/differences-between-index-primary-unique-fulltext-in-mysql) index:

```sql
CREATE UNIQUE INDEX idx_token ON user (token);
```

See what indexes use query:

```sql
EXPLAIN SELECT ...
```

List all indexes:

```sql
SHOW INDEX FROM page;
```

Delete an index:

```sql
DROP INDEX index_name ON table_name
```

#### Difference Between Index Types:

* **KEY or INDEX** refers to a normal non-unique index. Non-distinct values for the index are allowed, so the index may contain rows with identical values in all columns of the index. These indexes don't enforce any restraints on your data so they are used only for making sure certain queries can run quickly.

* **UNIQUE** refers to an index where all rows of the index must be unique. That is, the same row may not have identical non-NULL values for all columns in this index as another row. As well as being used to speed up queries, UNIQUE indexes can be used to enforce restraints on data, because the database system does not allow this distinct values rule to be broken when inserting or updating data. Your database system may allow a UNIQUE index to be applied to columns which allow NULL values, in which case two rows are allowed to be identical if they both contain a NULL value (the rationale here is that NULL is considered not equal to itself). Depending on your application, however, you may find this undesirable: if you wish to prevent this, you should disallow NULL values in the relevant columns.

* **PRIMARY** acts exactly like a UNIQUE index, except that it is always named 'PRIMARY', and there may be only one on a table (and there should always be one; though some database systems don't enforce this). A PRIMARY index is intended as a primary means to uniquely identify any row in the table, so unlike UNIQUE it should not be used on any columns which allow NULL values. Your PRIMARY index should be on the smallest number of columns that are sufficient to uniquely identify a row. Often, this is just one column containing a unique auto-incremented number, but if there is anything else that can uniquely identify a row, such as "countrycode" in a list of countries, you can use that instead. Some database systems (such as MySQL's InnoDB) will store a table's records on disk in the order in which they appear in the PRIMARY index.

* **FULLTEXT** indexes are different from all of the above, and their behaviour differs significantly between database systems. FULLTEXT indexes are only useful for full text searches done with the MATCH() / AGAINST() clause, unlike the above three - which are typically implemented internally using b-trees (allowing for selecting, sorting or ranges starting from left most column) or hash tables (allowing for selection starting from left most column).

### Alter Table

Add a column;

```sql
ALTER TABLE `table` ADD COLUMN `created_at` BIGINT(20) NULL DEFAULT 0 AFTER `page_id`;
```

Rename a column:

```sql
ALTER TABLE `page` CHANGE `page_language` `language` VARCHAR(255) COLLATE utf8mb4_unicode_ci;
```

Remove a column:

```sql
ALTER TABLE `page` DROP COLUMN `content_language`;
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

#### Defining Variables

```make
$(eval missingPackages := `grep -oFf /tmp/.snt-go-pkgs Gopkg.lock`)
```

#### Conditions

```make
@if [ "$(missingPackages)" = "" ]; then\
  echo "Gopkg.lock looks good.";\
else \
  echo "Gopkg.lock is missing $(missingPackages)"; \
  exit 1;\
fi
```

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

## Decimal & Binary Conversion

Example Number: 13

* List the powers of two. (E.g 1 2 4 8 16 32 64 128 256 ...)
* Take the largest power of two less than or equal to 13; 8.
* 13=8+5. Take the largest power of two less than or equal to 5; 4.
* Result: 13=8+4+1

After breaking down the decimal into digits, we can find out the binary representation
by listing radix and marking each digit if it exists in the values we found above;
the result will be 1101.

More example conversions:

| Decimal | Digits | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| --- | ---  | --- | --- | --- | --- | --- | --- | --- |
| 13 | 8, 4, 1 | | | | 1 | 1 | 0 | 1 |
| 114 | 64, 32, 16, 2 | 1 | 1 | 1 | 0 | 0 | 1 | 0 |

## Bitwise Operations

| Operator | Symbol | Description |
| --- | --- | --- |
| And | & | If both LHS and RHS are 1, then the result will be 1, in all other cases result will be 0 |
| Or | \| | If both LHS and RHS are 0 then the result will be 0, in all other cases result will be 1 |
| Exclusive Or | ^ | If both LHS and RHS are same then the result will be 0, otherwise the result will be 1 |
| Complement | ~ |  If the given operand is positive integer, then add 1 and change the sign. If the given operand is negative integer, then subtract 1 and change the sign. |
| Left Shift | << | Shifts the bits of first number to left by number of positions indicated by second number |
| Right Shift | >> |     |

### `And`, `Or` and `Exclusive Or`

Get the binary equivalent of two numbers and apply the rule to their digits.

For example, 2 | 5:

| Decimal       |  16 |   8 |   4 |   2 |   1 |
| ---           | --- | --- | --- | --- | --- |
| 2             |   0 |   0 |   0 |   1 |   0 |
| 5             |   0 |   0 |   1 |   0 |   1 |
| 4 + 2 + 1 = 7 |   0 |   0 |   1 |   1 |   1 |

### Left / Right Shift

Shift given N number X times to left or right positions.

For example, 1 << 4;

|               | Decimal |  16 |   8 |   4 |   2 |   1 |
| ---           |     --- | --- | --- | --- | --- | --- |
| Input         |       1 |   0 |   0 |   0 |   0 |   1 |
| Output:       |      16 |   1 |   0 |   0 |   0 |   0 |

Another example, 7 << 2

|         | Decimal |  64 |  32 |  16 |   8 |   4 |   2 |   1 |
| ---     |     --- | --- | --- | --- | --- | --- | --- | --- |
| Input   |       7 |   0 |   0 |   0 |   0 |   1 |   1 |   1 |
| Output: |      28 |   0 |   0 |   1 |   1 |   1 |   0 |   0 |
