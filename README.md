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

**Manage cPanel and Plesk reseller accounts from a single WiseCP server module.**

One module, two panels. You never pick the panel type — the module asks the server itself and
remembers which panel answered.

![WiseCP](https://img.shields.io/badge/WiseCP-self--hosted-4A90D9?style=flat-square)
![PHP](https://img.shields.io/badge/PHP-7.4%20%E2%80%93%208.4-777BB4?style=flat-square&logo=php&logoColor=white)
![cPanel](https://img.shields.io/badge/cPanel%2FWHM-supported-FF6C2C?style=flat-square)
![Plesk](https://img.shields.io/badge/Plesk-supported-53BCE6?style=flat-square)

</div>

---

## 📑 Contents

- [✨ What it does](#-what-it-does)
- [📋 Requirements](#-requirements)
- [🚀 Installation](#-installation)
- [🔍 Logs and troubleshooting](#-logs-and-troubleshooting)
- [🧩 Things worth knowing](#-things-worth-knowing)
- [📄 Changelog](#-changelog)

---

## ✨ What it does

| Feature | cPanel/WHM | Plesk |
|---|:---:|:---:|
| Connection test and automatic panel detection | ✅ | ✅ |
| Account creation | ✅ | ✅ |
| Suspend / unsuspend | ✅ | ✅ |
| Termination | ✅ | ✅ *(ownership verified)* |
| Password change | ✅ | ✅ |
| Package / plan change | ✅ | ✅ |
| Disk & bandwidth usage sync | ✅ | ✅ |
| One-click login to the client panel | ✅ | ✅ |
| One-click login from the admin area | ✅ | ✅ |

> 💡 **Built for resellers.** It does not need root or admin access; the module works with the
> permissions of your own reseller account, and every account it creates counts against your quota.

---

## 📋 Requirements

- **WiseCP**, self-hosted, with administrator access
- **PHP** 7.4 – 8.4
- PHP extensions: `curl`, `simplexml`
- A **cPanel/WHM reseller account** (WHM API token) &nbsp;or&nbsp; a **Plesk reseller account**
  (API key or the panel password)
- Outbound access from the WiseCP server to the panel server on the panel's API port

> ✅ No database table is created, no cron job is required, and there are no composer dependencies.
> Installation is nothing more than copying a folder.

---

## 🚀 Installation

### 1️⃣ Install the module

Copy the `DNAHosting` folder into the `coremio/modules/Servers/` directory of your WiseCP
installation.

```
wisecp/
└── coremio/
    └── modules/
        └── Servers/
            └── DNAHosting/     ← here
```

### 2️⃣ Add the server

**Products / Services → Hosting/Server → Shared Server Settings → Add New Shared Server**

| Field | What to enter |
|---|---|
| **Server Automation Type** | `DNAHosting` — the folder name, listed exactly like that |
| **IP Address** | The real address of the panel server; the module connects here |
| **Username** | Your reseller username on that panel |
| **Password** | A WHM API token on cPanel, an API key or the panel password on Plesk |
| **Connect with SSL** | Tick it |
| **Port** | `2087` for cPanel, `8443` for Plesk |

> ⚠️ **The Hostname field at the top of the form is only a label.** The module connects to
> **IP Address**, never to that one. Your servers appear under this label in the server list.

### 3️⃣ Test the connection

Press **Test Connection** before saving, or simply save — WiseCP runs the test on its own.

A green result confirms both the credentials and the detected panel. A failure shows the concrete
HTTP code or panel error; see [Logs and troubleshooting](#-logs-and-troubleshooting).

### 4️⃣ Create a server group

If you have more than one server, use **Shared Server Settings → Server Groups** to create a group
and bind the product to the group instead of a single server. Two distribution types are offered:

- **Always add to the least full server.**
- **Fill one server completely, then move on to the least full server.**

Servers are moved between the **Unassigned → Assigned** lists with `Add` / `Remove`.

> ⚠️ **Keep a group homogeneous per panel.** The package list on the product form is pulled from the
> **single** server selected at that moment. If a group holds both a cPanel and a Plesk server, the
> package name you picked may have no counterpart on the other panel, and an order landing on that
> server fails with *package not found*.

### 5️⃣ Configure the product

**Products / Services → Hosting/Server → Web Hosting Packages** → open the package → **Module
Settings** tab. Under **Server Selection**, choose **Single Server** or **Server Group** and pick
your DNAHosting server. The module then draws its own fields:

| Setting | Value |
|---|---|
| **Detected panel** | The panel actually found on that server, for example `cPanel / WHM`. An error here means detection failed |
| **Package / Plan** | The package list pulled live from that server |
| **Automatic Setup** | On: the order is provisioned automatically. Off: admin approval is required |

> 💡 **Do not worry about the package prefix on cPanel.** For a package that shows up as
> `bakcay328_paket2` in the panel, the module resolves the `username_` prefix itself. On Plesk the
> list is every service plan defined on the server.

**Save it — the module is ready to use.** 🎉

**‼️From this point on you can manage cPanel and Plesk reseller accounts through the module across every WiseCP workflow. Creation, suspension and termination are entirely under WiseCP's control.**

---

## 🔍 Logs and troubleshooting

**Tools → Logs → Module Logs**

| Log | When it writes | What it contains |
|---|---|---|
| **Module Logs**<br>*Tools → Logs → Module Logs* | Only while the **Module Logs** feature is on | Every request sent to the panel and the response it returned, tagged with the operation name such as `createacct` or `webspace.add` |

> 💡 The switch that enables logging sits at the top of that same page. Turn it on before
> reproducing the problem, then turn it back off.

> 🔐 The server's API token or password, any account password the module generates or changes, and
> SSO session tokens are masked with `***` **before anything is written** — in the request and in
> the response alike.

### Common errors

| Symptom | Cause and fix |
|---|---|
| `HTTP 403`, or a `cpanelresult` envelope in the error text | The reseller behind the token has no WHM-level privilege for that call. Grant the account listing, creation, suspension, termination, password, package upgrade, package listing, bandwidth and session privileges in **WHM → Resellers → Edit Reseller's ACL List**, then regenerate the token **as that reseller** in **WHM → Development → Manage API Tokens** |
| Plesk **11003** | The API key was issued for a different IP — generate a new one for the address WiseCP connects from, or put the panel password in the Password field |
| Plesk **1014** | Plesk rejected the request body for the XML-API version this server speaks. Check that you run the current module version; the module log names the element it objected to |
| An error text instead of the package list on the product form | Detection or the package call failed; the reason is written on the same line |

> 💡 Every other HTTP error arrives with a plain-text summary extracted from the panel's response
> body — a bare status code is never the whole story.

---

## 🧩 Things worth knowing

<details>
<summary><b>Panel differences</b></summary>

<br>

- **Termination on Plesk is ownership-verified.** Every account the module opens is tagged with an
  internal id; that tag is checked before any operation, so the module can never be pointed at a
  subscription created by hand in the panel.
- **Changing the domain of a live service is refused on Plesk.** A Plesk subscription is found by
  its domain, so editing it would make every later operation fail permanently. On cPanel the domain
  can be edited; the account keeps serving the old domain until you change it in the panel.
- **Duplicate domain protection.** Termination is refused while the same domain is still attached to
  another active or suspended service on the same server.

</details>

<details>
<summary><b>Panel detection</b></summary>

<br>

The panel type is never configured. On the first call the module probes the server and remembers
which panel answered.

The port only decides which panel is tried **first**: `8443` and `8880` try Plesk first, anything
else tries cPanel first. The decision itself always comes from a real API call, and the other panel
is tried when the first guess does not answer. A wrong port slows detection down, it does not break
it.

</details>

<details>
<summary><b>Credentials</b></summary>

<br>

Both panels take their credential in the **Password** field, which WiseCP stores encrypted. The
**Access Hash** field is never used by this module and is not shown on DNAHosting servers.

On Plesk the module first tries the credential as an API key and falls back to HTTP basic auth on
its own, so you do not have to tell it which one you entered.

</details>

<details>
<summary><b>Out of scope</b></summary>

<br>

Email account and forwarder management, selling reseller accounts, importing existing accounts into
WiseCP, and a *log in to the root panel* button in the admin area. The module holds a **reseller**
credential only — never root — so there is no root panel for it to open.

</details>

---

## 📄 Changelog

Version-by-version changes are in [CHANGELOG.md](CHANGELOG.md).

---

<div align="center">

**DNA Reseller Hosting** · cPanel & Plesk reseller module for WiseCP

[domainnameapi.com](https://www.domainnameapi.com) · [Reseller panel](https://dm.domainnameapi.com/hosting)

</div>
