## CIDRAM v3 中文（简体）文档。

### 内容
- 1. [前言](#user-content-SECTION1)
- 2. [如何安装](#user-content-SECTION2)
- 3. [如何使用](#user-content-SECTION3)
- 4. [前端管理](#user-content-SECTION4)
- 5. [配置选项](#user-content-SECTION5)
- 6. [签名格式](#user-content-SECTION6)
- 7. [已知的兼容问题](#user-content-SECTION7)
- 8. [常见问题（FAQ）](#user-content-SECTION8)
- 9. [法律信息](#user-content-SECTION9)

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### 1. <a name="SECTION1"></a>前言

CIDRAM （无类别域间路由访问管理器）是一个PHP脚本，​旨在保护网站途经阻止请求该从始发IP地址视为不良的流量来源，​包括（但不限于）流量该从非人类的访问端点，​云服务，​垃圾邮件发送者，​网站铲运机，​等等。​它通过计算CIDR的提供的IP地址从入站请求和试图匹配这些CIDR反对它的签名文件（这些签名文件包含CIDR的IP地址视为不良的流量来源）；如果找到匹配，​请求被阻止。

*(看到：[什么是“CIDR”？​](#user-content-WHAT_IS_A_CIDR))。​*

[CIDRAM](https://cidram.github.io/) COPYRIGHT 2016 和走向未来 GNU/GPLv2 由 [[Caleb M (Maikuolan)](https://github.com/Maikuolan)](https://github.com/Maikuolan)。

本脚本是基于GNU通用许可V2.0版许可协议发布的，​您可以在许可协议的允许范围内自行修改和发布，​但请遵守GNU通用许可协议。​使用脚本的过程中，​作者不提供任何担保和任何隐含担保。​更多的细节请参见GNU通用公共许可证，​下的`LICENSE.txt`文件也可从访问：
- <https://www.gnu.org/licenses/>。
- <https://opensource.org/licenses/>。

现在CIDRAM的代码文件和关联包可以从以下地址免费下载：
- [GitHub](https://github.com/CIDRAM/CIDRAM)。
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram)。
- [SourceForge](https://sourceforge.net/projects/cidram/)。

---


### 2. <a name="SECTION2"></a>如何安装

#### 2.0 安装手工

首先，您需要一个新的CIDRAM副本。​您可以从[CIDRAM/CIDRAM](https://github.com/CIDRAM/CIDRAM)存储库下载最新版本的CIDRAM存档。​具体来说，您需要一个“vault”目录的新副本​（存档中的所有其他内容都可以安全的删除或忽略）。

在v3之前，必须在公共根目录中的某个位置安装CIDRAM，以便能够访问CIDRAM前端。​但是，从v3开始，这不是必需的。​现在，为了最大限度地提高安全性并防止未经授权访问CIDRAM及其文件，建议将CIDRAM安装在公共根目录之外。​只要PHP可以访问它，只要它是安全的，只要您对它感到满意，您就可以在任何地方安装CIDRAM。​不再需要将目录名称保留为“vault”，因此您可以将其重命名为您想要的任何名称​（但为了方便起见，文档将继续将其称为“vault”目录）。

当您准备好，将“vault”目录上传到您选择的位置，并确保它具有必要的权限，以便PHP能够写入该目录​（根据系统，您可能不需要做任何事情，或者您可能需要将CHMOD 755设置为目录，或者如果755有问题，您可以试试777，但不推荐777因为它不太安全）。

接下来，为了让CIDRAM能够保护您的代码库或CMS，您需要创建一个“入口点”。​这样的入口点包括三件事：

1. 在代码库或CMS的适当位置包含“loader.php”文件。
2. CIDRAM core的实例化。
3. 调用“protect”方法。

简单的例子：

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

如果您使用Apache网络服务器并且可以访问`php.ini`，则可以使用`auto_prepend_file`指令在任何PHP请求发出时执行CIDRAM。​在这种情况下，创建入口点的最合适位置是在其自己的文件中，然后您将在`auto_prepend_file`指令中引用该文件。

例子：

`auto_prepend_file = "/path/to/your/entrypoint.php"`

或者在`.htaccess`文件中：

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

在其他情况下，创建入口点的最合适位置可能是在代码库或CMS中的最早点。​这确保了每当访问您网站上的页面时它总是会执行。​如果您的代码库使用“引导程序”，那么该文件的开头就是一个很好的例子。​如果您的代码库有一个中央文件负责连接到您的数据库，那么该文件的开头将是另一个很好的例子。

#### 2.1 与COMPOSER安装

[CIDRAM是在Packagist上](https://packagist.org/packages/cidram/cidram)，​所以，​如果您熟悉Composer，​您可以使用Composer安装CIDRAM。

`composer require cidram/cidram`

#### 2.2 为WORDPRESS安装

[CIDRAM在WordPress插件数据库中注册](https://wordpress.org/plugins/cidram/)，​您可以直接从插件仪表板安装CIDRAM。​您可以像其他插件一样安装，​不需要添加步骤。

*警告：在插件仪表板里更新CIDRAM会导致干净的安装！​如果您已经自定义了您的安装（更改了您的配置，​安装的模块等），​在插件仪表板里进行更新时，​这些定制将会丢失！​日志文件也将丢失！​要保留日志文件和自定义，​请通过CIDRAM前端更新页面进行更新。​*

#### 2.3 配置和定制

强烈建议您检查新安装的配置，以便能够根据需要进行调整。​您可能还想安装其他模块、签名文件、创建辅助规则、或实施其他自定义，以便您的安装能够最好地满足您的需求。​我建议使用前端来做这些事情。

---


### 3. <a name="SECTION3"></a>如何使用

CIDRAM 应自动阻止不良的请求至您的网站，​没有任何需求除了初始安装。

您可以定制您的配置和您可以定制什么CIDR被阻止通过修改您的配置文件和/或您的签名文件.

如果您遇到任何假阳性，​请联系我让我知道这件事。 *(看到：[什么是“假阳性”？​](#user-content-WHAT_IS_A_FALSE_POSITIVE))。​*

CIDRAM可以手动或通过前端更新。​CIDRAM也可以通过Composer或WordPress更新，如果最初通过这些方式安装的话。

---


### 4. <a name="SECTION4"></a>前端管理

#### 4.0 什么是前端。

前端提供了一种方便，​轻松的方式来维护，​管理和更新CIDRAM安装。​您可以通过日志页面查看，​共享和下载日志文件，​您可以通过配置页面修改配置，​您可以通过更新页面安装和卸载组件，​和您可以通过文件管理器上传，​下载和修改文件在vault。

#### 4.1 如何访问前端。

就像以前一样，您需要创建一个入口点才能访问前端。​这样的入口点包括三件事：

1. 在代码库或CMS的适当位置包含“loader.php”文件。
2. CIDRAM front-end的实例化。
3. 调用“view”方法。

简单的例子：

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

“FrontEnd”类扩展了“Core”类。​这意味着您可以在调用“view”方法之前调用“protect”方法，以阻止可能不需要的流量访问前端。​这样做完全是可选的。

简单的例子：

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

为前端创建入口点的最合适位置是在其自己的专用文件中。​与以前不同，您希望前端入口点只能通过直接请求入口点所在的特定文件来访问。​因此，您不想在此处使用`auto_prepend_file`或`.htaccess`。

创建前端入口点后，使用浏览器访问它。​应该显示一个登录页面。​在登录页面，输入默认用户名和密码（admin/password），然后按登录按钮。

注意：第一次登录后，​以防止未经授权的访问前端，​您应该立即更改您的用户名和密码！​这是非常重要的，​因为它可以任意PHP代码上传到您的网站通过前端。

此外，为了获得最佳安全性，强烈建议为所有前端帐户启用“双因素身份验证”（下面提供的说明）。

#### 4.2 如何使用前端。

每个前端页面上都有说明，​用于解释正确的用法和它的预期目的。​如果您需要进一步的解释或帮助，​请联系支持。​另外，​YouTube上还有一些演示视频。

#### 4.3 2FA（双因素身份验证）

通过启用双因素身份验证，可以使前端更安全。​当登录使用2FA的帐户时，会向与该帐户关联的电子邮件地址发送电子邮件。​此电子邮件包含“2FA代码”，用户必须输入它（以及他们的用户名和密码），为了能够使用该帐户登录。​这意味着获取帐户密码不足以让任何黑客或潜在攻击者能够帐户登录，因为他们还需要访问帐户的电子邮件地址才能接收和使用会话的2FA代码（从而使前端更安全）。

首先，为了启用双因素身份验证，请使用前端更新页面来安装PHPMailer组件。​CIDRAM使用PHPMailer发送电子邮件。

在安装PHPMailer后，您需要通过CIDRAM配置页面或配置文件填充PHPMailer的配置指令。​有关这些配置指令的更多信息包含在本文档的配置部分中。​在填充PHPMailer配置指令后，将`enable_two_factor`设置为`true`。​现在应启用双因素身份验证。

接下来，您需要让CIDRAM知道在使用该帐户登录时将2FA代码发送到何处。​为此，请使用电子邮件地址作为帐户的用户名（例如，`foo@bar.tld`），或者将电子邮件地址作为用户名的一部分包括在内，就像通常发送电子邮件一样（例如，`Foo Bar <foo@bar.tld>`）。

注意：保护您的vault免受未经授权的访问（例如，通过加强服务器的安全性和限制公共访问权限）在此非常重要，因为未经授权访问您的配置文件（存储在您的vault中）可能会暴露您的出站SMTP设置（包括SMTP用户名和密码）。​在启用双因素身份验证之前，应确保您的vault已正确保护。​如果您无法做到这一点，那么至少应该创建一个专门用于此目的的新电子邮件帐户，为了降低与暴露的SMTP设置相关的风险。

---


### 5. <a name="SECTION5"></a>配置选项

下列是一个列表的变量发现在`config.yml`配置文件的CIDRAM，​以及一个说明的他们的目的和功能。

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

#### “general” （类别）
基本配置（任何不属于其他类别的核心配置）。

##### “stages” `[string]`
- 用于执行链的各个阶段的控件（是否启用，是否记录错误，等等）。

```
stages
├─Tests ("执行签名文件测试")
├─Modules ("执行模块")
├─SearchEngineVerification ("执行搜索引擎验证")
├─SocialMediaVerification ("执行社交媒体验证")
├─OtherVerification ("执行其他验证")
├─Aux ("执行辅助规则")
├─Reporting ("执行报告")
├─Tracking ("执行IP跟踪")
├─RL ("执行速率限制")
├─CAPTCHA ("部署验证码（被阻止的请求）")
├─Statistics ("更新统计")
├─Webhooks ("执行webhook")
├─PrepareFields ("为输出和日志准备字段")
├─Output ("生成输出（被阻止的请求）")
├─WriteLogs ("写入日志（被阻止的请求）")
├─Terminate ("终止请求（被阻止的请求）")
├─AuxRedirect ("根据辅助规则重定向")
└─NonBlockedCAPTCHA ("部署验证码（非阻止的请求）")
```

##### “fields” `[string]`
- 用于阻止事件的字段控件（当请求被阻止时）。

```
fields
├─ID ("ID")
├─ScriptIdent ("脚本版本")
├─DateTime ("日期/时间")
├─IPAddr ("IP地址")
├─IPAddrResolved ("IP地址（解决）")
├─Query ("网页查询")
├─Referrer ("引荐")
├─UA ("用户代理")
├─UALC ("用户代理（小写）")
├─SignatureCount ("签名计数")
├─Signatures ("签名参考")
├─WhyReason ("为什么被阻止")
├─ReasonMessage ("为什么被阻止（详细）")
├─rURI ("重建URI")
├─Infractions ("违规")
├─ASNLookup ("ASN查询")
├─CCLookup ("国家代码查询")
├─Verified ("身份验证")
├─Expired ("已过期")
├─Ignored ("忽略了")
├─Request_Method ("请求方法")
├─Protocol ("协议")
├─Hostname ("主机名")
└─CAPTCHA ("CAPTCHA状态")
```

##### “timezone” `[string]`
- 这用于指定要使用的时区​（例如，Africa/Cairo，America/New_York，Asia/Tokyo，Australia/Perth，Europe/Berlin，Pacific/Guam，等等）。​指定“SYSTEM”使PHP自动为您处理。

```
timezone
├─SYSTEM ("使用系统默认时区。")
├─UTC ("UTC")
└─…其他
```

##### “time_offset” `[int]`
- 时区偏移量（分钟）。

##### “time_format” `[string]`
- CIDRAM使用的日期符号格式。​可根据要求增加附加选项。

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

##### “ipaddr” `[string]`
- 在哪里可以找到连接请求IP地址？​（可以使用为服务例如Cloudflare和类似）。​标准 = REMOTE_ADDR。​警告：不要修改此除非您知道什么您做着！

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (标准)")
└─…其他
```

也可以看看：
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### “http_response_header_code” `[int]`
- 阻止请求时，CIDRAM应发送哪个HTTP状态消息？

```
http_response_header_code
├─200 (200 OK （好的）): 最不健壮，但最用户友好。​自动请求很可能将此响应解释为成功。
├─403 (403 Forbidden （禁止的）): 更健壮，但不太用户友好。​一般最推荐的。
├─410 (410 Gone （走了）): 解决假阳性时可能会导致问题，因为某些浏览器会缓存此状态消息并且不会发送后续请求，即使在被解除阻止后也是如此。​在某些情况下可能是最可取的。
├─418 (418 I'm a teapot （我是一个茶壶）): 引用愚人节的笑话【{{Links.RFC2324}}】。​任何客户端、机器人、浏览器、或其他方式都不太可能理解。​它是为了娱乐和方便而提供的，但是通常不推荐。
├─451 (451 Unavailable For Legal Reasons （因法律原因不可用）): 主要出于法律原因被阻止时推荐。​不推荐在其他情况下。
└─503 (503 Service Unavailable （服务不可用）): 最健壮，但最不用户友好。​推荐用于受到攻击，或处理极其持久的有害流量时。
```

##### “silent_mode” `[string]`
- CIDRAM应该默默重定向被拦截的访问而不是显示该“拒绝访问”页吗？​指定位置至重定向被拦截的访问，​或让它空将其禁用。

##### “lang” `[string]`
- 指定标准CIDRAM语言。

```
lang
├─en ("English")
├─ar ("العربية")
├─bn ("বাংলা")
├─de ("Deutsch")
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
├─pl ("Polski")
├─pt ("Português")
├─ru ("Русский")
├─sv ("Svenska")
├─ta ("தமிழ்")
├─th ("ภาษาไทย")
├─tr ("Türkçe")
├─uk ("Українська")
├─ur ("اردو")
├─vi ("Tiếng Việt")
├─zh ("中文（简体）")
└─zh-tw ("中文（傳統）")
```

##### “lang_override” `[bool]`
- 尽可能根据HTTP_ACCEPT_LANGUAGE进行本地化？True（真）=进行本地化【标准】；False（假）=不要本地化。

##### “numbers” `[string]`
- 您如何喜欢显示数字？​选择最适合示例。

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

##### “emailaddr” `[string]`
- 如果您希望，​您可以提供电子邮件地址这里要给予用户当他们被阻止，​他们使用作为接触点为支持和/或帮助在的情况下他们错误地阻止。​警告:您提供的任何电子邮件地址，​它肯定会被获得通过垃圾邮件机器人和铲运机，​所以，​它强烈推荐如果选择提供一个电子邮件地址这里，​您保证它是一次性的和/或不是很重要（换一种说法，​您可能不希望使用您的主电子邮件地址或您的企业电子邮件地址）。

##### “emailaddr_display_style” `[string]`
- 您希望如何将电子邮件地址呈现给用户？

```
emailaddr_display_style
├─default ("可点击的链接")
└─noclick ("不可点击的文字")
```

##### “ban_override” `[int]`
- 覆盖“http_response_header_code”当“infraction_limit”已被超过？ 200 = 不要覆盖【标准】。​其他值与“http_response_header_code”的可用值相同。

```
ban_override
├─200 (200 OK （好的）): 最不健壮，但最用户友好。​自动请求很可能将此响应解释为成功。
├─403 (403 Forbidden （禁止的）): 更健壮，但不太用户友好。​一般最推荐的。
├─410 (410 Gone （走了）): 解决假阳性时可能会导致问题，因为某些浏览器会缓存此状态消息并且不会发送后续请求，即使在被解除阻止后也是如此。​在某些情况下可能是最可取的。
├─418 (418 I'm a teapot （我是一个茶壶）): 引用愚人节的笑话【{{Links.RFC2324}}】。​任何客户端、机器人、浏览器、或其他方式都不太可能理解。​它是为了娱乐和方便而提供的，但是通常不推荐。
├─451 (451 Unavailable For Legal Reasons （因法律原因不可用）): 主要出于法律原因被阻止时推荐。​不推荐在其他情况下。
└─503 (503 Service Unavailable （服务不可用）): 最健壮，但最不用户友好。​推荐用于受到攻击，或处理极其持久的有害流量时。
```

##### “default_dns” `[string]`
- DNS服务器列表，​用于主机名查找。​警告：不要修改此除非您知道什么您做着！

__常问问题。__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.zh.md#在default_dns中我可以使用什么" hreflang="zh-CN">在“default_dns”中我可以使用什么？</a></em>

##### “default_algo” `[string]`
- 定义要用于所有未来密码和会话的算法。

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### “statistics” `[string]`
- 控制要跟踪的统计信息。

```
statistics
├─Blocked-IPv4 ("请求已阻止 – IPv4")
├─Blocked-IPv6 ("请求已阻止 – IPv6")
├─Blocked-Other ("请求已阻止 – 其他")
├─Banned-IPv4 ("请求已禁止 – IPv4")
├─Banned-IPv6 ("请求已禁止 – IPv6")
├─Passed-IPv4 ("允许的请求 – IPv4")
├─Passed-IPv6 ("允许的请求 – IPv6")
├─Passed-Other ("允许的请求 – 其他")
├─CAPTCHAs-Failed ("CAPTCHA尝试 – 失败！")
└─CAPTCHAs-Passed ("CAPTCHA尝试 – 成功！")
```

##### “force_hostname_lookup” `[bool]`
- 强制主机名查找？​True（真）=跟踪；False（假）=不跟踪【标准】。​主机名查询通常在“根据需要”的基础上执行，但可以在所有请求上强制。​这可能会有助于提供日志文件中更详细的信息，但也可能会对性能产生轻微的负面影响。

##### “allow_gethostbyaddr_lookup” `[bool]`
- 当UDP不可用时允许gethostbyaddr查找？​True（真）=允许【标准】；False（假）=不允许。

注意：IPv6查找在某些32位系统上可能无法正常工作。

##### “disabled_channels” `[string]`
- 这可用于防止CIDRAM在发送请求时使用特定通道（例如，在更新时，在获取组件元数据时，等等）。

```
disabled_channels
├─GitHub ("GitHub")
├─BitBucket ("BitBucket")
└─GoogleDNS ("GoogleDNS")
```

##### “default_timeout” `[int]`
- 用于外部请求的默认超时？ 标准 = 12秒。

##### “sensitive” `[string]`
- 视为敏感页面的路径列表。​需要时，将根据重建的URI检查列出的每个路径。​以正斜杠开头的路径将被视为文字，并从请求的路径部分开始匹配。​否则，以非字母数字字符开头并以相同字符（或相同字符加上可选的“i”标志）结束的路径将被视为正则表达式。​任何其他类型的路径都将被视为文字，并且可以匹配URI的任何部分。​被视为敏感页面的路径可能会影响某些模块的行为方式，但不会产生任何其他影响。

#### “components” （类别）
CIDRAM使用的组件的启用和停用的配置。​通常由更新页面填充，但也可以从此处进行管理，以实现更好的控制以及更新页面无法识别的自定义组件。

##### “ipv4” `[string]`
- IPv4签名文件。

##### “ipv6” `[string]`
- IPv6签名文件。

##### “modules” `[string]`
- 模块。

##### “imports” `[string]`
- 进口。​通常用于向CIDRAM提供组件的配置信息。

##### “events” `[string]`
- 事件处理程序。​通常用于修改CIDRAM在内部的行为方式或提供附加功能。

#### “logging” （类别）
与日志相关的配置（与其他類別相關的被排除）。

##### “standard_log” `[string]`
- 人类可读文件用于记录所有被拦截的访问。​指定一个文件名，​或留空以禁用。

##### “apache_style_log” `[string]`
- Apache风格文件用于记录所有被拦截的访问。​指定一个文件名，​或留空以禁用。

##### “serialised_log” `[string]`
- 连载的文件用于记录所有被拦截的访问。​指定一个文件名，​或留空以禁用。

##### “error_log” `[string]`
- 用于记录检测到的任何非致命错误的文件。​指定一个文件名，​或留空以禁用。

##### “report_log” `[string]`
- 用于记录发送到外部API的任何报告的文件。​指定一个文件名，​或留空以禁用。

##### “truncate” `[string]`
- 截断日志文件当他们达到一定的大小吗？​值是在B/KB/MB/GB/TB，​是日志文件允许的最大大小直到它被截断。​默认值为“0KB”将禁用截断（日志文件可以无限成长）。​注意：适用于单个日志文件！​日志文件大小不被算集体的。

##### “log_rotation_limit” `[int]`
- 日志轮转限制了任何时候应该存在的日志文件的数量。​当新的日志文件被创建时，如果日志文件的指定的最大数量已经超过，将执行指定的操作。​您可以在此指定所需的限制。​值为“0”将禁用日志轮转。

##### “log_rotation_action” `[string]`
- 日志轮转限制了任何时候应该存在的日志文件的数量。​当新的日志文件被创建时，如果日志文件的指定的最大数量已经超过，将执行指定的操作。​您可以在此处指定所需的操作。

```
log_rotation_action
├─Delete ("删除最旧的日志文件，直到不再超出限制。")
└─Archive ("首先归档，然后删除最旧的日志文件，直到不再超出限制。")
```

##### “log_banned_ips” `[bool]`
- 包括IP禁止从阻止请求在日志文件吗？​True（真）=是【标准】；False（假）=不是。

##### “log_sanitisation” `[bool]`
- 当使用前端日志页面查看日志数据时，CIDRAM在显示之前清理日志数据。​这可以保护用户免受XSS攻击和其他潜在威胁。​但是，默认情况下，在记录期间不会清理数据。​这是为了确保准确地保留日志数据（可以帮助任何未来的启发式或法医分析）。​但是，如果用户尝试使用外部工具读取日志数据，如果这些外部工具不执行自己的清理过程，用户可能会受到XSS攻击。​如有必要，可以使用此配置指令更改默认行为。 True = 记录数据时清理数据（数据保存不太准确，但XSS风险较低）。 False = 记录数据时不要清理数据（数据保存得更准确，但XSS风险更高）【标准】。

#### “frontend” （类别）
前端的配置。

##### “frontend_log” `[string]`
- 前端登录尝试的录音文件。​指定一个文件名，​或留空以禁用。

##### “signatures_update_event_log” `[string]`
- 通过前端更新签名时用于记录的文件。​指定一个文件名，​或留空以禁用。

##### “max_login_attempts” `[int]`
- 最大前端登录尝试次数。​标准=5。

##### “theme” `[string]`
- 用于前端的默认主题。

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

##### “magnification” `[float]`
- 字体放大。​标准 = 1。

##### “custom_header” `[string]`
- 在所有前端页面的开头作为HTML插入。​如果您想在所有此类页面中包含网站徽标、个性化标题、脚本、或类似，这可能会很有用。

##### “custom_footer” `[string]`
- 在所有前端页面的末尾作为HTML插入。​如果您想在所有此类页面中包含法律声明、联系链接、业务信息、或类似，这可能会很有用。

##### “remotes” `[string]`
- 更新系统用于获取组件元数据的地址列表。​这可能需要在升级到新的主要版本时进行调整，或者在获取新的更新源时进行调整，但在正常情况下应该不理会。

##### “enable_two_factor” `[bool]`
- 该指令确定是否将2FA用于前端帐户。

#### “signatures” （类别）
签名，签名文件，模块，等的配置。

##### “shorthand” `[string]`
- 当与使用给定速记词的签名匹配时，控制如何处理请求。

```
shorthand
├─Attacks ("攻击")
├─Bogon ("⁰ 火星IP")
├─Cloud ("云服务")
├─Generic ("通用")
├─Legal ("¹ 法律义务")
├─Malware ("恶意软件")
├─Proxy ("² 代理")
├─Spam ("垃圾邮件的风险")
├─Banned ("³ 禁止")
├─BadIP ("³ 无效的IP！")
├─RL ("³ 速率限制")
└─Other ("⁴ 其他")
```

__0.__ 如果您的网站需要通过LAN或localhost访问，不要阻止它。​否则，您可以阻止它。

__1.__ 标准签名文件不使用它，但它仍然受支持，因为它可能对某些用户有用。

__2.__ 如果您需要用户能够通过代理访问您的网站，不要阻止它。​否则，您可以阻止它。

__3.__ 不支持直接在签名中使用，但在特定情况下可以通过其他方式调用。

__4.__ 当速记词不使用或CIDRAM不识别时。

__对于每个签名只有一个。__ 签名可以调用多个分类，但只能使用一个速记词。​多个速记词可能是合适的，但由于只能使用一个，我们试图始终只使用最合适的。

__优先。__ 选定的选项始终优先于未选定的选项。​例如，如果多个速记词是生效的，但只有一个被设置为被阻止，则请求仍将被阻止。

__人类端点和云服务。__ 云服务可能是指虚拟主机提供商、服务器场、数据中心、或许多其他事物。​人类端点是指人类访问互联网的方式，例如，通过互联网服务提供商。​网络通常只提供一个或另一个，但有时可能同时提供两者。​我们试图不将潜在的人类端点识别为云服务。​因此，如果云服务的范围由已知的人类端点共享，则可以将其识别为其他东西。​同样，如果范围不被任何已知的人类端点共享，我们会试图始终将云服务识别为云服务。​因此，明确标识为云服务的请求很可能不会与任何已知的人类端点共享其范围。​同样，由攻击或垃圾邮件的风险明确识别的请求很可能共享范围。​然而，互联网总是在不断变化，网络的目的可以改变，范围总是被买卖，所以关于假阳性的保持有意识和警惕。

##### “default_tracktime” `[string]`
- 应跟踪IP地址的持续时间。​标准 = 7d0°0′0″ （1周）。

##### “infraction_limit” `[int]`
- 从IP最大允许违规数量之前它被禁止。​标准=10。

##### “tracking_override” `[bool]`
- 允许模块覆盖跟踪选项吗？​True（真）=允许【标准】；False（假）=不允许。

#### “verification” （类别）
请求来源验证配置。

##### “search_engines” `[string]`
- 用于验证来自搜索引擎的请求的控件。

```
search_engines
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

__什么是“阳性”和“阴性”？__ 在验证请求提供的身份时，成功的结果可以描述为“阳性”或“阴性”。​当所呈现的身份被确认为真实身份时，将被描述为“阳性”。​当所提供的身份被证实为伪造时，将被描述为“阴性”。​但是，不成功的结果（例如，验证失败，或无法确定所提供身份的真实性）不会被描述为“阳性”或“阴性”。​相反，不成功的结果将被简单地描述为未验证。​当没有尝试验证请求提供的身份时，该请求同样会被描述为未验证。​这些术语仅在请求提供的身份被识别的情况下才有意义，因此，在可以进行验证的情况下。​如果提供的身份与上面提供的选项不匹配，或者没有提供身份，则上面提供的选项变得无关。

__什么是“一击绕过”？__ 在某些情况下，由于签名文件、模块、或请求的其他条件，可能仍会阻止经过肯定验证的请求，为了避免误报，可能需要绕过。​在绕过旨在处理仅一项违规行为的情况下，这样的绕过可以被描述为“一击绕过”。

##### “social_media” `[string]`
- 用于验证来自社交媒体平台的请求的控件。

```
social_media
├─Embedly ("Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("Pinterest")
└─Twitterbot ("Twitterbot")
```

__什么是“阳性”和“阴性”？__ 在验证请求提供的身份时，成功的结果可以描述为“阳性”或“阴性”。​当所呈现的身份被确认为真实身份时，将被描述为“阳性”。​当所提供的身份被证实为伪造时，将被描述为“阴性”。​但是，不成功的结果（例如，验证失败，或无法确定所提供身份的真实性）不会被描述为“阳性”或“阴性”。​相反，不成功的结果将被简单地描述为未验证。​当没有尝试验证请求提供的身份时，该请求同样会被描述为未验证。​这些术语仅在请求提供的身份被识别的情况下才有意义，因此，在可以进行验证的情况下。​如果提供的身份与上面提供的选项不匹配，或者没有提供身份，则上面提供的选项变得无关。

__什么是“一击绕过”？__ 在某些情况下，由于签名文件、模块、或请求的其他条件，可能仍会阻止经过肯定验证的请求，为了避免误报，可能需要绕过。​在绕过旨在处理仅一项违规行为的情况下，这样的绕过可以被描述为“一击绕过”。

** 需要ASN查找功能（例如，通过IP-API或BGPView模块）。

##### “other” `[string]`
- 用于在可能的情况下，验证其他类型的请求的控件。

```
other
├─AdSense ("AdSense")
├─AmazonAdBot ("AmazonAdBot")
└─Grapeshot ("Oracle Data Cloud Crawler")
```

__什么是“阳性”和“阴性”？__ 在验证请求提供的身份时，成功的结果可以描述为“阳性”或“阴性”。​当所呈现的身份被确认为真实身份时，将被描述为“阳性”。​当所提供的身份被证实为伪造时，将被描述为“阴性”。​但是，不成功的结果（例如，验证失败，或无法确定所提供身份的真实性）不会被描述为“阳性”或“阴性”。​相反，不成功的结果将被简单地描述为未验证。​当没有尝试验证请求提供的身份时，该请求同样会被描述为未验证。​这些术语仅在请求提供的身份被识别的情况下才有意义，因此，在可以进行验证的情况下。​如果提供的身份与上面提供的选项不匹配，或者没有提供身份，则上面提供的选项变得无关。

__什么是“一击绕过”？__ 在某些情况下，由于签名文件、模块、或请求的其他条件，可能仍会阻止经过肯定验证的请求，为了避免误报，可能需要绕过。​在绕过旨在处理仅一项违规行为的情况下，这样的绕过可以被描述为“一击绕过”。

##### “adjust” `[string]`
- 在验证上下文中调整其他功能的控件。

```
adjust
├─Negatives ("被阻止的阴性")
└─NonVerified ("被阻止的未验证")
```

#### “recaptcha” （类别）
ReCaptcha的配置（为人们提供了一种在受阻时重新获得访问权限的方法）。

##### “usemode” `[int]`
- 何时应提供CAPTCHA吗？​注意：列入白名单或已验证且未阻止的请求永远不需要完成CAPTCHA。​另请注意：CAPTCHA可以提供有用的保护层，防止机器人和各种恶意自动请求，但不会提供任何针对恶意人类的保护。

```
usemode
├─0 (决不 !!!)
├─1 (仅当被阻止时，在签名限制之内，并且不被禁止。)
├─2 (仅当被阻止时，专门标明使用时，在签名限制之内，并且不被禁止。)
├─3 (仅在签名限制之内，并且不被禁止（不管是否被阻止）。)
├─4 (仅在不被阻止时。)
└─5 (仅在不被阻止时，或专门标明使用时，在签名限制之内，并且不被禁止。)
```

##### “lockip” `[bool]`
- 应该CAPTCHA锁定到IP？

##### “lockuser” `[bool]`
- 应该CAPTCHA锁定到用户？

##### “sitekey” `[string]`
- 可以在您的CAPTCHA服务的仪表板中找到该值。

也可以看看：
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### “secret” `[string]`
- 可以在您的CAPTCHA服务的仪表板中找到该值。

也可以看看：
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### “expiry” `[float]`
- 记得CAPTCHA多少小时？ 标准 = 720 （1个月）。

##### “recaptcha_log” `[string]`
- 记录所有的CAPTCHA的尝试？​要做到这一点，​指定一个文件名到使用。​如果不，​离开这个变量为空白。

##### “signature_limit” `[int]`
- 撤销CAPTCHA之前允许的最大签名数。标准 = 1。

##### “api” `[string]`
- 使用哪个API？

```
api
├─V2 ("V2 (选框)")
└─Invisible ("V2 (不可见的)")
```

##### “show_cookie_warning” `[bool]`
- 显示cookie警告吗？​True（真）=显示【标准】；False（假）=不显示。

##### “show_api_message” `[bool]`
- 显示API讯息吗？​True（真）=显示【标准】；False（假）=不显示。

##### “nonblocked_status_code” `[int]`
- 向未阻止的请求显示CAPTCHA时应使用哪个状态代码？

```
nonblocked_status_code
├─200 (200 OK （好的）): 最不健壮，但最用户友好。​自动请求很可能将此响应解释为成功。
├─403 (403 Forbidden （禁止的）): 更健壮，但不太用户友好。​一般最推荐的。
├─418 (418 I'm a teapot （我是一个茶壶）): 引用愚人节的笑话【{{Links.RFC2324}}】。​任何客户端、机器人、浏览器、或其他方式都不太可能理解。​它是为了娱乐和方便而提供的，但是通常不推荐。
├─429 (429 Too Many Requests （请求过多）): 推荐用于速率限制、处理DDoS攻击、和防洪。​不推荐在其他情况下。
└─451 (451 Unavailable For Legal Reasons （因法律原因不可用）): 主要出于法律原因被阻止时推荐。​不推荐在其他情况下。
```

#### “hcaptcha” （类别）
HCaptcha的配置（为人们提供了一种在受阻时重新获得访问权限的方法）。

##### “usemode” `[int]`
- 何时应提供CAPTCHA吗？​注意：列入白名单或已验证且未阻止的请求永远不需要完成CAPTCHA。​另请注意：CAPTCHA可以提供有用的保护层，防止机器人和各种恶意自动请求，但不会提供任何针对恶意人类的保护。

```
usemode
├─0 (决不 !!!)
├─1 (仅当被阻止时，在签名限制之内，并且不被禁止。)
├─2 (仅当被阻止时，专门标明使用时，在签名限制之内，并且不被禁止。)
├─3 (仅在签名限制之内，并且不被禁止（不管是否被阻止）。)
├─4 (仅在不被阻止时。)
└─5 (仅在不被阻止时，或专门标明使用时，在签名限制之内，并且不被禁止。)
```

##### “lockip” `[bool]`
- 应该CAPTCHA锁定到IP？

##### “lockuser” `[bool]`
- 应该CAPTCHA锁定到用户？

##### “sitekey” `[string]`
- 可以在您的CAPTCHA服务的仪表板中找到该值。

也可以看看：
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### “secret” `[string]`
- 可以在您的CAPTCHA服务的仪表板中找到该值。

也可以看看：
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### “expiry” `[float]`
- 记得CAPTCHA多少小时？ 标准 = 720 （1个月）。

##### “hcaptcha_log” `[string]`
- 记录所有的CAPTCHA的尝试？​要做到这一点，​指定一个文件名到使用。​如果不，​离开这个变量为空白。

##### “signature_limit” `[int]`
- 撤销CAPTCHA之前允许的最大签名数。标准 = 1。

##### “api” `[string]`
- 使用哪个API？

```
api
├─V1 ("V1")
└─Invisible ("V1 (不可见的)")
```

##### “show_cookie_warning” `[bool]`
- 显示cookie警告吗？​True（真）=显示【标准】；False（假）=不显示。

##### “show_api_message” `[bool]`
- 显示API讯息吗？​True（真）=显示【标准】；False（假）=不显示。

##### “nonblocked_status_code” `[int]`
- 向未阻止的请求显示CAPTCHA时应使用哪个状态代码？

```
nonblocked_status_code
├─200 (200 OK （好的）): 最不健壮，但最用户友好。​自动请求很可能将此响应解释为成功。
├─403 (403 Forbidden （禁止的）): 更健壮，但不太用户友好。​一般最推荐的。
├─418 (418 I'm a teapot （我是一个茶壶）): 引用愚人节的笑话【{{Links.RFC2324}}】。​任何客户端、机器人、浏览器、或其他方式都不太可能理解。​它是为了娱乐和方便而提供的，但是通常不推荐。
├─429 (429 Too Many Requests （请求过多）): 推荐用于速率限制、处理DDoS攻击、和防洪。​不推荐在其他情况下。
└─451 (451 Unavailable For Legal Reasons （因法律原因不可用）): 主要出于法律原因被阻止时推荐。​不推荐在其他情况下。
```

#### “legal” （类别）
法律要求的配置。

##### “pseudonymise_ip_addresses” `[bool]`
- 编写日志文件时使用假名的IP地址吗？​True（真）=使用假名【标准】；False（假）=不使用假名。

##### “privacy_policy” `[string]`
- 要显示在任何生成的页面的页脚中的相关隐私政策的地址。​指定一个URL，或留空以禁用。

#### “template_data” （类别）
模板和主题的配置。

##### “theme” `[string]`
- 用于CIDRAM的默认主题。

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

##### “magnification” `[float]`
- 字体放大。​标准 = 1。

##### “css_url” `[string]`
- 自定义主题的CSS文件URL。

##### “block_event_title” `[string]`
- 为阻止事件显示的页面标题。

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("拒绝访问！")
└─…其他
```

##### “captcha_title” `[string]`
- 为CAPTCHA请求显示的页面标题。

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…其他
```

##### “custom_header” `[string]`
- 在所有“拒绝访问”页面的开头作为HTML插入。​如果您想在所有此类页面中包含网站徽标、个性化标题、脚本、或类似，这可能会很有用。

##### “custom_footer” `[string]`
- 在所有“拒绝访问”页面的末尾作为HTML插入。​如果您想在所有此类页面中包含法律声明、联系链接、业务信息、或类似，这可能会很有用。

#### “rate_limiting” （类别）
速率限制的配置（不建议一般使用）。

##### “max_bandwidth” `[string]`
- 在为将来的请求启用速率限制之前的最大允许带宽量。​值为0将禁用此类速率限制。​标准=0KB。

##### “max_requests” `[int]`
- 在为将来的请求启用速率限制之前允许的最大请求数。​值为0将禁用此类速率限制。​标准=0。

##### “precision_ipv4” `[int]`
- 监视IPv4使用时的精度。​值镜像CIDR块大小。​设置为32以获得最佳精度。​标准=32。

##### “precision_ipv6” `[int]`
- 监视IPv6使用时的精度。​值镜像CIDR块大小。​设置为128以获得最佳精度。​标准=128。

##### “allowance_period” `[string]`
- 监视使用情况的持续时间。​标准=0°0′0″。

##### “exceptions” `[string]`
- 例外（即，不应限制速率的请求）。​仅在启用速率限制时有效。

```
exceptions
├─Whitelisted ("在白名单中的请求")
└─Verified ("经过验证的搜索引擎和社交媒体请求")
```

##### “segregate” `[bool]`
- 域名和主机的配额应该分开还是共享？ True = 配额将被分开。 False = 配额将被共享【标准】。

#### “supplementary_cache_options” （类别）
补充缓存选项。​注意：更改这些值可能会使您注销。

##### “prefix” `[string]`
- 该值将附加到所有缓存条目的键的开头。​标准 = “CIDRAM_”。​当同一服务器上存在多个安装时，这对于将它们的缓存彼此分开非常有用。

##### “enable_apcu” `[bool]`
- 指定是否尝试使用APCu进行缓存。​标准 = True。

##### “enable_memcached” `[bool]`
- 指定是否尝试使用Memcached进行缓存。​标准 = False。

##### “enable_redis” `[bool]`
- 指定是否尝试使用Redis进行缓存。​标准 = False。

##### “enable_pdo” `[bool]`
- 指定是否尝试使用PDO进行缓存。​标准 = False。

##### “memcached_host” `[string]`
- Memcached主机值。​标准 = “localhost”。

##### “memcached_port” `[int]`
- Memcached端口值。​标准 = “11211”。

##### “redis_host” `[string]`
- Redis主机值。​标准 = “localhost”。

##### “redis_port” `[int]`
- Redis端口值。​标准 = “6379”。

##### “redis_timeout” `[float]`
- Redis超时值。​标准 = “2.5”。

##### “pdo_dsn” `[string]`
- PDO DSN值。​标准 = “mysql:dbname=cidram;host=localhost;port=3306”。

__常问问题。__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.zh.md#HOW_TO_USE_PDO" hreflang="zh-CN">“PDO DSN”是什么？如何能PDO与CIDRAM一起使用？</a></em>

##### “pdo_username” `[string]`
- PDO用户名。

##### “pdo_password” `[string]`
- PDO密码。

#### “bypasses” （类别）
默认签名绕过配置。

##### “used” `[string]`
- 应该使用哪些绕过？

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

---


### 6. <a name="SECTION6"></a>签名格式

*也可以看看：*
- *[什么是“签名”？](#user-content-WHAT_IS_A_SIGNATURE)*

#### 6.0 基本概念（对于签名文件）

所有IPv4签名遵循格式：`xxx.xxx.xxx.xxx/yy [Function] [Param]`。
- `xxx.xxx.xxx.xxx` 代表CIDR块开始（初始IP地址八比特组）。
- `yy` 代表CIDR块大小 [1-32]。
- `[Function]` 指令脚本做什么用的署名（应该怎么签名考虑）。
- `[Param]` 代表任何其他信息其可以由需要 `[Function]`。

所有IPv6签名遵循格式：`xxxx:xxxx:xxxx:xxxx::xxxx/yy [Function] [Param]`。
- `xxxx:xxxx:xxxx:xxxx::xxxx` 代表CIDR块的开始（初始IP地址八比特组）。​完整符号和缩写符号是可以接受的（和每都必须遵循相应和相关IPv6符号标准，​但有一个例外：IPv6地址不能开头是与缩写当用来在签名该脚本，​由于以何种方式CIDR是构建由脚本；例如，​当用来在签名，​`::1/128`应该这样写`0::1/128`，​和`::0/128`应该这样写`0::/128`）。
- `yy` 代表CIDR块大小 [1-128]。
- `[Function]` 指令脚本做什么用的署名（应该怎么签名考虑）。
- `[Param]` 代表任何其他信息其可以由需要 `[Function]`。

CIDRAM签名文件应该使用Unix的换行符（`%0A`，​或`\n`）！​其他换行符类型/风格（例如，​Windows `%0D%0A`或`\r\n`换行符，​Mac `%0D`或`\r`换行符，​等等） 可以被用于，​但不是优选。​非Unix的换行符将正常化至Unix的换行符由脚本。

精准无误的CIDR符号是必须的，​不会是承认签名。​另外，​所有的CIDR签名必须用一个IP地址该始于一个数在该CIDR块分割适合于它的块大小（例如，​如果您想阻止所有的IP从`10.128.0.0`到`11.127.255.255`，​`10.128.0.0/8`不会是承认由脚本，​但`10.128.0.0/9`和`11.0.0.0/9`结合使用，​将是承认由脚本）。

任何数据在签名文件不承认为一个签名也不为签名相关的语法由脚本将被忽略，​因此，​这意味着您可以放心地把任何未签名数据和任何您想要的在签名文件没有打破他们和没有打破该脚本。​注释是可以接受的在签名文件，​和没有特殊的格式需要为他们。​Shell风格的哈希注释是首选，​但并非强制；从功能的角度，​无论您是否选择使用Shell风格的哈希注释，​有没有区别为脚本，​但使用Shell风格的哈希帮助IDE和纯文本编辑器正确地突出的各个签名章节文件（所以，​Shell风格的哈希可以帮助作为视觉辅助在编辑）。

`[Function]` 可能的值如下：
- Run
- Whitelist
- Greylist
- Deny

如果“Run”是用来，​当该签名被触发，​该脚本将尝试执行（使用一个`require_once`声明）一个外部PHP脚本，​由指定的`[Param]`值（工作目录应该是“/vault/”脚本目录）。

例子：`127.0.0.0/8 Run example.php`

这可能是有用如果您想执行一些特定的PHP代码对一些特定的IP和/或CIDR。

如果“Whitelist”是用来，​当该签名被触发，​该脚本将重置所有检测（如果有过任何检测）和打破该测试功能。​`[Param]`被忽略。​此功能将白名单一个IP地址或一个CIDR。

例子：`127.0.0.1/32 Whitelist`

如果“Greylist”是用来，​当该签名被触发，​该脚本将重置所有检测（如果有过任何检测）和跳到下一个签名文件以继续处理。​`[Param]`被忽略。

例子：`127.0.0.1/32 Greylist`

如果“Deny”是用来，​当该签名被触发，​假设没有白名单签名已触发为IP地址和/或CIDR，​访问至保护的页面被拒绝。​您要使用“Deny”为实际拒绝一个IP地址和/或CIDR范围。​当任何签名利用的“Deny”被触发，​该“拒绝访问”脚本页面将生成和请求到保护的页面会被杀死。

“Deny”的`[Param]`值会被解析为“拒绝访问”页面，​提供给客户机/用户作为引原因他们访问到请求的页面被拒绝。​它可以是一个短期和简单的句子，​为解释原因（什么应该足够了；一个简单的消息像“我不想让您在我的网站”会好起来的），​或一小撮之一的短关键字供应的通过脚本。​如果使用，​它们将被替换由脚本使用预先准备的解释为什么客户机/用户已被阻止。

预先准备的解释具有多语言支持和可以翻译通过脚本根据您的语言指定的通过`lang`脚本配置指令。​另外，​您可以指令脚本忽略“Deny”签名根据他们的价`[Param]`值（如果他们使用这些短关键字）通过脚本配置指令（每短关键字有一个相应的指令到处理相应的签名或忽略它）。​`[Param]`值不使用这些短关键字，​然而，​没有多语言支持和因此不会被翻译通过脚本，​并且还，​不能直接控制由脚本配置。

可用的短关键字是：
- Attacks
- Bogon
- Cloud
- Generic
- Legal
- Malware
- Proxy
- Spam

#### 6.1 标签

##### 6.1.0 章节标签

如果要分割您的自定义签名成各个章节，​您可以识别这些各个章节为脚本通过加入一个章节标签立即跟着每签名章节，​伴随着签名章节名字（看下面的例子）。

```
# 章节一。
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: 章节一
```

为了打破章节标签和以确保标签不是确定不正确的对于签名章节从较早的在签名文件，​确保有至少有两个连续的换行符之间您的标签和您的较早的签名章节。​任何未标记签名将默认为“IPv4”或“IPv6”（取决于签名类型被触发）。

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: 章节一
```

在上面的例子`1.2.3.4/32`和`2.3.4.5/32`将标为“IPv4”，​而`4.5.6.7/32`和`5.6.7.8/32`将标为“章节一”.

同样逻辑也可以应用于分离其他标签类型。

特别是，当假阳性发生时，章节标签对调试非常有用，通过提供一个简单的方法来找到问题的确切来源，并当通过前端日志页面查看日志文件时，可以非常有用地过滤日志文件条目​（章节名称可通过前端日志页面进行点击，并可用作过滤标准）。​如果在一些签名章节中章节标签是省略，当这些签名被触发时，CIDRAM使用签名文件的名称以及阻止的IP地址类型（IPv4或IPv6）作为后备，因此，章节标签是完全可选的。​但是，在某些情况下，可能会推荐使用它们，例如签名文件模糊地命名，或当难以清楚地识别阻止请求的签名的来源时。

##### 6.1.1 过期标签

如果您想签名一段时间后过期，​以类似的方式来章节标签，​您可以使用一个“过期标签”来指定在签名应该不再有效。​过期标签使用格式“年年年年.月月.日日”（看下面的例子）。

```
# 章节一。
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

过期的签名永远不会被任何请求触发。

##### 6.1.2 原产标签

如果您想要指定某个特定签名的原产国，可以使用“原产标签”来实现。​原产标签接受与其适用的签名相对应的国家的“[ISO 3166-1 二位字母](https://zh.wikipedia.org/wiki/ISO_3166-1)”代码。​这些代码必须写成大写（小写或混合大小写不能正确显示）。​当使用原产标签时，会将其添加到“为什么被阻止”日志字段条目中，为任何请求被阻止因为签名的标签应用。

如果安装了可选的“flags CSS”组件，当通过前端日志页面查看日志文件时，由原产标签附加的信息被其相应的国旗取代。​无论是原始形式还是国旗，这些信息是可点击的，并当点击时，它将通过类似识别的日志条目来过滤日志条目（从而有效地启用日志页面按来源国过滤）。

注意：从技术上讲，这不是任何形式的地理定位，因为它不涉及从IP查找特定的位置信息，反而，它允许我们当请求被特定的签名阻止时明确指出一个原产国。​同一个签名章节允许有多个原产标签。

假设的例子：

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

任何标签都可以联合使用，所有标签都是可选（看下面的例子）。

```
# 示例章节。
1.2.3.4/32 Deny Generic
Origin: US
Tag: 示例章节
Expires: 2016.12.31
```

##### 6.1.3 延缓标签

当大量安装并主动使用的签名文件时，安装可能会变得非常复杂，并且可能存在一些重叠的签名。​在这些情况下，为了防止在阻止事件期间触发多个重叠的签名，在大量安装并主动使用的某些其他特定签名文件的情况下，延缓标签可用于延缓特定签名章节。​在某些签名比其他签名更频繁更新的情况下，这可能很有用，为了延缓较不频繁更新的签名，于赞成更频繁更新的签名。

延缓标签与其他类型的标签类似地使用。​标签的值应该是要赞成的签名文件的名称。

例子：

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 6.1.4 分类标签

分类标签提供了一种在IP测试页面上显示其他信息的方式，并且模块和辅助规则可以利用分类标签来实现更复杂的行为和经过微调的决策。

分类标签的使用类似于其他类型的标签。​分类标签的值可用作模块和辅助规则的条件。​分类标签可以通过用分号分隔这些值来提供多个值。​最终用户永远不会看到分类标签的值。

例子：

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 6.2 YAML

##### 6.2.0 YAML基本概念

简化形式的YAML标记可以使用在签名文件用于目的定义行为和配置设置具体到个人签名章节。​这可能是有用的如果您希望您的配置指令值到变化之间的个人签名和签名章节（例如；如果您想提供一个电子邮件地址为支持票为任何用户拦截的通过一个特定的签名，​但不希望提供一个电子邮件地址为支持票为用户拦截的通过任何其他签名；如果您想一些具体的签名到触发页面重定向；如果您想标记一个签名为使用的reCAPTCHA/hCAPTCHA；如果您想日志拦截的访问到单独的文件按照个人签名和/或签名章节）。

使用YAML标记在签名文件是完全可选（即，​如果您想用这个，​您可以用这个，​但您没有需要用这个），​和能够利用最的（但不所有的）配置指令。

注意：YAML标记实施在CIDRAM是很简单也很有限；它的目的是满足特定要求的CIDRAM在方式具有熟悉的YAML标记，​但不跟随也不符合规定的官方规格（因此，​将不会是相同的其他实现别处，​和可能不适合其他项目别处）。

在CIDRAM，​YAML标记段被识别到脚本通过使用三个连字符（“---”），​和终止靠他们的签名章节通过双换行符。​一个典型的YAML标记段在一个签名章节被组成的三个连字符在一行立马之后的CIDR列表和任何标签，​接着是二维表为键值对（第一维，​配置指令类别；第二维，​配置指令）为哪些配置指令应修改（和哪些值）每当一个签名内那签名章节被触发（看下面的例子）。

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

##### 6.2.1 如何“特别标记”签名章节为使用的reCAPTCHA或hCAPTCHA

当“usemode”是“2”或“5”，​为“特别标记”签名章节为使用的reCAPTCHA或hCAPTCHA，​一个条目是包括在YAML段为了那个签名章节（看下面的例子）。

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

#### 6.3 辅

##### 6.3.0 忽略签名章节

此外，​如果您想CIDRAM完全忽略一些具体的章节内的任何签名文件，​您可以使用`ignore.dat`文件为指定忽略哪些章节。​在新行，​写`Ignore`，​空间，​然后该名称的章节您希望CIDRAM忽略（看下面的例子）。

```
Ignore 章节一
```

这也可以通过使用CIDRAM前端的“章节列表”页面提供的接口来实现。

##### 6.3.1 辅助规则

如果您觉得编写自己的自定义签名文件或自定义模块对您来说太复杂了，更简单的替代方案可能是使用CIDRAM前端的“辅助规则”页面提供的接口。​通过选择适当的选项并指定有关特定类型的请求的详细信息，您可以指示CIDRAM如何响应这些请求。​在所有签名文件和模块已经完成执行之后执行“辅助规则”。

#### 6.4 <a name="MODULE_BASICS"></a>基本概念（对于模块）

模块可用于扩展CIDRAM的功能，执行额外的任务，或处理额外的逻辑。

由于模块是作为PHP文件编写的，如果您对CIDRAM代码库有足够的了解，则可以根据需要构建模块，并根据需要编写模块签名​（在合理范围的什么可以用PHP来完成内）。

*注意：如果您不舒服使用PHP代码，则不建议编写自己的模块。*

CIDRAM提供了一些用于模块的功能，这将使编写自己的模块变得更简单和容易。​有关此功能的信息如下所述。

#### 6.5 模块功能

##### 6.5.0 “$this->trigger”

模块签名通常使用`$this->trigger`编写。​在大多数情况下，为了编写模块，这个闭包比其他任何东西都重要。

`$this->trigger`接受4个参数：`$Condition`、`$ReasonShort`、`$ReasonLong`（可选的）、和`$DefineOptions`（可选的）。

`$Condition`感实性被评估，和如果是true（真），签名是“触发”。​如果是false（假），签名不是“触发”。​`$Condition`通常包含PHP代码来评估应该导致请求被阻止的条件。

当签名被“触发”时，`$ReasonShort`在“为什么被阻止”字段中被引用。

`$ReasonLong`是一个可选消息，当用户/客户端被阻止时显示给用户/客户端，解释为什么他们被阻止。​省略时默认为标准的“拒绝访问”消息。

`$DefineOptions`是一个包含键/值对的可选数组，用于定义特定于请求实例的配置选项。​配置选项将在签名被“触发”时应用。

`$this->trigger`当签名是“触发”时将返回true（真），当签名不是“触发”时将返回false（假）。

##### 6.5.1 “$this->bypass”

签名旁路通常使用`$this->bypass`编写。

`$this->bypass`接受3个参数：`$Condition`、`$ReasonShort`、和`$DefineOptions`（可选的）。

`$Condition`感实性被评估，和如果是true（真），旁路是“触发”。​如果是false（假），旁路不是“触发”。​`$Condition`通常包含PHP代码来评估应不该导致请求被阻止的条件。

当旁路被“触发”时，`$ReasonShort`在“为什么被阻止”字段中被引用。

`$DefineOptions`是一个包含键/值对的可选数组，用于定义特定于请求实例的配置选项。​配置选项将在旁路被“触发”时应用。

`$this->bypass`当旁路是“触发”时将返回true（真），当旁路不是“触发”时将返回false（假）。

##### 6.5.2 “$this->dnsReverse”

这可以用来获取IP地址的主机名。​如果您想创建一个模块来阻止主机名，这个闭包可能是有用的。

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

#### 6.6 模块变量

模块在其自己的范围内执行，并且由模块定义的任何变量将不能被其他模块访问，也不由父脚本，除非它们存储在`$CIDRAM`数组中（模块执行完成后，其他所有内容都将被擦洗）。

下面列出了一些可能对您的模块有用的常见变量：

变量 | 说明
----|----
`$this->BlockInfo['DateTime']` | 当前日期和时间。
`$this->BlockInfo['IPAddr']` | 当前请求的IP地址。
`$this->BlockInfo['ScriptIdent']` | CIDRAM脚本版本。
`$this->BlockInfo['Query']` | 当前请求的查询。
`$this->BlockInfo['Referrer']` | 当前请求的引用者（如果存在）。
`$this->BlockInfo['UA']` | 当前请求的用户代理【user agent】。
`$this->BlockInfo['UALC']` | 当前请求的用户代理【user agent】（小写）。
`$this->BlockInfo['ReasonMessage']` | 当前请求被阻止时显示给用户/客户端的消息。
`$this->BlockInfo['SignatureCount']` | 当前请求的触发的签名数量。
`$this->BlockInfo['Signatures']` | 针对当前请求触发的任何签名的参考信息。
`$this->BlockInfo['WhyReason']` | 针对当前请求触发的任何签名的参考信息。

---


### 7. <a name="SECTION7"></a>已知的兼容问题

下列软件包和产品被发现与CIDRAM不兼容：
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

已提供模块以确保以下软件包和产品与CIDRAM兼容：
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__

*也可以看看：​[兼容性图表](https://maikuolan.github.io/Compatibility-Charts/)。*

---


### 8. <a name="SECTION8"></a>常见问题（FAQ）

- [什么是“签名”？](#user-content-WHAT_IS_A_SIGNATURE)
- [什么是“CIDR”？](#user-content-WHAT_IS_A_CIDR)
- [什么是“假阳性”？](#user-content-WHAT_IS_A_FALSE_POSITIVE)
- [CIDRAM可以阻止整个国家吗？](#user-content-BLOCK_ENTIRE_COUNTRIES)
- [什么是签名更新频率？](#user-content-SIGNATURE_UPDATE_FREQUENCY)
- [我在使用CIDRAM时遇到问题和我不知道该怎么办！​请帮忙！](#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [因为CIDRAM，​我被阻止从我想访问的网站！​请帮忙！](#user-content-BLOCKED_WHAT_TO_DO)
- [我想使用CIDRAM（在v2期间）与早于7.2的PHP版本；​您能帮我吗？](#user-content-MINIMUM_PHP_VERSION_V3)
- [我可以使用单个CIDRAM安装来保护多个域吗？](#user-content-PROTECT_MULTIPLE_DOMAINS)
- [我不想浪费时间安装这个和确保它在我的网站上功能正常；我可以雇用您这样做吗？](#user-content-PAY_YOU_TO_DO_IT)
- [我可以聘请您或这个项目的任何开发者私人工作吗？](#user-content-HIRE_FOR_PRIVATE_WORK)
- [我需要专家修改，​的定制，​等等；您能帮我吗？](#user-content-SPECIALIST_MODIFICATIONS)
- [我是开发人员，​网站设计师，​或程序员。​我可以接受还是提供与这个项目有关的工作？](#user-content-ACCEPT_OR_OFFER_WORK)
- [我想为这个项目做出贡献；我可以这样做吗？](#user-content-WANT_TO_CONTRIBUTE)
- [可以使用cron自动更新吗？](#user-content-CRON_TO_UPDATE_AUTOMATICALLY)
- [什么是“违规”？](#user-content-WHAT_ARE_INFRACTIONS)
- [CIDRAM可以阻止主机名？](#user-content-BLOCK_HOSTNAMES)
- [在“default_dns”中我可以使用什么？](#在default_dns中我可以使用什么)
- [我可以使用CIDRAM保护网站以外的东西吗（例如，电子邮件服务器，FTP，SSH，IRC，等）？](#user-content-PROTECT_OTHER_THINGS)
- [如果我在使用CDN或缓存服务的同时使用CIDRAM，会发生问题吗？](#user-content-CDN_CACHING_PROBLEMS)
- [CIDRAM会保护我的网站免受DDoS攻击吗？](#user-content-DDOS_ATTACKS)
- [当我通过更新页面启用或禁用模块或签名文件时，它会在配置中它们将按字母数字排序。​我可以改变他们排序的方式吗？](#user-content-CHANGE_COMPONENT_SORT_ORDER)
- [“PDO DSN”是什么？如何能PDO与CIDRAM一起使用？](#user-content-HOW_TO_USE_PDO)
- [CIDRAM正在阻止cronjobs。​如何解决这个问题？](#user-content-BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>什么是“签名”？

在CIDRAM的上下文中，​“签名”是一些数据，​它表示/识别我们正在寻找的东西，​通常是IP地址或CIDR，​并包含一些说明，​告诉CIDRAM最好的回应方法当它遇到我们正在寻找的。​CIDRAM的典型签名如下所示：

对于“签名文件”：

`1.2.3.4/32 Deny Generic`

对于“模块”：

```PHP
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*注意：“签名文件”的签名，和“模块”的签名，不是一回事。*

经常（但不总是），​签名是捆绑在一起，​形成“签名章节”，​经常伴随评论，​标记，​和/或相关元数据。​这可以用于为签名提供附加上下文和/或附加说明。

#### <a name="WHAT_IS_A_CIDR"></a>什么是“CIDR”？

“CIDR” 是 “Classless Inter-Domain Routing” 的首字母缩写 （“无类别域间路由”） *【[1](https://zh.wikipedia.org/wiki/%E6%97%A0%E7%B1%BB%E5%88%AB%E5%9F%9F%E9%97%B4%E8%B7%AF%E7%94%B1), [2](https://whatismyipaddress.com/cidr)】*。​这个首字母缩写用于这个包的名称，​“CIDRAM”，​是 “Classless Inter-Domain Routing Access Manager” 的首字母缩写 （“无类别域间路由访问管理器”）。

然而，​在CIDRAM的上下文中（如，​在本文档中，​在CIDRAM的讨论中，​或在CIDRAM语言数据中），​当“CIDR”（单数）或“CIDRs”（复数）被提及时（因此当我们用这些词作为名词在自己的权利，​而不作为首字母缩写），​我们的意图是一个子网，​用CIDR表示法表示。​使用CIDR/CIDRs而不是子网的原因是澄清它是用CIDR表示法表示的子网是我们的意思 （因为子网可以用几种不同的方式表达）。​因此，​CIDRAM可以被认为是“子网访问管理器”。

这个双重含义可能看起来很歧义，​但这个解释并提供上下文应该有助于解决这个歧义。

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>什么是“假阳性”？

术语“假阳性”（*或者：“假阳性错误”；“虚惊”*；英语：*false positive*； *false positive error*； *false alarm*），​很简单地描述，​和在一个广义上下文，​被用来当测试一个因子，​作为参考的测试结果，​当结果是阳性（即：因子被确定为“阳性”，​或“真”），​但预计将为（或者应该是）阴性（即：因子，​在现实中，​是“阴性”，​或“假”）。​一个“假阳性”可被认为是同样的“哭狼” (其中，​因子被测试是是否有狼靠近牛群，​因子是“假”由于该有没有狼靠近牛群，​和因子是报告为“阳性”由牧羊人通过叫喊“狼，​狼”），​或类似在医学检测情况，​当患者被诊断有一些疾病，​当在现实中，​他们没有疾病。

一些相关术语是“真阳性”，​“真阴性”和“假阴性”。​一个“真阳性”指的是当测试结果和真实因子状态都是“真”（或“阳性”），​和一个“真阴性”指的是当测试结果和真实因子状态都是“假”（或“阴性”）；一个“真阳性”或“真阴性”被认为是一个“正确的推理”。​对立面“假阳性”是一个“假阴性”；一个“假阴性”指的是当测试结果是“阴性”（即：因子被确定为“阴性”，​或“假”），​但预计将为（或者应该是）阳性（即：因子，​在现实中，​是“阳性”，​或“真”）。

在CIDRAM的上下文，​这些术语指的是CIDRAM的签名和什么/谁他们阻止。​当CIDRAM阻止一个IP地址由于恶劣的，​过时的，​或不正确的签名，​但不应该这样做，​或当它这样做为错误的原因，​我们将此事件作为一个“假阳性”。​当CIDRAM未能阻止IP地址该应该已被阻止，​由于不可预见的威胁，​缺少签名或不足签名，​我们将此事件作为一个“检测错过”（同样的“假阴性”）。

这可以通过下表来概括：

&nbsp; | CIDRAM不应该阻止IP地址 | CIDRAM应该阻止IP地址
---|---|---
CIDRAM不会阻止IP地址 | 真阴性（正确的推理） | 检测错过（同样的“假阴性”）
CIDRAM会阻止IP地址 | __假阳性__ | 真阳性（正确的推理）

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>CIDRAM可以阻止整个国家吗？

它可以。​最简单的方法是安装BGPView模块并根据需要进行配置。

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>什么是签名更新频率？

更新频率根据相关的签名文件而有所不同。​所有的CIDRAM签名文件的维护者通常尽量保持他们的签名为最新，​但是因为我们所有人都有各种其他承诺，​和因为我们的生活超越了项目，​和因为我们不得到经济补偿/付款为我们的项目的努力，​无法保证精确的更新时间表。​通常，​签名被更新每当有足够的时间，​和维护者尝试根据必要性和根据范围之间的变化频率确定优先级。​帮助总是感谢，​如果您愿意提供任何。

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>我在使用CIDRAM时遇到问题和我不知道该怎么办！​请帮忙！

- 您使用软件的最新版本吗？​您使用签名文件的最新版本吗？​如果这两个问题的答案是不，​尝试首先更新一切，​然后检查问题是否仍然存在。​如果它仍然存在，​继续阅读。
- 您检查过所有的文档吗？​如果没有做，​请这样做。​如果文档不能解决问题，​继续阅读。
- 您检查过[issues页面](https://github.com/CIDRAM/CIDRAM/issues)吗？​检查是否已经提到了问题。​如果已经提到了，​请检查是否提供了任何建议，​想法或解决方案。​按照需要尝试解决问题。
- 如果问题仍然存在，请通过在issues页面上创建新issue寻求帮助。

#### <a name="BLOCKED_WHAT_TO_DO"></a>因为CIDRAM，​我被阻止从我想访问的网站！​请帮忙！

CIDRAM使网站所有者能够阻止不良流量，​但网站所有者有责任为自己决定如何使用CIDRAM。​在关于默认签名文件假阳性的情况下，​可以进行校正。​但关于从特定网站解除阻止，​您需要与相关网站的所有者进行沟通。​当进行校正时，​至少，​他们需要更新他们的签名文件和/或安装。​在其他情况下（例如，​当他们修改了他们的安装，​当他们创建自己的自定义签名，​等等），​解决您的问题的责任完全是他们的，​并完全不在我们的控制之内。

#### <a name="MINIMUM_PHP_VERSION_V3"></a>我想使用CIDRAM（在v2期间）与早于7.2的PHP版本；​您能帮我吗？

不能。PHP≥7.2是CIDRAM v3的最低要求。

*也可以看看：​[兼容性图表](https://maikuolan.github.io/Compatibility-Charts/)。*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>我可以使用单个CIDRAM安装来保护多个域吗？

可以。​CIDRAM安装未绑定到特定域，​因此可以用来保护多个域。​通常，​当CIDRAM安装保护只一个域，​我们称之为“单域安装”，​和当CIDRAM安装保护多个域和/或子域，​我们称之为“多域安装”。​如果您进行多域安装并需要使用不同的签名文件为不同的域，​或需要不同配置CIDRAM为不同的域，​这可以做到。​加载配置文件后（`config.yml`），​CIDRAM将寻找“配置覆盖文件”特定于所请求的域（`xn--cjs74vvlieukn40a.tld.config.yml`），​并如果发现，​由配置覆盖文件定义的任何配置值将用于执行实例而不是由配置文件定义的配置值。​配置覆盖文件与配置文件相同，​并通过您的决定，​可能包含CIDRAM可用的所有配置指令，​或任何必需的章节当需要。​配置覆盖文件根据它们旨在的域来命名（所以，​例如，​如果您需要一个配置覆盖文件为域，​`https://www.some-domain.tld/`，​它的配置覆盖文件应该被命名`some-domain.tld.config.yml`，​和它应该放置在`vault`与配置文件，​`config.yml`）。​域名是从标题`HTTP_HOST`派生的；“www”被忽略。

#### <a name="PAY_YOU_TO_DO_IT"></a>我不想浪费时间安装这个和确保它在我的网站上功能正常；我可以雇用您这样做吗？

也许。​这是根据具体情况考虑的。​告诉我们您需要什么，​您提供什么，​和我们会告诉您是否可以帮忙。

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>我可以聘请您或这个项目的任何开发者私人工作吗？

*参考上面。​*

#### <a name="SPECIALIST_MODIFICATIONS"></a>我需要专家修改，​的定制，​等等；您能帮我吗？

*参考上面。​*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>我是开发人员，​网站设计师，​或程序员。​我可以接受还是提供与这个项目有关的工作？

您可以。​我们的许可证并不禁止这一点。

#### <a name="WANT_TO_CONTRIBUTE"></a>我想为这个项目做出贡献；我可以这样做吗？

您可以。​对项目的贡献是欢迎。​有关详细信息，​请参阅“CONTRIBUTING.md”。

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>可以使用cron自动更新吗？

您可以。​前端有内置了API，外部脚本可以使用它与更新页面进行交互。​一个单独的脚本，“[Cronable](https://github.com/Maikuolan/Cronable)”，是可用，它可以由您的cron manager或cron scheduler程序使用于自动更新此和其他支持的包（此脚本提供自己的文档）。

#### <a name="WHAT_ARE_INFRACTIONS"></a>什么是“违规”？

“签名计数”和“违规”都与在任何特定请求期间触发的签名的严重性和数量是有关，无论是由于签名文件、模块、辅助规则、还是其他原因。​但是，虽然“签名计数”仅针对该特定请求持续存在，但“违规”可以持续存在由`default_tracktime`确定的请求数量。

这确保了当请求因足够数量的违规而被阻止时，来自同一源的后续请求也可以被阻止。

#### <a name="BLOCK_HOSTNAMES"></a>CIDRAM可以阻止主机名？

可以做。这可以通过创建辅助规则或自定义模块来实现。

![阻止主机名的辅助规则](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>在“default_dns”中我可以使用什么？

通常，任何可靠的DNS服务器的IP应该就足够了。​如果您正在寻找建议，[public-dns.info](https://public-dns.info/)和[OpenNIC](https://servers.opennic.org/)提供已知的公共DNS服务器的广泛列表。​或者，请参阅下表：

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

*注意：​我对任何列出的DNS服务或其他方式的隐私惯例，安全性，功效和可靠性不做任何声明或保证。​请在做出关于他们的决定时做您自己的研究。*

#### <a name="PROTECT_OTHER_THINGS"></a>我可以使用CIDRAM保护网站以外的东西吗（例如，电子邮件服务器，FTP，SSH，IRC，等）？

您可以（在法律意义上说），但不应该（在技术和实际意义上）。​我们的许可证不限制哪些技术实施CIDRAM，但CIDRAM是一种WAF（Web应用程序防火墙），一直旨在保护网站。​因为它没有考虑到其他技术，所以它不太可能有效或为其他技术提供可靠的保护，实施可能会很困难，并且假阳性和检测错过的风险非常高。

#### <a name="CDN_CACHING_PROBLEMS"></a>如果我在使用CDN或缓存服务的同时使用CIDRAM，会发生问题吗？

也许。​这取决于相关服务的性质以及您如何使用它。​通常，如果您只缓存静态资产（例如，图像，CSS，等；任何通常不会随时间变化的东西），则不应该有任何问题。​但是，如果您要缓存的数据通常会在请求时动态生成，或者如果您正在缓存POST请求的结果，那么可能会有问题（这基本上会使您的网站及其环境成为强制静态，并且CIDRAM不太可能在强制静态环境中提供任何有意义的好处）。​CIDRAM也可能有特定的配置要求，具体取决于您使用的CDN或缓存服务（您需要确保为您正在使用的特定CDN或缓存服务正确配置CIDRAM）。​未能正确配置CIDRAM可能会导致严重假阳性和检测错过。

#### <a name="DDOS_ATTACKS"></a>CIDRAM会保护我的网站免受DDoS攻击吗？

总之：不，它不能。

更详细地说阐述：CIDRAM将有助于减少不需要的流量的可能造成的影响，为您的网站（从而降低带宽成本），为您的硬件（例如，您的服务器处理请求的能力），并可以帮助减少各种其他潜在的负面影响。​然而，为了理解这个问题，必须记住两件重要的事情。

首先，CIDRAM是一个PHP包，因此可以在安装PHP的机器上运行。​这意味着CIDRAM只能在服务器收到请求后才能看到并阻止请求。​其次，有效的DDoS缓解应该在请求到达DDoS攻击所针对的服务器之前对其进行过滤。​理想情况下，DDoS攻击应该在能够首先到达目标服务器之前通过能够丢弃或重新路由与攻击相关的流量的解决方案来检测和缓解。

这可以使用专用的内部部署硬件解决方案，基于云的解决方案，如专用的DDoS缓解服务，通过耐DDoS网络路由域名的DNS，基于云的过滤，或者它们的一些组合实施。​无论如何，这个问题有点太复杂，不能仅仅用一到两个段落来解释，所以如果这是您想追求的主题，我会建议您做进一步的研究。​当DDoS攻击的本质被正确理解时，这个答案会更有意义。

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>当我通过更新页面启用或禁用模块或签名文件时，它会在配置中它们将按字母数字排序。​我可以改变他们排序的方式吗？

这个有可能。​如果您需要强制某些文件以特定顺序执行，您可以在列出配置指令的位置中的在他们的名字之前添加一些任意数据，并用冒号分隔。​当更新页面随后再次对文件进行排序时，这个添加的任意数据会影响排序顺序，因此导致它们按照您想要的顺序执行，并且不需要重命名它们。

例如，假设配置指令包含如下列出的文件：

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

如果您想首先执行`file3.php`，您可以在文件名前添加`aaa:`或类似：

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

然后，如果启用了新文件`file6.php`，当更新页面再次对它们进行排序时，它应该像这样结束：

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

当文件禁用时的情况是相同的。​相反，如果您希望文件最后执行，您可以在文件名前添加`zzz:`或类似。​在任何情况下，您都不需要重命名相关文件。

#### <a name="HOW_TO_USE_PDO"></a>“PDO DSN”是什么？如何能PDO与CIDRAM一起使用？

“PDO” 是 “[PHP Data Objects](https://www.php.net/manual/zh/intro.pdo.php)” 的首字母缩写（它的意思是“PHP数据对象”）。​它为PHP提供了一个接口，使其能够连接到各种PHP应用程序通常使用的某些数据库系统。

“DSN” 是 “[data source name](https://en.wikipedia.org/wiki/Data_source_name)” 的首字母缩写（它的意思是“数据源名称”）。​“PDO DSN”向PDO描述了它应如何连接到数据库。

CIDRAM可以将PDO用于缓存。​为了使其正常工作，您需要相应地配置CIDRAM，从而启用PDO，需要为CIDRAM创建一个新数据库以供使用（如果您尚未想到要供CIDRAM使用的数据库），并需要按照以下结构在数据库中创建一个新表。

当数据库连接成功时，但是必要的表不存在，表自动创建将尝试。​但是，此行为尚未经过广泛测试，因此无法保证成功。

当然，这仅在您确实希望CIDRAM使用PDO时适用。​如果您对CIDRAM使用平面文件缓存（按照其默认配置）或提供的任何其他各种缓存选项感到足够满意，则无需费心设置数据库，数据库表，等等。

下面描述的结构使用“cidram”作为其数据库名称，但是您可以使用任何想要的数据库名称，只要在DSN配置中名称被复制。

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

CIDRAM的`pdo_dsn`应配置如下。

```
取决于所使用的数据库驱动程序......
├─4d （警告：实验性，未经测试，不建议！）
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └要查找数据库的主机。
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └要使用的数据库的名称。
│                │              │
│                │              └连接的主机端口号。
│                │
│                └要查找数据库的主机。
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └要使用的数据库的名称。
│    │          │
│    │          └要查找数据库的主机。
│    │
│    └可能的值： “mssql”， “sybase”， “dblib”。
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├可以是本地数据库文件的路径。
│                    │
│                    ├可以连接主机和端口号。
│                    │
│                    └如果要使用此功能，请参阅Firebird文档。
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └要连接的在目录中数据库。
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └要连接的在目录中数据库。
├─mysql （最推荐！）
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └连接的主机端口号。
│                 │            │
│                 │            └要查找数据库的主机。
│                 │
│                 └要使用的数据库的名称。
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├可以参考特定的在目录中数据库。
│               │
│               ├可以连接主机和端口号。
│               │
│               └如果要使用此功能，请参阅Oracle文档。
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├可以参考特定的在目录中数据库。
│         │
│         ├可以连接主机和端口号。
│         │
│         └如果要使用此功能，请参阅ODBC/DB2文档。
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └要使用的数据库的名称。
│               │              │
│               │              └连接的主机端口号。
│               │
│               └要查找数据库的主机。
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └要使用的本地数据库文件的路径。
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └要使用的数据库的名称。
                   │         │
                   │         └连接的主机端口号。
                   │
                   └要查找数据库的主机。
```

如果不确定如何构造DSN，请尝试先查看它是否按原样工作，而不进行任何更改。

请注意， `pdo_username` 和 `pdo_password` 应与您为数据库选择的用户名和密码相同。

#### <a name="BLOCK_CRON"></a>CIDRAM正在阻止cronjobs。​如何解决这个问题？

如果您为了cronjobs的目的使用专用文件，如果在普通用户请求期间不需要调用它（即，在cronjobs上下文之外），解决此问题的最直接方法是在cronjobs期间不要执行CIDRAM（即，不要将CIDRAM链接到负责处理cronjobs的文件）。

或者，如果那不可能，但是您的cron服务器的IP地址相对一致且可预测，您可以尝试将cron服务器的IP地址列入白名单，通过在自定义签名文件中为其创建白名单签名，或通过创建辅助规则为其。​如果您的cron服务器的IP地址定期旋转并且不是特别可预测，但仍然来自同一特定网络，您可以尝试在`ignore.dat`文件中列出负责阻止该签名的签名章节的名称。

如果您尝试了所有这些想法，但没有一个对您有用，或者如果您需要帮助弄清楚如何做，您可以在CIDRAM的issues页面上创建新issue，以寻求帮助。

---


### 9. <a name="SECTION9"></a>法律信息

#### 9.0 章节前言

本文档章节描述了有关该软件包的使用和实施的可能法律考虑事项，并提供一些基本的相关信息。​这对于一些用户来说可能很重要，作为确保遵守其运营所在国家可能存在的任何法律要求的一种手段。​一些用户可能需要根据这些信息调整他们的网站政策。

首先，请认识到我（软件包作者）不是律师或合格的法律专业人员。​因此，我无法合法提供法律建议。​此外，在某些情况下，不同国家和地区的具体法律要求可能会有所不同。​这些不同的法律要求有时可能会相互矛盾​（例如：支持[隐私权](https://zh.wikipedia.org/wiki/%E9%9A%90%E7%A7%81%E6%9D%83)和[被遺忘權](https://zh.wikipedia.org/wiki/%E8%A2%AB%E9%81%BA%E5%BF%98%E6%AC%8A)的国家，与支持扩展数据保留的国家相比）。​还要考虑到对软件包的访问不限于特定的国家或辖区，因此，软件包用户群很可能在地理上多样化。​这些观点认为，我无法说明在所有方面对所有用户“符合法律”意味着什么。​不过，我希望这里的信息能够帮助您自己决定您必须做些什么为了在软件包的上下文中符合法律。​如果您对此处的信息有任何疑问或担忧，或者您需要从法律角度提供更多帮助和建议，我会建议咨询合格的法律专业人员。

#### 9.1 法律责任

此软件包不提供任何担保（这已由包许可证提及）。​这包括（但不限于）所有责任范围。​为了您的方便，该软件包已提供给您。​希望它会有用，它会为您带来一些好处。​但是，使用或实施该软件包是您自己的选择。​您不是被迫使用或实施该软件包，但是当您这样做时，您需要对该决定负责。​我，和其他软件包贡献者，对于您的决定的后果不承担法律责任，无论是直接的，间接的，暗示的，还是其他方式。

#### 9.2 第三方

取决于其确切的配置和实施，在某些情况下，该软件包可能与第三方进行通信和共享信息。​在某些情况下，某些辖区可能会将此信息定义为“[个人身份信息](https://zh.wikipedia.org/wiki/%E5%80%8B%E4%BA%BA%E5%8F%AF%E8%AD%98%E5%88%A5%E8%B3%87%E8%A8%8A)”（PII）。

这些信息如何被这些第三方使用，是受这些第三方制定的各种政策的约束，并且超出了本文档的范围。​但是，在所有这些情况下，与这些第三方共享信息可能被禁用。​在所有这些情况下，如果您选择启用它，则有责任研究您可能遇到的任何问题（如果您担心这些第三方的隐私，安全，和PII使用情况）。​如果存在任何疑问，或者您对PII方面的这些第三方的行为不满意，最好禁用与这些第三方分享的所有信息。

为了透明的目的，共享信息的类型，以及与谁共享，如下所述。

##### 9.2.0 主机名查找

如果您使用任何旨在与主机名配合使用的功能或模块（例如，​“坏主机阻塞模块”，​“tor project exit nodes block module”，​“搜索引擎验证”），​CIDRAM需要能够以某种获得入站请求的主机名。​通常，它通过请求来自DNS服务器的入站请求的IP地址的主机名来执行此操作，或者通过安装CIDRAM的系统提供的功能请求信息（这通常被称为“主机名查找”）。​默认定义的DNS服务器属于[Google DNS](https://dns.google.com/)服务（但可以通过配置轻松更改）。​与之交流的确切服务是可配置的，并取决于您如何配置软件包。​在使用安装CIDRAM的系统提供的功能的情况下，您需要联系您的系统管理员以确定哪些为主机名查找的路由使用。​通过避免受影响的模块或根据您的需要修改软件包配置，可以防止CIDRAM中的主机名查找。

*相关配置指令：*
- `general` -> `allow_gethostbyaddr_lookup`
- `general` -> `default_dns`
- `general` -> `force_hostname_lookup`
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.1 搜索引擎验证和社交媒体验证

当启用搜索引擎验证时，CIDRAM尝试执行“正向DNS查找”以验证声称源自搜索引擎的请求是否真实。​同样，当启用社交媒体验证时，CIDRAM对为社交媒体请求做同样的事情。​为此，它使用[Google DNS](https://dns.google.com/)服务尝试从这些入站请求的主机名解析IP地址（在这个过程中，这些入站请求的主机名与服务共享）。

*相关配置指令：*
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.2 CAPTCHA

CIDRAM支持reCAPTCHA和hCAPTCHA。​他们需要API密钥才能正常工作。​默认情况下禁用，但它们可以通过配置所需的API密钥启用。​在启用的情况下，在服务与CIDRAM或用户的浏览器之间可能会发生通信。​这可能涉及通信信息，例如用户的IP地址，用户代理，操作系统，以及可用于请求的其他详细信息。

##### 9.2.3 STOP FORUM SPAM 【停止论坛垃圾邮件】

[Stop Forum Spam](https://www.stopforumspam.com/)是一个辉煌的，免费提供的服务，可以帮助保护论坛，博客，和网站免受垃圾邮件制造者。​它提供了一个已知垃圾邮件发送者的数据库，以及一个可用来检查数据库中是否列出IP地址，用户名或电子邮件地址的API。

CIDRAM提供了一个可选模块，它使用API来检查入站请求的IP地址是否属于可疑垃圾邮件发送者。​如果安装并激活模块时候，则可以根据模块的配置和预期用途将用户的IP地址与服务共享。

##### 9.2.4 ABUSEIPDB

CIDRAM提供了一个可选模块，用于使用[AbuseIPDB](https://www.abuseipdb.com/) API阻止滥用的IP地址。​如果安装并激活模块时候，则可以根据模块的配置和预期用途将用户的IP地址与服务共享。

##### 9.2.5 BGPVIEW

CIDRAM提供了一个可选模块，以使用[BGPView](https://bgpview.io/)执行ASN和国家代码查找。​提供了根据其ASN或来源国家阻止或将在白名单上放请求的功能。​如果安装并激活模块时候，则可以根据模块的配置和预期用途将用户的IP地址与服务共享。

##### 9.2.6 PROJECT HONEYPOT

CIDRAM提供了一个可选模块，用于使用[Project Honeypot](https://www.projecthoneypot.org/) API阻止滥用的IP地址。​如果安装并激活模块时候，则可以根据模块的配置和预期用途将用户的IP地址与服务共享。

#### 9.3 日志记录

由于多种原因，日志记录是CIDRAM的重要组成部分。​当未记录导致它们的阻止事件时，可能难以诊断和解决假阳性。​当未记录阻止事件时，可能很难确定CIDRAM在某些情况下的表现如何，而且可能很难确定其不足之处，以及可能需要更改哪些配置或签名，以使其继续按预期运行。​无论如何，一些用户可能不想要记录，并且它仍然是完全可选的。​在CIDRAM中，默认情况下日志记录是禁用。​要启用它，必须相应地配置CIDRAM。

另外，如果日志记录在法律上是允许的，并且在法律允许的范围内（例如，可记录的信息类型，多长时间，在什么情况下），可以变化，具体取决于管辖区域和CIDRAM的实施上下文（例如，如果您是个人或公司实体经营，如果您在商业或非商业基础上运营，等等）。​因此，仔细阅读本节可能对您有用。

CIDRAM可以执行多种类型的日志记录。​不同类型的日志记录涉及不同类型的信息，出于各种原因。

##### 9.3.0 阻止事件

CIDRAM可以执行的主要日志记录类型与“阻止事件”有关。​当CIDRAM阻止请求时会发生这种日志记录类型，并且可以以三种不同的格式提供：
- 人类可读的日志文件。
- Apache风格的日志文件。
- 序列化日志文件。

记录到人类可读日志文件的阻止事件通常看起来像这样（作为示例）：

```
ID： 1234
脚本版本： CIDRAM v1.6.0
日期/时间： Day, dd Mon 20xx hh:ii:ss +0000
IP地址： x.x.x.x
主机名： dns.hostname.tld
签名计数： 1
签名参考： x.x.x.x/xx
为什么被阻止： 云服务 ("网络名字", Lxx:Fx, [XX])!
用户代理： Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
重建URI： https://your-site.tld/index.php
CAPTCHA状态： 打开。
```

记录到Apache样式的日志文件中的同一阻止事件看起来像这样：

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

阻止事件记录通常包括以下信息：
- 阻止事件的ID号码。
- 目前正在使用的CIDRAM版本。
- 阻止事件发生的日期和时间。
- 被阻止请求的IP地址。
- 被阻止请求的IP地址的主机名（如果可用）。
- 请求触发的签名数。
- 触发的签名引用。
- 引用阻止事件的原因和一些基本的相关调试信息。
- 被阻止请求的用户代理（即，请求实体如何向请求标识自己）。
- 重建最初请求的资源的标识符。
- 当前请求的CAPTCHA状态（相关时）。

*负责此类日志记录的配置指令，适用于以下三种格式中的每一种：*
- `logging` -> `apache_style_log`
- `logging` -> `serialised_log`
- `logging` -> `standard_log`

当这些指令保留为空时，这种类型的日志记录将保持禁用状态。

##### 9.3.1 CAPTCHA日志记录

此类日志记录特定于CAPTCHA实例，仅在用户尝试完成CAPTCHA实例时才会发生。

CAPTCHA日志条目包含尝试完成CAPTCHA实例的用户的IP地址，尝试发生的日期和时间以及CAPTCHA状态。​CAPTCHA日志条目通常看起来像这样（作为示例）：

```
IP地址：x.x.x.x - Date/Time: Day, dd Mon 20xx hh:ii:ss +0000 - CAPTCHA状态：成功！
```

*负责CAPTCHA日志记录的配置指令是：*
- `hcaptcha` -> `hcaptcha_log`
- `recaptcha` -> `recaptcha_log`

##### 9.3.2 前端日志记录

此类日志记录涉及前端登录尝试，仅在用户尝试登录前端时才会发生（假设启用了前端访问）。

前端日志条目包含尝试登录的用户的IP地址，尝试发生的日期和时间以及的结果（登录成功或失败）。​前端日志条目通常看起来像这样（作为示例）：

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - 已登录。
```

*负责前端日志记录的配置指令是：*
- `frontend` -> `frontend_log`

##### 9.3.3 日志轮换

您可能希望在一段时间后清除日志，或者可能被要求依法执行（即，您在法律上允许保留日志的时间可能受法律限制）。​您可以通过在程序包配置指定的日志文件名中包含日期/时间标记（例如，`{yyyy}-{mm}-{dd}.log`），​然后启用日志轮换来实现此目的（日志轮换允许您在超出指定限制时对日志文件执行某些操作）。

例如：如果法律要求我在30天后删除日志，我可以在我的日志文件的名称中指定`{dd}.log`（`{dd}`代表天），将`log_rotation_limit`的值设置为30，并将`log_rotation_action`的值设置为`Delete`。

相反，如果您需要长时间保留日志，你可以选择完全不使用日志轮换，或者你可以将`log_rotation_action`的值设置为`Archive`，以压缩日志文件，从而减少它们占用的磁盘空间总量。

*相关配置指令：*
- `logging` -> `log_rotation_action`
- `logging` -> `log_rotation_limit`

##### 9.3.4 日志截断

如果这是您想要做的事情，也可以在超过特定大小时截断个别日志文件。

*相关配置指令：*
- `logging` -> `truncate`

##### 9.3.5 IP地址“PSEUDONYMISATION”

首先，如果您不熟悉这个术语，“pseudonymisation”是指处理个人数据，使其不能在没有补充信息的情况下被识别为属于任何特定的“数据主体”，并规定这些补充信息分开保存，采取技术和组织措施以确保个人数据不能被识别给任何自然人。

以下资源可以帮助更详细地解释它：
- [[trust-hub.com] What is pseudonymisation?](https://www.trust-hub.com/news/what-is-pseudonymisation/)
- [[Wikipedia] Pseudonymization](https://en.wikipedia.org/wiki/Pseudonymization)

在某些情况下，您可能在法律上要求对收集，处理，或存储的任何PII进行“pseudonymise”或“anonymise”。​虽然这个概念已经存在了相当长的一段时间，但GDPR/DSGVO提到，并特别鼓励“pseudonymisation”。

当记录它们时，CIDRAM可以对IP地址进行pseudonymise，如果这是您想做的事情。​当这个情况发生时，IPv4地址的最后八位字节，以及IPv6地址的第二部分之后的所有内容，将由“x”表示（有效地将IPv4地址四舍五入到它的第24个子网因素的初始地址，和将IPv6地址四舍五入到它的第32个子网因素的初始地址）。

*注意：CIDRAM的IP地址pseudonymisation过程不会影响CIDRAM的IP跟踪功能。​如果这对您来说是个问题，最好完全禁用IP跟踪。*

*相关配置指令：*
- `legal` -> `pseudonymise_ip_addresses`

##### 9.3.6 省略日志信息

如果要防止完全记录特定类型的信息，也可以这样做。​在配置页面，请参考`fields`配置指令来控制哪些字段出现在日志条目和“拒绝访问”页面上。

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

*注意：当完全从日志中省略IP地址时，没有理由对IP地址进行pseudonymise。*

*相关配置指令：*
- `general` -> `fields`

##### 9.3.7 统计

CIDRAM可选择跟踪统计信息，例如自特定时间以来发生的阻止事件或CAPTCHA实例的总数。​默认情况下此功能是禁用，但可以通过程序包配置启用此功能。​此功能仅跟踪发生的事件总数，不包括有关特定事件的任何信息（因此，不应被视为PII）。

*相关配置指令：*
- `general` -> `statistics`

##### 9.3.8 加密

CIDRAM不[加密](https://zh.wikipedia.org/wiki/%E5%8A%A0%E5%AF%86)其缓存或任何日志信息。​可能会在将来引入缓存和日志加密，但目前没有任何具体的计划。​如果您担心未经授权的第三方获取可能包含PII或敏感信息（如缓存或日志）的CIDRAM部分的访问权限，我建议不要将CIDRAM安装在可公开访问的位置（例如，在标准`public_html`或等效目录之外【可用于大多数标准网络服务器】安装CIDRAM），​也我建议对安装目录强制执行适当的限制权限（特别是对于vault目录）。​如果这还不足以解决您的疑虑，应该配置CIDRAM为不会首先收集或记录引起您关注的信息类型（例如，通过禁用日志记录）。

#### 9.4 COOKIE

CIDRAM在其代码库中的两个点设置[cookie](https://zh.wikipedia.org/wiki/Cookie)。​首先，当用户成功完成CAPTCHA实例时（这假定`lockuser`设置为`true`），CIDRAM设置cookie，以便能够在后续请求中记住用户已经完成了CAPTCHA实例，这样就不需要不断要求用户在后续请求中完成CAPTCHA实例。​其次，当用户成功登录前端时，CIDRAM设置cookie以便能够在后续请求中的记住用户（即，cookie用于向登录会话验证用户身份）。

在这两种情况下，cookie警告显着显示（适用时），警告用户如果他们参与相关操作将设置cookie。 Cookie不会在代码库中的任何其他位置设置。

*注意：在某些司法管辖区中，“不可见的” CAPTCHA API可能与Cookie法律不兼容，任何受这些法律约束的网站都应该避免这个API。​选择改用其他提供的API，或完全禁用CAPTCHA，可能是更可取的选择。*

*相关配置指令：*
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 9.5 市场营销和广告

CIDRAM不收集或处理任何信息用于营销或广告目的，既不销售也不从任何收集或记录的信息中获利。​CIDRAM不是商业企业，也不涉及任何商业利益，因此做这些事情没有任何意义。​自项目开始以来就一直如此，今天仍然如此。​此外，做这些事情会对整个项目的精神和预期目的产生反作用，并且只要我继续维护项目，永远不会发生。

#### 9.6 隐私政策

在某些情况下，您可能需要依法在您网站的所有页面和部分上清楚地显示您的隐私政策链接。​这可能为了确保用户充分了解您的隐私惯例，收集的个人身份信息类型以及您打算如何使用它的是很重要。​为了能够在CIDRAM的“拒绝访问”页面上包含这样的链接，提供了配置指令来指定隐私策略的URL。

*注意：​强烈建议您的隐私政策页面不放在CIDRAM的保护之后。​如果CIDRAM保护您的隐私政策页面，并且被CIDRAM阻止的用户点击隐私政策的链接，他们将再次被阻止，并且无法看到您的隐私政策。​理想情况下，您应链接到您的隐私政策的静态副本，例如HTML页面或纯文本文件，该文件不受CIDRAM保护。*

*相关配置指令：*
- `legal` -> `privacy_policy`

#### 9.7 GDPR/DSGVO

“通用数据保护条例”（GDPR）是欧盟法规，自2018年5月25日起生效。​该法规的主要目标是向欧盟公民和居民提供有关其个人数据的控制权，并统一欧盟内有关隐私和个人数据的法规。

该法规包含有关处理任何欧盟“数据主体”（任何已识别或可识别的自然人）的“[个人身份信息](https://zh.wikipedia.org/wiki/%E5%80%8B%E4%BA%BA%E5%8F%AF%E8%AD%98%E5%88%A5%E8%B3%87%E8%A8%8A)”（PII）的具体规定。​为了符合条例，“企业”（按照法规的定义），和任何相关的系统和流程必须默认实现“隐私设计”，​必须使用尽可能高的隐私设置，​必须对任何存储或处理的信息实施必要的保护措施（数据的 pseudonymisation 或完整 anonymisation ），​必须明确无误地声明他们收集的数据类型，​他们如何处理数据，​出于何种原因，​他们保留多长时间，​以及他们是否与任何第三方分享这些数据，​与第三方共享的数据类型，​为什么，​等等。

只有按照条例有合法依据才能处理数据。​一般而言，这意味着为了在合法基础上处理数据主体的数据，必须遵守法律义务，或者仅在从数据主体获得明确，明智，明确的同意之后才进行处理。

因为条例的各个方面可能会及时演变，并为了避免过时信息的传播，从权威来源中学习可能会更好的，而不是简单地在包文档中包含相关信息（这个信息可能最终会过时）。

一些推荐的资源用于了解更多信息：
- [关于欧盟GDPR隐私合规，中国数字营销人不得不知的9大问题](http://www.adexchanger.cn/top_news/28813.html)
- [史上最严的隐私条例出台，2018年开始执行](https://zhuanlan.zhihu.com/p/20865602)
- [《欧盟数据保护条例》对中国企业的影响 —- 以阿里巴巴集团为例](https://spiegeler.com/%E3%80%8A%E6%AC%A7%E7%9B%9F%E6%95%B0%E6%8D%AE%E4%BF%9D%E6%8A%A4%E6%9D%A1%E4%BE%8B%E3%80%8B%E5%AF%B9%E4%B8%AD%E5%9B%BD%E4%BC%81%E4%B8%9A%E7%9A%84%E5%BD%B1%E5%93%8D-%E4%BB%A5%E9%98%BF%E9%87%8C/)
- [歐盟個人資料保護法 GDPR 即將上路！與電商賣家息息相關的 Google Analytics 資料保留政策，你瞭解了嗎？](https://shopline.hk/blog/google-analytics-gdpr/)
- [歐盟一般資料保護規範](https://zh.wikipedia.org/wiki/%E6%AD%90%E7%9B%9F%E4%B8%80%E8%88%AC%E8%B3%87%E6%96%99%E4%BF%9D%E8%AD%B7%E8%A6%8F%E7%AF%84)
- [REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679)

---


最后更新：2023年3月5日。
