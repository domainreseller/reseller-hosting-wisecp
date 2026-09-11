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

**Verwalten Sie cPanel- und Plesk-Reseller-Konten aus einem einzigen WiseCP-Servermodul.**

Ein Modul, zwei Panels. Sie wählen den Paneltyp nie aus — das Modul fragt den Server selbst und
merkt sich, welches Panel geantwortet hat.

![WiseCP](https://img.shields.io/badge/WiseCP-self--hosted-4A90D9?style=flat-square)
![PHP](https://img.shields.io/badge/PHP-7.4%20%E2%80%93%208.4-777BB4?style=flat-square&logo=php&logoColor=white)
![cPanel](https://img.shields.io/badge/cPanel%2FWHM-unterst%C3%BCtzt-FF6C2C?style=flat-square)
![Plesk](https://img.shields.io/badge/Plesk-unterst%C3%BCtzt-53BCE6?style=flat-square)

</div>

---

## 📑 Inhalt

- [✨ Was es kann](#-was-es-kann)
- [📋 Voraussetzungen](#-voraussetzungen)
- [🚀 Installation](#-installation)
- [🔍 Protokolle und Fehlersuche](#-protokolle-und-fehlersuche)
- [🧩 Wissenswertes](#-wissenswertes)
- [📄 Changelog](#-changelog)

---

## ✨ Was es kann

| Funktion | cPanel/WHM | Plesk |
|---|:---:|:---:|
| Verbindungstest und automatische Panel-Erkennung | ✅ | ✅ |
| Konto anlegen | ✅ | ✅ |
| Sperren / entsperren | ✅ | ✅ |
| Kündigung | ✅ | ✅ *(mit Eigentumsprüfung)* |
| Passwortänderung | ✅ | ✅ |
| Paket- / Planwechsel | ✅ | ✅ |
| Abgleich von Speicher- und Traffic-Verbrauch | ✅ | ✅ |
| Ein-Klick-Login ins Kundenpanel | ✅ | ✅ |
| Ein-Klick-Login aus dem Adminbereich | ✅ | ✅ |

> 💡 **Für Reseller gebaut.** Root- oder Admin-Zugang ist nicht nötig; das Modul arbeitet mit den
> Rechten Ihres eigenen Reseller-Kontos, und jedes angelegte Konto zählt gegen Ihr Kontingent.

---

## 📋 Voraussetzungen

- **WiseCP**, selbst gehostet, mit Administratorzugang
- **PHP** 7.4 – 8.4
- PHP-Erweiterungen: `curl`, `simplexml`
- Ein **cPanel/WHM-Reseller-Konto** (WHM-API-Token) &nbsp;oder&nbsp; ein **Plesk-Reseller-Konto**
  (API-Schlüssel oder Panel-Passwort)
- Ausgehender Zugriff vom WiseCP-Server auf den Panel-Server über den API-Port des Panels

> ✅ Es wird keine Datenbanktabelle angelegt, kein Cronjob benötigt und es gibt keine
> composer-Abhängigkeiten. Die Installation besteht aus dem Kopieren eines Ordners.

---

## 🚀 Installation

### 1️⃣ Modul installieren

Kopieren Sie den Ordner `DNAHosting` in das Verzeichnis `coremio/modules/Servers/` Ihrer
WiseCP-Installation.

```
wisecp/
└── coremio/
    └── modules/
        └── Servers/
            └── DNAHosting/     ← hierhin
```

### 2️⃣ Server hinzufügen

**Products / Services → Hosting/Server → Shared Server Settings → Add New Shared Server**

| Feld | Was einzutragen ist |
|---|---|
| **Server Automation Type** | `DNAHosting` — der Ordnername, genau so in der Liste |
| **IP Address** | Die tatsächliche Adresse des Panel-Servers; dorthin verbindet das Modul |
| **Username** | Ihr Reseller-Benutzername auf diesem Panel |
| **Password** | bei cPanel ein WHM-API-Token, bei Plesk ein API-Schlüssel oder das Panel-Passwort |
| **Connect with SSL** | Aktivieren |
| **Port** | `2087` für cPanel, `8443` für Plesk |

> ⚠️ **Das Feld Hostname oben im Formular ist nur eine Bezeichnung.** Das Modul verbindet sich zur
> **IP Address**, nie zu diesem Feld. In der Serverliste erscheinen Ihre Server unter dieser
> Bezeichnung.

### 3️⃣ Verbindung testen

Drücken Sie vor dem Speichern **Test Connection**, oder speichern Sie einfach — WiseCP führt den
Test von sich aus durch.

Ein grünes Ergebnis bestätigt sowohl die Zugangsdaten als auch das erkannte Panel. Bei einem Fehler
erscheint der konkrete HTTP-Code oder Panel-Fehler; siehe
[Protokolle und Fehlersuche](#-protokolle-und-fehlersuche).

### 4️⃣ Servergruppe anlegen

Bei mehreren Servern legen Sie unter **Shared Server Settings → Server Groups** eine Gruppe an und
binden das Produkt an die Gruppe statt an einen einzelnen Server. Zwei Verteilungsarten stehen zur
Wahl:

- **Immer auf den am wenigsten ausgelasteten Server legen.**
- **Einen Server vollständig füllen, danach auf den am wenigsten ausgelasteten wechseln.**

Server werden mit `Add` / `Remove` zwischen den Listen **Unassigned → Assigned** verschoben.

> ⚠️ **Halten Sie eine Gruppe panelseitig homogen.** Die Paketliste im Produktformular wird von dem
> in diesem Moment ausgewählten **einen** Server geladen. Enthält eine Gruppe cPanel- und
> Plesk-Server, hat der gewählte Paketname auf dem anderen Panel womöglich keine Entsprechung, und
> eine dort landende Bestellung scheitert mit *Paket nicht gefunden*.

### 5️⃣ Produkt konfigurieren

**Products / Services → Hosting/Server → Web Hosting Packages** → Paket öffnen → Reiter **Module
Settings**. Wählen Sie unter **Server Selection** entweder **Single Server** oder **Server Group**
und markieren Sie Ihren DNAHosting-Server. Daraufhin zeichnet das Modul seine eigenen Felder:

| Einstellung | Wert |
|---|---|
| **Detected panel** | Das auf diesem Server tatsächlich gefundene Panel, zum Beispiel `cPanel / WHM`. Ein Fehler hier bedeutet, dass die Erkennung fehlgeschlagen ist |
| **Package / Plan** | Die live von diesem Server geladene Paketliste |
| **Automatic Setup** | An: die Bestellung wird automatisch bereitgestellt. Aus: eine Admin-Freigabe ist nötig |

> 💡 **Um das Paketpräfix auf cPanel müssen Sie sich nicht kümmern.** Bei einem Paket, das im Panel
> als `bakcay328_paket2` erscheint, löst das Modul das Präfix `benutzername_` selbst auf. Auf Plesk
> ist die Liste jeder auf dem Server definierte Service-Plan.

**Speichern — das Modul ist einsatzbereit.** 🎉

**‼️Ab hier verwalten Sie cPanel- und Plesk-Reseller-Konten in jedem WiseCP-Ablauf über das Modul. Anlegen, Sperren und Kündigen liegen vollständig in der Hand von WiseCP.**

---

## 🔍 Protokolle und Fehlersuche

**Tools → Logs → Module Logs**

| Protokoll | Wann es schreibt | Was darin steht |
|---|---|---|
| **Module Logs**<br>*Tools → Logs → Module Logs* | Nur solange die Funktion **Module Logs** eingeschaltet ist | Jede an das Panel gesendete Anfrage und die zurückgegebene Antwort, gekennzeichnet mit dem Operationsnamen wie `createacct` oder `webspace.add` |

> 💡 Der Schalter dafür sitzt oben auf derselben Seite. Schalten Sie ihn ein, bevor Sie das Problem
> reproduzieren, und danach wieder aus.

> 🔐 Das API-Token bzw. Passwort des Servers, alle vom Modul erzeugten oder geänderten
> Kontopasswörter und SSO-Sitzungstoken werden — in Anfrage wie Antwort — **vor dem Schreiben** mit
> `***` maskiert.

### Häufige Fehler

| Symptom | Ursache und Lösung |
|---|---|
| `HTTP 403` oder ein `cpanelresult`-Umschlag im Fehlertext | Der Reseller hinter dem Token hat für diesen Aufruf keine WHM-Berechtigung. Erteilen Sie unter **WHM → Resellers → Edit Reseller's ACL List** die Rechte für Kontenliste, Anlegen, Sperren, Kündigen, Passwort, Paket-Upgrade, Paketliste, Traffic und Sitzung und erzeugen Sie das Token dann **als dieser Reseller** unter **WHM → Development → Manage API Tokens** neu |
| Plesk **11003** | Der API-Schlüssel wurde für eine andere IP ausgestellt — erzeugen Sie einen neuen für die Adresse, von der WiseCP verbindet, oder tragen Sie das Panel-Passwort ins Feld Password ein |
| Plesk **1014** | Plesk hat den Anfragekörper für die XML-API-Version dieses Servers abgelehnt. Prüfen Sie, ob Sie die aktuelle Modulversion einsetzen; das Modullog nennt das beanstandete Element |
| Statt der Paketliste erscheint im Produktformular ein Fehlertext | Die Erkennung oder der Paketabruf ist fehlgeschlagen; der Grund steht in derselben Zeile |

> 💡 Jeder andere HTTP-Fehler kommt mit einer Klartext-Zusammenfassung aus dem Antwortkörper des
> Panels — ein nackter Statuscode ist nie die ganze Geschichte.

---

## 🧩 Wissenswertes

<details>
<summary><b>Panel-Unterschiede</b></summary>

<br>

- **Die Kündigung auf Plesk ist eigentumsgeprüft.** Jedes vom Modul angelegte Konto wird mit einer
  internen Kennung markiert; diese Markierung wird vor jeder Operation geprüft, sodass das Modul nie
  auf ein von Hand im Panel angelegtes Abonnement gerichtet werden kann.
- **Das Ändern der Domain eines laufenden Dienstes wird auf Plesk abgelehnt.** Ein Plesk-Abonnement
  wird über seine Domain gefunden, eine Änderung würde jede spätere Operation dauerhaft scheitern
  lassen. Auf cPanel lässt sich die Domain bearbeiten; das Konto bedient weiter die alte Domain, bis
  Sie sie im Panel ändern.
- **Schutz vor doppelten Domains.** Eine Kündigung wird abgelehnt, solange dieselbe Domain noch an
  einem anderen aktiven oder gesperrten Dienst auf demselben Server hängt.

</details>

<details>
<summary><b>Panel-Erkennung</b></summary>

<br>

Der Paneltyp wird nirgends konfiguriert. Beim ersten Aufruf sondiert das Modul den Server und merkt
sich, welches Panel geantwortet hat.

Der Port entscheidet nur, welches Panel **zuerst** versucht wird: `8443` und `8880` versuchen Plesk
zuerst, jeder andere Wert cPanel. Die Entscheidung selbst stammt immer aus einem echten API-Aufruf,
und das andere Panel wird versucht, wenn die erste Vermutung nicht antwortet. Ein falscher Port
verlangsamt die Erkennung, er zerstört sie nicht.

</details>

<details>
<summary><b>Zugangsdaten</b></summary>

<br>

Beide Panels nehmen ihre Zugangsdaten im Feld **Password** entgegen, das WiseCP verschlüsselt
ablegt. Das Feld **Access Hash** verwendet dieses Modul nie und es wird bei DNAHosting-Servern gar
nicht angezeigt.

Auf Plesk probiert das Modul die Zugangsdaten zuerst als API-Schlüssel und fällt von selbst auf HTTP
Basic Auth zurück; Sie müssen ihm nicht sagen, was Sie eingetragen haben.

</details>

<details>
<summary><b>Nicht im Funktionsumfang</b></summary>

<br>

Verwaltung von E-Mail-Konten und Weiterleitungen, der Verkauf von Reseller-Konten, der Import
bestehender Konten nach WiseCP und ein *Login ins Root-Panel* im Adminbereich. Das Modul hält nur
eine **Reseller**-Zugangsinformation — kein Root — es gibt also kein Root-Panel, das es öffnen
könnte.

</details>

---

## 📄 Changelog

Die Änderungen Version für Version stehen in [CHANGELOG.md](CHANGELOG.md).

---

<div align="center">

**DNA Reseller Hosting** · cPanel- & Plesk-Reseller-Modul für WiseCP

[domainnameapi.com](https://www.domainnameapi.com) · [Reseller-Panel](https://dm.domainnameapi.com/hosting)

</div>
