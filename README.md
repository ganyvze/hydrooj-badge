# HydroOJ Badge Plugin

为 HydroOJ 添加用户徽章管理功能的插件。

## 功能特性

- **徽章展示**：展示所有拥有徽章的用户列表
- **徽章创建**：为指定用户创建自定义徽章（支持自定义文本、背景色、文字颜色）
- **徽章管理**：管理员可以查看和删除用户的徽章
- **权限控制**：基于 HydroOJ 权限系统，区分普通用户和管理员操作

## 安装

```bash
# 在 HydroOJ 根目录下
npm install hydrooj-badge
```

或在 `package.json` 中添加依赖：

```json
{
  "dependencies": {
    "hydrooj-badge": "^0.0.1"
  }
}
```

## 配置

在 HydroOJ 的配置文件中启用插件：

```yaml
plugins:
  badge:
    enabled: true
```

## 使用说明

### 路由说明

| 路由 | 方法 | 权限要求 | 说明 |
|------|------|----------|------|
| `/badge` | GET | PRIV_USER_PROFILE | 查看所有拥有徽章的用户 |
| `/badge/create` | GET/POST | PRIV_CREATE_DOMAIN | 创建新徽章（管理员） |
| `/badge/manage` | GET | PRIV_CREATE_DOMAIN | 管理徽章（管理员） |
| `/badge/manage/:uid/del` | GET | PRIV_CREATE_DOMAIN | 删除指定用户的徽章 |

### 创建徽章

1. 访问 `/badge/create` 页面
2. 输入用户的 UID 或用户名
3. 设置徽章文本（会自动过滤引号字符）
4. 设置背景颜色（HEX 格式，如 `#569CD6`）
5. 设置文字颜色（HEX 格式，如 `#FFFFFF`）
6. 提交创建

### 徽章格式

徽章信息存储在用户模型的 `badge` 字段中，格式为：
```
文本 + 背景色 + 文字颜色
```

例如：`管理员#FF0000#FFFFFF`

### 权限说明

- **普通用户**：可以查看所有徽章（`/badge`）
- **管理员**（需要 `PRIV_CREATE_DOMAIN` 权限）：
  - 创建徽章
  - 管理徽章
  - 删除徽章

## 技术实现

- **数据存储**：徽章信息存储在 HydroOJ 的 UserModel 中
- **前端展示**：使用 Nunjucks 模板渲染徽章样式
- **颜色验证**：支持 3 位或 6 位 HEX 颜色码

## 开发信息

- **作者**：33DAI
- **版本**：0.0.1
- **许可证**：AGPL-3.0
- **主文件**：index.ts

## 注意事项

1. 如果用户已有徽章，创建新徽章会覆盖原有徽章
2. 颜色码必须是有效的 HEX 格式（如 `#FFF` 或 `#FFFFFF`）
3. 徽章文本会自动过滤单引号和双引号字符
4. 删除徽章操作不可恢复，请谨慎操作

## 截图

（可选：添加插件界面截图）

## 贡献

欢迎提交 Issue 和 Pull Request！

## 相关链接

- [HydroOJ 官方文档](https://hydro.ac/docs)
- [问题反馈](https://github.com/your-repo/hydrooj-badge/issues)
