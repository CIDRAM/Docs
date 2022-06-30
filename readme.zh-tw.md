## CIDRAM v3 中文（傳統）文檔。

### 內容
- 1. [前言](#SECTION1)
- 2. [如何安裝](#SECTION2)
- 3. [如何使用](#SECTION3)
- 4. [前端管理](#SECTION4)
- 5. [配置選項](#SECTION5)
- 6. [簽名格式](#SECTION6)
- 7. [已知的兼容問題](#SECTION7)
- 8. [常見問題（FAQ）](#SECTION8)
- 9. [法律信息](#SECTION9)

*翻譯註釋：如果錯誤（例如，​翻譯差異，​錯別字，​等等），​英文版這個文件是考慮了原版和權威版。​如果您發現任何錯誤，​您的協助糾正他們將受到歡迎。​*

---


### 1. <a name="SECTION1"></a>前言

CIDRAM （無類別域間路由訪問管理器）是一個PHP腳本，​旨在保護網站途經阻止請求該從始發IP地址視為不良的流量來源，​包括（但不限於）流量該從非人類的訪問端點，​雲服務，​垃圾郵件發送者，​網站鏟運機，​等等。​它通過計算CIDR的提供的IP地址從入站請求和試圖匹配這些CIDR反對它的簽名文件（這些簽名文件包含CIDR的IP地址視為不良的流量來源）；如果找到匹配，​請求被阻止。

*(看到：[什麼是『CIDR』？​](#WHAT_IS_A_CIDR))。​*

[CIDRAM](https://cidram.github.io/) COPYRIGHT 2016 和走向未來 GNU/GPLv2 由 [Caleb M (Maikuolan)](https://github.com/Maikuolan)。

本腳本是基於GNU通用許可V2.0版許可協議發布的，​您可以在許可協議的允許範圍內自行修改和發布，​但請遵守GNU通用許可協議。​使用腳本的過程中，​作者不提供任何擔保和任何隱含擔保。​更多的細節請參見GNU通用公共許可證，​下的`LICENSE.txt`文件也可從訪問：
- <https://www.gnu.org/licenses/>。
- <https://opensource.org/licenses/>。

現在CIDRAM的代碼文件和關聯包可以從以下地址免費下載：
- [GitHub](https://github.com/CIDRAM/CIDRAM)。
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram)。
- [SourceForge](https://sourceforge.net/projects/cidram/)。

---


### 2. <a name="SECTION2"></a>如何安裝

#### 2.0 安裝手工

首先，您需要一個新的CIDRAM副本。​您可以從[CIDRAM/CIDRAM](https://github.com/CIDRAM/CIDRAM)存儲庫下載最新版本的CIDRAM存檔。​具體來說，您需要一個『vault』目錄的新副本​（存檔中的所有其他內容都可以安全的刪除或忽略）。

在v3之前，必須在公共根目錄中的某個位置安裝CIDRAM，以便能夠訪問CIDRAM前端。​但是，從v3開始，這不是必需的。​現在，為了最大限度地提高安全性並防止未經授權訪問CIDRAM及其文件，建議將CIDRAM安裝在公共根目錄之外。​只要PHP可以訪問它，只要它是安全的，只要您對它感到滿意，您就可以在任何地方安裝CIDRAM。​不再需要將目錄名稱保留為『vault』，因此您可以將其重命名為您想要的任何名稱​（但為了方便起見，文檔將繼續將其稱為『vault』目錄）。

當您準備好，將『vault』目錄上傳到您選擇的位置，並確保它具有必要的權限，以便PHP能夠寫入該目錄​（根據系統，您可能不需要做任何事情，或者您可能需要將CHMOD 755設置為目錄，或者如果755有問題，您可以試試777，但不推薦777因為它不太安全）。

接下來，為了讓CIDRAM能夠保護您的代碼庫或CMS，您需要創建一個『入口點』。​這樣的入口點包括三件事：

1. 在代碼庫或CMS的適當位置包含『loader.php』文件。
2. CIDRAM core的實例化。
3. 調用『protect』方法。

簡單的例子：

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

如果您使用Apache網絡服務器並且可以訪問`php.ini`，則可以使用`auto_prepend_file`指令在任何PHP請求發出時執行CIDRAM。​在這種情況下，創建入口點的最合適位置是在其自己的文件中，然後您將在`auto_prepend_file`指令中引用該文件。

例子：

`auto_prepend_file = "/path/to/your/entrypoint.php"`

或者在`.htaccess`文件中：

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

在其他情況下，創建入口點的最合適位置可能是在代碼庫或CMS中的最早點。​這確保了每當訪問您網站上的頁面時它總是會執行。​如果您的代碼庫使用『引導程序』，那麼該文件的開頭就是一個很好的例子。​如果您的代碼庫有一個中央文件負責連接到您的數據庫，那麼該文件的開頭將是另一個很好的例子。

#### 2.1 與COMPOSER安裝

[CIDRAM是在Packagist上](https://packagist.org/packages/cidram/cidram)，​所以，​如果您熟悉Composer，​您可以使用Composer安裝CIDRAM。

`composer require cidram/cidram`

#### 2.2 為WORDPRESS安裝

[CIDRAM在WordPress插件數據庫中註冊](https://wordpress.org/plugins/cidram/)，​您可以直接從插件儀表板安裝CIDRAM。​您可以像其他插件一樣安裝，​不需要添加步驟。

*警告：在插件儀表板裡更新CIDRAM會導致乾淨的安裝！​如果您已經自定義了您的安裝（更改了您的配置，​安裝的模塊等），​在插件儀表板裡進行更新時，​這些定制將會丟失！​日誌文件也將丟失！​要保留日誌文件和自定義，​請通過CIDRAM前端更新頁面進行更新。​*

#### 2.3 配置和定制

強烈建議您檢查新安裝的配置，以便能夠根據需要進行調整。​您可能還想安裝其他模塊、簽名文件、創建輔助規則、或實施其他自定義，以便您的安裝能夠最好地滿足您的需求。​我建議使用前端來做這些事情。

---


### 3. <a name="SECTION3"></a>如何使用

CIDRAM 應自動阻止不良的請求至您的網站，​沒有任何需求除了初始安裝。

您可以定制您的配置和您可以定制什麼CIDR被阻止通過修改您的配置文件和/或您的簽名文件.

如果您遇到任何假陽性，​請聯繫我讓我知道這件事。 *(看到：[什麼是『假陽性』？​](#WHAT_IS_A_FALSE_POSITIVE))。​*

CIDRAM可以手動或通過前端更新。​CIDRAM也可以通過Composer或WordPress更新，如果最初通過這些方式安裝的話。

---


### 4. <a name="SECTION4"></a>前端管理

#### 4.0 什麼是前端。

前端提供了一種方便，​輕鬆的方式來維護，​管理和更新CIDRAM安裝。​您可以通過日誌頁面查看，​共享和下載日誌文件，​您可以通過配置頁面修改配置，​您可以通過更新頁面安裝和卸載組件，​和您可以通過文件管理器上傳，​下載和修改文件在vault。

#### 4.1 如何訪問前端。

就像以前一樣，您需要創建一個入口點才能訪問前端。​這樣的入口點包括三件事：

1. 在代碼庫或CMS的適當位置包含『loader.php』文件。
2. CIDRAM front-end的實例化。
3. 調用『view』方法。

簡單的例子：

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

『FrontEnd』類擴展了『Core』類。​這意味著您可以在調用『view』方法之前調用『protect』方法，以阻止可能不需要的流量訪問前端。​這樣做完全是可選的。

簡單的例子：

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

為前端創建入口點的最合適位置是在其自己的專用文件中。​與以前不同，您希望前端入口點只能通過直接請求入口點所在的特定文件來訪問。​因此，您不想在此處使用`auto_prepend_file`或`.htaccess`。

創建前端入口點後，使用瀏覽器訪問它。​應該顯示一個登錄頁面。​在登錄頁面，輸入默認用戶名和密碼（admin/password），然後按登錄按鈕。

注意：第一次登錄後，​以防止未經授權的訪問前端，​您應該立即更改您的用戶名和密碼！​這是非常重要的，​因為它可以任意PHP代碼上傳到您的網站通過前端。

此外，為了獲得最佳安全性，強烈建議為所有前端帳戶啟用『雙因素身份驗證』（下面提供的說明）。

#### 4.2 如何使用前端。

每個前端頁面上都有說明，​用於解釋正確的用法和它的預期目的。​如果您需要進一步的解釋或幫助，​請聯繫支持。​另外，​YouTube上還有一些演示視頻。

#### 4.3 2FA（雙因素身份驗證）

通過啟用雙因素身份驗證，可以使前端更安全。​當登錄使用2FA的帳戶時，會向與該帳戶關聯的電子郵件地址發送電子郵件。​此電子郵件包含『2FA代碼』，用戶必須輸入它（以及他們的用戶名和密碼），為了能夠使用該帳戶登錄。​這意味著獲取帳戶密碼不足以讓任何黑客或潛在攻擊者能夠帳戶登錄，因為他們還需要訪問帳戶的電子郵件地址才能接收和使用會話的2FA代碼（從而使前端更安全）。

首先，為了啟用雙因素身份驗證，請使用前端更新頁面來安裝PHPMailer組件。​CIDRAM使用PHPMailer發送電子郵件。

在安裝PHPMailer後，您需要通過CIDRAM配置頁面或配置文件填充PHPMailer的配置指令。​有關這些配置指令的更多信息包含在本文檔的配置部分中。​在填充PHPMailer配置指令後，將`enable_two_factor`設置為`true`。​現在應啟用雙因素身份驗證。

接下來，您需要讓CIDRAM知道在使用該帳戶登錄時將2FA代碼發送到何處。​為此，請使用電子郵件地址作為帳戶的用戶名（例如，`foo@bar.tld`），或者將電子郵件地址作為用戶名的一部分包括在內，就像通常發送電子郵件一樣（例如，`Foo Bar <foo@bar.tld>`）。

注意：保護您的vault免受未經授權的訪問（例如，通過加強服務器的安全性和限制公共訪問權限）在此非常重要，因為未經授權訪問您的配置文件（存儲在您的vault中）可能會暴露您的出站SMTP設置（包括SMTP用戶名和密碼）。​在啟用雙因素身份驗證之前，應確保您的vault已正確保護。​如果您無法做到這一點，那麼至少應該創建一個專門用於此目的的新電子郵件帳戶，為了降低與暴露的SMTP設置相關的風險。

---


### 5. <a name="SECTION5"></a>配置選項

下列是一個列表的變量發現在`config.yml`配置文件的CIDRAM，​以及一個說明的他們的目的和功能。

```
配置 (v3)
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
│       lang [string]
│       lang_override [bool]
│       numbers [string]
│       emailaddr [string]
│       emailaddr_display_style [string]
│       ban_override [int]
│       default_dns [string]
│       search_engine_verification [string]
│       social_media_verification [string]
│       other_verification [string]
│       default_algo [string]
│       statistics [string]
│       force_hostname_lookup [bool]
│       allow_gethostbyaddr_lookup [bool]
│       disabled_channels [string]
│       default_timeout [int]
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
│       remotes [string]
│       enable_two_factor [bool]
├───signatures
│       block_attacks [bool]
│       block_cloud [bool]
│       block_bogons [bool]
│       block_generic [bool]
│       block_legal [bool]
│       block_malware [bool]
│       block_proxies [bool]
│       block_spam [bool]
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
├───rate_limiting
│       max_bandwidth [string]
│       max_requests [int]
│       precision_ipv4 [int]
│       precision_ipv6 [int]
│       allowance_period [float]
│       exceptions [string]
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
├───abuseipdb
│       api_key [string]
│       max_age_in_days [int]
│       minimum_confidence_score [int]
│       max_cs_for_captcha [int]
│       minimum_total_reports [int]
│       report_back [bool]
│       lookup_strategy [int]
│       build_profiles_from_usage_type [bool]
├───bgpview
│       blocked_asns [string]
│       whitelisted_asns [string]
│       blocked_ccs [string]
│       whitelisted_ccs [string]
├───bunnycdn
│       positive_action [string]
├───bypasses
│       used [string]
├───extras
│       signatures [string]
├───projecthoneypot
│       api_key [string]
│       max_age_in_days [int]
│       minimum_threat_score [int]
│       max_ts_for_captcha [int]
│       lookup_strategy [int]
└───sfs
        offer_captcha [bool]
```

#### 『general』 （類別）
基本配置（任何不屬於其他類別的核心配置）。

##### 『stages』 `[string]`
- 用於執行鏈的各個階段的控件（是否啟用，是否記錄錯誤，等等）。

```
stages
├─Tests ("執行簽名文件測試")
├─Modules ("執行模塊")
├─SearchEngineVerification ("執行搜索引擎驗證")
├─SocialMediaVerification ("執行社交媒體驗證")
├─OtherVerification ("執行其他驗證")
├─Aux ("執行輔助規則")
├─Reporting ("執行報告")
├─Tracking ("執行IP跟踪")
├─RL ("執行速率限制")
├─CAPTCHA ("部署驗證碼（被阻止的請求）")
├─Statistics ("更新統計")
├─Webhooks ("執行webhook")
├─PrepareFields ("為輸出和日誌準備字段")
├─Output ("生成輸出（被阻止的請求）")
├─WriteLogs ("寫入日誌（被阻止的請求）")
├─Terminate ("終止請求（被阻止的請求）")
├─AuxRedirect ("根據輔助規則重定向")
└─NonBlockedCAPTCHA ("部署驗證碼（非阻止的請求）")
```

##### 『fields』 `[string]`
- 用於阻止事件的字段控件（當請求被阻止時）。

```
fields
├─ID ("ID")
├─ScriptIdent ("腳本版本")
├─DateTime ("日期/時間")
├─IPAddr ("IP地址")
├─IPAddrResolved ("IP地址（解決）")
├─Query ("網頁查詢")
├─Referrer ("引薦")
├─UA ("用戶代理")
├─UALC ("用戶代理（小寫）")
├─SignatureCount ("簽名計數")
├─Signatures ("簽名參考")
├─WhyReason ("為什麼被阻止")
├─ReasonMessage ("為什麼被阻止（詳細）")
├─rURI ("重建URI")
├─Infractions ("違規")
├─ASNLookup ("ASN查詢")
├─CCLookup ("國家代碼查詢")
├─Verified ("身份驗證")
├─Expired ("已過期")
├─Ignored ("忽略了")
├─Request_Method ("請求方法")
├─Hostname ("主機名")
└─CAPTCHA ("CAPTCHA狀態")
```

##### 『timezone』 `[string]`
- 這用於指定要使用的時區​（例如，Africa/Cairo，America/New_York，Asia/Tokyo，Australia/Perth，Europe/Berlin，Pacific/Guam，等等）。​指定『SYSTEM』使PHP自動為您處理。

```
timezone
├─SYSTEM ("使用系統默認時區。")
├─UTC ("UTC")
└─…其他
```

##### 『time_offset』 `[int]`
- 時區偏移量（分鐘）。

##### 『time_format』 `[string]`
- CIDRAM使用的日期符號格式。​可根據要求增加附加選項。

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
└─…其他
```

##### 『ipaddr』 `[string]`
- 在哪裡可以找到連接請求IP地址？​（可以使用為服務例如Cloudflare和類似）。​標準 = REMOTE_ADDR。​警告：不要修改此除非您知道什麼您做著！

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (標準)")
└─…其他
```

也可以看看：
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### 『http_response_header_code』 `[int]`
- 阻止請求時，CIDRAM應發送哪個HTTP狀態消息？

```
http_response_header_code
├─200 (200 OK （好的）): 最不健壯，但最用戶友好。​自動請求很可能將此響應解釋為成功。
├─403 (403 Forbidden （禁止的）): 更健壯，但不太用戶友好。​一般最推薦的。
├─410 (410 Gone （走了）): 解決假陽性時可能會導致問題，因為某些瀏覽器會緩存此狀態消息並且不會發送後續請求，即使在被解除阻止後也是如此。​在某些情況下可能是最可取的。
├─418 (418 I'm a teapot （我是一個茶壺）): 引用愚人節的笑話【{{Links.RFC2324}}】。​任何客戶端、機器人、瀏覽器、或其他方式都不太可能理解。​它是為了娛樂和方便而提供的，但是通常不推薦。
├─451 (451 Unavailable For Legal Reasons （因法律原因不可用）): 主要出於法律原因被阻止時推薦。​不推薦在其他情況下。
└─503 (503 Service Unavailable （服務不可用）): 最健壯，但最不用戶友好。​推薦用於受到攻擊，或處理極其持久的有害流量時。
```

##### 『silent_mode』 `[string]`
- CIDRAM應該默默重定向被攔截的訪問而不是顯示該『拒絕訪問』頁嗎？​指定位置至重定向被攔截的訪問，​或讓它空將其禁用。

##### 『lang』 `[string]`
- 指定標準CIDRAM語言。

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

##### 『lang_override』 `[bool]`
- 盡可能根據HTTP_ACCEPT_LANGUAGE進行本地化？True（真）=進行本地化【標準】；False（假）=不要本地化。

##### 『numbers』 `[string]`
- 您如何喜歡顯示數字？​選擇最適合示例。

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

##### 『emailaddr』 `[string]`
- 如果您希望，​您可以提供電子郵件地址這裡要給予用戶當他們被阻止，​他們使用作為接觸點為支持和/或幫助在的情況下他們錯誤地阻止。​警告:您提供的任何電子郵件地址，​它肯定會被獲得通過垃圾郵件機器人和鏟運機，​所以，​它強烈推薦如果選擇提供一個電子郵件地址這裡，​您保證它是一次性的和/或不是很重要（換一種說法，​您可能不希望使用您的主電子郵件地址或您的企業電子郵件地址）。

##### 『emailaddr_display_style』 `[string]`
- 您希望如何將電子郵件地址呈現給用戶？

```
emailaddr_display_style
├─default ("可點擊的鏈接")
└─noclick ("不可點擊的文字")
```

##### 『ban_override』 `[int]`
- 覆蓋『http_response_header_code』當『infraction_limit』已被超過？​當覆蓋：已阻止的請求返回一個空白頁（不使用模板文件）。​200 = 不要覆蓋【標準】。​其他值與『http_response_header_code』的可用值相同。

```
ban_override
├─200 (200 OK （好的）): 最不健壯，但最用戶友好。​自動請求很可能將此響應解釋為成功。
├─403 (403 Forbidden （禁止的）): 更健壯，但不太用戶友好。​一般最推薦的。
├─410 (410 Gone （走了）): 解決假陽性時可能會導致問題，因為某些瀏覽器會緩存此狀態消息並且不會發送後續請求，即使在被解除阻止後也是如此。​在某些情況下可能是最可取的。
├─418 (418 I'm a teapot （我是一個茶壺）): 引用愚人節的笑話【{{Links.RFC2324}}】。​任何客戶端、機器人、瀏覽器、或其他方式都不太可能理解。​它是為了娛樂和方便而提供的，但是通常不推薦。
├─451 (451 Unavailable For Legal Reasons （因法律原因不可用）): 主要出於法律原因被阻止時推薦。​不推薦在其他情況下。
└─503 (503 Service Unavailable （服務不可用）): 最健壯，但最不用戶友好。​推薦用於受到攻擊，或處理極其持久的有害流量時。
```

##### 『default_dns』 `[string]`
- DNS服務器列表，​用於主機名查找。​警告：不要修改此除非您知道什麼您做著！

__常問問題。__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.zh-tw.md#WHAT_CAN_I_USE_FOR_DEFAULT_DNS" hreflang="zh-TW">在『default_dns』中我可以使用什麼？</a></em>

##### 『search_engine_verification』 `[string]`
- 用於驗證來自搜索引擎的請求的控件。

```
search_engine_verification
├─Amazonbot ("Amazonbot")
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

__什麼是『陽性』和『陰性』？__ 在驗證請求提供的身份時，成功的結果可以描述為『陽性』或『陰性』。​當所呈現的身份被確認為真實身份時，將被描述為『陽性』。​當所提供的身份被證實為偽造時，將被描述為『陰性』。​但是，不成功的結果（例如，驗證失敗，或無法確定所提供身份的真實性）不會被描述為『陽性』或『陰性』。​相反，不成功的結果將被簡單地描述為未驗證。​當沒有嘗試驗證請求提供的身份時，該請求同樣會被描述為未驗證。​這些術語僅在請求提供的身份被識別的情況下才有意義，因此，在可以進行驗證的情況下。​如果提供的身份與上面提供的選項不匹配，或者沒有提供身份，則上面提供的選項變得無關。

__什麼是『一擊繞過』？__ 在某些情況下，由於簽名文件、模塊、或請求的其他條件，可能仍會阻止經過肯定驗證的請求，為了避免誤報，可能需要繞過。​在繞過旨在處理僅一項違規行為的情況下，這樣的繞過可以被描述為『一擊繞過』。

##### 『social_media_verification』 `[string]`
- 用於驗證來自社交媒體平台的請求的控件。

```
social_media_verification
├─Embedly ("Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("Pinterest")
└─Twitterbot ("Twitterbot")
```

__什麼是『陽性』和『陰性』？__ 在驗證請求提供的身份時，成功的結果可以描述為『陽性』或『陰性』。​當所呈現的身份被確認為真實身份時，將被描述為『陽性』。​當所提供的身份被證實為偽造時，將被描述為『陰性』。​但是，不成功的結果（例如，驗證失敗，或無法確定所提供身份的真實性）不會被描述為『陽性』或『陰性』。​相反，不成功的結果將被簡單地描述為未驗證。​當沒有嘗試驗證請求提供的身份時，該請求同樣會被描述為未驗證。​這些術語僅在請求提供的身份被識別的情況下才有意義，因此，在可以進行驗證的情況下。​如果提供的身份與上面提供的選項不匹配，或者沒有提供身份，則上面提供的選項變得無關。

__什麼是『一擊繞過』？__ 在某些情況下，由於簽名文件、模塊、或請求的其他條件，可能仍會阻止經過肯定驗證的請求，為了避免誤報，可能需要繞過。​在繞過旨在處理僅一項違規行為的情況下，這樣的繞過可以被描述為『一擊繞過』。

** 需要ASN查找功能（例如，通過BGPView模塊）。

##### 『other_verification』 `[string]`
- 用於在可能的情況下，驗證其他類型的請求的控件。

```
other_verification
├─AdSense ("AdSense")
├─AmazonAdBot ("AmazonAdBot")
└─Grapeshot ("Oracle Data Cloud Crawler")
```

__什麼是『陽性』和『陰性』？__ 在驗證請求提供的身份時，成功的結果可以描述為『陽性』或『陰性』。​當所呈現的身份被確認為真實身份時，將被描述為『陽性』。​當所提供的身份被證實為偽造時，將被描述為『陰性』。​但是，不成功的結果（例如，驗證失敗，或無法確定所提供身份的真實性）不會被描述為『陽性』或『陰性』。​相反，不成功的結果將被簡單地描述為未驗證。​當沒有嘗試驗證請求提供的身份時，該請求同樣會被描述為未驗證。​這些術語僅在請求提供的身份被識別的情況下才有意義，因此，在可以進行驗證的情況下。​如果提供的身份與上面提供的選項不匹配，或者沒有提供身份，則上面提供的選項變得無關。

__什麼是『一擊繞過』？__ 在某些情況下，由於簽名文件、模塊、或請求的其他條件，可能仍會阻止經過肯定驗證的請求，為了避免誤報，可能需要繞過。​在繞過旨在處理僅一項違規行為的情況下，這樣的繞過可以被描述為『一擊繞過』。

##### 『default_algo』 `[string]`
- 定義要用於所有未來密碼和會話的算法。

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### 『statistics』 `[string]`
- 控制要跟踪的統計信息。

```
statistics
├─Blocked-IPv4 ("請求已阻止 – IPv4")
├─Blocked-IPv6 ("請求已阻止 – IPv6")
├─Blocked-Other ("請求已阻止 – 其他")
├─Banned-IPv4 ("請求已禁止 – IPv4")
├─Banned-IPv6 ("請求已禁止 – IPv6")
├─Passed-IPv4 ("允許的請求 – IPv4")
├─Passed-IPv6 ("允許的請求 – IPv6")
├─Passed-Other ("允許的請求 – 其他")
├─CAPTCHAs-Failed ("CAPTCHA嘗試 – 失敗！")
└─CAPTCHAs-Passed ("CAPTCHA嘗試 – 成功！")
```

##### 『force_hostname_lookup』 `[bool]`
- 強制主機名查找？​True（真）=跟踪；False（假）=不跟踪【標準】。​主機名查詢通常在『根據需要』的基礎上執行，但可以在所有請求上強制。​這可能會有助於提供日誌文件中更詳細的信息，但也可能會對性能產生輕微的負面影響。

##### 『allow_gethostbyaddr_lookup』 `[bool]`
- 當UDP不可用時允許gethostbyaddr查找？​True（真）=允許【標準】；False（假）=不允許。

注意：IPv6查找在某些32位系統上可能無法正常工作。

##### 『disabled_channels』 `[string]`
- 這可用於防止CIDRAM在發送請求時使用特定通道（例如，在更新時，在獲取組件元數據時，等等）。

```
disabled_channels
├─GitHub ("GitHub")
├─BitBucket ("BitBucket")
└─GoogleDNS ("GoogleDNS")
```

##### 『default_timeout』 `[int]`
- 用於外部請求的默認超時？ 標準 = 12秒。

#### 『components』 （類別）
CIDRAM使用的組件的啟用和停用的配置。​通常由更新頁面填充，但也可以從此處進行管理，以實現更好的控制以及更新頁面無法識別的自定義組件。

##### 『ipv4』 `[string]`
- IPv4簽名文件。

##### 『ipv6』 `[string]`
- IPv6簽名文件。

##### 『modules』 `[string]`
- 模塊。

##### 『imports』 `[string]`
- 進口。​通常用於向CIDRAM提供組件的配置信息。

##### 『events』 `[string]`
- 事件處理程序。​通常用於修改CIDRAM在內部的行為方式或提供附加功能。

#### 『logging』 （類別）
與日誌相關的配置（與其他類別相關的被排除）。

##### 『standard_log』 `[string]`
- 人類可讀文件用於記錄所有被攔截的訪問。​指定一個文件名，​或留空以禁用。

##### 『apache_style_log』 `[string]`
- Apache風格文件用於記錄所有被攔截的訪問。​指定一個文件名，​或留空以禁用。

##### 『serialised_log』 `[string]`
- 連載的文件用於記錄所有被攔截的訪問。​指定一個文件名，​或留空以禁用。

##### 『error_log』 `[string]`
- 用於記錄檢測到的任何非致命錯誤的文件。​指定一個文件名，​或留空以禁用。

##### 『truncate』 `[string]`
- 截斷日誌文件當他們達到一定的大小嗎？​值是在B/KB/MB/GB/TB，​是日誌文件允許的最大大小直到它被截斷。​默認值為『0KB』將禁用截斷（日誌文件可以無限成長）。​注意：適用於單個日誌文件！​日誌文件大小不被算集體的。

##### 『log_rotation_limit』 `[int]`
- 日誌輪轉限制了任何時候應該存在的日誌文件的數量。​當新的日誌文件被創建時，如果日誌文件的指定的最大數量已經超過，將執行指定的操作。​您可以在此指定所需的限制。​值為『0』將禁用日誌輪轉。

##### 『log_rotation_action』 `[string]`
- 日誌輪轉限制了任何時候應該存在的日誌文件的數量。​當新的日誌文件被創建時，如果日誌文件的指定的最大數量已經超過，將執行指定的操作。​您可以在此處指定所需的操作。

```
log_rotation_action
├─Delete ("刪除最舊的日誌文件，直到不再超出限制。")
└─Archive ("首先歸檔，然後刪除最舊的日誌文件，直到不再超出限制。")
```

##### 『log_banned_ips』 `[bool]`
- 包括IP禁止從阻止請求在日誌文件嗎？​True（真）=是【標準】；False（假）=不是。

##### 『log_sanitisation』 `[bool]`
- 當使用前端日誌頁面查看日誌數據時，CIDRAM在顯示之前清理日誌數據。​這可以保護用戶免受XSS攻擊和其他潛在威脅。​但是，默認情況下，在記錄期間不會清理數據。​這是為了確保准確地保留日誌數據（可以幫助任何未來的啟發式或法醫分析）。​但是，如果用戶嘗試使用外部工具讀取日誌數據，如果這些外部工具不執行自己的清理過程，用戶可能會受到XSS攻擊。​如有必要，可以使用此配置指令更改默認行為。 True = 記錄數據時清理數據（數據保存不太準確，但XSS風險較低）。 False = 記錄數據時不要清理數據（數據保存得更準確，但XSS風險更高）【標準】。

#### 『frontend』 （類別）
前端的配置。

##### 『frontend_log』 `[string]`
- 前端登錄嘗試的錄音文件。​指定一個文件名，​或留空以禁用。

##### 『signatures_update_event_log』 `[string]`
- 通過前端更新簽名時用於記錄的文件。​指定一個文件名，​或留空以禁用。

##### 『max_login_attempts』 `[int]`
- 最大前端登錄嘗試次數。​標準=5。

##### 『theme』 `[string]`
- 用於前端的默認主題。

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
└─…其他
```

##### 『magnification』 `[float]`
- 字體放大。​標準 = 1。

##### 『remotes』 `[string]`
- 更新系統用於獲取組件元數據的地址列表。​這可能需要在升級到新的主要版本時進行調整，或者在獲取新的更新源時進行調整，但在正常情況下應該不理會。

##### 『enable_two_factor』 `[bool]`
- 該指令確定是否將2FA用於前端帳戶。

#### 『signatures』 （類別）
簽名，簽名文件，模塊，等的配置。

##### 『block_attacks』 `[bool]`
- 阻止攻擊和其他異常流量相關的CIDR嗎？​例如，端口掃描、黑客攻擊、漏洞探測、等等。​除非您遇到問題當這樣做，​通常，​這應該被設置為『true』（真）。

##### 『block_cloud』 `[bool]`
- 阻止CIDR認定為屬於虛擬主機或云服務嗎？​如果您操作一個API服務從您的網站或如果您預計其他網站連接到您的網站，​這應該被設置為『false』（假）。​如果不，​這應該被設置為『true』（真）。

##### 『block_bogons』 `[bool]`
- 阻止bogon(『ㄅㄡㄍㄛㄋ』)/martian（​『火星』）CIDR嗎？​如果您希望連接到您的網站從您的本地網絡/本地主機/localhost/LAN/等等，​這應該被設置為『false』（假）。​如果不，​這應該被設置為『true』（真）。

##### 『block_generic』 `[bool]`
- 阻止CIDR一般建議對於黑名單嗎？​這包括簽名不標記為的一章节任何其他更具體簽名類別。

##### 『block_legal』 `[bool]`
- 阻止CIDR因為法律義務嗎？​這個指令通常不應該有任何作用，因為CIDRAM默認情況下不會將任何CIDR與『法律義務』相關聯，​但它作為一個額外的控制措施存在，以利於任何可能因法律原因而存在的自定義簽名文件或模塊。

##### 『block_malware』 `[bool]`
- 阻止與惡意軟件相關的CIDR嗎？​這包括C&C服務器，受感染的機器，涉及惡意軟件分發的機器，等等。

##### 『block_proxies』 `[bool]`
- 阻止CIDR認定為屬於代理服務或VPN嗎？​如果您需要該用戶可以訪問您的網站從代理服務和VPN，​這應該被設置為『false』（假）。​除此以外，​如果您不需要代理服務或VPN，​這應該被設置為『true』（真）作為一個方式以提高安全性。

##### 『block_spam』 `[bool]`
- 阻止高風險垃圾郵件CIDR嗎？​除非您遇到問題當這樣做，​通常，​這應該被設置為『true』（真）。

##### 『default_tracktime』 `[int]`
- 多少秒鐘來跟踪模塊禁止的IP。​標準 = 604800 （1週）。

##### 『infraction_limit』 `[int]`
- 從IP最大允許違規數量之前它被禁止。​標準=10。

##### 『tracking_override』 `[bool]`
- 允許模塊覆蓋跟踪選項嗎？​True（真）=允許【標準】；False（假）=不允許。

#### 『recaptcha』 （類別）
ReCaptcha的配置（為人們提供了一種在受阻時重新獲得訪問權限的方法）。

##### 『usemode』 `[int]`
- 何時應提供CAPTCHA嗎？​注意：列入白名單或已驗證且未阻止的請求永遠不需要完成CAPTCHA。​另請注意：CAPTCHA可以提供有用的保護層，防止機器人和各種惡意自動請求，但不會提供任何針對惡意人類的保護。

```
usemode
├─0 (決不 !!!)
├─1 (僅當被阻止時，在簽名限制之內，並且不被禁止。)
├─2 (僅當被阻止時，專門標明使用時，在簽名限制之內，並且不被禁止。)
├─3 (僅在簽名限制之內，並且不被禁止（不管是否被阻止）。)
├─4 (僅在不被阻止時。)
└─5 (僅在不被阻止時，或專門標明使用時，在簽名限制之內，並且不被禁止。)
```

##### 『lockip』 `[bool]`
- 應該CAPTCHA鎖定到IP？

##### 『lockuser』 `[bool]`
- 應該CAPTCHA鎖定到用戶？

##### 『sitekey』 `[string]`
- 可以在您的CAPTCHA服務的儀表板中找到該值。

也可以看看：
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### 『secret』 `[string]`
- 可以在您的CAPTCHA服務的儀表板中找到該值。

也可以看看：
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### 『expiry』 `[float]`
- 記得CAPTCHA多少小時？ 標準 = 720 （1個月）。

##### 『recaptcha_log』 `[string]`
- 記錄所有的CAPTCHA的嘗試？​要做到這一點，​指定一個文件名到使用。​如果不，​離開這個變量為空白。

##### 『signature_limit』 `[int]`
- 撤銷CAPTCHA之前允許的最大簽名數。標準 = 1。

##### 『api』 `[string]`
- 使用哪個API？

```
api
├─V2 ("V2 (選框)")
└─Invisible ("V2 (不可見的)")
```

##### 『show_cookie_warning』 `[bool]`
- 顯示cookie警告嗎？​True（真）=顯示【標準】；False（假）=不顯示。

##### 『show_api_message』 `[bool]`
- 顯示API訊息嗎？​True（真）=顯示【標準】；False（假）=不顯示。

##### 『nonblocked_status_code』 `[int]`
- 向未阻止的請求顯示CAPTCHA時應使用哪個狀態代碼？

```
nonblocked_status_code
├─200 (200 OK （好的）): 最不健壯，但最用戶友好。​自動請求很可能將此響應解釋為成功。
├─403 (403 Forbidden （禁止的）): 更健壯，但不太用戶友好。​一般最推薦的。
├─418 (418 I'm a teapot （我是一個茶壺）): 引用愚人節的笑話【{{Links.RFC2324}}】。​任何客戶端、機器人、瀏覽器、或其他方式都不太可能理解。​它是為了娛樂和方便而提供的，但是通常不推薦。
├─429 (429 Too Many Requests （請求過多）): 推薦用於速率限制、處理DDoS攻擊、和防洪。​不推薦在其他情況下。
└─451 (451 Unavailable For Legal Reasons （因法律原因不可用）): 主要出於法律原因被阻止時推薦。​不推薦在其他情況下。
```

#### 『hcaptcha』 （類別）
HCaptcha的配置（為人們提供了一種在受阻時重新獲得訪問權限的方法）。

##### 『usemode』 `[int]`
- 何時應提供CAPTCHA嗎？​注意：列入白名單或已驗證且未阻止的請求永遠不需要完成CAPTCHA。​另請注意：CAPTCHA可以提供有用的保護層，防止機器人和各種惡意自動請求，但不會提供任何針對惡意人類的保護。

```
usemode
├─0 (決不 !!!)
├─1 (僅當被阻止時，在簽名限制之內，並且不被禁止。)
├─2 (僅當被阻止時，專門標明使用時，在簽名限制之內，並且不被禁止。)
├─3 (僅在簽名限制之內，並且不被禁止（不管是否被阻止）。)
├─4 (僅在不被阻止時。)
└─5 (僅在不被阻止時，或專門標明使用時，在簽名限制之內，並且不被禁止。)
```

##### 『lockip』 `[bool]`
- 應該CAPTCHA鎖定到IP？

##### 『lockuser』 `[bool]`
- 應該CAPTCHA鎖定到用戶？

##### 『sitekey』 `[string]`
- 可以在您的CAPTCHA服務的儀表板中找到該值。

也可以看看：
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### 『secret』 `[string]`
- 可以在您的CAPTCHA服務的儀表板中找到該值。

也可以看看：
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### 『expiry』 `[float]`
- 記得CAPTCHA多少小時？ 標準 = 720 （1個月）。

##### 『hcaptcha_log』 `[string]`
- 記錄所有的CAPTCHA的嘗試？​要做到這一點，​指定一個文件名到使用。​如果不，​離開這個變量為空白。

##### 『signature_limit』 `[int]`
- 撤銷CAPTCHA之前允許的最大簽名數。標準 = 1。

##### 『api』 `[string]`
- 使用哪個API？

```
api
├─V1 ("V1")
└─Invisible ("V1 (不可見的)")
```

##### 『show_cookie_warning』 `[bool]`
- 顯示cookie警告嗎？​True（真）=顯示【標準】；False（假）=不顯示。

##### 『show_api_message』 `[bool]`
- 顯示API訊息嗎？​True（真）=顯示【標準】；False（假）=不顯示。

##### 『nonblocked_status_code』 `[int]`
- 向未阻止的請求顯示CAPTCHA時應使用哪個狀態代碼？

```
nonblocked_status_code
├─200 (200 OK （好的）): 最不健壯，但最用戶友好。​自動請求很可能將此響應解釋為成功。
├─403 (403 Forbidden （禁止的）): 更健壯，但不太用戶友好。​一般最推薦的。
├─418 (418 I'm a teapot （我是一個茶壺）): 引用愚人節的笑話【{{Links.RFC2324}}】。​任何客戶端、機器人、瀏覽器、或其他方式都不太可能理解。​它是為了娛樂和方便而提供的，但是通常不推薦。
├─429 (429 Too Many Requests （請求過多）): 推薦用於速率限制、處理DDoS攻擊、和防洪。​不推薦在其他情況下。
└─451 (451 Unavailable For Legal Reasons （因法律原因不可用）): 主要出於法律原因被阻止時推薦。​不推薦在其他情況下。
```

#### 『legal』 （類別）
法律要求的配置。

##### 『pseudonymise_ip_addresses』 `[bool]`
- 編寫日誌文件時使用假名的IP地址嗎？​True（真）=使用假名【標準】；False（假）=不使用假名。

##### 『privacy_policy』 `[string]`
- 要顯示在任何生成的頁面的頁腳中的相關隱私政策的地址。​指定一個URL，或留空以禁用。

#### 『template_data』 （類別）
模板和主題的配置。

##### 『theme』 `[string]`
- 用於CIDRAM的默認主題。

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
└─…其他
```

##### 『magnification』 `[float]`
- 字體放大。​標準 = 1。

##### 『css_url』 `[string]`
- 自定義主題的CSS文件URL。

##### 『block_event_title』 `[string]`
- 為阻止事件顯示的頁面標題。

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("拒絕訪問！")
└─…其他
```

##### 『captcha_title』 `[string]`
- 為CAPTCHA請求顯示的頁面標題。

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…其他
```

#### 『rate_limiting』 （類別）
速率限制的配置（不建議一般使用）。

##### 『max_bandwidth』 `[string]`
- 在為將來的請求啟用速率限制之前的最大允許帶寬量。​值為0將禁用此類速率限制。​標準=0KB。

##### 『max_requests』 `[int]`
- 在為將來的請求啟用速率限制之前允許的最大請求數。​值為0將禁用此類速率限制。​標準=0。

##### 『precision_ipv4』 `[int]`
- 監視IPv4使用時的精度。​值鏡像CIDR塊大小。​設置為32以獲得最佳精度。​標準=32。

##### 『precision_ipv6』 `[int]`
- 監視IPv6使用時的精度。​值鏡像CIDR塊大小。​設置為128以獲得最佳精度。​標準=128。

##### 『allowance_period』 `[float]`
- 監視使用情況的小時數。​標準=0。

##### 『exceptions』 `[string]`
- 例外（即，不應限制速率的請求）。​僅在啟用速率限制時有效。

```
exceptions
├─Whitelisted ("在白名單中的請求")
└─Verified ("經過驗證的搜索引擎和社交媒體請求")
```

#### 『supplementary_cache_options』 （類別）
補充緩存選項。​注意：更改這些值可能會使您註銷。

##### 『prefix』 `[string]`
- 該值將附加到所有緩存條目的鍵的開頭。​默認 = 『CIDRAM_』。​當同一服務器上存在多個安裝時，這對於將它們的緩存彼此分開非常有用。

##### 『enable_apcu』 `[bool]`
- 指定是否嘗試使用APCu進行緩存。​默認 = True。

##### 『enable_memcached』 `[bool]`
- 指定是否嘗試使用Memcached進行緩存。​默認 = False。

##### 『enable_redis』 `[bool]`
- 指定是否嘗試使用Redis進行緩存。​默認 = False。

##### 『enable_pdo』 `[bool]`
- 指定是否嘗試使用PDO進行緩存。​默認 = False。

##### 『memcached_host』 `[string]`
- Memcached主機值。​默認 = 『localhost』。

##### 『memcached_port』 `[int]`
- Memcached端口值。​默認 = 『11211』。

##### 『redis_host』 `[string]`
- Redis主機值。​默認 = 『localhost』。

##### 『redis_port』 `[int]`
- Redis端口值。​默認 = 『6379』。

##### 『redis_timeout』 `[float]`
- Redis超時值。​默認 = 『2.5』。

##### 『pdo_dsn』 `[string]`
- PDO DSN值。​默認 = 『mysql:dbname=cidram;host=localhost;port=3306』。

__常問問題。__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.zh-tw.md#HOW_TO_USE_PDO" hreflang="zh-TW">『PDO DSN』是什麼？如何能PDO與CIDRAM一起使用？</a></em>

##### 『pdo_username』 `[string]`
- PDO用戶名。

##### 『pdo_password』 `[string]`
- PDO密碼。

#### 『abuseipdb』 （類別）
AbuseIPDB模塊的配置。

##### 『api_key』 `[string]`
- 請在此處輸入您的API密鑰。

也可以看看：
- [Register - AbuseIPDB](https://www.abuseipdb.com/register)
- [link_get_api_key](https://www.abuseipdb.com/account/api)

##### 『max_age_in_days』 `[int]`
- 執行查找時將考慮報告的最長天數（必須是1到365之間的數字）。標準=365。

##### 『minimum_confidence_score』 `[int]`
- 為了讓CIDRAM阻止IP地址所需的最低置信度分數（必須是0到100之間的數字）。標準=50。

##### 『max_cs_for_captcha』 `[int]`
- 為了提供CAPTCHA的目的最大置信度分數（必須是0到100之間的數字）。標準=10。

##### 『minimum_total_reports』 `[int]`
- 為了讓CIDRAM阻止IP地址所需的最小總報告數。標準=1。

##### 『report_back』 `[bool]`
- 允許CIDRAM使用您的API密鑰將檢測到的不良行為報告回AbuseIPDB馬？標準=False。

##### 『lookup_strategy』 `[int]`
- 應該為哪些請求執行查找？

```
lookup_strategy
├─0 (不要執行。): 使用如果您只想將該模塊用於報告目的，而不是檢查結果。
├─1 (所有請求。): 更嚴格和徹底，但也可能更快地達到配額，可能導致被鎖定在服務之外。​此外，儘管結果被緩存，但在某些情況下仍可能對網站性能產生負面影響。​在某些情況下可能是必要的，但通常不推薦。
└─2 (僅對敏感頁面的請求（例如，登錄頁面，註冊表單，等等）。): 不那麼嚴格和徹底，但在配額和限制方面更加保守，並且不太可能對性能產生負面影響。​大多數情況下推薦的策略。
```

##### 『build_profiles_from_usage_type』 `[bool]`
- 使用API返回的使用類型構建分類？ False = 不要使用。 True = 使用。 標準 = True。

#### 『bgpview』 （類別）
BGPView模塊的配置（為CIDRAM提供ASN和國家代碼查找工具）。

##### 『blocked_asns』 `[string]`
- 被BGPView模塊匹配時要阻止的ASN列表。

##### 『whitelisted_asns』 `[string]`
- 由BGPView模塊匹配時要列入白名單的ASN列表。

##### 『blocked_ccs』 `[string]`
- 由BGPView模塊匹配時要阻止的國家列表（由其{{Links.ISO.3166}}兩個字母的國家代碼標識）。

##### 『whitelisted_ccs』 `[string]`
- 由BGPView模塊匹配時要列入白名單的國家列表（由其{{Links.ISO.3166}}兩個字母的國家代碼標識）。

#### 『bunnycdn』 （類別）
BunnyCDN兼容性模塊配置。

##### 『positive_action』 `[string]`
- CIDRAM遇到BunnyCDN的請求時應該執行什麼動作？ 默認操作 = 繞行。

```
positive_action
├─bypass ("觸發旁路。): 只要至少已經觸發了一個簽名，就從觸發的簽名數中減去一個計數。推薦用於處理可能由默認簽名文件引起的簡單假陽性。"
├─greylist ("將請求列入灰名單。): 重置觸發的簽名數量，但繼續處理請求。​當您不想將請求列入白名單，但需要比觸發的繞過更實質的時推薦使用。"
└─whitelist ("將請求列入白名單。): 重置觸發的簽名數量，併中止對請求的任何進一步處理。​保證CIDRAM永遠不會阻止請求。"
```

#### 『bypasses』 （類別）
默認簽名繞過配置。

##### 『used』 `[string]`
- 應該使用哪些繞過？

```
used
├─AbuseIPDB ("AbuseIPDB")
├─AmazonAdBot ("AmazonAdBot")
├─Bingbot ("Bingbot")
├─DuckDuckBot ("DuckDuckBot")
├─Embedly ("Embedly")
├─Feedbot ("Feedbot")
├─Feedspot ("Feedspot")
├─GoogleFiber ("Google Fiber")
├─Googlebot ("Googlebot")
├─Grapeshot ("Grapeshot")
├─Jetpack ("Jetpack")
├─PetalBot ("PetalBot")
├─Pinterest ("Pinterest")
└─Redditbot ("Redditbot")
```

#### 『extras』 （類別）
可選的安全附加模塊配置。

##### 『signatures』 `[string]`
- 應該尊重哪些類型的簽名？

```
signatures
├─empty_ua ("空的用戶代理。")
├─query ("基於請求查詢的簽名。")
├─raw ("基於原始請求輸入的簽名。")
├─ruri ("基於重構URI的簽名。")
└─uri ("基於請求URI的簽名。")
```

#### 『projecthoneypot』 （類別）
Project Honeypot模塊的配置。

##### 『api_key』 `[string]`
- 請在此處輸入您的API密鑰。

也可以看看：
- [Project Honeypot Terms of Service.](https://www.projecthoneypot.org/terms_of_service_use.php)
- [link_get_api_key](https://www.projecthoneypot.org/httpbl_configure.php)

##### 『max_age_in_days』 `[int]`
- 執行查找時將考慮報告的最長天數。標準=365。

##### 『minimum_threat_score』 `[int]`
- 為了讓CIDRAM阻止IP地址所需的最低威脅分數（必須是1到100之間的數字）。標準=10。

##### 『max_ts_for_captcha』 `[int]`
- 為了提供CAPTCHA的目的最大威脅分數（必須是1到100之間的數字）。標準=10。

##### 『lookup_strategy』 `[int]`
- 應該為哪些請求執行查找？

```
lookup_strategy
├─0 (不要執行。): 使用如果您只想將該模塊用於報告目的，而不是檢查結果。
├─1 (所有請求。): 更嚴格和徹底，但也可能更快地達到配額，可能導致被鎖定在服務之外。​此外，儘管結果被緩存，但在某些情況下仍可能對網站性能產生負面影響。​在某些情況下可能是必要的，但通常不推薦。
└─2 (僅對敏感頁面的請求（例如，登錄頁面，註冊表單，等等）。): 不那麼嚴格和徹底，但在配額和限制方面更加保守，並且不太可能對性能產生負面影響。​大多數情況下推薦的策略。
```

#### 『sfs』 （類別）
Stop Forum Spam模塊的配置。

##### 『offer_captcha』 `[bool]`
- 當此模塊阻止請求時，可能會提供驗證碼。​標準 = True。​注意：它不會覆蓋其他指令。​要提供驗證碼，所有指令必須一致，必要的密鑰必須配置，等等。​在通常允許提供驗證碼的情況下，將此指令設置為『false』可以防止為該模塊專門阻止的請求提供驗證碼。

---


### 6. <a name="SECTION6"></a>簽名格式

*也可以看看：*
- *[什麼是『簽名』？](#WHAT_IS_A_SIGNATURE)*

#### 6.0 基本概念（對於簽名文件）

所有IPv4簽名遵循格式：`xxx.xxx.xxx.xxx/yy [Function] [Param]`。
- `xxx.xxx.xxx.xxx` 代表CIDR塊開始（初始IP地址八比特組）。
- `yy` 代表CIDR塊大小 [1-32]。
- `[Function]` 指令腳本做什麼用的署名（應該怎麼簽名考慮）。
- `[Param]` 代表任何其他信息其可以由需要 `[Function]`。

所有IPv6簽名遵循格式：`xxxx:xxxx:xxxx:xxxx::xxxx/yy [Function] [Param]`。
- `xxxx:xxxx:xxxx:xxxx::xxxx` 代表CIDR塊的開始（初始IP地址八比特組）。​完整符號和縮寫符號是可以接受的（和每都必須遵循相應和相關IPv6符號標準，​但有一個例外：IPv6地址不能開頭是與縮寫當用來在簽名該腳本，​由於以何種方式CIDR是構建由腳本；例如，​當用來在簽名，​`::1/128`應該這樣寫`0::1/128`，​和`::0/128`應該這樣寫`0::/128`)。
- `yy` 代表CIDR塊大小 [1-128]。
- `[Function]` 指令腳本做什麼用的署名（應該怎麼簽名考慮）。
- `[Param]` 代表任何其他信息其可以由需要 `[Function]`。

CIDRAM簽名文件應該使用Unix的換行符（`%0A`，​或`\n`）！​其他換行符類型/風格（例如，​Windows `%0D%0A`或`\r\n`換行符，​Mac `%0D`或`\r`換行符，​等等） 可以被用於，​但不是優選。​非Unix的換行符將正常化至Unix的換行符由腳本。

精準無誤的CIDR符號是必須的，​不會是承認簽名。​另外，​所有的CIDR簽名必須用一個IP地址該始於一個數在該CIDR塊分割適合於它的塊大小（例如，​如果您想阻止所有的IP從`10.128.0.0`到`11.127.255.255`，​`10.128.0.0/8`不會是承認由腳本，​但`10.128.0.0/9`和`11.0.0.0/9`結合使用，​將是承認由腳本）。

任何數據在簽名文件不承認為一個簽名也不為簽名相關的語法由腳本將被忽略，​因此，​這意味著您可以放心地把任何未簽名數據和任何您想要的在簽名文件沒有打破他們和沒有打破該腳本。​註釋是可以接受的在簽名文件，​和沒有特殊的格式需要為他們。​Shell風格的哈希註釋是首選，​但並非強制；從功能的角度，​無論您是否選擇使用Shell風格的哈希註釋，​有沒有區別為腳本，​但使用Shell風格的哈希幫助IDE和純文本編輯器正確地突出的各個章节簽名文件（所以，​Shell風格的哈希可以幫助作為視覺輔助在編輯）。

`[Function]` 可能的值如下：
- Run
- Whitelist
- Greylist
- Deny

如果『Run』是用來，​當該簽名被觸發，​該腳本將嘗試執行（使用一個`require_once`聲明）一個外部PHP腳本，​由指定的`[Param]`值（工作目錄應該是『/vault/』腳本目錄）。

例子：`127.0.0.0/8 Run example.php`

這可能是有用如果您想執行一些特定的PHP代碼對一些特定的IP和/或CIDR。

如果『Whitelist』是用來，​當該簽名被觸發，​該腳本將重置所有檢測（如果有過任何檢測）和打破該測試功能。​`[Param]`被忽略。​此功能將白名單一個IP地址或一個CIDR。

例子：`127.0.0.1/32 Whitelist`

如果『Greylist』是用來，​當該簽名被觸發，​該腳本將重置所有檢測（如果有過任何檢測）和跳到下一個簽名文件以繼續處理。​`[Param]`被忽略。

例子：`127.0.0.1/32 Greylist`

如果『Deny』是用來，​當該簽名被觸發，​假設沒有白名單簽名已觸發為IP地址和/或CIDR，​訪問至保護的頁面被拒絕。​您要使用『Deny』為實際拒絕一個IP地址和/或CIDR範圍。​當任何簽名利用的『Deny』被觸發，​該『拒絕訪問』腳本頁面將生成和請求到保護的頁面會被殺死。

『Deny』的`[Param]`值會被解析為『拒絕訪問』頁面，​提供給客戶機/用戶作為引原因他們訪問到請求的頁面被拒絕。​它可以是一個短期和簡單的句子，​為解釋原因（什麼應該足夠了；一個簡單的消息像『我不想讓您在我的網站』會好起來的），​或一小撮之一的短關鍵字供應的通過腳本。​如果使用，​它們將被替換由腳本使用預先準備的解釋為什麼客戶機/用戶已被阻止。

預先準備的解釋具有多語言支持和可以翻譯通過腳本根據您的語言指定的通過`lang`腳本配置指令。​另外，​您可以指令腳本忽略『Deny』簽名根據他們的價`[Param]`值（如果他們使用這些短關鍵字）通過腳本配置指令（每短關鍵字有一個相應的指令到處理相應的簽名或忽略它）。​`[Param]`值不使用這些短關鍵字，​然而，​沒有多語言支持和因此不會被翻譯通過腳本，​並且還，​不能直接控制由腳本配置。

可用的短關鍵字是：
- Attacks
- Bogon
- Cloud
- Generic
- Legal
- Malware
- Proxy
- Spam

#### 6.1 標籤

##### 6.1.0 章節標籤

如果要分割您的自定義簽名成各個章節，​您可以識別這些各個章節為腳本通過加入一個章節標籤立即跟著每簽名章節，​伴隨著簽名章節名字（看下面的例子）。

```
# 章節一。
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: 章節一
```

為了打破章節標籤和以確保標籤不是確定不正確的對於簽名章節從較早的在簽名文件，​確保有至少有兩個連續的換行符之間您的標籤和您的較早的簽名章節。​任何未標記簽名將默認為『IPv4』或『IPv6』（取決於簽名類型被觸發）。

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: 章節一
```

在上面的例子`1.2.3.4/32`和`2.3.4.5/32`將標為『IPv4』，​而`4.5.6.7/32`和`5.6.7.8/32`將標為『章節一』.

同樣邏輯也可以應用於分離其他標籤類型。

特別是，當假陽性發生時，章節標籤對調試非常有用，通過提供一個簡單的方法來找到問題的確切來源，並當通過前端日誌頁面查看日誌文件時，可以非常有用地過濾日誌文件條目​（章節名稱可通過前端日誌頁面進行點擊，並可用作過濾標準）。​如果在一些簽名章節中章節標籤是省略，當這些簽名被觸發時，CIDRAM使用簽名文件的名稱以及阻止的IP地址類型（IPv4或IPv6）作為後備，因此，章節標籤是完全可選的。​但是，在某些情況下，可能會推薦使用它們，例如簽名文件模糊地命名，或當難以清楚地識別阻止請求的簽名的來源時。

##### 6.1.1 過期標籤

如果您想簽名一段時間後過期，​以類似的方式來章節標籤，​您可以使用一個『過期標籤』來指定在簽名應該不再有效。​過期標籤使用格式『年年年年.月月.日日』（看下面的例子）。

```
# 章節一。
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

過期的簽名永遠不會被任何請求觸發。

##### 6.1.2 起源標籤

如果您想要指定某個特定簽名的原產國，可以使用『原產標籤』來實現。​原產標籤接受與其適用的簽名相對應的國家的『[ISO 3166-1 二位字母](https://zh.wikipedia.org/wiki/ISO_3166-1)』代碼。​這些代碼必須寫成大寫（小寫或混合大小寫不能正確顯示）。​當使用原產標籤時，會將其添加到『為什麼被阻止』日誌字段條目中，為任何請求被阻止因為簽名的標籤應用。

如果安裝了可選的『flags CSS』組件，當通過前端日誌頁面查看日誌文件時，由原產標籤附加的信息被其相應的國旗取代。​無論是原始形式還是國旗，這些信息是可點擊的，並當點擊時，它將通過類似識別的日誌條目來過濾日誌條目（從而有效地啟用日誌頁面按來源國過濾）。

注意：從技術上講，這不是任何形式的地理定位，因為它不涉及從IP查找特定的位置信息，反而，它允許我們當請求被特定的簽名阻止時明確指出一個原產國。​同一個簽名章節允許有多個原產標籤。

假設的例子：

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

任何標籤都可以聯合使用，所有標籤都是可選（看下面的例子）。

```
# 示例章節。
1.2.3.4/32 Deny Generic
Origin: US
Tag: 示例章節
Expires: 2016.12.31
```

##### 6.1.3 延緩標籤

當大量安裝並主動使用的簽名文件時，安裝可能會變得非常複雜，並且可能存在一些重疊的簽名。​在這些情況下，為了防止在阻止事件期間觸發多個重疊的簽名，在大量安裝並主動使用的某些其他特定簽名文件的情況下，延緩標籤可用於延緩特定簽名章節。​在某些簽名比其他簽名更頻繁更新的情況下，這可能很有用，為了延緩較不頻繁更新的簽名，於贊成更頻繁更新的簽名。

延緩標籤與其他類型的標籤類似地使用。​標籤的值應該是要贊成的簽名文件的名稱。

例子：

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 6.1.4 分類標籤

分類標籤提供了一種在IP測試頁面上顯示其他信息的方式，並且模塊和輔助規則可以利用分類標籤來實現更複雜的行為和經過微調的決策。

分類標籤的使用類似於其他類型的標籤。​分類標籤的值可用作模塊和輔助規則的條件。​分類標籤可以通過用分號分隔這些值來提供多個值。​最終用戶永遠不會看到分類標籤的值。

例子：

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 6.2 YAML

##### 6.2.0 YAML基本概念

簡化形式的YAML標記可以使用在簽名文件用於目的定義行為和配置設置具體到個人簽名章節。​這可能是有用的如果您希望您的配置指令值到變化之間的個人簽名和簽名章節（例如；如果您想提供一個電子郵件地址為支持票為任何用戶攔截的通過一個特定的簽名，​但不希望提供一個電子郵件地址為支持票為用戶攔截的通過任何其他簽名；如果您想一些具體的簽名到觸發頁面重定向；如果您想標記一個簽名為使用的reCAPTCHA/hCAPTCHA；如果您想日誌攔截的訪問到單獨的文件按照個人簽名和/或簽名章節）。

使用YAML標記在簽名文件是完全可選（即，​如果您想用這個，​您可以用這個，​但您沒有需要用這個），​和能夠利用最的（但不所有的）配置指令。

注意：YAML標記實施在CIDRAM是很簡單也很有限；它的目的是滿足特定要求的CIDRAM在方式具有熟悉的YAML標記，​但不跟隨也不符合規定的官方規格（因此，​將不會是相同的其他實現別處，​和可能不適合其他項目別處）。

在CIDRAM，​YAML標記段被識別到腳本通過使用三個連字符（『---』），​和終止靠他們的簽名章節通過雙換行符。​一個典型的YAML標記段在一個簽名章節被組成的三個連字符在一行立馬之後的CIDR列表和任何標籤，​接著是二維表為鍵值對（第一維，​配置指令類別；第二維，​配置指令）為哪些配置指令應修改（和哪些值）每當一個簽名內那簽名章節被觸發（看下面的例子）。

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

##### 6.2.1 如何『特別標記』簽名章節為使用的reCAPTCHA或hCAPTCHA

當『usemode』是『2』或『5』，​為『特別標記』簽名章節為使用的reCAPTCHA或hCAPTCHA，​一個條目是包括在YAML段為了那個簽名章節（看下面的例子）。

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

#### 6.3 輔

##### 6.3.0 忽略簽名章節

此外，​如果您想CIDRAM完全忽略一些具體的章節內的任何簽名文件，​您可以使用`ignore.dat`文件為指定忽略哪些章節。​在新行，​寫`Ignore`，​空間，​然後該名稱的章節您希望CIDRAM忽略（看下面的例子）。

```
Ignore 章節一
```

這也可以通過使用CIDRAM前端的『章節列表』頁面提供的接口來實現。

##### 6.3.1 輔助規則

如果您覺得編寫自己的自定義簽名文件或自定義模塊對您來說太複雜了，更簡單的替代方案可能是使用CIDRAM前端的『輔助規則』頁面提供的接口。​通過選擇適當的選項並指定有關特定類型的請求的詳細信息，您可以指示CIDRAM如何響應這些請求。​在所有簽名文件和模塊已經完成執行之後執行『輔助規則』。

#### 6.4 <a name="MODULE_BASICS"></a>基本概念（對於模塊）

模塊可用於擴展CIDRAM的功能，執行額外的任務，或處理額外的邏輯。​通常，當除了起源IP地址之外的原因需要阻止請求時它們使用​（因此，當CIDR簽名不足以阻止請求）。​模塊被寫為PHP文件，因此，通常，模塊簽名被寫為PHP代碼。

由於模塊是作為PHP文件編寫的，如果您對CIDRAM代碼庫有足夠的了解，則可以根據需要構建模塊，並根據需要編寫模塊簽名​（在合理範圍的什麼可以用PHP來完成內）。​但是，為了您自己的方便，並為了介於存在的模塊和您自己的之間好的理解，建議分析上面鏈接的模板，以便能夠使用它提供的結構和格式。

*注意：如果您不舒服使用PHP代碼，則不建議編寫自己的模塊。*

CIDRAM提供了一些用於模塊的功能，這將使編寫自己的模塊變得更簡單和容易。​有關此功能的信息如下所述。

#### 6.5 模塊功能

##### 6.5.0 『$this->trigger』

模塊簽名通常使用`$this->trigger`編寫。​在大多數情況下，為了編寫模塊，這個閉包比其他任何東西都重要。

`$this->trigger`接受4個參數：`$Condition`、`$ReasonShort`、`$ReasonLong`（可選的）、和`$DefineOptions`（可選的）。

`$Condition`感實性被評估，和如果是true（真），簽名是『觸發』。​如果是false（假），簽名不是『觸發』。​`$Condition`通常包含PHP代碼來評估應該導致請求被阻止的條件。

當簽名被『觸發』時，`$ReasonShort`在『為什麼被阻止』字段中被引用。

`$ReasonLong`是一個可選消息，當用戶/客戶端被阻止時顯示給用戶/客戶端，解釋為什麼他們被阻止。​省略時默認為標準的『拒絕訪問』消息。

`$DefineOptions`是一個包含鍵/值對的可選數組，用於定義特定於請求實例的配置選項。​配置選項將在簽名被『觸發』時應用。

`$this->trigger`當簽名是『觸發』時將返回true（真），當簽名不是『觸發』時將返回false（假）。

##### 6.5.1 『$this->bypass』

簽名旁路通常使用`$this->bypass`編寫。

`$this->bypass`接受3個參數：`$Condition`、`$ReasonShort`、和`$DefineOptions`（可選的）。

`$Condition`感實性被評估，和如果是true（真），旁路是『觸發』。​如果是false（假），旁路不是『觸發』。​`$Condition`通常包含PHP代碼來評估應不該導致請求被阻止的條件。

當旁路被『觸發』時，`$ReasonShort`在『為什麼被阻止』字段中被引用。

`$DefineOptions`是一個包含鍵/值對的可選數組，用於定義特定於請求實例的配置選項。​配置選項將在旁路被『觸發』時應用。

`$this->bypass`當旁路是『觸發』時將返回true（真），當旁路不是『觸發』時將返回false（假）。

##### 6.5.2 『$this->dnsReverse』

這可以用來獲取IP地址的主機名。​如果您想創建一個模塊來阻止主機名，這個閉包可能是有用的。

例子：
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

#### 6.6 模塊變量

模塊在其自己的範圍內執行，並且由模塊定義的任何變量將不能被其他模塊訪問，也不由父腳本，除非它們存儲在`$CIDRAM`數組中（模塊執行完成後，其他所有內容都將被擦洗）。

下面列出了一些可能對您的模塊有用的常見變量：

變量 | 說明
----|----
`$this->BlockInfo['DateTime']` | 當前日期和時間。
`$this->BlockInfo['IPAddr']` | 當前請求的IP地址。
`$this->BlockInfo['ScriptIdent']` | CIDRAM腳本版本。
`$this->BlockInfo['Query']` | 當前請求的查詢。
`$this->BlockInfo['Referrer']` | 當前請求的引用者（如果存在）。
`$this->BlockInfo['UA']` | 當前請求的用戶代理【user agent】。
`$this->BlockInfo['UALC']` | 當前請求的用戶代理【user agent】（小寫）。
`$this->BlockInfo['ReasonMessage']` | 當前請求被阻止時顯示給用戶/客戶端的消息。
`$this->BlockInfo['SignatureCount']` | 當前請求的觸發的簽名數量。
`$this->BlockInfo['Signatures']` | 針對當前請求觸發的任何簽名的參考信息。
`$this->BlockInfo['WhyReason']` | 針對當前請求觸發的任何簽名的參考信息。

---


### 7. <a name="SECTION7"></a>已知的兼容問題

下列軟件包和產品被發現與CIDRAM不兼容：
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

已提供模塊以確保以下軟件包和產品與CIDRAM兼容：
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__

*也可以看看：​[兼容性圖表](https://maikuolan.github.io/Compatibility-Charts/)。*

---


### 8. <a name="SECTION8"></a>常見問題（FAQ）

- [什麼是『簽名』？](#WHAT_IS_A_SIGNATURE)
- [什麼是『CIDR』？](#WHAT_IS_A_CIDR)
- [什麼是『假陽性』？](#WHAT_IS_A_FALSE_POSITIVE)
- [CIDRAM可以阻止整個國家嗎？](#BLOCK_ENTIRE_COUNTRIES)
- [什麼是簽名更新頻率？](#SIGNATURE_UPDATE_FREQUENCY)
- [我在使用CIDRAM時遇到問題和我不知道該怎麼辦！​請幫忙！](#ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [因為CIDRAM，​我被阻止從我想訪問的網站！​請幫忙！](#BLOCKED_WHAT_TO_DO)
- [我想使用CIDRAM（在v2期间）與早於7.2的PHP版本；​您能幫我嗎？](#MINIMUM_PHP_VERSION_V3)
- [我可以使用單個CIDRAM安裝來保護多個域嗎？](#PROTECT_MULTIPLE_DOMAINS)
- [我不想浪費時間安裝這個和確保它在我的網站上功能正常；我可以僱用您這樣做嗎？](#PAY_YOU_TO_DO_IT)
- [我可以聘請您或這個項目的任何開發者私人工作嗎？](#HIRE_FOR_PRIVATE_WORK)
- [我需要專家修改，​的定制，​等等；您能幫我嗎？](#SPECIALIST_MODIFICATIONS)
- [我是開發人員，​網站設計師，​或程序員。​我可以接受還是提供與這個項目有關的工作？](#ACCEPT_OR_OFFER_WORK)
- [我想為這個項目做出貢獻；我可以這樣做嗎？](#WANT_TO_CONTRIBUTE)
- [可以使用cron自動更新嗎？](#CRON_TO_UPDATE_AUTOMATICALLY)
- [什麼是『違規』？](#WHAT_ARE_INFRACTIONS)
- [CIDRAM可以阻止主機名？](#BLOCK_HOSTNAMES)
- [在『default_dns』中我可以使用什麼？](#WHAT_CAN_I_USE_FOR_DEFAULT_DNS)
- [我可以使用CIDRAM保護網站以外的東西嗎（例如，電子郵件服務器，FTP，SSH，IRC，等）？](#PROTECT_OTHER_THINGS)
- [如果我在使用CDN或緩存服務的同時使用CIDRAM，會發生問題嗎？](#CDN_CACHING_PROBLEMS)
- [CIDRAM會保護我的網站免受DDoS攻擊嗎？](#DDOS_ATTACKS)
- [當我通過更新頁面啟用或禁用模塊或簽名文件時，它會在配置中它們將按字母數字排序。​我可以改變他們排序的方式嗎？](#CHANGE_COMPONENT_SORT_ORDER)
- [『PDO DSN』是什麼？如何能PDO與CIDRAM一起使用？](#HOW_TO_USE_PDO)
- [CIDRAM正在阻止cronjobs。​如何解決這個問題？](#BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>什麼是『簽名』？

在CIDRAM的上下文中，​『簽名』是一些數據，​它表示/識別我們正在尋找的東西，​通常是IP地址或CIDR，​並包含一些說明，​告訴CIDRAM最好的回應方法當它遇到我們正在尋找的。​CIDRAM的典型簽名如下所示：

對於『簽名文件』：

`1.2.3.4/32 Deny Generic`

對於『模塊』：

```PHP
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*注意：『簽名文件』的簽名，和『模塊』的簽名，不是一回事。*

經常（但不總是），​簽名是捆綁在一起，​形成『簽名章節』，​經常伴隨評論，​標記，​和/或相關元數據。​這可以用於為簽名提供附加上下文和/或附加說明。

#### <a name="WHAT_IS_A_CIDR"></a>什麼是『CIDR』？

『CIDR』 是 『Classless Inter-Domain Routing』 的首字母縮寫 （『無類別域間路由』） *【[1](https://zh.wikipedia.org/wiki/%E6%97%A0%E7%B1%BB%E5%88%AB%E5%9F%9F%E9%97%B4%E8%B7%AF%E7%94%B1), [2](https://whatismyipaddress.com/cidr)】*。​這個首字母縮寫用於這個包的名稱，​『CIDRAM』，​是 『Classless Inter-Domain Routing Access Manager』 的首字母縮寫 （『無類別域間路由訪問管理器』）。

然而，​在CIDRAM的上下文中（如，​在本文檔中，​在CIDRAM的討論中，​或在CIDRAM語言數據中），​當『CIDR』（單數）或『CIDRs』（複數）被提及時（因此當我們用這些詞作為名詞在自己的權利，​而不作為首字母縮寫），​我們的意圖是一個子網，​用CIDR表示法表示。​使用CIDR/CIDRs而不是子網的原因是澄清它是用CIDR表示法表示的子網是我們的意思 （因為子網可以用幾種不同的方式表達）。​因此，​CIDRAM可以被認為是『子網訪問管理器』。

這個雙重含義可能看起來很歧義，​但這個解釋並提供上下文應該有助於解決這個歧義。

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>什麼是『假陽性』？

術語『假陽性』（*或者：『假陽性錯誤』；『虛驚』*；英語：*false positive*； *false positive error*； *false alarm*），​很簡單地描述，​和在一個廣義上下文，​被用來當測試一個因子，​作為參考的測試結果，​當結果是陽性（即：因子被確定為『陽性』，​或『真』），​但預計將為（或者應該是）陰性（即：因子，​在現實中，​是『陰性』，​或『假』）。​一個『假陽性』可被認為是同樣的『哭狼』 (其中，​因子被測試是是否有狼靠近牛群，​因子是『假』由於該有沒有狼靠近牛群，​和因子是報告為『陽性』由牧羊人通過叫喊『狼，​狼』），​或類似在醫學檢測情況，​當患者被診斷有一些疾病，​當在現實中，​他們沒有疾病。

一些相關術語是『真陽性』，​『真陰性』和『假陰性』。​一個『真陽性』指的是當測試結果和真實因子狀態都是『真』（或『陽性』），​和一個『真陰性』指的是當測試結果和真實因子狀態都是『假』（或『陰性』）；一個『真陽性』或『真陰性』被認為是一個『正確的推理』。​對立面『假陽性』是一個『假陰性』；一個『假陰性』指的是當測試結果是『陰性』（即：因子被確定為『陰性』，​或『假』），​但預計將為（或者應該是）陽性（即：因子，​在現實中，​是『陽性』，​或『真』）。

在CIDRAM的上下文，​這些術語指的是CIDRAM的簽名和什麼/誰他們阻止。​當CIDRAM阻止一個IP地址由於惡劣的，​過時的，​或不正確的簽名，​但不應該這樣做，​或當它這樣做為錯誤的原因，​我們將此事件作為一個『假陽性』。​當CIDRAM未能阻止IP地址該應該已被阻止，​由於不可預見的威脅，​缺少簽名或不足簽名，​我們將此事件作為一個『檢測錯過』（同樣的『假陰性』）。

這可以通過下表來概括：

&nbsp; | CIDRAM不應該阻止IP地址 | CIDRAM應該阻止IP地址
---|---|---
CIDRAM不會阻止IP地址 | 真陰性（正確的推理） | 檢測錯過（同樣的『假陰性』）
CIDRAM會阻止IP地址 | __假陽性__ | 真陽性（正確的推理）

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>CIDRAM可以阻止整個國家嗎？

它可以。​最簡單的方法是安裝BGPView模塊並根據需要進行配置。

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>什麼是簽名更新頻率？

更新頻率根據相關的簽名文件而有所不同。​所有的CIDRAM簽名文件的維護者通常盡量保持他們的簽名為最新，​但是因為我們所有人都有各種其他承諾，​和因為我們的生活超越了項目，​和因為我們不得到經濟補償/付款為我們的項目的努力，​無法保證精確的更新時間表。​通常，​簽名被更新每當有足夠的時間，​和維護者嘗試根據必要性和根據范圍之間的變化頻率確定優先級。​幫助總是感謝，​如果您願意提供任何。

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>我在使用CIDRAM時遇到問題和我不知道該怎麼辦！​請幫忙！

- 您使用軟件的最新版本嗎？​您使用簽名文件的最新版本嗎？​如果這兩個問題的答案是不，​嘗試首先更新一切，​然後檢查問題是否仍然存在。​如果它仍然存在，​繼續閱讀。
- 您檢查過所有的文檔嗎？​如果沒有做，​請這樣做。​如果文檔不能解決問題，​繼續閱讀。
- 您檢查過[issues頁面](https://github.com/CIDRAM/CIDRAM/issues)嗎？​檢查是否已經提到了問題。​如果已經提到了，​請檢查是否提供了任何建議，​想法或解決方案。​按照需要嘗試解決問題。
- 如果問題仍然存在，請通過在issues頁面上創建新issue尋求幫助。

#### <a name="BLOCKED_WHAT_TO_DO"></a>因為CIDRAM，​我被阻止從我想訪問的網站！​請幫忙！

CIDRAM使網站所有者能夠阻止不良流量，​但網站所有者有責任為自己決定如何使用CIDRAM。​在關於默認簽名文件假陽性的情況下，​可以進行校正。​但關於從特定網站解除阻止，​您需要與相關網站的所有者進行溝通。​當進行校正時，​至少，​他們需要更新他們的簽名文件和/或安裝。​在其他情況下（例如，​當他們修改了他們的安裝，​當他們創建自己的自定義簽名，​等等），​解決您的問題的責任完全是他們的，​並完全不在我們的控制之內。

#### <a name="MINIMUM_PHP_VERSION_V3"></a>我想使用CIDRAM（在v2期间）與早於7.2的PHP版本；​您能幫我嗎？

不能。PHP≥7.2是CIDRAM v3的最低要求。

*也可以看看：​[兼容性圖表](https://maikuolan.github.io/Compatibility-Charts/)。*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>我可以使用單個CIDRAM安裝來保護多個域嗎？

可以。​CIDRAM安裝未綁定到特定域，​因此可以用來保護多個域。​通常，​當CIDRAM安裝保護只一個域，​我們稱之為『單域安裝』，​和當CIDRAM安裝保護多個域和/或子域，​我們稱之為『多域安裝』。​如果您進行多域安裝並需要使用不同的簽名文件為不同的域，​或需要不同配置CIDRAM為不同的域，​這可以做到。​加載配置文件後（`config.yml`），​CIDRAM將尋找『配置覆蓋文件』特定於所請求的域（`xn--cjs74vvlieukn40a.tld.config.yml`），​並如果發現，​由配置覆蓋文件定義的任何配置值將用於執行實例而不是由配置文件定義的配置值。​配置覆蓋文件與配置文件相同，​並通過您的決定，​可能包含CIDRAM可用的所有配置指令，​或任何必需的章節當需要。​配置覆蓋文件根據它們旨在的域來命名（所以，​例如，​如果您需要一個配置覆蓋文件為域，​`https://www.some-domain.tld/`，​它的配置覆蓋文件應該被命名`some-domain.tld.config.yml`，​和它應該放置在`vault`與配置文件，​`config.yml`）。​域名是從標題`HTTP_HOST`派生的；『www』被忽略。

#### <a name="PAY_YOU_TO_DO_IT"></a>我不想浪費時間安裝這個和確保它在我的網站上功能正常；我可以僱用您這樣做嗎？

也許。​這是根據具體情況考慮的。​告訴我們您需要什麼，​您提供什麼，​和我們會告訴您是否可以幫忙。

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>我可以聘請您或這個項目的任何開發者私人工作嗎？

*參考上面。​*

#### <a name="SPECIALIST_MODIFICATIONS"></a>我需要專家修改，​的定制，​等等；您能幫我嗎？

*參考上面。​*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>我是開發人員，​網站設計師，​或程序員。​我可以接受還是提供與這個項目有關的工作？

您可以。​我們的許可證並不禁止這一點。

#### <a name="WANT_TO_CONTRIBUTE"></a>我想為這個項目做出貢獻；我可以這樣做嗎？

您可以。​對項目的貢獻是歡迎。​有關詳細信息，​請參閱『CONTRIBUTING.md』。

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>可以使用cron自動更新嗎？

您可以。​前端有內置了API，外部腳本可以使用它與更新頁面進行交互。​一個單獨的腳本，『[Cronable](https://github.com/Maikuolan/Cronable)』，是可用，它可以由您的cron manager或cron scheduler程序使用於自動更新此和其他支持的包（此腳本提供自己的文檔）。

#### <a name="WHAT_ARE_INFRACTIONS"></a>什麼是『違規』？

『簽名計數』和『違規』都與在任何特定請求期間觸發的簽名的嚴重性和數量是有關，無論是由於簽名文件、模塊、輔助規則、還是其他原因。​但是，雖然『簽名計數』僅針對該特定請求持續存在，但『違規』可以持續存在由`default_tracktime`確定的請求數量。

這確保了當請求因足夠數量的違規而被阻止時，來自同一源的後續請求也可以被阻止。

#### <a name="BLOCK_HOSTNAMES"></a>CIDRAM可以阻止主機名？

可以做。您將需要創建一個自定義模塊文件。 *看到：[基本概念（對於模塊）](#MODULE_BASICS)*.

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>在『default_dns』中我可以使用什麼？

通常，任何可靠的DNS服務器的IP應該就足夠了。​如果您正在尋找建議，[public-dns.info](https://public-dns.info/)和[OpenNIC](https://servers.opennic.org/)提供已知的公共DNS服務器的廣泛列表。​或者，請參閱下表：

IP | 操作者
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

*注意：​我對任何列出的DNS服務或其他方式的隱私慣例，安全性，功效和可靠性不做任何聲明或保證。​請在做出關於他們的決定時做您自己的研究。*

#### <a name="PROTECT_OTHER_THINGS"></a>我可以使用CIDRAM保護網站以外的東西嗎（例如，電子郵件服務器，FTP，SSH，IRC，等）？

您可以（在法律意義上說），但不應該（在技術和實際意義上）。​我們的許可證不限制哪些技術實施CIDRAM，但CIDRAM是一種WAF（Web應用程序防火牆），一直旨在保護網站。​因為它沒有考慮到其他技術，所以它不太可能有效或為其他技術提供可靠的保護，實施可能會很困難，並且假陽性和檢測錯過的風險非常高。

#### <a name="CDN_CACHING_PROBLEMS"></a>如果我在使用CDN或緩存服務的同時使用CIDRAM，會發生問題嗎？

也許。​這取決於相關服務的性質以及您如何使用它。​通常，如果您只緩存靜態資產（例如，圖像，CSS，等；任何通常不會隨時間變化的東西），則不應該有任何問題。​但是，如果您要緩存的數據通常會在請求時動態生成，或者如果您正在緩存POST請求的結果，那麼可能會有問題（這基本上會使您的網站及其環境成為強制靜態，並且CIDRAM不太可能在強制靜態環境中提供任何有意義的好處）。​CIDRAM也可能有特定的配置要求，具體取決於您使用的CDN或緩存服務（您需要確保為您正在使用的特定CDN或緩存服務正確配置CIDRAM）。​未能正確配置CIDRAM可能會導致嚴重假陽性和檢測錯過。

#### <a name="DDOS_ATTACKS"></a>CIDRAM會保護我的網站免受DDoS攻擊嗎？

總之：不，它不能。

更詳細地說闡述：CIDRAM將有助於減少不需要的流量的可能造成的影響，為您的網站（從而降低帶寬成本），為您的硬件（例如，您的服務器處理請求的能力），並可以幫助減少各種其他潛在的負面影響。​然而，為了理解這個問題，必須記住兩件重要的事情。

首先，CIDRAM是一個PHP包，因此可以在安裝PHP的機器上運行。​這意味著CIDRAM只能在服務器收到請求後才能看到並阻止請求。​其次，有效的DDoS緩解應該在請求到達DDoS攻擊所針對的服務器之前對其進行過濾。​理想情況下，DDoS攻擊應該在能夠首先到達目標服務器之前通過能夠丟棄或重新路由與攻擊相關的流量的解決方案來檢測和緩解。

這可以使用專用的內部部署硬件解決方案，基於雲的解決方案，如專用的DDoS緩解服務，通過耐DDoS網絡路由域名的DNS，基於雲的過濾，或者它們的一些組合實施。​無論如何，這個問題有點太複雜，不能僅僅用一到兩個段落來解釋，所以如果這是您想追求的主題，我會建議您做進一步的研究。​當DDoS攻擊的本質被正確理解時，這個答案會更有意義。

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>當我通過更新頁面啟用或禁用模塊或簽名文件時，它會在配置中它們將按字母數字排序。​我可以改變他們排序的方式嗎？

這個有可能。​如果您需要強制某些文件以特定順序執行，您可以在列出配置指令的位置中的在他們的名字之前添加一些任意數據，並用冒號分隔。​當更新頁面隨後再次對文件進行排序時，這個添加的任意數據會影響排序順序，因此導致它們按照您想要的順序執行，並且不需要重命名它們。

例如，假设配置指令包含如下列出的文件：

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

如果您想首先執行`file3.php`，您可以在文件名前添加`aaa:`或類似：

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

然後，如果啟用了新文件`file6.php`，當更新頁面再次對它們進行排序時，它應該像這樣結束：

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

當文件禁用時的情況是相同的。​相反，如果您希望文件最後執行，您可以在文件名前添加`zzz:`或類似。​在任何情況下，您都不需要重命名相關文件。

#### <a name="HOW_TO_USE_PDO"></a>『PDO DSN』是什麼？如何能PDO與CIDRAM一起使用？

『PDO』 是 『[PHP Data Objects](https://www.php.net/manual/zh/intro.pdo.php)』 的首字母縮寫（它的意思是『PHP數據對象』）。​它為PHP提供了一個接口，使其能夠連接到各種PHP應用程序通常使用的某些數據庫系統。

『DSN』 是 『[data source name](https://en.wikipedia.org/wiki/Data_source_name)』 的首字母縮寫（它的意思是『數據源名稱』）。​『PDO DSN』向PDO描述了它應如何連接到數據庫。

CIDRAM可以將PDO用於緩存。​為了使其正常工作，您需要相應地配置CIDRAM，從而啟用PDO，需要為CIDRAM創建一個新數據庫以供使用（如果您尚未想到要供CIDRAM使用的數據庫），並需要按照以下結構在數據庫中創建一個新表。

當數據庫連接成功時，但是必要的表不存在，表自動創建將嘗試。​但是，此行為尚未經過廣泛測試，因此無法保證成功。

當然，這僅在您確實希望CIDRAM使用PDO時適用。​如果您對CIDRAM使用平面文件緩存（按照其默認配置）或提供的任何其他各種緩存選項感到足夠滿意，則無需費心設置數據庫，數據庫表，等等。

下面描述的結構使用『cidram』作為其數據庫名稱，但是您可以使用任何想要的數據庫名稱，只要在DSN配置中名稱被複製。

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

CIDRAM的`pdo_dsn`應配置如下。

```
取決於所使用的數據庫驅動程序......
├─4d （警告：實驗性，未經測試，不建議！）
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └要查找數據庫的主機。
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └要使用的數據庫的名稱。
│                │              │
│                │              └連接的主機端口號。
│                │
│                └要查找數據庫的主機。
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └要使用的數據庫的名稱。
│    │          │
│    │          └要查找數據庫的主機。
│    │
│    └可能的值： 『mssql』， 『sybase』， 『dblib』。
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├可以是本地數據庫文件的路徑。
│                    │
│                    ├可以連接主機和端口號。
│                    │
│                    └如果要使用此功能，請參閱Firebird文檔。
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └要連接的在目錄中數據庫。
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └要連接的在目錄中數據庫。
├─mysql （最推薦！）
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └連接的主機端口號。
│                 │            │
│                 │            └要查找數據庫的主機。
│                 │
│                 └要使用的數據庫的名稱。
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├可以參考特定的在目錄中數據庫。
│               │
│               ├可以連接主機和端口號。
│               │
│               └如果要使用此功能，請參閱Oracle文檔。
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├可以參考特定的在目錄中數據庫。
│         │
│         ├可以連接主機和端口號。
│         │
│         └如果要使用此功能，請參閱ODBC/DB2文檔。
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └要使用的數據庫的名稱。
│               │              │
│               │              └連接的主機端口號。
│               │
│               └要查找數據庫的主機。
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └要使用的本地數據庫文件的路徑。
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └要使用的數據庫的名稱。
                   │         │
                   │         └連接的主機端口號。
                   │
                   └要查找數據庫的主機。
```

如果不確定如何構造DSN，請嘗試先查看它是否按原樣工作，而不進行任何更改。

請注意， `pdo_username` 和 `pdo_password` 應與您為數據庫選擇的用戶名和密碼相同。

#### <a name="BLOCK_CRON"></a>CIDRAM正在阻止cronjobs。​如何解決這個問題？

如果您為了cronjobs的目的使用專用文件，如果在普通用戶請求期間不需要調用它（即，在cronjobs上下文之外），解決此問題的最直接方法是在cronjobs期間不要執行CIDRAM（即，不要將CIDRAM鏈接到負責處理cronjobs的文件）。

或者，如果那不可能，但是您的cron服務器的IP地址相對一致且可預測，您可以嘗試將cron服務器的IP地址列入白名單，通過在自定義簽名文件中為其創建白名單簽名，或通過創建輔助規則為其。​如果您的cron服務器的IP地址定期旋轉並且不是特別可預測，但仍然來自同一特定網絡，您可以嘗試在`ignore.dat`文件中列出負責阻止該簽名的簽名章節的名稱。

如果您嘗試了所有這些想法，但沒有一個對您有用，或者如果您需要幫助弄清楚如何做，您可以在CIDRAM的issues頁面上創建新issue，以尋求幫助。

---


### 9. <a name="SECTION9"></a>法律信息

#### 9.0 章節前言

本文檔章節描述了有關該軟件包的使用和實施的可能法律考慮事項，並提供一些基本的相關信息。​這對於一些用戶來說可能很重要，作為確保遵守其運營所在國家可能存在的任何法律要求的一種手段。​一些用戶可能需要根據這些信息調整他們的網站政策。

首先，請認識到我（軟件包作者）不是律師或合格的法律專業人員。​因此，我無法合法提供法律建議。​此外，在某些情況下，不同國家和地區的具體法律要求可能會有所不同。​這些不同的法律要求有時可能會相互矛盾​（例如：支持[隱私權](https://zh.wikipedia.org/wiki/%E9%9A%B1%E7%A7%81%E6%AC%8A_(%E8%87%BA%E7%81%A3))和[被遺忘權](https://zh.wikipedia.org/wiki/%E8%A2%AB%E9%81%BA%E5%BF%98%E6%AC%8A)的國家，與支持擴展數據保留的國家相比）。​還要考慮到對軟件包的訪問不限於特定的國家或轄區，因此，軟件包用戶群很可能在地理上多樣化。​這些觀點認為，我無法說明在所有方面對所有用戶『符合法律』意味著什麼。​不過，我希望這裡的信息能夠幫助您自己決定您必須做些什麼為了在軟件包的上下文中符合法律。​如果您對此處的信息有任何疑問或擔憂，或者您需要從法律角度提供更多幫助和建議，我會建議諮詢合格的法律專業人員。

#### 9.1 法律責任

此軟件包不提供任何擔保（這已由包許可證提及）。​這包括（但不限於）所有責任範圍。​為了您的方便，該軟件包已提供給您。​希望它會有用，它會為您帶來一些好處。​但是，使用或實施該軟件包是您自己的選擇。​您不是被迫使用或實施該軟件包，但是當您這樣做時，您需要對該決定負責。​我，和其他軟件包貢獻者，對於您的決定的後果不承擔法律責任，無論是直接的，間接的，暗示的，還是其他方式。

#### 9.2 第三方

取決於其確切的配置和實施，在某些情況下，該軟件包可能與第三方進行通信和共享信息。​在某些情況下，某些轄區可能會將此信息定義為『[個人身份信息](https://zh.wikipedia.org/wiki/%E5%80%8B%E4%BA%BA%E5%8F%AF%E8%AD%98%E5%88%A5%E8%B3%87%E8%A8%8A)』（PII）。

這些信息如何被這些第三方使用，是受這些第三方制定的各種政策的約束，並且超出了本文檔的範圍。​但是，在所有這些情況下，與這些第三方共享信息可能被禁用。​在所有這些情況下，如果您選擇啟用它，則有責任研究您可能遇到的任何問題（如果您擔心這些第三方的隱私，安全，和PII使用情況）。​如果存在任何疑問，或者您對PII方面的這些第三方的行為不滿意，最好禁用與這些第三方分享的所有信息。

為了透明的目的，共享信息的類型，以及與誰共享，如下所述。

##### 9.2.0 主機名查找

如果您使用任何旨在與主機名配合使用的功能或模塊（例如，​『壞主機阻塞模塊』，​『tor project exit nodes block module』，​『搜索引擎驗證』），​CIDRAM需要能夠以某種獲得入站請求的主機名。​通常，它通過請求來自DNS服務器的入站請求的IP地址的主機名來執行此操作，或者通過安裝CIDRAM的系統提供的功能請求信息（這通常被稱為『主機名查找』）。​默認定義的DNS服務器屬於[Google DNS](https://dns.google.com/)服務（但可以通過配置輕鬆更改）。​與之交流的確切服務是可配置的，並取決於您如何配置軟件包。​在使用安裝CIDRAM的系統提供的功能的情況下，您需要聯繫您的系統管理員以確定哪些為主機名查找的路由使用。​通過避免受影響的模塊或根據您的需要修改軟件包配置，可以防止CIDRAM中的主機名查找。

*相關配置指令：*
- `general` -> `default_dns`
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`
- `general` -> `force_hostname_lookup`
- `general` -> `allow_gethostbyaddr_lookup`

當啟用搜索引擎驗證時，CIDRAM嘗試執行『正向DNS查找』以驗證聲稱源自搜索引擎的請求是否真實。​同樣，當啟用社交媒體驗證時，CIDRAM對為社交媒體請求做同樣的事情。​為此，它使用[Google DNS](https://dns.google.com/)服務嘗試從這些入站請求的主機名解析IP地址（在這個過程中，這些入站請求的主機名與服務共享）。

*相關配置指令：*
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`

##### 9.2.2 CAPTCHA

CIDRAM支持reCAPTCHA和hCAPTCHA。​他們需要API密鑰才能正常工作。​默認情況下禁用，但它們可以通過配置所需的API密鑰啟用。​在啟用的情況下，在服務與CIDRAM或用戶的瀏覽器之間可能會發生通信。​這可能涉及通信信息，例如用戶的IP地址，用戶代理，操作系統，以及可用於請求的其他詳細信息。

##### 9.2.3 STOP FORUM SPAM 【停止論壇垃圾郵件】

[Stop Forum Spam](https://www.stopforumspam.com/)是一個輝煌的，免費提供的服務，可以幫助保護論壇，博客，和網站免受垃圾郵件製造者。​它提供了一個已知垃圾郵件發送者的數據庫，以及一個可用來檢查數據庫中是否列出IP地址，用戶名或電子郵件地址的API。

CIDRAM提供了一個可選模塊，它使用API​來檢查入站請求的IP地址是否屬於可疑垃圾郵件發送者。​如果安裝並激活模塊時候，則可以根據模塊的配置和預期用途將用戶的IP地址與服務共享。

##### 9.2.4 ABUSEIPDB

CIDRAM提供了一個可選模塊，用於使用[AbuseIPDB](https://www.abuseipdb.com/) API阻止濫用的IP地址。​如果安裝並激活模塊時候，則可以根據模塊的配置和預期用途將用戶的IP地址與服務共享。

##### 9.2.5 BGPVIEW

CIDRAM提供了一個可選模塊，以使用[BGPView](https://bgpview.io/)執行ASN和國家代碼查找。​提供了根據其ASN或來源國家阻止或將在白名單上放請求的功能。​如果安裝並激活模塊時候，則可以根據模塊的配置和預期用途將用戶的IP地址與服務共享。

##### 9.2.6 PROJECT HONEYPOT

CIDRAM提供了一個可選模塊，用於使用[Project Honeypot](https://www.projecthoneypot.org/) API阻止濫用的IP地址。​如果安裝並激活模塊時候，則可以根據模塊的配置和預期用途將用戶的IP地址與服務共享。

#### 9.3 日誌記錄

由於多種原因，日誌記錄是CIDRAM的重要組成部分。​當未記錄導致它們的阻止事件時，可能難以診斷和解決假陽性。​當未記錄阻止事件時，可能很難確定CIDRAM在某些情況下的表現如何，而且可能很難確定其不足之處，以及可能需要更改哪些配置或簽名，以使其繼續按預期運行。​無論如何，一些用戶可能不想要記錄，並且它仍然是完全可選的。​在CIDRAM中，默認情況下日誌記錄是禁用。​要啟用它，必須相應地配置CIDRAM。

另外，如果日誌記錄在法律上是允許的，並且在法律允許的範圍內（例如，可記錄的信息類型，多長時間，在什麼情況下），可以變化，具體取決於管轄區域和CIDRAM的實施上下文（例如，如果您是個人或公司實體經營，如果您在商業或非商業基礎上運營，等等）。​因此，仔細閱讀本節可能對您有用。

CIDRAM可以執行多種類型的日誌記錄。​不同類型的日誌記錄涉及不同類型的信息，出於各種原因。

##### 9.3.0 阻止事件

CIDRAM可以執行的主要日誌記錄類型與『阻止事件』有關。​當CIDRAM阻止請求時會發生這種日誌記錄類型，並且可以以三種不同的格式提供：
- 人類可讀的日誌文件。
- Apache風格的日誌文件。
- 序列化日誌文件。

記錄到人類可讀日誌文件的阻止事件通常看起來像這樣（作為示例）：

```
ID： 1234
腳本版本： CIDRAM v1.6.0
日期/時間： Day, dd Mon 20xx hh:ii:ss +0000
IP地址： x.x.x.x
主機名： dns.hostname.tld
簽名計數： 1
簽名參考： x.x.x.x/xx
為什麼被阻止： 雲服務 ("網絡名字", Lxx:Fx, [XX])!
用戶代理： Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
重建URI： https://your-site.tld/index.php
CAPTCHA狀態： 打開。
```

記錄到Apache樣式的日誌文件中的同一阻止事件看起來像這樣：

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

阻止事件記錄通常包括以下信息：
- 阻止事件的ID號碼。
- 目前正在使用的CIDRAM版本。
- 阻止事件發生的日期和時間。
- 被阻止請求的IP地址。
- 被阻止請求的IP地址的主機名（如果可用）。
- 請求觸發的簽名數。
- 觸發的簽名引用。
- 引用阻止事件的原因和一些基本的相關調試信息。
- 被阻止請求的用戶代理（即，請求實體如何向請求標識自己）。
- 重建最初請求的資源的標識符。
- 當前請求的CAPTCHA狀態（相關時）。

*負責此類日誌記錄的配置指令，適用於以下三種格式中的每一種：*
- `general` -> `logfile`
- `general` -> `logfile_apache`
- `general` -> `logfile_serialized`

當這些指令保留為空時，這種類型的日誌記錄將保持禁用狀態。

##### 9.3.1 CAPTCHA日誌記錄

此類日誌記錄特定於CAPTCHA實例，僅在用戶嘗試完成CAPTCHA實例時才會發生。

CAPTCHA日誌條目包含嘗試完成CAPTCHA實例的用戶的IP地址，嘗試發生的日期和時間以及CAPTCHA狀態。​CAPTCHA日誌條目通常看起來像這樣（作為示例）：

```
IP地址：x.x.x.x - Date/Time: Day, dd Mon 20xx hh:ii:ss +0000 - CAPTCHA狀態：成功！
```

*負責CAPTCHA日誌記錄的配置指令是：*
- `recaptcha` -> `logfile`
- `hcaptcha` -> `logfile`

##### 9.3.2 前端日誌記錄

此類日誌記錄涉及前端登錄嘗試，僅在用戶嘗試登錄前端時才會發生（假設啟用了前端訪問）。

前端日誌條目包含嘗試登錄的用戶的IP地址，嘗試發生的日期和時間以及的結果（登錄成功或失敗）。​前端日誌條目通常看起來像這樣（作為示例）：

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - 已登錄。
```

*負責前端日誌記錄的配置指令是：*
- `frontend` -> `frontend_log`

##### 9.3.3 日誌輪換

您可能希望在一段時間後清除日誌，或者可能被要求依法執行（即，您在法律上允許保留日誌的時間可能受法律限制）。​您可以通過在程序包配置指定的日誌文件名中包含日期/時間標記（例如，`{yyyy}-{mm}-{dd}.log`），​然後啟用日誌輪換來實現此目的（日誌輪換允許您在超出指定限制時對日誌文件執行某些操作）。

例如：如果法律要求我在30天后刪除日誌，我可以在我的日誌文件的名稱中指定`{dd}.log`（`{dd}`代表天），將`log_rotation_limit`的值設置為30，並將`log_rotation_action`的值設置為`Delete`。

相反，如果您需要長時間保留日誌，你可以選擇完全不使用日誌輪換，或者你可以將`log_rotation_action`的值設置為`Archive`，以壓縮日誌文件，從而減少它們佔用的磁盤空間總量。

*相關配置指令：*
- `general` -> `log_rotation_limit`
- `general` -> `log_rotation_action`

##### 9.3.4 日誌截斷

如果這是您想要做的事情，也可以在超過特定大小時截斷個別日誌文件。

*相關配置指令：*
- `general` -> `truncate`

##### 9.3.5 IP地址『PSEUDONYMISATION』

首先，如果您不熟悉這個術語，『pseudonymisation』是指處理個人數據，使其不能在沒有補充信息的情況下被識別為屬於任何特定的『數據主體』，並規定這些補充信息分開保存，採取技術和組織措施以確保個人數據不能被識別給任何自然人。

以下資源可以幫助更詳細地解釋它：
- [[trust-hub.com] What is pseudonymisation?](https://www.trust-hub.com/news/what-is-pseudonymisation/)
- [[Wikipedia] Pseudonymization](https://en.wikipedia.org/wiki/Pseudonymization)

在某些情況下，您可能在法律上要求對收集，處理，或存儲的任何PII進行『pseudonymise』或『anonymise』。​雖然這個概念已經存在了相當長的一段時間，但GDPR/DSGVO提到，並特別鼓勵『pseudonymisation』。

當記錄它們時，CIDRAM可以對IP地址進行pseudonymise，如果這是您想做的事情。​當這個情況發生時，IPv4地址的最後八位字節，以及IPv6地址的第二部分之後的所有內容，將由『x』表示（有效地將IPv4地址四捨五入到它的第24個子網因素的初始地址，和將IPv6地址四捨五入到它的第32個子網因素的初始地址）。

*注意：CIDRAM的IP地址pseudonymisation過程不會影響CIDRAM的IP跟踪功能。​如果這對您來說是個問題，最好完全禁用IP跟踪。*

*相關配置指令：*
- `legal` -> `pseudonymise_ip_addresses`

##### 9.3.6 省略日誌信息

如果要防止完全記錄特定類型的信息，也可以這樣做。​在配置頁面，請參考`fields`配置指令來控制哪些字段出現在日誌條目和『拒絕訪問』頁面上。

*注意：當完全從日誌中省略IP地址時，沒有理由對IP地址進行pseudonymise。*

*相關配置指令：*
- `general` -> `fields`

##### 9.3.7 統計

CIDRAM可選擇跟踪統計信息，例如自特定時間以來發生的阻止事件或CAPTCHA實例的總數。​默認情況下此功能是禁用，但可以通過程序包配置啟用此功能。​此功能僅跟踪發生的事件總數，不包括有關特定事件的任何信息（因此，不應被視為PII）。

*相關配置指令：*
- `general` -> `statistics`

##### 9.3.8 加密

CIDRAM不[加密](https://zh.wikipedia.org/wiki/%E5%8A%A0%E5%AF%86)其緩存或任何日誌信息。​可能會在將來引入緩存和日誌加密，但目前沒有任何具體的計劃。​如果您擔心未經授權的第三方獲取可能包含PII或敏感信息（如緩存或日誌）的CIDRAM部分的訪問權限，我建議不要將CIDRAM安裝在可公開訪問的位置（例如，在標準`public_html`或等效目錄之外【可用於大多數標準網絡服務器】安裝CIDRAM），​也我建議對安裝目錄強制執行適當的限制權限（特別是對於vault目錄）。​如果這還不足以解決您的疑慮，應該配置CIDRAM為不會首先收集或記錄引起您關注的信息類型（例如，通過禁用日誌記錄）。

#### 9.4 COOKIE

CIDRAM在其代碼庫中的兩個點設置[cookie](https://zh.wikipedia.org/wiki/Cookie)。​首先，當用戶成功完成CAPTCHA實例時（這假定`lockuser`設置為`true`），CIDRAM設置cookie，以便能夠在後續請求中記住用戶已經完成了CAPTCHA實例，這樣就不需要不斷要求用戶在後續請求中完成CAPTCHA實例。​其次，當用戶成功登錄前端時，CIDRAM設置cookie以便能夠在後續請求中的記住用戶（即，cookie用於向登錄會話驗證用戶身份）。

在這兩種情況下，cookie警告顯著顯示（適用時），警告用戶如果他們參與相關操作將設置cookie。 Cookie不會在代碼庫中的任何其他位置設置。

*注意：在某些司法管轄區中，『不可见的』 CAPTCHA API可能與Cookie法律不兼容，任何受這些法律約束的網站都應該避免這個API。​選擇改用其他提供的API，或完全禁用CAPTCHA，可能是更可取的選擇。*

*相關配置指令：*
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 9.5 市場營銷和廣告

CIDRAM不收集或處理任何信息用於營銷或廣告目的，既不銷售也不從任何收集或記錄的信息中獲利。​CIDRAM不是商業企業，也不涉及任何商業利益，因此做這些事情沒有任何意義。​自項目開始以來就一直如此，今天仍然如此。​此外，做這些事情會對整個項目的精神和預期目的產生反作用，並且只要我繼續維護項目，永遠不會發生。

#### 9.6 隱私政策

在某些情況下，您可能需要依法在您網站的所有頁面和部分上清楚地顯示您的隱私政策鏈接。​這可能為了確保用戶充分了解您的隱私慣例，收集的個人身份信息類型以及您打算如何使用它的是很重要。​為了能夠在CIDRAM的『拒絕訪問』頁面上包含這樣的鏈接，提供了配置指令來指定隱私策略的URL。

*注意：​強烈建議您的隱私政策頁面不放在CIDRAM的保護之後。​如果CIDRAM保護您的隱私政策頁面，並且被CIDRAM阻止的用戶點擊隱私政策的鏈接，他們將再次被阻止，並且無法看到您的隱私政策。​理想情況下，您應鏈接到您的隱私政策的靜態副本，例如HTML頁面或純文本文件，該文件不受CIDRAM保護。*

*相關配置指令：*
- `legal` -> `privacy_policy`

#### 9.7 GDPR/DSGVO

『通用數據保護條例』（GDPR）是歐盟法規，自2018年5月25日起生效。​該法規的主要目標是向歐盟公民和居民提供有關其個人數據的控制權，並統一歐盟內有關隱私和個人數據的法規。

該法規包含有關處理任何歐盟『數據主體』（任何已識別或可識別的自然人）的『[個人身份信息](https://zh.wikipedia.org/wiki/%E5%80%8B%E4%BA%BA%E5%8F%AF%E8%AD%98%E5%88%A5%E8%B3%87%E8%A8%8A)』（PII）的具體規定。​為了符合條例，『企業』（按照法規的定義），和任何相關的系統和流程必須默認實現『隱私設計』，​必須使用盡可能高的隱私設置，​必須對任何存儲或處理的信息實施必要的保護措施（數據的 pseudonymisation 或完整 anonymisation ），​必須明確無誤地聲明他們收集的數據類型，​他們如何處理數據，​出於何種原因，​他們保留多長時間，​以及他們是否與任何第三方分享這些數據，​與第三方共享的數據類型，​為什麼，​等等。

只有按照條例有合法依據才能處理數據。​一般而言，這意味著為了在合法基礎上處理數據主體的數據，必須遵守法律義務，或者僅在從數據主體獲得明確，明智，明確的同意之後才進行處理。

因為條例的各個方面可能會及時演變，並為了避免過時信息的傳播，從權威來源中學習可能會更好的，而不是簡單地在包文檔中包含相關信息（這個信息可能最終會過時）。

一些推薦的資源用於了解更多信息：
- [关于欧盟GDPR隐私合规，中国数字营销人不得不知的9大问题](http://www.adexchanger.cn/top_news/28813.html)
- [史上最严的隐私条例出台，2018年开始执行](https://zhuanlan.zhihu.com/p/20865602)
- [《欧盟数据保护条例》对中国企业的影响 —- 以阿里巴巴集团为例](https://spiegeler.com/%E3%80%8A%E6%AC%A7%E7%9B%9F%E6%95%B0%E6%8D%AE%E4%BF%9D%E6%8A%A4%E6%9D%A1%E4%BE%8B%E3%80%8B%E5%AF%B9%E4%B8%AD%E5%9B%BD%E4%BC%81%E4%B8%9A%E7%9A%84%E5%BD%B1%E5%93%8D-%E4%BB%A5%E9%98%BF%E9%87%8C/)
- [歐盟個人資料保護法 GDPR 即將上路！與電商賣家息息相關的 Google Analytics 資料保留政策，你瞭解了嗎？](https://shopline.hk/blog/google-analytics-gdpr/)
- [歐盟一般資料保護規範](https://zh.wikipedia.org/wiki/%E6%AD%90%E7%9B%9F%E4%B8%80%E8%88%AC%E8%B3%87%E6%96%99%E4%BF%9D%E8%AD%B7%E8%A6%8F%E7%AF%84)
- [REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679)

---


最後更新：2022年6月30日。
