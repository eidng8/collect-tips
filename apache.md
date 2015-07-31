[TOC]


## `Alias`

The order of `Alias` is **significant** for nested aliases. Say

```apacheconf
# this is correct
Alias /parent/child1/ "/path/to/child/1"
Alias /parent/child2/ "/path/to/child/2"
Alias /parent/        "/path/to/parent"
```

The aobve yields the desired mapping. If the order is reversed to

```apacheconf
# this is wrong
Alias /parent/        "/path/to/parent"
Alias /parent/child1/ "/path/to/child/1"
Alias /parent/child2/ "/path/to/child/2"
```

You'll get error like

```text
The Alias directive in /some/httpd.conf at line 5 will probably never match because it overlaps an earlier Alias
```
