## CIDRAM v3のドキュメンテーション（日本語）。

### 目次
- １.[序文](#user-content-SECTION1)
- ２.[インストール方法](#user-content-SECTION2)
- ３.[使用方法](#user-content-SECTION3)
- ４.[フロントエンドの管理](#user-content-SECTION4)
- ５.[コンフィギュレーション（設定オプション）](#user-content-SECTION5)
- ６.[シグネチャ（署名）フォーマット](#user-content-SECTION6)
- ７.[適合性問題](#user-content-SECTION7)
- ８.[よくある質問（ＦＡＱ）](#user-content-SECTION8)
- ９.[法律情報](#user-content-SECTION9)

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### １.<a name="SECTION1"></a>序文

CIDRAM（シドラム、​クラスレス・ドメイン間・ルーティング・アクセス・マネージャー 『Classless Inter-Domain Routing Access Manager』）は、​ＰＨＰスクリプトです。​ウェブサイトを保護するように設計されて、​ＩＰアドレス（望ましくないトラフィックのあるソースとみなします）から、​発信リクエストをブロックすることによって（ヒト以外のアクセスエンドポイント、​クラウドサービス、​スパムロボット、​スクレーパー、​等）。​ＩＰアドレスの可能ＣＩＤＲを計算することにより、​ＣＩＤＲは、​そのシグネチャ・ファイルと比較することができます（これらのシグネチャ・ファイルは不要なＩＰアドレスに対応するCIDRのリストが含まれています）；​一致が見つかった場合、​リクエストはブロックされます。

*（参照する：​[「ＣＩＤＲ」とは何ですか？​](#user-content-WHAT_IS_A_CIDR)）。*

[CIDRAM](https://cidram.github.io/)著作権２０１３とＧＮＵ一般公衆ライセンスv2を超える権利について：[Caleb M (Maikuolan)](https://github.com/Maikuolan)著。

本スクリプトはフリーウェアです。​フリーソフトウェア財団発行のＧＮＵ一般公衆ライセンス・バージョン２（またはそれ以降のバージョン）に従い、​再配布ならびに加工が可能です。​配布の目的は、​役に立つことを願ってのものですが、​『保証はなく、​また商品性や特定の目的に適合するのを示唆するものでもありません』。​『LICENSE.txt』にある『GNU General Public License』（一般ライセンス）を参照して下さい。​以下のURLからも閲覧できます：
- <https://www.gnu.org/licenses/>。
- <https://opensource.org/licenses/>。

本ドキュメントならびに関連パッケージは以下のＵＲＬからダウンロードできます。
- [GitHub](https://github.com/CIDRAM/CIDRAM)。
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram)。
- [SourceForge](https://sourceforge.net/projects/cidram/)。

---


### ２.<a name="SECTION2"></a>インストール方法

#### 2.0 手動インストール

まず、それを操作するためにCIDRAMの新しいコピーが必要になります。​「[CIDRAM/CIDRAM](https://github.com/CIDRAM/CIDRAM)」リポジトリから最新バージョンのCIDRAMのアーカイブをダウンロードできます。​具体的には、「vault」ディレクトリの新しいコピーが必要になります（「vault」ディレクトリとその内容以外のアーカイブからのすべては、安全に削除または無視することができます）。

v3より前は、CIDRAMフロントエンドにアクセスできるようにするために、パブリック・ルート内のどこかにCIDRAMをインストールする必要がありました。​ただし、v3以降では、これは必要ありません。​セキュリティを最大化し、CIDRAMとそのファイルへの不正アクセスを防ぐために、代わりにパブリック・ルートの外部にCIDRAMをインストールすることをお勧めします。​ＰＨＰでアクセスできる限り、安全である限り、そして満足している限り、どこにでもCIDRAMをインストールできます。​ディレクトリ名を「vault」として保持する必要がなくなったため、好きなように名前を変更できます​（ただし、便宜上、ドキュメンテーションでは、引き続き「vault」ディレクトリと呼びます）。

準備ができたら、「vault」ディレクトリを選択した場所にアップロードし、ＰＨＰがディレクトリに書き込めるようにするために必要な権限があることを確認します​（システムによっては、何もする必要がない場合や、ディレクトリでCHMODを「755」に設定する必要がある場合があります、または、「755」に問題がある場合は、「777」を試すことができますが、安全性が低いため、「777」はお勧めしません）。

次に、CIDRAMがコードベースまたはＣＭＳを保護できるようにするには、「エントリポイント」を作成する必要があります。​このようなエントリポイントは、次の３つで構成されます：

1. コードベースまたはＣＭＳの適切なポイントに「loader.php」ファイルを含める。
2. 「CIDRAM core」のインスタンシエーション。
3. 「protect」メソッドの呼び出し。

簡単な例：

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

Apacheウェブサーバーを使用していて、`php.ini`ファイルにアクセスできる場合は、ＰＨＰリクエストが行われるたびにCIDRAMを実行するために、`auto_prepend_file`ディレクティブを使用できます。​このような場合、エントリポイントを作成するのに最も適切な場所は独自のファイルであり、`auto_prepend_file`ディレクティブで引用する必要になります。

例：

`auto_prepend_file = "/path/to/your/entrypoint.php"`

または、これは`.htaccess`ファイルになります：

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

その他の場合、エントリポイントを作成するための最も適切な場所は、コードベースまたはCMS内の可能な限り早いポイントで、誰かがウェブサイト全体の任意のページにアクセスするたびに常にロードされることです。​コードベースが「ブートストラップ」を利用している場合、良い例は「ブートストラップ」ファイルの最初にあります。​コードベースにデータベースへの接続を担当する中央ファイルがある場合、別の良い例はその中央ファイルの最初にあります。

#### 2.1 COMPOSERを使用してインストールする

[CIDRAMはPackagistに登録されています](https://packagist.org/packages/cidram/cidram)。 Composerを使い慣れている場合は、​Composerを使用してCIDRAMをインストールできます。

`composer require cidram/cidram`

#### 2.2 WORDPRESSためにインストールする

[CIDRAMは、​WordPressプラグインデータベースにプラグインとして登録されています](https://wordpress.org/plugins/cidram/)。​プラグイン・ダッシュボードからCIDRAMを直接インストールできます。​他のプラグインと同じ方法でインストールでき、​追加手順は不要です。

*警告：プラグイン・ダッシュボードを介してCIDRAMを更新すると、​クリーン・インストールが行われます。​インストールをカスタマイズした場合（あなたの設定を変更した、​モジュールをインストールしたなど）、​これらのカスタマイズは、​プラグイン・ダッシュボードを介して更新すると、​失われます！​ログ・ファイルも失われます！​ログ・ファイルとカスタム化を保持するには、​CIDRAMフロントエンド・アップデイト・ページで更新します。*

#### 2.3 「コンフィギュレーション」と「カストマイゼーション」

必要に応じて調整できるように、新しいインストールの構成を確認することを強くお勧めします。​追加のモジュール、シグネチャ・ファイルをインストールしたり、補助ルールを作成したり、その他のカスタマイズを実装して、インストールをニーズに最適にすることもできます。​これらのことを行うには、フロントエンドを使用することをお勧めします。

---


### ３.<a name="SECTION3"></a>使用方法

CIDRAMは自動的に望ましくないリクエストをブロックする必要があります；支援が必要とされていません（インストールを除きます）。

あなたの設定ファイルを変更することによって、​コンフィギュレーション設定をカスタマイズすることができます。​あなたのシグネチャ・ファイルを変更することによって、​ＣＩＤＲがブロックされて変更することができます。

誤検出（偽陽性）や新種の疑わしきものに遭遇した、​関することについては何でもお知らせ下さい。 *（参照する：​[「偽陽性」とは何ですか？​](#user-content-WHAT_IS_A_FALSE_POSITIVE)）。*

CIDRAMは、手動で、または、フロントエンド経由で更新できます。​CIDRAMは、もともとそれらの手段を介してインストールされていれば、ComposerまたはWordPress経由で更新することもできます。

---


### ４.<a name="SECTION4"></a>フロントエンドの管理

#### 4.0 フロントエンドは何です。

フロントエンドは、​CIDRAMのインストールを維持、​管理、​更新するための便利で簡単な方法を提供します。​ログ・ページを使用してログ・ファイルを表示、​共有、​ダウンロードすることができます、​コンフィギュレーションページでコンフィギュレーションを変更できます、​アップデートページを使用してコンポーネントをインストールおよびアンインストールできます、​そして、​ファイル・マネージャーを使用してvault「ボールト」内のファイルをアップロード、​ダウンロード、​および変更することができます。

#### 4.1 フロントエンドにアクセスする方法。

以前と同じように、フロントエンドにアクセスするにはエントリポイントを作成する必要があります。​このようなエントリポイントは、次の３つで構成されます：

1. コードベースまたはＣＭＳの適切なポイントに「loader.php」ファイルを含める。
2. 「CIDRAM front-end」のインスタンシエーション。
3. 「view」メソッドの呼び出し。

簡単な例：

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

「FrontEnd」クラスは「Core」クラスを拡張します。​これは、潜在的に不要なトラフィックがフロントエンドにアクセスするのをブロックするために、「view」メソッドを呼び出す前に「protect」メソッドを呼び出すことができることを意味します。​そうすることは完全にオプションです。

簡単な例：

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

フロントエンドのエントリポイントを作成するのに最も適切な場所は、専用のファイルです。​以前とは異なり、エントリポイントが存在する特定のファイルを直接要求することによってのみフロントエンド・エントリポイントにアクセス可能にする必要があります。​したがって、あなたはここで`auto_prepend_file`または`.htaccess`は使用したくない。

フロントエンド・エントリポイントを作成したら、ブラウザを使用してアクセスします。​ログイン・ページが表示されます。​ログイン・ページで、デフォルトのユーザー名とパスワード（admin/password）を入力し、ログイン・ボタンを押します。

注意：あなたが初めてログインした後、​フロントエンドへの不正アクセスを防ぐために、​あなたはすぐにユーザー名とパスワードを変更する必要があります！​これは非常に重要です、​なぜなら、​フロントエンドから任意のＰＨＰコードをあなたのウェブサイトにアップロードすることができるからです。

また、最適なセキュリティを実現するには、すべてのフロントエンド・アカウントに対して「二要素認証」を有効にすることを強くお勧めします（下記の手順）。

#### 4.2 フロントエンドの使い方。

フロントエンドの各ページには、​目的の説明とその使用方法の説明があります。​詳しい説明や特別な支援が必要な場合は、​サポートにお問い合わせください。​また、​デモを提供するYouTube上で利用可能な動画もあります。

#### 4.3 ２ＦＡ（二要素認証）

２ＦＡ「二要素認証」を有効にすることで、フロントエンドをより安全にすることができます。​２ＦＡを使用するアカウントにログインすると、そのアカウントに関連付けられた電子Ｅメール・アドレスに電子Ｅメールが送信されます。​このＥメールには「２ＦＡコード」が含まれています。​このアカウントを使用してログインできるように、ユーザーはこの２ＦＡコードとユーザー名とパスワードを入力する必要があります。​つまり、アカウントのパスワードでは、ハッカーや潜在的な攻撃者がそのアカウントにログインするのに十分ではありません。​セッションに関連付けられた２ＦＡコードを受信して利用するには、そのアカウントに関連付けられた電子Ｅメールアドレスにアクセスする必要があります。

まず、２ＦＡを有効にするには、フロントエンドのアップデイト・ページを使用して、PHPMailerコンポーネントをインストールします。​CIDRAMは、電子Ｅメールを送信するために、PHPMailerを利用します。

PHPMailerをインストールしたら、CIDRAMコンフィギュレーション・ページまたはコンフィギュレーション・ファイルを使用して、PHPMailerのコンフィギュレーション・ディレクティブを設定する必要があります。​これらのコンフィギュレーション・ディレクティブの詳細については、このドキュメントのコンフィギュレーション・セクションに記載されています。​PHPMailerコンフィギュレーション・ディレクティブを設定したら、`enable_two_factor`を`true`に設定します。​２ＦＡが有効にされている。

次に、CIDRAMがそのアカウントでログインする際に２ＦＡコードを送信する場所を知るように、電子Ｅメール・アドレスをアカウントに関連付ける必要があります。​これを行うには、電子Ｅメール・アドレスをアカウントのユーザー名として使用する（例えば、`foo@bar.tld`）か、電子Ｅメール・アドレスを通常どおり電子Ｅメールを送信する場合と同じ方法でユーザー名の一部として含めます（例えば、`Foo Bar <foo@bar.tld>`）。

注意：不正なアクセスからvaultを保護することは特に重要です（例えば、サーバーのセキュリティを強化し、パブリック・アクセス許可を制限する）。​コンフィギュレーション・ファイル（あなたのvaultに保存されています）の不正なアクセスが送信SMTPコンフィギュレーションを公開する可能性があります（SMTPユーザー名とパスワードを含む）。​２ＦＡを有効にする前に、vaultが適切に保護されていることを確認する必要があります。​あなたがこれを行うことができない場合は、少なくとも、この目的のために専用の新しい電子Ｅメール・アカウントを作成する必要があります（公開されたSMTPコンフィギュレーションに関連するリスクを軽減するため）。

---


### ５.<a name="SECTION5"></a>コンフィギュレーション（設定オプション）

以下は`config.yml`設定ファイルにある変数ならびにその目的と機能のリストです。

```
コンフィギュレーション (v3)
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

#### "general" （カテゴリ）
全般的な設定（他のカテゴリに属さないの設定）。

##### "stages" `[string]`
- 実行チェーンの段階のコントロールです （有効かどうか、エラーがログに記録されるかどうか、など）。

```
stages
├─Tests ("シグネチャ・ファイル・テストを実行する")
├─Modules ("モジュールを実行する")
├─SearchEngineVerification ("検索エンジンの検証を実行する")
├─SocialMediaVerification ("ソーシャル・メディア検証を実行する")
├─OtherVerification ("その他の検証を実行する")
├─Aux ("補助ルールを実行する")
├─Reporting ("レポートを実行する")
├─Tracking ("ＩＰトラッキングを実行する")
├─RL ("レート制限を実行する")
├─CAPTCHA ("キャプチャを展開する（ブロックされたリクエスト）")
├─Statistics ("統計をアップデートする")
├─Webhooks ("Webhookを実行する")
├─PrepareFields ("出力とログ用のフィールドを準備する")
├─Output ("出力を生成する（ブロックされたリクエスト）")
├─WriteLogs ("ログへの書き込み（ブロックされたリクエスト）")
├─Terminate ("リクエストを終了する（ブロックされたリクエスト）")
├─AuxRedirect ("補助ルールに従ってリダイレクトする")
└─NonBlockedCAPTCHA ("キャプチャを展開する（ブロックされていないリクエスト）")
```

##### "fields" `[string]`
- ブロック・イベント中のために、フィールドのコントロールです （リクエストがブロックされたとき）。

```
fields
├─ID ("ＩＤ")
├─ScriptIdent ("スクリプトのバージョン")
├─DateTime ("日/月/年/時刻")
├─IPAddr ("ＩＰアドレス")
├─IPAddrResolved ("ＩＰアドレス（解決済み）")
├─Query ("クエリー")
├─Referrer ("リファラー")
├─UA ("ユーザーエージェント")
├─UALC ("ユーザーエージェント（小文字）")
├─SignatureCount ("シグネチャの数")
├─Signatures ("シグネチャリファレンス")
├─WhyReason ("なぜブロックされましたか")
├─ReasonMessage ("なぜブロックされましたか（詳細な）")
├─rURI ("ＵＲＩ再構築された")
├─Infractions ("違反")
├─ASNLookup ("** ＡＳＮルックアップ")
├─CCLookup ("** 国コード・ルックアップ")
├─Verified ("確認済みの身元")
├─Expired ("期限切れ")
├─Ignored ("無視された")
├─Request_Method ("リクエスト・メソッド")
├─Protocol ("プロトコル")
├─Hostname ("ホスト名")
├─CAPTCHA ("キャプチャ・ステータス")
└─Inspection ("* 条件検査")
```

* 補助ルールのデバッグのみを目的としています。​ブロックされたユーザーには表示されません。

** ＡＳＮルックアップ機能が必要です（たとえば、IP-APIモジュールまたはBGPViewモジュールを介して）。

##### "timezone" `[string]`
- 使用するタイムゾーンを指定します​（例えば、「Africa/Cairo」、「America/New_York」、「Asia/Tokyo」、「Australia/Perth」、「Europe/Berlin」、「Pacific/Guam」、等等）。​「SYSTEM」を指定すると、ＰＨＰがこれを自動的に処理します。

```
timezone
├─SYSTEM ("システムのデフォルトタイムゾーンを使用します。")
├─UTC ("UTC")
└─…その他
```

##### "time_offset" `[int]`
- タイムゾーン・オフセット（分）。

##### "time_format" `[string]`
- CIDRAMで使用される日付表記形式。​追加のオプションがリクエストに応じて追加される場合があります。

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
└─…その他
```

##### "ipaddr" `[string]`
- 接続リクエストのＩＰアドレスをどこで見つけるべきかについて（Cloudflareのようなサービスに対して有効）。​Default（デフォルト設定） = REMOTE_ADDR。​注意：あなたが何をしているのか、​分からない限り、​これを変更しないでください。

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (デフォルト)")
└─…その他
```

参照してください：
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### "http_response_header_code" `[int]`
- リクエストをブロックするときに、CIDRAMが送信するＨＴＴＰステータス・メッセージはどれですか？

```
http_response_header_code
├─200 (200 OK （大丈夫です）): それは最小の堅牢が、最もユーザー・フレンドリーです。
│ 自動化されたリクエストは、この応答をリクエストが成功したことを示すものとして解釈する可能性があります。
├─403 (403 Forbidden （禁断）): それはもっと堅牢ですが、少ないユーザー・フレンドリーです。
│ ほとんどの場合に推奨されます。
├─410 (410 Gone （なくなっています）): 一部のブラウザは、ブロックが解除された後でも、このステータス・メッセージをキャッシュし、後続のリクエストを送信しないため、偽陽性を解決するときに問題が発生する可能性があります。
│ 特定の種類のトラフィックでは、状況によっては最も望ましい場合があります。
├─418 (418 I'm a teapot （私はティーポットです）): エイプリル・フールのジョークを参照しています（{{Links.RFC2324}}）。
│ クライアント、ボット、ブラウザ、などに理解される可能性はほとんどありません。
│ 娯楽と利便性のために提供されていますが、一般的にはお勧めしません。
├─451 (451 Unavailable For Legal Reasons （法的な理由で利用できません）): 主に法的な理由でブロックする場合に推奨されます。
│ 他のコンテキストでは推奨されません。
└─503 (503 Service Unavailable （サービスは利用できません）): それは最も堅牢が、最小のユーザー・フレンドリーです。
  攻撃を受けている場合、または非常に永続的な不要なトラフィックを処理する場合に推奨されます。
```

##### "silent_mode" `[string]`
- 「アクセス拒否」ページを表示する代わりに、​CIDRAMはブロックされたアクセス試行を自動的にリダイレクトする必要がありますか？​はいの場合は、​リダイレクトの場所を指定します。​いいえの場合は、​この変数を空白のままにします。

##### "lang" `[string]`
- CIDRAMのデフォルト言語を設定します。

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

##### "lang_override" `[bool]`
- 可能な限り「HTTP_ACCEPT_LANGUAGE」に従ってローカライズしますか？ True = はい（Default/デフォルルト）。 False = いいえ。

##### "numbers" `[string]`
- どのように数字を表示するのが好きですか？​あなたに一番正しい例を選択してください。

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
- ここにＥメールアドレスを入力して、​ユーザーがブロックされているときにユーザーに送信することができます。​これはサポートと支援に使用できます（誤ってブロックされた場合、​等）。​警告：​ここに入力された電子Ｅメールアドレスは、​おそらくスパムロボットによって取得されます。​ここで提供される電子Ｅメールアドレスは、​すべて使い捨てにすることを強く推奨します（例えば、​プライマリ個人アドレスまたはビジネスアドレスを使用しない、​等）。

##### "emailaddr_display_style" `[string]`
- ユーザーに電子Ｅメール・アドレスを提示することをどのように希望しますか？

```
emailaddr_display_style
├─default ("クリック可能なリンク")
└─noclick ("クリックできないテキスト")
```

##### "ban_override" `[int]`
- 「infraction_limit」を超えたときに「http_response_header_code」を上書きしますか？ ２００ = 上書きしない（Default/デフォルルト）。​他の値は、「http_response_header_code」の利用可能な値と同じです。

```
ban_override
├─200 (200 OK （大丈夫です）): それは最小の堅牢が、最もユーザー・フレンドリーです。
│ 自動化されたリクエストは、この応答をリクエストが成功したことを示すものとして解釈する可能性があります。
├─403 (403 Forbidden （禁断）): それはもっと堅牢ですが、少ないユーザー・フレンドリーです。
│ ほとんどの場合に推奨されます。
├─410 (410 Gone （なくなっています）): 一部のブラウザは、ブロックが解除された後でも、このステータス・メッセージをキャッシュし、後続のリクエストを送信しないため、偽陽性を解決するときに問題が発生する可能性があります。
│ 特定の種類のトラフィックでは、状況によっては最も望ましい場合があります。
├─418 (418 I'm a teapot （私はティーポットです）): エイプリル・フールのジョークを参照しています（{{Links.RFC2324}}）。
│ クライアント、ボット、ブラウザ、などに理解される可能性はほとんどありません。
│ 娯楽と利便性のために提供されていますが、一般的にはお勧めしません。
├─451 (451 Unavailable For Legal Reasons （法的な理由で利用できません）): 主に法的な理由でブロックする場合に推奨されます。
│ 他のコンテキストでは推奨されません。
└─503 (503 Service Unavailable （サービスは利用できません）): それは最も堅牢が、最小のユーザー・フレンドリーです。
  攻撃を受けている場合、または非常に永続的な不要なトラフィックを処理する場合に推奨されます。
```

##### "default_dns" `[string]`
- ホスト名検索に使用する、​ＤＮＳ（ドメイン・ネーム・システム）サーバーのリスト。​注意：あなたが何をしているのか、​分からない限り、​これを変更しないでください。

__ＦＡＱ。__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.ja.md#default_dnsには何が使えますか" hreflang="ja">「default_dns」には何が使えますか？</a></em>

##### "default_algo" `[string]`
- 将来のすべてのパスワードとセッションに使用するアルゴリズムを定義します。

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### "statistics" `[string]`
- 追跡する統計情報を制御します。

```
statistics
├─Blocked-IPv4 ("ブロックされたリクエスト – IPv4")
├─Blocked-IPv6 ("ブロックされたリクエスト – IPv6")
├─Blocked-Other ("ブロックされたリクエスト – その他")
├─Banned-IPv4 ("禁止されたリクエスト – IPv4")
├─Banned-IPv6 ("禁止されたリクエスト – IPv6")
├─Passed-IPv4 ("許可されたリクエスト – IPv4")
├─Passed-IPv6 ("許可されたリクエスト – IPv6")
├─Passed-Other ("許可されたリクエスト – その他")
├─CAPTCHAs-Failed ("キャプチャの試み – 失敗！")
└─CAPTCHAs-Passed ("キャプチャの試み – 合格！")
```

##### "force_hostname_lookup" `[bool]`
- ホスト名検索を強制しますか？ True = はい。 False = いいえ（Default/デフォルルト）。​ホスト名検索は、通常、「必要に応じて」実行されますが、すべてのリクエストに対して強制することができます。​これは、より詳細な情報をログ・ファイルに提供する手段として有用ですが、パフォーマンスに多少の悪影響を及ぼすこともあります。

##### "allow_gethostbyaddr_lookup" `[bool]`
- ＵＤＰが利用できない場合、gethostbyaddrルックアップを許可しますか？ True = はい（Default/デフォルルト）。 False = いいえ。

注：一部の３２ビットシステムでは、ＩＰｖ６ルックアップが正しく機能しない場合があります。

##### "disabled_channels" `[string]`
- これは、要求を送信するときにCIDRAMが特定のチャネルを使用しないようにするために使用できます​（例えば、更新時、コンポーネント・メタデータの取得時、など）。

```
disabled_channels
├─GitHub ("GitHub")
├─BitBucket ("BitBucket")
└─GoogleDNS ("GoogleDNS")
```

##### "default_timeout" `[int]`
- 外部リクエストに使用するデフォルトのタイムアウト？ Default/デフォルルト = １２秒。

##### "sensitive" `[string]`
- 機密ページとみなすパスのリスト。​各のリストされたパスは、必要に応じて、ＵＲＩ再構築されたに対してチェックされます。​スラッシュで始まるパスはリテラルとして扱われ、リクエストのパス・コンポーネントから照合されます。​英数字以外の文字で始まり、同じ文字（または同じ文字と「i」フラグ）で終わるパスは、正規表現として扱われます。​他の種類のパスはリテラルとして扱われ、ＵＲＩのどの部分からでも一致できます。​パスが機密ページと見なされるかどうかは、一部のモジュールの動作に影響を与える可能性がありますが、他の影響はありません。

#### "components" （カテゴリ）
CIDRAMによって使用されるコンポーネントをアクティブ化および非アクティブ化するための設定。​通常、アップデート・ページに入力されますが、ここから管理して、より細かく制御したり、アップデート・ページで認識されないカスタム・コンポーネントを管理したりすることもできます。

##### "ipv4" `[string]`
- ＩＰｖ４シグネチャ・ファイル。

##### "ipv6" `[string]`
- ＩＰｖ６シグネチャ・ファイル。

##### "modules" `[string]`
- モジュール。

##### "imports" `[string]`
- 輸入。​通常、コンポーネントのコンフィギュレーション情報をCIDRAMに提供するために使用されます。

##### "events" `[string]`
- イベント・ハンドラー。​通常、CIDRAMの内部動作を変更したり、追加機能を提供したりするために使用されます。

#### "logging" （カテゴリ）
ロギングに関連するコンフィギュレーション（他のカテゴリに該当するものを除く）。

##### "standard_log" `[string]`
- アクセス試行阻止の記録、​人間によって読み取り可能。​ファイル名指定するか、​無効にしたい場合は空白のままにして下さい。

##### "apache_style_log" `[string]`
- アクセス試行阻止の記録、​Apacheスタイル。​ファイル名指定するか、​無効にしたい場合は空白のままにして下さい。

##### "serialised_log" `[string]`
- アクセス試行阻止の記録、​シリアル化されました。​ファイル名指定するか、​無効にしたい場合は空白のままにして下さい。

##### "error_log" `[string]`
- 検出された致命的でないエラーを記録するためのファイル。​ファイル名指定するか、​無効にしたい場合は空白のままにして下さい。

##### "outbound_request_log" `[string]`
- アウトバウンド要求の結果を記録するためのファイル。​ファイル名指定するか、​無効にしたい場合は空白のままにして下さい。

##### "report_log" `[string]`
- 外部ＡＰＩに送信されたレポートを記録するためのファイル。​ファイル名指定するか、​無効にしたい場合は空白のままにして下さい。

##### "truncate" `[string]`
- ログ・ファイルが一定のサイズに達したら切り詰めますか？​値は、​ログ・ファイルが切り捨てられる前に大きくなる可能性があるＢ/ＫＢ/ＭＢ/ＧＢ/ＴＢ単位の最大サイズです。​デフォルト値の０ＫＢは切り捨てを無効にします （ログ・ファイルは無期限に拡張できます）。​注：個々のログ・ファイルに適用されます。​ログ・ファイルのサイズは一括して考慮されません。

##### "log_rotation_limit" `[int]`
- ログ・ローテーションは、一度に存在する必要があるログ・ファイルの数を制限します。​新しいログ・ファイルが作成されると、ログ・ファイルの総数が指定された制限を超えると、指定されたアクションが実行されます。​ここで希望の制限を指定することができます。​値「0」は、ログ・ローテーションを無効にします。

##### "log_rotation_action" `[string]`
- ログ・ローテーションは、一度に存在する必要があるログ・ファイルの数を制限します。​新しいログ・ファイルが作成されると、ログ・ファイルの総数が指定された制限を超えると、指定されたアクションが実行されます。​ここで希望のアクションを指定できます。

```
log_rotation_action
├─Delete ("最も古いログ・ファイルを削除して、制限を超過しないようにします。")
└─Archive ("最初にアーカイブしてから、最も古いログ・ファイルを削除して、制限を超過しないようにします。")
```

##### "log_banned_ips" `[bool]`
- 禁止されたＩＰからブロックされたリクエストをログ・ファイルに含めますか？ True = はい（Default/デフォルルト）。 False = いいえ。

##### "log_sanitisation" `[bool]`
- フロントエンドのログページを使用してログデータを表示する場合、ＸＳＳ攻撃やその他の潜在的な脅威からユーザーを保護する、CIDRAMはログデータを表示前にサニタイズします。​ただし、デフォルトでは、データはロギング中にサニタイズされません。​これは、ログデータが正確に記録されるようにするためです（将来必要になる可能性があるヒューリスティックまたはフォレンジック分析に役立ちます）。​ただし、ユーザーが外部ツールを使用してログデータを読み込もうとした場合、それらの外部ツールが独自のサニティゼーション・プロセスを実行しない場合、ユーザーがＸＳＳ攻撃にさらされる可能性があります。​必要に応じて、このコンフィギュレーション・ディレクティブを使ってデフォルトの動作を変更することができます。 True = データを記録するときは、それをサニタイズして（記録データの精度はもっと低いですが、ＸＳＳリスクはもっと低いです）。 False = データを記録するときは、それをサニタイズしない（記録データの精度はもっと高いですが、ＸＳＳリスクはもっと高いです）。 Default/デフォルルト = False。

#### "frontend" （カテゴリ）
フロントエンド・コンフィギュレーション。

##### "frontend_log" `[string]`
- フロントエンド・ログインの試みを記録するためのファイル。​ファイル名指定するか、​無効にしたい場合は空白のままにして下さい。

##### "signatures_update_event_log" `[string]`
- フロントエンドを介してシグネチャ・ファイルが更新されたときにログに記録するためのファイル。​ファイル名指定するか、​無効にしたい場合は空白のままにして下さい。

##### "max_login_attempts" `[int]`
- ログイン試行の最大回数（フロントエンド）。​Default（デフォルト設定） = ５。

##### "theme" `[string]`
- フロントエンドに使用するデフォルト・テーマ。

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
└─…その他
```

##### "magnification" `[float]`
- フォントの倍率。​Default/デフォルルト = １。

##### "custom_header" `[string]`
- すべてのフロントエンド・ページの最初にＨＴＭＬとして挿入されます。​ウェブサイトのロゴ、パーソナライズされたヘッダー、スクリプト、などに役立ちます。

##### "custom_footer" `[string]`
- すべてのフロントエンド・ページの最下部にＨＴＭＬとして挿入されます。​法的通知、連絡先リンク、ビジネス情報、などに役立ちます。

##### "remotes" `[string]`
- アップデーターがコンポーネント・メタデータをフェッチするために使用するアドレスのリスト。​これは、新しいメジャーバージョンにアップグレードするとき、または更新用の新しいソースを取得するときに調整する必要がある場合がありますが、通常の状況ではそのままにしておく必要があります。

##### "enable_two_factor" `[bool]`
- このディレクティブは、フロントエンド・アカウントに２ＦＡを使用するかどうかを決定します。

#### "signatures" （カテゴリ）
シグネチャ、シグネチャ・ファイル、モジュール、などのコンフィギュレーション。

##### "shorthand" `[string]`
- 与えられた速記語を利用するシグネチャに対してポジティブ・マッチがある場合に、要求をどう処理するかを制御のためです。

```
shorthand
├─Attacks ("攻撃")
├─Bogon ("⁰ ボゴンＩＰ")
├─Cloud ("クラウド・サービス")
├─Generic ("ジェネリック")
├─Legal ("¹ 法的")
├─Malware ("マルウェア")
├─Proxy ("² プロキシ")
├─Spam ("スパム・リスク")
├─Banned ("³ 禁止された")
├─BadIP ("³ 無効なＩＰ")
├─RL ("³ レート制限は達しました")
└─Other ("⁴ その他")
```

__0.__ ウェブサイトにＬＡＮまたはｌｏｃａｌｈｏｓｔ「ローカルホスト」経由でアクセスする必要がある場合は、これをブロックしないで。​それ以外の場合は、これをブロックできます。

__1.__ デフォルト・シグネチャ・ファイルはどれもこれを使用していませんが、それでも一部のユーザーにとって役立つ可能性がある場合に備えてサポートされています。

__2.__ ユーザーがプロキシ経由でウェブサイトにアクセスできるようにする必要がある場合は、これをブロックしないで。​それ以外の場合は、これをブロックできます。

__3.__ シグネチャ内直接使用はサポートされていませんが、特定の状況では他の方法で呼び出される場合があります。

__4.__ 速記語をまったく使用されていないか、CIDRAMによって認識されない場合を参照します。

__シグネチャごとに一つ。__ シグネチャは複数のプロファイルを呼び出すことができますが、速記語を一つだけ使用できます。​複数の速記語が適切な場合もありますが、一つしか使用できないため、常に最適な速記語のみを使用することを目指しています。

__優先順位。__ 選択されたオプションは、選択されていないオプションよりも常に優先されます。​たとえば、複数の速記語が使用されているが、そのうちの一つだけがブロックされるように設定されている場合、リクエストは引き続きブロックされます。

__ヒューマン・エンドポイントとクラウド・サービス。__ クラウド・サービスは、ウェブホスティング・プロバイダー、サーバー・ファーム、データ・センター、またはその他の多くのものを参照場合があります。​ヒューマン・エンドポイントは、人間がインターネットにアクセスする手段を参照します、たとえば、インターネット・サービス・プロバイダーなどを介して。​ネットワークは通常、どちらか一方のみを提供しますが、両方を提供する場合もあります。​私たちは、潜在的なヒューマン・エンドポイントをクラウド・サービスとして決して識別しないことを目指しています。​したがって、クラウド・サービスの範囲が既知のヒューマン・エンドポイントによって共有されている場合、クラウド・サービスは別のものとして識別される可能性があります。​同様に、既知のヒューマン・エンドポイントと共有される範囲がない場合は、常にクラウド・サービスとして識別しようとします。​したがって、クラウド・サービスとして明示的に識別されたリクエストは、範囲を既知のヒューマン・エンドポイントと共有する可能性が低いです。​同様に、攻撃またはスパム・リスクによって明示的に識別されたリクエストは、範囲を共有する可能性が高いです。​ただし、インターネットは常に流動的であり、ネットワークの目的は時間の経過とともに変化し、範囲は常に売買されているため、偽陽性については意識し、警戒してください。

##### "default_tracktime" `[string]`
- ＩＰアドレスを追跡する期間。​Default（デフォルト設定） = 「7d0°0′0″」 （１週間）。

##### "infraction_limit" `[int]`
- ＩＰがＩＰトラッキングによって禁止される前に発生することが、​許される違反の最大数。​Default（デフォルト設定） = １０。

##### "tracking_override" `[bool]`
- モジュールが追跡オプションをオーバーライドできるようにしますか？ True = はい（Default/デフォルルト）。 False = いいえ。

#### "verification" （カテゴリ）
リクエストの発信元を確認するためコンフィギュレーション。

##### "search_engines" `[string]`
- 検索エンジンからのリクエストを検証するためのコントロール。

```
search_engines
├─Amazonbot ("Amazonbot")
├─Applebot ("Applebot")
├─Baidu ("Baiduspider/百度")
├─Bingbot ("Bingbot")
├─DuckDuckBot ("DuckDuckBot")
├─Googlebot ("Googlebot")
├─MojeekBot ("MojeekBot")
├─Neevabot ("Neevabot")
├─PetalBot ("PetalBot")
├─Qwantify ("Qwantify/Bleriot")
├─SeznamBot ("SeznamBot")
├─Sogou ("Sogou/搜狗")
├─Yahoo ("Yahoo/Slurp")
├─Yandex ("Yandex/Яндекс")
└─YoudaoBot ("YoudaoBot")
```

__「陽性」と「陰性」とは何ですか？__ リクエストによって提示されたＩＤを検証する場合、成功した結果は「陽性」または「陰性」と記述できます。​提示されたＩＤが真のＩＤであることが確認された場合、「陽性」と記述されます。​提示されたＩＤが偽物であることが確認された場合、「陰性」と記述されます。​ただし、失敗した結果（たとえば、検証が失敗した、または提示されたＩＤの信憑性を判断できない）は、「陽性」または「陰性」とは記述れません。​代わりに、失敗した結果は単に未確認として記述されます。​リクエストによって提示されたＩＤを検証する試みが行われない場合、リクエストは同様に未検証として記述されます。​この用語は、リクエストによって提示されたＩＤが認識されるコンテキストでのみ意味があります（したがって、検証が可能な場合）。​提示されたＩＤが上記のオプションと一致しない場合、またはＩＤが提示されていない場合、上記のオプションは無関係になります。

__「シングル・ヒット・バイパス」とは何ですか？__ 場合によっては、シグネチャ・ファイル、モジュール、またはリクエストの他の条件の結果として、肯定的に検証されたリクエストがブロックされることがあります、誤検知を回避するためにバイパスが必要になる場合があります。​バイパスが正確に一つの違反を処理することを目的としている場合、そのようなバイパスは「シングル・ヒット・バイパス」として記述できます。

##### "social_media" `[string]`
- ソーシャル・メディア・プラットフォームからのリクエストを検証するためのコントロール。

```
social_media
├─Embedly ("Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("Pinterest")
├─Snapchat ("Snapchat")
└─Twitterbot ("Twitterbot")
```

__「陽性」と「陰性」とは何ですか？__ リクエストによって提示されたＩＤを検証する場合、成功した結果は「陽性」または「陰性」と記述できます。​提示されたＩＤが真のＩＤであることが確認された場合、「陽性」と記述されます。​提示されたＩＤが偽物であることが確認された場合、「陰性」と記述されます。​ただし、失敗した結果（たとえば、検証が失敗した、または提示されたＩＤの信憑性を判断できない）は、「陽性」または「陰性」とは記述れません。​代わりに、失敗した結果は単に未確認として記述されます。​リクエストによって提示されたＩＤを検証する試みが行われない場合、リクエストは同様に未検証として記述されます。​この用語は、リクエストによって提示されたＩＤが認識されるコンテキストでのみ意味があります（したがって、検証が可能な場合）。​提示されたＩＤが上記のオプションと一致しない場合、またはＩＤが提示されていない場合、上記のオプションは無関係になります。

__「シングル・ヒット・バイパス」とは何ですか？__ 場合によっては、シグネチャ・ファイル、モジュール、またはリクエストの他の条件の結果として、肯定的に検証されたリクエストがブロックされることがあります、誤検知を回避するためにバイパスが必要になる場合があります。​バイパスが正確に一つの違反を処理することを目的としている場合、そのようなバイパスは「シングル・ヒット・バイパス」として記述できます。

** ＡＳＮルックアップ機能が必要です（たとえば、IP-APIモジュールまたはBGPViewモジュールを介して）。

##### "other" `[string]`
- 可能な場合は、他の種類のリクエストを検証するためのコントロール。

```
other
├─AdSense ("AdSense")
├─AmazonAdBot ("AmazonAdBot")
└─Grapeshot ("Oracle Data Cloud Crawler")
```

__「陽性」と「陰性」とは何ですか？__ リクエストによって提示されたＩＤを検証する場合、成功した結果は「陽性」または「陰性」と記述できます。​提示されたＩＤが真のＩＤであることが確認された場合、「陽性」と記述されます。​提示されたＩＤが偽物であることが確認された場合、「陰性」と記述されます。​ただし、失敗した結果（たとえば、検証が失敗した、または提示されたＩＤの信憑性を判断できない）は、「陽性」または「陰性」とは記述れません。​代わりに、失敗した結果は単に未確認として記述されます。​リクエストによって提示されたＩＤを検証する試みが行われない場合、リクエストは同様に未検証として記述されます。​この用語は、リクエストによって提示されたＩＤが認識されるコンテキストでのみ意味があります（したがって、検証が可能な場合）。​提示されたＩＤが上記のオプションと一致しない場合、またはＩＤが提示されていない場合、上記のオプションは無関係になります。

__「シングル・ヒット・バイパス」とは何ですか？__ 場合によっては、シグネチャ・ファイル、モジュール、またはリクエストの他の条件の結果として、肯定的に検証されたリクエストがブロックされることがあります、誤検知を回避するためにバイパスが必要になる場合があります。​バイパスが正確に一つの違反を処理することを目的としている場合、そのようなバイパスは「シングル・ヒット・バイパス」として記述できます。

##### "adjust" `[string]`
- 検証のコンテキストで他の機能を調整するためのコントロール。

```
adjust
├─Negatives ("ブロックされた陰性")
└─NonVerified ("ブロックされた未確認")
```

#### "recaptcha" （カテゴリ）
ReCaptchaの設定（ブロックされたときに人間がアクセスを取り戻す方法を提供します）。

##### "usemode" `[int]`
- キャプチャはいつ提供する必要がありますか？​注：ホワイト・リストされまたは検証済みでブロックされていないリクエストは、キャプチャを完了する必要はありません。​また注意してください：​ＣＡＰＴＣＨＡは、ボットやさまざまな種類の悪意のある自動化されたリクエストに対する有用な追加の保護レイヤーを提供できますが、悪意のある人間に対する保護は提供しません。

```
usemode
├─0 (決して !!!)
├─1 (ブロックされ、シグネチャの制限内であり、禁止されていない場合のみ。)
├─2 (ブロックされ、シグネチャの制限内であり、使用するために特別にマークされている、禁止されていない場合のみ。)
├─3 (シグネチャの制限内であり、禁止されていない場合のみ（ブロックされているかどうかに関係なく）。)
├─4 (ブロックされていない場合のみ。)
└─5 (ブロックされていない場合、またはシグネチャの制限内であり、使用するために特別にマークされている場合のみ。)
```

##### "lockip" `[bool]`
- キャプチャをＩＰにロックしますか？

##### "lockuser" `[bool]`
- キャプチャをユーザーにロックしますか？

##### "sitekey" `[string]`
- この値は、キャプチャ・サービスのダッシュボードに表示されます。

参照してください：
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "secret" `[string]`
- この値は、キャプチャ・サービスのダッシュボードに表示されます。

参照してください：
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "expiry" `[float]`
- キャプチャ・インスタンスを覚えておく時間数。 Default（デフォルルト） = ７２０（１ヶ月）。

##### "recaptcha_log" `[string]`
- キャプチャ試行の記録。​ファイル名指定するか、​無効にしたい場合は空白のままにして下さい。

##### "signature_limit" `[int]`
- キャプチャが取り消される前に許可されるシグネチャの最大数。​Default/デフォルルト = １。

##### "api" `[string]`
- どのＡＰＩを使用するのですか？

```
api
├─V2 ("V2 (チェック・ボックス)")
└─Invisible ("V2 (インビジブル)")
```

##### "show_cookie_warning" `[bool]`
- クッキーの警告を表示しますか？ True = はい（Default/デフォルルト）。 False = いいえ。

##### "show_api_message" `[bool]`
- ＡＰＩメッセージを表示しますか？ True = はい（Default/デフォルルト）。 False = いいえ。

##### "nonblocked_status_code" `[int]`
- ブロックされていないリクエストにキャプチャを表示する場合、どのステータス・コードを使用する必要がありますか？

```
nonblocked_status_code
├─200 (200 OK （大丈夫です）): それは最小の堅牢が、最もユーザー・フレンドリーです。
│ 自動化されたリクエストは、この応答をリクエストが成功したことを示すものとして解釈する可能性があります。
├─403 (403 Forbidden （禁断）): それはもっと堅牢ですが、少ないユーザー・フレンドリーです。
│ ほとんどの場合に推奨されます。
├─418 (418 I'm a teapot （私はティーポットです）): エイプリル・フールのジョークを参照しています（{{Links.RFC2324}}）。
│ クライアント、ボット、ブラウザ、などに理解される可能性はほとんどありません。
│ 娯楽と利便性のために提供されていますが、一般的にはお勧めしません。
├─429 (429 Too Many Requests （リクエストが多すぎます）): レート制限、ＤＤｏＳ攻撃に対処する場合、およびフラッド防止に推奨されます。
│ 他のコンテキストでは推奨されません。
└─451 (451 Unavailable For Legal Reasons （法的な理由で利用できません）): 主に法的な理由でブロックする場合に推奨されます。
  他のコンテキストでは推奨されません。
```

#### "hcaptcha" （カテゴリ）
HCaptchaの設定（ブロックされたときに人間がアクセスを取り戻す方法を提供します）。

##### "usemode" `[int]`
- キャプチャはいつ提供する必要がありますか？​注：ホワイト・リストされまたは検証済みでブロックされていないリクエストは、キャプチャを完了する必要はありません。​また注意してください：​ＣＡＰＴＣＨＡは、ボットやさまざまな種類の悪意のある自動化されたリクエストに対する有用な追加の保護レイヤーを提供できますが、悪意のある人間に対する保護は提供しません。

```
usemode
├─0 (決して !!!)
├─1 (ブロックされ、シグネチャの制限内であり、禁止されていない場合のみ。)
├─2 (ブロックされ、シグネチャの制限内であり、使用するために特別にマークされている、禁止されていない場合のみ。)
├─3 (シグネチャの制限内であり、禁止されていない場合のみ（ブロックされているかどうかに関係なく）。)
├─4 (ブロックされていない場合のみ。)
└─5 (ブロックされていない場合、またはシグネチャの制限内であり、使用するために特別にマークされている場合のみ。)
```

##### "lockip" `[bool]`
- キャプチャをＩＰにロックしますか？

##### "lockuser" `[bool]`
- キャプチャをユーザーにロックしますか？

##### "sitekey" `[string]`
- この値は、キャプチャ・サービスのダッシュボードに表示されます。

参照してください：
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "secret" `[string]`
- この値は、キャプチャ・サービスのダッシュボードに表示されます。

参照してください：
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "expiry" `[float]`
- キャプチャ・インスタンスを覚えておく時間数。 Default（デフォルルト） = ７２０（１ヶ月）。

##### "hcaptcha_log" `[string]`
- キャプチャ試行の記録。​ファイル名指定するか、​無効にしたい場合は空白のままにして下さい。

##### "signature_limit" `[int]`
- キャプチャが取り消される前に許可されるシグネチャの最大数。​Default/デフォルルト = １。

##### "api" `[string]`
- どのＡＰＩを使用するのですか？

```
api
├─V1 ("V1")
└─Invisible ("V1 (インビジブル)")
```

##### "show_cookie_warning" `[bool]`
- クッキーの警告を表示しますか？ True = はい（Default/デフォルルト）。 False = いいえ。

##### "show_api_message" `[bool]`
- ＡＰＩメッセージを表示しますか？ True = はい（Default/デフォルルト）。 False = いいえ。

##### "nonblocked_status_code" `[int]`
- ブロックされていないリクエストにキャプチャを表示する場合、どのステータス・コードを使用する必要がありますか？

```
nonblocked_status_code
├─200 (200 OK （大丈夫です）): それは最小の堅牢が、最もユーザー・フレンドリーです。
│ 自動化されたリクエストは、この応答をリクエストが成功したことを示すものとして解釈する可能性があります。
├─403 (403 Forbidden （禁断）): それはもっと堅牢ですが、少ないユーザー・フレンドリーです。
│ ほとんどの場合に推奨されます。
├─418 (418 I'm a teapot （私はティーポットです）): エイプリル・フールのジョークを参照しています（{{Links.RFC2324}}）。
│ クライアント、ボット、ブラウザ、などに理解される可能性はほとんどありません。
│ 娯楽と利便性のために提供されていますが、一般的にはお勧めしません。
├─429 (429 Too Many Requests （リクエストが多すぎます）): レート制限、ＤＤｏＳ攻撃に対処する場合、およびフラッド防止に推奨されます。
│ 他のコンテキストでは推奨されません。
└─451 (451 Unavailable For Legal Reasons （法的な理由で利用できません）): 主に法的な理由でブロックする場合に推奨されます。
  他のコンテキストでは推奨されません。
```

#### "legal" （カテゴリ）
法的要件のコンフィギュレーション。

##### "pseudonymise_ip_addresses" `[bool]`
- ログ・ファイルを書き込むときにＩＰアドレス偽名化するか「プセユードニマイズ」？ True = はい（Default/デフォルルト）。 False = いいえ。

##### "privacy_policy" `[string]`
- 生成されたページのフッターに表示される関連プライバシー・ポリシーのアドレス。​ＵＲＬを指定するか、無効にしたい場合は空白のままにして下さい。

#### "template_data" （カテゴリ）
テンプレートとテーマの設定。

##### "theme" `[string]`
- CIDRAMに使用するデフォルト・テーマ。

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
└─…その他
```

##### "magnification" `[float]`
- フォントの倍率。​Default/デフォルルト = １。

##### "css_url" `[string]`
- カスタムテーマのＣＳＳファイルＵＲＬ。

##### "block_event_title" `[string]`
- ブロック・イベントに表示するページ・タイトル。

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("アクセス拒否！")
└─…その他
```

##### "captcha_title" `[string]`
- キャプチャ・リクエストに表示するページ・タイトル。

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…その他
```

##### "custom_header" `[string]`
- すべての「アクセス拒否」ページの最初にＨＴＭＬとして挿入されます。​ウェブサイトのロゴ、パーソナライズされたヘッダー、スクリプト、などに役立ちます。

##### "custom_footer" `[string]`
- すべての「アクセス拒否」ページの最下部にＨＴＭＬとして挿入されます。​法的通知、連絡先リンク、ビジネス情報、などに役立ちます。

#### "rate_limiting" （カテゴリ）
レート制限の設定（一般的な使用には推奨されません）。

##### "max_bandwidth" `[string]`
- 将来の要求に対してレート制限を有効にする前の許容期間内に許容される最大帯域幅。​０の値は、このタイプのレート制限を無効にします。​Default/デフォルルト = 0KB。

##### "max_requests" `[int]`
- 将来の要求に対してレート制限を有効にする前に、許容期間内に許可される要求の最大数。​０の値は、このタイプのレート制限を無効にします。​Default/デフォルルト = 0。

##### "precision_ipv4" `[int]`
- ＩＰｖ４の使用状況を監視する際の精度。​値はＣＩＤＲブロック・サイズを反映します。​最高の精度を得るには３２に設定します。​Default/デフォルルト = 32。

##### "precision_ipv6" `[int]`
- ＩＰｖ６の使用状況を監視する際の精度。​値はＣＩＤＲブロック・サイズを反映します。​最高の精度を得るには１２８に設定します。​Default/デフォルルト = 128。

##### "allowance_period" `[string]`
- 使用状況を監視する期間。​Default/デフォルルト = 0°0′0″。

##### "exceptions" `[string]`
- 例外（すなわち、レート制限されるべきではないリクエスト）。​レート制限が有効な場合にのみ効果があります。

```
exceptions
├─Whitelisted ("ホワイトリストに登録されたリクエスト")
└─Verified ("検証済みの検索エンジンとソーシャル・メディアのリクエスト")
```

##### "segregate" `[bool]`
- 異なるドメインおよびホストのクォータを分離または共有する必要がありますか？ True = クォータは分離されます。 False = クォータは共有されます（Default/デフォルルト）。

#### "supplementary_cache_options" （カテゴリ）
補足キャッシュ・オプション。 注：これらの値を変更すると、ログアウトする可能性があります。

##### "prefix" `[string]`
- ここで指定された値は、すべてのキャッシュ・エントリ・キーの前に追加されます。 Default/デフォルルト = 「CIDRAM_」。 同じサーバーに複数のインストールが存在する場合、これはキャッシュを互いに分離しておくのに役立ちます。

##### "enable_apcu" `[bool]`
- キャッシュに「APCu」を使用するかどうかを指定します。 Default/デフォルルト = True。

##### "enable_memcached" `[bool]`
- キャッシュに「Memcached」を使用するかどうかを指定します。 Default/デフォルルト = False。

##### "enable_redis" `[bool]`
- キャッシュに「Redis」を使用するかどうかを指定します。 Default/デフォルルト = False。

##### "enable_pdo" `[bool]`
- キャッシュに「PDO」を使用するかどうかを指定します。 Default/デフォルルト = False。

##### "memcached_host" `[string]`
- Memcachedのホスト値。 Default/デフォルルト = 「localhost」。

##### "memcached_port" `[int]`
- Memcachedのポート値。 Default/デフォルルト = 「11211」。

##### "redis_host" `[string]`
- Redisのホスト値。 Default/デフォルルト = 「localhost」。

##### "redis_port" `[int]`
- Redisのポート値。 Default/デフォルルト = 「6379」。

##### "redis_timeout" `[float]`
- Redisのタイムアウト値。 Default/デフォルルト = 「2.5」。

##### "pdo_dsn" `[string]`
- PDOのDSN値。 Default/デフォルルト = 「mysql:dbname=cidram;host=localhost;port=3306」。

__ＦＡＱ。__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.ja.md#user-content-HOW_TO_USE_PDO" hreflang="ja">「PDO DSN」とは何ですか？​CIDRAMでPDOを使用するにはどうすればよいですか？</a></em>

##### "pdo_username" `[string]`
- PDOのユーザー名。

##### "pdo_password" `[string]`
- PDOのパスワード。

#### "bypasses" （カテゴリ）
デフォルト・シグネチャ・バイパスのコンフィギュレーション。

##### "used" `[string]`
- どのバイパスを使用する必要がありますか？

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
├─Neevabot ("Neevabot")
├─PetalBot ("PetalBot")
├─Pinterest ("Pinterest")
├─Redditbot ("Redditbot")
└─Snapchat ("Snapchat")
```

---


### ６.<a name="SECTION6"></a>シグネチャ（署名）フォーマット

*参照：*
- *[「シグネチャ」とは何ですか？](#user-content-WHAT_IS_A_SIGNATURE)*

#### 6.0 基本原則 （シグネチャ・ファイルの場合）

すべてのＩＰｖ４シグネチャはこの形式に従います：​`xxx.xxx.xxx.xxx/yy 「機能」 「パラメータ」`
- `xxx.xxx.xxx.xxx`は、​ＣＩＤＲブロックの先頭を表します（ブロックの最初のＩＰアドレスのオクテット）。
- `yy`は、​ブロックサイズを表します（１ー３２）。
- `「機能」`は、​スクリプトにシグネチャの処理方法を指示します。
- `「パラメータ」`は、​`「機能」`で必要、​な追加情報を表します。

すべてのＩＰｖ６シグネチャはこの形式に従います：​`xxxx:xxxx:xxxx:xxxx::xxxx/yy 「機能」 「パラメータ」`
- `xxxx:xxxx:xxxx:xxxx::xxxx`は、​ＣＩＤＲブロックの先頭を表します（ブロックの最初のＩＰアドレスのオクテット）。​完全表記と省略表記の両方が可能です。​彼らはＩＰｖ６仕様に準拠する必要があります、​1つの例外を除いて：​CIDRAMでは、​ＩＰｖ６アドレスは省略で始めることはできません。​例えば：​`::1/128`は`0::1/128`、​そして`::0/128`は`0::/128`と表す必要があります。
- `yy`は、​ブロックサイズを表します（１ー１２８）。
- `「機能」`は、​スクリプトにシグネチャの処理方法を指示します。
- `「パラメータ」`は、​`「機能」`で必要、​な追加情報を表します。

シグネチャ・ファイルの改行はUnix標準を使用すべきです （`%0A`、​`\n`）。​他の標準も使用できますが、​推奨されません （例えば、​Windowsの`%0D%0A`、​`\r\n`、​Macの`%0D`、​`\r`、​等）。​非UNIX改行は正規化されます。

正確で正しいＣＩＤＲ表記が必要です。​スクリプトは、​不正確な表記（または、​不正確な表記を伴うシグネチャ）を認識しません。​さらに、​すべてのＣＩＤＲは、​均等に割り切れる必要があります（例えば、​`10.128.0.0`から`11.127.255.255`までのすべてをブロックしたい場合、​`10.128.0.0/8`はスクリプトによって認識されません、​しかし、​`10.128.0.0/9`と`11.0.0.0/9`を組み合わせて使用するとは、​スクリプトによって認識されます）。

スクリプトによって認識されないシグネチャ・ファイル内のものは無視されます。​つまり、​シグネチャ・ファイルを破損することなく、​ほぼすべてのデータをシグネチャ・ファイルに安全に入れることができます。​シグネチャ・ファイルのコメントは受け入れ可能です。​特殊な書式設定は必要ありません。​シェル形式のハッシュが推奨されますが、​強制はされません（シェルスタイルのハッシングは、​IDEやプレーンテキストエディタに役立ちます）。

「機能」の可能な値：
- Run
- Whitelist
- Greylist
- Deny

「Run」を使用すると、​シグネチャがトリガーされると、​スクリプトは`require_once`ステートメントによって（`「パラメータ」`値で指定されます）外部のＰＨＰスクリプトの実行を試みます。​作業ディレクトリは「`/vault/`」ディレクトリです。

例：​`127.0.0.0/8 Run example.php`

特定のＩＰ/ＣＩＤＲに対して特定のＰＨＰコードを実行する場合に便利です。

「Whitelist」を使用すると、​シグネチャがトリガーされると、​スクリプトはすべての検出をリセットします（何かの検出があった場合）、​テスト機能を終了します。​`「パラメータ」`は無視されます。​これは、​ＩＰまたはＣＩＤＲをホワイトリストに登録するのと同じです。

例：​`127.0.0.1/32 Whitelist`

「Greylist」を使用すると、​シグネチャがトリガーされると、​スクリプトはすべての検出をリセットします（何かの検出があった場合）、​処理を続行するために次のシグネチャ・ファイルにスキップする。​`「パラメータ」`は無視されます。

例：​`127.0.0.1/32 Greylist`

「Deny」を使用すると、​シグネチャがトリガーされると、​保護されたページへのアクセスは拒否されます（ＩＰ/ＣＩＤＲがホワイトリストに登録されていない場合）。​「Deny」は、​実際にＩＰアドレスとＣＩＤＲの範囲をブロックするために使用するものです。​「Deny」を使用するシグネチャがトリガーされると、​「アクセス拒否」ページが生成され、​保護されたページへのリクエストが終了します。

「Deny」によって受け入れられた`「パラメータ」`値は、​「アクセス拒否」ページ出力に処理されます、​リクエストされたページへのアクセスが拒否された理由として、​クライアント/ユーザーに提供されます。​それは短くて簡単な文章にすることができます（なぜそれらをブロックすることを選択したのか説明するために）。​また、​略語とすることもできます（事前準備された説明をクライアント/ユーザーに提供する）。

あらかじめ用意された説明にはL10Nのサポートがあり、​スクリプトで翻訳することができます。​翻訳は、​スクリプト・コンフィギュレーションの`lang`ディレクティブを使用して指定した言語に基づいて行われます。​さらに、​これらの短縮形の単語を使用している場合、​`「パラメータ」`値に基づいて 「Deny」シグネチャを無視するようスクリプトに指示できます。​これは、​スクリプト設定で指定されたディレクティブを介して行われます（それぞれの省略形に対応するディレクティブがあります）。​ただし、​他の`「パラメータ」`値にはL10Nがサポートされていません（したがって、​他の値は翻訳されません、​そしてコンフィギュレーションによって制御可能ではない）。

略語：
- Attacks
- Bogon
- Cloud
- Generic
- Legal
- Malware
- Proxy
- Spam

#### 6.1 タグ

##### 6.1.0 セクション・タグ

セクション名と「セクション・タグ」を追加することにより、​スクリプトに対する個々のセクションを識別することができます（以下の例を参照してください）。

```
# セクション１。
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: セクション１
```

セクション・タグを終了し、​シグネチャセクションが誤って識別されないようにするには、​タグと前のセクションの間に少なくとも２つの改行が連続していることを確認してください。​タグなしシグネチャは、​デフォルトで「ＩＰｖ４」または「ＩＰｖ６」のいずれかになります（どのタイプのシグネチャがトリガされているかに応じて）。

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: セクション１
```

上記の例で、​`1.2.3.4/32`と`2.3.4.5/32`は、​「ＩＰｖ４」でタグ付けされま；す一方、​`4.5.6.7/32`と`5.6.7.8/32`は、​「セクション１」でタグ付けされま。

他のタイプのタグの分離にも同じロジックを適用することができます。

セクション・タグは、偽陽性が発生した場合のデバッグに非常に役立ちます。​彼らが、問題の正確な原因を簡単に見つける方法を提供します。​フロントエンド・ログ・ページからログ・ファイルを表示するときに、ログ・ファイル・エントリをフィルタリングするのに非常に役立ちます（セクション名はフロントエンド・ログ・ページでクリック可能で、フィルタリング基準として使用できます）。​一部の特定のシグネチャで、セクション・タグが省略されている場合、シグネチャがトリガーされると、CIDRAMはシグネチャ・ファイルの名前とブロックされたＩＰアドレス（ＩＰｖ４またはＩＰｖ６）のタイプをフォールバックとして使用します。​したがって、セクション・タグは完全にオプションです。​しかし、シグネチャ・ファイルの名前が曖昧である場合や、要求をブロックする原因となるシグネチャのソースを明確に特定することが困難な場合など、いくつかのケースで推奨される場合があります。

##### 6.1.1 期限タグ

「期限タグ」を使用して、​シグネチャの有効期限を指定することができます。​期限切れのタグがこの形式を使用します：​「年年年年.月月.日日」 （以下の例を参照してください）。

```
# セクション１。
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

有効期限が切れたシグネチャは、どの要求に対してもトリガされません。

##### 6.1.2 原点タグ

特定シグネチャの原点国を指定する場合は、「原点タグ」を使用してすることができます。​起点タグは、「[ISO 3166-1 Alpha-2](https://ja.wikipedia.org/wiki/ISO_3166-1)」コードを受け入れます。​このコードは、該当するシグネチャの原点国に対応しています。​これらのコードは、大文字で書く必要があります（小文字または大文字と小文字が混在すると正しく表示されません）。原点タグが使用されると、関連するブロックされた要求の「なぜブロックされましたか」ログ項目に追加されます。

オプションの「flags CSS」コンポーネントがインストールされている場合、フロントエンド・ログ・ページでログ・ファイルを表示するとき、原点タグによって追加された情報は対応する国旗に置き換えられます。​この情報は、生の形態であろうと国旗であろうと、クリック可能である。​クリックすると、同様のログ・エントリに従ってログ・エントリがフィルタリングされます（これにより、原点国のフィルタリングが可能になります）。

注：技術的には、これは積極的に特定の位置情報を求めていないため、ジオロケーションではありません。​代わりに、これにより、特定シグネチャの原産国を明示することができます。​同じシグネチャ・セクション内で複数の原点タグを使用することができます。

仮説的な例：

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

任意のタグを組み合わせて使用することができ、すべてのタグはオプションです​（以下の例を参照してください）。

```
# 例セクション。
1.2.3.4/32 Deny Generic
Origin: US
Tag: 例セクション
Expires: 2016.12.31
```

##### 6.1.3 延期タグ

大量のシグネチャ・ファイルがインストールされ、使用されている場合、インストールが非常に複雑になり、重複するシグネチャが存在する可能性があります。​これらの場合、ブロック・イベント中に複数の重複シグネチャがトリガーされるのを防ぐために、延期タグを使用して、特定のシグネチャ・セクションを他のシグネチャ・ファイルのために延期することができる。​これは、一部のシグネチャが他のシグネチャよりも頻繁に更新される場合に役立ちます、頻繁に更新されないシグネチャよりも頻繁に更新されるシグネチャに優先順位を付ける。

延期タグは他のタイプのタグと同様に使用されます。​タグの値は、インストールされた積極的に使用されるシグネチャ・ファイルと一致する必要があります。

例：

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 6.1.4 プロファイル・タグ

プロファイル・タグは、ＩＰテスト・ページに追加情報を表示する手段を提供し、モジュールおよび補助ルールによって活用して、より複雑な動作と微調整された意思決定を行うことができます。

プロファイルタ・グは、他のタイプのタグと同様に使用されます。​プロファイル・タグの値は、モジュールおよび補助ルールの条件として使用できます。​プロファイル・タグは、それらの値をセミコロンで区切ることにより、複数の値を提供できます。​エンド・ユーザーには、プロファイル・タグの値は表示されません。

例：

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 6.2 ＹＡＭＬ

##### 6.2.0 ＹＡＭＬ基本原則

セクション固有の設定を定義するために、​シンプルな形式のＹＡＭＬマークアップをシグネチャ・ファイルで使用することができます。​これは、​異なるシグネチャセクションに対して異なる設定を行う場合に便利です （例えば：​サポートチケットのＥメールアドレスを指定したい場合は、​しかし特定のセクションのみ；​特定のシグネチャでページリダイレクトをトリガーしたい場合は；​reCAPTCHA/hCAPTCHAで使用するためにシグネチャセクションをマークしたい場合は；​個々のシグネチャに基づいて、​そして/または、​シグネチャセクションに基づいて、​ブロックされたアクセス試行を別々のファイルに記録したい場合は）。

シグネチャ・ファイルでのＹＡＭＬマークアップの使用はオプションです（即ち、​あなたが望むならそれを使うことができますが、​そうする必要はありません）。​大部分の（しかしすべてではない）コンフィギュレーション・ディレクティブを活用することができます。

注意：CIDRAMにおけるＹＡＭＬマークアップの実装は非常に単純化されており、​非常に制限されています。​これは、​ＹＡＭＬマークアップに精通した方法で、​しかし公式仕様書に従ったり準拠したりすることはない、​CIDRAMに固有の要件を満たすことを意図しています（他の実装と同じように動作しない可能性があり、​そして他のプロジェクトには適していない可能性があります）。

CIDRAMでは、​ＹＡＭＬマークアップセグメントはスクリプトに対して３つのダッシュで（「---」）識別されます。​ＹＡＭＬマークアップセグメントは、​二重改行によってシグネチャセクションと一緒に終了します。​典型的なセグメントは、​ＣＩＤＲとタグのリストの直後の行に３つのダッシュでコンフィギュレーションされ、​続いて２次元のキーと値のペアのリストが続きます。​（１番目のディメンションは、​コンフィギュレーション・ディレクティブのカテゴリです；２番目のディメンションは、​コンフィギュレーション・ディレクティブです）。​以下の例を参照してください。

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

##### 6.2.1 reCAPTCHAまたはhCAPTCHAで使用するためにシグネチャセクションをマークする方法。

「usemode」が「2」または「5」の場合、​reCAPTCHAまたはhCAPTCHAで使用するためにシグネチャセクションをマークするには、​そのシグネチャセクションのＹＡＭＬマーカーセグメントを含めてください（以下の例を参照してください）。

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

#### 6.3 補助

##### 6.3.0 シグネチャ・セクションを無視する

さらに、​CIDRAMに特定のシグネチャセクションを完全に無視させたい場合、​「`ignore.dat`」ファイルを使用して、​無視するセクションを指定することができます。​新しい行に`Ignore`と書いてください、​次に、​スペース、​次に、​CIDRAMが無視するセクションの名前（以下の例を参照してください）。

```
Ignore セクション１
```

これは、CIDRAMフロントエンドの「セクション・リスト」ページで提供されるインターフェイスを使用しても実現できます。

##### 6.3.1 補助ルール

独自のカスタム・シグネチャ・ファイルまたはカスタム・モジュールの作成が複雑すぎると感じる場合は、CIDRAMフロントエンドの「補助ルール」ページで提供されるインターフェイスを使用する方が簡単な方法があります。​適切なオプションを選択し、特定のタイプの要求に関する詳細を指定することにより、CIDRAMに要求に対する応答方法を指示できます。​「補助ルール」は、すべてのシグネチャ・ファイルとモジュールが既に実行を終了した後に実行されます。

#### 6.4 <a name="MODULE_BASICS"></a>基本原則 （モジュールの場合）

モジュールを使用して、CIDRAMの機能を拡張したり、追加のタスクを実行したり、追加ロジックを処理することができます。

モジュールはＰＨＰファイルとして記述されているため、CIDRAMコードベースを十分に理解している場合は、必要に応じてモジュールとモジュール・シグネチャを構造化できます（ＰＨＰで可能なことを理由に）。

*注意：​ＰＨＰコードの操作に慣れていない場合は、独自のモジュールを作成することはお勧めしません。*

CIDRAMは、独自のモジュールを簡単かつ簡単に作成できる機能を提供しています。​この機能に関する情報は、以下で説明します。

#### 6.5 モジュール機能

##### 6.5.0 "$this->trigger"

モジュール・シグネチャは、通常、`$this->trigger`で記述されます。​ほとんどの場合、このクロージャ（method）はモジュールを書く目的のために何よりも重要になります。

`$this->trigger`は４つのパラメータを受け取ります：​`$Condition`、`$ReasonShort`、`$ReasonLong`（オプショナル）、`$DefineOptions`（オプショナル）。

`$Condition`の真実性が評価されます。​真の場合（true）、シグネチャはトリガーされます。​偽の場合（false）、シグネチャはトリガーされません。​`$Condition`には通常、リクエストをブロックする条件を評価するためのＰＨＰコードが含まれています。

シグネチャがトリガーされると、「なぜブロックされましたか」フィールドに`$ReasonShort`が引用されます。

`$ReasonLong`は、ユーザー/クライアントがブロックされたときにそれらがブロックされた理由を説明するためにユーザー/クライアントに表示されるオプションのメッセージです。​省略された場合、標準の「アクセス拒否」メッセージを使用します。

`$DefineOptions`は、オプショナル・キーと値のペアを含む配列です。​これは、リクエスト・インスタンスに固有の設定オプションを定義するために使用されます。​設定オプションは、シグネチャがトリガーされたときに適用されます。

`$this->trigger`は、シグネチャがトリガされたときに真（true）を返し、そうでないときに偽（false）を返します。

##### 6.5.1 "$this->bypass"

シグネチャ・バイパスは、通常、`$this->bypass`で記述されます。

`$this->bypass`は３つのパラメータを受け取ります：​`$Condition`、`$ReasonShort`、`$DefineOptions`（オプショナル）。

`$Condition`の真実性が評価されます。​真の場合（true）、バイパスはトリガーされます。​偽の場合（false）、バイパスはトリガーされません。​`$Condition`には通常、リクエストをブロックしてはならない条件を評価するＰＨＰコードが含まれています。

バイパスがトリガーされると、「なぜブロックされましたか」フィールドに`$ReasonShort`が引用されます。

`$DefineOptions`は、オプショナル・キーと値のペアを含む配列です。​これは、リクエスト・インスタンスに固有の設定オプションを定義するために使用されます。​設定オプションは、バイパスがトリガーされたときに適用されます。

`$this->bypass`は、バイパスがトリガされたときに真（true）を返し、そうでないときに偽（false）を返します。

##### 6.5.2 "$this->dnsReverse"

これは、ＩＰアドレスのホスト名を取得するために使用できます。​ホスト名をブロックするモジュールを作成する場合は、このクロージャーが便利です。

例：
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

#### 6.6 モジュール変数

モジュールは独自のスコープ内で実行され、モジュールで定義された変数は他のモジュールや親スクリプトにアクセスできません。​`$CIDRAM`配列に格納されている場合を除いて（この配列は保持されます；モジュールの実行が終了した後はすべてがフラッシュされます）。

あなたのモジュールに役立つ一般的な変数は次のとおりです：

変数 | 説明
----|----
`$this->BlockInfo['DateTime']` | 現在の日付と時刻。
`$this->BlockInfo['IPAddr']` | 現在のリクエストのＩＰアドレス。
`$this->BlockInfo['ScriptIdent']` | CIDRAMスクリプトのバージョン。
`$this->BlockInfo['Query']` | 現在のリクエストのクエリ。
`$this->BlockInfo['Referrer']` | 現在のリクエストのリファラー（存在する場合）。
`$this->BlockInfo['UA']` | 現在のリクエストのユーザー・エージェント（user agent）。
`$this->BlockInfo['UALC']` | 現在のリクエストの小文字でユーザー・エージェント（user agent）。
`$this->BlockInfo['ReasonMessage']` | 現在のリクエストがブロックされている場合、ユーザー/クライアントに表示されるメッセージです。
`$this->BlockInfo['SignatureCount']` | 現在のリクエストに対してトリガされたシグネチャの数。
`$this->BlockInfo['Signatures']` | 現在のリクエストに対してトリガーされたシグネチャーの参照情報。
`$this->BlockInfo['WhyReason']` | 現在のリクエストに対してトリガーされたシグネチャーの参照情報。

---


### 7. <a name="SECTION7"></a>適合性問題

次のパッケージと製品は、CIDRAMと互換性がないことが判明しています。
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

CIDRAMとの互換性を確保するために、以下のパッケージと製品用、モジュールが用意されています。
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__

*参照：​[互換性チャート](https://maikuolan.github.io/Compatibility-Charts/)。*

---


### ８.<a name="SECTION8"></a>よくある質問（ＦＡＱ）

- [「シグネチャ」とは何ですか？](#user-content-WHAT_IS_A_SIGNATURE)
- [「ＣＩＤＲ」とは何ですか？](#user-content-WHAT_IS_A_CIDR)
- [「偽陽性」とは何ですか？](#user-content-WHAT_IS_A_FALSE_POSITIVE)
- [CIDRAMは国全体をブロックできますか？](#user-content-BLOCK_ENTIRE_COUNTRIES)
- [シグネチャはどれくらいの頻度でアップデイトされますか？](#user-content-SIGNATURE_UPDATE_FREQUENCY)
- [CIDRAMを使用しているときに問題が発生しましたが、​何をすべきかわかりません！​助けてください！](#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [私はCIDRAMによってウェブサイトからブロックされています！​助けてください！](#user-content-BLOCKED_WHAT_TO_DO)
- [7.2より古いＰＨＰバージョンでCIDRAM（v2の場合）を使用したいと思います；​手伝ってくれますか？](#user-content-MINIMUM_PHP_VERSION_V3)
- [複数のドメインを保護するために１つのCIDRAMインストールを使用できますか？](#user-content-PROTECT_MULTIPLE_DOMAINS)
- [私はこれをインストールするか、​それが私のウェブサイト上で動作することを保証する時間を費やす、​にしたくない；​それできますか？​私はあなたを雇うことができますか？](#user-content-PAY_YOU_TO_DO_IT)
- [あなたまたはこのプロジェクトの任意の開発者は雇用可能ですか？](#user-content-HIRE_FOR_PRIVATE_WORK)
- [私は専門家の変更、​カスタム化、​等が必要です；​手伝ってくれますか？](#user-content-SPECIALIST_MODIFICATIONS)
- [私は開発者、​ウェブサイトデザイナー、​またはプログラマーです。​このプロジェクトに関連する作業を行うことはできますか？](#user-content-ACCEPT_OR_OFFER_WORK)
- [私はプロジェクトに貢献したい；​これはできますか？](#user-content-WANT_TO_CONTRIBUTE)
- [Cronを使って自動的にアップデートできますか？](#user-content-CRON_TO_UPDATE_AUTOMATICALLY)
- [「違反」とは何ですか？](#user-content-WHAT_ARE_INFRACTIONS)
- [CIDRAMはホスト名をブロックできますか？](#user-content-BLOCK_HOSTNAMES)
- [「default_dns」には何が使えますか？](#default_dnsには何が使えますか)
- [CIDRAMを使用してウェブサイト以外のもの（メールサーバー、ＦＴＰ、ＳＳＨ、ＩＲＣ、など）を保護することはできますか？](#user-content-PROTECT_OTHER_THINGS)
- [ＣＤＮやキャッシュ・サービスを使用するのと同時にCIDRAMを使用すると問題が発生しますか？](#user-content-CDN_CACHING_PROBLEMS)
- [CIDRAMは、私のウェブサイトをＤＤｏＳ攻撃から守りますか？](#user-content-DDOS_ATTACKS)
- [アップデート・ページでモジュールまたはシグネチャ・ファイルを有効または無効にすると、コンフィギュレーションに英数字でソートされます。​彼らのソート方法を変更することはできますか？](#user-content-CHANGE_COMPONENT_SORT_ORDER)
- [「PDO DSN」とは何ですか？​CIDRAMでPDOを使用するにはどうすればよいですか？](#user-content-HOW_TO_USE_PDO)
- [CIDRAMはcronjobsをブロックしています。​これを修正する方法は？](#user-content-BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>「シグネチャ」とは何ですか？

CIDRAMの文脈では、​「シグネチャ」とは、​インジケータ/識別子として機能するデータである。​私たちはそれを使って、​探しているものを見つけます（通常はＩＰアドレスまたはＣＩＤＲです）。​しばしば、​それはCIDRAMのための何らかの命令を含む（応答する最善の方法、​等）。​CIDRAMの典型的なシグネチャは、​次のようになります。

「シグネチャ・ファイル」の場合：

`1.2.3.4/32 Deny Generic`

「モジュール」の場合：

```PHP
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*注意：​「シグネチャ・ファイル」のシグネチャと、「モジュール」のシグネチャは、同じではありません。*

しばしば（しかし、​常にではない）、​シグネチャは一緒に束ねられて「シグネチャセクション」を形成します。​コメント、​マークアップ、​および関連するメタデータが付いていることがよくあります（これは、​追加の文脈およびさらなる指示を提供するために使用することができる）。

#### <a name="WHAT_IS_A_CIDR"></a>「ＣＩＤＲ」とは何ですか？

「ＣＩＤＲ」は「Classless Inter-Domain Routing」（クラスレス・ドメイン間・ルーティング）の略語です *「[１](https://ja.wikipedia.org/wiki/Classless_Inter-Domain_Routing)、​[２](https://whatismyipaddress.com/cidr)」*。​この略語は、​このパッケージの名前の一部、​「CIDRAM」、​として使用されます。​「CIDRAM」は「Classless Inter-Domain Routing Access Manager」（クラスレス・ドメイン間・ルーティング・アクセス・マネージャー）の略語です。

しかし、​CIDRAMの文脈では（例えば、​このドキュメント内、​CIDRAMに関する議論の中で、​CIDRAM言語データ内）、​「CIDR」が言及されるたびに、​私たちの意図する意味は、​CIDR表記を使って表現されたサブネットです。​これは、​意味を明確にするためです（サブネットは複数の方法で表現できるため）。​したがって、​CIDRAMは「サブネット・アクセス・マネージャ」と見なすことができます。

この説明は、​提供された文脈とともに、​あいまいさを解決するのに役立つはずです。

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>「偽陽性」とは何ですか？

一般化された文脈で簡単に説明、​条件の状態をテストするときに、​結果を参照する目的で、​用語「偽陽性」（*または：偽陽性のエラー、​虚報；* 英語：*false positive*; *false positive error*; *false alarm*）の意味は、​結果は「陽性」のようです、​しかし結果は間違いです（即ち、​真の条件は「陽性/真」とみなされます、​しかしそれは本当に「陰性/偽」です）。​「偽陽性」は「泣く狼」に類似していると考えることができます（その状態は群の近くに狼がいるかどうかである、​真の条件は「偽/陰性」です、​群れの近くに狼がないからです、​しかし条件は「真/陽性」として報告されます、​羊飼いが「狼！​狼！​」を叫んだからです）、​または、​医療検査に類似、​患者が誤って診断されたとき。

いくつかの関連する用語は、​「真陽性」、​「真陰性」、​と「偽陰性」です。​これらの用語が示す意味：​「真陽性」の意味は、​テスト結果と真の条件が真です（即ち、​「陽性」です）。​「真陰性」の意味は、​テスト結果と真の条件が偽です（即ち、​「陰性」です）。​「真陽性」と「真陰性」は「正しい推論」とみなされます。​「偽陽性」の反対は「偽陰性」です。​「偽陰性」の意味は、​テスト結果が偽です（即ち、​「陰性」です）、​しかし、​真の条件が本当に真です（即ち、​「陽性」です）；​両方テスト結果と真の条件、​が「真/陽性」すべきであるはずです。

CIDRAMの文脈で、​これらの用語は、​CIDRAMのシグネチャとそれらがブロックするものを指します。​CIDRAMが誤ってＩＰアドレスをブロックすると（例えば、​不正確なシグネチャ、​時代遅れのシグネチャなどによる）、​我々はこのイベント「偽陽性」のを呼び出します。​CIDRAMがＩＰアドレスをブロックできなかった場合（例えば、​予期せぬ脅威、​シグネチャの欠落などによる）、​我々はこのイベント「不在検出」のを呼び出します（「偽陰性」のアナログです）。

これは、​以下の表に要約することができます。

&nbsp; | CIDRAMは、​ＩＰアドレスをブロック必要がありません | CIDRAMは、​ＩＰアドレスをブロック必要があります
---|---|---
CIDRAMは、​ＩＰアドレスをブロックしません | 真陰性（正しい推論） | 不在検出（それは「偽陰性」と同じです）
CIDRAMは、​ＩＰアドレスをブロックします | __偽陽性__ | 真陽性（正しい推論）

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>CIDRAMは国全体をブロックできますか？

はい。​これを行う最も簡単な方法は、BGPViewモジュールをインストールし、必要に応じて構成することです。

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>シグネチャはどれくらいの頻度でアップデイトされますか？

アップデイト頻度は、​シグネチャ・ファイルによって異なります。​CIDRAMのシグネチャ・ファイルのすべてのメンテナーが頻繁にアップデイトを試みる、​しかし、​私たちの皆様には、​他にもさまざまなコミットメントがあり、​私たちはプロジェクトの外で生活しており、​と誰も財政的に補償されていない、​したがって、​正確なアップデイトスケジュールは保証されません。​一般に、​十分な時間があればシグネチャがアップデイトされます。​メンテナーは必要性と範囲間の変化の頻度に基づいて優先順位をつけようとする。​あなたが何かを提供できるのであれば、​援助は常に高く評価されます。

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>CIDRAMを使用しているときに問題が発生しましたが、​何をすべきかわかりません！​助けてください！

- あなたは最新のソフトウェアバージョンを使用していますか？​あなたは最新のシグネチャ・ファイルバージョンを使用していますか？​そうでない場合は、​まずすべてをアップデイトしてください。​問題が解決しないかどうかをチェックしてください。​それが続く場合は、​読んでください。
- あなたはドキュメンテーションをチェックしましたか？​もしそうでなければ、​そうしてください。​ドキュメンテーションを使用して問題を解決できない場合は、​引き続き読んでください。
- **[イシュー・ページ](https://github.com/CIDRAM/CIDRAM/issues)** をチェックしましたか？​問題が以前に言及されているかどうかをチェックしてください。​提案、​アイデア、​ソリューションが提供されたかどうかをチェックしてください。
- 問題が解決しない場合は、​教えてください。​イシュー・ページに関する新しいディスカッションを作成する。

#### <a name="BLOCKED_WHAT_TO_DO"></a>私はCIDRAMによってウェブサイトからブロックされています！​助けてください！

CIDRAMは、​ウェブサイト所有者が望ましくないトラフィックをブロックする手段を提供します、​しかし、​ウェブサイト所有者は、​その使用方法を決定する必要があります。​シグネチャ・ファイルに誤検出がある場合、​訂正を行うことができる、​しかし、​特定のウェブサイトからブロック解除されていることに関して、​あなたはウェブサイト所有者に連絡する必要があります。​修正が行われると、​更新が必要になります。​それ以外の場合は、​問題を解決するのは彼らの責任です。​カスタム化と個人的な選択は、​私たちのコントロールを完全に超えています。

#### <a name="MINIMUM_PHP_VERSION_V3"></a>7.2より古いＰＨＰバージョンでCIDRAM（v2の場合）を使用したいと思います；​手伝ってくれますか？

いいえ。 PHP≥7.2 は CIDRAM v3 の最小要件です。

*参照：​[互換性チャート](https://maikuolan.github.io/Compatibility-Charts/)。*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>複数のドメインを保護するために１つのCIDRAMインストールを使用できますか？

はい。​CIDRAMのインストールは特定のドメインに限定されていません、​したがって、​複数のドメインを保護するために使用できます。​一般的に、​１つのドメインのみを保護するインストール、​私たちは「単一ドメイン・インストール」と呼んでいますで、​複数のドメイン/サブドメインを保護するインストール、​私たちは「マルチドメイン・インストール」と呼んでいます。​マルチドメインインストールを使用している場合で、​異なるドメインに異なるシグネチャ・ファイルセットを使用する必要がある場合や、​異なるドメインにCIDRAMを異なる設定する必要があります、​これを行うことができます。​コンフィギュレーション・ファイルをロードした後（`config.yml`）、​CIDRAMは、​リクエストされたドメインの「コンフィギュレーション・オーバーライド・ファイル」の存在をチェックします (`xn--48jua8kwd4hof5er493ch97b.tld.config.yml`)、​そして見つかった場合、​コンフィギュレーション・オーバーライド・ファイルによって定義されたコンフィギュレーション値は、​コンフィギュレーション・ファイルによって定義されたコンフィギュレーション値ではなく、​実行インスタンスに使用されます。​コンフィギュレーション・オーバーライド・ファイルは、​コンフィギュレーション・ファイルと同じです。​お客様の裁量で、​CIDRAMで利用可能なすべての設定指示句の全体または必要なサブセクションを含めることができます。​コンフィギュレーション・オーバーライド・ファイルは彼らが意図しているドメインに従って命名されます （そう、​例えば、​ドメイン`https://www.some-domain.tld/`にコンフィギュレーション・オーバーライド・ファイルが必要な場合は、​コンフィギュレーション・オーバーライド・ファイルの名前は`some-domain.tld.config.yml`にする必要があります。​通常の設定ファイルと同じ場所に保存する必要があります）。​ドメイン名は `HTTP_HOST` から来ます。​"www"は無視されます。

#### <a name="PAY_YOU_TO_DO_IT"></a>私はこれをインストールするか、​それが私のウェブサイト上で動作することを保証する時間を費やす、​にしたくない；​それできますか？​私はあなたを雇うことができますか？

多分。​これは、​ケースバイケースで検討されています。​あなたのニーズと提供できるものを教えてください。​私たちが助けることができるかどうかを教えてあげます。

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>あなたまたはこのプロジェクトの任意の開発者は雇用可能ですか？

*上記を参照。*

#### <a name="SPECIALIST_MODIFICATIONS"></a>私は専門家の変更、​カスタム化、​等が必要です；​手伝ってくれますか？

*上記を参照。*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>私は開発者、​ウェブサイトデザイナー、​またはプログラマーです。​このプロジェクトに関連する作業を行うことはできますか？

はい。​私たちのライセンスはこれを禁止していません。

#### <a name="WANT_TO_CONTRIBUTE"></a>私はプロジェクトに貢献したい；​これはできますか？

はい。​プロジェクトへの貢献は大歓迎です。​詳細については、​「CONTRIBUTING.md」を参照してください。

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>Cronを使って自動的にアップデートできますか？

はい。​外部スクリプトを介してアップデート・ページと対話するためのＡＰＩがフロントエンドに組み込まれています。​別のスクリプト、「[Cronable](https://github.com/Maikuolan/Cronable)」、が利用可能です。​これは「cron manager （クロン・マネージャー）」や「cron scheduler （クロン・スケジューラ）」がこれと他のサポートされているパッケージを自動的に更新するために使うことができます（このスクリプトは独自のドキュメントを提供しています）。

#### <a name="WHAT_ARE_INFRACTIONS"></a>「違反」とは何ですか？

「シグネチャの数」と「違反」はどちらも、特定のリクエスト中にトリガーされたシグネチャの重大度と数に、シグネチャ・ファイル、モジュール、補助ルール、などの理由に関係なく、関連しています。​ただし、「シグネチャの数」はその特定の要求に対してのみ持続しますが、「違反」は`default_tracktime`によって決定された数の要求にわたって持続する可能性があります。

これは、リクエストが十分な数の違反でブロックされた場合、同じソースからの後続のリクエストもブロックできるようになります。

#### <a name="BLOCK_HOSTNAMES"></a>CIDRAMはホスト名をブロックできますか？

はい。これは、補助ルールまたはカスタム・モジュールを作成することで実現できます。

![ホスト名をブロックするための補助ルール](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>「default_dns」には何が使えますか？

あなたが提案を探しているならば、「[public-dns.info](https://public-dns.info/)」と「[OpenNIC](https://servers.opennic.org/)」は既知の公開ＤＮＳサーバーの広範なリストを提供します。​または、次の表を参照してください：

ＩＰ | オペレーター
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

*注意：​私は、ＤＮＳサービス（リストされた、リストされていない、いずれの場合）のプライバシーの実践、セキュリティ、有効性、または信頼性に関して、いかなる請求または保証もしません。​決定を下す際には、あなた自身の研究をしてください。*

#### <a name="PROTECT_OTHER_THINGS"></a>CIDRAMを使用してウェブサイト以外のもの（メールサーバー、ＦＴＰ、ＳＳＨ、ＩＲＣ、など）を保護することはできますか？

それは（法的に）可能ですが、それは（実質的かつ技術的に）良い考えではありません。​CIDRAMライセンスは、どの技術がCIDRAMを実装するかを制限しません。​しかし、CIDRAMはＷＡＦ「ウェブ・アプリケーション・ファイアウォール」であり、常にウェブサイトを保護するためのものです。​他のテクノロジを念頭に置いて設計されたものではないため、他のテクノロジに対して効果的であるか、または信頼性の高い保護を提供する可能性は低いです。​実装が難しくなる可能性があり、偽陽性や不在検出のリスクは非常に高いです。

#### <a name="CDN_CACHING_PROBLEMS"></a>ＣＤＮやキャッシュ・サービスを使用するのと同時にCIDRAMを使用すると問題が発生しますか？

多分。​これは、サービスとそれをどのように使用しているかによって異なります。​一般的に、静的アセットのみをキャッシュする場合、問題はありません（静的アセットは、時間の経過とともに変化しないものを意味します；例えば、画像、CSS、など）。​しかし、要求に応じて動的に生成されるデータをキャッシュするときや、POST要求の結果をキャッシュしているときに問題が生じることがあります（これはあなたのウェブサイトとその環境を静的にし、CIDRAMは静的な環境で意味のある利益をもたらすことはまずありません）。​使用しているＣＤＮまたはキャッシュ・サービスに基づいて、CIDRAMに固有のコンフィギュレーション要件が存在する場合があります（ニーズに合わせてCIDRAMが正しく設定されていることを確認してください）。​コンフィギュレーションが正しくないと、重大な問題が発生することがあります。

#### <a name="DDOS_ATTACKS"></a>CIDRAMは、私のウェブサイトをＤＤｏＳ攻撃から守りますか？

短い答え：いいえ。

より詳細な答え：​CIDRAMは、望ましくないトラフィックがあなたのウェブサイトに及ぼす影響を軽減するのに役立ちます（ウェブサイトの帯域幅コストを削減します）、​望ましくないトラフィックがあなたのハードウェアに及ぼす影響を軽減するのに役立ちます（例えば、リクエストを処理して提供するサーバーの能力）、​望ましくないトラフィックに関連するその他のさまざまな潜在的な悪影響を軽減するのに役立ちます。​しかし、この質問を理解するためには、２つの重要なことを覚えておく必要があります。 １. CIDRAMはＰＨＰパッケージであるため、ＰＨＰがインストールされているマシンで動作します。​このため、CIDRAMは、サーバーがすでに要求を受信した後にのみ要求を表示およびブロックできます。 ２. 効果的なＤＤｏＳ軽減は、ＤＤｏＳ攻撃の対象となるサーバーに到達する前に要求をフィルタリングする必要があります。​理想的には、ＤＤｏＳ攻撃は、ターゲット・サーバーに到達する前に、攻撃に関連するトラフィックをドロップまたは再ルーティングできるソリューションによって検出および緩和する必要があります。

これは、専用のオンプレミス・ハードウェア・ソリューション、専用のＤＤｏＳ軽減サービスなどのクラウド・ベースのソリューション、ＤＤｏＳ対応ネットワークを介してドメインのＤＮＳをルーティング、クラウド・ベースのフィルタリング、またはそれらのいくつかの組み合わせを使用して実施することができる。​いずれにしても、この主題はちょうど単なる段落または２つで完全に説明するのは少し複雑すぎる。​これがあなたが追求したい科目であれば、さらなる研究をすることをお勧めします。​ＤＤｏＳ攻撃の真の性質が適切に理解されている場合、この回答はより理にかなっています。

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>アップデート・ページでモジュールまたはシグネチャ・ファイルを有効または無効にすると、コンフィギュレーションに英数字でソートされます。​彼らのソート方法を変更することはできますか？

はい。​特定の順序で実行するファイルが必要な場合は、コンフィギュレーション・ディレクティブの名前の前に任意のデータを追加できます（このデータと名前を区切るためにコロンを使用します）。​その後、アップデート・ページでファイルを再度並べ替えると、この追加された任意のデータがソート順に影響します。​これにより、それらの名前を変更せずに、必要な順序で実行されます。

例えば、次のようにファイルをコンフィギュレーション・ディレクティブがあるとします：

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

`file3.php`を最初に実行したければ、ファイル名の前に`aaa:`のようなものを追加することができます：

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

次に、新しいファイル`file6.php`が有効になっている場合、アップデート・ページがそれらをすべて並べ替えると、次のようになります：

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

ファイルが非アクティブになったときと同じ状況です。​逆に、ファイルを最後に実行したい場合は、ファイルの名前の前に`zzz:`のようなものを追加することができます。​いずれの場合でも、問題のファイルの名前を変更する必要はありません。

#### <a name="HOW_TO_USE_PDO"></a>「PDO DSN」とは何ですか？​CIDRAMでPDOを使用するにはどうすればよいですか？

「PDO」は「[PHP Data Objects](https://www.php.net/manual/ja/intro.pdo.php)」の頭字語です。​さまざまなPHPアプリケーションで一般的に使用されるデータベース・システムに接続できるように、PHPのインターフェイスを提供します。

「DSN」は「[data source name](https://en.wikipedia.org/wiki/Data_source_name)」（データ・ソース名）の頭字語です。​「PDO DSN」は、PDOがデータベースに接続する方法を説明しています。

CIDRAMは、キャッシュにPDOを利用するオプションを提供します。​これが適切に機能するためには、それに応じてCIDRAMのコンフィギュレーションを設定する必要があります（したがって、PDOを有効にします）、次にCIDRAMが使用する新しいデータベースを作成します（CIDRAMが使用するデータベースをまだ考慮していない場合）、次に、以下に説明する構造に従って、データベースに新しいテーブルを作成します。

データベース接続は成功したが、必要なテーブルが存在しない場合、それは自動的に作成しようとします。​ただし、この動作は十分にテストされていないため、成功を保証することはできません。

もちろん、これは、CIDRAMで実際にPDOを使用する場合にのみ適用されます。​フラット・ファイル・キャッシュ（デフォルトのコンフィギュレーションに従って）、または提供されているその他のさまざまなキャッシュオプションを使用することに満足している場合は、データベース、テーブルなどの設定に悩む必要はありません。

以下で説明する構造では、データベース名として「cidram」を使用していますが、DSN構成で同じ名前が複製される限り、データベースに任意の名前を使用できます。

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

CIDRAMの「`pdo_dsn`」コンフィギュレーション・ディレクティブは、次のように設定する必要があります。

```
使用するデータベース・ドライバーに応じて...
├─4d （警告：実験的、未テスト、非推奨！）
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └データベースを見つけるために接続するホスト。
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └データベース使用する名前。
│                │              │
│                │              └ホストに接続するポート番号。
│                │
│                └データベースを見つけるために接続するホスト。
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └データベース使用する名前。
│    │          │
│    │          └データベースを見つけるために接続するホスト。
│    │
│    └可能な値：「mssql」、「sybase」、「dblib」。
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├ローカル・データベース・ファイルへのパスにすることができます。
│                    │
│                    ├ホストとポート番号で接続できます。
│                    │
│                    └これを使用する場合は、Firebirdのドキュメントを参照してください。
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └接続するカタログ化されたデータベース。
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └接続するカタログ化されたデータベース。
├─mysql （最も推奨されます！）
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └ホストに接続するポート番号。
│                 │            │
│                 │            └データベースを見つけるために接続するホスト。
│                 │
│                 └データベース使用する名前。
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├特定のカタログ化されたデータベースを参照できます。
│               │
│               ├ホストとポート番号で接続できます。
│               │
│               └これを使用する場合は、Oracleのドキュメントを参照してください。
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├特定のカタログ化されたデータベースを参照できます。
│         │
│         ├ホストとポート番号で接続できます。
│         │
│         └これを使用する場合は、ODBC/DB2のドキュメントを参照してください。
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └データベース使用する名前。
│               │              │
│               │              └ホストに接続するポート番号。
│               │
│               └データベースを見つけるために接続するホスト。
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └使用するローカル・データベース・ファイルへのパス。
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └データベース使用する名前。
                   │         │
                   │         └ホストに接続するポート番号。
                   │
                   └データベースを見つけるために接続するホスト。
```

DSNの特定の部分に何を使用するかわからない場合は、何も変更せずに、DSNがそのまま機能するかどうかを最初に確認してください。

「`pdo_username`」と「`pdo_password`」は、データベース用に選択したユーザー名とパスワードと同じでなければならないことに注意してください。

#### <a name="BLOCK_CRON"></a>CIDRAMはcronjobsをブロックしています。​これを修正する方法は？

Cronjobsの目的で専用ファイルを使用している場合、通常のユーザー・リクエスト中にそのファイルを呼び出す必要がない場合（つまり、cronjobsのコンテキスト外）、これを修正する最も簡単な方法は、cronjobs中にCIDRAMがまったく実行されないようにすることです（つまり、cronjobsの処理を担当するファイルには、CIDRAMをフックしない）。

あるいは、それが不可能な場合、ただし、cronサーバーのIPアドレスは比較的一貫性があり予測可能な場合、cronサーバーのIPアドレスをホワイトリストに登録してみてできます。​これを行うには、カスタム・シグネチャ・ファイルにホワイトリスト・シグネチャを作成するか、補助ルールを作成できます。​CronサーバーのIPアドレスが定期的にローテーションし、特に予測できない場合、しかし、それにもかかわらず、同じ特定のネットワーク内から残ります場合、`ignore.dat`ファイルに、それをそもそもブロックするシグネチャ・セクションの名前をリストすることができます。

これらのアイデアをすべて試したが、どれも役に立たなかった場合、または、その方法を理解するのに助けが必要な場合、CIDRAMのissuesページで新しいissueを作成できます。

---


### ９.<a name="SECTION9"></a>法律情報

#### 9.0 セクション・プリアンブル

ドキュメンテーションのこのセクションは、パッケージの使用と実装に関する法律上の考慮事項を説明し、基本的な関連情報を提供することを目的としています。​これは、操作している国に存在する可能性のある法的要件の遵守を確実にする手段として、一部のユーザーにとって重要な場合があります。​一部のユーザーは、この情報に従ってウェブサイトポリシーを調整する必要があります。

まず、私（パッケージ作成者）は弁護士ではない、有資格の法律専門家でもないことを認識してください。​したがって、私は法律上のアドバイスを提供する法的資格はありません。​また、場合によっては、正確な法的要件は、国や地域によって異なる場合があります。​また、これらが競合することがあります​（例えば：[プライバシーの権利](https://ja.wikipedia.org/wiki/%E3%83%97%E3%83%A9%E3%82%A4%E3%83%90%E3%82%B7%E3%83%BC)を享受する国と[忘れられる権利](https://ja.wikipedia.org/wiki/%E5%BF%98%E3%82%8C%E3%82%89%E3%82%8C%E3%82%8B%E6%A8%A9%E5%88%A9)の場合には、拡張されたデータ保持を望む国と比較して）。​また、パッケージへのアクセスが特定の国や管轄区域に限定されているわけではないので、パッケージのユーザーベースは地理的に多様である可能性が高いと考えてください。​これらの点を考慮して、私はすべての点で、すべてのユーザーにとって「法的に準拠する」であることが何を意味するかを述べる立場にはいません。​ただし、ここに記載されている情報が、パッケージの文脈で法的に遵守するために必要な作業を自分で決定するのに役立つことを願っています。​疑義が存続する場合、または法的な観点から追加の助けと助言が必要な場合は、有資格の法律専門家に相談することをおすすめします。

#### 9.1 責任

パッケージ・ライセンスに記載されている通り、パッケージは無保証で提供されます。​これには、すべての責任範囲が含まれます（ただしこれに限定されません）。​あなたの便宜のためにパッケージが提供されています。​それが有用であり、それがあなたのためにいくつかの利益をもたらすことが期待されます。​しかし、あなたがパッケージを使用するか実装するかは、あなた自身の選択です。​あなたはパッケージを使用するよう強制されません。​しかし、あなたが決めるところでは、あなたはその決定に責任があります。​あなたの意思決定の結果について、私と他のパッケージ寄稿者は、直接的、間接的、暗示的、またはその他の方法にかかわらず、責任を負いません。

#### 9.2 第三者

その正確なコンフィギュレーションと実装に応じて、パッケージは場合によっては第三者と通信し、情報を共有することがあります。​この情報は、いくつかの国において、状況によっては、「[個人識別情報](https://ja.wikipedia.org/wiki/%E5%80%8B%E4%BA%BA%E6%83%85%E5%A0%B1)」（ＰＩＩ）と定義することができます。

これらの第三者がこの情報をどのように使用するかは、これらの第三者によって定められたさまざまなポリシーの対象となります。​このドキュメントの範囲外です。​ただし、このような場合は、これらの第三者との情報の共有を無効にすることができます。​そのような場合は、有効にすることを選択した場合、これらの第三者によるＰＩＩのプライバシー、セキュリティ、および使用に関する懸念事項を調査することは、おあなたの責任です。​ご不明な点がある場合、またはＰＩＩに関してこれらの第三者の行為に不満がある場合は、これらの第三者との情報の共有をすべて無効にすることが最善の方法です。

透明性のために、共有される情報のタイプと、誰と、以下に記載されています。

##### 9.2.0 ホスト名検索

ホスト名を扱う機能やモジュールを使用している場合（例えば、「危険なホスト・ブロッカー・モジュール」、「tor project exit nodes block module」、「サーチ・エンジン・ベリフィケーション」）、CIDRAMは、インバウンド要求のホスト名を何らかの形で取得できる必要があります。​通常、ＤＮＳサーバーからの着信要求のＩＰアドレスのホスト名を要求するか、またはCIDRAMがインストールされているシステムによって提供される機能によって情報を要求します（これは通常、「ホスト名検索」として知られています）。​デフォルトで定義されているＤＮＳサーバーは[Google DNS](https://dns.google.com/)サービスに属しています（これはコンフィギュレーションによって簡単に変更できます）。​通信される正確なサービスは構成可能であり、パッケージの構成方法によって異なります。​CIDRAMがインストールされているシステムで提供される機能を使用する場合は、システム管理者に連絡して、ホスト名検索で使用するルートを判断する必要があります。​影響を受けるモジュールを避けるか、必要に応じてパッケージ構成を変更して、CIDRAMでホスト名検索を防止できます。

*関連するコンフィギュレーション・ディレクティブ：*
- `general` -> `allow_gethostbyaddr_lookup`
- `general` -> `default_dns`
- `general` -> `force_hostname_lookup`
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.1 検索エンジンの検証 （サーチ・エンジン・ベリフィケーション） ＋ ソーシャル・メディアの検証 （ソーシャル・メディア・ベリフィケーション）

これらのコンフィギュレーション・ディレクティブを有効にすると、CIDRAMは、検索エンジンやソーシャルメディアから発信されたと思われるリクエストの信憑性を検証するために、「転送ＤＮＳルックアップ」を実行しようとします。​これを行うために、[Google DNS](https://dns.google.com/)サービスを使用して、これらのインバウンド・リクエストのホスト名からＩＰアドレスを解決しようとします（このプロセスでは、これらのインバウンド・リクエストのホスト名はサービスと共有されます）。

*関連するコンフィギュレーション・ディレクティブ：*
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.2 キャプチャ

CIDRAMはreCAPTCHAとhCAPTCHAをサポートしています。​正しく機能するには、ＡＰＩキーが必要です。​これらはデフォルトで無効になっていますが、必要なＡＰＩキーを構成することで有効になる場合があります。​有効にすると、サービスとCIDRAMまたはユーザーのブラウザとの間で通信が発生する場合があります。​これには、ユーザーのＩＰアドレス、ユーザー・エージェント、オペレーティング・システム、およびリクエストで利用可能なその他の詳細などの情報の通信が含まれる可能性があります。

##### 9.2.3 STOP FORUM SPAM （ストップ・フォーラム・スパム）

[Stop Forum Spam](https://www.stopforumspam.com/)は、スパマーからフォーラム、ブログ、ウェブサイトを保護するのに役立つ、無料で利用できる素晴らしいサービスです。​これは、既知のスパマーのデータベースと、ＩＰアドレス、ユーザー名、または電子Ｅメール・アドレスがそのデータベースにリストされているかどうかを確認するために利用できるＡＰＩを提供することによってこれを行います。

CIDRAMは、このＡＰＩを利用するオプショナル・モジュールを提供します。​インバウンド・リクエストのＩＰアドレスが疑わしいスパマーに属するかどうかをチェックします。​モジュールがインストールされ、アクティブ化されると、モジュールはユーザーのＩＰアドレスをサービスと共有するがあります。

##### 9.2.4 ABUSEIPDB

CIDRAMは、[AbuseIPDB](https://www.abuseipdb.com/) APIを使用して虐待的なＩＰアドレスをブロックするためのオプションのモジュールを提供します。​モジュールがインストールされ、アクティブ化されると、モジュールはユーザーのＩＰアドレスをサービスと共有するがあります。

##### 9.2.5 BGPVIEW

CIDRAMは、[BGPView](https://bgpview.io/) APIを使用してＡＳＮおよび国コードのルックアップを実行するオプショナル・モジュールを提供します。​これらのルックアップにより、ＡＳＮまたは原産国に基づいてリクエストをブロックまたはホワイトリストに登録できます。​モジュールがインストールされ、アクティブ化されると、モジュールはユーザーのＩＰアドレスをサービスと共有するがあります。

##### 9.2.6 PROJECT HONEYPOT

CIDRAMは、[Project Honeypot](https://www.projecthoneypot.org/) APIを使用して虐待的なＩＰアドレスをブロックするためのオプションのモジュールを提供します。​モジュールがインストールされ、アクティブ化されると、モジュールはユーザーのＩＰアドレスをサービスと共有するがあります。

#### 9.3 ロギング

ロギングは、多くの理由からCIDRAMの重要な部分です。​ブロック・イベントをロギングせずに、偽陽性が発生した場合、それを診断して解決することは困難です。​ロギングせずに、CIDRAMがいかに効果的に実行されているかを確かめること、その潜在的な問題を確認すること、機能させるために必要なコンフィギュレーションやシグネチャの変更を決定するのが難しいことがあります。​いずれにせよ、ロギングは一部のユーザーには望ましくなく、完全にオプションです。​CIDRAMでは、デフォルトでロギングは無効になっています。​これを有効にするには、それに応じてCIDRAMを設定する必要があります。

ロギングが法的に許可されているかどうか、および法的に許容される範囲で​（例えば、ログに記録される可能性があるタイプの情報、期間、および状況）、​管轄区域およびCIDRAMが実施されている状況に応じて変わる可能性がある​（例えば、あなたが個人として、企業として、商業的または非商業的に動作しているかどうか）。​したがって、このセクションを注意深く読んで役に立つかもしれない。

CIDRAMが実行できる複数のタイプのロギングがあります。​異なるタイプのロギングには、さまざまな理由で異なるタイプの情報が含まれます。

##### 9.3.0 ブロック・イベント

CIDRAMが実行できる主なタイプのロギングは、「ブロック・イベント」に関係します。​このタイプのロギングは、CIDRAMが要求をブロックする時期に関係し、３つの異なる形式で提供できます：
- 人間が読めるログ・ファイル。
- Apacheスタイル・ログ・ファイル。
- シリアライズされたログ・ファイル。

人間が読めるログ・ファイルに記録されたブロック・イベントは、通常次のようになります（例として）：

```
ＩＤ：1234
スクリプトのバージョン：CIDRAM v1.6.0
日/月/年/時刻：Day, dd Mon 20xx hh:ii:ss +0000
ＩＰアドレス：x.x.x.x
ホスト名：dns.hostname.tld
シグネチャの数：1
シグネチャリファレンス：x.x.x.x/xx
なぜブロックされましたか：クラウド・サービス ("Network Name", Lxx:Fx, [XX])!
ユーザーエージェント：Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
ＵＲＩ再構築された：https://your-site.tld/index.php
キャプチャ・ステータス：オン。
```

Apacheスタイル・ログ・ファイルに記録された同じブロック・イベントは、次のようになります：

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

ログに記録されたブロック・イベントには、通常、次の情報が含まれます。
- ブロック・イベントを参照するＩＤ番号。
- 現在使用中のCIDRAMのバージョン。
- ブロック・イベントが発生した日時。
- ブロックされた要求のＩＰアドレス。
- ブロックされた要求のＩＰアドレスのホスト名（使用可能な場合）。
- 要求によってトリガーされたシグネチャの数。
- トリガされたシグネチャへの参照。
- ブロック・イベントの理由、およびいくつかの基本的な関連するデバッグ情報。
- ブロックされた要求のユーザー・エージェント（すなわち、要求側エンティティが要求に対してどのように自身を識別する）。
- 要求されたリソースの識別子の再構成。
- 現在のリクエストのキャプチャ・ステータス（該当する場合）。

*このタイプのロギングを担当するコンフィギュレーション・ディレクティブは、利用可能な３つのフォーマットのそれぞれについて。*
- `logging` -> `apache_style_log`
- `logging` -> `serialised_log`
- `logging` -> `standard_log`

これらのディレクティブを空のままにすると、このタイプのロギングは無効のままです。

##### 9.3.1 キャプチャ・ロギング

このタイプのロギングは、特にキャプチャ・インスタンスに関連し、ユーザーがキャプチャ・インスタンスを完了しようとした場合にのみ発生します。

キャプチャ・ログ・エントリには、キャプチャ・インスタンスを完了しようとしているユーザーのＩＰアドレス、試行が行われた日時、およびキャプチャのステータスが含まれます。​キャプチャ・ログ・エントリは通常、次のようになります（例として）。

```
ＩＰアドレス：x.x.x.x - 日/月/年/時刻：Day, dd Mon 20xx hh:ii:ss +0000 - キャプチャのステータス：合格！
```

*キャプチャ・ロギングを担当するコンフィギュレーション・ディレクティブ：*
- `hcaptcha` -> `hcaptcha_log`
- `recaptcha` -> `recaptcha_log`

##### 9.3.2 フロントエンド・ロギング

このロギングは、フロントエンドのログイン試行に関係します。​これは、ユーザーがフロントエンドにログインしようとするとき、およびフロントエンド・アクセスが有効な場合にのみ発生します。

フロントエンドのログ・エントリには、ログインしようとしているユーザーのＩＰアドレス、試行が行われた日時、試行の結果が含まれます（正常にログインしたか、ログインに失敗しました）。​フロントエンドのログ・エントリは通常、次のようになります（例として）。

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - ログインしました。
```

*フロントエンド・ロギングを担当するコンフィギュレーション・ディレクティブ：*
- `frontend` -> `frontend_log`

##### 9.3.3 ログ・ローテーション

一定期間後にログをパージしたい場合や、法律によってログをパージする必要がある場合があります（例えば、ログを保持することが法的に許可される時間は、法律によって制限される場合があります）。​ログ・ローテーションを使用すると、指定された制限を超えるとログ・ファイルに対して何らかのアクションを実行できます。​パッケージ・コンフィギュレーションで指定されたログ・ファイルの名前に日付/時刻マーカーを含めることし（例えば、`{yyyy}-{mm}-{dd}.log`）、ログ・ローテーションを有効にするで、これを行うことができます。

例えば：法的に３０日後にログを削除する必要がある場合は、ログ・ファイルの名前に`{dd}.log`を（`{dd}`は日を表す）指定し、`log_rotation_limit`の値を`30`に設定し、`log_rotation_action`の値を`Delete`に設定することができます。

逆に、長期間ログを保持する必要がある場合は、ログ・ローテーションを無効にするか、ログ・ファイルを圧縮するために`log_rotation_action`の値を`Archive`に設定することができます（占有するディスク・スペースの総量が削減されます）。

*関連するコンフィギュレーション・ディレクティブ：*
- `logging` -> `log_rotation_action`
- `logging` -> `log_rotation_limit`

##### 9.3.4 ログ切り捨て

必要に応じて、特定のサイズを超えた個々のログ・ファイルを切り捨てることができます。

*関連するコンフィギュレーション・ディレクティブ：*
- `logging` -> `truncate`

##### 9.3.5 ＩＰアドレス・スドニマイゼーション

まず、あなたが用語に精通していない場合：​「スドニマイゼーション」（pseudonymisation）とは、補足情報なしで特定のデータ対象に特定できないような個人データの処理を指します​（ただし、そのような補足情報は、個人データが自然人に特定されないことを保証するために、個別に維持され、技術的および組織的措置を受けるものとします）。

次のリソースは詳細情報を提供します。
- [[trust-hub.com] What is pseudonymisation?](https://www.trust-hub.com/news/what-is-pseudonymisation/)
- [[Wikipedia] Pseudonymization](https://en.wikipedia.org/wiki/Pseudonymization)

場合によっては、収集、処理、または保存されたＰＩＩに対して「アノニマイゼーション」または「スドニマイゼーション」を実施することが法的に要求されることがあります。​このコンセプトはかなり以前から存在していましたが、ＧＤＰＲ/ＤＳＶＧＯは「スドニマイゼーション」を特に言及し、奨励しています。

必要に応じて、CIDRAMはＩＰアドレスを記録するときにこれを行うことができます。​ログに記録されると、ＩＰｖ４アドレスの最後のオクテット、およびＩＰｖ６アドレスの２番目の部分の後のすべてが、「x」として表される。​これは、本質的には、ＩＰｖ４アドレスを２４番目のサブネット・ファクタの最初のアドレスに丸め、ＩＰｖ６アドレスを３２番目のサブネット・ファクタの最初のアドレスに丸めます。

*注意：CIDRAMのＩＰアドレス・スドニマイゼーションは、CIDRAMのＩＰトラッキング機能には影響しません。​これが問題の場合は、ＩＰトラッキングを完全に無効にすることをお勧めします。*

*関連するコンフィギュレーション・ディレクティブ：*
- `legal` -> `pseudonymise_ip_addresses`

##### 9.3.6 ログ情報を省略

特定の種類の情報が完全にログに記録されないようにして、これをさらに進めたい場合は、これも可能です。​コンフィギュレーション・ページで、「`fields`」コンフィギュレーション・ディレクティブを参照して、ログ・エントリおよび「アクセス拒否」ページに表示されるフィールドを制御してください。

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

*注意：ログからＩＰアドレスを完全に省略するときにＩＰアドレス・スドニマイゼーションを使用する理由はありません。*

*関連するコンフィギュレーション・ディレクティブ：*
- `general` -> `fields`

##### 9.3.7 統計（スタティスティックス）

CIDRAMは、オプションで、特定の時間以降に発生したブロック・イベントまたはキャプチャ・インスタンスの総数などの統計を追跡できます。​この機能はデフォルトで無効になっていますが、パッケージ・コンフィギュレーションで有効にすることができます。​この機能は、発生したイベントの総数のみを追跡します。​特定のイベントに関する情報は含まれていませんので、ＰＩＩと見なされるべきではありません。

*関連するコンフィギュレーション・ディレクティブ：*
- `general` -> `statistics`

##### 9.3.8 暗号化 （エンクリプション）

CIDRAMは、キャッシュまたはログ情報を[暗号化](https://ja.wikipedia.org/wiki/%E6%9A%97%E5%8F%B7)しません。​キャッシュとログの暗号化は、将来導入される可能性がありますが、現在のところ具体的な計画はありません。​権限のない第三者によるＰＩＩへのアクセスについて（例えば、キャッシュ、ログ）：​CIDRAMは、一般にアクセス可能な場所にはインストールしないことをお勧めします（例えば、ほとんどのウェブサーバーで使用できる標準の`public_html`ディレクトリの外にCIDRAMをインストールする）、​そして適切に制限された権限が強制されるようにする（特に、「vault」ディレクトリ）。​懸念が残っている場合は、CIDRAMを設定して、この情報が収集または記録されないようにすることができます​（例えば、ロギングを無効にするなど）。

#### 9.4 COOKIES （クッキー）

CIDRAMは、コードベースの2つのポイントで[Cookie](https://ja.wikipedia.org/wiki/HTTP_cookie)を設定します。 １.ユーザーがキャプチャ・インスタンスを正常に完了すると（これは、`lockuser`が`true`に設定されていると仮定します）、CIDRAMは、ユーザーがすでにキャプチャ・インスタンスを完了しているという後続の要求を覚えておくために、Cookieを設定します。​この方法では、後続のリクエストでキャプチャ・インスタンスを完了するようユーザーに継続的に要求する必要はありません。 ２.ユーザーがフロントエンドに正常にログインすると、CIDRAMは後続のリクエストのためにユーザーを覚えておくためにCookieを設定します（すなわち、Cookieはユーザーをログインセッションに認証するために使用されます）。

いずれの場合も、Cookieに関する警告が目立つように表示され（該当する場合）、Cookieが関連するアクションに関与する場合にCookieが設定されることをユーザーに警告します。​Cookieは、コードベースの他のどの場所にも設定されていません。

*注意：「インビジブル」キャプチャＡＰＩは、一部の法域ではクッキー法と互換性がない可能性があります。​クッキー法の対象となるウェブサイトはそれを避けるべきです。​代わりに、提供されている他のＡＰＩを使用するか、キャプチャを完全に無効にすることを選択することをお勧めします。*

*関連するコンフィギュレーション・ディレクティブ：*
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 9.5 マーケティングやアドバタイジング

CIDRAMは、マーケティングやアドバタイジング目的で情報を収集または処理しません。​収集または記録された情報を販売したり、利益を得たりすることはありません。​CIDRAMは商業的企業ではなく、商業的利益には関係しないので、これらのことは意味をなさないでしょう。​これは、プロジェクトの開始以来のケースであり、今日も引き続き行われています。​さらに、これらのことを行うことは、プロジェクトの精神と目的に沿ったものではなく、私がプロジェクトを維持し続ける限り、決して起こらないでしょう。

#### 9.6 プライバシー・ポリシー

場合によっては、ウェブサイトのすべてのページとセクションにプライバシー・ポリシーへのリンクを明確に表示することが法的に要求されることがあります。​これは、ユーザーが正確なプライバシー・プラクティス、収集するＰＩＩのタイプ、および使用する方法を十分に知らされていることを保証する手段として重要です。​このようなリンクをCIDRAMの「アクセス拒否」ページに含めるには、プライバシー・ポリシーのＵＲＬを指定するためのコンフィギュレーション・ディレクティブが用意されています。

*注意：​プライバシー・ポリシー・ページは、CIDRAMの保護の背後に置かないことを強くお勧めします。​CIDRAMがプライバシー・ポリシー・ページを保護し、CIDRAMによってブロックされたユーザーがプライバシー・ポリシーへのリンクをクリックすると、ユーザーは再びブロックされ、プライバシー・ポリシーが表示されなくなります。​理想的には、ＨＴＴＰページやプレーン・テキスト・ファイルなど、プライバシー・ポリシーの静的コピーにリンクする。*

*関連するコンフィギュレーション・ディレクティブ：*
- `legal` -> `privacy_policy`

#### 9.7 GDPR/DSGVO

一般データ保護規制（ＧＤＰＲ）は、2018年5月25日に発効するＥＵの規制です。​規制の第一の目的は、ＥＵ市民および居住者に個人情報を管理させ、個人情報および個人情報に関するＥＵ内の規制を統一することです。

この規制には、ＥＵ（欧州連合）の「データ主体」（識別された、または識別可能な自然人）の「[個人識別情報](https://ja.wikipedia.org/wiki/%E5%80%8B%E4%BA%BA%E6%83%85%E5%A0%B1)」（ＰＩＩ）の処理に関する特定の規定が含まれています。​規制に準拠するためには、「企業」（規制によって定義されている）、関連するシステムおよびプロセスは、デフォルトで「<a href="https://ja.wikipedia.org/wiki/%E3%83%97%E3%83%A9%E3%82%A4%E3%83%90%E3%82%B7%E3%83%BC%E3%83%90%E3%82%A4%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3">プライバシー・バイ・デザイン</a>」を実装する必要があります、最高のプライバシー設定を使用する必要があります、格納された情報または処理された情報のためにセーフガードを実装する必要があります（「スドニマイゼーション」の実装またはデータの完全な「アノニマイゼーション」を含むがこれらに限定されません）、収集するデータの種類、処理方法、理由、保持期間、および第三者とこのデータを共有するかどうかを明確かつ明白に宣言する必要があります、第三者と共有されるデータの種類、方法、理由などが含まれます。

規制によって定義されているように、合法的な根拠がない限り、データを処理することはできません。​一般的に、これは、合法的な基準でデータ対象のデータを処理するためには、法的義務を遵守しなければならないを意味します、または明示され、十分に情報があり、明白な同意がデータ対象から得られた後にのみ行われる。

規制のいくつかの側面は時間とともに変化する可能性があります。​時代遅れの情報が広がらないようにするには、関係する情報をここに入れるのではなく、正式な情報源から規制について学ぶ方が良いでしょう（ここに含まれる情報が古くなる可能性があります）。

より多くの情報を習得するための推奨リソース：
- [GDPR（EU一般データ保護規制）とは | 語句説明・適用範囲・与える影響を解説](https://boxil.jp/mag/a4605/)
- [EU一般データ保護規則](https://ja.wikipedia.org/wiki/EU%E4%B8%80%E8%88%AC%E3%83%87%E3%83%BC%E3%82%BF%E4%BF%9D%E8%AD%B7%E8%A6%8F%E5%89%87)
- [GDPR（EU一般データ保護規制）対策](https://eizone.info/gdpr/)
- [REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679)
- [GDPRの対象となる個人データとは](https://www.eyjapan.jp/services/advisory/column/2017-06-06.html)

---


最終アップデート：２０２３年３月２５日。
