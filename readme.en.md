## Documentation for CIDRAM v3 (English).

### Contents
- 1. [PREAMBLE](#user-content-SECTION1)
- 2. [HOW TO INSTALL](#user-content-SECTION2)
- 3. [HOW TO USE](#user-content-SECTION3)
- 4. [FRONT-END MANAGEMENT](#user-content-SECTION4)
- 5. [CONFIGURATION OPTIONS](#user-content-SECTION5)
- 6. [SIGNATURE FORMAT](#user-content-SECTION6)
- 7. [KNOWN COMPATIBILITY PROBLEMS](#user-content-SECTION7)
- 8. [FREQUENTLY ASKED QUESTIONS (FAQ)](#user-content-SECTION8)
- 9. [LEGAL INFORMATION](#user-content-SECTION9)
- 10. [UPGRADING FROM PREVIOUS MAJOR VERSIONS](#user-content-SECTION10)

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### 1. <a name="SECTION1"></a>PREAMBLE

CIDRAM (Classless Inter-Domain Routing Access Manager) is a PHP script designed to protect websites by blocking requests originating from IP addresses regarded as being sources of undesirable traffic, including (but not limited to) traffic from non-human access endpoints, cloud services, spambots, scrapers, etc. It does this by calculating the possible CIDRs of the IP addresses supplied from inbound requests and then attempting to match these possible CIDRs against its signature files (these signature files contain lists of CIDRs of IP addresses regarded as being sources of undesirable traffic); If matches are found, the requests are blocked.

*(See: [What is a "CIDR"?](#user-content-WHAT_IS_A_CIDR)).*

[CIDRAM](https://cidram.github.io/) COPYRIGHT 2016 and beyond GNU/GPLv2 by [Caleb M (Maikuolan)](https://github.com/Maikuolan).

This script is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version. This script is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details, located in the `LICENSE.txt` file and available also from:
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

This document and its associated package can be downloaded for free from:
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [SourceForge](https://sourceforge.net/projects/cidram/).

---


### 2. <a name="SECTION2"></a>HOW TO INSTALL

#### 2.0 INSTALLING MANUALLY

Firstly, you'll need a fresh copy of CIDRAM to work with. You can download an archive of the latest version of CIDRAM from the [CIDRAM/CIDRAM](https://github.com/CIDRAM/CIDRAM) repository. Specifically, you'll need a fresh copy of the "vault" directory (everything from the archive other than the "vault" directory and its contents can be safely deleted or disregarded).

Prior to v3, it was necessary to install CIDRAM somewhere within your public root in order to be able to access the CIDRAM front-end. However, from v3 onwards, that isn't necessary, and in order to maximise security and to prevent unauthorised access to CIDRAM and its files, it's recommended instead to install CIDRAM *outside* your public root. It doesn't particularly matter exactly where you choose to install CIDRAM, as long as it's somewhere accessible by PHP, somewhere reasonably secure, and somewhere you're happy with. It's also not necessary to maintain the name of the "vault" directory anymore, so you can rename "vault" to whatever name you'd prefer (but for the sake of convenience, the documentation will continue to refer to it as the "vault" directory).

When you're ready, upload the "vault" directory to your chosen location, and ensure that it has the permissions necessary in order for PHP to be able to write to the directory (depending on the system in question, sometimes you won't need to do anything, or sometimes you'll need to set CHMOD 755 to the directory, or if there are problems with 755, you can try 777, but 777 isn't recommended due to being less secure).

Next, in order for CIDRAM to be able to protect your codebase or CMS, you'll need to create an "entrypoint". Such an entrypoint consists of three things:

1. Inclusion of the "loader.php" file at an appropriate point in your codebase or CMS.
2. Instantiation of the CIDRAM core.
3. Calling the "protect" method.

A simple example:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

If you're using an Apache webserver and have access to `php.ini`, you can use the `auto_prepend_file` directive to prepend CIDRAM whenever any PHP request is made. In such a case, the most appropriate place to create your entrypoint would be in its own file, and you would then cite that file at the `auto_prepend_file` directive.

Example:

`auto_prepend_file = "/path/to/your/entrypoint.php"`

Or this in the `.htaccess` file:

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

In other cases, the most appropriate place to create your entrypoint would be at the earliest point possible within your codebase or CMS to always be loaded whenever someone accesses any page across your entire website. If your codebase utilises a "bootstrap", a good example would be at the very beginning of your "bootstrap" file. If your codebase has a central file responsible for connecting to your database, another good example would be at the very beginning of that central file.

#### 2.1 INSTALLING WITH COMPOSER

[CIDRAM is registered with Packagist](https://packagist.org/packages/cidram/cidram), and so, if you're familiar with Composer, you can use Composer to install CIDRAM.

`composer require cidram/cidram`

#### 2.2 INSTALLING FOR WORDPRESS

[CIDRAM is registered as a plugin with the WordPress plugins database](https://wordpress.org/plugins/cidram/), and you can install CIDRAM directly from the plugins dashboard. You can install it in the same manner as any other plugin, and no addition steps are required.

*Warning: Updating CIDRAM via the plugins dashboard results in a clean installation! If you've customised your installation (changed your configuration, installed modules, etc), these customisations will be lost when updating via the plugins dashboard! Logfiles will also be lost when updating via the plugins dashboard! To preserve logfiles and customisations, update via the CIDRAM front-end updates page.*

#### 2.3 CONFIGURATION AND CUSTOMISATION

It's strongly recommended for you to review the configuration of your new installation in order for you to be able to adjust it according to your needs. You may also want to install additional modules, signature files, create auxiliary rules, or implement other customisations in order for your installation to be able to best suit your needs. I recommend using the front-end to do these things.

---


### 3. <a name="SECTION3"></a>HOW TO USE

CIDRAM should automatically block undesirable requests to your website without requiring any manual assistance, aside from its initial installation.

You can customise your configuration and customise which CIDRs are blocked by modifying your configuration file and/or your signature files.

If you encounter any false positives, please contact me to let me know about it. *(See: [What is a "false positive"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM can be updated manually or via the front-end. CIDRAM can also be updated via Composer or WordPress, if originally installed via those means.

---


### 4. <a name="SECTION4"></a>FRONT-END MANAGEMENT

#### 4.0 WHAT IS THE FRONT-END.

The front-end provides a convenient and easy way to maintain, manage, and update your CIDRAM installation. You can view, share, and download logfiles via the logs page, you can modify configuration via the configuration page, you can install and uninstall components via the updates page, and you can upload, download, and modify files in your vault via the file manager.

#### 4.1 HOW TO ACCESS THE FRONT-END.

Similar to how you needed to create an entrypoint in order for CIDRAM to protect your website, you'll also need to create an entrypoint in order to access the front-end. Such an entrypoint consists of three things:

1. Inclusion of the "loader.php" file at an appropriate point in your codebase or CMS.
2. Instantiation of the CIDRAM front-end.
3. Calling the "view" method.

A simple example:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

The "FrontEnd" class extends the "Core" class, meaning that if you want, you can call the "protect" method before calling the "view" method in order to block potentially unwanted traffic from accessing the front-end. Doing so is entirely optional.

A simple example:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

The most appropriate place to create an entrypoint for the front-end is in its own dedicated file. Unlike your previously created entrypoint, you want your front-end entrypoint to be accessible only by requesting directly for the specific file where the entrypoint exists, so in this case, you won't want to use `auto_prepend_file` or `.htaccess`.

After having created your front-end entrypoint, use your browser to access it. You should be presented with a login page. At the login page, enter the default username and password (admin/password) and press the login button.

Note: After you've logged in for the first time, in order to prevent unauthorised access to the front-end, you should immediately change your username and password! This is very important, because it's possible to upload arbitrary PHP code to your website via the front-end.

Also, for optimal security, enabling "two-factor authentication" for all front-end accounts is strongly recommended (instructions provided below).

#### 4.2 HOW TO USE THE FRONT-END.

Instructions are provided on each page of the front-end, to explain the correct way to use it and its intended purpose. If you need further explanation or any special assistance, please contact support. Alternatively, there are some videos available on YouTube which could help by way of demonstration.

#### 4.3 TWO-FACTOR AUTHENTICATION

It's possible to make the front-end more secure by enabling two-factor authentication ("2FA"). When logging into a 2FA-enabled account, an email is sent to the email address associated with that account. This email contains a "2FA code", which the user must then enter, in addition to the username and password, in order to be able to log in using that account. This means that obtaining an account password would not be enough for any hacker or potential attacker to be able to log into that account, as they would also need to already have access to the email address associated with that account in order to be able to receive and utilise the 2FA code associated with the session, thus making the front-end more secure.

Firstly, to enable two-factor authentication, using the front-end updates page, install the PHPMailer component. CIDRAM utilises PHPMailer for sending emails.

After you've installed PHPMailer, you'll need to populate the configuration directives for PHPMailer via the CIDRAM configuration page or configuration file. More information about these configuration directives is included in the configuration section of this document. After you've populated the PHPMailer configuration directives, set `enable_two_factor` to `true`. Two-factor authentication should now be enabled.

Next, you'll need to associate an email address with an account, so that CIDRAM knows where to send 2FA codes when logging in with that account. To do this, use the email address as the username for the account (like `foo@bar.tld`), or include the email address as part of the username in the same way that you would when sending an email normally (like `Foo Bar <foo@bar.tld>`).

Note: Protecting your vault against unauthorised access (e.g., by hardening your server's security and public access permissions), is particularly important here, due to that unauthorised access to your configuration file (which is stored in your vault), could risk exposing your outbound SMTP settings (including SMTP username and password). You should ensure that your vault is properly secured before enabling two-factor authentication. If you're unable to do this, then at least, you should create a new email account, dedicated for this purpose, as such to reduce the risks associated with exposed SMTP settings.

---


### 5. <a name="SECTION5"></a>CONFIGURATION OPTIONS

The following is a list of the directives available to CIDRAM in the `config.yml` configuration file, along with a description of the purpose of these directives.

```
Configuration (v3)
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
│       pdo_dsn [string]
│       pdo_username [string]
│       pdo_password [string]
└───bypasses
        used [string]
```

#### "general" (Category)
General configuration (any core configuration not belonging to other categories).

##### "stages" `[string]`
- Controls for the stages of the execution chain (whether enabled, whether errors are logged, etc).

```
stages
├─Tests ("Execute signature files tests")
├─Modules ("Execute modules")
├─SearchEngineVerification ("Execute search engine verification")
├─SocialMediaVerification ("Execute social media verification")
├─OtherVerification ("Execute other verification")
├─Aux ("Execute auxiliary rules")
├─Reporting ("Execute reporting")
├─Tracking ("Execute IP tracking")
├─RL ("Execute rate limiting")
├─CAPTCHA ("Deploy CAPTCHAs (blocked requests)")
├─Statistics ("Update statistics")
├─Webhooks ("Execute webhooks")
├─PrepareFields ("Prepare fields for output and logs")
├─Output ("Generate output (blocked requests)")
├─WriteLogs ("Write to logs (blocked requests)")
├─Terminate ("Terminate the request (blocked requests)")
├─AuxRedirect ("Redirect according to auxiliary rules")
└─NonBlockedCAPTCHA ("Deploy CAPTCHAs (non-blocked requests)")
```

##### "fields" `[string]`
- Controls for the fields during block events (when a request is blocked).

```
fields
├─ID ("ID")
├─ScriptIdent ("Script version")
├─DateTime ("Date/Time")
├─IPAddr ("IP address")
├─IPAddrResolved ("IP address (resolved)")
├─Query ("Query")
├─Referrer ("Referrer")
├─UA ("User agent")
├─UALC ("User agent (lower-case)")
├─SignatureCount ("Signatures count")
├─Signatures ("Signatures reference")
├─WhyReason ("Why blocked")
├─ReasonMessage ("Why blocked (detailed)")
├─rURI ("Reconstructed URI")
├─Infractions ("Infractions")
├─ASNLookup ("** ASN lookup")
├─CCLookup ("** Country code lookup")
├─Verified ("Verified identity")
├─Expired ("Expired")
├─Ignored ("Ignored")
├─Request_Method ("Request method")
├─Protocol ("Protocol")
├─Hostname ("Hostname")
├─CAPTCHA ("CAPTCHA state")
└─Inspection ("* Conditions inspection")
```

* Intended only for debugging auxiliary rules. Not displayed to blocked users.

** Requires ASN lookup functionality (e.g., via the IP-API or BGPView module).

##### "timezone" `[string]`
- This is used to specify the timezone to use (e.g., Africa/Cairo, America/New_York, Asia/Tokyo, Australia/Perth, Europe/Berlin, Pacific/Guam, etc). Specify "SYSTEM" to let PHP handle this for you automatically.

```
timezone
├─SYSTEM ("Use system default timezone.")
├─UTC ("UTC")
└─…Other
```

##### "time_offset" `[int]`
- Timezone offset in minutes.

##### "time_format" `[string]`
- The date/time notation format used by CIDRAM. Additional options may be added upon request.

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
└─…Other
```

##### "ipaddr" `[string]`
- Where to find the IP address of connecting requests? (Useful for services such as Cloudflare and the likes). Default = REMOTE_ADDR. WARNING: Don't change this unless you know what you're doing!

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (Default)")
└─…Other
```

See also:
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### "http_response_header_code" `[int]`
- Which HTTP status message should CIDRAM send when blocking requests?

```
http_response_header_code
├─200 (200 OK): Least robust, but most user-friendly. Automated requests will most likely
│ interpret this response as indication that the request was successful.
├─403 (403 Forbidden): More robust, but less user-friendly. Recommended for most general
│ circumstances.
├─410 (410 Gone): Could cause problems when resolving false positives, because some browsers
│ will cache this status message and not send subsequent requests, even after
│ having been unblocked. May be the most preferable in some contexts, for
│ certain kinds of traffic.
├─418 (418 I'm a teapot): References an April Fools' joke ({{Links.RFC2324}}). Very unlikely to be
│ understood by any client, bot, browser, or otherwise. Provided for amusement
│ and convenience, but not generally recommended.
├─451 (451 Unavailable For Legal Reasons): Recommended when blocking primarily for legal reasons. Not recommended in
│ other contexts.
└─503 (503 Service Unavailable): Most robust, but least user-friendly. Recommended for when under attack, or
  for when dealing with extremely persistent unwanted traffic.
```

##### "silent_mode" `[string]`
- Should CIDRAM silently redirect blocked access attempts instead of displaying the "access denied" page? If yes, specify the location to redirect blocked access attempts to. If no, leave this variable blank.

##### "silent_mode_response_header_code" `[int]`
- Which HTTP status message should CIDRAM send when silently redirecting blocked access attempts?

```
silent_mode_response_header_code
├─301 (301 Moved Permanently): Instructs the client that the redirect is PERMANENT, and that the request
│ method used for the redirect MAY be different than the request method used
│ for the initial request.
├─302 (302 Found): Instructs the client that the redirect is TEMPORARY, and that the request
│ method used for the redirect MAY be different than the request method used
│ for the initial request.
├─307 (307 Temporary Redirect): Instructs the client that the redirect is TEMPORARY, and that the request
│ method used for the redirect may NOT be different than the request method
│ used for the initial request.
└─308 (308 Permanent Redirect): Instructs the client that the redirect is PERMANENT, and that the request
  method used for the redirect may NOT be different than the request method
  used for the initial request.
```

No matter how we instruct the client, it's important to remember that we ultimately have no control over what the client chooses to do, and there's zero guarantee that the client will honour our instructions.

##### "lang" `[string]`
- Specify the default language for CIDRAM.

```
lang
├─ar ("العربية")
├─bg ("Български")
├─bn ("বাংলা")
├─cs ("Čeština")
├─de ("Deutsch")
├─en ("English (AU/GB/NZ)")
├─en-US ("English (US)")
├─es ("Español")
├─fa ("فارسی")
├─fr ("Français")
├─he ("עברית")
├─hi ("हिंदी")
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
├─pt ("Português (Brasil)")
├─pt-PT ("Português (Europeu)")
├─ru ("Русский")
├─sv ("Svenska")
├─ta ("தமிழ்")
├─th ("ภาษาไทย")
├─tr ("Türkçe")
├─uk ("Українська")
├─ur ("اردو")
├─vi ("Tiếng Việt")
├─zh ("中文（简体）")
└─zh-TW ("中文（傳統）")
```

##### "lang_override" `[bool]`
- Localise according to HTTP_ACCEPT_LANGUAGE whenever possible? True = Yes [Default]; False = No.

##### "numbers" `[string]`
- How do you prefer numbers to be displayed? Select the example that looks the most correct to you.

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
- If you wish, you can supply an email address here to be given to users when they're blocked, for them to use as a point of contact for support and/or assistance for in the event of them being blocked mistakenly or in error. WARNING: Whatever email address you supply here will most certainly be acquired by spambots and scrapers during the course of its being used here, and so, it's strongly recommended that if you choose to supply an email address here, that you ensure that the email address you supply here is a disposable address and/or an address that you don't mind being spammed (in other words, you probably don't want to use your primary personal or primary business email addresses).

##### "emailaddr_display_style" `[string]`
- How would you prefer the email address to be presented to users?

```
emailaddr_display_style
├─default ("Clickable link")
└─noclick ("Non-clickable text")
```

##### "ban_override" `[int]`
- Override "http_response_header_code" when "infraction_limit" is exceeded? 200 = Don't override [Default]. Other values are the same as the available values for "http_response_header_code".

```
ban_override
├─200 (200 OK): Least robust, but most user-friendly. Automated requests will most likely
│ interpret this response as indication that the request was successful.
├─403 (403 Forbidden): More robust, but less user-friendly. Recommended for most general
│ circumstances.
├─410 (410 Gone): Could cause problems when resolving false positives, because some browsers
│ will cache this status message and not send subsequent requests, even after
│ having been unblocked. May be the most preferable in some contexts, for
│ certain kinds of traffic.
├─418 (418 I'm a teapot): References an April Fools' joke ({{Links.RFC2324}}). Very unlikely to be
│ understood by any client, bot, browser, or otherwise. Provided for amusement
│ and convenience, but not generally recommended.
├─451 (451 Unavailable For Legal Reasons): Recommended when blocking primarily for legal reasons. Not recommended in
│ other contexts.
└─503 (503 Service Unavailable): Most robust, but least user-friendly. Recommended for when under attack, or
  for when dealing with extremely persistent unwanted traffic.
```

##### "default_dns" `[string]`
- A list of DNS servers to use for hostname lookups. WARNING: Don't change this unless you know what you're doing!

__FAQ.__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.en.md#what-can-i-use-for-default_dns" hreflang="en-AU">What can I use for "default_dns"?</a></em>

##### "default_algo" `[string]`
- Defines which algorithm to use for all future passwords and sessions.

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### "statistics" `[string]`
- Controls which statistical information to track.

```
statistics
├─Blocked-IPv4 ("Requests blocked – IPv4")
├─Blocked-IPv6 ("Requests blocked – IPv6")
├─Blocked-Other ("Requests blocked – Other")
├─Banned-IPv4 ("Requests banned – IPv4")
├─Banned-IPv6 ("Requests banned – IPv6")
├─Passed-IPv4 ("Requests passed – IPv4")
├─Passed-IPv6 ("Requests passed – IPv6")
├─Passed-Other ("Requests passed – Other")
├─CAPTCHAs-Failed ("CAPTCHA attempts – Failed!")
├─CAPTCHAs-Passed ("CAPTCHA attempts – Passed!")
├─Reported-IPv4-OK ("Requests reported to external APIs – IPv4 – OK")
├─Reported-IPv4-Failed ("Requests reported to external APIs – IPv4 – Failed")
├─Reported-IPv6-OK ("Requests reported to external APIs – IPv6 – OK")
└─Reported-IPv6-Failed ("Requests reported to external APIs – IPv6 – Failed")
```

##### "force_hostname_lookup" `[bool]`
- Force hostname lookups? True = Yes; False = No [Default]. Hostname lookups are normally performed on an "as needed" basis, but can be forced for all requests. Doing so may be useful as a means of providing more detailed information in the log files, but may also have a slightly negative effect on performance.

##### "allow_gethostbyaddr_lookup" `[bool]`
- Allow gethostbyaddr lookups when UDP is unavailable? True = Yes [Default]; False = No.

Note: IPv6 lookups mightn't work correctly on some 32-bit systems.

##### "disabled_channels" `[string]`
- This can be used to prevent CIDRAM from using particular channels when sending requests (e.g., when updating, when fetching component metadata, etc).

```
disabled_channels
├─GitHub ("GitHub")
├─BitBucket ("BitBucket")
└─GoogleDNS ("GoogleDNS")
```

##### "default_timeout" `[int]`
- Default timeout to use for external requests? Default = 12 seconds.

##### "sensitive" `[string]`
- A list of paths to regard as sensitive pages. Each path listed will be checked against the reconstructed URI when needed. A path which begins with a forward slash will be treated as a literal, and matched from the path component of the request onward. Otherwise, a path which begins with a non-alphanumeric character, and ends with that same character (or that same character plus an optional "i" flag) will be treated as a regular expression. Any other kind of path will be treated as a literal, and can match from any part of the URI. Whether a path is regarded as a sensitive page may affect how some modules behave, but doesn't have any effect otherwise.

#### "components" (Category)
Configuration for the activation and the deactivation of the components used by CIDRAM. Typically populated by the updates page, but can also be managed from here for finer control and for custom components not recognised by the updates page.

##### "ipv4" `[string]`
- IPv4 signature files.

##### "ipv6" `[string]`
- IPv6 signature files.

##### "modules" `[string]`
- Modules.

##### "imports" `[string]`
- Imports. Typically used to supply a component's configuration information to CIDRAM.

##### "events" `[string]`
- Event handlers. Typically used to modify the way CIDRAM behaves internally or to provide additional functionality.

#### "logging" (Category)
Configuration related to logging (excluding that applicable to other categories).

##### "standard_log" `[string]`
- Human-readable file for logging all blocked access attempts. Specify a filename, or leave blank to disable.

##### "apache_style_log" `[string]`
- Apache-style file for logging all blocked access attempts. Specify a filename, or leave blank to disable.

##### "serialised_log" `[string]`
- Serialised file for logging all blocked access attempts. Specify a filename, or leave blank to disable.

##### "error_log" `[string]`
- A file for logging any non-fatal errors detected. Specify a filename, or leave blank to disable.

##### "outbound_request_log" `[string]`
- A file for logging the results of any outbound requests. Specify a filename, or leave blank to disable.

##### "report_log" `[string]`
- A file for logging any reports sent to external APIs. Specify a filename, or leave blank to disable.

##### "truncate" `[string]`
- Truncate log files when they reach a certain size? Value is the maximum size in B/KB/MB/GB/TB that a log file may grow to before being truncated. The default value of 0KB disables truncation (log files can grow indefinitely). Note: Applies to individual log files! The size of log files is not considered collectively.

##### "log_rotation_limit" `[int]`
- Log rotation limits the number of log files that should exist at any one time. When new log files are created, if the total number of log files exceeds the specified limit, the specified action will be performed. You can specify the desired limit here. A value of 0 will disable log rotation.

##### "log_rotation_action" `[string]`
- Log rotation limits the number of log files that should exist at any one time. When new log files are created, if the total number of log files exceeds the specified limit, the specified action will be performed. You can specify the desired action here.

```
log_rotation_action
├─Delete ("Delete the oldest log files, until the limit is no longer exceeded.")
└─Archive ("Firstly archive, and then delete the oldest log files, until the limit is no longer exceeded.")
```

##### "log_banned_ips" `[bool]`
- Include blocked requests from banned IPs in logs? True = Yes [Default]; False = No.

##### "log_sanitisation" `[bool]`
- When using the front-end logs page to view log data, CIDRAM sanitises the log data before displaying it, to protect users from XSS attacks and other potential threats that log data could contain. However, by default, data isn't sanitised during logging. This is to ensure that log data is preserved accurately, to aid any heuristic or forensic analysis that might be necessary in the future. However, in the event that a user attempts to read log data using external tools, and if those external tools don't perform their own sanitisation process, the user could be exposed to XSS attacks. If necessary, you can change the default behaviour using this configuration directive. True = Sanitise data when logging it (data is preserved less accurately, but XSS risk is lower). False = Don't sanitise data when logging it (data is preserved more accurately, but XSS risk is higher) [Default].

#### "frontend" (Category)
Configuration for the front-end.

##### "frontend_log" `[string]`
- File for logging front-end login attempts. Specify a filename, or leave blank to disable.

##### "signatures_update_event_log" `[string]`
- A file for logging when signatures are updated via the front-end. Specify a filename, or leave blank to disable.

##### "max_login_attempts" `[int]`
- Maximum number of front-end login attempts. Default = 5.

##### "theme" `[string]`
- The default theme to use for the front-end.

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
└─…Other
```

##### "magnification" `[float]`
- Font magnification. Default = 1.

##### "custom_header" `[string]`
- Inserted as HTML at the very beginning of all front-end pages. This could be useful in case you want to include a website logo, personalised header, scripts, or similar at all such pages.

##### "custom_footer" `[string]`
- Inserted as HTML at the very bottom of all front-end pages. This could be useful in case you want to include a legal notice, contact link, business information or similar at all such pages.

##### "remotes" `[string]`
- A list of the addresses used by the updater to fetch component metadata. This may need to be adjusted when upgrading to a new major version, or when acquiring a new source for updates, but under normal circumstances should be left alone.

##### "enable_two_factor" `[bool]`
- This directive determines whether to use 2FA for front-end accounts.

#### "signatures" (Category)
Configuration for signatures, signature files, modules, etc.

##### "shorthand" `[string]`
- Controls for what to do with a request when there's a positive match against a signature which utilises the given shorthand words.

```
shorthand
├─Attacks ("Attacks")
├─Bogon ("⁰ Bogon IP")
├─Cloud ("Cloud service")
├─Generic ("Generic")
├─Legal ("¹ Legal")
├─Malware ("Malware")
├─Proxy ("² Proxy")
├─Spam ("Spam risk")
├─Banned ("³ Banned")
├─BadIP ("³ Invalid IP")
├─RL ("³ Rate limited")
└─Other ("⁴ Other")
```

__0.__ If your website needs access via LAN or localhost, don't block this. Otherwise though, you can block this.

__1.__ None of the default signature files use this, but it's supported nonetheless in case it might be useful for some users.

__2.__ If you need users to be able to access your website via proxies, don't block this. Otherwise though, you can block this.

__3.__ Direct usage in signatures isn't supported, but it may be invoked by other means in particular circumstances.

__4.__ Refers to cases where shorthand words aren't used at all, or aren't recognised by CIDRAM.

__One per signature.__ A signature may invoke multiple profiles, but can use only one shorthand word. It's possible that multiple shorthand words may be suitable, but as only one can be used, we aim to always use only the most suitable.

__Priority.__ An option selected always takes priority over an option not selected. E.g., if multiple shorthand words are in play but only one of them is set as being blocked, the request will still be blocked.

__Human endpoints and cloud services.__ Cloud service may refer to webhosting providers, server farms, data centres, or any number of other things. Human endpoint refers to the means by which a human accesses the internet, such as by way of an internet service provider. A network usually provides just one or the other, but may sometimes provide both. We aim to never identify potential human endpoints as cloud services. Therefore, a cloud service may be identified as something else if its range is shared by known human endpoints. Conversely, we aim to always identify cloud services, whose ranges are not shared by any known human endpoints, as cloud services. Therefore, a request identified explicitly as a cloud service probably doesn't share its range with any known human endpoints. Likewise, a request identified explicitly by attacks or spam probably does. However, the internet is always in flux, the purposes of networks changes over time, and ranges are always being bought or sold, so remain cognisant and vigilant in regards to false positives.

##### "default_tracktime" `[string]`
- The duration that IP addresses should be tracked for. Default = 7d0°0′0″ (1 week).

##### "infraction_limit" `[int]`
- Maximum number of infractions an IP is allowed to incur before it is banned by IP tracking. Default = 10.

##### "tracking_override" `[bool]`
- Allow modules to override tracking options? True = Yes [Default]; False = No.

#### "verification" (Category)
Configuration for verifying where requests originate from.

##### "search_engines" `[string]`
- Controls for verifying requests from search engines.

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

__What are "positives" and "negatives"?__ When verifying the identity presented by a request, a successful outcome could be described as "positive" or "negative". In the case that the identity presented is confirmed to be the true identity, it would be described as "positive". In the case that the identity presented is confirmed to be falsified, it would be described as "negative". However, an unsuccessful outcome (e.g., verification fails, or the veracity of the identity presented isn't able to be determined) would not be described as "positive" or "negative". Instead, an unsuccessful outcome would be described simply as non-verified. When no attempt to verify the identity presented by a request is made, the request would likewise be described as non-verified. The terms make sense only in the context where the identity presented by a request is recognised, and therefore, where verification is possible. In cases where the identity presented doesn't match the options provided above, or where no identity is presented, the options provided above become irrelevant.

__What are "single-hit bypasses"?__ In some cases, a positive-verified request may still blocked as a result of the signature files, modules, or other conditions of the request, and bypasses may be necessary in order to avoid false positives. In the case where a bypass is intended to deal with exactly one infraction, no more and no less, such a bypass could be described as a "single-hit bypass".

* This option has a corresponding bypass under <code class="s">bypasses➡used</code>. It's recommended to ensure that the checkbox for the corresponding bypass is marked the same way as the checkbox for attempting to verify this option.

##### "social_media" `[string]`
- Controls for verifying requests from social media platforms.

```
social_media
├─Embedly ("* Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("* Pinterest")
├─Snapchat ("* Snapchat")
└─Twitterbot ("*!! Twitterbot")
```

__What are "positives" and "negatives"?__ When verifying the identity presented by a request, a successful outcome could be described as "positive" or "negative". In the case that the identity presented is confirmed to be the true identity, it would be described as "positive". In the case that the identity presented is confirmed to be falsified, it would be described as "negative". However, an unsuccessful outcome (e.g., verification fails, or the veracity of the identity presented isn't able to be determined) would not be described as "positive" or "negative". Instead, an unsuccessful outcome would be described simply as non-verified. When no attempt to verify the identity presented by a request is made, the request would likewise be described as non-verified. The terms make sense only in the context where the identity presented by a request is recognised, and therefore, where verification is possible. In cases where the identity presented doesn't match the options provided above, or where no identity is presented, the options provided above become irrelevant.

__What are "single-hit bypasses"?__ In some cases, a positive-verified request may still blocked as a result of the signature files, modules, or other conditions of the request, and bypasses may be necessary in order to avoid false positives. In the case where a bypass is intended to deal with exactly one infraction, no more and no less, such a bypass could be described as a "single-hit bypass".

* This option has a corresponding bypass under <code class="s">bypasses➡used</code>. It's recommended to ensure that the checkbox for the corresponding bypass is marked the same way as the checkbox for attempting to verify this option.

** Requires ASN lookup functionality (e.g., via the IP-API or BGPView module).

*!! High likelihood of causing false positives due to iMessage.

##### "other" `[string]`
- Controls for verifying other kinds of requests where possible.

```
other
├─AdSense ("AdSense")
├─AmazonAdBot ("* AmazonAdBot")
└─Grapeshot ("* Oracle Data Cloud Crawler (Grapeshot)")
```

__What are "positives" and "negatives"?__ When verifying the identity presented by a request, a successful outcome could be described as "positive" or "negative". In the case that the identity presented is confirmed to be the true identity, it would be described as "positive". In the case that the identity presented is confirmed to be falsified, it would be described as "negative". However, an unsuccessful outcome (e.g., verification fails, or the veracity of the identity presented isn't able to be determined) would not be described as "positive" or "negative". Instead, an unsuccessful outcome would be described simply as non-verified. When no attempt to verify the identity presented by a request is made, the request would likewise be described as non-verified. The terms make sense only in the context where the identity presented by a request is recognised, and therefore, where verification is possible. In cases where the identity presented doesn't match the options provided above, or where no identity is presented, the options provided above become irrelevant.

__What are "single-hit bypasses"?__ In some cases, a positive-verified request may still blocked as a result of the signature files, modules, or other conditions of the request, and bypasses may be necessary in order to avoid false positives. In the case where a bypass is intended to deal with exactly one infraction, no more and no less, such a bypass could be described as a "single-hit bypass".

* This option has a corresponding bypass under <code class="s">bypasses➡used</code>. It's recommended to ensure that the checkbox for the corresponding bypass is marked the same way as the checkbox for attempting to verify this option.

##### "adjust" `[string]`
- Controls to adjust other features when in the context of verification.

```
adjust
├─Negatives ("Blocked negatives")
└─NonVerified ("Blocked non-verified")
```

#### "recaptcha" (Category)
Configuration for ReCaptcha (provides a way for humans to regain access when blocked).

##### "usemode" `[int]`
- When should the CAPTCHA be offered? Note: Whitelisted or verified and non-blocked requests never need to complete a CAPTCHA. Also note: CAPTCHAs can provide a useful, additional layer of protection against bots and various kinds of malicious automated requests, but won't provide any protection against a malicious human.

```
usemode
├─0 (Never !!!)
├─1 (Only when blocked, within the signature limit, and not banned.)
├─2 (Only when blocked, specially marked for use, within the signature limit, and not banned.)
├─3 (Only when within the signature limit, and not banned (regardless of whether blocked).)
├─4 (Only when not blocked.)
└─5 (Only when not blocked, or when specially marked for use, within the signature limit, and not banned.)
```

##### "lockip" `[bool]`
- Lock CAPTCHA to IPs?

##### "lockuser" `[bool]`
- Lock CAPTCHA to users?

##### "sitekey" `[string]`
- This value can be found in the dashboard for your CAPTCHA service.

See also:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "secret" `[string]`
- This value can be found in the dashboard for your CAPTCHA service.

See also:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "expiry" `[float]`
- Number of hours to remember CAPTCHA instances. Default = 720 (1 month).

##### "recaptcha_log" `[string]`
- Log all CAPTCHA attempts? If yes, specify the name to use for the log file. If no, leave this variable blank.

##### "signature_limit" `[int]`
- Maximum number of signatures allowed before the CAPTCHA offer is withdrawn. Default = 1.

##### "api" `[string]`
- Which API to use?

```
api
├─V2 ("V2 (Checkbox)")
└─Invisible ("V2 (Invisible)")
```

##### "show_cookie_warning" `[bool]`
- Show cookie warning? True = Yes [Default]; False = No.

##### "show_api_message" `[bool]`
- Show API message? True = Yes [Default]; False = No.

##### "nonblocked_status_code" `[int]`
- Which status code should be used when displaying CAPTCHAs to non-blocked requests?

```
nonblocked_status_code
├─200 (200 OK): Least robust, but most user-friendly. Automated requests will most likely
│ interpret this response as indication that the request was successful.
├─403 (403 Forbidden): More robust, but less user-friendly. Recommended for most general
│ circumstances.
├─418 (418 I'm a teapot): References an April Fools' joke ({{Links.RFC2324}}). Very unlikely to be
│ understood by any client, bot, browser, or otherwise. Provided for amusement
│ and convenience, but not generally recommended.
├─429 (429 Too Many Requests): Recommended for rate limiting, when dealing with DDoS attacks, and for flood
│ prevention. Not recommended in other contexts.
└─451 (451 Unavailable For Legal Reasons): Recommended when blocking primarily for legal reasons. Not recommended in
  other contexts.
```

#### "hcaptcha" (Category)
Configuration for HCaptcha (provides a way for humans to regain access when blocked).

##### "usemode" `[int]`
- When should the CAPTCHA be offered? Note: Whitelisted or verified and non-blocked requests never need to complete a CAPTCHA. Also note: CAPTCHAs can provide a useful, additional layer of protection against bots and various kinds of malicious automated requests, but won't provide any protection against a malicious human.

```
usemode
├─0 (Never !!!)
├─1 (Only when blocked, within the signature limit, and not banned.)
├─2 (Only when blocked, specially marked for use, within the signature limit, and not banned.)
├─3 (Only when within the signature limit, and not banned (regardless of whether blocked).)
├─4 (Only when not blocked.)
└─5 (Only when not blocked, or when specially marked for use, within the signature limit, and not banned.)
```

##### "lockip" `[bool]`
- Lock CAPTCHA to IPs?

##### "lockuser" `[bool]`
- Lock CAPTCHA to users?

##### "sitekey" `[string]`
- This value can be found in the dashboard for your CAPTCHA service.

See also:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "secret" `[string]`
- This value can be found in the dashboard for your CAPTCHA service.

See also:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "expiry" `[float]`
- Number of hours to remember CAPTCHA instances. Default = 720 (1 month).

##### "hcaptcha_log" `[string]`
- Log all CAPTCHA attempts? If yes, specify the name to use for the log file. If no, leave this variable blank.

##### "signature_limit" `[int]`
- Maximum number of signatures allowed before the CAPTCHA offer is withdrawn. Default = 1.

##### "api" `[string]`
- Which API to use?

```
api
├─V1 ("V1")
└─Invisible ("V1 (Invisible)")
```

##### "show_cookie_warning" `[bool]`
- Show cookie warning? True = Yes [Default]; False = No.

##### "show_api_message" `[bool]`
- Show API message? True = Yes [Default]; False = No.

##### "nonblocked_status_code" `[int]`
- Which status code should be used when displaying CAPTCHAs to non-blocked requests?

```
nonblocked_status_code
├─200 (200 OK): Least robust, but most user-friendly. Automated requests will most likely
│ interpret this response as indication that the request was successful.
├─403 (403 Forbidden): More robust, but less user-friendly. Recommended for most general
│ circumstances.
├─418 (418 I'm a teapot): References an April Fools' joke ({{Links.RFC2324}}). Very unlikely to be
│ understood by any client, bot, browser, or otherwise. Provided for amusement
│ and convenience, but not generally recommended.
├─429 (429 Too Many Requests): Recommended for rate limiting, when dealing with DDoS attacks, and for flood
│ prevention. Not recommended in other contexts.
└─451 (451 Unavailable For Legal Reasons): Recommended when blocking primarily for legal reasons. Not recommended in
  other contexts.
```

#### "legal" (Category)
Configuration for legal requirements.

##### "pseudonymise_ip_addresses" `[bool]`
- Pseudonymise IP addresses when logging? True = Yes [Default]; False = No.

##### "privacy_policy" `[string]`
- The address of a relevant privacy policy to be displayed in the footer of any generated pages. Specify a URL, or leave blank to disable.

#### "template_data" (Category)
Configuration for templates and themes.

##### "theme" `[string]`
- The default theme to use for CIDRAM.

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
└─…Other
```

##### "magnification" `[float]`
- Font magnification. Default = 1.

##### "css_url" `[string]`
- CSS file URL for custom themes.

##### "block_event_title" `[string]`
- The page title to display for block events.

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("Access denied!")
└─…Other
```

##### "captcha_title" `[string]`
- The page title to display for CAPTCHA requests.

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…Other
```

##### "custom_header" `[string]`
- Inserted as HTML at the very beginning of all "access denied" pages. This could be useful in case you want to include a website logo, personalised header, scripts, or similar at all such pages.

##### "custom_footer" `[string]`
- Inserted as HTML at the very bottom of all "access denied" pages. This could be useful in case you want to include a legal notice, contact link, business information or similar at all such pages.

#### "rate_limiting" (Category)
Configuration for rate limiting (not recommended for general use).

##### "max_bandwidth" `[string]`
- The maximum amount of bandwidth allowed within the allowance period before rate limiting future requests. A value of 0 disables this type of rate limiting. Default = 0KB.

##### "max_requests" `[int]`
- The maximum number of requests allowed within the allowance period before rate limiting future requests. A value of 0 disables this type of rate limiting. Default = 0.

##### "precision_ipv4" `[int]`
- The precision to use for tracking IPv4 usage. Value mirrors CIDR block size. Set to 32 for best precision. Default = 32.

##### "precision_ipv6" `[int]`
- The precision to use for tracking IPv6 usage. Value mirrors CIDR block size. Set to 128 for best precision. Default = 128.

##### "allowance_period" `[string]`
- The duration to track usage. Default = 0°0′0″.

##### "exceptions" `[string]`
- Exceptions (i.e., requests which shouldn't be rate limited). Relevant only when rate limiting is enabled.

```
exceptions
├─Whitelisted ("Whitelisted requests")
├─Verified ("Verified search engine and social media requests")
└─FE ("Requests to the CIDRAM front-end")
```

##### "segregate" `[bool]`
- Should quotas for different domains and hosts be segregated or shared? True = Quotas will be segregated. False = Quotas will be shared [Default].

#### "supplementary_cache_options" (Category)
Supplementary cache options. Note: Changing these values may potentially log you out.

##### "prefix" `[string]`
- The value specified here will be prepended to all cache entry keys. Default = "CIDRAM_". When multiple installations exist at the same server, this can be useful for keeping their caches separate from each other.

##### "enable_apcu" `[bool]`
- Specifies whether to try using APCu for caching. Default = True.

##### "enable_memcached" `[bool]`
- Specifies whether to try using Memcached for caching. Default = False.

##### "enable_redis" `[bool]`
- Specifies whether to try using Redis for caching. Default = False.

##### "enable_pdo" `[bool]`
- Specifies whether to try using PDO for caching. Default = False.

##### "memcached_host" `[string]`
- Memcached host value. Default = "localhost".

##### "memcached_port" `[int]`
- Memcached port value. Default = "11211".

##### "redis_host" `[string]`
- Redis host value. Default = "localhost".

##### "redis_port" `[int]`
- Redis port value. Default = "6379".

##### "redis_timeout" `[float]`
- Redis timeout value. Default = "2.5".

##### "pdo_dsn" `[string]`
- PDO DSN value. Default = "mysql:dbname=cidram;host=localhost;port=3306".

__FAQ.__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.en.md#user-content-HOW_TO_USE_PDO" hreflang="en-AU">What is a "PDO DSN"? How can I use PDO with CIDRAM?</a></em>

##### "pdo_username" `[string]`
- PDO username.

##### "pdo_password" `[string]`
- PDO password.

#### "bypasses" (Category)
Default signature bypasses configuration.

##### "used" `[string]`
- Which bypasses should be used?

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


### 6. <a name="SECTION6"></a>SIGNATURE FORMAT

*See also:*
- *[What is a "signature"?](#user-content-WHAT_IS_A_SIGNATURE)*

#### 6.0 BASICS (FOR SIGNATURE FILES)

All IPv4 signatures follow the format: `xxx.xxx.xxx.xxx/yy [Function] [Param]`.
- `xxx.xxx.xxx.xxx` represents the beginning of the CIDR block (the octets of the initial IP address in the block).
- `yy` represents the CIDR block size [1-32].
- `[Function]` instructs the script what to do with the signature (how the signature should be regarded).
- `[Param]` represents whatever additional information may be required by `[Function]`.

All IPv6 signatures follow the format: `xxxx:xxxx:xxxx:xxxx::xxxx/yy [Function] [Param]`.
- `xxxx:xxxx:xxxx:xxxx::xxxx` represents the beginning of the CIDR block (the octets of the initial IP address in the block). Complete notation and abbreviated notation are both acceptable (and each MUST follow the appropriate and relevant standards of IPv6 notation, but with one exception: an IPv6 address can never begin with an abbreviation when used in a signature for this script, due to the way in which CIDRs are reconstructed by the script; For example, `::1/128` should be expressed, when used in a signature, as `0::1/128`, and `::0/128` expressed as `0::/128`).
- `yy` represents the CIDR block size [1-128].
- `[Function]` instructs the script what to do with the signature (how the signature should be regarded).
- `[Param]` represents whatever additional information may be required by `[Function]`.

The signature files for CIDRAM SHOULD use Unix-style linebreaks (`%0A`, or `\n`)! Other types/styles of linebreaks (e.g., Windows `%0D%0A` or `\r\n` linebreaks, Mac `%0D` or `\r` linebreaks, etc) MAY be used, but are NOT preferred. Non-Unix-style linebreaks will be normalised to Unix-style linebreaks by the script.

Precise and correct CIDR notation is required, otherwise the script will NOT recognise the signatures. Additionally, all the CIDR signatures of this script MUST begin with an IP address whose IP number can divide evenly into the block division represented by its CIDR block size (e.g., if you wanted to block all IPs from `10.128.0.0` to `11.127.255.255`, `10.128.0.0/8` would NOT be recognised by the script, but `10.128.0.0/9` and `11.0.0.0/9` used in conjunction, WOULD be recognised by the script).

Anything in the signature files not recognised as a signature nor as signature-related syntax by the script will be IGNORED, therefore meaning that you can safely put any non-signature data that you want into the signature files without breaking them and without breaking the script. Comments are acceptable in the signature files, and no special formatting is required for them. Shell-style hashing for comments is preferred, but not enforced; Functionally, it makes no difference to the script whether or not you choose to use Shell-style hashing for comments, but using Shell-style hashing helps IDEs and plain-text editors to correctly highlight the various parts of the signature files (and so, Shell-style hashing can assist as a visual aid while editing).

The possible values of `[Function]` are as follows:
- Run
- Whitelist
- Greylist
- Deny

If "Run" is used, when the signature is triggered, the script will attempt to execute (using a `require_once` statement) an external PHP script, specified by the `[Param]` value (the working directory should be the "/vault/" directory of the script).

Example: `127.0.0.0/8 Run example.php`

This can be useful if you want to execute some specific PHP code for some specific IPs and/or CIDRs.

If "Whitelist" is used, when the signature is triggered, the script will reset all detections (if there's been any detections) and break the test function. `[Param]` is ignored. This function is the equivalent of whitelisting a particular IP or CIDR from being detected.

Example: `127.0.0.1/32 Whitelist`

If "Greylist" is used, when the signature is triggered, the script will reset all detections (if there's been any detections) and skip to the next signature file to continue processing. `[Param]` is ignored.

Example: `127.0.0.1/32 Greylist`

If "Deny" is used, when the signature is triggered, assuming no whitelist signature has been triggered for the given IP address and/or given CIDR, access to the protected page will be denied. "Deny" is what you'll want to use to actually block an IP address and/or CIDR range. When any signatures are triggered that make use of "Deny", the "Access Denied" page of the script will be generated and the request to the protected page killed.

The `[Param]` value accepted by "Deny" will be parsed to the "Access Denied" page output, supplied to the client/user as the cited reason for their access to the requested page being denied. It can be either a short and simple sentence, explaining why you've chosen to block them (anything should suffice, even a simple "I don't want you on my website"), or one of a small handful of shorthand words supplied by the script, that if used, will be replaced by the script with a pre-prepared explanation of why the client/user has been blocked.

The pre-prepared explanations have L10N support and can be translated by the script based upon the language you specify to the `lang` directive of the script configuration. Additionally, you can instruct the script to ignore "Deny" signatures based upon their `[Param]` value (if they're using these shorthand words) via the directives specified by the script configuration (each shorthand word has a corresponding directive to either process the corresponding signatures or to ignore them). `[Param]` values that don't use these shorthand words, however, don't have L10N support and therefore WON'T be translated by the script, and additionally, aren't directly controllable by the script configuration.

The available shorthand words are:
- Attacks
- Bogon
- Cloud
- Generic
- Legal
- Malware
- Proxy
- Spam

#### 6.1 TAGS

##### 6.1.0 SECTION TAGS

If you want to split your custom signatures into individual sections, you can identify these individual sections to the script by adding a "section tag" immediately after the signatures of each section, along with the name of your signature section (see the example below).

```
# Section 1.
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: Section 1
```

To break section tagging and to ensure that tags aren't incorrectly identified to signature sections from earlier in the signature files, simply ensure that there are at least two consecutive linebreaks between your tag and your earlier signature sections. Any untagged signatures will default to either "IPv4" or "IPv6" (depending on which types of signatures are being triggered).

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: Section 1
```

In the above example `1.2.3.4/32` and `2.3.4.5/32` will be tagged as "IPv4", whereas `4.5.6.7/32` and `5.6.7.8/32` will be tagged as "Section 1".

The same logic can be applied for separating other types of tags, too.

In particular, section tags can be very useful for debugging when false positives occur, by providing an easy means of locating the exact source of the problem, and can be very useful for filtering logfile entries when viewing logfiles via the front-end logs page (section names are clickable via the front-end logs page and can be used as a filtering criteria). If section tags are omitted for some particular signatures, when those signatures are triggered, CIDRAM uses the name of the signature file along with the type of IP address blocked (IPv4 or IPv6) as a fallback, and thus, section tags are entirely optional. They may be recommend in some cases though, such as when signature files are vaguely named or when it may otherwise be difficult to clearly identify the source of the signatures causing a request to be blocked.

##### 6.1.1 EXPIRY TAGS

If you want signatures to expire after some time, in a similar manner to section tags, you can use an "expiry tag" to specify when signatures should cease to be valid. Expiry tags use the format "YYYY.MM.DD" (see the example below).

```
# Section 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

Expired signatures will never be triggered on any request, no matter what.

##### 6.1.2 ORIGIN TAGS

If you want to specify the country of origin for some particular signature, you can do so using an "origin tag". An origin tag accepts an "[ISO 3166-1 Alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)" code corresponding to the country of origin for the signatures that it applies to. These codes must be written in upper-case (lower-case or mixed-case won't render correctly). When an origin tag is used, it is added to the "Why blocked" log field entry for any requests blocked as a result of the signatures that the tag is applied to.

If the optional "flags CSS" component is installed, when viewing logfiles via the front-end logs page, information appended by origin tags is replaced with the flag of the country corresponding to that information. This information, whether in its raw form or as a country flag, is clickable, and when clicked on, will filter log entries by way of other similarly identifying log entries (effectively allowing those accessing the logs page to filter by way of country of origin).

Note: Technically, this isn't any form of geolocation, due to that it doesn't involve looking up any specific information relating to inbound IPs, but rather, simply allows us to explicitly state a country of origin for any requests blocked by specific signatures. Multiple origin tags are permissible within the same signature section.

Hypothetical example:

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

Any tags may be used in conjunction, and all tags are optional (see the example below).

```
# Example Section.
1.2.3.4/32 Deny Generic
Origin: US
Tag: Example Section
Expires: 2016.12.31
```

##### 6.1.3 DEFERENCE TAGS

When large numbers of signature files are installed and actively used, installations can become quite complex, and there may be some signatures which overlap. In these cases, in order to prevent multiple, overlapping signatures being triggered during block events, deference tags may be used to defer specific signature sections in cases where some other specific signature file is installed and actively used. This may be useful in cases where some signatures are updated more frequently than others, in order to defer the less frequently updated signatures in favour of the more frequently updated signatures.

Deference tags are used similarly to other types of tags. The tag's value should match an installed and actively used signature file to be deferred to.

Example:

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 6.1.4 PROFILE TAGS

Profile tags provide a means to display additional information at the IP test page, and can be leveraged by modules and auxiliary rules for more complex behaviour and fine-tuned decision making.

Profile tags are used similarly to other types of tags. The values of profile tags can be used as a condition for modules and auxiliary rules. Profile tags can provide multiple values by separating those values with a semicolon. The end-user never sees the values of profile tags.

Example:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 6.2 YAML

##### 6.2.0 YAML BASICS

A simplified form of YAML markup may be used in signature files for the purpose of defining behaviours and settings specific to individual signature sections. This may be useful if you want the value of your configuration directives to differ on the basis of individual signatures and signature sections (for example; if you want to supply an email address for support tickets for any users blocked by one particular signature, but don't want to supply an email address for support tickets for users blocked by any other signatures; if you want some specific signatures to trigger a page redirect; if you want to mark a signature section for use with reCAPTCHA/hCAPTCHA; if you want to log blocked access attempts to separate files on the basis of individual signatures and/or signature sections).

Use of YAML markup in the signature files is entirely optional (i.e., you may use it if you wish to do so, but you are not required to do so), and is able to leverage most (but not all) configuration directives.

Note: YAML markup implementation in CIDRAM is very simplistic and very limited; It is intended to fulfill requirements specific to CIDRAM in a manner that has the familiarity of YAML markup, but neither follows nor complies with official specifications (and therefore won't behave in the same way as more thorough implementations elsewhere, and may not be appropriate for other projects elsewhere).

In CIDRAM, YAML markup segments are identified to the script by three dashes ("---"), and terminate alongside their containing signature sections by double-linebreaks. A typical YAML markup segment within a signature section consists of three dashes on a line immediately after the list of CIDRs and any tags, followed by a two dimensional list of key-value pairs (first dimension, configuration directive categories; second dimension, configuration directives) for which configuration directives should be modified (and to which values) whenever a signature within that signature section is triggered (see the examples below).

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

##### 6.2.1 HOW TO "SPECIALLY MARK" SIGNATURE SECTIONS FOR USE WITH reCAPTCHA/hCAPTCHA

When "usemode" is 2 or 5, to "specially mark" signature sections for use with reCAPTCHA/hCAPTCHA, an entry is included in the YAML segment for that signature section (see the example below).

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

#### 6.3 AUXILIARY

##### 6.3.0 IGNORING SIGNATURE SECTIONS

In addition, if you want CIDRAM to completely ignore some specific sections within any of the signature files, you can use the `ignore.dat` file to specify which sections to ignore. On a new line, write `Ignore`, followed by a space, followed by the name of the section that you want CIDRAM to ignore (see the example below).

```
Ignore Section 1
```

This can also be achieved by using the interface provided by the "sections list" page of the CIDRAM front-end.

##### 6.3.1 AUXILIARY RULES

If you feel that writing your own custom signature files or custom modules is too complicated for you, a simpler alternative may be to use the interface provided by the "auxiliary rules" page of the CIDRAM front-end. By selecting the appropriate options and specifying details about specific types of requests, you can instruct CIDRAM how to respond to those requests. "Auxiliary rules" are executed after all signature files and modules have already finished executing.

#### 6.4 <a name="MODULE_BASICS"></a>BASICS (FOR MODULES)

Modules can be used to extend the functionality of CIDRAM, perform additional tasks, or process additional logic.

Due to that modules are written as PHP files, if you're adequately familiar with the CIDRAM codebase, you can structure your modules however you want, and write your module signatures however you want (within reason of what is possible with PHP).

*Note: If you're not comfortable working with PHP code, writing your own modules is not recommended.*

Some functionality is provided by CIDRAM for modules to use, which should make it simpler and easier to write your own modules. Information about this functionality is described below.

#### 6.5 MODULE FUNCTIONALITY

##### 6.5.0 "$this->trigger"

Module signatures are typically written with `$this->trigger`. In most cases, this method will be more important than anything else for the purpose of writing modules.

`$this->trigger` accepts 4 parameters: `$Condition`, `$ReasonShort`, `$ReasonLong` (optional), and `$DefineOptions` (optional).

The truthiness of `$Condition` is evaluated, and if true, the signature is "triggered". If false, the signature is *not* "triggered". `$Condition` typically contains PHP code to evaluate a condition that should cause a request to be blocked.

`$ReasonShort` is cited in the "Why Blocked" field when the signature is "triggered".

`$ReasonLong` is an optional message to be displayed to the user/client for when they're blocked, to explain why they've been blocked. Defaults to the standard "Access Denied" message when omitted.

`$DefineOptions` is an optional array containing key/value pairs, used to define configuration options specific to the request instance. Configuration options will be applied when the signature is "triggered".

`$this->trigger` returns true when the signature is "triggered", and false when it isn't.

##### 6.5.1 "$this->bypass"

Signature bypasses are typically written with `$this->bypass`.

`$this->bypass` accepts 3 parameters: `$Condition`, `$ReasonShort`, and `$DefineOptions` (optional).

The truthiness of `$Condition` is evaluated, and if true, the bypass is "triggered". If false, the bypass is *not* "triggered". `$Condition` typically contains PHP code to evaluate a condition that should *not* cause a request to be blocked.

`$ReasonShort` is cited in the "Why Blocked" field when the bypass is "triggered".

`$DefineOptions` is an optional array containing key/value pairs, used to define configuration options specific to the request instance. Configuration options will be applied when the bypass is "triggered".

`$this->bypass` returns true when the bypass is "triggered", and false when it isn't.

##### 6.5.2 "$this->dnsReverse"

This can be used to fetch the hostname of an IP address. If you want to create a module to block hostnames, this method could be useful.

Example:
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

#### 6.6 MODULE VARIABLES

Modules execute within their own scope, and any variables defined by a module, won't be accessible to other modules, or to the parent script, unless they're stored in the `$CIDRAM` array (everything else is flushed after the module execution finishes).

Listed below are some common variables that might be useful for your module:

Variable | Description
----|----
`$this->BlockInfo['DateTime']` | The current date and time.
`$this->BlockInfo['IPAddr']` | IP address for the current request.
`$this->BlockInfo['ScriptIdent']` | CIDRAM script version.
`$this->BlockInfo['Query']` | The query for the current request.
`$this->BlockInfo['Referrer']` | The referrer for the current request (if one exists).
`$this->BlockInfo['UA']` | The user agent for the current request.
`$this->BlockInfo['UALC']` | The user agent for the current request (lower-cased).
`$this->BlockInfo['ReasonMessage']` | The message to be displayed to the user/client for the current request if they're blocked.
`$this->BlockInfo['SignatureCount']` | The number of signatures triggered for the current request.
`$this->BlockInfo['Signatures']` | Reference information for any signatures triggered for the current request.
`$this->BlockInfo['WhyReason']` | Reference information for any signatures triggered for the current request.

---


### 7. <a name="SECTION7"></a>KNOWN COMPATIBILITY PROBLEMS

The following packages and products have been found to be incompatible with CIDRAM:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

Modules have been made available to ensure that the following packages and products will be compatible with CIDRAM:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__

*See also: [Compatibility Charts](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 8. <a name="SECTION8"></a>FREQUENTLY ASKED QUESTIONS (FAQ)

- [What is a "signature"?](#user-content-WHAT_IS_A_SIGNATURE)
- [What is a "CIDR"?](#user-content-WHAT_IS_A_CIDR)
- [What is a "false positive"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)
- [Can CIDRAM block entire countries?](#user-content-BLOCK_ENTIRE_COUNTRIES)
- [How frequently are signatures updated?](#user-content-SIGNATURE_UPDATE_FREQUENCY)
- [I've encountered a problem while using CIDRAM and I don't know what to do about it! Please help!](#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [I've been blocked by CIDRAM from a website that I want to visit! Please help!](#user-content-BLOCKED_WHAT_TO_DO)
- [I want to use CIDRAM v3 with a PHP version older than 7.2; Can you help?](#user-content-MINIMUM_PHP_VERSION_V3)
- [Can I use a single CIDRAM installation to protect multiple domains?](#user-content-PROTECT_MULTIPLE_DOMAINS)
- [I don't want to mess around with installing this and getting it to work with my website; Can I just pay you to do it all for me?](#user-content-PAY_YOU_TO_DO_IT)
- [Can I hire you or any of the developers of this project for private work?](#user-content-HIRE_FOR_PRIVATE_WORK)
- [I need specialist modifications, customisations, etc; Can you help?](#user-content-SPECIALIST_MODIFICATIONS)
- [I'm a developer, website designer, or programmer. Can I accept or offer work relating to this project?](#user-content-ACCEPT_OR_OFFER_WORK)
- [I want to contribute to the project; Can I do this?](#user-content-WANT_TO_CONTRIBUTE)
- [Can I use cron to update automatically?](#user-content-CRON_TO_UPDATE_AUTOMATICALLY)
- [What are "infractions"?](#user-content-WHAT_ARE_INFRACTIONS)
- [Can CIDRAM block hostnames?](#user-content-BLOCK_HOSTNAMES)
- [What can I use for "default_dns"?](#what-can-i-use-for-default_dns)
- [Can I use CIDRAM to protect things other than websites (e.g., email servers, FTP, SSH, IRC, etc)?](#user-content-PROTECT_OTHER_THINGS)
- [Will problems occur if I use CIDRAM at the same time as using CDNs or caching services?](#user-content-CDN_CACHING_PROBLEMS)
- [Will CIDRAM protect my website from DDoS attacks?](#user-content-DDOS_ATTACKS)
- [When I activate or deactivate modules or signature files via the updates page, it sorts them alphanumerically in the configuration. Can I change the way that they get sorted?](#user-content-CHANGE_COMPONENT_SORT_ORDER)
- [What is a "PDO DSN"? How can I use PDO with CIDRAM?](#user-content-HOW_TO_USE_PDO)
- [CIDRAM is blocking cronjobs; How to fix this?](#user-content-BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>What is a "signature"?

In the context of CIDRAM, a "signature" refers to data that acts as an indicator/identifier for something specific that we're looking for, usually an IP address or CIDR, and includes some instruction for CIDRAM, telling it the best way to respond when it encounters what we're looking for. A typical signature for CIDRAM looks something like this:

For "signature files":

`1.2.3.4/32 Deny Generic`

For "modules":

```PHP
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*Note: Signatures for "signature files", and signatures for "modules", are not the same thing.*

Often (but not always), signatures will bundled together in groups, forming "signature sections", often accompanied by comments, markup, and/or related metadata that can be used to provide additional context for the signatures and/or further instruction.

#### <a name="WHAT_IS_A_CIDR"></a>What is a "CIDR"?

"CIDR" is an acronym for "Classless Inter-Domain Routing" *[[1](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing), [2](https://whatismyipaddress.com/cidr)]*, and it's this acronym that's used as part of the name for this package, "CIDRAM", which is an acronym for "Classless Inter-Domain Routing Access Manager".

However, in the context of CIDRAM (such as, within this documentation, within discussions relating to CIDRAM, or within the CIDRAM language data), whenever a "CIDR" (singular) or "CIDRs" (plural) is mentioned or referred to (and thus whereby we use these words as nouns in their own right, as opposed to as acronyms), what's intended and meant by this is a subnet (or subnets), expressed using CIDR notation. The reason that CIDR (or CIDRs) is used instead of subnet (or subnets) is to make it clear that it's specifically subnets expressed using CIDR notation that's being referred to (because CIDR notation is just one of several different ways that subnets can be expressed). CIDRAM could, therefore, be considered a "subnet access manager".

Although this dual meaning of "CIDR" may present some ambiguity in some cases, this explanation, along with the context provided, should help to resolve such ambiguity.

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>What is a "false positive"?

The term "false positive" (*alternatively: "false positive error"; "false alarm"*), described very simply, and in a generalised context, is used when testing for a condition, to refer to the results of that test, when the results are positive (i.e., the condition is determined to be "positive", or "true"), but are expected to be (or should have been) negative (i.e., the condition, in reality, is "negative", or "false"). A "false positive" could be considered analogous to "crying wolf" (wherein the condition being tested is whether there's a wolf near the herd, the condition is "false" in that there's no wolf near the herd, and the condition is reported as "positive" by the shepherd by way of calling "wolf, wolf"), or analogous to situations in medical testing wherein a patient is diagnosed as having some illness or disease, when in reality, they have no such illness or disease.

Related outcomes when testing for a condition can be described using the terms "true positive", "true negative" and "false negative". A "true positive" refers to when the results of the test and the actual state of the condition are both true (or "positive"), and a "true negative" refers to when the results of the test and the actual state of the condition are both false (or "negative"); A "true positive" or a "true negative" is considered to be a "correct inference". The antithesis of a "false positive" is a "false negative"; A "false negative" refers to when the results of the test are negative (i.e., the condition is determined to be "negative", or "false"), but are expected to be (or should have been) positive (i.e., the condition, in reality, is "positive", or "true").

In the context of CIDRAM, these terms refer to the signatures of CIDRAM and what/whom they block. When CIDRAM blocks an IP address due to bad, outdated or incorrect signatures, but shouldn't have done so, or when it does so for the wrong reasons, we refer to this event as a "false positive". When CIDRAM fails to block an IP address that should have been blocked, due to unforeseen threats, missing signatures or shortfalls in its signatures, we refer to this event as a "missed detection" (which is analogous to a "false negative").

This can be summarised by the table below:

&nbsp; | CIDRAM should *NOT* block an IP address | CIDRAM *SHOULD* block an IP address
---|---|---
CIDRAM does *NOT* block an IP address | True negative (correct inference) | Missed detection (analogous to false negative)
CIDRAM *DOES* block an IP address | __False positive__ | True positive (correct inference)

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>Can CIDRAM block entire countries?

Yes. The easiest way to do this would be by installing the BGPView module and configuring it according to your needs.

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>How frequently are signatures updated?

Update frequency varies depending on the signature files in question. All maintainers for CIDRAM signature files generally try to keep their signatures as up-to-date as is possible, but as all of us have various other commitments, our lives outside the project, and as none of us are financially compensated (i.e., paid) for our efforts on the project, a precise update schedule can't be guaranteed. Generally, signatures are updated whenever there's enough time to update them, and generally, maintainers try to prioritise based on necessity and on how frequently changes occur among ranges. Assistance is always appreciated if you're willing to offer any.

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>I've encountered a problem while using CIDRAM and I don't know what to do about it! Please help!

- Are you using the latest version of the software? Are you using the latest versions of your signature files? If the answer to either of these two questions is no, try to update everything first, and check whether the problem persists. If it persists, continue reading.
- Have you checked through all the documentation? If not, please do so. If the problem can't be solved using the documentation, continue reading.
- Have you checked the **[issues page](https://github.com/CIDRAM/CIDRAM/issues)**, to see whether the problem has been mentioned before? If it's been mentioned before, check whether any suggestions, ideas, and/or solutions were provided, and follow as per necessary to try to resolve the problem.
- If the problem still persists, please seek help about it by creating a new issue on the issues page.

#### <a name="BLOCKED_WHAT_TO_DO"></a>I've been blocked by CIDRAM from a website that I want to visit! Please help!

CIDRAM provides a means for website owners to block undesirable traffic, but it's the responsibility of website owners to decide for themselves how they want to use CIDRAM. In case of the false positives relating to the signature files normally included with CIDRAM, corrections can be made, but in regards to being unblocked from specific websites, you'll need to take that up with the owners of the websites in question. In cases where corrections are made, at the very least, they'll need to update their signature files and/or installation, and in other cases (such as, for example, where they've modified their installation, created their own custom signatures, etc), the responsibility to solve your problem is entirely theirs, and is entirely outside our control.

#### <a name="MINIMUM_PHP_VERSION_V3"></a>I want to use CIDRAM v3 with a PHP version older than 7.2; Can you help?

No. PHP≥7.2 is a minimum requirement for CIDRAM v3.

*See also: [Compatibility Charts](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>Can I use a single CIDRAM installation to protect multiple domains?

Yes. CIDRAM installations are not naturally locked to specific domains, and can therefore be used to protect multiple domains. Generally, we refer to CIDRAM installations protecting only one domain as "single-domain installations", and we refer to CIDRAM installations protecting multiple domains and/or sub-domains as "multi-domain installations". If you operate a multi-domain installation and need to use different sets of signature files for different domains, or need CIDRAM to be configured differently for different domains, it's possible to do this. After loading the configuration file (`config.yml`), CIDRAM will check for the existence of a "configuration overrides file" specific to the domain (or sub-domain) being requested (`the-domain-being-requested.tld.config.yml`), and if found, any configuration values defined by the configuration overrides file will be used for the execution instance instead of the configuration values defined by the configuration file. Configuration overrides files are identical to the configuration file, and at your discretion, may contain either the entirety of all configuration directives available to CIDRAM, or whichever small subsection required which differs from the values normally defined by the configuration file. Configuration overrides files are named according to the domain that they are intended for (so, for example, if you need a configuration overrides file for the domain, `https://www.some-domain.tld/`, its configuration overrides file should be named as `some-domain.tld.config.yml`, and should be placed within the vault alongside the configuration file, `config.yml`). The domain name for the execution instance is derived from the `HTTP_HOST` header of the request; "www" is ignored.

#### <a name="PAY_YOU_TO_DO_IT"></a>I don't want to mess around with installing this and getting it to work with my website; Can I just pay you to do it all for me?

Maybe. This is considered on a case-by-case basis. Let us know what you need, what you're offering, and we'll let you know whether we can help.

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>Can I hire you or any of the developers of this project for private work?

*See above.*

#### <a name="SPECIALIST_MODIFICATIONS"></a>I need specialist modifications, customisations, etc; Can you help?

*See above.*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>I'm a developer, website designer, or programmer. Can I accept or offer work relating to this project?

Yes. Our license does not prohibit this.

#### <a name="WANT_TO_CONTRIBUTE"></a>I want to contribute to the project; Can I do this?

Yes. Contributions to the project are very welcome. Please see "CONTRIBUTING.md" for more information.

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>Can I use cron to update automatically?

Yes. An API is built into the front-end for interacting with the updates page via external scripts. A separate script, "[Cronable](https://github.com/Maikuolan/Cronable)", is available, and can be used by your cron manager or cron scheduler to update this and other supported packages automatically (this script provides its own documentation).

#### <a name="WHAT_ARE_INFRACTIONS"></a>What are "infractions"?

"Signatures count" and "infractions" both relate to the severity and number of signatures triggered during any particular request, whether due to signature files, modules, auxiliary rules, or otherwise, but while the "signatures count" persists only for that particular request, "infractions" can persist over any number of requests, for as long as is determined by the `default_tracktime`.

This provides a mechanism to ensure that requests from potentially dangerous sources can be blocked upon secondary requests from any particular such source whereby that source had already been blocked during a prior request with a sufficient number of infractions.

#### <a name="BLOCK_HOSTNAMES"></a>Can CIDRAM block hostnames?

Yes. This can be achieved by creating an auxiliary rule or custom module.

![An auxiliary rule for blocking hostnames](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>What can I use for "default_dns"?

Generally, the IP of any reliable DNS server should suffice. If you're looking for suggestions, [public-dns.info](https://public-dns.info/) and [OpenNIC](https://servers.opennic.org/) provide extensive lists of known, public DNS servers. Alternatively, see the table below:

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

*Note: I make no claims or guarantees regarding the privacy practices, security, efficacy, nor reliability of any DNS services, listed or otherwise. Please do your own research when making decisions about them.*

#### <a name="PROTECT_OTHER_THINGS"></a>Can I use CIDRAM to protect things other than websites (e.g., email servers, FTP, SSH, IRC, etc)?

You can (legally), but shouldn't (technically; practically). Our license does not limit which technologies implement CIDRAM, but CIDRAM is a WAF (Web Application Firewall) and has always been intended to protect websites. Because it wasn't designed with other technologies in mind, it's unlikely to be effective or provide reliable protection for other technologies, implementation is likely to be difficult, and the risk of false positives and missed detections is very high.

#### <a name="CDN_CACHING_PROBLEMS"></a>Will problems occur if I use CIDRAM at the same time as using CDNs or caching services?

Maybe. This depends on the nature of the service in question, and how you're using it. Generally, if you're only caching static assets (images, CSS, etc; anything that doesn't generally change over time), there shouldn't be any problems. There may be problems though, if you're caching data that would otherwise typically be generated dynamically when requested, or if you're caching the results of POST requests (this would essentially render your website and its environment as obligatorily static, and CIDRAM is unlikely to provide any meaningful benefit in an obligatorily static environment). There may also be specific configuration requirements for CIDRAM, depending on which CDN or caching service you're using (you'll need to ensure that CIDRAM is configured correctly for the specific CDN or caching service that you're using). Failure to configure CIDRAM correctly may lead to significantly problematic false positives and missed detections.

#### <a name="DDOS_ATTACKS"></a>Will CIDRAM protect my website from DDoS attacks?

Short answer: No.

Slightly longer answer: CIDRAM will help reduce the impact that unwanted traffic can have on your website (thus reducing your website's bandwidth costs), will help reduce the impact that unwanted traffic can have on your hardware (e.g., your server's ability to process and serve requests), and can help to reduce various other potential negative effects associated with unwanted traffic. However, there are two important things that must be remembered in order to understand this question.

Firstly, CIDRAM is a PHP package, and therefore operates at the machine where PHP is installed. This means that CIDRAM can only see and block a request *after* the server has already received it. Secondly, effective [DDoS mitigation](https://en.wikipedia.org/wiki/DDoS_mitigation) should filter requests *before* they reach the server targeted by the DDoS attack. Ideally, DDoS attacks should be detected and mitigated by solutions capable of dropping or rerouting traffic associated with attacks, before it reaches the targeted server in the first place.

This can be implemented using dedicated, on-premise hardware solutions, and/or cloud-based solutions such as dedicated DDoS mitigation services, routing a domain's DNS through DDoS-resistant networks, cloud-based filtering, or some combination thereof. In any case though, this subject is a little too complex to explain thoroughly with just a mere paragraph or two, so I would recommend doing further research if this is a subject you want to pursue. When the true nature of DDoS attacks is properly understood, this answer will make more sense.

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>When I activate or deactivate modules or signature files via the updates page, it sorts them alphanumerically in the configuration. Can I change the way that they get sorted?

Yes. If you need to force some files to execute in a specific order, you can add some arbitrary data before their names in the configuration directive where they're listed, separated by a colon. When the updates page subsequently sorts the files again, this added arbitrary data will affect the sort order, causing them consequently to execute in the order that you want, without needing to rename any of them.

For example, assuming a configuration directive with files listed as follows:

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

If you wanted `file3.php` to execute first, you could add something like `aaa:` before the name of the file:

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

Then, if a new file, `file6.php`, is activated, when the updates page resorts them all, it should end up like this:

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

Same situation when a file is deactivated. Conversely, if you wanted the file to execute last, you could add something like `zzz:` before the name of the file. In any case, you won't need to rename the file in question.

#### <a name="HOW_TO_USE_PDO"></a>What is a "PDO DSN"? How can I use PDO with CIDRAM?

"PDO" is an acronym for "[PHP Data Objects](https://www.php.net/manual/en/intro.pdo.php)". It provides an interface for PHP to be able to connect to some database systems commonly utilised by various PHP applications.

"DSN" is an acronym for "[data source name](https://en.wikipedia.org/wiki/Data_source_name)". The "PDO DSN" describes to PDO how it should connect to a database.

CIDRAM provides the option to utilise PDO for caching purposes. In order for this to work properly, you'll need to configure CIDRAM accordingly, enabling PDO, create a new database for CIDRAM to use (if you don't already have in mind a database for CIDRAM to use), and create a new table in your database in accordance with the structure described below.

When a database connection is successfully, but the necessary table doesn't exist, it will attempt to create it automatically. However, this behaviour hasn't been extensively tested and success can't be guaranteed.

This, of course, only applies if you actually want CIDRAM to use PDO. If you're happy enough for CIDRAM to use flatfile caching (per its default configuration), or any of the various other caching options provided, you won't need to bother troubling yourself with setting up databases, tables and so on.

The structure described below uses "cidram" as its database name, but you can use whichever name you want for your database, so long as that same name is replicated at your DSN configuration.

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

CIDRAM's `pdo_dsn` configuration directive should be configured as described below.

```
Depending on which database driver is used...
├─4d (Warning: Experimental, untested, not recommended!)
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └The host to connect with to find the database.
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └The name of the database to use.
│                │              │
│                │              └The port number to connect to the host.
│                │
│                └The host to connect with to find the database.
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └The name of the database to use.
│    │          │
│    │          └The host to connect with to find the database.
│    │
│    └Possible values: "mssql", "sybase", "dblib".
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├Can be a path to a local database file.
│                    │
│                    ├Can connect with a host and port number.
│                    │
│                    └You should refer to the Firebird documentation if you
│                     want to use this.
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └Which catalogued database to connect with.
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └Which catalogued database to connect with.
├─mysql (Most recommended!)
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └The port number to connect to
│                 │            │               the host.
│                 │            │
│                 │            └The host to connect with to find the
│                 │             database.
│                 │
│                 └The name of the database to use.
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├Can refer to the specific catalogued database.
│               │
│               ├Can connect with a host and port number.
│               │
│               └You should refer to the Oracle documentation if you want to
│                use this.
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├Can refer to the specific catalogued database.
│         │
│         ├Can connect with a host and port number.
│         │
│         └You should refer to the ODBC/DB2 documentation if you want to use
│          this.
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └The name of the database to use.
│               │              │
│               │              └The port number to connect to the host.
│               │
│               └The host to connect with to find the database.
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └The path to the local database file to use.
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └The name of the database to use.
                   │         │
                   │         └The port number to connect to the host.
                   │
                   └The host to connect with to find the database.
```

If you're not sure about what to use for some particular part of your DSN, try seeing firstly whether it works as is, without changing anything.

Note that `pdo_username` and `pdo_password` should be the same as the username and password you've chosen for your database.

#### <a name="BLOCK_CRON"></a>CIDRAM is blocking cronjobs; How to fix this?

If you're using a dedicated file for the purpose of cronjobs, and if that file doesn't need to be called during normal user requests (i.e., outside the context of cronjobs), the most straightforward way to fix this would be to ensure that CIDRAM isn't executed at all during your cronjobs (i.e., don't hook CIDRAM to the file responsible for handling your cronjobs).

Alternatively, if that isn't possible, but your cron server's IP address is relatively consistent and predictable, you could try whitelisting your cron server's IP address, either by creating a whitelist signature for it in a custom signature file, or by creating an auxiliary rule to whitelist it. If your cron server's IP address regularly rotates and isn't particularly predictable, but nonetheless remains from within the same particular network, you could try listing in your `ignore.dat` file the name of the signature section responsible for blocking it in the first place.

If you've tried all of those ideas and none of them worked for you, or if you need help figuring out how to do it, you can create a new issue at CIDRAM's issues page to ask for help.

---


### 9. <a name="SECTION9"></a>LEGAL INFORMATION

#### 9.0 SECTION PREAMBLE

This section of the documentation is intended to describe possible legal considerations regarding the use and implementation of the package, and to provide some basic related information. This may be important for some users as a means to ensure compliancy with any legal requirements that may exist in the countries that they operate in, and some users may need to adjust their website policies in accordance with this information.

First and foremost, please realise that I (the package author) am not a lawyer, nor a qualified legal professional of any kind. Therefore, I am not legally qualified to provide legal advice. Also, in some cases, exact legal requirements may vary between different countries and jurisdictions, and these varying legal requirements may sometimes conflict (such as, for example, in the case of countries that favour [privacy rights](https://en.wikipedia.org/wiki/Right_to_privacy) and the [right to be forgotten](https://en.wikipedia.org/wiki/Right_to_be_forgotten), versus countries that favour extended [data retention](https://en.wikipedia.org/wiki/Data_retention)). Consider also that access to the package is not restricted to specific countries or jurisdictions, and therefore, the package userbase is likely to the geographically diverse. These points considered, I'm not in a position to state what it means to be "legally compliant" for all users, in all regards. However, I hope that the information herein will help you to come to a decision yourself regarding what you must do in order to remain legally compliant in the context of the package. If you have any doubts or concerns regarding the information herein, or if you need additional help and advice from a legal perspective, I would recommend consulting a qualified legal professional.

#### 9.1 LIABILITY AND RESPONSIBILITY

As per already stated by the package license, the package is provided without any warranty. This includes (but is not limited to) all scope of liability. The package is provided to you for your convenience, in the hope that it will be useful, and that it will provide some benefit for you. However, whether you use or implement the package, is your own choice. You are not forced to use or implement the package, but when you do so, you are responsible for that decision. Neither I, nor any other contributors to the package, are legally responsible for the consequences of the decisions that you make, regardless of whether direct, indirect, implied, or otherwise.

#### 9.2 THIRD PARTIES

Depending on its exact configuration and implementation, the package may communicate and share information with third parties in some cases. This information may be defined as "[personally identifiable information](https://en.wikipedia.org/wiki/Personal_data)" (PII) in some contexts, by some jurisdictions.

How this information may be used by these third parties, is subject to the various policies set forth by these third parties, and is outside the scope of this documentation. However, in all such cases, sharing of information with these third parties can be disabled. In all such cases, if you choose to enable it, it is your responsibility to research any concerns that you may have regarding the privacy, security, and usage of PII by these third parties. If any doubts exist, or if you're unsatisfied with the conduct of these third parties in regards to PII, it may be best to disable all sharing of information with these third parties.

For the purpose of transparency, the type of information shared, and with whom, is described below.

##### 9.2.0 HOSTNAME LOOKUP

If you use any features or modules intended to work with hostnames (such as the "bad hosts blocker module", "tor project exit nodes block module", or "search engine verification", for example), CIDRAM needs to be able to obtain the hostname of inbound requests somehow. Typically, it does this by requesting the hostname of the IP address of inbound requests from a DNS server, or by requesting the information through functionality provided by the system where CIDRAM is installed (this is typically referred to as a "hostname lookup"). The DNS servers defined by default belong to the [Google DNS](https://dns.google.com/) service (but this can be easily changed via configuration). The exact services communicated with is configurable, and depends on how you configure the package. In the case of using functionality provided by the system where CIDRAM is installed, you'll need to contact your system administrator to determine which routes hostname lookups use. Hostname lookups can be prevented in CIDRAM by avoiding the affected modules or by modifying the package configuration in accordance with your needs.

*Relevant configuration directives:*
- `general` -> `allow_gethostbyaddr_lookup`
- `general` -> `default_dns`
- `general` -> `force_hostname_lookup`
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.1 SEARCH ENGINE VERIFICATION AND SOCIAL MEDIA VERIFICATION

When search engine verification is enabled, CIDRAM attempts to perform "forward DNS lookups" to verify whether requests claiming to originate from search engines are authentic. Similarly, when social media verification is enabled, CIDRAM does the same for apparent social media requests. To do this, it uses the [Google DNS](https://dns.google.com/) service to attempt to resolve IP addresses from the hostnames of these inbound requests (in this process, the hostnames of these inbound requests is shared with the service).

*Relevant configuration directives:*
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.2 CAPTCHA

CIDRAM supports reCAPTCHA and hCAPTCHA. They require API keys in order to be work correctly. They are disabled by default, but may be enabled by configuring the required API keys. When enabled, communication may occur between the service and CIDRAM or the user's browser. This may potentially involve communicating information such as the user's IP address, user agent, operating system, and other details available to the request.

##### 9.2.3 STOP FORUM SPAM

[Stop Forum Spam](https://www.stopforumspam.com/) is a fantastic, freely available service that can help to protect forums, blogs, and websites from spammers. It does this by providing a database of known spammers, and an API that can be leveraged to check whether an IP address, username, or email address is listed on its database.

CIDRAM provides an optional module that leverages this API to check whether the IP address of inbound requests belongs to a suspected spammer. When the module is installed and activated, user IP addresses may be shared with the service in accordance with the configuration and the intended purpose of the module.

##### 9.2.4 ABUSEIPDB

CIDRAM provides an optional module to block abusive IP addresses using the [AbuseIPDB](https://www.abuseipdb.com/) API. When the module is installed and activated, user IP addresses may be shared with the service in accordance with the configuration and the intended purpose of the module.

##### 9.2.5 BGPVIEW

CIDRAM provides an optional module to perform ASN and country code lookups using the [BGPView](https://bgpview.io/) API. These lookups provide the ability to block or whitelist requests on the basis of their ASN or country of origin. When the module is installed and activated, user IP addresses may be shared with the service in accordance with the configuration and the intended purpose of the module.

##### 9.2.6 PROJECT HONEYPOT

CIDRAM provides an optional module to block abusive IP addresses using the [Project Honeypot](https://www.projecthoneypot.org/) API. When the module is installed and activated, user IP addresses may be shared with the service in accordance with the configuration and the intended purpose of the module.

#### 9.3 LOGGING

Logging is an important part of CIDRAM for a number of reasons. It may be difficult to diagnose and resolve false positives when the block events that cause them aren't logged. Without logging block events, it may be difficult to ascertain exactly how performant CIDRAM is in any particular context, and it may be difficult to determine where its shortfalls may be, and what changes may be required to its configuration or signatures accordingly, in order for it to continue functioning as intended. Regardless, logging mightn't be desirable for all users, and remains entirely optional. In CIDRAM, logging is disabled by default. To enable it, CIDRAM must be configured accordingly.

Additionally, whether logging is legally permissible, and to the extent that it is legally permissible (e.g., the types of information that may be logged, for how long, and under what circumstances), may vary, depending on jurisdiction and on the context where CIDRAM is implemented (e.g., whether you're operating as an individual, as a corporate entity, and whether on a commercial or non-commercial basis). It may therefore be useful for you to read through this section carefully.

There are multiple types of logging that CIDRAM can perform. Different types of logging involves different types of information, for different reasons.

##### 9.3.0 BLOCK EVENTS

The primary type of logging that CIDRAM can perform relates to "block events". This type of logging relates to when CIDRAM blocks a request, and can be provided in three different formats:
- Human readable logfiles.
- Apache-style logfiles.
- Serialised logfiles.

A block event, logged to a human readable logfile, typically looks something like this (as an example):

```
ID: 1234
Script Version: CIDRAM v1.6.0
Date/Time: Day, dd Mon 20xx hh:ii:ss +0000
IP Address: x.x.x.x
Hostname: dns.hostname.tld
Signatures Count: 1
Signatures Reference: x.x.x.x/xx
Why Blocked: Cloud service ("Network Name", Lxx:Fx, [XX])!
User Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
Reconstructed URI: https://your-site.tld/index.php
CAPTCHA State: Enabled.
```

That same block event, logged to an Apache-style logfile, would look something like this:

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

A logged block event typically includes the following information:
- An ID number referencing the block event.
- The version of CIDRAM currently in use.
- The date and time that the block event occurred.
- The IP address of the blocked request.
- The hostname of the IP address of the blocked request (when available).
- The number of signatures triggered by the request.
- References to the signatures triggered.
- References to the reasons for the block event and some basic, related debug information.
- The user agent of the blocked request (i.e., how the requesting entity identified itself to the request).
- A reconstruction of the identifier for the resource originally requested.
- The CAPTCHA state for the current request (when relevant).

*The configuration directives responsible for this type of logging, and for each of the three formats available, are:*
- `logging` -> `apache_style_log`
- `logging` -> `serialised_log`
- `logging` -> `standard_log`

When these directives are left empty, this type of logging will remain disabled.

##### 9.3.1 CAPTCHA LOGGING

This type of logging relates specifically to CAPTCHA instances, and occurs only when a user attempts to complete a CAPTCHA instance.

A CAPTCHA log entry contains the IP address of the user attempting to complete a CAPTCHA instance, the date and time that the attempt occurred, and the CAPTCHA state. A CAPTCHA log entry typically looks something like this (as an example):

```
IP Address: x.x.x.x - Date/Time: Day, dd Mon 20xx hh:ii:ss +0000 - CAPTCHA State: Passed!
```

*The configuration directive responsible for CAPTCHA logging is:*
- `hcaptcha` -> `hcaptcha_log`
- `recaptcha` -> `recaptcha_log`

##### 9.3.2 FRONT-END LOGGING

This type of logging relates front-end login attempts, and occurs only when a user attempts to log into the front-end (assuming front-end access is enabled).

A front-end log entry contains the IP address of the user attempting to log in, the date and time that the attempt occurred, and the results of the attempt (successfully logged in, or failed to log in). A front-end log entry typically looks something like this (as an example):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Logged in.
```

*The configuration directive responsible for front-end logging is:*
- `frontend` -> `frontend_log`

##### 9.3.3 LOG ROTATION

You may want to purge logs after a period of time, or may be required to do so by law (i.e., the amount of time that it's legally permissible for you to retain logs may be limited by law). You can achieve this by including date/time markers in the names of your logfiles as per specified by your package configuration (e.g., `{yyyy}-{mm}-{dd}.log`), and then enabling log rotation (log rotation allows you to perform some action on logfiles when specified limits are exceeded).

For example: If I was legally required to delete logs after 30 days, I could specify `{dd}.log` in the names of my logfiles (`{dd}` represents days), set the value of `log_rotation_limit` to 30, and set the value of `log_rotation_action` to `Delete`.

Conversely, if you're required to retain logs for an extended period of time, you could either not use log rotation at all, or you could set the value of `log_rotation_action` to `Archive`, to compress logfiles, thereby reducing the total amount of disk space that they occupy.

*Relevant configuration directives:*
- `logging` -> `log_rotation_action`
- `logging` -> `log_rotation_limit`

##### 9.3.4 LOG TRUNCATION

It's also possible to truncate individual logfiles when they exceed a certain size, if this is something you might need or want to do.

*Relevant configuration directives:*
- `logging` -> `truncate`

##### 9.3.5 IP ADDRESS PSEUDONYMISATION

Firstly, if you're not familiar with the term, "pseudonymisation" refers to the processing of personal data as such that it can't be identified to any specific data subject anymore without supplementary information, and provided that such supplementary information is maintained separately and subject to technical and organisational measures to ensure that personal data can't be identified to any natural person.

The following resources can help to explain it in more detail:
- [[trust-hub.com] What is pseudonymisation?](https://www.trust-hub.com/news/what-is-pseudonymisation/)
- [[dataprotection.ie] Anonymisation and pseudonymisation](https://www.dataprotection.ie/docs/Anonymisation-and-pseudonymisation/1594.htm)
- [[Wikipedia] Pseudonymization](https://en.wikipedia.org/wiki/Pseudonymization)

In some circumstances, you may be legally required to anonymise or pseudonymise any PII collected, processed, or stored. Although this concept has existed for quite some time now, GDPR/DSGVO notably mentions, and specifically encourages "pseudonymisation".

CIDRAM is able to pseudonymise IP addresses when logging them, if this is something you might need or want to do. When CIDRAM pseudonymises IP addresses, when logged, the final octet of IPv4 addresses, and everything after the second part of IPv6 addresses is represented by an "x" (effectively rounding IPv4 addresses to the initial address of the 24th subnet they factor into, and IPv6 addresses to the initial address of the 32nd subnet they factor into).

*Note: CIDRAM's IP address pseudonymisation process doesn't affect CIDRAM's IP tracking feature. If this is a problem for you, it may be best to disable IP tracking entirely.*

*Relevant configuration directives:*
- `legal` -> `pseudonymise_ip_addresses`

##### 9.3.6 OMITTING LOG INFORMATION

If you want to take it a step further by preventing specific types of information from being logged entirely, this is also possible to do. At the configuration page, please refer to the `fields` configuration directive to control which fields appear in log entries and on the "Access Denied" page.

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

*Note: There's no reason to pseudonymise IP addresses when omitting them from logs entirely.*

*Relevant configuration directives:*
- `general` -> `fields`

##### 9.3.7 STATISTICS

CIDRAM is optionally able to track statistics such as the total number of block events or CAPTCHA instances that have occurred since some particular point in time. This feature is disabled by default, but can be enabled via the package configuration. This feature only tracks the total number of events occurred, and doesn't include any information about specific events (and therefore, shouldn't be regarded as PII).

*Relevant configuration directives:*
- `general` -> `statistics`

##### 9.3.8 ENCRYPTION

CIDRAM doesn't encrypt its cache or any log information. Cache and log [encryption](https://en.wikipedia.org/wiki/Encryption) may be introduced in the future, but there aren't any specific plans for it currently. If you're concerned about unauthorised third parties gaining access to parts of CIDRAM that may contain PII or sensitive information such as its cache or logs, I would recommend that CIDRAM not be installed at a publicly accessible location (e.g., install CIDRAM outside the standard `public_html` directory or equivalent thereof available to most standard webservers) and that appropriately restrictive permissions be enforced for the directory where it resides (in particular, for the vault directory). If that isn't sufficient to address your concerns, then configure CIDRAM as such that the types of information causing your concerns won't be collected or logged in the first place (such as, by disabling logging).

#### 9.4 COOKIES

CIDRAM sets [cookies](https://en.wikipedia.org/wiki/HTTP_cookie) at two points in its codebase. Firstly, when a user successfully completes a CAPTCHA instance (and assuming that `lockuser` is set to `true`), CIDRAM sets a cookie in order to be able to remember for subsequent requests that the user has already completed a CAPTCHA instance, so that it won't need to continuously ask the user to complete a CAPTCHA instance on subsequent requests. Secondly, when a user successfully logs into the front-end, CIDRAM sets a cookie in order to be able to remember the user for subsequent requests (i.e., cookies are used to authenticate the user to a login session).

In both cases, cookie warnings are displayed prominently (when applicable), warning the user that cookies will be set if they engage in the relevant actions. Cookies aren't set at any other points in the codebase.

*Note: The "invisible" CAPTCHA APIs might be incompatible with cookie laws in some jurisdictions, and should be avoided by any websites subject to such laws. Opting to use the other provided APIs instead, or simply disabling CAPTCHAs entirely, may be preferable.*

*Relevant configuration directives:*
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 9.5 MARKETING AND ADVERTISING

CIDRAM doesn't collect or process any information for marketing or advertising purposes, and neither sells nor profits from any collected or logged information. CIDRAM is not a commercial enterprise, nor is related to any commercial interests, so doing these things wouldn't make any sense. This has been the case since the beginning of the project, and continues to be the case today. Additionally, doing these things would be counter-productive to the spirit and intended purpose of the project as a whole, and for as long as I continue to maintain the project, will never happen.

#### 9.6 PRIVACY POLICY

In some circumstances, you may be legally required to clearly display a link to your privacy policy on all pages and sections of your website. This may be important as a means to ensure that users are well-informed of your exact privacy practices, the types of PII you collect, and how you intend to use it. In order to be able to include such a link on CIDRAM's "Access Denied" page, a configuration directive is provided to specify the URL to your privacy policy.

*Note: It's strongly recommended that your privacy policy page isn't placed behind CIDRAM's protection. If CIDRAM protects your privacy policy page, and a user blocked by CIDRAM clicks the link to your privacy policy, they'll just be blocked again, and won't be able to see your privacy policy. Ideally, you should link to a static copy of your privacy policy, such as an HTML page or plain-text file which isn't protected by CIDRAM.*

*Relevant configuration directives:*
- `legal` -> `privacy_policy`

#### 9.7 GDPR/DSGVO

The General Data Protection Regulation (GDPR) is a regulation of the European Union, which comes into effect as of May 25, 2018. The primary goal of the regulation is to give control to EU citizens and residents regarding their own personal data, and to unify regulation within the EU concerning privacy and personal data.

The regulation contains specific provisions pertaining to the processing of "[personally identifiable information](https://en.wikipedia.org/wiki/Personal_data)" (PII) of any "data subjects" (any identified or identifiable natural person) either from or within the EU. To be compliant with the regulation, "enterprises" (as per defined by the regulation), and any relevant systems and processes must implement "[privacy by design](https://en.wikipedia.org/wiki/Privacy_by_design)" by default, must use the highest possible privacy settings, must implement necessary safeguards for any stored or processed information (including, but not limited to, the implementation of pseudonymisation or full anonymisation of data), must clearly and unambiguously declare the types of data they collect, how they process it, for what reasons, for how long they retain it, and whether they share this data with any third parties, the types of data shared with third parties, how, why, and so on.

Data may not be processed unless there's a lawful basis for doing so, as per defined by the regulation. Generally, this means that in order to process a data subject's data on a lawful basis, it must be done in compliance with legal obligations, or done only after explicit, well-informed, unambiguous consent has been obtained from the data subject.

Because aspects of the regulation may evolve in time, in order to avoid the propagation of outdated information, it may be better to learn about the regulation from an authoritative source, as opposed to simply including the relevant information here in the package documentation (which may eventually become outdated as the regulation evolves).

[EUR-Lex](https://eur-lex.europa.eu/) (a part of the official website of the European Union that provides information about EU law) provides extensive information about GDPR/DSGVO, available in 24 different languages (at the time of writing this), and available for download in PDF format. I would definitely recommend reading the information that they provide, in order to learn more about GDPR/DSGVO:
- [REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679)

[Intersoft Consulting](https://www.intersoft-consulting.de/) also provides extensive information about GDPR/DSGVO, available in German and English, which could be useful to learn more about GDPR/DSGVO:
- [General Data Protection Regulation (GDPR) – Final text neatly arranged](https://gdpr-info.eu/)

Alternatively, there's a brief (non-authoritative) overview of GDPR/DSGVO available at Wikipedia:
- [General Data Protection Regulation](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation)

---


### 10. <a name="SECTION10"></a>UPGRADING FROM PREVIOUS MAJOR VERSIONS

#### 10.0 CIDRAM v3

There are significant differences between v3 and previous major versions. Importantly, the way entrypoints work, the way modules are structured, and the way the updater works for v3 is different to the way those things worked for previous major versions. Because of these differences, the best way to upgrade to v3 from previous major versions would be to perform a fresh installation.

If you want to keep your configuration and your auxiliary rules, before beginning the upgrade process, go to the front-end backup page. From there, configuration and auxiliary rules can be exported. Exporting will cause a file to be downloaded. After upgrading to the new major version, that file can be used to import the previously exported data to the installation.

Because of changes to the way modules are structured, modules intended for previous major versions would need to be rewritten in order to work properly for v3. Direct migration won't work. The same is true for events.

The way signature files are structured has not changed, so signature files intended for previous major verions can be directly migrated into v3 without any problems anticipated.

Since v3, modules, signature files, and events each have their own dedicated directories (so, for v3, they would each go into their respective dedicated directories, instead of the root of the vault).

Some of the signature files, modules, and blocklists publicly available for previous major versions have been deprecated, so not everything will be available for v3. In most cases, they won't be needed anyway, due to new features and core functionality added since v3.

There are some subtle changes to the way auxiliary rules are structured, and there are changes to the configuration, but if you use the import/export feature at the front-end backup page, you won't need to manually rewrite, adjust, or recreate anything. When importing, CIDRAM knows what's needed, and will handle it for you automatically.

#### 10.1 CIDRAM v4

CIDRAM v4 doesn't yet exist. However, when the time comes to upgrade from v3 to v4, the upgrade process should be much simpler. We won't know exactly how significantly different it will be until the time comes, but I anticipate the differences to be much less than before, and mechanisms have already been implemented into v3 right from the start to facilitate a smoother upgrade process. As long as there aren't significant changes to the updater or the way that entrypoints work, it should, in theory, be possible to upgrade entirely via the front-end, without the need to perform a fresh installation.

More detailed information will be included here, in the documentation, at an appropriate time in the future.

---


Last Updated: 24 July 2023 (2023.07.24).
