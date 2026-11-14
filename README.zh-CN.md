# Shopify Develop —— Dawn 主题学习仓库

[English](./README.md) | 中文

本仓库基于 Shopify 官方开源主题 **Dawn 16.1.1**（`main` 分支）克隆，用于本地研读与二次开发练习。英文版说明见 [README.md](./README.md)。

> 原始主题版权归 Shopify Inc. 所有，许可证见 [LICENSE.md](./LICENSE.md)。本仓库仅作个人学习用途；二次开发后如需上架 Theme Store，须满足与 Dawn 实质差异化等官方要求。

## 仓库背景

- **基线版本**：Dawn 16.1.1（对应提交 `3e9ee228`）
- **远程配置**：

  | 远程名 | 地址 | 用途 |
  | --- | --- | --- |
  | `origin` | `https://github.com/wahahalala/Shopify_develop.git` | 个人仓库，日常推送 / 拉取使用 |
  | `upstream` | `https://github.com/Shopify/dawn.git` | Shopify 官方上游，用于跟进官方更新 |

## 目录结构

Dawn 是 Online Store 2.0 主题，遵循 Shopify 主题标准目录约定：

| 目录 / 文件 | 作用 |
| --- | --- |
| `layout/` | 全局布局模板（如 `theme.liquid` 站点骨架、`password.liquid` 密码页） |
| `templates/` | 页面入口模板，以 JSON 模板为主，如 `index.json`、`product.json`、`collection.json`、`cart.json`、`search.json` |
| `sections/` | 页面区块，可在模板中被引用、复用与排序（48 个文件） |
| `snippets/` | 可复用的 Liquid 代码片段（39 个文件） |
| `assets/` | 静态资源：CSS、JavaScript、图片、SVG 等（191 个文件） |
| `config/` | 主题设置定义（`settings_schema.json`）与默认设置数据（`settings_data.json`） |
| `locales/` | 多语言翻译文件（`.json`）及对应 schema |
| `.github/workflows/` | GitHub Actions：Theme Check、Lighthouse、CLA 校验 |
| `.theme-check.yml` | Theme Check 静态检查规则开关 |
| `release-notes.md` | 各版本发布说明 |

## 本地开发

### 前置要求

- 安装 [Shopify CLI](https://github.com/Shopify/shopify-cli)（Node.js 环境）
- 一个可用于开发的 Shopify 开发商店（Development Store）

### 常用命令

```bash
# 启动本地开发服务器，实时预览主题修改
shopify theme dev

# 把本地主题推送到指定店铺
shopify theme push

# 运行 Theme Check 静态代码检查
shopify theme check
```

### 代码规范

- 格式化工具：Prettier（配置见 `.prettierrc.json`）
- 代码检查：Theme Check，规则开关见 `.theme-check.yml`

## 同步官方上游更新

当需要把 Shopify 官方 Dawn 的最新改动合并到本仓库时：

```bash
# 1. 拉取上游最新代码
git fetch upstream

# 2. 把 upstream/main 合并到本地当前分支
git merge upstream/main

# 3. 解决冲突后推送到个人仓库
git push origin main
```

## 提交与推送

```bash
# 查看状态
git status

# 暂存改动并提交
git add .
git commit -m "提交说明"

# 推送到个人仓库（origin/main 已建立跟踪）
git push
```

## CI 与 Secrets

`.github/workflows/ci.yml` 中的 Lighthouse 工作流通过 GitHub Secrets 读取店铺地址、访问令牌等配置（如 `SHOP_STORE_OS2`、`SHOP_ACCESS_TOKEN`、`LHCI_GITHUB_TOKEN`）。这些敏感值**不写入仓库文件**；在本个人仓库中如需启用对应工作流，需到仓库 **Settings → Secrets and variables → Actions** 中自行配置同名 Secrets。

## 安全说明

- 仓库内不含 `.env`、私钥、证书、硬编码 Token 或店铺域名等明文私密信息。
- 本地 Git 凭据由系统凭据管理器保存，不要把个人访问令牌（Personal Access Token）提交或写入仓库。
