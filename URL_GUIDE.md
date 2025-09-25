# GitHub Pages URL 配置指南

## 新的访问格式

由于GitHub Pages不支持动态路径，我们改用URL参数的方式：

### 方案一：简洁参数格式（推荐）
```
https://wapxlw.github.io/tousu/?e=ENT20250911NSBWN3CZ&c=REMpPIuh2c
```

### 方案二：完整参数格式
```
https://wapxlw.github.io/tousu/?enterprise=ENT20250911NSBWN3CZ&channel=REMpPIuh2c
```

## 参数说明

| 参数 | 完整名称 | 说明 | 示例值 |
|------|----------|------|--------|
| `e` | `enterprise` | 企业ID | `ENT20250911NSBWN3CZ` |
| `c` | `channel` | 通道SN | `REMpPIuh2c` |
| `page` | `page` | 页面类型（可选） | `notice`（投诉须知页面） |

## 页面访问示例

### 1. 投诉表单页面
```
https://wapxlw.github.io/tousu/?e=ENT20250911NSBWN3CZ&c=REMpPIuh2c
```

### 2. 投诉须知页面
```
https://wapxlw.github.io/tousu/?e=ENT20250911NSBWN3CZ&c=REMpPIuh2c&page=notice
```

## 后端系统配置

在后端系统中创建通道时，请使用以下链接格式：

### GitHub Pages域名模式链接生成
```php
// 在 Utils.php 中的 generateChannelLink 方法
public static function generateChannelLink($enterpriseId, $channelSn, $domainType = 'short_link') {
    if ($domainType === 'github_pages') {
        // GitHub Pages域名列表
        $githubPagesDomains = self::getActiveGitHubPagesDomains();
        if (!empty($githubPagesDomains)) {
            $domain = $githubPagesDomains[0]; // 使用第一个可用域名
            return "https://{$domain['domain']}/?e={$enterpriseId}&c={$channelSn}";
        }
    }
    
    // 短链域名逻辑...
}
```

## 技术实现

### 前端URL解析优先级
1. **URL参数优先**：`?e=xxx&c=xxx`
2. **路径参数兼容**：`/tousu/ENT20250911NSBWN3CZ/REMpPIuh2c`（仍保留支持）

### 页面路由处理
- 默认显示投诉表单页面
- 当URL包含 `page=notice` 时显示投诉须知页面
- 页面间跳转保持URL参数

## 优势

1. **兼容性好**：URL参数格式在所有静态托管平台都能正常工作
2. **SEO友好**：搜索引擎能正确索引带参数的页面
3. **易于分享**：用户可以直接复制粘贴完整URL
4. **调试方便**：参数在地址栏中清晰可见，便于排查问题

## 迁移说明

### 原有路径格式仍然支持
为了向后兼容，以下格式仍然有效：
- `/tousu/ENT20250911NSBWN3CZ/REMpPIuh2c`
- 通过404.html重定向机制转为参数格式

### 推荐使用新格式
在生成新的投诉链接时，建议使用参数格式，确保最佳的兼容性和稳定性。