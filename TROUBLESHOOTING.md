# GitHub Pages 域名 404 错误解决方案

## 问题分析

访问 `https://wapxlw.github.io/tousu/ENT20250911NSBWN3CZ/REMpPIuh2c` 时出现404错误，主要原因：

1. **GitHub Pages域名未在系统中配置**
2. **通道可能不存在或未激活**
3. **前端路由配置不完整**

## 解决步骤

### 第一步：配置GitHub Pages域名

1. 登录后端管理系统：`https://qyts.wosb.cn/login.php`
2. 进入"域名管理"页面
3. 启用GitHub Pages功能（如果未启用）
4. 添加GitHub Pages域名：
   - 域名：`wapxlw.github.io`
   - GitHub用户名：`wapxlw`
   - 仓库名称：`tousu`（根据实际仓库名称修改）
   - 分支：`gh-pages` 或 `main`
   - 状态：启用

### 第二步：验证通道配置

1. 进入"通道管理"页面
2. 查找通道SN：`REMpPIuh2c`
3. 确认：
   - 通道状态为"激活"
   - 企业ID为 `ENT20250911NSBWN3CZ`
   - 域名类型设置为"GitHub Pages域名模式"

### 第三步：前端文件部署

确保以下文件已正确部署到GitHub Pages：

1. ✅ `404.html` - 处理SPA路由重定向
2. ✅ `index.html` - 包含路由恢复逻辑
3. ✅ `assets/js/app.js` - API配置已更新

### 第四步：验证配置

访问以下URL进行测试：

1. **直接访问首页**：`https://wapxlw.github.io/`
2. **访问投诉页面**：`https://wapxlw.github.io/ENT20250911NSBWN3CZ/REMpPIuh2c`
3. **访问投诉须知**：`https://wapxlw.github.io/ENT20250911NSBWN3CZ/REMpPIuh2c/notice`

## 技术说明

### GitHub Pages SPA路由处理

GitHub Pages是静态网站托管，不支持服务器端路由。我们使用以下方案：

1. **404.html重定向**：当访问不存在的路径时，GitHub Pages显示404.html
2. **sessionStorage存储**：404.html将路径信息保存到sessionStorage
3. **重定向到index.html**：自动跳转到主页面
4. **路径恢复**：index.html从sessionStorage恢复原始路径

### API配置

前端通过以下配置与后端通信：

```javascript
const API_CONFIG = {
    BASE_URL: 'https://qyts.wosb.cn',
    endpoints: {
        complaint: '/api/complain.php',
        complaintTypes: '/api/get_complaint_types.php',
        // ... 其他接口
    }
};
```

## 常见问题

### Q: 仍然出现404错误？
A: 请检查：
1. GitHub Pages域名是否已在后端系统中添加
2. 通道状态是否为激活
3. GitHub Pages部署是否完成（通常需要几分钟）

### Q: 页面显示但功能不正常？
A: 请检查：
1. 浏览器开发者工具的网络请求
2. API接口是否返回正确数据
3. 跨域配置是否正确

### Q: 如何查看详细错误信息？
A: 打开浏览器开发者工具（F12），查看Console和Network标签页的错误信息。

## 联系支持

如果问题仍然存在，请提供以下信息：
1. 浏览器开发者工具的错误截图
2. 网络请求的响应数据
3. 具体的访问时间和步骤