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

**Beheer cPanel- en Plesk-reselleraccounts vanuit één WiseCP-servermodule.**

Eén module, twee panels. U kiest het paneltype nooit — de module vraagt het de server zelf en
onthoudt welk panel antwoordde.

![WiseCP](https://img.shields.io/badge/WiseCP-self--hosted-4A90D9?style=flat-square)
![PHP](https://img.shields.io/badge/PHP-7.4%20%E2%80%93%208.4-777BB4?style=flat-square&logo=php&logoColor=white)
![cPanel](https://img.shields.io/badge/cPanel%2FWHM-ondersteund-FF6C2C?style=flat-square)
![Plesk](https://img.shields.io/badge/Plesk-ondersteund-53BCE6?style=flat-square)

</div>

---

## 📑 Inhoud

- [✨ Wat de module doet](#-wat-de-module-doet)
- [📋 Vereisten](#-vereisten)
- [🚀 Installatie](#-installatie)
- [🔍 Logs en probleemoplossing](#-logs-en-probleemoplossing)
- [🧩 Goed om te weten](#-goed-om-te-weten)
- [📄 Changelog](#-changelog)

---

## ✨ Wat de module doet

| Functie | cPanel/WHM | Plesk |
|---|:---:|:---:|
| Verbindingstest en automatische paneldetectie | ✅ | ✅ |
| Account aanmaken | ✅ | ✅ |
| Opschorten / heractiveren | ✅ | ✅ |
| Beëindigen | ✅ | ✅ *(eigendom geverifieerd)* |
| Wachtwoord wijzigen | ✅ | ✅ |
| Pakket / plan wijzigen | ✅ | ✅ |
| Synchronisatie van schijf- en dataverbruik | ✅ | ✅ |
| Met één klik inloggen op het klantpanel | ✅ | ✅ |
| Met één klik inloggen vanuit het adminpaneel | ✅ | ✅ |

> 💡 **Gebouwd voor resellers.** Root- of adminrechten zijn niet nodig; de module werkt met de
> rechten van uw eigen selleraccount, en elk account dat zij aanmaakt telt mee voor uw quotum.

---

## 📋 Vereisten

- **WiseCP**, op eigen server, met beheerderstoegang
- **PHP** 7.4 – 8.4
- PHP-extensies: `curl`, `simplexml`
- Een **cPanel/WHM-reselleraccount** (WHM API-token) &nbsp;of&nbsp; een **Plesk-reselleraccount**
  (API-sleutel of het panelwachtwoord)
- Uitgaande toegang van de WiseCP-server naar de panelserver op de API-poort van het panel

> ✅ Er wordt geen databasetabel aangemaakt, er is geen cronjob nodig en er zijn geen
> composer-afhankelijkheden. De installatie bestaat uit het kopiëren van een map.

---

## 🚀 Installatie

### 1️⃣ Installeer de module

Kopieer de map `DNAHosting` naar de directory `coremio/modules/Servers/` van uw WiseCP-installatie.

```
wisecp/
└── coremio/
    └── modules/
        └── Servers/
            └── DNAHosting/     ← hierheen
```

### 2️⃣ Voeg de server toe

**Products / Services → Hosting/Server → Shared Server Settings → Add New Shared Server**

| Veld | Wat in te vullen |
|---|---|
| **Server Automation Type** | `DNAHosting` — de mapnaam, precies zo in de lijst |
| **IP Address** | Het echte adres van de panelserver; daarheen maakt de module verbinding |
| **Username** | Uw resellergebruikersnaam op dat panel |
| **Password** | Een WHM API-token op cPanel, een API-sleutel of het panelwachtwoord op Plesk |
| **Connect with SSL** | Aanvinken |
| **Port** | `2087` voor cPanel, `8443` voor Plesk |

> ⚠️ **Het veld Hostname boven in het formulier is alleen een label.** De module verbindt via
> **IP Address**, niet via dat veld. In de serverlijst verschijnen uw servers onder dit label.

### 3️⃣ Test de verbinding

Druk vóór het opslaan op **Test Connection**, of sla gewoon op — WiseCP voert de test zelf uit.

Een groen resultaat bevestigt zowel de inloggegevens als het gedetecteerde panel. Bij een fout ziet
u de concrete HTTP-code of panelfout; zie [Logs en probleemoplossing](#-logs-en-probleemoplossing).

### 4️⃣ Maak een servergroep

Hebt u meer dan één server, maak dan via **Shared Server Settings → Server Groups** een groep aan en
koppel het product aan de groep in plaats van aan één server. Er zijn twee verdeeltypen:

- **Altijd toevoegen aan de minst gevulde server.**
- **Eén server volledig vullen en daarna naar de minst gevulde server gaan.**

Servers worden met `Add` / `Remove` verplaatst tussen de lijsten **Unassigned → Assigned**.

> ⚠️ **Houd een groep homogeen per panel.** De pakketlijst op het productformulier wordt opgehaald
> bij de **ene** server die op dat moment geselecteerd is. Bevat een groep zowel een cPanel- als een
> Plesk-server, dan heeft de gekozen pakketnaam op het andere panel mogelijk geen tegenhanger, en
> mislukt een bestelling die daar terechtkomt met *pakket niet gevonden*.

### 5️⃣ Configureer het product

**Products / Services → Hosting/Server → Web Hosting Packages** → open het pakket → tabblad **Module
Settings**. Kies onder **Server Selection** voor **Single Server** of **Server Group** en selecteer
uw DNAHosting-server. Daarna tekent de module haar eigen velden:

| Instelling | Waarde |
|---|---|
| **Detected panel** | Het panel dat daadwerkelijk op die server is gevonden, bijvoorbeeld `cPanel / WHM`. Een fout hier betekent dat de detectie is mislukt |
| **Package / Plan** | De pakketlijst die live bij die server wordt opgehaald |
| **Automatic Setup** | Aan: de bestelling wordt automatisch uitgerold. Uit: goedkeuring door een beheerder is nodig |

> 💡 **Over de pakketprefix op cPanel hoeft u zich geen zorgen te maken.** Voor een pakket dat in het
> panel als `bakcay328_paket2` verschijnt, lost de module de prefix `gebruikersnaam_` zelf op. Op
> Plesk is de lijst elk serviceplan dat op de server is gedefinieerd.

**Sla het op — de module is klaar voor gebruik.** 🎉

**‼️Vanaf hier beheert u cPanel- en Plesk-reselleraccounts via de module in elke WiseCP-workflow. Aanmaken, opschorten en beëindigen vallen volledig onder de controle van WiseCP.**

---

## 🔍 Logs en probleemoplossing

**Tools → Logs → Module Logs**

| Log | Wanneer het schrijft | Wat het bevat |
|---|---|---|
| **Module Logs**<br>*Tools → Logs → Module Logs* | Alleen zolang de functie **Module Logs** aanstaat | Elk verzoek dat naar het panel gaat en het antwoord dat terugkomt, voorzien van de bewerkingsnaam zoals `createacct` of `webspace.add` |

> 💡 De schakelaar hiervoor staat boven aan diezelfde pagina. Zet hem aan voordat u het probleem
> reproduceert en daarna weer uit.

> 🔐 Het API-token of wachtwoord van de server, alle accountwachtwoorden die de module genereert of
> wijzigt en SSO-sessietokens worden — zowel in het verzoek als in het antwoord — met `***` gemaskeerd
> **voordat er iets wordt weggeschreven**.

### Veelvoorkomende fouten

| Symptoom | Oorzaak en oplossing |
|---|---|
| `HTTP 403`, of een `cpanelresult`-envelop in de fouttekst | De reseller achter het token heeft voor die aanroep geen rechten op WHM-niveau. Ken in **WHM → Resellers → Edit Reseller's ACL List** de rechten toe voor accountlijst, aanmaken, opschorten, beëindigen, wachtwoord, pakketupgrade, pakketlijst, dataverkeer en sessie, en genereer het token daarna opnieuw **als die reseller** via **WHM → Development → Manage API Tokens** |
| Plesk **11003** | De API-sleutel is voor een ander IP uitgegeven — genereer een nieuwe voor het adres waarvandaan WiseCP verbindt, of zet het panelwachtwoord in het veld Password |
| Plesk **1014** | Plesk weigerde de body van het verzoek voor de XML-API-versie die deze server spreekt. Controleer of u de actuele moduleversie gebruikt; het modulelog noemt het element waartegen bezwaar werd gemaakt |
| Een fouttekst in plaats van de pakketlijst op het productformulier | De detectie of de pakketaanroep is mislukt; de reden staat op dezelfde regel |

> 💡 Elke andere HTTP-fout komt met een samenvatting in platte tekst uit de responsbody van het panel
> — een kale statuscode is nooit het hele verhaal.

---

## 🧩 Goed om te weten

<details>
<summary><b>Verschillen tussen de panels</b></summary>

<br>

- **Beëindigen op Plesk wordt op eigendom gecontroleerd.** Elk account dat de module opent krijgt een
  intern id; dat label wordt vóór elke bewerking gecontroleerd, zodat de module nooit op een
  handmatig in het panel aangemaakt abonnement kan worden gericht.
- **Het domein van een lopende dienst wijzigen wordt op Plesk geweigerd.** Een Plesk-abonnement wordt
  op zijn domein gevonden, dus een wijziging zou elke latere bewerking blijvend laten mislukken. Op
  cPanel kan het domein wel worden bewerkt; het account blijft het oude domein bedienen totdat u het
  in het panel wijzigt.
- **Bescherming tegen dubbele domeinen.** Beëindigen wordt geweigerd zolang hetzelfde domein nog aan
  een andere actieve of opgeschorte dienst op dezelfde server hangt.

</details>

<details>
<summary><b>Paneldetectie</b></summary>

<br>

Het paneltype wordt nergens geconfigureerd. Bij de eerste aanroep polst de module de server en
onthoudt welk panel antwoordde.

De poort bepaalt alleen welk panel **eerst** wordt geprobeerd: `8443` en `8880` proberen eerst Plesk,
elke andere waarde eerst cPanel. De beslissing zelf komt altijd uit een echte API-aanroep, en het
andere panel wordt geprobeerd wanneer de eerste gok niet antwoordt. Een verkeerde poort vertraagt de
detectie, zij breekt haar niet.

</details>

<details>
<summary><b>Inloggegevens</b></summary>

<br>

Beide panels nemen hun inloggegeven in het veld **Password**, dat WiseCP versleuteld opslaat. Het
veld **Access Hash** gebruikt deze module nooit en het wordt bij DNAHosting-servers niet getoond.

Op Plesk probeert de module het gegeven eerst als API-sleutel en valt zij uit zichzelf terug op HTTP
basic auth; u hoeft haar niet te vertellen welke van de twee u hebt ingevuld.

</details>

<details>
<summary><b>Buiten scope</b></summary>

<br>

Beheer van e-mailaccounts en doorstuuradressen, het verkopen van reselleraccounts, het importeren van
bestaande accounts in WiseCP en een knop *inloggen op het rootpanel* in het adminpaneel. De module
houdt alleen een **reseller**-inloggegeven vast — geen root — dus er is geen rootpanel dat zij kan
openen.

</details>

---

## 📄 Changelog

De wijzigingen per versie staan in [CHANGELOG.md](CHANGELOG.md).

---

<div align="center">

**DNA Reseller Hosting** · cPanel- & Plesk-resellermodule voor WiseCP

[domainnameapi.com](https://www.domainnameapi.com) · [Resellerpanel](https://dm.domainnameapi.com/hosting)

</div>
