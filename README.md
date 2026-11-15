# 拾光 · 版本清单

本仓库**仅存放 `version.json`**，用于「拾光」APP 内的「检查更新」功能读取。

- 主应用代码仓库保持私有，本仓库不含任何业务代码或用户数据。
- APP 依次从 jsDelivr CDN 与 GitHub raw 读取 `version.json`，读取失败时自动降级，不影响任何本地功能。

## 字段说明

| 字段 | 说明 |
| --- | --- |
| `version` | 最新版本号（语义化，如 `4.8.0`） |
| `versionCode` | Android versionCode |
| `publishedAt` | 发布时间（ISO 8601） |
| `notes` | 更新日志简要（纯文本，`·` 开头为条目） |
| `pageUrl` | 发布页地址 |
| `apkUrl` | 直链下载地址，留空则使用 `pageUrl` |
