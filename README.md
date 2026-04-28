# WindsurfGate

> Windsurf IDE 多账号管理插件

**作者：执**

---

## 这是什么

一个直接装在 Windsurf 里的小工具。让你在多个 Windsurf 账号之间一键切来切去，不用每次重新登录、不用手动改配置。

## 能做什么

- **一键切号** — 点一下按钮换账号，Windsurf 自动重新登录
- **批量添加 / 导入** — 一次性把一堆账号粘进来或从 `.txt` 文件导入，10 个并发处理
- **配额查询** — 自动看每个账号的日 / 周用量，到期日期一目了然
- **多种登录方式**
  - Session Token / Auth1 Token — 粘进来自动识别
  - 邮箱密码 — 走 Devin 登录流程
  - 也能从 `.txt` 文件成批读
- **机器码自动重置** — 切号同时自动换机器码，干净
- **JSON 导入导出** — 备份、迁移、分享都方便

## 怎么装

把 `windsurf-gate-2.0.9.vsix` 文件拖进 Windsurf 安装就完事。

或者命令行：

```bash
windsurf --install-extension windsurf-gate-2.0.9.vsix
```

装完左侧栏会出现 WindsurfGate 图标，点进去就能用。

## 怎么用

### 添加账号

点顶部的 **+ 添加账号** 按钮：

- **Session Token 标签页**（默认） — 把 token 粘进去，可批量
  - 支持 `devin-session-token$xxx`
  - 支持 `auth1_xxx`
  - 支持 `账号----密码` 格式（`emailA----passwordA` 一行一对）
  - 多种格式可以混着粘，自动识别
- **邮箱密码标签页** — 单条添加（用 Devin 邮密登录）

### 切换账号

点账号卡片右边的双箭头按钮 → 直接切。

点账号卡片本身 = 选中（不切号），上方浮出操作栏：复制邮箱 / 复制信息 / 删除。

### 邮箱 / apiKey 直接复制

- 卡片上的邮箱字段 — 点一下复制邮箱
- 邮箱下面的 apiKey 缩写 — 点一下复制完整 apiKey

### 导入 / 导出

顶部 **导出** / **导入** 按钮。导出是 JSON。导入支持 JSON 和纯 `.txt`（每行一个 token / 一对邮密）。

## macOS 用户：去掉切号确认弹框（可选）

切号默认会被 Windsurf 弹一下 "Are you sure" 二次确认，点 Yes 就过。如果想完全无感切号，跑一次：

```bash
sudo bash scripts/patch-bypass-confirm.sh
```

需要在 **系统设置 → 隐私与安全性 → 应用程序管理** 里给"终端"打勾。

跑完完全退出 Windsurf 重新打开 → 之后切号 0 弹框 0 密码。

还原：
```bash
sudo bash scripts/patch-bypass-confirm.sh --restore
```

## 常见问题

**切号说"账号缺少凭证"？**

这账号是 IDE 自动从你当前登录态导入的，没存切号 token。删掉它，用 Session Token 重新加一遍就好。

**配额刷新失败？**

可能是 token 过期了，重新加一次该账号即可。

**Windsurf 升级后切号又弹"Are you sure"？**

Windsurf 升级会覆盖 `extension.js`，重新跑一次上面那条 patch 脚本就行。

---

**作者：执**

仓库：<https://github.com/Yuy-0415/WindsurfGateVsix>
