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

**Gérez les comptes revendeur cPanel et Plesk depuis un seul module serveur WiseCP.**

Un module, deux panneaux. Vous ne choisissez jamais le type de panneau — le module interroge
lui-même le serveur et retient quel panneau a répondu.

![WiseCP](https://img.shields.io/badge/WiseCP-self--hosted-4A90D9?style=flat-square)
![PHP](https://img.shields.io/badge/PHP-7.4%20%E2%80%93%208.4-777BB4?style=flat-square&logo=php&logoColor=white)
![cPanel](https://img.shields.io/badge/cPanel%2FWHM-pris%20en%20charge-FF6C2C?style=flat-square)
![Plesk](https://img.shields.io/badge/Plesk-pris%20en%20charge-53BCE6?style=flat-square)

</div>

---

## 📑 Sommaire

- [✨ Ce que fait le module](#-ce-que-fait-le-module)
- [📋 Prérequis](#-prérequis)
- [🚀 Installation](#-installation)
- [🔍 Journaux et dépannage](#-journaux-et-dépannage)
- [🧩 Bon à savoir](#-bon-à-savoir)
- [📄 Journal des modifications](#-journal-des-modifications)

---

## ✨ Ce que fait le module

| Fonction | cPanel/WHM | Plesk |
|---|:---:|:---:|
| Test de connexion et détection automatique du panneau | ✅ | ✅ |
| Création de compte | ✅ | ✅ |
| Suspension / réactivation | ✅ | ✅ |
| Résiliation | ✅ | ✅ *(propriété vérifiée)* |
| Changement de mot de passe | ✅ | ✅ |
| Changement de pack / plan | ✅ | ✅ |
| Synchronisation de l'espace disque et du trafic | ✅ | ✅ |
| Connexion en un clic au panneau client | ✅ | ✅ |
| Connexion en un clic depuis l'espace admin | ✅ | ✅ |

> 💡 **Conçu pour les revendeurs.** Aucun accès root ou administrateur n'est nécessaire ; le module
> travaille avec les droits de votre propre compte revendeur, et chaque compte qu'il crée est
> décompté de votre quota.

---

## 📋 Prérequis

- **WiseCP**, auto-hébergé, avec un accès administrateur
- **PHP** 7.4 – 8.4
- Extensions PHP : `curl`, `simplexml`
- Un **compte revendeur cPanel/WHM** (jeton API WHM) &nbsp;ou&nbsp; un **compte revendeur Plesk**
  (clé API ou mot de passe du panneau)
- Un accès sortant du serveur WiseCP vers le serveur du panneau, sur le port API du panneau

> ✅ Aucune table de base de données n'est créée, aucune tâche cron n'est nécessaire et il n'y a
> aucune dépendance composer. L'installation se limite à copier un dossier.

---

## 🚀 Installation

### 1️⃣ Installez le module

Copiez le dossier `DNAHosting` dans le répertoire `coremio/modules/Servers/` de votre installation
WiseCP.

```
wisecp/
└── coremio/
    └── modules/
        └── Servers/
            └── DNAHosting/     ← ici
```

### 2️⃣ Ajoutez le serveur

**Products / Services → Hosting/Server → Shared Server Settings → Add New Shared Server**

| Champ | Ce qu'il faut saisir |
|---|---|
| **Server Automation Type** | `DNAHosting` — c'est le nom du dossier, affiché tel quel dans la liste |
| **IP Address** | L'adresse réelle du serveur du panneau ; c'est là que le module se connecte |
| **Username** | Votre nom d'utilisateur revendeur sur ce panneau |
| **Password** | Un jeton API WHM sur cPanel, une clé API ou le mot de passe du panneau sur Plesk |
| **Connect with SSL** | Cochez-le |
| **Port** | `2087` pour cPanel, `8443` pour Plesk |

> ⚠️ **Le champ Hostname en haut du formulaire n'est qu'une étiquette.** Le module se connecte via
> **IP Address**, jamais via ce champ. Vos serveurs apparaissent sous cette étiquette dans la liste.

### 3️⃣ Testez la connexion

Appuyez sur **Test Connection** avant d'enregistrer, ou enregistrez simplement — WiseCP lance le
test de lui-même.

Un résultat vert confirme à la fois les identifiants et le panneau détecté. En cas d'échec, le code
HTTP ou l'erreur du panneau s'affiche précisément ; voir [Journaux et dépannage](#-journaux-et-dépannage).

### 4️⃣ Créez un groupe de serveurs

Si vous avez plusieurs serveurs, créez un groupe dans **Shared Server Settings → Server Groups** et
rattachez le produit au groupe plutôt qu'à un serveur unique. Deux types de répartition sont
proposés :

- **Toujours ajouter sur le serveur le moins rempli.**
- **Remplir un serveur entièrement, puis passer au serveur le moins rempli.**

Les serveurs se déplacent entre les listes **Unassigned → Assigned** avec `Add` / `Remove`.

> ⚠️ **Gardez un groupe homogène côté panneau.** La liste des packs du formulaire produit est
> chargée depuis le **seul** serveur sélectionné à cet instant. Si un groupe contient à la fois un
> serveur cPanel et un serveur Plesk, le nom de pack choisi peut n'avoir aucun équivalent sur
> l'autre panneau, et une commande qui y atterrit échoue avec *pack introuvable*.

### 5️⃣ Configurez le produit

**Products / Services → Hosting/Server → Web Hosting Packages** → ouvrez le pack → onglet **Module
Settings**. Sous **Server Selection**, choisissez **Single Server** ou **Server Group**, puis cochez
votre serveur DNAHosting. Le module dessine alors ses propres champs :

| Réglage | Valeur |
|---|---|
| **Detected panel** | Le panneau réellement trouvé sur ce serveur, par exemple `cPanel / WHM`. Une erreur ici signifie que la détection a échoué |
| **Package / Plan** | La liste des packs chargée en direct depuis ce serveur |
| **Automatic Setup** | Activé : la commande est provisionnée automatiquement. Désactivé : une validation administrateur est requise |

> 💡 **Ne vous souciez pas du préfixe de pack sur cPanel.** Pour un pack affiché dans le panneau
> comme `bakcay328_paket2`, le module résout lui-même le préfixe `nomutilisateur_`. Sur Plesk, la
> liste correspond à chaque plan de service défini sur le serveur.

**Enregistrez — le module est prêt à l'emploi.** 🎉

**‼️À partir d'ici, vous gérez les comptes revendeur cPanel et Plesk via le module dans tous les flux WiseCP. La création, la suspension et la résiliation restent entièrement sous le contrôle de WiseCP.**

---

## 🔍 Journaux et dépannage

**Tools → Logs → Module Logs**

| Journal | Quand il écrit | Ce qu'il contient |
|---|---|---|
| **Module Logs**<br>*Tools → Logs → Module Logs* | Uniquement tant que la fonction **Module Logs** est active | Chaque requête envoyée au panneau et la réponse renvoyée, étiquetées avec le nom de l'opération, par exemple `createacct` ou `webspace.add` |

> 💡 L'interrupteur se trouve en haut de cette même page. Activez-le avant de reproduire le
> problème, puis désactivez-le.

> 🔐 Le jeton API ou mot de passe du serveur, tous les mots de passe de compte générés ou modifiés
> par le module et les jetons de session SSO — dans la requête comme dans la réponse — sont masqués
> par `***` **avant toute écriture**.

### Erreurs fréquentes

| Symptôme | Cause et solution |
|---|---|
| `HTTP 403`, ou une enveloppe `cpanelresult` dans le texte d'erreur | Le revendeur derrière le jeton n'a pas de droit au niveau WHM pour cet appel. Accordez dans **WHM → Resellers → Edit Reseller's ACL List** les droits de liste des comptes, création, suspension, résiliation, mot de passe, montée en gamme, liste des packs, trafic et session, puis régénérez le jeton **en tant que ce revendeur** dans **WHM → Development → Manage API Tokens** |
| Plesk **11003** | La clé API a été émise pour une autre IP — générez-en une nouvelle pour l'adresse depuis laquelle WiseCP se connecte, ou saisissez le mot de passe du panneau dans le champ Password |
| Plesk **1014** | Plesk a rejeté le corps de la requête pour la version XML-API que parle ce serveur. Vérifiez que vous utilisez la version actuelle du module ; le journal du module nomme l'élément contesté |
| Un texte d'erreur à la place de la liste des packs sur le formulaire produit | La détection ou l'appel des packs a échoué ; la raison est écrite sur la même ligne |

> 💡 Toute autre erreur HTTP arrive avec un résumé en texte brut extrait du corps de réponse du
> panneau — un code d'état nu n'est jamais toute l'histoire.

---

## 🧩 Bon à savoir

<details>
<summary><b>Différences entre les panneaux</b></summary>

<br>

- **La résiliation sur Plesk est vérifiée par propriété.** Chaque compte ouvert par le module est
  marqué d'un identifiant interne ; ce marqueur est contrôlé avant toute opération, si bien que le
  module ne peut jamais être dirigé vers un abonnement créé à la main dans le panneau.
- **Changer le domaine d'un service en production est refusé sur Plesk.** Un abonnement Plesk est
  retrouvé par son domaine : une modification ferait échouer définitivement toutes les opérations
  suivantes. Sur cPanel le domaine peut être modifié ; le compte continue de servir l'ancien domaine
  jusqu'à ce que vous le changiez dans le panneau.
- **Protection contre les domaines en double.** La résiliation est refusée tant que le même domaine
  est encore rattaché à un autre service actif ou suspendu sur le même serveur.

</details>

<details>
<summary><b>Détection du panneau</b></summary>

<br>

Le type de panneau n'est configuré nulle part. Au premier appel, le module sonde le serveur et
retient quel panneau a répondu.

Le port décide seulement du panneau essayé **en premier** : `8443` et `8880` essaient Plesk d'abord,
toute autre valeur essaie cPanel d'abord. La décision elle-même vient toujours d'un véritable appel
API, et l'autre panneau est essayé si la première hypothèse ne répond pas. Un mauvais port ralentit
la détection, il ne la casse pas.

</details>

<details>
<summary><b>Identifiants</b></summary>

<br>

Les deux panneaux prennent leur identifiant dans le champ **Password**, que WiseCP stocke chiffré.
Le champ **Access Hash** n'est jamais utilisé par ce module et n'apparaît pas sur les serveurs
DNAHosting.

Sur Plesk, le module essaie d'abord l'identifiant comme clé API puis bascule de lui-même vers
l'authentification HTTP basic ; vous n'avez pas à lui dire lequel vous avez saisi.

</details>

<details>
<summary><b>Hors périmètre</b></summary>

<br>

La gestion des comptes e-mail et des redirections, la vente de comptes revendeur, l'import de
comptes existants dans WiseCP et un bouton *connexion au panneau root* dans l'espace admin. Le
module ne détient qu'un identifiant **revendeur** — jamais root — il n'y a donc aucun panneau root
qu'il puisse ouvrir.

</details>

---

## 📄 Journal des modifications

Les changements version par version se trouvent dans [CHANGELOG.md](CHANGELOG.md).

---

<div align="center">

**DNA Reseller Hosting** · Module revendeur cPanel & Plesk pour WiseCP

[domainnameapi.com](https://www.domainnameapi.com) · [Panneau revendeur](https://dm.domainnameapi.com/hosting)

</div>
