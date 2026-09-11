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

**cPanel və Plesk diler hesablarını tək bir WiseCP server modulundan idarə edin.**

Bir modul, iki panel. Panel tipini siz seçmirsiniz — modul serverdən özü soruşur və hansı panelin
cavab verdiyini yadda saxlayır.

![WiseCP](https://img.shields.io/badge/WiseCP-self--hosted-4A90D9?style=flat-square)
![PHP](https://img.shields.io/badge/PHP-7.4%20%E2%80%93%208.4-777BB4?style=flat-square&logo=php&logoColor=white)
![cPanel](https://img.shields.io/badge/cPanel%2FWHM-d%C9%99st%C9%99kl%C9%99nir-FF6C2C?style=flat-square)
![Plesk](https://img.shields.io/badge/Plesk-d%C9%99st%C9%99kl%C9%99nir-53BCE6?style=flat-square)

</div>

---

## 📑 Mündəricat

- [✨ Nə edir](#-nə-edir)
- [📋 Tələblər](#-tələblər)
- [🚀 Quraşdırma](#-quraşdırma)
- [🔍 Loglar və problemlərin həlli](#-loglar-və-problemlərin-həlli)
- [🧩 Bilinməsi lazım olanlar](#-bilinməsi-lazım-olanlar)
- [📄 Dəyişiklik jurnalı](#-dəyişiklik-jurnalı)

---

## ✨ Nə edir

| Funksiya | cPanel/WHM | Plesk |
|---|:---:|:---:|
| Bağlantı testi və avtomatik panel təyini | ✅ | ✅ |
| Hesab yaratmaq | ✅ | ✅ |
| Dayandırmaq / bərpa etmək | ✅ | ✅ |
| Ləğv etmək | ✅ | ✅ *(sahiblik yoxlanılır)* |
| Şifrə dəyişmək | ✅ | ✅ |
| Paket / plan dəyişmək | ✅ | ✅ |
| Disk və trafik istifadəsinin sinxronizasiyası | ✅ | ✅ |
| Müştəri panelinə bir kliklə giriş | ✅ | ✅ |
| Admin tərəfindən bir kliklə giriş | ✅ | ✅ |

> 💡 **Dilerlər üçün hazırlanıb.** Root və ya admin girişi tələb olunmur; modul sizin öz diler
> hesabınızın icazələri ilə işləyir və yaratdığı hər hesab sizin kvotanızdan gedir.

---

## 📋 Tələblər

- Öz serverinizdə quraşdırılmış, admin girişiniz olan **WiseCP**
- **PHP** 7.4 – 8.4
- PHP genişlənmələri: `curl`, `simplexml`
- Ya **cPanel/WHM diler hesabı** (WHM API tokeni) &nbsp;ya da&nbsp; **Plesk diler hesabı**
  (API açarı və ya panel şifrəsi)
- WiseCP serverindən panel serverinə, panelin API portu üzərindən çıxış girişi

> ✅ Verilənlər bazasında cədvəl yaradılmır, cron tələb olunmur, composer asılılığı yoxdur.
> Quraşdırma bir qovluğu kopyalamaqdan ibarətdir.

---

## 🚀 Quraşdırma

### 1️⃣ Modulu yükləyin

`DNAHosting` qovluğunu WiseCP quraşdırmanızın `coremio/modules/Servers/` kataloquna kopyalayın.

```
wisecp/
└── coremio/
    └── modules/
        └── Servers/
            └── DNAHosting/     ← bura
```

### 2️⃣ Serveri əlavə edin

**Products / Services → Hosting/Server → Shared Server Settings → Add New Shared Server**

| Sahə | Nə daxil edilir |
|---|---|
| **Server Automation Type** | `DNAHosting` — qovluq adıdır, siyahıda olduğu kimi görünür |
| **IP Address** | Panel serverinin real ünvanı; modul bura qoşulur |
| **Username** | Həmin paneldəki diler istifadəçi adınız |
| **Password** | cPanel-də WHM API tokeni, Plesk-də API açarı və ya panel şifrəsi |
| **Connect with SSL** | İşarələyin |
| **Port** | cPanel üçün `2087`, Plesk üçün `8443` |

> ⚠️ **Formanın yuxarısındakı Hostname sahəsi yalnız etiketdir.** Modul qoşulmaq üçün **IP Address**
> sahəsini istifadə edir, onu yox. Serverləriniz siyahıda bu etiketlə görünür.

### 3️⃣ Bağlantını yoxlayın

Yadda saxlamazdan əvvəl **Test Connection** düyməsinə basın, ya da sadəcə yadda saxlayın — WiseCP
testi özü işlədir.

Yaşıl nəticə həm giriş məlumatlarını, həm təyin edilən paneli təsdiqləyir. Xəta halında konkret HTTP
kodu və ya panel xətası göstərilir; bax [Loglar və problemlərin həlli](#-loglar-və-problemlərin-həlli).

### 4️⃣ Server qrupu yaradın

Birdən çox serveriniz varsa, **Shared Server Settings → Server Groups** altında qrup yaradıb məhsulu
tək server yerinə qrupa bağlayın. İki paylama tipi təklif olunur:

- **Həmişə ən az dolu olan serverə əlavə et.**
- **Bir serveri tam dolana qədər doldur, sonra ən az dolu olana keç.**

Serverlər **Unassigned → Assigned** siyahıları arasında `Add` / `Remove` ilə daşınır.

> ⚠️ **Qrupu panel baxımından eyni cinsli saxlayın.** Məhsul formasındakı paket siyahısı həmin an
> seçilmiş **tək bir** serverdən çəkilir. Qrupda həm cPanel, həm Plesk serveri varsa, seçdiyiniz
> paket adının digər paneldə qarşılığı olmaya bilər və həmin serverə düşən sifariş *paket tapılmadı*
> ilə uğursuz olar.

### 5️⃣ Məhsulu tənzimləyin

**Products / Services → Hosting/Server → Web Hosting Packages** → paketi açın → **Module Settings**
bölməsi. **Server Selection** altında **Single Server** və ya **Server Group** seçib DNAHosting
serverinizi işarələyin. Bundan sonra modul öz sahələrini çəkir:

| Tənzimləmə | Dəyər |
|---|---|
| **Detected panel** | Həmin serverdə həqiqətən tapılan panel, məsələn `cPanel / WHM`. Burada xəta varsa, təyin uğursuz olub |
| **Package / Plan** | Həmin serverdən canlı çəkilən paket siyahısı |
| **Automatic Setup** | Açıq: sifariş avtomatik quraşdırılır. Bağlı: admin təsdiqi tələb olunur |

> 💡 **cPanel-də paket ön şəkilçisini dərd etməyin.** Paneldə `bakcay328_paket2` kimi görünən paket
> üçün modul `istifadəçiadı_` ön şəkilçisini özü həll edir. Plesk-də siyahı serverdə təyin edilmiş
> hər xidmət planıdır.

**Yadda saxlayın — modul istifadəyə hazırdır.** 🎉

**‼️Bu andan etibarən cPanel və Plesk diler hesablarını bütün WiseCP axınlarında modul üzərindən idarə edirsiniz. Yaratma, dayandırma və ləğv tamamilə WiseCP-nin nəzarətindədir.**

---

## 🔍 Loglar və problemlərin həlli

**Tools → Logs → Module Logs**

| Log | Nə vaxt yazır | Nə saxlayır |
|---|---|---|
| **Module Logs**<br>*Tools → Logs → Module Logs* | Yalnız **Module Logs** funksiyası açıq olduqda | Panelə göndərilən hər sorğu və qayıdan hər cavab, `createacct` və ya `webspace.add` kimi əməliyyat adı ilə etiketlənmiş şəkildə |

> 💡 Bunu açan keçid eyni səhifənin yuxarısındadır. Problemi təkrarlamazdan əvvəl açın, sonra bağlayın.

> 🔐 Serverin API tokeni və ya şifrəsi, modulun yaratdığı və ya dəyişdirdiyi hesab şifrələri və SSO
> sessiya tokenləri — həm sorğuda, həm cavabda — **yazılmazdan əvvəl** `***` ilə maskalanır.

### Tez-tez rast gəlinən xətalar

| Əlamət | Səbəb və həll |
|---|---|
| `HTTP 403` və ya xəta mətnində `cpanelresult` zərfi | Tokenin arxasındakı dilerin həmin çağırış üçün WHM səviyyəsində icazəsi yoxdur. **WHM → Resellers → Edit Reseller's ACL List** altında hesab siyahısı, yaratma, dayandırma, ləğv, şifrə, paket yüksəltmə, paket siyahısı, trafik və sessiya icazələrini verin, sonra tokeni **həmin diler kimi** **WHM → Development → Manage API Tokens** üzərindən yenidən yaradın |
| Plesk **11003** | API açarı başqa IP üçün verilib — WiseCP-nin qoşulduğu ünvan üçün yenisini yaradın və ya Password sahəsinə panel şifrəsini yazın |
| Plesk **1014** | Plesk bu serverin danışdığı XML-API versiyası üçün sorğu gövdəsini rədd etdi. Modulun güncəl versiyasını işlətdiyinizi yoxlayın; modul logu etiraz edilən elementi göstərir |
| Məhsul formasında paket siyahısı yerinə xəta mətni | Təyin və ya paket çağırışı uğursuz oldu; səbəb eyni sətirdə yazılıb |

> 💡 Digər hər HTTP xətası panelin cavab gövdəsindən çıxarılmış düz mətn xülasə ilə gəlir — çılpaq
> status kodu heç vaxt hekayənin hamısı deyil.

---

## 🧩 Bilinməsi lazım olanlar

<details>
<summary><b>Panel fərqləri</b></summary>

<br>

- **Plesk-də ləğv sahiblik yoxlanışı ilə aparılır.** Modulun açdığı hər hesab daxili bir kimliklə
  etiketlənir; bu etiket hər əməliyyatdan əvvəl yoxlanılır, beləliklə modul paneldə əl ilə
  yaradılmış abunəliyə heç vaxt yönəldilə bilməz.
- **Plesk-də işlək xidmətin domenini dəyişmək rədd edilir.** Plesk abunəliyi domeni ilə tapıldığına
  görə dəyişiklik sonrakı hər əməliyyatı daimi olaraq pozardı. cPanel-də domen redaktə oluna bilər;
  hesab siz paneldə dəyişənə qədər köhnə domenə xidmət göstərməyə davam edir.
- **Təkrarlanan domen qoruması.** Eyni domen həmin serverdə başqa aktiv və ya dayandırılmış xidmətə
  hələ bağlıdırsa, ləğv rədd edilir.

</details>

<details>
<summary><b>Panel təyini</b></summary>

<br>

Panel tipi heç yerdə konfiqurasiya edilmir. Modul ilk çağırışda serveri yoxlayır və hansı panelin
cavab verdiyini yadda saxlayır.

Port yalnız hansı panelin **əvvəl** yoxlanacağını müəyyən edir: `8443` və `8880` əvvəlcə Plesk-i,
digər hər dəyər əvvəlcə cPanel-i yoxlayır. Qərarın özü həmişə real API çağırışından gəlir və ilk
təxmin cavab verməzsə digər panel yoxlanılır. Yanlış port təyini yavaşladır, sındırmır.

</details>

<details>
<summary><b>Giriş məlumatları</b></summary>

<br>

Hər iki panel giriş məlumatını **Password** sahəsindən alır; WiseCP bu sahəni şifrəli saxlayır.
**Access Hash** sahəsi bu modulda heç istifadə olunmur və DNAHosting serverlərində göstərilmir.

Plesk-də modul giriş məlumatını əvvəlcə API açarı kimi sınayır, alınmazsa özü HTTP basic auth-a
keçir; hansını daxil etdiyinizi ona demək lazım deyil.

</details>

<details>
<summary><b>Əhatə xaricində</b></summary>

<br>

E-poçt hesabları və yönləndirmələrin idarəsi, diler hesabı satışı, mövcud hesabların WiseCP-yə idxalı
və admin tərəfində *root panelinə giriş* düyməsi. Modul yalnız **diler** giriş məlumatı saxlayır —
root yox — deməli aça biləcəyi bir root paneli yoxdur.

</details>

---

## 📄 Dəyişiklik jurnalı

Versiya-versiya dəyişikliklər [CHANGELOG.md](CHANGELOG.md) faylındadır.

---

<div align="center">

**DNA Reseller Hosting** · WiseCP üçün cPanel və Plesk diler modulu

[domainnameapi.com](https://www.domainnameapi.com) · [Diler paneli](https://dm.domainnameapi.com/hosting)

</div>
