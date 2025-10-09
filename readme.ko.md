## CIDRAM v4 설명서 (한국어).

### 목차
- 1. [서문](#user-content-SECTION1)
- 2. [설치 방법](#user-content-SECTION2)
- 3. [사용 방법](#user-content-SECTION3)
- 4. [프론트엔드 관리](#user-content-SECTION4)
- 5. [설정 옵션](#user-content-SECTION5)
- 6. [서명 형식](#user-content-SECTION6)
- 7. [알려진 호환성 문제](#user-content-SECTION7)
- 8. [자주 묻는 질문 (FAQ)](#user-content-SECTION8)
- 9. [법률 정보](#user-content-SECTION9)
- 10. [이전 주 버전에서 업그레이드](#user-content-SECTION10)

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### 1. <a name="SECTION1"></a>서문

CIDRAM (시도라무 클래스없는 도메인 간 라우팅 액세스 매니저; "Classless Inter-Domain Routing Access Manager")는 PHP 스크립트입니다. 웹 사이트를 보호하도록 설계되어 IP 주소 (원치 않는 트래픽이있는 소스로 간주합니다)에서 전송 요청을 차단하여 (인간 이외의 액세스 엔드 포인트 클라우드 서비스 스팸봇 스크레이퍼 등). IP 주소의 수 CIDR을 계산하여 CIDR은 시그니처 파일과 비교할 수 있습니다 (이 서명 파일은 불필요한 IP 주소에 해당하는 CIDR의 목록이 포함되어 있습니다); 일치가 발견되면 요청이 차단됩니다.

*(참조하십시오 : ["CIDR"이란 무엇입니까?](#user-content-WHAT_IS_A_CIDR)).*

[CIDRAM](https://cidram.github.io/) COPYRIGHT 2016 and beyond GNU/GPLv2 by [Caleb M (Maikuolan)](https://github.com/Maikuolan).

이 스크립트는 자유 소프트웨어입니다; 당신은 자유 소프트웨어 재단이 발표한 GNU 일반 공중 사용 허가서 버전 2 또는 그 이후 버전에 따라 이 스크립트를 재배포하거나 수정할 수 있습니다. 이 스크립트가 유용하게 사용되기를 바라지만 상용으로 사용되거나 특정 목적에 적합할 것이라는 것을 묵시적인 보증을 포함한 그 어떠한 형태로도 보증하지 않습니다. 자세한 내용은 `LICENSE.txt` 파일 또는 다음 링크에서 확인할 수 있는 GNU 일반 공중 사용 허가서를 참조하시기 바랍니다 :
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

CIDRAM은 여기에서 무료로 다운로드할 수 있습니다 :
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM).

이 문서와 다양한 번역본은 여기에서 확인할 수 있습니다 :
- [GitHub](https://github.com/CIDRAM/Docs).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram-docs).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM-Docs).

---


### 2. <a name="SECTION2"></a>설치 방법

#### 2.0 수동 설치

먼저, 작업할 CIDRAM의 새 복사본이 필요합니다. [CIDRAM/CIDRAM](https://github.com/CIDRAM/CIDRAM) 저장소에서 최신 버전의 CIDRAM 아카이브를 다운로드할 수 있습니다. 구체적으로 말하면, "vault" 디렉터리의 새 복사본이 필요합니다 ("vault" 디렉터리와 그 내용을 제외한 아카이브의 모든 항목을 안전하게 삭제하거나 무시할 수 있습니다).

v3 이전에는, CIDRAM 프런트 엔드에 액세스할 수 있으려면 공용 루트 내의 어딘가에 CIDRAM을 설치해야 했습니다. 그러나, v3부 터는 그럴 필요가 없습니다. 보안을 최대화하고 CIDRAM 및 해당 파일에 대한 무단 액세스를 방지하려면, 대신, 공용 루트 *외부에* CIDRAM을 설치하는 것이 좋습니다. PHP가 액세스할 수 있는 한, 위치가 안전한 한, 당신이 위치에 만족하는 한, CIDRAM을 어디에나 설치할 수 있습니다. 디렉터리 이름을 "vault"로 유지하는 것은 더 이상 필요하지 않으므로, 원하는 이름으로 이름을 변경할 수 있습니다 (그러나, 편의를 위해, 문서에서는 계속 이를 "vault" 디렉터리로 참조합니다).

준비되면, "vault" 디렉터리를 선택한 위치에 업로드하고, PHP가 디렉터리에 쓸 수 있도록 하는 데 필요한 권한이 있는지 확인하십시오 (시스템에 따라, 아무것도 할 필요가 없거나, CHMOD 755를 디렉터리로 설정해야 할 수도 있습니다. 또는, 755에 문제가 있는 경우, 777을 시도할 수, 있지만 777은 보안이 취약하므로 권장하지 않습니다).

다음으로, CIDRAM이 코드 베이스 또는 CMS를 보호할 수 있으려면 "진입점"을 만들어야 합니다. 이러한 진입점은 다음 세 가지로 구성됩니다 :

1. 코드 베이스 또는 CMS의 적절한 지점에 "loader.php" 파일을 포함합니다.
2. CIDRAM core의 인스턴스화.
3. "protect" 메서드를 호출합니다.

간단한 예 :

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

Apache 웹 서버를 사용 중이고 `php.ini`에 액세스할 수 있는 경우, PHP 요청이 만들어질 때마다 CIDRAM을 실행하기 위해, `auto_prepend_file` 지시문을 사용할 수 있습니다. 이러면, 진입점을 생성하는 데 가장 적절한 위치는 자체 파일이며, `auto_prepend_file` 지시문에서 해당 파일을 인용합니다.

예 :

`auto_prepend_file = "/path/to/your/entrypoint.php"`

또는 `.htaccess` 파일에서 :

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

다른 경우에, 진입점을 생성하는 가장 적절한 위치는 웹사이트의 모든 페이지에 대해 항상 로드되도록 코드 베이스 또는 CMS 내에서 가능한 한 초기 하는 것입니다. 코드 베이스가 "bootstrap"을 사용한다면, "bootstrap" 파일의 시작 부분이 좋은 선택이 될 것입니다. 코드 베이스에 데이터베이스 연결을 담당하는 파일이 있는 경우, 해당 파일도 좋은 선택이 될 것입니다.

#### 2.1 COMPOSER를 사용하여 설치한다

[CIDRAM는 Packagist에 등록되어 있습니다](https://packagist.org/packages/cidram/cidram). Composer를 익숙한 경우 Composer를 사용하여 CIDRAM를 설치할 수 있습니다.

`composer require cidram/cidram`

#### 2.2 WORDPRESS 위해 설치한다

[CIDRAM은 WordPress 플러그인 데이터베이스에 플러그인으로 등록되어 있습니다](https://wordpress.org/plugins/cidram/). 플러그인 대시 보드에서 CIDRAM를 직접 설치할 수 있습니다. 다른 플러그인과 같은 방법으로 설치할 수 (추가 절차는 필요하지 않습니다).

*경고 : 플러그인 대시 보드를 통해 CIDRAM를 업데이트하면 클린 설치가 이루어집니다. 설치를 사용자 정의한 경우 (당신의 설정을 변경 한 모듈을 설치 한 등) 이러한 정의는 플러그인 대시 보드를 통해 업데이트하면 손실됩니다! 로그 파일도 손실됩니다! 로그 파일과 문화를 유지하려면 CIDRAM 프론트 엔드 업 데이트 페이지에 업데이트합니다.*

#### 2.3 구성 및 사용자 정의

필요에 따라 조정할 수 있도록 새 설치의 구성을 검토하는 것이 좋습니다. 필요에 가장 잘 맞는 설치를 위해 추가 모듈, 서명 파일을 설치하거나, 보조 규칙을 생성하거나, 기타 사용자 정의를 구현할 수도 있습니다. 이러한 작업을 수행하려면 프론트 엔드를 사용하는 것이 좋습니다.

---


### 3. <a name="SECTION3"></a>사용 방법

CIDRAM은 자동으로 원치 않는 요청을 차단해야합니다; 지원이 필요하지 않습니다 (설치 제외).

당신의 설정 파일을 수정하여 구성 설정을 사용자 정의 할 수 있습니다. 당신의 서명 파일을 변경하여 CIDRs이 차단 된 변경 할 수 있습니다.

오진 (거짓 양성)과 신종 의심스러운 것으로 발생, 관한 것에 대해서는 무엇이든 알려주세요. *(참조하십시오 : ["거짓 양성"는 무엇입니까?](#user-content-WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM은 수동으로 또는 프런트 엔드를 통해 업데이트 할 수 있습니다. CIDRAM은 원래 이러한 수단을 통해 설치된 경우 Composer 또는 WordPress를 통해 업데이트 할 수도 있습니다.

---


### 4. <a name="SECTION4"></a>프론트엔드 관리

#### 4.0 프론트 엔드는 무엇입니다.

프론트 엔드는 CIDRAM 설치 유지 관리 업데이트하기위한 편리하고 쉬운 방법을 제공합니다. 로그 페이지를 사용하여 로그 파일을 공유, 다운로드 할 수있는 구성 페이지에서 구성을 변경할 수 있습니다, 업데이트 페이지를 사용하여 구성 요소를 설치 및 제거 할 수 있습니다, 그리고 파일 관리자를 사용하여 vault에 파일을 업로드, 다운로드 및 변경할 수 있습니다.

#### 4.1 프론트 엔드를 액세스하는 방법.

이전과 마찬가지로, 프런트 엔드에 액세스하려면 진입점을 만들어야 합니다. 이러한 진입점은 다음 세 가지로 구성됩니다 :

1. 코드 베이스 또는 CMS의 적절한 지점에 "loader.php" 파일을 포함합니다.
2. CIDRAM front-end의 인스턴스화.
3. "view" 메서드를 호출합니다.

간단한 예 :

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

"FrontEnd" 클래스는 "Core" 클래스를 확장합니다. 즉, 잠재적으로 원하지 않는 트래픽이 프런트 엔드에 액세스하는 것을 차단하기 위해 "view" 메서드를 호출하기 전에 "protect" 메서드를 호출할 수 있습니다. 그렇게 하는 것은 전적으로 선택 사항입니다.

간단한 예 :

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

프런트 엔드에 대한 진입점을 만드는 데 가장 적절한 위치는 자체 전용 파일입니다. 이전과 달리, 진입점이 존재하는 특정 파일을 직접 요청해야만 프런트 엔드 진입점에 액세스할 수 있기를 원합니다. 따라서, 여기에서 `auto_prepend_file` 또는 `.htaccess`를 사용하고 싶지 않습니다.

프런트 엔드 진입점을 만든 후, 브라우저를 사용하여 액세스합니다. 로그인 페이지가 표시되어야 합니다. 로그인 페이지에서 기본 사용자 이름과 비밀번호 (admin/password)를 입력하고 로그인 버튼을 누릅니다.

주의 : 당신이 처음 로그인 한 후 프론트 엔드에 대한 무단 액세스를 방지하기 위해 신속하게 사용자 이름과 암호를 변경해야합니다! 이것은 매우 중요합니다, 왜냐하면 프론트 엔드에서 임의의 PHP 코드를 당신의 웹 사이트에 업로드 할 수 있기 때문입니다.

최적의 보안을 위해 모든 프런트 엔드 계정에 대해 2FA (이중 인증)을 사용하는 것이 좋습니다 (아래 제공된 지침).

#### 4.2 프론트 엔드 사용.

프론트 엔드의 각 페이지에는 목적에 대한 설명과 사용 방법에 대한 설명이 있습니다. 전체 설명이나 특별한 지원이 필요한 경우 지원에 문의하십시오. 또한 데모를 제공 할 YouTube에서 사용 가능한 동영상도 있습니다.

#### 4.3 2FA (이중 인증)

2FA를 사용하면 프런트 엔드를 더욱 안전하게 만들 수 있습니다. 2FA를 사용하는 계정에 로그인하면 해당 계정과 연결된 이메일 주소로 이메일이 전송됩니다. 이 이메일에는 "2FA 코드"가 포함되어 있습니다. 사용자는이 계정을 사용하여 로그인 할 수 있도록 사용자 이름과 비밀번호 외에도 사용자가 입력해야합니다. 즉, 해커 또는 잠재적 공격자가 해당 계정에 로그인 할 수 있도록 계정 암호로는 충분하지 않습니다. 세션과 관련된 2FA 코드를 수신하고 활용하려면 해당 계정과 연결된 이메일 주소에 대한 액세스 권한이 있어야합니다.

2FA를 사용하려면 프론트 엔드 업데이트 페이지를 사용하여 PHPMailer 구성 요소를 설치하십시오. CIDRAM은 PHPMailer를 사용하여 이메일을 전송합니다.

PHPMailer를 설치 한 후 CIDRAM 구성 페이지 또는 구성 파일을 통해 PHPMailer의 구성 지시문을 채워야합니다. 이러한 구성 지시문에 대한 자세한 내용은이 설명서의 구성 섹션에 포함되어 있습니다. PHPMailer 설정 지시어를 채운 후에는 `enable_two_factor`를 `true`로 설정하십시오. 이제 2FA가 활성화되어야합니다.

해당 계정으로 로그인 할 때 2FA 코드를 보낼 위치를 CIDRAM이 알 수 있도록 이메일 주소를 계정과 연결해야합니다. 전자 메일 주소를 계정의 사용자 이름 (예 : `foo@bar.tld`)으로 사용하거나 정상적으로 전자 메일을 보낼 때와 동일한 방법 (예 : `Foo Bar <foo@bar.tld>`)으로 사용자 이름의 일부로 전자 메일 주소를 포함하십시오.

노트 : 무단 액세스로부터 vault보호는 특히 중요합니다 (예 : 서버의 보안을 강화하고 공용 액세스 권한을 제한함으로써). vault에 저장되어있는 구성 파일에 대한 무단 액세스로 인해 SMTP 사용자 이름과 암호를 비롯한 아웃 바운드 SMTP 설정이 노출 될 수 있습니다. 2FA를 사용하기 전에 vault가 적절하게 보안되어 있는지 확인해야합니다. 이 작업을 수행 할 수 없으면 노출 된 SMTP 설정과 관련된 위험을 줄이기 위해 이러한 용도로 전용 된 새 전자 메일 계정을 만들어야합니다.

---


### 5. <a name="SECTION5"></a>설정 옵션

다음은 `config.yml`설정 파일에있는 변수 및 그 목적과 기능의 목록입니다.

```
구성 (v4)
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

#### "general" (카테고리)
일반 설정 (다른 카테고리에 속하지 않는 설정).

##### "stages" `[string]`
- 실행 체인의 단계에 대한 제어 (활성화 여부, 오류 기록 여부, 등등).

```
stages───[이 단계를 활성화하시겠습니까?]─[이 단계에서 생성된 오류를 기록하시겠습니까?]─[이 단계에서 생성된 위반은 IP 추적에 포함되어야 합니까?]
├─BanCheck ("금지되었는지 확인하는")
├─Tests ("서명 파일 테스트 실행")
├─Modules ("모듈 실행")
├─SearchEngineVerification ("검색 엔진 검증 실행")
├─SocialMediaVerification ("소셜 미디어 검증 실행")
├─OtherVerification ("기타 검증 실행")
├─Aux ("보조 규칙 실행")
├─Tracking ("IP 추적 실행")
├─RL ("속도 제한 실행")
├─CAPTCHA ("보안문자 배포 (차단된 요청)")
├─Reporting ("보고 실행")
├─Statistics ("통계 업데이트")
├─Webhooks ("웹훅 실행")
├─TriggerNotifications ("이메일 트리거 알림 대기열 처리")
├─PrepareFields ("출력 및 로그용 필드 준비")
├─Output ("출력 생성 (차단된 요청)")
├─WriteLogs ("로그에 쓰기 (차단된 요청)")
├─Terminate ("요청 종료 (차단된 요청)")
├─AuxRedirect ("보조 규칙에 따라 리디렉션")
└─NonBlockedCAPTCHA ("보안문자 배포 (차단되지 않은 요청)")
```

##### "fields" `[string]`
- 블록 이벤트 중 필드 제어 (요청이 차단되었을 때).

```
fields───[이 필드가 로그 항목에 나타나야 합니까?]─[이 필드가 "액세스 거부" 페이지에 나타나야 합니까?]─[이 필드가 비어 있으면 생략하시겠습니까?]
├─ID ("신분증")
├─ScriptIdent ("스크립트 버전")
├─DateTime ("일·월·년·시간")
├─IPAddr ("IP 주소")
├─IPAddrResolved ("IP 주소 (해결됨)")
├─Query ("쿼리")
├─Referrer ("추천자")
├─UA ("사용자 에이전트")
├─UALC ("사용자 에이전트 (소문자)")
├─SignatureCount ("서명수")
├─Signatures ("서명 참조")
├─WhyReason ("왜 차단이 되셨나요")
├─ReasonMessage ("왜 차단이 되셨나요 (상세한)")
├─rURI ("URI 재구성 된")
├─Infractions ("위반")
├─ASNLookup ("** ASN 조회")
├─CCLookup ("** 국가 코드 조회")
├─Verified ("확인 된 신원")
├─Expired ("만료됨")
├─Ignored ("무시 됨")
├─Request_Method ("요청 방법")
├─Protocol ("프로토콜")
├─SEC_CH_UA_PLATFORM ("!! SEC_CH_UA_PLATFORM")
├─SEC_CH_UA_MOBILE ("!! SEC_CH_UA_MOBILE")
├─SEC_CH_UA ("!! SEC_CH_UA")
├─Hostname ("호스트 이름")
├─CAPTCHA ("CAPTCHA의 상태")
├─Inspection ("* 조건 검사")
└─ClientL10NAccepted ("언어 해상도")
```

* 보조 규칙 디버깅 전용입니다. 차단된 사용자에게는 표시되지 않습니다.

** ASN 조회 기능이 필요합니다 (예 : IP-API 또는 BGPView 모듈을 통해).

!! 이는 낮은 엔트로피 클라이언트 힌트입니다. 클라이언트 힌트는 새로운 실험적 웹 기술이지만 아직 모든 브라우저와 주요 클라이언트에서 널리 지원되지는 않습니다. *보다 : <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA#browser_compatibility" dir="ltr" hreflang="en-US" rel="noopener noreferrer external">Sec-CH-UA - HTTP | MDN</a>.* 클라이언트 힌트는 핑거프린팅에 유용할 수 있지만 광범위하게 지원되지 않으므로 요청에 클라이언트 힌트가 있다고 가정하거나 의존해서는 안 됩니다 (즉, 부재를 기준으로 차단하는 것은 나쁜 생각입니다).

##### "timezone" `[string]`
- 사용할 시간대를 지정합니다 (예 : Africa/Cairo, America/New_York, Asia/Tokyo, Australia/Perth, Europe/Berlin, Pacific/Guam, 등등). PHP가 자동으로 처리하도록하려면, "SYSTEM"을 지정하십시오.

```
timezone
├─SYSTEM ("시스템 기본 시간대를 사용하십시오.")
├─UTC ("UTC")
└─…다른
```

##### "time_offset" `[int]`
- 시간대 오프셋 (분).

##### "time_format" `[string]`
- CIDRAM에서 사용되는 날짜 형식. 추가 옵션이 요청에 따라 추가 될 수 있습니다.

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
└─…다른
```

__*자리 표시자 – 설명 – 예시는 2024-04-30T18:27:49+08:00를 기준으로 합니다.*__<br />
`{yyyy}` – 연도 – 예 : 2024.<br />
`{yy}` – 약식 연도 – 예 : 24.<br />
`{Mon}` – 해당 월의 약칭(영문) – 예 : Apr.<br />
`{mm}` – 앞에 0이 붙는 달 – 예 : 04.<br />
`{m}` – 달 – 예 : 4.<br />
`{Day}` – 요일의 약칭(영문) – 예 : Tue.<br />
`{dd}` – 앞에 0이 붙은 해당 월의 일 – 예 : 30.<br />
`{d}` – 해당 월의 일 – 예 : 30.<br />
`{hh}` – 앞에 0이 붙은 시간(24시간제 사용) – 예 : 18.<br />
`{h}` – 시간(24시간제 사용) – 예 : 18.<br />
`{ii}` – 앞에 0이 붙는 분 – 예 : 27.<br />
`{i}` – 분 – 예 : 27.<br />
`{ss}` – 앞에 0이 붙은 초 – 예 : 49.<br />
`{s}` – 초 – 예 : 49.<br />
`{tz}` – 시간대(콜론 제외) – 예 : +0800.<br />
`{t:z}` – 시간대(콜론 포함) – 예 : +08:00.

##### "ipaddr" `[string]`
- 연결 요청의 IP 주소를 어디에서 찾을 것인가에 대해 (Cloudflare와 같은 서비스에 유용합니다). Default (기본 설정) = REMOTE_ADDR. 주의 : 당신이 무엇을하고 있는지 모르는 한이를 변경하지 마십시오.

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (기본값)")
└─…다른
```

또한보십시오 :
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### "http_response_header_code" `[int]`
- 요청을 차단할 때 CIDRAM이 전송해야하는 HTTP 상태 메시지는 무엇입니까?

```
http_response_header_code───[기본값]─[적법한]─[금지 된]
├─200 (200 OK): 가장 덜 강력하지만 가장 사용자 친화적입니다. 자동화된
│ 요청은 이 응답을 요청이 성공했다는 표시로 해석할
│ 가능성이 큽니다. 차단되지 않은 요청에 권장됩니다.
├─403 (403 Forbidden (금지)): 더 강력하지만, 사용자 친화성은 떨어집니다. 대부분의
│ 일반적인 상황에 권장됩니다.
├─410 (410 Gone (갔다)): 일부 브라우저는 차단 해제된 후에도 이 상태 메시지를
│ 캐시하고 후속 요청을 보내지 않기 때문에 가 양성을
│ 해결할 때 문제를 일으킬 수 있습니다. 어떤 상황에서는
│ 특정 종류의 트래픽에 대해 가장 선호될 수 있습니다.
├─418 (418 I'm a teapot (나는 찻주전자)): 만우절 농담을 참고하여 (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). 클라이언트, 로봇,
│ 브라우저, 등이 이해하지 못할 가능성이 매우 높습니다.
│ 오락과 편의를 위해 제공되지만, 일반적으로 권장되지
│ 않습니다.
├─451 (451 Unavailable For Legal Reasons (법적 이유로 사용할 수 없음)): 주로 법적 이유로 차단할 때 권장됩니다. 다른
│ 상황에서는 권장되지 않습니다.
└─503 (503 Service Unavailable (서비스 불가)): 가장 강력하지만 사용자 친화적이지 않습니다.
  공격받거나 매우 지속적인 원치 않는 트래픽을 처리할 때
  권장됩니다.
```

__1.__ "무음 모드"가 적용되면, `general➡silent_mode_response_header_code`에 의해 정의된 HTTP 상태 메시지가 사용됩니다 (이게 가장 높은 우선순위를 가집니다).

__2.__ 요청 엔터티가 위반 한도를 초과하여 차단된 경우, "금지 된"에 대한 HTTP 상태 메시지가 사용됩니다.

__3.__ 속도 제한으로 인해 차단된 경우, 429가 사용되고, 리소스 충돌로 인해 차단된 경우, `signatures➡conflict_response`로 정의된 HTTP 상태 메시지가 사용됩니다 (이 맥락에서 속도 제한과 리소스 충돌은 동등한 우선권을 갖습니다).

__4.__ "HTTP 상태 코드 재정의"를 설정하는 보조 규칙으로 인해 차단된 경우, 해당 HTTP 상태 코드 재정의가 사용됩니다.

__5.__ 법적 이유로 차단된 경우 (즉, "적법한"이라는 약어를 사용하는 사용자 정의 서명으로 인해 차단된 경우), "적법한"에 대한 HTTP 상태 메시지가 사용됩니다.

__6.__ 다른 모든 차단된 요청의 경우 "기본값"에 대한 HTTP 상태 메시지가 사용됩니다 (이게 가장 낮은 우선순위를 갖습니다).

##### "silent_mode" `[string]`
- "액세스 거부" 페이지를 표시하는 대신 CIDRAM는 차단 된 액세스 시도를 자동으로 리디렉션해야합니까? 그렇다면 리디렉션 위치를 지정합니다. 아니오의 경우이 변수를 비워 둡니다.

##### "silent_mode_response_header_code" `[int]`
- 차단된 액세스 시도를 자동으로 리디렉션할 때 CIDRAM이 전송해야하는 HTTP 상태 메시지는 무엇입니까?

```
silent_mode_response_header_code
├─301 (301 Moved Permanently (영구 이동)): 리디렉션이 영구적임을 클라이언트에 지시합니다.
│ 리디렉션 및 초기 요청의 요청 방법은 다를 수 있습니다.
├─302 (302 Found (임시 이동)): 리디렉션이 일시적임을 클라이언트에 지시합니다.
│ 리디렉션 및 초기 요청의 요청 방법은 다를 수 있습니다.
├─307 (307 Temporary Redirect (임시 리다이렉션)): 리디렉션이 일시적임을 클라이언트에 지시합니다.
│ 리디렉션 및 초기 요청의 요청 방법은 다를 수 없습니다.
└─308 (308 Permanent Redirect (영구 리다이렉션)): 리디렉션이 영구적임을 클라이언트에 지시합니다.
  리디렉션 및 초기 요청의 요청 방법은 다를 수 없습니다.
```

우리가 고객에게 지시하는 방법에 상관없이, 궁극적으로 고객이 선택하는 것을 제어할 수 없으며 고객이 우리의 지시를 존중할 것이라는 보장이 전혀 없다는 점을 기억하는 것이 중요합니다.

##### "lang" `[string]`
- CIDRAM의 기본 언어를 설정합니다.

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
- 가능할 때마다 HTTP_ACCEPT_LANGUAGE에 따라 현지화 하시겠습니까? True = 예 (Default / 기본값); False = 아니오.

##### "numbers" `[string]`
- 어떻게 숫자를 표시하는 것을 선호합니까? 가장 정확한 것으로 보이는 예제를 선택하십시오.

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
- 여기에 이메일 주소를 입력하고 사용자가 차단 된 경우 사용자에게 보낼 수 있습니다. 이것은 지원과 지원에 사용할 수 있습니다 (실수로 차단 된 경우 등). 경고 : 여기에 입력 된 전자 이메일 주소는 아마 스팸 로봇에 의해 취득됩니다. 여기에서 제공되는 전자 이메일 주소는 모든 일회용하는 것이 좋습니다 (예를 들어, 기본 개인 주소 또는 비즈니스 주소를 사용하지 않는 등).

##### "emailaddr_display_style" `[string]`
- 사용자에게 전자 메일 주소를 어떻게 표시 하시겠습니까?

```
emailaddr_display_style
├─default ("클릭 가능한 링크")
└─noclick ("클릭 할 수 없는 텍스트")
```

##### "default_dns" `[string]`
- 호스트 이름 검색에 사용하는 DNS (도메인 이름 시스템) 서버의 목록입니다. 주의 : 당신이 무엇을하고 있는지 모르는 한이를 변경하지 마십시오.

__자주하는 질문.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.ko.md#default_dns에-사용할-수있는-항목은-무엇입니까" hreflang="ko-KR">"default_dns"에 사용할 수있는 항목은 무엇입니까?</a>*

##### "default_algo" `[string]`
- 향후 모든 암호와 세션에 사용할 알고리즘을 정의합니다.

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### "statistics" `[string]`
- 추적할 통계 정보를 제어합니다.

```
statistics───[IPv4]─[IPv6]─[다른]
├─Blocked ("차단된 요청")
├─Banned ("금지된 요청")
├─Passed ("허용된 요청")
├─ReportOK ("외부 API에 보고된 요청 – 확인")
└─ReportFailed ("외부 API에 보고된 요청 – 실패했습니다")
```

참고 : 보조 규칙에 대한 통계를 추적할지 여부는 보조 규칙 페이지에서 제어할 수 있습니다.

##### "statistics_captchas" `[string]`
- CAPTCHA에 대해 추적할 통계 정보를 제어합니다.

```
statistics_captchas───[실패했습니다]─[성공했습니다]─[제공됨]
├─HCaptcha ("hCaptcha")
├─FriendlyCaptcha ("Friendly Captcha")
└─CloudflareTurnstile ("Cloudflare Turnstile")
```

참고 : 보조 규칙에 대한 통계를 추적할지 여부는 보조 규칙 페이지에서 제어할 수 있습니다.

##### "force_hostname_lookup" `[bool]`
- 호스트 이름 검색을 시행 하시겠습니까 (모든 요청)? True = 예; False = 아니오 (Default / 기본 설정). 호스트 이름 검색은 일반적으로 "필요에 따라"수행됩니다, 그러나 모든 요청에 대해 강제 될 수 있습니다. 이는 로그 파일에보다 자세한 정보를 제공하는 데 유용 할 수 있습니다, 그러나 또한 성능에 약간 부정적인 영향을 줄 수 있습니다.

##### "allow_gethostbyaddr_lookup" `[bool]`
- UDP를 사용할 수 없을 때 gethostbyaddr 검색을 허용 하시겠습니까? True = 예 (Default / 기본 설정); False = 아니오.

참고 : IPv6 조회는 일부 32비트 시스템에서 제대로 작동하지 않을 수 있습니다.

##### "disabled_channels" `[string]`
- 이것은 CIDRAM이 요청을 보낼 때 특정 채널을 사용하지 못하게하는 데 사용할 수 있습니다 (예를 들어, 업데이트 할 때, 구성 요소 메타 데이터를 가져올 때, 등등).

```
disabled_channels
├─GitHub ("<span class="origin us">US</span> GitHub")
├─BitBucket ("<span class="origin us">US</span> BitBucket")
├─Codeberg ("<span class="origin de">DE</span> Codeberg")
└─GoogleDNS ("<span class="origin us">US</span> GoogleDNS")
```

##### "request_proxy" `[string]`
- 아웃바운드 요청을 프록시를 통해 보내려면, 여기에 해당 프록시를 지정하세요. 그렇지 않은 경우, 이 항목을 비워 두십시오.

##### "request_proxyauth" `[string]`
- 프록시를 통해 아웃바운드 요청을 보내고 해당 프록시에 사용자 이름과 비밀번호가 필요한 경우, 여기에 해당 사용자 이름과 비밀번호를 지정하십시오 (예를 들어, `user:pass`). 그렇지 않은 경우, 이 항목을 비워 두십시오.

##### "default_timeout" `[int]`
- 외부 요청에 사용할 기본 제한 시간? Default (기본 설정) = 12 초.

##### "sensitive" `[string]`
- 민감한 페이지로 간주할 경로 목록입니다. 나열된 각 경로는 필요할 때 재구성된 URI에 관해 확인됩니다. 슬래시로 시작하는 경로는 리터럴로 처리되며 요청의 경로 구성 요소부터 일치합니다. 영숫자가 아닌 문자로 시작하고 동일한 문자(또는 동일한 문자와 선택적 "i" 플래그)로 끝나는 경로는 정규식으로 처리됩니다. 다른 종류의 경로는 리터럴로 취급되며 URI의 모든 부분에서 일치할 수 있습니다. 경로가 민감한 페이지로 간주하는지 여부는 일부 모듈의 작동 방식에 영향을 미칠 수 있지만 다른 것에는 영향을 미치지 않습니다.

##### "email_notification_address" `[string]`
- 이메일을 통해 CIDRAM으로부터 알림을 받기로 선택한 경우, 예를 들어 특정 보조 규칙이 트리거되는 경우, 여기서 해당 알림의 수신자 주소를 지정할 수 있습니다.

##### "email_notification_name" `[string]`
- 이메일을 통해 CIDRAM으로부터 알림을 받기로 선택한 경우, 예를 들어 특정 보조 규칙이 트리거되는 경우, 여기서 해당 알림의 수신자 이름을 지정할 수 있습니다.

##### "email_notification_when" `[string]`
- 생성된 후 알림을 보내는 시기.

```
email_notification_when
├─Immediately ("즉시.")
├─After24Hours ("24시간 후, 함께 묶음 (또는 수동으로 트리거되는 경우, 예를 들어, cron을 통해).")
└─ManuallyOnly ("수동으로 트리거되는 경우에만 (예를 들어, cron을 통해).")
```

#### "components" (카테고리)
CIDRAM에서 사용하는 구성 요소를 활성화 및 비활성화하기 위한 구성입니다. 일반적으로 업데이트 페이지에 의해 채워지지만, 세부 제어 및 업데이트 페이지에서 인식하지 못하는 사용자 지정 구성 요소를 위해 여기에서 관리할 수도 있습니다.

##### "ipv4" `[string]`
- IPv4 서명 파일.

##### "ipv6" `[string]`
- IPv6 서명 파일.

##### "modules" `[string]`
- 모듈.

##### "imports" `[string]`
- 수입품. 일반적으로 구성 요소의 구성 정보를 CIDRAM에 제공하는 데 사용됩니다.

##### "events" `[string]`
- 이벤트 핸들러. 일반적으로 CIDRAM이 내부적으로 작동하는 방식을 수정하거나 추가 기능을 제공하는 데 사용됩니다.

#### "logging" (카테고리)
로깅 관련 구성 (다른 카테고리에 적용되는 것을 제외).

##### "standard_log" `[string]`
- 액세스 시도 저지를 기록, 인간에 의해 읽기 가능. 파일 이름을 지정하십시오. 비활성화하려면 비워 둡니다.

유용한 팁 : 시간 형식 자리 표시자를 사용하여 로그 파일 이름에 날짜/시간 정보를 첨부할 수 있습니다. 사용 가능한 시간 형식 자리 표시자는 <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>에 표시됩니다.

##### "apache_style_log" `[string]`
- 액세스 시도 저지를 기록, Apache 스타일. 파일 이름을 지정하십시오. 비활성화하려면 비워 둡니다.

유용한 팁 : 시간 형식 자리 표시자를 사용하여 로그 파일 이름에 날짜/시간 정보를 첨부할 수 있습니다. 사용 가능한 시간 형식 자리 표시자는 <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>에 표시됩니다.

##### "serialised_log" `[string]`
- 액세스 시도 저지를 기록 직렬화되었습니다. 파일 이름을 지정하십시오. 비활성화하려면 비워 둡니다.

유용한 팁 : 시간 형식 자리 표시자를 사용하여 로그 파일 이름에 날짜/시간 정보를 첨부할 수 있습니다. 사용 가능한 시간 형식 자리 표시자는 <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>에 표시됩니다.

##### "error_log" `[string]`
- 치명적이지 않은 오류를 탐지하기위한 파일. 파일 이름을 지정하십시오. 비활성화하려면 비워 둡니다.

유용한 팁 : 시간 형식 자리 표시자를 사용하여 로그 파일 이름에 날짜/시간 정보를 첨부할 수 있습니다. 사용 가능한 시간 형식 자리 표시자는 <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>에 표시됩니다.

##### "outbound_request_log" `[string]`
- 아웃바운드 요청의 결과를 기록하기 위한 파일. 파일 이름을 지정하십시오. 비활성화하려면 비워 둡니다.

유용한 팁 : 시간 형식 자리 표시자를 사용하여 로그 파일 이름에 날짜/시간 정보를 첨부할 수 있습니다. 사용 가능한 시간 형식 자리 표시자는 <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>에 표시됩니다.

##### "report_log" `[string]`
- 외부 API로 전송된 보고서를 기록하기 위한 파일입니다. 파일 이름을 지정하십시오. 비활성화하려면 비워 둡니다.

유용한 팁 : 시간 형식 자리 표시자를 사용하여 로그 파일 이름에 날짜/시간 정보를 첨부할 수 있습니다. 사용 가능한 시간 형식 자리 표시자는 <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>에 표시됩니다.

##### "truncate" `[string]`
- 로그 파일이 특정 크기에 도달하면 잘 있습니까? 값은 로그 파일이 잘 리기 전에 커질 가능성이있는 B/KB/MB/GB/TB 단위의 최대 크기입니다. 기본값 "0KB"은 절단을 해제합니다 (로그 파일은 무한정 확장 할 수 있습니다). 참고 : 개별 로그 파일에 적용됩니다! 로그 파일의 크기는 일괄 적으로 고려되지 않습니다.

##### "log_rotation_limit" `[int]`
- 로그 회전은 한 번에 존재해야하는 로그 파일 수를 제한합니다. 새 로그 파일을 만들 때 총 로그, 파일 수가 지정된 제한을 초과하면, 지정된 작업이 수행됩니다. 여기서 원하는 한계를 지정할 수 있습니다. 값 0은 로그 회전을 비활성화합니다.

##### "log_rotation_action" `[string]`
- 로그 회전은 한 번에 존재해야하는 로그 파일 수를 제한합니다. 새 로그 파일을 만들 때 총 로그, 파일 수가 지정된 제한을 초과하면, 지정된 작업이 수행됩니다. 여기서 원하는 동작을 지정할 수 있습니다.

```
log_rotation_action
├─Delete ("제한이 더 이상 초과되지 않을 때까지, 가장 오래된 로그 파일을 삭제하십시오.")
└─Archive ("제한이 더 이상 초과되지 않을 때까지, 가장 오래된 로그 파일을 보관 한 다음 삭제하십시오.")
```

##### "log_banned_ips" `[bool]`
- 금지 된 IP에서 차단 된 요청을 로그 파일에 포함됩니까? True = 예 (Default / 기본값); False = 아니오.

##### "log_sanitisation" `[bool]`
- 프런트 엔드 로그 페이지를 사용하여 로그 데이터를 볼 때, XSS 공격 및 기타 잠재적 인 위협으로부터 사용자를 보호하기 위해 CIDRAM은 로그 데이터를 표시하기 전에 위생 처리합니다. 그러나 기본적으로, 로깅 중에는 데이터가 삭제되지 않습니다. 이렇게하면 로그 데이터가 정확하게 보존됩니다 (앞으로 필요할 수도있는 경험적 또는 법의학 분석에 유용합니다). 그러나, 사용자가 외부 도구를 사용하여 로그 데이터를 읽으려고하면, 외부 도구가 자체 위생 처리를 수행하지 않는 경우, 사용자가 XSS 공격에 노출 될 수 있습니다. 필요한 경우, 이 구성 지정 문을 사용하여 기본 작동을 변경할 수 있습니다. True = 데이터 로깅 할 때 데이터, 위생적으로하다 (기록된 데이터 정확도가 더 낮습니다, 않지만 XSS 위험이 더 낮습니다). False = 데이터 로깅 할 때 데이터, 위생적으로하지 마라 (기록된 데이터 정확도가 더 높습니다, 않지만 XSS 위험이 더 높습니다) (Default / 기본 설정).

#### "frontend" (카테고리)
프런트 엔드에 대한 구성입니다.

##### "frontend_log" `[string]`
- 프론트 엔드 로그인 시도를 기록하는 파일. 파일 이름을 지정하십시오. 비활성화하려면 비워 둡니다.

유용한 팁 : 시간 형식 자리 표시자를 사용하여 로그 파일 이름에 날짜/시간 정보를 첨부할 수 있습니다. 사용 가능한 시간 형식 자리 표시자는 <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>에 표시됩니다.

##### "signatures_update_event_log" `[string]`
- 프런트 엔드임를 통해 서명이 업데이트될 때 로깅을 위한 파일입니다. 파일 이름을 지정하십시오. 비활성화하려면 비워 둡니다.

유용한 팁 : 시간 형식 자리 표시자를 사용하여 로그 파일 이름에 날짜/시간 정보를 첨부할 수 있습니다. 사용 가능한 시간 형식 자리 표시자는 <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>에 표시됩니다.

##### "max_login_attempts" `[int]`
- 로그인 시도 최대 횟수입니다 (프론트 엔드). Default (기본 설정) = 5.

##### "theme" `[string]`
- 프런트 엔드에 사용할 테마입니다.

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
└─…다른
```

##### "theme_mode" `[string]`
- 프런트 엔드에 사용할 테마의 모드입니다.

```
theme_mode
├─normal ("정상")
└─inverted ("반전")
```

##### "magnification" `[float]`
- 글꼴 배율. Default (기본 설정) = 1.

##### "custom_header" `[string]`
- 모든 프런트 엔드 페이지의 맨 처음에 HTML로 삽입됩니다. 웹사이트 로고, 개인화된 헤더, 스크립트, 등에 유용합니다.

##### "custom_footer" `[string]`
- 모든 프런트 엔드 페이지의 맨 아래에 HTML로 삽입됩니다. 법적 고지, 연락처 링크, 비즈니스 정보, 등에 유용합니다.

##### "remotes" `[string]`
- 구성 요소 메타데이터를 가져오기 위해 업데이트할 터에서 사용하는 주소 목록입니다. 이것은 새로운 주 버전으로 업그레이드하거나 업데이트를 위한 새로운 소스를 얻을 때 조정해야 할 수 있지만 일반적인 상황에서는 그대로 두어야 합니다.

##### "enable_two_factor" `[bool]`
- 이 지시문은 프런트 엔드 계정에 2FA를 사용할지 여부를 결정합니다.

#### "signatures" (카테고리)
서명, 서명 파일, 모듈, 등의 설정.

##### "shorthand" `[string]`
- 주어진 속기 단어를 사용하는 서명에 대해 긍정적인 일치가 있을 때 요청을 처리하는 방법을 제어합니다.

```
shorthand───[차단하세요.]─[프로필을.]─[차단되면, 출력 템플릿을 억제합니다.]
├─Attacks ("공격")
├─Bogon ("⁰ 보곤 IP")
├─Cloud ("클라우드 서비스")
├─Generic ("일반")
├─Legal ("¹ 적법한")
├─Malware ("멀웨어")
├─Proxy ("² 프록시")
├─Spam ("스팸")
├─Banned ("³ 금지 된")
├─BadIP ("³ 잘못된 IP")
├─RL ("³ 제한 속도")
├─Conflict ("³ 충돌")
└─Other ("⁴ 다른")
```

__0.__ 웹 사이트에 LAN 또는 localhost를 통한 액세스가 필요한 경우, 이를 차단하지 마십시오. 그렇지 않은 경우, 이를 차단할 수 있습니다.

__1.__ 기본 서명 파일은 이것을 사용하지 않습니다, 그러나 일부 사용자에게 유용한 경우를 위해 지원됩니다.

__2.__ 사용자가 프록시를 통해 웹사이트에 액세스할 수 있도록 해야 하는 경우, 이를 차단하지 마십시오. 그렇지 않은 경우, 이를 차단할 수 있습니다.

__3.__ 서명에서 직접 사용은 지원되지 않지만, 특정 상황에서는 다른 수단으로 호출될 수 있습니다.

__4.__ 속기 단어를 전혀 사용하지 않거나 CIDRAM에서 인식하지 못하는 경우를 말합니다.

__서명당 하나.__ 서명은 여러 프로필을 호출할 수 있지만, 하나의 속기 단어만 사용할 수 있습니다. 여러 개의 속기 단어가 적합할 수 있지만, 하나만 사용할 수 있으므로, 항상 가장 적합한 속기 단어만 사용하려고 합니다.

__우선 사항.__ 선택한 옵션은 항상 선택되지 않은 옵션보다 우선합니다. 예를 들어, 여러 속기 단어가 사용 중이지만, 그중 하나만 차단된 것으로 설정된 경우, 요청은 계속 차단됩니다.

__휴먼 엔드포인트 및 클라우드 서비스.__ 클라우드 서비스는 웹호스팅 제공자, 서버 팜, 데이터 센터 또는 기타 여러 가지를 참조할 수 있습니다. 휴먼 엔드포인트는 인간이 인터넷에 액세스하는 수단을 나타냅니다, 예를 들어, 인터넷 서비스 제공자를 통해. 네트워크는 일반적으로 둘 중 하나만, 제공하지만 때로는 둘 다를 제공할 수도 있습니다. 우리는 잠재적인 휴먼 엔드포인트를 클라우드 서비스로 식별하지 않으려고 합니다. 따라서, 클라우드 서비스는 알려진 인간 엔드포인트와 범위를 공유하는 경우 다른 것으로 식별될 수 있습니다. 마찬가지로, 알려진 인간 엔드포인트가 범위를 공유하지 않는 경우, 클라우드 서비스를 클라우드 서비스로 식별하려고 합니다. 따라서, 클라우드 서비스로 식별된 요청은 알려진 인간 엔드포인트와 범위를 공유하지 않을 가능성이 높습니다. 마찬가지로, 공격이나 스팸으로 식별된 요청은 범위를 공유할 가능성이 높습니다. 그러나, 인터넷은 항상 유동적이며, 네트워크의 목적은 시간이 지남에 따라 변경되며, 범위는 항상 구매 또는 판매되므로, 거짓 양성 관련하여 인식하고 경계하십시오.

##### "default_tracktime" `[string]`
- IP 주소를 추적해야 하는 기간입니다. Default (기본값) = 7d0°0′0″ (1 주).

##### "infraction_limit" `[int]`
- IP가 IP 추적에 의해 금지되기 전에 발생하는 것이 허용된다 위반의 최대 수. Default (기본값) = 10.

##### "tracking_override" `[bool]`
- 모듈이 추적 옵션을 재정의하도록 허용하시겠습니까? True = 예 (Default / 기본 설정); False = 아니오.

##### "conflict_response" `[int]`
- 같은 리소스에 동시에 액세스하려는 시도가 너무 많은 경우 (예, 동일한 리소스에 대해 동일한 머신에서 여러 PHP 프로세스에 동시 요청), 일부 시도는 실패할 수 있습니다. 이것이 서명 파일이나 모듈에 영향을 미치는 경우, CIDRAM이 요청에 대해 효과적인 결정을 내리지 못할 수 있습니다. 이런 일이 발생하면, 요청을 차단해야 할까요? 그리고 CIDRAM은 어떤 HTTP 상태 메시지를 보내야 할까요?

```
conflict_response
├─0 (요청을 차단하지 마세요.): 악성인 것으로 확신할 때만 요청을 차단하거나, 거짓
│ 양성 반응에 대해 신중하게 대처하려는 경우 이 (원치
│ 않는 교통이 가끔 통과하는 대가를 치르면서), 옵션을
│ 선택하세요. 무해한 요청인지 확실하지 않을 때 경계를
│ 유지하고 요청을 차단하려면 (가끔씩 거짓 양성 반응이
│ 나올 수 있다는 대가를 치르며), 사용 가능한 다른 옵션
│ 중 하나를 선택하세요.
├─409 (409 Conflict (충돌)): 리소스 충돌에 (예 : 병합 충돌, 파일 액세스 충돌, 등등)
│ 권장됩니다. 다른 상황에서는 권장되지 않습니다.
└─429 (429 Too Many Requests (너무 많은 요청)): 속도 제한, DDoS 공격 처리, 및 홍수 방지에 권장됩니다.
  다른 상황에서는 권장되지 않습니다.
```

#### "verification" (카테고리)
요청의 출처를 확인하기 위한 구성.

##### "search_engines" `[string]`
- 검색 엔진의 요청을 확인하기 위한 컨트롤입니다.

```
search_engines───[검증을 시도?]─[네거티브를 차단하시겠습니까?]─[검증되지 않은 요청을 차단하시겠습니까?]─[단일 히트 바이 패스를 허용하시겠습니까?]─[포지티브를 추적 해제하시겠습니까?]
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

__"긍정적"과 "부정적"이란 무엇입니까?__ 요청으로 제시된 신원을 확인할 때 성공적인 결과는 "긍정적" 또는 "부정적"으로 설명될 수 있습니다. 제시한 신분이 실제 신분으로 확인되면 "긍정적"으로 기재됩니다. 제시한 신원이 위조된 것으로 확인되는 경우 "부정적"으로 기재됩니다. 그러나, 실패한 결과는 (예 : 확인에 실패하거나, 제시된 신원의 진실성을 확인할 수 없음) "긍정적" 또는 "부정적"으로 설명되지 않습니다. 대신, 실패한 결과는 단순히 검증되지 않은 것으로 설명됩니다. 요청으로 제시된 신원을 확인하려는 시도가 없을 때 요청은 마찬가지로 확인되지 않은 것으로 설명됩니다. 이 용어는 요청으로 제공된 신원이 인식되고 따라서 검증이 가능한 상황에서만 의미가 있습니다. 이 용어는 요청으로 제공된 신원이 인식되고 따라서 검증이 가능한 상황에서만 의미가 있습니다.

__"단일 히트 바이 패스"란 무엇입니까?__ 어떤 경우에는 서명 파일, 모듈, 또는 기타 요청 조건으로 인해 긍정적으로 확인된 요청이 여전히 차단될 수 있으며 소 탐을 피하고자 바이 패스가 필요할 수 있습니다. 바이패스가 정확히 하나의 위반을 처리하도록 의도된 경우 이러한 바이패스는 "단일 히트 바이 패스"로 설명될 수 있습니다.

* 이 옵션은 `bypasses➡used` 아래에 해당 바이패스가 있습니다. 해당 바이패스의 확인란이 이 옵션의 확인을 위한 확인란과 동일한 방식으로 표시되어 있는지 확인하는 것이 좋습니다.

##### "social_media" `[string]`
- 소셜 미디어 플랫폼의 요청을 확인하기 위한 컨트롤입니다.

```
social_media───[검증을 시도?]─[네거티브를 차단하시겠습니까?]─[검증되지 않은 요청을 차단하시겠습니까?]─[단일 히트 바이 패스를 허용하시겠습니까?]─[포지티브를 추적 해제하시겠습니까?]
├─Embedly ("* Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("* Pinterest")
├─Snapchat ("* Snapchat")
└─Twitterbot ("*!! Twitterbot")
```

__"긍정적"과 "부정적"이란 무엇입니까?__ 요청으로 제시된 신원을 확인할 때 성공적인 결과는 "긍정적" 또는 "부정적"으로 설명될 수 있습니다. 제시한 신분이 실제 신분으로 확인되면 "긍정적"으로 기재됩니다. 제시한 신원이 위조된 것으로 확인되는 경우 "부정적"으로 기재됩니다. 그러나, 실패한 결과는 (예 : 확인에 실패하거나, 제시된 신원의 진실성을 확인할 수 없음) "긍정적" 또는 "부정적"으로 설명되지 않습니다. 대신, 실패한 결과는 단순히 검증되지 않은 것으로 설명됩니다. 요청으로 제시된 신원을 확인하려는 시도가 없을 때 요청은 마찬가지로 확인되지 않은 것으로 설명됩니다. 이 용어는 요청으로 제공된 신원이 인식되고 따라서 검증이 가능한 상황에서만 의미가 있습니다. 이 용어는 요청으로 제공된 신원이 인식되고 따라서 검증이 가능한 상황에서만 의미가 있습니다.

__"단일 히트 바이 패스"란 무엇입니까?__ 어떤 경우에는 서명 파일, 모듈, 또는 기타 요청 조건으로 인해 긍정적으로 확인된 요청이 여전히 차단될 수 있으며 소 탐을 피하고자 바이 패스가 필요할 수 있습니다. 바이패스가 정확히 하나의 위반을 처리하도록 의도된 경우 이러한 바이패스는 "단일 히트 바이 패스"로 설명될 수 있습니다.

* 이 옵션은 `bypasses➡used` 아래에 해당 바이패스가 있습니다. 해당 바이패스의 확인란이 이 옵션의 확인을 위한 확인란과 동일한 방식으로 표시되어 있는지 확인하는 것이 좋습니다.

** ASN 조회 기능이 필요합니다 (예 : IP-API 또는 BGPView 모듈을 통해).

*!! iMessage로 인해 오탐이 발생할 가능성이 높습니다.

##### "other" `[string]`
- 가능한 경우 다른 종류의 요청을 확인하기 위한 제어입니다.

```
other───[검증을 시도?]─[네거티브를 차단하시겠습니까?]─[검증되지 않은 요청을 차단하시겠습니까?]─[단일 히트 바이 패스를 허용하시겠습니까?]─[포지티브를 추적 해제하시겠습니까?]
├─AdSense ("AdSense")
├─AmazonAdBot ("* AmazonAdBot")
├─ChatGPT-User ("!! ChatGPT-User")
└─GPTBot ("!! GPTBot")
```

__"긍정적"과 "부정적"이란 무엇입니까?__ 요청으로 제시된 신원을 확인할 때 성공적인 결과는 "긍정적" 또는 "부정적"으로 설명될 수 있습니다. 제시한 신분이 실제 신분으로 확인되면 "긍정적"으로 기재됩니다. 제시한 신원이 위조된 것으로 확인되는 경우 "부정적"으로 기재됩니다. 그러나, 실패한 결과는 (예 : 확인에 실패하거나, 제시된 신원의 진실성을 확인할 수 없음) "긍정적" 또는 "부정적"으로 설명되지 않습니다. 대신, 실패한 결과는 단순히 검증되지 않은 것으로 설명됩니다. 요청으로 제시된 신원을 확인하려는 시도가 없을 때 요청은 마찬가지로 확인되지 않은 것으로 설명됩니다. 이 용어는 요청으로 제공된 신원이 인식되고 따라서 검증이 가능한 상황에서만 의미가 있습니다. 이 용어는 요청으로 제공된 신원이 인식되고 따라서 검증이 가능한 상황에서만 의미가 있습니다.

__"단일 히트 바이 패스"란 무엇입니까?__ 어떤 경우에는 서명 파일, 모듈, 또는 기타 요청 조건으로 인해 긍정적으로 확인된 요청이 여전히 차단될 수 있으며 소 탐을 피하고자 바이 패스가 필요할 수 있습니다. 바이패스가 정확히 하나의 위반을 처리하도록 의도된 경우 이러한 바이패스는 "단일 히트 바이 패스"로 설명될 수 있습니다.

* 이 옵션은 `bypasses➡used` 아래에 해당 바이패스가 있습니다. 해당 바이패스의 확인란이 이 옵션의 확인을 위한 확인란과 동일한 방식으로 표시되어 있는지 확인하는 것이 좋습니다.

!! 진짜든 가짜든 상관없이, 대부분의 사용자는 이것이 차단되기를 원할 것입니다. 이는 "검증을 시도"를 선택하지 않고 "검증되지 않은 요청을 차단하시겠습니까"을 선택함으로써 달성할 수 있습니다. 그러나, 일부 사용자는 이러한 요청을 확인할 수 있기를 원할 수 있기 때문에 (긍정적인 것은 허용하면서 부정적인 것은 차단하기 위해), 모듈을 통해 이러한 요청을 차단하는 대신, 이러한 요청을 처리하는 옵션이 여기에 제공됩니다.

##### "adjust" `[string]`
- 검증과 관련하여 다른 기능을 조정하는 컨트롤입니다.

```
adjust───[HCaptcha 억제]─[Friendly Captcha 억제]─[Cloudflare Turnstile 억제]
├─Negatives ("차단된 네거티브")
└─NonVerified ("차단된 검증되지 않은")
```

#### "captcha" (카테고리)
CAPTCHA 설정 (차단될 때 사람이 다시 액세스할 수 있는 방법을 제공합니다).

##### "usemode" `[int]`
- CAPTCHA는 언제 제공해야 합니까 ? 여기에서 지원되는 각 공급자에 대한 기본 동작을 지정할 수 있습니다. 참고 : 허용 목록에 있거나 확인되고 차단되지 않은 요청은 보안 문자를 작성할 필요가 없습니다. 또한 참고 : CAPTCHA는 봇 및 다양한 종류의 악성 자동 요청에 대한 유용한 추가 보호 계층을 제공할 수 있지만 악의적인 사람에 대한 보호는 제공하지 않습니다.

```
usemode───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─0 (못.)
├─1 (차단되었을, 서명 한도 내고 금지되지 않으면 때만.)
├─2 (차단되었을, 특별히 사용 표시, 서명 한도 내고 금지되지 않으면 때만.)
├─3 (서명 한도 내고 금지되지 않으면 때만 (차단 여부와 관계없이).)
├─4 (차단되지 때만.)
├─5 (차단되지 않은 경우, 또는 특별히 사용 표시, 서명 한도 내고 금지되지 않으면 때만.)
└─6 (차단되지 않은 경우에만, 민감한 페이지 요청 시.)
```

##### "nonblocked_status_code" `[int]`
- 차단되지 않은 요청에 CAPTCHA를 표시 할 때 어떤 상태 코드를 사용해야합니까?

```
nonblocked_status_code───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─200 (200 OK): 가장 덜 강력하지만 가장 사용자 친화적입니다. 자동화된
│ 요청은 이 응답을 요청이 성공했다는 표시로 해석할
│ 가능성이 큽니다. 차단되지 않은 요청에 권장됩니다.
├─403 (403 Forbidden (금지)): 더 강력하지만, 사용자 친화성은 떨어집니다. 대부분의
│ 일반적인 상황에 권장됩니다.
├─418 (418 I'm a teapot (나는 찻주전자)): 만우절 농담을 참고하여 (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). 클라이언트, 로봇,
│ 브라우저, 등이 이해하지 못할 가능성이 매우 높습니다.
│ 오락과 편의를 위해 제공되지만, 일반적으로 권장되지
│ 않습니다.
├─429 (429 Too Many Requests (너무 많은 요청)): 속도 제한, DDoS 공격 처리, 및 홍수 방지에 권장됩니다.
│ 다른 상황에서는 권장되지 않습니다.
└─451 (451 Unavailable For Legal Reasons (법적 이유로 사용할 수 없음)): 주로 법적 이유로 차단할 때 권장됩니다. 다른
  상황에서는 권장되지 않습니다.
```

##### "api" `[string]`
- 어떤 API를 사용할 수 있습니까?

```
api───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─v0 ("v0")
├─v1 ("v1")
├─Invisible ("v1 (보이지 않음)")
└─v2 ("v2")
```

##### "messages" `[string]`
- CAPTCHA와 함께 표시될 메시지입니다.

```
messages───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─cookie_warning ("쿠키 경고 표시 하시겠습니까 ?): 해당 국가 또는 주의 개인정보 보호법 (예 : EU의 GDPR/DSGVO,
│ 브라질의 LGPD, 등)에 따라, 법적으로 요구될 수 있습니다."
└─api_message ("API 메시지를 표시 하시겠습니까 ?): CAPTCHA를 완료하기 위한 API에 적합한 사용자 지침입니다."
```

##### "lockto" `[string]`
- CAPTCHA를 잠글 대상.

```
lockto───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─ip ("CAPTCHA는 CAPTCHA를 완료하는 사용자의 IP 주소에 잠금되어야 하며, 실제 사용자에게는 잠금되어서는 안 됩니다.): 쿠키는 사용자를 식별하는 데 사용되지 않습니다.
│ CAPTCHA를 성공적으로 완료하여 접근이 회복된 경우,
│ 동일한 IP 주소에서 접속하는 모든 사람에게 적용됩니다."
├─user ("CAPTCHA는 CAPTCHA를 완료한 사용자에게만 잠금되어야 하지만, IP 주소에는 잠금되어서는 안 됩니다.): 쿠키는 사용자를 식별하는 데 사용됩니다. CAPTCHA를
│ 성공적으로 완료하여 접근이 회복된 경우, 이는 CAPTCHA를
│ 완료한 사용자에게만 적용되며, 쿠키가 유효한 한 IP
│ 주소가 변경되더라도 유지됩니다."
└─both ("CAPTCHA는 CAPTCHA를 완료한 사용자와 해당 IP 주소에 모두 잠금되어야 합니다.): 쿠키는 사용자를 식별하는 데 사용됩니다. CAPTCHA를
  성공적으로 완료하여 접근이 회복된 경우, 이는 사용자가
  CAPTCHA를 완료한 경우에만 적용됩니다. IP 주소가 변경되면
  액세스가 지속되지 않습니다."
```

##### "hcaptcha_sitekey" `[string]`
- CIDRAM과 함께 hCaptcha를 사용하려면 여기에 값을 입력해야 합니다. 그렇지 않다면 무시해도 됩니다.

이 값은 보안 문자 서비스의 대시 보드에서 찾을 수 있습니다.

또한보십시오 :
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "hcaptcha_secret" `[string]`
- CIDRAM과 함께 hCaptcha를 사용하려면 여기에 값을 입력해야 합니다. 그렇지 않다면 무시해도 됩니다.

이 값은 보안 문자 서비스의 대시 보드에서 찾을 수 있습니다.

또한보십시오 :
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "friendly_sitekey" `[string]`
- CIDRAM과 함께 Friendly Captcha를 사용하려면 여기에 값을 입력해야 합니다. 그렇지 않다면 무시해도 됩니다.

이 값은 보안 문자 서비스의 대시 보드에서 찾을 수 있습니다.

또한보십시오 :
- [Friendly Captcha Dashboard](https://app.friendlycaptcha.eu/dashboard)

##### "friendly_apikey" `[string]`
- CIDRAM과 함께 Friendly Captcha를 사용하려면 여기에 값을 입력해야 합니다. 그렇지 않다면 무시해도 됩니다.

이 값은 보안 문자 서비스의 대시 보드에서 찾을 수 있습니다.

또한보십시오 :
- [Friendly Captcha Dashboard](https://app.friendlycaptcha.eu/dashboard)

##### "turnstile_sitekey" `[string]`
- CIDRAM과 함께 Cloudflare Turnstile를 사용하려면 여기에 값을 입력해야 합니다. 그렇지 않다면 무시해도 됩니다.

이 값은 보안 문자 서비스의 대시 보드에서 찾을 수 있습니다.

또한보십시오 :
- [Cloudflare Dashboard](https://dash.cloudflare.com/)

##### "turnstile_secret" `[string]`
- CIDRAM과 함께 Cloudflare Turnstile를 사용하려면 여기에 값을 입력해야 합니다. 그렇지 않다면 무시해도 됩니다.

이 값은 보안 문자 서비스의 대시 보드에서 찾을 수 있습니다.

또한보십시오 :
- [Cloudflare Dashboard](https://dash.cloudflare.com/)

##### "expiry" `[float]`
- 보안 문자 인스턴스를 기억 시간. Default (기본 설정) = 720 (1 개월).

##### "signature_limit" `[int]`
- 보안 문자 제안이 철회되기 전에 허용되는 최대 서명 수입니다. Default (기본 설정) = 1.

##### "log" `[string]`
- 보안 문자 시도 기록. 파일 이름을 지정하십시오. 비활성화하려면 비워 둡니다.

유용한 팁 : 시간 형식 자리 표시자를 사용하여 로그 파일 이름에 날짜/시간 정보를 첨부할 수 있습니다. 사용 가능한 시간 형식 자리 표시자는 <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>에 표시됩니다.

#### "legal" (카테고리)
법적 요구 사항 설정.

##### "pseudonymise_ip_addresses" `[bool]`
- 로그 파일을 쓸 때 가명으로 하다 IP 주소? True = 예 (Default / 기본 설정); False = 아니오.

##### "privacy_policy" `[string]`
- 생성 된 페이지의 꼬리말에 표시 할 관련 개인 정보 정책 방침의 주소입니다. URL 지정, 또는 사용하지 않으려면 비워 두십시오.

#### "template_data" (카테고리)
템플릿 및 테마 설정.

##### "theme" `[string]`
- 블록 이벤트와 CAPTCHA 요청에 사용할 테마입니다.

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
└─…다른
```

##### "theme_mode" `[string]`
- 블록 이벤트와 CAPTCHA 요청에 사용할 테마의 모드입니다.

```
theme_mode
├─normal ("정상")
└─inverted ("반전")
```

##### "magnification" `[float]`
- 글꼴 배율. Default (기본 설정) = 1.

##### "css_url" `[string]`
- 사용자 정의 테마의 CSS 파일 URL입니다.

##### "block_event_title" `[string]`
- 블록 이벤트에 대해 표시할 페이지 제목입니다.

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("액세스 거부!")
└─…다른
```

##### "captcha_title" `[string]`
- CAPTCHA 요청에 대해 표시할 페이지 제목입니다.

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…다른
```

##### "custom_header" `[string]`
- 모든 "액세스 거부" 페이지의 맨 처음에 HTML로 삽입됩니다. 웹사이트 로고, 개인화된 헤더, 스크립트, 등에 유용합니다.

##### "custom_footer" `[string]`
- 모든 "액세스 거부" 페이지 맨 아래에 HTML로 삽입됩니다. 법적 고지, 연락처 링크, 비즈니스 정보, 등에 유용합니다.

#### "rate_limiting" (카테고리)
속도 제한 설정 (일반적인 사용에는 권장되지 않습니다).

참고해주세요, 다른 모든 CIDRAM 기능과 마찬가지로, CIDRAM의 속도 제한 기능은 CIDRAM이 연결된 페이지와 리소스에만 적용할 수 있습니다. 일반적으로 이는 연결된 PHP 리소스에서 명시적으로 제공되는 경우를 제외하고는 PHP가 아닌 리소스는 다루어지지 않음을 의미합니다. 서버 모듈, cPanel, 또는 기타 네트워크 도구를 사용하여 속도 제한을 적용할 수 있다면 CIDRAM의 속도 제한 기능 대신 이를 사용하는 것이 더 좋습니다. 또한, 동기가 부여되고 결의가 있는 사용자는 IP 주소를 순환시키거나 CIDRAM이 아직 인식하지 못하는 프록시나 VPN 공급자로 전환함으로써 속도 제한을 쉽게 우회할 수 있으며, 속도 제한은 실제 최종 사용자에게 매우 귀찮을 수 있습니다. 때로는 필요할 수도 있지만, 대개 바람직하지는 않습니다.

##### "max_bandwidth" `[string]`
- 향후 요청에 대해 속도 제한을 사용하기 전에 허용 기간 내에 허용되는 최대 대역폭입니다. 0 값은 이러한 유형의 속도 제한을 비활성화합니다. Default (기본 설정) = 0KB.

##### "max_requests" `[int]`
- 향후 요청에 대해 속도 제한을 사용하도록 설정하기 전에 허용 기간 내에 허용되는 최대 요청 수입니다. 0 값은 이러한 유형의 속도 제한을 비활성화합니다. Default (기본 설정) = 0.

##### "precision_ipv4" `[int]`
- IPv4 사용을 모니터링 할 때 사용할 정밀도입니다. 값은 CIDR 블록 크기와 동일합니다. 최상의 정밀도를 위해 32로 설정하십시오. Default (기본 설정) = 32.

##### "precision_ipv6" `[int]`
- IPv6 사용을 모니터링 할 때 사용할 정밀도입니다. 값은 CIDR 블록 크기와 동일합니다. 최상의 정밀도를 위해 128로 설정하십시오. Default (기본 설정) = 128.

##### "allowance_period" `[string]`
- 사용량을 모니터 할 기간입니다. Default (기본 설정) = 0°0′0″.

##### "exceptions" `[string]`
- 예외 (즉, 속도 제한이 없어야하는 요청). 속도 제한이 활성화 된 경우에만 해당됩니다.

```
exceptions
├─Whitelisted ("화이트리스트 된 것으로 표시된 요청")
├─Verified ("확인 된 검색 엔진 및 소셜 미디어 요청")
└─FE ("CIDRAM 프런트 엔드에 대한 요청")
```

##### "segregate" `[bool]`
- 서로 다른 도메인과 호스트에 대한 할당량을 분리하거나 공유해야 합니까? True = 할당량이 분리됩니다. False = 할당량이 공유됩니다 (Default / 기본 설정).

#### "supplementary_cache_options" (카테고리)
보충 캐시 옵션. 참고 : 이 값을 변경하면 잠재적으로 로그아웃될 수 있습니다.

##### "prefix" `[string]`
- 여기에 지정된 값은 모든 캐시 항목 키 앞에 추가됩니다. Default (기본값) = "CIDRAM_". 동일한 서버에 여러 설치가 있는 경우, 캐시를 서로 분리하여 유지하는 데 유용할 수 있습니다.

##### "enable_apcu" `[bool]`
- 캐싱에 APCu를 사용할지 여부를 지정합니다. Default (기본값) = True.

##### "enable_memcached" `[bool]`
- 캐싱에 Memcached를 사용할지 여부를 지정합니다. Default (기본값) = False.

##### "enable_redis" `[bool]`
- 캐싱에 Redis를 사용할지 여부를 지정합니다. Default (기본값) = False.

##### "enable_pdo" `[bool]`
- 캐싱에 PDO를 사용할지 여부를 지정합니다. Default (기본값) = False.

##### "memcached_host" `[string]`
- Memcached 호스트 값. Default (기본값) = localhost.

##### "memcached_port" `[int]`
- Memcached 포트 값. Default (기본값) = "11211".

##### "redis_host" `[string]`
- Redis 호스트 값. Default (기본값) = localhost.

##### "redis_port" `[int]`
- Redis 포트 값. Default (기본값) = "6379".

##### "redis_timeout" `[float]`
- Redis 시간 초과 값. Default (기본값) = "2.5".

##### "redis_database_number" `[int]`
- Redis 데이터베이스 번호입니다. Default (기본값) = 0. 참고 : Redis 클러스터에서는 0 이외의 값을 사용할 수 없습니다.

##### "pdo_dsn" `[string]`
- PDO DSN 값. Default (기본값) = "mysql:dbname=cidram;host=localhost;port=3306".

__자주하는 질문.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.ko.md#user-content-HOW_TO_USE_PDO" hreflang="ko-KR">"PDO DSN"은 무엇입니까? CIDRAM과 함께 PDO를 사용하려면 어떻게해야합니까?</a>*

##### "pdo_username" `[string]`
- PDO 사용자 이름.

##### "pdo_password" `[string]`
- PDO 암호.

#### "bypasses" (카테고리)
기본 서명 바이 패스 구성.

##### "used" `[string]`
- 어떤 바이 패스를 사용해야 합니까?

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
└─Yandex ("Yandex/Яндекс")
```

---


### 6. <a name="SECTION6"></a>서명 형식

*참조 :*
- *["서명"이란 무엇입니까?](#user-content-WHAT_IS_A_SIGNATURE)*

#### 6.0 기초 (서명 파일의 경우)

모든 IPv4 서명이 형식을 따릅니다 : `xxx.xxx.xxx.xxx/yy [기능] [매개 변수]`
- `xxx.xxx.xxx.xxx`는 CIDR 블록의 시작을 나타냅니다 (블록의 첫 번째 IP 주소 옥텟).
- `yy`는 블록 사이즈를 나타냅니다 (1-32).
- `[기능]`스크립트에 서명을 어떻게 처리를 지시합니다.
- `[매개 변수]`은 `[기능]`에 필요, 추가 정보를 나타냅니다.

모든 IPv6 서명이 형식을 따릅니다 : `xxxx:xxxx:xxxx:xxxx::xxxx/yy [기능] [매개 변수]`
- `xxxx:xxxx:xxxx:xxxx::xxxx`는 CIDR 블록의 시작을 나타냅니다 (블록의 첫 번째 IP 주소 옥텟). 전체 표현 및 약식 표기가 모두 가능합니다. 그들은 IPv6 사양을 준수해야합니다 하나의 예외를 제외하고 : CIDRAM에서는 IPv6 주소는 생략로 시작할 수 없습니다. 예를 들면 : `::1/128`는 `0::1/128`, 그리고 `::0/128`는 `0::/128`로 표시해야합니다.
- `yy`는 블록 사이즈를 나타냅니다 (1-128).
- `[기능]`스크립트에 서명을 어떻게 처리를 지시합니다.
- `[매개 변수]`은 `[기능]`에 필요, 추가 정보를 나타냅니다.

서명 파일의 줄 바꿈은 Unix 표준을 사용해야합니다 (`%0A`, `\n`). 다른 표준도 사용할 수 있지만 권장되지 않습니다 (예를 들어, Windows `%0D%0A`, `\r\n`, Mac `%0D`, `\r`, 등). 비 Unix 개행는 정규화됩니다.

정확하고 올바른 CIDR 표기법이 필요합니다. 스크립트는 부정확 한 표기 (또는 부정확 한 표기를 따른 서명)을 인식하지 않습니다. 또한 모든 CIDR은 균등하게 나눌 필요가 있습니다 (예를 들어, `10.128.0.0`에서`11.127.255.255`까지 모두 차단하려는 경우, `10.128.0.0/8`는 스크립트가 인식되지 않습니다, 그러나, `10.128.0.0/9`자 `11.0.0.0/9`를 함께 사용하면 스크립트에 의해 인식됩니다).

스크립트가 인식되지 않는 시그니처 파일의 것은 무시됩니다. 즉, 서명 파일을 손상없이 거의 모든 데이터를 서명 파일에 안전하게 넣을 수 있습니다. 서명 파일의 댓글은 허용입니다. 특별한 서식이 필요하지 않습니다. 쉘 형식의 해시가 권장되지만 강제는되지 않습니다 (쉘 스타일 해시는 IDE이나 일반 텍스트 편집기에 도움이됩니다).

"기능"의 가능한 값 :
- Run
- Whitelist
- Greylist
- Deny

"Run"을 사용하면 서명이 트리거되면 스크립트는`require_once` 문이 (`[매개 변수]` 값으로 지정됩니다) 외부의 PHP 스크립트의 실행을 시도합니다. 작업 디렉토리는 `/vault/` 디렉토리입니다.

예 : `127.0.0.0/8 Run example.php`

특정 IP/CIDR에 대해 특정 PHP 코드를 실행하는 경우에 유용합니다.

"Whitelist"를 사용하면 서명이 트리거되면 스크립트는 모든 검색을 재설정합니다 (뭔가의 검출이 있었을 경우) 테스트 기능을 종료합니다. `[매개 변수]`는 무시됩니다. 이것은 IP 또는 CIDR 화이트리스트에 등록하는 것과 같습니다.

예 : `127.0.0.1/32 Whitelist`

"Greylist"을 사용하면 서명이 트리거되면 스크립트는 모든 검색을 재설정합니다 (뭔가의 검출이 있었을 경우) 처리를 계속하기 위해 다음의 서명 파일로 바로 이동한다. `[매개 변수]`는 무시됩니다.

예 : `127.0.0.1/32 Greylist`

"Deny"를 사용하면 서명이 트리거되면 보호 된 페이지에 대한 액세스가 거부됩니다 (IP/CIDR 화이트리스트에 등록되어 있지 않은 경우). "Deny"실제로 IP 주소와 CIDR 범위를 차단하기 위해 사용하는 것입니다. "Deny"를 사용하는 서명이 트리거 될 때 "액세스 거부"페이지가 생성되고 보호 된 페이지에 대한 요청을 종료합니다.

"Deny"에 의해 받아 들여진 `[매개 변수]`값은 "액세스 거부"페이지 출력 처리됩니다 요청 된 페이지에 대한 액세스가 거부 된 이유는 클라이언트/사용자에게 제공됩니다. 그것은 짧고 간단한 문장을 할 수 있습니다 (왜 그들을 차단하는 것을 선택했는지 설명하기 위해). 또한 축약 할 수 있습니다 (사전 준비된 설명을 클라이언트/사용자에게 제공합니다).

미리 준비된 설명은 L10N의 지원이 스크립트로 번역 할 수 있습니다. 번역은 스크립트 구성의`lang` 지시문을 사용하여 지정된 언어에 따라 이루어집니다. 또한 이러한 단축형 단어를 사용하는 경우 `[매개 변수]`값에 따라 "Deny"서명을 무시하도록 스크립트에 지시 할 수 있습니다. 이것은 스크립트 설정에 지정된 지시어를 통해 이루어집니다 (각각의 약어에 해당하는 지시문이 있습니다). 그러나 다른 `[매개 변수]`값은 L10N이 지원되지 않습니다 (따라서 다른 값은 번역되지 않습니다, 그리고 조직에 의해 통제 가능하지 않다).

약어 :
- Attacks
- Bogon
- Cloud
- Generic
- Legal
- Malware
- Proxy
- Spam

#### 6.1 태그

##### 6.1.0 섹션 태그

섹션 이름 "섹션 태그"를 추가하여 스크립트에 대한 개별 섹션을 식별 할 수 있습니다 (아래의 예를 참조하십시오).

```
# 섹션 1.
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: 섹션 1
```

섹션 태그를 종료하고 서명 섹션이 잘못 식별되지 않도록하려면 태그와 이전 섹션 사이에 적어도 2 개의 줄이 연속 있는지 확인하십시오. 태그없이 서명은 기본적으로 "IPv4"또는 "IPv6"중 하나입니다 (어떤 유형의 서명이 트리거되어 있는지에 따라).

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: 섹션 1
```

위의 예에서`1.2.3.4/32`와 `2.3.4.5/32`은 "IPv4"태그됩니다; 니다 한편 `4.5.6.7/32`와 `5.6.7.8/32`은 "섹션 1"태그됩니다.

다른 유형의 태그를 분리하는 데에도 같은 논리를 적용 할 수 있습니다.

섹션 태그는 오 탐지 (false positive)가 발생할 때 문제의 정확한 원인을 쉽게 찾을 수있는 방법을 제공하여 디버깅에 매우 유용합니다. 프런트 엔드 로그 페이지를 통해 로그 파일을 볼 때 로그 파일 항목 필터링에 매우 유용 할 수 있습니다 (섹션 이름은 프런트 엔드 로그 페이지를 통해 클릭 할 수 있으며 필터링 기준으로 사용할 수 있습니다). 특정 서명에 대해 섹션 태그가 생략 된 경우 해당, 서명이 트리거되면, CIDRAM은 차단 된 IP 주소 유형 (IPv4 또는 IPv6)과 함께 서명 파일의 이름을 폴백으로 사용합니다. 따라서 섹션 태그는 전적으로 선택 사항입니다. 서명 파일이 모호하게 이름이 지정된 경우 또는, 요청을 차단하도록 만드는 서명의 출처를 명확하게 식별하기 어려운 경우와 같이, 일부 경우에 권장 될 수 있습니다.

##### 6.1.1 기한 태그

"기한 태그"를 사용하여 서명의 유효 기간을 지정할 수 있습니다. 만료 된 태그가이 형식을 사용합니다 : "년년년년.월월.날날" (아래의 예를 참조하십시오).

```
# 섹션 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

만료 된 서명은 요청에 대해 트리거되지 않습니다.

##### 6.1.2 원산지 태그

특정 서명의 원산지를 지정하려면 "원산지 태그"를 사용하십시오. 원산지 태그는 "[ISO 3166-1 Alpha-2](https://ko.wikipedia.org/wiki/ISO_3166-1_alpha-2)" 코드를 허용합니다. 이 코드는 해당 서명의 원산지 국가에 해당합니다. 이 코드는 대문자로 작성해야합니다 (소문자 또는 대소 문자가 혼합되어 올바르게 표시되지 않습니다). 원산지 태그가 사용되면 관련 차단 요청에 대한 "왜 차단이 되셨나요"로그 필드 항목에 추가됩니다.

선택적 "flags CSS"구성 요소가 설치된 경우, 프런트 엔드 로그 페이지를 통해 로그 파일을 볼 때 원본 태그로 추가 된 정보가 해당 국가 플래그로 바뀝니다. 이 정보는 원시 형식이든 국가 국기이든간에 클릭 할 수 있습니다. 클릭하면, 비슷한 로그 항목에 따라 로그 항목이 필터링됩니다 (이로 인해 원산지별로 필터링 할 수 있습니다).

참고 : 기술적으로 이것은 특정 위치 정보를 적극적으로 찾지 않기 때문에 위치 정보가 아닙니다. 대신 특정 국가의 서명을 원산지 국가에 명시 할 수 있습니다. 동일한 서명 섹션 내에서 여러 개의 원산지 태그를 사용할 수 있습니다.

가설적인 예 :

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

모든 태그를 함께 사용할 수 있으며 모든 태그는 선택 사항입니다 (아래의 예를 참조하십시오).

```
# 예 섹션.
1.2.3.4/32 Deny Generic
Origin: US
Tag: 예 섹션
Expires: 2016.12.31
```

##### 6.1.3 지연 태그

많은 수의 서명 파일이 설치되어 있고 적극적으로 사용될 때, 설치가 복잡해질 수 있으며 중복되는 일부 서명이있을 수 있습니다. 이러한 경우 블록 이벤트 중에 여러 개의 중첩되는 서명이 트리거되지 않도록 연기 태그를 사용하여 특정 서명 섹션을 연기하여 다른 서명 파일을 우선 사용할 수 있습니다. 이것은 일부 서명이 다른 것보다 자주 갱신되는 경우에 유용 할 수 있으며 업데이트 빈도가 낮은 서명보다 업데이트 빈도가 높은 서명에 우선 순위를 부여합니다.

지연 태그는 다른 태그 유형과 유사하게 사용됩니다. 태그의 값은 설치되고 적극적으로 사용되는 서명 파일과 일치해야합니다.

예 :

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 6.1.4 프로필 태그

프로필 태그는 IP 테스트 페이지에 추가 정보를 표시하는 수단을 제공하며 모듈 및 보조 규칙을 통해 더 복잡한 동작과 미세 조정된 의사 결정을 위해 활용할 수 있습니다.

프로필 태그는 다른 유형의 태그와 유사하게 사용됩니다. 프로필 태그의 값은 모듈 및 보조 규칙에 대한 조건으로 사용할 수 있습니다. 프로필 태그는 세미콜론으로 이러한 값을 구분하여 여러 값을 제공 할 수 있습니다. 최종 사용자는 프로필 태그값을 볼 수 없습니다.

예 :

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 6.2 YAML

##### 6.2.0 YAML 기초

섹션 관련 설정을 정의하기 위해, 간단한 형식의 YAML 마크 업을 서명 파일로 사용할 수 있습니다. 이것은 다른 서명 섹션에 대해 다른 설정을 할 때 유용합니다 (예를 들면 : 지원 티켓의 이메일 주소를 지정하려면, 그러나 특정 섹션 만; 특정 서명으로 페이지 리디렉션을 트리거하려면; hCaptcha에서 사용하기 위해 서명 섹션을 표시하려면; 개별 서명에 따라 그리고/또는 서명 섹션에 따라, 차단 된 액세스 시도를 별도의 파일에 기록하려면).

서명 파일로 YAML 마크 업의 사용은 옵션입니다 (즉, 당신이 원한다면 그것을 사용할 수 있지만 그렇게 할 필요는 없습니다). 대부분의 (하지만 전부는 아니지만) 구성 지시문을 활용할 수 있습니다.

주의 : CIDRAM의 YAML 마크 업의 구현은 매우 단순화되어 매우 제한되어 있습니다. 이것은 YAML 마크 업에 정통한 방법으로하지만 공식 규격을 따르지하거나 준수 할 수 없는 CIDRAM의 특정 요구 사항을 충족하기위한 것입니다 (다른 구현과 같은 방식으로 작동하지 않을 가능성이 있고, 다른 프로젝트에 적합하지 않을 수 있습니다).

CIDRAM는 YAML 마크 업 세그먼트는 스크립트에 3 개의 대시 ("---") 식별됩니다. YAML 마크 업 세그먼트는 이중 줄 바꿈에 의해 서명 섹션과 함께 종료합니다. 전형적인 세그먼트는 CIDR 및 태그 목록의 직후의 행에 3 개의 대시로 구성되며 이어 2 차원의 키와 값 쌍의 목록이 나옵니다. (첫 번째 차원은 지시어의 카테고리입니다; 두 번째 차원은 설정 지시어입니다). 다음의 예를 참조하십시오.

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

#### 6.3 보조

##### 6.3.0 서명 섹션 무시

또한 CIDRAM 특정 서명 섹션을 완전히 무시하려는 경우 `ignore.dat`파일을 사용하여 무시하는 섹션을 지정할 수 있습니다. 새로운 행에`Ignore`과 써주세요 다음, 공간, 그런 CIDRAM 무시하는 섹션의 이름 (다음의 예를 참조하십시오).

```
Ignore 섹션 1
```

CIDRAM 프런트 엔드의 "섹션 목록"페이지에서 제공하는 인터페이스를 사용하여이 작업을 수행 할 수도 있습니다.

##### 6.3.1 보조 규칙

나만의 맞춤 서명 파일이나 맞춤 모듈을 작성하는 것이 너무 복잡하다고 생각되면, 더 간단한 대안은 CIDRAM 프런트 엔드의 "보조 규칙"페이지에서 제공하는 인터페이스를 사용하는 것일 수 있습니다. 적절한 옵션을 선택하고 특정 유형의 요청에 대한 세부 정보를 지정하면 CIDRAM에 요청에 응답하는 방법을 지시 할 수 있습니다. "보조 규칙"은 모든 서명 파일과 모듈이 이미 실행을 마친 후에 실행됩니다.

#### 6.4 <a name="MODULE_BASICS"></a>기초 (모듈 경우)

모듈은 CIDRAM의 기능을 확장하거나, 추가 작업을 수행하거나 추가 논리를 처리하는 데 사용할 수 있습니다.

모듈은 PHP 파일로 작성되기 때문에, CIDRAM 코드베이스에 대해 잘 알고 있다면, 원하는대로 모듈과 모듈 서명을 구성 할 수 있습니다 (합리적인 한도 내에서).

*노트 : PHP 코드 작업에 익숙하지 않은 경우 자신 만의 모듈을 작성하는 것은 좋지 않습니다.*

CIDRAM이 제공하는 일부 기능을 사용하면 모듈을 더 간단하고 쉽게 작성할 수 있습니다. 이 기능에 대한 정보는 아래에 설명되어 있습니다.

#### 6.5 모듈 기능

##### 6.5.0 "$this->trigger"

모듈 서명은 일반적으로 `$this->trigger`로 작성됩니다. 대부분의 경우, 모듈 작성을 목적으로이 method 다른 어떤 것보다 중요합니다.

`$this->trigger`는 4 개의 매개 변수를 허용합니다 : `$Condition`, `$ReasonShort`, `$ReasonLong` (선택 과목), 및 `$DefineOptions` (선택 과목).

`$Condition`의 진실성이 평가됩니다. True의 경우, 서명은 트리거됩니다. False의 경우, 서명은 트리거되지 않습니다. `$Condition`에는 대개 요청을 차단해야하는 조건을 평가하는 PHP 코드가 들어 있습니다.

서명이 트리거되면, `$ReasonShort`가 "왜 차단이 되셨나요"필드에 표시됩니다.

`$ReasonLong`은 차단되었을 때 사용자/클라이언트에게 차단 된 이유를 설명하기 위해 표시되는 선택적 메시지입니다. 생략시 표준 "액세스 거부"메시지를 사용합니다.

`$DefineOptions`는 키/값 쌍을 포함하는 선택적 배열입니다. 요청 인스턴스와 관련된 구성 옵션을 정의하는 데 사용됩니다. 구성 옵션은 서명이 트리거 될 때 적용됩니다.

`$this->trigger`는 서명이 트리거되면 true를 반환하고, 그렇지 않으면 false를 반환합니다.

##### 6.5.1 "$this->bypass"

서명 우회는 일반적으로 `$this->bypass`로 작성됩니다.

`$this->bypass`는 3 개의 매개 변수를 허용합니다 : `$Condition`, `$ReasonShort`, 및 `$DefineOptions` (선택 과목).

`$Condition`의 진실성이 평가됩니다. True의 경우, 우회가은 트리거됩니다. False의 경우, 우회가은 트리거되지 않습니다. `$Condition`에는 일반적으로 요청을 차단해서는 안되는 조건을 평가하는 PHP 코드가 들어 있습니다.

우회가이 트리거되면, `$ReasonShort`가 "왜 차단이 되셨나요"필드에 표시됩니다.

`$DefineOptions`는 키/값 쌍을 포함하는 선택적 배열입니다. 요청 인스턴스와 관련된 구성 옵션을 정의하는 데 사용됩니다. 구성 옵션은 우회가이 트리거 될 때 적용됩니다.

`$this->bypass`는 우회가 트리거되면 true를, 그렇지 않으면 false를 반환합니다.

##### 6.5.2 "$this->dnsReverse"

IP 주소의 호스트 이름을 가져 오는 데 사용할 수 있습니다. 호스트 이름을 차단하는 모듈을 만들려면이, method가 유용 할 수 있습니다.

예 :
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

#### 6.6 모듈 변수

모듈은 자체 범위 내에서 실행되며 모듈에 정의 된 변수는 다른 모듈이나 상위 스크립트에 액세스 할 수 없습니다 (`$CIDRAM`배열에 저장되어 있지 않으면; 모듈 실행이 끝난 후에 다른 모든 것은 비워진다).

다음은 모듈에 유용한 몇 가지 일반적인 변수입니다 :

변수 | 설명
----|----
`$this->BlockInfo['DateTime']` | 현재 날짜와 시간.
`$this->BlockInfo['IPAddr']` | 현재 요청의 IP 주소.
`$this->BlockInfo['IPAddrResolved']` | 현재 요청에 대한 IP 주소가 6to4, Teredo, 또는 ISATAP 주소인 경우 해당 주소는 해당 IPv4 주소로 확인됩니다. 그렇지 않은 경우에는, 현재 요청에 대한 IP 주소가 됩니다.
`$this->BlockInfo['ScriptIdent']` | CIDRAM 스크립트 버전.
`$this->BlockInfo['Query']` | 현재 요청에 대한 쿼리입니다.
`$this->BlockInfo['Referrer']` | 현재 요청에 대한 리퍼러 (존재하는 경우).
`$this->BlockInfo['UA']` | 현재 요청에 대한 사용자 에이전트입니다 (user agent).
`$this->BlockInfo['UALC']` | 현재 요청에 대한 소문자의 사용자 에이전트입니다 (user agent).
`$this->BlockInfo['ReasonMessage']` | 현재 요청이 차단 된 경우 사용자/클라이언트에게 표시 할 메시지입니다.
`$this->BlockInfo['SignatureCount']` | 현재 요청에 대해 트리거 된 서명 수입니다.
`$this->BlockInfo['Signatures']` | 현재 요청에 대해 트리거 된 모든 서명에 대한 참조 정보.
`$this->BlockInfo['WhyReason']` | 현재 요청에 대해 트리거 된 모든 서명에 대한 참조 정보.
`$this->BlockInfo['Request_Method']` | 현재 요청의 요청 방법입니다.
`$this->BlockInfo['Protocol']` | 현재 요청의 프로토콜입니다.

---


### 7. <a name="SECTION7"></a>알려진 호환성 문제

다음 패키지 및 제품이 CIDRAM과 호환되지 않습니다.
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

CIDRAM과의 호환성을 보장하기 위해, 다음 패키지 및 제품에, 모듈을 사용할 수 있습니다.
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__
- __[Quic cloud](https://wordpress.org/support/topic/quic-dot-cloud-requires-all-ips-allowed/)__

*참조 : [호환성 차트](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 8. <a name="SECTION8"></a>자주 묻는 질문 (FAQ)

- ["서명"이란 무엇입니까?](#user-content-WHAT_IS_A_SIGNATURE)
- ["CIDR"이란 무엇입니까?](#user-content-WHAT_IS_A_CIDR)
- ["거짓 양성"는 무엇입니까?](#user-content-WHAT_IS_A_FALSE_POSITIVE)
- [CIDRAM는 나라 전체를 차단할 수 있습니까?](#user-content-BLOCK_ENTIRE_COUNTRIES)
- [서명은 얼마나 자주 업데이트됩니까?](#user-content-SIGNATURE_UPDATE_FREQUENCY)
- [CIDRAM을 사용하는 데 문제가 발생했지만 무엇을 해야할지 모르겠어요! 도와주세요!](#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [나는 CIDRAM 의해 웹 사이트에서 차단되어 있습니다! 도와주세요!](#user-content-BLOCKED_WHAT_TO_DO)
- [7.2보다 오래된 PHP 버전에서 CIDRAM v3~v4을 사용하고 싶습니다; 도울 수 있니?](#user-content-MINIMUM_PHP_VERSION_V3)
- [단일 CIDRAM 설치를 사용하여 여러 도메인을 보호 할 수 있습니까?](#user-content-PROTECT_MULTIPLE_DOMAINS)
- [나는 이것을 설치하거나 그것이 내 웹 사이트상에서 동작하는 것을 보장하는 시간을 보내고, 하고 싶지 않아; 그것을 할 수 있습니까? 나는 당신을 고용 할 수 있습니까?](#user-content-PAY_YOU_TO_DO_IT)
- [당신 또는 이 프로젝트의 모든 개발자는 고용 가능합니까?](#user-content-HIRE_FOR_PRIVATE_WORK)
- [나는 전문가의 변경 및 사용자 맞춤형 등이 필요합니다; 도울 수 있니?](#user-content-SPECIALIST_MODIFICATIONS)
- [나는 개발자, 웹 사이트 디자이너, 또는 프로그래머입니다. 이 프로젝트 관련 작업을 할 수 있습니까?](#user-content-ACCEPT_OR_OFFER_WORK)
- [나는 프로젝트에 공헌하고 싶다; 이것은 수 있습니까?](#user-content-WANT_TO_CONTRIBUTE)
- [Cron을 사용하여 자동으로 업데이트 할 수 있습니까?](#user-content-CRON_TO_UPDATE_AUTOMATICALLY)
- ["위반"이란 무엇입니까?](#user-content-WHAT_ARE_INFRACTIONS)
- [CIDRAM이 호스트 이름을 차단할 수 있습니까?](#user-content-BLOCK_HOSTNAMES)
- ["default_dns"에 사용할 수있는 항목은 무엇입니까?](#default_dns에-사용할-수있는-항목은-무엇입니까)
- [CIDRAM을 사용하여 웹 사이트 (예 : 이메일 서버, FTP, SSH, IRC, 등) 이외의 것을 보호 할 수 있습니까?](#user-content-PROTECT_OTHER_THINGS)
- [CDN 또는 캐싱 서비스를 사용하는 것과 동시에 CIDRAM을 사용하면 문제가 발생합니까?](#user-content-CDN_CACHING_PROBLEMS)
- [CIDRAM이 내 웹 사이트를 DDoS 공격으로부터 보호합니까?](#user-content-DDOS_ATTACKS)
- [모듈 또는 서명 파일이 업데이트 페이지를 통해 활성화되거나 비활성화되면, 구성에서 문자 또는 숫자로 정렬됩니다. 분류 방식을 변경할 수 있습니까?](#user-content-CHANGE_COMPONENT_SORT_ORDER)
- ["PDO DSN"은 무엇입니까? CIDRAM과 함께 PDO를 사용하려면 어떻게해야합니까?](#user-content-HOW_TO_USE_PDO)
- [CIDRAM이 cronjobs을 차단하고 있습니다. 문제를 해결하는 방법?](#user-content-BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>"서명"이란 무엇입니까?

CIDRAM의 맥락에서 "서명"이라 함은 지표/식별자 역할을하는 데이터이다. 우리는 그것을 사용하여 원하는 정보를 찾습니다 (일반적으로 IP 주소 또는 CIDR입니다). 종종 그것은 CIDRAM위한 어떤 명령을 포함 (응답하는 최선의 방법 등). CIDRAM의 전형적인 서명은 다음과 같습니다.

"서명 파일"의 경우 :

`1.2.3.4/32 Deny Generic`

"모듈"의 경우 :

```PHP
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*노트 : "서명 파일"에 대한 서명과, "모듈"에 대한 서명은, 동일한 것이 아닙니다.*

종종 (그러나 항상은 아니지만) 서명은 함께 묶어 "서명 섹션"을 형성합니다. 코멘트, 마크 업 및 관련 메타 데이터를 가진 경우가 종종 있습니다 (이것은 추가 문맥 및 추가 지침을 제공하는 데 사용할 수있다).

#### <a name="WHAT_IS_A_CIDR"></a>"CIDR"이란 무엇입니까?

"CIDR"은 "Classless Inter-Domain Routing"의 두문자어 입니다 *[[1](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9D%B4%EB%8D%94_(%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%82%B9)), [2](https://whatismyipaddress.com/cidr)]*. 이 두문자어 패키지의 이름의 일부로 사용됩니다 (CIDRAM). "CIDRAM"은 "Classless Inter-Domain Routing Access Manager"의 두문자어 입니다.

그러나 CIDRAM의 맥락에서 (예를 들어, 이 문서, CIDRAM 관한 논의에서, CIDRAM 언어 데이터에), "CIDR"또는 "CIDRs"이 언급 될 때마다, 우리가 의도 한 의미는 CIDR 표기법을 사용하여 표현 된 서브넷입니다. 이 목적은 우리의 의미를 분명히하기위한 것입니다 (서브넷이 여러 가지 방법으로 표현 될 수 있기 때문에). 따라서 CIDRAM은 "서브넷 액세스 관리자"로 간주 될 수 있습니다.

이 설명은 제공된 컨텍스트와 함께 모호성을 해결하는 데 도움이됩니다.

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>"거짓 양성"는 무엇입니까?

일반화 된 상황에서 쉽게 설명 조건의 상태를 테스트 할 때 결과를 참조 할 목적으로 용어 "거짓 양성"의 (*또는 : 위양성의 오류, 허위 보도;* 영어 : *false positive*; *false positive error*; *false alarm*) 의미는 결과는 "양성"의 것, 그러나 결과는 실수 (즉, 진실의 조건은 "양성/진실"로 간주됩니다, 그러나 정말 "음성/거짓"입니다). "거짓 양성"는 "우는 늑대"와 유사하다고 생각할 수 있습니다 (그 상태는 군 근처에 늑대가 있는지 여부이다, 진실 조건은 "거짓/음성"입니다 무리의 가까이에 늑대가 없기 때문입니다하지만 조건은 "진실/양성"로보고됩니다 목자가 "늑대! 늑대!"를 외쳤다 때문입니다) 또는 의료 검사와 유사 환자가 잘못 진단 된 경우.

몇 가지 관련 용어는 "진실 양성", "진실 음성"와 "거짓 음성"입니다. 이러한 용어가 나타내는 의미 : "진실 양성"의 의미는 테스트 결과와 진실 조건이 진실입니다 (즉, "양성"입니다). "진실 음성"의 의미는 테스트 결과와 진실 조건이 거짓 (즉, "음성"입니다). "진실 양성"과 "진실 음성"는 "올바른 추론"로 간주됩니다. "거짓 양성"의 반대는 "거짓 음성"입니다. "거짓 음성"의 의미는 테스트 결과가 거짓입니다 (즉, "음성"입니다) 하지만 진실의 조건이 정말 진실입니다 (즉, "양성"입니다); 두 테스트 결과와 진실 인 조건이 "진실/양성" 해야한다 것입니다.

CIDRAM의 맥락에서 이러한 용어는 CIDRAM 서명과 그들이 차단하는 것을 말합니다. CIDRAM가 잘못 IP 주소를 차단하면 (예를 들어, 부정확 한 서명 구식의 서명 등에 의한), 우리는이 이벤트 "거짓 양성"를 호출합니다. CIDRAM가 IP 주소를 차단할 수 없는 경우 (예를 들어, 예상치 못한 위협 서명 누락 등으로 인한), 우리는이 이벤트 "부재 감지"를 호출합니다 ("거짓 음성" 아날로그입니다).

이것은 다음 표에 요약 할 수 있습니다.

&nbsp; | IP 주소를 차단 필요가 CIDRAM 없습니다 | IP 주소를 CIDRAM 차단해야합니다
---|---|---
IP 주소를 CIDRAM 차단하지 않습니다 | 진실 음성 (올바른 추론) | 놓친 (그것은 "거짓 음성"와 같습니다)
IP 주소를 CIDRAM 차단합니다 | __거짓 양성__ | 진실 양성 (올바른 추론)

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>CIDRAM는 나라 전체를 차단할 수 있습니까?

예. 가장 쉬운 방법은 BGPView 모듈을 설치하고 필요에 따라 구성하는 것입니다.

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>서명은 얼마나 자주 업데이트됩니까?

업 데이트 빈도는 서명 파일에 따라 다릅니다. CIDRAM 서명 파일의 모든 메인테이너가 자주 업 데이트를 시도하지만, 우리의 여러분에게는 그 밖에도 다양한 노력이있어, 우리는 프로젝트 외부에서 생활하고 있으며, 아무도 재정적으로 보상되지 않는, 따라서 정확한 업 데이트 일정은 보장되지 않습니다. 일반적으로 충분한 시간이 있으면 서명이 업 데이트됩니다. 메인테이너는 필요성과 범위 사이의 변화의 빈도에 따라 우선 순위를 내려고한다. 당신이 뭔가를 제공 할 수 있다면, 원조는 항상 높게 평가됩니다.

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>CIDRAM을 사용하는 데 문제가 발생했지만 무엇을 해야할지 모르겠어요! 도와주세요!

- 당신은 최신 소프트웨어 버전을 사용하고 있습니까? 당신은 최신 서명 파일 버전을 사용하고 있습니까? 그렇지 않은 경우, 먼저 업 데이트하십시오. 문제가 해결되지 여부를 확인하십시오. 그것이 계속되면 읽어보십시오.
- 당신은 문서를 확인 했습니까? 만약 그렇지 않으면, 그렇지하십시오. 문서를 사용하여 문제를 해결할 수 없는 경우, 계속 읽어보십시오.
- **[이슈 페이지를](https://github.com/CIDRAM/CIDRAM/issues)** 확인 했습니까? 문제가 이전에 언급되어 있는지 확인하십시오. 제안, 아이디어, 솔루션이 제공되었는지 여부를 확인하십시오.
- 문제가 해결되지 않으면 알려 주시기 바랍니다. 이슈 페이지에서 토론을 창조한다.

#### <a name="BLOCKED_WHAT_TO_DO"></a>나는 CIDRAM 의해 웹 사이트에서 차단되어 있습니다! 도와주세요!

CIDRAM는 웹 사이트 소유자가 원하지 않는 트래픽을 차단하는 수단을 제공합니다, 하지만 웹 사이트 소유자는 그 사용 방법을 결정해야합니다. 서명 파일에 오류 검출이있는 경우, 정정을 할 수, 그러나 특정 웹 사이트에서 차단 해제되어 관해서, 당신은 웹 사이트 소유자에게 문의해야합니다. 수정이 이루어지면 업데이트가 필요합니다. 그렇지 않으면 문제를 해결하는 것은 그들의 책임입니다. 맞춤화와 개인 선택은 전적으로 우리가 통제 할 수 없는 것입니다.

#### <a name="MINIMUM_PHP_VERSION_V3"></a>7.2보다 오래된 PHP 버전에서 CIDRAM v3~v4을 사용하고 싶습니다; 도울 수 있니?

아니오. PHP≥7.2은 CIDRAM v3~v4의 최소 요구 사항입니다.

*참조 : [호환성 차트](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>단일 CIDRAM 설치를 사용하여 여러 도메인을 보호 할 수 있습니까?

예. CIDRAM 설치는 특정 도메인에 국한되지 않습니다, 따라서 여러 도메인을 보호하기 위해 사용할 수 있습니다. 일반적으로, 하나의 도메인 만 보호 설치 우리는 "단일 도메인 설치"이 라고 부릅니다에서 여러 도메인을 보호하는 설치 우리는 "멀티 도메인 설치"이 라고 있습니다. 다중 도메인 설치를 사용하는 경우 다른 도메인에 다른 서명 파일 세트를 사용할 필요가 있거나 다른 도메인에 CIDRAM을 다른 설정해야합니다 이것을 할 수 있습니다. 설정 파일을로드 한 후 (`config.yml`), CIDRAM 요청 된 도메인의 "구성 재정 파일"의 존재를 확인합니다 (`xn--hq1bngz0pl7nd2aqft27a.tld.config.yml`), 그리고 발견 된 경우, 구성 재정 파일에 의해 정의 된 구성 값은 설정 파일에 의해 정의 된 구성 값이 아니라 실행 인스턴스에 사용됩니다. 구성 재정 파일은 설정 파일과 동일합니다. 귀하의 재량에 따라 CIDRAM에서 사용할 수있는 모든 구성 지시문 전체 또는 필요한 하위 섹션을 포함 할 수 있습니다. 구성 재정 파일은 그들이 의도하는 도메인에 따라 지정됩니다 (그래서 예를 들면, 도메인 `https://www.some-domain.tld/` 컨피규레이션 재정 파일이 필요한 경우, 구성 재정 파일의 이름은 `some-domain.tld.config.yml` 할 필요가 있습니다. 일반 구성 파일과 동일한 위치에 보관해야합니다). 도메인 이름은 `HTTP_HOST` 에서옵니다. "www"는 무시됩니다.

#### <a name="PAY_YOU_TO_DO_IT"></a>나는 이것을 설치하거나 그것이 내 웹 사이트상에서 동작하는 것을 보장하는 시간을 보내고, 하고 싶지 않아; 그것을 할 수 있습니까? 나는 당신을 고용 할 수 있습니까?

아마. 이는 사례별로 검토되고 있습니다. 당신의 요구로 제공할 수 있는 것을 가르쳐주세요. 우리가 도울 수 있는지를 가르쳐주고 있습니다.

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>당신 또는 이 프로젝트의 모든 개발자는 고용 가능합니까?

*위를 참조하십시오.*

#### <a name="SPECIALIST_MODIFICATIONS"></a>나는 전문가의 변경 및 사용자 맞춤형 등이 필요합니다; 도울 수 있니?

*위를 참조하십시오.*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>나는 개발자, 웹 사이트 디자이너, 또는 프로그래머입니다. 이 프로젝트 관련 작업을 할 수 있습니까?

예. 우리의 라이센스는이를 금지하지 않습니다.

#### <a name="WANT_TO_CONTRIBUTE"></a>나는 프로젝트에 공헌하고 싶다; 이것은 수 있습니까?

예. 프로젝트에 기여 환영합니다. 자세한 내용은 "CONTRIBUTING.md"를 참조하십시오.

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>Cron을 사용하여 자동으로 업데이트 할 수 있습니까?

예. 외부 스크립트를 통해 업데이트 페이지와 상호 작용하기위한 프런트 엔드에 API가 내장되어 있습니다. 별도의 스크립트 인 "[Cronable](https://github.com/Maikuolan/Cronable)"을 사용할 수 있습니다. Cron 관리자 또는 Cron 스케줄러가이 사용할 수 있습니다, 패키지 및 기타 지원되는 패키지를 자동으로 업데이트하는 데 사용할 수 있습니다 (이 스크립트는 자체 문서를 제공합니다.).

#### <a name="WHAT_ARE_INFRACTIONS"></a>"위반"이란 무엇입니까?

"서명수" 및 "위반"은 모두 특정 요청 중에 트리거 된 서명의 심각도 및 수와 서명 파일, 모듈, 보조 규칙, 등으로 인한 것인지 여부에 관계없이 관련됩니다. 그러나, "서명수"는 해당 특정 요청에 대해서만 지속하지만, "위반"은 `default_tracktime`에 의해 결정된 만큼 많은 요청에 대해 지속할 수 있습니다.

이렇게 하면 충분한 수의 위반으로 요청이 차단될 때 동일한 소스의 후속 요청도 차단될 수 있습니다.

#### <a name="BLOCK_HOSTNAMES"></a>CIDRAM이 호스트 이름을 차단할 수 있습니까?

예. 이는 보조 규칙 또는 사용자 정의 모듈을 생성하여 달성할 수 있습니다.

![호스트 이름 차단을 위한 보조 규칙](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>"default_dns"에 사용할 수있는 항목은 무엇입니까?

제안을 찾고있는 경우, [public-dns.info](https://public-dns.info/)및 [OpenNIC](https://servers.opennic.org/)는 알려진 공개 DNS 서버의 광범위한 목록을 제공합니다. 또는 아래 표를 참조하십시오 :

IP | 운영자
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

*노트 : 본인은 모든 DNS 서비스의 개인, 열거 되든 그렇지 않든, 정보 보호 관행, 보안, 효능 또는 신뢰성과 관련하여 어떠한 보증이나 보장도하지 않습니다. 그들에 대한 결정을 내릴 때 자신의 연구를하십시오.*

#### <a name="PROTECT_OTHER_THINGS"></a>CIDRAM을 사용하여 웹 사이트 (예 : 이메일 서버, FTP, SSH, IRC, 등) 이외의 것을 보호 할 수 있습니까?

합법적으로, 당신은 이것을 할 수 있습니다. 기술적으로나 실질적으로, 당신은해서는 안됩니다. 우리의 라이센스는 CIDRAM을 구현하는 기술을 제한하지 않습니다. 그러나, CIDRAM은 WAF (웹 응용 프로그램 방화벽)이며 웹 사이트를 보호하기위한 것입니다. 다른 기술을 염두에두고 설계되지 않았기 때문에 다른 기술에 대한 효과적이거나 신뢰할 수있는 보호를 제공하지는 않습니다. 구현이 어려울 가능성이 높으며, 가양 성 및 누락 감지 위험이 매우 높습니다.

#### <a name="CDN_CACHING_PROBLEMS"></a>CDN 또는 캐싱 서비스를 사용하는 것과 동시에 CIDRAM을 사용하면 문제가 발생합니까?

아마도. 이것은 서비스와 사용 방법에 따라 달라질 수 있습니다. 일반적으로, 정적 애셋 만 캐싱하는 경우 아무 문제가 없어야합니다 (정적 애셋이란 시간이 지나도 변하지 않는 것을 의미합니다; 예 : 이미지, CSS, 등). 그러나, 일반적으로 요청에 따라 동적으로 생성되는 데이터를 캐싱하거나 POST 요청의 결과를 캐싱 할 때 문제가 발생할 수 있습니다 (이것은 귀하의 웹 사이트와 그 환경을 정적으로 렌더링 할 것이며, CIDRAM은 정적 환경에서 의미있는 이점을 제공하지 않을 것입니다). 사용중인 CDN 또는 캐싱 서비스에 따라, CIDRAM에 대한 특정 구성 요구 사항이있을 수 있습니다 (귀하의 필요에 맞게 CIDRAM이 올바르게 구성되었는지 확인하십시오). 잘못된 구성은 심각한 문제를 일으킬 수 있습니다.

#### <a name="DDOS_ATTACKS"></a>CIDRAM이 내 웹 사이트를 DDoS 공격으로부터 보호합니까?

짧은 대답 : 아니오.

더 자세한 대답 : CIDRAM은 원하지 않는 트래픽이 웹 사이트 (웹 사이트의 대역폭 비용 절감) 및 하드웨어에 (예를 들어, 요청을 처리하고 제공하는 서버 기능) 미칠 수있는 영향을 줄이는 데 도움이됩니다. 또한 원하지 않는 트래픽과 관련된 여러 가지 잠재적 인 부정적인 영향을 줄일 수 있습니다. 그러나이 질문을 이해하기 위해서는 반드시 기억해야 할 중요한 두 가지 사항이 있습니다. 1. CIDRAM은 PHP 패키지이므로 PHP가 설치된 시스템에서 작동합니다. 이 때문에 CIDRAM은 서버가 이미 요청을 수신 한 후에 만 요청을 인식하고 차단할 수 있습니다. 2. 효과적인 DDoS 완화는 요청이 DDoS 공격의 대상인 서버에 도달하기 전에 요청을 필터링해야합니다. DDoS 공격은 대상 서버에 도달하기 전에 공격과 관련된 트래픽을 중단 또는 재 라우팅 할 수있는 솔루션에 의해 탐지되고 완화되어야합니다.

이것은 전용 "온 프레미스" 하드웨어 솔루션, 전용 DDoS 완화 서비스와 같은 클라우드 기반 솔루션, DDoS 방지 네트워크를 통해 도메인의 DNS 라우팅, 클라우드 기반 필터링, 또는 이들의 조합 일 수있다를 사용하여 구현할 수 있습니다. 어쨌든, 이 주제는 단순한 단락 또는 2 단으로 철저히 설명하기에는 너무 복잡합니다. 이것이 당신이 추구하고자하는 주제라면 더 깊은 연구를하는 것이 좋습니다. DDoS 공격의 진정한 본질이 제대로 이해되면이 대답이 더욱 의미가 있습니다.

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>모듈 또는 서명 파일이 업데이트 페이지를 통해 활성화되거나 비활성화되면, 구성에서 문자 또는 숫자로 정렬됩니다. 분류 방식을 변경할 수 있습니까?

예. 특정 순서로 실행할 파일이 필요할 때, 그들의 이름 앞에 설정 지시자가있는 임의의 데이터를 추가 할 수있다 (콜론을 사용하여이 데이터와 이름을 구분하십시오). 이후에 업데이트 페이지가 파일을 다시 정렬하면, 추가 된 임의의 데이터가 정렬 순서에 영향을줍니다. 이렇게하면 파일이 원하는 순서대로 실행됩니다, 그 중 하나의 이름을 바꿀 필요가 없습니다.

예를 들어, 다음과 같이 나열된 파일이있는 구성 지시문을 가정합니다 :

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

`file3.php`를 먼저 실행시키고 싶다면, 파일 이름 앞에 `aaa:`와 같은 것을 추가 할 수 있습니다 :

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

그런 다음 새 파일 `file6.php`가 활성화되면, 업데이트 페이지에서 모두 다시 정렬하면 다음과 같이 끝납니다 :

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

파일이 비활성화 될 때와 동일한 상황입니다. 반대로, 파일을 마지막으로 실행하려면, 파일 이름 앞에 `zzz:`와 같은 것을 추가 할 수 있습니다. 어떤 경우이든 해당 파일의 이름을 바꿀 필요가 없습니다.

#### <a name="HOW_TO_USE_PDO"></a>"PDO DSN"은 무엇입니까? CIDRAM과 함께 PDO를 사용하려면 어떻게해야합니까?

"PDO"는 "[PHP Data Objects](https://www.php.net/manual/en/intro.pdo.php)"의 약어입니다 (PHP 데이터 객체). PHP가 다양한 PHP 응용 프로그램에서 일반적으로 사용하는 일부 데이터베이스 시스템에 연결할 수 있도록 인터페이스를 제공합니다.

"DSN"은 "[data source name](https://en.wikipedia.org/wiki/Data_source_name)"의 약어입니다 (데이터 소스 이름). "PDO DSN"은 PDO가 데이터베이스에 연결하는 방법을 설명합니다.

CIDRAM은 캐싱 목적으로 PDO 을 활용할 수 있는 옵션을 제공합니. 이 기능이 제대로 작동하려면, CIDRAM을 적절히 구성하고 (따라서 PDO를 사용하도록 설정), 사용할 CIDRAM 용 데이터베이스를 새로 작성하고 (CIDRAM 용 데이터베이스를 아직 염두에 두지 않은 경우), 그런 아래 설명된 구조에 따라 데이터베이스에 새 테이블을 작성하십시오.

데이터베이스 연결이 성공한 경우, 그러나 필요한 테이블이 존재하지 않습니다, 자동 생성이 시도됩니다. 그러나 이 동작은 광범위하게 테스트 되지 않았으며 성공을 보장할 수 없습니다.

물론 이것은 실제로 CIDRAM이 PDO 을 사용하도록 하려는 경우에만 적용됩니다. 플랫 파일 캐싱 (기본 구성에 따라) 또는 제공된 다양한 캐싱 옵션을 사용하기에 충분하다면, 데이터베이스, 테이블 등을 설정하는 데 어려움을 겪을 필요가 없습니다.

아래 설명된 구조는 "cidram"을 데이터베이스 이름으로 사용하지만, DSN 구성에 동일한 이름이 복제되는 한 데이터베이스에 원하는 이름을 사용할 수 있습니다.

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

CIDRAM의 `pdo_dsn` 설정 지시어는 아래와 같이 설정해야합니다.

```
사용되는 데이터베이스 드라이버에 따라...
├─4d (경고 : 실험적, 테스트 되지 않은, 권장하지 않음!)
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └데이터베이스를 찾기 위해 연결할 호스트입니다.
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └사용할 데이터베이스의 이름입니다.
│                │              │
│                │              └호스트에 연결할 포트 번호입니다.
│                │
│                └데이터베이스를 찾기 위해 연결할 호스트입니다.
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └사용할 데이터베이스의 이름입니다.
│    │          │
│    │          └데이터베이스를 찾기 위해 연결할 호스트입니다.
│    │
│    └가능한 값 : "mssql", "sybase", "dblib".
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├로컬 데이터베이스 파일의 경로일 수 있습니다.
│                    │
│                    ├호스트 및 포트 번호와 연결할 수 있습니다.
│                    │
│                    └이것을 사용하려면 Firebird 설명서를 참조하십시오.
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └연결할 카탈로그 된 데이터베이스입니다.
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └연결할 카탈로그 된 데이터베이스입니다.
├─mysql (가장 추천!)
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └호스트에 연결할 포트 번호입니다.
│                 │            │
│                 │            └데이터베이스를 찾기 위해 연결할 호스트입니다.
│                 │
│                 └사용할 데이터베이스의 이름입니다.
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├카탈로그 된 특정 데이터베이스를 참조 할 수 있습니다.
│               │
│               ├호스트 및 포트 번호와 연결할 수 있습니다.
│               │
│               └이것을 사용하려면 Oracle 설명서를 참조하십시오.
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├카탈로그 된 특정 데이터베이스를 참조 할 수 있습니다.
│         │
│         ├호스트 및 포트 번호와 연결할 수 있습니다.
│         │
│         └이것을 사용하려면 ODBC/DB2 설명서를 참조하십시오.
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └사용할 데이터베이스의 이름입니다.
│               │              │
│               │              └호스트에 연결할 포트 번호입니다.
│               │
│               └데이터베이스를 찾기 위해 연결할 호스트입니다.
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └사용할 로컬 데이터베이스 파일의 경로입니다.
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └사용할 데이터베이스의 이름입니다.
                   │         │
                   │         └호스트에 연결할 포트 번호입니다.
                   │
                   └데이터베이스를 찾기 위해 연결할 호스트입니다.
```

DSN의 특정 부분에 무엇을 사용해야할지 확실하지 않은 경우, 아무것도 변경하지 않고 그대로 작동하는지 먼저 확인하십시오.

`pdo_username` 및 `pdo_password` 는 데이터베이스에 대해 선택한 사용자 이름 및 비밀번호와 같아야합니다.

#### <a name="BLOCK_CRON"></a>CIDRAM이 cronjobs을 차단하고 있습니다. 문제를 해결하는 방법?

cronjobs에 특정 파일을 사용하는 경우, 일반 사용자 요청 중에 해당 파일을 호출 할 필요가없는 경우 (즉, 크론 작업의 맥락 밖에서), 이 문제를 해결하는 가장 간단한 방법은 cronjobs 동안 CIDRAM이 전혀 실행되지 않도록하는 것입니다 (즉, cronjob 처리를 담당하는 파일에 CIDRAM을 연결하지 마십시오).

또는 불가능한 경우, cron 서버의 IP 주소가 비교적 일관되고 예측 가능한 경우, cron 서버의 IP 주소를 허용 목록에 추가 할 수 있습니다. 사용자 정의 서명 파일에서 화이트리스트 서명을 작성하여이를 수행 할 수 있습니다 또는 보조 규칙을 작성하여. cron 서버의 IP 주소가 정기적으로 변경되고 특별히 예측할 수 없는 경우, 그럼에도 불구하고 동일한 특정 네트워크 내에 남아 있습니다, 먼저 `ignore.dat`파일에 차단을 담당하는 서명 섹션의 이름을 나열 해 볼 수 있습니다.

당신이 그 아이디어를 모두 시도했지만 그들 중 누구도 당신을 위해 일하지 않았다면, 또는 수행 방법을 알아내는 데 도움이 필요한 경우, CIDRAM issues 페이지에서 새 issue를 만들어 도움을 요청할 수 있습니다.

---


### 9. <a name="SECTION9"></a>법률 정보

#### 9.0 섹션 프리앰블

이 절은 패키지의 사용 및 구현에 관한 가능한 법적 고려 사항을 설명하고 기본 관련 정보를 제공하기위한 것입니다. 이 정보는 자국에서있을 수있는 법적 요구 사항 때문에 일부 사용자에게 중요 할 수 있습니다. 일부 사용자는이 정보에 따라 웹 사이트 정책을 조정해야 할 수도 있습니다.

무엇보다, 나는 (패키지 저자)가 변호사 또는 자격을 갖춘 법률 전문가가 아님을 알아 주시기 바랍니다. 따라서, 나는 법률 자문을 제공 할 자격이 없다. 또한 법률 요건은 국가 및 관할 구역마다 다를 수 있습니다. 이러한 다양한 법적 요구 사항도 때로는 충돌 할 수 있습니다 (예를 들면 : [개인 정보 보호 권리와](https://ko.wikipedia.org/wiki/%EC%A0%95%EB%B3%B4%ED%86%B5%EC%8B%A0%EB%A7%9D_%EC%9D%B4%EC%9A%A9%EC%B4%89%EC%A7%84_%EB%B0%8F_%EC%A0%95%EB%B3%B4%EB%B3%B4%ED%98%B8_%EB%93%B1%EC%97%90_%EA%B4%80%ED%95%9C_%EB%B2%95%EB%A5%A0#%EA%B0%9C%EC%9D%B8%EC%A0%95%EB%B3%B4%EC%9D%98_%EB%B3%B4%ED%98%B8) [잊혀진 권리를](https://namu.wiki/w/%EC%9E%8A%ED%9E%90%20%EA%B6%8C%EB%A6%AC) 선호하는 국가들, 확장 된 데이터 보존을 선호하는 국가들에 비해). 패키지에 대한 액세스가 특정 국가 또는 관할 지역에만 국한되지, 않으므로 패키지 사용자베이스가 지리적으로 다양 할 수 있습니다. 이 점을 고려해 볼 때, 나는 모든 사람에게 "법적으로 준수하는"것이 무엇을 의미 하는지를 말할 입장이 아닙니다. 그러나 여기에있는 정보가 패키지의 맥락에서 법적으로 준수하기 위해해야 할 일을 스스로 결정하는 데 도움이되기를 바랍니다. 의심의 여지가 있거나 법률적인 관점에서 추가 도움과 조언이 필요한 경우 자격을 갖춘 법률 전문가와상의하는 것이 좋습니다.

#### 9.1 책임

패키지 라이센스에 의해 이미 명시된 바와 같이, 패키지에는 어떠한 보증도 없습니다. 여기에는 모든 책임 범위가 포함되지만 이에 국한되지는 않습니다. 이 패키지는 편리함을 위해 제공되며, 유용 할 것으로 기대되며, 귀하에게 도움이 될 것입니다. 그러나, 당신이 패키지를 사용하든, 당신 자신의 선택입니다. 당신은 패키지를 사용하도록 강요 당하지 않지만, 그렇게 할 때, 당신은 그 결정에 대한 책임이 있습니다. 본인 및 기타 패키지 제공자는 귀하가 직접, 간접적으로, 암시 적으로, 또는 다른 방법으로 관계없이, 결정한 결과에 대해 법적 책임을지지 않습니다.

#### 9.2 제 3 자

정확한 구성과 구현에 따라, 패키지는 경우에 따라 제 3 자와 통신하고 정보를 공유 할 수 있습니다. 이 정보는 일부 관할 구역에 따라 일부 상황에서 "[개인 식별 정보](https://ko.wikipedia.org/wiki/%EA%B0%9C%EC%9D%B8%EC%A0%95%EB%B3%B4)"(PII)로 정의 될 수 있습니다.

이 정보가 이러한 제 3 자에 의해 어떻게 사용될 수 있는지는 제 3 자에 의해 설정된 다양한 정책의 적용을받습니다. 설명서는 이러한 요점을 다루지 않습니다. 그러나 이러한 모든 경우에 이러한 제 3 자와의 정보 공유를 비활성화 할 수 있습니다. 그러한 모든 경우, 이를 사용하기로 선택한 경우, 이러한 제 3 자의 개인 정보, 보안 및 PII 사용과 관련하여 우려 할 사항을 조사하는 것은 귀하의 책임입니다. 의심스러운 점이 있거나 PII와 관련하여 이러한 제 3 자의 행위에 만족하지 않는 경우, 이러한 제 3 자와의 모든 정보 공유를 비활성화하는 것이 가장 좋습니다.

투명성을 목적으로, 공유되는 정보의 유형은 아래에 설명되어 있습니다.

##### 9.2.0 호스트 이름 조회

호스트 이름으로 작업하도록 의도 된 기능 또는 모듈을 사용하는 경우 (예를 들어, "위험한 호스트 차단 모듈", "tor project exit nodes block module", "검색 엔진 검증"), CIDRAM은 인바운드 요청의 호스트 이름을 어떻게 든 얻을 수 있어야합니다. 일반적으로 DNS 서버에서 인바운드 요청의 IP 주소 호스트 이름을 요청하거나 CIDRAM이 설치된 시스템에서 제공하는 기능을 통해 정보를 요청하여이 작업을 수행합니다 (이것은 일반적으로 "호스트 이름 조회"로 알려져 있습니다). 기본적으로 정의 된 DNS 서버는 [Google DNS](https://dns.google.com/) 서비스에 속합니다 (그러나 구성을 통해 쉽게 변경할 수 있음). 전달 된 정확한 서비스는 구성 할 수 있으며 패키지를 구성하는 방법에 따라 다릅니다. CIDRAM이 설치된 시스템에서 제공하는 기능을 사용하는 경우 시스템 관리자에게 문의하여 호스트 이름 조회에서 사용하는 경로를 확인해야합니다. 영향을받는 모듈을 피하거나 필요에 따라 패키지 구성을 수정하여 CIDRAM에서 호스트 이름 조회를 방지 할 수 있습니다.

*관련 설정 지시어 :*
- `general` -> `allow_gethostbyaddr_lookup`
- `general` -> `default_dns`
- `general` -> `force_hostname_lookup`
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.1 검색 엔진 검증 및 소셜 미디어 검증

이러한 구성 지시문을 사용하면, CIDRAM은 "순방향 DNS 조회"를 수행하여 검색 엔진 및 소셜 미디어에서 발생했다고 추정되는 요청의 진위 여부를 확인합니다. 이렇게하기 위해 [Google DNS](https://dns.google.com/) 서비스를 사용하여 이러한 인바운드 요청의 호스트 이름에서 IP 주소를 확인합니다 (이 프로세스에서 이러한 인바운드 요청의 호스트 이름은 서비스와 공유됩니다).

*관련 설정 지시어 :*
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.2 CAPTCHA

CIDRAM은 hCaptcha를 지원합니다. 올바르게 작동하려면 API 키가 필요합니다. 기본적으로 비활성화되어 있지만 필요한 API 키를 구성하여 활성화 할 수 있습니다. 활성화되면 서비스와 CIDRAM 또는 사용자 브라우저 간에 통신이 발생할 수 있습니다. 여기에는 사용자의 IP 주소, 사용자 에이전트, 운영 체제 및 요청에 사용할 수 있는 기타 세부 정보와 같은 정보 통신이 포함될 수 있습니다.

##### 9.2.3 STOP FORUM SPAM

[Stop Forum Spam](https://www.stopforumspam.com/)는 무료이며 환상적인 서비스입니다. 스팸 발송자로부터 포럼, 블로그 및 웹 사이트를 보호하는 데 도움이 될 수 있습니다. 이렇게하기 위해 알려진 스팸 발송자 데이터베이스와 IP 주소, 사용자 이름 또는 이메일 주소가 데이터베이스에 있는지 여부를 확인하는 데 활용할 수있는 API를 제공합니다.

CIDRAM은 인바운드 요청의 IP 주소가 의심되는 스팸 발송자에 속하는지 여부를 확인하는 선택적 모듈을 제공합니다. 모듈이 설치되고 활성화되면, 사용자 IP 주소는 모듈의 구성 및 의도된 목적에 따라 서비스와 공유될 수 있습니다.

##### 9.2.4 ABUSEIPDB

CIDRAM은 [AbuseIPDB](https://www.abuseipdb.com/) API를 사용하여 까다로운 IP 주소를 차단하는 모듈을 제공합니다. 모듈이 설치되고 활성화되면, 사용자 IP 주소는 모듈의 구성 및 의도된 목적에 따라 서비스와 공유될 수 있습니다.

##### 9.2.5 BGPVIEW, IP-API

CIDRAM은 [BGPView](https://bgpview.io/) API와 [IP-API](https://ip-api.com/) API를 사용하여 ASN 및 국가 코드 조회를 수행하는 선택적 모듈을 제공합니다. 이러한 조회는 ASN 또는 출신 국가를 기준으로 요청을 차단하거나 허용하는 기능을 제공합니다. 모듈이 설치되고 활성화되면, 사용자 IP 주소는 모듈의 구성 및 의도된 목적에 따라 서비스와 공유될 수 있습니다.

##### 9.2.6 PROJECT HONEYPOT

CIDRAM은 [Project Honeypot](https://www.projecthoneypot.org/) API를 사용하여 까다로운 IP 주소를 차단하는 모듈을 제공합니다. 모듈이 설치되고 활성화되면, 사용자 IP 주소는 모듈의 구성 및 의도된 목적에 따라 서비스와 공유될 수 있습니다.

#### 9.3 로깅

로깅은 여러 가지 이유로 CIDRAM의 중요한 부분입니다. 로깅 차단 이벤트가 없으면 오탐 (false positive)이 발생하면이를 진단하고 해결하기 어려울 수 있습니다. 로깅 블록 이벤트가 없으면 CIDRAM이 얼마나 효과적으로 수행되는지를 확인하기 어려울 수 있습니다. 그것의 부족을 확인하는 것은 어려울 수 있으며 의도 한대로 기능을 계속 수행하려면 구성이나 서명에 어떤 변경이 필요할 수 있습니다. 어쨌든 로깅은 일부 사용자가 원하지 않는 경우도 있으며 전체적으로 선택 사항입니다. CIDRAM에서 로깅은 기본적으로 사용되지 않습니다. 이를 사용하려면 CIDRAM을 적절히 구성해야합니다.

또한, 관할권 및 구현 컨텍스트에 따라 (예 : 당신이 개인으로서 또는 기업체로서 및 상업적 또는 비상업적 기반 여부 운영되고 있는지 여부), 로깅의 법적인 허용이 달라질 수 있습니다 (예 : 로깅의 할 수있는 정보의 유형, 기간 및 상황). 따라서, 이 섹션을주의 깊게 읽는 것이 유용 할 수 있습니다.

CIDRAM이 수행 할 수있는 로깅에는 여러 유형이 있습니다. 서로 다른 유형의 로깅에는 여러 가지 다른 유형의 정보가 포함됩니다.

##### 9.3.0 블록 이벤트

CIDRAM에서의 주요 로깅 유형은 "블록 이벤트"와 관련이 있습니다. 이 유형의 로깅은 CIDRAM이 요청을 차단하는시기와 관련이 있습니다. 그것은 세 가지 다른 형식으로 제공 될 수 있습니다 :
- 사람이 읽을 수있는 로그 파일.
- Apache 스타일의 로그 파일.
- 직렬화 된 로그 파일.

블록 이벤트 로그 항목은 일반적으로 다음과 같습니다 (예로서) :

```
신분증 : 1234
스크립트 버전 : CIDRAM v1.6.0
일·월·년·시간 : Day, dd Mon 20xx hh:ii:ss +0000
IP 주소 : x.x.x.x
호스트 이름 : dns.hostname.tld
서명수 : 1
서명 참조 : x.x.x.x/xx
왜 차단이 되셨나요 : 클라우드 서비스 ("네트워크 이름", Lxx:Fx, [XX])!
사용자 에이전트 : Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
URI 재구성 된 : https://your-site.tld/index.php
CAPTCHA의 상태 : 온.
```

Apache 스타일의 로그 파일에 기록하면, 다음과 같이 보입니다 :

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

로깅 된 블록 이벤트는 일반적으로 다음 정보를 포함합니다 :
- 블록 이벤트를 참조하는 ID 번호입니다.
- 현재 사용중인 CIDRAM의 버전입니다.
- 블록 이벤트가 발생한 날짜와 시간입니다.
- 차단 된 요청의 IP 주소입니다.
- 차단 된 요청의 IP 주소의 호스트 이름 (유효한 때).
- 요청에 의해 트리거 된 서명 수입니다.
- 트리거 된 서명 참조.
- 블록 이벤트의 이유 및 일부 관련 디버그 정보.
- 차단 된 요청의 사용자 에이전트 (즉, how요청 엔터티가 요청에 자신을 식별했습니다).
- 원래 요청 된 자원에 대한 식별자의 재구성.
- 현재 요청에 대한 CAPTCHA 상태 (관련성이있는 경우).

*다음 세 가지 형식 각각에 대해 이러한 유형의 로깅을 담당하는 구성 지시문입니다.*
- `logging` -> `apache_style_log`
- `logging` -> `serialised_log`
- `logging` -> `standard_log`

이러한 지시문을 비워두면이, 유형의 로깅은 비활성화 된 상태로 유지됩니다.

##### 9.3.1 CAPTCHA 로깅

이 유형의 로깅은 CAPTCHA 인스턴스와 관련이 있으며 사용자가 CAPTCHA 인스턴스를 완료하려고 할 때만 발생합니다.

CAPTCHA 로그 항목에는 CAPTCHA 인스턴스를 완료하려는 사용자의 IP 주소, 시도가 발생한 날짜 및 시간 및 CAPTCHA 상태가 들어 있습니다. CAPTCHA 로그 항목은 일반적으로 다음과 같이 표시됩니다 (예로서) :

```
IP 주소 : x.x.x.x - 일·월·년·시간 : Day, dd Mon 20xx hh:ii:ss +0000 - CAPTCHA의 상태 : 합격!
```

*CAPTCHA 로깅을 담당하는 구성 지시문 :*
- `hcaptcha` -> `hcaptcha_log`

##### 9.3.2 프론트 엔드 로깅

이 로깅은 프런트 엔드 로그인 시도와 관련이 있습니다. 사용자가 프런트 엔드에 로그인을 시도 할 때 및 프런트 엔드 액세스가 활성화 된 경우에만 발생합니다.

프런트 엔드 로그 항목에는 로그인을 시도하는 사용자의 IP 주소, 시도가 발생한 날짜와 시간 및 시도의 결과가 포함됩니다 (로그인 성공 또는 로그인 실패). 프론트 엔드 로그 항목은 일반적으로 다음과 같이 표시됩니다 (예로서) :

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - 로그인 했습니다.
```

*프런트 엔드 로깅을 담당하는 구성 지시문 :*
- `frontend` -> `frontend_log`

##### 9.3.3 로그 회전

일정 기간 후에 로그를 제거하려고 할 수 있습니다, 또는 법에 따라 그렇게해야 할 수도 있습니다 (즉, 로그를 보관하는 것이 법적으로 허용되는 시간은 법률에 의해 제한 될 수 있습니다). 로그 파일의 이름에 날짜/시간 표시자를 (예를 들어, `{yyyy}-{mm}-{dd}.log`) 포함하고 (패키지 구성에 지정된대로) 로그 회전을 활성화하여이 작업을 수행 할 수 있습니다 (로그 회전을 사용하면 지정된 제한을 초과하면 로그 파일에 대해 몇 가지 작업을 수행 할 수 있습니다).

예 : 법적으로 30 일 후에 로그를 삭제해야한다면, 로그 파일 이름에 `{dd}.log`를 지정하고 (`{dd}`는 일 수를 나타냅니다), `log_rotation_limit` 값을 30으로 설정하고, `log_rotation_action` 값을 `Delete`로 설정할 수 있습니다.

또는, 오랜 시간 동안 로그를 유지해야하는 경우, 로그 회전을 비활성화하거나, 로그 파일을 압축하기 위해 `log_rotation_action` 값을 `Archive`로 설정하십시오 (이렇게하면 점유하는 디스크 공간의 총량이 줄어 듭니다).

*관련 설정 지시어 :*
- `logging` -> `log_rotation_action`
- `logging` -> `log_rotation_limit`

##### 9.3.4 로그 자르기

원하는 경우 특정 크기를 초과하면 개별 로그 파일을자를 수 있습니다.

*관련 설정 지시어 :*
- `logging` -> `truncate`

##### 9.3.5 IP 주소 PSEUDONYMISATION

첫째, 용어에 익숙하지 않은 경우, "pseudonymisation"는 보충 정보없이 특정 "데이터 주체"로 식별 될 수 없는 방식으로 개인 데이터를 처리하는 것을 의미합니다 (개인 정보를 자연인에게 확인할 수 없도록 추가 정보가 별도로 유지되고 기술적 및 조직적 조치를 조건으로 제공되어야합니다).

다음 자료는 추가 정보를 제공합니다.
- [[trust-hub.com] What is pseudonymisation?](https://www.trust-hub.com/news/what-is-pseudonymisation/)
- [[Wikipedia] Pseudonymization](https://en.wikipedia.org/wiki/Pseudonymization)

어떤 경우에는, 수집, 처리 또는 저장되는 "PII"에 대해 "anonymisation"또는 "pseudonymisation"을 구현할 법적 구속을받을 수 있습니다. 이 개념은 현재 상당 기간 존재 해 왔지만 GDPR/DSGVO는 "pseudonymisation"을 언급하고 장려합니다.

원하는 경우 CIDRAM은 IP 주소를 기록 할 때이 작업을 수행 할 수 있습니다. 기록 될 때 IPv4 주소의 마지막 옥텟과 IPv6 주소의 두 번째 부분 이후의 모든 항목은 "x"로 표시됩니다. 이것은 본질적으로 IPv4 주소를 24 번째 서브넷 요소의 초기 주소로 반올림하고 IPv6 주소를 32 번째 서브넷 요소의 초기 주소로 반올림합니다.

*노트 : CIDRAM의 IP 주소 pseudonymisation 프로세스는 CIDRAM의 IP 추적 기능에 영향을 미치지 않습니다. 이것이 당신에게 문제가된다면, IP 추적을 완전히 비활성화하는 것이 가장 좋습니다.*

*관련 설정 지시어 :*
- `legal` -> `pseudonymise_ip_addresses`

##### 9.3.6 로그 정보 생략

특정 유형의 정보가 전적으로 기록되는 것을 방지하여 한 걸음 더 나아가고 싶다면 이렇게하는 것도 가능합니다. 구성 페이지에서 `fields` 구성 지시문을 참조하여 로그 항목과 "액세스 거부" 페이지에 표시되는 필드를 제어하십시오.

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

*노트 : 로그에서 IP 주소를 완전히 생략 할 때 IP 주소 pseudonymisation을 사용할 이유가 없습니다.*

*관련 설정 지시어 :*
- `general` -> `fields`

##### 9.3.7 통계

CIDRAM은 선택적으로 특정 시간 이후에 발생한 블록 이벤트 또는 CAPTCHA 인스턴스의 총 수와 같은 통계를 추적 할 수 있습니다. 이 기능은 기본적으로 비활성화되어 있지만 패키지 구성을 통해 활성화 할 수 있습니다. 이 기능은 발생 된 총 이벤트 수만 추적합니다. 특정 이벤트에 대한 정보는 포함되어 있지 않으므로 PII로 간주되어서는 안됩니다.

*관련 설정 지시어 :*
- `general` -> `statistics`

##### 9.3.8 암호화

CIDRAM은 캐시 또는 로그 정보를 [암호화](https://ko.wikipedia.org/wiki/%EC%95%94%ED%98%B8%ED%99%94)하지 않습니다. 캐시 및 로그 암호화는 향후 도입 될 수 있지만 현재 구체적인 계획은 없습니다. 승인되지 않은 제 3 자의 개인 식별 정보 (PII)에 대한 액세스 (예, 캐시 또는 로그) : 공개적으로 접근 가능한 위치에 CIDRAM을 설치하지 않을 것을 권장합니다 (예, 대부분의 표준 웹 서버에서 사용할 수있는 표준 `public_html` 디렉토리 외부에 CIDRAM 설치) 과 적절하게 제한적인 권한이 시행되는지 확인하십시오 (특히 vault 디렉토리의 경우). 문제가 지속되면 CIDRAM을 구성하여이 정보가 수집되거나 기록되지 않도록 할 수 있습니다 (예, 로깅 비활성화).

#### 9.4 COOKIE (쿠키)

CIDRAM은 [쿠키](https://ko.wikipedia.org/wiki/HTTP_%EC%BF%A0%ED%82%A4)를 코드베이스의 두 지점에 설정합니다. 1. 사용자가 CAPTCHA 인스턴스를 성공적으로 완료하면 (이것은 `lockuser`가 `true`로 설정된다고 가정합니다), CIDRAM은 사용자가 이미 CAPTCHA 인스턴스를 완료했다는 후속 요청을 기억할 수 있도록 쿠키를 설정합니다. 이렇게하면 후속 요청에서 사용자에게 CAPTCHA 인스턴스를 완료하도록 계속 요청하지 않아도됩니다. 2. 사용자가 프론트 엔드에 성공적으로 로그인하면, CIDRAM은 후속 요청에 대해 사용자를 기억할 수 있도록 쿠키를 설정합니다 (즉, 쿠키는 로그인 세션에 대해 사용자를 인증하는 데 사용됩니다).

두 경우 모두, 사용자는 관련 작업에 참여할 경우 쿠키가 설정된다는 사실을 눈에 띄게 경고합니다. 쿠키는 코드베이스의 다른 지점에서 설정되지 않습니다.

*노트 : "보이지 않는"CAPTCHA API는 일부 관할권에서 쿠키 법률과 호환되지 않을 수 있습니다. 쿠키 법이 적용되는 웹 사이트는을 피해 야합니다. 대신, 제공된 다른 API를 사용하거나, 단순히 CAPTCHA를 완전히 비활성화하는 것이, 바람직 할 수 있습니다.*

*관련 설정 지시어 :*
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 9.5 마케팅과 광고

CIDRAM은 마케팅이나 광고 목적으로 정보를 수집하거나 처리하지 않습니다. 수집되거나 기록 된 정보를 판매하거나 이익을 얻지 않습니다. CIDRAM은 상업적 기업이 아니며 상업적 이익과 관련이 없으므로, 이러한 일을하는 것이 타당하지 않습니다. 이것은 프로젝트가 시작된 이래로 그랬다, 오늘날에도 계속해서 그러합니다. 또한, 이러한 일을하는 것은 프로젝트의 정신과 목적에 맞지 않습니다과, 내가 프로젝트를 계속 유지한다면, 결코 일어나지 않을 것이다.

#### 9.6 개인 정보 정책

경우에 따라 웹 사이트의 모든 페이지와 섹션에 개인 정보 취급 방침에 대한 링크를 명확하게 표시해야 할 수도 있습니다. 이는 개인 정보 보호 관행, 수집하는 개인 식별 정보 유형 및 개인 정보 사용 방법에 대해 사용자에게 알리는 데 중요 할 수 있습니다. 이러한 링크를 CIDRAM의 "액세스 거부"페이지에 포함 시키려면 개인 정보 보호 정책에 대한 URL을 지정하는 구성 지시문이 제공됩니다.

*노트 : 개인 정보 취급 방침 페이지가 CIDRAM의 보호 뒤에 있지 않도록 적극 권장합니다. CIDRAM이 개인 정보 취급 방침 페이지를 보호하고 CIDRAM에 의해 차단 된 사용자가 개인 정보 취급 방침 링크를 클릭하면 다시 차단되어 개인 정보 취급 방침을 볼 수 없습니다. 이상적으로는 HTML 페이지 또는 일반 텍스트 파일과 같은 개인 정보 취급 방침의 정적 복사본에 연결해야합니다.*

*관련 설정 지시어 :*
- `legal` -> `privacy_policy`

#### 9.7 GDPR/DSGVO

일반 데이터 보호 규정 (GDPR)은 2018 년 5 월 25 일부터 효력을 발생하는 유럽 연합 (EU)의 규정입니다. 이 규정의 주요 목표는 EU 시민과 주민들에게 개인 정보를 통제하고 프라이버시 및 개인 정보와 관련하여 EU 내 규정을 통일하는 것입니다.

이 규정에는 유럽 연합 (EU)의 "데이터 주체"에 대한 "[개인 식별 정보](https://ko.wikipedia.org/wiki/%EA%B0%9C%EC%9D%B8%EC%A0%95%EB%B3%B4)"(PII) 처리와 관련된 특정 조항이 포함되어 있습니다 ("데이터 주체"는 식별 된 또는 식별 가능한 자연인을 의미합니다). 규정을 준수하려면 "기업"(규정에 정의 된대로) 및 관련 시스템 및 프로세스가 수행해야하는 몇 가지 사항이 있습니다 : 표준으로 "디자인에 의한 개인 정보 보호"구현; 최대한 높은 개인 정보 설정 사용; 저장된 정보 나 처리 된 정보에 대한 안전 장치 구현 (여기에는 다음이 포함됩니다 : 데이터의 pseudonymisation 또는 완전한 anonymisation 구현); 데이터 수집 유형, 처리 방법, 이유, 보유 기간 및 제 3 자와의 공유 여부를 모호하지 않게 선언하십시오; 제 3 자와 공유하는 데이터의 유형, 방법, 이유 등을 설명합니다.

규정에 정의 된대로 합법적 인 근거가없는 한 데이터를 처리 할 수 없습니다. 이것은 다음을 의미합니다 : 처리는 법적 의무를 준수하여 수행되어야합니다, 또는, 명백하고, 정보에 입각하고, 모호하지 않은 동의가 데이터 주체로부터 얻어진 후에 만 그것을 행한다.

규제의 일부 측면은 시간이 지남에 따라 변경 될 수 있습니다. 구식 정보의 확산을 피하기 위해, 관련 정보를 여기에 포함하는 대신 권위있는 출처에서 규제에 대해 배우는 것이 더 좋습니다 (여기에 포함 된 정보가 오래 될 수 있습니다).

추가 정보를 배우기 위해 권장되는 자료 :
- [유럽 개인정보 보호법 GDPR 안내](https://www.privacy.go.kr/gdpr)
- [유럽 개인정보보호법, GDPR을 알아보자 | HACKTAGON](https://hacktagon.github.io/chinnie/law/gdpr/privacy/GDPR_01)
- [REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679)
- [일반 데이터 보호 규칙](https://ko.wikipedia.org/wiki/%EC%9D%BC%EB%B0%98_%EB%8D%B0%EC%9D%B4%ED%84%B0_%EB%B3%B4%ED%98%B8_%EA%B7%9C%EC%B9%99)

---


### 10. <a name="SECTION10"></a>이전 주 버전에서 업그레이드

#### 10.0 CIDRAM v3로 업그레이드

v3와 이전 주 버전 간에는 상당한 차이가 있습니다. 진입점이 작동하는 방식, 모듈이 구성되는 방식, 및 업데이터가 v3에서 작동하는 방식은 이전 주요 버전에서 작동하는 방식과 다릅니다. 이러한 차이점 때문에, 이전 주 버전에서 v3로 업그레이드하는 가장 좋은 방법은 새로 설치하는 것입니다.

구성 및 보조 규칙을 유지하려면, 업그레이드 프로세스를 시작하기 전에, 프런트 엔드 백업 페이지로 이동하십시오. 여기에서, 구성 및 보조 규칙을 내보낼 수 있습니다. 내보내면 파일이 다운로드됩니다. 새 주 버전으로 업그레이드한 후, 해당 파일을 사용하여 이전에 내보낸 데이터를 설치로 가져올 수 있습니다.

모듈이 구성되는 방식이 변경되었기 때문에, v3에서 제대로 작동하려면 이전 주 버전용 모듈을 다시 작성해야 합니다. 직접 마이그레이션이 작동하지 않습니다. 이벤트도 마찬가지입니다.

서명 파일이 구성되는 방식은 변경되지, 않았으므로 이전 주요 버전용 서명 파일을 예상되는 문제 없이 v3로 직접 마이그레이션할 수 있습니다.

v3부터, 모듈, 서명 파일, 및 이벤트에는 각각 고유한 전용 디렉터리가 있습니다 (그래서 그들은 vault 바닥 대신에 거기로 갈 것입니다).

이전 주 버전의 서명 파일, 모듈, 및 차단 목록 중 일부는 v3에서 사용할 수 없습니다. 대부분의 경우, v3 이후에 추가된 새로운 기능으로 인해, 필요하지 않습니다.

보조 규칙 및 구성이 약간 변경되었지만, 프런트 엔드 백업 페이지에서 가져오기/내보내기 기능을 사용하면, 수동으로 수행할 작업이 불필요. 가져올 때, CIDRAM은 무엇이 필요한지 알고 자동으로 처리합니다.

v3에서 도입된 변경 사항 목록(추가된 기능, 제거된 기능, 등등)은 [v3 변경 로그를](https://github.com/CIDRAM/CIDRAM/blob/v3/Changelog.md#v300) 참조하세요.

#### 10.1 CIDRAM v3 이전 버전에서 CIDRAM v4로 업그레이드

위를 참조하세요 : 새로 설치하는 것이 좋습니다.

#### 10.2 CIDRAM v3에서 CIDRAM v4로 업그레이드

1. 첫째, 프런트엔드 업데이트 페이지에서, 사용 가능한 업데이트가 있으면 모두 설치하세요. 이렇게 하면 업그레이드에 필요한 모든 코드를 사용할 수 있으며 업데이터에 필요한 작업량을 줄이는 데 도움이 됩니다.

2. 프런트엔드 구성 페이지에서 __`frontend➡remotes`__ 를 찾으세요. 목록에서 `/v3/`를 `/v4/`로 변경하세요. 업데이트를 클릭하여 구성을 저장하세요. 이 변경 사항은 업데이트를 찾을 때 업데이터가 의도한 주요 버전을 대상으로 지정하도록 지시합니다.

3. 프런트엔드 백업 페이지에서, 내보내기를 선택하고, 구성, 통계, 보조 규칙에 대한 확인란을, 선택한 다음 확인을 눌러 백업을 다운로드합니다. 몇 가지 변화가 있었습니다. 예를 들어, "기록하지 마십시오" 동작은 보조 규칙에서 제거되었습니다 ("로깅 억제" 옵션을 대신 사용하여 동일한 결과를 얻을 수 있음). 이러한 변경 사항을 적용하려면 업그레이드 후 이 백업을 CIDRAM으로 다시 가져와야 합니다.

4. 프런트엔드 업데이트 페이지에, 새로운 주요 버전에 대한 업데이트가 표시됩니다. 시간 초과를 방지하려면, 모든 항목을 업데이트하기 전에, 먼저 CIDRAM 코어나 CIDRAM 프런트엔드만 업데이트해 보세요 (둘은 서로 종속되어 있으므로 하나를 업데이트하면 둘 다 자동으로 업데이트됩니다). 구조적, 스타일적 변화로 인해, 페이지가 깨져 보일 수 있지만, 실제로는 깨지지 않았습니다. 다른 프런트엔드 페이지에서 Ctrl+F5를 눌러 하드 새로 고침을 시도해 보세요 (즉, 브라우저가 캐시에 의존하지 않고 CSS 스타일 및 기타 주변 데이터의 새 사본을 가져오는 새로 고침입니다). 그러면 페이지 구조와 CSS 스타일이 올바르게 표시될 것입니다. 그렇지 않은 경우, 브라우저 캐시를 지워보세요.

5. 다음으로, 다른 모든 것을 업데이트할 수 있습니다. 프런트엔드 업데이트 페이지에서, 페이지 상단에 버튼이 보이면, 모두 업데이트를 클릭하세요.

6. 남아있는 잘못된 업데이트나 손상된 파일이 없는지 확인하고 모든 것이 제대로 되어 있는지 확인하려면 "모두 수리"를 클릭하세요. 실제로 이런 문제가 발생하는 경우는 매우 드물지만, 안전하게 처리하는 것이 좋습니다.

7. 프런트엔드 백업 페이지에서, 가져오기를 선택하고, 구성, 통계, 보조 규칙에 대한 확인란을, 파일을 선택하는 버튼을 클릭하고, 앞서 다운로드한 백업을 찾아 선택한 다음 확인을 눌러 해당 백업을 가져옵니다. CIDRAM은 변경 사항을 수용하기 위해 필요한 모든 조정을 자동으로 수행합니다.

8. 업그레이드가 완료되었습니다. 다음으로, 새로운 주요 버전에서 도입된 변경 사항으로 인해 프런트엔드 구성 페이지를 간략하게 살펴보고 싶을 수 있습니다 (예를 들어, 새로운 기능의 경우). 새로운 주요 버전은 서명 파일, 모듈, 또는 이벤트에 어떠한 변경 사항도 도입하지 않으므로 업그레이드할 때 이에 대해 걱정할 필요가 없습니다.

v4에서 도입된 변경 사항 목록(추가된 기능, 제거된 기능, 등등)은 [v4 변경 로그를](https://github.com/CIDRAM/CIDRAM/blob/v4/Changelog.md#v400) 참조하세요.

---


최종 업데이트 : 2025년 10월 9일.
