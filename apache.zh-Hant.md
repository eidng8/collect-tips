[TOC]


## `Alias`

`Alias` 配置的順序**千萬**不能亂。如：

```apacheconf
# 正確
Alias /parent/child1/ "/path/to/child/1"
Alias /parent/child2/ "/path/to/child/2"
Alias /parent/        "/path/to/parent"
```

如果將其倒轉：

```apacheconf
# 錯誤
Alias /parent/        "/path/to/parent"
Alias /parent/child1/ "/path/to/child/1"
Alias /parent/child2/ "/path/to/child/2"
```

就會出錯：

```text
The Alias directive in /some/httpd.conf at line 5 will probably never match because it overlaps an earlier Alias
```
