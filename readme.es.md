## Documentación para CIDRAM v4 (Español).

### Contenidos
- 1. [PREÁMBULO](#user-content-SECTION1)
- 2. [CÓMO INSTALAR](#user-content-SECTION2)
- 3. [CÓMO USAR](#user-content-SECTION3)
- 4. [GESTIÓN DEL FRONT-END](#user-content-SECTION4)
- 5. [OPCIONES DE CONFIGURACIÓN](#user-content-SECTION5)
- 6. [FORMATO DE FIRMAS](#user-content-SECTION6)
- 7. [CONOCIDOS PROBLEMAS DE COMPATIBILIDAD](#user-content-SECTION7)
- 8. [PREGUNTAS MÁS FRECUENTES (FAQ)](#user-content-SECTION8)
- 9. [INFORMACIÓN LEGAL](#user-content-SECTION9)
- 10. [ACTUALIZACIÓN DE VERSIONES PRINCIPALES ANTERIORES](#user-content-SECTION10)

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### 1. <a name="SECTION1"></a>PREÁMBULO

CIDRAM (Classless Inter-Domain Routing Access Manager) es un script PHP diseñado para proteger sitios web bloqueando solicitudes desde direcciones IP consideradas como fuentes de tráfico no deseado, incluyendo (pero no limitado a) tráfico desde puntos de acceso inhumanos, servicios en la nube, spambots, scrapers, etc. Esto se hace calculando las posibles CIDRs de las direcciones IP suministradas desde solicitudes entrantes e intentando hacer coincidir estos posibles CIDRs en contra de sus archivos de firmas (estos archivos de firmas contienen listas de CIDRs de direcciones IP consideradas como fuentes de tráfico no deseado); Si se encuentran coincidencias, las solicitudes son bloqueadas.

*(Ver: [¿Qué es un "CIDR"?](#user-content-WHAT_IS_A_CIDR)).*

[CIDRAM](https://cidram.github.io/) COPYRIGHT 2016 y más allá GNU/GPLv2 por [Caleb M (Maikuolan)](https://github.com/Maikuolan).

Este script es un software gratuito; puede redistribuirlo y/o modificarlo según los términos de la GNU General Public License, publicada por la Free Software Foundation; tanto la versión 2 de la licencia como cualquier versión posterior. Este script es distribuido con la esperanza de que será útil, pero SIN NINGUNA GARANTÍA; también, sin ninguna implícita garantía de COMERCIALIZACIÓN o IDONEIDAD PARA UN PARTICULAR PROPÓSITO. Vea la GNU General Public License para más detalles, ubicada en el `LICENSE.txt` archivo también disponible en:
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

CIDRAM se puede descargar gratuitamente desde aquí:
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM).

Este documento y varias traducciones del mismo se pueden encontrar aquí:
- [GitHub](https://github.com/CIDRAM/Docs).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram-docs).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM-Docs).

---


### 2. <a name="SECTION2"></a>CÓMO INSTALAR

#### 2.0 INSTALACIÓN MANUAL

En primer lugar, necesitará una copia nueva de CIDRAM para trabajar. Puede descargar la última versión de CIDRAM desde el repositorio [CIDRAM/CIDRAM](https://github.com/CIDRAM/CIDRAM). Específicamente, necesitará una copia nueva del directorio "vault" (todo lo que esté fuera del directorio "vault" y su contenido se puede eliminar o descartar sin preocupaciones).

Antes de v3, era necesario instalar CIDRAM en algún lugar dentro de su raíz pública para poder acceder al front-end de CIDRAM. Pero, desde v3 en adelante, eso no es necesario, y para maximizar la seguridad y evitar el acceso no autorizado a CIDRAM y sus archivos, se recomienda instalar CIDRAM *fuera* de su raíz pública. No importa exactamente dónde elija instalar CIDRAM, siempre que sea un lugar accesible para PHP, un lugar razonablemente seguro, y un lugar con el que esté satisfecho. Tampoco es necesario mantener el nombre del directorio "vault", por lo que puede cambiar el nombre de "vault" por el nombre que prefiera (pero por el bien de conveniencia, la documentación continuará refiriéndose a él como el directorio "vault").

Cuando esté listo, cargue el directorio "vault" en la ubicación elegida, y asegúrese de que tenga los permisos necesarios para que PHP pueda escribir en el directorio (dependiendo del sistema en cuestión, a veces no necesitará hacer nada, o a veces deberá configurar CHMOD 755 en el directorio, o si hay problemas con 755, puede probar con 777, pero no se recomienda 777 debido a que es menos seguro).

A continuación, para que CIDRAM pueda proteger su base de código o CMS, deberá crear un "punto de entrada". Tal punto de entrada consta de tres cosas:

1. Inclusión del archivo "loader.php" en un punto apropiado en su base de código o CMS.
2. Instanciación del CIDRAM core.
3. Llamando al método "protect".

Un ejemplo sencillo:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

Si está utilizando un servidor web Apache y tiene acceso a `php.ini`, puede usar la directiva `auto_prepend_file` para anteponer CIDRAM siempre que se realice una solicitud de PHP. En tal caso, el lugar más apropiado para crear su punto de entrada sería en su propio archivo, que luego citaría en la directiva `auto_prepend_file`.

Ejemplo:

`auto_prepend_file = "/path/to/your/entrypoint.php"`

O esto en el archivo `.htaccess`:

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

En otros casos, el lugar más apropiado para crear su punto de entrada sería lo antes posible dentro de su base de código o CMS para que siempre se cargue cada vez que alguien acceda a cualquier página en todo su sitio web. Si su base de código utiliza un "bootstrap", un buen ejemplo sería al principio de su archivo "bootstrap". Si su base de código tiene un archivo central responsable de conectarse a su base de datos, otro buen ejemplo sería al principio de ese archivo central.

#### 2.1 INSTALACIÓN CON COMPOSER

[CIDRAM está registrado con Packagist](https://packagist.org/packages/cidram/cidram), y por lo tanto, si está familiarizado con Composer, puede utilizar Composer para instalar CIDRAM.

`composer require cidram/cidram`

#### 2.2 INSTALACIÓN PARA WORDPRESS

[CIDRAM está registrado como un plugin con la base de datos de plugins de WordPress](https://wordpress.org/plugins/cidram/), y puede instalar CIDRAM directamente desde el panel de plugins. Puede instalarlo de la misma manera que cualquier otro plugin, y no se requieren pasos adicionales.

*¡Advertencia: Actualizar CIDRAM a través del panel de plugins da como resultado una instalación limpia! Si ha personalizado su instalación (cambiado su configuración, módulos instalados, etc), estas personalizaciones se perderán al actualizar a través del panel de plugins! Los archivos de registro también se perderán al actualizar a través del panel de plugins! Para conservar los archivos de registro y las personalizaciones, actualice a través de la página de actualizaciones del front-end de CIDRAM.*

#### 2.3 CONFIGURACIÓN Y PERSONALIZACIÓN

Se recomienda encarecidamente que revise la configuración de su nueva instalación para que pueda ajustarla según sus necesidades. También es posible que desee instalar módulos adicionales, archivos de firma, crear reglas auxiliares, o implementar otras personalizaciones para que su instalación pueda adaptarse mejor a sus necesidades. Recomiendo usar el front-end para hacer estas cosas.

---


### 3. <a name="SECTION3"></a>CÓMO USAR

CIDRAM debe bloquear automáticamente las solicitudes indeseables a su website sin requiriendo intervención manual, aparte de sus instalación inicial.

Puede personalizar su configuración y personalizar cuál de los CIDRs son bloqueados por modificando su archivo de configuración y/o su archivos de firmas.

Si tiene algún falsos positivos, por favor contacto conmigo para decirme. *(Ver: [¿Qué es un "falso positivo"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM se puede actualizar manualmente o a través del front-end. CIDRAM también se puede actualizar a través de Composer o WordPress, si se instaló originalmente por esos medios.

---


### 4. <a name="SECTION4"></a>GESTIÓN DEL FRONT-END

#### 4.0 CUÁL ES EL FRONT-END.

El front-end proporciona una manera cómoda y fácil de mantener, administrar y actualizar la instalación de CIDRAM. Puede ver, compartir y descargar archivos de registro a través de la página de registros, puede modificar la configuración a través de la página de configuración, puede instalar y desinstalar componentes a través de la página de actualizaciones, y puede cargar, descargar y modificar archivos en su vault a través del administración de archivos.

#### 4.1 CÓMO ACCEDER EL FRONT-END.

Similar a cómo necesitaba crear un punto de entrada para que CIDRAM protegiera su sitio web, también deberá crear un punto de entrada para acceder al front-end. Tal punto de entrada consta de tres cosas:

1. Inclusión del archivo "loader.php" en un punto apropiado en su base de código o CMS.
2. Instanciación del CIDRAM front-end.
3. Llamando al método "view".

Un ejemplo sencillo:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

La clase "FrontEnd" amplía la clase "Core", lo que significa que, si lo desea, puede llamar al método "protect" antes de llamar al método "view" para bloquear el acceso del tráfico potencialmente no deseado al front-end. Hacerlo es totalmente opcional.

Un ejemplo sencillo:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

El lugar más apropiado para crear un punto de entrada para el front-end es su propio archivo dedicado. Diferente de su punto de entrada creado anteriormente, desea que su punto de entrada para el front-end sea accesible solo por medio de solicitando directamente el archivo específico donde existe el punto de entrada, de este modo no querrá usar `auto_prepend_file` o `.htaccess`.

Después de haber creado su punto de entrada para el front-end, use su navegador para acceder a él. Se debe presentar una página de login. En la página de login, ingrese el nombre de usuario y la contraseña predeterminados (admin/password) y presione el botón para iniciar sesión.

Nota: Después de iniciar la sesión por primera vez, con el fin de impedir el acceso no autorizado al front-end, usted debe cambiar inmediatamente su nombre de usuario y su contraseña! Esto es muy importante, ya que es posible subir código arbitrario de PHP a su sitio web a través del front-end.

Además, para una seguridad óptima, se recomienda encarecidamente habilitar la "autenticación de dos factores" para todas las cuentas del front-end (se proporcionan instrucciones a continuación).

#### 4.2 CÓMO UTILIZAR EL FRONT-END.

Las instrucciones se proporcionan en cada página del front-end, para explicar la manera correcta de usarlo y su propósito. Si necesita más explicaciones o cualquier ayuda especial, póngase en contacto con el soporte. Alternativamente, hay algunos videos disponibles en YouTube que podrían ayudar a modo de demostración.

#### 4.3 AUTENTICACIÓN DE DOS FACTORES

Es posible hacer que el front-end sea más seguro habilitando la autenticación de dos factores ("2FA"). Cuando se inicia una sesión usando una cuenta habilitada para 2FA, se envía un correo electrónico a la dirección de correo electrónico asociada con esa cuenta. Este correo electrónico contiene un "código 2FA", que el usuario debe ingresar, además del nombre de usuario y la contraseña, para poder iniciar sesión con esa cuenta. Esto significa que la obtención de una contraseña de cuenta no sería suficiente para que cualquier hacker o posible atacante pueda iniciar sesión en esa cuenta, ya que también necesitarían tener acceso a la dirección de correo electrónico asociada con esa cuenta para poder recibir y utilizar el código 2FA asociado a la sesión, por lo tanto haciendo el front-end más seguro.

En primer lugar, para habilitar la autenticación de dos factores, utilizando la página de actualizaciones del front-end, instale el componente PHPMailer. CIDRAM utiliza PHPMailer para enviar correos electrónicos.

Después de instalar PHPMailer, deberá llenar las directivas de configuración de PHPMailer a través de la página de configuración de CIDRAM o el archivo de configuración. Se incluye más información sobre estas directivas de configuración en la sección de configuración de este documento. Después de haber llenado las directivas de configuración de PHPMailer, configure `enable_two_factor` a `true`. La autenticación de dos factores ahora debería estar habilitada.

A continuación, deberá asociar una dirección de correo electrónico con una cuenta, para que CIDRAM sepa a dónde enviar códigos 2FA cuando inicie sesión con esa cuenta. Para hacer esto, use la dirección de correo electrónico como el nombre de usuario de la cuenta (como `foo@bar.tld`), o incluya la dirección de correo electrónico como parte del nombre de usuario de la misma manera que lo haría al enviar un correo electrónico normalmente (como `Foo Bar <foo@bar.tld>`).

Nota: Proteger su vault contra el acceso no autorizado (p.ej., a modo de endureciendo la seguridad de su servidor y los permisos de acceso público), es particularmente importante aquí, debido a ese acceso no autorizado a su archivo de configuración (que se almacena en su vault), podría exponer la configuración de SMTP saliente (incluido el nombre de usuario y la contraseña de SMTP). Debe asegurarse de que su vault esté correctamente asegurada antes de habilitar la autenticación de dos factores. Si no puede hacer esto, al menos, debe crear una nueva cuenta de correo electrónico, dedicada a tal fin, para reducir los riesgos asociados con la configuración SMTP expuesta.

---


### 5. <a name="SECTION5"></a>OPCIONES DE CONFIGURACIÓN

La siguiente es una lista de variables encuentran en la `config.yml` configuración archivo de CIDRAM, junto con una descripción de sus propósito y función.

```
Configuración (v4)
│
├───general
│       stages [string]
│       fields [string]
│       timezone [string]
│       time_offset [int]
│       time_format [string]
│       ipaddr [string]
│       http_response_header_code [int]
│       silent_mode [string]
│       silent_mode_response_header_code [int]
│       lang [string]
│       lang_override [bool]
│       numbers [string]
│       emailaddr [string]
│       emailaddr_display_style [string]
│       default_dns [string]
│       default_algo [string]
│       statistics [string]
│       statistics_captchas [string]
│       force_hostname_lookup [bool]
│       allow_gethostbyaddr_lookup [bool]
│       disabled_channels [string]
│       request_proxy [string]
│       request_proxyauth [string]
│       default_timeout [int]
│       sensitive [string]
│       email_notification_address [string]
│       email_notification_name [string]
│       email_notification_when [string]
├───components
│       ipv4 [string]
│       ipv6 [string]
│       modules [string]
│       imports [string]
│       events [string]
├───logging
│       standard_log [string]
│       apache_style_log [string]
│       serialised_log [string]
│       error_log [string]
│       outbound_request_log [string]
│       report_log [string]
│       truncate [string]
│       log_rotation_limit [int]
│       log_rotation_action [string]
│       log_banned_ips [bool]
│       log_sanitisation [bool]
├───frontend
│       frontend_log [string]
│       signatures_update_event_log [string]
│       max_login_attempts [int]
│       theme [string]
│       theme_mode [string]
│       magnification [float]
│       custom_header [string]
│       custom_footer [string]
│       remotes [string]
│       enable_two_factor [bool]
├───signatures
│       shorthand [string]
│       default_tracktime [string]
│       infraction_limit [int]
│       tracking_override [bool]
│       conflict_response [int]
├───verification
│       search_engines [string]
│       social_media [string]
│       other [string]
│       adjust [string]
├───captcha
│       usemode [int]
│       nonblocked_status_code [int]
│       api [string]
│       messages [string]
│       lockto [string]
│       hcaptcha_sitekey [string]
│       hcaptcha_secret [string]
│       friendly_sitekey [string]
│       friendly_apikey [string]
│       turnstile_sitekey [string]
│       turnstile_secret [string]
│       expiry [float]
│       signature_limit [int]
│       log [string]
├───legal
│       pseudonymise_ip_addresses [bool]
│       privacy_policy [string]
├───template_data
│       theme [string]
│       theme_mode [string]
│       magnification [float]
│       css_url [string]
│       block_event_title [string]
│       captcha_title [string]
│       custom_header [string]
│       custom_footer [string]
├───rate_limiting
│       max_bandwidth [string]
│       max_requests [int]
│       precision_ipv4 [int]
│       precision_ipv6 [int]
│       allowance_period [string]
│       exceptions [string]
│       segregate [bool]
├───supplementary_cache_options
│       prefix [string]
│       enable_apcu [bool]
│       enable_memcached [bool]
│       enable_redis [bool]
│       enable_pdo [bool]
│       memcached_host [string]
│       memcached_port [int]
│       redis_host [string]
│       redis_port [int]
│       redis_timeout [float]
│       redis_database_number [int]
│       pdo_dsn [string]
│       pdo_username [string]
│       pdo_password [string]
└───bypasses
        used [string]
```

#### "general" (Categoría)
Configuración general (cualquier configuración que no pertenezca a otras categorías).

##### "stages" `[string]`
- Controles para las etapas de la cadena de ejecución (si está habilitado, si se registran errores, etc).

```
stages───[¿Habilitar esta etapa?]─[¿Registrar los errores generados durante esta etapa?]─[¿Las infracciones generadas durante esta etapa deben contar para el seguimiento de IP?]
├─BanCheck ("Comprobar si está prohibido")
├─Tests ("Ejecutar pruebas de los archivos de firma")
├─Modules ("Ejecutar módulos")
├─SearchEngineVerification ("Ejecutar la verificación del motor de búsqueda")
├─SocialMediaVerification ("Ejecutar la verificación de las redes sociales")
├─OtherVerification ("Ejecutar otra verificación")
├─Aux ("Ejecutar reglas auxiliares")
├─Tracking ("Ejecutar seguimiento de IP")
├─RL ("Ejecutar la limitación de tasa")
├─CAPTCHA ("Desplegar CAPTCHAs (solicitudes bloqueadas)")
├─Reporting ("Ejecutar reportes")
├─Statistics ("Actualizar estadísticas")
├─Webhooks ("Ejecutar webhooks")
├─TriggerNotifications ("Procesar la cola de notificaciones de desencadenamiento por correo electrónico")
├─PrepareFields ("Preparar campos para salida y registros")
├─Output ("Generar salida (solicitudes bloqueadas)")
├─WriteLogs ("Escribir en registros (solicitudes bloqueadas)")
├─Terminate ("Terminar la solicitud (solicitudes bloqueadas)")
├─AuxRedirect ("Redirigir según reglas auxiliares")
└─NonBlockedCAPTCHA ("Desplegar CAPTCHAs (solicitudes no bloqueadas)")
```

##### "fields" `[string]`
- Controles para los campos durante eventos de bloque (cuando se bloquea una solicitud).

```
fields───[¿Debería aparecer este campo en las entradas de registro?]─[¿Debería aparecer este campo en la página "acceso denegado"?]─[¿Omitir este campo cuando está vacío?]
├─ID ("ID")
├─ScriptIdent ("Guión versión")
├─DateTime ("Fecha/Hora")
├─IPAddr ("Dirección IP")
├─IPAddrResolved ("Dirección IP (resuelto)")
├─Query ("Consulta")
├─Referrer ("Referente")
├─UA ("Agente de usuario")
├─UALC ("Agente de usuario (minúscula)")
├─SignatureCount ("Recuento de firmas")
├─Signatures ("Firmas referencias")
├─WhyReason ("Razón bloqueado")
├─ReasonMessage ("Razón bloqueado (detallado)")
├─rURI ("Reconstruida URI")
├─Infractions ("Infracciones")
├─ASNLookup ("** Búsqueda de ASN")
├─CCLookup ("** Búsqueda de código de país")
├─Verified ("Identidad verificada")
├─Expired ("Expirado")
├─Ignored ("Ignorado")
├─Request_Method ("Método de solicitud")
├─Protocol ("Protocolo")
├─SEC_CH_UA_PLATFORM ("!! SEC_CH_UA_PLATFORM")
├─SEC_CH_UA_MOBILE ("!! SEC_CH_UA_MOBILE")
├─SEC_CH_UA ("!! SEC_CH_UA")
├─Hostname ("Nombre de host")
├─CAPTCHA ("Estado CAPTCHA")
├─Inspection ("* Inspección de condiciones")
└─ClientL10NAccepted ("Resolución de idioma")
```

* Destinado solo para reglas auxiliares. No se muestra a los usuarios bloqueados.

** Requiere la funcionalidad de búsqueda de ASN (por ejemplo, a través del módulo IP-API o BGPView).

!! Esta es una sugerencia de cliente de baja entropía. Las sugerencias de cliente son una tecnología web nueva y experimental que aún no es ampliamente compatible con todos los navegadores y clientes principales. *Ver: <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA#browser_compatibility" dir="ltr" hreflang="en-US" rel="noopener noreferrer external">Sec-CH-UA - HTTP | MDN</a>.* Aunque las sugerencias de los clientes pueden ser útiles para la toma de huellas digitales, ya que no cuentan con un amplio soporte, no se debe asumir ni confiar en su presencia en las solicitudes (es decir, bloquear en función de su ausencia es una mala idea).

##### "timezone" `[string]`
- Esto se usa para especificar la zona horaria a usar (por ejemplo, Africa/Cairo, America/New_York, Asia/Tokyo, Australia/Perth, Europe/Berlin, Pacific/Guam, etc). Especifique "SYSTEM" para permitir que PHP maneje esto automáticamente.

```
timezone
├─SYSTEM ("Usar la zona horaria predefinida del sistema.")
├─UTC ("UTC")
└─…Otro
```

##### "time_offset" `[int]`
- Desplazamiento del huso horario en minutos.

##### "time_format" `[string]`
- El formato de notación de fecha/hora usado por CIDRAM. Se pueden añadir opciones adicionales bajo petición.

```
time_format
├─{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss} {tz} ("{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss} {tz}")
├─{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss} ("{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss}")
├─{Day}, {dd} {Mon} {yyyy} ("{Day}, {dd} {Mon} {yyyy}")
├─{yyyy}.{mm}.{dd} {hh}:{ii}:{ss} {tz} ("{yyyy}.{mm}.{dd} {hh}:{ii}:{ss} {tz}")
├─{yyyy}.{mm}.{dd} {hh}:{ii}:{ss} ("{yyyy}.{mm}.{dd} {hh}:{ii}:{ss}")
├─{yyyy}.{mm}.{dd} ("{yyyy}.{mm}.{dd}")
├─{yyyy}-{mm}-{dd} {hh}:{ii}:{ss} {tz} ("{yyyy}-{mm}-{dd} {hh}:{ii}:{ss} {tz}")
├─{yyyy}-{mm}-{dd} {hh}:{ii}:{ss} ("{yyyy}-{mm}-{dd} {hh}:{ii}:{ss}")
├─{yyyy}-{mm}-{dd} ("{yyyy}-{mm}-{dd}")
├─{yyyy}/{mm}/{dd} {hh}:{ii}:{ss} {tz} ("{yyyy}/{mm}/{dd} {hh}:{ii}:{ss} {tz}")
├─{yyyy}/{mm}/{dd} {hh}:{ii}:{ss} ("{yyyy}/{mm}/{dd} {hh}:{ii}:{ss}")
├─{yyyy}/{mm}/{dd} ("{yyyy}/{mm}/{dd}")
├─{dd}.{mm}.{yyyy} {hh}:{ii}:{ss} {tz} ("{dd}.{mm}.{yyyy} {hh}:{ii}:{ss} {tz}")
├─{dd}.{mm}.{yyyy} {hh}:{ii}:{ss} ("{dd}.{mm}.{yyyy} {hh}:{ii}:{ss}")
├─{dd}.{mm}.{yyyy} ("{dd}.{mm}.{yyyy}")
├─{dd}-{mm}-{yyyy} {hh}:{ii}:{ss} {tz} ("{dd}-{mm}-{yyyy} {hh}:{ii}:{ss} {tz}")
├─{dd}-{mm}-{yyyy} {hh}:{ii}:{ss} ("{dd}-{mm}-{yyyy} {hh}:{ii}:{ss}")
├─{dd}-{mm}-{yyyy} ("{dd}-{mm}-{yyyy}")
├─{dd}/{mm}/{yyyy} {hh}:{ii}:{ss} {tz} ("{dd}/{mm}/{yyyy} {hh}:{ii}:{ss} {tz}")
├─{dd}/{mm}/{yyyy} {hh}:{ii}:{ss} ("{dd}/{mm}/{yyyy} {hh}:{ii}:{ss}")
├─{dd}/{mm}/{yyyy} ("{dd}/{mm}/{yyyy}")
├─{mm}.{dd}.{yyyy} {hh}:{ii}:{ss} {tz} ("{mm}.{dd}.{yyyy} {hh}:{ii}:{ss} {tz}")
├─{mm}.{dd}.{yyyy} {hh}:{ii}:{ss} ("{mm}.{dd}.{yyyy} {hh}:{ii}:{ss}")
├─{mm}.{dd}.{yyyy} ("{mm}.{dd}.{yyyy}")
├─{mm}-{dd}-{yyyy} {hh}:{ii}:{ss} {tz} ("{mm}-{dd}-{yyyy} {hh}:{ii}:{ss} {tz}")
├─{mm}-{dd}-{yyyy} {hh}:{ii}:{ss} ("{mm}-{dd}-{yyyy} {hh}:{ii}:{ss}")
├─{mm}-{dd}-{yyyy} ("{mm}-{dd}-{yyyy}")
├─{mm}/{dd}/{yyyy} {hh}:{ii}:{ss} {tz} ("{mm}/{dd}/{yyyy} {hh}:{ii}:{ss} {tz}")
├─{mm}/{dd}/{yyyy} {hh}:{ii}:{ss} ("{mm}/{dd}/{yyyy} {hh}:{ii}:{ss}")
├─{mm}/{dd}/{yyyy} ("{mm}/{dd}/{yyyy}")
├─{yy}.{mm}.{dd} {hh}:{ii}:{ss} {tz} ("{yy}.{mm}.{dd} {hh}:{ii}:{ss} {tz}")
├─{yy}.{mm}.{dd} {hh}:{ii}:{ss} ("{yy}.{mm}.{dd} {hh}:{ii}:{ss}")
├─{yy}.{mm}.{dd} ("{yy}.{mm}.{dd}")
├─{yy}-{mm}-{dd} {hh}:{ii}:{ss} {tz} ("{yy}-{mm}-{dd} {hh}:{ii}:{ss} {tz}")
├─{yy}-{mm}-{dd} {hh}:{ii}:{ss} ("{yy}-{mm}-{dd} {hh}:{ii}:{ss}")
├─{yy}-{mm}-{dd} ("{yy}-{mm}-{dd}")
├─{yy}/{mm}/{dd} {hh}:{ii}:{ss} {tz} ("{yy}/{mm}/{dd} {hh}:{ii}:{ss} {tz}")
├─{yy}/{mm}/{dd} {hh}:{ii}:{ss} ("{yy}/{mm}/{dd} {hh}:{ii}:{ss}")
├─{yy}/{mm}/{dd} ("{yy}/{mm}/{dd}")
├─{dd}.{mm}.{yy} {hh}:{ii}:{ss} {tz} ("{dd}.{mm}.{yy} {hh}:{ii}:{ss} {tz}")
├─{dd}.{mm}.{yy} {hh}:{ii}:{ss} ("{dd}.{mm}.{yy} {hh}:{ii}:{ss}")
├─{dd}.{mm}.{yy} ("{dd}.{mm}.{yy}")
├─{dd}-{mm}-{yy} {hh}:{ii}:{ss} {tz} ("{dd}-{mm}-{yy} {hh}:{ii}:{ss} {tz}")
├─{dd}-{mm}-{yy} {hh}:{ii}:{ss} ("{dd}-{mm}-{yy} {hh}:{ii}:{ss}")
├─{dd}-{mm}-{yy} ("{dd}-{mm}-{yy}")
├─{dd}/{mm}/{yy} {hh}:{ii}:{ss} {tz} ("{dd}/{mm}/{yy} {hh}:{ii}:{ss} {tz}")
├─{dd}/{mm}/{yy} {hh}:{ii}:{ss} ("{dd}/{mm}/{yy} {hh}:{ii}:{ss}")
├─{dd}/{mm}/{yy} ("{dd}/{mm}/{yy}")
├─{mm}.{dd}.{yy} {hh}:{ii}:{ss} {tz} ("{mm}.{dd}.{yy} {hh}:{ii}:{ss} {tz}")
├─{mm}.{dd}.{yy} {hh}:{ii}:{ss} ("{mm}.{dd}.{yy} {hh}:{ii}:{ss}")
├─{mm}.{dd}.{yy} ("{mm}.{dd}.{yy}")
├─{mm}-{dd}-{yy} {hh}:{ii}:{ss} {tz} ("{mm}-{dd}-{yy} {hh}:{ii}:{ss} {tz}")
├─{mm}-{dd}-{yy} {hh}:{ii}:{ss} ("{mm}-{dd}-{yy} {hh}:{ii}:{ss}")
├─{mm}-{dd}-{yy} ("{mm}-{dd}-{yy}")
├─{mm}/{dd}/{yy} {hh}:{ii}:{ss} {tz} ("{mm}/{dd}/{yy} {hh}:{ii}:{ss} {tz}")
├─{mm}/{dd}/{yy} {hh}:{ii}:{ss} ("{mm}/{dd}/{yy} {hh}:{ii}:{ss}")
├─{mm}/{dd}/{yy} ("{mm}/{dd}/{yy}")
├─{yyyy}年{m}月{d}日 {hh}時{ii}分{ss}秒 ("{yyyy}年{m}月{d}日 {hh}時{ii}分{ss}秒")
├─{yyyy}年{m}月{d}日 {hh}:{ii}:{ss} {tz} ("{yyyy}年{m}月{d}日 {hh}:{ii}:{ss} {tz}")
├─{yyyy}年{m}月{d}日 ("{yyyy}年{m}月{d}日")
├─{yy}年{m}月{d}日 {hh}時{ii}分{ss}秒 ("{yy}年{m}月{d}日 {hh}時{ii}分{ss}秒")
├─{yy}年{m}月{d}日 {hh}:{ii}:{ss} {tz} ("{yy}年{m}月{d}日 {hh}:{ii}:{ss} {tz}")
├─{yy}年{m}月{d}日 ("{yy}年{m}月{d}日")
├─{yyyy}년 {m}월 {d}일 {hh}시 {ii}분 {ss}초 ("{yyyy}년 {m}월 {d}일 {hh}시 {ii}분 {ss}초")
├─{yyyy}년 {m}월 {d}일 {hh}:{ii}:{ss} {tz} ("{yyyy}년 {m}월 {d}일 {hh}:{ii}:{ss} {tz}")
├─{yyyy}년 {m}월 {d}일 ("{yyyy}년 {m}월 {d}일")
├─{yy}년 {m}월 {d}일 {hh}시 {ii}분 {ss}초 ("{yy}년 {m}월 {d}일 {hh}시 {ii}분 {ss}초")
├─{yy}년 {m}월 {d}일 {hh}:{ii}:{ss} {tz} ("{yy}년 {m}월 {d}일 {hh}:{ii}:{ss} {tz}")
├─{yy}년 {m}월 {d}일 ("{yy}년 {m}월 {d}일")
├─{yyyy}-{mm}-{dd}T{hh}:{ii}:{ss}{t:z} ("{yyyy}-{mm}-{dd}T{hh}:{ii}:{ss}{t:z}")
├─{d}. {m}. {yyyy} ("{d}. {m}. {yyyy}")
└─…Otro
```

__*Marcador de posición – Explicación – Ejemplo basado en 2024-04-30T18:27:49+08:00.*__<br />
`{yyyy}` – El año – P.ej. 2024.<br />
`{yy}` – El año abreviado – P.ej. 24.<br />
`{Mon}` – El nombre abreviado del mes (en inglés) – P.ej. Apr.<br />
`{mm}` – El mes con ceros a la izquierda – P.ej. 04.<br />
`{m}` – El mes – P.ej. 4.<br />
`{Day}` – El nombre abreviado del día (en inglés) – P.ej. Tue.<br />
`{dd}` – El día con ceros a la izquierda – P.ej. 30.<br />
`{d}` – El día – P.ej. 30.<br />
`{hh}` – La hora con ceros a la izquierda (utiliza el formato de 24 horas) – P.ej. 18.<br />
`{h}` – La hora (utiliza el formato de 24 horas) – P.ej. 18.<br />
`{ii}` – El minuto con ceros a la izquierda – P.ej. 27.<br />
`{i}` – El minuto – P.ej. 27.<br />
`{ss}` – El segundo con ceros a la izquierda – P.ej. 49.<br />
`{s}` – El segundo – P.ej. 49.<br />
`{tz}` – La zona horaria (sin dos puntos) – P.ej. +0800.<br />
`{t:z}` – La zona horaria (con dos puntos) – P.ej. +08:00.

##### "ipaddr" `[string]`
- ¿Dónde puedo encontrar el IP dirección de las solicitudes entrantes? (Útil para servicios como Cloudflare). Predefinido = REMOTE_ADDR. ¡AVISO: No cambie esto a menos que sepas lo que estás haciendo!

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (Predefinido)")
└─…Otro
```

Ver también:
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### "http_response_header_code" `[int]`
- ¿Cuál mensaje de estado HTTP debe enviar CIDRAM cuando se bloquean las solicitudes?

```
http_response_header_code───[Predefinido]─[Legal]─[Prohibido]
├─200 (200 OK): Menos robusto, pero más fácil de usar. Lo más probable que las
│ solicitudes automatizadas interpreten esta respuesta como una indicación de
│ que la solicitud fue exitosa. Recomendado para solicitudes no bloqueadas.
├─403 (403 Forbidden (Prohibido)): Un poco más robusto, pero un poco menos fácil de usar. Recomendado para la
│ mayoría de las circunstancias generales.
├─410 (410 Gone (Ido)): Podría causar problemas a la hora de resolver falsos positivos, ya que
│ algunos navegadores almacenan en caché este mensaje de estado y no envían
│ solicitudes posteriores, incluso después de haber sido desbloqueados. Puede
│ ser el más preferible en algunos contextos, para ciertos tipos de tráfico.
├─418 (418 I'm a teapot (Soy una tetera)): Hace referencia a una broma del Día de los Inocentes (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Es muy poco probable que
│ cualquier cliente, bot, navegador, u otro lo entiendará. Provisto por
│ diversión y conveniencia, pero generalmente no recomendado.
├─451 (451 Unavailable For Legal Reasons (No disponible por razones legales)): Recomendado cuando se bloquea principalmente por razones legales. No
│ recomendado en otros contextos.
└─503 (503 Service Unavailable (Servicio no disponible)): Más robusto, pero menos fácil de usar. Recomendado para cuando está bajo
  ataque, o para cuando se trata de tráfico no deseado extremadamente
  persistente.
```

__1.__ Cuando el "modo silencioso" está activo, se utilizará el mensaje de estado HTTP definido por `general➡silent_mode_response_header_code` (esto tiene la mayor precedencia).

__2.__ Cuando la entidad solicitante haya sido prohibido por exceder el límite de infracciones, se utilizará el mensaje de estado HTTP "prohibido".

__3.__ Cuando se bloquea debido a una limitación de tasa, se utilizará 429, o cuando se bloquea debido a conflictos de recursos, se utilizará el mensaje de estado HTTP definido por `signatures➡conflict_response` (la limitación de tasa y los conflictos por los recursos tienen igual precedencia en este contexto).

__4.__ Cuando se bloquea debido a una regla auxiliar que establece una "reemplazo del código de estado HTTP", se utilizará esa reemplazo del código de estado HTTP.

__5.__ Cuando se bloquea debido a razones legales (es decir, cuando se bloquea debido a una firma personalizada que utiliza la palabra abreviada "legal"), se utilizará el mensaje de estado HTTP para "legal".

__6.__ Para todas las demás solicitudes bloqueadas, se utilizará el mensaje de estado HTTP "predefinido" (este tiene la precedencia más baja).

##### "silent_mode" `[string]`
- Debería CIDRAM silencio redirigir los intentos de acceso bloqueados en lugar de mostrar la página "acceso denegado"? En caso afirmativo, especifique la ubicación para redirigir los intentos de acceso bloqueados. Si no, dejar esta variable en blanco.

##### "silent_mode_response_header_code" `[int]`
- ¿Cuál mensaje de estado HTTP debe enviar CIDRAM al redirigir silenciosamente los intentos de acceso bloqueados?

```
silent_mode_response_header_code
├─301 (301 Moved Permanently (Movido permanentemente)): Indica al cliente que la redirección es PERMANENTE, y que el método de
│ solicitud utilizado para la redirección PUEDE ser diferente del método de
│ solicitud utilizado para la solicitud inicial.
├─302 (302 Found (Encontrado)): Indica al cliente que la redirección es TEMPORAL, y que el método de
│ solicitud utilizado para la redirección PUEDE ser diferente del método de
│ solicitud utilizado para la solicitud inicial.
├─307 (307 Temporary Redirect (Redirección temporal)): Indica al cliente que la redirección es TEMPORAL, y que el método de
│ solicitud utilizado para la redirección NO puede ser diferente del método
│ de solicitud utilizado para la solicitud inicial.
└─308 (308 Permanent Redirect (Redirección permanente)): Indica al cliente que la redirección es PERMANENTE, y que el método de
  solicitud utilizado para la redirección NO puede ser diferente del método
  de solicitud utilizado para la solicitud inicial.
```

Independientemente de como instruimos al cliente, es importante recordar que no tenemos control sobre lo que el cliente elige hacer, y no hay garantía de que el cliente cumplirá con nuestras instrucciones.

##### "lang" `[string]`
- Especifique la predefinido del lenguaje para CIDRAM.

```
lang
├─af ("Afrikaans")
├─ar ("العربية")
├─bg ("Български")
├─bn ("বাংলা")
├─bs ("Bosanski")
├─ca ("Català")
├─cs ("Čeština")
├─de ("Deutsch")
├─en ("English (AU/GB/NZ)")
├─en-CA ("English (CA)")
├─en-US ("English (US)")
├─es ("Español")
├─fa ("فارسی")
├─fr ("Français (FR)")
├─fr-CA ("Français (CA)")
├─gl ("Galego")
├─gu ("ગુજરાતી")
├─he ("עברית")
├─hi ("हिंदी")
├─hr ("Hrvatski")
├─id ("Bahasa Indonesia")
├─it ("Italiano")
├─ja ("日本語")
├─ko ("한국어")
├─lv ("Latviešu")
├─ml ("മലയാളം")
├─mr ("मराठी")
├─ms ("Bahasa Melayu")
├─nl ("Nederlandse")
├─no ("Norsk")
├─pa ("ਪੰਜਾਬੀ")
├─pl ("Polski")
├─pt-BR ("Português (Brasil)")
├─pt-PT ("Português (Europeu)")
├─ro ("Română")
├─ru ("Русский")
├─sv ("Svenska")
├─sr ("Српски")
├─ta ("தமிழ்")
├─th ("ภาษาไทย")
├─tr ("Türkçe")
├─uk ("Українська")
├─ur ("اردو")
├─vi ("Tiếng Việt")
├─zh-Hans ("中文（简体）")
└─zh-Hant ("中文（傳統）")
```

##### "lang_override" `[bool]`
- ¿Localizar según HTTP_ACCEPT_LANGUAGE siempre que sea posible? True = Sí [Predefinido]; False = No.

##### "numbers" `[string]`
- ¿Cómo prefieres los números que se muestran? Seleccione el ejemplo que le parezca más correcto.

```
numbers
├─Arabic-1 ("١٢٣٤٥٦٧٫٨٩")
├─Arabic-2 ("١٬٢٣٤٬٥٦٧٫٨٩")
├─Arabic-3 ("۱٬۲۳۴٬۵۶۷٫۸۹")
├─Arabic-4 ("۱۲٬۳۴٬۵۶۷٫۸۹")
├─Armenian ("Ճ̅Ի̅Գ̅ՏՇԿԷ")
├─Base-12 ("4b6547.a8")
├─Base-16 ("12d687.e3")
├─Bengali-1 ("১২,৩৪,৫৬৭.৮৯")
├─Burmese-1 ("၁၂၃၄၅၆၇.၈၉")
├─China-1 ("123,4567.89")
├─Chinese-Simplified ("一百二十三万四千五百六十七点八九")
├─Chinese-Simplified-Financial ("壹佰贰拾叁萬肆仟伍佰陆拾柒点捌玖")
├─Chinese-Traditional ("一百二十三萬四千五百六十七點八九")
├─Chinese-Traditional-Financial ("壹佰貳拾叄萬肆仟伍佰陸拾柒點捌玖")
├─Fullwidth ("１２３４５６７.８９")
├─Geez ("፻፳፫፼፵፭፻፷፯")
├─Hebrew ("א׳׳ב׳קג׳יד׳ךסז")
├─India-1 ("12,34,567.89")
├─India-2 ("१२,३४,५६७.८९")
├─India-3 ("૧૨,૩૪,૫૬૭.૮૯")
├─India-4 ("੧੨,੩੪,੫੬੭.੮੯")
├─India-5 ("೧೨,೩೪,೫೬೭.೮೯")
├─India-6 ("౧౨,౩౪,౫౬౭.౮౯")
├─Japanese ("百万二十万三万四千五百六十七・八九分")
├─Javanese ("꧑꧒꧓꧔꧕꧖꧗.꧘꧙")
├─Khmer-1 ("១.២៣៤.៥៦៧,៨៩")
├─Lao-1 ("໑໒໓໔໕໖໗.໘໙")
├─Latin-1 ("1,234,567.89")
├─Latin-2 ("1 234 567.89")
├─Latin-3 ("1.234.567,89")
├─Latin-4 ("1 234 567,89")
├─Latin-5 ("1,234,567·89")
├─Mayan ("𝋧𝋮𝋦𝋨𝋧.𝋱𝋰")
├─Mongolian ("᠑᠒᠓᠔᠕᠖᠗.᠘᠙")
├─NoSep-1 ("1234567.89")
├─NoSep-2 ("1234567,89")
├─Odia ("୧୨୩୪୫୬୭.୮୯")
├─Roman ("M̅C̅C̅X̅X̅X̅I̅V̅DLXVII")
├─SDN-Dwiggins ("4E6,547;X8")
├─SDN-Pitman ("4↋6,547;↊8")
├─Tamil ("௲௲௨௱௲௩௰௲௪௲௫௱௬௰௭")
├─Thai-1 ("๑,๒๓๔,๕๖๗.๘๙")
├─Thai-2 ("๑๒๓๔๕๖๗.๘๙")
└─Tibetan ("༡༢༣༤༥༦༧.༨༩")
```

##### "emailaddr" `[string]`
- Si deseado, usted puede suministrar una dirección de correo electrónico aquí que se dará a los usuarios cuando ellos están bloqueadas, para ellos utilizar como un punto de contacto para soporte y/o asistencia para el caso de ellos están bloqueadas por error. ADVERTENCIA: Cualquiera que sea la dirección de correo electrónico que usted suministrar aquí, que será sin duda adquirida por spambots y raspadores/scrapers durante el curso de su siendo utilizar aquí, y entonces, se recomienda encarecidamente que si eliges para suministrar una dirección de correo electrónico aquí, que se asegura de que la dirección de correo electrónico usted suministrar aquí es una dirección desechable y/o una dirección que usted no se preocupan por para ser bombardeado por correo (en otras palabras, es probable que usted no quiere utilizar sus correos electrónicos personal principal o comercio principal).

##### "emailaddr_display_style" `[string]`
- ¿Cómo prefieres que la dirección de correo electrónico sea presentada a los usuarios?

```
emailaddr_display_style
├─default ("Enlace que se puede hacer clic")
└─noclick ("Texto que no se puede hacer clic")
```

##### "default_dns" `[string]`
- Una lista de los servidores DNS que se utilizarán para las búsquedas de nombres del host. ¡AVISO: No cambie esto a menos que sepas lo que estás haciendo!

__FAQ.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.es.md#qué-puedo-usar-para-default_dns" hreflang="es-ES">¿Qué puedo usar para "default_dns"?</a>*

##### "default_algo" `[string]`
- Define qué algoritmo utilizar para todas las contraseñas y sesiones en el futuro.

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### "statistics" `[string]`
- Controla qué información estadística rastrear.

```
statistics───[IPv4]─[IPv6]─[Otro]
├─Blocked ("Solicitudes bloqueadas")
├─Banned ("Solicitudes prohibidas")
├─Passed ("Solicitudes aprobadas")
├─ReportOK ("Solicitudes reportados a API externos – OK")
└─ReportFailed ("Solicitudes reportados a API externos – Fallado")
```

Nota: Desde la página de reglas auxiliares se puede controlar si realizar un rastreo de las estadísticas de las reglas auxiliares.

##### "statistics_captchas" `[string]`
- Controla qué información estadística rastrear para los CAPTCHA.

```
statistics_captchas───[Fallado]─[Pasado]─[Servido]
├─HCaptcha ("hCaptcha")
├─FriendlyCaptcha ("Friendly Captcha")
└─CloudflareTurnstile ("Cloudflare Turnstile")
```

Nota: Desde la página de reglas auxiliares se puede controlar si realizar un rastreo de las estadísticas de las reglas auxiliares.

##### "force_hostname_lookup" `[bool]`
- ¿Forzar búsquedas de nombres de host? True = Sí; False = No [Predefinido]. Las búsquedas de nombres de host normalmente se realizan según sea necesario, pero se pueden forzar para todas las solicitudes. Hacerlo puede ser útil como un medio para proporcionar información más detallada en los archivos de registro, pero también puede tener un efecto ligeramente negativo en el rendimiento.

##### "allow_gethostbyaddr_lookup" `[bool]`
- ¿Permitir búsquedas gethostbyaddr cuando UDP no está disponible? True = Sí [Predefinido]; False = No.

Nota: Es posible que las búsquedas de IPv6 no funcionen correctamente en algunos sistemas de 32 bits.

##### "disabled_channels" `[string]`
- Esto se puede usar para evitar que CIDRAM use canales particulares al enviar solicitudes (por ejemplo, al actualizar, al obtener metadatos de componentes, etc).

```
disabled_channels
├─GitHub ("<span class="origin bgHRdBl">US</span> GitHub")
├─BitBucket ("<span class="origin bgHRdBl">US</span> BitBucket")
├─Codeberg ("<span class="origin bgVBkRd fgYlw">DE</span> Codeberg")
└─GoogleDNS ("<span class="origin bgHRdBl">US</span> GoogleDNS")
```

##### "request_proxy" `[string]`
- Si desea que las solicitudes salientes se envíen a través de un proxy, especifique ese proxy aquí. En caso contrario, deje esto en blanco.

##### "request_proxyauth" `[string]`
- Si envía solicitudes salientes a través de un proxy y ese proxy requiere un nombre de usuario y una contraseña, especifique ese nombre de usuario y contraseña aquí (p.ej., `user:pass`). En caso contrario, deje esto en blanco.

##### "default_timeout" `[int]`
- ¿Tiempo de espera predefinido para usar en solicitudes externas? Predefinido = 12 segundos.

##### "sensitive" `[string]`
- Una lista de rutas para considerar como páginas confidenciales. Cada ruta listada se comparará con el URI reconstruido cuando sea necesario. Una ruta que comienza con una barra inclinada se tratará como un literal, y se comparará desde el componente de ruta de la solicitud en adelante. Alternativamente, una ruta que comienza con un carácter no alfanumérico, y termina con ese mismo carácter (o ese mismo carácter más un indicador "i" opcional) se tratará como una expresión regular. Cualquier otro tipo de ruta se tratará como un literal, y puede coincidir con cualquier parte del URI. Si una ruta se considera una página confidencial puede afectar el comportamiento de algunos módulos, pero no tiene ningún efecto en otros casos.

##### "email_notification_address" `[string]`
- Si ha optado por recibir notificaciones del CIDRAM por correo electrónico, por ejemplo, cuando se activan reglas auxiliares específicas, puede especificar la dirección del destinatario de esas notificaciones aquí.

##### "email_notification_name" `[string]`
- Si ha optado por recibir notificaciones del CIDRAM por correo electrónico, por ejemplo, cuando se activan reglas auxiliares específicas, puede especificar el nombre del destinatario de esas notificaciones aquí.

##### "email_notification_when" `[string]`
- Cuándo enviar notificaciones después de ser generadas.

```
email_notification_when
├─Immediately ("Inmediatamente.")
├─After24Hours ("Después de 24 horas, agrupados juntos (o cuando se desencadena manualmente, por ejemplo, a través de cron).")
└─ManuallyOnly ("Sólo cuando se desencadena manualmente (por ejemplo, a través de cron).")
```

#### "components" (Categoría)
Configuración para la activación y la desactivación de los componentes utilizados por CIDRAM. Normalmente se administra desde la página de actualizaciones, pero también se puede administrar desde aquí para un control más preciso y para los componentes personalizados que la página de actualizaciones no reconoce.

##### "ipv4" `[string]`
- Archivos de firmas IPv4.

##### "ipv6" `[string]`
- Archivos de firmas IPv6.

##### "modules" `[string]`
- Módulos.

##### "imports" `[string]`
- Importaciones. Normalmente se utiliza para proporcionar información de configuración de un componente a CIDRAM.

##### "events" `[string]`
- Manejadores de eventos. Normalmente se usa para modificar la forma en que CIDRAM se comporta internamente o para proporcionar funcionalidad adicional.

#### "logging" (Categoría)
Configuración relacionada con el registro (excluyendo lo que es aplicable a otras categorías).

##### "standard_log" `[string]`
- Un archivo legible por humanos para el registro de todos los intentos de acceso bloqueados. Especificar el nombre del archivo, o dejar en blanco para desactivar.

Consejo útil: Puede adjuntar información de fecha/hora a los nombres de los archivos de registro utilizando marcadores de posición de formato de hora. Los marcadores de posición de formato de hora disponibles se muestran en <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "apache_style_log" `[string]`
- Un archivo en el estilo de Apache para el registro de todos los intentos de acceso bloqueados. Especificar el nombre del archivo, o dejar en blanco para desactivar.

Consejo útil: Puede adjuntar información de fecha/hora a los nombres de los archivos de registro utilizando marcadores de posición de formato de hora. Los marcadores de posición de formato de hora disponibles se muestran en <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "serialised_log" `[string]`
- Un archivo serializado para el registro de todos los intentos de acceso bloqueados. Especificar el nombre del archivo, o dejar en blanco para desactivar.

Consejo útil: Puede adjuntar información de fecha/hora a los nombres de los archivos de registro utilizando marcadores de posición de formato de hora. Los marcadores de posición de formato de hora disponibles se muestran en <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "error_log" `[string]`
- Un archivo para registrar cualquier error detectado que no sea fatal. Especificar el nombre del archivo, o dejar en blanco para desactivar.

Consejo útil: Puede adjuntar información de fecha/hora a los nombres de los archivos de registro utilizando marcadores de posición de formato de hora. Los marcadores de posición de formato de hora disponibles se muestran en <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "outbound_request_log" `[string]`
- Un archivo para registrar los resultados de cualquier solicitud saliente. Especificar el nombre del archivo, o dejar en blanco para desactivar.

Consejo útil: Puede adjuntar información de fecha/hora a los nombres de los archivos de registro utilizando marcadores de posición de formato de hora. Los marcadores de posición de formato de hora disponibles se muestran en <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "report_log" `[string]`
- Un archivo para registrar cualquier reportes enviados a las API externas. Especificar el nombre del archivo, o dejar en blanco para desactivar.

Consejo útil: Puede adjuntar información de fecha/hora a los nombres de los archivos de registro utilizando marcadores de posición de formato de hora. Los marcadores de posición de formato de hora disponibles se muestran en <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "truncate" `[string]`
- ¿Truncar archivos de registro cuando alcanzan cierto tamaño? Valor es el tamaño máximo en B/KB/MB/GB/TB que un archivo de registro puede crecer antes de ser truncado. El valor predefinido de 0KB deshabilita el truncamiento (archivos de registro pueden crecer indefinidamente). Nota: ¡Se aplica a archivos de registro individuales! El tamaño de los archivos de registro no se considera colectivamente.

##### "log_rotation_limit" `[int]`
- La rotación de registros limita la cantidad de archivos de registro que deberían existir al mismo tiempo. Cuando se crean nuevos archivos de registro, si la cantidad total de archivos de registro excede el límite especificado, se realizará la acción especificada. Puede especificar el límite deseado aquí. Un valor de 0 deshabilitará la rotación de registros.

##### "log_rotation_action" `[string]`
- La rotación de registros limita la cantidad de archivos de registro que deberían existir al mismo tiempo. Cuando se crean nuevos archivos de registro, si la cantidad total de archivos de registro excede el límite especificado, se realizará la acción especificada. Puede especificar la acción deseada aquí.

```
log_rotation_action
├─Delete ("Eliminar los archivos de registro más antiguos, hasta que el límite ya no se exceda.")
└─Archive ("Primero archiva, y luego eliminar los archivos de registro más antiguos, hasta que el límite ya no se exceda.")
```

##### "log_banned_ips" `[bool]`
- ¿Incluir las solicitudes bloqueadas de IPs prohibidos en los archivos de registro? True = Sí [Predefinido]; False = No.

##### "log_sanitisation" `[bool]`
- Cuando se utiliza el front-end página de los archivos de registro para ver los datos de registro, CIDRAM sanea los datos de registro antes de mostrarlos, para proteger a los usuarios de los ataques XSS y otras amenazas potenciales que podrían estar contenido dentro de los datos de registro. Pero, de forma predefinida, los datos no se sanean durante el registro. Esto es para asegurar que los datos de registro se conserven con precisión, para ayudar a cualquier análisis heurístico o forense que pueda ser necesario en el futuro. Pero, en el caso de que un usuario intente leer los datos de registro utilizando herramientas externas, y si esas herramientas externas no realizan su propio proceso de saneamiento, el usuario podría estar expuesto a ataques XSS. Si es necesario, puede cambiar el comportamiento predefinido utilizando esta directiva de configuración. True = Sanear datos al registrarlo (los datos se conservan con menos precisión, pero el riesgo de XSS es menor). False = No sanear datos al registrarlo (los datos se conservan con mayor precisión, pero el riesgo de XSS es mayor) [Predefinido].

#### "frontend" (Categoría)
Configuración para el front-end.

##### "frontend_log" `[string]`
- Archivo para registrar intentos de login al front-end. Especificar el nombre del archivo, o dejar en blanco para desactivar.

Consejo útil: Puede adjuntar información de fecha/hora a los nombres de los archivos de registro utilizando marcadores de posición de formato de hora. Los marcadores de posición de formato de hora disponibles se muestran en <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signatures_update_event_log" `[string]`
- Un archivo para registrar cuando las firmas se actualizan a través del front-end. Especificar el nombre del archivo, o dejar en blanco para desactivar.

Consejo útil: Puede adjuntar información de fecha/hora a los nombres de los archivos de registro utilizando marcadores de posición de formato de hora. Los marcadores de posición de formato de hora disponibles se muestran en <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "max_login_attempts" `[int]`
- Número máximo de intentos de login al front-end. Predefinido = 5.

##### "theme" `[string]`
- El tema a utilizar para el front-end.

```
theme
├─default ("Default")
├─bluemetal ("Blue Metal")
├─fullmoon ("Full Moon")
├─moss ("Moss")
├─primer ("Primer")
├─primerdark ("Primer Dark")
├─rbi ("Red-Blue Inverted")
├─slate ("Slate")
└─…Otro
```

##### "theme_mode" `[string]`
- El modo para el tema a utilizar para el front-end.

```
theme_mode
├─normal ("Normal")
└─inverted ("Invertido")
```

##### "magnification" `[float]`
- Ampliación de fuente. Predefinido = 1.

##### "custom_header" `[string]`
- Insertado como HTML al principio de todas las páginas del front-end. Esto podría ser útil en caso de que desee incluir un logotipo de sitio web, un encabezado personalizado, scripts, o similar en todas dichas páginas.

##### "custom_footer" `[string]`
- Insertado como HTML al final de todas las páginas del front-end. Esto podría ser útil en caso de que desee incluir un aviso legal, enlace de contacto, información comercial, o similar en todas dichas páginas.

##### "remotes" `[string]`
- Una lista de las direcciones utilizadas por el actualizador para obtener los metadatos de los componentes. Es posible que esto debe ajustarse al actualizar a una nueva versión principal, o al adquirir una nueva fuente de actualizaciones, pero en circunstancias normales debe dejarse así.

##### "enable_two_factor" `[bool]`
- Esta directiva determina si se debe usar 2FA para las cuentas del front-end.

#### "signatures" (Categoría)
Configuración para firmas, archivos de firma, módulos, etc.

##### "shorthand" `[string]`
- Controla qué hacer con una solicitud cuando hay una coincidencia positiva con una firma que utiliza las palabras abreviadas dadas.

```
shorthand───[Bloquearlo.]─[Perfilarlo.]─[Cuando está bloqueado, suprime la plantilla de salida.]
├─Attacks ("Ataques")
├─Bogon ("⁰ Bogon IP")
├─Cloud ("Servicio en la nube")
├─Generic ("Genérico")
├─Legal ("¹ Legal")
├─Malware ("Malware")
├─Proxy ("² Proxy")
├─Spam ("Spam")
├─Banned ("³ Prohibido")
├─BadIP ("³ IP no válida")
├─RL ("³ Tarifa limitada")
├─Conflict ("³ Conflicto")
└─Other ("⁴ Otro")
```

__0.__ Si su sitio web necesita acceso a través de LAN o localhost, no bloquee esto. De lo contrario, puedes bloquear esto.

__1.__ Ninguno de los archivos de firma predefinidos usa esto, pero no obstante, es soportado en caso que pueda ser útil para algunos usuarios.

__2.__ Si necesita que los usuarios puedan acceder a su sitio web a través de proxies, no bloquee esto. De lo contrario, puedes bloquear esto.

__3.__ El uso directo en las firmas no es soportados, pero se puede invocar por otros medios en circunstancias particulares.

__4.__ Se refiere a los casos en que las palabras abreviadas no se usan en absoluto, o no son reconocidas por CIDRAM.

__Uno por firma.__ Una firma puede invocar múltiples perfiles, pero puede usar solo una palabra abreviada. Es posible que varias palabras abreviadas sean adecuadas, pero como solo se puede usar una, apuntamos de usar siempre las más adecuadas.

__Prioridad.__ Una opción seleccionada siempre tiene prioridad sobre una opción no seleccionada. Por ejemplo, si hay varias palabras abreviadas en juego, pero solo una de ellas está configurada como bloqueada, la solicitud seguirá bloqueada.

__Puntos finales humanos y servicios en la nube.__ Servicio en la nube puede referirse a proveedores de alojamiento web, granjas de servidores, centros de datos, o una serie de otras cosas. Punto final humano se refiere a los medios por los cuales un humano accede a internet, por ejemplo, a través de un proveedor de servicios de internet. Una red generalmente proporciona solo uno u otro, pero a veces puede proporcionar ambos. Apuntamos nunca identificar puntos finales humanos potenciales como servicios en la nube. Por lo tanto, un servicio en la nube puede identificarse como algo más si su rango es compartido por puntos finales humanos conocidos. Del mismo modo, apuntamos identificar siempre los servicios en la nube, cuyos rangos no son compartidos por ningún punto final humano conocido, como servicios en la nube. Por lo tanto, una solicitud identificada explícitamente como un servicio en la nube probablemente no comparta su rango con ningún punto final humano conocido. Asimismo, una solicitud identificada explícitamente por ataques o riesgo de spam probablemente los comparta. Sin embargo, internet siempre está en constante cambio, los propósitos de las redes cambian con el tiempo, y los rangos siempre se compran o venden, así que manténgase consciente y vigilante a los falsos positivos.

##### "default_tracktime" `[string]`
- La duración que se deben seguir las direcciones IP. Predefinido = 7d0°0′0″ (1 semana).

##### "infraction_limit" `[int]`
- Número máximo de infracciones a las que un IP puede incurrir antes de ser prohibido por el rastreo IP. Predefinido = 10.

##### "tracking_override" `[bool]`
- ¿Permitir que los módulos reemplacen las opciones de seguimiento? True = Sí [Predefinido]; False = No.

##### "conflict_response" `[int]`
- Cuando hay demasiados intentos simultáneos de acceder a los mismos recursos (por ejemplo, solicitudes simultáneas a múltiples procesos PHP en la misma máquina para los mismos recursos), algunos de esos intentos pueden fallar. En el caso poco común y poco probable de que esto afecte a los archivos de firma o los módulos, es posible que CIDRAM no pueda tomar una determinación efectiva sobre la solicitud. ¿Si esto sucede, se debe bloquear la solicitud, y qué mensaje de estado HTTP debe enviar CIDRAM?

```
conflict_response
├─0 (No bloquees la solicitud.): Si prefiere que las solicitudes se bloqueen solo cuando esté seguro de que
│ son malignas, o prefiere pecar de cauteloso con respecto a los falsos
│ positivos (a costa de que ocasionalmente entre tráfico no deseado), elija
│ esta opción. Si prefiere que se bloqueen las solicitudes si no está seguro
│ de que sean benignas, o prefiere pecar de vigilante (a costa de producir
│ falsos positivos ocasionales), elija una de las otras opciones disponibles.
├─409 (409 Conflicto): Recomendado para conflictos de recursos (por ejemplo, conflictos de fusión,
│ conflictos de acceso a archivos, etc). No recomendado en otros contextos.
└─429 (429 Too Many Requests (Demasiadas solicitudes)): Recomendado para la limitación de tasa, cuando se trata de ataques DDoS, y
  para la prevención de inundaciones. No recomendado en otros contextos.
```

#### "verification" (Categoría)
Configuración para verificar de dónde se originan las solicitudes.

##### "search_engines" `[string]`
- Controles para verificar las solicitudes de los motores de búsqueda.

```
search_engines───[¿Intentar verificar?]─[¿Bloquear negativos?]─[¿Bloquear solicitudes no verificados?]─[¿Permitir bypasses de un solo golpe?]─[¿No rastrear positivos?]
├─Amazonbot ("Amazonbot")
├─Applebot ("Applebot")
├─Baidu ("* Baiduspider/百度")
├─Bingbot ("* Bingbot")
├─DuckDuckBot ("* DuckDuckBot")
├─Googlebot ("* Googlebot")
├─MojeekBot ("MojeekBot")
├─PetalBot ("* PetalBot")
├─Qwantify ("Qwantify/Bleriot")
├─SeznamBot ("SeznamBot")
├─Sogou ("* Sogou/搜狗")
├─Yahoo ("Yahoo/Slurp")
├─Yandex ("* Yandex/Яндекс")
└─YoudaoBot ("YoudaoBot")
```

__¿Qué son "positivos" y "negativos"?__ Cuando verificando la identidad presentada por una solicitud, un resultado exitoso podría describirse como "positivo" o "negativo". Cuando se confirma que la identidad presentada es la verdadera identidad, se describiría como "positiva". Cuando se confirma que la identidad presentada es falsa, se describirá como "negativa". Sin embargo, un resultado fallido (por ejemplo, la verificación falló, o no se puede determinar la veracidad de la identidad presentada) no se describiría como "positivo" o "negativo". En cambio, un resultado fallido se describiría simplemente como no verificado. Cuando no se intenta verificar la identidad presentada por una solicitud, la solicitud también se describiría como no verificado. Los términos tienen sentido solo en el contexto en el que se reconoce la identidad presentada por una solicitud y, por lo tanto, donde la verificación es posible. En los casos en que la identidad presentada no coincida con las opciones proporcionadas anteriormente, o cuando no se presente ninguna identidad, las opciones proporcionadas anteriormente se vuelven irrelevantes.

__¿Qué son los "bypasses de un solo golpe"?__ En algunos casos, una solicitud con verificación positiva aún puede bloquearse como resultado de los archivos de firma, módulos, u otras condiciones de la solicitud, y las bypasses pueden ser necesarias para evitar falsos positivos. En el caso de que una bypass esté destinada a tratar exactamente una infracción, ni más ni menos, dicha bypass podría describirse como una "bypass de un solo golpe".

* Esta opción tiene un bypass correspondiente bajo `bypasses➡used`. Se recomienda asegurarse de que la casilla de verificación para la bypass correspondiente esté marcado de la misma manera que la casilla de verificación para intentar verificar esta opción.

##### "social_media" `[string]`
- Controles para verificar las solicitudes de las plataformas de redes sociales.

```
social_media───[¿Intentar verificar?]─[¿Bloquear negativos?]─[¿Bloquear solicitudes no verificados?]─[¿Permitir bypasses de un solo golpe?]─[¿No rastrear positivos?]
├─Embedly ("* Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("* Pinterest")
├─Snapchat ("* Snapchat")
└─Twitterbot ("*!! Twitterbot")
```

__¿Qué son "positivos" y "negativos"?__ Cuando verificando la identidad presentada por una solicitud, un resultado exitoso podría describirse como "positivo" o "negativo". Cuando se confirma que la identidad presentada es la verdadera identidad, se describiría como "positiva". Cuando se confirma que la identidad presentada es falsa, se describirá como "negativa". Sin embargo, un resultado fallido (por ejemplo, la verificación falló, o no se puede determinar la veracidad de la identidad presentada) no se describiría como "positivo" o "negativo". En cambio, un resultado fallido se describiría simplemente como no verificado. Cuando no se intenta verificar la identidad presentada por una solicitud, la solicitud también se describiría como no verificado. Los términos tienen sentido solo en el contexto en el que se reconoce la identidad presentada por una solicitud y, por lo tanto, donde la verificación es posible. En los casos en que la identidad presentada no coincida con las opciones proporcionadas anteriormente, o cuando no se presente ninguna identidad, las opciones proporcionadas anteriormente se vuelven irrelevantes.

__¿Qué son los "bypasses de un solo golpe"?__ En algunos casos, una solicitud con verificación positiva aún puede bloquearse como resultado de los archivos de firma, módulos, u otras condiciones de la solicitud, y las bypasses pueden ser necesarias para evitar falsos positivos. En el caso de que una bypass esté destinada a tratar exactamente una infracción, ni más ni menos, dicha bypass podría describirse como una "bypass de un solo golpe".

* Esta opción tiene un bypass correspondiente bajo `bypasses➡used`. Se recomienda asegurarse de que la casilla de verificación para la bypass correspondiente esté marcado de la misma manera que la casilla de verificación para intentar verificar esta opción.

** Requiere la funcionalidad de búsqueda de ASN (por ejemplo, a través del módulo IP-API o BGPView).

*!! Alta probabilidad de causar falsos positivos debido a iMessage.

##### "other" `[string]`
- Controles para verificar otros tipos de solicitudes cuando sea posible.

```
other───[¿Intentar verificar?]─[¿Bloquear negativos?]─[¿Bloquear solicitudes no verificados?]─[¿Permitir bypasses de un solo golpe?]─[¿No rastrear positivos?]
├─AdSense ("AdSense")
├─AmazonAdBot ("* AmazonAdBot")
├─ChatGPT-User ("!! ChatGPT-User")
├─GPTBot ("!! GPTBot")
├─OAI-SearchBot ("!! OAI-SearchBot")
└─UptimeRobot ("UptimeRobot")
```

__¿Qué son "positivos" y "negativos"?__ Cuando verificando la identidad presentada por una solicitud, un resultado exitoso podría describirse como "positivo" o "negativo". Cuando se confirma que la identidad presentada es la verdadera identidad, se describiría como "positiva". Cuando se confirma que la identidad presentada es falsa, se describirá como "negativa". Sin embargo, un resultado fallido (por ejemplo, la verificación falló, o no se puede determinar la veracidad de la identidad presentada) no se describiría como "positivo" o "negativo". En cambio, un resultado fallido se describiría simplemente como no verificado. Cuando no se intenta verificar la identidad presentada por una solicitud, la solicitud también se describiría como no verificado. Los términos tienen sentido solo en el contexto en el que se reconoce la identidad presentada por una solicitud y, por lo tanto, donde la verificación es posible. En los casos en que la identidad presentada no coincida con las opciones proporcionadas anteriormente, o cuando no se presente ninguna identidad, las opciones proporcionadas anteriormente se vuelven irrelevantes.

__¿Qué son los "bypasses de un solo golpe"?__ En algunos casos, una solicitud con verificación positiva aún puede bloquearse como resultado de los archivos de firma, módulos, u otras condiciones de la solicitud, y las bypasses pueden ser necesarias para evitar falsos positivos. En el caso de que una bypass esté destinada a tratar exactamente una infracción, ni más ni menos, dicha bypass podría describirse como una "bypass de un solo golpe".

* Esta opción tiene un bypass correspondiente bajo `bypasses➡used`. Se recomienda asegurarse de que la casilla de verificación para la bypass correspondiente esté marcado de la misma manera que la casilla de verificación para intentar verificar esta opción.

!! La mayoría de los usuarios probablemente querrán que esto se bloquee, independientemente de si es real o falso. Eso se puede lograr si no se selecciona "intentar verificar" y se selecciona "bloquear solicitudes no verificadas". Pero, debido a que algunos usuarios pueden querer poder verificar dichas solicitudes (para bloquear las negativas y permitir las positivas), en lugar de bloquear dichas solicitudes a través de módulos, aquí se proporcionan opciones para manejar dichas solicitudes.

##### "adjust" `[string]`
- Controles para ajustar otras funciones en el contexto de la verificación.

```
adjust───[Suprimir hCaptcha]─[Suprimir Friendly Captcha]─[Suprimir Cloudflare Turnstile]
├─Negatives ("Negativos que están bloqueados")
└─NonVerified ("No verificados que están bloqueados")
```

#### "captcha" (Categoría)
Configuración para CAPTCHAs (proporciona una forma para que los humanos recuperen el acceso cuando están bloqueados).

##### "usemode" `[int]`
- ¿Cuándo se deben ofrecer CAPTCHAs? Puede especificar aquí el comportamiento preferido para cada proveedor compatible.

```
usemode───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─0 (Nunca.)
├─1 (Solo cuando está bloqueado, dentro del límite de firmas y no está prohibido.)
├─2 (Solo cuando está bloqueado, marcado especialmente para su uso, dentro del límite de firmas y no está prohibido.)
├─3 (Solo cuando está dentro del límite de firmas y no está prohibido (independientemente de si está bloqueado).)
├─4 (Solo cuando no está bloqueado.)
├─5 (Solo cuando no está bloqueado, o cuando está especialmente marcado para su uso, dentro del límite de firmas y no está prohibido.)
└─6 (Solo cuando no está bloqueado, en solicitudes de páginas confidenciales.)
```

Nota: Las solicitudes incluidas en la lista blanca o verificadas y no bloqueadas nunca necesitan completar un CAPTCHA.

También tenga en cuenta: Los CAPTCHA pueden proporcionar una capa de protección útil contra bots y varios tipos de solicitudes automatizadas y maliciosas, pero no proporcionán ninguna protección contra humanos maliciosas.

Las solicitudes se pueden "marcar para su uso" a través de reglas auxiliares.

Si una solicitud se considera "sensible" está determinado por <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_sensitive">`general➡sensitive`</a>.

El "límite de firma" está determinado por <a onclick="javascript:toggleconfigNav('captchaRow','captchaShowLink')" href="#config_captcha_signature_limit">`captcha➡signature_limit`</a>.

##### "nonblocked_status_code" `[int]`
- ¿Qué código de estado se debe usar al mostrar CAPTCHA a solicitudes no bloqueadas?

```
nonblocked_status_code───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─200 (200 OK): Menos robusto, pero más fácil de usar. Lo más probable que las
│ solicitudes automatizadas interpreten esta respuesta como una indicación de
│ que la solicitud fue exitosa. Recomendado para solicitudes no bloqueadas.
├─403 (403 Forbidden (Prohibido)): Un poco más robusto, pero un poco menos fácil de usar. Recomendado para la
│ mayoría de las circunstancias generales.
├─418 (418 I'm a teapot (Soy una tetera)): Hace referencia a una broma del Día de los Inocentes (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Es muy poco probable que
│ cualquier cliente, bot, navegador, u otro lo entiendará. Provisto por
│ diversión y conveniencia, pero generalmente no recomendado.
├─429 (429 Too Many Requests (Demasiadas solicitudes)): Recomendado para la limitación de tasa, cuando se trata de ataques DDoS, y
│ para la prevención de inundaciones. No recomendado en otros contextos.
└─451 (451 Unavailable For Legal Reasons (No disponible por razones legales)): Recomendado cuando se bloquea principalmente por razones legales. No
  recomendado en otros contextos.
```

##### "api" `[string]`
- ¿Qué API usar?

```
api───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─v0 ("v0")
├─v1 ("v1")
├─Invisible ("v1 (Invisible)")
└─v2 ("v2")
```

##### "messages" `[string]`
- Mensajes que se mostrarán junto a los CAPTCHA.

```
messages───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─cookie_warning ("¿Mostrar advertencia de cookie?): Dependiendo de las leyes de privacidad de su país o estado (por ejemplo,
│ GDPR/DSGVO en la UE, LGPD en Brasil, etc), esto puede ser legalmente
│ requerido."
└─api_message ("¿Mostrar mensaje de API?): Instrucciones al usuario, adecuadas a la API utilizada, relativas a la
  cumplimentación del CAPTCHA."
```

##### "lockto" `[string]`
- A qué vincular los CAPTCHA.

```
lockto───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─ip ("Vincula los CAPTCHA a la dirección IP del usuario que completa el CAPTCHA, pero no al usuario real.): Las cookies NO se utilizan para identificar a los usuarios. Cuando se
│ recupera el acceso debido a completar con éxito un CAPTCHA, se aplica a
│ cualquier persona que se conecte desde la misma dirección IP."
├─user ("Vincula los CAPTCHA al usuario que completa el CAPTCHA, pero no a su dirección IP.): Las cookies se utilizan para identificar a los usuarios. Cuando se recupera
│ el acceso debido a completar con éxito un CAPTCHA, se aplica solo al
│ usuario que completó el CAPTCHA y, mientras su cookie siga siendo válida,
│ persistirá, incluso si su dirección IP cambia."
└─both ("Vincula los CAPTCHA al usuario que completa el CAPTCHA así como a su dirección IP.): Las cookies se utilizan para identificar a los usuarios. Cuando se recupera
  el acceso debido a completar con éxito un CAPTCHA, se aplica solo al
  usuario que completó el CAPTCHA y no persistirá si su dirección IP
  cambia."
```

##### "hcaptcha_sitekey" `[string]`
- Si desea usar hCaptcha con CIDRAM, deberá ingresar un valor aquí. De lo contrario, puede ignorarlo.

Este valor se puede encontrar en el panel de control de su servicio de CAPTCHA.

Ver también:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "hcaptcha_secret" `[string]`
- Si desea usar hCaptcha con CIDRAM, deberá ingresar un valor aquí. De lo contrario, puede ignorarlo.

Este valor se puede encontrar en el panel de control de su servicio de CAPTCHA.

Ver también:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "friendly_sitekey" `[string]`
- Si desea usar Friendly Captcha con CIDRAM, deberá ingresar un valor aquí. De lo contrario, puede ignorarlo.

Este valor se puede encontrar en el panel de control de su servicio de CAPTCHA.

Ver también:
- [Friendly Captcha Dashboard](https://app.friendlycaptcha.eu/dashboard)

##### "friendly_apikey" `[string]`
- Si desea usar Friendly Captcha con CIDRAM, deberá ingresar un valor aquí. De lo contrario, puede ignorarlo.

Este valor se puede encontrar en el panel de control de su servicio de CAPTCHA.

Ver también:
- [Friendly Captcha Dashboard](https://app.friendlycaptcha.eu/dashboard)

##### "turnstile_sitekey" `[string]`
- Si desea usar Cloudflare Turnstile con CIDRAM, deberá ingresar un valor aquí. De lo contrario, puede ignorarlo.

Este valor se puede encontrar en el panel de control de su servicio de CAPTCHA.

Ver también:
- [Cloudflare Dashboard](https://dash.cloudflare.com/)

##### "turnstile_secret" `[string]`
- Si desea usar Cloudflare Turnstile con CIDRAM, deberá ingresar un valor aquí. De lo contrario, puede ignorarlo.

Este valor se puede encontrar en el panel de control de su servicio de CAPTCHA.

Ver también:
- [Cloudflare Dashboard](https://dash.cloudflare.com/)

##### "expiry" `[float]`
- Número de horas para recordar instancias de CAPTCHA. Predefinido = 720 (1 mes).

##### "signature_limit" `[int]`
- Número máximo de firmas permitidas antes de que se retire la oferta de CAPTCHA. Predefinido = 1.

##### "log" `[string]`
- Registrar todos los intentos de CAPTCHA? En caso afirmativo, especifique el nombre que se utilizará para el archivo de registro. Si no, dejar esta variable en blanco.

Consejo útil: Puede adjuntar información de fecha/hora a los nombres de los archivos de registro utilizando marcadores de posición de formato de hora. Los marcadores de posición de formato de hora disponibles se muestran en <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

#### "legal" (Categoría)
Configuración para requisitos legales.

##### "pseudonymise_ip_addresses" `[bool]`
- ¿Seudonimizar las direcciones IP cuando al escribir archivos de registro? True = Sí [Predefinido]; False = No.

##### "privacy_policy" `[string]`
- La dirección de una política de privacidad relevante que se mostrará en el pie de página de cualquier página generada. Especificar una URL, o dejar en blanco para desactivar.

#### "template_data" (Categoría)
Configuración para plantillas y temas.

##### "theme" `[string]`
- El tema a utilizar para los eventos de bloque y las solicitudes de CAPTCHA.

```
theme
├─default ("Default")
├─bluemetal ("Blue Metal")
├─fullmoon ("Full Moon")
├─moss ("Moss")
├─primer ("Primer")
├─primerdark ("Primer Dark")
├─rbi ("Red-Blue Inverted")
├─slate ("Slate")
└─…Otro
```

##### "theme_mode" `[string]`
- El modo para el tema a utilizar para los eventos de bloque y las solicitudes de CAPTCHA.

```
theme_mode
├─normal ("Normal")
└─inverted ("Invertido")
```

##### "magnification" `[float]`
- Ampliación de fuente. Predefinido = 1.

##### "css_url" `[string]`
- URL del archivo CSS para temas personalizados.

##### "block_event_title" `[string]`
- El título de la página que se mostrará para los eventos de bloque.

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("¡Acceso denegado!")
└─…Otro
```

##### "captcha_title" `[string]`
- El título de la página que se mostrará para las solicitudes de CAPTCHA.

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…Otro
```

##### "custom_header" `[string]`
- Insertado como HTML al principio de todas las páginas "acceso denegado". Esto podría ser útil en caso de que desee incluir un logotipo de sitio web, un encabezado personalizado, scripts, o similar en todas dichas páginas.

##### "custom_footer" `[string]`
- Insertado como HTML al final de todas las páginas "acceso denegado". Esto podría ser útil en caso de que desee incluir un aviso legal, enlace de contacto, información comercial, o similar en todas dichas páginas.

#### "rate_limiting" (Categoría)
Configuración para limitar la tasa de acceso (no recomendado para uso general).

Tenga en cuenta que, al igual que con todas las demás funciones de CIDRAM, la función de limitación de tasa de CIDRAM solo se puede aplicar a aquellas páginas y recursos a los que CIDRAM está conectado. Por lo general, eso significaría que los recursos que no sean PHP no estarían cubiertos, excepto cuando fueran atendidos explícitamente por recursos PHP conectados. Si puede usar un módulo de servidor, cPanel, o alguna otra herramienta de red para aplicar la limitación de tasa, sería mejor usar eso en lugar de la función de limitación de tasa de CIDRAM. También tenga en cuenta que un usuario suficientemente motivado podría fácilmente eludir la limitación de tasa rotando su dirección IP o cambiando a un proveedor proxy o VPN que CIDRAM aún no conoce, y tenga en cuenta que la limitación de tasa puede ser muy molesta para los usuarios finales reales. A veces puede ser necesario, pero rara vez es deseable.

##### "max_bandwidth" `[string]`
- La cantidad máxima de ancho de banda permitida dentro del período de asignación antes de habilitar los límites de tarifas para solicitudes futuras. Un valor de 0 desactiva este tipo de limitación de la tarifa. Predefinido = 0KB.

##### "max_requests" `[int]`
- El número máximo de solicitudes permitido dentro del período de asignación antes de habilitar los límites de tarifas para solicitudes futuras. Un valor de 0 desactiva este tipo de limitación de la tarifa. Predefinido = 0.

##### "precision_ipv4" `[int]`
- La precisión a utilizar cuando se monitorea el uso de IPv4. El valor refleja el tamaño del bloque CIDR. Establecer en 32 para la mejor precisión. Predefinido = 32.

##### "precision_ipv6" `[int]`
- La precisión a utilizar cuando se monitorea el uso de IPv6. El valor refleja el tamaño del bloque CIDR. Establecer en 128 para la mejor precisión. Predefinido = 128.

##### "allowance_period" `[string]`
- La duración para monitorear el uso. Predefinido = 0°0′0″.

##### "exceptions" `[string]`
- Excepciones (es decir, solicitudes que no deberían limitada). Relevante solo cuando la limitación de tasa está habilitada.

```
exceptions
├─Whitelisted ("Solicitudes en la lista blanca")
├─Verified ("Solicitudes verificadas de motores de búsqueda y redes sociales")
└─FE ("Solicitudes al front-end de CIDRAM")
```

##### "segregate" `[bool]`
- ¿Deberían segregarse o compartirse las cuotas para diferentes dominios y hosts? True = Las cuotas serán segregadas. False = Las cuotas serán compartidas [Predefinido].

#### "supplementary_cache_options" (Categoría)
Opciones de caché suplementarias. Nota: Cambiar estos valores puede potencialmente cerrar la sesión.

##### "prefix" `[string]`
- El valor especificado aquí se antepondrá a las claves de todas las entradas de la caché. Predefinido = "CIDRAM_". Cuando existen varias instalaciones en el mismo servidor, esto puede ser útil para mantener sus cachés separados entre sí.

##### "enable_apcu" `[bool]`
- Especifica si se intenta utilizar APCu para el almacenamiento en caché. Predefinido = True.

##### "enable_memcached" `[bool]`
- Especifica si se intenta utilizar Memcached para el almacenamiento en caché. Predefinido = False.

##### "enable_redis" `[bool]`
- Especifica si se intenta utilizar Redis para el almacenamiento en caché. Predefinido = False.

##### "enable_pdo" `[bool]`
- Especifica si se intenta utilizar PDO para el almacenamiento en caché. Predefinido = False.

##### "memcached_host" `[string]`
- Valor del host de Memcached. Predefinido = localhost.

##### "memcached_port" `[int]`
- Valor del puerto de Memcached. Predefinido = "11211".

##### "redis_host" `[string]`
- Valor del host de Redis. Predefinido = localhost.

##### "redis_port" `[int]`
- Valor del puerto de Redis. Predefinido = "6379".

##### "redis_timeout" `[float]`
- Valor del tiempo de espera de Redis. Predefinido = "2.5".

##### "redis_database_number" `[int]`
- Número de base de datos de Redis. Predefinido = 0. Nota: No se pueden utilizar valores distintos de 0 con Redis Cluster.

##### "pdo_dsn" `[string]`
- Valor del DSN de PDO. Predefinido = "mysql:dbname=cidram;host=localhost;port=3306".

__FAQ.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.es.md#user-content-HOW_TO_USE_PDO" hreflang="es-ES">¿Qué es un "PDO DSN"? Cómo puedo usar PDO con CIDRAM?</a>*

##### "pdo_username" `[string]`
- Nombre del usuario de PDO.

##### "pdo_password" `[string]`
- Contraseña de PDO.

#### "bypasses" (Categoría)
La configuración de las bypasses de firmas estándar.

##### "used" `[string]`
- ¿Qué bypasses se deben utilizar?

```
used
├─AbuseIPDB ("AbuseIPDB")
├─AmazonAdBot ("AmazonAdBot")
├─Baidu ("Baiduspider/百度")
├─Bingbot ("Bingbot")
├─DuckDuckBot ("DuckDuckBot")
├─Embedly ("Embedly")
├─Feedbot ("Feedbot")
├─Feedspot ("Feedspot")
├─GoogleFiber ("Google Fiber")
├─Googlebot ("Googlebot")
├─Jetpack ("Jetpack")
├─PetalBot ("PetalBot")
├─Pinterest ("Pinterest")
├─Redditbot ("Redditbot")
├─Snapchat ("Snapchat")
├─Sogou ("Sogou/搜狗")
├─Yandex ("Yandex/Яндекс")
└─iCloud ("iCloud (iPhone Safari Bypass)")
```

---


### 6. <a name="SECTION6"></a>FORMATO DE FIRMAS

*Ver también:*
- *[¿Qué es una "firma"?](#user-content-WHAT_IS_A_SIGNATURE)*

#### 6.0 LOS FUNDAMENTOS (PARA ARCHIVOS DE FIRMA)

Todas las firmas IPv4 siguen el formato: `xxx.xxx.xxx.xxx/yy [Function] [Param]`.
- `xxx.xxx.xxx.xxx` representa el comienzo del bloque de CIDRs (los octetos de la dirección IP inicial en el bloque).
- `yy` representa el tamaño del bloque de CIDRs [1-32].
- `[Function]` se instruir a la script de qué hacer con la firma (cómo la firma debe considerado).
- `[Param]` representa cualquier información adicional que puede ser necesario por `[Function]`.

Todas las firmas IPv6 siguen el formato: `xxxx:xxxx:xxxx:xxxx::xxxx/yy [Function] [Param]`.
- `xxxx:xxxx:xxxx:xxxx::xxxx` representa el comienzo del bloque de CIDRs (los octetos de la dirección IP inicial en el bloque). Notación completa y notación abreviada son ambos aceptables (y cada uno DEBE seguir las normas apropiadas y pertinentes of IPv6 notation, pero con una excepción: una dirección IPv6 no puede comenzar con una abreviatura cuando utilizada en una firma para este script, debido a la manera en que la CIDRs se reconstruyen por la script; Por ejemplo, `::1/128` deben expresarse, cuando utilizada en una firma, como `0::1/128`, y `::0/128` expresado como `0::/128`).
- `yy` representa el tamaño del bloque de CIDRs [1-128].
- `[Function]` se instruir a la script de qué hacer con la firma (cómo la firma debe considerado).
- `[Param]` representa cualquier información adicional que puede ser necesario por `[Function]`.

Los archivos de firmas para CIDRAM DEBERÍAN utilizar saltos de línea en el estilo de Unix (`%0A`, o `\n`)! Otros tipos/estilos de saltos de línea (por ejemplo, Windows `%0D%0A` o `\r\n` saltos de línea, Mac `%0D` o `\r` saltos de línea, etc) PUEDE ser usado, pero NO son preferidas. Saltos de línea que no en el estilo de Unix será normalizado a saltos de línea en el estilo de Unix por la script.

Notación CIDR precisa y correcta se requiere, de lo contrario la script no reconocerá las firmas. Adicionalmente, todas las firmas de este script DEBE comenzar con una dirección IP cuyo número IP puede dividir de una manera uniforme dentro la división del bloque representada por el tamaño de sus bloque CIDR (por ejemplo, si desea bloquear todas las IPs de `10.128.0.0` a `11.127.255.255`, `10.128.0.0/8` NO sería reconocido por la script, pero `10.128.0.0/9` y `11.0.0.0/9` utilizado junto, SERÍA reconocido por la script).

Cualquier cosa en los archivos de firmas no reconocido como una firma ni como sintaxis relacionados con la firmas por la script se ignorará, y por lo tanto significa que usted puede poner con seguridad cualquier datos que desea en los archivos de firmas sin romperlos y sin romper la script. Los comentarios son aceptables en los archivos de firmas, y no formato especial se requiere para ellos. Hash en el estilo de Shell para comentarios se prefiere, pero no forzada; Funcionalmente, no hace ninguna diferencia a la script independientemente de si usted elige utilizar hash en el estilo de Shell para comentarios, pero utilizar hash en el estilo de Shell ayuda IDEs y editores de texto sin formato resaltar correctamente las diversas partes de los archivos de firmas (y entonces, hash en el estilo de Shell puede ayudar como ayuda visual durante la edición).

Los valores posibles de `[Function]` son las siguientes:
- Run
- Whitelist
- Greylist
- Deny

Si "Run" es utilizada, cuando la firma es activada, la script intentará ejecutar (usando una instrucción `require_once`) un script PHP externa, especificado por el valor de `[Param]` (el directorio de trabajo debe ser el directorio "/vault/" de la script).

Ejemplo: `127.0.0.0/8 Run example.php`

Esto puede ser útil si se desea ejecutar alguna código PHP específica para algunas direcciones IP específicas y/o CIDRs.

Si "Whitelist" es utilizada, cuando la firma es activada, la script se reinicializará todas las detecciones (si ha habido alguna detecciones) y romper la función para prueba. `[Param]` se ignora. Esta función es el equivalente de poner en una lista blanca un IP o CIDR particular, evitando que sea detectado.

Ejemplo: `127.0.0.1/32 Whitelist`

Si "Greylist" es utilizada, cuando la firma es activada, la script se reinicializará todas las detecciones (si ha habido alguna detecciones) y saltar al siguiente archivo de firmas para continuar su procesamiento. `[Param]` se ignora.

Ejemplo: `127.0.0.1/32 Greylist`

Si "Deny" es utilizada, cuando la firma es activada, suponiendo que no firma lista blanca se ha activada para la dirección IP dada y/o CIDR dada, el acceso a la página protegida será denegada. "Deny" es lo que usted desea utilizar para bloquear efectivamente una dirección IP y/o CIDR. Cuando cualquier firmas son activadas que hacen uso de "Deny", el "Acceso Denegado" página de la script se generará y la solicitud a la página protegida será matado.

El valor de `[Param]` aceptado por "Deny" será dado a la salida del "Acceso Denegado" página, suministrado al cliente/usuario como la razón citada para su acceso a la página solicitada siendo denegado. Puede ser una frase corta y simple, explicar por qué ha elegido para bloquearlos (cualquier cosa debería ser suficiente, incluso un simple "yo no te quiero en mi sitio"), o uno de un pequeño puñado de palabras abreviadas suministrado por la script, que si utilizada, será reemplazado por la script con una explicación pre-preparada de por qué el cliente/usuario ha sido bloqueado.

Las explicaciones pre-preparadas tienen soporte para L10N y puede ser traducido por la script basado en el idioma que especifique a la directiva `lang` de la configuración de la script. Adicionalmente, puede instruir a la script ignorar las firmas "Deny" basado en el valor de su `[Param]` (si están usando estas palabras abreviadas) a través de las directrivas especificadas por la configuración de la script (cada palabra abreviada tiene una directiva correspondiente ya sea para procesar las firmas correspondientes o para ignorarlos). Los valores de `[Param]` que no utilizan estas palabras abreviadas, sin embargo, no tienen soporte para L10N y por lo tanto NO será traducido por la script, y además, no son controlable directamente por la configuración de la script.

Las palabras abreviadas disponibles son:
- Attacks
- Bogon
- Cloud
- Generic
- Legal
- Malware
- Proxy
- Spam

#### 6.1 ETIQUETAS

##### 6.1.0 ETIQUETAS DE SECCIÓN

Si desea dividir sus firmas personalizadas en secciones individuales, se puede identificar estas secciones individuales a la script mediante la adición de una "etiqueta de sección" inmediatamente después de las firmas de cada sección, junto con el nombre de su sección de firmas (vea el ejemplo siguiente).

```
# Sección 1.
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: Sección 1
```

Para romper las etiquetas de secciones y para asegurar que las etiquetas no son identificado incorrectamente a las secciones de firmas más temprano en los archivos de firmas, Simplemente asegúrese de que hay al menos dos saltos de línea consecutivos entre su etiqueta y su sección de firmas de más temprano. Cualquier firmas que no son etiquetados será predefinida a ya sea "IPv4" o "IPv6" (dependiendo de qué tipos de firmas se activan).

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: Sección 1
```

En el ejemplo anterior `1.2.3.4/32` y `2.3.4.5/32` será etiquetado como "IPv4", mientras `4.5.6.7/32` y `5.6.7.8/32` será etiquetado como "Sección 1".

La misma lógica se puede aplicar para separar otros tipos de etiquetas, también.

En particular, las etiquetas de sección pueden ser muy útiles para la depuración cuando se producen falsos positivos, al proporcionar un medio fácil de determinar la fuente exacta del problema, y pueden ser muy útiles para filtrar entradas de archivos de registro cuando se visualizan archivos de registro a través de la página de registros del front-end (nombres de sección se puede hacer clic a través de la página de registros del front-end y pueden usarse como un criterio de filtrado). Si las etiquetas de sección se omiten para algunas firmas particulares, cuando estas firmas se desencadenan, CIDRAM utiliza el nombre del archivo de firma junto con el tipo de dirección IP bloqueada (IPv4 o IPv6) como alternativa, y por lo tanto, las etiquetas de sección son completamente opcionales. Sin embargo, pueden recomendarse en algunos casos, como cuando los archivos de firma tienen un nombre vago o cuando puede ser difícil identificar claramente la fuente de las firmas que causa el bloqueo de una solicitud.

##### 6.1.1 ETIQUETAS DE EXPIRACIÓN

Si desea firmas para expiran después de un tiempo, de una manera similar a las etiquetas de sección, se puede utilizar una "etiqueta de expiración" para especificar cuándo deben firmas dejarán de ser válidas. Etiquetas de expiración utilizan el formato "AAAA.MM.DD" (vea el ejemplo siguiente).

```
# Sección 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

Las firmas expiradas nunca se desencadenán en ninguna solicitud, sin importar qué.

##### 6.1.2 ETIQUETAS DE ORIGEN

Si desea especificar el país de origen para alguna firma particular, puede hacerlo usando una "etiqueta de origen". Una etiqueta de origen acepta un código "[ISO 3166-1 Alfa-2](https://es.wikipedia.org/wiki/ISO_3166-1)" correspondiente al país de origen para las firmas a las que se aplica. Estos códigos deben escribirse en mayúsculas (minúsculas no se mostrarán correctamente). Cuando se utiliza una etiqueta de origen, se agrega a la entrada del campo de registro "Razón Bloqueado" para todas las solicitudes bloqueadas como resultado de las firmas a las que se aplica la etiqueta.

Si el componente opcional "flags CSS" está instalado, cuando se visualizan los archivos de registro a través de la página de registros del front-end, la información adjunta por las etiquetas de origen se reemplaza por el indicador del país correspondiente a esa información. Esta información, ya sea en su forma original o como bandera de país, se puede hacer clic, y cuando se hace clic en ella, filtrará las entradas de registro a través de otras entradas de registro de identificación similar (permitiendo de manera efectiva que aquellos que acceden a la página de registros se filtren por país de origen).

Nota: Técnicamente, esta no es ninguna forma de geolocalización, debido a que no involucra buscar ninguna información específica relacionada con las IP entrantes, sino simplemente, nos permite indicar explícitamente un país de origen para cualquier solicitud bloqueada por firmas específicas. Se permiten múltiples etiquetas de origen dentro de la misma sección de firma.

Ejemplo hipotético:

```
1.2.3.4/32 Deny Generic
Origin: CN
2.3.4.5/32 Deny Generic
Origin: FR
4.5.6.7/32 Deny Generic
Origin: DE
6.7.8.9/32 Deny Generic
Origin: US
Tag: Foobar
```

Cualquier etiqueta se puede usar en conjunto, y todas las etiquetas son opcionales (vea el ejemplo siguiente).

```
# Sección Ejemplo.
1.2.3.4/32 Deny Generic
Origin: US
Tag: Sección Ejemplo
Expires: 2016.12.31
```

##### 6.1.3 ETIQUETAS DE DEFERENCIA

Cuando se instalan y usan activamente grandes cantidades de archivos de firmas, las instalaciones pueden volverse bastante complejas y es posible que haya algunas firmas que se superpongan. En estos casos, para evitar que se desencadenen varias firmas superpuestas durante los eventos de bloque, las etiquetas de deferencia se pueden usar para diferir secciones de firmas específicas en los casos en que se instala y utiliza activamente algún otro archivo de firmas específico. Esto puede ser útil en casos en que algunas firmas se actualicen con mayor frecuencia que otras, con el fin de diferir las firmas actualizadas menos frecuentemente a favor de las firmas actualizadas con mayor frecuencia.

Las etiquetas de deferencia se usan de manera similar a otros tipos de etiquetas. El valor de la etiqueta debe coincidir con un archivo de firma instalado y utilizado activamente para ser diferido.

Ejemplo:

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 6.1.4 ETIQUETAS DE PERFIL

Las etiquetas de perfil proporcionan un medio para mostrar información adicional en la página de prueba de IP y pueden ser aprovechadas por módulos y reglas auxiliares para un comportamiento más complejo y una toma de decisiones más precisa.

Las etiquetas de perfil se utilizan de manera similar a otros tipos de etiquetas. Los valores de las etiquetas de perfil se pueden utilizar como condición para módulos y reglas auxiliares. Las etiquetas de perfil pueden proporcionar varios valores separando esos valores con un punto y coma. El usuario final nunca ve los valores de las etiquetas de perfil.

Ejemplo:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 6.2 YAML

##### 6.2.0 LOS FUNDAMENTOS DE YAML

Una forma simplificada de YAML markup se puede utilizar en los archivos de firmas con el propósito de definir los comportamientos y configuraciones específicas para las secciones de firmas individuales. Esto puede ser útil si desea que el valor de sus directivas de configuración diferir sobre la base de las firmas individuales y las secciones de firmas (por ejemplo; si desea proporcionar una dirección de correo electrónico para los tickets de soporte para cualquier usuario bloqueadas por una firma particular, pero no desea proporcionar una dirección de correo electrónico para tickets de soporte para usuarios bloqueados por cualquier otro firmas; si desea por algunas firmas específicas para desencadenar una redirección de página; si desea marcar una sección de firmas para usar con hCaptcha; si desea registrar los intentos de acceso bloqueados para archivos separados sobre la base de firmas individuales y/o secciones de firmas).

El uso de YAML markup en los archivos de firma es totalmente opcional (es decir, usted puede utilizarlo si desea hacerlo, pero no está obligado a hacerlo), y es capaz de aprovechar la mayoría (pero no todos) de las directivas de configuración.

Nota: La implementación de YAML markup en CIDRAM es muy simplista y muy limitado; Se tiene la intención de cumplir con los requisitos específicos para CIDRAM de una manera que tiene la familiaridad de YAML markup, pero no se sigue o cumple con las especificaciones oficiales (y por lo tanto no se comportará de la misma manera que las implementaciones más a fondo en otros lugares, y puede no ser apropiado para otros proyectos en otros lugares).

En CIDRAM, segmentos de YAML markup se identifican a la script a modo de tres guiones ("---"), y terminar junto a las secciones de firmas que acompañas vía doble saltos de línea. Un segmento típico de YAML markup dentro de una sección de firmas consiste en tres guiones en una línea inmediatamente después de la lista de CIDRs y cualquier etiquetas, seguido de una lista bidimensional de pares valores-clave (primera dimensión, categorías de directivas de configuración; segunda dimensión, directivas de configuración) de las directivas de configuración que deben modificarse (y para cual los valores) siempre que una firma dentro de esa sección de firmas se desencadena (ver los ejemplos siguientes).

```
# Foobar 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
4.5.6.7/32 Deny Generic
Tag: Foobar 1
---
general:
 http_response_header_code: 403
 emailaddr: username@domain.tld
logging:
 standard_log: "logfile.{yyyy}-{mm}-{dd}.txt"
 apache_style_log: "access.{yyyy}-{mm}-{dd}.txt"
 serialised_log: "serial.{yyyy}-{mm}-{dd}.txt"
template_data:
 css_url: "https://domain.tld/cidram.css"

# Foobar 2.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
4.5.6.7/32 Deny Generic
Tag: Foobar 2
---
general:
 http_response_header_code: 503
logging:
 standard_log: "logfile.Foobar2.{yyyy}-{mm}-{dd}.txt"
 apache_style_log: "access.Foobar2.{yyyy}-{mm}-{dd}.txt"
 serialised_log: "serial.Foobar2.{yyyy}-{mm}-{dd}.txt"

# Foobar 3.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
4.5.6.7/32 Deny Generic
Tag: Foobar 3
---
general:
 http_response_header_code: 403
 silent_mode: "http://127.0.0.1/"
```

#### 6.3 AUXILIAR

##### 6.3.0 IGNORANDO LAS SECCIONES DE FIRMA

En adición, si quieres CIDRAM ignorar completamente algunas secciones específicas dentro de cualquiera de los archivos de firmas, puede utilizar el archivo `ignore.dat` para especificar qué secciones por ignorar. En una línea nueva, escribir `Ignore`, seguido de un espacio, seguido del nombre de la sección que desea CIDRAM ignorar (vea el ejemplo siguiente).

```
Ignore Sección 1
```

Esto también se puede lograr utilizando la interfaz proporcionada por la página de "lista de secciones" del front-end de CIDRAM.

##### 6.3.1 REGLAS AUXILIARES

Si cree que escribir sus propios archivos de firmas personalizadas o módulos personalizados es demasiado complicado para usted, una alternativa más simple puede ser utilizar la interfaz proporcionada por la página de "reglas auxiliares" del front-end de CIDRAM. Al seleccionar las opciones apropiadas y especificar detalles sobre tipos específicos de solicitudes, puede indicar a CIDRAM cómo responder a esas solicitudes. Las "reglas auxiliares" se ejecutan después de que todos los archivos y módulos de firmas ya hayan terminado de ejecutarse.

##### 6.3.2 GUARDAR Y ACTIVAR ARCHIVOS DE FIRMA PERSONALIZADOS

Para CIDRAM v2 y anteriores, en la vault, encontrará dos archivos: `ipv4_custom.dat.RenameMe` y `ipv6_custom.dat.RenameMe`. Puede guardar firmas personalizadas en esos archivos o, si lo prefiere, puede crear archivos nuevos para sus firmas personalizadas y nombrarlas como desee. Para CIDRAM v2 y anteriores, los archivos de firma personalizados deben guardarse en la base del directorio de la vault.

Para CIDRAM v3 y posteriores, no hay archivos proporcionados previamente para firmas personalizadas, pero también puedes crear archivos nuevos para sus firmas personalizadas y nombrarlas como desees. Para CIDRAM v3 y posteriores, los archivos de firma personalizados deben guardarse en el directorio "signatures" preparado de su instalación de CIDRAM.

Para "activar" los archivos de firma personalizados, estos deben estar citados por las directivas de configuración "ipv4" o "ipv6" de su archivo de configuración (dependiendo de si los archivos de firma personalizados están destinados a firmas IPv4 o IPv6).

Para CIDRAM v2 y anteriores, "ipv4" e "ipv6" se encuentran en la categoría de configuración "signatures".

Para CIDRAM v3 y posteriores, "ipv4" e "ipv6" se encuentran en la categoría de configuración "components".

#### 6.4 <a name="MODULE_BASICS"></a>LOS FUNDAMENTOS (PARA MÓDULOS)

Los módulos se pueden usar para ampliar la funcionalidad de CIDRAM, realizar tareas adicionales o procesar lógica adicional.

Debido a que los módulos se escriben como archivos PHP, si está familiarizado adecuadamente con la base de código de CIDRAM, puede estructurar los módulos de la forma que desee, y escribe las firmas de tu módulo como quieras (dentro de lo que es posible con PHP).

*Nota: Si no se siente cómodo trabajando con código PHP, no se recomienda escribir sus propios módulos.*

CIDRAM brinda cierta funcionalidad que los módulos pueden usar, lo que simplifica la escritura de sus propios módulos. La información sobre esta funcionalidad se describe a continuación.

#### 6.5 FUNCIONALIDAD DEL MÓDULO

##### 6.5.0 "$this->trigger"

Las firmas de los módulos generalmente se escriben con `$this->trigger`. En la mayoría de los casos, este method será más importante que cualquier otra cosa con el fin de escribir módulos.

`$this->trigger` acepta 4 parámetros: `$Condition`, `$ReasonShort`, `$ReasonLong` (opcional), y `$DefineOptions` (opcional).

La veracidad de `$Condition` se evalúa, y si es true/verdadera, la firma se "desencadena". Si es false/falso, la firma *no* se "desencadena". `$Condition` generalmente contiene código PHP para evaluar una condición que debe causar el bloqueo de una solicitud.

`$ReasonShort` se cita en el campo "Razón Bloqueado" cuando la firma se "desencadena".

`$ReasonLong` es un mensaje opcional que se mostrará al usuario/cliente para cuando estén bloqueados, para explicar por qué se han bloqueado. Se predetermina al mensaje estándar "¡Acceso Denegado!" cuando se omite.

`$DefineOptions` es una array opcional que contiene pares clave/valor, que se utiliza para definir opciones de configuración específicas para la instancia de solicitud. Las opciones de configuración se aplicarán cuando la firma se "desencadena".

`$this->trigger` devuelve true/verdadero cuando la firma se "desencadena" y false/falso cuando no es así.

##### 6.5.1 "$this->bypass"

Los bypass de la firma generalmente se escriben con `$this->bypass`.

`$this->bypass` acepta 3 parámetros: `$Condition`, `$ReasonShort`, y `$DefineOptions` (opcional).

La veracidad de `$Condition` se evalúa, y si es true/verdadera, el bypass se "desencadena". Si es false/falso, el bypass *no* se "desencadena". `$Condition` generalmente contiene código PHP para evaluar una condición que *no* debe causar el bloqueo de una solicitud.

`$ReasonShort` se cita en el campo "Razón Bloqueado" cuando el bypass se "desencadena".

`$DefineOptions` es una array opcional que contiene pares clave/valor, que se utiliza para definir opciones de configuración específicas para la instancia de solicitud. Las opciones de configuración se aplicarán cuando el bypass se "desencadena".

`$this->bypass` devuelve true/verdadero cuando el bypass se "desencadena" y false/falso cuando no es así.

##### 6.5.2 "$this->dnsReverse"

Esto se puede usar para buscar el nombre del host de una dirección IP. Si desea crear un módulo para bloquear nombres de host, este method podría ser útil.

Ejemplo:
```PHP
<?php
/** Fetch hostname. */
if (empty($this->CIDRAM['Hostname'])) {
    $this->CIDRAM['Hostname'] = $this->dnsReverse($this->BlockInfo['IPAddr']);
}

/** Example signature. */
if (strlen($this->CIDRAM['Hostname']) && $this->CIDRAM['Hostname'] !== $this->BlockInfo['IPAddr']) {
    $this->trigger($this->CIDRAM['Hostname'] === 'www.foobar.tld', 'Foobar.tld', 'Hostname Foobar.tld is not allowed.');
}
```

#### 6.6 VARIABLES DE MÓDULO

Los módulos se ejecutan dentro de su propio alcance, y cualquier variable definida por un módulo, no será accesible para otros módulos, o para el script principal, a menos que estén almacenados en la array `$CIDRAM` (todo lo demás se vacía después de que finaliza la ejecución del módulo).

A continuación se enumeran algunas variables comunes que pueden ser útiles para su módulo:

Variable | Descripción
----|----
`$this->BlockInfo['DateTime']` | La fecha y hora actual.
`$this->BlockInfo['IPAddr']` | Dirección IP para la solicitud actual.
`$this->BlockInfo['IPAddrResolved']` | Si la dirección IP de la solicitud actual es una dirección 6to4, Teredo, o ISATAP, esa dirección se resuelve en su equivalente IPv4. En caso contrario, se indicará la dirección IP de la solicitud actual.
`$this->BlockInfo['ScriptIdent']` | Versión de CIDRAM.
`$this->BlockInfo['Query']` | La consulta para la solicitud actual.
`$this->BlockInfo['Referrer']` | El referente para la solicitud actual (si existe).
`$this->BlockInfo['UA']` | El agente de usuario (user agent) para la solicitud actual.
`$this->BlockInfo['UALC']` | El agente de usuario (user agent) para la solicitud actual (en minúsculas).
`$this->BlockInfo['ReasonMessage']` | El mensaje que se mostrará al usuario/cliente para la solicitud actual si están bloqueados.
`$this->BlockInfo['SignatureCount']` | El número de firmas desencadenadas para la solicitud actual.
`$this->BlockInfo['Signatures']` | Información de referencia para cualquier firma desencadenada para la solicitud actual.
`$this->BlockInfo['WhyReason']` | Información de referencia para cualquier firma desencadenada para la solicitud actual.
`$this->BlockInfo['Request_Method']` | El método de solicitud de la solicitud actual.
`$this->BlockInfo['Protocol']` | El protocolo de la solicitud actual.

---


### 7. <a name="SECTION7"></a>CONOCIDOS PROBLEMAS DE COMPATIBILIDAD

Se ha encontrado que los siguientes paquetes y productos son incompatibles con CIDRAM:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

Los módulos se han puesto a disposición para garantizar que los siguientes paquetes y productos sean compatibles con CIDRAM:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__
- __[Quic cloud](https://wordpress.org/support/topic/quic-dot-cloud-requires-all-ips-allowed/)__

*Ver también: [Gráficos de Compatibilidad](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 8. <a name="SECTION8"></a>PREGUNTAS MÁS FRECUENTES (FAQ)

- [¿Qué es una "firma"?](#user-content-WHAT_IS_A_SIGNATURE)
- [¿Qué es un "CIDR"?](#user-content-WHAT_IS_A_CIDR)
- [¿Qué es un "falso positivo"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)
- [¿Puede CIDRAM bloquear países enteros?](#user-content-BLOCK_ENTIRE_COUNTRIES)
- [¿Con qué frecuencia se actualizan las firmas?](#user-content-SIGNATURE_UPDATE_FREQUENCY)
- [¡He encontrado un problema mientras uso CIDRAM y no sé qué hacer al respecto! ¡Por favor ayuda!](#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [¡He sido bloqueado por CIDRAM desde un sitio web que quiero visitar! ¡Por favor ayuda!](#user-content-BLOCKED_WHAT_TO_DO)
- [Quiero usar CIDRAM v2~v4 con una versión de PHP más vieja que 7.2; ¿Puede usted ayudar?](#user-content-MINIMUM_PHP_VERSION_V3)
- [¿Puedo usar una sola instalación de CIDRAM para proteger múltiples dominios?](#user-content-PROTECT_MULTIPLE_DOMAINS)
- [No quiero molestarme con la instalación de este y conseguir que funcione con mi sitio web; ¿Puedo pagarte por hacer todo por mí?](#user-content-PAY_YOU_TO_DO_IT)
- [¿Puedo contratar a usted oa cualquiera de los desarrolladores de este proyecto para el trabajo privado?](#user-content-HIRE_FOR_PRIVATE_WORK)
- [Necesito modificaciones especiales, personalizaciones, etc; ¿Puede usted ayudar?](#user-content-SPECIALIST_MODIFICATIONS)
- [Soy desarrollador, diseñador de sitios web o programador. ¿Puedo aceptar u ofrecer trabajos relacionados con este proyecto?](#user-content-ACCEPT_OR_OFFER_WORK)
- [Quiero contribuir al proyecto; ¿Puedo hacer esto?](#user-content-WANT_TO_CONTRIBUTE)
- [¿Puedo usar cron para actualizar automáticamente?](#user-content-CRON_TO_UPDATE_AUTOMATICALLY)
- [¿Qué son "infracciones"?](#user-content-WHAT_ARE_INFRACTIONS)
- [¿Puede CIDRAM bloquear nombres de host?](#user-content-BLOCK_HOSTNAMES)
- [¿Qué puedo usar para "default_dns"?](#qué-puedo-usar-para-default_dns)
- [¿Puedo usar CIDRAM para proteger cosas que no sean sitios web (por ejemplo, servidores de correo electrónico, FTP, SSH, IRC, etc)?](#user-content-PROTECT_OTHER_THINGS)
- [¿Se producirán problemas si uso CIDRAM al mismo tiempo que uso CDN o servicios de caché?](#user-content-CDN_CACHING_PROBLEMS)
- [¿CIDRAM protegerá mi sitio web de los ataques DDoS?](#user-content-DDOS_ATTACKS)
- [Cuando activar o desactivar módulos o archivos de firmas a través de la página de actualizaciones, los ordena de forma alfanumérica en la configuración. ¿Puedo cambiar la forma en que se ordenan?](#user-content-CHANGE_COMPONENT_SORT_ORDER)
- [¿Qué es un "PDO DSN"? Cómo puedo usar PDO con CIDRAM?](#user-content-HOW_TO_USE_PDO)
- [CIDRAM está bloqueando cronjobs; ¿Cómo arreglar esto?](#user-content-BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>¿Qué es una "firma"?

En el contexto de CIDRAM, una "firma" se refiere a datos que actúan como un indicador/identificador para algo específico que estamos buscando, normalmente una dirección IP o CIDR, e incluye algunas instrucciones para CIDRAM, diciéndole la mejor manera de responder cuando encuentra lo que estamos buscando. Una firma típica para CIDRAM se parece a esto:

Para "archivos de firma":

`1.2.3.4/32 Deny Generic`

Para "módulos":

```PHP
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*Nota: Las firmas para "archivos de firma", y las firmas para "módulos", no son lo mismo.*

A menudo (pero no siempre), las firmas se agruparán en grupos, formando "secciones de firmas", a menudo acompañado de comentarios, markup, y/o metadatos relacionados que se pueden utilizar para proporcionar contexto adicional para las firmas y/o instrucción adicional.

#### <a name="WHAT_IS_A_CIDR"></a>¿Qué es un "CIDR"?

"CIDR" es un acrónimo para "Classless Inter-Domain Routing" (o "enrutamiento entre dominios sin clases") *[[1](https://es.wikipedia.org/wiki/Classless_Inter-Domain_Routing), [2](https://whatismyipaddress.com/cidr)]*, y es este acrónimo que se utiliza como parte del nombre de este paquete, "CIDRAM", que es un acrónimo de "Classless Inter-Domain Routing Access Manager".

En el contexto de CIDRAM, "CIDR" (o "CIDRs") se refiere específicamente a las subredes expresadas mediante la notación CIDR.

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>¿Qué es un "falso positivo"?

El término "falso positivo" (*alternativamente: "error falso positivo"; "falsa alarma"*; Inglés: *false positive*; *false positive error*; *false alarm*), descrito muy simplemente, y en un contexto generalizado, se utiliza cuando se prueba para una condición, para referirse a los resultados de esa prueba, cuando los resultados son positivos (es decir, la condición se determina como "positivo", o "verdadero"), pero se espera que sean (o debería haber sido) negativo (es decir, la condición, en realidad, es "negativo", o "falso"). Un "falso positivo" podría considerarse análoga a "llorando lobo" (donde la condición que se está probando es si hay un lobo cerca de la manada, la condición es "falso" en el que no hay lobo cerca de la manada, y la condición se reporta como "positiva" por el pastor a modo de llamando "lobo, lobo"), o análogos a situaciones en las pruebas médicas donde un paciente es diagnosticado con alguna enfermedad o dolencia, cuando en realidad, no tienen tal enfermedad o dolencia.

Algunos términos relacionados para cuando se prueba para un condición son "verdadero positivo", "verdadero negativo" y "falso negativo". Un "verdadero positivo" se refiere a cuando los resultados de la prueba y el estado real de la condición son ambas verdaderas (o "positivas"), y un "verdadero negativo" se refiere a cuando los resultados de la prueba y el estado real de la condición son ambas falsas (o "negativas"); Un "verdadero positivo" o "negativo verdadero" se considera que es una "inferencia correcta". La antítesis de un "falso positivo" es un "falso negativo"; Un "falso negativo" se refiere a cuando los resultados de la prueba son negativos (es decir, la condición se determina como "negativo", o "falso"), pero se espera que sean (o debería haber sido) positivo (es decir, la condición, en realidad, es "positivo", o "verdadero").

En el contexto de CIDRAM, estos términos se refieren a las firmas de CIDRAM y lo qué/quién se bloquean. Cuando CIDRAM se bloquean una dirección IP debido al mal, obsoleta o firmas incorrectas, pero no debería haber hecho, o cuando lo hace por las razones equivocadas, nos referimos a este evento como un "falso positivo". Cuando CIDRAM no puede bloquear una dirección IP que debería haber sido bloqueado, debido a las amenazas imprevistas, firmas perdidas o déficit en sus firmas, nos referimos a este evento como una "detección perdida" o "missed detection" (que es análogo a un "falso negativo").

Esto se puede resumir en la siguiente tabla:

&nbsp; | CIDRAM *NO* debe bloquear una dirección IP | CIDRAM *DEBE* bloquear una dirección IP
---|---|---
CIDRAM *NO* hace bloquear una dirección IP | Verdadero negativo (inferencia correcta) | Detección perdida (análogo a un falso negativo)
CIDRAM *HACE* bloquear una dirección IP | __Falso positivo__ | Verdadero positivo (inferencia correcta)

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>¿Puede CIDRAM bloquear países enteros?

Sí. La forma más fácil de hacerlo sería instalar el módulo BGPView y configurarlo de acuerdo con sus necesidades.

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>¿Con qué frecuencia se actualizan las firmas?

La frecuencia de actualización varía dependiendo de los archivos de firma en cuestión. Todos los mantenedores de los archivos de firma para CIDRAM generalmente tratan de mantener sus firmas tan actualizadas como sea posible, pero como todos nosotros tenemos varios otros compromisos, nuestras vidas fuera del proyecto, y como ninguno de nosotros es financieramente compensado (o pagado) por nuestros esfuerzos en el proyecto, no se puede garantizar un calendario de actualización preciso. Generalmente, las firmas se actualizan siempre que haya suficiente tiempo para actualizarlas, y generalmente, los mantenedores tratan de priorizar basándose en la necesidad y en la frecuencia con la que ocurren cambios entre rangos. La ayuda siempre es apreciada si usted está dispuesto a ofrecer cualquiera.

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>¡He encontrado un problema mientras uso CIDRAM y no sé qué hacer al respecto! ¡Por favor ayuda!

- ¿Está utilizando la última versión del software? ¿Está utilizando las últimas versiones de sus archivos de firma? Si la respuesta a cualquiera de estas dos preguntas es no, intente actualizar todo primero, y compruebe si el problema persiste. Si persiste, continúe leyendo.
- ¿Ha revisado toda la documentación? Si no, por favor, hágalo. Si el problema no puede resolverse utilizando la documentación, continúe leyendo.
- ¿Ha revisado la **[página de issues](https://github.com/CIDRAM/CIDRAM/issues)**, para ver si el problema ha sido mencionado antes? Si se ha mencionado antes, compruebe si se han proporcionado sugerencias, ideas y/o soluciones, y siga según sea necesario para tratar de resolver el problema.
- Si el problema persiste, solicite ayuda al crear un nuevo issue en la página de issues.

#### <a name="BLOCKED_WHAT_TO_DO"></a>¡He sido bloqueado por CIDRAM desde un sitio web que quiero visitar! ¡Por favor ayuda!

CIDRAM proporciona un medio para que los propietarios de sitios web bloqueen tráfico indeseable, pero es responsabilidad de los propietarios de sitios web decidir por sí mismos cómo quieren usar CIDRAM. En el caso de los falsos positivos relativos a los archivos de firma normalmente incluidos en CIDRAM, correcciones pueden hacerse, Pero en lo que respecta a ser desbloqueado de sitios web específicos, usted tendrá que tomar eso con los propietarios de los sitios web en cuestión. En los casos en que se realizan correcciones, por lo menos, tendrán que actualizar sus archivos de firma y/o instalación, y en otros casos (tales como, por ejemplo, donde han modificado su instalación, crearon sus propias firmas personalizadas, etc), la responsabilidad de resolver su problema es enteramente suya, y está totalmente fuera de nuestro control.

#### <a name="MINIMUM_PHP_VERSION_V3"></a>Quiero usar CIDRAM v2~v4 con una versión de PHP más vieja que 7.2; ¿Puede usted ayudar?

No. PHP≥7.2 es un requisito mínimo para CIDRAM v2~v4.

*Ver también: [Gráficos de Compatibilidad](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>¿Puedo usar una sola instalación de CIDRAM para proteger múltiples dominios?

Sí. Las instalaciones de CIDRAM no están ligados naturalmente en dominios específicos, y por lo tanto puede ser utilizado para proteger múltiples dominios. En general, nos referimos a las instalaciones de CIDRAM que protegen solo un dominio como "instalaciones solo-dominio" ("single-domain installations"), y nos referimos a las instalaciones de CIDRAM que protegen múltiples dominios y/o subdominios como "instalaciones multi-dominio" ("multi-domain installations"). Si utiliza una instalación multi-dominio y es necesario utilizar diferentes conjuntos de archivos de firmas para diferentes dominios, o si CIDRAM debe configurarse de manera diferente para diferentes dominios, es posible hacer esto. Después de cargar el archivo de configuración (`config.yml`), CIDRAM comprobará la existencia de un "archivo de sustitución para configuración" específico del dominio (o subdominio) que se solicita (`el-dominio-que-se-solicita.tld.config.yml`), y si se encuentra, cualquier valor de configuración definido por el archivo de sustitución para configuración se utilizará para la instancia de ejecución en lugar de los valores de configuración definidos por el archivo de configuración. Los archivos de sustitución para configuración son idénticos al archivo de configuración, ya su discreción, puede contener la totalidad de todas las directivas de configuración disponibles para CIDRAM, o lo que sea subsección necesaria que difiera de los valores normalmente definidos por el archivo de configuración. Los archivos de sustitución para configuración se nombran de acuerdo con el dominio al que están destinados (así por ejemplo, si se requiere un archivo de sustitución para configuración para el dominio, `https://www.some-domain.tld/`, su archivo de sustitución para configuración debe ser nombrado como `some-domain.tld.config.yml`, y debe colocarse dentro de la vault junto con el archivo de configuración, `config.yml`). El nombre del dominio para la instancia de ejecución se deriva del encabezado `HTTP_HOST` de la solicitud; "www" se ignora.

#### <a name="PAY_YOU_TO_DO_IT"></a>No quiero molestarme con la instalación de este y conseguir que funcione con mi sitio web; ¿Puedo pagarte por hacer todo por mí?

Quizás. Esto se considera caso por caso. Háganos saber lo que necesita, lo que está ofreciendo y le diremos si podemos ayudar.

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>¿Puedo contratar a usted oa cualquiera de los desarrolladores de este proyecto para el trabajo privado?

*Ver la respuesta anterior.*

#### <a name="SPECIALIST_MODIFICATIONS"></a>Necesito modificaciones especiales, personalizaciones, etc; ¿Puede usted ayudar?

*Ver la respuesta anterior.*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>Soy desarrollador, diseñador de sitios web o programador. ¿Puedo aceptar u ofrecer trabajos relacionados con este proyecto?

Sí. Nuestra licencia no lo prohíbe.

#### <a name="WANT_TO_CONTRIBUTE"></a>Quiero contribuir al proyecto; ¿Puedo hacer esto?

Sí. Las contribuciones al proyecto son muy bienvenidas. Consulte "CONTRIBUTING.md" para obtener más información.

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>¿Puedo usar cron para actualizar automáticamente?

Sí. Una API está integrada en el front-end para interactuar con la página de actualizaciones a través de scripts externos. Un script separado, "[Cronable](https://github.com/Maikuolan/Cronable)", está disponible, y puede ser utilizado por su cron manager o cron scheduler para actualizar este y otros paquetes soportados automáticamente (este script proporciona su propia documentación).

#### <a name="WHAT_ARE_INFRACTIONS"></a>¿Qué son "infracciones"?

El "recuento de firmas" y las "infracciones" se relacionan con la gravedad y la cantidad de firmas desencadenadas durante una solicitud particular, ya sea debido a archivos de firmas, módulos, reglas auxiliares, u otros, pero mientras que el "recuento de firmas" persiste solo para esa solicitud en particular, las "infracciones" pueden persistir en cualquier número de solicitudes, siempre que lo determine el `default_tracktime`.

Esto proporciona un mecanismo para garantizar que las solicitudes de fuentes potencialmente peligrosas puedan bloquearse en solicitudes secundarias de cualquier fuente particular en la que esa fuente ya haya sido bloqueada durante una solicitud anterior con un número suficiente de infracciones.

#### <a name="BLOCK_HOSTNAMES"></a>¿Puede CIDRAM bloquear nombres de host?

Sí. Esto se puede lograr creando una regla auxiliar o un módulo personalizado.

![Una regla auxiliar para bloquear nombres de host](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>¿Qué puedo usar para "default_dns"?

En general, la IP de cualquier servidor DNS confiable debería ser suficiente. Si está buscando sugerencias, [public-dns.info](https://public-dns.info/) y [OpenNIC](https://servers.opennic.org/) brindan amplias listas de servidores DNS conocidos y públicos. Alternativamente, vea la tabla a continuación:

IP | Operador
---|---
`1.1.1.1` | [Cloudflare](https://www.cloudflare.com/learning/dns/what-is-1.1.1.1/)
`8.8.4.4`<br />`8.8.8.8`<br />`2001:4860:4860::8844`<br />`2001:4860:4860::8888` | [Google Public DNS](https://developers.google.com/speed/public-dns/)
`9.9.9.9`<br />`149.112.112.112` | [Quad9 DNS](https://www.quad9.net/)
`84.200.69.80`<br />`84.200.70.40`<br />`2001:1608:10:25::1c04:b12f`<br />`2001:1608:10:25::9249:d69b` | [DNS.WATCH](https://dns.watch/index)
`208.67.220.220`<br />`208.67.222.220`<br />`208.67.222.222` | [OpenDNS Home](https://www.opendns.com/)
`77.88.8.1`<br />`77.88.8.8`<br />`2a02:6b8::feed:0ff`<br />`2a02:6b8:0:1::feed:0ff` | [Yandex.DNS](https://dns.yandex.com/advanced/)
`8.20.247.20`<br />`8.26.56.26` | [Comodo Secure DNS](https://www.comodo.com/secure-dns/)
`216.146.35.35`<br />`216.146.36.36` | [Dyn](https://help.dyn.com/internet-guide-setup/)
`64.6.64.6`<br />`64.6.65.6` | [Verisign Public DNS](https://www.verisign.com/en_US/security-services/public-dns/index.xhtml)
`37.235.1.174`<br />`37.235.1.177`<br />`45.33.97.5`<br />`172.104.237.57`<br />`172.104.49.100` | [FreeDNS](https://freedns.zone/en/)
`156.154.70.1`<br />`156.154.71.1`<br />`2610:a1:1018::1`<br />`2610:a1:1019::1` | [Neustar Security](https://www.security.neustar/dns-services/free-recursive-dns-service)
`45.32.36.36`<br />`45.77.165.194` | [Fourth Estate](https://dns.fourthestate.co/)
`74.82.42.42` | [Hurricane Electric](https://dns.he.net/)
`195.46.39.39`<br />`195.46.39.40` | [SafeDNS](https://www.safedns.com/en/features/)
`89.233.43.71`<br />`91.239.100.100 `<br />`2001:67c:28a4::`<br />`2a01:3a0:53:53::` | [UncensoredDNS](https://blog.uncensoreddns.org/)
`208.76.50.50`<br />`208.76.51.51` | [SmartViper](https://www.markosweb.com/free-dns/)

*Nota: Yo no realizo ningún reclamo o garantía con respecto a las prácticas de privacidad, seguridad, eficacia ni confiabilidad de los servicios de DNS enumerados o de otro modo. Por favor, haga su propia investigación al tomar decisiones sobre ellos.*

#### <a name="PROTECT_OTHER_THINGS"></a>¿Puedo usar CIDRAM para proteger cosas que no sean sitios web (por ejemplo, servidores de correo electrónico, FTP, SSH, IRC, etc)?

Puedes (legalmente), pero no deberías (técnicamente; prácticamente). Nuestra licencia no limita qué tecnologías implementan CIDRAM, pero CIDRAM es un WAF (firewall de aplicaciones web) y siempre ha sido diseñado para proteger sitios web. Debido a que no fue diseñado con otras tecnologías en mente, es improbable que sea efectivo o brinde protección confiable para otras tecnologías, la implementación es probable que sea difícil, y el riesgo de falsos positivos y detecciones perdidas es muy alto.

#### <a name="CDN_CACHING_PROBLEMS"></a>¿Se producirán problemas si uso CIDRAM al mismo tiempo que uso CDN o servicios de caché?

Posiblemente. Esto depende de la naturaleza del servicio en cuestión y de cómo lo está usando. En general, si solo está almacenando en caché activos estáticos (imágenes, CSS, etc; cualquier cosa que generalmente no cambia con el tiempo), no debería haber ningún problema. Pero, puede haber problemas si almacena datos en caché que, de lo contrario, se generarían dinámicamente cuando se soliciten, o si está almacenando en caché los resultados de las solicitudes POST (esto esencialmente haría que su sitio web y su entorno sean obligatoriamente estáticos, y es improbable que CIDRAM proporcione ningún beneficio significativo en un entorno obligatoriamente estático). También puede haber requisitos de configuración específicos para CIDRAM, dependiendo de qué CDN o servicio de caché está utilizando (deberá asegurarse de que CIDRAM esté configurado correctamente para el CDN o el servicio de caché específico que está utilizando). Si CIDRAM no se configura correctamente, pueden producirse falsos positivos y detecciones perdidas.

#### <a name="DDOS_ATTACKS"></a>¿CIDRAM protegerá mi sitio web de los ataques DDoS?

Respuesta corta: No.

Respuesta un poco más larga: CIDRAM ayudará a reducir el impacto que el tráfico no deseado puede tener en su sitio web (en efecto reduciendo los costos de ancho de banda de su sitio web), ayudará a reducir el impacto que el tráfico no deseado puede tener en su hardware (por ejemplo, la capacidad de su servidor para procesar y atender solicitudes), y puede ayudar a reducir otros posibles efectos negativos asociados con el tráfico no deseado. Sin embargo, hay dos cosas importantes que deben recordarse para comprender esta pregunta.

En primer lugar, CIDRAM es un paquete PHP y, por lo tanto, opera en la máquina donde está instalado PHP. Esto significa que CIDRAM solo puede ver y bloquear una solicitud *después* de que el servidor ya la haya recibido. En segundo lugar, la [mitigación de DDoS](https://es.wikipedia.org/wiki/Mitigaci%C3%B3n_de_DDoS) efectiva debe filtrar las solicitudes *antes* de que lleguen al servidor al que se dirige el ataque DDoS. Idealmente, los ataques DDoS deberían ser detectados y mitigados por soluciones capaces de eliminar o redirigir el tráfico asociado con ataques, antes de que llegue al servidor objetivo en primer lugar.

Esto puede implementarse utilizando soluciones de hardware locales dedicadas y/o soluciones basadas en la nube, como servicios de mitigación DDoS dedicados, enrutamiento del DNS de un dominio a través de redes resistentes a DDoS, filtrado basado en la nube, o alguna combinación de los mismos. En cualquier caso, este tema es un poco demasiado complejo para explicarlo exhaustivamente con solo un párrafo o dos, por lo que recomendaría investigar más si este es un tema que desea seguir. Cuando la verdadera naturaleza de los ataques DDoS se entiende correctamente, esta respuesta tendrá más sentido.

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>Cuando activar o desactivar módulos o archivos de firmas a través de la página de actualizaciones, los ordena de forma alfanumérica en la configuración. ¿Puedo cambiar la forma en que se ordenan?

Sí. Si necesita forzar algunos archivos se ejecuten en un orden específico, puede agregar algunos datos arbitrarios antes de sus nombres en la directiva de configuración donde están listados, separados por dos puntos. Cuando la página de actualizaciones clasifique los archivos nuevamente, esta información adicional arbitraria afectará el orden de clasificación, haciendo que, en consecuencia, se ejecuten en el orden que desee, sin necesidad de cambiar el nombre de ninguno de ellos.

Por ejemplo, suponiendo una directiva de configuración con los archivos enumerados de la siguiente manera:

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

Si quería ejecutar `file3.php` primero, puede agregar algo como `aaa:` antes del nombre del archivo:

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

Entonces, si se activa un archivo nuevo, `file6.php`, cuando la página de actualizaciones los clasifique nuevamente, debería terminar así:

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

La misma situación cuando un archivo está desactivado. Por el contrario, si quería que el archivo se ejecuta al final, podría agregar algo como `zzz:` antes del nombre del archivo. En cualquier caso, no necesitará cambiar el nombre del archivo en cuestión.

#### <a name="HOW_TO_USE_PDO"></a>¿Qué es un "PDO DSN"? Cómo puedo usar PDO con CIDRAM?

"PDO" es un acrónimo de "[PHP Data Objects](https://www.php.net/manual/es/intro.pdo.php)" (objetos de datos PHP). Proporciona una interfaz para PHP para poder conectarse a algunos sistemas de bases de datos comúnmente utilizados por varias aplicaciones PHP.

"DSN" es un acrónimo de "[data source name](https://es.wikipedia.org/wiki/Data_Source_Name)" (nombre de fuente de datos). El "PDO DSN" describe a PDO cómo debe conectarse a una base de datos.

CIDRAM ofrece la opción de utilizar PDO para fines de almacenamiento en caché. Para que esto funcione correctamente, deberá configurar CIDRAM en consecuencia, habilitando PDO, crear una nueva base de datos para que CIDRAM la use (si aún no tiene en mente una base de datos para que CIDRAM la use) y crear una nueva tabla en su base de datos de acuerdo con la estructura que se describe a continuación.

Cuando una conexión de base de datos se realiza correctamente, pero la tabla necesaria no existe, intentará crearla automáticamente. Pero, este comportamiento no se ha probado exhaustivamente y no se puede garantizar el éxito.

Esto, por supuesto, solo se aplica si realmente desea que CIDRAM use PDO. Si está lo suficientemente contento de que CIDRAM use el almacenamiento en caché de archivos planos (según su configuración predeterminada), o cualquiera de las otras opciones de almacenamiento en caché proporcionadas, no tendrá que preocuparse de configurar bases de datos, tablas, etc.

La estructura que se describe a continuación usa "cidram" como nombre de la base de datos, pero puede usar el nombre que desee para su base de datos, siempre que ese mismo nombre se replique en su configuración DSN.

```
╔══════════════════════════════════════════════╗
║ DATABASE "cidram"                            ║
║ │╔═══════════════════════════════════════════╩═════╗
║ └╫─TABLE "Cache" (UTF-8)                           ║
║  ╠═╪═FIELD══CHARSET═DATATYPE═════KEY══NULL═DEFAULT═╣
║  ║ ├─"Key"──UTF-8───VARCHAR(128)─PRI──×────×       ║
║  ║ ├─"Data"─UTF-8───TEXT─────────×────×────×       ║
╚══╣ └─"Time"─×───────INT(>=10)────×────×────×       ║
   ╚═════════════════════════════════════════════════╝
```

La directiva de configuración `pdo_dsn` de CIDRAM debe configurarse como se describe a continuación.

```
Dependiendo de qué controlador de base de datos se use...
├─4d (¡Advertencia: Experimental, no probado, no recomendado!)
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └El host con el que conectarse para encontrar la base de datos.
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └El nombre de la base de datos a
│                │              │             usar.
│                │              │
│                │              └El número de puerto para conectarse al host.
│                │
│                └El host con el que conectarse para encontrar la base de
│                 datos.
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └El nombre de la base de datos a usar.
│    │          │
│    │          └El host con el que conectarse para encontrar la base de datos.
│    │
│    └Valores posibles: "mssql", "sybase", "dblib".
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├Puede ser una ruta a un archivo de base de datos local.
│                    │
│                    ├Se puede conectar con un host y número de puerto.
│                    │
│                    └Debe consultar la documentación de Firebird si desea usar
│                     esto.
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └Con qué base de datos catalogada para conectarse.
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └Con qué base de datos catalogada para conectarse.
├─mysql (¡Lo más recomendado!)
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └El número de puerto para
│                 │            │               conectarse al host.
│                 │            │
│                 │            └El host con el que conectarse para encontrar la
│                 │             base de datos.
│                 │
│                 └El nombre de la base de datos a usar.
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├Puede hacer referencia a la base de datos catalogada
│               │específica.
│               │
│               ├Se puede conectar con un host y número de puerto.
│               │
│               └Debe consultar la documentación de Oracle si desea usar esto.
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├Puede hacer referencia a la base de datos catalogada específica.
│         │
│         ├Se puede conectar con un host y número de puerto.
│         │
│         └Debe consultar la documentación de ODBC/DB2 si desea usar esto.
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └El nombre de la base de datos a
│               │              │            usar.
│               │              │
│               │              └El número de puerto para conectarse al host.
│               │
│               └El host con el que conectarse para encontrar la base de datos.
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └La ruta al archivo de base de datos local a utilizar.
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └El nombre de la base de datos a usar.
                   │         │
                   │         └El número de puerto para conectarse al host.
                   │
                   └El host con el que conectarse para encontrar la base de datos.
```

Si no está seguro de qué usar para una parte particular de su DSN, intenta ver primero si funciona como está, sin cambiar nada.

Tenga en cuenta que `pdo_username` y` pdo_password` deben coincidir con el nombre de usuario y la contraseña que eligió para su base de datos.

#### <a name="BLOCK_CRON"></a>CIDRAM está bloqueando cronjobs; ¿Cómo arreglar esto?

Si está utilizando un archivo dedicado con el propósito de cronjobs, y si ese archivo no necesita ser llamado durante las solicitudes normales del usuario (es decir, fuera del contexto de cronjobs), la forma más directa de solucionar esto sería asegurarse de que CIDRAM no se ejecute en absoluto durante sus cronjobs (es decir, no conecte CIDRAM al archivo responsable de manejar sus cronjobs).

Alternativamente, si eso no es posible, pero la dirección IP de su servidor cron es relativamente consistente y predecible, podría intentar incluir en la lista blanca la dirección IP de su servidor cron por medio de creando una firma en un archivo de firma personalizado o creando una regla auxiliar en consecuencia para incluirlo en la lista blanca. Si la dirección IP de su servidor cron cambia regularmente y no es particularmente predecible, pero no obstante permanece dentro de la misma red particular, puede intentar incluir en su archivo `ignore.dat` el nombre de la sección de la firma responsable de bloquearlo en primer lugar.

Si ha probado todas esas ideas y ninguna funcionó para usted, o si necesita ayuda para descubrir cómo hacerlo, puede crear un nuevo issue en la página de issues de CIDRAM para pedir ayuda.

---


### 9. <a name="SECTION9"></a>INFORMACIÓN LEGAL

#### 9.0 PREÁMBULO DE SECCIÓN

La intención de esta sección de la documentación es para describir posibles consideraciones legales con respecto al uso y la implementación del paquete, y para proporcionar cierta información básica relacionada. Esto puede ser importante para algunos usuarios como un medio para garantizar el cumplimiento de los requisitos legales que puedan existir en los países en los que operan, y algunos usuarios pueden necesitar ajustar las políticas de su sitio web de acuerdo con esta información.

Primero y ante todo, tenga en cuenta que yo (el autor del paquete) no soy un abogado, ni un profesional legal calificado de ningún tipo. Por lo tanto, no estoy legalmente calificado para brindar asesoramiento legal. Además, en algunos casos, los requisitos legales exactos pueden variar entre diferentes países y jurisdicciones, y estos diferentes requisitos legales pueden a veces entrar en conflicto (como, por ejemplo, en el caso de países que favorecen los [derechos de privacidad](https://es.wikipedia.org/wiki/Derecho_a_la_intimidad) y el [derecho a ser olvidado](https://es.wikipedia.org/wiki/Derecho_al_olvido), frente a los países que favorecen la [retención de datos extendida](https://es.wikipedia.org/wiki/Retenci%C3%B3n_de_datos_de_telecomunicaci%C3%B3n)). Considere también que el acceso al paquete no está restringido a países o jurisdicciones específicos, y por lo tanto, es probable que la base de usuarios del paquete sea geográficamente diversa. Considerados estos puntos, no estoy en condiciones de decir lo que significa ser "legalmente compatible" para todos los usuarios, en todos los aspectos. Sin embargo, espero que la información en este documento lo ayude a tomar una decisión sobre lo que debe hacer para cumplir con la ley en el contexto del paquete. Si tiene alguna duda o inquietud con respecto a la información aquí incluida, o si necesita ayuda y asesoramiento adicional desde una perspectiva legal, le recomiendo consultar a un profesional legal calificado.

#### 9.1 RESPONSABILIDAD

Según lo establecido por la licencia del paquete, el paquete se proporciona sin ninguna garantía. Esto incluye (pero no se limita a) todo el alcance de la responsabilidad. El paquete se le proporciona para su conveniencia, con la esperanza de que sea útil y le proporcionará algún beneficio. Pero, si usa o implementa el paquete, es su propia decisión. No está obligado a usar o implementar el paquete, pero cuando lo hace, usted es responsable de esa decisión. Ni yo ni ningún otro contribuyente del paquete somos legalmente responsables de las consecuencias de las decisiones que usted tome, independientemente de si son directas, indirectas, implícitas o de otro tipo.

#### 9.2 TERCEROS

Dependiendo de su configuración e implementación exactas, el paquete puede comunicarse y compartir información con terceros en algunos casos. Esta información puede definirse como "[información personal](https://es.wikipedia.org/wiki/Informaci%C3%B3n_personal)" (PII) en algunos contextos, en algunas jurisdicciones.

La forma en que esta información puede ser utilizada por estos terceros está sujeta a las diversas políticas establecidas por estos terceros y está fuera del alcance de esta documentación. Pero, en todos estos casos, se puede deshabilitar el intercambio de información con estos terceros. En todos estos casos, si elige habilitarlo, es su responsabilidad investigar cualquier inquietud que pueda tener con respecto a la privacidad, seguridad y uso de PII por parte de estos terceros. Si tiene alguna duda, o si no está satisfecho con la conducta de estos terceros en lo que respecta a PII, puede ser mejor desactivar el intercambio de información con estos terceros.

A los efectos de la transparencia, el tipo de información compartida, y con quién, se describe a continuación.

##### 9.2.0 BÚSQUEDA DE NOMBRES DE HOST

Si usa funciones o módulos destinados a trabajar con nombres de host (como el "módulo bloqueador de hosts malos", "tor project exit nodes block module", o la "verificación de los motores de búsqueda", por ejemplo), CIDRAM necesita poder obtener el nombre de host de las solicitudes entrantes de alguna manera. Normalmente, lo hace al solicitar el nombre de host de la dirección IP de las solicitudes entrantes desde un servidor DNS, o solicitando la información a través de la funcionalidad provista por el sistema donde está instalado CIDRAM (esto se conoce típicamente como una "búsqueda de nombre de host"). Los servidores DNS predefinidos pertenecen al servicio [Google DNS](https://dns.google.com/) (pero esto se puede cambiar fácilmente a través de la configuración). Los servicios exactos comunicados son configurables y dependen de cómo configure el paquete. En el caso de utilizar la funcionalidad proporcionada por el sistema donde está instalado CIDRAM, deberá ponerse en contacto con el administrador de su sistema para determinar qué rutas utilizan las búsquedas de nombres de host. Las búsquedas de nombre de host se pueden evitar en CIDRAM por evitando los módulos afectados o modificando la configuración del paquete de acuerdo con sus necesidades.

*Directivas de configuración relevantes:*
- `general` -> `allow_gethostbyaddr_lookup`
- `general` -> `default_dns`
- `general` -> `force_hostname_lookup`
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.1 VERIFICACIÓN DEL MOTOR DE BÚSQUEDA Y REDES SOCIALES

Cuando la verificación del motor de búsqueda está habilitada, CIDRAM intenta realizar "búsquedas DNS hacia adelante" para verificar si las solicitudes que afirman tener su origen en los motores de búsqueda son auténticas. Del mismo modo, cuando la verificación de redes sociales está habilitada, CIDRAM hace lo mismo para solicitudes aparentes de redes sociales. Para hacer esto, utiliza el servicio [Google DNS](https://dns.google.com/) para intentar resolver las direcciones IP de los nombres de host de estas solicitudes entrantes (en este proceso, los nombres de host de estas solicitudes entrantes se comparten con el servicio).

*Directivas de configuración relevantes:*
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.2 CAPTCHA

CIDRAM suporte CAPTCHA. Requieren claves API para funcionar correctamente. Están deshabilitados de forma predeterminada, pero se pueden habilitar configurando las claves API requeridas. Cuando están habilitado, la comunicación puede ocurrir entre el servicio y CIDRAM o el navegador del usuario. Esto puede implicar la comunicación de información como la dirección IP del usuario, el agente de usuario, el sistema operativo, y otros detalles disponibles para la solicitud.

##### 9.2.3 STOP FORUM SPAM

[Stop Forum Spam](https://www.stopforumspam.com/) es un fantástico servicio gratuito que puede ayudar a proteger los foros, blogs, y sitios web de los spammers. Lo hace al proporcionar una base de datos de spammers conocidos, y una API que se puede aprovechar para verificar si una dirección IP, nombre de usuario, o dirección de correo electrónico aparece en su base de datos.

CIDRAM proporciona un módulo opcional que aprovecha esta API para verificar si la dirección IP de las solicitudes entrantes pertenece a un sospechoso de spammer. Cuando el módulo está instalado y activado, las direcciones IP del usuario se pueden compartir con el servicio de acuerdo con la configuración y el propósito previsto del módulo.

##### 9.2.4 ABUSEIPDB

CIDRAM proporciona módulos opcionales para bloquear direcciones IP abusivas utilizando la API de [AbuseIPDB](https://www.abuseipdb.com/). Cuando el módulo está instalado y activado, las direcciones IP del usuario se pueden compartir con el servicio de acuerdo con la configuración y el propósito previsto del módulo.

##### 9.2.5 BGPVIEW, IP-API

CIDRAM proporciona un módulo opcional para realizar búsquedas de código de país y ASN utilizando la API de [BGPView](https://bgpview.io/) y la API de [IP-API](https://ip-api.com/). Estas búsquedas proporcionan la capacidad de bloquear o incluir en la lista blanca las solicitudes en función de su ASN o país de origen. Cuando uno de ellos está instalado y activado, las direcciones IP del usuario se pueden compartir con el servicio de acuerdo con la configuración y el propósito previsto del módulo.

##### 9.2.6 PROJECT HONEYPOT

CIDRAM proporciona un módulo opcional para bloquear direcciones IP abusivas utilizando la API de [Project Honeypot](https://www.projecthoneypot.org/). Cuando el módulo está instalado y activado, las direcciones IP del usuario se pueden compartir con el servicio de acuerdo con la configuración y el propósito previsto del módulo.

#### 9.3 REGISTRO DE DATOS

El registro de datos es una parte importante de CIDRAM por varias razones. Puede ser difícil diagnosticar y resolver falsos positivos cuando los eventos de bloqueo que los causan no se registran. Sin registrar eventos de bloques, puede ser difícil determinar con exactitud qué tan eficiente es el CIDRAM en un contexto particular, y puede ser difícil determinar dónde se encuentran sus deficiencias, y qué cambios pueden requerirse en su configuración o firmas en consecuencia, para que continúe funcionando según lo previsto. En todo caso, el registro de datos puede no ser deseable para todos los usuarios, y sigue siendo totalmente opcional. En CIDRAM, el registro de datos está deshabilitado de forma predeterminada. Para habilitarlo, CIDRAM debe configurarse en consecuencia.

Además, si el registro de datos es legalmente permisible, y en la medida en que sea legalmente permisible (por ejemplo, los tipos de información que pueden registrarse, por cuánto tiempo, y en qué circunstancias), puede variar, dependiendo de la jurisdicción y del contexto donde se implemente el CIDRAM (por ejemplo, ya sea que esté operando como individuo, como una entidad corporativa, y sea comercial o no comercial). Por lo tanto, puede serle útil leer atentamente esta sección.

Existen varios tipos de registro que CIDRAM puede realizar. Los diferentes tipos de registro implican diferentes tipos de información, por diferentes razones.

##### 9.3.0 EVENTOS DE BLOQUE

El tipo principal de registro que CIDRAM puede realizar se relaciona con "eventos de bloque". Este tipo de registro se relaciona con cuándo CIDRAM bloquea una solicitud, y se puede proporcionar en tres formatos diferentes:
- Archivos de registro legibles por humanos.
- Archivos de registro de estilo Apache.
- Archivos de registro serializados.

Un evento de bloque, conectado a un archivo de registro legible por humanos, normalmente se ve así (como un ejemplo):

```
ID: 1234
Guion Versión: CIDRAM v1.6.0
Fecha/Hora: Day, dd Mon 20xx hh:ii:ss +0000
Dirección IP: x.x.x.x
Nombre de host: dns.hostname.tld
Firmas Cuentas: 1
Firmas Referencias: x.x.x.x/xx
Razón Bloqueado: Servicio en la nube ("Nombre de red", Lxx:Fx, [XX])!
Agente de Usuario: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
Reconstruida URI: https://your-site.tld/index.php
Estado CAPTCHA: Activado.
```

Ese mismo evento de bloque, conectado a un archivo de registro de estilo Apache, se vería así:

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

Un evento de bloque registrado generalmente incluye la siguiente información:
- Un número de ID que hace referencia al evento de bloque.
- La versión de CIDRAM actualmente en uso.
- La fecha y la hora en que ocurrió el evento de bloqueo.
- La dirección IP de la solicitud bloqueada.
- El nombre de host de la dirección IP de la solicitud bloqueada (cuando esté disponible).
- El número de firmas activadas por la solicitud.
- Referencias a las firmas activadas.
- Las referencias a los motivos del evento de bloque y algunos básicos, relacionados con la información de depuración.
- El agente de usuario de la solicitud bloqueada (cómo se identificó la entidad solicitante a la solicitud).
- Una reconstrucción del identificador para el recurso solicitado originalmente.
- El estado CAPTCHA para la solicitud actual (cuando sea relevante).

*Las directivas de configuración responsables de este tipo de registro y de cada uno de los tres formatos disponibles son:*
- `logging` -> `apache_style_log`
- `logging` -> `serialised_log`
- `logging` -> `standard_log`

Cuando estas directivas se dejan vacías, este tipo de registro permanecerá desactivado.

##### 9.3.1 REGISTROS DE CAPTCHA

Este tipo de registro se relaciona específicamente con instancias CAPTCHA, y ocurre solo cuando un usuario intenta completar una instancia de CAPTCHA.

Una entrada de registros de CAPTCHA contiene la dirección IP del usuario que intenta completar una instancia de CAPTCHA, la fecha y la hora en que se produjo el intento, y el estado CAPTCHA. Una entrada de registros de CAPTCHA generalmente se ve así (como un ejemplo):

```
Dirección IP: x.x.x.x - Fecha/Hora: Day, dd Mon 20xx hh:ii:ss +0000 - Estado CAPTCHA: ¡Éxito!
```

*La directiva de configuración responsable del registros de CAPTCHA es:*
- `captcha` -> `log`

##### 9.3.2 REGISTROS DE FRONT-END

Este tipo de registro relaciona los intentos de inicio de sesión del front-end, y ocurre solo cuando un usuario intenta iniciar sesión en el front-end (suponiendo que el acceso al front-end esté habilitado).

Una entrada de registro en el front-end contiene la dirección IP del usuario que intenta iniciar sesión, la fecha y la hora en que se produjo el intento, y los resultados del intento (inicio de sesión exitoso o fallido). Una entrada de registro del front-end generalmente se ve así (como un ejemplo):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Conectado.
```

*La directiva de configuración responsable del inicio de sesión es:*
- `frontend` -> `frontend_log`

##### 9.3.3 ROTACIÓN DE REGISTROS

Es posible que desee purgar los registros después de un período de tiempo, o posible la ley lo requiera (es decir, la cantidad de tiempo que está legalmente permitido para conservar los registros puede estar limitada por la ley). Puede lograr esto incluyendo marcadores de fecha/hora en los nombres de sus archivos de registro según lo especificado por la configuración de su paquete (por ejemplo, `{yyyy}-{mm}-{dd}.log`), y luego habilitar la rotación de registros (la rotación de registros le permite realizar alguna acción en los archivos de registro cuando se exceden los límites especificados).

Por ejemplo: Si se me exigiera legalmente que borrara los registros después de 30 días, podría especificar `{dd}.log` en los nombres de mis archivos de registro (`{dd}` representa días), establecer el valor de `log_rotation_limit` en 30, y establecer el valor de `log_rotation_action` en `Delete`.

Por el contrario, si está obligado a conservar registros por un período prolongado de tiempo, puede no utilizar la rotación de registros, o puede establecer el valor de `log_rotation_action` en `Archive`, para comprimir archivos de registro, lo que reduce la cantidad total de espacio en disco que ocupan.

*Directivas de configuración relevantes:*
- `logging` -> `log_rotation_action`
- `logging` -> `log_rotation_limit`

##### 9.3.4 TRUNCAMIENTO DE REGISTROS

También es posible truncar archivos de registro individuales cuando exceden un cierto tamaño, si esto es algo que podría necesitar o querer hacer.

*Directivas de configuración relevantes:*
- `logging` -> `truncate`

##### 9.3.5 SEUDONIMIZACIÓN DE DIRECCIONES IP

Primeramente, si no está familiarizado con el término, "seudonimización" se refiere al procesamiento de datos personales como tal que ya no se puede identificar a ningún sujeto de datos específico sin información adicional, y siempre que dicha información adicional se mantenga por separado y esté sujeta a medidas técnicas y organizativas para garantizar que los datos personales no puedan identificarse a ninguna persona física.

Los siguientes recursos pueden ayudar a explicarlo con más detalle:
- [[confilegal.com] La importancia del seudonimización en el nuevo Reglamento de Protección de Datos](https://confilegal.com/20170129-la-importancia-del-seudonimizacion-en-el-nuevo-reglamento-de-proteccion-de-datos/)
- [[forlopd.es] ¿Cómo me protege la seudonimización?](https://www.forlopd.es/web/blog/index.php/seudonimizacion-y-proteccion-de-datos/)
- [[Wikipedia] Seudonimización](https://es.wikipedia.org/wiki/Seudonimizaci%C3%B3n)

En algunas circunstancias, se le puede ser legalmente requerido anonimizar o seudonimizar cualquier PII recopilada, procesada, o almacenada. Aunque este concepto ha existe desde hace bastante tiempo, GDPR/DSGVO menciona especialmente, y específicamente alienta "seudonimización".

CIDRAM es capaz de seudonimizar las direcciones IP cuando las registra, si es algo que podría necesitar o querer hacer. Cuando CIDRAM seudonimizar de direcciones IP, cuando se registra, el octeto final de las direcciones IPv4, y todo lo que ocurre después de la segunda parte de las direcciones IPv6 está representado por una "x" (redondeando efectivamente las direcciones IPv4 a la dirección inicial de la 24 subred en la que tienen en cuenta, y las direcciones IPv6 a la dirección inicial de la 32 subred en la que tienen en cuenta).

*Nota: El proceso de seudonimización de las direcciones IP en CIDRAM no afecta la función de seguimiento de las direcciones IP en CIDRAM. Si esto es un problema para usted, puede ser mejor desactivar por completo el seguimiento de IP.*

*Directivas de configuración relevantes:*
- `legal` -> `pseudonymise_ip_addresses`

##### 9.3.6 OMITIENDO INFORMACIÓN DE REGISTRO

Si desea ir un paso más allá al evitar que se registren por completo los tipos de información específicos, también es posible hacerlo. En la página de configuración, consulte la directiva de configuración `fields` para controlar qué campos aparecen en las entradas de registro y en la página "Acceso Denegado".

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

*Nota: No hay ninguna razón para seudonimizar direcciones IP al omitirlas de los registros por completo.*

*Directivas de configuración relevantes:*
- `general` -> `fields`

##### 9.3.7 ESTADÍSTICA

CIDRAM es opcionalmente capaz de rastrear estadísticas tales como el número total de eventos de bloque o instancias de CAPTCHA que han ocurrido desde algún punto particular en el tiempo. Esta característica está deshabilitada de manera predeterminada, pero se puede habilitar a través de la configuración del paquete. Esta característica solo rastrea el número total de eventos ocurridos, y no incluye ninguna información sobre eventos específicos (y por lo tanto, no debe considerarse como PII).

*Directivas de configuración relevantes:*
- `general` -> `statistics`

##### 9.3.8 ENCRIPTACIÓN

CIDRAM no encripta su caché ni ninguna información de registro. [Encriptación](https://es.wikipedia.org/wiki/Cifrado_(criptograf%C3%ADa)) del caché y del registro se puede introducir en el futuro, pero no hay planes actuales para esto. Si le preocupa que terceros no autorizados accedan a partes de CIDRAM que puedan contener PII o información confidencial, como su caché o registros, recomendaría que CIDRAM no se instale en una ubicación de acceso público (por ejemplo, instale CIDRAM fuera del directorio `public_html` o equivalente disponible para la mayoría de los servidores web estándar) y que los permisos apropiadamente restrictivos se apliquen para el directorio donde reside (en particular, para el directorio vault). Si eso no es suficiente para abordar sus inquietudes, configure CIDRAM de forma que los tipos de información que causen sus inquietudes no se recopilen o registrado en primer lugar (por ejemplo, a modo de deshabilitar el registro).

#### 9.4 COOKIES

CIDRAM establece [cookies](https://es.wikipedia.org/wiki/Cookie_(inform%C3%A1tica)) en dos puntos en su base de código. El primer punto, dependiendo de cómo se haya configurado `lockto`, CIDRAM puede establecer una cookie para recordar cuándo un usuario ha completado un CAPTCHA. El segundo punto, cuando un usuario ha iniciado una sesión en el front-end, CIDRAM establece una cookie para poder recordar al usuario para solicitudes posteriores (es decir, las cookies se usan para autenticar al usuario en una sesión).

En ambos casos, las advertencias de cookies se muestran prominentemente (cuando sea aplicable), advirtiendo al usuario que las cookies se establecerán si participan en las acciones pertinentes. Las cookies no se establecen en ningún otro punto en la base de código.

*Nota: Las API CAPTCHA "invisibles" pueden ser incompatibles con las leyes de cookies en algunas jurisdicciones, y debería ser evitada por cualquier sitio web sujeto a dichas leyes. Optar por utilizar las otras API proporcionadas, o simplemente deshabilitar CAPTCHA por completo, puede ser preferible.*

*Directivas de configuración relevantes:*
- `captcha` -> `lockto`
- `captcha` -> `api`

#### 9.5 MARKETING Y PUBLICIDAD

CIDRAM no recopila ni procesa ninguna información con fines comerciales o publicitarios, y tampoco vende ni obtiene ganancias de ninguna información recopilada o registrada. CIDRAM no es una empresa comercial, ni está relacionada con ningún interés comercial, por lo que hacer estas cosas no tendría ningún sentido. Este ha sido el caso desde el comienzo del proyecto, y sigue siendo el caso hoy en día. Además, hacer estas cosas sería contraproducente para el espíritu y el propósito del proyecto como un todo, y mientras continúe manteniendo el proyecto, nunca sucederá.

#### 9.6 POLÍTICA DE PRIVACIDAD

En algunas circunstancias, se le puede exigir legalmente que muestre claramente un enlace a su política de privacidad en todas las páginas y secciones de su sitio web. Esto puede ser importante como un medio para garantizar que los usuarios estén bien informados sobre sus prácticas de privacidad exactas, los tipos de información personal que recopila y cómo piensa utilizarla. Para poder incluir un enlace en la página "Acceso Denegado" de CIDRAM, se proporciona una directiva de configuración para especificar la URL de su política de privacidad.

*Nota: Se recomienda encarecidamente que su página de política de privacidad no quede detrás de la protección de CIDRAM. Si CIDRAM protege su página de política de privacidad, y un usuario bloqueado por CIDRAM hace clic en el enlace a su política de privacidad, se volverá a bloquear y no podrá ver su política de privacidad. Idealmente, debe enlace a una copia estática de su política de privacidad, como una página HTML, o un archivo de texto sin formato que no esté protegido por CIDRAM.*

*Directivas de configuración relevantes:*
- `legal` -> `privacy_policy`

#### 9.7 GDPR/DSGVO

El Reglamento General de Protección de Datos (GDPR) es un reglamento de la Unión Europea, que entra en vigor el 25 Mayo de 2018. El objetivo principal de la regulación es dar control a los ciudadanos y residentes de la UE con respecto a sus propios datos personales, y unificar la regulación dentro de la UE con respecto a la privacidad y los datos personales.

El reglamento contiene disposiciones específicas relativas al procesamiento de [información de identificación personal](https://es.wikipedia.org/wiki/Informaci%C3%B3n_personal) de cualquier "sujeto de datos" (cualquier persona física identificada o identificable) de la UE o dentro de ella. Para cumplir con la regulación, las "empresas" (según lo definido por la regulación) y cualquier sistema y proceso relevante deben implementar "privacidad por diseño" como estándar, debe usar la configuración de privacidad más alta posible, debe implementar las salvaguardas necesarias para cualquier información almacenada o procesada (incluyendo, pero no limitado a, la implementación de seudonimización o anonimización completa de datos), debe declarar clara e inequívocamente los tipos de datos que recopilan, cómo lo procesan, por qué motivos, por cuánto tiempo lo retienen, y si comparten estos datos con terceros, los tipos de datos compartidos con terceros, cómo, por qué, y así sucesivamente.

Los datos no pueden procesarse a menos que haya una base legal para hacerlo, según lo definido por la regulación. Generalmente, esto significa que para procesar los datos de un sujeto de datos de manera legal, debe hacerse de conformidad con las obligaciones legales, o solo después de que se haya obtenido el consentimiento explícito, bien informado e inequívoco del sujeto de los datos.

Debido a que algunos aspectos de la regulación pueden evolucionar en el tiempo, para evitar la propagación de información desactualizada, puede ser mejor aprender sobre la regulación desde una fuente autorizada, en lugar de simplemente incluir la información relevante aquí en la documentación del paquete (que puede con el tiempo se volverá obsoleto a medida que la regulación evolucione).

[EUR-Lex](https://eur-lex.europa.eu/) (una parte del sitio web oficial de la Unión Europea que proporciona información sobre la legislación de la UE) proporciona amplia información sobre GDPR/DSGVO, disponible en 24 idiomas diferentes (al momento de escribir esto), y disponible para su descarga en formato PDF. Definitivamente recomendaría leer la información que proporcionan, para aprender más sobre GDPR/DSGVO:
- [REGLAMENTO (UE) 2016/679 DEL PARLAMENTO EUROPEO Y DEL CONSEJO](https://eur-lex.europa.eu/legal-content/ES/TXT/?uri=celex:32016R0679)

Alternativamente, hay una breve descripción (no autoritativa) de GDPR/DSGVO disponible en Wikipedia:
- [Reglamento General de Protección de Datos](https://es.wikipedia.org/wiki/Reglamento_General_de_Protecci%C3%B3n_de_Datos)

---


### 10. <a name="SECTION10"></a>ACTUALIZACIÓN DE VERSIONES PRINCIPALES ANTERIORES

#### 10.0 Actualización a CIDRAM v3

Existen diferencias significativas entre v3 y las versiones principales anteriores. Es importante destacar que la forma en que funcionan los puntos de entrada, la forma en que se estructuran los módulos, y la forma en que funciona el actualizador para v3 es diferente a la forma en que funcionaban esas cosas para las versiones principales anteriores. Debido a estas diferencias, la mejor manera de actualizar a v3 desde versiones principales anteriores sería realizar una instalación nueva.

Si desea conservar su configuración y sus reglas auxiliares, antes de comenzar el proceso de actualización, vaya a la página de copia de seguridad del front-end. Desde allí, se pueden exportar las reglas auxiliares y de configuración. La exportación hará que se descargue un archivo. Después de actualizar a la nueva versión principal, ese archivo se puede usar para importar los datos exportados previamente a la instalación.

Debido a los cambios en la forma en que se estructuran los módulos, los módulos destinados a las versiones principales anteriores deberán reescribirse para que funcionen correctamente para v3. La migración directa no funcionará. Lo mismo es cierto para los eventos.

La forma en que se estructuran los archivos de firmas no ha cambiado, por lo que los archivos de firmas destinados a las versiones principales anteriores se pueden migrar directamente a v3 sin que se anticipen problemas.

Los módulos, archivos de firma, y eventos tienen cada uno sus propios directorios dedicados, lo cual es una nueva adición desde v3 (entonces, para v3, cada uno iría a sus respectivos directorios dedicados, en lugar de a la raíz de la vault).

Algunos de los archivos de firma, módulos, y listas de bloqueo disponibles públicamente para versiones principales anteriores han quedado obsoletos, por lo que no todo estará disponible para v3. En la mayoría de los casos, no serán necesarios de todos modos, debido a las nuevas características y funciones principales agregadas desde v3.

Hay algunos cambios sutiles en la forma en que se estructuran las reglas auxiliares, y hay cambios en la configuración, pero si usa la función de importación/exportación en la página de copia de seguridad del front-end, no necesitará volver a escribir, ajustar, o recrear manualmente nada. Al importar, CIDRAM sabe lo que se necesita y lo manejará automáticamente.

Para obtener una lista de los cambios introducidos por la v3 (por ejemplo, características agregadas, características eliminadas, etc), consulte el [registro de cambios de la v3](https://github.com/CIDRAM/CIDRAM/blob/v3/Changelog.md#v300).

#### 10.1 Actualización a CIDRAM v4 desde una versión anterior a CIDRAM v3

Consulte lo anterior: Se recomienda una nueva instalación.

#### 10.2 Actualización a CIDRAM v4 desde CIDRAM v3

1. En primer lugar, vaya a la página de actualizaciones del front-end y, si hay actualizaciones disponibles, asegúrese de instalarlas todas. Esto garantiza que cualquier código escrito más recientemente que pueda ser necesario para actualizar versiones principales correctamente estará disponible para el actualizador, y también ayuda a reducir la cantidad de trabajo que el actualizador necesitará hacer cuando actualice versiones principales más adelante.

2. Vaya a la página de configuración del front-end y busque __`frontend➡remotes`__. En la lista, donde veas `/v3/`, cámbiala a `/v4/`. Haga clic en actualizar para guardar su configuración. Este cambio le indica al actualizador que seleccione la versión principal deseada cuando busque actualizaciones.

3. Vaya a la página de copia de seguridad del front-end. Seleccione exportar, marque las casillas de verificación para configuración, para estadísticas, y para reglas auxiliares, y luego presione OK para descargar una copia de seguridad. Se han realizado algunos cambios. Por ejemplo, se ha eliminado la acción "no registrar" de las reglas auxiliares (se puede usar la opción "suprimir registro" para lograr lo mismo). Necesitará importar esta copia de seguridad nuevamente a CIDRAM después de la actualización.

4. Vaya a la página de actualizaciones del front-end. Ahora deberían aparecer las actualizaciones para la nueva versión principal. Para evitar tiempos de espera, antes de actualizar todo, primero intente actualizar solo el core CIDRAM o el front-end CIDRAM (ya que ambos son dependencias mutuas entre sí, actualizar uno debería actualizar ambos automáticamente de todos modos). Como la estructura de la página y el estilo CSS para el front-end han cambiado significativamente entre las versiones principales, inicialmente puede parecer roto después de la actualización; no es así. Vaya a cualquier otra página front-end y presione Ctrl+F5 para intentar realizar una actualización completa (es decir, una actualización mediante la cual el navegador obtiene una copia nueva del estilo CSS y otros periféricos en lugar de confiar en su caché). La estructura de la página y el estilo CSS deberían entonces aparecer correctamente. Si no es así, intenta borrar el caché de tu navegador.

5. Ahora que se han actualizado el core y el front-end, y la estructura de la página y el estilo CSS aparecen correctamente, puedes actualizar todo lo demás. Vaya a la página de actualizaciones del front-end y, si ve el botón en la parte superior de la página, haga clic en actualizar todo.

6. Para garantizar que no haya ninguna actualización incorrecta persistente, ya sea pasada o presente, ni ningún archivo dañado en la instalación, y para garantizar que todo esté como debería estar, haga clic en reparar todo. Muy raramente debería convertirse en un problema real, pero es mejor ir a lo seguro.

7. Vaya a la página de copia de seguridad del front-end. Seleccione importar, marque las casillas de verificación para configuración, para estadísticas, y para reglas auxiliares, haga clic en el botón para seleccionar un archivo, localice y seleccione la copia de seguridad que descargó anteriormente, y presione OK para importar esa copia de seguridad. CIDRAM realizará automáticamente cualquier ajuste necesario para adaptarse a los cambios.

8. Ahora que ha actualizado con éxito las versiones principales, es posible que desee explorar brevemente la página de configuración del front-end debido a los cambios introducidos por la nueva versión principal (por ejemplo, para las características recientemente introducidas). Dejando esto de lado, ya has completado la actualización. La nueva versión principal no introduce ningún cambio en los archivos de firma, módulos, o eventos, por lo que no necesita preocuparse por eso al actualizar.

Para obtener una lista de los cambios introducidos por la v4 (por ejemplo, características agregadas, características eliminadas, etc), consulte el [registro de cambios de la v4](https://github.com/CIDRAM/CIDRAM/blob/v4/Changelog.md#v400).

---


Última Actualización: 1 de Abril de 2026 (2026.04.01).
