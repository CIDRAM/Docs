## Documentatie voor CIDRAM v3 (Nederlandse).

### Inhoud
- 1. [PREAMBULE](#user-content-SECTION1)
- 2. [HOE TE INSTALLEREN](#user-content-SECTION2)
- 3. [HOE TE GEBRUIKEN](#user-content-SECTION3)
- 4. [FRONTEND MANAGEMENT](#user-content-SECTION4)
- 5. [CONFIGURATIE-OPTIES](#user-content-SECTION5)
- 6. [SIGNATURE FORMAAT](#user-content-SECTION6)
- 7. [BEKENDE COMPATIBILITEITSPROBLEMEN](#user-content-SECTION7)
- 8. [VEELGESTELDE VRAGEN (FAQ)](#user-content-SECTION8)
- 9. [LEGALE INFORMATIE](#user-content-SECTION9)
- 10. [UPGRADEN VAN EERDERE HOOFDVERSIES](#user-content-SECTION10)

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### 1. <a name="SECTION1"></a>PREAMBULE

CIDRAM (Classless Inter-Domain Routing Access Manager) is een PHP-script ontworpen om sites te beschermen door het blokkeren van verzoeken afkomstig van IP-adressen beschouwd als bronnen van ongewenste verkeer, inclusief (maar niet gelimiteerd tot) het verkeer van niet-menselijke toegang eindpunten, cloud diensten, spambots, schrapers/scrapers, enz. Het doet dit door het berekenen van de mogelijke CIDR's van de IP-adressen geleverde van binnenkomende verzoeken en dan het vergelijken van deze mogelijke CIDR's tegen zijn signatuurbestanden (deze signatuurbestanden bevatten lijsten van CIDR's van IP-adressen beschouwd als bronnen van ongewenste verkeer); Als overeenkomsten worden gevonden, de verzoeken worden geblokkeerd.

*(Zien: [Wat is een "CIDR"?](#user-content-WHAT_IS_A_CIDR)).*

[CIDRAM](https://cidram.github.io/) COPYRIGHT 2016 en verder GNU/GPLv2 van [Caleb M (Maikuolan)](https://github.com/Maikuolan).

Dit script is gratis software; u kunt, onder de voorwaarden van de GNU General Public License zoals gepubliceerd door de Free Software Foundation, herdistribueren en/of wijzigen dit; ofwel versie 2 van de Licentie, of (naar uw keuze) enige latere versie. Dit script wordt gedistribueerd in de hoop dat het nuttig zal zijn, maar ZONDER ENIGE GARANTIE; zonder zelfs de impliciete garantie van VERKOOPBAARHEID of GESCHIKTHEID VOOR EEN BEPAALD DOEL. Zie de GNU General Public License voor meer informatie, gelegen in het `LICENSE.txt` bestand en ook beschikbaar uit:
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

Dit document en de bijbehorende pakket kunt gedownload gratis zijn van:
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [SourceForge](https://sourceforge.net/projects/cidram/).

---


### 2. <a name="SECTION2"></a>HOE TE INSTALLEREN

#### 2.0 HANDMATIG INSTALLEREN

Eerste, nodig u een nieuwe kopie van CIDRAM. U kunt een archief van de nieuwste versie van CIDRAM downloaden van de [CIDRAM/CIDRAM](https://github.com/CIDRAM/CIDRAM)-repository. In het bijzonder nodig u een nieuwe kopie van de "vault"-map (alles uit het archief behalve de "vault"-map en de inhoud ervan kan veilig worden verwijderd of genegeerd).

Vóór v3 was het nodig om CIDRAM ergens in je openbare root te installeren om toegang te krijgen tot de CIDRAM-frontend. Vanaf v3 echter dat is niet meer nodig, en om de veiligheid te maximaliseren en ongeoorloofde toegang tot CIDRAM en zijn bestanden te voorkomen, wordt aanbevolen om in plaats om CIDRAM *buiten* uw openbare root te installeren. U kunt CIDRAM installeren waar u wilt, zolang het ergens toegankelijk met PHP, ergens redelijk veilig, en ergens u tevreden over. Het is ook niet meer nodig om de naam van de "vault"-map te behouden, dus u kunt de "vault"-map hernoemen naar elke gewenste naam (maar voor het gemak zal de documentatie ernaar blijven verwijzen als "vault").

Upload de "vault"-map naar de gekozen locatie en zorg ervoor dat het de benodigde machtigingen heeft zodat PHP kan schrijven naar de map (afhankelijk van het systeem hoeft u soms niets te doen, of soms moet u CHMOD 755 in de directory zetten, of als er problemen zijn met 755, u kunt 777 proberen, maar 777 wordt niet aanbevolen omdat het minder veilig is).

Om CIDRAM in staat te stellen uw codebase of CMS te beschermen, moet u vervolgens een "ingangspunt" maken. Zo'n ingangspunt bestaat uit drie dingen:

1. Opname van het "loader.php"-bestand op een geschikt punt in uw codebase of CMS.
2. Instantiatie van de CIDRAM core.
3. Aanroepen van de "protect"-methode.

Een eenvoudig voorbeeld:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

Als u een Apache-webserver gebruikt en toegang hebt tot `php.ini`, kunt u de `auto_prepend_file`-richtlijn gebruiken om CIDRAM uit te voeren wanneer een PHP-verzoek wordt gedaan. In een dergelijk geval zou de meest geschikte plaats om uw ingangspunt te creëren in zijn eigen bestand zijn, en u zou dat bestand dan citeren bij de `auto_prepend_file`-richtlijn.

Voorbeeld:

`auto_prepend_file = "/path/to/your/entrypoint.php"`

Of dit in het `.htaccess`-bestand:

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

In andere gevallen is de meest geschikte plaats om uw ingangspunt te maken zo vroeg mogelijk in uw codebase of CMS, zodat het altijd wordt geladen wanneer iemand een pagina op uw website vraagt. Als uw codebase een "bootstrap" gebruikt, een goed voorbeeld zou helemaal aan het begin van uw "bootstrap"-bestand staan. Als uw codebase een centraal bestand heeft dat verantwoordelijk is voor de verbinding met uw database, een ander goed voorbeeld is helemaal aan het begin van dat centrale bestand.

#### 2.1 INSTALLEREN MET COMPOSER

[CIDRAM is geregistreerd bij Packagist](https://packagist.org/packages/cidram/cidram), en dus, als u bekend bent met Composer, kunt u Composer gebruiken om CIDRAM installeren.

`composer require cidram/cidram`

#### 2.2 INSTALLEREN VOOR WORDPRESS

[CIDRAM is geregistreerd als een plugin met de WordPress plugins databank](https://wordpress.org/plugins/cidram/), en u kunt CIDRAM direct vanaf het plugin-dashboard installeren. U kunt het op dezelfde manier installeren als elke andere plugin, en geen toevoeging stappen nodig zijn.

*Waarschuwing: Het bijwerken van CIDRAM via het plugin-dashboard resulteert in een schone installatie! Als u uw installatie hebt aangepast (verander uw configuratie, geïnstalleerde modules, enz), deze aanpassingen worden verloren bij het updaten via het plugin-dashboard! Logbestanden worden ook verloren bij het updaten via het plugin-dashboard! Om de logbestanden en aanpassingen te bewaren, bijwerken via de CIDRAM frontend updates pagina.*

#### 2.3 CONFIGURATIE EN PERSONALISATIE

Het wordt ten zeerste aanbevolen om de configuratie van uw nieuwe installatie te bekijken, zodat u dit aan uw behoeften kunt aanpassen. Mogelijk wilt u ook aanvullende modules or signatuurbestanden te installeren, aanvullende regels te maken, of andere aanpassingen om uw installatie te doorvoeren, zodat dit het beste aansluit bij uw wensen. Ik raad aan om de frontend te gebruiken om deze dingen te doen.

---


### 3. <a name="SECTION3"></a>HOE TE GEBRUIKEN

CIDRAM moet blokkeren ongewenste verzoeken naar uw website automatisch zonder enige handmatige hulp, afgezien van de eerste installatie.

U kunt aanpassen uw configuratie en aanpassen de CIDR's dat zal worden geblokkeerd door het modificeren van het configuratiebestand en/of uw signatuurbestanden.

Als u tegenkomen een valse positieven, neem dan contact met mij op om me te laten weten. *(Zien: [Wat is een "vals positieve"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM kan handmatig of via de frontend worden bijgewerkt. CIDRAM kan ook worden bijgewerkt via Composer of WordPress, indien oorspronkelijk via die middelen geïnstalleerd.

---


### 4. <a name="SECTION4"></a>FRONTEND MANAGEMENT

#### 4.0 WAT IS DE FRONTEND.

De frontend biedt een gemakkelijke en eenvoudige manier te onderhouden, beheren en updaten van uw CIDRAM installatie. U kunt bekijken, delen en downloaden log bestanden via de pagina logs, u kunt de configuratie wijzigen via de configuratiepagina, u kunt installeren en verwijderen/desinstalleren van componenten via de pagina updates, en u kunt uploaden, downloaden en wijzigen bestanden in uw vault via de bestandsbeheer.

#### 4.1 HOE TOEGANG TE KRIJGEN TOT DE FRONTEND.

Net zoals u een ingangspunt moest maken om CIDRAM uw website te laten beschermen, moet u ook een ingangspunt maken om toegang te krijgen tot de frontend. Zo'n ingangspunt bestaat uit drie dingen:

1. Opname van het "loader.php"-bestand op een geschikt punt in uw codebase of CMS.
2. Instantiatie van de CIDRAM frontend.
3. Aanroepen van de "view"-methode.

Een eenvoudig voorbeeld:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

De "FrontEnd"-klasse breidt de "Core"-klasse uit, wat inhoudt dat desgewenst u de "protect"-methode kunt aanroepen voordat de "view"-methode om te voorkomen dat mogelijk ongewenst verkeer toegang krijgt tot de frontend. Dit is geheel optioneel.

Een eenvoudig voorbeeld:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

De beste plaats om een ingangspunt voor de frontend te maken is in een eigen speciaal bestand. In tegenstelling tot uw eerder gemaakte ingangspunt, wilt u dat uw frontend ingangspunt alleen toegankelijk is door rechtstreeks om het specifieke bestand waarin het ingangspunt bestaat te vragen, dus in dit geval wilt u hier geen `auto_prepend_file` of `.htaccess` gebruiken.

Nadat u uw frontend ingangspunt heeft gemaakt, toegang krijgen via uw browser. Er moet een inlogpagina worden weergegeven. Voer op de inlogpagina de standaard gebruikersnaam en wachtwoord (admin/password) in en druk op de inloggen-knop.

Notitie: Nadat u hebt ingelogd voor de eerste keer, om ongeautoriseerde toegang tot de frontend te voorkomen, moet u onmiddellijk veranderen uw gebruikersnaam en wachtwoord! Dit is zeer belangrijk, want het is mogelijk om willekeurige PHP-code te uploaden naar uw website via de frontend.

Voor optimale beveiliging wordt het ten zeerste aanbevolen om "twee-factor authenticatie" voor alle frontend accounts in te schakelen (onderstaande instructies).

#### 4.2 HOE DE FRONTEND GEBRUIKEN.

Instructies worden op elke pagina van de frontend, om uit te leggen hoe het te gebruiken en het beoogde doel. Als u meer uitleg of een speciale hulp nodig hebben, neem dan contact op met ondersteuning. Als alternatief, zijn er een aantal video's op YouTube die zouden kunnen helpen door middel van een demonstratie.

#### 4.3 TWEE-FACTOR AUTHENTICATIE

Het is mogelijk om de frontend veiliger te maken door twee-factor authenticatie ("2FA") in te schakelen. Bij inloggen met een account waarvoor 2FA is ingeschakeld, een e-mail wordt verzonden naar het e-mailadres dat aan dat account is gekoppeld. Deze e-mail bevat een "2FA-code", die de gebruiker vervolgens moet invoeren, in aanvulling op de gebruikersnaam en het wachtwoord, om te kunnen inloggen met dat account. Dit betekent dat het verkrijgen van een accountwachtwoord niet genoeg is voor een hacker of potentiële aanvaller om zich bij dat account te kunnen aanmelden, omdat ze ook al toegang moeten hebben tot het e-mailadres dat aan dat account is gekoppeld om de 2FA-code die aan de sessie is gekoppeld te kunnen ontvangen en gebruiken, daarmee het frontend veiliger maken.

Ten eerste, om twee-factor authenticatie in te schakelen, gebruikt u de frontend-updates-pagina om de PHPMailer-component te installeren. CIDRAM gebruikt PHPMailer voor het verzenden van e-mails.

Nadat u PHPMailer heeft geïnstalleerd, moet u de configuratie-richtlijnen voor PHPMailer invullen via de configuratiepagina of het configuratiebestand van CIDRAM. Meer informatie over deze configuratie-richtlijnen is opgenomen in de configuratiesectie van dit document. Nadat u de PHPMailer-configuratie-richtlijnen hebt ingevuld, stelt u `enable_two_factor` in op `true`. Twee-factor authenticatie moet nu worden ingeschakeld.

Volgende, u moet een e-mailadres koppelen aan een account, zodat CIDRAM weet waar 2FA-codes moeten worden verzonden wanneer hij zich aanmeldt met dat account. Om dit te doen, gebruik het e-mailadres als de gebruikersnaam voor het account (b.v., `foo@bar.tld`), of neem het e-mailadres op als onderdeel van de gebruikersnaam op dezelfde manier als bij het normaal verzenden van een e-mail (b.v., `Foo Bar <foo@bar.tld>`).

Notitie: Het beschermen van uw vault tegen ongeautoriseerde toegang (b.v., door de beveiliging van uw server en openbare toegangsrechten te verbeteren), is hier bijzonder belangrijk, vanwege deze ongeautoriseerde toegang tot uw configuratiebestand (dat is opgeslagen in uw vault), kan het risico lopen dat uw uitgaande SMTP-instellingen (inclusief SMTP gebruikersnaam en wachtwoord) worden weergegeven. U moet ervoor zorgen dat uw vault correct is beveiligd voordat u twee-factor authenticatie inschakelt. Als u dit niet kunt doen, moet u op z'n minst een nieuw e-mailaccount maken, speciaal voor dit doel, om de risico's van blootgestelde SMTP-instellingen te verminderen.

---


### 5. <a name="SECTION5"></a>CONFIGURATIE-OPTIES

Het volgende is een lijst van variabelen die in de `config.yml` configuratiebestand van CIDRAM, samen met een beschrijving van hun doel en functie.

```
Configuratie (v3)
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
│       ban_override [int]
│       default_dns [string]
│       default_algo [string]
│       statistics [string]
│       force_hostname_lookup [bool]
│       allow_gethostbyaddr_lookup [bool]
│       disabled_channels [string]
│       default_timeout [int]
│       sensitive [string]
│       email_notification_address [string]
│       email_notification_name [string]
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
├───verification
│       search_engines [string]
│       social_media [string]
│       other [string]
│       adjust [string]
├───recaptcha
│       usemode [int]
│       lockip [bool]
│       lockuser [bool]
│       sitekey [string]
│       secret [string]
│       expiry [float]
│       recaptcha_log [string]
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
│       hcaptcha_log [string]
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

#### "general" (Categorie)
Algemene configuratie (elke kernconfiguratie die niet tot andere categorieën behoort).

##### "stages" `[string]`
- Controles voor de fasen van de uitvoeringsketen (of ingeschakeld, of fouten worden geregistreerd, enz).

```
stages
├─Tests ("Voer de signatuurbestandentests")
├─Modules ("Voer de modules")
├─SearchEngineVerification ("Voer zoekmachine verificatie")
├─SocialMediaVerification ("Voer sociale media verificatie")
├─OtherVerification ("Voer andere verificatie")
├─Aux ("Voer aanvullende regels")
├─Tracking ("Voer IP-tracking")
├─RL ("Voer tarieflimiet")
├─CAPTCHA ("Voeg CAPTCHA's (geblokkeerde verzoeken)")
├─Reporting ("Voer rapportage")
├─Statistics ("Bijwerk statistieken")
├─Webhooks ("Voer webhooks")
├─PrepareFields ("Voorbereiden velden voor uitvoer en logs")
├─Output ("Genereren uitvoer (geblokkeerde verzoeken)")
├─WriteLogs ("Schrijf naar logs (geblokkeerde verzoeken)")
├─Terminate ("Beëindig het verzoek (geblokkeerde verzoeken)")
├─AuxRedirect ("Omleiden volgens aanvullende regels")
└─NonBlockedCAPTCHA ("Voeg CAPTCHA's (niet-geblokkeerde verzoeken)")
```

##### "fields" `[string]`
- Controles voor de velden tijdens blokgebeurtenissen (wanneer een verzoek wordt geblokkeerd).

```
fields
├─ID ("ID")
├─ScriptIdent ("Script versie")
├─DateTime ("Datum/Tijd")
├─IPAddr ("IP-Adres")
├─IPAddrResolved ("IP-adres (vastbesloten)")
├─Query ("Query")
├─Referrer ("Verwijzer")
├─UA ("Gebruikersagent")
├─UALC ("Gebruikersagent (kleine letters)")
├─SignatureCount ("Signatures tellen")
├─Signatures ("Signatures verwijzing")
├─WhyReason ("Waarom geblokkeerd")
├─ReasonMessage ("Waarom geblokkeerd (gedetailleerd)")
├─rURI ("Gereconstrueerde URI")
├─Infractions ("Overtredingen")
├─ASNLookup ("** ASN opzoeken")
├─CCLookup ("** Landcode opzoeken")
├─Verified ("Geverifieerde identiteit")
├─Expired ("Verlopen")
├─Ignored ("Genegeerd")
├─Request_Method ("Verzoek methode")
├─Protocol ("Protocol")
├─SEC_CH_UA_PLATFORM ("!! SEC_CH_UA_PLATFORM")
├─SEC_CH_UA_MOBILE ("!! SEC_CH_UA_MOBILE")
├─SEC_CH_UA ("!! SEC_CH_UA")
├─Hostname ("Hostname")
├─CAPTCHA ("CAPTCHA state")
├─Inspection ("* Inspectie van de voorwaarden")
└─ClientL10NAccepted ("Taalresolutie")
```

* Alleen bedoeld voor het debuggen van aanvullende regels. Niet weergegeven voor geblokkeerde gebruikers.

** Vereist ASN-opzoekfunctionaliteit (b.v., via de IP-API-module of BGPView-module).

!! Dit is een clienthint met een lage entropie. Clienthints zijn een nieuwe, experimentele webtechnologie die nog niet breed wordt ondersteund door alle browsers en grote clients. *Zien: <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA#browser_compatibility" dir="ltr" hreflang="en-US" rel="noopener noreferrer external">Sec-CH-UA - HTTP | MDN</a>.* Clienthints kunnen nuttig zijn voor het nemen van vingerafdrukken, maar omdat ze niet breed worden ondersteund, er mag niet van worden uitgegaan of op vertrouwd dat ze aanwezig zullen zijn in verzoeken (d.w.z., blokkeren op basis van hun afwezigheid is een slecht idee).

##### "timezone" `[string]`
- Dit wordt gebruikt om de te gebruiken tijdzone op te geven (b.v., Africa/Cairo, America/New_York, Asia/Tokyo, Australia/Perth, Europe/Berlin, Pacific/Guam, enz). Geef "SYSTEM" op om PHP dit automatisch voor u te laten afhandelen.

```
timezone
├─SYSTEM ("Gebruik de systeem standaard tijdzone.")
├─UTC ("UTC")
└─…Anders
```

##### "time_offset" `[int]`
- Tijdzone offset in minuten.

##### "time_format" `[string]`
- De datum notatie gebruikt door CIDRAM. Extra opties kunnen worden toegevoegd op aanvraag.

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
└─…Anders
```

__*Tijdelijke aanduiding – Uitleg – Voorbeeld gebaseerd op 2024-04-30T18:27:49+08:00.*__<br />
`{yyyy}` – Het jaartal – B.v., 2024.<br />
`{yy}` – Het afgekorte jaartal – B.v., 24.<br />
`{Mon}` – De afgekorte naam van de maand (in het Engels) – B.v., Apr.<br />
`{mm}` – De maand met voorloopnullen – B.v., 04.<br />
`{m}` – De maand – B.v., 4.<br />
`{Day}` – De afgekorte naam van de dag (in het Engels) – B.v., Tue.<br />
`{dd}` – De dag met voorloopnullen – B.v., 30.<br />
`{d}` – De dag – B.v., 30.<br />
`{hh}` – Het uur met voorloopnullen (gebruikt 24-uurs tijd) – B.v., 18.<br />
`{h}` – Het uur (gebruikt 24-uurs tijd) – B.v., 18.<br />
`{ii}` – De minuut met voorloopnullen – B.v., 27.<br />
`{i}` – De minuut – B.v., 27.<br />
`{ss}` – De seconde met voorloopnullen – B.v., 49.<br />
`{s}` – De seconde – B.v., 49.<br />
`{tz}` – De tijdzone (zonder dubbele punt) – B.v., +0800.<br />
`{t:z}` – De tijdzone (met dubbele punt) – B.v., +08:00.

##### "ipaddr" `[string]`
- Waar het IP-adres van het aansluiten verzoek te vinden? (Handig voor diensten zoals Cloudflare en dergelijke). Standaard = REMOTE_ADDR. WAARSCHUWING: Verander dit niet tenzij u weet wat u doet!

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (Standaard)")
└─…Anders
```

Zie ook:
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### "http_response_header_code" `[int]`
- Welk HTTP-statusbericht moet CIDRAM verzenden bij het blokkeren van verzoeken?

```
http_response_header_code
├─200 (200 OK): Minst robuust, maar meest gebruiksvriendelijk. Geautomatiseerde verzoeken
│ zullen dit antwoord hoogstwaarschijnlijk interpreteren als een indicatie dat
│ het verzoek was succesvol.
├─403 (403 Forbidden (Verboden)): Robuuster, maar minder gebruiksvriendelijk. Aanbevolen voor de meeste
│ algemene omstandigheden.
├─410 (410 Gone (Weg)): Kan problemen veroorzaken bij het oplossen van valse positieven, omdat
│ sommige browsers dit statusbericht in de cache opslaan en geen volgende
│ verzoeken verzenden, zelfs niet nadat de blokkering is opgeheven. Kan in
│ sommige contexten, voor bepaalde soorten verkeer, de meeste voorkeur hebben.
├─418 (418 I'm a teapot (Ik ben een theepot)): Verwijst naar een 1-aprilgrap (<a href="https://tools.ietf.org/html/rfc2324"
│ dir="ltr" hreflang="en-US" rel="noopener noreferrer external">RFC 2324</a>).
│ Het is zeer onwaarschijnlijk dat deze door een client, bot, browser, of
│ anderszins wordt begrepen. Geleverd voor amusement en gemak, maar over het
│ algemeen niet aanbevolen.
├─451 (451 Unavailable For Legal Reasons (Om juridische redenen onbeschikbaar)): Aanbevolen bij blokkering voornamelijk om juridische redenen. Niet
│ aanbevolen in andere contexten.
└─503 (503 Service Unavailable (Dienst onbeschikbaar)): Meest robuust, maar minst gebruiksvriendelijk. Aanbevolen voor wanneer u
  wordt aangevallen, of wanneer u te maken hebt met extreem hardnekkig
  ongewenst verkeer.
```

##### "silent_mode" `[string]`
- Moet CIDRAM stilletjes omleiden geblokkeerd toegang pogingen in plaats van het weergeven van de "toegang geweigerd" pagina? Als ja, geef de locatie te omleiden geblokkeerd toegang pogingen. Als nee, verlaat deze variabele leeg.

##### "silent_mode_response_header_code" `[int]`
- Welk HTTP-statusbericht moet CIDRAM verzenden bij het stilzwijgend omleiden van geblokkeerde toegangspogingen?

```
silent_mode_response_header_code
├─301 (301 Moved Permanently (Permanent verhuisd)): Instrueert de client dat de omleiding PERMANENT is, en dat de verzoekmethode
│ die wordt gebruikt voor de omleiding KAN verschillen van de verzoekmethode
│ die wordt gebruikt voor het oorspronkelijke verzoek.
├─302 (302 Found (Gevonden)): Instrueert de client dat de omleiding TIJDELIJK is, en dat de verzoekmethode
│ die wordt gebruikt voor de omleiding KAN verschillen van de verzoekmethode
│ die wordt gebruikt voor het oorspronkelijke verzoek.
├─307 (307 Temporary Redirect (Tijdelijke omleiding)): Instrueert de client dat de omleiding TIJDELIJK is, en dat de verzoekmethode
│ die wordt gebruikt voor de omleiding NIET mag verschillen van de
│ verzoekmethode die wordt gebruikt voor het oorspronkelijke verzoek.
└─308 (308 Permanent Redirect (Permanente omleiding)): Instrueert de client dat de omleiding PERMANENT is, en dat de verzoekmethode
  die wordt gebruikt voor de omleiding NIET mag verschillen van de
  verzoekmethode die wordt gebruikt voor het oorspronkelijke verzoek.
```

Het maakt niet uit hoe we de klant instrueren, het is belangrijk om te onthouden dat we uiteindelijk geen controle hebben over wat de klant kiest om te doen, en er is geen enkele garantie dat de klant onze instructies zal opvolgen.

##### "lang" `[string]`
- Geef de standaardtaal voor CIDRAM.

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
├─fr ("Français")
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
- Waar mogelijk lokaliseren volgens HTTP_ACCEPT_LANGUAGE? True = Ja [Standaard]; False = Nee.

##### "numbers" `[string]`
- Hoe verkiest u nummers die worden weergegeven? Selecteer het voorbeeld dat het meest correct voor u lijkt.

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
- Indien u wenst, u kunt een e-mailadres op hier te geven te geven aan de gebruikers als ze geblokkeerd, voor hen te gebruiken als aanspreekpunt voor steun en/of assistentie in het geval dat ze worden onrechte geblokkeerd. WAARSCHUWING: Elke e-mailadres u leveren hier zal zeker worden overgenomen met spambots en schrapers in de loop van zijn wezen die hier gebruikt, en dus, het wordt ten zeerste aanbevolen als u ervoor kiest om een e-mailadres hier te leveren, dat u ervoor zorgen dat het e-mailadres dat u hier leveren is een wegwerp-adres en/of een adres dat u niet de zorg over wordt gespamd (met andere woorden, u waarschijnlijk niet wilt om uw primaire persoonlijk of primaire zakelijke e-mailadressen te gebruik).

##### "emailaddr_display_style" `[string]`
- Hoe zou u het e-mailadres voor gebruikers willen aanbieden?

```
emailaddr_display_style
├─default ("Klikbare link")
└─noclick ("Niet-klikbare tekst")
```

##### "ban_override" `[int]`
- Overrijden "http_response_header_code" wanneer "infraction_limit" wordt overschreden? 200 = Niet overrijden [Standaard]. Andere waarden zijn hetzelfde als de beschikbare waarden voor "http_response_header_code".

```
ban_override
├─200 (200 OK): Minst robuust, maar meest gebruiksvriendelijk. Geautomatiseerde verzoeken
│ zullen dit antwoord hoogstwaarschijnlijk interpreteren als een indicatie dat
│ het verzoek was succesvol.
├─403 (403 Forbidden (Verboden)): Robuuster, maar minder gebruiksvriendelijk. Aanbevolen voor de meeste
│ algemene omstandigheden.
├─410 (410 Gone (Weg)): Kan problemen veroorzaken bij het oplossen van valse positieven, omdat
│ sommige browsers dit statusbericht in de cache opslaan en geen volgende
│ verzoeken verzenden, zelfs niet nadat de blokkering is opgeheven. Kan in
│ sommige contexten, voor bepaalde soorten verkeer, de meeste voorkeur hebben.
├─418 (418 I'm a teapot (Ik ben een theepot)): Verwijst naar een 1-aprilgrap (<a href="https://tools.ietf.org/html/rfc2324"
│ dir="ltr" hreflang="en-US" rel="noopener noreferrer external">RFC 2324</a>).
│ Het is zeer onwaarschijnlijk dat deze door een client, bot, browser, of
│ anderszins wordt begrepen. Geleverd voor amusement en gemak, maar over het
│ algemeen niet aanbevolen.
├─451 (451 Unavailable For Legal Reasons (Om juridische redenen onbeschikbaar)): Aanbevolen bij blokkering voornamelijk om juridische redenen. Niet
│ aanbevolen in andere contexten.
└─503 (503 Service Unavailable (Dienst onbeschikbaar)): Meest robuust, maar minst gebruiksvriendelijk. Aanbevolen voor wanneer u
  wordt aangevallen, of wanneer u te maken hebt met extreem hardnekkig
  ongewenst verkeer.
```

##### "default_dns" `[string]`
- Een lijst met DNS-servers te gebruiken voor de hostnaam lookups. WAARSCHUWING: Verander dit niet tenzij u weet wat u doet!

__FAQ.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.nl.md#wat-kan-ik-gebruiken-voor-default_dns" hreflang="nl-NL">Wat kan ik gebruiken voor "default_dns"?</a>*

##### "default_algo" `[string]`
- Definieert welk algoritme u wilt gebruiken voor alle toekomstige wachtwoorden en sessies.

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### "statistics" `[string]`
- Bepaalt welke statistische informatie moet worden bijgehouden.

```
statistics
├─Blocked-IPv4 ("Verzoeken geblokkeerd – IPv4")
├─Blocked-IPv6 ("Verzoeken geblokkeerd – IPv6")
├─Blocked-Other ("Verzoeken geblokkeerd – Anders")
├─Banned-IPv4 ("Verzoeken verbannen – IPv4")
├─Banned-IPv6 ("Verzoeken verbannen – IPv6")
├─Passed-IPv4 ("Verzoeken toegestaan – IPv4")
├─Passed-IPv6 ("Verzoeken toegestaan – IPv6")
├─Passed-Other ("Verzoeken toegestaan – Anders")
├─CAPTCHAs-Failed ("CAPTCHA pogingen – Mislukt!")
├─CAPTCHAs-Passed ("CAPTCHA pogingen – Succes!")
├─Reported-IPv4-OK ("Verzoeken gerapporteerd aan externe API's – IPv4 – OK")
├─Reported-IPv4-Failed ("Verzoeken gerapporteerd aan externe API's – IPv4 – Mislukt")
├─Reported-IPv6-OK ("Verzoeken gerapporteerd aan externe API's – IPv6 – OK")
└─Reported-IPv6-Failed ("Verzoeken gerapporteerd aan externe API's – IPv6 – Mislukt")
```

Opmerking: Het bijhouden van statistieken voor aanvullende regels kan worden beheerd vanaf de pagina met aanvullende regels.

##### "force_hostname_lookup" `[bool]`
- Hostname-opzoekingen afdwingen? True = Ja; False = Nee [Standaard]. Hostname-opzoekingen worden normaal uitgevoerd op basis van noodzaak, maar kan voor alle verzoeken worden gedwongen. Dit kan nuttig zijn als een middel om meer gedetailleerde informatie in de logbestanden te verstrekken, maar kan ook een licht negatief effect hebben op de prestaties.

##### "allow_gethostbyaddr_lookup" `[bool]`
- Zoeken op gethostbyaddr toestaan als UDP niet beschikbaar is? True = Ja [Standaard]; False = Nee.

Opmerking: IPv6-opzoeken mogelijk werken niet correct op sommige 32-bits systemen.

##### "disabled_channels" `[string]`
- Dit kan worden gebruikt om te voorkomen dat CIDRAM bepaalde kanalen gebruikt bij het verzenden van verzoeken (b.v., bij het bijwerken, bij het ophalen van metagegevens van componenten, enzovoort).

```
disabled_channels
├─GitHub ("GitHub")
├─BitBucket ("BitBucket")
└─GoogleDNS ("GoogleDNS")
```

##### "default_timeout" `[int]`
- Standaard time-out om te gebruiken voor externe verzoeken? Standaard = 12 seconden.

##### "sensitive" `[string]`
- Een lijst met paden die als gevoelige pagina's moeten worden beschouwd. Elk vermeld pad wordt indien nodig gecontroleerd aan de hand van de gereconstrueerde URI. Een pad dat begint met een schuine streep naar voren wordt behandeld als een letterlijke waarde en wordt gematcht vanaf de padcomponent van het verzoek. Anders wordt een pad dat begint met een niet-alfanumeriek teken en eindigt met datzelfde teken (of datzelfde teken plus een optionele "i"-vlag) behandeld als een reguliere expressie. Elk ander pad wordt behandeld als een letterlijk pad en kan overeenkomen met elk deel van de URI. Of een pad als een gevoelige pagina wordt beschouwd, kan van invloed zijn op het gedrag van sommige modules, maar heeft verder geen effect.

##### "email_notification_address" `[string]`
- Als u ervoor heeft gekozen om meldingen van CIDRAM via e-mail te ontvangen, b.v., wanneer specifieke aanvullende regels worden geactiveerd, u kunt hier het adres van de ontvanger voor deze meldingen opgeven.

##### "email_notification_name" `[string]`
- Als u ervoor heeft gekozen om meldingen van CIDRAM via e-mail te ontvangen, b.v., wanneer specifieke aanvullende regels worden geactiveerd, u kunt hier de naam van de ontvanger voor die meldingen opgeven.

#### "components" (Categorie)
Configuratie voor het activeren en het deactiveren van de door CIDRAM gebruikte componenten. Meestal gevuld door de updates-pagina, maar kan ook vanaf hier worden beheerd voor fijnere controle en voor aangepaste componenten die niet worden herkend door de updates-pagina.

##### "ipv4" `[string]`
- IPv4-signatuurbestanden.

##### "ipv6" `[string]`
- IPv6-signatuurbestanden.

##### "modules" `[string]`
- Modules.

##### "imports" `[string]`
- Import. Meestal gebruikt om de configuratie-informatie van een component aan CIDRAM te leveren.

##### "events" `[string]`
- Evenement-Behandelaars. Meestal gebruikt om de manier waarop CIDRAM zich intern gedraagt te wijzigen of om extra functionaliteit te bieden.

#### "logging" (Categorie)
Configuratie gerelateerd aan logging (dat wat gerelateerd aan andere categorieën is uitgesloten).

##### "standard_log" `[string]`
- Mensen leesbare bestand om alle geblokkeerde toegang pogingen te loggen. Geef een bestandsnaam, of laat leeg om uit te schakelen.

Handige tip: U kunt datum-/tijdinformatie aan de namen van logbestanden toevoegen door tijdelijke aanduidingen voor de tijdnotatie te gebruiken. Beschikbare tijdelijke aanduidingen voor tijdnotatie worden weergegeven bij <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "apache_style_log" `[string]`
- Apache-stijl bestand om alle geblokkeerde toegang pogingen te loggen. Geef een bestandsnaam, of laat leeg om uit te schakelen.

Handige tip: U kunt datum-/tijdinformatie aan de namen van logbestanden toevoegen door tijdelijke aanduidingen voor de tijdnotatie te gebruiken. Beschikbare tijdelijke aanduidingen voor tijdnotatie worden weergegeven bij <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "serialised_log" `[string]`
- Geserialiseerd bestand om alle geblokkeerde toegang pogingen te loggen. Geef een bestandsnaam, of laat leeg om uit te schakelen.

Handige tip: U kunt datum-/tijdinformatie aan de namen van logbestanden toevoegen door tijdelijke aanduidingen voor de tijdnotatie te gebruiken. Beschikbare tijdelijke aanduidingen voor tijdnotatie worden weergegeven bij <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "error_log" `[string]`
- Een bestand voor het vastleggen van gedetecteerde niet-fatale fouten. Geef een bestandsnaam, of laat leeg om uit te schakelen.

Handige tip: U kunt datum-/tijdinformatie aan de namen van logbestanden toevoegen door tijdelijke aanduidingen voor de tijdnotatie te gebruiken. Beschikbare tijdelijke aanduidingen voor tijdnotatie worden weergegeven bij <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "outbound_request_log" `[string]`
- Een bestand voor het loggen van de resultaten van eventuele uitgaande verzoeken. Geef een bestandsnaam, of laat leeg om uit te schakelen.

Handige tip: U kunt datum-/tijdinformatie aan de namen van logbestanden toevoegen door tijdelijke aanduidingen voor de tijdnotatie te gebruiken. Beschikbare tijdelijke aanduidingen voor tijdnotatie worden weergegeven bij <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "report_log" `[string]`
- Een bestand voor het loggen van rapporten die naar externe API's zijn verzonden. Geef een bestandsnaam, of laat leeg om uit te schakelen.

Handige tip: U kunt datum-/tijdinformatie aan de namen van logbestanden toevoegen door tijdelijke aanduidingen voor de tijdnotatie te gebruiken. Beschikbare tijdelijke aanduidingen voor tijdnotatie worden weergegeven bij <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "truncate" `[string]`
- Trunceren logbestanden wanneer ze een bepaalde grootte bereiken? Waarde is de maximale grootte in B/KB/MB/GB/TB dat een logbestand kan groeien tot voordat het wordt getrunceerd. De standaardwaarde van 0KB schakelt truncatie uit (logbestanden kunnen onbepaald groeien). Notitie: Van toepassing op individuele logbestanden! De grootte van de logbestanden wordt niet collectief beschouwd.

##### "log_rotation_limit" `[int]`
- Logrotatie beperkt het aantal logbestanden dat op elk moment zou moeten bestaan. Wanneer nieuwe logbestanden worden gemaakt en het totale aantal logbestanden de opgegeven limiet overschrijdt, wordt de opgegeven actie uitgevoerd. U kunt hier de gewenste limiet opgeven. Een waarde van 0 zal logrotatie uitschakelen.

##### "log_rotation_action" `[string]`
- Logrotatie beperkt het aantal logbestanden dat op elk moment zou moeten bestaan. Wanneer nieuwe logbestanden worden gemaakt en het totale aantal logbestanden de opgegeven limiet overschrijdt, wordt de opgegeven actie uitgevoerd. U kunt hier de gewenste actie opgeven.

```
log_rotation_action
├─Delete ("Verwijder de oudste logbestanden, totdat de limiet niet langer wordt overschreden.")
└─Archive ("Eerst archiveer en verwijder vervolgens de oudste logbestanden, totdat de limiet niet langer wordt overschreden.")
```

##### "log_banned_ips" `[bool]`
- Omvatten geblokkeerde verzoeken van verbannen IP-adressen in de logbestanden? True = Ja [Standaard]; False = Nee.

##### "log_sanitisation" `[bool]`
- Bij gebruik van de frontend logbestanden pagina om loggegevens te bekijken, CIDRAM sanitiseert de loggegevens voordat deze worden weergegeven, om gebruikers te beschermen tegen XSS-aanvallen en andere potentiële bedreigingen die logboekgegevens kunnen bevatten. Standaard echter, gegevens worden niet gesanitiseerd wanneer ze worden opgenomen. Dit is om ervoor te zorgen dat loggegevens nauwkeurig worden bewaard, om eventuele heuristische of forensische analyses te ondersteunen die in de toekomst nodig kunnen zijn. Echter, in het geval dat een gebruiker probeert om loggegevens te lezen met behulp van externe hulpmiddelen, en of die externe tools hun eigen sanitatieproces niet uitvoeren, de gebruiker kan worden blootgesteld aan XSS-aanvallen. Indien nodig kunt u het standaardgedrag wijzigen met behulp van deze configuratierichtlijn. True = Sanitiseren gegevens tijdens het opnemen (gegevens worden minder nauwkeurig bewaard, maar het XSS-risico is lager). False = Sanitiseren gegevens niet tijdens het opnemen (gegevens worden nauwkeuriger bewaard, maar het XSS-risico is hoger) [Standaard].

#### "frontend" (Categorie)
Configuratie voor de frontend.

##### "frontend_log" `[string]`
- Bestand om de frontend login pogingen te loggen. Geef een bestandsnaam, of laat leeg om uit te schakelen.

Handige tip: U kunt datum-/tijdinformatie aan de namen van logbestanden toevoegen door tijdelijke aanduidingen voor de tijdnotatie te gebruiken. Beschikbare tijdelijke aanduidingen voor tijdnotatie worden weergegeven bij <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signatures_update_event_log" `[string]`
- Een bestand om te loggen wanneer signatures worden bijgewerkt via de frontend. Geef een bestandsnaam, of laat leeg om uit te schakelen.

Handige tip: U kunt datum-/tijdinformatie aan de namen van logbestanden toevoegen door tijdelijke aanduidingen voor de tijdnotatie te gebruiken. Beschikbare tijdelijke aanduidingen voor tijdnotatie worden weergegeven bij <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "max_login_attempts" `[int]`
- Maximum aantal frontend-inlogpogingen. Standaard = 5.

##### "theme" `[string]`
- Standaard thema om te gebruiken voor de frontend.

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
└─…Anders
```

##### "magnification" `[float]`
- Lettergrootte vergroting. Standaard = 1.

##### "custom_header" `[string]`
- Ingevoegd als HTML aan het begin van alle frontend pagina's. Dit kan handig zijn als u op al dergelijke pagina's een websitelogo, gepersonaliseerde koptekst, scripts, of iets dergelijks wilt opnemen.

##### "custom_footer" `[string]`
- Ingevoegd als HTML onderaan alle frontend pagina's. Dit kan handig zijn als u op al dergelijke pagina's een juridische kennisgeving, een contactlink, bedrijfsinformatie, of iets dergelijks wilt opnemen.

##### "remotes" `[string]`
- Een lijst met de adressen die door de updater worden gebruikt om metagegevens van componenten op te halen. Dit moet mogelijk worden aangepast bij het upgraden naar een nieuwe hoofdversie, of bij het verkrijgen van een nieuwe bron voor updates, maar onder normale omstandigheden moet dit met rust worden gelaten.

##### "enable_two_factor" `[bool]`
- Deze richtlijn bepaalt of 2FA wordt gebruikt voor frontend-accounts.

#### "signatures" (Categorie)
Configuratie voor signatures, signatuurbestanden, modules, enz.

##### "shorthand" `[string]`
- Controles voor wat te doen met een verzoek wanneer er een positieve overeenkomst is met een signature die de gegeven stenowoorden gebruikt.

```
shorthand
├─Attacks ("Aanvallen")
├─Bogon ("⁰ Bogon IP")
├─Cloud ("Cloud Service")
├─Generic ("Algemeen")
├─Legal ("¹ Wettelijke")
├─Malware ("Malware")
├─Proxy ("² Proxy")
├─Spam ("Spam risico")
├─Banned ("³ Verbannen")
├─BadIP ("³ Ongeldig IP")
├─RL ("³ Tarief beperkt")
└─Other ("⁴ Anders")
```

__0.__ Als uw website nodig toegang via LAN of localhost, blokkeer dit dan niet. Anders u kunt dit blokkeren.

__1.__ Geen van de standaard signatuurbestanden gebruikt dit, maar het wordt niettemin ondersteund voor het geval het voor sommige gebruikers nuttig kan zijn.

__2.__ Als uw gebruikers nodig toegang tot uw website via proxy's, blokkeer dit dan niet. Anders u kunt dit blokkeren.

__3.__ Direct gebruik in signatures wordt niet ondersteund, maar kan in bepaalde omstandigheden op andere manieren worden aangeroepen.

__4.__ Verwijst naar gevallen waarin stenowoorden helemaal niet worden gebruikt, of niet worden herkend door CIDRAM.

__Eén per signature.__ Een signature kan meerdere profielen oproepen, maar kan slechts één stenowoord gebruiken. Het is mogelijk dat meerdere stenowoorden geschikt zijn, maar aangezien er maar één kan worden gebruikt, we streven ernaar altijd alleen de meest geschikte te gebruiken.

__Prioriteit.__ Een geselecteerde optie heeft altijd voorrang op een niet geselecteerde optie. B.v., als er meerdere stenowoorden in het spel zijn, maar slechts één ervan als geblokkeerd is ingesteld, wordt het verzoek nog steeds geblokkeerd.

__Menselijke eindpunten en cloud services.__ Cloud service kan verwijzen naar webhosting providers, server farms, data centers of een aantal andere dingen. Menselijk eindpunt verwijst naar de manier waarop een mens toegang krijgt tot internet, b.v., via een internetprovider. Een netwerk biedt meestal slechts een of het ander, maar kan soms beide bieden. We streven ernaar om potentiële menselijke eindpunten nooit als cloudservices te identificeren. Daarom een cloud service kan worden geïdentificeerd als iets anders als het bereik wordt gedeeld door bekende menselijke eindpunten. Evenzo, we streven ernaar om cloud services, waarvan het bereik niet wordt gedeeld door bekende menselijke eindpunten, altijd als cloud services te identificeren. Daarom een aanvraag dat expliciet als een cloud service wordt geïdentificeerd waarschijnlijk niet deelt het bereik met bekende menselijke eindpunten. Evenzo, een verzoek dat expliciet wordt geïdentificeerd door aanvallen of spam risico waarschijnlijk deelt het bereik. Het internet is echter altijd in beweging, de doeleinden van netwerken veranderen in de loop van de tijd, en bereik worden altijd gekocht of verkocht, dus blijf bewust en waakzaam met betrekking tot valse positieven.

##### "default_tracktime" `[string]`
- De duur dat IP-adressen moeten worden gevolgd. Standaard = 7d0°0′0″ (1 week).

##### "infraction_limit" `[int]`
- Maximum aantal overtredingen een IP mag worden gesteld voordat hij wordt verbannen door IP-tracking. Standaard = 10.

##### "tracking_override" `[bool]`
- Moeten modules worden toegestaan om opties voor tracking te overschrijven? True = Ja [Standaard]; False = Nee.

#### "verification" (Categorie)
Configuratie om te verifiëren waar verzoeken vandaan komen.

##### "search_engines" `[string]`
- Controles voor het verifiëren van verzoeken van zoekmachines.

```
search_engines
├─Amazonbot ("Amazonbot")
├─Applebot ("Applebot")
├─Baidu ("* Baiduspider/百度")
├─Bingbot ("* Bingbot")
├─DuckDuckBot ("* DuckDuckBot")
├─Googlebot ("* Googlebot")
├─MojeekBot ("MojeekBot")
├─Neevabot ("* Neevabot")
├─PetalBot ("* PetalBot")
├─Qwantify ("Qwantify/Bleriot")
├─SeznamBot ("SeznamBot")
├─Sogou ("* Sogou/搜狗")
├─Yahoo ("Yahoo/Slurp")
├─Yandex ("* Yandex/Яндекс")
└─YoudaoBot ("YoudaoBot")
```

__Wat zijn "positieven" en "negatieven"?__ Bij het verifiëren van de identiteit die door een verzoek wordt gepresenteerd, een succesvol resultaat kan worden omschreven als "positief" of "negatief". In het geval dat wordt bevestigd dat de gepresenteerde identiteit de ware identiteit is, deze als "positief" beschreven wordt. In het geval dat wordt bevestigd dat de gepresenteerde identiteit vervalst is, deze als "negatief" beschreven wordt. Een onsuccesvolle uitkomst (b.v., verificatie mislukt, of de juistheid van de gepresenteerde identiteit kan niet worden vastgesteld) wordt echter niet als "positief" of "negatief" beschreven. In plaats daarvan zou een mislukte uitkomst eenvoudigweg als niet-geverifieerd worden beschreven. Als er geen poging wordt gedaan om de identiteit van het verzoek te verifiëren, het verzoek wordt eveneens als niet-geverifieerd beschreven. De termen hebben alleen zin in de context waarin de identiteit van het verzoek wordt herkend, en dus waar verificatie mogelijk is. In gevallen waarin de gepresenteerde identiteit niet overeenkomt met de bovenstaande opties, of waar geen identiteit wordt gepresenteerd, worden de bovenstaande opties irrelevant.

__Wat zijn "enkele-treffer bypasses"?__ In sommige gevallen kan een positief-geverifieerd verzoek nog steeds worden geblokkeerd als gevolg van de signatuurbestanden, modules, of andere voorwaarden van het verzoek, en bypasses kunnen nodig zijn om valse positieven te voorkomen. In het geval dat een bypass bedoeld is om precies één overtreding af te handelen, niet meer en niet minder, dergelijke een bypass zou kunnen worden omschreven als een "enkele-treffer bypass".

* Deze optie heeft een bijbehorende bypass onder `bypasses➡used`. Ongeacht of het selectievakje om te proberen deze optie te verifiëren is ingeschakeld, het wordt aanbevolen om ervoor te zorgen dat het selectievakje voor de corresponderende bypass hetzelfde is.

##### "social_media" `[string]`
- Controles voor het verifiëren van verzoeken van sociale media platforms.

```
social_media
├─Embedly ("* Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("* Pinterest")
├─Snapchat ("* Snapchat")
└─Twitterbot ("*!! Twitterbot")
```

__Wat zijn "positieven" en "negatieven"?__ Bij het verifiëren van de identiteit die door een verzoek wordt gepresenteerd, een succesvol resultaat kan worden omschreven als "positief" of "negatief". In het geval dat wordt bevestigd dat de gepresenteerde identiteit de ware identiteit is, deze als "positief" beschreven wordt. In het geval dat wordt bevestigd dat de gepresenteerde identiteit vervalst is, deze als "negatief" beschreven wordt. Een onsuccesvolle uitkomst (b.v., verificatie mislukt, of de juistheid van de gepresenteerde identiteit kan niet worden vastgesteld) wordt echter niet als "positief" of "negatief" beschreven. In plaats daarvan zou een mislukte uitkomst eenvoudigweg als niet-geverifieerd worden beschreven. Als er geen poging wordt gedaan om de identiteit van het verzoek te verifiëren, het verzoek wordt eveneens als niet-geverifieerd beschreven. De termen hebben alleen zin in de context waarin de identiteit van het verzoek wordt herkend, en dus waar verificatie mogelijk is. In gevallen waarin de gepresenteerde identiteit niet overeenkomt met de bovenstaande opties, of waar geen identiteit wordt gepresenteerd, worden de bovenstaande opties irrelevant.

__Wat zijn "enkele-treffer bypasses"?__ In sommige gevallen kan een positief-geverifieerd verzoek nog steeds worden geblokkeerd als gevolg van de signatuurbestanden, modules, of andere voorwaarden van het verzoek, en bypasses kunnen nodig zijn om valse positieven te voorkomen. In het geval dat een bypass bedoeld is om precies één overtreding af te handelen, niet meer en niet minder, dergelijke een bypass zou kunnen worden omschreven als een "enkele-treffer bypass".

* Deze optie heeft een bijbehorende bypass onder `bypasses➡used`. Ongeacht of het selectievakje om te proberen deze optie te verifiëren is ingeschakeld, het wordt aanbevolen om ervoor te zorgen dat het selectievakje voor de corresponderende bypass hetzelfde is.

** Vereist ASN-opzoekfunctionaliteit (b.v., via de IP-API-module of BGPView-module).

*!! Grote kans op het veroorzaken van valse positieven vanwege iMessage.

##### "other" `[string]`
- Controles voor het verifiëren van andere soorten verzoeken waar mogelijk.

```
other
├─AdSense ("AdSense")
├─AmazonAdBot ("* AmazonAdBot")
├─ChatGPT-User ("!! ChatGPT-User")
├─GPTBot ("!! GPTBot")
└─Grapeshot ("* Oracle Data Cloud Crawler (Grapeshot)")
```

__Wat zijn "positieven" en "negatieven"?__ Bij het verifiëren van de identiteit die door een verzoek wordt gepresenteerd, een succesvol resultaat kan worden omschreven als "positief" of "negatief". In het geval dat wordt bevestigd dat de gepresenteerde identiteit de ware identiteit is, deze als "positief" beschreven wordt. In het geval dat wordt bevestigd dat de gepresenteerde identiteit vervalst is, deze als "negatief" beschreven wordt. Een onsuccesvolle uitkomst (b.v., verificatie mislukt, of de juistheid van de gepresenteerde identiteit kan niet worden vastgesteld) wordt echter niet als "positief" of "negatief" beschreven. In plaats daarvan zou een mislukte uitkomst eenvoudigweg als niet-geverifieerd worden beschreven. Als er geen poging wordt gedaan om de identiteit van het verzoek te verifiëren, het verzoek wordt eveneens als niet-geverifieerd beschreven. De termen hebben alleen zin in de context waarin de identiteit van het verzoek wordt herkend, en dus waar verificatie mogelijk is. In gevallen waarin de gepresenteerde identiteit niet overeenkomt met de bovenstaande opties, of waar geen identiteit wordt gepresenteerd, worden de bovenstaande opties irrelevant.

__Wat zijn "enkele-treffer bypasses"?__ In sommige gevallen kan een positief-geverifieerd verzoek nog steeds worden geblokkeerd als gevolg van de signatuurbestanden, modules, of andere voorwaarden van het verzoek, en bypasses kunnen nodig zijn om valse positieven te voorkomen. In het geval dat een bypass bedoeld is om precies één overtreding af te handelen, niet meer en niet minder, dergelijke een bypass zou kunnen worden omschreven als een "enkele-treffer bypass".

* Deze optie heeft een bijbehorende bypass onder `bypasses➡used`. Ongeacht of het selectievakje om te proberen deze optie te verifiëren is ingeschakeld, het wordt aanbevolen om ervoor te zorgen dat het selectievakje voor de corresponderende bypass hetzelfde is.

!! De meeste gebruikers zullen waarschijnlijk willen dat dit wordt geblokkeerd, ongeacht of het echt of vervalst is. Dat kan worden bereikt door "proberen te verifiëren" niet te selecteren en "niet-geverifieerde verzoeken blokkeren" te selecteren. Omdat sommige gebruikers dergelijke verzoeken echter willen kunnen verifiëren (om negatieven te blokkeren en positieven toe te staan), in plaats van dergelijke verzoeken via modules te blokkeren, worden hier opties geboden voor het afhandelen van dergelijke verzoeken.

##### "adjust" `[string]`
- Controles om andere functionaliteit aan te passen in de context van verificatie.

```
adjust
├─Negatives ("Geblokkeerde negatieven")
└─NonVerified ("Geblokkeerde niet-geverifieerde")
```

#### "recaptcha" (Categorie)
Configuratie voor ReCaptcha (biedt een manier voor mensen om toegang te krijgen wanneer ze worden geblokkeerd).

##### "usemode" `[int]`
- Wanneer moet de CAPTCHA worden aangeboden? Opmerking: Op de witte lijst geplaatste of geverifieerde en niet-geblokkeerde verzoeken hoeven nooit een CAPTCHA in te vullen. Let ook op: CAPTCHA's kunnen een nuttige, extra beschermingslaag bieden tegen bots en verschillende soorten kwaadwillende geautomatiseerde verzoeken, maar bieden geen enkele bescherming tegen kwaadwillende mensen.

```
usemode
├─0 (Nooit !!!)
├─1 (Alleen wanneer geblokkeerd, binnen de signatures limiet, en niet verbannen.)
├─2 (Alleen wanneer geblokkeerd, speciaal gemarkeerd voor gebruik, binnen de signatures limiet, en niet verbannen.)
├─3 (Alleen binnen de signatures limiet en niet verbannen (ongeacht of deze is geblokkeerd).)
├─4 (Alleen wanneer niet geblokkeerd.)
├─5 (Alleen wanneer niet geblokkeerd, of wanneer speciaal gemarkeerd voor gebruik, binnen de signatures limiet, en niet verbannen.)
└─6 (Alleen wanneer niet geblokkeerd, bij verzoek van gevoelige pagina's.)
```

##### "lockip" `[bool]`
- Binden CAPTCHA om IP's?

##### "lockuser" `[bool]`
- Binden CAPTCHA om gebruikers?

##### "sitekey" `[string]`
- Deze waarde is te vinden in het dashboard voor uw CAPTCHA-service.

Zie ook:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "secret" `[string]`
- Deze waarde is te vinden in het dashboard voor uw CAPTCHA-service.

Zie ook:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "expiry" `[float]`
- Aantal uren om CAPTCHA instanties herinneren. Standaard = 720 (1 maand).

##### "recaptcha_log" `[string]`
- Log alle CAPTCHA pogingen? Zo ja, geef de naam te gebruiken voor het logbestand. Zo nee, laat u deze variabele leeg.

Handige tip: U kunt datum-/tijdinformatie aan de namen van logbestanden toevoegen door tijdelijke aanduidingen voor de tijdnotatie te gebruiken. Beschikbare tijdelijke aanduidingen voor tijdnotatie worden weergegeven bij <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signature_limit" `[int]`
- Maximaal aantal toegestane signatures voordat een CAPTCHA-aanbieding wordt ingetrokken. Standaard = 1.

##### "api" `[string]`
- Welke API gebruiken?

```
api
├─V2 ("V2 (Selectievakje)")
└─Invisible ("V2 (Onzichtbaar)")
```

##### "show_cookie_warning" `[bool]`
- Cookiewaarschuwing weergeven? True = Ja [Standaard]; False = Nee.

##### "show_api_message" `[bool]`
- API-bericht weergeven? True = Ja [Standaard]; False = Nee.

##### "nonblocked_status_code" `[int]`
- Welke statuscode moet worden gebruikt bij het weergeven van CAPTCHA's voor niet-geblokkeerde verzoeken?

```
nonblocked_status_code
├─200 (200 OK): Minst robuust, maar meest gebruiksvriendelijk. Geautomatiseerde verzoeken
│ zullen dit antwoord hoogstwaarschijnlijk interpreteren als een indicatie dat
│ het verzoek was succesvol.
├─403 (403 Forbidden (Verboden)): Robuuster, maar minder gebruiksvriendelijk. Aanbevolen voor de meeste
│ algemene omstandigheden.
├─418 (418 I'm a teapot (Ik ben een theepot)): Verwijst naar een 1-aprilgrap (<a href="https://tools.ietf.org/html/rfc2324"
│ dir="ltr" hreflang="en-US" rel="noopener noreferrer external">RFC 2324</a>).
│ Het is zeer onwaarschijnlijk dat deze door een client, bot, browser, of
│ anderszins wordt begrepen. Geleverd voor amusement en gemak, maar over het
│ algemeen niet aanbevolen.
├─429 (429 Too Many Requests (Te veel verzoeken)): Aanbevolen voor de tarieflimiet, bij het omgaan met DDoS-aanvallen, en voor
│ het voorkomen van overstromingen. Niet aanbevolen in andere contexten.
└─451 (451 Unavailable For Legal Reasons (Om juridische redenen onbeschikbaar)): Aanbevolen bij blokkering voornamelijk om juridische redenen. Niet
  aanbevolen in andere contexten.
```

#### "hcaptcha" (Categorie)
Configuratie voor HCaptcha (biedt een manier voor mensen om toegang te krijgen wanneer ze worden geblokkeerd).

##### "usemode" `[int]`
- Wanneer moet de CAPTCHA worden aangeboden? Opmerking: Op de witte lijst geplaatste of geverifieerde en niet-geblokkeerde verzoeken hoeven nooit een CAPTCHA in te vullen. Let ook op: CAPTCHA's kunnen een nuttige, extra beschermingslaag bieden tegen bots en verschillende soorten kwaadwillende geautomatiseerde verzoeken, maar bieden geen enkele bescherming tegen kwaadwillende mensen.

```
usemode
├─0 (Nooit !!!)
├─1 (Alleen wanneer geblokkeerd, binnen de signatures limiet, en niet verbannen.)
├─2 (Alleen wanneer geblokkeerd, speciaal gemarkeerd voor gebruik, binnen de signatures limiet, en niet verbannen.)
├─3 (Alleen binnen de signatures limiet en niet verbannen (ongeacht of deze is geblokkeerd).)
├─4 (Alleen wanneer niet geblokkeerd.)
├─5 (Alleen wanneer niet geblokkeerd, of wanneer speciaal gemarkeerd voor gebruik, binnen de signatures limiet, en niet verbannen.)
└─6 (Alleen wanneer niet geblokkeerd, bij verzoek van gevoelige pagina's.)
```

##### "lockip" `[bool]`
- Binden CAPTCHA om IP's?

##### "lockuser" `[bool]`
- Binden CAPTCHA om gebruikers?

##### "sitekey" `[string]`
- Deze waarde is te vinden in het dashboard voor uw CAPTCHA-service.

Zie ook:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "secret" `[string]`
- Deze waarde is te vinden in het dashboard voor uw CAPTCHA-service.

Zie ook:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "expiry" `[float]`
- Aantal uren om CAPTCHA instanties herinneren. Standaard = 720 (1 maand).

##### "hcaptcha_log" `[string]`
- Log alle CAPTCHA pogingen? Zo ja, geef de naam te gebruiken voor het logbestand. Zo nee, laat u deze variabele leeg.

Handige tip: U kunt datum-/tijdinformatie aan de namen van logbestanden toevoegen door tijdelijke aanduidingen voor de tijdnotatie te gebruiken. Beschikbare tijdelijke aanduidingen voor tijdnotatie worden weergegeven bij <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signature_limit" `[int]`
- Maximaal aantal toegestane signatures voordat een CAPTCHA-aanbieding wordt ingetrokken. Standaard = 1.

##### "api" `[string]`
- Welke API gebruiken?

```
api
├─V1 ("V1")
└─Invisible ("V1 (Onzichtbaar)")
```

##### "show_cookie_warning" `[bool]`
- Cookiewaarschuwing weergeven? True = Ja [Standaard]; False = Nee.

##### "show_api_message" `[bool]`
- API-bericht weergeven? True = Ja [Standaard]; False = Nee.

##### "nonblocked_status_code" `[int]`
- Welke statuscode moet worden gebruikt bij het weergeven van CAPTCHA's voor niet-geblokkeerde verzoeken?

```
nonblocked_status_code
├─200 (200 OK): Minst robuust, maar meest gebruiksvriendelijk. Geautomatiseerde verzoeken
│ zullen dit antwoord hoogstwaarschijnlijk interpreteren als een indicatie dat
│ het verzoek was succesvol.
├─403 (403 Forbidden (Verboden)): Robuuster, maar minder gebruiksvriendelijk. Aanbevolen voor de meeste
│ algemene omstandigheden.
├─418 (418 I'm a teapot (Ik ben een theepot)): Verwijst naar een 1-aprilgrap (<a href="https://tools.ietf.org/html/rfc2324"
│ dir="ltr" hreflang="en-US" rel="noopener noreferrer external">RFC 2324</a>).
│ Het is zeer onwaarschijnlijk dat deze door een client, bot, browser, of
│ anderszins wordt begrepen. Geleverd voor amusement en gemak, maar over het
│ algemeen niet aanbevolen.
├─429 (429 Too Many Requests (Te veel verzoeken)): Aanbevolen voor de tarieflimiet, bij het omgaan met DDoS-aanvallen, en voor
│ het voorkomen van overstromingen. Niet aanbevolen in andere contexten.
└─451 (451 Unavailable For Legal Reasons (Om juridische redenen onbeschikbaar)): Aanbevolen bij blokkering voornamelijk om juridische redenen. Niet
  aanbevolen in andere contexten.
```

#### "legal" (Categorie)
Configuratie voor wettelijke vereisten.

##### "pseudonymise_ip_addresses" `[bool]`
- Pseudonimiseren de IP-adressen bij het schrijven van logbestanden? True = Ja [Standaard]; False = Nee.

##### "privacy_policy" `[string]`
- Het adres van een relevant privacybeleid dat moet worden weergegeven in de voettekst van eventuele gegenereerde pagina's. Geef een URL, of laat leeg om uit te schakelen.

#### "template_data" (Categorie)
Configuratie voor sjablonen en thema's.

##### "theme" `[string]`
- Standaard thema om te gebruiken voor CIDRAM.

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
└─…Anders
```

##### "magnification" `[float]`
- Lettergrootte vergroting. Standaard = 1.

##### "css_url" `[string]`
- CSS-bestand URL voor aangepaste thema's.

##### "block_event_title" `[string]`
- De paginatitel die moet worden weergegeven voor blokgebeurtenissen.

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("Toegang geweigerd!")
└─…Anders
```

##### "captcha_title" `[string]`
- De paginatitel die moet worden weergegeven voor CAPTCHA-verzoeken.

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…Anders
```

##### "custom_header" `[string]`
- Ingevoegd als HTML aan het begin van alle "toegang geweigerd" pagina's. Dit kan handig zijn als u op al dergelijke pagina's een websitelogo, gepersonaliseerde koptekst, scripts, of iets dergelijks wilt opnemen.

##### "custom_footer" `[string]`
- Ingevoegd als HTML onderaan alle "toegang geweigerd" pagina's. Dit kan handig zijn als u op al dergelijke pagina's een juridische kennisgeving, een contactlink, bedrijfsinformatie, of iets dergelijks wilt opnemen.

#### "rate_limiting" (Categorie)
Configuratie voor tarieflimiet (niet aanbevolen voor algemeen gebruik).

##### "max_bandwidth" `[string]`
- De maximale hoeveelheid toegestane bandbreedte binnen de toeslagperiode voordat tarieflimiet voor toekomstige verzoeken wordt ingeschakeld. Een waarde van 0 schakelt dit type tarieflimiet uit. Standaard = 0KB.

##### "max_requests" `[int]`
- Het maximale aantal toegestane verzoeken binnen de toeslagperiode voordat de tarieflimiet voor toekomstige verzoeken wordt ingeschakeld. Een waarde van 0 schakelt dit type tarieflimiet uit. Standaard = 0.

##### "precision_ipv4" `[int]`
- De precisie om te gebruiken bij het monitoren op het gebruik van IPv4. Waarde weerspiegelt de CIDR-blokgrootte. Stel in op 32 voor de beste precisie. Standaard = 32.

##### "precision_ipv6" `[int]`
- De precisie om te gebruiken bij het monitoren op het gebruik van IPv6. Waarde weerspiegelt de CIDR-blokgrootte. Stel in op 128 voor de beste precisie. Standaard = 128.

##### "allowance_period" `[string]`
- De duur om het gebruik bij te controleren. Standaard = 0°0′0″.

##### "exceptions" `[string]`
- Excepties (d.w.z., verzoeken die moet niet worden beperkt). Alleen relevant wanneer tarieflimiet is ingeschakeld.

```
exceptions
├─Whitelisted ("Verzoeken gemarkeerd als op de witte lijst")
├─Verified ("Geverifieerde verzoeken van zoekmachines en sociale media")
└─FE ("Verzoeken aan de front-end van CIDRAM")
```

##### "segregate" `[bool]`
- Moeten quota voor verschillende domeinen en hosts worden gescheiden of gedeeld? True = Quota zullen worden gescheiden. False = Quota zullen worden gedeeld [Standaard].

#### "supplementary_cache_options" (Categorie)
Aanvullende cache-opties. Opmerking: Als u deze waarden wijzigt, mogelijk bent u uitgelogd.

##### "prefix" `[string]`
- De hier opgegeven waarde wordt toegevoegd aan alle cache-invoersleutels. Standaard = "CIDRAM_". Als er meerdere installaties op dezelfde server staan, dit kan handig zijn om hun caches gescheiden van elkaar te houden.

##### "enable_apcu" `[bool]`
- Dit geeft aan of APCu moet worden gebruikt voor caching. Standaard = True.

##### "enable_memcached" `[bool]`
- Dit geeft aan of Memcached moet worden gebruikt voor caching. Standaard = False.

##### "enable_redis" `[bool]`
- Dit geeft aan of Redis moet worden gebruikt voor caching. Standaard = False.

##### "enable_pdo" `[bool]`
- Dit geeft aan of PDO moet worden gebruikt voor caching. Standaard = False.

##### "memcached_host" `[string]`
- Memcached hostwaarde. Standaard = "localhost".

##### "memcached_port" `[int]`
- Memcached poortwaarde. Standaard = "11211".

##### "redis_host" `[string]`
- Redis hostwaarde. Standaard = "localhost".

##### "redis_port" `[int]`
- Redis poortwaarde. Standaard = "6379".

##### "redis_timeout" `[float]`
- Redis timeoutwaarde. Standaard = "2.5".

##### "redis_database_number" `[int]`
- Redis-databasenummer. Standaard = 0. Opmerking: Kan geen andere waarden dan 0 gebruiken met Redis Cluster.

##### "pdo_dsn" `[string]`
- PDO DSN-waarde. Standaard = "mysql:dbname=cidram;host=localhost;port=3306".

__FAQ.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.nl.md#user-content-HOW_TO_USE_PDO" hreflang="nl-NL">Wat is een "PDO DSN"? Hoe kan ik PDO gebruiken met CIDRAM?</a>*

##### "pdo_username" `[string]`
- PDO gebruikersnaam.

##### "pdo_password" `[string]`
- PDO wachtwoord.

#### "bypasses" (Categorie)
Configuratie voor de standaard bypasses voor signatures.

##### "used" `[string]`
- Welke bypasses moeten worden gebruikt?

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
├─Grapeshot ("Grapeshot")
├─Jetpack ("Jetpack")
├─Neevabot ("Neevabot")
├─PetalBot ("PetalBot")
├─Pinterest ("Pinterest")
├─Redditbot ("Redditbot")
├─Snapchat ("Snapchat")
├─Sogou ("Sogou/搜狗")
└─Yandex ("Yandex/Яндекс")
```

---


### 6. <a name="SECTION6"></a>SIGNATURE FORMAAT

*Zie ook:*
- *[Wat is een "signature"?](#user-content-WHAT_IS_A_SIGNATURE)*

#### 6.0 BASICS (VOOR SIGNATUURBESTANDEN)

Alle IPv4 signatures volgt het formaat: `xxx.xxx.xxx.xxx/yy [Function] [Param]`.
- `xxx.xxx.xxx.xxx` vertegenwoordigt het begin van het CIDR blok (de octetten van de eerste IP-adres in het blok).
- `yy` vertegenwoordigt het CIDR blokgrootte [1-32].
- `[Function]` instrueert het script wat te doen met de signature (hoe de signature moet worden beschouwd).
- `[Param]` vertegenwoordigt alle aanvullende informatie dat kan worden verlangd door `[Function]`.

Alle IPv6 signatures volgt het formaat: `xxxx:xxxx:xxxx:xxxx::xxxx/yy [Function] [Param]`.
- `xxxx:xxxx:xxxx:xxxx::xxxx` vertegenwoordigt het begin van het CIDR blok (de octetten van de eerste IP-adres in het blok). Compleet notatie en verkorte notatie zijn beide aanvaardbaar (en ieder moet volg de juiste en relevante normen van IPv6-notatie, maar met één uitzondering: een IPv6-adres kan nooit beginnen met een afkorting wanneer het wordt gebruikt in een signature voor dit script, vanwege de manier waarop CIDR's door het script zijn gereconstrueerd; Bijvoorbeeld, `::1/128` moet worden uitgedrukt, bij gebruik in een signature, als `0::1/128`, en `::0/128` uitgedrukt als `0::/128`).
- `yy` vertegenwoordigt het CIDR blokgrootte [1-128].
- `[Function]` instrueert het script wat te doen met de signature (hoe de signature moet worden beschouwd).
- `[Param]` vertegenwoordigt alle aanvullende informatie dat kan worden verlangd door `[Function]`.

De signatuurbestanden voor CIDRAM MOET gebruiken Unix-stijl regeleinden (`%0A`, or `\n`)! Andere soorten/stijlen van regeleinden (b.v., Windows `%0D%0A` of `\r\n` regeleinden, Mac `%0D` of `\r` regeleinden, enz) KAN worden gebruikt, maar zijn NIET voorkeur. Non-Unix-stijl regeleinden wordt genormaliseerd naar Unix-stijl regeleinden door het script.

Nauwkeurig en correct CIDR-notatie is vereist, anders zal het script NIET de signatures herkennen. Tevens, alle CIDR signatures van dit script MOET beginnen met een IP-adres waarvan het IP-nummer kan gelijkmatig in het blok divisie vertegenwoordigd door haar CIDR blokgrootte verdelen (b.v., als u wilde alle IP-adressen van `10.128.0.0` naar `11.127.255.255` te blokkeren, `10.128.0.0/8` zou door het script NIET worden herkend, maar `10.128.0.0/9` en `11.0.0.0/9` in combinatie, ZOU door het script worden herkend).

Alles wat in de signatuurbestanden niet herkend als een signature noch als signature-gerelateerde syntaxis door het script worden GENEGEERD, daarom dit betekent dat om veilig alle niet-signature gegevens die u wilt in de signatuurbestanden u kunnen zetten zonder verbreking van de signatuurbestanden of de script. Reacties zijn in de signatuurbestanden aanvaardbare, en geen speciale opmaak of formaat is vereist voor hen. Shell-stijl hashing voor commentaar heeft de voorkeur, maar is niet afgedwongen; Functioneel, het maakt geen verschil voor het script ongeacht of u kiest voor Shell-stijl hashing om commentaar te gebruiken, maar gebruik van Shell-stijl hashing helpt IDE's en platte tekst editors om correct te markeren de verschillende delen van de signatuurbestanden (en dus, Shell-stijl hashing kan helpen als een visueel hulpmiddel tijdens het bewerken).

Mogelijke waarden van `[Function]` zijn als volgt:
- Run
- Whitelist
- Greylist
- Deny

Als "Run" wordt gebruikt, als de signature wordt getriggerd, het script zal proberen (gebruiken een `require_once` statement) om een externe PHP-script uit te voeren, gespecificeerd door de `[Param]` waarde (de werkmap moet worden de "/vault/" map van het script).

Voorbeeld: `127.0.0.0/8 Run example.php`

Dit kan handig zijn als u wilt, voor enige specifieke IP's en/of CIDR's, om specifieke PHP-code uit te voeren.

Als "Whitelist" wordt gebruikt, als de signature wordt getriggerd, het script zal alle detecties resetten (als er is al enige detecties) en breek de testfunctie. `[Param]` worden genegeerd. Deze functie werkt als een whitelist, om te voorkomen dat bepaalde IP-adressen en/of CIDR's van wordt gedetecteerd.

Voorbeeld: `127.0.0.1/32 Whitelist`

Als "Greylist" wordt gebruikt, als de signature wordt getriggerd, het script zal alle detecties resetten (als er is al enige detecties) en doorgaan naar de volgende signatuurbestand te gaan met verwerken. `[Param]` worden genegeerd.

Voorbeeld: `127.0.0.1/32 Greylist`

Als "Deny" wordt gebruikt, als de signature wordt getriggerd, veronderstelling dat er worden geen whitelist-signature getriggerd voor het opgegeven IP-adres en/of opgegeven CIDR, toegang tot de beveiligde pagina wordt ontzegd. "Deny" is wat u wilt gebruiken om een IP-adres en/of CIDR range te daadwerkelijk blokkeren. Wanneer enige signatures zijn getriggerd er dat gebruik "Deny", de "Toegang Geweigerd" pagina van het script zal worden gegenereerd en het verzoek naar de beveiligde pagina wordt gedood.

De `[Param]` waarde geaccepteerd door "Deny" zal worden parsed aan de "Toegang Geweigerd" pagina-uitgang, geleverd aan de klant/gebruiker als de genoemde reden voor hun toegang tot de gevraagde pagina worden geweigerd. Het kan een korte en eenvoudige zin zijn, uit te leggen waarom u hebt gekozen om ze te blokkeren (iets moeten volstaan, zelfs een simpele "Ik wil je niet op mijn website"), of een van het handjevol korte woorden geleverd door het script, dat als gebruikt, wordt vervangen door het script met een voorbereide toelichting waarom de klant/gebruiker is geblokkeerd.

De voorbereide toelichtingen hebben L10N-ondersteuning en kan worden vertaald door het script op basis van de taal die u opgeeft naar de `lang` richtlijn van het script-configuratie. Tevens, u kunt het script instrueren om "Deny"-signatures te negeren op basis van hun `[Param]` waarde (als ze gebruik maken van deze korte woorden) via de richtlijnen gespecificeerd door het script-configuratie (elk kort woord heeft een overeenkomstige richtlijn te verwerken overeenkomende signatures of te negeren hen). `[Param]` waarden dat niet gebruiken deze korte woorden, echter, hebben geen L10N-ondersteuning en daarom zal NIET worden vertaald door het script, en tevens, en zijn niet direct controleerbaar door het script-configuratie.

De beschikbare korte woorden zijn:
- Attacks
- Bogon
- Cloud
- Generic
- Legal
- Malware
- Proxy
- Spam

#### 6.1 ETIKETTEN

##### 6.1.0 SECTIE ETIKETTEN

Als u wilt uw aangepaste signatures te splitsen in afzonderlijke secties, u kunt deze individuele secties te identificeren om het script door toevoeging van een "sectie etiket" onmiddellijk na de signatures van elke sectie, samen met de naam van uw signature-sectie (zie het onderstaande voorbeeld).

```
# Sectie 1.
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: Sectie 1
```

Om sectie etiketteren te breken en zodat de etiketten zijn niet onjuist geïdentificeerd met signatuursecties uit eerder in de signatuurbestanden, gewoon ervoor zorgen dat er ten minste twee opeenvolgende regeleinden tussen uw etiket en uw eerdere signatuursecties. Een ongeëtiketteerd signatures wordt standaard om "IPv4" of "IPv6" (afhankelijk van welke soorten signatures worden getriggerd).

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: Sectie 1
```

In het bovenstaande voorbeeld `1.2.3.4/32` en `2.3.4.5/32` zal worden geëtiketteerd als "IPv4", terwijl `4.5.6.7/32` en `5.6.7.8/32` zal worden geëtiketteerd als "Sectie 1".

Dezelfde logica kan ook worden toegepast voor het scheiden van andere typen etiketten.

In het bijzonder kunnen sectie etiketten erg handig zijn voor foutopsporing wanneer valse positieven optreden, door een eenvoudige manier te voorzien om de exacte oorzaak van het probleem te vinden, en kunnen erg handig zijn om logbestanditems te filteren bij het bekijken van logbestanden via de frontend logbestanden pagina (sectienamen kunnen worden aangeklikt via de frontend logs pagina en kunnen worden gebruikt als filtercriteria). Als sectie etiketten zijn weggelaten voor bepaalde signatures, wanneer de signatures worden getriggerd, gebruikt CIDRAM de naam van het signatuurbestand samen met het type IP-adres geblokkeerd (IPv4 of IPv6) als een fallback, en dus zijn sectie etiketten volledig optioneel. In sommige gevallen kunnen ze echter worden aanbevolen, zoals wanneer signatuurbestanden vaag worden genoemd of wanneer het anders moeilijk zou zijn om de bron van de signatures duidelijk te identificeren waardoor een verzoek wordt geblokkeerd.

##### 6.1.1 VERVALTIJD ETIKETTEN

Als u wilt signatures te vervallen na verloop van tijd, op soortgelijke wijze als sectie etiketten, u kan een "vervaltijd etiket" gebruikt om aan te geven wanneer signatures moet niet meer geldig. Vervaltijd etiketten gebruiken het formaat "JJJJ.MM.DD" (zie het onderstaande voorbeeld).

```
# Sectie 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

Verlopen signatures zullen nooit worden getriggerd bij een aanvraag, wat er ook gebeurt.

##### 6.1.2 HERKOMST ETIKETTEN

Als u het land van herkomst voor een bepaalde signature wilt opgeven, kunt u dit doen met behulp van een "herkomst etiket". Een herkomst etiket accepteert een "[ISO 3166-1 2-letterig](https://nl.wikipedia.org/wiki/ISO_3166-1)"-code die overeenkomt met het land van herkomst voor de signatures waarop deze van toepassing is. Deze codes moeten in hoofd-letters worden geschreven (kleine-letters worden niet correct weergegeven). Wanneer een herkomst etiket wordt gebruikt, wordt deze toegevoegd aan het logveld "Waarom Geblokkeerd" voor alle verzoeken die zijn geblokkeerd als gevolg van de signatures waarop de etiket is toegepast.

Als de optionele component "flags CSS" is geïnstalleerd, wanneer u de logbestanden bekijkt via de frontend, wordt informatie dat toegevoegd door herkomst etiketten vervangen met de vlag van het land dat overeenkomt met die informatie. Deze informatie, in ruwe vorm of als de vlag van een land, kan worden aangeklikt, en wanneer erop wordt geklikt, filteren log-invoeren door middel van andere, soortgelijk identificerende log-invoeren (waardoor effectief degenen die de logs pagina openen te filteren op basis van land van herkomst).

Notitie: Technisch gezien is dit geen vorm van geolocatie, vanwege het feit dat het niet gaat om het opzoeken van specifieke informatie met betrekking tot inkomende IP's, maar in plaats stelt ons in staat om expliciet een land van herkomst opgeven voor verzoeken die worden geblokkeerd door specifieke signatures. Meerdere herkomst etiketten zijn toegestaan binnen dezelfde signature sectie.

Hypothetisch voorbeeld:

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

Alle etiketten kunnen samen worden gebruikt en alle etiketten zijn optioneel (zie het onderstaande voorbeeld).

```
# Voorbeeld Sectie.
1.2.3.4/32 Deny Generic
Origin: US
Tag: Voorbeeld Sectie.
Expires: 2016.12.31
```

##### 6.1.3 UITSTEL ETIKETTEN

Wanneer grote aantallen signatuurbestanden zijn geïnstalleerd en actief worden gebruikt, installaties kunnen behoorlijk ingewikkeld worden, en er kunnen signatures zijn die elkaar overlappen. In deze gevallen om te voorkomen dat meerdere, overlappende signatures worden geactiveerd tijdens blokgebeurtenissen, uitstel etiketten kunnen worden gebruikt om specifieke signature secties uit te stellen in gevallen waarin een ander specifiek signatuurbestand is geïnstalleerd en actief wordt gebruikt. Dit kan handig zijn in gevallen waarin sommige signatures vaker worden bijgewerkt dan andere, om de minder vaak bijgewerkte signatures uit te stellen ten gunste van de meer frequent bijgewerkte signatures.

Uitstel etiketten worden op dezelfde manier gebruikt als andere typen etiketten. De waarde van de etiket moet overeenkomen met een geïnstalleerd en actief gebruikt signatuurbestand dat moet worden uitgesteld.

Voorbeeld:

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 6.1.4 PROFIEL ETIKETTEN

Profiel etiketten bieden een middel om aanvullende informatie op de IP-testpagina weer te geven, en kunnen worden gebruikt door modules en aanvullende regels voor complexer gedrag en nauwkeurigere besluitvorming.

Profiel etiketten worden op dezelfde manier gebruikt als andere soorten etiketten. De waarden van profiel etiketten kunnen worden gebruikt als voorwaarde voor modules en aanvullende regels. Profiel etiketten kunnen meerdere waarden bieden door deze waarden te scheiden met een puntkomma. De eindgebruiker ziet nooit de waarden van profiel etiketten.

Voorbeeld:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 6.2 YAML

##### 6.2.0 YAML BASICS

Een vereenvoudigde vorm van YAML markup kan worden gebruikt in signatuurbestanden voor het bepalen van gedragingen en specifieke instellingen voor afzonderlijke signatuursecties. Dit kan handig zijn als u de waarde van uw configuratie richtlijnen willen afwijken op basis van individuele signatures en signatuursecties (bijvoorbeeld; als u wilt om een e-mailadres te leveren voor support tickets voor alle gebruikers geblokkeerd door een bepaalde signature, maar wil niet om een e-mailadres te leveren voor support tickets voor de gebruikers geblokkeerd door andere signatures; als u wilt een specifieke signatures te leiden tot een pagina redirect; als u wilt een signature-sectie voor gebruik met reCAPTCHA/hCAPTCHA te markeren; als u wilt om geblokkeerde toegang pogingen te loggen in afzonderlijke bestanden op basis van individuele signatures en/of signatuursecties).

Het gebruik van YAML markup in de signatuurbestanden is volledig optioneel (d.w.z., u kan het gebruiken als u wenst te doen, maar u bent niet verplicht om dit te doen), en is in staat om de meeste (maar niet alle) configuratie richtlijnen hefboomeffect.

Notitie: YAML markup implementatie in CIDRAM is zeer simplistisch en zeer beperkt; Het is bedoeld om de specifieke eisen van CIDRAM te voldoen op een manier dat heeft de vertrouwdheid van YAML markup, maar noch volgt noch voldoet aan de officiële specificaties (en zal daarom niet zich op dezelfde wijze als grondiger implementaties elders, en is misschien niet geschikt voor alle andere projecten elders).

In CIDRAM, YAML markup segmenten worden geïdentificeerd aan het script door drie streepjes ("---"), en eindigen naast hun bevattende signatuursecties door dubbel-regeleinden. Een typische YAML markup segment binnen een signature-sectie bestaat uit drie streepjes op een lijn onmiddellijk na de lijst van CIDR's en elke etiketten, gevolgd door een tweedimensionale lijst van sleutel-waarde paren (eerste dimensie, configuratie richtlijn categorieën; tweede dimensie, configuratie richtlijnen) voor welke configuratie richtlijnen moeten worden gewijzigd (en om welke waarden) wanneer een signature in die signature-sectie wordt getriggerd (zie de onderstaande voorbeelden).

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
recaptcha:
 lockip: false
 lockuser: true
 expiry: 720
 recaptcha_log: "recaptcha.{yyyy}-{mm}-{dd}.txt"
 enabled: true
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

##### 6.2.1 HOE OM SIGNATUURSECTIES TE MARKEREN VOOR GEBRUIK MET reCAPTCHA/hCAPTCHA

Als "usemode" is 2 of 5, om signatuursecties te markeren voor gebruik met reCAPTCHA/hCAPTCHA, een invoer wordt opgenomen in het YAML segment voor dat signature-sectie (zie het onderstaande voorbeeld).

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

#### 6.3 EXTRA INFORMATIE

##### 6.3.0 SIGNATUURSECTIES TE NEGEREN

Bovendien, als u wilt CIDRAM om enkele specifieke secties in iedereen van de signatuurbestanden te negeren, kunt u het `ignore.dat` bestand gebruiken om specificeren welke secties te negeren. Op een nieuwe regel, schrijven `Ignore`, gevolgd door een spatie, gevolgd door de naam van de sectie die u wilt CIDRAM te negeren (zie het onderstaande voorbeeld).

```
Ignore Sectie 1
```

Dit kan ook worden bereikt door de interface te gebruiken die wordt geboden door de pagina "sectielijst" van de frontend van CIDRAM.

##### 6.3.1 AANVULLENDE REGELS

Als u vindt dat het schrijven van uw eigen aangepaste signatuurbestanden of aangepaste modules te ingewikkeld voor u is, kan een eenvoudiger alternatief zijn om de interface te gebruiken die wordt geboden door de "aanvullende regels"-pagina van de front-end van CIDRAM. Door de juiste opties te selecteren en details over specifieke soorten verzoeken op te geven, kunt u CIDRAM instrueren hoe op die verzoeken moet worden gereageerd. "Aanvullende regels" worden uitgevoerd nadat alle signatuurbestanden en modules al zijn uitgevoerd.

#### 6.4 <a name="MODULE_BASICS"></a>BASICS (VOOR MODULES)

Modules kunnen worden gebruikt om de functionaliteit van CIDRAM uit te breiden, extra taken uit te voeren, of aanvullende logica te verwerken.

Vanwege dat modules worden geschreven als PHP-bestanden, als je voldoende bekend bent met de CIDRAM-codebase, kun je je modules structureren zoals u wilt, en schrijf uw module-signatures zoals u dat wilt (op grond van wat mogelijk is met PHP).

*Notitie: Als u het niet prettig vindt om met PHP-code te werken, wordt het niet aanbevolen om uw eigen modules te schrijven.*

CIDRAM biedt een aantal functies voor het gebruik van modules, waardoor het eenvoudiger en gemakkelijker is om uw eigen modules te schrijven. Informatie over deze functionaliteit wordt hieronder beschreven.

#### 6.5 MODULE FUNCTIONALITEIT

##### 6.5.0 "$this->trigger"

Module-signatures worden meestal geschreven met `$this->trigger`. In de meeste gevallen zal deze method belangrijker zijn dan iets anders om modules te schrijven.

`$this->trigger` accepteert 4 parameters: `$Condition`, `$ReasonShort`, `$ReasonLong` (optioneel), en `$DefineOptions` (optioneel).

De waarachtigheid van `$Condition` wordt geëvalueerd, en indien true/waar, wordt de signature "getriggerd". Indien deze false/vals is, wordt de signature *niet* "getriggerd". `$Condition` bevat meestal PHP-code om een voorwaarde te evalueren die ervoor moet zorgen dat een verzoek wordt geblokkeerd.

`$ReasonShort` wordt vermeld in het "Waarom Geblokkeerd" veld wanneer de signature wordt "getriggerd".

`$ReasonLong` is een optioneel bericht dat aan de gebruiker/client moet worden weergegeven voor wanneer ze zijn geblokkeerd, om uit te leggen waarom ze zijn geblokkeerd. Standaard ingesteld op het standaardbericht "Toegang Geweigerd" wanneer dit wordt weggelaten.

`$DefineOptions` is een optionele array met sleutel/waarde-paren, die wordt gebruikt om configuratie-opties te definiëren die specifiek zijn voor de instantie. Configuratie-opties worden toegepast wanneer de signature "getriggerd" is.

`$this->trigger` retourneert true/waar als de signature "getriggerd" is, en false/vals als dat niet het geval is.

##### 6.5.1 "$this->bypass"

Signature-bypasses worden meestal geschreven met `$this->bypass`.

`$this->bypass` accepteert 3 parameters: `$Condition`, `$ReasonShort`, en `$DefineOptions` (optioneel).

De waarachtigheid van `$Condition` wordt geëvalueerd, en indien true/waar, wordt de bypass "getriggerd". Indien deze false/vals is, wordt de bypass *niet* "getriggerd". `$Condition` bevat meestal PHP-code om een voorwaarde te evalueren die ervoor moet zorgen dat een verzoek wordt *niet* geblokkeerd.

`$ReasonShort` wordt vermeld in het "Waarom Geblokkeerd" veld wanneer de bypass wordt "getriggerd".

`$DefineOptions` is een optionele array met sleutel/waarde-paren, die wordt gebruikt om configuratie-opties te definiëren die specifiek zijn voor de instantie. Configuratie-opties worden toegepast wanneer de bypass "getriggerd" is.

`$this->bypass` retourneert true/waar als de bypass "getriggerd" is, en false/vals als dat niet het geval is.

##### 6.5.2 "$this->dnsReverse"

Dit kan worden gebruikt om de hostnaam van een IP-adres op te halen. Als u een module wilt maken om hostnamen te blokkeren, kan deze method nuttig zijn.

Voorbeeld:
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

#### 6.6 MODULE VARIABELEN

Modules worden in hun eigen bereik uitgevoerd, en alle variabelen gedefinieerd door een module, zullen niet toegankelijk zijn voor andere modules, of naar het bovenliggende script, tenzij ze zijn opgeslagen in de array `$CIDRAM` (al het andere wordt gespoeld nadat de module-uitvoering is voltooid).

Hieronder vindt u enkele veelvoorkomende variabelen die handig kunnen zijn voor uw module:

Variabele | Beschrijving
----|----
`$this->BlockInfo['DateTime']` | De huidige datum en tijd.
`$this->BlockInfo['IPAddr']` | IP-adres voor het huidige verzoek.
`$this->BlockInfo['ScriptIdent']` | CIDRAM-scriptversie.
`$this->BlockInfo['Query']` | De vraag voor het huidige verzoek.
`$this->BlockInfo['Referrer']` | De verwijzer voor het huidige verzoek (indien aanwezig).
`$this->BlockInfo['UA']` | De user-agent voor het huidige verzoek.
`$this->BlockInfo['UALC']` | De user-agent voor het huidige verzoek (in kleine letters).
`$this->BlockInfo['ReasonMessage']` | Het bericht dat moet worden weergegeven aan de gebruiker/client voor het huidige verzoek als ze zijn geblokkeerd.
`$this->BlockInfo['SignatureCount']` | Het aantal signatures dat is getriggerd voor het huidige verzoek.
`$this->BlockInfo['Signatures']` | Referentie-informatie voor alle signatures die zijn getriggerd voor het huidige verzoek.
`$this->BlockInfo['WhyReason']` | Referentie-informatie voor alle signatures die zijn getriggerd voor het huidige verzoek.

---


### 7. <a name="SECTION7"></a>BEKENDE COMPATIBILITEITSPROBLEMEN

De volgende pakketten en producten zijn incompatibel met CIDRAM:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

Modules zijn beschikbaar gemaakt om ervoor te zorgen dat de volgende pakketten en producten compatibel zijn met CIDRAM:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__

*Zie ook: [Compatibiliteitskaarten](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 8. <a name="SECTION8"></a>VEELGESTELDE VRAGEN (FAQ)

- [Wat is een "signature"?](#user-content-WHAT_IS_A_SIGNATURE)
- [Wat is een "CIDR"?](#user-content-WHAT_IS_A_CIDR)
- [Wat is een "vals positieve"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)
- [Kan CIDRAM blok hele landen?](#user-content-BLOCK_ENTIRE_COUNTRIES)
- [Hoe vaak worden signatures bijgewerkt?](#user-content-SIGNATURE_UPDATE_FREQUENCY)
- [Ik heb een fout tegengekomen tijdens het gebruik van CIDRAM en ik weet niet wat te doen! Help alstublieft!](#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [Ik ben geblokkeerd door CIDRAM van een website die ik wil bezoeken! Help alstublieft!](#user-content-BLOCKED_WHAT_TO_DO)
- [Ik wil CIDRAM v3 gebruiken met een PHP-versie ouder dan 7.2; Kan u helpen?](#user-content-MINIMUM_PHP_VERSION_V3)
- [Kan ik een enkele CIDRAM-installatie gebruiken om meerdere domeinen te beschermen?](#user-content-PROTECT_MULTIPLE_DOMAINS)
- [Ik wil niet tijd verspillen met het installeren van dit en om het te laten werken met mijn website; Kan ik u betalen om het te doen?](#user-content-PAY_YOU_TO_DO_IT)
- [Kan ik u of een van de ontwikkelaars van dit project voor privéwerk huren?](#user-content-HIRE_FOR_PRIVATE_WORK)
- [Ik heb speciale modificaties en aanpassingen nodig; Kan u helpen?](#user-content-SPECIALIST_MODIFICATIONS)
- [Ik ben een ontwikkelaar, website ontwerper, of programmeur. Kan ik werken aan dit project accepteren of aanbieden?](#user-content-ACCEPT_OR_OFFER_WORK)
- [Ik wil bijdragen aan het project; Kan ik dit doen?](#user-content-WANT_TO_CONTRIBUTE)
- [Kan ik cron gebruiken om automatisch bij te werken?](#user-content-CRON_TO_UPDATE_AUTOMATICALLY)
- [Wat zijn "overtredingen"?](#user-content-WHAT_ARE_INFRACTIONS)
- [Kan CIDRAM hostnamen blokkeren?](#user-content-BLOCK_HOSTNAMES)
- [Wat kan ik gebruiken voor "default_dns"?](#wat-kan-ik-gebruiken-voor-default_dns)
- [Kan ik CIDRAM gebruiken om andere dingen dan websites te beschermen (b.v., e-mailservers, FTP, SSH, IRC, enz)?](#user-content-PROTECT_OTHER_THINGS)
- [Zullen er problemen optreden als ik CIDRAM tegelijk gebruik met CDN's of cacheservices?](#user-content-CDN_CACHING_PROBLEMS)
- [Zal CIDRAM mijn website beschermen tegen DDoS-aanvallen?](#user-content-DDOS_ATTACKS)
- [Wanneer ik modules of signatuurbestanden activeer of deactiveer via de updates-pagina, sorteert deze ze alfanumeriek in de configuratie. Kan ik de manier wijzigen waarop ze worden gesorteerd?](#user-content-CHANGE_COMPONENT_SORT_ORDER)
- [Wat is een "PDO DSN"? Hoe kan ik PDO gebruiken met CIDRAM?](#user-content-HOW_TO_USE_PDO)
- [CIDRAM blokkeert cronjobs; Hoe dit op te lossen?](#user-content-BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>Wat is een "signature"?

In het context van CIDRAM, een "signature" verwijst naar gegevens die als een indicator/identifier werken, voor iets specifiek waarnaar we op zoek zijn, gewoonlijk een IP-adres of CIDR, en bevat een aantal instructies voor CIDRAM, vertelt het de beste manier om wanneer het ontmoet waar we naar op zoek zijn te reageren. Een typische signature voor CIDRAM ziet er als volgt uit:

Voor "signatuurbestanden":

`1.2.3.4/32 Deny Generic`

Voor "modules":

```PHP
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*Notitie: Signatures voor "signatuurbestanden", en signatures voor "modules", zijn niet hetzelfde.*

Vaak (maar niet altijd), signatures bundelen samen in groepen, dat vormen van "signatuursecties", vaak vergezeld van opmerkingen, markup, en/of gerelateerde metadata die kunnen om extra context voor de signatures en/of om verdere instructies worden gebruikt.

#### <a name="WHAT_IS_A_CIDR"></a>Wat is een "CIDR"?

"CIDR" is een acroniem voor "Classless Inter-Domain Routing" *[[1](https://nl.wikipedia.org/wiki/Classless_Inter-Domain_Routing), [2](https://whatismyipaddress.com/cidr)]*, en het is dit acroniem dat gebruikt wordt als onderdeel van de naam voor dit pakket, "CIDRAM", waarvoor is een acroniem voor "Classless Inter-Domain Routing Access Manager".

Echter, in het context van CIDRAM (zoals, binnen deze documentatie, binnen discussies met betrekking tot CIDRAM, of binnen de CIDRAM lokalisaties), wanneer een "CIDR" (enkelvoud) of "CIDR's" (meervoud) wordt genoemd of bedoeld (en dus waarbij we deze woorden als zelfstandige naamwoorden gebruiken, in tegenstelling tot als acroniemen), wat hier bedoeld is, is een subnet (of subnetten), uitgedrukt met CIDR notatie. De reden dat CIDR (of CIDR's) wordt gebruikt in plaats van subnet (of subnetten) is om duidelijk te maken dat het specifiek subnets wordt uitgedrukt met CIDR notatie waarnaar wordt verwezen (omdat CIDR notatie slechts één van de verschillende manieren waarop subnetten uitgedrukt kunnen worden). CIDRAM kan daarom beschouwd worden als een "subnet access manager".

Hoewel deze dubbele betekenis van "CIDR" in sommige gevallen dubbelzinnig kan zijn, deze uitleg, samen met de context die wordt verstrekt, zou moeten helpen om dubbelzinnigheid te heffen.

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>Wat is een "vals positieve"?

De term "vals positieve" (*alternatief: "vals positieve fout"; "vals alarm"*; Engels: *false positive*; *false positive error*; *false alarm*), zeer eenvoudig beschreven, en een algemene context, wordt gebruikt bij het testen voor een toestand, om verwijst naar om de resultaten van die test, wanneer de resultaten positief zijn (d.w.z, de toestand wordt vastgesteld als "positief"), maar wordt verwacht "negatief" te zijn (d.w.z, de toestand in werkelijkheid is "negatief"). Een "vals positieve" analoog aan "huilende wolf" kan worden beschouwd (waarin de toestand wordt getest, is of er een wolf in de buurt van de kudde, de toestand is "vals" in dat er geen wolf in de buurt van de kudde, en de toestand wordt gerapporteerd als "positief" door de herder door middel van schreeuwen "wolf, wolf"), of analoog aan situaties in medische testen waarin een patiënt gediagnosticeerd als met een ziekte of aandoening, terwijl het in werkelijkheid, hebben ze geen ziekte of aandoening.

Enkele andere termen die worden gebruikt zijn "waar positieve", "waar negatieve" en "vals negatieve". Een "waar positieve" verwijst naar wanneer de resultaten van de test en de huidige staat van de toestand zijn beide waar (of "positief"), and a "waar negatieve" verwijst naar wanneer de resultaten van de test en de huidige staat van de toestand zijn beide vals (of "negatief"); En "waar positieve" of en "waar negatieve" wordt beschouwd als een "correcte gevolgtrekking" zijn. De antithese van een "vals positieve" is een "vals negatieve"; Een "vals negatieve" verwijst naar wanneer de resultaten van de test is negatief (d.w.z, de aandoening wordt vastgesteld als "negatief"), maar wordt verwacht "positief" te zijn (d.w.z, de toestand in werkelijkheid is "positief").

In de context van CIDRAM, deze termen verwijzen naar de signatures van CIDRAM en wat/wie ze blokkeren. Wanneer CIDRAM blokkeert een IP-adres, als gevolg van slechte, verouderde of onjuiste signature, maar moet niet hebben gedaan, of wanneer het doet om de verkeerde redenen, we verwijzen naar deze gebeurtenis als een "vals positieve". Wanneer CIDRAM niet in slaagt te blokkeren om een IP-adres dat had moeten worden geblokkeerd, als gevolg van onvoorziene bedreigingen, ontbrekende signatures of tekorten in zijn signatures, we verwijzen naar deze gebeurtenis als een "gemiste detectie" (dat is analoog aan een "vals negatieve").

Dit kan worden samengevat in de onderstaande tabel:

&nbsp; | CIDRAM moet *NIET* een IP-adres te blokkeren | CIDRAM *MOET* een IP-adres te blokkeren
---|---|---
CIDRAM *NIET* doet blokkeren van een IP-adres | Waar negatieve (correcte gevolgtrekking) | Gemiste detectie (analoog aan vals negatieve)
CIDRAM *DOET* blokkeren van een IP-adres | __Vals positieve__ | Waar positieve (correcte gevolgtrekking)

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>Kan CIDRAM blok hele landen?

Ja. De eenvoudigste manier om dit te doen is door de BGPView-module te installeren en te configureren volgens uw behoeften.

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>Hoe vaak worden signatures bijgewerkt?

Bijwerkfrequentie varieert afhankelijk van de signatuurbestanden betrokken. Alle de onderhouders voor CIDRAM signatuurbestanden algemeen proberen om hun signatures regelmatig bijgewerkt te houden, maar als gevolg van dat ieder van ons hebben verschillende andere verplichtingen, ons leven buiten het project, en zijn niet financieel gecompenseerd (d.w.z., betaald) voor onze inspanningen aan het project, een nauwkeurige updateschema kan niet worden gegarandeerd. In het algemeen, signatures zullen worden bijgewerkt wanneer er genoeg tijd om dit te doen, en in het algemeen, onderhouders proberen om prioriteiten te stellen op basis van noodzaak en van hoe vaak veranderingen optreden tussen ranges. Het verlenen van bijstand wordt altijd gewaardeerde als u bent bereid om dat te doen.

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>Ik heb een fout tegengekomen tijdens het gebruik van CIDRAM en ik weet niet wat te doen! Help alstublieft!

- Gebruikt u de nieuwste versie van de software? Gebruikt u de nieuwste versies van uw signatuurbestanden? Indien het antwoord op een van deze twee vragen is nee, probeer eerst om alles te bijwerken, en controleer of het probleem zich blijft voordoen. Als dit aanhoudt, lees verder.
- Hebt u door alle documentatie gecontroleerd? Zo niet, doe dat dan. Als het probleem niet kan worden opgelost met behulp van de documentatie, lees verder.
- Hebt u de **[issues pagina](https://github.com/CIDRAM/CIDRAM/issues)** gecontroleerd, om te zien of het probleem al eerder is vermeld? Als het eerder vermeld, controleer of eventuele suggesties, ideeën en/of oplossingen werden verstrekt, en volg als per nodig om te proberen het probleem op te lossen.
- Als het probleem blijft bestaan, zoek hulp door een nieuw issue op de issues pagina te maken.

#### <a name="BLOCKED_WHAT_TO_DO"></a>Ik ben geblokkeerd door CIDRAM van een website die ik wil bezoeken! Help alstublieft!

CIDRAM biedt een manier voor website-eigenaren om ongewenst verkeer te blokkeren, maar het is de verantwoordelijkheid van de website-eigenaren om zelf te beslissen hoe ze willen CIDRAM gebruiken. In het geval van de valse positieven met betrekking tot de signatuurbestanden normaal meegeleverd met CIDRAM, correcties kunnen worden gemaakt, maar met betrekking tot het wordt gedeblokkeerd van specifieke websites, u nodig hebt om te communiceren met de eigenaren van de websites in kwestie. In gevallen waarin correcties worden gemaakt, op zijn minst, zullen ze nodig hebben om hun signatuurbestanden en/of installatie bij te werken, en in andere gevallen (zoals bijvoorbeeld, waarin ze hun installatie hebt gewijzigd, creëerden hun eigen aangepaste signatures, enz), het is hun verantwoordelijkheid om uw probleem op te lossen, en is geheel buiten onze controle.

#### <a name="MINIMUM_PHP_VERSION_V3"></a>Ik wil CIDRAM v3 gebruiken met een PHP-versie ouder dan 7.2; Kan u helpen?

Nee. PHP≥7.2 is een minimale vereiste voor CIDRAM v3.

*Zie ook: [Compatibiliteitskaarten](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>Kan ik een enkele CIDRAM-installatie gebruiken om meerdere domeinen te beschermen?

Ja. CIDRAM-installaties zijn niet van nature gebonden naar specifieke domeinen, en kan daarom worden gebruikt om meerdere domeinen te beschermen. Algemeen, wij verwijzen naar CIDRAM installaties die slechts één domein beschermen als "single-domain installaties", en wij verwijzen naar CIDRAM installaties die meerdere domeinen en/of subdomeinen beschermen als "multi-domain installaties". Als u een multi-domain installaties werken en nodig om verschillende signatuurbestanden voor verschillende domeinen te gebruiken, of nodig om CIDRAM anders geconfigureerd voor verschillende domeinen te zijn, het is mogelijk om dit te doen. Nadat het configuratiebestand hebt geladen (`config.yml`), CIDRAM controleert het bestaan van een "configuratie overschrijdend bestand" specifiek voor het domein (of sub-domein) dat wordt aangevraagd (`het-domein-dat-wordt-aangevraagd.tld.config.yml`), en als gevonden, elke configuratie waarden gedefinieerd door het configuratie overschrijdend bestand zal worden gebruikt in plaats van de configuratie waarden die zijn gedefinieerd door het configuratiebestand. Het configuratie overschrijdende bestanden zijn identiek aan het configuratiebestand, en naar eigen goeddunken, kan de volledige van alle configuratie richtlijnen beschikbaar voor CIDRAM bevatten, of wat dan ook kleine subsectie dat nodig is die afwijkt van de waarden die normaal door het configuratiebestand worden gedefinieerd. Het configuratie overschrijdende bestanden worden genoemd volgens het domein waaraan ze bestemd zijn (dus, bijvoorbeeld, als u een configuratie overschrijdend bestand voor het domein `https://www.some-domain.tld/` nodig hebt, het configuratie overschrijdende bestanden moeten worden genoemd als `some-domain.tld.config.yml`, en moeten naast het configuratiebestand, `config.yml`, in de vault geplaatst worden). De domeinnaam is afgeleid van de koptekst `HTTP_HOST` van het verzoek; "www" wordt genegeerd.

#### <a name="PAY_YOU_TO_DO_IT"></a>Ik wil niet tijd verspillen met het installeren van dit en om het te laten werken met mijn website; Kan ik u betalen om het te doen?

Misschien. Dit wordt per geval beoordeeld. Laat ons weten wat u nodig hebt, wat u aanbiedt, en wij laten u weten of we kunnen helpen.

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>Kan ik u of een van de ontwikkelaars van dit project voor privéwerk huren?

*Zie hierboven.*

#### <a name="SPECIALIST_MODIFICATIONS"></a>Ik heb speciale modificaties en aanpassingen nodig; Kan u helpen?

*Zie hierboven.*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>Ik ben een ontwikkelaar, website ontwerper, of programmeur. Kan ik werken aan dit project accepteren of aanbieden?

Ja. Onze licentie verbiedt dit niet.

#### <a name="WANT_TO_CONTRIBUTE"></a>Ik wil bijdragen aan het project; Kan ik dit doen?

Ja. Bijdragen aan het project zijn zeer welkom. Zie voor meer informatie "CONTRIBUTING.md".

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>Kan ik cron gebruiken om automatisch bij te werken?

Ja. Een API is ingebouwd in het frontend voor interactie met de updates pagina via externe scripts. Een apart script, "[Cronable](https://github.com/Maikuolan/Cronable)", is beschikbaar, en kan door uw cron manager of cron scheduler gebruikt worden om deze en andere ondersteunde pakketten automatisch te updaten (dit script biedt zijn eigen documentatie).

#### <a name="WHAT_ARE_INFRACTIONS"></a>Wat zijn "overtredingen"?

"Signatures tellen" en "overtredingen" hebben beide betrekking op de ernst en het aantal signatures dat tijdens een bepaald verzoek is geactiveerd, ongeacht of dit te wijten is aan signatuurbestanden, modules, aanvullende regels, of anderszins, maar terwijl het "signatures tellen" alleen voor dat specifieke verzoek blijft bestaan, "overtredingen" kunnen over een aantal verzoeken blijven bestaan, zolang als wordt bepaald door de `default_tracktime`.

Dit biedt een mechanisme om ervoor te zorgen dat verzoeken van potentieel gevaarlijke bronnen kunnen worden geblokkeerd, waarbij die bron al was geblokkeerd tijdens een eerder verzoek met een voldoende aantal overtredingen.

#### <a name="BLOCK_HOSTNAMES"></a>Kan CIDRAM hostnamen blokkeren?

Ja. Dit kan worden bereikt door een aanvullende regel of aangepaste module te maken.

![Een aanvullende regel voor het blokkeren van hostnamen](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>Wat kan ik gebruiken voor "default_dns"?

Over het algemeen zou het IP van een betrouwbare DNS-server voldoende moeten zijn. Als u op zoek bent naar suggesties, bieden [public-dns.info](https://public-dns.info/) en [OpenNIC](https://servers.opennic.org/) uitgebreide lijsten met bekende, openbare DNS-servers. Of, kijk in de onderstaande tabel:

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

*Notitie: Ik maak geen claims of garanties met betrekking tot de privacypraktijken, beveiliging, werkzaamheid of betrouwbaarheid van enige DNS-services die worden vermeld of anderszins. Doe uw eigen onderzoek als u beslissingen over hun neemt.*

#### <a name="PROTECT_OTHER_THINGS"></a>Kan ik CIDRAM gebruiken om andere dingen dan websites te beschermen (b.v., e-mailservers, FTP, SSH, IRC, enz)?

Je kan (in juridische zin), maar je zou dit niet moeten doen (in een technische en praktische zin). Onze licentie beperkt niet welke technologieën CIDRAM implementeren, maar CIDRAM is een WAF (Web Application Firewall) en is altijd bedoeld om websites te beschermen. Omdat het niet is ontworpen met andere technologieën in het achterhoofd, is het onwaarschijnlijk dat het effectief is of een betrouwbare bescherming biedt voor andere technologieën, implementatie zal waarschijnlijk moeilijk zijn, en het risico op valse positieven en gemiste detecties is zeer hoog.

#### <a name="CDN_CACHING_PROBLEMS"></a>Zullen er problemen optreden als ik CIDRAM tegelijk gebruik met CDN's of cacheservices?

Mogelijk. Dit is afhankelijk van de aard van de service in kwestie en hoe u deze gebruikt. Over het algemeen zijn er geen problemen als u alleen statische items (afbeeldingen, CSS, enz) in het cache plaatst. Er kunnen echter problemen zijn, als u gegevens in de cache opslaat die anders normaliter dynamisch zouden worden gegenereerd wanneer daarom wordt gevraagd, of als u de resultaten van POST-verzoeken in cache opslaat (dit zou in wezen uw website en zijn omgeving als verplicht statisch maken, en het is onwaarschijnlijk dat CIDRAM een zinvol voordeel biedt in een verplichte statische omgeving). Er kunnen ook specifieke configuratievereisten voor CIDRAM zijn, afhankelijk van welke CDN of cacheservice u gebruikt (je moet ervoor zorgen dat CIDRAM correct is geconfigureerd voor de specifieke CDN of cacheservice die u gebruikt). Het niet correct configureren van CIDRAM kan leiden tot aanzienlijk problematische valse positieven en gemiste detecties.

#### <a name="DDOS_ATTACKS"></a>Zal CIDRAM mijn website beschermen tegen DDoS-aanvallen?

Kort antwoord: Nee.

Een iets langer antwoord: CIDRAM helpt de impact van ongewenst verkeer op uw website te verminderen (waardoor de bandbreedtekosten van uw website worden geminderd), helpt de impact van ongewenst verkeer op uw hardware te verminderen (b.v., de mogelijkheid van uw server om verzoeken te verwerken en te serveren), en kan helpen om verschillende andere mogelijke negatieve effecten geassocieerd met ongewenst verkeer te verminderen. Er zijn echter twee belangrijke dingen die onthouden moeten worden om deze vraag te begrijpen.

Ten eerste, CIDRAM is een PHP-pakket en werkt daarom op de computer waarop PHP is geïnstalleerd. Dit betekent dat CIDRAM een verzoek alleen kan zien en blokkeren *nadat* de server het al heeft ontvangen. Ten tweede, effectieve DDoS-mitigatie moet aanvragen filteren *voordat* ze de server bereikt waarop de DDoS-aanval gericht is. In het ideale geval moeten DDoS-aanvallen worden gedetecteerd en beperkt door oplossingen die in staat zijn om verkeer dat is gekoppeld aan aanvallen te laten vallen of omleiden, voordat het in de eerste plaats de gerichte server bereikt.

Dit kan worden geïmplementeerd met behulp van speciale hardware-oplossingen op locatie, en/of cloudgebaseerde oplossingen zoals speciale DDoS-mitigatie diensten, routering van de DNS van een domein via DDoS-resistente netwerken, cloudgebaseerde filteren, of een combinatie daarvan. In elk geval is dit onderwerp echter een beetje te ingewikkeld om grondig met slechts een paar alinea's uit te leggen, dus ik zou aanraden verder onderzoek te doen als dit een onderwerp is dat u wilt nastreven. Wanneer de ware aard van DDoS-aanvallen goed wordt begrepen, zal dit antwoord logischer zijn.

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>Wanneer ik modules of signatuurbestanden activeer of deactiveer via de updates-pagina, sorteert deze ze alfanumeriek in de configuratie. Kan ik de manier wijzigen waarop ze worden gesorteerd?

Ja. Als u bepaalde bestanden wilt dwingen om in een specifieke volgorde uit te voeren, kunt u enkele willekeurige gegevens vóór hun naam toevoegen in de configuratie richtlijn waar ze worden vermeld, gescheiden door een dubbele punt. Wanneer de updates-pagina vervolgens de bestanden opnieuw sorteert, heeft deze toegevoegde willekeurige gegevens invloed op de sorteervolgorde, waardoor ze vervolgens in de gewenste volgorde worden uitgevoerd, zonder dat ze hoeven te hernoemen.

Stel dat u bijvoorbeeld een configuratie richtlijn aanneemt met de volgende bestanden:

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

Als u wilt dat `file3.php` het eerst uitvoert, u zou iets als `aaa:` kunnen toevoegen voor de naam van het bestand:

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

Als dan een nieuw bestand, `file6.php`, is geactiveerd, als de updates-pagina ze allemaal opnieuw sorteert, het zou zo moeten eindigen:

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

Dezelfde situatie wanneer een bestand is gedeactiveerd. Omgekeerd, als u wilde dat het bestand als laatste werd uitgevoerd, u zou iets als `zzz:` kunnen toevoegen voor de naam van het bestand. In elk geval hoeft u het betreffende bestand niet te hernoemen.

#### <a name="HOW_TO_USE_PDO"></a>Wat is een "PDO DSN"? Hoe kan ik PDO gebruiken met CIDRAM?

"PDO" is een acroniem voor "[PHP Data Objects](https://www.php.net/manual/en/intro.pdo.php)". Het biedt een interface voor PHP met sommige databasesystemen te verbinden die vaak worden gebruikt door verschillende PHP-applicaties.

"DSN" is een acroniem voor "[data source name](https://en.wikipedia.org/wiki/Data_source_name)". De "PDO DSN" beschrijft aan PDO hoe te verbinden met een database.

CIDRAM biedt de optie om PDO te gebruiken voor cachingdoeleinden. Om dit correct te laten werken, moet u CIDRAM dienovereenkomstig configureren, PDO ingeschakeld gemaakt, een nieuwe database maken die CIDRAM kan gebruiken (als u nog geen database voor CIDRAM in gedachten hebt), en een nieuwe tabel in uw database maken in overeenstemming met de hieronder beschreven structuur.

Wanneer een databaseverbinding succesvol is, maar de benodigde tabel bestaat niet, zal deze proberen de tabel automatisch aan te maken. Dit gedrag is echter niet uitgebreid getest en succes kan niet worden gegarandeerd.

Dit is natuurlijk alleen van toepassing als u daadwerkelijk wilt dat CIDRAM PDO gebruikt. Als u tevreden bent dat CIDRAM flatfile caching gebruikt (volgens de standaardconfiguratie), of een van de andere aangeboden cachingopties, hoeft u zich geen zorgen te maken over het opzetten van databases, tabellen, enzovoort.

De hieronder beschreven structuur gebruikt "cidram" als de databasenaam, maar u kunt elke gewenste naam gebruiken voor uw database, zolang diezelfde naam wordt gerepliceerd in uw DSN-configuratie.

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

CIDRAM's `pdo_dsn` configuratie-richtlijn moet worden geconfigureerd zoals hieronder beschreven.

```
Afhankelijk van welk databasestuurprogramma wordt gebruikt...
├─4d (Waarschuwing: Experimenteel, niet getest, niet aanbevolen!)
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └De host waarmee verbinding wordt gemaakt om de database te
│             vinden.
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └De naam van de database te
│                │              │             gebruiken.
│                │              │
│                │              └Het poortnummer waarmee verbinding moet worden
│                │               gemaakt met de host.
│                │
│                └De host waarmee verbinding wordt gemaakt om de database te
│                 vinden.
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └De naam van de database te gebruiken.
│    │          │
│    │          └De host waarmee verbinding wordt gemaakt om de database te
│    │           vinden.
│    │
│    └Mogelijke waarden: "mssql", "sybase", "dblib".
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├Kan een pad zijn naar een lokaal databasebestand.
│                    │
│                    ├Kan verbinding maken met een host en poortnummer.
│                    │
│                    └Raadpleeg de Firebird-documentatie als u hiervan gebruik
│                     wilt maken.
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └Met welke gecatalogiseerde database om verbinding mee te maken.
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └Met welke gecatalogiseerde database om verbinding mee te
│                  maken.
├─mysql (Meest aanbevolen!)
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └Het poortnummer waarmee
│                 │            │               verbinding moet worden gemaakt
│                 │            │               met de host.
│                 │            │
│                 │            └De host waarmee verbinding wordt gemaakt om de
│                 │             database te vinden.
│                 │
│                 └De naam van de database te gebruiken.
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├Kan verwijzen naar de specifieke gecatalogiseerde database.
│               │
│               ├Kan verbinding maken met een host en poortnummer.
│               │
│               └Raadpleeg de Oracle-documentatie als u hiervan gebruik wilt
│                maken.
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├Kan verwijzen naar de specifieke gecatalogiseerde database.
│         │
│         ├Kan verbinding maken met een host en poortnummer.
│         │
│         └Raadpleeg de ODBC/DB2-documentatie als u hiervan gebruik wilt maken.
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └De naam van de database te
│               │              │            gebruiken.
│               │              │
│               │              └Het poortnummer waarmee verbinding moet worden
│               │               gemaakt met de host.
│               │
│               └De host waarmee verbinding wordt gemaakt om de database te
│                vinden.
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └Het pad naar het te gebruiken lokale databasebestand.
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └De naam van de database te gebruiken.
                   │         │
                   │         └Het poortnummer waarmee verbinding moet worden
                   │          gemaakt met de host.
                   │
                   └De host waarmee verbinding wordt gemaakt om de database te
                    vinden.
```

Als u niet zeker weet wat u voor een bepaald deel van uw DSN moet gebruiken, probeer dan eerst te kijken of het werkt zoals het is, zonder iets te veranderen.

Merk op dat `pdo_username` en `pdo_password` hetzelfde moeten zijn als de gebruikersnaam en het wachtwoord dat u hebt gekozen voor uw database.

#### <a name="BLOCK_CRON"></a>CIDRAM blokkeert cronjobs; Hoe dit op te lossen?

Als u een toegewijd bestand gebruikt voor cronjobs, en als dat bestand niet hoeft te worden aangeroepen tijdens normale gebruikersverzoeken (d.w.z., buiten de context van cronjobs), de meest eenvoudige manier om dit op te lossen, is om ervoor te zorgen dat CIDRAM helemaal niet wordt uitgevoerd tijdens uw cronjobs (d.w.z., haak CIDRAM niet vast aan het bestand dat verantwoordelijk is voor de afhandeling van uw cronjobs).

Als alternatief, als dat niet mogelijk is, maar het IP-adres van uw cron-server is relatief consistent en voorspelbaar, u kunt proberen het IP-adres van uw cron-server op de witte lijst te zetten door er een signature op de witte lijst voor te maken in een aangepast signatuurbestand of door er een aanvullende regel voor te maken. Als het IP-adres van uw cron-server regelmatig roteert en niet bijzonder voorspelbaar is, maar blijft toch binnen hetzelfde netwerk, u zou kunnen proberen in uw `ignore.dat` bestand de naam te vermelden van de signatuursectie die verantwoordelijk is voor het blokkeren van het in de eerste plaats.

Als u al die ideeën hebt geprobeerd en geen van hen voor jou werkte, of als u hulp nodig hebt om uit te vinden hoe u het moet doen, u kunt een nieuw issue maken op de issues-pagina van CIDRAM om hulp te vragen.

---


### 9. <a name="SECTION9"></a>LEGALE INFORMATIE

#### 9.0 SECTIE PREAMBULE

Dit sectie van de documentatie is bedoeld om mogelijke juridische overwegingen met betrekking tot het gebruik en de implementatie van het pakket te beschrijven, en om wat basisgerelateerde informatie te verstrekken. Dit kan voor sommige gebruikers belangrijk zijn om naleving van eventuele wettelijke vereisten in de landen waarin zij actief zijn te waarborgen, en sommige gebruikers moeten hun website-beleid mogelijk aanpassen in overeenstemming met deze informatie.

Eerst en vooral, realiseer je alstublieft dat ik (de auteur van het pakket) geen advocaat en geen gekwalificeerde juridische professional van welke aard. Daarom ben ik niet juridisch gekwalificeerd om juridisch advies te geven. Ook in sommige gevallen, exacte wettelijke vereisten kunnen verschillen tussen verschillende landen en rechtsgebieden, en deze variërende wettelijke vereisten kunnen soms conflicteren (zoals bijvoorbeeld, in het geval van landen die voorrang geven aan [privacyrechten](https://nl.wikipedia.org/wiki/Privacy) en het [recht om te worden vergeten](https://nl.wikipedia.org/wiki/Recht_om_vergeten_te_worden), versus landen die de voorrang geven aan uitgebreide [dataretentie](https://nl.wikipedia.org/wiki/Dataretentie)). Overweeg ook dat toegang tot het pakket niet beperkt is tot specifieke landen of rechtsgebieden, en daarom is de gebruikersbasis van het pakket waarschijnlijk geografisch divers. Gezien deze punten, ben ik niet in de positie om aan te geven wat het betekent om "in overeenstemming met de wetgeving" te zijn voor alle gebruikers, in alle opzichten. Ik hoop echter dat de informatie hierin u zal helpen om zelf tot een beslissing te komen over wat u moet doen om wettelijk compatibel te blijven in de context van het pakket. Als u twijfels of zorgen hebt met betrekking tot de informatie hierin, of als u aanvullende hulp en advies nodig hebt vanuit een juridisch perspectief, ik zou aanraden een gekwalificeerde juridische professional te raadplegen.

#### 9.1 AANSPRAKELIJKHEID EN VERANTWOORDELIJKHEID

Zoals al aangegeven door de pakketlicentie, wordt het pakket geleverd zonder enige garantie. Dit omvat (maar is niet beperkt tot) alle reikwijdte van aansprakelijkheid. Het pakket wordt u aangeboden voor uw gemak, in de hoop dat dit nuttig zal zijn, en dat het u enig voordeel oplevert. Echter, of u het pakket gebruikt of implementeert, is uw eigen keuze. U bent niet gedwongen om het pakket te gebruiken of te implementeren, maar wanneer u dat doet, bent u verantwoordelijk voor dat besluit. Noch ik, noch andere bijdragers aan het pakket, zijn juridisch aansprakelijk voor de gevolgen van de beslissingen die u neemt, ongeacht of het direct, indirect, impliciet, of anderszins is.

#### 9.2 DERDEN

Afhankelijk van de precieze configuratie en implementatie, kan het pakket in sommige gevallen communiceren en informatie delen met derden. Deze informatie kan in sommige contexten door sommige rechtsgebieden worden gedefinieerd als "[persoonsgegevens](https://nl.wikipedia.org/wiki/Persoonsgegevens)".

Hoe deze informatie door deze derden kan worden gebruikt, is onderworpen aan de verschillende beleidsregels uiteengezet door deze derden, en valt buiten het bestek van deze documentatie. In al dergelijke gevallen echter, het delen van informatie met deze derden kan worden uitgeschakeld. In al dergelijke gevallen, als u ervoor kiest om het in te schakelen, is het uw verantwoordelijkheid om eventuele zorgen die u heeft met betrekking tot de privacy, veiligheid, en gebruik van persoonsgegevens door deze derden te onderzoeken. Als er twijfels bestaan, of als u niet tevreden bent met het gedrag van deze derden met betrekking tot persoonsgegevens, is het wellicht het beste om het delen van informatie met deze derden uit te schakelen.

Met het oog op transparantie wordt het type informatie dat wordt gedeeld en met wie, hieronder beschreven.

##### 9.2.0 HOSTNAAM LOOKUPS

Als u functies of modules gebruikt die bedoeld zijn om met hostnamen te werken (zoals de "slechte hosts blokkermodule", "tor project exit nodes block module", of "zoekmachine verificatie", bijvoorbeeld), moet CIDRAM in staat zijn om de hostnaam van inkomende verzoeken op de een of andere manier. Dit gebeurt meestal door de hostnaam van het IP-adres van inkomende verzoeken van een DNS-server op te vragen, of door de informatie op te vragen via functionaliteit die wordt geboden door het systeem waarop CIDRAM is geïnstalleerd (dit wordt meestal een "hostnaam lookup" verwezen naar). De DNS-servers die standaard worden gedefinieerd, behoren tot de [Google DNS](https://dns.google.com/)-service (maar dit kan eenvoudig via de configuratie worden gewijzigd). De exacte services waarmee wordt gecommuniceerd, kunnen worden geconfigureerd en zijn afhankelijk van de manier waarop u het pakket configureert. In het geval dat u functionaliteit gebruikt die wordt geboden door het systeem waarop CIDRAM is geïnstalleerd, moet u contact opnemen met uw systeembeheerder om te bepalen naar welke routes hostnaam lookups moeten worden gebruikt. Hostnaam lookups kunnen worden voorkomen in CIDRAM door de betreffende modules te vermijden of door de pakketconfiguratie aan te passen aan uw behoeften.

*Relevante configuratie-opties:*
- `general` -> `allow_gethostbyaddr_lookup`
- `general` -> `default_dns`
- `general` -> `force_hostname_lookup`
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.1 VERIFICATIE VAN ZOEKMACHINES EN SOCIALE MEDIA

Wanneer verificatie van zoekmachines is ingeschakeld, probeert CIDRAM "forward DNS-lookups" uit te voeren om te verifiëren of verzoeken die claimen afkomstig te zijn van zoekmachines authentiek zijn. Hetzelfde, wanneer verificatie van sociale media is ingeschakeld, CIDRAM doet hetzelfde voor schijnbare verzoeken van sociale media. Hiertoe gebruikt het de [Google DNS](https://dns.google.com/)-service om IP-adressen van de hostnamen van deze inkomende verzoeken op te lossen (in dit proces worden de hostnamen van deze inkomende verzoeken gedeeld met de service).

*Relevante configuratie-opties:*
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.2 CAPTCHA

CIDRAM ondersteunt reCAPTCHA en hCAPTCHA. Ze nodig API-sleutels om correct te werken. Ze zijn standaard uitgeschakeld, maar kunnen worden ingeschakeld door de vereiste API-sleutels te configureren. Indien ingeschakeld, kan er communicatie plaatsvinden tussen de service en CIDRAM of de browser van de gebruiker. Dit kan mogelijk informatie overbrengen zoals het IP-adres van de gebruiker, de user-agent, het besturingssysteem, en andere details die beschikbaar zijn voor het verzoek.

##### 9.2.3 STOP FORUM SPAM

[Stop Forum Spam](https://www.stopforumspam.com/) is een fantastische, vrij beschikbare service die kan helpen forums, blogs, en websites van spammers te beschermen. Het doet dit door een database van bekende spammers aan te bieden, en een API die kan worden gebruikt om te controleren of een IP-adres, gebruikersnaam, of e-mailadres in de database wordt vermeld.

CIDRAM biedt een optionele module die gebruikmaakt van deze API om te controleren of het IP-adres van inkomende verzoeken bij een verdachte spammer hoort. Wanneer de module is geïnstalleerd en geactiveerd, kunnen de gebruikers IP-adressen worden gedeeld met de service in overeenstemming met de configuratie en het beoogde doel van de module.

##### 9.2.4 ABUSEIPDB

CIDRAM biedt een optionele module om misbruik van IP-adressen te blokkeren met behulp van de [AbuseIPDB](https://www.abuseipdb.com/) API. Wanneer de module is geïnstalleerd en geactiveerd, kunnen de gebruikers IP-adressen worden gedeeld met de service in overeenstemming met de configuratie en het beoogde doel van de module.

##### 9.2.5 BGPVIEW, IP-API

CIDRAM biedt optionele modules voor het uitvoeren van ASN en landcode zoekopdrachten met behulp van de [BGPView](https://bgpview.io/) API en de [IP-API](https://ip-api.com/) API. Deze zoekopdrachten bieden de mogelijkheid om verzoeken te blokkeren of op de witte lijst te zetten op basis van hun ASN of land van herkomst. Wanneer een van deze is geïnstalleerd en geactiveerd, kunnen de gebruikers IP-adressen worden gedeeld met de service in overeenstemming met de configuratie en het beoogde doel van de module.

##### 9.2.6 PROJECT HONEYPOT

CIDRAM biedt een optionele module om misbruik van IP-adressen te blokkeren met behulp van de [Project Honeypot](https://www.projecthoneypot.org/) API. Wanneer de module is geïnstalleerd en geactiveerd, kunnen de gebruikers IP-adressen worden gedeeld met de service in overeenstemming met de configuratie en het beoogde doel van de module.

#### 9.3 LOGGEN

Te loggen is om een aantal redenen een belangrijk onderdeel van CIDRAM. Het kan moeilijk zijn om valse positieven te diagnosticeren en op te lossen wanneer de blokgebeurtenissen die deze veroorzaken niet worden vastgelegd. Zonder blokgebeurtenissen te loggen, kan het moeilijk zijn om precies vast te stellen hoe performant CIDRAM zich in een bepaalde context bevindt, en het kan moeilijk zijn om te bepalen waar zijn tekortkomingen kunnen zijn, en welke veranderingen nodig kunnen zijn voor de configuratie of signatures dienovereenkomstig, zodat het blijft functioneren zoals bedoeld. Ongeacht, loggen is misschien niet wenselijk voor alle gebruikers, en blijft volledig optioneel. In CIDRAM te loggen is standaard uitgeschakeld. Om dit in te schakelen, moet CIDRAM dienovereenkomstig worden geconfigureerd.

Ook, als te loggen wettelijk toegestaan is, en voor zover dat wettelijk toegestaan is (bijvoorbeeld, de soorten informatie die kan worden vastgelegd, voor hoelang, en onder welke omstandigheden), kan variëren, afhankelijk van het rechtsgebied en de context waarin CIDRAM wordt geïmplementeerd (bijvoorbeeld, of u als een individu, als een bedrijf, en op commerciële of niet-commerciële basis opereert). Het kan daarom nuttig zijn om dit gedeelte zorgvuldig door te lezen.

CIDRAM kan informatie op verschillende manieren loggen, wat verschillende soorten informatie inhoudt, om verschillende redenen.

##### 9.3.0 BLOKGEBEURTENISSEN

Het primaire type loggen dat CIDRAM kan uitvoeren, heeft betrekking op "blokgebeurtenissen". Dit type loggen heeft betrekking op wanneer CIDRAM een aanvraag blokkeert, en kan in drie verschillende indelingen worden aangeboden:
- Door mensen leesbare logbestanden.
- Apache-stijl logbestanden.
- Geserialiseerde logbestanden.

Een blokgebeurtenis, vastgelegd in een door mensen leesbaar logbestand, ziet er meestal als volgt uit (bijvoorbeeld):

```
ID: 1234
Script Versie: CIDRAM v1.6.0
Datum/Tijd: Day, dd Mon 20xx hh:ii:ss +0000
IP-Adres: x.x.x.x
Hostname: dns.hostname.tld
Signatures Tellen: 1
Signatures Verwijzing: x.x.x.x/xx
Waarom Geblokkeerd: Cloud Service ("Netwerknaam", Lxx:Fx, [XX])!
User Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
Gereconstrueerde URI: https://your-site.tld/index.php
CAPTCHA State: Enabled.
```

Diezelfde blokgebeurtenis, geregistreerd in een Apache-stijl logbestand, ziet er ongeveer zo uit:

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

Een geregistreerde blokgebeurtenis bevat meestal de volgende informatie:
- Een ID-nummer dat verwijst naar de blokgebeurtenis.
- De versie van CIDRAM die momenteel wordt gebruikt.
- De datum en tijd waarop de blokgebeurtenis plaatsvond.
- Het IP-adres van het geblokkeerde verzoek.
- De hostnaam van het IP-adres van het geblokkeerde verzoek (indien beschikbaar).
- Het aantal signatures dat door het verzoek is geactiveerd.
- Verwijzingen naar de geactiveerd signatures.
- Verwijzingen naar de redenen voor de blokgebeurtenis, en enkele standaard, gerelateerde foutopsporingsinformatie.
- De user agent van het geblokkeerde verzoek (d.w.z., hoe de verzoekende entiteit zichzelf identificeerde bij het verzoek).
- Een reconstructie van de identifier voor de oorspronkelijk aangevraagde bron.
- De CAPTCHA state voor het huidige verzoek (indien relevant).

*De configuratie richtlijnen die verantwoordelijk zijn voor dit type loggen, en voor elk van de drie beschikbare indelingen, zijn:*
- `logging` -> `apache_style_log`
- `logging` -> `serialised_log`
- `logging` -> `standard_log`

Wanneer deze richtlijnen leeg worden gelaten, blijft dit type logboek uitgeschakeld.

##### 9.3.1 CAPTCHA LOGGEN

Dit type loggen heeft specifiek betrekking op CAPTCHA-instanties, en gebeurt alleen op wanneer een gebruiker een CAPTCHA-instantie probeert te voltooien.

Een CAPTCHA-logsinvoer bevat het IP-adres van de gebruiker die probeert een CAPTCHA-instantie te voltooien, de datum en tijd waarop de poging heeft plaatsgevonden, en de CAPTCHA state. Een CAPTCHA-logsinvoer ziet er meestal als volgt uit (bijvoorbeeld):

```
IP-Adres: x.x.x.x - Datum/Tijd: Day, dd Mon 20xx hh:ii:ss +0000 - CAPTCHA State: Succes!
```

*De configuratie richtlijn die verantwoordelijk is voor CAPTCHA loggen is:*
- `hcaptcha` -> `hcaptcha_log`
- `recaptcha` -> `recaptcha_log`

##### 9.3.2 FRONTEND LOGGEN

Dit type loggen is bedoeld voor pogingen om bij de frontend in te loggen, en gebeurt alleen op wanneer een gebruiker zich probeert in te loggen bij de frontend (ervan uitgaande dat de frontend-toegang is ingeschakeld).

Een frontend logsinvoer bevat het IP-adres van de gebruiker die probeert in te loggen, de datum en tijd waarop de poging heeft plaatsgevonden, en de resultaten van de poging (ingelogd succesvol of niet). Een frontend logsinvoer ziet er meestal als volgt uit (bijvoorbeeld):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Ingelogd.
```

*De configuratie-optie die verantwoordelijk is voor de frontend toegang te loggen is:*
- `frontend` -> `frontend_log`

##### 9.3.3 LOGROTATIE

Mogelijk wilt u logs na een bepaalde periode opschonen, of mogelijk bent u wettelijk verplicht (d.w.z., de hoeveelheid tijd die het wettelijk toelaatbaar is om logs te bewaren, kan bij wet beperkt zijn). U kunt dit bereiken door datum/tijd-markeringen op te nemen in de namen van uw logbestanden, zoals gespecificeerd door uw pakketconfiguratie (b.v., `{yyyy}-{mm}-{dd}.log`), en vervolgens logrotatie in te schakelen (logrotatie stelt u in staat om enige actie in logbestanden uit te voeren wanneer de gespecificeerde limieten worden overschreden).

Bijvoorbeeld: Als ik wettelijk verplicht was om logs na 30 dagen te verwijderen, kon ik `{dd}.log` opgeven in de namen van mijn logbestanden (`{dd}` verwijst naar de dagen), de waarde van `log_rotation_limit` op 30 zetten, en de waarde van `log_rotation_action` op `Delete` zetten.

Omgekeerd, als u verplicht bent om logs gedurende langere tijd te bewaren, kunt u überhaupt geen logrotatie gebruiken, of kunt u de waarde van `log_rotation_action` op `Archive` zetten, om logbestanden te comprimeren, waardoor de totale hoeveelheid schijfruimte die ze innemen, wordt verminderd.

*Relevante configuratie-opties:*
- `logging` -> `log_rotation_action`
- `logging` -> `log_rotation_limit`

##### 9.3.4 LOGTRUNCATIE

Het is ook mogelijk om afzonderlijke logbestanden af te kappen als ze een bepaalde grootte overschrijden, als dit iets is dat u misschien nodig heeft, of zou willen doen.

*Relevante configuratie-opties:*
- `logging` -> `truncate`

##### 9.3.5 IP-ADRES PSEUDONIMISATIE

Ten eerste, als u niet bekend bent met de term, "pseudonimisatie" verwijst naar de verwerking van persoonsgegevens als zodanig, zodat deze niet meer kan worden geïdentificeerd aan een specifieke persoon zonder aanvullende informatie, en op voorwaarde dat dergelijke aanvullende informatie afzonderlijk wordt bijgehouden en onderworpen wordt aan technische en organisatorische maatregelen om ervoor te zorgen dat persoonsgegevens niet kunnen worden geïdentificeerd aan een natuurlijke persoon.

De volgende bronnen kunnen helpen om het in meer detail uit te leggen:
- [[privacycompany.eu] Wat is het verschil tussen pseudonimiseren en anonimiseren van persoonsgegevens en wat zijn de gevolgen?](https://www.privacycompany.eu/blog-wat-is-het-verschil-tussen-pseudonimiseren-en-anonimiseren-van-persoonsgegevens-en-wat-zijn-de-gevolgen/)
- [[nen.nl] Pseudonimisatie](https://www.nen.nl/Normontwikkeling/Pseudonimisatie.htm)
- [[considerati.com] Anonimiseren en pseudonimiseren: wat is het verschil en wat is het belang ervan?](https://www.considerati.com/nl/publicaties/blog/anonimiseren-en-pseudonimiseren-wat-is-het-verschil-en-wat-is-het-belang-ervan/)
- [[Wikipedia] Pseudonimiseren](https://nl.wikipedia.org/wiki/Pseudonimiseren)

In sommige omstandigheden kan het wettelijk verplicht zijn om PII die is verzameld, verwerkt, of opgeslagen, te anonimiseren of te pseudonimiseren. Hoewel dit concept al geruime tijd bestaat, GDPR/DSGVO vermeldt, en moedigt specifiek "pseudonimisatie".

CIDRAM kan IP-adressen pseudonimiseren wanneer ze worden geregistreerd, als dit iets is dat u misschien nodig heeft, of zou willen doen. Wanneer CIDRAM IP-adressen pseudonimiseert, wanneer geregistreerd, het laatste octet van IPv4-adressen, en alles na het tweede deel van IPv6-adressen wordt weergegeven door een "x" (effectief afronding van IPv4-adressen naar het initiële adres van het 24e subnet waar ze in factoreren, en IPv6-adressen naar het initiële adres van het 32e subnet waar ze in factoreren).

*Notitie: Het pseudonimisatieproces van het IP-adres van CIDRAM heeft geen invloed op de IP-trackingfunctie van CIDRAM. Als dit een probleem voor u is, is het misschien het beste om IP-tracking volledig uit te schakelen.*

*Relevante configuratie-opties:*
- `legal` -> `pseudonymise_ip_addresses`

##### 9.3.6 HET WEGLATEN VAN LOGINFORMATIE

Als u nog een stap verder wilt gaan door te voorkomen dat specifieke soorten informatie volledig worden vastgelegd, is dit ook mogelijk. Raadpleeg op de configuratiepagina de configuratierichtlijn `fields` om te bepalen welke velden worden weergegeven in logboekvermeldingen en op de pagina "Toegang Geweigerd".

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

*Notitie: Er is geen reden om IP-adressen te pseudonimiseren wanneer ze volledig uit logs worden weggelaten.*

*Relevante configuratie-opties:*
- `general` -> `fields`

##### 9.3.7 STATISTIEKEN

CIDRAM is optioneel in staat om statistieken bij te houden, zoals het totale aantal blokgebeurtenissen of CAPTCHA-instanties die zijn opgetreden sinds een bepaald tijdstip. Deze functie is standaard uitgeschakeld, maar kan worden ingeschakeld via de pakketconfiguratie. Deze functie houdt alleen het totale aantal opgetreden gebeurtenissen bij en bevat geen informatie over specifieke gebeurtenissen (en moet daarom niet als PII worden beschouwd).

*Relevante configuratie-opties:*
- `general` -> `statistics`

##### 9.3.8 ENCRYPTIE

CIDRAM codeert de cache of logboekinformatie niet. [Encryptie](https://nl.wikipedia.org/wiki/Encryptie) voor de cache en logs kunnen in de toekomst worden geïntroduceerd, maar er zijn momenteel geen specifieke plannen voor. Als u zich zorgen maakt over ongeautoriseerde derden die toegang krijgen tot delen van CIDRAM die mogelijk PII of gevoelige informatie bevatten, zoals de cache of logbestanden, raad ik CIDRAM aan niet te installeren op een openbare locatie (b.v., installeer CIDRAM buiten de standaard `public_html` directory of gelijkwaardig daarvan beschikbaar voor de meeste standaard webservers) en dat de juiste beperkende machtigingen worden afgedwongen voor de directory waar deze zich bevindt (in het bijzonder, voor de vault directory). Als dat niet voldoende is om uw zorgen weg te nemen, configureer dan CIDRAM als zodanig dat de soorten informatie die uw zorgen veroorzaken, niet zullen worden verzameld of ingelogd (zoals door loggen uit te schakelen).

#### 9.4 COOKIES

CIDRAM zet [cookies](https://nl.wikipedia.org/wiki/Cookie_(internet)) op twee punten in zijn codebase. Ten eerste, wanneer een gebruiker een CAPTCHA-instantie met succes voltooit (en ervan uitgaande dat `lockuser` is ingesteld op `true`), CIDRAM stelt een cookie in om te kunnen onthouden voor volgende verzoeken dat de gebruiker al een CAPTCHA-instantie heeft voltooid, zodat het niet nodig zal zijn om de gebruiker continu te vragen een CAPTCHA-instantie bij volgende aanvragen in te vullen. Ten tweede, wanneer een gebruiker zich met succes ingelogd bij de frontend, stelt CIDRAM een cookie in om de gebruiker te kunnen onthouden voor volgende aanvragen (d.w.z., cookies worden gebruikt om de gebruiker te authenticeren voor een login-sessie).

In beide gevallen worden cookiewaarschuwingen prominent weergegeven (als het relevant is), waardoor de gebruiker wordt gewaarschuwd dat cookies worden ingesteld als deze zich bezighouden met de relevante acties. Cookies zijn niet ingesteld op andere punten in de codebase.

*Notitie: De "onzichtbare" CAPTCHA-API's zijn mogelijk incompatibel met de cookiewetgeving in sommige rechtsgebieden, en moet worden vermeden door websites die onder dergelijke wetgeving vallen. Kiezen om in plaats daarvan de andere meegeleverde API's te gebruiken, of gewoon CAPTCHA volledig uitschakelen, kan de voorkeur hebben.*

*Relevante configuratie-opties:*
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 9.5 MARKETING EN ADVERTEREN

CIDRAM verzamelt of verwerkt geen informatie voor marketing of advertentie doeleinden, en verkoopt of profiteert niet van verzamelde of geregistreerde informatie. CIDRAM is geen commerciële onderneming, en houdt geen verband met commerciële belangen, dus het zou geen zin hebben om deze dingen te doen. Dit is sinds het begin van het project het geval geweest, en is nog steeds het geval. Bovendien zou het doen van deze dingen contraproductief zijn ten opzichte van de geest en het beoogde doel van het project als geheel, en zolang ik het project blijf onderhouden, zal het nooit gebeuren.

#### 9.6 PRIVACYBELEID

In sommige omstandigheden kan het wettelijk verplicht zijn om duidelijk een link naar uw privacybeleid te tonen op alle pagina's en secties van uw website. Dit kan belangrijk zijn als middel om ervoor te zorgen dat gebruikers goed geïnformeerd zijn over uw exacte privacypraktijken, de soorten PII die u verzamelt, en hoe u van plan bent om het te gebruiken. Om een dergelijke link op de pagina "Toegang Geweigerd" van CIDRAM te kunnen opnemen, wordt een configuratie-optie verstrekt om de URL van uw privacybeleid op te geven.

*Notitie: Het wordt ten zeerste aanbevolen dat uw pagina met privacybeleid niet achter de bescherming van CIDRAM wordt geplaatst. Als CIDRAM uw privacybeleid pagina beschermt, en een door CIDRAM geblokkeerde gebruiker op de koppeling naar uw privacybeleid klikt, worden ze gewoon opnieuw geblokkeerd, en kunnen ze uw privacybeleid niet zien. Idealiter moet u een koppeling maken naar een statische kopie van uw privacybeleid, zoals een HTML-pagina of een niet-gecodeerd bestand dat niet door CIDRAM wordt beschermd.*

*Relevante configuratie-opties:*
- `legal` -> `privacy_policy`

#### 9.7 GDPR/DSGVO/AVG

De Algemene Verordening Gegevensbescherming (AVG, of GDPR/DSGVO) is een verordening van de Europese Unie, die met ingang van 25 Mei 2018 in werking treedt. Het primaire doel van de verordening is om burgers en inwoners van de EU controle te geven over hun eigen persoonsgegevens, en om regelgeving binnen de EU te verenigen met betrekking tot privacy en persoonsgegevens.

De verordening bevat specifieke bepalingen met betrekking tot de verwerking van "[persoonsgegevens](https://nl.wikipedia.org/wiki/Persoonsgegevens)" (PII) van alle "betrokkenen" (elke geïdentificeerde of identificeerbare natuurlijke persoon) vanuit of binnen de EU. Om aan de regelgeving te voldoen, moeten "ondernemingen" (zoals bepaald door de verordening), en alle relevante systemen en processen moeten standaard "[privacy by design](https://autoriteitpersoonsgegevens.nl/nl/zelf-doen/privacycheck/privacy-design)" implementeren, moet de hoogst mogelijke privacy-instellingen gebruiken, moet de nodige waarborgen implementeren voor alle opgeslagen of verwerkte informatie (inclusief, maar niet beperkt tot, de implementatie van pseudonimisering of volledige anonimisering van gegevens), moet duidelijk en ondubbelzinnig verklaren welke soorten gegevens zij verzamelen, hoe zij deze verwerken, om welke redenen, hoe lang zij deze bewaren, en of zij deze gegevens delen met derden, de soorten gegevens die met derden worden gedeeld, hoe, waarom, enzovoort.

Gegevens worden mogelijk niet verwerkt tenzij er een wettelijke basis is om dit te doen, zoals bepaald door de verordening. In het algemeen betekent dit dat om de gegevens van een betrokkene op een wettige basis te verwerken, dit moet worden gedaan in overeenstemming met wettelijke verplichtingen, of alleen moet worden gedaan nadat de betrokkene expliciete, goed geïnformeerde, ondubbelzinnige toestemming heeft verkregen.

Omdat aspecten van de verordening in de loop van de tijd kunnen evolueren, om de verspreiding van verouderde informatie te voorkomen, is het wellicht beter om de verordening te leren van een gezaghebbende bron, in tegenstelling tot het simpelweg opnemen van de relevante informatie hier in de documentatie van het pakket (die uiteindelijk verouderd kan raken naarmate de regelgeving evolueert).

[EUR-Lex](https://eur-lex.europa.eu/) (een deel van de officiële website van de Europese Unie dat informatie biedt over EU-wetgeving) biedt uitgebreide informatie over GDPR/DSGVO/AVG, beschikbaar in 24 verschillende talen (op het moment dat dit wordt geschreven), en beschikbaar om te downloaden in PDF-formaat. Ik zou zeker aanraden om de informatie die ze bieden te lezen, om meer te leren over GDPR/DSGVO/AVG:
- [VERORDENING (EU) 2016/679 VAN HET EUROPEES PARLEMENT EN DE RAAD](https://eur-lex.europa.eu/legal-content/NL/TXT/?uri=celex:32016R0679)

Als alternatief is er een kort (niet-gezaghebbende) overzicht van GDPR/DSGVO/AVG beschikbaar op Wikipedia:
- [Algemene verordening gegevensbescherming](https://nl.wikipedia.org/wiki/Algemene_verordening_gegevensbescherming)

---


### 10. <a name="SECTION10"></a>UPGRADEN VAN EERDERE HOOFDVERSIES

#### 10.0 CIDRAM v3

Er zijn aanzienlijke verschillen tussen v3 en eerdere hoofdversies. Belangrijk is dat de manier waarop ingangspunten werken, de manier waarop modules zijn gestructureerd, en de manier waarop de updater werkt voor v3 anders is dan de manier waarop die dingen werkten voor eerdere hoofdversies. Vanwege deze verschillen is het uitvoeren van een nieuwe installatie de beste manier om te upgraden naar v3 van eerdere hoofdversies.

Als u uw configuratie en uw aanvullende regels wilt behouden, gaat u voordat u met het upgradeproces begint naar de front-end back-up-pagina. Van daaruit kunnen configuratie en aanvullende regels worden geëxporteerd. Bij het exporteren wordt een bestand gedownload. Na het upgraden naar de nieuwe hoofdversie kan dat bestand worden gebruikt om de eerder geëxporteerde gegevens naar de installatie te importeren.

Vanwege wijzigingen in de manier waarop modules zijn gestructureerd, zouden modules die bedoeld waren voor eerdere hoofdversies moeten worden herschreven om correct te werken voor v3. Directe migratie werkt niet. Hetzelfde geldt voor evenementen.

De manier waarop signatuurbestanden zijn gestructureerd, is niet veranderd, dus signatuurbestanden die bedoeld zijn voor eerdere hoofdversies kunnen zonder problemen rechtstreeks naar v3 worden gemigreerd.

Een nieuwe toevoeging sinds v3, modules, signatuurbestanden, en gebeurtenissen hebben elk hun eigen speciale mappen (dus voor v3 zouden ze elk naar hun respectievelijke speciale mappen gaan, in plaats van naar de root van de vault).

Sommige signatuurbestanden, modules, en blokkeerlijsten die openbaar beschikbaar waren voor eerdere hoofdversies, zijn verouderd, dus niet alles zal beschikbaar zijn voor v3. In de meeste gevallen zullen ze toch niet nodig zijn, vanwege nieuwe functies en kernfunctionaliteit die zijn toegevoegd sinds v3.

Er zijn enkele subtiele wijzigingen in de manier waarop aanvullende regels zijn gestructureerd en er zijn wijzigingen in de configuratie, maar als u de import/export functie op de front-end back-up-pagina gebruikt, hoeft u niets handmatig te herschrijven, aan te passen, of opnieuw te maken. Bij het importeren weet CIDRAM wat er nodig is en regelt het automatisch voor u.

#### 10.1 CIDRAM v4

CIDRAM v4 bestaat nog niet. Wanneer het echter tijd is om te upgraden van v3 naar v4, zou het upgradeproces veel eenvoudiger moeten zijn. We zullen niet precies weten hoeveel verschil het zal zijn tot de tijd daar is, maar ik verwacht dat de verschillen veel kleiner zullen zijn dan voorheen, en mechanismen zijn vanaf het begin al in v3 geïmplementeerd om een soepeler upgradeproces te vergemakkelijken. Zolang er geen significante wijzigingen zijn in de updater of de manier waarop ingangspunten werken, zou het in theorie mogelijk moeten zijn om volledig via de front-end te upgraden, zonder dat een nieuwe installatie nodig is.

Meer gedetailleerde informatie zal hier, in de documentatie, te zijner tijd in de toekomst worden opgenomen.

---


Laatste Bijgewerkt: 3 Juli 2024 (2024.07.03).
