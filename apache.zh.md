[TOC]


## `Alias`

`Alias` 配置的顺序**千万**不能乱。如：

```apacheconf
# 正确
Alias /parent/child1/ "/path/to/child/1"
Alias /parent/child2/ "/path/to/child/2"
Alias /parent/        "/path/to/parent"
```

如果将其倒转：

```apacheconf
# 错误
Alias /parent/        "/path/to/parent"
Alias /parent/child1/ "/path/to/child/1"
Alias /parent/child2/ "/path/to/child/2"
```

就会出错：

```text
The Alias directive in /some/httpd.conf at line 5 will probably never match because it overlaps an earlier Alias
```
