## Documentación para CIDRAM v3 (Español).

### Contenidos
- 1. [PREÁMBULO](#SECTION1)
- 2. [CÓMO INSTALAR](#SECTION2)
- 3. [CÓMO USAR](#SECTION3)
- 4. [GESTIÓN DEL FRONT-END](#SECTION4)
- 5. [ARCHIVOS INCLUIDOS EN ESTE PAQUETE](#SECTION5)
- 6. [OPCIONES DE CONFIGURACIÓN](#SECTION6)
- 7. [FORMATO DE FIRMAS](#SECTION7)
- 8. [CONOCIDOS PROBLEMAS DE COMPATIBILIDAD](#SECTION8)
- 9. [PREGUNTAS MÁS FRECUENTES (FAQ)](#SECTION9)
- 10. *Reservado para adiciones futuras a la documentación.*
- 11. [INFORMACIÓN LEGAL](#SECTION11)

*Nota relativa a las traducciones: En caso de errores (por ejemplo, discrepancias entre traducciones, errores tipográficos, etc), la versión en Inglés del README se considera la versión original y autorizada. Si encuentra algún error, su ayuda para corregirlo sera bienvenida.*

---


### 1. <a name="SECTION1"></a>PREÁMBULO

CIDRAM (Classless Inter-Domain Routing Access Manager) es un script PHP diseñado para proteger sitios web bloqueando solicitudes desde direcciones IP consideradas como fuentes de tráfico no deseado, incluyendo (pero no limitado a) tráfico desde puntos de acceso inhumanos, servicios en la nube, spambots, scrapers, etc. Esto se hace calculando las posibles CIDRs de las direcciones IP suministradas desde solicitudes entrantes e intentando hacer coincidir estos posibles CIDRs en contra de sus archivos de firmas (estos archivos de firmas contienen listas de CIDRs de direcciones IP consideradas como fuentes de tráfico no deseado); Si se encuentran coincidencias, las solicitudes son bloqueadas.

*(Ver: [¿Qué es un "CIDR"?](#WHAT_IS_A_CIDR)).*

[CIDRAM](https://cidram.github.io/) COPYRIGHT 2016 y más allá GNU/GPLv2 por [Caleb M (Maikuolan)](https://github.com/Maikuolan).

Este script es un software gratuito; puede redistribuirlo y/o modificarlo según los términos de la GNU General Public License, publicada por la Free Software Foundation; tanto la versión 2 de la licencia como cualquier versión posterior. Este script es distribuido con la esperanza de que será útil, pero SIN NINGUNA GARANTÍA; también, sin ninguna implícita garantía de COMERCIALIZACIÓN o IDONEIDAD PARA UN PARTICULAR PROPÓSITO. Vea la GNU General Public License para más detalles, ubicada en el `LICENSE.txt` archivo también disponible en:
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

Este documento y su paquete asociado puede ser descargado de forma gratuita desde:
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [SourceForge](https://sourceforge.net/projects/cidram/).

---


### 2. <a name="SECTION2"></a>CÓMO INSTALAR

#### 2.0 INSTALACIÓN MANUAL

1) Dado el hecho que estas leiendo esto, asumo que ya ha descargado y guardado una copia del script, descomprimido sus contenidos, teniendolo en algún lugar en su ordenador. Ahora, usted querrá averiguar en que parte del host o CMS desea colocar estos contenidos. Un directorio como `/public_html/cidram/` o similar (aunque, no importa el que usted elija, siempre y cuando sea algo seguro y con lo que estas satisfecho) será suficiente. *Antes de empezar a subir archivos, continue leyendo...*

2) Cambiar el nombre del archivo `config.ini.RenameMe` a `config.ini` (situado en el interior del `vault`), y opcionalmente (muy recomendable para usuarios avanzados, pero no recomendado para los usuarios principiantes o inexpertos), abre el archivo (este archivo contiene todas las directrizes disponibles para CIDRAM; encima de cada opción debe haber un breve comentario que describe lo que hace y para lo qué sirve). Ajuste estas opciones según sus necesidades, según lo que sea apropiado para su particular configuración. Guardar archivo, cerrar.

3) Subir los contenidos (CIDRAM y sus archivos) al directorio que habías decidido previamente (no necessitas incluir los archivos `*.txt`/`*.md`, pero deberias subir el resto).

4) CHMOD al `vault` directorio "755" (si tienes problemas, puede intentar "777"; aunque es menos seguro). El principal directorio de almacenamiento de los contenidos (el que escogio antes), en general, puede dejarlo solo, pero el estado del CHMOD deberia estar revisado si ha tenido problemas de permisos en su sistema en el pasado (predefinido, debería ser algo como "755"). En breve: Para que el paquete pueda funcionar correctamente, PHP necesita poder leer y escribir archivos dentro del directorio `vault`. Muchas cosas (actualización, registro, etc) no serán posibles si PHP no puede escribir en el directorio `vault`, y el paquete no funcionará en absoluto si PHP no puede leer desde el directorio `vault`. Pero, para una seguridad óptima, el directorio `vault` NO debe ser accesible públicamente (información sensible, como la información contenida por `config.ini` o `frontend.dat`, podría estar expuesta a atacantes potenciales si el directorio `vault` es públicamente accesible).

5) Luego, tendrás que "enganchar" CIDRAM a tu sistema o CMS. Hay varias maneras en que usted puede "enganchar" scripts como CIDRAM a su sistema o CMS, pero el más fácil es simplemente incluir el script al principio de un archivo central de su sistema o CMS (uno que en general siempre sea cargado cuando alguien accede a cualquier página a través de su web) utilizando un `require` o `include` declaración. Por lo general, esto sera algo almacenado en un directorio como `/includes`, `/assets` o `/functions`, y será menudo llamado algo así como `init.php`, `common_functions.php`, `functions.php` o similar. Vas a tener que averiguar qué archivo es por su situación; Si encuentra dificultades para resolver esto, visite la página de issues CIDRAM en GitHub. Para ello [utilizar `require` o `include`], inserte la siguiente línea de código al principio de ese núcleo archivo, reemplazando la cuerda contenida dentro de las comillas con la exacta dirección del `loader.php` archivo (dirección local, no la dirección HTTP; será similar a la dirreción `vault` mencionada anteriormente).

`<?php require '/user_name/public_html/cidram/loader.php'; ?>`

Guardar archivo, cerrarlo, subir otra vez.

-- O ALTERNATIVAMENTE --

Si está utilizando un servidor Apache y si usted tiene acceso a `php.ini`, puede utilizar la `auto_prepend_file` dirección para anteponer CIDRAM cuando cualquier solicitud PHP sea realizada. Algo como:

`auto_prepend_file = "/user_name/public_html/cidram/loader.php"`

O esto en el archivo `.htaccess`:

`php_value auto_prepend_file "/user_name/public_html/cidram/loader.php"`

6) ¡Eso es todo! :-)

#### 2.1 INSTALACIÓN CON COMPOSER

[CIDRAM está registrado con Packagist](https://packagist.org/packages/cidram/cidram), y por lo tanto, si está familiarizado con Composer, puede utilizar Composer para instalar CIDRAM (sin embargo, usted todavía necesitará preparar la configuración, los permisos y los ganchos; consulte "INSTALACIÓN MANUAL" pasos 2, 4, y 5).

`composer require cidram/cidram`

#### 2.2 INSTALACIÓN PARA WORDPRESS

Si desea utilizar CIDRAM con WordPress, puede ignorar todas las instrucciones anteriores. [CIDRAM está registrado como un plugin con la base de datos de plugins de WordPress](https://wordpress.org/plugins/cidram/), y puede instalar CIDRAM directamente desde el panel de plugins. Puede instalarlo de la misma manera que cualquier otro plugin, y no se requieren pasos adicionales. Al igual que con los otros métodos de instalación, puede personalizar su instalación modificando el contenido del archivo `config.ini` o utilizando la interfaz de usuario en la página de configuración. Si habilita la interfaz de CIDRAM y actualiza CIDRAM usando la página de actualizacione de la interfaz, esto se sincronizará automáticamente con la información de la versión plugin mostrada en el panel de plugins.

*¡Advertencia: Actualizar CIDRAM a través del panel de plugins da como resultado una instalación limpia! Si ha personalizado su instalación (cambiado su configuración, módulos instalados, etc), estas personalizaciones se perderán al actualizar a través del panel de plugins! Los archivos de registro también se perderán al actualizar a través del panel de plugins! Para conservar los archivos de registro y las personalizaciones, actualice a través de la página de actualizaciones del front-end de CIDRAM.*

---


### 3. <a name="SECTION3"></a>CÓMO USAR

CIDRAM debe bloquear automáticamente las solicitudes indeseables a su website sin requiriendo intervención manual, aparte de sus instalación inicial.

Puede personalizar su configuración y personalizar cuál de los CIDRs son bloqueados por modificando su archivo de configuración y/o su archivos de firmas.

Si tiene algún falsos positivos, por favor contacto conmigo para decirme. *(Ver: [¿Qué es un "falso positivo"?](#WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM se puede actualizar manualmente o a través del front-end. CIDRAM también se puede actualizar a través de Composer o WordPress, si se instaló originalmente por esos medios.

---


### 4. <a name="SECTION4"></a>GESTIÓN DEL FRONT-END

#### 4.0 CUÁL ES EL FRONT-END.

El front-end proporciona una manera cómoda y fácil de mantener, administrar y actualizar la instalación de CIDRAM. Puede ver, compartir y descargar archivos de registro a través de la página de registros, puede modificar la configuración a través de la página de configuración, puede instalar y desinstalar componentes a través de la página de actualizaciones, y puede cargar, descargar y modificar archivos en su vault a través del administración de archivos.

El front-end está desactivado de forma predeterminada para evitar el acceso no autorizado (el acceso no autorizado podría tener consecuencias significativas para su sitio web y su seguridad). Las instrucciones para habilitarlo se incluyen debajo de este párrafo.

#### 4.1 CÓMO HABILITAR EL FRONT-END.

1) Localizar la directiva `disable_frontend` dentro `config.ini`, y establézcalo en `false` (será predefinido como `true`).

2) Accesar `loader.php` desde tu navegador (p.ej., `http://localhost/cidram/loader.php`).

3) Inicie sesión con el nombre del usuario y la contraseña predeterminados (admin/password).

Nota: Después de iniciar la sesión por primera vez, con el fin de impedir el acceso no autorizado al front-end, usted debe cambiar inmediatamente su nombre de usuario y su contraseña! Esto es muy importante, ya que es posible subir código arbitrario de PHP a su sitio web a través del front-end.

Además, para una seguridad óptima, se recomienda encarecidamente habilitar la "autenticación de dos factores" para todas las cuentas del front-end (se proporcionan instrucciones a continuación).

#### 4.2 CÓMO UTILIZAR EL FRONT-END.

Las instrucciones se proporcionan en cada página del front-end, para explicar la manera correcta de usarlo y su propósito. Si necesita más explicaciones o cualquier ayuda especial, póngase en contacto con el soporte. Alternativamente, hay algunos videos disponibles en YouTube que podrían ayudar a modo de demostración.

#### 4.3 AUTENTICACIÓN DE DOS FACTORES

Es posible hacer que el front-end sea más seguro habilitando la autenticación de dos factores ("2FA"). Cuando se inicia una sesión usando una cuenta habilitada para 2FA, se envía un correo electrónico a la dirección de correo electrónico asociada con esa cuenta. Este correo electrónico contiene un "código 2FA", que el usuario debe ingresar, además del nombre de usuario y la contraseña, para poder iniciar sesión con esa cuenta. Esto significa que la obtención de una contraseña de cuenta no sería suficiente para que cualquier hacker o posible atacante pueda iniciar sesión en esa cuenta, ya que también necesitarían tener acceso a la dirección de correo electrónico asociada con esa cuenta para poder recibir y utilizar el código 2FA asociado a la sesión, por lo tanto haciendo el front-end más seguro.

En primer lugar, para habilitar la autenticación de dos factores, utilizando la página de actualizaciones del front-end, instale el componente PHPMailer. CIDRAM utiliza PHPMailer para enviar correos electrónicos. Cabe señalar que aunque CIDRAM, por sí mismo, es compatible con PHP >= 5.4.0, PHPMailer requiere PHP >= 5.5.0, lo que significa que no será posible habilitar la autenticación de dos factores para el front-end CIDRAM para usuarios de PHP 5.4.

Después de instalar PHPMailer, deberá llenar las directivas de configuración de PHPMailer a través de la página de configuración de CIDRAM o el archivo de configuración. Se incluye más información sobre estas directivas de configuración en la sección de configuración de este documento. Después de haber llenado las directivas de configuración de PHPMailer, configure `enable_two_factor` a `true`. La autenticación de dos factores ahora debería estar habilitada.

A continuación, deberá asociar una dirección de correo electrónico con una cuenta, para que CIDRAM sepa a dónde enviar códigos 2FA cuando inicie sesión con esa cuenta. Para hacer esto, use la dirección de correo electrónico como el nombre de usuario de la cuenta (como `foo@bar.tld`), o incluya la dirección de correo electrónico como parte del nombre de usuario de la misma manera que lo haría al enviar un correo electrónico normalmente (como `Foo Bar <foo@bar.tld>`).

Nota: Proteger su vault contra el acceso no autorizado (p.ej., a modo de endureciendo la seguridad de su servidor y los permisos de acceso público), es particularmente importante aquí, debido a ese acceso no autorizado a su archivo de configuración (que se almacena en su vault), podría exponer la configuración de SMTP saliente (incluido el nombre de usuario y la contraseña de SMTP). Debe asegurarse de que su vault esté correctamente asegurada antes de habilitar la autenticación de dos factores. Si no puede hacer esto, al menos, debe crear una nueva cuenta de correo electrónico, dedicada a tal fin, para reducir los riesgos asociados con la configuración SMTP expuesta.

---


### 5. <a name="SECTION5"></a>ARCHIVOS INCLUIDOS EN ESTE PAQUETE

```
https://github.com/CIDRAM/CIDRAM>v2
│   .gitattributes
│   .gitignore
│   Changelog.txt
│   composer.json
│   LICENSE.txt
│   loader.php
│   README.md
│   tests.php
├───.docker
│       docker-compose.yml
├───.github
│   │   FUNDING.yml
│   │
│   └───workflows
│           php-cs-fixer.yml
│           v2.yml
└───vault
    │   bypasses.php
    │   bypasses.yml
    │   captcha_default.html
    │   channels.yaml
    │   cidramblocklists.dat
    │   components.dat
    │   config.ini.RenameMe
    │   config.php
    │   config.yaml
    │   event_handlers.php
    │   frontend.php
    │   frontend_functions.php
    │   functions.php
    │   ignore.dat
    │   ipv4.dat
    │   ipv4_bogons.dat
    │   ipv4_custom.dat.RenameMe
    │   ipv4_isps.dat
    │   ipv4_nonblocking.dat
    │   ipv4_other.dat
    │   ipv6.dat
    │   ipv6_bogons.dat
    │   ipv6_custom.dat.RenameMe
    │   ipv6_isps.dat
    │   ipv6_nonblocking.dat
    │   ipv6_other.dat
    │   lang.php
    │   modules.dat
    │   outgen.php
    │   template_custom.html
    │   template_default.html
    │   themes.dat
    │   verification.yaml
    ├───classes
    │   │   Aggregator.php
    │   │   Captcha.php
    │   │   Constants.php
    │   │   HCaptcha.php
    │   │   ReCaptcha.php
    │   │   Reporter.php
    │   │
    │   └───Maikuolan
    │           Cache.php
    │           ComplexStringHandler.php
    │           DelayedIO.php
    │           Demojibakefier.php
    │           Events.php
    │           IPHeader.php
    │           L10N.php
    │           Matrix.php
    │           NumberFormatter.php
    │           Operation.php
    │           Request.php
    │           YAML.php
    ├───fe_assets
    │       auxiliary.js
    │       frontend.css
    │       frontend.html
    │       icons.php
    │       lock_bl_c.png
    │       lock_bl_o.png
    │       lock_rd_c.png
    │       lock_rd_o.png
    │       lock_wt_c.png
    │       lock_wt_o.png
    │       pips.php
    │       scripts.js
    │       _2fa.html
    │       _accounts.html
    │       _accounts_row.html
    │       _aux.html
    │       _aux_edit.html
    │       _cache.html
    │       _cidr_calc.html
    │       _cidr_calc_row.html
    │       _config.html
    │       _config_row.html
    │       _files.html
    │       _files_edit.html
    │       _files_rename.html
    │       _files_row.html
    │       _fixer.html
    │       _home.html
    │       _ip_aggregator.html
    │       _ip_test.html
    │       _ip_test_row.html
    │       _ip_tracking.html
    │       _ip_tracking_row.html
    │       _login.html
    │       _logs.html
    │       _nav_complete_access.html
    │       _nav_logs_access_only.html
    │       _range.html
    │       _range_intersector.html
    │       _range_row.html
    │       _range_subtractor.html
    │       _sections.html
    │       _statistics.html
    │       _updates.html
    │       _updates_row.html
    └───lang
            lang.ar.fe.yaml
            lang.ar.yaml
            lang.bn.fe.yaml
            lang.bn.yaml
            lang.de.fe.yaml
            lang.de.yaml
            lang.en.fe.yaml
            lang.en.yaml
            lang.es.fe.yaml
            lang.es.yaml
            lang.fr.fe.yaml
            lang.fr.yaml
            lang.hi.fe.yaml
            lang.hi.yaml
            lang.id.fe.yaml
            lang.id.yaml
            lang.it.fe.yaml
            lang.it.yaml
            lang.ja.fe.yaml
            lang.ja.yaml
            lang.ko.fe.yaml
            lang.ko.yaml
            lang.lv.fe.yaml
            lang.lv.yaml
            lang.nl.fe.yaml
            lang.nl.yaml
            lang.no.fe.yaml
            lang.no.yaml
            lang.pl.fe.yaml
            lang.pl.yaml
            lang.pt.fe.yaml
            lang.pt.yaml
            lang.ru.fe.yaml
            lang.ru.yaml
            lang.sv.fe.yaml
            lang.sv.yaml
            lang.ta.fe.yaml
            lang.ta.yaml
            lang.th.fe.yaml
            lang.th.yaml
            lang.tr.fe.yaml
            lang.tr.yaml
            lang.ur.fe.yaml
            lang.ur.yaml
            lang.vi.fe.yaml
            lang.vi.yaml
            lang.zh-tw.fe.yaml
            lang.zh-tw.yaml
            lang.zh.fe.yaml
            lang.zh.yaml
```

---


### 6. <a name="SECTION6"></a>OPCIONES DE CONFIGURACIÓN

La siguiente es una lista de variables encuentran en la `config.ini` configuración archivo de CIDRAM, junto con una descripción de sus propósito y función.

```
Configuración (v3)
│
├───general
│       logfile [string]
│       logfile_apache [string]
│       logfile_serialized [string]
│       error_log [string]
│       stages [string]
│       fields [string]
│       truncate [string]
│       log_rotation_limit [int]
│       log_rotation_action [string]
│       timezone [string]
│       time_offset [int]
│       time_format [string]
│       ipaddr [string]
│       http_response_header_code [int]
│       silent_mode [string]
│       lang [string]
│       lang_override [bool]
│       numbers [string]
│       emailaddr [string]
│       emailaddr_display_style [string]
│       disable_frontend [bool]
│       max_login_attempts [int]
│       frontend_log [string]
│       signatures_update_event_log [string]
│       ban_override [int]
│       log_banned_ips [bool]
│       default_dns [string]
│       search_engine_verification [string]
│       social_media_verification [string]
│       other_verification [string]
│       protect_frontend [bool]
│       default_algo [string]
│       statistics [string]
│       force_hostname_lookup [bool]
│       allow_gethostbyaddr_lookup [bool]
│       log_sanitisation [bool]
│       disabled_channels [string]
│       default_timeout [int]
│       config_imports [string]
│       events [string]
├───signatures
│       ipv4 [string]
│       ipv6 [string]
│       block_attacks [bool]
│       block_cloud [bool]
│       block_bogons [bool]
│       block_generic [bool]
│       block_legal [bool]
│       block_malware [bool]
│       block_proxies [bool]
│       block_spam [bool]
│       modules [string]
│       default_tracktime [int]
│       infraction_limit [int]
│       tracking_override [bool]
├───recaptcha
│       usemode [int]
│       lockip [bool]
│       lockuser [bool]
│       sitekey [string]
│       secret [string]
│       expiry [float]
│       logfile [string]
│       signature_limit [int]
│       api [string]
│       show_cookie_warning [bool]
│       show_api_message [bool]
│       nonblocked_status_code [int]
├───hcaptcha
│       usemode [int]
│       lockip [bool]
│       lockuser [bool]
│       sitekey [string]
│       secret [string]
│       expiry [float]
│       logfile [string]
│       signature_limit [int]
│       api [string]
│       show_cookie_warning [bool]
│       show_api_message [bool]
│       nonblocked_status_code [int]
├───legal
│       pseudonymise_ip_addresses [bool]
│       privacy_policy [string]
├───template_data
│       theme [string]
│       magnification [float]
│       css_url [string]
│       block_event_title [string]
│       captcha_title [string]
├───PHPMailer
│       event_log [string]
│       skip_auth_process [bool]
│       enable_two_factor [bool]
│       host [string]
│       port [int]
│       smtp_secure [string]
│       smtp_auth [bool]
│       username [string]
│       password [string]
│       set_from_address [string]
│       set_from_name [string]
│       add_reply_to_address [string]
│       add_reply_to_name [string]
├───rate_limiting
│       max_bandwidth [string]
│       max_requests [int]
│       precision_ipv4 [int]
│       precision_ipv6 [int]
│       allowance_period [float]
│       exceptions [string]
└───supplementary_cache_options
        prefix [string]
        enable_apcu [bool]
        enable_memcached [bool]
        enable_redis [bool]
        enable_pdo [bool]
        memcached_host [string]
        memcached_port [int]
        redis_host [string]
        redis_port [int]
        redis_timeout [float]
        pdo_dsn [string]
        pdo_username [string]
        pdo_password [string]
```

#### "general" (Categoría)
Configuración general (cualquier configuración que no pertenezca a otras categorías).

##### "logfile" `[string]`
- Un archivo legible por humanos para el registro de todos los intentos de acceso bloqueados. Especificar el nombre del archivo, o dejar en blanco para desactivar.

##### "logfile_apache" `[string]`
- Un archivo en el estilo de Apache para el registro de todos los intentos de acceso bloqueados. Especificar el nombre del archivo, o dejar en blanco para desactivar.

##### "logfile_serialized" `[string]`
- Un archivo serializado para el registro de todos los intentos de acceso bloqueados. Especificar el nombre del archivo, o dejar en blanco para desactivar.

##### "error_log" `[string]`
- Un archivo para registrar cualquier error detectado que no sea fatal. Especificar el nombre del archivo, o dejar en blanco para desactivar.

##### "stages" `[string]`
- Controles para las etapas de la cadena de ejecución (si está habilitado, si se registran errores, etc).

```
stages
├─Tests ("stage_tests")
├─Modules ("stage_modules")
├─SearchEngineVerification ("stage_sev")
├─SocialMediaVerification ("stage_smv")
├─OtherVerification ("stage_ov")
├─Aux ("stage_aux")
├─Reporting ("stage_reporting")
├─Tracking ("stage_tracking")
├─RL ("stage_rl")
├─CAPTCHA ("stage_captcha")
├─Statistics ("stage_statistics")
├─Webhooks ("stage_webhooks")
├─PrepareFields ("stage_preparefields")
├─Output ("stage_output")
├─WriteLogs ("stage_writelogs")
├─Terminate ("stage_terminate")
├─AuxRedirect ("stage_auxredirect")
└─NonBlockedCAPTCHA ("stage_nonblockedcaptcha")
```

##### "fields" `[string]`
- Controles para los campos durante eventos de bloque (cuando se bloquea una solicitud).

```
fields
├─ID ("field_id")
├─ScriptIdent ("field_scriptversion")
├─DateTime ("field_datetime")
├─IPAddr ("field_ipaddr")
├─IPAddrResolved ("field_ipaddr_resolved")
├─Query ("field_query")
├─Referrer ("field_referrer")
├─UA ("field_ua")
├─UALC ("field_ualc")
├─SignatureCount ("field_sigcount")
├─Signatures ("field_sigref")
├─WhyReason ("field_whyreason")
├─ReasonMessage ("field_reasonmessage")
├─rURI ("field_rURI")
├─Infractions ("field_infractions")
├─ASNLookup ("field_asnlookup")
├─CCLookup ("field_cclookup")
├─Verified ("field_verified")
├─Expired ("state_expired")
├─Ignored ("state_ignored")
├─Request_Method ("field_request_method")
├─Hostname ("field_hostname")
└─CAPTCHA ("field_captcha")
```

##### "truncate" `[string]`
- ¿Truncar archivos de registro cuando alcanzan cierto tamaño? Valor es el tamaño máximo en B/KB/MB/GB/TB que un archivo de registro puede crecer antes de ser truncado. El valor predeterminado de 0KB deshabilita el truncamiento (archivos de registro pueden crecer indefinidamente). Nota: ¡Se aplica a archivos de registro individuales! El tamaño de los archivos de registro no se considera colectivamente.

##### "log_rotation_limit" `[int]`
- La rotación de registros limita la cantidad de archivos de registro que deberían existir al mismo tiempo. Cuando se crean nuevos archivos de registro, si la cantidad total de archivos de registro excede el límite especificado, se realizará la acción especificada. Puede especificar el límite deseado aquí. Un valor de 0 deshabilitará la rotación de registros.

##### "log_rotation_action" `[string]`
- La rotación de registros limita la cantidad de archivos de registro que deberían existir al mismo tiempo. Cuando se crean nuevos archivos de registro, si la cantidad total de archivos de registro excede el límite especificado, se realizará la acción especificada. Puede especificar la acción deseada aquí. Delete = Eliminar los archivos de registro más antiguos, hasta que el límite ya no se exceda. Archive = Primero archiva, y luego eliminar los archivos de registro más antiguos, hasta que el límite ya no se exceda.

```
log_rotation_action
├─Delete ("Delete")
└─Archive ("Archive")
```

##### "timezone" `[string]`
- Esto se usa para especificar la zona horaria a usar (por ejemplo, Africa/Cairo, America/New_York, Asia/Tokyo, Australia/Perth, Europe/Berlin, Pacific/Guam, etc). Especifique "SYSTEM" para permitir que PHP maneje esto automáticamente.

```
timezone
├─SYSTEM ("Usar la zona horaria predeterminada del sistema.")
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

##### "ipaddr" `[string]`
- ¿Dónde puedo encontrar el IP dirección de las solicitudes entrantes? (Útil para servicios como Cloudflare y tales). Predefinido = REMOTE_ADDR. ¡AVISO: No cambie esto a menos que sepas lo que estás haciendo!

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
- [Forwarded - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### "http_response_header_code" `[int]`
- ¿Cuál mensaje de estado HTTP debe enviar CIDRAM cuando se bloquean las solicitudes? (Consulte la documentación para más información).

```
http_response_header_code
├─200 (200 OK)
├─403 (403 Forbidden)
├─410 (410 Gone)
├─418 (418 I'm a teapot)
├─451 (451 Unavailable For Legal Reasons)
└─503 (503 Service Unavailable)
```

##### "silent_mode" `[string]`
- Debería CIDRAM silencio redirigir los intentos de acceso bloqueados en lugar de mostrar la página "Acceso Denegado"? En caso afirmativo, especifique la ubicación para redirigir los intentos de acceso bloqueados. Si no, dejar esta variable en blanco.

##### "lang" `[string]`
- Especifique la predefinido del lenguaje para CIDRAM.

```
lang
├─en ("English")
├─ar ("العربية")
├─bn ("বাংলা")
├─de ("Deutsch")
├─es ("Español")
├─fr ("Français")
├─hi ("हिंदी")
├─id ("Bahasa Indonesia")
├─it ("Italiano")
├─ja ("日本語")
├─ko ("한국어")
├─lv ("Latviešu")
├─nl ("Nederlandse")
├─no ("Norsk")
├─pl ("Polski")
├─pt ("Português")
├─ru ("Русский")
├─sv ("Svenska")
├─ta ("தமிழ்")
├─th ("ภาษาไทย")
├─tr ("Türkçe")
├─ur ("اردو")
├─vi ("Tiếng Việt")
├─zh ("中文（简体）")
└─zh-tw ("中文（傳統）")
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
├─Armenian ("Ռ̅Մ̅Լ̅ՏՇԿԷ")
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
├─default ("field_clickable_link")
└─noclick ("field_nonclickable_text")
```

##### "disable_frontend" `[bool]`
- ¿Desactivar el acceso front-end? El acceso front-end puede hacer CIDRAM más manejable, pero también puede ser un riesgo de seguridad. Se recomienda administrar CIDRAM a través del back-end cuando sea posible, pero el acceso front-end se proporciona para cuando no es posible. Mantenerlo desactivado a menos que lo necesite. False = Activar el acceso front-end; True = Desactivar el acceso front-end [Predefinido].

##### "max_login_attempts" `[int]`
- Número máximo de intentos de login al front-end. Predefinido = 5.

##### "frontend_log" `[string]`
- Archivo para registrar intentos de login al front-end. Especificar el nombre del archivo, o dejar en blanco para desactivar.

##### "signatures_update_event_log" `[string]`
- Un archivo para registrar cuando las firmas se actualizan a través del front-end. Especificar el nombre del archivo, o dejar en blanco para desactivar.

##### "ban_override" `[int]`
- Anular "http_response_header_code" cuando "infraction_limit" es excedido? Cuando se anula: Las solicitudes bloqueadas devuelven una página en blanco (los archivos templates no se utilizan). 200 = No anular [Predefinido]. Otros valores son los mismos que los valores disponibles para "http_response_header_code".

```
ban_override
├─200 (200 OK)
├─403 (403 Forbidden)
├─410 (410 Gone)
├─418 (418 I'm a teapot)
├─451 (451 Unavailable For Legal Reasons)
└─503 (503 Service Unavailable)
```

##### "log_banned_ips" `[bool]`
- ¿Incluir las solicitudes bloqueadas de IPs prohibidos en los archivos de registro? True = Sí [Predefinido]; False = No.

##### "default_dns" `[string]`
- Una lista delimitada por comas de los servidores DNS que se utilizarán para las búsquedas de nombres del host. Predefinido = "8.8.8.8,8.8.4.4" (Google DNS). ¡AVISO: No cambie esto a menos que sepas lo que estás haciendo!

##### "search_engine_verification" `[string]`
- Controles para verificar las solicitudes de los motores de búsqueda.

```
search_engine_verification
├─Applebot ("Applebot")
├─Baidu ("Baiduspider/百度")
├─Bingbot ("Bingbot")
├─DuckDuckBot ("DuckDuckBot")
├─Googlebot ("Googlebot")
├─MojeekBot ("MojeekBot")
├─PetalBot ("PetalBot")
├─Qwantify ("Qwantify/Bleriot")
├─SeznamBot ("SeznamBot")
├─Sogou ("Sogou/搜狗")
├─Yahoo ("Yahoo/Slurp")
├─Yandex ("Yandex/Яндекс")
└─YoudaoBot ("YoudaoBot")
```

__¿Qué son "positivos" y "negativos"?__ Cuando verificando la identidad presentada por una solicitud, un resultado exitoso podría describirse como "positivo" o "negativo". Cuando se confirma que la identidad presentada es la verdadera identidad, se describiría como "positiva". Cuando se confirma que la identidad presentada es falsa, se describirá como "negativa". Sin embargo, un resultado fallido (por ejemplo, la verificación falló, o no se puede determinar la veracidad de la identidad presentada) no se describiría como "positivo" o "negativo". En cambio, un resultado fallido se describiría simplemente como no verificado. Cuando no se intenta verificar la identidad presentada por una solicitud, la solicitud también se describiría como no verificado. Los términos tienen sentido solo en el contexto en el que se reconoce la identidad presentada por una solicitud y, por lo tanto, donde la verificación es posible. En los casos en que la identidad presentada no coincida con las opciones proporcionadas anteriormente, o cuando no se presente ninguna identidad, las opciones proporcionadas anteriormente se vuelven irrelevantes.

__¿Qué son los "bypasses de un solo golpe"?__ En algunos casos, una solicitud con verificación positiva aún puede bloquearse como resultado de los archivos de firma, módulos, u otras condiciones de la solicitud, y las bypasses pueden ser necesarias para evitar falsos positivos. En el caso de que una bypass esté destinada a tratar exactamente una infracción, ni más ni menos, dicha bypass podría describirse como una "bypass de un solo golpe".

##### "social_media_verification" `[string]`
- Controles para verificar las solicitudes de las plataformas de redes sociales.

```
social_media_verification
├─Embedly ("Embedly")
├─Facebook ("Facebook external hit")
├─Pinterest ("Pinterest")
└─Twitterbot ("Twitterbot")
```

__¿Qué son "positivos" y "negativos"?__ Cuando verificando la identidad presentada por una solicitud, un resultado exitoso podría describirse como "positivo" o "negativo". Cuando se confirma que la identidad presentada es la verdadera identidad, se describiría como "positiva". Cuando se confirma que la identidad presentada es falsa, se describirá como "negativa". Sin embargo, un resultado fallido (por ejemplo, la verificación falló, o no se puede determinar la veracidad de la identidad presentada) no se describiría como "positivo" o "negativo". En cambio, un resultado fallido se describiría simplemente como no verificado. Cuando no se intenta verificar la identidad presentada por una solicitud, la solicitud también se describiría como no verificado. Los términos tienen sentido solo en el contexto en el que se reconoce la identidad presentada por una solicitud y, por lo tanto, donde la verificación es posible. En los casos en que la identidad presentada no coincida con las opciones proporcionadas anteriormente, o cuando no se presente ninguna identidad, las opciones proporcionadas anteriormente se vuelven irrelevantes.

__¿Qué son los "bypasses de un solo golpe"?__ En algunos casos, una solicitud con verificación positiva aún puede bloquearse como resultado de los archivos de firma, módulos, u otras condiciones de la solicitud, y las bypasses pueden ser necesarias para evitar falsos positivos. En el caso de que una bypass esté destinada a tratar exactamente una infracción, ni más ni menos, dicha bypass podría describirse como una "bypass de un solo golpe".

##### "other_verification" `[string]`
- Controles para verificar otros tipos de solicitudes cuando sea posible.

```
other_verification
├─AdSense ("AdSense")
├─AmazonAdBot ("AmazonAdBot")
└─Grapeshot ("Oracle Data Cloud Crawler")
```

__¿Qué son "positivos" y "negativos"?__ Cuando verificando la identidad presentada por una solicitud, un resultado exitoso podría describirse como "positivo" o "negativo". Cuando se confirma que la identidad presentada es la verdadera identidad, se describiría como "positiva". Cuando se confirma que la identidad presentada es falsa, se describirá como "negativa". Sin embargo, un resultado fallido (por ejemplo, la verificación falló, o no se puede determinar la veracidad de la identidad presentada) no se describiría como "positivo" o "negativo". En cambio, un resultado fallido se describiría simplemente como no verificado. Cuando no se intenta verificar la identidad presentada por una solicitud, la solicitud también se describiría como no verificado. Los términos tienen sentido solo en el contexto en el que se reconoce la identidad presentada por una solicitud y, por lo tanto, donde la verificación es posible. En los casos en que la identidad presentada no coincida con las opciones proporcionadas anteriormente, o cuando no se presente ninguna identidad, las opciones proporcionadas anteriormente se vuelven irrelevantes.

__¿Qué son los "bypasses de un solo golpe"?__ En algunos casos, una solicitud con verificación positiva aún puede bloquearse como resultado de los archivos de firma, módulos, u otras condiciones de la solicitud, y las bypasses pueden ser necesarias para evitar falsos positivos. En el caso de que una bypass esté destinada a tratar exactamente una infracción, ni más ni menos, dicha bypass podría describirse como una "bypass de un solo golpe".

##### "protect_frontend" `[bool]`
- Especifica si las protecciones normalmente proporcionadas por CIDRAM deben aplicarse al front-end. True = Sí [Predefinido]; False = No.

##### "default_algo" `[string]`
- Define qué algoritmo utilizar para todas las contraseñas y sesiones en el futuro. Opciones: PASSWORD_DEFAULT (predefinido), PASSWORD_BCRYPT, PASSWORD_ARGON2I (requiere PHP >= 7.2.0), PASSWORD_ARGON2ID (requiere PHP >= 7.3.0).

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I (PHP >= 7.2.0)")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### "statistics" `[string]`
- Controla qué información estadística rastrear.

```
statistics
├─Blocked-IPv4 ("Solicitudes bloqueadas – IPv4")
├─Blocked-IPv6 ("Solicitudes bloqueadas – IPv6")
├─Blocked-Other ("Solicitudes bloqueadas – Otro")
├─Banned-IPv4 ("Solicitudes prohibidas – IPv4")
├─Banned-IPv6 ("Solicitudes prohibidas – IPv6")
├─Passed-IPv4 ("Solicitudes aprobadas – IPv4")
├─Passed-IPv6 ("Solicitudes aprobadas – IPv6")
├─Passed-Other ("Solicitudes aprobadas – Otro")
├─CAPTCHAs-Failed ("Intentos de CAPTCHA – {state_failed}")
└─CAPTCHAs-Passed ("Intentos de CAPTCHA – {state_passed}")
```

##### "force_hostname_lookup" `[bool]`
- ¿Forzar búsquedas de nombres de host? True = Sí; False = No [Predefinido]. Las búsquedas de nombres de host normalmente se realizan según sea necesario, pero se pueden forzar para todas las solicitudes. Hacerlo puede ser útil como un medio para proporcionar información más detallada en los archivos de registro, pero también puede tener un efecto ligeramente negativo en el rendimiento.

##### "allow_gethostbyaddr_lookup" `[bool]`
- ¿Permitir búsquedas gethostbyaddr cuando UDP no está disponible? True = Sí [Predefinido]; False = No.

##### "log_sanitisation" `[bool]`
- Cuando se utiliza el front-end página de los archivos de registro para ver los datos de registro, CIDRAM sanea los datos de registro antes de mostrarlos, para proteger a los usuarios de los ataques XSS y otras amenazas potenciales que podrían estar contenido dentro de los datos de registro. Pero, de forma predefinida, los datos no se sanean durante el registro. Esto es para asegurar que los datos de registro se conserven con precisión, para ayudar a cualquier análisis heurístico o forense que pueda ser necesario en el futuro. Pero, en el caso de que un usuario intente leer los datos de registro utilizando herramientas externas, y si esas herramientas externas no realizan su propio proceso de saneamiento, el usuario podría estar expuesto a ataques XSS. Si es necesario, puede cambiar el comportamiento predefinido utilizando esta directiva de configuración. True = Sanear datos al registrarlo (los datos se conservan con menos precisión, pero el riesgo de XSS es menor). False = No sanear datos al registrarlo (los datos se conservan con mayor precisión, pero el riesgo de XSS es mayor) [Predefinido].

##### "disabled_channels" `[string]`
- Esto se puede usar para evitar que CIDRAM use canales particulares al enviar solicitudes (por ejemplo, al actualizar, al obtener metadatos de componentes, etc).

```
disabled_channels
├─GitHub ("GitHub")
├─BitBucket ("BitBucket")
└─GoogleDNS ("GoogleDNS")
```

##### "default_timeout" `[int]`
- ¿Tiempo de espera predeterminado para usar en solicitudes externas? Predeterminado = 12 segundos.

##### "config_imports" `[string]`
- Una lista delimitada por comas de archivos para importar a la configuración predeterminada de CIDRAM. Normalmente se llena con la página de actualizaciones al activar componentes que lo necesitan cuando sea necesario. En la mayoría de los casos, puede ignorarlo.

##### "events" `[string]`
- Los archivos listados aquí se cargan directamente después del archivo de los controladores de eventos. Normalmente se llena con la página de actualizaciones al activar componentes que lo necesitan cuando sea necesario. En la mayoría de los casos, puede ignorarlo.

#### "signatures" (Categoría)
Configuración para firmas, archivos de firma, módulos, etc.

##### "ipv4" `[string]`
- Una lista de los archivos de firmas IPv4 que CIDRAM debe tratar de utilizar, delimitado por comas.

##### "ipv6" `[string]`
- Una lista de los archivos de firmas IPv6 que CIDRAM debe tratar de utilizar, delimitado por comas.

##### "block_attacks" `[bool]`
- ¿Bloquear CIDRs asociados con ataques y otro tráfico anormal? Por ejemplo, escaneos de puertos, piratería, sondeo de vulnerabilidades, etc. A menos que experimentar problemas cuando hacerlo, en general, esto siempre debe establecerse para true.

##### "block_cloud" `[bool]`
- ¿Bloquear CIDRs identificados como pertenecientes de servicios de webhosting o servicios en la nube? Si usted operar un servicio de un API desde su sitio web o si usted espera otros sitios web para conectarse a su sitio web, esta directiva debe ser establecido para false. Si usted no espera esta, esta directiva debe ser establecido para true.

##### "block_bogons" `[bool]`
- ¿Bloquear CIDRs identificados como bogons/martians? Si usted espera conexiones a su sitio web desde dentro de su red local, desde localhost, o desde su LAN, esta directiva debe ser establecido para false. Si usted no espera estos tipos de conexiones, esta directiva debe ser establecido para true.

##### "block_generic" `[bool]`
- ¿Bloquear CIDRs recomendado generalmente para las listas negras? Esto abarca todos las firmas que no están marcadas como parte de cualquiera de los otros mas especifico categorías de firmas.

##### "block_legal" `[bool]`
- ¿Bloquear CIDRs en respuesta a obligaciones legales? Esta directiva normalmente no debería tener ningún efecto, porque CIDRAM no asocia ningún CIDR con "obligaciones legales" como estándar, pero existe aunque como una medida de control adicional en beneficio de cualquier archivo de firmas o módulo personalizado que pueda existir por razones legales.

##### "block_malware" `[bool]`
- ¿Bloquear CIDRs asociados con el malware? Esto incluye servidores de C&C, máquinas infectadas, máquinas involucradas en la distribución de malware, etc.

##### "block_proxies" `[bool]`
- ¿Bloquear CIDRs identificados como pertenecientes a los servicios de proxy o VPNs? Si requiere que los usuarios puedan acceder a su sitio web a partir de los servicios de proxy o VPNs, esta directiva debe ser establecido para false. Alternativamente, Si usted no requiere servicios de proxy o VPNs, esta directiva debe ser establecido para true como un medio para mejorar la seguridad.

##### "block_spam" `[bool]`
- ¿Bloquear CIDRs identificado como siendo de alto riesgo para el spam? A menos que experimentar problemas cuando hacerlo, en general, esto siempre debe establecerse para true.

##### "modules" `[string]`
- Una lista de archivos módulo a cargar después de comprobar las firmas IPv4/IPv6, delimitado por comas.

##### "default_tracktime" `[int]`
- ¿Cuántos segundos para realizar el seguimiento de las IP prohibidas por los módulos? Predefinido = 604800 (1 semana).

##### "infraction_limit" `[int]`
- Número máximo de infracciones a las que un IP puede incurrir antes de ser prohibido por el rastreo IP. Predefinido = 10.

##### "tracking_override" `[bool]`
- ¿Permitir que los módulos reemplacen las opciones de seguimiento? True = Sí [Predefinido]; False = No.

#### "recaptcha" (Categoría)
Configuración para ReCaptcha (proporciona una forma para que los humanos recuperen el acceso cuando están bloqueados).

##### "usemode" `[int]`
- ¿Cuándo se debe ofrecer el CAPTCHA? Nota: Las solicitudes incluidas en la lista blanca o verificadas y no bloqueadas nunca necesitan completar un CAPTCHA.

```
usemode
├─0 (Nunca !!!)
├─1 (Solo cuando está bloqueado, dentro del límite de firmas y no está prohibido.)
├─2 (Solo cuando está bloqueado, marcado especialmente para su uso, dentro del límite de firmas y no prohibido.)
├─3 (Solo cuando está dentro del límite de firmas y no está prohibido (independientemente de si está bloqueado).)
├─4 (Solo cuando no está bloqueado.)
└─5 (Solo cuando no esté bloqueado, o cuando esté especialmente marcado para su uso, dentro del límite de firmas y no esté prohibido.)
```

##### "lockip" `[bool]`
- Ligar CAPTCHA a los IPs?

##### "lockuser" `[bool]`
- Ligar CAPTCHA a los usuarios?

##### "sitekey" `[string]`
- Este valor se puede encontrar en el panel de control de su servicio de CAPTCHA.

Ver también:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "secret" `[string]`
- Este valor se puede encontrar en el panel de control de su servicio de CAPTCHA.

Ver también:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "expiry" `[float]`
- Número de horas para recordar instancias de CAPTCHA. Predefinido = 720 (1 mes).

##### "logfile" `[string]`
- Registrar todos los intentos de CAPTCHA? En caso afirmativo, especifique el nombre que se utilizará para el archivo de registro. Si no, dejar esta variable en blanco.

##### "signature_limit" `[int]`
- Número máximo de firmas permitidas antes de que se retire la oferta de CAPTCHA. Predefinido = 1.

##### "api" `[string]`
- ¿Qué API usar?

```
api
├─V2 ("V2 (Casilla de verificación)")
└─Invisible ("V2 (Invisible)")
```

##### "show_cookie_warning" `[bool]`
- ¿Mostrar advertencia de cookie? True = Sí [Predefinido]; False = No.

##### "show_api_message" `[bool]`
- ¿Mostrar mensaje de API? True = Sí [Predefinido]; False = No.

##### "nonblocked_status_code" `[int]`
- ¿Qué código de estado se debe usar al mostrar CAPTCHA a solicitudes no bloqueadas?

```
nonblocked_status_code
├─200 (200 OK)
├─403 (403 Forbidden)
├─418 (418 I'm a teapot)
├─429 (429 Too Many Requests)
└─451 (451 Unavailable For Legal Reasons)
```

#### "hcaptcha" (Categoría)
Configuración para HCaptcha (proporciona una forma para que los humanos recuperen el acceso cuando están bloqueados).

##### "usemode" `[int]`
- ¿Cuándo se debe ofrecer el CAPTCHA? Nota: Las solicitudes incluidas en la lista blanca o verificadas y no bloqueadas nunca necesitan completar un CAPTCHA.

```
usemode
├─0 (Nunca !!!)
├─1 (Solo cuando está bloqueado, dentro del límite de firmas y no está prohibido.)
├─2 (Solo cuando está bloqueado, marcado especialmente para su uso, dentro del límite de firmas y no prohibido.)
├─3 (Solo cuando está dentro del límite de firmas y no está prohibido (independientemente de si está bloqueado).)
├─4 (Solo cuando no está bloqueado.)
└─5 (Solo cuando no esté bloqueado, o cuando esté especialmente marcado para su uso, dentro del límite de firmas y no esté prohibido.)
```

##### "lockip" `[bool]`
- Ligar CAPTCHA a los IPs?

##### "lockuser" `[bool]`
- Ligar CAPTCHA a los usuarios?

##### "sitekey" `[string]`
- Este valor se puede encontrar en el panel de control de su servicio de CAPTCHA.

Ver también:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "secret" `[string]`
- Este valor se puede encontrar en el panel de control de su servicio de CAPTCHA.

Ver también:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "expiry" `[float]`
- Número de horas para recordar instancias de CAPTCHA. Predefinido = 720 (1 mes).

##### "logfile" `[string]`
- Registrar todos los intentos de CAPTCHA? En caso afirmativo, especifique el nombre que se utilizará para el archivo de registro. Si no, dejar esta variable en blanco.

##### "signature_limit" `[int]`
- Número máximo de firmas permitidas antes de que se retire la oferta de CAPTCHA. Predefinido = 1.

##### "api" `[string]`
- ¿Qué API usar?

```
api
├─V1 ("V1")
└─Invisible ("V1 (Invisible)")
```

##### "show_cookie_warning" `[bool]`
- ¿Mostrar advertencia de cookie? True = Sí [Predefinido]; False = No.

##### "show_api_message" `[bool]`
- ¿Mostrar mensaje de API? True = Sí [Predefinido]; False = No.

##### "nonblocked_status_code" `[int]`
- ¿Qué código de estado se debe usar al mostrar CAPTCHA a solicitudes no bloqueadas?

```
nonblocked_status_code
├─200 (200 OK)
├─403 (403 Forbidden)
├─418 (418 I'm a teapot)
├─429 (429 Too Many Requests)
└─451 (451 Unavailable For Legal Reasons)
```

#### "legal" (Categoría)
Configuración para requisitos legales.

##### "pseudonymise_ip_addresses" `[bool]`
- ¿Seudonimizar las direcciones IP cuando al escribir archivos de registro? True = Sí [Predefinido]; False = No.

##### "privacy_policy" `[string]`
- La dirección de una política de privacidad relevante que se mostrará en el pie de página de cualquier página generada. Especificar una URL, o dejar en blanco para desactivar.

#### "template_data" (Categoría)
Configuración para plantillas y temas.

##### "theme" `[string]`
- Tema predefinido a utilizar para CIDRAM.

```
theme
├─default ("Default")
├─bluemetal ("Blue Metal")
├─fullmoon ("Full Moon")
├─moss ("Moss")
├─obscured ("Obscured")
├─primer ("Primer")
├─primerdark ("Primer Dark")
├─rbi ("Red-Blue Inverted")
├─slate ("Slate")
└─…Otro
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
├─denied ("denied")
└─…Otro
```

##### "captcha_title" `[string]`
- El título de la página que se mostrará para las solicitudes de CAPTCHA.

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…Otro
```

#### "PHPMailer" (Categoría)
Configuración para PHPMailer (utilizado para la autenticación de dos factores).

##### "event_log" `[string]`
- Un archivo para registrar todos los eventos en relación con PHPMailer. Especificar el nombre del archivo, o dejar en blanco para desactivar.

##### "skip_auth_process" `[bool]`
- Establecer esta directiva en `true` indica a PHPMailer que omita el proceso de autenticación normal que normalmente se produce cuando se envía un correo electrónico a través de SMTP. Esto debe evitarse, ya que omitir este proceso puede exponer el correo electrónico saliente a ataques MITM, pero puede ser necesario en los casos en que este proceso impida que PHPMailer se conecte a un servidor SMTP.

##### "enable_two_factor" `[bool]`
- Esta directiva determina si se debe usar 2FA para las cuentas del front-end.

##### "host" `[string]`
- El host SMTP para usar para el correo electrónico saliente.

##### "port" `[int]`
- El número de puerto a usar para el correo electrónico saliente. Predefinido = 587.

##### "smtp_secure" `[string]`
- El protocolo a usar cuando se envía un correo electrónico a través de SMTP (TLS o SSL).

```
smtp_secure
├─default ("-")
├─tls ("TLS")
└─ssl ("SSL")
```

##### "smtp_auth" `[bool]`
- Esta directiva determina si autenticar sesiones SMTP (generalmente debería dejarse solo).

##### "username" `[string]`
- El nombre de usuario a usar cuando se envía un correo electrónico a través de SMTP.

##### "password" `[string]`
- La contraseña a usar cuando se envía un correo electrónico a través de SMTP.

##### "set_from_address" `[string]`
- La dirección del remitente para citar cuando se envía un correo electrónico a través de SMTP.

##### "set_from_name" `[string]`
- El nombre del remitente para citar cuando se envía un correo electrónico a través de SMTP.

##### "add_reply_to_address" `[string]`
- La dirección de la respuesta para citar cuando se envía un correo electrónico a través de SMTP.

##### "add_reply_to_name" `[string]`
- El nombre de la respuesta para citar cuando se envía un correo electrónico a través de SMTP.

#### "rate_limiting" (Categoría)
Configuración para limitar la velocidad de acceso (no recomendado para uso general).

##### "max_bandwidth" `[string]`
- La cantidad máxima de ancho de banda permitida dentro del período de asignación antes de habilitar los límites de tarifas para solicitudes futuras. Un valor de 0 desactiva este tipo de limitación de la tarifa. Predefinido = 0KB.

##### "max_requests" `[int]`
- El número máximo de solicitudes permitido dentro del período de asignación antes de habilitar los límites de tarifas para solicitudes futuras. Un valor de 0 desactiva este tipo de limitación de la tarifa. Predefinido = 0.

##### "precision_ipv4" `[int]`
- La precisión a utilizar cuando se monitorea el uso de IPv4. El valor refleja el tamaño del bloque CIDR. Establecer en 32 para la mejor precisión. Predefinido = 32.

##### "precision_ipv6" `[int]`
- La precisión a utilizar cuando se monitorea el uso de IPv6. El valor refleja el tamaño del bloque CIDR. Establecer en 128 para la mejor precisión. Predefinido = 128.

##### "allowance_period" `[float]`
- El número de horas para monitorear el uso. Predefinido = 0.

##### "exceptions" `[string]`
- Excepciones (es decir, solicitudes que no deberían limitada). Relevante solo cuando la limitación de velocidad está habilitada.

```
exceptions
├─Whitelisted ("field_whitelisted_requests")
└─Verified ("field_verified_requests")
```

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
- Valor del host de Memcached. Predefinido = "localhost".

##### "memcached_port" `[int]`
- Valor del puerto de Memcached. Predefinido = "11211".

##### "redis_host" `[string]`
- Valor del host de Redis. Predefinido = "localhost".

##### "redis_port" `[int]`
- Valor del puerto de Redis. Predefinido = "6379".

##### "redis_timeout" `[float]`
- Valor de tiempo de espera de Redis. Predefinido = "2.5".

##### "pdo_dsn" `[string]`
- Valor del DSN de PDO. Predefinido = "mysql:dbname=cidram;host=localhost;port=3306".

##### "pdo_username" `[string]`
- Nombre del usuario de PDO.

##### "pdo_password" `[string]`
- Contraseña de PDO.

---


### 7. <a name="SECTION7"></a>FORMATO DE FIRMAS

*Ver también:*
- *[¿Qué es una "firma"?](#WHAT_IS_A_SIGNATURE)*

#### 7.0 LOS FUNDAMENTOS (PARA ARCHIVOS DE FIRMA)

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

#### 7.1 ETIQUETAS

##### 7.1.0 ETIQUETAS DE SECCIÓN

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

##### 7.1.1 ETIQUETAS DE EXPIRACIÓN

Si desea firmas para expiran después de un tiempo, de una manera similar a las etiquetas de sección, se puede utilizar una "etiqueta de expiración" para especificar cuándo deben firmas dejarán de ser válidas. Etiquetas de expiración utilizan el formato "AAAA.MM.DD" (vea el ejemplo siguiente).

```
# Sección 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

Las firmas expiradas nunca se desencadenán en ninguna solicitud, sin importar qué.

##### 7.1.2 ETIQUETAS DE ORIGEN

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

##### 7.1.3 ETIQUETAS DE DEFERENCIA

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

##### 7.1.4 ETIQUETAS DE PERFIL

Las etiquetas de perfil proporcionan un medio para mostrar información adicional en la página de prueba de IP y pueden ser aprovechadas por módulos y reglas auxiliares para un comportamiento más complejo y una toma de decisiones más precisa.

Las etiquetas de perfil se utilizan de manera similar a otros tipos de etiquetas. Los valores de las etiquetas de perfil se pueden utilizar como condición para módulos y reglas auxiliares. Las etiquetas de perfil pueden proporcionar varios valores separando esos valores con un punto y coma. El usuario final nunca ve los valores de las etiquetas de perfil.

Ejemplo:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 7.2 YAML

##### 7.2.0 LOS FUNDAMENTOS DE YAML

Una forma simplificada de YAML markup se puede utilizar en los archivos de firmas con el propósito de definir los comportamientos y configuraciones específicas para las secciones de firmas individuales. Esto puede ser útil si desea que el valor de sus directivas de configuración diferir sobre la base de las firmas individuales y las secciones de firmas (por ejemplo; si desea proporcionar una dirección de correo electrónico para los tickets de soporte para cualquier usuario bloqueadas por una firma particular, pero no desea proporcionar una dirección de correo electrónico para tickets de soporte para usuarios bloqueados por cualquier otro firmas; si desea por algunas firmas específicas para desencadenar una redirección de página; si desea marcar una sección de firmas para usar con reCAPTCHA/hCAPTCHA; si desea registrar los intentos de acceso bloqueados para archivos separados sobre la base de firmas individuales y/o secciones de firmas).

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
 logfile: logfile.{yyyy}-{mm}-{dd}.txt
 logfile_apache: access.{yyyy}-{mm}-{dd}.txt
 logfile_serialized: serial.{yyyy}-{mm}-{dd}.txt
 forbid_on_block: false
 emailaddr: username@domain.tld
recaptcha:
 lockip: false
 lockuser: true
 expiry: 720
 logfile: recaptcha.{yyyy}-{mm}-{dd}.txt
 enabled: true
template_data:
 css_url: https://domain.tld/cidram.css

# Foobar 2.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
4.5.6.7/32 Deny Generic
Tag: Foobar 2
---
general:
 logfile: "logfile.Foobar2.{yyyy}-{mm}-{dd}.txt"
 logfile_apache: "access.Foobar2.{yyyy}-{mm}-{dd}.txt"
 logfile_serialized: "serial.Foobar2.{yyyy}-{mm}-{dd}.txt"
 forbid_on_block: 503

# Foobar 3.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
4.5.6.7/32 Deny Generic
Tag: Foobar 3
---
general:
 forbid_on_block: 403
 silent_mode: "http://127.0.0.1/"
```

##### 7.2.1 CÓMO "ESPECIALMENTE MARCAR" SECCIONES DE FIRMAS PARA USAR CON reCAPTCHA/hCAPTCHA

Cuando "usemode" es 2 o 5, para "especialmente marcar" secciones de firmas para usar con reCAPTCHA/hCAPTCHA, una entrada está incluida en el segmento de YAML para que esa sección de firmas (vea el ejemplo siguiente).

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Tag: CAPTCHA Marked
---
recaptcha:
 enabled: true
hcaptcha:
 enabled: true
```

#### 7.3 AUXILIAR

##### 7.3.0 IGNORANDO LAS SECCIONES DE FIRMA

En adición, si quieres CIDRAM ignorar completamente algunas secciones específicas dentro de cualquiera de los archivos de firmas, puede utilizar el archivo `ignore.dat` para especificar qué secciones por ignorar. En una línea nueva, escribir `Ignore`, seguido de un espacio, seguido del nombre de la sección que desea CIDRAM ignorar (vea el ejemplo siguiente).

```
Ignore Sección 1
```

Esto también se puede lograr utilizando la interfaz proporcionada por la página de "lista de secciones" del front-end de CIDRAM.

##### 7.3.1 REGLAS AUXILIARES

Si cree que escribir sus propios archivos de firmas personalizadas o módulos personalizados es demasiado complicado para usted, una alternativa más simple puede ser utilizar la interfaz proporcionada por la página de "reglas auxiliares" del front-end de CIDRAM. Al seleccionar las opciones apropiadas y especificar detalles sobre tipos específicos de solicitudes, puede indicar a CIDRAM cómo responder a esas solicitudes. Las "reglas auxiliares" se ejecutan después de que todos los archivos y módulos de firmas ya hayan terminado de ejecutarse.

#### 7.4 <a name="MODULE_BASICS"></a>LOS FUNDAMENTOS (PARA MÓDULOS)

Los módulos se pueden usar para ampliar la funcionalidad de CIDRAM, realizar tareas adicionales o procesar lógica adicional. Típicamente, se usan cuando es necesario bloquear una solicitud por razones distintas de la dirección IP de origen (y por lo tanto, cuando una firma CIDR no sea suficiente para bloquear la solicitud). Los módulos se escriben como archivos PHP y, por lo tanto, típicamente, las firmas de los módulos se escriben como código PHP.

Algunos buenos ejemplos de módulos CIDRAM se pueden encontrar aquí:
- https://github.com/CIDRAM/CIDRAM-Extras/tree/master/modules

Una plantilla para escribir nuevos módulos se puede encontrar aquí:
- https://github.com/CIDRAM/CIDRAM-Extras/blob/master/modules/module_template.php

Debido a que los módulos se escriben como archivos PHP, si está familiarizado adecuadamente con la base de código de CIDRAM, puede estructurar los módulos de la forma que desee, y escribe las firmas de tu módulo como quieras (dentro de lo que es posible con PHP). Pero, para su propia conveniencia, y en aras de una mejor inteligibilidad mutua entre los módulos existentes y su propio, se recomienda analizar la plantilla vinculada anteriormente, para poder usar la estructura y el formato que proporciona.

*Nota: Si no se siente cómodo trabajando con código PHP, no se recomienda escribir sus propios módulos.*

CIDRAM brinda cierta funcionalidad que los módulos pueden usar, lo que simplifica la escritura de sus propios módulos. La información sobre esta funcionalidad se describe a continuación.

#### 7.5 FUNCIONALIDAD DEL MÓDULO

##### 7.5.0 "$Trigger"

Las firmas de los módulos generalmente se escriben con `$Trigger`. En la mayoría de los casos, este closure será más importante que cualquier otra cosa con el fin de escribir módulos.

`$Trigger` acepta 4 parámetros: `$Condition`, `$ReasonShort`, `$ReasonLong` (opcional), y `$DefineOptions` (opcional).

La veracidad de `$Condition` se evalúa, y si es true/verdadera, la firma se "desencadena". Si es false/falso, la firma *no* se "desencadena". `$Condition` generalmente contiene código PHP para evaluar una condición que debe causar el bloqueo de una solicitud.

`$ReasonShort` se cita en el campo "Razón Bloqueado" cuando la firma se "desencadena".

`$ReasonLong` es un mensaje opcional que se mostrará al usuario/cliente para cuando estén bloqueados, para explicar por qué se han bloqueado. Se predetermina al mensaje estándar "¡Acceso Denegado!" cuando se omite.

`$DefineOptions` es una array opcional que contiene pares clave/valor, que se utiliza para definir opciones de configuración específicas para la instancia de solicitud. Las opciones de configuración se aplicarán cuando la firma se "desencadena".

`$Trigger` devuelve true/verdadero cuando la firma se "desencadena" y false/falso cuando no es así.

Para usar este closure en su módulo, recuerde primero heredarlo del alcance principal:
```PHP
$Trigger = $CIDRAM['Trigger'];
```

##### 7.5.1 "$Bypass"

Los bypass de la firma generalmente se escriben con `$Bypass`.

`$Bypass` acepta 3 parámetros: `$Condition`, `$ReasonShort`, y `$DefineOptions` (opcional).

La veracidad de `$Condition` se evalúa, y si es true/verdadera, el bypass se "desencadena". Si es false/falso, el bypass *no* se "desencadena". `$Condition` generalmente contiene código PHP para evaluar una condición que *no* debe causar el bloqueo de una solicitud.

`$ReasonShort` se cita en el campo "Razón Bloqueado" cuando el bypass se "desencadena".

`$DefineOptions` es una array opcional que contiene pares clave/valor, que se utiliza para definir opciones de configuración específicas para la instancia de solicitud. Las opciones de configuración se aplicarán cuando el bypass se "desencadena".

`$Bypass` devuelve true/verdadero cuando el bypass se "desencadena" y false/falso cuando no es así.

Para usar este closure en su módulo, recuerde primero heredarlo del alcance principal:
```PHP
$Bypass = $CIDRAM['Bypass'];
```

##### 7.5.2 "$CIDRAM['DNS-Reverse']"

Esto se puede usar para buscar el nombre del host de una dirección IP. Si desea crear un módulo para bloquear nombres de host, este closure podría ser útil.

Ejemplo:
```PHP
<?php
/** Inherit trigger closure (see functions.php). */
$Trigger = $CIDRAM['Trigger'];

/** Fetch hostname. */
if (empty($CIDRAM['Hostname'])) {
    $CIDRAM['Hostname'] = $CIDRAM['DNS-Reverse']($CIDRAM['BlockInfo']['IPAddr']);
}

/** Example signature. */
if ($CIDRAM['Hostname'] && $CIDRAM['Hostname'] !== $CIDRAM['BlockInfo']['IPAddr']) {
    $Trigger($CIDRAM['Hostname'] === 'www.foobar.tld', 'Foobar.tld', 'Hostname Foobar.tld is not allowed.');
}
```

#### 7.6 VARIABLES DE MÓDULO

Los módulos se ejecutan dentro de su propio alcance, y cualquier variable definida por un módulo, no será accesible para otros módulos, o para el script principal, a menos que estén almacenados en la array `$CIDRAM` (todo lo demás se vacía después de que finaliza la ejecución del módulo).

A continuación se enumeran algunas variables comunes que pueden ser útiles para su módulo:

Variable | Descripción
----|----
`$CIDRAM['BlockInfo']['DateTime']` | La fecha y hora actual.
`$CIDRAM['BlockInfo']['IPAddr']` | Dirección IP para la solicitud actual.
`$CIDRAM['BlockInfo']['ScriptIdent']` | Versión de CIDRAM.
`$CIDRAM['BlockInfo']['Query']` | La "query" para la solicitud actual.
`$CIDRAM['BlockInfo']['Referrer']` | El referente para la solicitud actual (si existe).
`$CIDRAM['BlockInfo']['UA']` | El agente de usuario (user agent) para la solicitud actual.
`$CIDRAM['BlockInfo']['UALC']` | El agente de usuario (user agent) para la solicitud actual (en minúsculas).
`$CIDRAM['BlockInfo']['ReasonMessage']` | El mensaje que se mostrará al usuario/cliente para la solicitud actual si están bloqueados.
`$CIDRAM['BlockInfo']['SignatureCount']` | El número de firmas desencadenadas para la solicitud actual.
`$CIDRAM['BlockInfo']['Signatures']` | Información de referencia para cualquier firma desencadenada para la solicitud actual.
`$CIDRAM['BlockInfo']['WhyReason']` | Información de referencia para cualquier firma desencadenada para la solicitud actual.

---


### 8. <a name="SECTION8"></a>CONOCIDOS PROBLEMAS DE COMPATIBILIDAD

Se ha encontrado que los siguientes paquetes y productos son incompatibles con CIDRAM:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

Los módulos se han puesto a disposición para garantizar que los siguientes paquetes y productos sean compatibles con CIDRAM:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__

*Ver también: [Gráficos de Compatibilidad](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 9. <a name="SECTION9"></a>PREGUNTAS MÁS FRECUENTES (FAQ)

- [¿Qué es una "firma"?](#WHAT_IS_A_SIGNATURE)
- [¿Qué es un "CIDR"?](#WHAT_IS_A_CIDR)
- [¿Qué es un "falso positivo"?](#WHAT_IS_A_FALSE_POSITIVE)
- [¿Puede CIDRAM bloquear países enteros?](#BLOCK_ENTIRE_COUNTRIES)
- [¿Con qué frecuencia se actualizan las firmas?](#SIGNATURE_UPDATE_FREQUENCY)
- [¡He encontrado un problema mientras uso CIDRAM y no sé qué hacer al respecto! ¡Por favor ayuda!](#ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [¡He sido bloqueado por CIDRAM desde un sitio web que quiero visitar! ¡Por favor ayuda!](#BLOCKED_WHAT_TO_DO)
- [Quiero usar CIDRAM (antes de v2) con una versión de PHP más vieja que 5.4.0; ¿Puede usted ayudar?](#MINIMUM_PHP_VERSION)
- [Quiero usar CIDRAM (v2) con una versión de PHP más vieja que 7.2.0; ¿Puede usted ayudar?](#MINIMUM_PHP_VERSION_V2)
- [¿Puedo usar una sola instalación de CIDRAM para proteger múltiples dominios?](#PROTECT_MULTIPLE_DOMAINS)
- [No quiero molestarme con la instalación de este y conseguir que funcione con mi sitio web; ¿Puedo pagarte por hacer todo por mí?](#PAY_YOU_TO_DO_IT)
- [¿Puedo contratar a usted oa cualquiera de los desarrolladores de este proyecto para el trabajo privado?](#HIRE_FOR_PRIVATE_WORK)
- [Necesito modificaciones especiales, personalizaciones, etc; ¿Puede usted ayudar?](#SPECIALIST_MODIFICATIONS)
- [Soy desarrollador, diseñador de sitios web o programador. ¿Puedo aceptar u ofrecer trabajos relacionados con este proyecto?](#ACCEPT_OR_OFFER_WORK)
- [Quiero contribuir al proyecto; ¿Puedo hacer esto?](#WANT_TO_CONTRIBUTE)
- [¿Puedo usar cron para actualizar automáticamente?](#CRON_TO_UPDATE_AUTOMATICALLY)
- [¿Qué son "infracciones"?](#WHAT_ARE_INFRACTIONS)
- [¿Puede CIDRAM bloquear nombres de host?](#BLOCK_HOSTNAMES)
- [¿Qué puedo usar para "default_dns"?](#WHAT_CAN_I_USE_FOR_DEFAULT_DNS)
- [¿Puedo usar CIDRAM para proteger cosas que no sean sitios web (por ejemplo, servidores de correo electrónico, FTP, SSH, IRC, etc)?](#PROTECT_OTHER_THINGS)
- [¿Se producirán problemas si uso CIDRAM al mismo tiempo que uso CDN o servicios de caché?](#CDN_CACHING_PROBLEMS)
- [¿CIDRAM protegerá mi sitio web de los ataques DDoS?](#DDOS_ATTACKS)
- [Cuando activar o desactivar módulos o archivos de firmas a través de la página de actualizaciones, los ordena de forma alfanumérica en la configuración. ¿Puedo cambiar la forma en que se ordenan?](#CHANGE_COMPONENT_SORT_ORDER)
- [¿Qué es un "PDO DSN"? Cómo puedo usar PDO con CIDRAM?](#HOW_TO_USE_PDO)
- [CIDRAM está bloqueando cronjobs; ¿Cómo arreglar esto?](#BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>¿Qué es una "firma"?

En el contexto de CIDRAM, una "firma" se refiere a datos que actúan como un indicador/identificador para algo específico que estamos buscando, normalmente una dirección IP o CIDR, e incluye algunas instrucciones para CIDRAM, diciéndole la mejor manera de responder cuando encuentra lo que estamos buscando. Una firma típica para CIDRAM se parece a esto:

Para "archivos de firma":

`1.2.3.4/32 Deny Generic`

Para "módulos":

```PHP
$Trigger(strpos($CIDRAM['BlockInfo']['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*Nota: Las firmas para "archivos de firma", y las firmas para "módulos", no son lo mismo.*

A menudo (pero no siempre), las firmas se agruparán en grupos, formando "secciones de firmas", a menudo acompañado de comentarios, markup, y/o metadatos relacionados que se pueden utilizar para proporcionar contexto adicional para las firmas y/o instrucción adicional.

#### <a name="WHAT_IS_A_CIDR"></a>¿Qué es un "CIDR"?

"CIDR" es un acrónimo para "Classless Inter-Domain Routing" (o "enrutamiento entre dominios sin clases") *[[1](https://es.wikipedia.org/wiki/Classless_Inter-Domain_Routing), [2](https://whatismyipaddress.com/cidr)]*, y es este acrónimo que se utiliza como parte del nombre de este paquete, "CIDRAM", que es un acrónimo de "Classless Inter-Domain Routing Access Manager".

Aunque, en el contexto de CIDRAM (tal como, dentro de esta documentación, dentro de los discusiones relacionados con CIDRAM, o dentro de los lingüísticos datos para CIDRAM), en cualquier momento que un "CIDR" (singular) o "CIDRs" (plural) se menciona o se hace referencia a (y por lo tanto, mediante el cual utilizamos estas palabras como sustantivos por derecho propio, en contraposición a como acrónimos), lo que se pretende y quiere decir con esto es una subred (o subredes), expresado usando la notación CIDR. La razón por la que CIDR (o CIDRs) se utiliza en lugar de subred (o subredes) es dejar claro que se trata específicamente de subredes expresadas mediante la notación CIDR a la que se hace referencia (porque la notación CIDR es sólo una de varias maneras diferentes que las subredes se pueden expresar). Por lo tanto, CIDRAM podría considerarse un "gestor de acceso para subredes".

Aunque este doble significado de "CIDR" puede presentar alguna ambigüedad en algunos casos, esta explicacion, junto con el contexto proporcionado, debe ayudar a resolver esa ambigüedad.

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

#### <a name="MINIMUM_PHP_VERSION"></a>Quiero usar CIDRAM (antes de v2) con una versión de PHP más vieja que 5.4.0; ¿Puede usted ayudar?

No. PHP >= 5.4.0 es un requisito mínimo para CIDRAM < v2.

#### <a name="MINIMUM_PHP_VERSION_V2"></a>Quiero usar CIDRAM (v2) con una versión de PHP más vieja que 7.2.0; ¿Puede usted ayudar?

No. PHP >= 7.2.0 es un requisito mínimo para CIDRAM v2.

*Ver también: [Gráficos de Compatibilidad](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>¿Puedo usar una sola instalación de CIDRAM para proteger múltiples dominios?

Sí. Las instalaciones de CIDRAM no están ligados naturalmente en dominios específicos, y por lo tanto puede ser utilizado para proteger múltiples dominios. En general, nos referimos a las instalaciones de CIDRAM que protegen solo un dominio como "instalaciones solo-dominio" ("single-domain installations"), y nos referimos a las instalaciones de CIDRAM que protegen múltiples dominios y/o subdominios como "instalaciones multi-dominio" ("multi-domain installations"). Si utiliza una instalación multi-dominio y es necesario utilizar diferentes conjuntos de archivos de firmas para diferentes dominios, o si CIDRAM debe configurarse de manera diferente para diferentes dominios, es posible hacer esto. Después de cargar el archivo de configuración (`config.ini`), CIDRAM comprobará la existencia de un "archivo de sustitución para configuración" específico del dominio (o subdominio) que se solicita (`el-dominio-que-se-solicita.tld.config.ini`), y si se encuentra, cualquier valor de configuración definido por el archivo de sustitución para configuración se utilizará para la instancia de ejecución en lugar de los valores de configuración definidos por el archivo de configuración. Los archivos de sustitución para configuración son idénticos al archivo de configuración, ya su discreción, puede contener la totalidad de todas las directivas de configuración disponibles para CIDRAM, o lo que sea subsección necesaria que difiera de los valores normalmente definidos por el archivo de configuración. Los archivos de sustitución para configuración se nombran de acuerdo con el dominio al que están destinados (así por ejemplo, si se requiere un archivo de sustitución para configuración para el dominio, `https://www.some-domain.tld/`, su archivo de sustitución para configuración debe ser nombrado como `some-domain.tld.config.ini`, y debe colocarse dentro de la vault junto con el archivo de configuración, `config.ini`). El nombre del dominio para la instancia de ejecución se deriva del encabezado `HTTP_HOST` de la solicitud; "www" se ignora.

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

Las "infracciones" determinan cuándo una IP que todavía no está bloqueada por ningún archivo de firma específico debe comenzar a bloquearse para futuras solicitudes, y están estrechamente asociados con el seguimiento de IP. Existen algunas funcionalidades y módulos que permiten que las solicitudes sean bloqueadas por razones distintas del origen del IP (tal como la presencia de agentes de usuario [user agents] correspondientes a spambots o hacktools, solicitudes peligrosas, DNS falsificado, etc), y cuando esto sucede, una "infracción" puede ocurrir. Proporcionan una forma de identificar las direcciones IP que corresponden a las solicitudes no deseadas que aún no pueden ser bloqueadas por ningún archivo de firma específico. Las infracciones generalmente corresponden de 1-a-1 con la cantidad de veces que se bloquea un IP, pero no siempre (los eventos de bloque severos pueden incurrir en un valor de infracción mayor que uno, y si "track_mode" es false, infracciones no ocurrirán para eventos de bloque causados únicamente por archivos de firma).

#### <a name="BLOCK_HOSTNAMES"></a>¿Puede CIDRAM bloquear nombres de host?

Sí. Para hacer esto, necesitarás crear un archivo de módulo personalizado. *Ver: [LOS FUNDAMENTOS (PARA MÓDULOS)](#MODULE_BASICS)*.

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

`file1.php,file2.php,file3.php,file4.php,file5.php`

Si quería ejecutar `file3.php` primero, puede agregar algo como `aaa:` antes del nombre del archivo:

`file1.php,file2.php,aaa:file3.php,file4.php,file5.php`

Entonces, si se activa un archivo nuevo, `file6.php`, cuando la página de actualizaciones los clasifique nuevamente, debería terminar así:

`aaa:file3.php,file1.php,file2.php,file4.php,file5.php,file6.php`

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


### 11. <a name="SECTION11"></a>INFORMACIÓN LEGAL

#### 11.0 PREÁMBULO DE SECCIÓN

La intención de esta sección de la documentación es para describir posibles consideraciones legales con respecto al uso y la implementación del paquete, y para proporcionar cierta información básica relacionada. Esto puede ser importante para algunos usuarios como un medio para garantizar el cumplimiento de los requisitos legales que puedan existir en los países en los que operan, y algunos usuarios pueden necesitar ajustar las políticas de su sitio web de acuerdo con esta información.

Primero y ante todo, tenga en cuenta que yo (el autor del paquete) no soy un abogado, ni un profesional legal calificado de ningún tipo. Por lo tanto, no estoy legalmente calificado para brindar asesoramiento legal. Además, en algunos casos, los requisitos legales exactos pueden variar entre diferentes países y jurisdicciones, y estos diferentes requisitos legales pueden a veces entrar en conflicto (como, por ejemplo, en el caso de países que favorecen los [derechos de privacidad](https://es.wikipedia.org/wiki/Derecho_a_la_intimidad) y el [derecho a ser olvidado](https://es.wikipedia.org/wiki/Derecho_al_olvido), frente a los países que favorecen la [retención de datos extendida](https://es.wikipedia.org/wiki/Retenci%C3%B3n_de_datos_de_telecomunicaci%C3%B3n)). Considere también que el acceso al paquete no está restringido a países o jurisdicciones específicos, y por lo tanto, es probable que la base de usuarios del paquete sea geográficamente diversa. Considerados estos puntos, no estoy en condiciones de decir lo que significa ser "legalmente compatible" para todos los usuarios, en todos los aspectos. Sin embargo, espero que la información en este documento lo ayude a tomar una decisión sobre lo que debe hacer para cumplir con la ley en el contexto del paquete. Si tiene alguna duda o inquietud con respecto a la información aquí incluida, o si necesita ayuda y asesoramiento adicional desde una perspectiva legal, le recomiendo consultar a un profesional legal calificado.

#### 11.1 RESPONSABILIDAD

Según lo establecido por la licencia del paquete, el paquete se proporciona sin ninguna garantía. Esto incluye (pero no se limita a) todo el alcance de la responsabilidad. El paquete se le proporciona para su conveniencia, con la esperanza de que sea útil y le proporcionará algún beneficio. Pero, si usa o implementa el paquete, es su propia decisión. No está obligado a usar o implementar el paquete, pero cuando lo hace, usted es responsable de esa decisión. Ni yo ni ningún otro contribuyente del paquete somos legalmente responsables de las consecuencias de las decisiones que usted tome, independientemente de si son directas, indirectas, implícitas o de otro tipo.

#### 11.2 TERCEROS

Dependiendo de su configuración e implementación exactas, el paquete puede comunicarse y compartir información con terceros en algunos casos. Esta información puede definirse como "[información personal](https://es.wikipedia.org/wiki/Informaci%C3%B3n_personal)" (PII) en algunos contextos, en algunas jurisdicciones.

La forma en que esta información puede ser utilizada por estos terceros está sujeta a las diversas políticas establecidas por estos terceros y está fuera del alcance de esta documentación. Pero, en todos estos casos, se puede deshabilitar el intercambio de información con estos terceros. En todos estos casos, si elige habilitarlo, es su responsabilidad investigar cualquier inquietud que pueda tener con respecto a la privacidad, seguridad y uso de PII por parte de estos terceros. Si tiene alguna duda, o si no está satisfecho con la conducta de estos terceros en lo que respecta a PII, puede ser mejor desactivar el intercambio de información con estos terceros.

A los efectos de la transparencia, el tipo de información compartida, y con quién, se describe a continuación.

##### 11.2.0 BÚSQUEDA DE NOMBRES DE HOST

Si usa funciones o módulos destinados a trabajar con nombres de host (como el "módulo bloqueador de hosts malos", "tor project exit nodes block module", o la "verificación de los motores de búsqueda", por ejemplo), CIDRAM necesita poder obtener el nombre de host de las solicitudes entrantes de alguna manera. Normalmente, lo hace al solicitar el nombre de host de la dirección IP de las solicitudes entrantes desde un servidor DNS, o solicitando la información a través de la funcionalidad provista por el sistema donde está instalado CIDRAM (esto se conoce típicamente como una "búsqueda de nombre de host"). Los servidores DNS predefinidos pertenecen al servicio [Google DNS](https://dns.google.com/) (pero esto se puede cambiar fácilmente a través de la configuración). Los servicios exactos comunicados son configurables y dependen de cómo configure el paquete. En el caso de utilizar la funcionalidad proporcionada por el sistema donde está instalado CIDRAM, deberá ponerse en contacto con el administrador de su sistema para determinar qué rutas utilizan las búsquedas de nombres de host. Las búsquedas de nombre de host se pueden evitar en CIDRAM por evitando los módulos afectados o modificando la configuración del paquete de acuerdo con sus necesidades.

*Directivas de configuración relevantes:*
- `general` -> `default_dns`
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`
- `general` -> `force_hostname_lookup`
- `general` -> `allow_gethostbyaddr_lookup`

##### 11.2.2 VERIFICACIÓN DEL MOTOR DE BÚSQUEDA Y REDES SOCIALES

Cuando la verificación del motor de búsqueda está habilitada, CIDRAM intenta realizar "búsquedas DNS hacia adelante" para verificar si las solicitudes que afirman tener su origen en los motores de búsqueda son auténticas. Del mismo modo, cuando la verificación de redes sociales está habilitada, CIDRAM hace lo mismo para solicitudes aparentes de redes sociales. Para hacer esto, utiliza el servicio [Google DNS](https://dns.google.com/) para intentar resolver las direcciones IP de los nombres de host de estas solicitudes entrantes (en este proceso, los nombres de host de estas solicitudes entrantes se comparten con el servicio).

*Directivas de configuración relevantes:*
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`

##### 11.2.3 CAPTCHA

CIDRAM suporte reCAPTCHA y hCAPTCHA. Requieren claves API para funcionar correctamente. Están deshabilitados de forma predeterminada, pero se pueden habilitar configurando las claves API requeridas. Cuando están habilitado, la comunicación puede ocurrir entre el servicio y CIDRAM o el navegador del usuario. Esto puede implicar la comunicación de información como la dirección IP del usuario, el agente de usuario, el sistema operativo, y otros detalles disponibles para la solicitud.

##### 11.2.4 STOP FORUM SPAM

[Stop Forum Spam](https://www.stopforumspam.com/) es un fantástico servicio gratuito que puede ayudar a proteger los foros, blogs, y sitios web de los spammers. Lo hace al proporcionar una base de datos de spammers conocidos, y una API que se puede aprovechar para verificar si una dirección IP, nombre de usuario, o dirección de correo electrónico aparece en su base de datos.

CIDRAM proporciona un módulo opcional que aprovecha esta API para verificar si la dirección IP de las solicitudes entrantes pertenece a un sospechoso de spammer. El módulo no está instalado de manera predeterminada, pero si decide instalarlo, las direcciones IP del usuario se pueden compartir con la API de Stop Forum Spam de acuerdo con el propósito del módulo. Cuando se instala el módulo, CIDRAM se comunica con esta API cada vez que una solicitud entrante solicita un recurso que CIDRAM reconoce como un tipo de recurso frecuentemente dirigido por los spammers (como páginas de inicio de sesión, páginas de registro, páginas de verificación de correo electrónico, formularios de comentarios, etc).

##### 11.2.5 ABUSEIPDB

CIDRAM proporciona un módulo opcional para bloquear direcciones IP abusivas utilizando la API de [AbuseIPDB](https://www.abuseipdb.com/). El módulo no está instalado de manera predeterminada, pero si decide instalarlo, las direcciones IP del usuario se pueden compartir con la API de AbuseIPDB de acuerdo con el propósito del módulo.

##### 11.2.6 BGPVIEW

CIDRAM proporciona un módulo opcional para realizar búsquedas de código de país y ASN utilizando la API de [BGPView](https://bgpview.io/). Estas búsquedas proporcionan la capacidad de bloquear o incluir en la lista blanca las solicitudes en función de su ASN o país de origen. El módulo no está instalado de manera predeterminada, pero si decide instalarlo, las direcciones IP del usuario se pueden compartir con la API de BGPView de acuerdo con el propósito del módulo.

#### 11.3 REGISTRO DE DATOS

El registro de datos es una parte importante de CIDRAM por varias razones. Puede ser difícil diagnosticar y resolver falsos positivos cuando los eventos de bloqueo que los causan no se registran. Sin registrar eventos de bloques, puede ser difícil determinar con exactitud qué tan eficiente es el CIDRAM en un contexto particular, y puede ser difícil determinar dónde se encuentran sus deficiencias, y qué cambios pueden requerirse en su configuración o firmas en consecuencia, para que continúe funcionando según lo previsto. En todo caso, el registro de datos puede no ser deseable para todos los usuarios, y sigue siendo totalmente opcional. En CIDRAM, el registro de datos está deshabilitado de forma predeterminada. Para habilitarlo, CIDRAM debe configurarse en consecuencia.

Además, si el registro de datos es legalmente permisible, y en la medida en que sea legalmente permisible (por ejemplo, los tipos de información que pueden registrarse, por cuánto tiempo, y en qué circunstancias), puede variar, dependiendo de la jurisdicción y del contexto donde se implemente el CIDRAM (por ejemplo, ya sea que esté operando como individuo, como una entidad corporativa, y sea comercial o no comercial). Por lo tanto, puede serle útil leer atentamente esta sección.

Existen varios tipos de registro que CIDRAM puede realizar. Los diferentes tipos de registro implican diferentes tipos de información, por diferentes razones.

##### 11.3.0 EVENTOS DE BLOQUE

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
- `general` -> `logfile`
- `general` -> `logfile_apache`
- `general` -> `logfile_serialized`

Cuando estas directivas se dejan vacías, este tipo de registro permanecerá desactivado.

##### 11.3.1 REGISTROS DE CAPTCHA

Este tipo de registro se relaciona específicamente con instancias CAPTCHA, y ocurre solo cuando un usuario intenta completar una instancia de CAPTCHA.

Una entrada de registros de CAPTCHA contiene la dirección IP del usuario que intenta completar una instancia de CAPTCHA, la fecha y la hora en que se produjo el intento, y el estado CAPTCHA. Una entrada de registros de CAPTCHA generalmente se ve así (como un ejemplo):

```
Dirección IP: x.x.x.x - Fecha/Hora: Day, dd Mon 20xx hh:ii:ss +0000 - Estado CAPTCHA: ¡Éxito!
```

*La directiva de configuración responsable del registros de CAPTCHA es:*
- `recaptcha` -> `logfile`
- `hcaptcha` -> `logfile`

##### 11.3.2 REGISTROS DE FRONT-END

Este tipo de registro relaciona los intentos de inicio de sesión del front-end, y ocurre solo cuando un usuario intenta iniciar sesión en el front-end (suponiendo que el acceso al front-end esté habilitado).

Una entrada de registro en el front-end contiene la dirección IP del usuario que intenta iniciar sesión, la fecha y la hora en que se produjo el intento, y los resultados del intento (inicio de sesión exitoso o fallido). Una entrada de registro del front-end generalmente se ve así (como un ejemplo):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Conectado.
```

*La directiva de configuración responsable del inicio de sesión es:*
- `general` -> `frontend_log`

##### 11.3.3 ROTACIÓN DE REGISTROS

Es posible que desee purgar los registros después de un período de tiempo, o posible la ley lo requiera (es decir, la cantidad de tiempo que está legalmente permitido para conservar los registros puede estar limitada por la ley). Puede lograr esto incluyendo marcadores de fecha/hora en los nombres de sus archivos de registro según lo especificado por la configuración de su paquete (por ejemplo, `{yyyy}-{mm}-{dd}.log`), y luego habilitar la rotación de registros (la rotación de registros le permite realizar alguna acción en los archivos de registro cuando se exceden los límites especificados).

Por ejemplo: Si se me exigiera legalmente que borrara los registros después de 30 días, podría especificar `{dd}.log` en los nombres de mis archivos de registro (`{dd}` representa días), establecer el valor de `log_rotation_limit` en 30, y establecer el valor de `log_rotation_action` en `Delete`.

Por el contrario, si está obligado a conservar registros por un período prolongado de tiempo, puede no utilizar la rotación de registros, o puede establecer el valor de `log_rotation_action` en `Archive`, para comprimir archivos de registro, lo que reduce la cantidad total de espacio en disco que ocupan.

*Directivas de configuración relevantes:*
- `general` -> `log_rotation_limit`
- `general` -> `log_rotation_action`

##### 11.3.4 TRUNCAMIENTO DE REGISTROS

También es posible truncar archivos de registro individuales cuando exceden un cierto tamaño, si esto es algo que podría necesitar o querer hacer.

*Directivas de configuración relevantes:*
- `general` -> `truncate`

##### 11.3.5 SEUDONIMIZACIÓN DE DIRECCIONES IP

Primeramente, si no está familiarizado con el término, "seudonimización" se refiere al procesamiento de datos personales como tal que ya no se puede identificar a ningún sujeto de datos específico sin información adicional, y siempre que dicha información adicional se mantenga por separado y esté sujeta a medidas técnicas y organizativas para garantizar que los datos personales no puedan identificarse a ninguna persona física.

Los siguientes recursos pueden ayudar a explicarlo con más detalle:
- [[confilegal.com] La importancia del seudonimización en el nuevo Reglamento de Protección de Datos](https://confilegal.com/20170129-la-importancia-del-seudonimizacion-en-el-nuevo-reglamento-de-proteccion-de-datos/)
- [[forlopd.es] ¿Cómo me protege la seudonimización?](https://www.forlopd.es/web/blog/index.php/seudonimizacion-y-proteccion-de-datos/)
- [[Wikipedia] Seudonimización](https://es.wikipedia.org/wiki/Seudonimizaci%C3%B3n)

En algunas circunstancias, se le puede ser legalmente requerido anonimizar o seudonimizar cualquier PII recopilada, procesada, o almacenada. Aunque este concepto ha existe desde hace bastante tiempo, GDPR/DSGVO menciona especialmente, y específicamente alienta "seudonimización".

CIDRAM es capaz de seudonimizar las direcciones IP cuando las registra, si es algo que podría necesitar o querer hacer. Cuando CIDRAM seudonimizar de direcciones IP, cuando se registra, el octeto final de las direcciones IPv4, y todo lo que ocurre después de la segunda parte de las direcciones IPv6 está representado por una "x" (redondeando efectivamente las direcciones IPv4 a la dirección inicial de la 24 subred en la que tienen en cuenta, y las direcciones IPv6 a la dirección inicial de la 32 subred en la que tienen en cuenta).

*Nota: El proceso de seudonimización de las direcciones IP en CIDRAM no afecta la función de seguimiento de las direcciones IP en CIDRAM. Si esto es un problema para usted, puede ser mejor desactivar por completo el seguimiento de IP. Esto puede lograrse configurando `track_mode` a `false` y evitando cualquier módulo.*

*Directivas de configuración relevantes:*
- `signatures` -> `track_mode`
- `legal` -> `pseudonymise_ip_addresses`

##### 11.3.6 OMITIENDO INFORMACIÓN DE REGISTRO

Si desea ir un paso más allá al evitar que se registren por completo los tipos de información específicos, también es posible hacerlo. CIDRAM proporciona directivas de configuración para controlar si las direcciones IP, los nombres de host, y los agentes de usuario se incluyen en los registros. De forma predeterminada, los tres puntos de datos se incluyen en los registros cuando están disponibles. Establecer cualquiera de estas directivas de configuración en `true` omite la información correspondiente de los registros.

*Nota: No hay ninguna razón para seudonimizar direcciones IP al omitirlas de los registros por completo.*

*Directivas de configuración relevantes:*
- `legal` -> `omit_ip`
- `legal` -> `omit_hostname`
- `legal` -> `omit_ua`

##### 11.3.7 ESTADÍSTICA

CIDRAM es opcionalmente capaz de rastrear estadísticas tales como el número total de eventos de bloque o instancias de CAPTCHA que han ocurrido desde algún punto particular en el tiempo. Esta característica está deshabilitada de manera predeterminada, pero se puede habilitar a través de la configuración del paquete. Esta característica solo rastrea el número total de eventos ocurridos, y no incluye ninguna información sobre eventos específicos (y por lo tanto, no debe considerarse como PII).

*Directivas de configuración relevantes:*
- `general` -> `statistics`

##### 11.3.8 ENCRIPTACIÓN

CIDRAM no encripta su caché ni ninguna información de registro. [Encriptación](https://es.wikipedia.org/wiki/Cifrado_(criptograf%C3%ADa)) del caché y del registro se puede introducir en el futuro, pero no hay planes actuales para esto. Si le preocupa que terceros no autorizados accedan a partes de CIDRAM que puedan contener PII o información confidencial, como su caché o registros, recomendaría que CIDRAM no se instale en una ubicación de acceso público (por ejemplo, instale CIDRAM fuera del directorio `public_html` o equivalente disponible para la mayoría de los servidores web estándar) y que los permisos apropiadamente restrictivos se apliquen para el directorio donde reside (en particular, para el directorio vault). Si eso no es suficiente para abordar sus inquietudes, configure CIDRAM de forma que los tipos de información que causen sus inquietudes no se recopilen o registrado en primer lugar (por ejemplo, a modo de deshabilitar el registro).

#### 11.4 COOKIES

CIDRAM establece [cookies](https://es.wikipedia.org/wiki/Cookie_(inform%C3%A1tica)) en dos puntos en su base de código. El primer punto, cuando un usuario completa con éxito una instancia de CAPTCHA (y suponiendo que `lockuser` se establece en `true`), CIDRAM establece una cookie para poder recordar, en solicitudes posteriores, que el usuario ya ha completado una instancia de CAPTCHA, de modo que no tendrá que pedir continuamente al usuario que complete una instancia de CAPTCHA en solicitudes posteriores. El segundo punto, cuando un usuario ha iniciado una sesión en el front-end, CIDRAM establece una cookie para poder recordar al usuario para solicitudes posteriores (es decir, las cookies se usan para autenticar al usuario en una sesión).

En ambos casos, las advertencias de cookies se muestran prominentemente (cuando sea aplicable), advirtiendo al usuario que las cookies se establecerán si participan en las acciones pertinentes. Las cookies no se establecen en ningún otro punto en la base de código.

*Nota: Las API CAPTCHA "invisibles" pueden ser incompatibles con las leyes de cookies en algunas jurisdicciones, y debería ser evitada por cualquier sitio web sujeto a dichas leyes. Optar por utilizar las otras API proporcionadas, o simplemente deshabilitar CAPTCHA por completo, puede ser preferible.*

*Directivas de configuración relevantes:*
- `general` -> `disable_frontend`
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 11.5 MARKETING Y PUBLICIDAD

CIDRAM no recopila ni procesa ninguna información con fines comerciales o publicitarios, y tampoco vende ni obtiene ganancias de ninguna información recopilada o registrada. CIDRAM no es una empresa comercial, ni está relacionada con ningún interés comercial, por lo que hacer estas cosas no tendría ningún sentido. Este ha sido el caso desde el comienzo del proyecto, y sigue siendo el caso hoy en día. Además, hacer estas cosas sería contraproducente para el espíritu y el propósito del proyecto como un todo, y mientras continúe manteniendo el proyecto, nunca sucederá.

#### 11.6 POLÍTICA DE PRIVACIDAD

En algunas circunstancias, se le puede exigir legalmente que muestre claramente un enlace a su política de privacidad en todas las páginas y secciones de su sitio web. Esto puede ser importante como un medio para garantizar que los usuarios estén bien informados sobre sus prácticas de privacidad exactas, los tipos de información personal que recopila y cómo piensa utilizarla. Para poder incluir un enlace en la página "Acceso Denegado" de CIDRAM, se proporciona una directiva de configuración para especificar la URL de su política de privacidad.

*Nota: Se recomienda encarecidamente que su página de política de privacidad no quede detrás de la protección de CIDRAM. Si CIDRAM protege su página de política de privacidad, y un usuario bloqueado por CIDRAM hace clic en el enlace a su política de privacidad, se volverá a bloquear y no podrá ver su política de privacidad. Idealmente, debe enlace a una copia estática de su política de privacidad, como una página HTML, o un archivo de texto sin formato que no esté protegido por CIDRAM.*

*Directivas de configuración relevantes:*
- `legal` -> `privacy_policy`

#### 11.7 GDPR/DSGVO

El Reglamento General de Protección de Datos (GDPR) es un reglamento de la Unión Europea, que entra en vigor el 25 Mayo de 2018. El objetivo principal de la regulación es dar control a los ciudadanos y residentes de la UE con respecto a sus propios datos personales, y unificar la regulación dentro de la UE con respecto a la privacidad y los datos personales.

El reglamento contiene disposiciones específicas relativas al procesamiento de [información de identificación personal](https://es.wikipedia.org/wiki/Informaci%C3%B3n_personal) de cualquier "sujeto de datos" (cualquier persona física identificada o identificable) de la UE o dentro de ella. Para cumplir con la regulación, las "empresas" (según lo definido por la regulación) y cualquier sistema y proceso relevante deben implementar "privacidad por diseño" como estándar, debe usar la configuración de privacidad más alta posible, debe implementar las salvaguardas necesarias para cualquier información almacenada o procesada (incluyendo, pero no limitado a, la implementación de seudonimización o anonimización completa de datos), debe declarar clara e inequívocamente los tipos de datos que recopilan, cómo lo procesan, por qué motivos, por cuánto tiempo lo retienen, y si comparten estos datos con terceros, los tipos de datos compartidos con terceros, cómo, por qué, y así sucesivamente.

Los datos no pueden procesarse a menos que haya una base legal para hacerlo, según lo definido por la regulación. Generalmente, esto significa que para procesar los datos de un sujeto de datos de manera legal, debe hacerse de conformidad con las obligaciones legales, o solo después de que se haya obtenido el consentimiento explícito, bien informado e inequívoco del sujeto de los datos.

Debido a que algunos aspectos de la regulación pueden evolucionar en el tiempo, para evitar la propagación de información desactualizada, puede ser mejor aprender sobre la regulación desde una fuente autorizada, en lugar de simplemente incluir la información relevante aquí en la documentación del paquete (que puede con el tiempo se volverá obsoleto a medida que la regulación evolucione).

[EUR-Lex](https://eur-lex.europa.eu/) (una parte del sitio web oficial de la Unión Europea que proporciona información sobre la legislación de la UE) proporciona amplia información sobre GDPR/DSGVO, disponible en 24 idiomas diferentes (al momento de escribir esto), y disponible para su descarga en formato PDF. Definitivamente recomendaría leer la información que proporcionan, para aprender más sobre GDPR/DSGVO:
- [REGLAMENTO (UE) 2016/679 DEL PARLAMENTO EUROPEO Y DEL CONSEJO](https://eur-lex.europa.eu/legal-content/ES/TXT/?uri=celex:32016R0679)

Alternativamente, hay una breve descripción (no autoritativa) de GDPR/DSGVO disponible en Wikipedia:
- [Reglamento General de Protección de Datos](https://es.wikipedia.org/wiki/Reglamento_General_de_Protecci%C3%B3n_de_Datos)

---


Última Actualización: 25 de Marzo de 2022 (2022.03.25).
