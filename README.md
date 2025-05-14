# Rule

## Mosdns匹配规则

- 以 domain: 开头，域匹配。e.g: domain:google.com 会匹配自身 google.com，以及其子域名 www.google.com, maps.l.google.com 等。

- 以 full: 开头，完整匹配。e.g: full:google.com 只会匹配自身。

- 以 keyword: 开头，关键字匹配。e.g: keyword:google.com 会匹配包含这个字段的域名，如 google.com.hk, www.google.com.hk。

- 以 regexp: 开头，正则匹配(Golang 标准)。e.g: regexp:.+\.google\.com$。

- 匹配方式按如下顺序生效: full > domain > regexp > keyword。

- 性能:

- domain 和 full 匹配使用 HashMap，复杂度 O(1)。每 1w 域名约占用 1M 内存。

- keyword 和 regexp 匹配需遍历，复杂度 O(n)。注意: regexp 正则匹配会消耗大量资源。

## Mihomo 匹配规则

- DOMAIN-SUFFIX 匹配域名后缀 例：google.com匹配www.google.com/mail.google.com和google.com,但不匹配content-google.com

- DOMAIN 匹配完整域名

- DOMAIN-KEYWORD 使用域名关键字匹配

- DOMAIN-REGEX 域名正则表达式匹配