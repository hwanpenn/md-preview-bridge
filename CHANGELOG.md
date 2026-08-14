# Changelog

本项目遵循 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/) 规范，
版本号遵循 [Semantic Versioning](https://semver.org/lang/zh-CN/)。

## [0.1.3] - 2026-08-14

### 修复

- 🐛 **修复命令不可用**：修正打包时 `--no-dependencies` 导致 `ws` 模块未被包含进 `.vsix`，插件激活失败，`mdPreviewBridge.openInBrowser` 命令无法注册

## [0.1.2] - 2026-08-05

### 新增

- 🔌 **端口自动回退**：默认端口被占用时自动尝试 5180 ~ 5199，避免"点了图标浏览器打开一片空白"
- 🕵️ **占用者智能识别**：通过 `/__bridge_ping` 特征端点区分"是我们自己的另一个实例"还是"陌生程序"，给出针对性提示
- ⏰ **空闲自动回收**：无浏览器连接超过 30 分钟自动关服释放端口，节省系统资源；下次点击图标自动重启
- ⚙️ 新增配置项 `mdPreviewBridge.idleShutdownMinutes`（默认 30，设为 0 关闭自动回收）
- 📁 **资源管理器右键菜单**：在左侧文件树右键 `.md` / `.markdown` 文件即可打开预览
- 📝 **编辑器右键菜单**：编辑 Markdown 时右键也能直达预览

### 变更

- 命令标题精简为 `MD Preview: 在浏览器打开`（原 `... 打开当前 Markdown`）
- 服务启动失败时不再打开浏览器（原来会打到错误页），改为弹出明确错误提示

## [0.1.1] - 2026-08-05

### 变更

- 修正 `repository` / `bugs` / `homepage` 字段为真实 GitHub 地址（`hwanpenn/md-preview-bridge`）
- 为 Open VSX namespace 认证做准备

## [0.1.0] - 2026-08-05

### 新增

- 🌐 一键在系统默认浏览器打开当前 Markdown 文件（编辑器右上角图标 / 状态栏 / 命令面板）
- 🔗 双向实时同步：
  - VSCode 保存 / 外部工具修改 → 浏览器自动刷新
  - 浏览器 `Cmd+S` → 直接写回原文件，VSCode 自动 reload
- 🛡️ 冲突检测：磁盘 mtime 比对 + VSCode dirty 检查，拒绝覆盖未合并修改
- 📎 自动跟随：切换 md tab / 关闭 tab / 外部删除均能感知
- 🎨 前端支持 GFM（表格、任务列表、删除线、代码高亮），三种预览模式（编辑 / 双栏 / 预览）
- 🖱️ 双栏模式支持自定义拖拽条调节两栏宽度，比例持久化到 localStorage
- ⚙️ 可配置端口 `mdPreviewBridge.port`（默认 5179）
