## Dokumentation für CIDRAM v3 (Deutsch).

### Inhalt
- 1. [VORWORT](#SECTION1)
- 2. [INSTALLATION](#SECTION2)
- 3. [BENUTZUNG](#SECTION3)
- 4. [FRONTEND-MANAGEMENT](#SECTION4)
- 5. [IM PAKET ENTHALTENE DATEIEN](#SECTION5)
- 6. [EINSTELLUNGEN](#SECTION6)
- 7. [SIGNATURENFORMAT](#SECTION7)
- 8. [BEKANNTE KOMPATIBILITÄTSPROBLEME](#SECTION8)
- 9. [HÄUFIG GESTELLTE FRAGEN (FAQ)](#SECTION9)
- 10. *Reserviert für zukünftige Ergänzungen der Dokumentation.*
- 11. [RECHTSINFORMATION](#SECTION11)

*Hinweis für Übersetzungen: Im Falle von Fehlern (z.B., Diskrepanzen zwischen den Übersetzungen, Tippfehler, u.s.w.), die Englische Version des README als die ursprüngliche und maßgebliche Version ist betrachtet. Wenn Sie irgendwelche Fehler finden, ihre Hilfe bei der Korrektur wäre willkommen.*

---


### 1. <a name="SECTION1"></a>VORWORT

CIDRAM (Classless Inter-Domain Routing Access Manager) ist ein PHP-Skript gestaltete für Websites zu schützen, durch das Blockieren von IP-Adressen als Quellen von unerwünschten Verkehr angesehen, einschließlich (aber nicht beschränkt auf) Datenverkehr von nicht-menschlichen Zugang Endpunkte, Cloud-Services, spambots, Website Schaber, u.s.w. Es tut dies durch die möglichen CIDRs von IP-Adressen zu berechnen, von eingehenden Anfragen geliefert, und dann versuchen, diese gegen ihre Signaturdateien zu entsprechen (Diese Signaturdateien enthalten Listen von CIDRs von IP-Adressen als Ursachen für unerwünschte Verkehrs angesehen); Wenn Übereinstimmungen gefunden werden, die Anfragen ist blockiert.

*(Beziehen auf: [Was ist ein "CIDR"?](#WHAT_IS_A_CIDR)).*

[CIDRAM](https://cidram.github.io/) COPYRIGHT 2016 und darüber hinaus GNU/GPLv2 by [Caleb M (Maikuolan)](https://github.com/Maikuolan).

Dieses Skript ist freie Software; Sie können Sie weitergeben und/oder modifizieren unter den Bedingungen der GNU General Public License, wie von der Free Software Foundation veröffentlicht; entweder unter Version 2 der Lizenz oder (nach Ihrer Wahl) jeder späteren Version. Dieses Skript wird in der Hoffnung verteilt, dass es nützlich sein wird, allerdings OHNE JEGLICHE GARANTIE; ohne implizite Garantien für VERMARKTUNG/VERKAUF/VERTRIEB oder FÜR EINEN BESTIMMTEN ZWECK. Lesen Sie die GNU General Public License für weitere Details, in der Datei `LICENSE.txt`, ebenfalls verfügbar auf:
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

Dieses Dokument und das zugehörige Paket kann von folgenden Links kostenlos heruntergeladen werden:
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [SourceForge](https://sourceforge.net/projects/cidram/).

---


### 2. <a name="SECTION2"></a>INSTALLATION

#### 2.0 MANUELL INSTALLIEREN

1) Entpacken Sie das heruntergeladene Archiv auf Ihren lokalen PC. Erstellen Sie ein Verzeichnis, in welches Sie den Inhalt dieses Paketes auf Ihrem Host oder CMS installieren möchten. Ein Verzeichnis wie `/public_html/cidram/` o.ä. genügt, solange es Ihren Sicherheitsbedürfnissen oder persönlichen Präferenzen entspricht.

2) Die Datei `config.ini.RenameMe` (im `vault`-Verzeichnis) zu `config.ini` umbenennen. Optional (empfohlen für erfahrene Anwender, nicht empfohlen für Anwender ohne entsprechende Kenntnisse), öffnen Sie diese Datei (diese Datei beinhaltet alle funktionalen Optionen für CIDRAM; über jeder Option beschreibt ein kurzer Kommentar die Aufgabe dieser Option). Verändern Sie die Werte nach Ihren Bedürfnissen. Speichern und schließen Sie die Datei.

3) Laden Sie den kompletten Inhalt (CIDRAM und die Dateien) in das Verzeichnis hoch, für das Sie sich in Schritt 1 entschieden haben. Die Dateien `*.txt`/`*.md` müssen nicht mit hochgeladen werden.

4) Ändern Sie die Zugriffsberechtigungen des `vault`-Verzeichnisses auf "755" (wenn es Probleme gibt, Sie können "777" versuchen; Dies ist weniger sicher). Die Berechtigungen des übergeordneten Verzeichnises, in welchem sich der Inhalt befindet (das Verzeichnis, wofür Sie sich entschieden haben), können so belassen werden, überprüfen Sie jedoch die Berechtigungen, wenn in der Vergangenheit Zugriffsprobleme aufgetreten sind (Voreinstellung "755" o.ä.). Zusammenfassend: Damit das Paket ordnungsgemäß funktioniert, muss PHP in der Lage sein, Dateien im `vault`-Verzeichnis zu lesen und zu schreiben. Viele Dinge (Aktualisierung, Protokollierung, u.s.w.) sind nicht möglich, wenn PHP nicht in das `vault`-Verzeichnis schreiben kann, und das Paket funktioniert überhaupt nicht, wenn PHP nicht aus dem `vault`-Verzeichnis lesen kann. Zur optimalen Sicherheit darf das `vault`-Verzeichnis jedoch NICHT öffentlich zugänglich sein (sensible Informationen, wie die in `config.ini` oder `frontend.dat` enthaltenen Informationen, könnten potenziellen Angreifern ausgesetzt offengelegt werden, wenn das `vault`-Verzeichnis öffentlich zugänglich ist).

5) Binden Sie CIDRAM in Ihr System oder CMS ein. Es gibt viele verschiedene Möglichkeiten, ein Script wie CIDRAM einzubinden, am einfachsten ist es, das Script am Anfang einer Haupt-Datei (eine Datei, die immer geladen wird, wenn irgendeine beliebige Seite Ihres Webauftritts aufgerufen wird) Ihres Systems oder CMS mit Hilfe des `require`- oder `include`-Befehls einzubinden. Üblicherweise wird eine solche Datei in Verzeichnissen wie `/includes`, `/assets` or `/functions` gespeichert und wird häufig `init.php`, `common_functions.php`, `functions.php` o.ä. genannt. Sie müssen herausfinden, welche Datei dies für Ihre Bedürfnisse ist; Wenn Sie dabei Schwierigkeiten haben dies herauszufinden, besuchen Sie die CIDRAM Issues-Seiten auf GitHub und lassen Sie es uns wissen; Es ist möglich, dass entweder ich oder ein anderer Benutzer mit dem CMS, das Sie verwenden, Erfahrung hat (Sie müssen Sie mitteilen, welche CMS Sie verwenden) und möglicherweise in der Lage ist, etwas Unterstützung anzubieten. Fügen Sie in dieser Datei folgenden Code direkt am Anfang ein:

`<?php require '/user_name/public_html/cidram/loader.php'; ?>`

Ersetzen Sie den String zwischen den Anführungszeichen mit dem lokalen Pfad der Datei `loader.php`, nicht mit der HTTP-Adresse (ähnlich dem Pfad für das `vault`-Verzeichnis). Speichern und schließen Sie die Datei, laden Sie sie ggf. erneut hoch.

-- ODER ALTERNATIV --

Wenn Sie den Apache-Webserver verwenden oder wenn Sie Zugriff auf die `php.ini` oder eine ähnliche Datei haben, dann können Sie die `auto_prepend_file` Direktive verwenden um CIDRAM immer einzubinden wenn eine PHP-Anfrage erfolgt. Ungefähr so:

`auto_prepend_file = "/user_name/public_html/cidram/loader.php"`

Oder in der `.htaccess` Datei:

`php_value auto_prepend_file "/user_name/public_html/cidram/loader.php"`

6) Das ist alles! :-)

#### 2.1 INSTALLATION MIT COMPOSER

Da [CIDRAM bei Packagist registriert ist](https://packagist.org/packages/cidram/cidram), können Sie CIDRAM auch mittels Composer installieren. Allerdings müssen sie immer noch die Hooks und die Konfiguration vorbereiten. Siehe manuell installieren, Schritt 2, 4 und 5.

`composer require cidram/cidram`

#### 2.2 FÜR WORDPRESS INSTALLIEREN

Wenn Sie CIDRAM mit WordPress verwenden möchten, können Sie alle oben genannten Anweisungen ignorieren. Da [CIDRAM als Plugin in der WordPress Plugin Datenbank registriert ist](https://wordpress.org/plugins/cidram/) können Sie CIDRAM direkt aus dem Plugins-Dashboard installieren. CIRDAM kann auf demselben Wege wie jedes andere Plugin installiert werden, es sind keine weiteren Schritte erforderlich. Genauso wie bei den anderen Installationsmethoden, können Ihre Installation anpassen, indem Sie den Inhalt der `config.ini`-Datei anpassen. Alternativ können Sie auch die Frontend-Konfigurationsseite verwenden. Wenn Sie das Frontend für CIDRAM aktivieren und CIDRAM mit der Frontend-Aktualisierungsseite aktualisieren, dies wird automatisch mit den Plugin-Versionsinformationen synchronisiert, die im Plugins-Dashboard angezeigt werden.

*Warnung: Die Aktualisierung von CIDRAM über das Plugins-Dashboard führt zu einer sauberen Installation! Wenn Sie Ihre Installation angepasst haben (modifizierte Konfiguration, installierte Module, u.s.w.), gehen Anpassungen bei einer Aktualisierung über das Plugins-Dashboard verloren! Protokolldateien werden dabei ebenfalls gelöscht! Um Protokolldateien und Anpassungen zu erhalten, aktualisieren Sie CIDRAM über die CIDRAM-Frontend-Aktualisierungsseite.*

---


### 3. <a name="SECTION3"></a>BENUTZUNG

CIDRAM sollte automatisch unerwünschte Verkehr auf Ihre Website blockieren, ohne manuelle Unterstützung erforderlich, abgesehen von seiner Erstinstallation.

Sie können Ihre Konfiguration anpassen, und Sie können welche CIDRs blockiert festlegen, durch Sie Ihre Konfigurationsdatei und/oder Signaturdateien Modifizieren.

Wenn Sie Falsch-Positivs begegnen, bitte kontaktieren Sie mich zu informieren. *(Beziehen auf: [Was ist ein "Falsch-Positiv"?](#WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM kann manuell oder über das Frontend aktualisiert werden. CIDRAM kann auch über Composer oder WordPress aktualisiert werden, wenn es ursprünglich mit diesen Mitteln installiert wurde.

---


### 4. <a name="SECTION4"></a>FRONTEND-MANAGEMENT

#### 4.0 WAS IST DAS FRONTEND.

Das Frontend bietet eine bequeme und einfache Möglichkeit, für Ihre CIDRAM-Installation zu pflegen, zu verwalten und zu aktualisieren. Sie können Protokolldateien über die Protokollseite anzeigen, teilen und herunterladen, Sie können die Konfiguration über die Konfigurationsseite ändern, Sie können Komponenten über die Aktualisierungsseite installieren und deinstallieren, und Sie können Dateien in Ihrem vault über den Dateimanager hochladen, herunterladen und ändern.

Das Frontend ist standardmäßig deaktiviert, um unautorisiert Zugriff zu verhindern (unautorisiert Zugriff könnte erhebliche Konsequenzen für Ihre Website und ihre Sicherheit haben). Aktivieren Sie es, indem Sie die unten aufgeführten Anweisungen befolgen.

#### 4.1 WIE AKTIVIEREN SIE DAS FRONTEND.

1) Finden Sie die `disable_frontend`-Direktive in der Datei `config.ini`, und setzen Sie diese auf `false` (standardmäßig `true`).

2) Greifen Sie auf die `loader.php` aus Ihrem Browser zu (z.B., `http://localhost/cidram/loader.php`).

3) Loggen Sie sich mit dem standardmäßig Benutzernamen und Passwort ein (admin/password).

Hinweis: **Um unautorisierten zugriff auf das Frontend zu verhindern, sollten sie sofort nach dem ersten Login ihren Benutzernamen und Passwort ändern. Dies ist notwendig, da mithilfe des Frontend möglich ist, beliebigen PHP-Code auf Ihre Webseite hochzuladen.**

Für eine optimale Sicherheit wird außerdem empfohlen, die "Zwei-Faktor-Authentifizierung" für alle Frontend-Konten zu aktivieren (Anweisungen unten).

#### 4.2 WIE MAN DAS FRONTEND BENUTZT.

Anweisungen sind auf jeder Seite des Frontends vorhanden, um die richtige Verwendung und den vorgesehenen Zweck zu erläutern. Wenn Sie weitere Erklärungen oder spezielle Hilfe benötigen, wenden Sie sich bitte an den Support. Alternativ gibt es einige Videos auf YouTube, die durch Demonstration helfen könnten.

#### 4.3 ZWEI-FAKTOR-AUTHENTIFIZIERUNG

Es ist möglich, das Frontend sicherer zu machen, indem Sie die Zwei-Faktor-Authentifizierung ("2FA") aktivieren. Wenn Sie sich bei einem 2FA-aktivierten Konto eingeloggt, wird eine E-Mail an die zugehörige E-Mail-Adresse gesendet. Diese E-Mail enthält einen "2FA-Code", den der Nutzer zusätzlich zum Benutzernamen und Passwort eingeben muss, um sich mit diesem Konto einloggen zu können. Das bedeutet, dass das Erlangen eines Kontopassworts nicht ausreicht, um ein Konto zu übernehmen, da sie auch bereits Zugriff auf die mit diesem Konto verknüpfte E-Mail-Adresse haben müssen, um den mit der Sitzung verbundenen 2FA-Code empfangen und verwenden zu können, dadurch wird das Frontend sicherer.

Um die Zwei-Faktor-Authentifizierung zu aktivieren, verwenden Sie zunächst die Frontend-Aktualisierungsseite, um die PHPMailer-Komponente zu installieren. CIDRAM verwendet PHPMailer zum Senden von E-Mails. Hinweis: Obwohl CIDRAM selbst mit `PHP >= 5.4.0` kompatibel ist, benötigt PHPMailer `PHP >= 5.5.0`. Daher ist eine Zwei-Faktor-Authentifizierung für das CIDRAM-Frontend auf `PHP 5.4` CIDRAM Installationen nicht möglich.

Nachdem Sie PHPMailer installiert haben, müssen Sie die Konfigurationsdirektiven für PHPMailer über die CIDRAM-Konfigurationsseite oder Konfigurationsdatei ausfüllen. Weitere Informationen zu diesen Konfigurationsanweisungen finden Sie im [Konfigurationsabschnitt](#SECTION6) dieses Dokuments. Nachdem Sie die PHPMailer-Konfigurationsdirektiven gefüllt haben, setzen Sie `enable_two_factor` auf `true`. Die Zwei-Faktor-Authentifizierung sollte jetzt aktiviert sein.

Nächster, müssen Sie eine E-Mail-Adresse mit einem Konto verknüpfen, damit CIDRAM bei der Einloggen mit diesem Konto weiß, wohin die 2FA-Codes gesendet werden müssen. Um dies zu tun, verwenden Sie die E-Mail-Adresse als Nutzername für das Konto (wie `foo@bar.tld`), oder formatieren sie den Nutzernamen wie in Emails üblich (wie `Foo Bar <foo@bar.tld>`).

Hinweis: Besonders wichtig ist hier der Schutz Ihres Vault vor unbefugtem Zugriff (z.B., durch die Stärkung der Sicherheit Ihres Servers und die Einschränkung der öffentlichen Zugriffsrechte), da ein unbefugter Zugriff auf Ihre Konfigurationsdatei (die in Ihrem Vault gespeichert ist), Ihre Einstellungen für ausgehenden SMTP (einschließlich SMTP-Benutzername und Passwort) gefährden könnte. Sie sollten sicherstellen, dass Ihr Vault ordnungsgemäß gesichert ist, bevor Sie die Zwei-Faktor-Authentifizierung aktivieren. Wenn dies nicht möglich ist, sollten Sie zumindest ein neues E-Mail-Konto erstellen, das speziell für diesen Zweck vorgesehen ist, um die mit freiliegenden SMTP-Einstellungen verbundenen Risiken zu verringern.

---


### 5. <a name="SECTION5"></a>IM PAKET ENTHALTENE DATEIEN

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


### 6. <a name="SECTION6"></a>EINSTELLUNGEN

Nachfolgend finden Sie eine Liste der Variablen in der Konfigurationsdatei (`config.ini`) mit einer kurzen Beschreibung ihrer Funktionen.

```
Konfiguration (v3)
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

#### "general" (Kategorie)
Allgemeine Konfiguration (jede Kernkonfiguration, die nicht zu anderen Kategorien gehört).

##### "logfile" `[string]`
- Name einer Datei in welcher Menschenlesbar alle blockierten zugriffsversuche protokolliert werden. Geben Sie einen Dateinamen an oder lassen Sie die Option zum Deaktivieren leer.

##### "logfile_apache" `[string]`
- Name einer Apache-Stil-Datei in welcher alle blockierten zugriffsversuche protokolliert werden. Geben Sie einen Dateinamen an oder lassen Sie die Option zum Deaktivieren leer.

##### "logfile_serialized" `[string]`
- Name einer Datei zu protokollieren alle blockierten Zugriffsversuche (Format ist serialisiert). Geben Sie einen Dateinamen an oder lassen Sie die Option zum Deaktivieren leer.

##### "error_log" `[string]`
- Einer Datei zum Protokollieren aller erkannten Fehler, die nicht schwerwiegend sind. Geben Sie einen Dateinamen an oder lassen Sie die Option zum Deaktivieren leer.

##### "stages" `[string]`
- Kontrollen für die Phasen der Ausführungskette (ob aktiviert, ob Fehler protokolliert, u.s.w.).

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
- Kontrollen für die Felder während Blockereignissen (wenn eine Anfrage blockiert wird).

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
- Protokolldateien kürzen wenn diese eine bestimmte Größe erreichen? Wert ist die maximale Größe in B/KB/MB/GB/TB, die eine Protokolldatei erreichen kann, bevor sie gekürtzt wird. Der Standardwert von 0KB deaktiviert die Kürzung (Protokolldateien können unbegrenzt wachsen). Beachten: Gilt für einzelne Protokolldateien! Die Größe der Protokolldateien gilt nicht in der Summe aller Protokolldateien.

##### "log_rotation_limit" `[int]`
- Die Protokollrotation begrenzt die Anzahl der Protokolldateien, die gleichzeitig vorhanden sein dürfen. Wenn neue Protokolldateien erstellt werden, und wenn die Gesamtzahl der Protokolldateien den angegebenen Limit überschreitet, wird die angegebene Aktion ausgeführt. Sie können hier das gewünschte Limit angeben. Ein Wert von 0 deaktiviert die Protokollrotation.

##### "log_rotation_action" `[string]`
- Die Protokollrotation begrenzt die Anzahl der Protokolldateien, die gleichzeitig vorhanden sein sollten. Wenn neue Protokolldateien erstellt werden, und wenn die Gesamtzahl der Protokolldateien den angegebenen Limit überschreitet, wird die angegebene Aktion ausgeführt. Sie können hier die gewünschte Aktion angeben. Delete = Löschen Sie die ältesten Protokolldateien, bis das Limit nicht mehr überschritten wird. Archive = Zuerst archivieren, und dann löschen Sie die ältesten Protokolldateien, bis das Limit nicht mehr überschritten wird.

```
log_rotation_action
├─Delete ("Delete")
└─Archive ("Archive")
```

##### "timezone" `[string]`
- Gibt welche Zeitzone verwendet werden soll an (z.B., Africa/Cairo, America/New_York, Asia/Tokyo, Australia/Perth, Europe/Berlin, Pacific/Guam, u.s.w.). Damit PHP dies automatisch für Sie erledigt, geben Sie "SYSTEM" an.

```
timezone
├─SYSTEM ("System Standard-Zeitzone verwenden.")
├─UTC ("UTC")
└─…Andere
```

##### "time_offset" `[int]`
- Zeitzonenversatz in Minuten.

##### "time_format" `[string]`
- Das Datumsformat verwendet von CIDRAM. Zusätzliche Optionen können auf Anfrage hinzugefügt werden.

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
└─…Andere
```

##### "ipaddr" `[string]`
- Ort der IP-Adresse der aktuellen Verbindung im gesamten Datenstrom (nützlich für Cloud-Services). Standardeinstellung = REMOTE_ADDR. ACHTUNG: Ändern Sie diesen Wert nur, wenn Sie wissen, was Sie tun!

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (Standardeinstellung)")
└─…Andere
```

Siehe auch:
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### "http_response_header_code" `[int]`
- Welche HTTP-Status-Message sollte CIDRAM senden, wenn Anfragen blockiert werden? (Bitte beachten Sie die Dokumentation).

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
- Anstatt die „Zugriff verweigert“ Meldung auszugeben, sollte CIDRAM leise die Zugriffe umleiten? Wenn ja, geben Sie den Speicherort an auf welchen die Zugriffe umgeleitet werden sollen. Wenn nein, diese Variable leer lassen.

##### "lang" `[string]`
- Gibt die Standardsprache für CIDRAM an.

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
- Nach HTTP_ACCEPT_LANGUAGE lokalisieren wann möglich? True = Ja [Standardeinstellung]; False = Nein.

##### "numbers" `[string]`
- Wie willst du Nummern anzeigen? Wählen Sie das Beispiel aus, das Ihnen am besten entspricht.

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
- Wenn Sie möchten, können Sie hier eine E-Mail-Adresse angeben, geben auf den Benutzern wenn sie blockiert, für Unterstützung für den Fall dass sie ist blockiert versehentlich oder im fehler. WARNUNG: Jede E-Mail-Adresse die Sie hier angeben wird sicherlich durch Spambots erworben werden im Zuge ihrer Verwendung hier, und so, es wird dringend empfohlen, wenn Sie hier eine E-Mail-Adresse angeben, dass die E-Mail-Adresse die Sie hier angeben, eine Einwegadresse ist, und/oder eine Adresse die Sie nichts dagegen haben Spam (mit anderen Worten, möchten Sie wahrscheinlich nicht Ihre primären persönlichen oder primären geschäftlichen E-Mail-Adressen verwenden).

##### "emailaddr_display_style" `[string]`
- Wie möchten Sie die E-Mail-Adresse für die Nutzer anzeigen?

```
emailaddr_display_style
├─default ("field_clickable_link")
└─noclick ("field_nonclickable_text")
```

##### "disable_frontend" `[bool]`
- Frontend-Access deaktivieren? Frontend-Access kann CIDRAM einfacher zu handhaben machen, aber es kann auch ein potentielles Sicherheitsrisiko sein. Es wird empfohlen, wenn möglich, CIDRAM über die Back-End-Access zu verwalten, aber Frontend-Access ist für den Fall vorgesehen, wenn dies nicht möglich ist. Halten Sie es deaktiviert außer wenn Sie es brauchen. False = Frontend-Access aktivieren; True = Frontend-Access deaktivieren [Standardeinstellung].

##### "max_login_attempts" `[int]`
- Maximale Anzahl der Versucht zum Anmelden (Frontend). Standardeinstellung = 5.

##### "frontend_log" `[string]`
- Datei für die Protokollierung von Frontend Anmelde-Versuchen. Geben Sie einen Dateinamen an oder lassen Sie die Option zum Deaktivieren leer.

##### "signatures_update_event_log" `[string]`
- Einer Datei zum Protokollieren wenn Signaturen über das Front-End aktualisiert werden. Geben Sie einen Dateinamen an oder lassen Sie die Option zum Deaktivieren leer.

##### "ban_override" `[int]`
- Überschreiben "http_response_header_code" Wenn "infraction_limit" überschritten wird? Beim überschreiben: Blockierte Anfragen geben eine leere Seite zurück (Template-Dateien werden nicht verwendet). 200 = Nicht überschreiben [Standardeinstellung]. Andere Werte entsprechen den verfügbaren Werten für "http_response_header_code".

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
- Sollen auch blockierte Anfragen von verbannten IPs protokolliert werden? True = Ja [Standardeinstellung]; False = Nein.

##### "default_dns" `[string]`
- Eine durch Kommata getrennte Liste von DNS-Servern, die für Hostnamen-Lookups verwendet werden sollen. Standardeinstellung = "8.8.8.8,8.8.4.4" (Google DNS). ACHTUNG: Ändern Sie diesen Wert nur, wenn Sie wissen, was Sie tun!

##### "search_engine_verification" `[string]`
- Kontrollen für die Verifizierung von Anfragen von Suchmaschinen.

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

__Was sind „Positive“ und „Negative“?__ Das erfolgreiche Ergebnis der Verifizierung der durch eine Anfrage präsentierten Identität könnte als „positiv“ oder „negativ“ beschrieben werden. In dem Fall dass die präsentierte Identität als die wahre Identität bestätigt wird, würde sie als „positiv“ bezeichnet werden. In dem Fall dass die präsentierten Identität als gefälscht bestätigt, würde sie als „negativ“ bezeichnet werden. Ein erfolgloses Ergebnis (z.B., die Verifizierung fehlschlägt, oder die Echtheit der präsentierten Identität kann nicht festgestellt werden) würde jedoch nicht als „positiv“ oder „negativ“ beschrieben. Stattdessen würde ein erfolgloses Ergebnis einfach als nicht verifiziert beschrieben. Wenn kein Versuch unternommen wird für die durch eine Anfrage präsentierte Identität zu verifizieren, würde die Anfrage ebenfalls als nicht verifiziert beschrieben. Die Begriffe sind nur in dem Kontext sinnvoll, in dem die durch eine Anfrage präsentierte Identität anerkannt wird und daher der Verifizierung möglich ist. In dem Fall in denen die präsentierte Identität nicht mit den oben bereitgestellten Optionen übereinstimmt, oder wenn keine Identität präsentiert wird, werden die oben bereitgestellten Optionen irrelevant.

__Was sind „Single-Hit-Bypässe“?__ In einigen Fällen kann eine positiv verifizierte Anfrage aufgrund der Signaturdateien, Module, oder anderer Bedingungen der Anfrage immer noch blockiert werden, und Bypässe können erforderlich sein um Falsch-Positive zu vermeiden. In dem Fall in dem eine Bypass genau einen Verstoß behandeln beabsichtigt ist, nicht mehr und nicht weniger, könnte solche eine Bypass als „Single-Hit-Bypass“ beschrieben werden.

##### "social_media_verification" `[string]`
- Kontrollen für die Verifizierung von Anfragen von Social-Media-Plattformen.

```
social_media_verification
├─Embedly ("Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("Pinterest")
└─Twitterbot ("Twitterbot")
```

__Was sind „Positive“ und „Negative“?__ Das erfolgreiche Ergebnis der Verifizierung der durch eine Anfrage präsentierten Identität könnte als „positiv“ oder „negativ“ beschrieben werden. In dem Fall dass die präsentierte Identität als die wahre Identität bestätigt wird, würde sie als „positiv“ bezeichnet werden. In dem Fall dass die präsentierten Identität als gefälscht bestätigt, würde sie als „negativ“ bezeichnet werden. Ein erfolgloses Ergebnis (z.B., die Verifizierung fehlschlägt, oder die Echtheit der präsentierten Identität kann nicht festgestellt werden) würde jedoch nicht als „positiv“ oder „negativ“ beschrieben. Stattdessen würde ein erfolgloses Ergebnis einfach als nicht verifiziert beschrieben. Wenn kein Versuch unternommen wird für die durch eine Anfrage präsentierte Identität zu verifizieren, würde die Anfrage ebenfalls als nicht verifiziert beschrieben. Die Begriffe sind nur in dem Kontext sinnvoll, in dem die durch eine Anfrage präsentierte Identität anerkannt wird und daher der Verifizierung möglich ist. In dem Fall in denen die präsentierte Identität nicht mit den oben bereitgestellten Optionen übereinstimmt, oder wenn keine Identität präsentiert wird, werden die oben bereitgestellten Optionen irrelevant.

__Was sind „Single-Hit-Bypässe“?__ In einigen Fällen kann eine positiv verifizierte Anfrage aufgrund der Signaturdateien, Module, oder anderer Bedingungen der Anfrage immer noch blockiert werden, und Bypässe können erforderlich sein um Falsch-Positive zu vermeiden. In dem Fall in dem eine Bypass genau einen Verstoß behandeln beabsichtigt ist, nicht mehr und nicht weniger, könnte solche eine Bypass als „Single-Hit-Bypass“ beschrieben werden.

** Erfordert ASN-Lookup-Funktionalität (z.B., über das BGPView-Modul).

##### "other_verification" `[string]`
- Kontrollen für die Verifizierung die anderer Arten von Anfragen sofern möglich.

```
other_verification
├─AdSense ("AdSense")
├─AmazonAdBot ("AmazonAdBot")
└─Grapeshot ("Oracle Data Cloud Crawler")
```

__Was sind „Positive“ und „Negative“?__ Das erfolgreiche Ergebnis der Verifizierung der durch eine Anfrage präsentierten Identität könnte als „positiv“ oder „negativ“ beschrieben werden. In dem Fall dass die präsentierte Identität als die wahre Identität bestätigt wird, würde sie als „positiv“ bezeichnet werden. In dem Fall dass die präsentierten Identität als gefälscht bestätigt, würde sie als „negativ“ bezeichnet werden. Ein erfolgloses Ergebnis (z.B., die Verifizierung fehlschlägt, oder die Echtheit der präsentierten Identität kann nicht festgestellt werden) würde jedoch nicht als „positiv“ oder „negativ“ beschrieben. Stattdessen würde ein erfolgloses Ergebnis einfach als nicht verifiziert beschrieben. Wenn kein Versuch unternommen wird für die durch eine Anfrage präsentierte Identität zu verifizieren, würde die Anfrage ebenfalls als nicht verifiziert beschrieben. Die Begriffe sind nur in dem Kontext sinnvoll, in dem die durch eine Anfrage präsentierte Identität anerkannt wird und daher der Verifizierung möglich ist. In dem Fall in denen die präsentierte Identität nicht mit den oben bereitgestellten Optionen übereinstimmt, oder wenn keine Identität präsentiert wird, werden die oben bereitgestellten Optionen irrelevant.

__Was sind „Single-Hit-Bypässe“?__ In einigen Fällen kann eine positiv verifizierte Anfrage aufgrund der Signaturdateien, Module, oder anderer Bedingungen der Anfrage immer noch blockiert werden, und Bypässe können erforderlich sein um Falsch-Positive zu vermeiden. In dem Fall in dem eine Bypass genau einen Verstoß behandeln beabsichtigt ist, nicht mehr und nicht weniger, könnte solche eine Bypass als „Single-Hit-Bypass“ beschrieben werden.

##### "protect_frontend" `[bool]`
- Gibt an, ob die Schutzmaßnahmen normalerweise vom CIDRAM bereitgestellten auf das Frontend angewendet werden sollen. True = Ja [Standardeinstellung]; False = Nein.

##### "default_algo" `[string]`
- Definiert den Algorithmus für alle zukünftigen Passwörter und Sitzungen.

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### "statistics" `[string]`
- Kontrollen für welche statistischen Informationen nachverfolgt werden sollen.

```
statistics
├─Blocked-IPv4 ("Anfragen blockiert – IPv4")
├─Blocked-IPv6 ("Anfragen blockiert – IPv6")
├─Blocked-Other ("Anfragen blockiert – Andere")
├─Banned-IPv4 ("Anfragen verbannt – IPv4")
├─Banned-IPv6 ("Anfragen verbannt – IPv6")
├─Passed-IPv4 ("Anfragen erlaubt – IPv4")
├─Passed-IPv6 ("Anfragen erlaubt – IPv6")
├─Passed-Other ("Anfragen erlaubt – Andere")
├─CAPTCHAs-Failed ("CAPTCHA versucht – {state_failed}")
└─CAPTCHAs-Passed ("CAPTCHA versucht – {state_passed}")
```

##### "force_hostname_lookup" `[bool]`
- Hostnamen-Suchen werden normalerweise auf einer "wie benötigt"-Basis durchgeführt, können jedoch für alle Anforderungen erzwungen werden. Dies kann nützlich sein, um detailliertere Informationen in der Protokolldateien bereitzustellen, aber auch kann sich leicht negativ auf die Performance auswirken. Erzwinge Hostnamen-Suche? True = Ja; False = Nein [Standardeinstellung].

##### "allow_gethostbyaddr_lookup" `[bool]`
- gethostbyaddr-Suche erlauben, wenn UDP nicht verfügbar ist? True = Ja [Standardeinstellung]; False = Nein.

Hinweis: IPv6-Lookups funktionieren auf einigen 32-Bit-Systemen möglicherweise nicht richtig.

##### "log_sanitisation" `[bool]`
- Wenn Sie die Frontend Protokolldateien-Seite verwenden, um Protokolldaten anzuzeigen, saniert CIDRAM die Protokolldaten vor der Anzeige, um Benutzer vor XSS-Angriffen und anderen potenziellen Bedrohungen zu schützen, die Protokolldaten enthalten könnten. Standardmäßig werden Daten während der Protokollierung jedoch nicht saniert. Dadurch wird sichergestellt, dass die Protokolldaten genau aufbewahrt werden, um eine eventuell erforderliche heuristische oder forensische Analyse zu unterstützen. Falls jedoch ein Benutzer versucht, Protokolldaten mit externen Werkzeuge zu lesen, und wenn diese externen Werkzeuge keinen eigenen Sanierungsprozess durchführen, der Benutzer könnte XSS-Angriffen ausgesetzt sein. Bei Bedarf können Sie das Standardverhalten mithilfe dieser Konfigurationsanweisung ändern. True = Sanieren der Daten, wenn der Daten protokolliert (Daten werden weniger genau aufbewahrt, jedoch das XSS-Risiko ist geringer). False = Sanieren der Daten nicht, wenn der Daten protokolliert (Daten werden genauer aufbewahrt, jedoch das XSS-Risiko ist höher) [Standardeinstellung].

##### "disabled_channels" `[string]`
- Dies kann verwendet werden, um zu verhindern, dass CIDRAM beim Senden von Anforderungen bestimmte Kanäle verwendet (z.B., beim Aktualisieren, beim Abrufen von Komponentenmetadaten, u.s.w.).

```
disabled_channels
├─GitHub ("GitHub")
├─BitBucket ("BitBucket")
└─GoogleDNS ("GoogleDNS")
```

##### "default_timeout" `[int]`
- Standardzeitlimit für externe Anforderungen? Standardeinstellung = 12 Sekunden.

##### "config_imports" `[string]`
- Eine durch Kommata getrennte Liste von Dateien, die in die CIDRAM-Standardkonfiguration importiert werden sollen. Wird normalerweise von der Aktualisierungsseite nach Bedarf ausgefüllt wenn Komponenten aktiviert werden. In den meisten Fällen kann es ignorieren.

##### "events" `[string]`
- Hier aufgelistete Dateien werden direkt nach der Ereignishandlerdatei geladen. Wird normalerweise von der Aktualisierungsseite nach Bedarf ausgefüllt wenn Komponenten aktiviert werden. In den meisten Fällen kann es ignorieren.

#### "signatures" (Kategorie)
Konfiguration für Signaturen, Signaturdateien, Module, u.s.w.

##### "ipv4" `[string]`
- Eine Liste der IPv4-Signaturdateien, die CIDRAM zu analysieren versuchen sollte, getrennt durch Kommas. Hier können Sie Einträge hinzufügen, wenn Sie zusätzliche IPv4-Signaturdateien in CIDRAM aufnehmen möchten.

##### "ipv6" `[string]`
- Eine Liste der IPv6-Signaturdateien, die CIDRAM zu analysieren versuchen sollte, getrennt durch Kommas. Hier können Sie Einträge hinzufügen, wenn Sie zusätzliche IPv6-Signaturdateien in CIDRAM aufnehmen möchten.

##### "block_attacks" `[bool]`
- Blockieren Sie CIDRs, die mit Angriffen und anderem abnormalem Datenverkehr verbunden sind? z.B., Port-Scans, Hacking, Sondieren nach Schwachstellen, u.s.w. Solange Sie keine Probleme haben während Sie dies tun, allgemein, dies immer auf true sollte gesetzt sein.

##### "block_cloud" `[bool]`
- CIDRs blockieren, welche zu Web-/Server- Hostern gehören. Wenn Sie eine API betreiben oder erwarten, dass Sie oft Aufrufe von solchen Servern bekommen sollten Sie diese Option auf false (nicht blockieren) setzen. Wenn Sie solche Anfragen blockieren möchten, setzen Sie diese Option auf true [Standarteinstellung].

##### "block_bogons" `[bool]`
- Blockieren Sie Bogon/Martian CIDRs? Wenn Sie Verbindungen zu Ihrer Website von localhost, von Ihrem LAN, oder von innerhalb Ihres lokalen Netzwerks erwarten, diese Richtlinie auf false sollte gesetzt werden. Wenn Sie diese Verbindungen nicht erwarten, dies auf true sollte gesetzt werden.

##### "block_generic" `[bool]`
- Blockieren Sie CIDRs allgemein empfohlen für eine schwarze Liste? Dies gilt für alle Signaturen, die nicht als Teil einer der anderen spezifischen Signaturkategorien markiert sind.

##### "block_legal" `[bool]`
- Blockieren Sie CIDRs als Antwort auf gesetzliche Verpflichtungen? Diese Richtlinie sollte normalerweise keine Wirkung haben, da CIDRAM standardmäßig keine CIDRs mit "gesetzliche Verpflichtungen" assoziiert, aber es existiert dennoch als zusätzliche Kontrollmaßnahme für den Vorteil von benutzerdefinierten Signaturdateien oder Modulen, die aus gesetzlichen Gründen existieren könnten.

##### "block_malware" `[bool]`
- Blockieren Sie CIDRs in Verbindung mit Malware? Dazu gehören C&C-Server, infizierte Computer, Malware-Verteilung beteiligte Computer, u.s.w.

##### "block_proxies" `[bool]`
- Blockieren Sie CIDRs identifiziert als zu Proxy-Dienste oder VPNs gehören? Wenn Sie benötigen dass Benutzer auf Ihre Website von Proxy-Dienste und VPNs zugreifen können, diese Richtlinie auf false sollte gesetzt werden. Andernfalls, Wenn Sie Proxy-Dienste oder VPNs nicht benötigen, diese Richtlinie auf true sollte gesetzt werden, als Mittel zur Verbesserung der Sicherheit.

##### "block_spam" `[bool]`
- Blockieren Sie CIDRs identifiziert als ein hohem Risiko für Spam? Solange Sie keine Probleme haben während Sie dies tun, allgemein, dies immer auf true sollte gesetzt sein.

##### "modules" `[string]`
- Eine Liste der Moduldateien zu laden nach der Prüfung der IPv4/IPv6-Signaturen, durch Kommas begrenzt.

##### "default_tracktime" `[int]`
- Wie viele Sekunden sollen durch Module blockierte IPs getrackt werden? Standardeinstellung = 604800 (1 Woche).

##### "infraction_limit" `[int]`
- Maximale Anzahl von Verstöße, die eine IP zulassen darf, bevor sie durch IP-Tracking verbannt ist. Standardeinstellung = 10.

##### "tracking_override" `[bool]`
- Sollten Module erlaubt sein Tracking-Optionen zu überschreiben? True = Ja [Standardeinstellung]; False = Nein.

#### "recaptcha" (Kategorie)
Konfiguration für ReCaptcha (bietet eine Möglichkeit für Menschen den Zugang wiederherzustellen, wenn sie blockiert sind).

##### "usemode" `[int]`
- Wann sollte das CAPTCHA angeboten werden? Hinweis: Whitelist markierte oder verifizierte und nicht blockierte Anfragen müssen niemals ein CAPTCHA abschließen. Auch: CAPTCHAs können eine nützliche zusätzliche Schutzebene gegen Bots und verschiedene Arten von böswilligen automatisierten Anfragen bieten, aber bieten keinen Schutz gegen böswilligen Menschen.

```
usemode
├─0 (Noch nie !!!)
├─1 (Nur wenn blockiert, innerhalb des Signaturgrenze, und nicht verbannt.)
├─2 (Nur wenn blockiert, speziell für die Verwendung markiert, innerhalb der Signaturgrenze, und nicht verbannt.)
├─3 (Nur wenn innerhalb des Signaturgrenze, und nicht verbannt (unabhängig ob blockiert).)
├─4 (Nur wenn nicht blockiert.)
└─5 (Nur wenn nicht blockiert, oder wenn speziell für die Verwendung markiert, innerhalb der Signaturgrenze, und nicht verbannt.)
```

##### "lockip" `[bool]`
- Sperren Sie CAPTCHA auf IPs?

##### "lockuser" `[bool]`
- Sperren Sie CAPTCHA auf Benutzer?

##### "sitekey" `[string]`
- Dieser Wert befindet sich im Dashboard für Ihren CAPTCHA-Dienst.

Siehe auch:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "secret" `[string]`
- Dieser Wert befindet sich im Dashboard für Ihren CAPTCHA-Dienst.

Siehe auch:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "expiry" `[float]`
- Anzahl der Stunden an die sich CAPTCHA-Instanzen erinnern sollten. Standardeinstellung = 720 (1 Monat).

##### "logfile" `[string]`
- Protokollieren Sie alle CAPTCHA versucht? Geben Sie einen Dateinamen an oder lassen Sie die Option zum Deaktivieren leer.

##### "signature_limit" `[int]`
- Maximal zulässige Anzahl von Signaturen, bevor das CAPTCHA-Angebot zurückgezogen wird. Standardeinstellung = 1.

##### "api" `[string]`
- Welche API soll verwendet werden?

```
api
├─V2 ("V2 (Kontrollkästchen)")
└─Invisible ("V2 (Unsichtbar)")
```

##### "show_cookie_warning" `[bool]`
- Cookie-Warnung anzeigen? True = Ja [Standardeinstellung]; False = Nein.

##### "show_api_message" `[bool]`
- API-Nachricht anzeigen? True = Ja [Standardeinstellung]; False = Nein.

##### "nonblocked_status_code" `[int]`
- Welcher Statuscode sollte verwendet werden, wenn nicht-blockierte CAPTCHAs Anforderungen angezeigt werden?

```
nonblocked_status_code
├─200 (200 OK)
├─403 (403 Forbidden)
├─418 (418 I'm a teapot)
├─429 (429 Too Many Requests)
└─451 (451 Unavailable For Legal Reasons)
```

#### "hcaptcha" (Kategorie)
Konfiguration für HCaptcha (bietet eine Möglichkeit für Menschen den Zugang wiederherzustellen, wenn sie blockiert sind).

##### "usemode" `[int]`
- Wann sollte das CAPTCHA angeboten werden? Hinweis: Whitelist markierte oder verifizierte und nicht blockierte Anfragen müssen niemals ein CAPTCHA abschließen. Auch: CAPTCHAs können eine nützliche zusätzliche Schutzebene gegen Bots und verschiedene Arten von böswilligen automatisierten Anfragen bieten, aber bieten keinen Schutz gegen böswilligen Menschen.

```
usemode
├─0 (Noch nie !!!)
├─1 (Nur wenn blockiert, innerhalb des Signaturgrenze, und nicht verbannt.)
├─2 (Nur wenn blockiert, speziell für die Verwendung markiert, innerhalb der Signaturgrenze, und nicht verbannt.)
├─3 (Nur wenn innerhalb des Signaturgrenze, und nicht verbannt (unabhängig ob blockiert).)
├─4 (Nur wenn nicht blockiert.)
└─5 (Nur wenn nicht blockiert, oder wenn speziell für die Verwendung markiert, innerhalb der Signaturgrenze, und nicht verbannt.)
```

##### "lockip" `[bool]`
- Sperren Sie CAPTCHA auf IPs?

##### "lockuser" `[bool]`
- Sperren Sie CAPTCHA auf Benutzer?

##### "sitekey" `[string]`
- Dieser Wert befindet sich im Dashboard für Ihren CAPTCHA-Dienst.

Siehe auch:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "secret" `[string]`
- Dieser Wert befindet sich im Dashboard für Ihren CAPTCHA-Dienst.

Siehe auch:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "expiry" `[float]`
- Anzahl der Stunden an die sich CAPTCHA-Instanzen erinnern sollten. Standardeinstellung = 720 (1 Monat).

##### "logfile" `[string]`
- Protokollieren Sie alle CAPTCHA versucht? Geben Sie einen Dateinamen an oder lassen Sie die Option zum Deaktivieren leer.

##### "signature_limit" `[int]`
- Maximal zulässige Anzahl von Signaturen, bevor das CAPTCHA-Angebot zurückgezogen wird. Standardeinstellung = 1.

##### "api" `[string]`
- Welche API soll verwendet werden?

```
api
├─V1 ("V1")
└─Invisible ("V1 (Unsichtbar)")
```

##### "show_cookie_warning" `[bool]`
- Cookie-Warnung anzeigen? True = Ja [Standardeinstellung]; False = Nein.

##### "show_api_message" `[bool]`
- API-Nachricht anzeigen? True = Ja [Standardeinstellung]; False = Nein.

##### "nonblocked_status_code" `[int]`
- Welcher Statuscode sollte verwendet werden, wenn nicht-blockierte CAPTCHAs Anforderungen angezeigt werden?

```
nonblocked_status_code
├─200 (200 OK)
├─403 (403 Forbidden)
├─418 (418 I'm a teapot)
├─429 (429 Too Many Requests)
└─451 (451 Unavailable For Legal Reasons)
```

#### "legal" (Kategorie)
Konfiguration für gesetzliche Anforderungen.

##### "pseudonymise_ip_addresses" `[bool]`
- Pseudonymisieren IP-Adressen beim Schreiben der Protokolldateien? True = Ja [Standardeinstellung]; False = Nein.

##### "privacy_policy" `[string]`
- Die Adresse einer relevanten Datenschutz-Bestimmungen, die in der Fußzeile aller generierten Seiten angezeigt werden soll. Geben Sie eine URL ein, oder lassen Sie sie leer, um sie zu deaktivieren.

#### "template_data" (Kategorie)
Konfiguration für Vorlagen und Themen.

##### "theme" `[string]`
- Standard-Thema für CIDRAM verwenden.

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
└─…Andere
```

##### "magnification" `[float]`
- Schriftvergrößerung. Standardeinstellung = 1.

##### "css_url" `[string]`
- CSS-Datei URL für benutzerdefinierte Themen.

##### "block_event_title" `[string]`
- Der Seitentitel, der für Blockereignisse angezeigt werden soll.

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("denied")
└─…Andere
```

##### "captcha_title" `[string]`
- Der Seitentitel, der für CAPTCHA-Anforderungen angezeigt werden soll.

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…Andere
```

#### "PHPMailer" (Kategorie)
Konfiguration für PHPMailer (für Zwei-Faktor-Authentifizierung verwendet).

##### "event_log" `[string]`
- Eine Datei zum Protokollieren aller Ereignisse in Bezug auf PHPMailer. Geben Sie einen Dateinamen an oder lassen Sie die Option zum Deaktivieren leer.

##### "skip_auth_process" `[bool]`
- Wenn Sie diese Direktive auf `true` setzen, wird PHPMailer angewiesen, den normalen Authentifizierungsprozess zu überspringen, der normalerweise beim Senden von E-Mails über SMTP auftritt. Dies sollte vermieden werden, da das Überspringen dieses Prozesses ausgehende E-Mails MITM-Angriffen aussetzen kann. Dies kann jedoch in Fällen erforderlich sein, in denen dieser Prozess die Verbindung von PHPMailer zu einem SMTP-Server verhindert.

##### "enable_two_factor" `[bool]`
- Diese Direktive bestimmt, ob 2FA für Frontend-Konten verwendet werden soll.

##### "host" `[string]`
- Der SMTP-Host zum Senden von ausgehende E-Mails.

##### "port" `[int]`
- Die Portnummer zum Senden von ausgehende E-Mails. Standardeinstellung = 587.

##### "smtp_secure" `[string]`
- Das Protokoll zum Senden von E-Mails über SMTP (TLS oder SSL).

```
smtp_secure
├─default ("-")
├─tls ("TLS")
└─ssl ("SSL")
```

##### "smtp_auth" `[bool]`
- Diese Direktive bestimmt, ob SMTP-Sitzungen authentifiziert werden sollen (sollte normalerweise in Ruhe gelassen werden).

##### "username" `[string]`
- Der Benutzername zum Senden von E-Mails über SMTP.

##### "password" `[string]`
- Das Passwort zum Senden von E-Mails über SMTP.

##### "set_from_address" `[string]`
- Die Absenderadresse, die beim Senden von E-Mails über SMTP verwendet werden soll.

##### "set_from_name" `[string]`
- Der Name des Absenders, der beim Senden von E-Mails über SMTP verwendet werden soll.

##### "add_reply_to_address" `[string]`
- Die Antwortadresse, die beim Senden von E-Mails über SMTP verwendet werden soll.

##### "add_reply_to_name" `[string]`
- Der Name für der Antwort, die beim Senden von E-Mails über SMTP verwendet werden soll.

#### "rate_limiting" (Kategorie)
Konfiguration für Ratenbegrenzung (nicht für den allgemeinen Gebrauch empfohlen).

##### "max_bandwidth" `[string]`
- Die maximal zulässige Bandbreite innerhalb der Zulassungsperiode, bevor die Ratenbegrenzung für zukünftige Anforderungen aktiviert wird. Ein Wert von 0 deaktiviert diese Art der Ratenbegrenzung. Standardeinstellung = 0KB.

##### "max_requests" `[int]`
- Die maximale Anzahl von Anforderungen, die innerhalb der Zulassungsperiode zulässig sind, bevor die Ratenbegrenzung für zukünftige Anforderungen aktiviert wird. Ein Wert von 0 deaktiviert diese Art der Ratenbegrenzung. Standardeinstellung = 0.

##### "precision_ipv4" `[int]`
- Die Präzision für das Monitoring der IPv4-Nutzung. Der Wert spiegelt die CIDR-Blockgröße. Für beste Präzision auf 32 einstellen. Standardeinstellung = 32.

##### "precision_ipv6" `[int]`
- Die Präzision für das Monitoring der IPv6-Nutzung. Der Wert spiegelt die CIDR-Blockgröße. Für beste Präzision auf 128 einstellen. Standardeinstellung = 128.

##### "allowance_period" `[float]`
- Die Anzahl der Stunden, um die Nutzung zu überwachen. Standardeinstellung = 0.

##### "exceptions" `[string]`
- Ausnahmen (d.h., Anfragen die nicht ratenbegrenzt sein sollten). Nur relevant wenn die Ratenbegrenzung aktiviert ist.

```
exceptions
├─Whitelisted ("field_whitelisted_requests")
└─Verified ("field_verified_requests")
```

#### "supplementary_cache_options" (Kategorie)
Zusätzliche Cache-Optionen. Hinweis: Das Ändern dieser Werte kann Sie möglicherweise ausloggen.

##### "prefix" `[string]`
- Dieser Wert hier wird zu allen Cache-Eintragsschlüsseln vorangestellt. Standardeinstellung = "CIDRAM_". Wenn mehrere Installationen auf demselben Server vorhanden sind, kann dies nützlich sein, um ihre Caches getrennt zu halten.

##### "enable_apcu" `[bool]`
- Dies gibt an, ob APCu für das Caching verwendet werden soll. Standardeinstellung = True.

##### "enable_memcached" `[bool]`
- Dies gibt an, ob Memcached für das Caching verwendet werden soll. Standardeinstellung = False.

##### "enable_redis" `[bool]`
- Dies gibt an, ob Redis für das Caching verwendet werden soll. Standardeinstellung = False.

##### "enable_pdo" `[bool]`
- Dies gibt an, ob PDO für das Caching verwendet werden soll. Standardeinstellung = False.

##### "memcached_host" `[string]`
- Memcached Hostwert. Standardeinstellung = "localhost".

##### "memcached_port" `[int]`
- Memcached Portwert. Standardeinstellung = "11211".

##### "redis_host" `[string]`
- Redis Hostwert. Standardeinstellung = "localhost".

##### "redis_port" `[int]`
- Redis Portwert. Standardeinstellung = "6379".

##### "redis_timeout" `[float]`
- Redis Timeout-Wert. Standardeinstellung = "2.5".

##### "pdo_dsn" `[string]`
- PDO DSN-Wert. Standardeinstellung = "mysql:dbname=cidram;host=localhost;port=3306".

##### "pdo_username" `[string]`
- PDO Nutzername.

##### "pdo_password" `[string]`
- PDO Passwort.

---


### 7. <a name="SECTION7"></a>SIGNATURENFORMAT

*Siehe auch:*
- *[Was ist eine "Signatur"?](#WHAT_IS_A_SIGNATURE)*

#### 7.0 GRUNDLAGEN (FÜR SIGNATURDATEIEN)

Alle IPv4-Signaturen folgen dem Format: `xxx.xxx.xxx.xxx/yy [Funktion] [Param]`.
- `xxx.xxx.xxx.xxx` ist der Anfang des CIDR-Block (die Oktette der ursprünglichen IP-Adresse in dem Block).
- `yy` ist die CIDR-Block-Größe [1-32].
- `[Funktion]` weist das Skript an, was mit der Signatur zu tun ist (wie der Signatur zu betrachten).
- `[Param]` ist für jeden Zusätzlichen Parameter der für `[Funktion]` erforderlich sein können.

Alle IPv6-Signaturen folgen dem Format: `xxx.xxx.xxx.xxx/yy [Funktion] [Param]`.
- `xxxx:xxxx:xxxx:xxxx::xxxx` ist der Anfang des CIDR-Block (die Oktette der ursprünglichen IP-Adresse in dem Block). Sowohl die Komplette Notation als auch die abgekürzt Notation sind akzeptabel (und jeder MUSS den entsprechenden und relevanten Standards für die IPv6-Notation folgen, aber mit einer Ausnahme: Eine IPv6-Adresse darf nie mit einer Abkürzung beginnen wenn es in einer Signatur für dieses Skript verwendet wird, aufgrund der Art und Weise wie CIDRs durch das Script rekonstruiert; Beispielsweise, `::1/128` ausgedrückt sollte sein, wenn sie in einer Signatur verwendet werden, als `0::1/128`, und `::0/128` ausgedrückt als `0::/128`).
- `yy` ist die CIDR-Block-Größe [1-128].
- `[Funktion]` weist das Skript an, was mit der Signatur zu tun ist (wie der Signatur zu betrachten).
- `[Param]` ist für jeden Zusätzlichen Parameter der für `[Funktion]` erforderlich sein können.

Die Signaturdateien für CIDRAM SOLLTEN Unix-Stil-Zeilenumbrüche verwenden (`%0A`, oder `\n`)! Andere Arten/Stile von Zeilenumbrüchen (z.B., Windows `%0D%0A` oder `\r\n` Zeilenumbrüche, Mac `%0D` oder `\r` Zeilenumbrüche, u.s.w.) können verwendet werden, sind jedoch NICHT bevorzugt. Nicht-Unix-Stil-Zeilenumbrüche werden durch das Skript auf Unix-Stil-Zeilenumbrüche normalisiert.

Präzise und korrekte CIDR-Notation ist erforderlich, andernfalls wird das Skript die Signaturen NICHT erkennen. Zusätzlich, alle CIDR-Signaturen dieses Skript MÜSSEN mit einer IP-Adresse beginnen deren IP-Nummer gleichmäßig geteilt in die Blockteilung dargestellt durch ihre CIDR-Blockgröße werden kann (z.B., wenn Sie alle IPs blockieren von `10.128.0.0` nach `11.127.255.255` wollten, `10.128.0.0/8` wurde erkennen durch das Skript NICHT, aber `10.128.0.0/9` und `11.0.0.0/9` verwendet in Verbindung, WURDE erkennen durch das Skript).

Alles in den Signaturdateien nicht als Signatur noch Signatur-bezogene Syntax anerkannt durch das Skript wird IGNORIERT, dies bedeutet dass sie jegliche nicht Signatur in die Signaturdateien schreiben können, ohne dass das Script in seiner Funktionalität beschädigt wird. Kommentare sind in den Signaturdateien akzeptabel, und keine weite spezielle Formatierung für diese erforderlich. Kommentare mit Rauten ('#') wie in der Shell wird bevorzugt, aber nicht gefordert. Kommentare auf diesen weg zu kennzeichnen hilft IDEs Kommentare auch visuell als solche zu kennzeichen.

Die möglichen Werte für `[Funktion]` sind wie folgt:
- Run
- Whitelist
- Greylist
- Deny

Wenn "Run" verwendet wird, wenn die Signatur ausgelöst wird, das Skript ausgeführt (mittels `require_once`) welches durch `[Param]` angegeben wurde (das Arbeitsverzeichnis sollte das Verzeichnis "/vault/" des Skripts sein).

*Beispiel: `127.0.0.0/8 Run example.php`*

Das kann nützlich sein wenn Sie für einige spezifische IPs und/oder CIDRs eigene PHP-Scripte ausführen möchten.

Wenn "Whitelist" verwendet wird, wenn die Signatur ausgelöst wird, wird das Script alle Erkennungen zurücksetzen (wenn es Entdeckungen gab) und bricht die Testfunktion ab. `[Param]` wird ignoriert. Diese Funktion entspricht dem Whitelisting einer bestimmten IP oder CIDR so dass keine Erkennung stattfindet.

Beispiel: `127.0.0.1/32 Whitelist`

Wenn "Greylist" verwendet wird, wenn die Signatur ausgelöst wird, wird das Skript alle Erkennungen zurücksetzen (wenn es irgendwelche Entdeckungen gab) und springt zur nächsten Signaturdatei, um die Verarbeitung fortzusetzen. `[Param]` wird ignoriert.

Beispiel: `127.0.0.1/32 Greylist`

Wenn "Deny" verwendet wird, wenn die Signatur ausgelöst wird, vorausgesetzt keine Whitelist-Signatur für die angegebene IP-Adresse und/oder angegebene CIDR ausgelöst wurde, wird der Zugriff auf die geschützte Seite verweigert. "Deny" ist was Sie verwenden möchten, um tatsächlich eine IP-Adresse und/oder CIDR zu blockieren. Wenn eine Signatur asugelöst wird, die "Deny" verwendet, wird die "Zugriff verweigert" Seite generiert und die Anforderung an die geschützte Seite getötet.

Der `[Param]`-Wert welcher von "Deny" akzeptiert udn verarbeitet wird wird auf der "Zugriff verweigert" Seite verwendet und wird dem Kunden/Benutzer als Sperrgrund zur Verfügung gestellt. Es kann ein kurzer und einfacher Satz sein um zu erklären, warum Sie sich dazu entschieden haben, diese Blockierregel zu erstellen (alles sollte genügen, sogar eine einfaches "Ich will Sie nicht auf meiner Website"), oder eines von einer Handvoll von Kurzwörter welche von dem Script zur Verfügung gestellt werden.

Die vorbereiteten Erklärungen haben L10N-Unterstützung und können durch das Skript übersetzt werden. Dies geschieht basierend auf der Sprache welche Sie in der `lang` Richtlinie der Skript-Konfiguration angeben. Zusätzlich, können Sie das Skript anweisen dies für "Deny" Signaturen zu ignorieren, basierend auf ihrem `[Param]`-Wert (wenn sie diese Kurzwörter verwenden) über die in der Skript-Konfiguration spezifizierten Richtlinien (jedes Kurzwort hat eine entsprechende Richtlinie für die entsprechenden Signaturen diese entweder zu verarbeiten oder zu ignorieren). `[Param]`-Werte welche diese Kurzwörter nicht verwenden haben jedoch keine L10N-Unterstützung, und werden daher nicht NICHT durch das Skript übersetzt, und sind des weiteren nicht direkt durch die Skript-Konfiguration kontrollierbar.

Die verfügbaren Kurzwörter sind:
- Attacks   ("Angriffe")
- Bogon     ("Bogon-IP")
- Cloud     ("Cloud-Service")
- Generic   ("Generisch")
- Legal     ("Gesetzliche")
- Malware   ("Malware")
- Proxy     ("Proxy-Service")
- Spam      ("Spam Risiko")

Die Übersetzungen für die jeweilige Sprache können in der Datei `/vault/lang/lang.<sprache>.php` eingesehen werden.

#### 7.1 TAGS

##### 7.1.0 SEKTION-TAGS

Wenn Sie Ihre benutzerdefinierten Signaturen in einzelne Sektionen aufteilen möchten, können Sie diese einzelne Sektionen gegenüber dem Skript identifizieren indem sie einen "Sektions-Tag" unmittelbar nach dem Signaturen der jeder Sektion, zusammen mit dem Namen ihrer Signatur-Sektion (siehe Beispiel unten), hinzufügen.

```
# Sektion 1.
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: Sektion 1
```

Um das Abschnitts-Tagging zu unterbrechen und sicherzustellen, dass Tags nicht falsch für Signaturabschnitte aus früheren Signaturdateien identifiziert werden, stellen Sie einfach sicher, dass es mindestens zwei aufeinanderfolgende Zeilenumbrüche zwischen Ihrem Tag und Ihren früheren Signaturabschnitten gibt. Alle nicht markierten Signaturen werden standardmäßig entweder auf "IPv4" oder "IPv6" gesetzt (je nachdem, welche Arten von Signaturen ausgelöst werden).

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: Sektion 1
```

In dem obigen Beispiel, wird `1.2.3.4/32` und `2.3.4.5/32` als "IPv4" markiert werden, wohingegen `4.5.6.7/32` und `5.6.7.8/32` als "Sektion 1" markiert wird.

Die gleiche Logik kann auch zum Trennen anderer Arten von Tags angewendet werden.

Insbesondere, Sektion-Tags können beim Debuggen sehr nützlich sein, wenn Falsche-Positives auftreten, durch Bereitstellung einer Möglichkeit, die genaue Ursache des Problems zu finden, und können beim Filtern von Protokolleinträgen beim Anzeigen von Protokolldateien über die Frontend-Protokollseite sehr nützlich sein (Sektionsnamen sind über die Frontend-Protokollseite anklickbar und können als Filterkriterien verwendet werden). Wenn für bestimmte Signaturen Sektion-Tags weggelassen werden, verwendet CIDRAM beim Auslösen dieser Signaturen den Namen der Signaturdatei zusammen mit dem Typ der blockierten IP-Adresse (IPv4 oder IPv6) als Fallback, daher sind Sektion-Tags völlig optional. Sie können jedoch in einigen Fällen empfohlen werden, z.B. wenn die Signaturdateien vage benannt werden oder wenn es sonst schwierig ist, die Quelle der Signaturen eindeutig zu identifizieren, die eine verbannte Anforderung verursachen.

##### 7.1.1 ABLAUF-TAGS

Wenn Sie möchten dass Signaturen nach einiger Zeit ablaufen, in einer Weise ähnlicher wie Sektion-Tags, können Sie ein "Ablauf-Tag" verwenden um anzugeben wann Signaturen nicht mehr gültig sind. Ablauf-Tags verwenden das Format "JJJJ.MM.TT" (siehe Beispiel unten).

```
# Sektion 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

Abgelaufene Signaturen werden niemals in Reaktion irgendeine Anfrage ausgelöst, egal was passiert.

##### 7.1.2 URSPRUNGS-TAGS

Wenn Sie das Herkunftsland für eine bestimmte Signatur angeben möchten, können Sie dies mit einem "Ursprungs-Tag" tun. Ein Ursprungs-Tag akzeptiert einen "[ISO 3166-1 Alpha-2](https://de.wikipedia.org/wiki/ISO-3166-1-Kodierliste)"-Code, der dem Ursprungsland für die Signaturen entspricht, auf die es angewendet wird. Diese Codes müssen in Großbuchstaben geschrieben werden (Kleinbuchstaben oder Groß-/Kleinschreibung werden nicht korrekt dargestellt). Wenn ein Ursprungs-Tag verwendet wird, wird es zum Log-Feld für alle Anfragen "Warum blockiert" hinzugefügt, die aufgrund der Signaturen blockiert wurden, auf die das Tag angewendet wurde.

Wenn die optionale Komponente "flags CSS" installiert ist, und Log-Dateien im Frontend angezeigt werden, werden die angehängten Ursprungs-Informationen in die Flaggen der entsprechenden Länder umgewandelt. Diese Information ist anklickbar um nach Ähnlichen Logeinträgen zu filtern (denjenigen, die auf die Protokollseite zugreifen, die Möglichkeit zu geben, nach dem Herkunftsland zu filtern).

Hinweis: Technisch gesehen ist, dies keine Form von Geolokalisierung, weil es keine spezifischen Informationen sucht in Bezug auf eingehende IPs, aber stattdessen, erlaubt uns einfach, ein Herkunftsland für alle Anfragen anzugeben, die durch bestimmte Signaturen blockiert werden. Innerhalb derselben Signatur-Sektionen sind mehrere Ursprungs-Tags zulässig.

Hypothetisches Beispiel:

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

Alle Tags können zusammen verwendet werden, und alle Tags sind optional (siehe Beispiel unten).

```
# Beispiel Sektion.
1.2.3.4/32 Deny Generic
Origin: US
Tag: Beispiel Sektion
Expires: 2016.12.31
```

##### 7.1.3 ABWERTUNGS-TAGS

Wenn eine große Anzahl von Signaturdateien installiert und aktiviert verwendet wird, können Installationen sehr komplex werden, und es können einige Signaturen vorhanden sein, die sich überlappen. Um in diesen Fällen zu verhindern, dass während Blockereignissen mehrere überlappende Signaturen ausgelöst werden, können Abwertungs-Tags verwendet werden, um bestimmte Signatur-Sektionen in Fällen zu verschieben, in denen eine andere spezifische Signaturdateien installiert und aktiv verwendet werden. Dies kann nützlich sein, wenn einige Signaturen häufiger als andere aktualisiert werden, um die weniger häufig aktualisierten Signaturen zugunsten der häufiger aktualisierten Signaturen zu verschieben.

Abwertungs-Tags werden ähnlich wie andere Tags verwendet. Der Wert des Tags sollte mit einer installierten und aktiv genutzten Signaturdatei übereinstimmen, auf die der Tag verschieben werden soll.

Beispiel:

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 7.1.4 PROFIL-TAGS

Profil-Tags bieten eine Möglichkeit zusätzliche Informationen auf der IP-Testseite anzuzeigen, und können von Modulen und Hilfsregeln für ein komplexeres Verhalten und eine genauere Entscheidungsfindung genutzt werden.

Profil-Tags werden ähnlich wie andere Arten von Tags verwendet. Die Werte von Profil-Tags können als Bedingung für Module und Hilfsregeln verwendet werden. Profil-Tags können mehrere Werte bereitstellen, durch Trennen dieser Werte durch ein Semikolon. Der Endbenutzer sieht niemals die Werte von Profil-Tags.

Beispiel:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 7.2 YAML

##### 7.2.0 YAML GRUNDLAGEN

Eine vereinfachte Form von YAML-Markup kann in Signaturdateien verwendet werden, um Verhalten und Einstellungen spezifisch für einzelne Signatur-Sektionen zu definieren. Dies kann nützlich sein wenn Sie den Wert von Ihrer Konfiguration-Richtlinien variieren möchten auf der Grundlage von individuellen Signaturen und Signatur-Sektionen (beispielsweise; wenn Sie eine E-Mail-Adresse für Support-Tickets anbieten möchten, für irgendein Benutzer welche durch eine spezifische Signatur blockiert sind, aber Sie diese E-Mail-Adresse nicht für Nutzer welche durch andere Signaturen blockiert sind bieten möchten; wenn Sie möchten dass bestimmte Signaturen eine Seitenumleitung auslösen; wenn Sie einen Signatur-Sektion für die Verwendung mit reCAPTCHA/hCAPTCHA freischalten möchten; wenn Sie um blockierte Zugriffsversuche zu protokollieren in einzelne Dateien auf der Grundlage von einzelnen Signaturen und/oder Signatur-Sektionen möchten).

Die Verwendung von YAML-Markup in den Signaturdateien ist völlig optional (d.h., Sie können YAML-Markup verwenden, wenn Sie dies möchten, aber Sie sind nicht verpflichtet dies zu tun), und ist in der Lage die meisten (aber nicht alles) Konfigurations-Richtlinien zu nutzen.

*Beachten: Die YAML-Markup-Implementierung in CIDRAM ist sehr einfach und sehr begrenzt; Es ist ausgelegt um die Anforderungen zu erfüllen welche spezifisch für CIDRAM sind, in einer Weise dass die Vertrautheit mit YAML-Markup gegeben ist, aber folgt nicht den offiziellen Spezifikationen (und wird sich daher nicht in der gleichen Weisewie wie gründlichere Implementierungen anderswo verhalten, und möglicherweise nicht für andere Projekte anderswo geeignet sein).*

In CIDRAM werden YAML-Markup-Segmente durch drei Bindestriche ("---") gegenüber dem Skript identifiziert und enden neben ihren enthaltenen Signaturabschnitten durch doppelte Zeilenumbrüche. Ein typisches YAML-Markup-Segment innerhalb eines Signaturabschnitts besteht aus drei Strichen in einer Zeile unmittelbar nach der Liste der CIDRs und aller Tags, gefolgt von einer zweidimensionalen Liste der Schlüssel-Wert-Paare (erste Dimension, Konfigurationsanweisungskategorien; zweite Dimension, Konfigurationsanweisungen), für die Konfigurationsanweisungen geändert werden sollten (und auf welche Werte), wenn eine Signatur innerhalb dieses Signaturabschnitts ausgelöst wird (siehe die folgenden Beispiele).

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

##### 7.2.1 WIE MAN "SPEZIELL MARKIEREN" DEN SIGNATUR-SEKTIONEN FÜR DIE VERWENDUNG MIT reCAPTCHA/hCAPTCHA NUTZT

Wenn "usemode" 2 oder 5 ist, um Signatur-Sektionen "besonders zumarkiert" für die Verwendung mit reCAPTCHA/hCAPTCHA, ist ein Eintrag in dem YAML-Segment für diese Signatur-Sektion enthalten (siehe Beispiel unten).

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

#### 7.3 ZUSATZINFORMATION

##### 7.3.0 IGNORIEREN VON SIGNATUR-SEKTIONEN

In Ergänzung, wenn Sie möchten dass CIDRAM wird bestimmte Sektionen innerhalb irgendein der Signaturdateien vollständig ignoriert, können Sie die Datei `ignore.dat` verwenden, um festzulegen welche Sektionen zu ignorieren sind. Schreiben sie `Ignore` in eine neue Linie, gefolgt von einem Leerzeichen, gefolgt durch dem Namen der Sektion welche Sie CIDRAM Anweisen möchten zu ignorieren (siehe Beispiel unten).

```
Ignore Sektion 1
```

Dies kann auch erreicht werden, indem die Schnittstelle verwendet wird, die auf der Seite "Sektionsliste" des CIDRAM-Frontend bereitgestellt wird.

##### 7.3.1 HILFSREGELN

Wenn Sie das Schreiben Ihrer eigenen benutzerdefinierten Signaturdateien oder benutzerdefinierten Module für zu kompliziert halten, könnte die Verwendung der unter "Hilfsregeln" im CIDRAM-Frontend bereitgestellten Schnittstelle eine hilfe sein. Indem Sie die entsprechenden Optionen auswählen und Details zu bestimmten Anforderungsarten angeben, können Sie CIDRAM anweisen, wie auf diese Anfragen zu reagieren ist. "Hilfsregeln" werden ausgeführt, nachdem die Ausführung alle der Signaturdateien und Module bereits abgeschlossen ist.

#### 7.4 <a name="MODULE_BASICS"></a>GRUNDLAGEN (FÜR MODULE)

Module können verwendet werden, um die Funktionalität von CIDRAM zu erweitern, zusätzliche Aufgaben auszuführen oder zusätzliche Logik zu verarbeiten. Typischerweise werden sie Verwendet, wenn eine Anforderung auf einer anderen Basis als der ursprünglichen IP-Adresse blockiert werden muss (und daher, wenn eine CIDR-Signatur nicht ausreicht, um die Anfrage zu blockieren). Module werden als PHP-Dateien geschrieben, und daher werden Modul-Signaturen typischerweise als PHP-Code geschrieben.

Einige gute Beispiele für CIDRAM-Module finden Sie hier:
- https://github.com/CIDRAM/CIDRAM-Extras/tree/master/modules

Eine Vorlage zum Schreiben neuer Module finden Sie hier:
- https://github.com/CIDRAM/CIDRAM-Extras/blob/master/modules/module_template.php

Da Module als PHP-Dateien geschrieben werden, können Sie Ihre Module beliebig strukturieren und schreiben Sie Ihre Modul-Signaturen wie Sie wollen (im Rahmen des Zumutbaren für was mit PHP möglich ist), wenn Sie mit der CIDRAM-Codebasis ausreichend vertraut sind. Jedoch, zu Ihrer eigenen Bequemlichkeit und aus Gründen der besseren gegenseitigen Verständlichkeit zwischen vorhandenen Modulen und Ihren eigenen, es wird empfohlen, die oben verlinkte Vorlage zu analysieren, um die von ihr bereitgestellte Struktur und das Format verwenden zu können.

*Beachten: Wenn Sie nicht komfortabel im Umgang mit PHP sind, wird das Schreiben eigener Module nicht empfohlen.*

Einige Module für Funktionen werden von CIDRAM zur Verfügung gestellt, die es einfacher machen sollten eigene Module zu schreiben. Informationen zu dieser Funktionalität werden im Folgenden beschrieben.

#### 7.5 MODUL-FUNKTIONALITÄT

##### 7.5.0 "$Trigger"

Modul-Signaturen werden typischerweise mit `$Trigger` geschrieben. In den meisten Fällen ist diese Schließung für das Schreiben von Modulen wichtiger als alles andere.

`$Trigger` akzeptiert 4 Parameter: `$Condition`, `$ReasonShort`, `$ReasonLong` (optional), und `$DefineOptions` (optional).

Die Wahrheit von `$Condition` wird ausgewertet, und wenn dies wahr/true, wird die Signatur "ausgelöst". Wenn falsch/false, wird die Signatur *nicht* "ausgelöst". `$Condition` enthält typischerweise PHP-Code, um eine Bedingung auszuwerten, die dazu führen sollte, dass eine Anfrage blockiert wird.

`$ReasonShort` wird im Feld "Warum blockierte" angegeben, wenn die Signatur "ausgelöst" wird.

`$ReasonLong` ist eine optionale Nachricht, die dem Benutzer/Client angezeigt wird, wenn sie blockiert werden, um zu erklären, warum sie blockiert wurden. "Zugriff verweigert" wenn leer.

`$DefineOptions` ist ein optionales Array, das Schlüssel/Wert-Paare enthält, mit denen Konfigurationsoptionen definiert werden, die für die Anforderungsinstanz spezifisch sind. Konfigurationsoptionen werden angewendet, wenn die Signatur "ausgelöst" wird.

`$Trigger` gibt wahr/true zurück, wenn die Signatur "ausgelöst" wird, und falsch/false, wenn dies nicht der Fall ist.

Um diese Closure in Ihrem Modul zu verwenden, denken Sie daran sie dies zuerst vom übergeordneten Geltungsbereich zu übernehmen:
```PHP
$Trigger = $CIDRAM['Trigger'];
```

##### 7.5.1 "$Bypass"

Signatur-Bypass wird normalerweise mit `$Bypass` geschrieben.

`$Bypass` akzeptiert 3 Parameter: `$Condition`, `$ReasonShort`, und `$DefineOptions` (optional).

Die Wahrheit von `$Condition` wird ausgewertet, und wenn dies wahr/true, wird die Signatur "ausgelöst". Wenn falsch/false, wird die Signatur *nicht* "ausgelöst". `$Condition` enthält typischerweise PHP-Code, um eine Bedingung auszuwerten, die dazu führen sollte, dass eine Anfrage *nicht* blockiert wird.

`$ReasonShort` wird im Feld "Warum blockierte" angegeben, wenn der Bypass "ausgelöst" wird.

`$DefineOptions` ist ein optionales Array, das Schlüssel/Wert-Paare enthält, mit denen Konfigurationsoptionen definiert werden, die für die Anforderungsinstanz spezifisch sind. Konfigurationsoptionen werden angewendet, wenn die Bypass "ausgelöst" wird.

`$Bypass` gibt wahr/true zurück, wenn die Bypass "ausgelöst" wird, und falsch/false, wenn dies nicht der Fall ist.

Um diese Closure in Ihrem Modul zu verwenden, denken Sie daran sie dies zuerst vom übergeordneten Geltungsbereich zu übernehmen:
```PHP
$Bypass = $CIDRAM['Bypass'];
```

##### 7.5.2 "$CIDRAM['DNS-Reverse']"

Dies kann verwendet werden, um den Hostnamen einer IP-Adresse abzurufen. Wenn Sie ein Modul zum Blockieren von Hostnamen erstellen möchten, könnte diese Closure nützlich sein.

Beispiel:
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

#### 7.6 MODUL VARIABLEN

Module werden in ihrer eigenen Umgebung ausgeführt, und alle Variablen, die von einem Modul definiert werden, sind für andere Module oder das übergeordnete Skript nicht zugänglich, es sei denn, sie sind im Array `$CIDRAM` gespeichert. Alles andere wird gelöscht, nachdem die Modulausführung abgeschlossen ist.

Im Folgenden finden Sie einige allgemeine Variablen, die für Ihr Modul nützlich sein könnten:

Variable | Beschreibung
----|----
`$CIDRAM['BlockInfo']['DateTime']` | Das aktuelle Datum und die Uhrzeit.
`$CIDRAM['BlockInfo']['IPAddr']` | IP-Adresse für die aktuelle Anfrage.
`$CIDRAM['BlockInfo']['ScriptIdent']` | CIDRAM Script-Version.
`$CIDRAM['BlockInfo']['Query']` | Die Abfrage (query) für die aktuelle Anfrage.
`$CIDRAM['BlockInfo']['Referrer']` | Der Referrer für die aktuelle Anfrage (falls vorhanden).
`$CIDRAM['BlockInfo']['UA']` | Der Benutzeragent (user agent) für die aktuelle Anfrage.
`$CIDRAM['BlockInfo']['UALC']` | Der Benutzeragent (user agent) für die aktuelle Anfrage (als Kleinbuchstaben).
`$CIDRAM['BlockInfo']['ReasonMessage']` | Die Nachricht, die dem Benutzer/Client für die aktuelle Anfrage angezeigt wird, wenn sie blockiert sind.
`$CIDRAM['BlockInfo']['SignatureCount']` | Die Anzahl der Signaturen, die für die aktuelle Anfrage ausgelöst wurden.
`$CIDRAM['BlockInfo']['Signatures']` | Referenzinformationen für alle Signaturen, die für die aktuelle Anforderung ausgelöst wurden.
`$CIDRAM['BlockInfo']['WhyReason']` | Referenzinformationen für alle Signaturen, die für die aktuelle Anforderung ausgelöst wurden.

---


### 8. <a name="SECTION8"></a>BEKANNTE KOMPATIBILITÄTSPROBLEME

Die folgenden Pakete und Produkte haben sich als inkompatibel mit CIDRAM erwiesen:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

Module wurden zur Verfügung gestellt, um sicherzustellen, dass die folgenden Pakete und Produkte mit CIDRAM kompatibel sind:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__

*Siehe auch: [Kompatibilitätstabellen](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 9. <a name="SECTION9"></a>HÄUFIG GESTELLTE FRAGEN (FAQ)

- [Was ist eine "Signatur"?](#WHAT_IS_A_SIGNATURE)
- [Was ist ein "CIDR"?](#WHAT_IS_A_CIDR)
- [Was ist ein "Falsch-Positiv"?](#WHAT_IS_A_FALSE_POSITIVE)
- [Kann CIDRAM ganze Länder blockieren?](#BLOCK_ENTIRE_COUNTRIES)
- [Wie häufig werden Signaturen aktualisiert?](#SIGNATURE_UPDATE_FREQUENCY)
- [Ich habe ein Problem bei der Verwendung von CIDRAM und ich weiß nicht was ich tun soll! Bitte helfen Sie!](#ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [CIDRAM hat mich von einer Website blockiert die ich besuchen möchte! Bitte helfen Sie!](#BLOCKED_WHAT_TO_DO)
- [Ich möchte CIDRAM (vor v2) mit einer PHP-Version älter als 5.4.0 verwenden; Können Sie helfen?](#MINIMUM_PHP_VERSION)
- [Ich möchte CIDRAM (v2) mit einer PHP-Version älter als 7.2.0 verwenden; Können Sie helfen?](#MINIMUM_PHP_VERSION_V2)
- [Kann ich eine einzige CIDRAM-Installation verwenden, um mehrere Domains zu schützen?](#PROTECT_MULTIPLE_DOMAINS)
- [Ich möchte keine Zeit damit verbringen (es zu installieren, es richtig zu ordnen, u.s.w.); Kann ich dich einfach bezahlen, um alles für mich zu tun?](#PAY_YOU_TO_DO_IT)
- [Kann ich Sie oder einen der Entwickler dieses Projektes für private Arbeit einstellen?](#HIRE_FOR_PRIVATE_WORK)
- [Ich brauche spezialisierte Modifikationen, Anpassungen, u.s.w.; Können Sie helfen?](#SPECIALIST_MODIFICATIONS)
- [Ich bin ein Entwickler, Website-Designer oder Programmierer. Kann ich die Arbeit an diesem Projekt annehmen oder anbieten?](#ACCEPT_OR_OFFER_WORK)
- [Ich möchte zum Projekt beitragen; Darf ich dies machen?](#WANT_TO_CONTRIBUTE)
- [Kann ich cron verwenden, um automatisch zu aktualisieren?](#CRON_TO_UPDATE_AUTOMATICALLY)
- [Was sind "Verstöße"?](#WHAT_ARE_INFRACTIONS)
- [Kann CIDRAM Hostnamen blockieren?](#BLOCK_HOSTNAMES)
- [Was kann ich für "default_dns" verwenden?](#WHAT_CAN_I_USE_FOR_DEFAULT_DNS)
- [Kann ich CIDRAM verwenden, um andere Dinge als Websites zu schützen (z.B. E-Mail-Server, FTP, SSH, IRC u.s.w.)?](#PROTECT_OTHER_THINGS)
- [Werden Probleme auftreten, wenn ich CIDRAM gleichzeitig mit CDNs oder Caching-Diensten verwende?](#CDN_CACHING_PROBLEMS)
- [Wird CIDRAM meine Website vor DDoS-Angriffen schützen?](#DDOS_ATTACKS)
- [Wenn ich Module oder Signaturdateien über die Aktualisierungsseite aktiviere oder deaktiviere, sortiert sich diese alphanumerisch in der Konfiguration. Kann ich die Art der Sortierung ändern?](#CHANGE_COMPONENT_SORT_ORDER)
- [Was ist ein "PDO DSN"? Wie kann ich PDO mit CIDRAM verwenden?](#HOW_TO_USE_PDO)
- [CIDRAM blockiert Cronjobs; Wie kann das behoben werden?](#BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>Was ist eine "Signatur"?

Im Kontext von CIDRAM, eine "Signatur" bezieht sich auf Daten, die als Indikator/Identifikator fungieren, für etwas Bestimmtes dass wir suchen (normalerweise eine IP-Adresse oder CIDR), und enthält einige Anweisungen für CIDRAM, wie am besten zu reagieren ist, wenn der angegebene Fall eintritt. Eine typische CIDRAM Signatur sieht in etwa so aus:

Für "Signaturdateien":

`1.2.3.4/32 Deny Generic`

Für "Module":

```PHP
$Trigger(strpos($CIDRAM['BlockInfo']['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*Beachten: Signaturen für "Signaturdateien", und Signaturen für "Module", sind nicht dasselbe.*

Oft (aber nicht immer) werden Signaturen in Gruppen zusammengebunden, um "Signatur-Sektionen" zu bilden, oft begleitet von Kommentaren, Markup und/oder verwandten Metadaten welche dazu verwendet werden, um zusätzlichen Kontext für die Signaturen bereitstellen zu können, oder enthalten weitere Informationen.

#### <a name="WHAT_IS_A_CIDR"></a>Was ist ein "CIDR"?

"CIDR" ist ein Akronym für "Classless Inter-Domain Routing" *[[1](https://de.wikipedia.org/wiki/Classless_Inter-Domain_Routing), [2](https://whatismyipaddress.com/cidr)]*, und es ist dieses Akronym, das als Teil des Namens für dieses Paket, "CIDRAM", verwendet wird, um ein größeres Akronym zu bilden, "Classless Inter-Domain Routing Access Manager".

Aber, im Kontext von CIDRAM (sowie, in dieser Dokumentation, in Diskussionen über CIDRAM, oder in den CIDRAM-Sprachdaten), wann immer ein "CIDR" (Singular) oder "CIDRs" (Plural) ist erwähnt (und somit, wobei wir diese Wörter als Substantive in ihrem eigenen Recht verwenden, im Gegensatz zu Akronymen), was beabsichtigt und gemeint ist ein Subnetz (oder Subnetze), ausgedrückt mit CIDR-Notation. Der Grund dafür, dass CIDR (oder CIDRs) verwendet wird, anstelle von Subnetz (oder Subnetze) ist um zu klären, es ist Subnetze mit CIDR-Notation ausgedrückt auf die wir uns beziehen (weil CIDR-Notation ist nur eine von verschiedenen Möglichkeiten, wie Subnetze ausgedrückt werden können). CIDRAM könnte daher als "Subnetz Access Manager" betrachtet werden.

Obwohl diese doppelte Bedeutung von "CIDR" in einigen Fällen mehrdeutig werden kann, diese erklärung, zusammen mit dem Kontext zur Verfügung gestellt, sollte helfen diese Mehrdeutigkeit zu lösen.

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>Was ist ein "Falsch-Positiv"?

Der Begriff "Falsch-Positiv" (*Alternative: "falsch-positiv Fehler"; "falscher Alarm"*; Englisch: *false positive*; *false positive error*; *false alarm*), sehr einfach beschrieben, und in einem verallgemeinerten Kontext, wird verwendet, wenn eine Bedingung zu testen ist und wenn die Ergebnisse positiv sind (also wenn die Bedingung als positiv bewertet wird) jedoch die Bedingung als negativ erwartet (oder negativ sein sollte) wird. In der Medizin ist ein "falsch Positiv" ein Begriff dafür, wenn Patienten mit einer Krankheit identifiziert wurden

Einige andere Begriffe verwendet: "Wahr-Positiv", "Wahr-Negativ" und "Falsch-Negativ". Eine "Wahr-Positiv" ist, wenn die Ergebnisse des Tests und der wahren Zustand beide wahr sind (oder "Positiv"), und eine "Wahr-Negativ" ist, wenn die Ergebnisse des Tests und der wahren Zustand beide falsch sind (oder "Negativ"); Eine "Wahr-Positiv" oder Eine "Wahr-Negativ" gilt als eine "korrekte Folgerung". Die Antithese von einem "Falsch-Positiv" ist ein "Falsch-Negativ"; Ein "Falsch-Negativ" ist, wenn die Ergebnisse des Tests negativ sind (d.h., die Bedingung bestimmt wird negativ oder falsch zu sein), aber ein positives Resultat zu erwarten ist (oder sollte gewesen, d.h., der Zustand, in Wirklichkeit, ist "positiv", oder "wahr").

Im Kontext der CIDRAM, Diese Begriffe beziehen sich auf der Signaturen von CIDRAM, und was/wen sie blockieren. Wenn CIDRAM Blöcke eine IP-Adresse wegen schlechten, veralteten oder falschen Signaturen blockieren, sollten dies aber nicht so getan haben, oder wenn sie es aus den falschen Gründen, beziehen wir uns auf dieses Ergebnis als "Falsch-Positiv". Wenn CIDRAM, aufgrund unvorhergesehener Bedrohungen, fehlenden Signaturen oder Defiziten in ihren Signaturen, versagt eine IP-Adresse zu blockieren, die blockiert werden sollte, beziehen wir uns auf dieses Ereignis als eine "verpasste Erkennung" (das entspricht einem "Falsch-Negativ").

Dies kann durch die folgende Tabelle zusammengefasst werden:

&nbsp; | CIDRAM sollte *KEINE* IP-Adresse blockieren | CIDRAM *SOLLTE* eine IP-Adresse blockieren
---|---|---
CIDRAM blockiert eine IP-Adresse *NICHT* | Wahr-Negativ (korrekte Folgerung) | **Verpasste Erkennung (analog zu Falsch-Negativ)**
CIDRAM blockiert eine IP-Adresse | __Falsch-Positiv__ | True-Positiv (korrekte Folgerung)

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>Kann CIDRAM ganze Länder blockieren?

Ja. Der einfachste Weg ist das BGPView-Modul zu installieren und es gemäß Ihren Anforderungen zu konfigurieren.

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>Wie häufig werden Signaturen aktualisiert?

Die Aktualisierungshäufigkeit hängt von den betreffenden Signaturdateien ab. In der Regel, versuchen alle Betreuer von CIDRAM Signaturen diese so aktuell wie möglich zu halten, aber da wir alle anderen Verpflichtungen in unserem Leben außerhalb des Projekts haben, und da für unsere Bemühungen um das Projekt keiner von uns finanziell entschädigt wird (d.h., bezahlt), kann kein genauer Aktualisierungs-Zeitplan garantiert werden. In der Regel, werden Signaturen aktualisiert, wann immer es genügend Zeit gibt sie zu aktualisieren, und Betreuer versuchen auf der Grundlage der Notwendigkeit und auf der Grundlage der häufigkeit der Veränderungen unter den Bereichen auftreten zu priorisieren. Hilfe wird immer geschätzt, wenn Sie bereit sind irgendwelche anzubieten.

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>Ich habe ein Problem bei der Verwendung von CIDRAM und ich weiß nicht was ich tun soll! Bitte helfen Sie!

- Verwenden Sie die neueste Version der Software? Verwenden Sie die neuesten Versionen Ihrer Signaturdateien? Wenn die Antwort auf eine dieser beiden Fragen nein ist, versuchen sie zuerst diese zu aktualisieren, und überprüfen Sie ob das Problem weiterhin besteht. Wenn es weiterhin besteht, lesen Sie weiter.
- Haben Sie alles in der Dokumentation überprüft? Wenn nicht, bitte tun Sie dies. Wenn das Problem nicht mit der Dokumentation gelöst werden kann, lesen Sie weiter.
- Haben Sie die **[Issues-Seite](https://github.com/CIDRAM/CIDRAM/issues)** überprüft, ob ein solches oder ähnliches Problem vorher erwähnt wurde? Wenn es vorher erwähnt wurde, überprüfen Sie, ob irgendwelche Vorschläge, Ideen und/oder Lösungen zur Verfügung gestellt wurden, und folgend Sie diesen um ihr Problem zu Lösen.
- Wenn das Problem weiterhin besteht, bitte fragen Sie nach Hilfe, indem Sie auf der  **[Issues-Seite](https://github.com/CIDRAM/CIDRAM/issues)** ein neues Issue erstellen.

#### <a name="BLOCKED_WHAT_TO_DO"></a>CIDRAM hat mich von einer Website blockiert die ich besuchen möchte! Bitte helfen Sie!

CIDRAM bietet ein Mittel für Website-Besitzer, um unerwünschten Verkehr zu blockieren, aber es liegt in der Verantwortung der Website-Besitzer, selbst zu entscheiden, wie sie CIDRAM nutzen wollen. Im Falle der falschen-Positiven in Bezug auf der Signaturdateien die normalerweise mit CIDRAM enthalten sind, können Korrekturen vorgenommen werden, aber in Bezug auf das entblockiert werden von bestimmten Websites, müssen Sie mit den Betreibern der Websites sprechen. In Fällen in denen Korrekturen vorgenommen werden, müssen diese ihre Signaturdateien und/oder Installationen aktualisieren, und in anderen Fällen (wie zum Beispiel, in welchen diese ihre Installation geändert haben, oder in wlchen sie ihre eigenen benutzerdefinierten Signaturen erstellt haben, u.s.w.). Die Verantwortung um dieses Problem zu lösen, liegt ganz bei ihnen und ist außerhalb unserer Kontrolle.

#### <a name="MINIMUM_PHP_VERSION"></a>Ich möchte CIDRAM (vor v2) mit einer PHP-Version älter als 5.4.0 verwenden; Können Sie helfen?

Nein. PHP >= 5.4.0 ist eine Mindestanforderung für CIDRAM < v2.

#### <a name="MINIMUM_PHP_VERSION_V2"></a>Ich möchte CIDRAM (v2) mit einer PHP-Version älter als 7.2.0 verwenden; Können Sie helfen?

Nein. PHP >= 7.2.0 ist eine Mindestanforderung für CIDRAM v2.

*Siehe auch: [Kompatibilitätstabellen](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>Kann ich eine einzige CIDRAM-Installation verwenden, um mehrere Domains zu schützen?

Ja. CIDRAM-Installationen sind natürlich nicht auf bestimmte Domains festgelegt, und können daher zum Schutz mehrerer Domains verwendet werden. Allgemein, verweisen wir darauf, CIDRAM-Installationen die nur eine Domain schützen als "Single-Domain-Installationen" zu Konfigurieren, und CIDRAM-Installationen die mehrere Domains und/oder Subdomains schützen als "Multi-Domain-Installationen" zu Konfigurieren. Wenn Sie eine Multi-Domain-Installation betreiben und verschiedene Sätze von Signaturdateien für verschiedene Domains verwenden müssen, oder für verschiedene Domains unterschiedliche Konfigurationen verwenden müssen, ist dies möglich. Nach dem Laden der Konfigurationsdatei (`config.ini`), prüft CIDRAM auf die Existenz einer "Konfiguration-Überschreib Datei", die für die angefordert Domain (oder Subdomain) spezifisch ist (`die-domain-angefordert.tld.config.ini`), und wenn gefunden, alle von der Konfiguration-Überschreibt Datei definierten Konfigurationswerte werden für die Ausführungsinstanz verwendet, anstelle der von der Konfigurationsdatei definierten Konfigurationswerten. Konfiguration-Überschreibt Dateien sind identisch mit der Konfigurationsdatei, und nach eigenem Ermessen, kann entweder die Gesamtheit aller Konfigurationsdirektiven für CIDRAM enthalten, oder was auch immer kleiner Unterabschnitt erforderlich ist, die sich normalerweise von den in der Konfigurationsdatei definierten Konfigurationswerte unterscheidet. Konfiguration-Überschreibt Dateien werden nach der Domain für die sie bestimmt sind benannt (so zum Beispiel, wenn Sie eine Konfiguration-Überschreibt Dateien benötigen für die Domäne, `https://www.some-domain.tld/`, seine Konfiguration-Überschreibt Datei sollte benannt werden als `some-domain.tld.config.ini`, und sollte in dem vault neben der Konfigurationsdatei `config.ini` platziert werden). Der Domains-Name für die Ausführungsinstanz wird aus dem `HTTP_HOST`-Header der Anforderung abgeleitet; "www" wird ignoriert.

#### <a name="PAY_YOU_TO_DO_IT"></a>Ich möchte keine Zeit damit verbringen (es zu installieren, es richtig zu ordnen, u.s.w.); Kann ich dich einfach bezahlen, um alles für mich zu tun?

Vielleicht. Dies wird von Fall zu Fall bewertet. Sagen Sie uns was sie brauchen und was du anbietest. Danach können wir ihnen sagen, ob wir helfen können.

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>Kann ich Sie oder einen der Entwickler dieses Projektes für private Arbeit einstellen?

*Siehe oben.*

#### <a name="SPECIALIST_MODIFICATIONS"></a>Ich brauche spezialisierte Modifikationen, Anpassungen, u.s.w.; Können Sie helfen?

*Siehe oben.*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>Ich bin ein Entwickler, Website-Designer oder Programmierer. Kann ich die Arbeit an diesem Projekt annehmen oder anbieten?

Ja. Unsere Lizenz verbietet dies nicht.

#### <a name="WANT_TO_CONTRIBUTE"></a>Ich möchte zum Projekt beitragen; Darf ich dies machen?

Ja. Beiträge zum Projekt sind sehr willkommen. Bitte beachten Sie "CONTRIBUTING.md" für weitere Informationen.

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>Kann ich cron verwenden, um automatisch zu aktualisieren?

Ja. Eine API ist in das Frontend integriert, um über externe Skripte mit der Aktualisierungsseite zu interagieren. Ein separates Skript, "[Cronable](https://github.com/Maikuolan/Cronable)", ist verfügbar, und kann von Ihrem Cron-Manager oder Cron-Scheduler verwendet werden, um dieses und andere unterstützte Pakete automatisch zu aktualisieren (dieses Skript enthält eine eigene Dokumentation).

#### <a name="WHAT_ARE_INFRACTIONS"></a>Was sind "Verstöße"?

„Zählung den Signaturen“ und „Verstöße“ beziehen sich beide auf die Schwere und die Anzahl der Signaturen, die während einer bestimmten Anfrage ausgelöst werden, sei es aufgrund von Signaturdateien, Modulen, Hilfsregeln, oder anderweitig, aber während die „Zählung den Signaturen“ nur für diese Spezifische Anfrage bestehen bleibt, können „Verstöße“ über eine beliebige Anzahl von Anfragen bestehen bleiben, solange dies durch das `default_tracktime` bestimmt wird.

Dies bietet einer Mechanismus um sicherzustellen dass Anforderungen von potenziell gefährlichen Quellen blockiert werden können, wobei diese Quelle bereits während einer vorherigen Anforderung mit einer ausreichenden Anzahl von Verstößen blockiert wurde.

#### <a name="BLOCK_HOSTNAMES"></a>Kann CIDRAM Hostnamen blockieren?

Ja. Dazu müssen Sie eine benutzerdefinierte Moduldatei erstellen. *Siehe: [GRUNDLAGEN (FÜR MODULE)](#MODULE_BASICS)*.

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>Was kann ich für "default_dns" verwenden?

Die IP eines jeden zuverlässigen DNS-Servers sollte in der Regel ausreichen. Wenn Sie nach Vorschlägen suchen, bieten [public-dns.info](https://public-dns.info/) und [OpenNIC](https://servers.opennic.org/) umfangreiche Listen bekannter öffentlicher DNS-Server. Alternativ, sehen Sie die folgende Tabelle:

IP | Operator
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

*Hinweis: Ich mache keine Angaben oder Garantien in Bezug auf die Datenschutzpraktiken, die Sicherheit, die Wirksamkeit oder die Zuverlässigkeit von DNS-Diensten, die aufgelistet sind oder nicht. Bitte stellen Sie Ihre eigene Forschung an, wenn Sie Entscheidungen über die Wahl des DNS-Servers treffen.*

#### <a name="PROTECT_OTHER_THINGS"></a>Kann ich CIDRAM verwenden, um andere Dinge als Websites zu schützen (z.B. E-Mail-Server, FTP, SSH, IRC u.s.w.)?

Sie können (rechtlich), aber dies sollten Sie nicht (technisch; praktisch). Unsere Lizenz beschränkt nicht, welche Technologien CIDRAM implementieren, aber CIDRAM ist eine WAF (Web Application Firewall) und war schon immer zum Schutz von Webseiten gedacht. Da es nicht mit anderen Technologien entwickelt wurde, ist es unwahrscheinlich, dass es mit anderen Technologien effektiv ist, oder um für andere Technologien zuverlässigen Schutz bietet, die Umsetzung dürfte schwierig sein, und das Risiko von Falsch-Positivs und verpassten Erkennungen ist sehr hoch.

#### <a name="CDN_CACHING_PROBLEMS"></a>Werden Probleme auftreten, wenn ich CIDRAM gleichzeitig mit CDNs oder Caching-Diensten verwende?

Möglicherweise. Dies hängt von der Art des Dienstes ab und davon, wie Sie es verwenden. Im Algemeinen, wenn Sie nur statische Assets im Cache speichern (Bilder, CSS, u.s.w.; alles, was sich im Laufe der Zeit nicht ändert), sollten keine Probleme auftreten. Es kann jedoch Probleme geben, wenn Sie Daten zwischenspeichern, die andernfalls, wenn angefordert, typischerweise dynamisch generiert würde, oder wenn Sie die Ergebnisse von POST-Anfragen zwischenspeichern (dies würde Ihre Website und ihre Umgebung im Wesentlichen statisch machen, und es ist unwahrscheinlich, dass CIDRAM in einer obligatorisch statischen Umgebung einen nennenswerten Nutzen bringt). Es kann auch spezifische Konfigurationsanforderungen für CIDRAM geben, abhängig davon, welchen CDN oder Caching-Service Sie verwenden (Sie müssen sicherstellen, dass CIDRAM für den bestimmten CDN oder Caching-Dienst, den Sie verwenden, korrekt konfiguriert ist). Wenn CIDRAM nicht richtig konfiguriert wird, kann dies zu erheblich problematischen Falsch-Positive und verpassten Erkennungen verursachen.

#### <a name="DDOS_ATTACKS"></a>Wird CIDRAM meine Website vor DDoS-Angriffen schützen?

Kurze Antwort: Nein.

Etwas längere Antwort: CIDRAM wird dazu beitragen, die Auswirkungen unerwünschten Verkehrs auf Ihre Website (dadurch reduzieren Sie die Bandbreitenkosten Ihrer Website) und Hardware (z.B., die Fähigkeit Ihres Servers, Anfragen zu bearbeiten und zu bedienen) zu reduzieren, und es kann helfen, verschiedene andere, möglicherweise negative Effekte zu reduzieren, die mit unerwünschtem Verkehr verbunden sind. Es gibt jedoch zwei wichtige Dinge, an die man sich erinnern muss, um diese Frage zu verstehen.

Erstens ist CIDRAM ein PHP-Paket, und arbeitet daher auf dem Rechner, auf dem PHP installiert ist. Dies bedeutet, dass CIDRAM eine Anfrage nur sehen und blockieren kann, nachdem der Server sie bereits erhalten hat. Zweitens sollte eine effektive DDoS-Mitigation Anfragen filtern, bevor sie den vom DDoS-Angriff betroffenen Server erreichen. Im Idealfall sollten DDoS-Angriffe durch Lösungen erkannt und gemildert werden, die in der Lage sind, den mit Angriffen verbundenen Datenverkehr zu löschen oder umzuleiten, bevor er den Zielserver überhaupt erreicht.

Dies kann mit dedizierten Vor-Ort-Hardware-Lösungen, und/oder Cloud-basierte Lösungen wie dedizierten DDoS-Mitigationsdiensten, routing des DNS einer Domain über DDoS-resistente Netzwerke, Cloud-basierte Filterung, oder eine Kombination davon implementiert werden. Auf jeden Fall ist dieses Thema ein wenig zu komplex, um es mit nur ein oder zwei Paragraphen gründlich zu erklären, also würde ich empfehlen, weitere Nachforschungen anzustellen, wenn dies ein Thema ist, dem Sie nachgehen wollen. Wenn die wahre Natur von DDoS-Angriffen richtig verstanden wird, wird diese Antwort mehr Sinn machen.

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>Wenn ich Module oder Signaturdateien über die Aktualisierungsseite aktiviere oder deaktiviere, sortiert sich diese alphanumerisch in der Konfiguration. Kann ich die Art der Sortierung ändern?

Ja. Wenn Sie einige Dateien zwingen müssen, in einer bestimmten Reihenfolge ausgeführt zu werden, können Sie einige beliebige Daten vor ihren Namen in der Konfigurationsdirektive in der sie aufgeführt sind hinzufügen, durch einen Doppelpunkt getrennt. Wenn die Aktualisierungsseite anschließend die Dateien erneut sortiert, wirken sich diese zusätzlichen Daten auf die Sortierreihenfolge aus und führen dazu, dass sie in der von Ihnen gewünschten Reihenfolge ausgeführt werden, ohne diese umbenennen zu müssen.

z.B., angenommen dass eine Konfigurationsdirektive mit den folgenden Dateien ist aufgeführt:

`file1.php,file2.php,file3.php,file4.php,file5.php`

Wenn Sie `file3.php` zuerst ausführen möchten, Sie könnten etwas wie `aaa:` vor dem Namen der Datei hinzufügen:

`file1.php,file2.php,aaa:file3.php,file4.php,file5.php`

Wenn dann eine neue Datei `file6.php` aktiviert wird, wenn die Aktualisierungsseite sie alle wieder sortiert, sollte es so enden:

`aaa:file3.php,file1.php,file2.php,file4.php,file5.php,file6.php`

Gleiche Situation, wenn eine Datei deaktiviert ist. Umgekehrt, wenn Sie möchten, dass die Datei zuletzt ausgeführt wird, Sie könnten etwas wie `zzz:` vor dem Namen der Datei hinzufügen. In jedem Fall müssen Sie die betreffende Datei nicht umbenennen.

#### <a name="HOW_TO_USE_PDO"></a>Was ist ein "PDO DSN"? Wie kann ich PDO mit CIDRAM verwenden?

"PDO" ist eine Akronym für "[PHP Data Objects](https://www.php.net/manual/de/intro.pdo.php)". Es bietet eine Schnittstelle zum Verbinden von PHP mit einigen Datenbanksystemen die häufig von verschiedenen PHP-Anwendungen verwendet werden.

"DSN" ist eine Akronym für "[data source name](https://de.wikipedia.org/wiki/Data_Source_Name)". Der "PDO DSN" beschreibt wie PDO zum einer Datenbank verbindet.

CIDRAM bietet die Option, PDO für Caching-Zwecke zu verwenden. Damit dies ordnungsgemäß funktioniert, müssen Sie CIDRAM entsprechend konfigurieren, PDO aktivieren, eine neue Datenbank für CIDRAM erstellen (falls Sie noch keine Datenbank für CIDRAM in Betracht gezogen haben) und eine neue Tabelle erstellen in Ihrer Datenbank entsprechend der unten beschriebenen Struktur.

Wenn eine Datenbankverbindung erfolgreich hergestellt wurde, aber die erforderliche Tabelle jedoch nicht vorhanden ist, wird versucht sie automatisch zu erstellen. Dieses Verhalten wurde jedoch nicht ausführlich getestet und der Erfolg kann nicht garantiert werden.

Dies gilt natürlich nur, wenn CIDRAM tatsächlich PDO verwenden soll. Wenn Sie zufrieden sind, dass CIDRAM Flatfile-Caching (gemäß Standardkonfiguration) oder eine der verschiedenen anderen Caching-Optionen verwendet, müssen Sie sich nicht mit dem Einrichten von Datenbanken, Tabellen u.s.w. befassen.

In der unten beschriebenen Struktur wird "cidram" als Datenbankname verwendet. Sie können jedoch einen beliebigen Namen für Ihre Datenbank verwenden, sofern dieser Name in Ihrer DSN-Konfiguration repliziert wird.

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

Die Konfigurationsanweisung `pdo_dsn` von CIDRAM sollte wie folgt konfiguriert werden.

```
Abhängig davon, welcher Datenbanktreiber verwendet wird...
├─4d (Warnung: Experimentell, ungetestet, nicht empfohlen!)
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └Der Host, auf dem sich die Datenbank befindet.
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └Der Name der Datenbank.
│                │              │
│                │              └Die Portnummer, die beim Herstellen der
│                │               Verbindung verwendet werden soll.
│                │
│                └Der Host, auf dem sich die Datenbank befindet.
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └Der Name der Datenbank.
│    │          │
│    │          └Der Host, auf dem sich die Datenbank befindet.
│    │
│    └Mögliche Werte: "mssql", "sybase", "dblib".
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├Kann ein Pfad zu einer lokalen Datenbankdatei sein.
│                    │
│                    ├Kann eine Verbindung mit einem Host und einer Portnummer
│                    │herstellen.
│                    │
│                    └Sie sollten auf die Firebird-Dokumentation lesen wenn Sie
│                     diese verwenden möchten.
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └Die katalogisierte Datenbank, mit der eine Verbindung hergestellt
│             werden soll.
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └Die katalogisierte Datenbank, mit der eine Verbindung
│                  hergestellt werden soll.
├─mysql (Am meisten empfohlen!)
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └Die Portnummer, die beim
│                 │            │               Herstellen der Verbindung
│                 │            │               verwendet werden soll.
│                 │            │
│                 │            └Der Host, auf dem sich die Datenbank befindet.
│                 │
│                 └Der Name der Datenbank.
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├Kann auf die spezifische katalogisierte Datenbank verweisen.
│               │
│               ├Kann eine Verbindung mit einem Host und einer Portnummer
│               │herstellen.
│               │
│               └Sie sollten auf die Oracle-Dokumentation lesen wenn Sie diese
│                verwenden möchten.
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├Kann auf die spezifische katalogisierte Datenbank verweisen.
│         │
│         ├Kann eine Verbindung mit einem Host und einer Portnummer herstellen.
│         │
│         └Sie sollten auf die ODBC/DB2-Dokumentation lesen wenn Sie diese
│          verwenden möchten.
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └Der Name der Datenbank.
│               │              │
│               │              └Die Portnummer, die beim Herstellen der
│               │               Verbindung verwendet werden soll.
│               │
│               └Der Host, auf dem sich die Datenbank befindet.
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └Der Pfad zur lokalen Datenbankdatei, die verwendet werden soll.
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └Der Name der Datenbank.
                   │         │
                   │         └Die Portnummer, die beim Herstellen der
                   │          Verbindung verwendet werden soll.
                   │
                   └Der Host, auf dem sich die Datenbank befindet.
```

Wenn Sie sich nicht sicher sind, was Sie für einen bestimmten Teil Ihres DSN verwenden sollen, prüfen Sie zunächst, ob der DSN so funktioniert, wie er ist, ohne etwas zu ändern.

Beachten Sie, dass `pdo_username` und `pdo_password` mit dem Benutzernamen und dem Passwort übereinstimmen sollten, die Sie für Ihre Datenbank ausgewählt haben.

#### <a name="BLOCK_CRON"></a>CIDRAM blockiert Cronjobs; Wie kann das behoben werden?

Wenn Sie eine dedizierte Datei für Cronjobs verwenden, und wenn diese Datei bei normalen Benutzeranforderungen nicht aufgerufen werden muss (d.h., außerhalb des Kontexts von Cronjobs), die einfachste Möglichkeit dies zu beheben ist sicherzustellen, dass CIDRAM während Ihrer Cronjobs überhaupt nicht ausgeführt wird (d.h., binden Sie CIDRAM nicht in die Datei die für die Verarbeitung Ihrer Cronjobs zuständig ist).

Alternative, wenn das nicht möglich ist, aber die IP-Adresse Ihres Cron-Servers ist relativ konsistent und vorhersehbar, Sie können versuchen die IP-Adresse Ihres Cron-Servers auf eine Whiteliste zu setzen, entweder durch erstellen einer Whitelist-Signatur in einer benutzerdefinierten Signaturdatei oder durch erstellen einer Hilfsregel für es whitelistet wird. Wenn die IP-Adresse Ihres Cron-Servers regelmäßig wechselt und nicht besonders vorhersehbar ist, aber dennoch bleibt innerhalb des gleichen bestimmten Netzwerks, Sie können versuchen in Ihrer Datei `ignore.dat` den Namen des Signaturabschnitts auflisten, der für die Blockierung verantwortlich ist.

Wenn Sie all diese Ideen ausprobiert haben und keine davon für Sie funktioniert hat, oder wenn Sie Hilfe brauchen um herauszufinden wie es geht, Sie können ein neues Issue auf der Issues-Seite von CIDRAM erstellen für Hilfe zu bitten.

---


### 11. <a name="SECTION11"></a>RECHTSINFORMATION

#### 11.0 ABSCHNITT VORWORT

Dieser Abschnitt der Dokumentation beschreibt mögliche rechtliche Überlegungen zur Verwendung und Implementierung des Pakets, und um einige grundlegende verwandte Informationen zur Verfügung zu stellen. Dies kann für einige Benutzer wichtig sein, um sicherzustellen, dass die gesetzlichen Anforderungen in den Ländern eingehalten werden, in denen sie tätig sind, und einige Benutzer müssen möglicherweise ihre Website-Richtlinien in Übereinstimmung mit diesen Informationen anpassen.

Zuallererst, bitte beachten Sie, dass ich (der Autor des Pakets) weder Rechtsanwalt noch qualifizierter Jurist bin. Daher bin ich rechtlich nicht zur Rechtsberatung qualifiziert. Auch, in einigen Fällen können die genauen rechtlichen Anforderungen zwischen verschiedenen Ländern und Rechtsordnungen variieren, und diese unterschiedlichen rechtlichen Anforderungen können sich manchmal widersprechen (wie zum Beispiel, in Ländern, die [Privatsphäre](https://de.wikipedia.org/wiki/Privatsph%C3%A4re) und das [Recht auf Vergessenwerden bevorzugen](https://de.wikipedia.org/wiki/Recht_auf_Vergessenwerden), gegenüber Ländern, die eine erweiterte [Vorratsdatenspeicherung](https://de.wikipedia.org/wiki/Vorratsdatenspeicherung) bevorzugen). Berücksichtigen Sie auch, dass der Zugriff auf das Paket nicht auf bestimmte Länder oder Gerichtsbarkeiten beschränkt ist und daher die Paket-Nutzerbasis wahrscheinlich geografisch-vielfältig ist. Nach diesen Punkten kann ich nicht sagen, was es heißt, in allen Belangen für alle Nutzer "rechtskonform" zu sein. Jedoch, ich hoffe, dass die hier enthaltenen Informationen Ihnen helfen, selbst zu einer Entscheidung zu kommen, was Sie tun müssen, um im Kontext des Pakets rechtskonform zu bleiben. Wenn Sie Zweifel oder Bedenken hinsichtlich der hierin enthaltenen Informationen haben, oder wenn Sie aus rechtlicher Sicht zusätzliche Hilfe und Rat benötigen, würde ich Ihnen empfehlen, einen qualifizierten Rechtsberater zu konsultieren.

#### 11.1 HAFTUNG UND VERANTWORTUNG

Wie bereits in der Paketlizenz angegeben, wird das Paket ohne jegliche Gewährleistung bereitgestellt. Dies beinhaltet (aber ist nicht beschränkt auf) den gesamten Umfang der Haftung. Das Paket wird Ihnen zu Ihrer Bequemlichkeit zur Verfügung gestellt, in der Hoffnung, dass es nützlich sein wird, und dass es Ihnen einen Vorteil bringen wird. Sie das Paket verwenden oder implementieren, ist jedoch Ihre eigene Entscheidung. Sie sind nicht gezwungen, das Paket zu verwenden oder zu implementieren, aber wenn Sie dies tun, sind Sie für diese Entscheidung verantwortlich. Weder ich noch andere Mitwirkende des Pakets sind rechtlich verantwortlich für die Folgen der Entscheidungen, die Sie treffen, unabhängig davon, ob sie direkt, indirekt, implizit oder anderweitig sind.

#### 11.2 DRITTE

Abhängig von seiner genauen Konfiguration und Implementierung kann das Paket in einigen Fällen mit Dritten kommunizieren und Informationen teilen. Diese Informationen können in einigen Kontexten von einigen Gerichtsbarkeiten als "[personenbezogene Daten](https://de.wikipedia.org/wiki/Personenbezogene_Daten)" (oder "PII") definiert werden.

Wie diese Informationen von diesen Dritten verwendet werden können, unterliegt den verschiedenen Richtlinien, die von diesen Dritten festgelegt wurden, und liegt außerhalb des Anwendungsbereichs dieser Dokumentation. In allen diesen Fällen jedoch kann der Austausch von Informationen mit diesen Dritten deaktiviert werden. In allen diesen Fällen liegt es in Ihrer Verantwortung, wenn Sie sich dafür entscheiden, Ihre Bedenken hinsichtlich der Vertraulichkeit, Sicherheit, und Verwendung von personenbezogenen Daten durch diese Dritten zu untersuchen. Wenn irgendwelche Zweifel bestehen oder wenn Sie mit dem Verhalten dieser Dritten in Bezug auf PII nicht zufrieden sind, ist es möglicherweise am besten, den gesamten Informationsaustausch mit diesen Dritten zu deaktivieren.

Aus Gründen der Transparenz wird im Folgenden beschrieben, welche Art von Informationen, und mit wem, geteilt werden.

##### 11.2.0 HOSTNAME-SUCHE

Wenn Sie Funktionen oder Module verwenden, die mit Hostnamen arbeiten (z.B., "Schlechte Hosts Blocker-Modul", "tor project exit nodes block module", oder "Suchmaschinen-Verifizierung", u.s.w.), muss CIDRAM in der Lage sein, den Hostnamen eingehender Anfragen irgendwie zu erhalten. Typischerweise wird dazu der Hostname der IP-Adresse eingehender Anforderungen von einem DNS-Server angefordert, oder die Informationen über die Funktionalität angefordert, die vom System bereitgestellt werden, auf dem CIDRAM installiert ist (dies wird typischerweise als "Hostname-Suche" bezeichnet). Die standardmäßig definierten DNS-Server gehören zu [Google DNS](https://dns.google.com/) (dies kann jedoch einfach über die Konfiguration geändert werden). Die genauen Dienste, mit denen kommuniziert wird, sind konfigurierbar und hängen von der Konfiguration des Pakets ab. Wenn Sie Funktionen verwenden, die von dem System bereitgestellt werden, auf dem CIDRAM installiert ist, müssen Sie sich an Ihren Systemadministrator wenden, um zu ermitteln, welche Routen Hostnamen-Lookups verwenden. Hostnamen-Suchen können in CIDRAM verhindert werden, indem die betroffenen Module vermieden oder die Paketkonfiguration entsprechend Ihren Anforderungen geändert wird.

*Relevante Konfigurationsdirektiven:*
- `general` -> `default_dns`
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`
- `general` -> `force_hostname_lookup`
- `general` -> `allow_gethostbyaddr_lookup`

##### 11.2.2 VERIFIZIERUNG VON SUCHMASCHINEN UND SOCIAL MEDIA

Wenn die Verifizierung von Suchmaschinen aktiviert ist, versucht CIDRAM "Forward-DNS-Lookups" durchzuführen, um zu überprüfen, ob Anfragen, die behaupten, von Suchmaschinen zu stammen, authentisch sind. Gleichfalls, wenn die Verifizierung von Social Media aktiviert ist, macht CIDRAM das gleiche für scheinbare Social-Media-Anfragen. Um dies zu tun, verwendet es den [Google DNS](https://dns.google.com/)-Dienst, um IP-Adressen aus den Hostnamen dieser eingehenden Anfragen aufzulösen (in diesem Prozess werden die Hostnamen dieser eingehenden Anfragen für den Dienst freigegeben).

*Relevante Konfigurationsdirektiven:*
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`

##### 11.2.3 CAPTCHA

CIDRAM unterstützt reCAPTCHA und hCAPTCHA. Sie benötigen API-Schlüssel, um ordnungsgemäß zu funktionieren. Sie sind standardmäßig deaktiviert, können jedoch durch Konfigurieren der erforderlichen API-Schlüssel aktiviert werden. Wenn diese Option aktiviert ist, kann eine Kommunikation zwischen dem Dienst und CIDRAM oder dem Browser des Benutzers erfolgen. Dies kann möglicherweise die Übermittlung von Informationen wie die IP-Adresse des Benutzers, den Benutzeragenten, das Betriebssystem und andere Details zur Anfrage verfügbar.

##### 11.2.4 STOP FORUM SPAM

[Stop Forum Spam](https://www.stopforumspam.com/) ist ein fantastischer, frei verfügbarer Dienst, mit dem Sie Foren, Blogs und Websites vor Spammern schützen können. Dies geschieht durch Bereitstellung einer Datenbank bekannter Spammer und einer API, mit der überprüft werden kann, ob eine IP-Adresse, ein Benutzername oder eine E-Mail-Adresse in der Datenbank aufgeführt ist.

CIDRAM bietet ein optionales Modul, das diese API nutzt, um zu prüfen, ob die IP-Adresse eingehender Anfragen zu einem mutmaßlichen Spammer gehört. Das Modul wird nicht standardmäßig installiert, aber wenn Sie es installieren, können Benutzer-IP-Adressen mit der Stop Forum Spam API in Übereinstimmung mit dem beabsichtigten Zweck des Moduls geteilt werden. Wenn das Modul installiert wird, kommuniziert CIDRAM mit dieser API immer dann, wenn eine eingehende Anfrage eine Ressource anfordert, die von CIDRAM als eine Art von Ressource erkannt wird, die häufig von Spammern angegriffen wird (wie Einloggen-Seiten, Registrierungsseiten, E-Mail-Verifizierungsseiten, Kommentarformulare, u.s.w.).

##### 11.2.5 ABUSEIPDB

CIDRAM bietet ein optionales Modul zum Blockieren missbräuchlicher IP-Adressen mithilfe der [AbuseIPDB](https://www.abuseipdb.com/) API. Das Modul wird nicht standardmäßig installiert, aber wenn Sie es installieren, können Benutzer-IP-Adressen mit der AbuseIPDB API in Übereinstimmung mit dem beabsichtigten Zweck des Moduls geteilt werden.

##### 11.2.6 BGPVIEW

CIDRAM bietet ein optionales Modul für die Suche nach ASNs und Ländercodes mithilfe der [BGPView](https://bgpview.io/)-API. Diese Suchvorgänge bieten die Möglichkeit, Anfragen auf der Grundlage ihres ASNs oder ihres Herkunftslandes zu blockieren oder auf die Whitelist zu setzen. Das Modul wird nicht standardmäßig installiert, aber wenn Sie es installieren, können Benutzer-IP-Adressen mit der BGPView API in Übereinstimmung mit dem beabsichtigten Zweck des Moduls geteilt werden.

#### 11.3 PROTOKOLLIERUNG

Protokollierung ist aus verschiedenen Gründen ein wichtiger Teil von CIDRAM. Es kann schwierig sein, falsche Positive zu diagnostizieren und zu beheben, wenn die Blockereignisse, die sie verursachen, nicht protokolliert werden. Ohne Blockereignisse zu protokollieren, kann es schwierig sein, exakt festzustellen, wie gut CIDRAM in einem bestimmten Kontext funktioniert, und es kann schwierig sein zu bestimmen, wo die Defizite liegen und welche Änderungen möglicherweise an der Konfiguration oder den Signaturen vorgenommen werden müssen, damit es weiterhin wie beabsichtigt funktioniert. Ungeachtet, die Protokollierung ist möglicherweise nicht für alle Benutzer wünschenswert und bleibt vollständig optional. In CIDRAM ist die Protokollierung standardmäßig deaktiviert. Um es zu aktivieren, muss CIDRAM entsprechend konfiguriert werden.

Zusätzlich, ob Protokollierung rechtlich zulässig ist, und in welchem Umfang es rechtlich zulässig ist (z.B., die Arten von Informationen, die protokolliert werden können, für wie lange und unter welchen Umständen), kann je nach Rechtsprechung und Kontext (z.B., ob Sie als Einzelperson, als juristische Person tätig sind, und ob auf kommerzieller oder nichtkommerzieller Basis), in dem CIDRAM implementiert wird, variieren. Es kann daher sinnvoll sein, diesen Abschnitt sorgfältig durchzulesen.

Es gibt mehrere Arten der Protokollierung, die CIDRAM ausführen kann. Verschiedene Arten der Protokollierung beinhalten verschiedene Arten von Informationen, aus verschiedenen Gründen.

##### 11.3.0 BLOCKEREIGNISSE

Der primäre Art der Protokollierung, den CIDRAM ausführen kann, bezieht sich auf "Blockereignisse". Diese Art der Protokollierung bezieht sich auf das Blockieren einer Anforderung durch CIDRAM und kann in drei verschiedenen Formaten bereitgestellt werden:
- Menschenlesbar oder benutzerfreundliche Protokolldateien.
- Apache-Stil Protokolldateien.
- Serialisierte Protokolldateien.

Ein Blockereignis, das in einer für menschenlesbaren Protokolldatei protokolliert wird, sieht in etwa wie folgt aus (als Beispiel):

```
ID: 1234
Script-Version: CIDRAM v1.6.0
Datum/Uhrzeit: Day, dd Mon 20xx hh:ii:ss +0000
IP-Adresse: x.x.x.x
Hostname: dns.hostname.tld
Zählung den Signaturen: 1
Referenz für den Signaturen: x.x.x.x/xx
Warum blockierte: Cloud-Service ("Netzwerkname", Lxx:Fx, [XX])!
Benutzeragent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
Rekonstruierte URI: https://your-site.tld/index.php
Status der CAPTCHA: Aktiviert.
```

Das gleiche Blockereignis, das in einer Protokolldatei im Apache-Stil protokolliert wird, würde ungefähr so aussehen:

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

Ein protokolliertes Blockereignis enthält normalerweise die folgenden Informationen:
- Eine ID-Nummer, die auf das Blockereignis verweist.
- Die derzeit verwendete Version von CIDRAM.
- Datum und Uhrzeit des Auftretens des Blockereignisses.
- Die IP-Adresse der verbannten Anfrage.
- Der Hostname der IP-Adresse der verbannten Anfrage (wenn verfügbar).
- Die Anzahl der Signaturen, die von der Anfrage ausgelöst wurden.
- Verweise auf die ausgelösten Signaturen.
- Verweise auf die Gründe für das Blockereignis und einige grundlegende Debuginformationen.
- Der Benutzeragent der verbannten Anfrage (d.h., wie sich die anfragende Einheit gegenüber der Anfrage identifiziert hat).
- Eine Rekonstruktion der Identifizierung für die ursprünglich angeforderte Ressource.
- Der CAPTCHA-Status für die aktuelle Anfrage (falls relevant).

*Die Konfigurationsdirektiven, die für diese Art der Protokollierung und für jedes der drei verfügbaren Formate verantwortlich sind:*
- `general` -> `logfile`
- `general` -> `logfile_apache`
- `general` -> `logfile_serialized`

Wenn diese Direktiven leer bleiben, bleibt diese Art der Protokollierung deaktiviert.

##### 11.3.1 CAPTCHA PROTOKOLLIERUNG

Diese Art der Protokollierung bezieht sich speziell auf CAPTCHA-Instanzen und tritt nur auf, wenn ein Benutzer versucht, eine CAPTCHA-Instanz abzuschließen.

Ein CAPTCHA-Protokolleintrag enthält die IP-Adresse des Benutzers, der versucht, eine CAPTCHA-Instanz abzuschließen, das Datum und die Uhrzeit des Versuchs, und der Status der CAPTCHA. Ein CAPTCHA-Protokolleintrag sieht in etwa wie folgt aus (als Beispiel):

```
IP-Adresse: x.x.x.x - Date/Time: Day, dd Mon 20xx hh:ii:ss +0000 - Status der CAPTCHA: Gelungen!
```

*Die für die CAPTCHA-Protokollierung verantwortliche Konfigurationsdirektiven lautet:*
- `recaptcha` -> `logfile`
- `hcaptcha` -> `logfile`

##### 11.3.2 FRONTEND PROTOKOLLIERUNG

Diese Art der Protokollierung bezieht sich auf Frontend-Einloggen-Versuchen und tritt nur auf, wenn ein Benutzer versucht, sich am Frontend anzumelden (vorausgesetzt, der Frontend-Zugriff ist aktiviert).

Ein Frontend-Protokolleintrag enthält die IP-Adresse des Benutzers, der sich anzumelden versucht, das Datum und die Uhrzeit des Versuchs, und die Ergebnisse des Versuchs (erfolgreich eingeloggt oder könnte sich nicht einloggen). Ein Frontend-Protokolleintrag sieht in etwa wie folgt aus (als Beispiel):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Eingeloggt.
```

*Die für die Frontend-Protokollierung verantwortliche Konfigurationsdirektiven lautet:*
- `general` -> `frontend_log`

##### 11.3.3 PROTOKOLLROTATION

Möglicherweise möchten Sie Protokolle nach einer gewissen Zeit löschen, oder müssen dies gesetzlich tun (d.h., die Zeitspanne, die für die Aufbewahrung von Protokolldateien gesetzlich zulässig ist, kann gesetzlich beschränkt sein). Sie können dies erreichen, indem Sie Datums/Zeitmarkierungen in die Namen Ihrer Protokolldateien einfügen, die in Ihrer Paketkonfiguration festgelegt sind (z.B., `{yyyy}-{mm}-{dd}.log`), und dann Aktivieren der Protokollrotation (Protokollrotation ermöglicht es Ihnen, einige Aktionen in Protokolldateien durchzuführen, wenn bestimmte Limits überschritten werden).

Beispielsweise: Wenn ich gesetzlich dazu verpflichtet wäre, Protokolldateien nach 30 Tagen zu löschen, könnte ich `{dd}.log` in den Namen meiner Protokolldateien angeben (`{dd}` steht für Tage), setze den Wert von `log_rotation_limit` auf 30, und setze den Wert von `log_rotation_action` auf `Delete`.

Umgekehrt, wenn Sie Protokolldateien für einen längeren Zeitraum aufbewahren müssen, Sie könnten entweder überhaupt keine Protokollrotation verwenden, oder Sie könnten den Wert von `log_rotation_action` auf `Archive` setzen, um Protokolldateien zu komprimieren, wodurch der Gesamtbetrag des belegten Speicherplatzes reduziert wird.

*Relevante Konfigurationsdirektiven:*
- `general` -> `log_rotation_limit`
- `general` -> `log_rotation_action`

##### 11.3.4 PROTOKOLL-TRUNKIERUNG

Es ist auch möglich, um einzelne Protokolldateien zu trunkieren, wenn sie eine bestimmte Größe überschreiten, falls Sie dies benötigen oder tun möchten.

*Relevante Konfigurationsdirektiven:*
- `general` -> `truncate`

##### 11.3.5 IP-ADRESSE PSEUDONYMISIERUNG

Erstens, wenn Sie mit dem Begriff nicht vertraut sind, "Pseudonymisierung" bezieht sich auf die Verarbeitung personenbezogener Daten, so dass sie ohne zusätzliche Informationen nicht mehr für eine bestimmte Person identifiziert werden können, und vorausgesetzt, dass diese zusätzlichen Informationen getrennt aufbewahrt werden, und vorbehaltlich technischer und organisatorischer Maßnahmen, um sicherzustellen, dass personenbezogene Daten für keine natürliche Person identifiziert werden können.

Die folgenden Ressourcen können helfen, es genauer zu erklären:
- [[johner-institut.de] Anonymisierung und Pseudonymisierung](https://www.johner-institut.de/blog/gesundheitswesen/anonymisierung-und-pseudonymisierung/)
- [[datenschutzbeauftragter-info.de] Pseudonymisierung – was ist das eigentlich?](https://www.datenschutzbeauftragter-info.de/pseudonymisierung-was-ist-das-eigentlich/)
- [[Wikipedia] Anonymisierung und Pseudonymisierung](https://de.wikipedia.org/wiki/Anonymisierung_und_Pseudonymisierung)

Unter gewissen Umständen sind Sie gesetzlich dazu verpflichtet, alle PII, die gesammelt, verarbeitet oder gespeichert werden, zu anonymisieren oder zu pseudonymisieren. Obwohl dieses Konzept schon seit einiger Zeit besteht, erwähnt und ermutigt die GDPR/DSGVO ausdrücklich die "Pseudonymisierung" der PII.

CIDRAM ist in der Lage, IP-Adressen zu pseudonymisieren, wenn Sie sie protokollieren, wenn Sie dies benötigen oder tun möchten. Wenn CIDRAM IP-Adressen pseudonymisiert, wird das letzte Oktett von IPv4-Adressen und alles nach dem zweiten Teil von IPv6-Adressen durch ein "x" dargestellt (runden effektiv IPv4-Adressen in Subnetz 24 und IPv6-Adressen in Subnetz 32 ab).

*Hinweis: Der IP-Adress-Pseudonymisierungsprozess von CIDRAM hat keinen Einfluss auf die IP-Tracking-Funktion von CIDRAM. Wenn dies ein Problem für Sie darstellt, ist es möglicherweise am besten, das IP-Tracking vollständig zu deaktivieren.*

*Relevante Konfigurationsdirektiven:*
- `legal` -> `pseudonymise_ip_addresses`

##### 11.3.6 WEGLASSUNG VON PROTOKOLLINFORMATIONEN

Wenn Sie einen Schritt weiter gehen wollen, indem Sie verhindern, dass bestimmte Arten von Informationen vollständig protokolliert werden, ist dies ebenfalls möglich. CIDRAM stellt Konfigurationsdirektiven bereit, um zu steuern, ob IP-Adressen, Hostnamen und Benutzeragenten in Protokolldateien enthalten sind. Standardmäßig sind alle drei Datenpunkte in den Protokollen enthalten, wenn sie verfügbar sind. Wenn Sie eine dieser Konfigurationsdirektiven auf `true` setzen, werden die entsprechenden Informationen aus den Protokollen weggelassen.

*Hinweis: Es gibt keinen Grund, um IP-Adressen zu pseudonymisieren, wenn sie vollständig aus den Protokollen entfernt werden.*

*Relevante Konfigurationsdirektiven:*
- `legal` -> `omit_ip`
- `legal` -> `omit_hostname`
- `legal` -> `omit_ua`

##### 11.3.7 STATISTIKEN

CIDRAM ist optional in der Lage, Statistiken wie die Gesamtzahl der seit einem bestimmten Zeitpunkt aufgetretenen Blockereignisse oder CAPTCHA-Instanzen zu verfolgen. Diese Funktion ist standardmäßig deaktiviert, kann jedoch über die Paketkonfiguration aktiviert werden. Diese Funktion verfolgt nur die Gesamtzahl der aufgetretenen Ereignisse, und enthält keine Informationen zu bestimmten Ereignissen (und sollten daher nicht als PII betrachtet werden).

*Relevante Konfigurationsdirektiven:*
- `general` -> `statistics`

##### 11.3.8 KRYPTOGRAPHIE

CIDRAM verwendet keine [Kryptografie](https://de.wikipedia.org/wiki/Kryptographie) zu den Cache oder Protokollierung. Kryptographie für den Cache oder Protokollierung kann in Zukunft eingeführt werden, aber es gibt derzeit keine konkreten Pläne dafür. Wenn Sie befürchten, dass unbefugte Dritte Zugang zu Teilen von CIDRAM erhalten, die PII oder vertrauliche Informationen wie Cache oder Protokolle enthalten, würde ich empfehlen, CIDRAM nicht an einem öffentlich zugänglichen Ort zu installieren (z.B., installieren Sie CIDRAM außerhalb des Standard-Verzeichnisses `public_html` oder eines entsprechenden Verzeichnisses, das für die meisten Standard-Webserver verfügbar ist) und dass entsprechend restriktive Berechtigungen für das Verzeichnis erzwungen werden, in dem sie sich befinden (insbesondere für das vault verzeichnis). Wenn dies nicht ausreicht, um Ihre Bedenken auszuräumen, konfigurieren Sie CIDRAM so, dass die Arten von Informationen, die Ihre Bedenken verursachen, nicht erfasst oder protokolliert werden (z.B. durch Deaktivieren der Protokollierung).

#### 11.4 COOKIES

CIDRAM setzt [Cookies](https://de.wikipedia.org/wiki/HTTP-Cookie) an zwei Stellen in seiner Codebasis. Erstens, wenn ein Benutzer eine CAPTCHA-Instanz erfolgreich abgeschlossen hat (und angenommen, dass `lockuser` auf `true` gesetzt ist), CIDRAM setzt einen Cookie, um sich bei nachfolgenden Anfragen daran erinnern zu können, dass der Benutzer bereits eine CAPTCHA-Instanz abgeschlossen hat, damit muss der Benutzer nicht ständig aufgefordert werden, eine CAPTCHA-Instanz bei nachfolgenden Anfragen zu vervollständigen. Zweitens, wenn sich ein Benutzer erfolgreich am Frontend eingeloggt, CIDRAM setzt eine einen Cookie, um sich den Benutzer für nachfolgende Anfragen merken zu können (d.h., Cookies dienen zur Authentifizierung des Benutzers bei einer Einloggen-Sitzung).

In beiden Fällen werden Cookie-Warnungen angezeigt (falls zutreffend), die den Benutzer warnen, dass Cookies gesetzt werden, wenn sie die relevanten Aktionen ausführt. An anderen Stellen in der Codebasis werden keine Cookies gesetzt.

*Hinweis: Die "unsichtbaren" CAPTCHA-APIs sind in einigen Ländern möglicherweise nicht mit den Cookie-Gesetzen kompatibel, und sollte von Websites die solchen Gesetzen unterliegen vermieden werden. Es kann vorzuziehen sein stattdessen die anderen bereitgestellten APIs zu verwenden, oder CAPTCHA vollständig zu deaktivieren.*

*Relevante Konfigurationsdirektiven:*
- `general` -> `disable_frontend`
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 11.5 VERMARKTUNG UND WERBUNG

CIDRAM sammelt und verarbeitet keine Informationen für der Zweck des Vermarktung oder Werbung, und weder verkauft noch profitiert von gesammelten oder protokolliert Informationen. CIDRAM ist kein kommerzielles Unternehmen, noch bezieht es sich auf irgendwelche kommerziellen Interessen, daher macht es keinen Sinn, diese Dinge zu tun. Dies ist seit Beginn des Projekts der Fall und ist auch heute noch der Fall. Außerdem, diese Dinge wären kontraproduktiv für den Geist und den beabsichtigten Zweck des gesamten Projekts, und so lange ich das Projekt weiterführen, wird nie passieren.

#### 11.6 DATENSCHUTZERKLÄRUNG

Unter bestimmten Umständen können Sie gesetzlich dazu verpflichtet sein, auf allen Seiten und Abschnitten Ihrer Website einen Link zu Ihrer Datenschutzerklärung deutlich anzuzeigen. Dies kann wichtig sein, um sicherzustellen, dass die Benutzer genau über Ihre genauen Datenschutzpraktiken, die Arten von personenbezogenen Daten, die Sie sammeln, und über Ihre beabsichtigte Verwendung informiert sind. Um einen solchen Link auf der Seite "Zugriff verweigert" von CIDRAM einzubinden, wird eine Konfigurationsdirektive bereitgestellt, um die URL zu Ihrer Datenschutzerklärung anzugeben.

*Hinweis: Es wird dringend empfohlen, dass Ihre Datenschutzerklärung nicht hinter dem Schutz von CIDRAM steht. Wenn CIDRAM Ihre Datenschutzerklärung schützt und ein von CIDRAM blockierter Benutzer auf den Link zu Ihrer Datenschutzerklärung klickt, sie werden nur erneut blockiert, und können Ihre Datenschutzerklärung nicht sehen. Idealerweise sollten Sie eine Link zu einer statischen Kopie Ihrer Datenschutzerklärung erstellen, z.B. eine HTML-Seite oder eine Nur-Text-Datei, die nicht durch CIDRAM geschützt ist.*

*Relevante Konfigurationsdirektiven:*
- `legal` -> `privacy_policy`

#### 11.7 GDPR/DSGVO

Die Datenschutz-Grundverordnung (DSGVO) ist eine Verordnung der Europäischen Union, die am 25. Mai 2018 in Kraft tritt. Das Hauptziel der Verordnung besteht darin, den EU-Bürgern und EU-Anwohnern die Kontrolle über ihre eigenen personenbezogenen Daten zu ermöglichen und die Regulierung innerhalb der EU in Bezug auf Privatsphäre und personenbezogene Daten zu vereinheitlichen.

Die Verordnung enthält spezifische Bestimmungen für die Verarbeitung "[personenbezogenen Daten](https://de.wikipedia.org/wiki/Personenbezogene_Daten)" (PII) von "betroffenen Personen" (jede identifizierte oder identifizierbare natürliche Person) aus oder innerhalb der EU. Um der Verordnung zu entsprechen, müssen "Unternehmen" (gemäß der Definition in der Verordnung) und alle relevanten Systeme und Prozesse "[Datenschutz durch Design](https://digitalcourage.de/blog/2015/was-ist-privacy-design)" standardmäßig implementieren, müssen die höchstmögliche Privatsphäre Einstellungen verwenden, müssen die erforderlichen Sicherheitsmaßnahmen für gespeicherte oder verarbeitete Informationen implementieren (einschließlich, aber nicht beschränkt auf die Durchführung der Pseudonymisierung oder vollständigen Anonymisierung von Daten), müssen die Art der Daten, die sie sammeln, eindeutig und eindeutig angeben, aus welchen Gründen, für wie lange sie diese Daten speichern und ob sie diese Daten an Dritte weitergeben, die Arten von Daten, die mit Dritten geteilt werden, wie, warum, u.s.w.

Daten dürfen nicht verarbeitet werden, es sei denn, es gibt eine gesetzliche Grundlage dafür, wie in der Verordnung definiert. Im Allgemeinen bedeutet dies, dass die Verarbeitung der Daten eines Datensubjekts auf gesetzlicher Grundlage gemäß den gesetzlichen Verpflichtungen oder nur nach ausdrücklicher, gut informierter und eindeutiger Zustimmung der betroffenen Person erfolgen muss.

Da sich Aspekte der Verordnung mit der Zeit weiterentwickeln können, um die Verbreitung veralteter Informationen zu vermeiden, ist es möglicherweise besser, die Vorschrift von einer autoritativen Quelle zu erfahren, als einfach die relevanten Informationen hier in die Paketdokumentation einzubeziehen (was eventuell mit der Entwicklung der Verordnung veraltet).

[EUR-Lex](https://eur-lex.europa.eu/) (ein Teil der offiziellen Website der Europäischen Union, die Informationen über EU-Recht bietet) bietet umfangreiche Informationen zu GDPR/DSGVO, die zum Zeitpunkt der Erstellung in 24 Sprachen verfügbar sind, und im PDF-Format heruntergeladen werden können. Ich würde definitiv empfehlen, die Informationen zu lesen, die sie zur Verfügung stellen, um mehr über GDPR/DSGVO zu erfahren:
- [VERORDNUNG (EU) 2016/679 DES EUROPÄISCHEN PARLAMENTS UND DES RATES](https://eur-lex.europa.eu/legal-content/DE/TXT/?uri=celex:32016R0679)

[Intersoft Consulting](https://www.intersoft-consulting.de/) bietet auch umfassende Informationen über DSGVO, die in deutscher und englischer Sprache verfügbar sind und die nützlich sein könnten, um mehr über GDPR/DSGVO zu erfahren:
- [Datenschutz-Grundverordnung (EU-DSGVO) als übersichtliche Website](https://dsgvo-gesetz.de/)

Alternativ gibt es einen kurzen (nicht autoritativen) Überblick über die GDPR/DSGVO bei Wikipedia:
- [Datenschutz-Grundverordnung](https://de.wikipedia.org/wiki/Datenschutz-Grundverordnung)

---


Zuletzt aktualisiert: 28. März 2022 (2022.03.28).
