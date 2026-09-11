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

**Gestione cuentas de revendedor de cPanel y Plesk desde un único módulo de servidor de WiseCP.**

Un módulo, dos paneles. Usted nunca elige el tipo de panel: el módulo se lo pregunta al servidor y
recuerda qué panel respondió.

![WiseCP](https://img.shields.io/badge/WiseCP-self--hosted-4A90D9?style=flat-square)
![PHP](https://img.shields.io/badge/PHP-7.4%20%E2%80%93%208.4-777BB4?style=flat-square&logo=php&logoColor=white)
![cPanel](https://img.shields.io/badge/cPanel%2FWHM-compatible-FF6C2C?style=flat-square)
![Plesk](https://img.shields.io/badge/Plesk-compatible-53BCE6?style=flat-square)

</div>

---

## 📑 Índice

- [✨ Qué hace](#-qué-hace)
- [📋 Requisitos](#-requisitos)
- [🚀 Instalación](#-instalación)
- [🔍 Registros y diagnóstico](#-registros-y-diagnóstico)
- [🧩 Cosas que conviene saber](#-cosas-que-conviene-saber)
- [📄 Historial de cambios](#-historial-de-cambios)

---

## ✨ Qué hace

| Función | cPanel/WHM | Plesk |
|---|:---:|:---:|
| Prueba de conexión y detección automática del panel | ✅ | ✅ |
| Creación de cuenta | ✅ | ✅ |
| Suspender / reactivar | ✅ | ✅ |
| Cancelación | ✅ | ✅ *(propiedad verificada)* |
| Cambio de contraseña | ✅ | ✅ |
| Cambio de paquete / plan | ✅ | ✅ |
| Sincronización de disco y tráfico | ✅ | ✅ |
| Acceso al panel del cliente con un clic | ✅ | ✅ |
| Acceso con un clic desde el área de administración | ✅ | ✅ |

> 💡 **Pensado para revendedores.** No necesita acceso root ni de administrador; el módulo trabaja
> con los permisos de su propia cuenta de revendedor, y cada cuenta que crea consume su cuota.

---

## 📋 Requisitos

- **WiseCP** en su propio servidor, con acceso de administrador
- **PHP** 7.4 – 8.4
- Extensiones de PHP: `curl`, `simplexml`
- Una **cuenta de revendedor de cPanel/WHM** (token de la API de WHM) &nbsp;o&nbsp; una **cuenta de
  revendedor de Plesk** (clave de API o la contraseña del panel)
- Acceso saliente desde el servidor de WiseCP al servidor del panel, en el puerto de la API del panel

> ✅ No se crea ninguna tabla en la base de datos, no hace falta cron y no hay dependencias de
> composer. La instalación consiste en copiar una carpeta.

---

## 🚀 Instalación

### 1️⃣ Instale el módulo

Copie la carpeta `DNAHosting` en el directorio `coremio/modules/Servers/` de su instalación de
WiseCP.

```
wisecp/
└── coremio/
    └── modules/
        └── Servers/
            └── DNAHosting/     ← aquí
```

### 2️⃣ Añada el servidor

**Products / Services → Hosting/Server → Shared Server Settings → Add New Shared Server**

| Campo | Qué introducir |
|---|---|
| **Server Automation Type** | `DNAHosting`: es el nombre de la carpeta y aparece tal cual en la lista |
| **IP Address** | La dirección real del servidor del panel; ahí se conecta el módulo |
| **Username** | Su usuario de revendedor en ese panel |
| **Password** | Un token de la API de WHM en cPanel; una clave de API o la contraseña del panel en Plesk |
| **Connect with SSL** | Márquelo |
| **Port** | `2087` para cPanel, `8443` para Plesk |

> ⚠️ **El campo Hostname de la parte superior del formulario es solo una etiqueta.** El módulo se
> conecta mediante **IP Address**, no mediante ese campo. En el listado sus servidores aparecen con
> esa etiqueta.

### 3️⃣ Pruebe la conexión

Pulse **Test Connection** antes de guardar, o guarde directamente: WiseCP ejecuta la prueba por su
cuenta.

Un resultado verde confirma tanto las credenciales como el panel detectado. Si falla, se muestra el
código HTTP concreto o el error del panel; vea [Registros y diagnóstico](#-registros-y-diagnóstico).

### 4️⃣ Cree un grupo de servidores

Si tiene más de un servidor, cree un grupo en **Shared Server Settings → Server Groups** y vincule
el producto al grupo en lugar de a un único servidor. Se ofrecen dos tipos de distribución:

- **Añadir siempre al servidor menos ocupado.**
- **Llenar un servidor por completo y luego pasar al menos ocupado.**

Los servidores se mueven entre las listas **Unassigned → Assigned** con `Add` / `Remove`.

> ⚠️ **Mantenga cada grupo homogéneo por panel.** La lista de paquetes del formulario del producto
> se obtiene del **único** servidor seleccionado en ese momento. Si un grupo contiene un servidor
> cPanel y otro Plesk, el nombre de paquete elegido puede no tener equivalente en el otro panel, y
> el pedido que caiga allí fallará con *paquete no encontrado*.

### 5️⃣ Configure el producto

**Products / Services → Hosting/Server → Web Hosting Packages** → abra el paquete → pestaña
**Module Settings**. En **Server Selection** elija **Single Server** o **Server Group** y marque su
servidor DNAHosting. Entonces el módulo dibuja sus propios campos:

| Ajuste | Valor |
|---|---|
| **Detected panel** | El panel encontrado realmente en ese servidor, por ejemplo `cPanel / WHM`. Un error aquí significa que la detección ha fallado |
| **Package / Plan** | La lista de paquetes obtenida en vivo de ese servidor |
| **Automatic Setup** | Activado: el pedido se aprovisiona automáticamente. Desactivado: requiere aprobación del administrador |

> 💡 **No se preocupe por el prefijo del paquete en cPanel.** Para un paquete que en el panel
> aparece como `bakcay328_paket2`, el módulo resuelve por su cuenta el prefijo `usuario_`. En Plesk
> la lista es cada plan de servicio definido en el servidor.

**Guárdelo: el módulo ya está listo.** 🎉

**‼️A partir de aquí gestiona las cuentas de revendedor de cPanel y Plesk desde el módulo en todos los flujos de WiseCP. La creación, la suspensión y la cancelación quedan enteramente bajo el control de WiseCP.**

---

## 🔍 Registros y diagnóstico

**Tools → Logs → Module Logs**

| Registro | Cuándo escribe | Qué contiene |
|---|---|---|
| **Module Logs**<br>*Tools → Logs → Module Logs* | Solo mientras la función **Module Logs** está activa | Cada petición enviada al panel y la respuesta recibida, etiquetadas con el nombre de la operación, como `createacct` o `webspace.add` |

> 💡 El interruptor está en la parte superior de esa misma página. Actívelo antes de reproducir el
> problema y desactívelo después.

> 🔐 El token de API o la contraseña del servidor, cualquier contraseña de cuenta que el módulo
> genere o cambie y los tokens de sesión SSO —tanto en la petición como en la respuesta— se
> enmascaran con `***` **antes de escribir nada**.

### Errores frecuentes

| Síntoma | Causa y solución |
|---|---|
| `HTTP 403`, o una envoltura `cpanelresult` en el texto del error | El revendedor al que pertenece el token no tiene privilegio de nivel WHM para esa llamada. Conceda en **WHM → Resellers → Edit Reseller's ACL List** los permisos de listado de cuentas, creación, suspensión, cancelación, contraseña, mejora de paquete, listado de paquetes, tráfico y sesión, y regenere después el token **como ese revendedor** en **WHM → Development → Manage API Tokens** |
| Plesk **11003** | La clave de API se emitió para otra IP: genere una nueva para la dirección desde la que conecta WiseCP, o ponga la contraseña del panel en el campo Password |
| Plesk **1014** | Plesk rechazó el cuerpo de la petición para la versión de XML-API que habla ese servidor. Compruebe que usa la versión actual del módulo; el log del módulo indica el elemento rechazado |
| Un texto de error en lugar de la lista de paquetes en el formulario del producto | Falló la detección o la llamada de paquetes; el motivo está escrito en esa misma línea |

> 💡 Cualquier otro error HTTP llega con un resumen en texto plano extraído del cuerpo de respuesta
> del panel: un código de estado a secas nunca es la historia completa.

---

## 🧩 Cosas que conviene saber

<details>
<summary><b>Diferencias entre paneles</b></summary>

<br>

- **La cancelación en Plesk verifica la propiedad.** Cada cuenta que abre el módulo se marca con un
  identificador interno; esa marca se comprueba antes de cualquier operación, de modo que el módulo
  nunca puede apuntar a una suscripción creada a mano en el panel.
- **Cambiar el dominio de un servicio en marcha se rechaza en Plesk.** Una suscripción de Plesk se
  localiza por su dominio, así que modificarlo haría fallar de forma permanente todas las
  operaciones posteriores. En cPanel el dominio sí puede editarse; la cuenta sigue sirviendo el
  dominio antiguo hasta que lo cambie en el panel.
- **Protección contra dominios duplicados.** La cancelación se rechaza mientras el mismo dominio
  siga vinculado a otro servicio activo o suspendido en el mismo servidor.

</details>

<details>
<summary><b>Detección del panel</b></summary>

<br>

El tipo de panel no se configura en ningún sitio. En la primera llamada el módulo sondea el
servidor y recuerda qué panel respondió.

El puerto solo decide qué panel se prueba **primero**: `8443` y `8880` prueban antes Plesk,
cualquier otro valor prueba antes cPanel. La decisión en sí procede siempre de una llamada real a
la API, y se prueba el otro panel cuando la primera suposición no responde. Un puerto equivocado
ralentiza la detección, no la rompe.

</details>

<details>
<summary><b>Credenciales</b></summary>

<br>

Ambos paneles reciben su credencial en el campo **Password**, que WiseCP guarda cifrado. El campo
**Access Hash** no lo usa nunca este módulo y ni siquiera se muestra en los servidores DNAHosting.

En Plesk el módulo prueba primero la credencial como clave de API y recurre por su cuenta a la
autenticación HTTP basic; no hace falta que le diga cuál ha introducido.

</details>

<details>
<summary><b>Fuera del alcance</b></summary>

<br>

La gestión de cuentas de correo y reenvíos, la venta de cuentas de revendedor, la importación de
cuentas existentes a WiseCP y un botón de *acceso al panel root* en el área de administración. El
módulo solo guarda una credencial de **revendedor** —nunca root—, así que no hay ningún panel root
que pueda abrir.

</details>

---

## 📄 Historial de cambios

Los cambios versión a versión están en [CHANGELOG.md](CHANGELOG.md).

---

<div align="center">

**DNA Reseller Hosting** · Módulo de revendedor cPanel y Plesk para WiseCP

[domainnameapi.com](https://www.domainnameapi.com) · [Panel de revendedor](https://dm.domainnameapi.com/hosting)

</div>
