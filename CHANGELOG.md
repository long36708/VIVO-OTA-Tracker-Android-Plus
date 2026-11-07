# 更新日志（Changelog）

本项目遵循语义化版本（见 `docs/VERSIONING.md`），推送 `v*` 标签时由
GitHub Actions 自动构建并发布 Release，本文件记录各版本的功能变化。

## [未发布]

### 新增
- **一键查看 metadata**：分区列表页「包内文件」卡片下新增「查看 metadata」按钮，
  直接定位并预览 `META-INF/com/android/metadata`（机型 / 版本 / 安全补丁等键值信息），
  支持复制全部与下载，不再需要逐层进入 META-INF 目录；包内无该文件时 Toast 提示。
  压缩条目由 `readEntryBytes` 的 inflateRaw 通路直接解压读取
  （`docs/REMOTE_ZIP_STREAM_PARSING.md` §2.8 旁路设计的落地）。
- **粘贴参数查询**：非 root 设备可粘贴真实设备参数（机型代号 / 硬件版本 / 软件版本等）
  查询 OTA 更新。

### 修复
- 分区列表页直接发起的预览 / 下载此前会因未打开过「包内文件」（嵌套导航栈为空）
  取不到数据源而静默失败，现回退到根数据源。

## [1.9.0] - 2026-10-27

### 新增
- **自动检测版本更新**：启动时静默检查 GitHub Releases（24 小时节流），
  发现新版本在首页顶部显示横幅（去更新 / 忽略，忽略后同版本不再弹出）；
  关于页提供手动「检查更新」入口。

## [1.8.0] - 2026-10-27

### 新增
- 不支持机型提醒：未配置或占位版本号的机型在版本号输入框处给出醒目提示。
- 内置版本库批量补充 `default_sw_version`（89 → 174 条）及 `optional_sw_versions`。

### 修复
- vivo OTA 查询兼容修复：平板分支 `vgcCu` 参数、全量包 retcode=210 自动改增量重试、
  GBK 编码错误消息解码。
- 代码评审修复：210 重试改为精确解析 retcode；占位版本判定豁免 vivo S7 / iQOO Z5x
  等老机型的无 `.W` 后缀合法版本号；移除 `default_sw_version` 的 camelCase 死分支。

更早版本的变更见 [GitHub Releases](https://github.com/long36708/VIVO-OTA-Tracker-Android-Plus/releases)。
