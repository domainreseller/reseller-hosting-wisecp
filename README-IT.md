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

**Gestisca gli account reseller cPanel e Plesk da un unico modulo server per WiseCP.**

Un modulo, due pannelli. Il tipo di pannello non lo sceglie lei — il modulo interroga direttamente
il server e ricorda quale pannello ha risposto.

![WiseCP](https://img.shields.io/badge/WiseCP-self--hosted-4A90D9?style=flat-square)
![PHP](https://img.shields.io/badge/PHP-7.4%20%E2%80%93%208.4-777BB4?style=flat-square&logo=php&logoColor=white)
![cPanel](https://img.shields.io/badge/cPanel%2FWHM-supportato-FF6C2C?style=flat-square)
![Plesk](https://img.shields.io/badge/Plesk-supportato-53BCE6?style=flat-square)

</div>

---

## 📑 Indice

- [✨ Cosa fa](#-cosa-fa)
- [📋 Requisiti](#-requisiti)
- [🚀 Installazione](#-installazione)
- [🔍 Log e risoluzione dei problemi](#-log-e-risoluzione-dei-problemi)
- [🧩 Cose da sapere](#-cose-da-sapere)
- [📄 Changelog](#-changelog)

---

## ✨ Cosa fa

| Funzione | cPanel/WHM | Plesk |
|---|:---:|:---:|
| Test di connessione e rilevamento automatico del pannello | ✅ | ✅ |
| Creazione dell'account | ✅ | ✅ |
| Sospensione / riattivazione | ✅ | ✅ |
| Cessazione | ✅ | ✅ *(proprietà verificata)* |
| Cambio password | ✅ | ✅ |
| Cambio pacchetto / piano | ✅ | ✅ |
| Sincronizzazione di spazio disco e traffico | ✅ | ✅ |
| Accesso al pannello cliente con un clic | ✅ | ✅ |
| Accesso con un clic dall'area amministrativa | ✅ | ✅ |

> 💡 **Pensato per i reseller.** Non serve accesso root o amministrativo; il modulo lavora con i
> permessi del suo account reseller, e ogni account creato viene scalato dalla sua quota.

---

## 📋 Requisiti

- **WiseCP** installato su un suo server, con accesso amministrativo
- **PHP** 7.4 – 8.4
- Estensioni PHP: `curl`, `simplexml`
- Un **account reseller cPanel/WHM** (token API WHM) &nbsp;oppure&nbsp; un **account reseller Plesk**
  (chiave API o password del pannello)
- Accesso in uscita dal server WiseCP verso il server del pannello, sulla porta API del pannello

> ✅ Non viene creata alcuna tabella nel database, non serve un cron e non ci sono dipendenze
> composer. L'installazione consiste nel copiare una cartella.

---

## 🚀 Installazione

### 1️⃣ Installi il modulo

Copi la cartella `DNAHosting` nella directory `coremio/modules/Servers/` della sua installazione
WiseCP.

```
wisecp/
└── coremio/
    └── modules/
        └── Servers/
            └── DNAHosting/     ← qui
```

### 2️⃣ Aggiunga il server

**Products / Services → Hosting/Server → Shared Server Settings → Add New Shared Server**

| Campo | Cosa inserire |
|---|---|
| **Server Automation Type** | `DNAHosting` — è il nome della cartella, appare così nell'elenco |
| **IP Address** | L'indirizzo reale del server del pannello; è lì che il modulo si connette |
| **Username** | Il suo nome utente reseller su quel pannello |
| **Password** | Un token API WHM su cPanel, una chiave API o la password del pannello su Plesk |
| **Connect with SSL** | Lo spunti |
| **Port** | `2087` per cPanel, `8443` per Plesk |

> ⚠️ **Il campo Hostname in cima al modulo è solo un'etichetta.** Il modulo si connette tramite
> **IP Address**, non tramite quel campo. Nell'elenco i suoi server compaiono con questa etichetta.

### 3️⃣ Verifichi la connessione

Prima di salvare prema **Test Connection**, oppure salvi direttamente — WiseCP esegue il test da sé.

Un esito verde conferma sia le credenziali sia il pannello rilevato. In caso di errore viene
mostrato il codice HTTP o l'errore del pannello; veda
[Log e risoluzione dei problemi](#-log-e-risoluzione-dei-problemi).

### 4️⃣ Crei un gruppo di server

Se ha più di un server, crei un gruppo in **Shared Server Settings → Server Groups** e colleghi il
prodotto al gruppo anziché a un singolo server. Sono previsti due tipi di distribuzione:

- **Aggiungi sempre al server meno pieno.**
- **Riempi completamente un server, poi passa a quello meno pieno.**

I server si spostano tra gli elenchi **Unassigned → Assigned** con `Add` / `Remove`.

> ⚠️ **Mantenga ogni gruppo omogeneo per pannello.** L'elenco dei pacchetti nel modulo prodotto
> viene letto dal **singolo** server selezionato in quel momento. Se un gruppo contiene sia un
> server cPanel sia uno Plesk, il nome del pacchetto scelto potrebbe non avere corrispondenza
> sull'altro pannello e l'ordine che finisce su quel server fallisce con *pacchetto non trovato*.

### 5️⃣ Configuri il prodotto

**Products / Services → Hosting/Server → Web Hosting Packages** → apra il pacchetto → scheda
**Module Settings**. In **Server Selection** scelga **Single Server** o **Server Group** e selezioni
il suo server DNAHosting. A quel punto il modulo disegna i propri campi:

| Impostazione | Valore |
|---|---|
| **Detected panel** | Il pannello effettivamente trovato su quel server, ad esempio `cPanel / WHM`. Un errore qui significa che il rilevamento è fallito |
| **Package / Plan** | L'elenco dei pacchetti letto in tempo reale da quel server |
| **Automatic Setup** | Attivo: l'ordine viene attivato automaticamente. Disattivo: serve l'approvazione dell'amministratore |

> 💡 **Su cPanel non si preoccupi del prefisso del pacchetto.** Per un pacchetto che nel pannello
> compare come `bakcay328_paket2`, il modulo risolve da sé il prefisso `nomeutente_`. Su Plesk
> l'elenco è costituito da ogni piano di servizio definito sul server.

**Salvi — il modulo è pronto all'uso.** 🎉

**‼️Da questo momento gestisce gli account reseller cPanel e Plesk tramite il modulo in ogni flusso di WiseCP. Creazione, sospensione e cessazione restano interamente sotto il controllo di WiseCP.**

---

## 🔍 Log e risoluzione dei problemi

**Tools → Logs → Module Logs**

| Log | Quando scrive | Cosa contiene |
|---|---|---|
| **Module Logs**<br>*Tools → Logs → Module Logs* | Solo mentre la funzione **Module Logs** è attiva | Ogni richiesta inviata al pannello e la risposta ricevuta, etichettate con il nome dell'operazione come `createacct` o `webspace.add` |

> 💡 L'interruttore si trova in cima alla stessa pagina. Lo attivi prima di riprodurre il problema e
> lo disattivi subito dopo.

> 🔐 Il token API o la password del server, tutte le password degli account generate o modificate
> dal modulo e i token di sessione SSO — sia nella richiesta sia nella risposta — vengono mascherati
> con `***` **prima che venga scritto qualsiasi cosa**.

### Errori più frequenti

| Sintomo | Causa e soluzione |
|---|---|
| `HTTP 403`, oppure un involucro `cpanelresult` nel testo dell'errore | Il reseller a cui appartiene il token non ha privilegi a livello WHM per quella chiamata. In **WHM → Resellers → Edit Reseller's ACL List** conceda i permessi di elenco account, creazione, sospensione, cessazione, password, upgrade del pacchetto, elenco pacchetti, traffico e sessione, quindi rigeneri il token **come quel reseller** in **WHM → Development → Manage API Tokens** |
| Plesk **11003** | La chiave API è stata emessa per un altro IP — ne generi una nuova per l'indirizzo da cui WiseCP si collega, oppure inserisca la password del pannello nel campo Password |
| Plesk **1014** | Plesk ha rifiutato il corpo della richiesta per la versione XML-API parlata da questo server. Verifichi di usare la versione aggiornata del modulo; il log del modulo indica l'elemento contestato |
| Un testo di errore al posto dell'elenco pacchetti nel modulo prodotto | Il rilevamento o la chiamata dei pacchetti è fallita; il motivo è scritto sulla stessa riga |

> 💡 Ogni altro errore HTTP arriva con un riepilogo in testo semplice estratto dal corpo della
> risposta del pannello — un codice di stato nudo non è mai tutta la storia.

---

## 🧩 Cose da sapere

<details>
<summary><b>Differenze tra i pannelli</b></summary>

<br>

- **Su Plesk la cessazione verifica la proprietà.** Ogni account aperto dal modulo viene marcato con
  un identificativo interno; il marcatore viene controllato prima di qualunque operazione, così il
  modulo non può mai essere puntato su un abbonamento creato a mano nel pannello.
- **Su Plesk il cambio di dominio di un servizio attivo viene rifiutato.** Un abbonamento Plesk si
  ritrova tramite il dominio, quindi una modifica farebbe fallire in modo permanente ogni operazione
  successiva. Su cPanel il dominio è modificabile; l'account continua a servire il vecchio dominio
  finché non lo cambia nel pannello.
- **Protezione dai domini duplicati.** La cessazione viene rifiutata finché lo stesso dominio è
  ancora collegato a un altro servizio attivo o sospeso sullo stesso server.

</details>

<details>
<summary><b>Rilevamento del pannello</b></summary>

<br>

Il tipo di pannello non si configura da nessuna parte. Alla prima chiamata il modulo sonda il server
e ricorda quale pannello ha risposto.

La porta decide soltanto quale pannello viene provato **per primo**: `8443` e `8880` provano prima
Plesk, qualunque altro valore prova prima cPanel. La decisione vera arriva sempre da una chiamata
API reale e l'altro pannello viene provato se la prima ipotesi non risponde. Una porta sbagliata
rallenta il rilevamento, non lo rompe.

</details>

<details>
<summary><b>Credenziali</b></summary>

<br>

Entrambi i pannelli ricevono la credenziale nel campo **Password**, che WiseCP conserva cifrato. Il
campo **Access Hash** non viene mai usato da questo modulo e sui server DNAHosting non compare
affatto.

Su Plesk il modulo prova la credenziale prima come chiave API e ripiega da sé sull'autenticazione
HTTP basic; non deve dirgli quale delle due ha inserito.

</details>

<details>
<summary><b>Fuori ambito</b></summary>

<br>

La gestione di caselle e inoltri e-mail, la vendita di account reseller, l'importazione in WiseCP di
account già esistenti e un pulsante *accesso al pannello root* nell'area amministrativa. Il modulo
custodisce soltanto una credenziale **reseller** — mai root — quindi non esiste alcun pannello root
che possa aprire.

</details>

---

## 📄 Changelog

Le modifiche versione per versione sono in [CHANGELOG.md](CHANGELOG.md).

---

<div align="center">

**DNA Reseller Hosting** · Modulo reseller cPanel & Plesk per WiseCP

[domainnameapi.com](https://www.domainnameapi.com) · [Pannello reseller](https://dm.domainnameapi.com/hosting)

</div>
