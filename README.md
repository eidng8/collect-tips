[简体中文](README.zh.md) [繁体中文](README.zh-Hant.md)


## [Haroopad](http://pad.haroopress.com/user.html)

![Haroopad Logo](http://pad.haroopress.com/assets/images/logo-small.png)
The Markdown editor I use. There are many similar products out there, each with their own strength. I choose it for cross platform, the nice TOC feature, and it's free. :smirk:


## [GitHub](http://github.com/)

The almighty, you know, nothing more to say.

Looking forward to using the anticipated [TOC](https://github.com/isaacs/github/issues/215).

And the clients:

```text
http://windows.github.com/
https://mac.github.com/
https://mobile.github.com/
```

Or from git-scm

```text
http://git-scm.com/downloads
```


## Subjects

### [Apache HTTP](apache.md)

### [JavaScript](js.md)

### [Mac OS](macos.md)

### [Nginx](nginx.md)

### [HTML]
[List of HTML Entities](html-entities.html)

### [PHP](php.md)

### [Swift](swift.md)

### [Tools](tools.md)

### [Public Mirrors](mirrors.md)

### RDBMS

#### SQL-99 feature differences

##### Recursive Query

https://en.wikipedia.org/wiki/Hierarchical_and_recursive_queries_in_SQL

```sql
WITH RECURSIVE ttt (c1, c2, /*c3, ...., cN*/) AS (
  /* anchor query: The starting point of the recursion */
  UNION ALL
  /* recursive query: The part of the query that refers back to the common table expression itself */
)
-- Main query that utilizes common table expression
SELECT * FROM ttt;
```

###### Supported by

* PostreSQL
* Oracle 11g,
* IBM DB2
* Microsoft SQL Server
* Apache Derby
* MySQL 8+
* SQLite 3.34+ ?

###### NOT supported by

* MySQL 5.x
* SQLite
* Informix
* Firebird
  
