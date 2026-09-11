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

**أدِر حسابات الموزّعين على cPanel وPlesk من وحدة خوادم واحدة في WiseCP.**

وحدة واحدة، لوحتان. أنت لا تختار نوع اللوحة — الوحدة تسأل الخادم بنفسها وتتذكر أي لوحة استجابت.

![WiseCP](https://img.shields.io/badge/WiseCP-self--hosted-4A90D9?style=flat-square)
![PHP](https://img.shields.io/badge/PHP-7.4%20%E2%80%93%208.4-777BB4?style=flat-square&logo=php&logoColor=white)
![cPanel](https://img.shields.io/badge/cPanel%2FWHM-supported-FF6C2C?style=flat-square)
![Plesk](https://img.shields.io/badge/Plesk-supported-53BCE6?style=flat-square)

</div>

---

## 📑 المحتويات

- [✨ ما الذي تقوم به](#-ما-الذي-تقوم-به)
- [📋 المتطلبات](#-المتطلبات)
- [🚀 التثبيت](#-التثبيت)
- [🔍 السجلات وحل المشكلات](#-السجلات-وحل-المشكلات)
- [🧩 أمور ينبغي معرفتها](#-أمور-ينبغي-معرفتها)
- [📄 سجل التغييرات](#-سجل-التغييرات)

---

## ✨ ما الذي تقوم به

| الميزة | cPanel/WHM | Plesk |
|---|:---:|:---:|
| اختبار الاتصال والكشف التلقائي عن اللوحة | ✅ | ✅ |
| إنشاء الحسابات | ✅ | ✅ |
| التعليق / إلغاء التعليق | ✅ | ✅ |
| الإنهاء | ✅ | ✅ *(مع التحقق من الملكية)* |
| تغيير كلمة المرور | ✅ | ✅ |
| تغيير الباقة / الخطة | ✅ | ✅ |
| مزامنة استهلاك القرص وحركة البيانات | ✅ | ✅ |
| الدخول إلى لوحة العميل بنقرة واحدة | ✅ | ✅ |
| الدخول بنقرة واحدة من واجهة المدير | ✅ | ✅ |

> 💡 **مصمّمة للموزّعين.** لا تحتاج إلى صلاحية root أو مدير؛ تعمل الوحدة بصلاحيات حساب الموزّع
> الخاص بك، وكل حساب تنشئه يُحتسب من حصتك.

---

## 📋 المتطلبات

- **WiseCP** مثبّتة على خادمك ولديك صلاحية مدير عليها
- **PHP** 7.4 – 8.4
- امتدادات PHP: `curl` و`simplexml`
- إمّا **حساب موزّع cPanel/WHM** (رمز WHM API) &nbsp;أو&nbsp; **حساب موزّع Plesk**
  (مفتاح API أو كلمة مرور اللوحة)
- نفاذ صادر من خادم WiseCP إلى خادم اللوحة على منفذ API الخاص باللوحة

> ✅ لا يُنشأ أي جدول في قاعدة البيانات، ولا حاجة إلى cron، ولا توجد اعتماديات composer. التثبيت
> ليس أكثر من نسخ مجلد.

---

## 🚀 التثبيت

### 1️⃣ ثبِّت الوحدة

انسخ مجلد `DNAHosting` إلى الدليل `coremio/modules/Servers/` في تثبيت WiseCP لديك.

```
wisecp/
└── coremio/
    └── modules/
        └── Servers/
            └── DNAHosting/     ← هنا
```

### 2️⃣ أضف الخادم

**Products / Services → Hosting/Server → Shared Server Settings → Add New Shared Server**

| الحقل | ما يُدخل فيه |
|---|---|
| **Server Automation Type** | `DNAHosting` — وهو اسم المجلد، ويظهر في القائمة كما هو |
| **IP Address** | العنوان الحقيقي لخادم اللوحة؛ إليه تتصل الوحدة |
| **Username** | اسم مستخدم الموزّع لديك على تلك اللوحة |
| **Password** | رمز WHM API على cPanel، ومفتاح API أو كلمة مرور اللوحة على Plesk |
| **Connect with SSL** | فعّله |
| **Port** | `2087` لـ cPanel و`8443` لـ Plesk |

> ⚠️ **حقل Hostname في أعلى النموذج ليس إلا تسمية.** تتصل الوحدة عبر **IP Address** لا عبره. وتظهر
> خوادمك في القائمة تحت هذه التسمية.

### 3️⃣ اختبر الاتصال

اضغط **Test Connection** قبل الحفظ، أو احفظ مباشرة — فـ WiseCP يجري الاختبار من تلقاء نفسه.

النتيجة الخضراء تؤكد بيانات الاعتماد واللوحة المكتشفة معًا. وعند الفشل يظهر رمز HTTP أو خطأ اللوحة
بشكل محدد؛ راجع [السجلات وحل المشكلات](#-السجلات-وحل-المشكلات).

### 4️⃣ أنشئ مجموعة خوادم

إن كان لديك أكثر من خادم، أنشئ مجموعة من **Shared Server Settings → Server Groups** واربط المنتج
بالمجموعة بدل خادم واحد. ويتاح نوعان للتوزيع:

- **أضِف دائمًا إلى الخادم الأقل امتلاءً.**
- **املأ خادمًا واحدًا بالكامل ثم انتقل إلى الأقل امتلاءً.**

تُنقل الخوادم بين قائمتَي **Unassigned → Assigned** بزرَّي `Add` / `Remove`.

> ⚠️ **حافظ على تجانس المجموعة من حيث اللوحة.** قائمة الباقات في نموذج المنتج تُجلب من **خادم واحد**
> هو المحدَّد في تلك اللحظة. وإذا ضمّت المجموعة خادم cPanel وخادم Plesk معًا، فقد لا يكون لاسم
> الباقة نظير على اللوحة الأخرى، فيفشل الطلب الذي يقع على ذلك الخادم برسالة *الباقة غير موجودة*.

### 5️⃣ اضبط المنتج

**Products / Services → Hosting/Server → Web Hosting Packages** ← افتح الباقة ← تبويب **Module
Settings**. وتحت **Server Selection** اختر **Single Server** أو **Server Group** ثم حدِّد خادم
DNAHosting. عندها ترسم الوحدة حقولها الخاصة:

| الإعداد | القيمة |
|---|---|
| **Detected panel** | اللوحة الموجودة فعليًا على ذلك الخادم، مثل `cPanel / WHM`. وظهور خطأ هنا يعني فشل الكشف |
| **Package / Plan** | قائمة الباقات المجلوبة مباشرة من ذلك الخادم |
| **Automatic Setup** | مُفعّل: يُنشَأ الطلب تلقائيًا. مُعطّل: تلزم موافقة المدير |

> 💡 **لا تشغل بالك ببادئة الباقة على cPanel.** للباقة التي تظهر في اللوحة باسم `bakcay328_paket2`
> تحلّ الوحدة البادئة `username_` بنفسها. أما على Plesk فالقائمة هي كل خطة خدمة معرَّفة على الخادم.

**احفظ — الوحدة جاهزة للاستخدام.** 🎉

**‼️من هذه النقطة تدير حسابات الموزّعين على cPanel وPlesk عبر الوحدة في كل مسارات WiseCP. الإنشاء والتعليق والإنهاء كلها تحت سيطرة WiseCP بالكامل.**

---

## 🔍 السجلات وحل المشكلات

**Tools → Logs → Module Logs**

| السجل | متى يكتب | ماذا يحتوي |
|---|---|---|
| **Module Logs**<br>*Tools → Logs → Module Logs* | فقط أثناء تفعيل ميزة **Module Logs** | كل طلب يُرسل إلى اللوحة وكل استجابة تعود، موسومًا باسم العملية مثل `createacct` أو `webspace.add` |

> 💡 مفتاح التفعيل في أعلى الصفحة نفسها. فعّله قبل إعادة إنتاج المشكلة ثم أوقفه بعدها.

> 🔐 رمز API الخاص بالخادم أو كلمة مروره، وأي كلمات مرور حسابات تولّدها الوحدة أو تغيّرها، ورموز
> جلسات SSO — في الطلب والاستجابة معًا — تُقنَّع بـ `***` **قبل كتابة أي شيء**.

### الأخطاء الشائعة

| العَرَض | السبب والحل |
|---|---|
| `HTTP 403` أو ظهور غلاف `cpanelresult` في نص الخطأ | الموزّع صاحب الرمز لا يملك صلاحية على مستوى WHM لذلك الاستدعاء. امنح صلاحيات سرد الحسابات والإنشاء والتعليق والإنهاء وكلمة المرور وترقية الباقة وسرد الباقات وحركة البيانات وإنشاء الجلسة من **WHM → Resellers → Edit Reseller's ACL List**، ثم أعد توليد الرمز **بصفتك ذلك الموزّع** من **WHM → Development → Manage API Tokens** |
| Plesk **11003** | مفتاح API صادر لعنوان IP مختلف — ولّد مفتاحًا جديدًا للعنوان الذي يتصل منه WiseCP، أو ضع كلمة مرور اللوحة في حقل Password |
| Plesk **1014** | رفض Plesk جسم الطلب بالنسبة لإصدار XML-API الذي يتحدثه هذا الخادم. تأكد من استخدامك أحدث إصدار من الوحدة؛ وسجل الوحدة يذكر العنصر المرفوض |
| نص خطأ بدل قائمة الباقات في نموذج المنتج | فشل الكشف أو فشل استدعاء الباقات؛ والسبب مكتوب في السطر نفسه |

> 💡 كل خطأ HTTP آخر يصل مع ملخّص نصي مستخرج من جسم استجابة اللوحة — فرمز الحالة المجرَّد ليس القصة
> كاملة أبدًا.

---

## 🧩 أمور ينبغي معرفتها

<details>
<summary><b>الفروق بين اللوحتين</b></summary>

<br>

- **الإنهاء على Plesk يخضع للتحقق من الملكية.** كل حساب تفتحه الوحدة يُوسم بمعرّف داخلي، ويُفحص هذا
  الوسم قبل أي عملية، فلا يمكن توجيه الوحدة أبدًا إلى اشتراك أُنشئ يدويًا في اللوحة.
- **تغيير نطاق خدمة قائمة مرفوض على Plesk.** يُعثر على اشتراك Plesk عبر نطاقه، ولذلك فإن تعديله
  يجعل كل عملية لاحقة تفشل بشكل دائم. أما على cPanel فيمكن تعديل النطاق؛ ويظل الحساب يخدم النطاق
  القديم حتى تغيّره في اللوحة.
- **الحماية من تكرار النطاق.** يُرفض الإنهاء ما دام النطاق نفسه مرتبطًا بخدمة أخرى نشطة أو معلَّقة
  على الخادم ذاته.

</details>

<details>
<summary><b>الكشف عن اللوحة</b></summary>

<br>

لا يُضبط نوع اللوحة في أي مكان. تسبر الوحدة الخادم في أول استدعاء وتتذكر أي لوحة استجابت.

المنفذ يحدد فقط أي لوحة تُجرَّب **أولًا**: المنفذان `8443` و`8880` يجربان Plesk أولًا، وأي قيمة
أخرى تجرب cPanel أولًا. أما القرار نفسه فيأتي دائمًا من استدعاء API حقيقي، وتُجرَّب اللوحة الأخرى
إن لم يستجب التخمين الأول. المنفذ الخاطئ يبطئ الكشف ولا يعطّله.

</details>

<details>
<summary><b>بيانات الاعتماد</b></summary>

<br>

كلتا اللوحتين تأخذان بيانات الاعتماد من حقل **Password**، وتخزّنه WiseCP مشفَّرًا. أما حقل
**Access Hash** فلا تستخدمه هذه الوحدة إطلاقًا ولا يظهر أصلًا على خوادم DNAHosting.

على Plesk تجرّب الوحدة بيانات الاعتماد أولًا كمفتاح API ثم تتراجع من تلقاء نفسها إلى مصادقة HTTP
الأساسية، فلا حاجة لأن تخبرها بأيّهما أدخلت.

</details>

<details>
<summary><b>خارج النطاق</b></summary>

<br>

إدارة حسابات البريد والتحويلات، وبيع حسابات الموزّعين، واستيراد الحسابات القائمة إلى WiseCP، وزر
*الدخول إلى لوحة root* في واجهة المدير. فالوحدة لا تحمل سوى بيانات اعتماد **موزّع** — لا root —
فليست هناك لوحة root لتفتحها.

</details>

---

## 📄 سجل التغييرات

التغييرات إصدارًا بإصدار موجودة في [CHANGELOG.md](CHANGELOG.md).

---

<div align="center">

**DNA Reseller Hosting** · وحدة cPanel و Plesk للموزّعين على WiseCP

[domainnameapi.com](https://www.domainnameapi.com) · [لوحة الموزّع](https://dm.domainnameapi.com/hosting)

</div>
