<div align="center">
  <a href="README-TR.md">TR <img style="padding-top: 8px" src="https://raw.githubusercontent.com/yammadev/flag-icons/master/png/TR.png" alt="TR" height="20" /></a>
  <a href="README.md"> | EN <img style="padding-top: 8px" src="https://raw.githubusercontent.com/yammadev/flag-icons/master/png/US.png" alt="EN" height="20" /></a>
  <a href="README-DE.md"> | DE <img style="padding-top: 8px" src="https://raw.githubusercontent.com/yammadev/flag-icons/master/png/DE.png" alt="DE" height="20" /></a>
  <a href="README-SA.md"> | AR <img style="padding-top: 8px" src="https://raw.githubusercontent.com/yammadev/flag-icons/master/png/SA.png" alt="AR" height="20" /></a>
  <a href="README-NL.md"> | NL <img style="padding-top: 8px" src="https://raw.githubusercontent.com/yammadev/flag-icons/master/png/NL.png" alt="NL" height="20" /></a>
  <a href="README-AZ.md"> | AZ <img style="padding-top: 8px" src="https://raw.githubusercontent.com/yammadev/flag-icons/master/png/AZ.png" alt="AZ" height="20" /></a>
  <a href="README-CN.md"> | CN <img style="padding-top: 8px" src="https://raw.githubusercontent.com/yammadev/flag-icons/master/png/CN.png" alt="CN" height="20" /></a>
  <a href="README-FR.md"> | FR <img style="padding-top: 8px" src="https://raw.githubusercontent.com/yammadev/flag-icons/master/png/FR.png" alt="FR" height="20" /></a>
  <a href="README-IT.md"> | IT <img style="padding-top: 8px" src="https://raw.githubusercontent.com/yammadev/flag-icons/master/png/IT.png" alt="IT" height="20" /></a>
  <a href="README-RU.md"> | RU <img style="padding-top: 8px" src="https://raw.githubusercontent.com/yammadev/flag-icons/master/png/RU.png" alt="RU" height="20" /></a>
  <a href="README-ES.md"> | ES <img style="padding-top: 8px" src="https://raw.githubusercontent.com/yammadev/flag-icons/master/png/ES.png" alt="ES" height="20" /></a>
</div>

<div align="center">

# DNA Reseller Hosting

**用一个 WiseCP 服务器模块管理 cPanel 与 Plesk 经销商账户。**

一个模块，两种面板。面板类型无需你选择 —— 模块会亲自询问服务器，并记住是哪种面板作出了响应。

