# 拾光 · 版本清单

本仓库**仅存放 `version.json`**，用于「拾光」APP 内的「检查更新」功能读取。

- 主应用代码仓库保持私有，本仓库不含任何业务代码或用户数据。
- APP 依次从 jsDelivr CDN 与 GitHub raw 读取 `version.json`，读取失败时自动降级，不影响任何本地功能。

## 字段说明

| 字段 | 说明 |
| --- | --- |
| `version` | 最新版本号（语义化，如 `4.9.0`） |
| `versionCode` | Android versionCode |
| `publishedAt` | 发布时间（ISO 8601） |
| `notes` | 更新日志简要（纯文本，`·` 开头为条目，建议 4-6 条） |
| `pageUrl` | 发布页地址 |
| `apkUrl` | 直链下载地址，留空则使用 `pageUrl` |

## 发版流程（重要）

每次发布新版本，**必须**同步更新本仓库，否则客户端检查不到更新：

```bash
# 1. 改 version / versionCode / publishedAt / notes / pageUrl
vim version.json

# 2. 提交并推送
git add version.json
git commit -m "release: v4.9.0"
git push

# 3. 刷新 CDN 缓存（关键，否则 jsDelivr 仍返回旧版本，最长 12 小时）
curl "https://purge.jsdelivr.net/gh/sageramboleo/shiguang-updates@main/version.json"

# 4. 验证已生效
curl -s "https://cdn.jsdelivr.net/gh/sageramboleo/shiguang-updates@main/version.json" | head -5
```

> jsDelivr 对 `@main` 分支有长时间缓存，第 3 步的 purge 不能省。
> 客户端虽然带了时间戳参数，但 CDN 缓存键不含 query，仍需服务端刷新。
