# 匹配规则

## MosDNS 匹配规则

- **domain:**  
  匹配指定域名及其子域名。  
  示例：`domain:google.com` 匹配 `google.com`、`www.google.com`、`maps.l.google.com` 等。

- **full:**  
  仅匹配完全相同的域名。  
  示例：`full:google.com` 仅匹配 `google.com`。

- **keyword:**  
  匹配包含指定关键字的域名。  
  示例：`keyword:google.com` 匹配 `google.com.hk`、`www.google.com.hk` 等。

- **regexp:**  
  使用 Golang 标准正则表达式匹配域名。  
  示例：`regexp:.+\.google\.com$` 匹配以 `.google.com` 结尾的域名。

- **匹配优先级：**  
  规则按以下顺序生效：`full` > `domain` > `regexp` > `keyword`。

- **性能：**  
  - `domain` 和 `full` 使用 HashMap，复杂度 O(1)。约 1 万个域名占用 1MB 内存。  
  - `keyword` 和 `regexp` 需要遍历，复杂度 O(n)。注意：`regexp` 正则匹配消耗资源较多。

## Mihomo 匹配规则

- **DOMAIN-SUFFIX:**  
  匹配指定域名及其子域名。  
  示例：`google.com` 匹配 `www.google.com`、`mail.google.com` 和 `google.com`，但不匹配 `content-google.com`。

- **DOMAIN:**  
  仅匹配完全相同的域名。  
  示例：`google.com` 仅匹配 `google.com`。

- **DOMAIN-KEYWORD:**  
  匹配包含指定关键字的域名。  
  示例：`google.com` 匹配 `google.com.hk`、`www.google.com.hk` 等。

- **DOMAIN-REGEX:**  
  使用正则表达式匹配域名。  
  示例：正则模式 `.+\.google\.com$` 匹配以 `.google.com` 结尾的域名。