![WiseCP](https://img.shields.io/badge/WiseCP-self--hosted-4A90D9?style=flat-square)
![PHP](https://img.shields.io/badge/PHP-7.4%20%E2%80%93%208.4-777BB4?style=flat-square&logo=php&logoColor=white)
![cPanel](https://img.shields.io/badge/cPanel%2FWHM-%E6%94%AF%E6%8C%81-FF6C2C?style=flat-square)
![Plesk](https://img.shields.io/badge/Plesk-%E6%94%AF%E6%8C%81-53BCE6?style=flat-square)

</div>

---

## 📑 目录

- [✨ 功能一览](#-功能一览)
- [📋 环境要求](#-环境要求)
- [🚀 安装](#-安装)
- [🔍 日志与故障排查](#-日志与故障排查)
- [🧩 须知事项](#-须知事项)
- [📄 更新日志](#-更新日志)

---

## ✨ 功能一览

| 功能 | cPanel/WHM | Plesk |
|---|:---:|:---:|
| 连接测试与面板自动识别 | ✅ | ✅ |
| 创建账户 | ✅ | ✅ |
| 暂停 / 恢复 | ✅ | ✅ |
| 删除 | ✅ | ✅ *(校验归属)* |
| 修改密码 | ✅ | ✅ |
| 更换套餐 / 方案 | ✅ | ✅ |
| 磁盘与流量用量同步 | ✅ | ✅ |
| 一键登录客户面板 | ✅ | ✅ |
| 从管理后台一键登录 | ✅ | ✅ |

> 💡 **为经销商而设计。** 无需 root 或管理员权限；模块以你自己的经销商账户权限运行，它创建的每个账户都会
> 占用你的配额。

---

## 📋 环境要求

- 自建的 **WiseCP**，并且你拥有管理员权限
- **PHP** 7.4 – 8.4
- PHP 扩展：`curl`、`simplexml`
- 一个 **cPanel/WHM 经销商账户**（WHM API 令牌）&nbsp;或&nbsp;一个 **Plesk 经销商账户**
  （API 密钥或面板密码）
- 从 WiseCP 服务器到面板服务器、面板 API 端口的出站访问

> ✅ 不创建任何数据库表，不需要 cron，也没有 composer 依赖。安装只是复制一个文件夹而已。

---

## 🚀 安装

### 1️⃣ 部署模块

把 `DNAHosting` 文件夹复制到 WiseCP 安装目录下的 `coremio/modules/Servers/`。

```
wisecp/
└── coremio/
    └── modules/
        └── Servers/
            └── DNAHosting/     ← 放这里
```

### 2️⃣ 添加服务器

**Products / Services → Hosting/Server → Shared Server Settings → Add New Shared Server**

| 字段 | 填写内容 |
|---|---|
| **Server Automation Type** | `DNAHosting` —— 即文件夹名，列表中原样显示 |
| **IP Address** | 面板服务器的真实地址；模块连接的就是这里 |
| **Username** | 你在该面板上的经销商用户名 |
| **Password** | cPanel 填 WHM API 令牌，Plesk 填 API 密钥或面板密码 |
| **Connect with SSL** | 勾选 |
| **Port** | cPanel 用 `2087`，Plesk 用 `8443` |

> ⚠️ **表单顶部的 Hostname 字段只是一个标签。** 模块连接时使用 **IP Address**，而不是它。服务器列表中
> 会以该标签显示你的服务器。

### 3️⃣ 测试连接

保存前点击 **Test Connection**，或者直接保存 —— WiseCP 会自行执行测试。

绿色结果同时确认凭据和识别出的面板。失败时会显示具体的 HTTP 状态码或面板错误；参见
[日志与故障排查](#-日志与故障排查)。

### 4️⃣ 创建服务器组

如果有多台服务器，请在 **Shared Server Settings → Server Groups** 中创建分组，并把产品绑定到分组而不是
单台服务器。有两种分配方式：

- **始终添加到占用最少的服务器。**
- **先把一台服务器填满，然后转到占用最少的服务器。**

服务器通过 `Add` / `Remove` 在 **Unassigned → Assigned** 两个列表之间移动。

> ⚠️ **同一分组内请保持面板类型一致。** 产品表单中的套餐列表只从当时选中的**那一台**服务器拉取。如果分组里
> 同时有 cPanel 和 Plesk 服务器，你选择的套餐名在另一种面板上可能没有对应项，落到该服务器的订单会以
> *找不到套餐* 失败。

### 5️⃣ 配置产品

**Products / Services → Hosting/Server → Web Hosting Packages** → 打开套餐 → **Module Settings**
选项卡。在 **Server Selection** 下选择 **Single Server** 或 **Server Group**，然后勾选你的 DNAHosting
服务器。随后模块会绘制自己的字段：

| 设置 | 取值 |
|---|---|
| **Detected panel** | 模块在该服务器上实际发现的面板，例如 `cPanel / WHM`。此处出现错误即表示识别失败 |
| **Package / Plan** | 从该服务器实时拉取的套餐列表 |
| **Automatic Setup** | 开启：订单自动开通。关闭：需要管理员审核 |

> 💡 **cPanel 上无需理会套餐前缀。** 对于在面板中显示为 `bakcay328_paket2` 的套餐，模块会自行解析
> `username_` 前缀。在 Plesk 上，列表就是服务器上定义的每一个服务方案。

**保存 —— 模块即可使用。** 🎉

**‼️从这一刻起，你可以在 WiseCP 的所有流程中通过模块管理 cPanel 与 Plesk 经销商账户。创建、暂停和删除完全由 WiseCP 掌控。**

---

## 🔍 日志与故障排查

**Tools → Logs → Module Logs**

| 日志 | 何时写入 | 内容 |
|---|---|---|
| **Module Logs**<br>*Tools → Logs → Module Logs* | 仅在 **Module Logs** 功能开启时 | 发送到面板的每个请求及其返回的响应，并标注操作名，例如 `createacct` 或 `webspace.add` |

> 💡 开关就在同一页面的顶部。复现问题前打开，之后再关闭。

> 🔐 服务器的 API 令牌或密码、模块生成或修改的账户密码，以及 SSO 会话令牌 —— 无论在请求还是响应中 ——
> 都会在**写入之前**用 `***` 掩码。

### 常见错误

| 现象 | 原因与解决 |
|---|---|
| `HTTP 403`，或错误文本中出现 `cpanelresult` 外层包装 | 令牌背后的经销商账户对该调用没有 WHM 级权限。请在 **WHM → Resellers → Edit Reseller's ACL List** 中授予账户列表、创建、暂停、删除、密码、套餐升级、套餐列表、流量与会话权限，然后**以该经销商身份**在 **WHM → Development → Manage API Tokens** 重新生成令牌 |
| Plesk **11003** | API 密钥是为另一个 IP 签发的 —— 请为 WiseCP 实际出口地址重新生成，或在 Password 字段填写面板密码 |
| Plesk **1014** | 对于该服务器所用的 XML-API 版本，Plesk 拒绝了请求体。请确认使用的是最新版模块；模块日志会指出被拒绝的元素 |
| 产品表单中显示错误文本而不是套餐列表 | 面板识别或套餐调用失败；原因就写在同一行 |

> 💡 其他任何 HTTP 错误都会附带从面板响应体中提取的纯文本摘要 —— 光看状态码从来讲不完整个故事。

---

## 🧩 须知事项

<details>
<summary><b>两种面板的差异</b></summary>

<br>

- **Plesk 上的删除会校验归属。** 模块开通的每个账户都带有内部标识；任何操作之前都会检查该标识，因此模块
  绝不会被指向面板中手工创建的订阅。
- **Plesk 上拒绝修改在用服务的域名。** Plesk 订阅是按域名查找的，修改会让之后的每一次操作永久失败。
  cPanel 上域名可以修改；在你于面板中变更之前，账户会继续服务旧域名。
- **重复域名保护。** 只要同一台服务器上还有另一个活动或暂停的服务在使用该域名，删除就会被拒绝。

</details>

<details>
<summary><b>面板识别</b></summary>

<br>

面板类型不需要在任何地方配置。首次调用时模块会探测服务器，并记住是哪种面板作出了响应。

端口只决定**先**尝试哪种面板：`8443` 与 `8880` 先试 Plesk，其他数值先试 cPanel。决定本身始终来自一次真实的
API 调用，第一次猜测没有响应时会再试另一种面板。端口填错只会让识别变慢，并不会让它失效。

</details>

<details>
<summary><b>凭据</b></summary>

<br>

两种面板的凭据都填在 **Password** 字段，WiseCP 会加密保存。本模块从不使用 **Access Hash** 字段，
DNAHosting 服务器上也不会显示该字段。

在 Plesk 上，模块会先把凭据当作 API 密钥尝试，失败后自行回退到 HTTP basic auth；你不需要告诉它填的是哪一种。

</details>

<details>
<summary><b>不在范围内</b></summary>

<br>

邮箱账户与转发管理、销售经销商账户、把既有账户导入 WiseCP，以及管理后台的 *登录 root 面板* 按钮。模块只持有
**经销商**凭据 —— 而非 root —— 因此没有可供它打开的 root 面板。

</details>

---

## 📄 更新日志

各版本的变更记录见 [CHANGELOG.md](CHANGELOG.md)。

---

<div align="center">

**DNA Reseller Hosting** · 适用于 WiseCP 的 cPanel & Plesk 经销商模块

[domainnameapi.com](https://www.domainnameapi.com) · [经销商面板](https://dm.domainnameapi.com/hosting)

</div>
