## Documentazione per CIDRAM v4 (Italiano).

### Contenuti
- 1. [PREAMBOLO](#user-content-SECTION1)
- 2. [COME INSTALLARE](#user-content-SECTION2)
- 3. [COME USARE](#user-content-SECTION3)
- 4. [GESTIONE FRONT-END](#user-content-SECTION4)
- 5. [OPZIONI DI CONFIGURAZIONE](#user-content-SECTION5)
- 6. [FIRMA FORMATO](#user-content-SECTION6)
- 7. [CONOSCIUTI COMPATIBILITÀ PROBLEMI](#user-content-SECTION7)
- 8. [DOMANDE FREQUENTI (FAQ)](#user-content-SECTION8)
- 9. [INFORMAZIONE LEGALE](#user-content-SECTION9)
- 10. [AGGIORNAMENTO DA VERSIONI PRINCIPALI PRECEDENTI](#user-content-SECTION10)

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### 1. <a name="SECTION1"></a>PREAMBOLO

CIDRAM (Classless Inter-Domain Routing Access Manager) è uno script PHP progettato per proteggere i siti web bloccando le richieste provenienti da indirizzi IP considerati come fonti di traffico indesiderato, includendo (ma non limitato a) il traffico proveniente da punti d'accesso non umani, servizi cloud, spambot, scraper, ecc. Questo è possibile calcolando i possibili CIDR degli indirizzi IP forniti da richieste in entrata e poi confrontando questi possibili CIDR con i file di firme (queste file di firme contengono liste di CIDR di indirizzi IP considerati come fonti di traffico indesiderato); se vengono trovati riscontri, le richieste sono bloccate.

*(Vedere: [Che cos'è un "CIDR"?](#user-content-WHAT_IS_A_CIDR)).*

[CIDRAM](https://cidram.github.io/) COPYRIGHT 2016 e oltre GNU/GPLv2 [Caleb M (Maikuolan)](https://github.com/Maikuolan).

Questo script è un software "libero"; è possibile ridistribuirlo e/o modificarlo sotto i termini della GNU General Public License come pubblicato dalla Free Software Foundation; o la versione 2 della licenza, o (a propria scelta) una versione successiva. Questo script è distribuito nella speranza che possa essere utile, ma SENZA ALCUNA GARANZIA; senza neppure la implicita garanzia di COMMERCIABILITÀ o IDONEITÀ PER UN PARTICOLARE SCOPO. Vedere la GNU General Public License per ulteriori dettagli, situato nella `LICENSE.txt` file e disponibili anche da:
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

CIDRAM può essere scaricato gratuitamente da qui:
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM).

Questo documento e le sue varie traduzioni possono essere trovati qui:
- [GitHub](https://github.com/CIDRAM/Docs).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram-docs).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM-Docs).

---


### 2. <a name="SECTION2"></a>COME INSTALLARE

#### 2.0 INSTALLAZIONE MANUALE

In primo luogo, avrai bisogno di una nuova copia di CIDRAM. È possibile scaricare un archivio dell'ultima versione di CIDRAM dal repository [CIDRAM/CIDRAM](https://github.com/CIDRAM/CIDRAM). In particolare, avrai bisogno di una nuova copia della directory "vault" (tutto dall'archivio tranne la directory "vault" e il suo contenuto può essere tranquillamente cancellato o ignorato).

Prima della v3, era necessario installare CIDRAM da qualche parte all'interno della radice pubblica per poter accedere al front-end CIDRAM. Tuttavia, dalla v3 in poi, non è necessario, e per massimizzare la sicurezza e prevenire l'accesso non autorizzato a CIDRAM e ai suoi file, si consiglia invece di installare CIDRAM al di *fuori* della tua root pubblica. Non importa esattamente dove scegli di installare CIDRAM, a patto che sia in un posto accessibile da PHP, in un posto ragionevolmente sicuro, e in un posto di cui sei soddisfatto. Inoltre non è più necessario mantenere il nome della directory "vault", quindi puoi rinominare "vault" con il nome che preferisci (ma per comodità, la documentazione continuerà a fare riferimento ad essa come alla directory "vault").

Quando sei pronto, carica la directory "vault" nella posto scelta e assicurati che abbia i permessi necessari affinché PHP possa scrivere nella directory (a seconda del sistema in questione, a volte non dovrai fare nulla, oa volte dovrai impostare CHMOD 755 nella directory, o se ci sono problemi con 755, puoi provare 777, ma 777 non è raccomandato perché meno sicuro).

Successivamente, affinché CIDRAM sia in grado di proteggere la tua base di codice o CMS, dovrai creare un "punto di ingresso". Un tale punto di ingresso è costituito da tre cose:

1. Inclusione del file "loader.php" in un punto appropriato nella tua codebase o CMS.
2. Istanziazione del CIDRAM core.
3. Chiamando il metodo "protect".

Un semplice esempio:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

Se stai usando un server web Apache e hai accesso a `php.ini`, puoi usare la direttiva `auto_prepend_file` per anteporre CIDRAM ogni volta che viene effettuata una richiesta PHP. In tal caso, il posto più appropriato per creare il tuo punto di ingresso sarebbe nel proprio file, e quindi citeresti quel file nella direttiva `auto_prepend_file`.

Esempio:

`auto_prepend_file = "/path/to/your/entrypoint.php"`

O questo nel file `.htaccess`:

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

In altri casi, il posto più appropriato per creare il tuo punto di ingresso sarebbe il più presto possibile all'interno della tua base di codice o CMS per essere sempre caricato ogni volta che qualcuno accede a qualsiasi pagina dell'intero sito web. Se la tua base di codice utilizza un "bootstrap", un buon esempio sarebbe proprio all'inizio del tuo file "bootstrap". Se la tua base di codice ha un file centrale responsabile della connessione al tuo database, un altro buon esempio sarebbe proprio all'inizio di quel file centrale.

#### 2.1 INSTALLARE CON COMPOSER

[CIDRAM è registrata con Packagist](https://packagist.org/packages/cidram/cidram), e così, se si ha familiarità con Composer, è possibile utilizzare Composer per l'installazione di CIDRAM.

`composer require cidram/cidram`

#### 2.2 INSTALLARE PER WORDPRESS

[CIDRAM è registrato come un plugin con il database dei plugin di WordPress](https://wordpress.org/plugins/cidram/), ed è possibile installare CIDRAM direttamente dalla pagina dei Plugin. È possibile installarlo nello stesso modo di qualsiasi altro plugin, e non sono necessari altri interventi.

*Avvertimento: L'aggiornamento di CIDRAM tramite il dashboard dei plugin provoca un'installazione pulita! Se hai personalizzato l'installazione (cambiato la tua configurazione, installati i moduli, ecc), queste personalizzazioni verranno perse quando si aggiorna tramite la pagina dei plugin! I file di registro verranno persi anche quando vengono aggiornati tramite la pagina dei plugin! Per preservare i file di registro e le personalizzazioni, aggiorna tramite la pagina di aggiornamenti del front-end per CIDRAM.*

#### 2.3 CONFIGURAZIONE E PERSONALIZZAZIONE

Si consiglia vivamente di rivedere la configurazione della nuova installazione per poterla adattare alle proprie esigenze. Potresti anche voler installare moduli aggiuntivi, file di firma, creare regole ausiliarie, o implementare altre personalizzazioni in modo che la tua installazione sia in grado di soddisfare al meglio le tue esigenze. Consiglio di usare il front-end per fare queste cose.

---


### 3. <a name="SECTION3"></a>COME USARE

CIDRAM dovrebbe bloccare automaticamente le richieste indesiderate al suo sito senza richiedere alcuna assistenza manuale, a parte la sua installazione iniziale.

È possibile personalizzare la sua configurazione e quali CIDR devono essere bloccati, modificando il vostro file di configurazione e/o file di firme.

Se si incontrano dei falsi positivi, per favore, contattatemi e fatemelo sapere. *(Vedere: [Che cosa è un "falso positivo"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM può essere aggiornato manualmente o tramite il front-end. CIDRAM può anche essere aggiornato tramite Composer o WordPress, se originariamente installato tramite tali mezzi.

---


### 4. <a name="SECTION4"></a>GESTIONE FRONT-END

#### 4.0 QUAL È IL FRONT-END.

Il front-end fornisce un modo conveniente e facile da mantenere, gestire e aggiornare l'installazione CIDRAM. È possibile visualizzare, condividere e scaricare file di log attraverso la pagina di log, è possibile modificare la configurazione attraverso la pagina di configurazione, è possibile installare e disinstallare i componenti attraverso la pagina degli aggiornamenti, e si può caricare, scaricare e modificare i file nel vault tramite il file manager.

#### 4.1 COME ACCEDERE IL FRONT-END.

In modo simile a come avevi bisogno di creare un punto di ingresso affinché CIDRAM protegga il tuo sito Web, dovrai anche creare un punto di ingresso per accedere al front-end. Un tale punto di ingresso è costituito da tre cose:

1. Inclusione del file "loader.php" in un punto appropriato nella tua codebase o CMS.
2. Istanziazione del CIDRAM front-end.
3. Chiamando il metodo "view".

Un semplice esempio:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

La classe "FrontEnd" estende la classe "Core", il che significa che se lo si desidera, è possibile chiamare il metodo "protect" prima di chiamare il metodo "view" per impedire al traffico potenzialmente indesiderato di accedere al front-end. Farlo è del tutto facoltativo.

Un semplice esempio:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

Il posto più appropriato per creare un punto di ingresso per il front-end è nel proprio file dedicato. A differenza del tuo punto di ingresso creato in precedenza, desideri che il tuo punto di ingresso del front-end sia accessibile solo richiedendo direttamente il file specifico in cui esiste il punto di ingresso, quindi in questo caso non vorrai usare `auto_prepend_file` o `.htaccess`.

Dopo aver creato il tuo punto di ingresso del front-end, utilizza il tuo browser per accedervi. Dovrebbe essere presentata una pagina di accesso. Nella pagina di accesso, inserisci il nome utente e la password predefiniti (admin/password) e premi il pulsante di accesso.

Nota: Dopo aver effettuato l'accesso per la prima volta, al fine di impedire l'accesso non autorizzato al front-end, si dovrebbe cambiare immediatamente il nome utente e la password! Questo è molto importante, perché è possibile caricare codice PHP arbitrario al suo sito web attraverso il front-end.

Inoltre, per una sicurezza ottimale, si consiglia vivamente di abilitare "l'autenticazione a due fattori" per tutti i conti front-end (istruzioni fornite di seguito).

#### 4.2 COME UTILIZZARE IL FRONT-END.

Le istruzioni sono fornite su ciascuna pagina del front-end, per spiegare il modo corretto di usarlo e la sua destinazione. Se avete bisogno di ulteriori spiegazioni o qualsiasi assistenza speciale, si prega di contattare il supporto. In alternativa, ci sono alcuni video disponibili su YouTube, che potrebbero aiutare per mezzo di dimostrazione.

#### 4.3 AUTENTICAZIONE A DUE FATTORI

È possibile rendere il front-end più sicuro attivando l'autenticazione a due fattori ("2FA"). Quando si accede a un account attivato per 2FA, viene inviata una posta elettronica all'indirizzo di posta elettronica associato a tale account. Questo indirizzo di posta elettronica contiene un "codice 2FA", che l'utente deve quindi inserire, inoltre al nome utente e alla password, per poter accedere utilizzando tale account. Ciò significa che l'ottenimento di una password dell'account non sarebbe sufficiente per consentire a qualsiasi hacker o potenziale utente malintenzionato di accedere a tale account, in quanto avrebbe anche bisogno di avere accesso all'indirizzo di posta elettronica associato a tale account per poter ricevere e utilizzare il codice 2FA associato alla sessione, rendendo così il front-end più sicuro.

Innanzitutto, per attivare l'autenticazione a due fattori, utilizzando la pagina degli aggiornamenti front-end, installare il componente PHPMailer. CIDRAM utilizza PHPMailer per l'invio di posta elettronica.

Dopo aver installato PHPMailer, dovrai compilare le direttive di configurazione per PHPMailer tramite la pagina di configurazione CIDRAM o il file di configurazione. Ulteriori informazioni su queste direttive di configurazione sono incluse nella sezione di configurazione di questo documento. Dopo aver compilato le direttive di configurazione di PHPMailer, imposta da `enable_two_factor` x `true`. L'autenticazione a due fattori dovrebbe ora essere attivata.

Successivamente, dovrai associare un indirizzo di posta elettronica a un account, in modo che CIDRAM sappia dove inviare i codici 2FA quando accede con quell'account. Per fare ciò, usa l'indirizzo di posta elettronica come nome utente per l'account (come `foo@bar.tld`), o includere l'indirizzo di posta elettronica come parte del nome utente nello stesso modo in cui si farebbe quando si invia una posta elettronica normalmente (come `Foo Bar <foo@bar.tld>`).

Nota: Proteggere il tuo vault dall'accesso non autorizzato (per esempio, per mezzo di rafforzando le autorizzazioni di sicurezza e di accesso pubblico del tuo server), è particolarmente importante qui, a causa di tale accesso non autorizzato al file di configurazione (che è memorizzato nel vault), potrebbe rischiare di esporre le impostazioni SMTP in uscita (incluso il nome utente e la password per il tuo SMTP). È meglio assicurarsi che il vault sia correttamente protetto prima di attivare l'autenticazione a due fattori. Se non sei in grado di farlo, almeno, dovresti creare un nuovo account di posta elettronica, dedicato a questo scopo, in quanto tale per ridurre i rischi associati alle impostazioni SMTP esposte.

---


### 5. <a name="SECTION5"></a>OPZIONI DI CONFIGURAZIONE

Il seguente è un elenco di variabili trovate nelle `config.yml` file di configurazione di CIDRAM, insieme con una descrizione del loro scopo e funzione.

```
Configurazione (v4)
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

#### "general" (Categoria)
Configurazione generale (qualsiasi configurazione di base non appartenente ad altre categorie).

##### "stages" `[string]`
- Controlli per le fasi della catena di esecuzione (se abilitato, se gli errori sono registrati, ecc).

```
stages───[Abilitare questa fase?]─[Gli errori generati durante questa fase devono essere registrati?]─[Le infrazioni generati durante questa fase devono essere conteggiate ai fini del tracciamento IP?]
├─BanCheck ("Controlla se è vietato")
├─Tests ("Esegui test sui file di firma")
├─Modules ("Esegui moduli")
├─SearchEngineVerification ("Esegui la verifica dei motori di ricerca")
├─SocialMediaVerification ("Esegui la verifica dei social media")
├─OtherVerification ("Esegui un'altra verifica")
├─Aux ("Esegui regole ausiliarie")
├─Tracking ("Esegui il tracciamento IP")
├─RL ("Esegui la limitazione della velocità")
├─CAPTCHA ("Presenta i CAPTCHA (richieste bloccate)")
├─Reporting ("Esegui rapporti")
├─Statistics ("Aggiorna le statistiche")
├─Webhooks ("Esegui webhook")
├─TriggerNotifications ("Elabora la coda di notifiche di innescamento posta elettronica")
├─PrepareFields ("Preparare i campi per l'output e i registri")
├─Output ("Genera output (richieste bloccate)")
├─WriteLogs ("Scrivi nei file di log (richieste bloccate)")
├─Terminate ("Termina la richiesta (richieste bloccate)")
├─AuxRedirect ("Reindirizzamento secondo regole ausiliarie")
└─NonBlockedCAPTCHA ("Presenta i CAPTCHA (richieste non bloccate)")
```

##### "fields" `[string]`
- Controlli per i campi durante gli eventi di blocco (quando una richiesta è bloccata).

```
fields───[Questo campo dovrebbe apparire nelle voci dei registri?]─[Questo campo dovrebbe apparire nella pagina "accesso negato"?]─[Ometti questo campo quando è vuoto?]
├─ID ("ID")
├─ScriptIdent ("Versione dello script")
├─DateTime ("Data/Tempo")
├─IPAddr ("Indirizzo IP")
├─IPAddrResolved ("Indirizzo IP (risoluto)")
├─Query ("Query")
├─Referrer ("Referente")
├─UA ("Agente utente")
├─UALC ("Agente utente (minuscolo)")
├─SignatureCount ("Conteggio delle firme")
├─Signatures ("Riferimento delle firme")
├─WhyReason ("Perché bloccato")
├─ReasonMessage ("Perché bloccato (dettagliato)")
├─rURI ("URI Ricostruito")
├─Infractions ("Infrazioni")
├─ASNLookup ("** Ricerca per ASN")
├─CCLookup ("** Ricerca per codice paese")
├─Verified ("Identità verificata")
├─Expired ("Scaduta")
├─Ignored ("Ignorato")
├─Request_Method ("Metodo di richiesta")
├─Protocol ("Protocollo")
├─SEC_CH_UA_PLATFORM ("!! SEC_CH_UA_PLATFORM")
├─SEC_CH_UA_MOBILE ("!! SEC_CH_UA_MOBILE")
├─SEC_CH_UA ("!! SEC_CH_UA")
├─Hostname ("Nome host")
├─CAPTCHA ("Stato CAPTCHA")
├─Inspection ("* Ispezione delle condizioni")
└─ClientL10NAccepted ("Risoluzione della lingua")
```

* Destinato solo al debug delle regole ausiliarie. Non mostrato agli utenti bloccati.

** Richiede la funzionalità di ricerca ASN (ad es., tramite il modulo IP-API o BGPView).

!! Questo è un suggerimento client a bassa entropia. I suggerimenti client sono una nuova tecnologia Web sperimentale che non è ancora ampiamente supportata in tutti i browser e nei principali client. *Guarda anche: <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA#browser_compatibility" dir="ltr" hreflang="en-US" rel="noopener noreferrer external">Sec-CH-UA - HTTP | MDN</a>.* Sebbene i suggerimenti client possano essere utili per il rilevamento delle impronte digitali, poiché non sono ampiamente supportati, la loro presenza nelle richieste non deve essere presupposta né considerata attendibile (cioè, bloccare in base alla loro assenza è una cattiva idea).

##### "timezone" `[string]`
- Questo è usato per specificare il fuso orario da usare (per esempio, Africa/Cairo, America/New_York, Asia/Tokyo, Australia/Perth, Europe/Berlin, Pacific/Guam, ecc). Specifica "SYSTEM" per consentire a PHP di gestirlo automaticamente.

```
timezone
├─SYSTEM ("Utilizza il fuso orario predefinito del sistema.")
├─UTC ("UTC")
└─…Altro
```

##### "time_offset" `[int]`
- Fuso orario offset in minuti.

##### "time_format" `[string]`
- Il formato della data/ora di notazione usata da CIDRAM. Ulteriori opzioni possono essere aggiunti su richiesta.

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
└─…Altro
```

__*Segnaposto – Spiegazione – Esempio basato sul 2024-04-30T18:27:49+08:00.*__<br />
`{yyyy}` – L'anno – Per esempio, 2024.<br />
`{yy}` – L'anno abbreviato – Per esempio, 24.<br />
`{Mon}` – Il nome abbreviato del mese (in inglese) – Per esempio, Apr.<br />
`{mm}` – Il mese con gli zeri iniziali – Per esempio, 04.<br />
`{m}` – Il mese – Per esempio, 4.<br />
`{Day}` – Il nome abbreviato del giorno (in inglese) – Per esempio, Tue.<br />
`{dd}` – Il giorno con gli zeri iniziali – Per esempio, 30.<br />
`{d}` – Il giorno – Per esempio, 30.<br />
`{hh}` – L'ora con gli zeri iniziali (utilizza il formato 24 ore) – Per esempio, 18.<br />
`{h}` – L'ora (utilizza il formato 24 ore) – Per esempio, 18.<br />
`{ii}` – I minuti con gli zeri iniziali – Per esempio, 27.<br />
`{i}` – I minuti – Per esempio, 27.<br />
`{ss}` – Il secondo con zeri iniziali – Per esempio, 49.<br />
`{s}` – Il secondo – Per esempio, 49.<br />
`{tz}` – Il fuso orario (senza i due punti) – Per esempio, +0800.<br />
`{t:z}` – Il fuso orario (con i due punti) – Per esempio, +08:00.

##### "ipaddr" `[string]`
- Dove trovare l'indirizzo IP di collegamento richiesta? (Utile per servizi come Cloudflare). Predefinito = REMOTE_ADDR. AVVISO: Non modificare questa se non sai quello che stai facendo!

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (Predefinito)")
└─…Altro
```

Guarda anche:
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### "http_response_header_code" `[int]`
- Quale messaggio di stato HTTP dovrebbe inviare CIDRAM durante il blocco delle richieste?

```
http_response_header_code───[Predefinito]─[Legale]─[Vietato]
├─200 (200 OK): Meno robusto, ma più facile da usare. Molto probabilmente le richieste
│ automatiche interpreteranno questa risposta come un'indicazione che la
│ richiesta riuscito. Consigliato per richieste non bloccate.
├─403 (403 Forbidden (Vietato)): Un po' più robusto, ma un po' meno facile da usare. Consigliato per la
│ maggior parte delle circostanze generali.
├─410 (410 Gone (Andato)): Potrebbe causare problemi durante la risoluzione dei falsi positivi, perché
│ alcuni browser memorizzano nella cache questo messaggio di stato e non
│ inviano richieste successive, anche dopo essere stati sbloccati. Può essere
│ il più preferibile in alcuni contesti, per specifici tipi di traffico.
├─418 (418 I'm a teapot (Sono una teiera)): Fa riferimento a uno scherzo di pesce d'aprile (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). È molto improbabile che
│ venga compreso da qualsiasi client, bot, browser, o altro. Fornito per
│ divertimento e comodità, ma generalmente non consigliato.
├─451 (451 Unavailable For Legal Reasons (Non disponibile per motivi legali)): Consigliato in caso di blocco principalmente per motivi legali. Non
│ consigliato in altri contesti.
└─503 (503 Service Unavailable (Servizio non disponibile)): Più robusto, ma meno facile da usare. Consigliato per quando si è sotto
  attacco, o quando si ha a che fare con traffico indesiderato estremamente
  persistente.
```

__1.__ Quando è attiva la "modalità silenziosa", verrà utilizzato il messaggio di stato HTTP definito da `general➡silent_mode_response_header_code` (questo ha la precedenza più alta).

__2.__ Se l'entità richiedente è stata vietata a causa del superamento del limite di infrazione, verrà utilizzato il messaggio di stato HTTP per "vietato".

__3.__ Se bloccato a causa della limitazione della velocità, verrà utilizzato 429 oppure, in caso di blocco a causa di conflitti di risorse, verrà utilizzato il messaggio di stato HTTP definito da `signatures➡conflict_response` (in questo contesto, la limitazione della velocità e i conflitti di risorse hanno pari precedenza).

__4.__ Se bloccato a causa di una regola ausiliaria che imposta un "sostituzione del codice di stato HTTP", verrà utilizzato tale sostituzione del codice di stato HTTP.

__5.__ Se bloccato per motivi legali (ad esempio, se bloccato a causa di una firma personalizzata che utilizza la parola abbreviata "legale"), verrà utilizzato il messaggio di stato HTTP per "legale".

__6.__ Per tutte le altre richieste bloccate, verrà utilizzato il messaggio di stato HTTP per "default" (questo ha la precedenza più bassa).

##### "silent_mode" `[string]`
- CIDRAM dovrebbe reindirizzare silenziosamente tutti i tentativi di accesso bloccati invece di visualizzare la pagina "accesso negato"? Se si, specificare la localizzazione di reindirizzare i tentativi di accesso bloccati. Se no, lasciare questo variabile vuoto.

##### "silent_mode_response_header_code" `[int]`
- Quale messaggio di stato HTTP dovrebbe inviare CIDRAM quando reindirizza silenziosamente i tentativi di accesso bloccati?

```
silent_mode_response_header_code
├─301 (301 Moved Permanently (Spostato definitivamente)): Indica al client che il reindirizzamento è PERMANENTE, e che il metodo di
│ richiesta utilizzato per il reindirizzamento PUÒ essere diverso dal metodo
│ di richiesta utilizzato per la richiesta iniziale.
├─302 (302 Found (Trovato)): Indica al client che il reindirizzamento è TEMPORANEO, e che il metodo di
│ richiesta utilizzato per il reindirizzamento PUÒ essere diverso dal metodo
│ di richiesta utilizzato per la richiesta iniziale.
├─307 (307 Temporary Redirect (Reindirizzamento temporaneo)): Indica al client che il reindirizzamento è TEMPORANEO, e che il metodo di
│ richiesta utilizzato per il reindirizzamento NON può essere diverso dal
│ metodo di richiesta utilizzato per la richiesta iniziale.
└─308 (308 Permanent Redirect (Reindirizzamento permanente)): Indica al client che il reindirizzamento è PERMANENTE, e che il metodo di
  richiesta utilizzato per il reindirizzamento NON può essere diverso dal
  metodo di richiesta utilizzato per la richiesta iniziale.
```

Indipendentemente da come istruiamo il cliente, è importante ricordare che alla fine non abbiamo alcun controllo su ciò che il cliente sceglie di fare, e non c'è alcuna garanzia che il cliente rispetti le nostre istruzioni.

##### "lang" `[string]`
- Specifica la lingua predefinita per CIDRAM.

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
- Localizzare secondo HTTP_ACCEPT_LANGUAGE quando possibile? True = Sì [Predefinito]; False = No.

##### "numbers" `[string]`
- Come preferisci che i numeri siano visualizzati? Seleziona l'esempio che ti sembra più corretto.

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
- Se si desidera, è possibile fornire un indirizzo di posta elettronica qui a dare utenti quando sono bloccati, per loro di utilizzare come punto di contatto per supporto e/o assistenza per il caso di che vengano bloccate per errore. AVVERTIMENTO: Qualunque sia l'indirizzo di posta elettronica si fornisce qui sarà certamente acquisito dal spambots e raschietti/scrapers nel corso del suo essere usato qui, e così, è fortemente raccomandato che se si sceglie di fornire un indirizzo di posta elettronica qui, che si assicurare che l'indirizzo di posta elettronica si fornisce qui è un indirizzo monouso e/o un indirizzo che si non ti dispiace essere spammato (in altre parole, probabilmente si non vuole usare il personale primaria o commerciale primaria indirizzi di posta elettronica).

##### "emailaddr_display_style" `[string]`
- Come preferisci che l'indirizzo di posta elettronica venga presentato agli utenti?

```
emailaddr_display_style
├─default ("Link cliccabile")
└─noclick ("Testo non cliccabile")
```

##### "default_dns" `[string]`
- Un elenco di server DNS da utilizzare per le ricerche dei nomi di host. AVVISO: Non modificare questa se non sai quello che stai facendo!

__FAQ.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.it.md#cosa-posso-usare-per-default_dns" hreflang="it-IT">Cosa posso usare per "default_dns"?</a>*

##### "default_algo" `[string]`
- Definisce quale algoritmo da utilizzare per tutte le password e le sessioni in futuro.

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### "statistics" `[string]`
- Controlla quali informazioni statistiche tracciare.

```
statistics───[IPv4]─[IPv6]─[Altro]
├─Blocked ("Richieste bloccate")
├─Banned ("Richieste vietate")
├─Passed ("Richieste accettate")
├─ReportOK ("Richieste rapportate ad API esterne – OK")
└─ReportFailed ("Richieste rapportate ad API esterne – Fallito")
```

Nota: È possibile controllare se tenere traccia delle statistiche per le regole ausiliarie dalla pagina delle regole ausiliarie.

##### "statistics_captchas" `[string]`
- Controlla quali informazioni statistiche tracciare per i CAPTCHA.

```
statistics_captchas───[Fallito]─[Superato]─[Servito]
├─HCaptcha ("hCaptcha")
├─FriendlyCaptcha ("Friendly Captcha")
└─CloudflareTurnstile ("Cloudflare Turnstile")
```

Nota: È possibile controllare se tenere traccia delle statistiche per le regole ausiliarie dalla pagina delle regole ausiliarie.

##### "force_hostname_lookup" `[bool]`
- Forzare la ricerca degli nome di host? True = Sì; False = No [Predefinito]. Le ricerche di nome di host vengono normalmente eseguite su base della necessità, ma può essere forzato a tutte le richieste. Ciò può essere utile come mezzo per fornire informazioni più dettagliate nei file di log, ma può anche avere un effetto leggermente negativo sulle prestazioni.

##### "allow_gethostbyaddr_lookup" `[bool]`
- Consenti ricerche gethostbyaddr quando UDP non è disponibile? True = Sì [Predefinito]; False = No.

Nota: Le ricerche IPv6 potrebbero non funzionare correttamente su alcuni sistemi a 32 bit.

##### "disabled_channels" `[string]`
- Questo può essere usato per impedire a CIDRAM di usare canali particolari quando si inviano richieste (ad esempio, quando si aggiorna, quando si recuperano i metadati del componente, ecc).

```
disabled_channels
├─GitHub ("<span class="origin bgHRdBl">US</span> GitHub")
├─BitBucket ("<span class="origin bgHRdBl">US</span> BitBucket")
├─Codeberg ("<span class="origin bgVBkRd fgYlw">DE</span> Codeberg")
└─GoogleDNS ("<span class="origin bgHRdBl">US</span> GoogleDNS")
```

##### "request_proxy" `[string]`
- Se si desidera che le richieste in uscita vengano inviate tramite un proxy, specificarlo qui. In caso contrario, lasciare vuoto questo campo.

##### "request_proxyauth" `[string]`
- Se si inviano richieste in uscita tramite un proxy e se tale proxy richiede un nome utente e una password, specificare qui il nome utente e la password (per esempio, `user:pass`). In caso contrario, lasciare vuoto questo campo.

##### "default_timeout" `[int]`
- Il tempo scaduto predefinito da utilizzare per le richieste esterne? Predefinito = 12 secondi.

##### "sensitive" `[string]`
- Un elenco di percorsi da considerare come pagine sensibili. Ogni percorso elencato verrà confrontato con l'URI ricostruito quando necessario. Un percorso che inizia con una barra verrà trattato come letterale, e confrontato dal componente del percorso della richiesta in poi. In alternativa, un percorso che inizia con un carattere non alfanumerico, e termina con lo stesso carattere (o lo stesso carattere più un flag "i" facoltativo) verrà trattato come un'espressione regolare. Qualsiasi altro tipo di percorso verrà trattato come letterale, e può corrispondere a qualsiasi parte dell'URI. Il fatto che un percorso sia considerato una pagina sensibile può influire sul comportamento di alcuni moduli, ma non ha alcun effetto in altri casi.

##### "email_notification_address" `[string]`
- Se hai scelto di ricevere notifiche da CIDRAM via la posta elettronica, ad esempio, quando vengono innescate regole ausiliarie specifiche, puoi specificare l'indirizzo del destinatario per tali notifiche qui.

##### "email_notification_name" `[string]`
- Se hai scelto di ricevere notifiche da CIDRAM via la posta elettronica, ad esempio, quando vengono innescate regole ausiliarie specifiche, puoi specificare il nome del destinatario per tali notifiche qui.

##### "email_notification_when" `[string]`
- Quando inviare le notifiche dopo la loro generazione.

```
email_notification_when
├─Immediately ("Immediatamente.")
├─After24Hours ("Dopo 24 ore, raggruppati insieme (o quando innescate manualmente, ad es., tramite cron).")
└─ManuallyOnly ("Solo quando innescate manualmente (ad es., tramite cron).")
```

#### "components" (Categoria)
Configurazione per l'attivazione e la disattivazione dei componenti utilizzati da CIDRAM. Tipicamente popolato dalla pagina degli aggiornamenti, ma può anche essere gestito da qui per un controllo più accurato e per componenti personalizzati non riconosciuti dalla pagina degli aggiornamenti.

##### "ipv4" `[string]`
- File di firma IPv4.

##### "ipv6" `[string]`
- File di firma IPv6.

##### "modules" `[string]`
- Moduli.

##### "imports" `[string]`
- Importazioni. Tipicamente utilizzato per fornire le informazioni di configurazione di un componente alla CIDRAM.

##### "events" `[string]`
- Gestori di eventi. Tipicamente utilizzato per modificare il modo in cui CIDRAM si comporta internamente o per fornire funzionalità aggiuntive.

#### "logging" (Categoria)
Configurazione relativa alla registrazione (escluso quello che è applicabile alle altre categorie).

##### "standard_log" `[string]`
- Un file leggibile dagli umani per la registrazione di tutti i tentativi di accesso bloccati. Specificare un nome di file, o lasciare vuoto per disabilitare.

Consiglio utile: È possibile allegare informazioni su data/ora ai nomi dei file di registro utilizzando i segnaposto del formato ora. I segnaposto del formato ora disponibili vengono visualizzati in <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "apache_style_log" `[string]`
- Un file nello stile di apache per la registrazione di tutti i tentativi di accesso bloccati. Specificare un nome di file, o lasciare vuoto per disabilitare.

Consiglio utile: È possibile allegare informazioni su data/ora ai nomi dei file di registro utilizzando i segnaposto del formato ora. I segnaposto del formato ora disponibili vengono visualizzati in <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "serialised_log" `[string]`
- Un file serializzato per la registrazione di tutti i tentativi di accesso bloccati. Specificare un nome di file, o lasciare vuoto per disabilitare.

Consiglio utile: È possibile allegare informazioni su data/ora ai nomi dei file di registro utilizzando i segnaposto del formato ora. I segnaposto del formato ora disponibili vengono visualizzati in <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "error_log" `[string]`
- Un file per la registrazione di eventuali errori non fatali rilevati. Specificare un nome di file, o lasciare vuoto per disabilitare.

Consiglio utile: È possibile allegare informazioni su data/ora ai nomi dei file di registro utilizzando i segnaposto del formato ora. I segnaposto del formato ora disponibili vengono visualizzati in <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "outbound_request_log" `[string]`
- Un file per la registrazione dei risultati di eventuali richieste in uscita. Specificare un nome di file, o lasciare vuoto per disabilitare.

Consiglio utile: È possibile allegare informazioni su data/ora ai nomi dei file di registro utilizzando i segnaposto del formato ora. I segnaposto del formato ora disponibili vengono visualizzati in <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "report_log" `[string]`
- Un file per la registrazione di tutti i rapporti inviati ad API esterne. Specificare un nome di file, o lasciare vuoto per disabilitare.

Consiglio utile: È possibile allegare informazioni su data/ora ai nomi dei file di registro utilizzando i segnaposto del formato ora. I segnaposto del formato ora disponibili vengono visualizzati in <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "truncate" `[string]`
- Troncare i file di log quando raggiungono una determinata dimensione? Il valore è la dimensione massima in B/KB/MB/GB/TB che un file di log può crescere prima di essere troncato. Il valore predefinito di 0KB disattiva il troncamento (i file di log possono crescere indefinitamente). Nota: Si applica ai singoli file di log! La dimensione dei file di log non viene considerata collettivamente.

##### "log_rotation_limit" `[int]`
- La rotazione dei log limita il numero di file di log che dovrebbero esistere in qualsiasi momento. Quando vengono creati nuovi file di log, se il numero totale di file di log supera il limite specificato, verrà eseguita l'azione specificata. Qui puoi specificare il limite desiderato. Un valore di 0 disabiliterà la rotazione dei log.

##### "log_rotation_action" `[string]`
- La rotazione dei log limita il numero di file di log che dovrebbero esistere in qualsiasi momento. Quando vengono creati nuovi file di log, se il numero totale di file di log supera il limite specificato, verrà eseguita l'azione specificata. Qui puoi specificare l'azione desiderato.

```
log_rotation_action
├─Delete ("Elimina i file di log più vecchi, finché il limite non viene più superato.")
└─Archive ("In primo luogo archiviare e quindi, eliminare i file di log più vecchi, finché il limite non viene più superato.")
```

##### "log_banned_ips" `[bool]`
- Includi richieste bloccate da IP vietati nei file di log? True = Sì [Predefinito]; False = No.

##### "log_sanitisation" `[bool]`
- Quando si utilizza il front-end pagina per i file di log per visualizzare i dati di log, CIDRAM sanitizzará i dati del registro prima di visualizzarli, per proteggere gli utenti dagli attacchi XSS e altre potenziali minacce che i dati di log potrebbero contenere. Tuttavia, per impostazione predefinita, i dati non vengono sanitizzati durante la registrazione. Questo è per garantire che i dati siano conservati in modo accurato, per aiutare qualsiasi analisi euristica che potrebbe essere necessaria in futuro. Tuttavia, nel caso in cui un utente tenti di leggere i dati utilizzando strumenti esterni, e se quegli strumenti esterni non eseguono il loro processo sanificazione, l'utente potrebbe essere esposto agli attacchi XSS. Se necessario, è possibile modificare il comportamento predefinito utilizzando questa direttiva di configurazione. True = Sanitizzare i dati durante la registrazione (i dati vengono conservati in modo meno accurato, ma il rischio XSS è inferiore). False = Non sanitizzare i dati durante la registrazione (i dati vengono conservati in modo più accurato, ma il rischio XSS è più alto) [Predefinito].

#### "frontend" (Categoria)
Configurazione per il front-end.

##### "frontend_log" `[string]`
- File per la registrazione di tentativi di accesso al front-end. Specificare un nome di file, o lasciare vuoto per disabilitare.

Consiglio utile: È possibile allegare informazioni su data/ora ai nomi dei file di registro utilizzando i segnaposto del formato ora. I segnaposto del formato ora disponibili vengono visualizzati in <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signatures_update_event_log" `[string]`
- Un file per la registrazione quando le firme vengono aggiornate tramite il front-end. Specificare un nome di file, o lasciare vuoto per disabilitare.

Consiglio utile: È possibile allegare informazioni su data/ora ai nomi dei file di registro utilizzando i segnaposto del formato ora. I segnaposto del formato ora disponibili vengono visualizzati in <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "max_login_attempts" `[int]`
- Numero massimo di tentativi di accesso al front-end. Predefinito = 5.

##### "theme" `[string]`
- Il tema da utilizzare per il front-end.

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
└─…Altro
```

##### "theme_mode" `[string]`
- La modalità per il tema da utilizzare per il front-end.

```
theme_mode
├─normal ("Normale")
└─inverted ("Invertito")
```

##### "magnification" `[float]`
- Ingrandimento del carattere. Predefinito = 1.

##### "custom_header" `[string]`
- Inserito come HTML all'inizio di tutte le pagine del front-end. Questo potrebbe essere utile nel caso in cui desideri includere il logo di un sito web, un'intestazione personalizzata, script, o simili in tutte queste pagine.

##### "custom_footer" `[string]`
- Inserito come HTML alla fine di tutte le pagine del front-end. Questo potrebbe essere utile nel caso in cui desideri includere un avviso legale, un link di contatto, informazioni commerciali, o simili in tutte queste pagine.

##### "remotes" `[string]`
- Un elenco degli indirizzi utilizzati dal sistema di aggiornamenti per recuperare i metadati dei componenti. Potrebbe essere necessario modificarlo durante l'aggiornamento a una nuova versione principale, o quando si acquisisce una nuova fonte per gli aggiornamenti, ma in circostanze normali dovrebbe essere lasciato in pace.

##### "enable_two_factor" `[bool]`
- Questa direttiva determina se utilizzare 2FA per gli account front-end.

#### "signatures" (Categoria)
Configurazione per firme, file di firma, moduli, ecc.

##### "shorthand" `[string]`
- Controlla cosa fare con una richiesta quando c'è una corrispondenza positiva con una firma che utilizza le parole abbreviate fornite.

```
shorthand───[Bloccalo.]─[Profilalo.]─[Quando bloccato, sopprima il modello di output.]
├─Attacks ("Attacchi")
├─Bogon ("⁰ Bogon IP")
├─Cloud ("Servizio cloud")
├─Generic ("Generico")
├─Legal ("¹ Legale")
├─Malware ("Malware")
├─Proxy ("² Proxy")
├─Spam ("Spam")
├─Banned ("³ Vietato")
├─BadIP ("³ IP non valido")
├─RL ("³ Velocità limitato")
├─Conflict ("³ Conflitto")
└─Other ("⁴ Altro")
```

__0.__ Se il suo sito web necessita di accesso tramite LAN o localhost, non bloccarlo. Altrimenti, puoi bloccarlo.

__1.__ Nessuno dei file di firma predefiniti lo utilizza, ma è comunque supportato nel caso in cui possa essere utile per alcuni utenti.

__2.__ Se hai bisogno che gli utenti possano accedere al suo sito web tramite proxy, non bloccarlo. Altrimenti, puoi bloccarlo.

__3.__ L'utilizzo diretto nelle firme non è supportato, ma può essere invocato con altri mezzi in circostanze particolari.

__4.__ Si riferisce a casi in cui le parole abbreviate non vengono utilizzate affatto, o non vengono riconosciute da CIDRAM.

__Uno per firma.__ Una firma può invocare più profili, ma può utilizzare solo una parola abbreviata. È possibile che più parole abbreviate possano essere adatte, ma poiché solo una può essere utilizzata, miriamo a utilizzare sempre solo le più adatte.

__Priorità.__ Un'opzione selezionata ha sempre la priorità su un'opzione non selezionata. Ad esempio, se sono in gioco più parole abbreviate ma solo una di esse è impostata come bloccata, la richiesta sarà comunque bloccata.

__Punti finali umani e servizi cloud.__ Il servizio cloud può fare riferimento a provider di web hosting, server farm, data center, o una serie di altre cose. Punto finale umano si riferisce ai mezzi con cui un umano accede a internet, ad esempio tramite un provider di servizi internet. Una rete di solito fornisce solo l'uno o l'altro, ma a volte può fornire entrambi. Miriamo a non identificare mai potenziali punti finali umani come servizi cloud. Pertanto, un servizio cloud può essere identificato come qualcos'altro se il suo gamme è condiviso da punti finali umani noti. Allo stesso modo, miriamo a identificare sempre i servizi cloud, i cui gamme non sono condivisi da alcun punto finale umano noto, come servizi cloud. Pertanto, una richiesta identificata esplicitamente come servizio cloud probabilmente non condivide il suo gamme con nessun punto finale umano noto. Allo stesso modo, una richiesta identificata esplicitamente da attacchi o rischio per lo spam probabilmente li condivide. Tuttavia, internet è sempre in evoluzione, gli scopi delle reti cambiano nel tempo, e le gamme vengono sempre acquistate o vendute, quindi rimani consapevole e vigile riguardo ai falsi positivi.

##### "default_tracktime" `[string]`
- La durata per la quale devono essere tracciati gli indirizzi IP. Predefinito = 7d0°0′0″ (1 settimana).

##### "infraction_limit" `[int]`
- Numero massimo di infrazioni un IP è permesso di incorrere prima di essere vietato dalle tracciamento IP. Predefinito = 10.

##### "tracking_override" `[bool]`
- I moduli dovrebbero essere autorizzati a sostituire le opzioni di tracciamento? True = Sì [Predefinito]; False = No.

##### "conflict_response" `[int]`
- Quando ce ne sono troppi tentativi simultanei di accedere alle stesse risorse (ad esempio, richieste simultanee a più processi PHP sulla stessa macchina per le stesse risorse), alcuni di questi tentativi potrebbero fallire. Nel raro e improbabile caso in cui ciò influisca sui file delle firme o sui moduli, CIDRAM potrebbe non essere in grado di prendere una decisione effettiva in merito alla richiesta. In tal caso, dovrebbe la richiesta essere bloccata, e quale messaggio di stato HTTP dovrebbe CIDRAM inviare?

```
conflict_response
├─0 (Non bloccare la richiesta.): Se preferisci che le richieste vengano bloccate solo quando sei certo che
│ siano maligne, o se preferisci essere cauto riguardo ai falsi positivi (a
│ costo di far passare occasionalmente traffico indesiderato), scegli questa
│ opzione. Se preferisci che le richieste vengano bloccate se non sei certo
│ che sono benigni, o preferisci essere più vigile (a costo di occasionali
│ falsi positivi), scegli una delle altre opzioni disponibili.
├─409 (409 Conflitto): Consigliato per conflitti di risorse (ad esempio, conflitti di unione,
│ conflitti di accesso ai file, ecc). Non consigliato in altri contesti.
└─429 (429 Too Many Requests (Troppe richieste)): Consigliato per la limitazione della velocità, quando si tratta di attacchi
  DDoS, e per la prevenzione delle inondazioni. Non consigliato in altri
  contesti.
```

#### "verification" (Categoria)
Configurazione per verificare da dove provengono le richieste.

##### "search_engines" `[string]`
- Controlli per la verifica delle richieste dai motori di ricerca.

```
search_engines───[Prova a verificare?]─[Blocca i negativi?]─[Blocca le richieste non verificate?]─[Consenti bypass a colpo singolo?]─[Annulla le tracciamento per i positivi?]
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

__Cosa sono "positivi" e "negativi"?__ Nel verificare l'identità presentata da una richiesta, un esito di successo potrebbe essere descritto come "positivo" o "negativo". Nel caso in cui l'identità presentata fosse confermata come la vera identità, sarebbe descritto come "positivo". Nel caso in cui l'identità presentata fosse confermata come falsificata, sarebbe descritto come "negativo". Tuttavia, un esito senza successo (ad esempio, la verifica è fallita, o non è possibile determinare la veridicità dell'identità presentata) non sarebbe descritto come "positivo" o "negativo". Invece, un esito senza successo verrebbe descritto semplicemente come non verificato. Quando non viene effettuato alcun tentativo di verificare l'identità presentata da una richiesta, la richiesta verrebbe ugualmente descritto come non verificato. I termini hanno senso solo nel contesto in cui viene riconosciuta l'identità presentata da una richiesta e, quindi, dove è possibile la verifica. Nei casi in cui l'identità presentata non corrisponda alle opzioni fornite sopra, o in cui non venga presentata alcuna identità, le opzioni sopra fornite diventano irrilevanti.

__Cosa sono i "bypass a colpo singolo"?__ In alcuni casi, una richiesta verificata positivamente potrebbe comunque essere bloccata a causa dei file di firma, dei moduli, o di altre condizioni della richiesta, e potrebbero essere necessari bypass per evitare falsi positivi. Nel caso in cui un bypass sia destinato a trattare esattamente un'infrazione, né più né meno, tale bypass potrebbe essere descritto come un "bypass a colpo singolo".

* Questa opzione ha un bypass corrispondente sotto `bypasses➡used`. Si consiglia di assicurarsi che la casella di controllo per il bypass corrispondente sia contrassegnato allo stesso modo della casella di controllo per tentare di verificare questa opzione.

##### "social_media" `[string]`
- Controlli per la verifica delle richieste dalle piattaforme dei social media.

```
social_media───[Prova a verificare?]─[Blocca i negativi?]─[Blocca le richieste non verificate?]─[Consenti bypass a colpo singolo?]─[Annulla le tracciamento per i positivi?]
├─Embedly ("* Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("* Pinterest")
├─Snapchat ("* Snapchat")
└─Twitterbot ("*!! Twitterbot")
```

__Cosa sono "positivi" e "negativi"?__ Nel verificare l'identità presentata da una richiesta, un esito di successo potrebbe essere descritto come "positivo" o "negativo". Nel caso in cui l'identità presentata fosse confermata come la vera identità, sarebbe descritto come "positivo". Nel caso in cui l'identità presentata fosse confermata come falsificata, sarebbe descritto come "negativo". Tuttavia, un esito senza successo (ad esempio, la verifica è fallita, o non è possibile determinare la veridicità dell'identità presentata) non sarebbe descritto come "positivo" o "negativo". Invece, un esito senza successo verrebbe descritto semplicemente come non verificato. Quando non viene effettuato alcun tentativo di verificare l'identità presentata da una richiesta, la richiesta verrebbe ugualmente descritto come non verificato. I termini hanno senso solo nel contesto in cui viene riconosciuta l'identità presentata da una richiesta e, quindi, dove è possibile la verifica. Nei casi in cui l'identità presentata non corrisponda alle opzioni fornite sopra, o in cui non venga presentata alcuna identità, le opzioni sopra fornite diventano irrilevanti.

__Cosa sono i "bypass a colpo singolo"?__ In alcuni casi, una richiesta verificata positivamente potrebbe comunque essere bloccata a causa dei file di firma, dei moduli, o di altre condizioni della richiesta, e potrebbero essere necessari bypass per evitare falsi positivi. Nel caso in cui un bypass sia destinato a trattare esattamente un'infrazione, né più né meno, tale bypass potrebbe essere descritto come un "bypass a colpo singolo".

* Questa opzione ha un bypass corrispondente sotto `bypasses➡used`. Si consiglia di assicurarsi che la casella di controllo per il bypass corrispondente sia contrassegnato allo stesso modo della casella di controllo per tentare di verificare questa opzione.

** Richiede la funzionalità di ricerca ASN (ad es., tramite il modulo IP-API o BGPView).

*!! Alta probabilità di causare falsi positivi a causa di iMessage.

##### "other" `[string]`
- Controlli per la verifica di altri tipi di richieste ove possibile.

```
other───[Prova a verificare?]─[Blocca i negativi?]─[Blocca le richieste non verificate?]─[Consenti bypass a colpo singolo?]─[Annulla le tracciamento per i positivi?]
├─AdSense ("AdSense")
├─AmazonAdBot ("* AmazonAdBot")
├─ChatGPT-User ("!! ChatGPT-User")
├─GPTBot ("!! GPTBot")
├─OAI-SearchBot ("!! OAI-SearchBot")
└─UptimeRobot ("UptimeRobot")
```

__Cosa sono "positivi" e "negativi"?__ Nel verificare l'identità presentata da una richiesta, un esito di successo potrebbe essere descritto come "positivo" o "negativo". Nel caso in cui l'identità presentata fosse confermata come la vera identità, sarebbe descritto come "positivo". Nel caso in cui l'identità presentata fosse confermata come falsificata, sarebbe descritto come "negativo". Tuttavia, un esito senza successo (ad esempio, la verifica è fallita, o non è possibile determinare la veridicità dell'identità presentata) non sarebbe descritto come "positivo" o "negativo". Invece, un esito senza successo verrebbe descritto semplicemente come non verificato. Quando non viene effettuato alcun tentativo di verificare l'identità presentata da una richiesta, la richiesta verrebbe ugualmente descritto come non verificato. I termini hanno senso solo nel contesto in cui viene riconosciuta l'identità presentata da una richiesta e, quindi, dove è possibile la verifica. Nei casi in cui l'identità presentata non corrisponda alle opzioni fornite sopra, o in cui non venga presentata alcuna identità, le opzioni sopra fornite diventano irrilevanti.

__Cosa sono i "bypass a colpo singolo"?__ In alcuni casi, una richiesta verificata positivamente potrebbe comunque essere bloccata a causa dei file di firma, dei moduli, o di altre condizioni della richiesta, e potrebbero essere necessari bypass per evitare falsi positivi. Nel caso in cui un bypass sia destinato a trattare esattamente un'infrazione, né più né meno, tale bypass potrebbe essere descritto come un "bypass a colpo singolo".

* Questa opzione ha un bypass corrispondente sotto `bypasses➡used`. Si consiglia di assicurarsi che la casella di controllo per il bypass corrispondente sia contrassegnato allo stesso modo della casella di controllo per tentare di verificare questa opzione.

!! La maggior parte degli utenti probabilmente vorrà che questo venga bloccato, indipendentemente dal fatto che sia reale o falsificato. Ciò può essere ottenuto non selezionando "prova a verificare" e selezionando "blocca le richieste non verificate". Tuttavia, poiché alcuni utenti potrebbero voler essere in grado di verificare tali richieste (per bloccare le richieste negative pur consentendo quelle positive), invece di bloccare tali richieste tramite moduli, qui vengono fornite le opzioni per la gestione di tali richieste.

##### "adjust" `[string]`
- Controlli per regolare altre funzionalità nel contesto della verifica.

```
adjust───[Sopprimi hCaptcha]─[Sopprimi Friendly Captcha]─[Sopprimi Cloudflare Turnstile]
├─Negatives ("I negativi che sono bloccati")
└─NonVerified ("I non verificati che sono bloccati")
```

#### "captcha" (Categoria)
Configurazione per CAPTCHA (fornisce un modo per gli umani di riottenere l'accesso quando bloccato).

##### "usemode" `[int]`
- Quando dovrebbero essere offerti i CAPTCHA? Qui puoi specificare il comportamento preferito per ciascun provider supportato.

```
usemode───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─0 (Mai.)
├─1 (Solo quando bloccato, entro il limite di firme, e non vietato.)
├─2 (Solo quando bloccato, appositamente contrassegnato per l'uso, entro il limite di firme, e non vietato.)
├─3 (Solo quando entro il limite di firme, e non vietato (indipendentemente dal fatto che sia bloccato).)
├─4 (Solo quando non è bloccato.)
├─5 (Solo quando non è bloccato, o quando è appositamente contrassegnato per l'uso, entro il limite di firme, e non è vietato.)
└─6 (Solo quando non è bloccato, in caso di richieste di pagine sensibili.)
```

Nota: Le richieste nella lista bianca o verificate e non bloccate non devono mai completare un CAPTCHA.

Nota anche: I CAPTCHA possono fornire un utile livello aggiuntivo di protezione contro i bot e vari tipi di richieste automatizzate e dannose, ma non forniscono alcuna protezione contro umani dannosi.

Le richieste possono essere "contrassegnate per l'uso" tramite regole ausiliarie.

Se una richiesta è considerata "sensibile" è determinato da <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_sensitive">`general➡sensitive`</a>.

Il "limite di firme" è determinato da <a onclick="javascript:toggleconfigNav('captchaRow','captchaShowLink')" href="#config_captcha_signature_limit">`captcha➡signature_limit`</a>.

##### "nonblocked_status_code" `[int]`
- Quale codice di stato deve essere utilizzato quando si visualizzano i CAPTCHA per le richieste non bloccate?

```
nonblocked_status_code───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─200 (200 OK): Meno robusto, ma più facile da usare. Molto probabilmente le richieste
│ automatiche interpreteranno questa risposta come un'indicazione che la
│ richiesta riuscito. Consigliato per richieste non bloccate.
├─403 (403 Forbidden (Vietato)): Un po' più robusto, ma un po' meno facile da usare. Consigliato per la
│ maggior parte delle circostanze generali.
├─418 (418 I'm a teapot (Sono una teiera)): Fa riferimento a uno scherzo di pesce d'aprile (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). È molto improbabile che
│ venga compreso da qualsiasi client, bot, browser, o altro. Fornito per
│ divertimento e comodità, ma generalmente non consigliato.
├─429 (429 Too Many Requests (Troppe richieste)): Consigliato per la limitazione della velocità, quando si tratta di attacchi
│ DDoS, e per la prevenzione delle inondazioni. Non consigliato in altri
│ contesti.
└─451 (451 Unavailable For Legal Reasons (Non disponibile per motivi legali)): Consigliato in caso di blocco principalmente per motivi legali. Non
  consigliato in altri contesti.
```

##### "api" `[string]`
- Quale API usare?

```
api───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─v0 ("v0")
├─v1 ("v1")
├─Invisible ("v1 (Invisibile)")
└─v2 ("v2")
```

##### "messages" `[string]`
- Messaggi da visualizzare insieme ai CAPTCHA.

```
messages───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─cookie_warning ("Mostra avviso sui cookie?): A seconda delle leggi sulla privacy del tuo Paese o Stato (ad esempio,
│ GDPR/DSGVO nell'UE, LGPD in Brasile, ecc), ciò potrebbe essere richiesto
│ per legge."
└─api_message ("Mostra messaggio API?): Istruzioni all'utente, appropriate all'API utilizzata, in merito al
  completamento del CAPTCHA."
```

##### "lockto" `[string]`
- A cosa associare i CAPTCHA.

```
lockto───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─ip ("Associare i CAPTCHA all'indirizzo IP dell'utente che completa il CAPTCHA, ma non all'utente effettivo.): I cookie NON vengono utilizzati per identificare gli utenti. Quando
│ l'accesso viene ripristinato grazie al completamento con successo di un
│ CAPTCHA, questo si applica a chiunque si connetta dallo stesso indirizzo
│ IP."
├─user ("Associare i CAPTCHA all'utente che completa il CAPTCHA, ma non al suo indirizzo IP.): I cookie vengono utilizzati per identificare gli utenti. Quando l'accesso
│ viene ripristinato grazie al completamento con successo di un CAPTCHA,
│ questo si applica solo all'utente che ha completato il CAPTCHA e, finché il
│ suo cookie rimane valido, persisterà, anche se il suo indirizzo IP cambia."
└─both ("Associare i CAPTCHA all'utente che completa il CAPTCHA e al suo indirizzo IP.): I cookie vengono utilizzati per identificare gli utenti. Quando l'accesso
  viene ripristinato grazie al completamento con successo di un CAPTCHA,
  questo si applica solo all'utente che ha completato il CAPTCHA e non
  persisterà se il suo indirizzo IP cambia."
```

##### "hcaptcha_sitekey" `[string]`
- Se vuoi usare hCaptcha con CIDRAM, dovrai inserire un valore qui. In caso contrario, puoi ignorarlo.

Questo valore può essere trovato nella dashboard del suo servizio CAPTCHA.

Guarda anche:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "hcaptcha_secret" `[string]`
- Se vuoi usare hCaptcha con CIDRAM, dovrai inserire un valore qui. In caso contrario, puoi ignorarlo.

Questo valore può essere trovato nella dashboard del suo servizio CAPTCHA.

Guarda anche:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "friendly_sitekey" `[string]`
- Se vuoi usare Friendly Captcha con CIDRAM, dovrai inserire un valore qui. In caso contrario, puoi ignorarlo.

Questo valore può essere trovato nella dashboard del suo servizio CAPTCHA.

Guarda anche:
- [Friendly Captcha Dashboard](https://app.friendlycaptcha.eu/dashboard)

##### "friendly_apikey" `[string]`
- Se vuoi usare Friendly Captcha con CIDRAM, dovrai inserire un valore qui. In caso contrario, puoi ignorarlo.

Questo valore può essere trovato nella dashboard del suo servizio CAPTCHA.

Guarda anche:
- [Friendly Captcha Dashboard](https://app.friendlycaptcha.eu/dashboard)

##### "turnstile_sitekey" `[string]`
- Se vuoi usare Cloudflare Turnstile con CIDRAM, dovrai inserire un valore qui. In caso contrario, puoi ignorarlo.

Questo valore può essere trovato nella dashboard del suo servizio CAPTCHA.

Guarda anche:
- [Cloudflare Dashboard](https://dash.cloudflare.com/)

##### "turnstile_secret" `[string]`
- Se vuoi usare Cloudflare Turnstile con CIDRAM, dovrai inserire un valore qui. In caso contrario, puoi ignorarlo.

Questo valore può essere trovato nella dashboard del suo servizio CAPTCHA.

Guarda anche:
- [Cloudflare Dashboard](https://dash.cloudflare.com/)

##### "expiry" `[float]`
- Numero di ore per ricordare le istanze CAPTCHA. Predefinito = 720 (1 mese).

##### "signature_limit" `[int]`
- Il numero massimo di firme consentito prima che l'offerta di CAPTCHA venga ritirata. Predefinito = 1.

##### "log" `[string]`
- Registrare tutti i tentativi per CAPTCHA? Se sì, specificare il nome da usare per il file di registrazione. Se non, lasciare questo variabile vuoto.

Consiglio utile: È possibile allegare informazioni su data/ora ai nomi dei file di registro utilizzando i segnaposto del formato ora. I segnaposto del formato ora disponibili vengono visualizzati in <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

#### "legal" (Categoria)
Configurazione per requisiti legali.

##### "pseudonymise_ip_addresses" `[bool]`
- Pseudonimizzare gli indirizzi IP durante la scrivono i file di registro? True = Sì [Predefinito]; False = No.

##### "privacy_policy" `[string]`
- L'indirizzo di una politica sulla privacy pertinente da visualizzare nel piè di pagina delle pagine generate. Specificare un URL, o lasciare vuoto per disabilitare.

#### "template_data" (Categoria)
Configurazione per modelli e temi.

##### "theme" `[string]`
- Il tema da utilizzare per gli eventi di blocco e le richieste CAPTCHA.

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
└─…Altro
```

##### "theme_mode" `[string]`
- La modalità per il tema da utilizzare per gli eventi di blocco e le richieste CAPTCHA.

```
theme_mode
├─normal ("Normale")
└─inverted ("Invertito")
```

##### "magnification" `[float]`
- Ingrandimento del carattere. Predefinito = 1.

##### "css_url" `[string]`
- URL del file CSS per i temi personalizzati.

##### "block_event_title" `[string]`
- Il titolo della pagina da visualizzare per gli eventi di blocco.

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("Accesso negato!")
└─…Altro
```

##### "captcha_title" `[string]`
- Il titolo della pagina da visualizzare per le richieste CAPTCHA.

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…Altro
```

##### "custom_header" `[string]`
- Inserito come HTML all'inizio di tutte le pagine di "accesso negato". Questo potrebbe essere utile nel caso in cui desideri includere il logo di un sito web, un'intestazione personalizzata, script, o simili in tutte queste pagine.

##### "custom_footer" `[string]`
- Inserito come HTML alla fine di tutte le pagine di "accesso negato". Questo potrebbe essere utile nel caso in cui desideri includere un avviso legale, un link di contatto, informazioni commerciali, o simili in tutte queste pagine.

#### "rate_limiting" (Categoria)
Configurazione per la limitazione della velocità (non raccomandato per uso generale).

Tieni presente che, come per tutte le altre funzionalità di CIDRAM, la limitazione della velocità di CIDRAM può essere applicata solo alle pagine e alle risorse a cui CIDRAM è connesso. Ciò significherebbe in genere che le risorse non PHP non sarebbero coperte, se non nei casi in cui fossero esplicitamente fornite da risorse PHP connesse. Se è possibile utilizzare un modulo server, cPanel, o qualche altro strumento di rete per imporre la limitazione della velocità, sarebbe meglio utilizzare quello anziché la funzionalità di limitazione della velocità di CIDRAM. Tieni presente che un utente attento e determinato potrebbe facilmente aggirare la limitazione della velocità ruotando il proprio indirizzo IP o passando a un provider proxy o VPN di cui CIDRAM non è ancora a conoscenza, e tieni presente che la limitazione della velocità può essere molto fastidiosa per gli utenti finali veri. A volte può essere necessario, ma raramente è auspicabile.

##### "max_bandwidth" `[string]`
- La quantità massima di larghezza di banda consentita entro il periodo di tolleranza prima di abilitare la limitazione della velocità per le richieste future. Un valore pari a 0 disabilita questo tipo di limitazione della velocità. Predefinito = 0KB.

##### "max_requests" `[int]`
- Il numero massimo di richieste consentite entro il periodo di tolleranza prima di abilitare la limitazione della velocità per le richieste future. Un valore pari a 0 disabilita questo tipo di limitazione della velocità. Predefinito = 0.

##### "precision_ipv4" `[int]`
- La precisione da utilizzare durante il monitoraggio dell'utilizzo di IPv4. Il valore riflette la dimensione del blocco CIDR. Impostare su 32 per la massima precisione. Predefinito = 32.

##### "precision_ipv6" `[int]`
- La precisione da utilizzare durante il monitoraggio dell'utilizzo di IPv6. Il valore riflette la dimensione del blocco CIDR. Impostare su 128 per la massima precisione. Predefinito = 128.

##### "allowance_period" `[string]`
- La durata per monitorare l'utilizzo. Predefinito = 0°0′0″.

##### "exceptions" `[string]`
- Eccezioni (cioè, richieste che non dovrebbero essere limitate). Rilevante solo quando è abilitata la limitazione della velocità.

```
exceptions
├─Whitelisted ("Richieste nella lista bianca")
├─Verified ("Richieste verificate da motori di ricerca e social media")
└─FE ("Richieste al front-end CIDRAM")
```

##### "segregate" `[bool]`
- Le quote per domini e host diversi devono essere segregate o condivise? True = Le quote saranno segregate. False = Le quote saranno condivise [Predefinito].

#### "supplementary_cache_options" (Categoria)
Opzioni di cache supplementari. Nota: La modifica di questi valori potrebbe potenzialmente disconnettersi.

##### "prefix" `[string]`
- Il valore specificato qui verrà anteposto a tutte le chiavi di ingresso della cache. Predefinito = "CIDRAM_". Quando esistono più installazioni sullo stesso server, questo può essere utile per mantenere le loro cache separate l'una dall'altra.

##### "enable_apcu" `[bool]`
- Specifica se provare a utilizzare APCu per la memorizzazione nella cache. Predefinito = True.

##### "enable_memcached" `[bool]`
- Specifica se provare a utilizzare Memcached per la memorizzazione nella cache. Predefinito = False.

##### "enable_redis" `[bool]`
- Specifica se provare a utilizzare Redis per la memorizzazione nella cache. Predefinito = False.

##### "enable_pdo" `[bool]`
- Specifica se provare a utilizzare PDO per la memorizzazione nella cache. Predefinito = False.

##### "memcached_host" `[string]`
- Il valore dell'host Memcached. Predefinito = localhost.

##### "memcached_port" `[int]`
- Il valore della porta Memcached. Predefinito = "11211".

##### "redis_host" `[string]`
- Il valore dell'host Redis. Predefinito = localhost.

##### "redis_port" `[int]`
- Il valore della porta Redis. Predefinito = "6379".

##### "redis_timeout" `[float]`
- Il valore del tempo scaduto per Redis. Predefinito = "2.5".

##### "redis_database_number" `[int]`
- Il numero del database Redis. Predefinito = 0. Nota: Non è possibile utilizzare valori diversi da 0 con Redis Cluster.

##### "pdo_dsn" `[string]`
- Il valore della DSN per PDO. Predefinito = "mysql:dbname=cidram;host=localhost;port=3306".

__FAQ.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.it.md#user-content-HOW_TO_USE_PDO" hreflang="it-IT">Che cos'è un "DSN PDO"? Come posso usare PDO con CIDRAM?</a>*

##### "pdo_username" `[string]`
- Il nome utente per PDO.

##### "pdo_password" `[string]`
- La password per PDO.

#### "bypasses" (Categoria)
Configurazione per i bypass di firma predefiniti.

##### "used" `[string]`
- Quali bypass dovrebbero essere usati?

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


### 6. <a name="SECTION6"></a>FIRMA FORMATO

*Guarda anche:*
- *[Che cosa è una "firma"?](#user-content-WHAT_IS_A_SIGNATURE)*

#### 6.0 NOZIONI DI BASE (PER FILE DI FIRMA)

Tutte le firme IPv4 seguono il formato: `xxx.xxx.xxx.xxx/yy [Function] [Param]`.
- `xxx.xxx.xxx.xxx` rappresenta l'inizio del blocco CIDR (gli ottetti dell'indirizzo IP iniziale nel blocco).
- `yy` rappresenta la dimensione del blocco CIDR [1-32].
- `[Function]` indica al script di cosa fare con la firma (come la firma dovrebbe essere considerata).
- `[Param]` rappresenta qualsiasi ulteriore informazione può essere richiesta di `[Function]`.

Tutte le firme IPv6 seguono il formato: `xxxx:xxxx:xxxx:xxxx::xxxx/yy [Function] [Param]`.
- `xxxx:xxxx:xxxx:xxxx::xxxx` rappresenta l'inizio del blocco CIDR (gli ottetti dell'indirizzo IP iniziale nel blocco). Notazione completa e la notazione abbreviata sono entrambi accettabili (e ognuno DEVE seguire gli standard adeguati e pertinenti di notazione IPv6, ma con una sola eccezione: un indirizzo IPv6 non può mai iniziare con l'abbreviazione quando usato in una firma per questo script, dovuto al modo in cui CIDRs vengono ricostruite dallo script; Per esempio, `::1/128` dovrebbe essere espresso, quando utilizzato in una firma, come `0::1/128`, e `::0/128` espresso come `0::/128`).
- `yy` rappresenta la dimensione del blocco CIDR [1-128].
- `[Function]` indica al script di cosa fare con la firma (come la firma dovrebbe essere considerata).
- `[Param]` rappresenta qualsiasi ulteriore informazione può essere richiesta di `[Function]`.

I file di firma per CIDRAM DOVREBBE utilizzare interruzioni di riga in stile Unix (`%0A`, o `\n`)! Altri tipi / stili di interruzioni di riga (per esempio, Windows `%0D%0A` o `\r\n` interruzioni di riga, Mac `%0D` o `\r` interruzioni di riga, ecc) PUÒ essere usato, ma NON sono da preferire. Interruzioni di riga che non sono in stile Unix sarà normalizzato a interruzioni di riga in stile Unix dallo script.

Precisa e corretta notazione CIDR è richiesta, altrimenti lo script non riconoscerà le firme. Inoltre, tutte le firme CIDR di questo script DEVE iniziare con un indirizzo IP il cui numero IP può dividere in modo uniforme nella divisione blocco rappresentato dal suo dimensione del blocco CIDR (per esempio, se si desidera bloccare tutti gli IP da `10.128.0.0` a `11.127.255.255`, `10.128.0.0/8` NON sarebbe riconosciuta dallo script, ma `10.128.0.0/9` e `11.0.0.0/9` usato insieme, SAREBBE riconosciuta dallo script).

Qualsiasi cosa ciò che nei file di firme non riconosciuto come firma né come sintassi connessi alle firme dallo script saranno IGNORATI, significa quindi che si può tranquillamente inserire qualsiasi dati che si desidera nei file di firme senza romperle e senza rompere lo script. I commenti sono accettabili nei file di firme, senza qualsiasi formattazione speciale richiesto per loro. Hashing in stile di Shell per i commenti è preferito, ma non forzata; Funzionalmente, non fa alcuna differenza per lo script anche se non si sceglie di utilizzare hashing in stile di Shell per i commenti, ma usando hashing in stile di Shell aiuta IDE ed editor di testo normale ad evidenziare correttamente le varie parti dei file di firme (e così, hashing in stile di Shell può aiutare come un aiuto visivo durante la modifica).

I valori possibili di `[Function]` sono le seguenti:
- Run
- Whitelist
- Greylist
- Deny

Se viene utilizzato "Run", quando la firma viene attivato, lo script tenterà di eseguire (utilizzando un statement `require_once`) uno script PHP esterna, specificato dal valore di `[Param]` (la directory di lavoro dovrebbe essere la directory dello script, "/vault/").

Esempio: `127.0.0.0/8 Run example.php`

Questo può essere utile se si desidera eseguire del codice PHP specifiche per alcuni IP e/o CIDR specifici.

Se viene utilizzato "Whitelist", quando la firma viene attivato, lo script si resetta tutti i rilevamenti (se c'è stato rilevamenti) e rompere la funzione di test. `[Param]` viene ignorato. Questa funzione garantisce che un particolare IP o CIDR non sarà rilevato.

Esempio: `127.0.0.1/32 Whitelist`

Se viene utilizzato "Greylist", quando la firma viene attivato, lo script si resetta tutti i rilevamenti (se c'è stato rilevamenti) e passare al file di firme successivo per continuare l'elaborazione. `[Param]` viene ignorato.

Esempio: `127.0.0.1/32 Greylist`

Se viene utilizzato "Deny", quando la firma viene attivato, supponendo che non firma whitelist è stato attivato per il dato indirizzo IP e/o dato CIDR, l'accesso alla pagina protetta sarà negato. "Deny" xxx è ciò che si desidera utilizzare per bloccare effettivamente un indirizzo IP e/o gamma CIDR. Quando qualsiasi firme vengono attivati che fanno uso di "Deny", il "Accesso Negato" pagina dello script sarà generato e la richiesta alla pagina protetta sarà ucciso.

Il valore di `[Param]` accettato da "Deny" sarà parsato per l'output della "Accesso Negato" pagina, fornito al cliente/utente come la ragione citata per il loro accesso alla pagina richiesta essere negata. Può essere una frase breve e semplice, spiegando il motivo per cui hai scelto di bloccarli (qualsiasi cosa dovrebbe essere sufficiente, anche un semplice "io non ti voglio sul mio sito"), o uno di una piccola manciata di parole brevi fornita dallo script, che se usato, sarà sostituito dallo script con una spiegazione pre-preparati del perché il cliente/utente è stato bloccato.

Le spiegazioni pre-preparati hanno il supporto L10N e può essere tradotto dallo script in base alla lingua specificata alla direttiva di configurazione dello script, `lang`. Inoltre, è possibile indicare lo script di ignorare le firme "Deny" in base al loro valore di `[Param]` (se si sta utilizzando queste brevi parole) tramite le direttive specificata dalla configurazione dello script (ogni parola breve ha un corrispondente direttiva al elaborare le firme corrispondenti o di ignorarle). I valori di `[Param]` che non utilizzare questi brevi parole, però, non hanno il supporto L10N e quindi NON sarà tradotto dallo script, e inoltre, non sono controllabili direttamente dalla configurazione dello script.

Le parole brevi disponibili sono:
- Attacks
- Bogon
- Cloud
- Generic
- Legal
- Malware
- Proxy
- Spam

#### 6.1 ETICHETTE

##### 6.1.0 ETICHETTE DI SEZIONE

Se si desidera dividere le vostre firme personalizzate in singole sezioni, è possibile identificare queste singole sezioni per lo script per aggiungendo un "etichetta di sezione" subito dopo le firme di ogni sezione, insieme con il nome della sezione di firme (vedere l'esempio cui seguito).

```
# Sezione 1.
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: Sezione 1
```

Per rompere l'etichetta della sezione e per assicurare che l'etichetta non sono identificati erroneamente alle sezioni di firme da prima nelle file di firme, semplicemente assicurare che ci sono almeno due interruzioni di riga consecutivi tra l'etichetta e le sezioni di firme precedenti. Qualsiasi firme senza un'etichetta saranno etichettato come "IPv4" o "IPv6" per predefinito (dipendente sui quali tipi di firme vengono attivati).

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: Sezione 1
```

Nell'esempio sopra `1.2.3.4/32` e `2.3.4.5/32` saranno etichettato come "IPv4", mentre `4.5.6.7/32` e `5.6.7.8/32` saranno etichettato come "Sezione 1".

La stessa logica può essere applicata anche per separare altri tipi di etichette.

In particolare, l'etichette di sezione possono essere molto utili per il debug quando si verificano falsi positivi, fornendo un facile mezzo di trovare l'esatta fonte del problema, e può essere molto utili per filtrare le voci del file di registro durante la visualizzazione dei file di registro tramite il front-end pagina per i file di log (i nomi delle sezioni sono selezionabili tramite la pagina dei front-end pagina per i file di log e possono essere utilizzati come criteri di filtro). Se l'etichetta della sezione vengono omessi per alcune firme particolari, quando tali firme vengono innescate, CIDRAM utilizza il nome del file di firma insieme al tipo di indirizzo IP bloccato (IPv4 o IPv6) come ripiego, e quindi, l'etichette di sezione sono completamente opzionali. In alcuni casi, tuttavia, possono essere raccomandati, ad esempio quando i file delle firme sono nominati vagamente o quando potrebbe essere difficile identificare chiaramente la fonte delle firme che causano il blocco di una richiesta.

##### 6.1.1 ETICHETTE DI SCADENZA

Se si desidera firme per scadono dopo un certo tempo, in modo analogo all'etichette sezione, è possibile utilizzare un "etichetta di scadenza" per specificare quando le firme dovrebbero cessano di essere validi. Etichette scadenza usano il formato "AAAA.MM.GG" (vedere l'esempio cui seguito).

```
# Sezione 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

Le firme scadute non verranno mai innescate su nessuna richiesta, non importa quale.

##### 6.1.2 ETICHETTE DI ORIGINE

Se si desidera specificare il paese di origine per alcune firme particolari, è possibile farlo utilizzando un "etichette di origine". Un etichette di origine accetta un codice "[ISO 3166-1 Alpha-2](https://it.wikipedia.org/wiki/ISO_3166-1_alpha-2)" corrispondente al paese di origine per le firme a cui si applica. Questi codici devono essere scritti in maiuscolo (minuscole non verranno visualizzate correttamente). Quando viene utilizzato un etichette di origine, viene aggiunto alla voce del campo di registro "Perché Bloccato" per qualsiasi richieste bloccate a seguito delle firme a cui il tag viene applicato.

Se è installato il componente opzionale "flags CSS", quando si visualizzano i file di registro tramite il front-end pagina per i file di log, le informazioni aggiunte dai etichette di origine vengono sostituite con la bandiera del paese corrispondente a tali informazioni. Questa informazione, sia nella sua forma grezza o come bandiera di un paese, è cliccabile e, quando viene cliccato, filtra le voci di registro tramite altre voci di registro che identificano in modo simile (abilitante effettivamente agli utenti che accedono alla pagina dei registri di filtrare in base al paese di origine).

Nota: Tecnicamente, questa non è una forma di geolocalizzazione, in quanto non implica la ricerca di alcuna informazione specifica relativa agli IP in entrata, ma piuttosto, semplicemente ci consente di dichiarare esplicitamente un paese di origine per qualsiasi richieste bloccate da firme specifiche. Sono consentiti più tag di origine all'interno della stessa sezione di firma.

Esempio ipotetico:

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

Qualsiasi tag possono essere utilizzati insieme e tutti i tag sono opzionali (vedere l'esempio cui seguito).

```
# Sezione Esempio.
1.2.3.4/32 Deny Generic
Origin: US
Tag: Sezione Esempio
Expires: 2016.12.31
```

##### 6.1.3 ETICHETTE DI DEFERENZA

Quando vengono installati e utilizzati attivamente un numero elevato di file di firma, le installazioni possono diventare piuttosto complesse, e potrebbero esserci alcune firme che si sovrappongono. In questi casi, al fine di evitare l'innescando di più firme sovrapposte durante gli eventi di blocco, i etichette di deferenza possono essere utilizzati per differire sezioni di firma specifiche nei casi in cui è installato e utilizzato attivamente un altro file di firma specifico. Questo può essere utile nei casi in cui alcune firme vengono aggiornate più frequentemente di altre, al fine di differire le firme meno frequentemente aggiornate a favore delle firme più frequentemente aggiornate.

I etichette di deferenza sono utilizzati in modo simile ad altri tipi di etichette. Il valore dell'etichetta deve corrispondere a un file di firma installato e utilizzato attivamente a cui essere differite.

Esempio:

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 6.1.4 ETICHETTE DI PROFILE

Le etichette del profilo forniscono un mezzo per visualizzare informazioni aggiuntive nella pagina di test IP e possono essere sfruttate da moduli e regole ausiliarie per comportamenti più complessi e processi decisionali ottimizzati.

Le etichette del profilo vengono utilizzate in modo simile ad altri tipi di etichette. I valori delle etichette del profilo possono essere utilizzati come condizione per moduli e regole ausiliarie. Le etichette del profilo possono fornire più valori separando tali valori con un punto e virgola. L'utente finale non vede mai i valori delle etichette del profilo.

Esempio:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 6.2 YAML

##### 6.2.0 YAML BASI

Una forma semplificata di YAML markup può essere utilizzato in file di firma al fine di definire comportamenti e le impostazioni specifiche per singole sezioni di firma. Questo può essere utile se si desidera che il valore delle vostre direttive di configurazione di differire sulla base delle singole firme e sezioni di firma (per esempio; se si desidera fornire un indirizzo di posta elettronica per i biglietti di supporto per tutti gli utenti bloccati da una firma particolare, ma non desidera fornire un indirizzo di posta elettronica per i biglietti di supporto per utenti bloccati con qualsiasi altro firme; se si desidera che alcune firme specifiche per innescare una reindirizzamento di pagina; se si desidera contrassegnare una sezione di firma per l'utilizzo con hCaptcha; se si desidera registrare i tentativi di accesso bloccati in file separati sulla base delle singole firme e/o sezioni di firma).

L'utilizzo di YAML markup nei file di firma è del tutto facoltativo (cioè, si può usare se si desidera farlo, ma non è richiesto a farlo), ed è in grado di sfruttare la maggior parte (ma non tutto) delle direttive di configurazione.

Nota: Implementazione di YAML markup in CIDRAM è molto semplice e molto limitato; Esso è destinato a soddisfare i requisiti specifici per CIDRAM in modo che ha la familiarità di YAML markup, ma non segue né è conforme alle specifiche tecniche (e quindi non si comporterà nello stesso modo come implementazioni più approfonditi altrove, e potrebbe non essere appropriato per altri progetti altrove).

In CIDRAM, segmenti di YAML markup vengono identificati allo script da tre trattini ("---"), e terminare al fianco dei loro contenenti sezioni di firma mediante due interruzioni di riga. Un tipico segmento di YAML markup all'interno di una sezione di firme consiste di tre trattini su una riga subito dopo l'elenco dei CIDRs e qualsiasi etichette, seguito da una lista bidimensionale delle chiave-valore coppie (prima dimensione, categorie di direttive di configurazione; seconda dimensione, direttive di configurazione) per i quali direttive di configurazione devono essere modificati (e in cui valori) ogniqualvolta una firma all'interno di tale sezione di firme viene innescato (vedere gli esempi qui sotto).

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

#### 6.3 AUSILIARIO

##### 6.3.0 IGNORANDO LE SEZIONI DI FIRMA

In aggiunta, se si desidera CIDRAM di ignorare completamente alcune sezioni specifiche in qualsiasi una delle file di firma, è possibile utilizzare il file `ignore.dat` per specificare quali sezioni a ignorare. In una nuova riga, scivere `Ignore`, seguito da uno spazio, seguito dal nome della sezione che si desidera CIDRAM a ignorare (vedere l'esempio cui seguito).

```
Ignore Sezione 1
```

Ciò può anche essere raggiunto utilizzando l'interfaccia fornita dalla pagina "lista delle sezioni" del front-end CIDRAM.

##### 6.3.1 REGOLE AUSILIARIE

Se ritieni che scrivere i tuoi file di firme personalizzati o moduli personalizzati sia troppo complicato per te, un'alternativa più semplice potrebbe essere quella di utilizzare l'interfaccia fornita dalla pagina "regole ausiliarie" del front-end CIDRAM. Selezionando le opzioni appropriate e specificando i dettagli sui tipi specifici di richieste, è possibile istruire CIDRAM su come rispondere a tali richieste. Le "regole ausiliarie" vengono eseguite dopo che tutti i file di firme e i moduli hanno già completato l'esecuzione.

##### 6.3.2 SALVANDO E ATTIVAZIONE DI FILE DI FIRMA PERSONALIZZATI

Per CIDRAM v2 e precedenti, nel vault troverai due file: `ipv4_custom.dat.RenameMe` e `ipv6_custom.dat.RenameMe`. Puoi salvare le firme personalizzate in questi file oppure, se preferisci, puoi creare nuovi file per le tue firme personalizzate, assegnando loro il nome desiderato. Per CIDRAM v2 e precedenti, i file di firma personalizzati devono essere salvati nella directory base del vault.

Per CIDRAM v3 e successive, non sono presenti file predefiniti per le firme personalizzate, ma è possibile creare nuovi file per le firme personalizzate, assegnando loro il nome desiderato. Per CIDRAM v3 e successive, i file di firma personalizzati devono essere salvati nella directory "signatures" preparata dell'installazione CIDRAM.

Per "attivare" i file di firma personalizzati, è necessario che siano citati dalle direttive di configurazione "ipv4" o "ipv6" del file di configurazione (a seconda che i file di firma personalizzati siano destinati alle firme IPv4 o IPv6).

Per CIDRAM v2 e precedenti, "ipv4" e "ipv6" si trovano nella categoria di configurazione "signatures".

Per CIDRAM v3 e successive, "ipv4" e "ipv6" si trovano nella categoria di configurazione "components".

#### 6.4 <a name="MODULE_BASICS"></a>NOZIONI DI BASE (PER MODULI)

I moduli possono essere utilizzati per estendere la funzionalità di CIDRAM, eseguire attività aggiuntive o elaborare una logica aggiuntiva.

Dato che i moduli sono scritti come file PHP, se hai familiarità con il codice CIDRAM, puoi strutturare i tuoi moduli come vuoi, e scrivi le tue firme del modulo come preferisci (entro i limiti di ciò che è possibile in PHP).

*Nota: Se non ti piace lavorare con il codice PHP, non è consigliabile scrivere i tuoi moduli.*

Alcune funzionalità sono fornite da CIDRAM per essere utilizzato dai moduli, il che dovrebbe rendere più semplice e facile scrivere i propri moduli. Le informazioni su questa funzionalità sono descritte di seguito.

#### 6.5 FUNZIONALITÀ DEL MODULO

##### 6.5.0 "$this->trigger"

Le firme dei moduli sono scritte tipicamente con `$this->trigger`. Nella maggior parte dei casi, questa method sarà più importante di ogni altra cosa allo scopo di scrivere moduli.

`$this->trigger` accetta 4 parametri: `$Condition`, `$ReasonShort`, `$ReasonLong` (opzionale), e `$DefineOptions` (opzionale).

La veridicità di `$Condition` è valutata e, se è true/vera, la firma è "innescato". Se false, la firma *non* è "innescato". `$Condition` contiene tipicamente codice PHP per valutare una condizione che dovrebbe causa una richiesta essere bloccare.

`$ReasonShort` è citato nel campo "Perché Bloccato" quando la firma è "innescata".

`$ReasonLong` è un messaggio opzionale da mostrare all'utente/cliente per quando sono bloccati, per spiegare perché sono stati bloccati. Utilizza il messaggio standard "Accesso Negato" quando omesso.

`$DefineOptions` è un array opzionale contenente coppie chiave/valore, utilizzato per definire le opzioni di configurazione specifiche dell'istanza della richiesta. Le opzioni di configurazione verranno applicate quando la firma è "innescata".

`$this->trigger` restituisce true quando la firma è "innescata", e false quando non lo è.

##### 6.5.1 "$this->bypass"

I bypass di firma sono scritte tipicamente con `$this->bypass`.

`$this->bypass` accetta 3 parametri: `$Condition`, `$ReasonShort`, e `$DefineOptions` (opzionale).

La veridicità di `$Condition` è valutata e, se è true/vera, il bypass è "innescato". Se false, il bypass *non* è "innescato". `$Condition` contiene tipicamente codice PHP per valutare una condizione che *non* dovrebbe causa una richiesta essere bloccare.

`$ReasonShort` è citato nel campo "Perché Bloccato" quando il bypass è "innescata".

`$DefineOptions` è un array opzionale contenente coppie chiave/valore, utilizzato per definire le opzioni di configurazione specifiche dell'istanza della richiesta. Le opzioni di configurazione verranno applicate quando il bypass è "innescata".

`$this->bypass` restituisce true quando il bypass è "innescata", e false quando non lo è.

##### 6.5.2 "$this->dnsReverse"

Questo può essere usato per recuperare il nome host di un indirizzo IP. Se vuoi creare un modulo per bloccare i nomi degli host, questa method potrebbe essere utile.

Esempio:
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

#### 6.6 VARIABILI DEL MODULO

I moduli eseguiti all'interno del proprio ambito, e qualsiasi variabile definita da un modulo, non saranno accessibili ad altri moduli, o allo script principale, tranne se sono memorizzati nella array `$CIDRAM` (tutto il resto viene svuotato al termine dell'esecuzione del modulo).

Di seguito sono elencate alcune variabili comuni che potrebbero essere utili per il tuo modulo:

Variabile | Descrizione
----|----
`$this->BlockInfo['DateTime']` | La data e l'ora correnti.
`$this->BlockInfo['IPAddr']` | L'indirizzo IP per la richiesta corrente.
`$this->BlockInfo['IPAddrResolved']` | Se l'indirizzo IP per la richiesta corrente è un indirizzo 6to4, Teredo, o ISATAP, tale indirizzo viene risolto nel suo equivalente IPv4. In caso contrario, l'indirizzo IP per la richiesta corrente.
`$this->BlockInfo['ScriptIdent']` | Versione di script CIDRAM.
`$this->BlockInfo['Query']` | La query per la richiesta corrente.
`$this->BlockInfo['Referrer']` | Il referrer per la richiesta corrente (se esiste).
`$this->BlockInfo['UA']` | L'agente utente (user agent) per la richiesta corrente.
`$this->BlockInfo['UALC']` | L'agente utente (user agent) per la richiesta corrente (in minuscolo).
`$this->BlockInfo['ReasonMessage']` | Il messaggio visualizzato all'utente/cliente per la richiesta corrente se sono bloccati.
`$this->BlockInfo['SignatureCount']` | Il numero di firme innescati per la richiesta corrente.
`$this->BlockInfo['Signatures']` | Informazioni di riferimento per eventuali firme innescati per la richiesta corrente.
`$this->BlockInfo['WhyReason']` | Informazioni di riferimento per eventuali firme innescati per la richiesta corrente.
`$this->BlockInfo['Request_Method']` | Il metodo di richiesta per la richiesta corrente.
`$this->BlockInfo['Protocol']` | Il protocollo per la richiesta corrente.

---


### 7. <a name="SECTION7"></a>CONOSCIUTI COMPATIBILITÀ PROBLEMI

I seguenti pacchetti e prodotti sono stati trovati incompatibili con CIDRAM:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

I moduli sono stati resi disponibili per garantire che i seguenti pacchetti e prodotti siano compatibili con CIDRAM:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__
- __[Quic cloud](https://wordpress.org/support/topic/quic-dot-cloud-requires-all-ips-allowed/)__

*Guarda anche: [Grafici di Compatibilità](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 8. <a name="SECTION8"></a>DOMANDE FREQUENTI (FAQ)

- [Che cos'è una "firma"?](#user-content-WHAT_IS_A_SIGNATURE)
- [Che cos'è un "CIDR"?](#user-content-WHAT_IS_A_CIDR)
- [Che cosa è un "falso positivo"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)
- [Può CIDRAM blocchi interi paesi?](#user-content-BLOCK_ENTIRE_COUNTRIES)
- [Con quale frequenza vengono aggiornate le firme?](#user-content-SIGNATURE_UPDATE_FREQUENCY)
- [Ho incontrato un problema durante l'utilizzo CIDRAM e non so che cosa fare al riguardo! Aiutami!](#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [CIDRAM mi ha bloccato da un sito web che voglio visitare! Aiutami!](#user-content-BLOCKED_WHAT_TO_DO)
- [Voglio usare CIDRAM v2~v4 con una versione di PHP più vecchio di 7.2; Puoi aiutami?](#user-content-MINIMUM_PHP_VERSION_V3)
- [Posso utilizzare un'installazione singola di CIDRAM per proteggere più domini?](#user-content-PROTECT_MULTIPLE_DOMAINS)
- [Non voglio perdere tempo con l'installazione di questo e farlo funzionare con il mio sito web; Posso pagarti per farlo per me?](#user-content-PAY_YOU_TO_DO_IT)
- [Posso assumere voi o uno degli sviluppatori di questo progetto per lavori privati?](#user-content-HIRE_FOR_PRIVATE_WORK)
- [Ho bisogno di modifiche specialistiche, personalizzazioni, ecc; Puoi aiutare?](#user-content-SPECIALIST_MODIFICATIONS)
- [Sono uno sviluppatore, un designer di siti web o un programmatore. Posso accettare o offrire lavori relativi a questo progetto?](#user-content-ACCEPT_OR_OFFER_WORK)
- [Voglio contribuire al progetto; Posso farlo?](#user-content-WANT_TO_CONTRIBUTE)
- [Posso utilizzare il cron per aggiornare automaticamente?](#user-content-CRON_TO_UPDATE_AUTOMATICALLY)
- [Cosa sono le "infrazioni"?](#user-content-WHAT_ARE_INFRACTIONS)
- [CIDRAM può bloccare i nomi degli host?](#user-content-BLOCK_HOSTNAMES)
- [Cosa posso usare per "default_dns"?](#cosa-posso-usare-per-default_dns)
- [Posso usare CIDRAM per proteggere cose diverse dai siti web (per esempio, server di posta elettronica, FTP, SSH, IRC, ecc)?](#user-content-PROTECT_OTHER_THINGS)
- [Avrò problemi se utilizzo CIDRAM contemporaneamente all'utilizzo di CDN o servizi di cache?](#user-content-CDN_CACHING_PROBLEMS)
- [CIDRAM proteggerà il mio sito Web dagli attacchi DDoS?](#user-content-DDOS_ATTACKS)
- [Quando si attivano o disattivano moduli o file di firma tramite la pagina degli aggiornamenti, li ordina in ordine alfanumerico nella configurazione. Posso cambiare il modo in cui vengono ordinati?](#user-content-CHANGE_COMPONENT_SORT_ORDER)
- [Che cos'è un "DSN PDO"? Come posso usare PDO con CIDRAM?](#user-content-HOW_TO_USE_PDO)
- [CIDRAM sta bloccando cronjobs; Come risolvere questo?](#user-content-BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>Che cos'è una "firma"?

Nel contesto di CIDRAM, una "firma" si riferisce a dati che fungono da indicatore/identificatore per qualcosa di specifico che stiamo cercando, di solito un indirizzo IP o CIDR, e include alcune istruzioni per CIDRAM, dicendogli il modo migliore per rispondere quando incontra quello che stiamo cercando. Una firma tipica per CIDRAM sembra qualcosa di simile:

Per "file di firma":

`1.2.3.4/32 Deny Generic`

Per "moduli":

```PHP
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*Nota: Le firme per "file di firma", e le firme per "moduli", non sono la stessa cosa.*

Spesso (ma non sempre), le firme verranno raggruppate in gruppi, formando "sezioni di firma", spesso accompagnati da commenti, markup e/o metadati correlati che possono essere utilizzati per fornire contesto aggiuntivo per le firme e/o ulteriori istruzioni.

#### <a name="WHAT_IS_A_CIDR"></a>Che cos'è un "CIDR"?

"CIDR" è un acronimo di "Classless Inter-Domain Routing" *[[1](https://it.wikipedia.org/wiki/Supernetting#CIDR), [2](https://whatismyipaddress.com/cidr)]* (talvolta noto come "supernetting"), ed è questo acronimo che viene utilizzato come parte del nome di questo pacchetto, "CIDRAM", di cui che è un acronimo di "Classless Inter-Domain Routing Access Manager".

Nel contesto di CIDRAM, "CIDR" (o "CIDRs") si riferisce specificamente alle sottoreti espresse utilizzando la notazione CIDR.

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>Che cosa è un "falso positivo"?

Il termine "falso positivo" (*in alternativa: "errore di falso positivo"; "falso allarme"*; Inglese: *false positive*; *false positive error*; *false alarm*), descritto molto semplicemente, e in un contesto generalizzato, viene utilizzato quando si analizza una condizione, per riferirsi ai risultati di tale analisi, quando i risultati sono positivi (cioè, la condizione è determinata a essere "positivo", o "vero"), ma dovrebbero essere (o avrebbe dovuto essere) negativo (cioè, la condizione, in realtà, è "negativo", o "falso"). Un "falso positivo" potrebbe essere considerato analogo a "piangendo lupo" (dove la condizione di essere analizzato è se c'è un lupo nei pressi della mandria, la condizione è "falso" in che non c'è nessun lupo nei pressi della mandria, e la condizione viene segnalato come "positivo" dal pastore per mezzo di chiamando "lupo, lupo"), o analogo a situazioni di test medici dove un paziente viene diagnosticato una malattia, quando in realtà, non hanno qualsiasi malattia.

Risultati correlati quando si analizza una condizione può essere descritto utilizzando i termini "vero positivo", "vero negativo" e "falso negativo". Un "vero positivo" si riferisce a quando i risultati dell'analisi e lo stato attuale della condizione sono entrambi vero (o "positivo"), e un "vero negativo" si riferisce a quando i risultati dell'analisi e lo stato attuale della condizione sono entrambe falso (o "negativo"); Un "vero positivo" o un "vero negativo" è considerato una "inferenza corretta". L'antitesi di un "falso positivo" è un "falso negativo"; Un "falso negativo" si riferisce a quando i risultati dell'analisi sono negativo (cioè, la condizione è determinata a essere "negativo", o "falso"), ma dovrebbero essere (o avrebbe dovuto essere) positivo (cioè, la condizione, in realtà, è "positivo", o "vero").

Nel contesto di CIDRAM, questi termini si riferiscono alle firme di CIDRAM e che cosa/chi bloccano. Quando CIDRAM si blocca un indirizzo IP a causa di firme male, obsoleti o errati, ma non avrebbe dovuto fare così, o quando lo fa per le ragioni sbagliate, ci riferiamo a questo evento come un "falso positivo". Quando CIDRAM non riesce a bloccare un indirizzo IP che avrebbe dovuto essere bloccato, a causa delle minacce impreviste, firme mancante o carenze nelle sue firme, ci riferiamo a questo evento come una "rivelazione mancante" o "missed detection" (che è analoga ad un "falso negativo").

Questo può essere riassunta dalla seguente tabella:

&nbsp; | CIDRAM *NON* dovrebbe bloccare un indirizzo IP | CIDRAM *DOVREBBE* bloccare un indirizzo IP
---|---|---
CIDRAM *NON* bloccare un indirizzo IP | Vero negativo (inferenza corretta) | Rivelazione mancante (analogous to falso negativo)
CIDRAM *FA* bloccare un indirizzo IP | __Falso positivo__ | Vero positivo (inferenza corretta)

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>Può CIDRAM blocchi interi paesi?

Sì. Il modo più semplice per farlo sarebbe installare il modulo BGPView e configurarlo in base alle proprie esigenze.

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>Con quale frequenza vengono aggiornate le firme?

Frequenza di aggiornamento varia a seconda delle file di firma in questione. Tutti i manutentori per i file di firma per CIDRAM in genere cercano di mantenere i loro firme aggiornato il più possibile, ma a causa di tutti noi abbiamo diversi altri impegni, la nostra vita al di fuori del progetto, e a causa di nessuno di noi sono finanziariamente compensato (o pagato) per i nostri sforzi sul progetto, un calendario di aggiornamento preciso non può essere garantita. In genere, le firme vengono aggiornati ogni volta che c'è abbastanza tempo per aggiornarli, e generalmente, manutentori cercano di dare la priorità sulla base di necessità e su come spesso i cambiamenti si verificano tra le gamme. L'assistenza è sempre apprezzato se siete disposti a offrire qualsiasi.

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>Ho incontrato un problema durante l'utilizzo CIDRAM e non so che cosa fare al riguardo! Aiutami!

- Si sta utilizzando la versione più recente del software? Si sta utilizzando le ultime versioni dei file di firma? Se la risposta a una di queste due domande è no, provare ad aggiornare tutto prima, e verificare se il problema persiste. Se persiste, continuare a leggere.
- Hai controllato attraverso tutta la documentazione? In caso non fatto, si prega di farlo. Se il problema non può essere risolto utilizzando la documentazione, continuare a leggere.
- Hai controllato la **[pagina dei issues](https://github.com/CIDRAM/CIDRAM/issues)**, per vedere se il problema è stato accennato prima? Se è stato accennato prima, verificare se sono stati forniti qualsiasi suggerimenti, idee, e/o soluzioni, e seguire come necessario per cercare di risolvere il problema.
- Se il problema persiste, si prega di cercare aiuto su di esso per mezzo di creando un nuovo issue nella pagina dei issues.

#### <a name="BLOCKED_WHAT_TO_DO"></a>CIDRAM mi ha bloccato da un sito web che voglio visitare! Aiutami!

CIDRAM fornisce un mezzo per proprietari di siti web per bloccare il traffico indesiderato, ma è la responsabilità dei proprietari di siti web di decidere per se stessi come vogliono usare CIDRAM. Nel caso dei falsi positivi relativi alla firma file normalmente incluso con CIDRAM, correzioni possono essere fatte, ma per essere sbloccato da siti web specifici, è necessario prendere quella con i proprietari dei siti web in questione. Nei casi in cui vengono effettuate correzioni, almeno, avranno bisogno di aggiornare i propri file di firma e/o installazione, e in altri casi (come ad esempio, dove hanno modificato il loro installazione, creato le proprie firme personalizzate, ecc), la responsabilità di risolvere il problema è tutto loro, ed è completamente al di fuori del nostro controllo.

#### <a name="MINIMUM_PHP_VERSION_V3"></a>Voglio usare CIDRAM v2~v4 con una versione di PHP più vecchio di 7.2; Puoi aiutami?

No. PHP≥7.2 è un requisito minimo per CIDRAM v2~v4.

*Guarda anche: [Grafici di Compatibilità](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>Posso utilizzare un'installazione singola di CIDRAM per proteggere più domini?

Sì. Le installazioni di CIDRAM non sono naturalmente legato a domini specifici, e quindi possono essere utilizzati per proteggere più domini. Generalmente, ci riferiamo alle installazioni di CIDRAM che proteggono un solo dominio come "installazioni per singolo dominio", e ci riferiamo a installazioni di CIDRAM che proteggono più domini e/o sottodomini come "installazioni per più domini". Se si esegue un'installazione per più domini e bisogno utilizzare diversi set di file di firma per diversi domini, o bisogno che CIDRAM essere configurato in modo diverso per diversi domini, è possibile farlo. Dopo aver caricato il file di configurazione (`config.yml`), CIDRAM verifica l'esistenza di un "file di sovrascrittura per la configurazione" specifico del dominio (o sottodominio) che viene richiesto (`il-dominio-che-viene-richiesto.tld.config.yml`), e se trovati, tutti i valori di configurazione definiti dal file di sovrascrittura per la configurazione verranno utilizzati per l'istanza di esecuzione invece dei valori di configurazione definiti dal file di configurazione. I file di sovrascrittura per la configurazione sono identiche al file di configurazione, e a vostra discrezione, può contenere l'insieme di tutte le direttive di configurazione disponibili a CIDRAM, o qualsiasi piccola sottosezione richiesta che differisca dai valori normalmente definiti dal file di configurazione. I file di sovrascrittura per la configurazione sono chiamati in base al dominio a cui sono destinati (così, per esempio, se hai bisogno di un file di sovrascrittura per la configurazione per il dominio, `https://www.some-domain.tld/`, la sua file di sovrascrittura per la configurazione deve essere denominato come `some-domain.tld.config.yml`, e deve essere collocato all'interno della vault insieme al file di configurazione, `config.yml`). Il nome di dominio per l'istanza di esecuzione è derivato dall'intestazione `HTTP_HOST` della richiesta; "www" viene ignorato.

#### <a name="PAY_YOU_TO_DO_IT"></a>Non voglio perdere tempo con l'installazione di questo e farlo funzionare con il mio sito web; Posso pagarti per farlo per me?

Forse. Ciò è considerato caso per caso. Dicci cosa hai bisogno, quello che stai offrendo, e ti dirà se possiamo aiutare.

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>Posso assumere voi o uno degli sviluppatori di questo progetto per lavori privati?

*Vedi sopra.*

#### <a name="SPECIALIST_MODIFICATIONS"></a>Ho bisogno di modifiche specialistiche, personalizzazioni, ecc; Puoi aiutare?

*Vedi sopra.*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>Sono uno sviluppatore, un designer di siti web o un programmatore. Posso accettare o offrire lavori relativi a questo progetto?

Sì. La nostra licenza non vieta questo.

#### <a name="WANT_TO_CONTRIBUTE"></a>Voglio contribuire al progetto; Posso farlo?

Sì. I contributi al progetto sono molto graditi. Per ulteriori informazioni, vedere "CONTRIBUTING.md".

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>Posso utilizzare il cron per aggiornare automaticamente?

Sì. Una API è incorporata nel front-end per interagire con la pagina degli aggiornamenti tramite script esterni. È disponibile uno script separato, "[Cronable](https://github.com/Maikuolan/Cronable)", e può essere utilizzato dal tuo cron manager o cron scheduler per aggiornare automaticamente questo e altri pacchetti supportati (questo script fornisce la propria documentazione).

#### <a name="WHAT_ARE_INFRACTIONS"></a>Cosa sono le "infrazioni"?

"Conteggio delle firme" e "infrazioni" si riferiscono entrambi alla gravità e al numero di firme innescate durante qualsiasi richiesta particolare, a causa di file delle firme, moduli, regole ausiliarie, o altro, ma mentre il "conteggio delle firme" persiste solo per quella particolare richiesta, le "infrazioni" possono persistere su qualsiasi numero di richieste, fintanto che è determinato dal `default_tracktime`.

Ciò fornisce un meccanismo per garantire che le richieste provenienti da fonti potenzialmente pericolose possano essere bloccate su richieste secondarie da qualsiasi fonte particolare per cui tale fonte era già stata bloccata durante una richiesta precedente con un numero sufficiente di infrazioni.

#### <a name="BLOCK_HOSTNAMES"></a>CIDRAM può bloccare i nomi degli host?

Sì. Ciò può essere ottenuto creando una regola ausiliaria o un modulo personalizzato.

![Una regola ausiliaria per bloccare i nomi host](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>Cosa posso usare per "default_dns"?

Se stai cercando suggerimenti, [public-dns.info](https://public-dns.info/) e [OpenNIC](https://servers.opennic.org/) forniscono elenchi di server DNS pubblici noti. In alternativa, vedi la tabella seguente:

IP | Operatore
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

*Nota: Non faccio reclami o garanzie riguardo alle pratiche di privacy, sicurezza, efficacia, né affidabilità di alcun servizio DNS, elencati o altrimenti. Per favore fai le tue ricerche quando prendi decisioni su di loro.*

#### <a name="PROTECT_OTHER_THINGS"></a>Posso usare CIDRAM per proteggere cose diverse dai siti web (per esempio, server di posta elettronica, FTP, SSH, IRC, ecc)?

Puoi (legalmente), ma non dovresti (tecnicamente; praticamente). La nostra licenza non limita le tecnologie che implementano CIDRAM, ma CIDRAM è un WAF (Web Application Firewall) ed è sempre stato concepito per proteggere i siti web. Poiché non è stato progettato pensando ad altre tecnologie, è improbabile che sia efficace o fornisca una protezione affidabile per altre tecnologie, l'implementazione è probabile che sia difficile, e il rischio di falsi positivi e rilevazioni mancate è molto alto.

#### <a name="CDN_CACHING_PROBLEMS"></a>Avrò problemi se utilizzo CIDRAM contemporaneamente all'utilizzo di CDN o servizi di cache?

Possibilmente. Questo dipende dalla natura del servizio in questione e da come lo stai usando. In genere, se si memorizzano nella cache solo risorse statiche (immagini, CSS, ecc; tutto ciò che generalmente non cambia nel tempo), non dovrebbero esserci problemi. Tuttavia, potrebbero verificarsi problemi se si memorizzano nella cache dati che altrimenti verrebbe generati in modo dinamico quando richiesto, o se stai memorizzando nella cache i risultati delle richieste POST (questo renderebbe essenzialmente statico il tuo sito web e il suo ambiente, e CIDRAM non è probabile di fornire alcun beneficio significativo in un ambiente statico obbligatorio). Potrebbero inoltre esserci requisiti di configurazione specifici per CIDRAM, basato sul servizio CDN o servizio cache che stai utilizzando (dovrai assicurarti che CIDRAM sia configurato correttamente per il servizio specifico di CDN o cache che stai utilizzando). La configurazione scorretto per CIDRAM può causare falsi positivi e rilevamenti mancati in modo significativo.

#### <a name="DDOS_ATTACKS"></a>CIDRAM proteggerà il mio sito Web dagli attacchi DDoS?

Risposta breve: No.

Risposta leggermente più lunga: CIDRAM aiuterà a ridurre l'impatto che il traffico indesiderato può avere sul tuo sito web (riducendo così i costi della larghezza di banda del tuo sito web), aiuterà a ridurre l'impatto che il traffico indesiderato può avere sul tuo hardware (ad esempio, la capacità del tuo server di elaborare e servire richieste), e può aiutare a ridurre vari altri potenziali effetti negativi associati al traffico indesiderato. Tuttavia, ci sono due cose importanti che devono essere ricordate per capire questa domanda.

In primo luogo, CIDRAM è un pacchetto PHP e pertanto opera nella macchina su cui è installato PHP. Ciò significa che CIDRAM può vedere e bloccare una richiesta solo *dopo* che il server l'ha già ricevuta. In secondo luogo, l'efficace mitigazione DDoS dovrebbe filtrare le richieste *prima* che raggiungano il server bersaglio dell'attacco DDoS. Idealmente, gli attacchi DDoS dovrebbero essere rilevati e mitigati da soluzioni in grado di rilasciare o reindirizzare il traffico associato agli attacchi, prima che raggiunga il server di destinazione in primo luogo.

Questo può essere implementato utilizzando soluzioni hardware dedicati on-premise, e/o soluzioni basate su cloud come servizi di attenuazione DDoS dedicati, indirizzare il DNS di un dominio attraverso reti resistenti agli attacchi DDoS, filtraggio basato su cloud, o qualche combinazione di questi. In ogni caso, questo argomento è un po 'troppo complicato da spiegare a fondo con un semplice paragrafo o due, quindi consiglierei di fare ulteriori ricerche se questo è un argomento che si desidera perseguire. Quando la vera natura degli attacchi DDoS è correttamente compresa, questa risposta avrà più senso.

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>Quando si attivano o disattivano moduli o file di firma tramite la pagina degli aggiornamenti, li ordina in ordine alfanumerico nella configurazione. Posso cambiare il modo in cui vengono ordinati?

Sì. Se è necessario forzare alcuni file per l'esecuzione in un ordinamento specifico, è possibile aggiungere alcuni dati arbitrari prima dei loro nomi nella direttiva di configurazione in cui sono elencati, separati da due punti. Quando la pagina degli aggiornamenti ordina di nuovo i file, questi dati arbitrari aggiunti influenzeranno l'ordinamento, causandoli di conseguenza nell'ordinamento che si desidera, senza dover rinominare nessuno di essi.

Ad esempio, assumendo una direttiva di configurazione con file elencati come segue:

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

Se si desidera che `file3.php` esegua prima, potresti aggiungere qualcosa come `aaa:` prima del nome del file:

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

Quindi, se un nuovo file, `file6.php`, viene attivato, quando la pagina degli aggiornamenti li ordina di nuovo tutti, dovrebbe finire in questo modo:

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

Stessa situazione quando un file è disattivato. Al contrario, se si desidera che il file venga eseguito per ultimo, è possibile aggiungere qualcosa come `zzz:` prima del nome del file. In ogni caso, non sarà necessario rinominare il file in questione.

#### <a name="HOW_TO_USE_PDO"></a>Che cos'è un "DSN PDO"? Come posso usare PDO con CIDRAM?

"PDO" è l'acronimo di "[PHP Data Objects](https://www.php.net/manual/en/intro.pdo.php)" (oggetti dati PHP). Fornisce un'interfaccia affinché PHP sia in grado di connettersi ad alcuni sistemi di database comunemente utilizzati da varie applicazioni PHP.

"DSN" è l'acronimo di "[data source name](https://it.wikipedia.org/wiki/Database_Source_Name)" (nome dell'origine dati). Il "PDO DSN" descrive al PDO come dovrebbe connettersi a un database.

CIDRAM offre la possibilità di utilizzare PDO per scopi di memorizzazione nella cache. Affinché ciò funzioni correttamente, dovrai configurare CIDRAM di conseguenza, abilitando PDO, creare un nuovo database da utilizzare per CIDRAM (se non hai già in mente un database da utilizzare per CIDRAM) e creare un nuovo tabella nel database in base alla struttura descritta di seguito.

Quando una connessione al database ha esito positivo, ma la tabella necessaria non esiste, tenterà di crearla automaticamente. Tuttavia, questo comportamento non è stato ampiamente testato e il successo non può essere garantito.

Questo, ovviamente, si applica solo se si desidera che CIDRAM utilizzi PDO. Se sei abbastanza felice per CIDRAM di utilizzare la memorizzazione nella cache dei file flat (in base alla sua configurazione predefinita) o una qualsiasi delle altre opzioni di memorizzazione nella cache fornite, non dovrai preoccuparti di creare database, tabelle e così via.

La struttura descritta di seguito utilizza "cidram" come nome del database, ma è possibile utilizzare qualunque nome tu voglia per il database, purché lo stesso nome venga replicato nella configurazione DSN.

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

La direttiva di configurazione `pdo_dsn` di CIDRAM dovrebbe essere configurata come descritto di seguito.

```
A seconda del driver del database utilizzato...
├─4d (Avvertimento: Sperimentale, non testato, non raccomandato!)
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └L'host con cui connettersi per trovare il database.
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └Il nome del database da
│                │              │             utilizzare.
│                │              │
│                │              └Il numero di porta con cui connettersi
│                │               all'host.
│                │
│                └L'host con cui connettersi per trovare il database.
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └Il nome del database da utilizzare.
│    │          │
│    │          └L'host con cui connettersi per trovare il database.
│    │
│    └Valori possibili: "mssql", "sybase", "dblib".
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├Può essere un percorso per un file di database locale.
│                    │
│                    ├Può connettersi con un host e un numero di porta.
│                    │
│                    └Dovresti leggi la documentazione di Firebird se si
│                     desidera utilizzare questo.
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └Il database catalogato con cui connettersi.
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └Il database catalogato con cui connettersi.
├─mysql (Più raccomandato!)
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └Il numero di porta con cui
│                 │            │               connettersi all'host.
│                 │            │
│                 │            └L'host con cui connettersi per trovare il
│                 │             database.
│                 │
│                 └Il nome del database da utilizzare.
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├Può fare riferimento al database catalogato specifico.
│               │
│               ├Può connettersi con un host e un numero di porta.
│               │
│               └Dovresti leggi la documentazione di Oracle se si desidera
│                utilizzare questo.
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├Può fare riferimento al database catalogato specifico.
│         │
│         ├Può connettersi con un host e un numero di porta.
│         │
│         └Dovresti leggi la documentazione di ODBC/DB2 se si desidera
│          utilizzare questo.
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └Il nome del database da utilizzare.
│               │              │
│               │              └Il numero di porta con cui connettersi
│               │               all'host.
│               │
│               └L'host con cui connettersi per trovare il database.
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └Il percorso del file di database locale da utilizzare.
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └Il nome del database da utilizzare.
                   │         │
                   │         └Il numero di porta con cui connettersi all'host.
                   │
                   └L'host con cui connettersi per trovare il database.
```

Se non sei sicuro di cosa utilizzare per una parte particolare del tuo DSN, prova innanzitutto a vedere se funziona così com'è, senza cambiare nulla.

Nota che `pdo_username` e `pdo_password` dovrebbero essere gli stessi del nome utente e della password che hai scelto per il tuo database.

#### <a name="BLOCK_CRON"></a>CIDRAM sta bloccando cronjobs; Come risolvere questo?

Se stai usando un file dedicato ai fini di cronjobs, e se quel file non ha bisogno di essere chiamato durante le normali richieste dell'utente (cioè, al di fuori del contesto dei cronjobs), il modo più semplice per risolvere questo problema sarebbe garantire che CIDRAM non venga eseguito durante i tuoi cronjobs (cioè, non agganciare CIDRAM al file responsabile della gestione dei tuoi cronjobs).

In alternativa, se ciò non è possibile, ma l'indirizzo IP del tuo server cron è relativamente coerente e prevedibile, potresti provare a creare una firma whitelist per l'indirizzo IP del tuo server cron in un file di firma personalizzato, oppure provare a creare una regola ausiliaria per esso. Se l'indirizzo IP del tuo server cron ruota regolarmente e non è particolarmente prevedibile, ma rimane comunque all'interno della stessa rete particolare, potresti provare a elencare nel tuo file `ignore.dat` il nome della sezione di firme responsabile del blocco in primo luogo.

Se hai provato tutte queste idee e nessuna di queste ha funzionato per te, o se hai bisogno di aiuto per capire come farlo, puoi creare un nuovo issue nella pagina dei issues di CIDRAM per chiedere aiuto.

---


### 9. <a name="SECTION9"></a>INFORMAZIONE LEGALE

#### 9.0 SEZIONE PREAMBOLO

Questa sezione della documentazione ha lo scopo di descrivere possibili considerazioni legali riguardanti l'uso e l'implementazione del pacchetto, e fornire alcune informazioni di base relative. Questo può essere importante per alcuni utenti come mezzo per garantire la conformità con eventuali requisiti legali che possono esistere nei paesi in cui operano, e alcuni utenti potrebbero aver bisogno di modificare le loro politiche del sito web in conformità con queste informazioni.

Innanzitutto per favore, renditi conto che io (l'autore del pacchetto) non sono un avvocato, né un professionista legale qualificato di alcun tipo. Pertanto, non sono legalmente qualificato per fornire consulenza legale. Inoltre, in alcuni casi, i requisiti legali esatti possono variare a seconda dei paesi e delle giurisdizioni, e questi varie requisiti legali possono a volte entrare in conflitto (come, per esempio, nel caso di paesi che favoriscono i [diritti alla privacy](https://it.wikipedia.org/wiki/Privacy) e il [diritto all'oblio](https://it.wikipedia.org/wiki/Diritto_all%27oblio), contro paesi che favoriscono la [conservazione estesa dei dati](https://it.wikipedia.org/wiki/Direttiva_sulla_conservazione_dei_dati)). Considera inoltre che l'accesso al pacchetto non è limitato a specifici paesi o giurisdizioni, e quindi, la base utente del pacchetto è probabilmente geograficamente diversa. Considerando questi punti, non sono in grado di affermare cosa significa essere "legalmente conformi" per tutti gli utenti, in ogni aspetto. Tuttavia, spero che le informazioni qui contenute ti aiutino a prendere una decisione autonomamente riguardo a ciò che devi fare per rimanere legalmente conforme nel contesto del pacchetto. In caso di dubbi o preoccupazioni in merito alle informazioni qui contenute, o se hai bisogno di aiuto e consigli aggiuntivi da un punto di vista legale, consiglierei di consultare un professionista legale qualificato.

#### 9.1 RESPONSABILITÀ

Come già indicato dalla licenza del pacchetto, il pacchetto è fornito senza alcuna garanzia. Questo include (ma non è limitato a) tutti gli ambiti di responsabilità. Il pacchetto ti è stato fornito per vostra comodità, nella speranza che sia utile e che ti fornisca alcuni vantaggi. Tuttavia, se si utilizza o si implementa il pacchetto, è una scelta personale. Non sei obbligato a utilizzare o implementare il pacchetto, ma quando lo fai, sei responsabile di tale decisione. Né io né alcun altro contributore al pacchetto siamo legalmente responsabili delle conseguenze delle decisioni che prendete, indipendentemente dal fatto che siano dirette, indirette, implicite, o meno.

#### 9.2 TERZE PARTI

A seconda della sua esatta configurazione e implementazione, in alcuni casi il pacchetto può comunicare e condividere informazioni con terze parti. Questa informazione può essere definita come "[dati personali](https://it.wikipedia.org/wiki/Dati_personali)" (PII) in alcuni contesti, da alcune giurisdizioni.

Il modo in cui queste informazioni possono essere utilizzate da queste terze parti, è soggetto alle varie politiche stabilite da queste terze parti e non rientra nell'ambito di questa documentazione. Tuttavia, in tutti questi casi, la condivisione di informazioni con queste terze parti può essere disabilitata. In tutti questi casi, se si sceglie di abilitarlo, è vostra responsabilità ricercare eventuali eventuali dubbi relativi alla privacy, alla sicurezza e all'utilizzo delle PII da parte di queste terze parti. In caso di dubbi, o se non sei soddisfatto della condotta di queste terze parti in merito alle PII, è meglio disabilitare tutte le informazioni condivise con queste terze parti.

Ai fini della trasparenza, il tipo di informazioni condivise e con chi è descritto di seguito.

##### 9.2.0 RICERCA DEL NOME HOST

Se si utilizzano funzioni o moduli destinati a funzionare con nomi host (come ad esempio il "modulo bloccante di cattivi host", "tor project exit nodes block module", o la "verifica dei motori di ricerca"), CIDRAM deve essere in grado di ottenere in qualche modo il nome host delle richieste in entrata. In genere, lo fa richiedendo il nome host dell'indirizzo IP delle richieste in entrata da un server DNS o richiedendo le informazioni tramite la funzionalità fornita dal sistema su cui è installato CIDRAM (questo in genere viene definito come un "ricerca del nome host"). I server DNS definiti per impostazione predefinita appartengono al servizio di [Google DNS](https://dns.google.com/) (ma possono essere facilmente modificati tramite la configurazione). I servizi esatti comunicati sono configurabili, e dipendono dalla modalità di configurazione del pacchetto. Nel caso in cui si utilizzi la funzionalità fornita dal sistema in cui è installato CIDRAM, è necessario contattare l'amministratore di sistema per determinare quali percorsi utilizzano le ricerche del nome host. Le ricerche del nome host possono essere prevenute in CIDRAM evitando i moduli interessati o modificando la configurazione del pacchetto in base alle proprie esigenze.

*Direttive di configurazione rilevanti:*
- `general` -> `allow_gethostbyaddr_lookup`
- `general` -> `default_dns`
- `general` -> `force_hostname_lookup`
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.1 VERIFICA DEI MOTORI DI RICERCA E DEI SOCIAL MEDIA

Quando la verifica dei motori di ricerca è abilitata, CIDRAM tenta di eseguire "inoltrare ricerche DNS" per verificare se le richieste che provengono presumibilmente dai motori di ricerca sono autentiche. Allo stesso modo, quando la verifica dei social media è abilitata, CIDRAM fa lo stesso per le apparenti richieste di social media. Per fare ciò, utilizza il servizio [Google DNS](https://dns.google.com/) per tentare di risolvere gli indirizzi IP dai nomi host di queste richieste in entrata (in questo processo, i nomi host di queste richieste in entrata sono condivisi con il servizio).

*Direttive di configurazione rilevanti:*
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.2 CAPTCHA

CIDRAM supporta i CAPTCHA. Richiedono chiavi API per funzionare correttamente. Sono disabilitati per impostazione predefinita, ma possono essere abilitati configurando le chiavi API richieste. Se abilitato, può verificarsi la comunicazione tra il servizio e CIDRAM o il browser dell'utente. Ciò può potenzialmente comportare la comunicazione di informazioni come l'indirizzo IP dell'utente, l'agente utente, il sistema operativo, e altri dettagli disponibili per la richiesta.

##### 9.2.3 STOP FORUM SPAM

[Stop Forum Spam](https://www.stopforumspam.com/) è un servizio fantastico, disponibile gratuitamente che può aiutare a proteggere forum, blog, e siti Web dagli spammer. Lo fa fornendo un database di spammer conosciuti e un'API che può essere sfruttata per verificare se un indirizzo IP, un nome utente, o un indirizzo di posta elettronica sono elencati nel suo database.

CIDRAM fornisce un modulo opzionale che sfrutta questa API per verificare se l'indirizzo IP delle richieste in entrata appartiene a un sospetto spammer. Quando il modulo è installato e attivato, gli indirizzi IP dell'utente possono essere condivisi con il servizio in conformità con la configurazione e allo scopo previsto del modulo.

##### 9.2.4 ABUSEIPDB

CIDRAM fornisce un modulo opzionale per bloccare indirizzi IP offensivi utilizzando l'API [AbuseIPDB](https://www.abuseipdb.com/). Quando il modulo è installato e attivato, gli indirizzi IP dell'utente possono essere condivisi con il servizio in conformità con la configurazione e allo scopo previsto del modulo.

##### 9.2.5 BGPVIEW, IP-API

CIDRAM fornisce moduli opzionali per eseguire ricerche di ASN e codice paese utilizzando l'API [BGPView](https://bgpview.io/) e l'API [IP-API](https://ip-api.com/). Queste ricerche offrono la possibilità di bloccare o evitare di bloccare le richieste in base al loro ASN o paese di origine. Quando uno di essi è installato e attivato, gli indirizzi IP dell'utente possono essere condivisi con il servizio in conformità con la configurazione e allo scopo previsto del modulo.

##### 9.2.6 PROJECT HONEYPOT

CIDRAM fornisce un modulo opzionale per bloccare indirizzi IP offensivi utilizzando l'API [Project Honeypot](https://www.projecthoneypot.org/). Quando il modulo è installato e attivato, gli indirizzi IP dell'utente possono essere condivisi con il servizio in conformità con la configurazione e allo scopo previsto del modulo.

#### 9.3 REGISTRAZIONE

La registrazione è una parte importante di CIDRAM per una serie di motivi. Potrebbe essere difficile diagnosticare e risolvere i falsi positivi quando gli eventi di blocco che li causano non vengono registrati. Senza registrare gli eventi di blocco, potrebbe essere difficile accertare esattamente quanto è performante CIDRAM in un particolare contesto, e potrebbe essere difficile determinare dove potrebbero essere le sue carenze, e quali modifiche potrebbero essere richieste alla sua configurazione o alle sue firme di conseguenza, affinché possa continuare a funzionare come previsto. Ciò nonostante, la registrazione potrebbe non essere auspicabile per tutti gli utenti, e rimane del tutto facoltativa. In CIDRAM, la registrazione è disabilitata per impostazione predefinita. Per abilitarlo, CIDRAM deve essere configurato di conseguenza.

Inoltre, se la registrazione è legalmente ammissibile, e nella misura in cui è legalmente ammissibile (ad esempio, i tipi di informazioni che possono essere registrati, per quanto tempo, e in quali circostanze), può variare, a seconda della giurisdizione e del contesto in cui è implementata la CIDRAM (ad esempio, se stai operando come individuo, come entità aziendale, e se commerciale o non commerciale). Potrebbe quindi essere utile leggere attentamente questa sezione.

Esistono diversi tipi di registrazione che CIDRAM può eseguire. Diversi tipi di registrazione coinvolgono diversi tipi di informazioni, per diversi motivi.

##### 9.3.0 EVENTI DI BLOCCO

Il tipo principale di registrazione che CIDRAM può eseguire correla agli "eventi di blocco". Questo tipo di registrazione si riferisce a quando CIDRAM blocca una richiesta, e può essere fornita in tre formati diversi:
- File di log leggibili dall'uomo.
- File di log in stile Apache.
- File di log serializzati.

Un evento di blocco, registrato in un file di log leggibile dall'uomo, in genere assomiglia a qualcosa come questo (ad esempio):

```
ID: 1234
Versione dello script: CIDRAM v1.6.0
Data/Tempo: Day, dd Mon 20xx hh:ii:ss +0000
Indirizzo IP: x.x.x.x
Nome host: dns.hostname.tld
Firme Conteggio: 1
Firme Riferimento: x.x.x.x/xx
Perché Bloccato: Servizio cloud ("Nome della rete", Lxx:Fx, [XX])!
User Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
URI Ricostruito: https://your-site.tld/index.php
Stato CAPTCHA: Attivato.
```

Lo stesso evento di blocco, registrato in un file di log in stile Apache, sarebbe simile a questo:

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

Un evento di blocco registrato include in genere le seguenti informazioni:
- Un numero ID che fa riferimento all'evento di blocco.
- La versione di CIDRAM attualmente in uso.
- La data e l'ora in cui si è verificato l'evento di blocco.
- L'indirizzo IP della richiesta bloccata.
- Il nome host dell'indirizzo IP della richiesta bloccata (se disponibile).
- Il numero di firme innescate dalla richiesta.
- Riferimenti alle firme innescate.
- Riferimenti ai motivi dell'evento di blocco e alcune informazioni di debug di base correlate.
- L'agente utente della richiesta bloccata (cioè, come l'entità richiedente si è identificata nella richiesta).
- Una ricostruzione dell'identificatore per la risorsa originariamente richiesta.
- Lo stato CAPTCHA per la richiesta corrente (se pertinente).

*Le direttive di configurazione responsabili di questo tipo di registrazione, e per ciascuno dei tre formati disponibili sono:*
- `logging` -> `apache_style_log`
- `logging` -> `serialised_log`
- `logging` -> `standard_log`

Quando queste direttive vengono lasciate vuote, questo tipo di registrazione rimarrà disabilitato.

##### 9.3.1 REGISTRI DI CAPTCHA

Questo tipo di registrazione è specifico per le istanze CAPTCHA, e si verifica solo quando un utente tenta di completare un'istanza di CAPTCHA.

Una voce di registro CAPTCHA contiene l'indirizzo IP dell'utente che tenta di completare un'istanza di CAPTCHA, la data e l'ora in cui si è verificato il tentativo, e lo stato CAPTCHA. Una voce di registro CAPTCHA in genere assomiglia a qualcosa come questo (ad esempio):

```
Indirizzo IP: x.x.x.x - Date/Time: Day, dd Mon 20xx hh:ii:ss +0000 - Stato CAPTCHA: Successo!
```

*La direttiva di configurazione responsabile delle registri di CAPTCHA è:*
- `captcha` -> `log`

##### 9.3.2 REGISTRI DEL FRONT-END

Questo tipo di registrazione si riferisce ai tenta di accedere al front-end, e si verifica solo quando un utente tenta di accedere al front-end (supponendo che l'accesso front-end sia abilitato).

Una voce di registro front-end contiene l'indirizzo IP dell'utente che tenta di accedere, la data e l'ora in cui si è verificato il tentativo, e i risultati del tentativo (se il tentativo è fallito o è riuscito). Una voce di registro front-end in genere assomiglia a qualcosa come questo (ad esempio):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Connesso.
```

*La direttiva di configurazione responsabile delle registri di front-end è:*
- `frontend` -> `frontend_log`

##### 9.3.3 ROTAZIONE DEL REGISTRO

Forse vuoi eliminare i log dopo un certo periodo di tempo, o forse sei obbligato a farlo per legge (cioè, la quantità di tempo per cui è legalmente ammissibile per te conservare i log può essere limitata dalla legge). È possibile ottenere ciò includendo indicatori di data/ora nei nomi dei file di log come specificato dalla configurazione del pacchetto (per esempio, `{yyyy}-{mm}-{dd}.log`), e quindi abilitando la rotazione del registro (la rotazione del registro permette di eseguire alcune azioni sui file di log quando vengono superati i limiti specificati).

Per esempio: Se dovessi legalmente richiesto di eliminare i log dopo 30 giorni, potrei specificare `{dd}.log` nei nomi dei miei file di log (`{dd}` rappresenta i giorni), impostare il valore di `log_rotation_limit` su 30, e impostare il valore di `log_rotation_action` su `Delete`.

Al contrario, se è necessario conservare i log per un lungo periodo di tempo, potresti scegliere di non utilizzare la rotazione del registro affatto, oppure puoi impostare il valore di `log_rotation_action` su `Archive`, per comprimere i file di log, riducendo in tal modo la quantità totale di spazio su disco che occupano.

*Direttive di configurazione rilevanti:*
- `logging` -> `log_rotation_action`
- `logging` -> `log_rotation_limit`

##### 9.3.4 TRONCAMENTO DEL REGISTRO

È anche possibile troncare i singoli file di registro quando superano una dimensione predeterminata, se questo è qualcosa che potrebbe essere necessario o desiderare.

*Direttive di configurazione rilevanti:*
- `logging` -> `truncate`

##### 9.3.5 PSEUDONIMIZZAZIONE DELL'INDIRIZZO IP

Innanzitutto, se non hai familiarità con il termine, "pseudonimizzazione" si riferisce al trattamento di dati personali in quanto tali che non può più essere identificato con alcun interessato specifico senza informazioni supplementari, e a condizione che tali informazioni supplementari siano mantenute separatamente e soggette a misure tecniche e organizzative per garantire che i dati personali non possano essere identificati da alcuna persona naturale.

In alcune circostanze, potrebbe essere richiesto per legge di anonimizzare o pseudonimizzare qualsiasi informazione personale raccolta, elaborata, o memorizzata. Sebbene questo concetto sia esistito già da un po' di tempo, GDPR/DSGVO menziona in particolare, e in particolare incoraggia la "pseudonimizzazione".

CIDRAM è in grado di pseudonimizzare gli indirizzi IP durante la registrazione, se questo è qualcosa che potresti aver bisogno o vuoi fare. Quando gli indirizzi IP sono pseudonimizzati da CIDRAM, quando registrati, l'ottetto finale degli indirizzi IPv4 e tutto ciò che segue la seconda parte degli indirizzi IPv6 è rappresentato da una "x" (arrotondare efficacemente gli indirizzi IPv4 all'indirizzo iniziale della 24a sottorete in cui fanno fattore e gli indirizzi IPv6 all'indirizzo iniziale della 32a sottorete a cui fanno fattore).

*Nota: Il processo di pseudonimizzazione degli indirizzi IP in CIDRAM non influisce sulla funzionalità di tracciamento IP in CIDRAM. Se questo è un problema per te, potrebbe essere meglio disabilitare completamente il tracciamento IP.*

*Direttive di configurazione rilevanti:*
- `legal` -> `pseudonymise_ip_addresses`

##### 9.3.6 OMETTENDO LE INFORMAZIONI DEL REGISTRO

Se si desidera fare un ulteriore passo avanti impedendo che determinati tipi di informazioni vengano registrati interamente, è anche possibile farlo. Nella pagina di configurazione, fare riferimento alla direttiva di configurazione `fields` per controllare quali campi vengono visualizzati nelle voci di registro e nella pagina "Accesso Negato".

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

*Nota: Non c'è motivo di pseudonimizzare gli indirizzi IP quando li si omette completamente dai log.*

*Direttive di configurazione rilevanti:*
- `general` -> `fields`

##### 9.3.7 STATISTICA

CIDRAM è facoltativamente in grado di tracciare statistiche come il numero totale di eventi di blocco o istanze di CAPTCHA che si sono verificati da un certo punto nel tempo. Questa funzione è disabilitata per impostazione predefinita, ma può essere abilitata tramite la configurazione del pacchetto. Questa funzione traccia solo il numero totale di eventi verificatisi e non include alcuna informazione su eventi specifici (e quindi non dovrebbe essere considerata come PII).

*Direttive di configurazione rilevanti:*
- `general` -> `statistics`

##### 9.3.8 CRITTOGRAFIA

CIDRAM non crittografa la sua cache o alcuna informazione di registro. La [crittografia](https://it.wikipedia.org/wiki/Crittografia) della cache e del registro potrebbe essere introdotta in futuro, ma al momento non sono previsti piani specifici. Se sei preoccupato per le terze parti non autorizzate che accedono a parti di CIDRAM che potrebbero contenere informazioni personali o riservate quali la cache o i registri, ti consiglio di non installare CIDRAM in una posizione accessibile al pubblico (per esempio, installare CIDRAM al di fuori della directory `public_html` standard o equivalente di quella disponibile per la maggior parte dei server Web standard) e che le autorizzazioni appropriatamente restrittive siano applicate per la directory in cui risiede (in particolare, per la directory del vault). Se ciò non è sufficiente per risolvere i tuoi dubbi, allora configura CIDRAM in modo tale che i tipi di informazioni che causano i tuoi dubbi non saranno raccolti o registrati in primo luogo (ad esempio, di disabilitando la registrazione).

#### 9.4 COOKIE

CIDRAM imposta i [cookie](https://it.wikipedia.org/wiki/Cookie) in due punti nella sua base di codice. Innanzitutto, a seconda di come è stato configurato `lockto`, CIDRAM potrebbe impostare un cookie per ricordare quando un utente ha completato un CAPTCHA. In secondo luogo, quando un utente accede con successo al front-end, CIDRAM imposta un cookie per poter ricordare all'utente le richieste successive (cioè, i cookie vengono utilizzati per autenticare l'utente in una sessione di accesso).

In entrambi i casi, gli avvertimenti sui cookie vengono visualizzati in modo prominenti (se applicabile), avvisando l'utente che i cookie verranno impostati se si impegnano nell'azioni in questione. I cookie non sono impostati in altri punti della base di codice.

*Nota: Le API CAPTCHA "invisibili" potrebbero essere incompatibili con le leggi sui cookie in alcune giurisdizioni, e dovrebbe essere evitato da qualsiasi sito web soggetto a tali leggi. Scegliere di utilizzare invece le altre API fornite, o semplicemente disabilitare il CAPTCHA completamente, potrebbe essere preferibile.*

*Direttive di configurazione rilevanti:*
- `captcha` -> `lockto`
- `captcha` -> `api`

#### 9.5 MARKETING E PUBBLICITÀ

CIDRAM non raccoglie né elabora alcuna informazione per scopi di marketing o pubblicitari, e non vende né guadagna da alcuna informazione raccolta o registrata. CIDRAM non è un'impresa commerciale, né è collegata ad alcun interesse commerciale, quindi fare queste cose non avrebbe alcun senso. Questo è stato il caso dall'inizio del progetto e continua ad esserlo oggi. Inoltre, fare queste cose sarebbe controproducente per lo spirito e lo scopo del progetto nel suo insieme e, finché continuerò a mantenere il progetto, non accadrà mai.

#### 9.6 POLITICA SULLA PRIVACY

In alcune circostanze, potresti essere legalmente obbligato a mostrare chiaramente un link alla tua politica sulla privacy su tutte le pagine e sezioni del tuo sito web. Questo può essere importante come mezzo per garantire che gli utenti siano ben informati delle tue esatte pratiche sulla privacy, i tipi di Informazioni personali che raccogli, e come intendi usarli. Per poter includere tale link nella pagina "Accesso Negato" di CIDRAM, viene fornita una direttiva di configurazione per specificare l'URL della tua politica sulla privacy.

*Nota: Si raccomanda vivamente che la pagina della politica sulla privacy non sia posizionata dietro la protezione di CIDRAM. Se CIDRAM protegge la tua politica sulla privacy, e un utente bloccato da CIDRAM fa clic sul link alla tua politica sulla privacy, verrà semplicemente bloccato di nuovo e non sarà in grado di vedere la tua politica sulla privacy. Idealmente, dovresti collegare a una copia statica della tua politica sulla privacy, come una pagina HTML o un file di testo semplice che non è protetto da CIDRAM.*

*Direttive di configurazione rilevanti:*
- `legal` -> `privacy_policy`

#### 9.7 GDPR/DSGVO

Il regolamento generale sulla protezione dei dati (GDPR) è un regolamento dell'Unione europea, che entrerà in vigore il 25 maggio 2018. L'obiettivo principale del regolamento è di dare il controllo dei cittadini e dei residenti dell'UE sui propri dati personali, e di unificare il regolamento all'interno dell'UE in materia di privacy e dati personali.

Il regolamento contiene disposizioni specifiche relative al trattamento di "[dati personali](https://it.wikipedia.org/wiki/Dati_personali)" (PII) di qualsiasi "interessato" (qualsiasi persona naturale identificata o identificabile) dall'UE o all'interno dell'UE. Per essere conformi al regolamento, le "imprese" (come definite dal regolamento), e tutti i sistemi e processi rilevanti devono implementare "[privacy by design](https://it.wikipedia.org/wiki/Privacy_by_design)" per impostazione predefinita, deve utilizzare le impostazioni di privacy più alte possibili, deve implementare le necessarie salvaguardie per qualsiasi informazione archiviata o elaborata (inclusa, ma non limitata a, l'implementazione della pseudonimizzazione o la completa anonimizzazione dei dati), deve dichiarare in modo chiaro e inequivocabile i tipi di dati che raccolgono, come li elaborano, per quali ragioni, per quanto tempo lo conservano, e se condividono questi dati con terze parti, i tipi di dati condivisi con terze parti, come, perché, e così via.

I dati non possono essere elaborati a meno che non vi sia una base legale per farlo, come definito dal regolamento. In generale, ciò significa che, al fine di elaborare i dati di un interessati su base legale, deve essere fatto in conformità con gli obblighi legali, o fatto solo dopo il consenso esplicito, ben informato, e non ambiguo è stato ottenuto dall'interessato.

Poiché gli aspetti del regolamento possono evolversi nel tempo, al fine di evitare la propagazione di informazioni obsolete, potrebbe essere meglio conoscere il regolamento da una fonte autorevole, al contrario di includere semplicemente le informazioni rilevanti qui nella documentazione del pacchetto (che potrebbe diventare obsoleto con l'evoluzione del regolamento).

[EUR-Lex](https://eur-lex.europa.eu/) (una parte del sito web ufficiale dell'Unione europea che fornisce informazioni sul diritto dell'UE) fornisce ampie informazioni su GDPR/DSGVO, disponibile in 24 lingue diverse (al momento della stesura di questo documento), e disponibile per il download in formato PDF. Consiglio vivamente di leggere le informazioni che forniscono, per saperne di più su GDPR/DSGVO:
- [REGOLAMENTO (UE) 2016/679 DEL PARLAMENTO EUROPEO E DEL CONSIGLIO](https://eur-lex.europa.eu/legal-content/IT/TXT/?uri=celex:32016R0679)

In alternativa, è disponibile una breve panoramica (non autorevole) di GDPR/DSGVO su Wikipedia:
- [Regolamento generale sulla protezione dei dati](https://it.wikipedia.org/wiki/Regolamento_generale_sulla_protezione_dei_dati)

---


### 10. <a name="SECTION10"></a>AGGIORNAMENTO DA VERSIONI PRINCIPALI PRECEDENTI

#### 10.0 Aggiornamento a CIDRAM v3

Esistono differenze significative tra la v3 e le versioni principali precedenti. Il modo in cui funzionano gli punti di ingresso, il modo in cui i moduli sono strutturati, e il modo in cui il programma di aggiornamento funziona per v3 è diverso dal modo in cui queste cose funzionavano per le versioni principali precedenti. A causa di queste differenze, il modo migliore per eseguire l'aggiornamento alla v3 dalle versioni principali precedenti sarebbe eseguire una nuova installazione.

Se vuoi mantenere la tua configurazione e le tue regole ausiliarie, prima di iniziare il processo di aggiornamento, vai alla pagina di backup front-end. Da qui è possibile esportare la configurazione e le regole ausiliarie. L'esportazione causerà il download di un file. Dopo l'aggiornamento alla nuova versione principale, tale file può essere utilizzato per importare nell'installazione i dati precedentemente esportati.

A causa delle modifiche al modo in cui i moduli sono strutturati, i moduli destinati alle versioni principali precedenti dovrebbero essere riscritti per funzionare correttamente per v3. La migrazione diretta non funzionerà. Lo stesso vale per gli eventi.

Il modo in cui sono strutturati i file delle firme non è cambiato, quindi i file delle firme destinati alle versioni principali precedenti possono essere migrati direttamente nella v3 senza alcun problema previsto.

I moduli, i file delle firme, e gli eventi hanno ciascuno le proprie directory dedicate, che è una nuova aggiunta dalla v3 (quindi, per v3, andrebbero ciascuno nelle rispettive directory dedicate, invece che nella radice del vault).

Alcuni dei file delle firme, dei moduli, e delle liste di blocco disponibili pubblicamente per le versioni principali precedenti sono stati deprecati, quindi non tutto sarà disponibile per la v3. Nella maggior parte dei casi, non saranno comunque necessari, a causa delle nuove funzionalità aggiunte dalla v3.

Ci sono alcune sottili modifiche al modo in cui sono strutturate le regole ausiliarie, e ci sono modifiche alla configurazione, ma se utilizzi la funzione di importazione/esportazione nella pagina di backup front-end, non avrai bisogno di riscrivere, regolare, o ricreare manualmente nulla. Durante l'importazione, CIDRAM sa cosa è necessario e lo gestirà automaticamente per te.

Per un elenco delle modifiche introdotte dalla v3 (ad esempio, funzionalità aggiunte, funzionalità rimosse, ecc), fare riferimento al [changelog della v3](https://github.com/CIDRAM/CIDRAM/blob/v3/Changelog.md#v300).

#### 10.1 Aggiornamento a CIDRAM v4 da una versione precedente a CIDRAM v3

Fare riferimento a quanto sopra: Si consiglia una nuova installazione.

#### 10.2 Aggiornamento a CIDRAM v4 da CIDRAM v3

1. Per prima cosa, vai alla pagina degli aggiornamenti front-end e, se sono disponibili aggiornamenti, assicurati di installarli tutti. Ciò garantisce che qualsiasi codice scritto più di recente, che potrebbe essere necessario per aggiornare correttamente le versioni principali, sarà disponibile per l'aggiornamento e aiuta anche a ridurre la quantità di lavoro che l'aggiornamento dovrà svolgere quando aggiornerà le versioni principali in un secondo momento.

2. Vai alla pagina di configurazione front-end e cerca __`frontend➡remotes`__. Nell'elenco, dove vedi `/v3/`, cambialo in `/v4/`. Fare clic su aggiornarlo per salvare la configurazione. Questa modifica indica all'aggiornamento di prendere di mira la versione principale prevista quando cerca aggiornamenti.

3. Vai alla pagina di backup front-end. Selezionare esportare, spuntare le caselle di controllo per la configurazione, per le statistiche, e per le regole ausiliarie, quindi premere OK per scaricare un backup. Sono state apportate alcune modifiche. Ad esempio, l'azione "non registrare" è stata rimossa dalle regole ausiliarie (per ottenere lo stesso risultato è possibile utilizzare l'opzione "sopprimi la registrazione"). Dopo l'aggiornamento, sarà necessario importare nuovamente questo backup in CIDRAM.

4. Vai alla pagina degli aggiornamenti front-end. Ora dovrebbero apparire gli aggiornamenti per la nuova versione principale. Per evitare timeout, prima di aggiornare tutto, prova ad aggiornare solo il core CIDRAM o il front-end CIDRAM (poiché entrambi sono interdipendenti l'uno dall'altro, aggiornandone uno dovrebbero comunque aggiornarli automaticamente entrambi). Poiché la struttura della pagina e lo stile CSS per il front-end sono cambiati in modo significativo tra le versioni principali, inizialmente potrebbe sembrare non funzionante dopo l'aggiornamento; non lo è. Vai a qualsiasi altra pagina front-end e premi Ctrl+F5 per provare a eseguire un aggiornamento forzato (ovvero un aggiornamento tramite il quale il browser recupera una nuova copia dello stile CSS e di altre periferiche invece di affidarsi alla propria cache). La struttura della pagina e lo stile CSS dovrebbero ora apparire correttamente. In caso contrario, prova a svuotare la cache del browser.

5. Ora che il core e il front-end sono stati aggiornati, e la struttura della pagina e lo stile CSS appaiono correttamente, puoi aggiornare tutto il resto. Vai alla pagina degli aggiornamenti front-end e, se vedi il pulsante nella parte superiore della pagina, fai clic su aggiorna tutto.

6. Per assicurarti che non ci siano aggiornamenti errati persistenti, passati o presenti, o file corrotti nell'installazione, e per assicurarti che tutto sia come dovrebbe essere, fai clic su ripara tutto. Molto raramente questo dovrebbe rappresentare un problema reale, ma è meglio andare sul sicuro.

7. Vai alla pagina di backup front-end. Selezionare importare, spuntare le caselle di controllo per la configurazione, per le statistiche, e per le regole ausiliarie, fare clic sul pulsante per selezionare un file, individuare e selezionare il backup scaricato in precedenza e, premere OK per importare tale backup. CIDRAM eseguirà automaticamente tutte le modifiche necessarie per adattarle ai cambiamenti.

8. Ora che hai aggiornato con successo le versioni principali, potresti voler esplorare brevemente la pagina di configurazione front-end a causa delle modifiche introdotte dalla nuova versione principale (ad esempio, per le nuove funzionalità introdotte). A parte questo, hai completato l'aggiornamento. La nuova versione principale non introduce alcuna modifica ai file di firma, ai moduli, o agli eventi, quindi non devi preoccuparti di questo durante l'aggiornamento.

Per un elenco delle modifiche introdotte dalla v4 (ad esempio, funzionalità aggiunte, funzionalità rimosse, ecc), fare riferimento al [changelog della v4](https://github.com/CIDRAM/CIDRAM/blob/v4/Changelog.md#v400).

---


Ultimo Aggiornamento: 1 Aprile 2026 (2026.04.01).
