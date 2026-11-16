# 拾光 · APK 发布仓库（公开）

这是「拾光」APP 的**官方发布渠道**：

- ✅ 每个版本的 **APK 安装包**（挂在 Releases，匿名可直接下载）
- ✅ **更新日志**（本页下方 + `CHANGELOG.md` + `version.json`）
- ❌ **不含源代码**——主仓库保持私有，本仓库只有清单与文档，没有任何业务代码

## 下载

**最新版：[v5.2.0](https://github.com/sageramboleo/shiguang-updates/releases/latest)** —— 进入后下载 `Shiguang-v5.2-debug.apk` 安装即可。

历史版本在 [Releases 列表](https://github.com/sageramboleo/shiguang-updates/releases)。

> 安装提示：这是 debug 签名包，安装时系统可能提示「未知来源」，允许即可；
> 覆盖安装升级不会丢失本地数据（数据在应用私有目录与备份 zip 中）。

## APP 内检查更新是怎么工作的

1. APP 读取本仓库的 `version.json`（jsDelivr CDN 优先，GitHub raw 兜底）
2. 比较版本号，有新版本就弹出更新日志与下载入口
3. 下载链接直指本仓库 Release 附件，浏览器打开即下
4. 读取失败一律静默降级，不影响任何本地功能

## 字段说明（version.json）

| 字段 | 说明 |
| --- | --- |
| `version` | 最新版本号（语义化，如 `5.2.0`） |
| `versionCode` | Android versionCode |
| `publishedAt` | 发布时间（ISO 8601） |
| `notes` | 更新日志简要（纯文本，`·` 开头为条目） |
| `pageUrl` | 发布页地址 |
| `apkUrl` | APK 直链（本仓库 Release 附件） |
| `history` | 最近几个版本的摘要，APP 内「更新日志」弹窗会展示 |

## 发版流程

```bash
# 1. 更新 version.json（version / versionCode / notes / apkUrl / history）与 CHANGELOG.md
vim version.json CHANGELOG.md

# 2. 提交推送
git add -A && git commit -m "release: v5.x.0" && git push

# 3. 在本仓库创建 Release 并上传 APK
gh release create v5.x.0 Shiguang-v5.x-debug.apk --title "..." --notes-file notes.md

# 4. 刷新 CDN 缓存（关键，否则 jsDelivr 最长 12 小时仍返回旧版本）
curl "https://purge.jsdelivr.net/gh/sageramboleo/shiguang-updates@main/version.json"

# 5. 验证
curl -s "https://cdn.jsdelivr.net/gh/sageramboleo/shiguang-updates@main/version.json" | head -5
```
