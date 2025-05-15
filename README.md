# 匹配规则指南

## MosDNS 规则

### 直连规则
- `china_list.txt` - 中国域名列表  
- `custom_direct.txt` - 自定义直连规则  
- `tracker.txt` - 追踪器域名  
- `tesla.txt` - Tesla 相关域名  
- `local_ptr.txt` - 本地 PTR 记录

### 代理规则
- `proxy_list.txt` - 代理域名列表  
- `custom_proxy.txt` - 自定义代理规则  
- `telegram.txt` - Telegram 相关域名

### 匹配类型
| 类型     | 说明 | 示例 |
|----------|------|------|
| `domain` | 匹配域名及其子域名 | `google.com` 匹配 `www.google.com` |
| `full`   | 精确匹配域名 | 仅匹配 `google.com` |
| `keyword`| 包含关键字的域名 | 匹配 `google.com.hk` |
| `regexp` | Golang 正则匹配 | `.+\.google\.com$` |

### 注意事项
1. **优先级**：`full` > `domain` > `regexp` > `keyword`
2. **性能**：
   - `domain`/`full`：O(1) 复杂度，1万域名≈1MB内存
   - `keyword`/`regexp`：O(n) 复杂度，正则较耗资源

## Mihomo 规则
| 类型            | 对应 MosDNS 类型 | 示例 |
|-----------------|------------------|------|
| `DOMAIN-SUFFIX` | `domain`         | `google.com` 匹配子域名 |
| `DOMAIN`        | `full`           | 仅匹配 `google.com` |
| `DOMAIN-KEYWORD`| `keyword`        | 匹配含关键字的域名 |
| `DOMAIN-REGEX`  | `regexp`         | 正则表达式匹配 |