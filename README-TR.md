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

**cPanel ve Plesk bayi hesaplarını tek bir WiseCP sunucu modülünden yönetin.**

Bir modül, iki panel. Panel tipini siz seçmezsiniz — modül sunucuya kendisi sorar ve hangi panelin
yanıt verdiğini hatırlar.

![WiseCP](https://img.shields.io/badge/WiseCP-self--hosted-4A90D9?style=flat-square)
![PHP](https://img.shields.io/badge/PHP-7.4%20%E2%80%93%208.4-777BB4?style=flat-square&logo=php&logoColor=white)
![cPanel](https://img.shields.io/badge/cPanel%2FWHM-destekleniyor-FF6C2C?style=flat-square)
![Plesk](https://img.shields.io/badge/Plesk-destekleniyor-53BCE6?style=flat-square)

</div>

---

## 📑 İçindekiler

- [✨ Neler yapar](#-neler-yapar)
- [📋 Gereksinimler](#-gereksinimler)
- [🚀 Kurulum](#-kurulum)
- [🔍 Kayıtlar ve sorun giderme](#-kayıtlar-ve-sorun-giderme)
- [🧩 Bilinmesi gerekenler](#-bilinmesi-gerekenler)
- [📄 Değişiklik günlüğü](#-değişiklik-günlüğü)

---

## ✨ Neler yapar

| Özellik | cPanel/WHM | Plesk |
|---|:---:|:---:|
| Bağlantı testi ve otomatik panel tespiti | ✅ | ✅ |
| Hesap oluşturma | ✅ | ✅ |
| Askıya alma / askıdan indirme | ✅ | ✅ |
| Sonlandırma | ✅ | ✅ *(sahiplik doğrulamalı)* |
| Şifre değiştirme | ✅ | ✅ |
| Paket / plan değiştirme | ✅ | ✅ |
| Disk ve trafik kullanımı eşitlemesi | ✅ | ✅ |
| Müşteri paneline tek tıkla giriş | ✅ | ✅ |
| Yönetici tarafından tek tıkla giriş | ✅ | ✅ |

> 💡 **Bayiler için yapıldı.** Root ya da yönetici erişimi gerekmez; modül kendi bayi hesabınızın
> yetkileriyle çalışır ve açtığı her hesap sizin kotanızdan düşer.

---

## 📋 Gereksinimler

- Kendi sunucunuzda kurulu, yönetici erişiminizin olduğu bir **WiseCP**
- **PHP** 7.4 – 8.4
- PHP eklentileri: `curl`, `simplexml`
- Bir **cPanel/WHM bayi hesabı** (WHM API token'ı) &nbsp;ya da&nbsp; bir **Plesk bayi hesabı**
  (API anahtarı veya panel şifresi)
- WiseCP sunucusundan panel sunucusuna, panelin API portunda dışa açık erişim

> ✅ Veritabanı tablosu oluşturulmaz, cron gerekmez, composer bağımlılığı yoktur. Kurulum bir klasörü
> kopyalamaktan ibarettir.

---

## 🚀 Kurulum

### 1️⃣ Modülü yükleyin

`DNAHosting` klasörünü WiseCP kurulumunuzun `coremio/modules/Servers/` dizinine kopyalayın.

```
wisecp/
└── coremio/
    └── modules/
        └── Servers/
            └── DNAHosting/     ← buraya
```

### 2️⃣ Sunucuyu ekleyin

**Ürünler / Hizmetler → Hosting/Sunucu → Paylaşımlı Sunucu Ayarları → Yeni Paylaşımlı Sunucu Ekle**

| Alan | Ne girilir |
|---|---|
| **Sunucu Otomasyon Türü** | `DNAHosting` — klasör adıdır, listede olduğu gibi görünür |
| **IP Adresi** | Panel sunucusunun gerçek adresi; modül buraya bağlanır |
| **Kullanıcı Adı** | O paneldeki bayi kullanıcı adınız |
| **Şifre** | cPanel'de WHM API token'ı, Plesk'te API anahtarı ya da panel şifresi |
| **SSL ile Bağlan** | İşaretleyin |
| **Port** | cPanel için `2087`, Plesk için `8443` |

> ⚠️ **Formun üst kısmındaki Hostname alanı yalnızca bir etikettir.** Modül bağlanmak için
> **IP Adresi** alanını kullanır, onu değil. Sunucularınız liste ekranında bu etiketle görünür.

### 3️⃣ Bağlantıyı test edin

Kaydetmeden önce **Bağlantıyı Sına** düğmesine basın ya da doğrudan kaydedin — WiseCP testi kendisi
çalıştırır.

Yeşil sonuç hem kimlik bilgisini hem tespit edilen paneli doğrular. Hata durumunda somut HTTP kodu
ya da panel hatası gösterilir; bkz. [Kayıtlar ve sorun giderme](#-kayıtlar-ve-sorun-giderme).

### 4️⃣ Sunucu grubu oluşturun

Birden fazla sunucunuz varsa **Paylaşımlı Sunucu Ayarları → Sunucu Grupları** altında grup oluşturup
ürünü tek sunucu yerine gruba bağlayın. İki dağıtım türü sunulur:

- **Her zaman en düşük doluluktaki sunucuya ekle.**
- **Bir sunucu tamamen dolana kadar ekle, ardından en düşük doluluktaki sunucuya geç.**

Sunucular **Atanmamış → Atanmış** listeleri arasında `Ekle` / `Kaldır` ile taşınır.

> ⚠️ **Grubu panel bazında homojen tutun.** Ürün formundaki paket listesi o an seçili olan **tek
> bir** sunucudan çekilir. Bir grupta hem cPanel hem Plesk sunucusu varsa seçtiğiniz paket adı diğer
> panelde karşılık bulmayabilir ve o sunucuya düşen sipariş *paket bulunamadı* ile başarısız olur.

### 5️⃣ Ürünü ayarlayın

**Ürünler / Hizmetler → Hosting/Sunucu → Web Hosting Paketleri** → paketi açın → **Modül Ayarları**
sekmesi. **Sunucu Seçimi** altında **Tekil Sunucu** ya da **Sunucu Grubu** seçip DNAHosting
sunucunuzu işaretleyin. Modül bunun üzerine kendi alanlarını çizer:

| Ayar | Değer |
|---|---|
| **Tespit edilen panel** | O sunucuda gerçekten bulunan panel, örneğin `cPanel / WHM`. Burada hata görünüyorsa tespit başarısız olmuştur |
| **Paket / Plan** | O sunucudan canlı çekilen paket listesi |
| **Otomatik Kurulum** | Açık: sipariş otomatik kurulur. Kapalı: yönetici onayı gerekir |

> 💡 **cPanel'de paket ön ekini dert etmeyin.** Panelde `bakcay328_paket2` olarak görünen bir paket
> için modül `kullanıcıadı_` ön ekini kendisi çözer. Plesk'te liste, sunucuda tanımlı her servis
> planıdır.

**Kaydedin — modül kullanıma hazır.** 🎉

**‼️Bu noktadan sonra cPanel ve Plesk bayi hesaplarını her WiseCP akışında modül üzerinden yönetebilirsiniz. Oluşturma, askıya alma ve sonlandırma tamamen WiseCP'nin denetimindedir.**

---

## 🔍 Kayıtlar ve sorun giderme

**Araçlar → İşlem Kayıtları (Logs) → Modül İşlem Kayıtları**

| Kayıt | Ne zaman yazar | Ne içerir |
|---|---|---|
| **Modül İşlem Kayıtları**<br>*Araçlar → İşlem Kayıtları → Modül İşlem Kayıtları* | Yalnızca **Modül İşlem Kayıtları** özelliği açıkken | Panele gönderilen her istek ve dönen her yanıt, `createacct` ya da `webspace.add` gibi işlem adıyla etiketlenmiş hâlde |

> 💡 Kaydı açan anahtar aynı sayfanın üst kısmındadır. Sorunu yeniden üretmeden önce açın, sonra
> kapatın.

> 🔐 Sunucunun API token'ı ya da şifresi, modülün ürettiği veya değiştirdiği hesap şifreleri ve SSO
> oturum jetonları — hem istekte hem yanıtta — **yazılmadan önce** `***` ile maskelenir.

### Sık karşılaşılan hatalar

| Belirti | Sebep ve çözüm |
|---|---|
| `HTTP 403` ya da hata metninde `cpanelresult` zarfı | Token'ın arkasındaki bayinin o çağrı için WHM düzeyinde yetkisi yok. **WHM → Resellers → Edit Reseller's ACL List** altında hesap listeleme, oluşturma, askıya alma, sonlandırma, şifre, paket yükseltme, paket listeleme, trafik ve oturum yetkilerini verin; ardından token'ı **o bayi olarak** **WHM → Development → Manage API Tokens** üzerinden yeniden üretin |
| Plesk **11003** | API anahtarı başka bir IP için üretilmiş — WiseCP'nin bağlandığı adres için yenisini üretin ya da Şifre alanına panel şifresini yazın |
| Plesk **1014** | Plesk, bu sunucunun konuştuğu XML-API sürümü için istek gövdesini reddetti. Modülün güncel sürümünü kullandığınızı doğrulayın; modül logu itiraz edilen elemanı gösterir |
| Ürün formunda paket listesi yerine hata metni | Tespit ya da paket çağrısı başarısız oldu; sebep aynı satırda yazılıdır |

> 💡 Diğer her HTTP hatası panelin yanıt gövdesinden çıkarılmış düz metin bir özetle gelir — çıplak
> bir durum kodu hiçbir zaman hikâyenin tamamı değildir.

---

## 🧩 Bilinmesi gerekenler

<details>
<summary><b>Panel farkları</b></summary>

<br>

- **Plesk'te sonlandırma sahiplik doğrulamalıdır.** Modülün açtığı her hesap dahilî bir kimlikle
  etiketlenir; bu etiket her işlemden önce kontrol edilir, böylece modül panelde elle oluşturulmuş
  bir aboneliğe asla yönlendirilemez.
- **Plesk'te canlı bir hizmetin alan adı değiştirilemez.** Plesk aboneliği alan adıyla bulunduğu
  için düzenleme sonraki her işlemi kalıcı olarak bozardı. cPanel'de alan adı düzenlenebilir; hesap,
  siz panelde değiştirene kadar eski alan adına hizmet vermeye devam eder.
- **Mükerrer alan adı koruması.** Aynı alan adı aynı sunucuda başka bir aktif ya da askıdaki hizmete
  hâlâ bağlıysa sonlandırma reddedilir.

</details>

<details>
<summary><b>Panel tespiti</b></summary>

<br>

Panel tipi hiçbir yerde yapılandırılmaz. Modül ilk çağrıda sunucuyu yoklar ve hangi panelin yanıt
verdiğini hatırlar.

Port yalnızca hangi panelin **önce** deneneceğini belirler: `8443` ve `8880` önce Plesk'i, diğer her
değer önce cPanel'i dener. Kararın kendisi her zaman gerçek bir API çağrısından gelir ve ilk tahmin
yanıt vermezse diğer panel denenir. Yanlış port tespiti yavaşlatır, bozmaz.

</details>

<details>
<summary><b>Kimlik bilgileri</b></summary>

<br>

Her iki panel de kimlik bilgisini **Şifre** alanından alır; WiseCP bu alanı şifreli saklar.
**Erişim Anahtarı (Access Hash)** alanı bu modülde hiç kullanılmaz ve DNAHosting sunucularında
formda görünmez.

Plesk'te modül kimlik bilgisini önce API anahtarı olarak dener, tutmazsa kendiliğinden HTTP basic
auth'a düşer; hangisini girdiğinizi ona söylemeniz gerekmez.

</details>

<details>
<summary><b>Kapsam dışı</b></summary>

<br>

E-posta hesabı ve yönlendirme yönetimi, bayi hesabı satışı, mevcut hesapların WiseCP'ye içe
aktarılması ve yönetici tarafında *root paneline giriş* düğmesi. Modül yalnızca bir **bayi** kimlik
bilgisi tutar — root değil — dolayısıyla açabileceği bir root paneli yoktur.

</details>

---

## 📄 Değişiklik günlüğü

Sürüm sürüm değişiklikler [CHANGELOG.md](CHANGELOG.md) dosyasında.

---

<div align="center">

**DNA Reseller Hosting** · WiseCP için cPanel & Plesk bayi modülü

[domainnameapi.com](https://www.domainnameapi.com) · [Bayi paneli](https://dm.domainnameapi.com/hosting)

</div>
