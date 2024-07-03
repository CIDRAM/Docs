## Documentação para CIDRAM v3 (Português).

### Conteúdo
- 1. [PREÂMBULO](#user-content-SECTION1)
- 2. [COMO INSTALAR](#user-content-SECTION2)
- 3. [COMO USAR](#user-content-SECTION3)
- 4. [GESTÃO DE FRONT-END](#user-content-SECTION4)
- 5. [OPÇÕES DE CONFIGURAÇÃO](#user-content-SECTION5)
- 6. [FORMATO DE ASSINATURAS](#user-content-SECTION6)
- 7. [PROBLEMAS DE COMPATIBILIDADE CONHECIDOS](#user-content-SECTION7)
- 8. [PERGUNTAS MAIS FREQUENTES (FAQ)](#user-content-SECTION8)
- 9. [INFORMAÇÃO LEGAL](#user-content-SECTION9)
- 10. [ATUALIZANDO DE VERSÕES PRINCIPAIS ANTERIORES](#user-content-SECTION10)

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### 1. <a name="SECTION1"></a>PREÂMBULO

CIDRAM (Classless Inter-Domain Routing Access Manager) é um script PHP projetados para proteger sites por bloqueando solicitações provenientes de endereços IP considerado como sendo fontes de tráfego indesejável, incluindo (mas não limitado a) o tráfego dos pontos de acesso não-humanos, serviços em nuvem, spambots, raspadores/scrapers, etc. Ele faz isso via calculando as possíveis CIDRs dos endereços IP fornecida a partir de solicitações de entrada e em seguida tentando comparar estas possíveis CIDRs contra os seus arquivos de assinaturas (estas arquivos de assinaturas contêm listas de CIDRs de endereços IP considerado como sendo fontes de tráfego indesejável); Se forem encontradas correspondências, as solicitações estão bloqueadas.

*(Vejo: [O que é um "CIDR"?](#user-content-WHAT_IS_A_CIDR)).*

[CIDRAM](https://cidram.github.io/) COPYRIGHT 2016 e além GNU/GPLv2 através do [Caleb M (Maikuolan)](https://github.com/Maikuolan).

Este script é livre software; você pode redistribuí-lo e/ou modificá-lo de acordo com os termos da GNU General Public License como publicada pela Free Software Foundation; tanto a versão 2 da Licença, ou (em sua opção) qualquer versão posterior. Este script é distribuído na esperança que possa ser útil, mas SEM QUALQUER GARANTIA; sem mesmo a implícita garantia de COMERCIALIZAÇÃO ou ADEQUAÇÃO A UM DETERMINADO FIM. Consulte a GNU General Public License para obter mais detalhes, localizado no `LICENSE.txt` arquivo e disponível também desde:
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

Este documento e seu pacote associado pode ser baixado gratuitamente de:
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [SourceForge](https://sourceforge.net/projects/cidram/).

---


### 2. <a name="SECTION2"></a>COMO INSTALAR

#### 2.0 INSTALANDO MANUALMENTE

Em primeiro lugar, você precisará de uma nova cópia do CIDRAM para trabalhar. Você pode baixar um arquivo da versão mais recente do CIDRAM do repositório [CIDRAM/CIDRAM](https://github.com/CIDRAM/CIDRAM). Especificamente, você precisará de uma nova cópia do diretório "vault" (tudo do arquivo, exceto o diretório "vault" e seu conteúdo, pode ser excluído ou desconsiderado com segurança).

Antes da v3, era necessário instalar o CIDRAM em algum lugar dentro de sua raiz pública para poder acessar o front-end do CIDRAM. No entanto, a partir da v3, isso não é necessário, e para maximizar a segurança e prevenir o acesso não autorizado ao CIDRAM e seus arquivos, é recomendado em vez disso instalar o CIDRAM *fora* de sua raiz pública. Não importa exatamente onde você escolhe instalar o CIDRAM, contanto que esteja em algum lugar acessível por PHP, em algum lugar razoavelmente seguro, e em algum lugar com o qual você esteja satisfeito. Também não é mais necessário manter o nome do diretório "vault", então você pode renomear "vault" para o nome que preferir (mas por conveniência, a documentação continuará a se referir a ele como o diretório "vault").

Quando estiver pronto, carregue o diretório "vault" para o local escolhido e certifique-se de que ele tenha as permissões necessárias para que o PHP possa gravar no diretório (dependendo do sistema em questão, às vezes você não precisará fazer nada, ou às vezes precisará definir CHMOD 755 para o diretório, ou se houver problemas com 755, você pode tentar 777, mas 777 não é recomendado por ser menos seguro).

Em seguida, para que o CIDRAM possa proteger sua base de código ou CMS, você precisará criar um "ponto de entrada". Tal ponto de entrada consiste em três coisas:

1. Inclusão do arquivo "loader.php" em um ponto apropriado em sua base de código ou CMS.
2. Instanciação do CIDRAM core.
3. Chamando o método "protect".

Um exemplo simples:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

Se você estiver usando um servidor web Apache e tiver acesso ao `php.ini`, você pode usar a diretiva `auto_prepend_file` para preceder o CIDRAM sempre que qualquer solicitação do PHP for feita. Nesse caso, o local mais apropriado para criar seu ponto de entrada seria em seu próprio arquivo, e você citaria esse arquivo na diretiva `auto_prepend_file`.

Exemplo:

`auto_prepend_file = "/path/to/your/entrypoint.php"`

Ou isso no arquivo `.htaccess`:

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

Em outros casos, o local mais apropriado para criar seu ponto de entrada seria o mais cedo possível dentro de sua base de código ou CMS para sempre ser carregado sempre que alguém acessar qualquer página em todo o seu site. Se sua base de código utiliza um "bootstrap", um bom exemplo seria no início do seu arquivo "bootstrap". Se a sua base de código tiver um arquivo central responsável por se conectar ao seu banco de dados, outro bom exemplo seria no início desse arquivo central.

#### 2.1 INSTALANDO COM COMPOSER

[CIDRAM está registrado no Packagist](https://packagist.org/packages/cidram/cidram), e então, se você estiver familiarizado com o Composer, poderá usar o Composer para instalar o CIDRAM.

`composer require cidram/cidram`

#### 2.2 INSTALANDO PARA WORDPRESS

[CIDRAM está registrado como um plugin com o banco de dados de plugins do WordPress](https://wordpress.org/plugins/cidram/), e você pode instalar CIDRAM diretamente do painel de plugins. Você pode instalá-lo da mesma maneira que qualquer outro plugin, e nenhuma etapa de adição é necessária.

*Atenção: A atualização do CIDRAM através do painel de plugins resulta numa instalação limpa! Se você personalizou sua instalação (mudou sua configuração, instalados módulos, etc), estas personalizações serão perdidas quando atualizando através do painel de plugins! Os arquivos de log também serão perdidos ao atualizar através do painel de plugins! Para preservar arquivos de log e personalizações, atualize através da página de atualizações de front-end do CIDRAM.*

#### 2.3 CONFIGURAÇÃO E CUSTOMIZAÇÃO

É altamente recomendável que você revise a configuração de sua nova instalação para poder ajustá-la de acordo com suas necessidades. Você também pode querer instalar módulos adicionais, arquivos de assinatura, criar regras auxiliares, ou implementar outras personalizações para que sua instalação possa atender melhor às suas necessidades. Eu recomendo usar o front-end para fazer essas coisas.

---


### 3. <a name="SECTION3"></a>COMO USAR

CIDRAM deve bloquear automaticamente as solicitações indesejáveis para o seu site sem necessidade de qualquer assistência manual, Além de sua instalação inicial.

Você pode personalizar a sua configuração e personalizar quais CIDRs são bloqueados por modificando seu arquivo de configuração e/ou seus arquivos de assinaturas.

Se você encontrar quaisquer falsos positivos, entre em contato comigo para me informar sobre isso. *(Vejo: [O que é um "falso positivo"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM pode ser atualizado manualmente ou através do front-end. CIDRAM também pode ser atualizado via Composer ou WordPress, se originalmente instalado por esses meios.

---


### 4. <a name="SECTION4"></a>GESTÃO DE FRONT-END

#### 4.0 O QUE É O FRONT-END.

O front-end fornece uma maneira conveniente e fácil de manter, gerenciar e atualizar sua instalação CIDRAM. Você pode visualizar, compartilhar e baixar arquivos de log através da página de logs, você pode modificar a configuração através da página de configuração, você pode instalar e desinstalar componentes através da página de atualizações, e você pode carregar, baixar e modificar arquivos no seu vault através do gerenciador de arquivos.

#### 4.1 COMO ACESSAR O FRONT-END.

Semelhante a como você precisava criar um ponto de entrada para que o CIDRAM protegesse seu site, você também precisará criar um ponto de entrada para acessar o front-end. Tal ponto de entrada consiste em três coisas:

1. Inclusão do arquivo "loader.php" em um ponto apropriado em sua base de código ou CMS.
2. Instanciação do CIDRAM front-end.
3. Chamando o método "view".

Um exemplo simples:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

A classe "FrontEnd" estende a classe "Core", o que significa que, se você quiser, pode chamar o método "protect" antes o método "view" para bloquear o tráfego potencialmente indesejado de acessar o front-end. Fazer isso é totalmente opcional.

Um exemplo simples:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

O local mais apropriado para criar um ponto de entrada para o front-end é em seu próprio arquivo dedicado. Ao contrário do ponto de entrada criado anteriormente, você deseja que seu ponto de entrada front-end seja acessível apenas solicitando diretamente o arquivo específico em que o ponto de entrada existe, portanto, nesse caso, você não desejará usar `auto_prepend_file` ou `.htaccess`.

Depois de criar seu ponto de entrada para o front-end, use seu navegador para acessá-lo. Você deve ser apresentado com uma página de login. Na página de login, digite o nome de usuário e senha padrão (admin/password) e pressione o botão de login.

Nota: Depois de efetuar login pela primeira vez, a fim de impedir o acesso não autorizado ao front-end, você deve imediatamente alterar seu nome de usuário e senha! Isto é muito importante, porque é possível fazer upload de código PHP arbitrário para o seu site através do front-end.

Além disso, para uma segurança ideal, é recomendável ativar a "autenticação de dois fatores" para todas as contas front-end (instruções fornecidas abaixo).

#### 4.2 COMO USAR O FRONT-END.

As instruções são fornecidas em cada página do front-end, para explicar a maneira correta de usá-lo e sua finalidade pretendida. Se precisar de mais explicações ou qualquer assistência especial, entre em contato com o suporte. Alternativamente, existem alguns vídeos disponíveis no YouTube que podem ajudar por meio de demonstração.

#### 4.3 AUTENTICAÇÃO DE DOIS FATORES

É possível tornar o front-end mais seguro ativando a autenticação de dois fatores ("2FA"). Ao fazer login numa conta ativada para 2FA, um e-mail é enviado para o endereço de e-mail associado a essa conta. Este e-mail contém um "código 2FA", que o usuário deve inserir, além do nome de usuário e da senha, para poder fazer login usando essa conta. Isso significa que a obtenção de uma senha de conta não seria suficiente para que qualquer hacker ou atacante em potencial pudesse fazer login nessa conta, já que eles também precisam ter acesso ao endereço de e-mail associado a essa conta para poder receber e utilizar o código 2FA associado à sessão, assim tornando assim o front-end mais seguro.

Em primeiro lugar, para ativar a autenticação de dois fatores, usando a página de atualizações do front-end, instale o componente PHPMailer. O CIDRAM utiliza o PHPMailer para enviar e-mails.

Depois de instalar o PHPMailer, você precisará preencher as diretivas de configuração do PHPMailer por meio da página de configuração para CIDRAM ou do arquivo de configuração. Mais informações sobre essas diretivas de configuração estão incluídas na seção de configuração deste documento. Depois de preencher as diretivas de configuração do PHPMailer, defina `enable_two_factor` para `true`. A autenticação de dois fatores agora deve estar ativada.

Em seguida, você precisará associar um endereço de e-mail a uma conta para que o CIDRAM saiba para onde enviar códigos 2FA ao fazer login com essa conta. Para fazer isso, use o endereço de e-mail como o nome de usuário da conta (como `foo@bar.tld`), ou incluir o endereço de e-mail como parte do nome de usuário da mesma forma que você faria ao enviar um e-mail normalmente (como `Foo Bar <foo@bar.tld>`).

Nota: Proteger seu vault contra acesso não autorizado (p.e., por meio de endurecendo as permissões de segurança e de acesso público do seu servidor), é particularmente importante aqui, devido a esse acesso não autorizado ao seu arquivo de configuração (que é armazenado no seu vault), pode arriscar expor suas configurações de SMTP (incluindo nome de usuário e senha SMTP). Você deve garantir que seu vault esteja adequadamente protegido antes de ativar a autenticação de dois fatores. Se você não conseguir fazer isso, então, pelo menos, você deve criar uma nova conta de e-mail, dedicada para essa finalidade, a fim de reduzir os riscos associados às configurações SMTP expostas.

---


### 5. <a name="SECTION5"></a>OPÇÕES DE CONFIGURAÇÃO

O seguinte é uma lista de variáveis encontradas no `config.yml` arquivo de configuração para CIDRAM, juntamente com uma descrição de sua propósito e função.

```
Configuração (v3)
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

#### "general" (Categoria)
Configuração geral (qualquer configuração principal que não pertença a outras categorias).

##### "stages" `[string]`
- Controles para as etapas da cadeia de execução (se ativado, se os erros são registrados, etc).

```
stages
├─Tests ("Executar testes para os arquivos de assinatura")
├─Modules ("Executar módulos")
├─SearchEngineVerification ("Executar verificação dos motores de busca")
├─SocialMediaVerification ("Executar verificação de mídia social")
├─OtherVerification ("Executar outra verificação")
├─Aux ("Executar regras auxiliares")
├─Tracking ("Executar monitoração de IP")
├─RL ("Executar a limitação de taxa")
├─CAPTCHA ("Implantar CAPTCHAs (solicitações bloqueadas)")
├─Reporting ("Executar relatórios")
├─Statistics ("Atualizar estatísticas")
├─Webhooks ("Executar webhooks")
├─PrepareFields ("Preparar campos para saída e logs")
├─Output ("Gerar saída (solicitações bloqueadas)")
├─WriteLogs ("Gravar nos logs (solicitações bloqueadas)")
├─Terminate ("Encerrar a solicitação (solicitações bloqueadas)")
├─AuxRedirect ("Redirecionar de acordo com regras auxiliares")
└─NonBlockedCAPTCHA ("Implantar CAPTCHAs (solicitações não bloqueadas)")
```

##### "fields" `[string]`
- Controles para os campos durante eventos de bloqueio (quando uma solicitação é bloqueada).

```
fields
├─ID ("ID")
├─ScriptIdent ("Versão do script")
├─DateTime ("Data/Hora")
├─IPAddr ("Endereço IP")
├─IPAddrResolved ("Endereço IP (resolvido)")
├─Query ("Query")
├─Referrer ("Referenciador")
├─UA ("Agente do usuário")
├─UALC ("Agente do usuário (minúscula)")
├─SignatureCount ("Contagem da assinaturas")
├─Signatures ("Assinaturas referência")
├─WhyReason ("Razão bloqueada")
├─ReasonMessage ("Razão bloqueada (detalhado)")
├─rURI ("Reconstruído URI")
├─Infractions ("Infrações")
├─ASNLookup ("** Pesquisa de ASN")
├─CCLookup ("** Pesquisa de código de país")
├─Verified ("Identidade verificada")
├─Expired ("Expirado")
├─Ignored ("Ignorado")
├─Request_Method ("Método de solicitação")
├─Protocol ("Protocolo")
├─SEC_CH_UA_PLATFORM ("!! SEC_CH_UA_PLATFORM")
├─SEC_CH_UA_MOBILE ("!! SEC_CH_UA_MOBILE")
├─SEC_CH_UA ("!! SEC_CH_UA")
├─Hostname ("Nome do host")
├─CAPTCHA ("Estado CAPTCHA")
├─Inspection ("* Inspeção do condições")
└─ClientL10NAccepted ("Resolução de idioma")
```

* Destina-se apenas à depuração de regras auxiliares. Não exibido para usuários bloqueados.

** Requer funcionalidade de pesquisa ASN (por exemplo, através do módulo IP-API ou BGPView).

!! Esta é uma dica do cliente de baixa entropia. As dicas de cliente são uma tecnologia web nova e experimental que ainda não é amplamente suportada em todos os navegadores e principais clientes. *Ver: <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA#browser_compatibility" dir="ltr" hreflang="en-US" rel="noopener noreferrer external">Sec-CH-UA - HTTP | MDN</a>.* Embora as dicas do cliente possam ser úteis para impressão digital, já que não são amplamente suportadas, sua presença nas solicitações não deve ser assumida nem confiável. (ou seja, bloquear com base na ausência é uma má ideia).

##### "timezone" `[string]`
- Isso é usado para especificar o fuso horário a ser usado (por exemplo, Africa/Cairo, America/New_York, Asia/Tokyo, Australia/Perth, Europe/Berlin, Pacific/Guam, etc). Especifique "SYSTEM" para permitir que o PHP lide com isso automaticamente.

```
timezone
├─SYSTEM ("Usar o fuso horário padrão do sistema.")
├─UTC ("UTC")
└─…Outros
```

##### "time_offset" `[int]`
- Deslocamento do fuso horário em minutos.

##### "time_format" `[string]`
- O formato de notação de data/tempo utilizado pelo CIDRAM. Opções adicionais podem ser adicionadas mediante solicitação.

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
└─…Outros
```

__*Espaço reservado – Explicação – Exemplo baseado em 2024-04-30T18:27:49+08:00.*__<br />
`{yyyy}` – O ano – Por exemplo, 2024.<br />
`{yy}` – O ano abreviado – Por exemplo, 24.<br />
`{Mon}` – O nome abreviado do mês (em inglês) – Por exemplo, Apr.<br />
`{mm}` – O mês com zeros à esquerda – Por exemplo, 04.<br />
`{m}` – O mês – Por exemplo, 4.<br />
`{Day}` – O nome abreviado do dia (em inglês) – Por exemplo, Tue.<br />
`{dd}` – O dia com zeros à esquerda – Por exemplo, 30.<br />
`{d}` – O dia – Por exemplo, 30.<br />
`{hh}` – A hora com zeros à esquerda (usa o formato de 24 horas) – Por exemplo, 18.<br />
`{h}` – A hora (usa o formato de 24 horas) – Por exemplo, 18.<br />
`{ii}` – O minuto com zeros à esquerda – Por exemplo, 27.<br />
`{i}` – O minuto – Por exemplo, 27.<br />
`{ss}` – O segundo com zeros à esquerda – Por exemplo, 49.<br />
`{s}` – O segundo – Por exemplo, 49.<br />
`{tz}` – O fuso horário (sem dois pontos) – Por exemplo, +0800.<br />
`{t:z}` – O fuso horário (com dois pontos) – Por exemplo, +08:00.

##### "ipaddr" `[string]`
- Onde encontrar o IP endereço das solicitações? (Útil por serviços como o Cloudflare e tal). Padrão = REMOTE_ADDR. ATENÇÃO: Não mude isso a menos que você saiba o que está fazendo!

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (Padrão)")
└─…Outros
```

Veja também:
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### "http_response_header_code" `[int]`
- Qual mensagem de status HTTP deve enviar o CIDRAM ao bloquear solicitações?

```
http_response_header_code
├─200 (200 OK): Menos robusto, mas mais amigável de usar. As solicitações automatizadas
│ provavelmente interpretarão essa resposta como indicação de que a
│ solicitação foi bem-sucedida.
├─403 (403 Forbidden (Proibido)): Um pouco mais robusto, mas um pouco menos amigável de usar. Recomendado
│ para a maioria das circunstâncias gerais.
├─410 (410 Gone (Se foi)): Pode causar problemas ao resolver falsos positivos, pois alguns navegadores
│ armazenam em cache essa mensagem de status e não enviam solicitações
│ subsequentes, mesmo após terem sido desbloqueadas. Pode ser o mais
│ preferível em alguns contextos, para certos tipos de tráfego.
├─418 (418 I'm a teapot (Eu sou um bule)): Referências uma piada de primeiro de abril (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Muito improvável de ser
│ entendido por qualquer cliente, bot, navegador, ou outro. Fornecido para
│ diversão e conveniência, mas geralmente não recomendado.
├─451 (451 Unavailable For Legal Reasons (Indisponível por motivos legais)): Recomendado ao bloquear principalmente por motivos legais. Não recomendado
│ em outros contextos.
└─503 (503 Service Unavailable (Serviço indisponível)): Mais robusto, mas menos amigável de usar. Recomendado para quando sob
  ataque, ou para lidar com tráfego indesejado extremamente persistente.
```

##### "silent_mode" `[string]`
- Deve CIDRAM silenciosamente redirecionar as tentativas de acesso bloqueadas em vez de exibir o "acesso negado" página? Se sim, especificar o local para redirecionar as tentativas de acesso bloqueadas para. Se não, deixe esta variável em branco.

##### "silent_mode_response_header_code" `[int]`
- Qual mensagem de status HTTP deve enviar o CIDRAM ao redirecionar silenciosamente as tentativas de acesso bloqueados?

```
silent_mode_response_header_code
├─301 (301 Moved Permanently (Movido Permanentemente)): Instrui o cliente que o redirecionamento é PERMANENTE, e que o método de
│ solicitação usado para o redirecionamento PODE ser diferente do método de
│ solicitação usado na solicitação inicial.
├─302 (302 Found (Encontrado)): Instrui o cliente que o redirecionamento é TEMPORÁRIO, e que o método de
│ solicitação usado para o redirecionamento PODE ser diferente do método de
│ solicitação usado na solicitação inicial.
├─307 (307 Temporary Redirect (Redirecionamento Temporário)): Instrui o cliente que o redirecionamento é TEMPORÁRIO, e que o método de
│ solicitação usado para o redirecionamento NÃO pode ser diferente do
│ método de solicitação usado para a solicitação inicial.
└─308 (308 Permanent Redirect (Redirecionamento Permanente)): Instrui o cliente que o redirecionamento é PERMANENTE, e que o método de
  solicitação usado para o redirecionamento NÃO pode ser diferente do
  método de solicitação usado para a solicitação inicial.
```

Independentemente de como instruímos o cliente, é importante lembrar que não temos controle sobre o que o cliente escolhe fazer, e não há garantia de que o cliente honrará nossas instruções.

##### "lang" `[string]`
- Especificar o padrão da linguagem por CIDRAM.

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
- Localizar de acordo com HTTP_ACCEPT_LANGUAGE sempre que possível? True = Sim [Padrão]; False = Não.

##### "numbers" `[string]`
- Como você prefere que os números sejam exibidos? Selecione o exemplo que parece mais correto para você.

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
- Se você desejar, você pode fornecer um endereço de e-mail aqui a ser dado para os usuários quando eles estão bloqueadas, para eles para usar como um ponto de contato para suporte e/ou assistência no caso de eles sendo bloqueado por engano ou em erro. AVISO: Qualquer endereço de e-mail que você fornecer aqui certamente vai ser adquirido por spambots e raspadores/scrapers durante o curso de seu ser usada aqui, e assim, é fortemente recomendado que, se você optar por fornecer um endereço de e-mail aqui, que você garantir que o endereço de e-mail você fornecer aqui é um endereço descartável e/ou um endereço que você não é importante (em outras palavras, você provavelmente não quer usar seu pessoal principal ou negócio principal endereço de e-mail).

##### "emailaddr_display_style" `[string]`
- Como você prefere que o endereço de e-mail seja apresentado aos usuários?

```
emailaddr_display_style
├─default ("Link clicável")
└─noclick ("Texto não-clicável")
```

##### "ban_override" `[int]`
- Sobrepor "http_response_header_code" quando "infraction_limit" é excedido? 200 = Não sobrepor [Padrão]. Outros valores são os mesmos que os valores disponíveis para "http_response_header_code".

```
ban_override
├─200 (200 OK): Menos robusto, mas mais amigável de usar. As solicitações automatizadas
│ provavelmente interpretarão essa resposta como indicação de que a
│ solicitação foi bem-sucedida.
├─403 (403 Forbidden (Proibido)): Um pouco mais robusto, mas um pouco menos amigável de usar. Recomendado
│ para a maioria das circunstâncias gerais.
├─410 (410 Gone (Se foi)): Pode causar problemas ao resolver falsos positivos, pois alguns navegadores
│ armazenam em cache essa mensagem de status e não enviam solicitações
│ subsequentes, mesmo após terem sido desbloqueadas. Pode ser o mais
│ preferível em alguns contextos, para certos tipos de tráfego.
├─418 (418 I'm a teapot (Eu sou um bule)): Referências uma piada de primeiro de abril (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Muito improvável de ser
│ entendido por qualquer cliente, bot, navegador, ou outro. Fornecido para
│ diversão e conveniência, mas geralmente não recomendado.
├─451 (451 Unavailable For Legal Reasons (Indisponível por motivos legais)): Recomendado ao bloquear principalmente por motivos legais. Não recomendado
│ em outros contextos.
└─503 (503 Service Unavailable (Serviço indisponível)): Mais robusto, mas menos amigável de usar. Recomendado para quando sob
  ataque, ou para lidar com tráfego indesejado extremamente persistente.
```

##### "default_dns" `[string]`
- Uma lista de servidores DNS a serem usados para pesquisas de nomes de host. ATENÇÃO: Não mude isso a menos que você saiba o que está fazendo!

__FAQ.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.pt.md#o-que-posso-usar-para-default_dns" hreflang="pt">O que posso usar para "default_dns"?</a>*

##### "default_algo" `[string]`
- Define qual algoritmo usar para todas as futuras senhas e sessões.

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### "statistics" `[string]`
- Controla quais informações estatísticas rastrear.

```
statistics
├─Blocked-IPv4 ("Solicitações bloqueadas – IPv4")
├─Blocked-IPv6 ("Solicitações bloqueadas – IPv6")
├─Blocked-Other ("Solicitações bloqueadas – Outros")
├─Banned-IPv4 ("Solicitações banidas – IPv4")
├─Banned-IPv6 ("Solicitações banidas – IPv6")
├─Passed-IPv4 ("Solicitações aprovadas – IPv4")
├─Passed-IPv6 ("Solicitações aprovadas – IPv6")
├─Passed-Other ("Solicitações aprovadas – Outros")
├─CAPTCHAs-Failed ("CAPTCHA tentativas – Falhou!")
├─CAPTCHAs-Passed ("CAPTCHA tentativas – Sucesso!")
├─Reported-IPv4-OK ("Solicitações relatados para APIs externos – IPv4 – OK")
├─Reported-IPv4-Failed ("Solicitações relatados para APIs externos – IPv4 – Falhou")
├─Reported-IPv6-OK ("Solicitações relatados para APIs externos – IPv6 – OK")
└─Reported-IPv6-Failed ("Solicitações relatados para APIs externos – IPv6 – Falhou")
```

Nota: O rastreamento de estatísticas para regras auxiliares pode ser controlado na página de regras auxiliares.

##### "force_hostname_lookup" `[bool]`
- Forçar pesquisas de nome de anfitrião? True = Sim; False = Não [Padrão]. As pesquisas de nome de anfitrião normalmente são realizadas com base na necessidade, mas pode ser forçado para todos os solicitações. Isso pode ser útil como forma de fornecer informações mais detalhadas nos arquivos de log, mas também pode ter um efeito ligeiramente negativo sobre o desempenho.

##### "allow_gethostbyaddr_lookup" `[bool]`
- Permitir pesquisas gethostbyaddr quando o UDP não está disponível? True = Sim [Padrão]; False = Não.

Nota: As pesquisas de IPv6 podem não funcionar corretamente em alguns sistemas de 32 bits.

##### "disabled_channels" `[string]`
- Isso pode ser usado para impedir que o CIDRAM use canais específicos ao enviar solicitações (por exemplo, ao atualizar, ao buscar metadados de componentes, etc).

```
disabled_channels
├─GitHub ("GitHub")
├─BitBucket ("BitBucket")
└─GoogleDNS ("GoogleDNS")
```

##### "default_timeout" `[int]`
- Tempo limite padrão a ser usado para solicitações externas? Padrão = 12 segundos.

##### "sensitive" `[string]`
- Uma lista de caminhos a serem considerados como páginas confidenciais. Cada caminho listado será verificado em relação ao URI reconstruído quando necessário. Um caminho que começa com uma barra será tratado como um literal, e correspondido a partir do componente de caminho da solicitação em diante. Como alternativa, um caminho que começa com um caractere não alfanumérico, e termina com o mesmo caractere (ou o mesmo caractere mais um sinalizador "i" opcional) será tratado como uma expressão regular. Qualquer outro tipo de caminho será tratado como um literal, e pode corresponder a qualquer parte do URI. O fato de um caminho ser considerado uma página confidencial pode afetar o comportamento de alguns módulos, mas não tem nenhum efeito de outra forma.

##### "email_notification_address" `[string]`
- Se você optou por receber notificações do CIDRAM por e-mail, por exemplo, quando regras auxiliares específicas são desencadeadas, você pode especificar o endereço do destinatário dessas notificações aqui.

##### "email_notification_name" `[string]`
- Se você optou por receber notificações do CIDRAM por e-mail, por exemplo, quando regras auxiliares específicas são desencadeadas, você pode especificar o nome do destinatário dessas notificações aqui.

#### "components" (Categoria)
Configuração para ativação e desativação dos componentes utilizados pelo CIDRAM. Normalmente preenchido pela página de atualizações, mas também pode ser gerenciado aqui para um controle mais preciso e para componentes personalizados não reconhecidos pela página de atualizações.

##### "ipv4" `[string]`
- Arquivos de assinaturas IPv4.

##### "ipv6" `[string]`
- Arquivos de assinaturas IPv6.

##### "modules" `[string]`
- Módulos.

##### "imports" `[string]`
- Importações. Normalmente usado para fornecer informações de configuração de um componente ao CIDRAM.

##### "events" `[string]`
- Manipuladores de eventos. Normalmente usado para modificar a maneira como o CIDRAM se comporta internamente ou para fornecer funcionalidade adicional.

#### "logging" (Categoria)
Configuração relacionada ao log (excluindo o que é aplicável a outras categorias).

##### "standard_log" `[string]`
- Um arquivo legível por humanos para registrar todas as tentativas de acesso bloqueadas. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

Dica útil: Você pode anexar informações de data/hora aos nomes dos arquivos de log usando espaços reservados de formato de hora. Os espaços reservados para formato de hora disponíveis são exibidos em <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "apache_style_log" `[string]`
- Um arquivo no estilo da Apache para registrar todas as tentativas de acesso bloqueadas. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

Dica útil: Você pode anexar informações de data/hora aos nomes dos arquivos de log usando espaços reservados de formato de hora. Os espaços reservados para formato de hora disponíveis são exibidos em <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "serialised_log" `[string]`
- Um arquivo serializado para registrar todas as tentativas de acesso bloqueadas. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

Dica útil: Você pode anexar informações de data/hora aos nomes dos arquivos de log usando espaços reservados de formato de hora. Os espaços reservados para formato de hora disponíveis são exibidos em <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "error_log" `[string]`
- Um arquivo para registrar erros detectados que não são fatais. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

Dica útil: Você pode anexar informações de data/hora aos nomes dos arquivos de log usando espaços reservados de formato de hora. Os espaços reservados para formato de hora disponíveis são exibidos em <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "outbound_request_log" `[string]`
- Um arquivo para registrar os resultados de quaisquer solicitações de saída. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

Dica útil: Você pode anexar informações de data/hora aos nomes dos arquivos de log usando espaços reservados de formato de hora. Os espaços reservados para formato de hora disponíveis são exibidos em <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "report_log" `[string]`
- Um arquivo para registrar quaisquer relatórios enviados para APIs externas. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

Dica útil: Você pode anexar informações de data/hora aos nomes dos arquivos de log usando espaços reservados de formato de hora. Os espaços reservados para formato de hora disponíveis são exibidos em <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "truncate" `[string]`
- Truncar arquivos de log quando atingem um determinado tamanho? Valor é o tamanho máximo em B/KB/MB/GB/TB que um arquivo de log pode crescer antes de ser truncado. O valor padrão de 0KB desativa o truncamento (arquivos de log podem crescer indefinidamente). Nota: Aplica-se a arquivos de log individuais! O tamanho dos arquivos de log não é considerado coletivamente.

##### "log_rotation_limit" `[int]`
- A rotação de log limita o número de arquivos de log que devem existir a qualquer momento. Quando novos arquivos de log são criados, se o número total de arquivos de log exceder o limite especificado, a ação especificada será executada. Você pode especificar o limite desejado aqui. Um valor de 0 desativará a rotação de log.

##### "log_rotation_action" `[string]`
- A rotação de log limita o número de arquivos de log que devem existir a qualquer momento. Quando novos arquivos de log são criados, se o número total de arquivos de log exceder o limite especificado, a ação especificada será executada. Você pode especificar a ação desejada aqui.

```
log_rotation_action
├─Delete ("Deletar os arquivos de log mais antigos, até o limite não seja mais excedido.")
└─Archive ("Primeiramente arquivar, e então deletar os arquivos de log mais antigos, até o limite não seja mais excedido.")
```

##### "log_banned_ips" `[bool]`
- Incluir solicitações bloqueadas de IPs banidas nos arquivos de log? True = Sim [Padrão]; False = Não.

##### "log_sanitisation" `[bool]`
- Ao usar o front-end página para os arquivos de log para exibir dados de log, o CIDRAM sanitiza os dados de log antes de exibi-los, para proteger os usuários contra ataques XSS e outras ameaças potenciais que os dados de log podem conter. No entanto, por padrão, os dados não são sanitizados durante o registro. Isso é para assegurar que os dados de log sejam preservados com precisão, para auxiliar qualquer análise heurística ou forense que possa ser necessária no futuro. No entanto, no caso de um usuário tentar ler dados de log usando ferramentas externas, e se essas ferramentas externas não realizarem seu próprio processo de sanitização, o usuário pode estar exposto a ataques XSS. Se necessário, você pode alterar o comportamento padrão usando esta diretiva de configuração. True = Sanitize dados ao registrá-lo (os dados são preservados com menos precisão, mas o risco de XSS é menor). False = Não sanitize dados ao registrá-lo (os dados são preservados com mais precisão, mas o risco de XSS é maior) [Padrão].

#### "frontend" (Categoria)
Configuração para o front-end.

##### "frontend_log" `[string]`
- Arquivo para registrar tentativas de login ao front-end. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

Dica útil: Você pode anexar informações de data/hora aos nomes dos arquivos de log usando espaços reservados de formato de hora. Os espaços reservados para formato de hora disponíveis são exibidos em <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signatures_update_event_log" `[string]`
- Um arquivo para registrar quando as assinaturas são atualizadas por meio do front-end. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

Dica útil: Você pode anexar informações de data/hora aos nomes dos arquivos de log usando espaços reservados de formato de hora. Os espaços reservados para formato de hora disponíveis são exibidos em <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "max_login_attempts" `[int]`
- Número máximo de tentativas de login ao front-end. Padrão = 5.

##### "theme" `[string]`
- Tema padrão a ser usado para o front-end.

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
└─…Outros
```

##### "magnification" `[float]`
- Ampliação de fonte. Padrão = 1.

##### "custom_header" `[string]`
- Inserido como HTML no início de todas as páginas do front-end. Isso pode ser útil caso você queira incluir um logotipo de site, cabeçalho personalizado, scripts, ou similares em todas essas páginas.

##### "custom_footer" `[string]`
- Inserido como HTML no final de todas as páginas do front-end. Isso pode ser útil caso você queira incluir um aviso legal, link de contato, informações comerciais, ou similares em todas essas páginas.

##### "remotes" `[string]`
- Uma lista dos endereços usados pelo atualizador para buscar metadados de componentes. Isso pode precisar ser ajustado ao atualizar para uma nova versão principal, ou ao adquirir uma nova fonte para atualizações, mas em circunstâncias normais deve ser deixado de lado.

##### "enable_two_factor" `[bool]`
- Esta diretiva determina se deve usar 2FA para contas front-end.

#### "signatures" (Categoria)
Configuração para assinaturas, arquivos de assinatura, módulos, etc.

##### "shorthand" `[string]`
- Controla o que fazer com uma solicitação quando há uma correspondência positiva com uma assinatura que utiliza as palavras curtas fornecidas.

```
shorthand
├─Attacks ("Ataques")
├─Bogon ("⁰ Bogon IP")
├─Cloud ("Serviço de nuvem")
├─Generic ("Genérico")
├─Legal ("¹ Legais")
├─Malware ("Malware")
├─Proxy ("² Proxy")
├─Spam ("Risco de spam")
├─Banned ("³ Banido")
├─BadIP ("³ IP inválido")
├─RL ("³ Taxa limitada")
└─Other ("⁴ Outros")
```

__0.__ Se seu site precisar de acesso via LAN ou localhost, não bloqueie isso. Caso contrário, você pode bloquear isso.

__1.__ Nenhum dos arquivos de assinatura padrão usa isso, mas é suportado mesmo assim, caso possa ser útil para alguns usuários.

__2.__ Se você precisar que os usuários possam acessar seu site por meio de proxies, não bloqueie isso. Caso contrário, você pode bloquear isso.

__3.__ O uso direto em assinaturas não é suportado, mas pode ser invocado por outros meios em circunstâncias específicas.

__4.__ Refere-se aos casos em que as palavras curtas não são usadas, ou não são reconhecidas pelo CIDRAM.

__Um por assinatura.__ Uma assinatura pode invocar vários perfis, mas pode usar apenas uma palavra curta. É possível que várias palavras curtas podem ser adequadas, mas como apenas uma pode ser usada, procuramos sempre usar apenas a mais adequada.

__Prioridade.__ Uma opção selecionada sempre tem prioridade sobre uma opção não selecionada. Por exemplo, se várias palavras curtas estiverem em jogo, mas apenas uma delas estiver definida como bloqueada, a solicitação ainda será bloqueada.

__Pontos finais humanos e serviços em nuvem.__ O serviço em nuvem pode se referir a provedores de hospedagem na web, farms de servidores, data centers, ou uma série de coisas diferentes. Ponto final humano refere-se ao meio pelo qual um humano acessa a internet, como por meio de um provedor de serviços de internet. Uma rede geralmente fornece apenas um ou outro, mas às vezes pode fornecer ambos. Visamos nunca identificar pontos finais humanos potenciais como serviços em nuvem. Portanto, um serviço de nuvem pode ser identificado como outra coisa se seu alcance for compartilhado por pontos finais humanos conhecidos. Vice versa, visamos sempre identificar serviços em nuvem, cujos alcances não são compartilhados por nenhum ponto final humano conhecido, como serviços em nuvem. Portanto, uma solicitação identificada explicitamente como um serviço de nuvem provavelmente não compartilha seu alcances com nenhum pontos finais humanos conhecidos. Da mesma forma, uma solicitação identificada explicitamente por ataques ou risco de spam provavelmente os compartilha. No entanto, a internet está sempre em fluxo, os propósitos das redes mudam ao longo do tempo, e os alcances estão sempre sendo comprados ou vendidos, portanto, permaneça ciente e vigilante em relação a falsos positivos.

##### "default_tracktime" `[string]`
- A duração pela qual os endereços IP devem ser rastreados. Padrão = 7d0°0′0″ (1 semana).

##### "infraction_limit" `[int]`
- Número máximo de infrações que um IP pode incorrer antes de ser banido por monitoração IP. Padrão = 10.

##### "tracking_override" `[bool]`
- Permitir que os módulos substituem as opções de monitoração? True = Sim [Padrão]; False = Não.

#### "verification" (Categoria)
Configuração para verificar a origem das solicitações.

##### "search_engines" `[string]`
- Controles para verificar solicitações de mecanismos de pesquisa.

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

__O que são "positivos" e "negativos"?__ Quando verificando a identidade apresentada por uma solicitação, um resultado bem-sucedido pode ser descrito como "positivo" ou "negativo". Quando a identidade apresentada for confirmada como sendo a verdadeira identidade, ela será descrita como "positiva". Quando a identidade apresentada for confirmada como falsificada, ela será descrita como "negativa". No entanto, um resultado malsucedido (por exemplo, falha na verificação, ou a veracidade da identidade apresentada não pode ser determinada) não seria descrito como "positivo" ou "negativo". Em vez disso, um resultado malsucedido seria descrito simplesmente como não verificado. Quando não for feita nenhuma tentativa de verificar a identidade apresentada por uma solicitação, a solicitação também será descrita como não verificado. Os termos fazem sentido apenas no contexto em que a identidade apresentada por uma solicitação é reconhecida e, portanto, onde a verificação é possível. Nos casos em que a identidade apresentada não corresponde às opções fornecidas acima, ou onde nenhuma identidade é apresentada, as opções fornecidas acima tornam-se irrelevantes.

__O que são "bypasses de acerto único"?__ Em alguns casos, uma solicitação com verificação positiva ainda pode ser bloqueada como resultado dos arquivos de assinatura, módulos, ou outras condições da solicitação, e bypasses podem ser necessários para evitar falsos positivos. No caso em que um bypass se destina a lidar com exatamente uma infração, nem mais nem menos, tal bypass pode ser descrito como um "bypass de acerto único".

* Esta opção tem um bypass correspondente em `bypasses➡used`. É recomendável que a caixa de seleção para o bypass correspondente esteja marcado da mesma forma que a caixa de seleção para tentar verificar esta opção.

##### "social_media" `[string]`
- Controles para verificar solicitações de plataformas de mídia social.

```
social_media
├─Embedly ("* Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("* Pinterest")
├─Snapchat ("* Snapchat")
└─Twitterbot ("*!! Twitterbot")
```

__O que são "positivos" e "negativos"?__ Quando verificando a identidade apresentada por uma solicitação, um resultado bem-sucedido pode ser descrito como "positivo" ou "negativo". Quando a identidade apresentada for confirmada como sendo a verdadeira identidade, ela será descrita como "positiva". Quando a identidade apresentada for confirmada como falsificada, ela será descrita como "negativa". No entanto, um resultado malsucedido (por exemplo, falha na verificação, ou a veracidade da identidade apresentada não pode ser determinada) não seria descrito como "positivo" ou "negativo". Em vez disso, um resultado malsucedido seria descrito simplesmente como não verificado. Quando não for feita nenhuma tentativa de verificar a identidade apresentada por uma solicitação, a solicitação também será descrita como não verificado. Os termos fazem sentido apenas no contexto em que a identidade apresentada por uma solicitação é reconhecida e, portanto, onde a verificação é possível. Nos casos em que a identidade apresentada não corresponde às opções fornecidas acima, ou onde nenhuma identidade é apresentada, as opções fornecidas acima tornam-se irrelevantes.

__O que são "bypasses de acerto único"?__ Em alguns casos, uma solicitação com verificação positiva ainda pode ser bloqueada como resultado dos arquivos de assinatura, módulos, ou outras condições da solicitação, e bypasses podem ser necessários para evitar falsos positivos. No caso em que um bypass se destina a lidar com exatamente uma infração, nem mais nem menos, tal bypass pode ser descrito como um "bypass de acerto único".

* Esta opção tem um bypass correspondente em `bypasses➡used`. É recomendável que a caixa de seleção para o bypass correspondente esteja marcado da mesma forma que a caixa de seleção para tentar verificar esta opção.

** Requer funcionalidade de pesquisa ASN (por exemplo, através do módulo IP-API ou BGPView).

*!! Alta probabilidade de causar falsos positivos devido a iMessage.

##### "other" `[string]`
- Controles para verificar outros tipos de solicitações sempre que possível.

```
other
├─AdSense ("AdSense")
├─AmazonAdBot ("* AmazonAdBot")
├─ChatGPT-User ("!! ChatGPT-User")
├─GPTBot ("!! GPTBot")
└─Grapeshot ("* Oracle Data Cloud Crawler (Grapeshot)")
```

__O que são "positivos" e "negativos"?__ Quando verificando a identidade apresentada por uma solicitação, um resultado bem-sucedido pode ser descrito como "positivo" ou "negativo". Quando a identidade apresentada for confirmada como sendo a verdadeira identidade, ela será descrita como "positiva". Quando a identidade apresentada for confirmada como falsificada, ela será descrita como "negativa". No entanto, um resultado malsucedido (por exemplo, falha na verificação, ou a veracidade da identidade apresentada não pode ser determinada) não seria descrito como "positivo" ou "negativo". Em vez disso, um resultado malsucedido seria descrito simplesmente como não verificado. Quando não for feita nenhuma tentativa de verificar a identidade apresentada por uma solicitação, a solicitação também será descrita como não verificado. Os termos fazem sentido apenas no contexto em que a identidade apresentada por uma solicitação é reconhecida e, portanto, onde a verificação é possível. Nos casos em que a identidade apresentada não corresponde às opções fornecidas acima, ou onde nenhuma identidade é apresentada, as opções fornecidas acima tornam-se irrelevantes.

__O que são "bypasses de acerto único"?__ Em alguns casos, uma solicitação com verificação positiva ainda pode ser bloqueada como resultado dos arquivos de assinatura, módulos, ou outras condições da solicitação, e bypasses podem ser necessários para evitar falsos positivos. No caso em que um bypass se destina a lidar com exatamente uma infração, nem mais nem menos, tal bypass pode ser descrito como um "bypass de acerto único".

* Esta opção tem um bypass correspondente em `bypasses➡used`. É recomendável que a caixa de seleção para o bypass correspondente esteja marcado da mesma forma que a caixa de seleção para tentar verificar esta opção.

!! A maioria dos usuários provavelmente deseja que isso seja bloqueado, independentemente de ser real ou falsificado. Ao não selecionar "tente verificar" e selecionar "bloquear solicitações não verificados", isso pode ser alcançado. Mas, devido alguns usuários podem querer verificar tais solicitações (a fim de bloquear os negativos enquanto permitem os positivos), em vez de bloquear tais solicitações por meio de módulos, as opções para lidar com essas solicitações são fornecidas aqui.

##### "adjust" `[string]`
- Controles para ajustar outros recursos no contexto de verificação.

```
adjust
├─Negatives ("Os negativos bloqueados")
└─NonVerified ("Os não verificados bloqueados")
```

#### "recaptcha" (Categoria)
Configuração para ReCaptcha (fornece uma maneira para os humanos recuperarem o acesso quando bloqueados).

##### "usemode" `[int]`
- Quando o CAPTCHA deve ser oferecido? Nota: Solicitações na lista branca ou verificadas e não bloqueadas nunca precisam completar um CAPTCHA. Também: Os CAPTCHAs podem fornecer uma camada de proteção útil contra bots e vários tipos de solicitações automatizadas e maliciosas, mas não fornecerão nenhuma proteção contra humanos maliciosas.

```
usemode
├─0 (Nunca !!!)
├─1 (Somente quando bloqueado, dentro do limite de assinaturas, e não banido.)
├─2 (Somente quando bloqueado, especialmente marcado para uso, dentro do limite de assinaturas, e não banido.)
├─3 (Somente quando dentro do limite de assinaturas, e não banido (independentemente de estar bloqueado).)
├─4 (Somente quando não está bloqueado.)
├─5 (Somente quando não está bloqueado, ou quando especialmente marcado para uso, dentro do limite de assinaturas, e não banido.)
└─6 (Somente quando não está bloqueado, em solicitações de páginas confidenciais.)
```

##### "lockip" `[bool]`
- Ligar CAPTCHA para IPs?

##### "lockuser" `[bool]`
- Ligar CAPTCHA para os usuários?

##### "sitekey" `[string]`
- Este valor pode ser encontrado no painel do seu serviço CAPTCHA.

Veja também:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "secret" `[string]`
- Este valor pode ser encontrado no painel do seu serviço CAPTCHA.

Veja também:
- [Invisible reCAPTCHA](https://developers.google.com/recaptcha/docs/invisible)
- [reCAPTCHA v2](https://developers.google.com/recaptcha/docs/display)
- [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3)

##### "expiry" `[float]`
- Número de horas para lembrar instâncias CAPTCHA. Padrão = 720 (1 mês).

##### "recaptcha_log" `[string]`
- Registrar todas as tentativas de CAPTCHA? Se sim, especificar o nome a ser usado para o arquivo de log. Se não, deixe esta variável em branco.

Dica útil: Você pode anexar informações de data/hora aos nomes dos arquivos de log usando espaços reservados de formato de hora. Os espaços reservados para formato de hora disponíveis são exibidos em <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signature_limit" `[int]`
- O número máximo de assinaturas permitidas antes que o CAPTCHA seja retirado. Padrão = 1.

##### "api" `[string]`
- Qual API usar?

```
api
├─V2 ("V2 (Caixa de seleção)")
└─Invisible ("V2 (Invisível)")
```

##### "show_cookie_warning" `[bool]`
- Mostrar aviso de cookie? True = Sim [Padrão]; False = Não.

##### "show_api_message" `[bool]`
- Mostrar mensagem API? True = Sim [Padrão]; False = Não.

##### "nonblocked_status_code" `[int]`
- Qual código de status deve ser usado ao exibir CAPTCHAs para solicitações não bloqueadas?

```
nonblocked_status_code
├─200 (200 OK): Menos robusto, mas mais amigável de usar. As solicitações automatizadas
│ provavelmente interpretarão essa resposta como indicação de que a
│ solicitação foi bem-sucedida.
├─403 (403 Forbidden (Proibido)): Um pouco mais robusto, mas um pouco menos amigável de usar. Recomendado
│ para a maioria das circunstâncias gerais.
├─418 (418 I'm a teapot (Eu sou um bule)): Referências uma piada de primeiro de abril (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Muito improvável de ser
│ entendido por qualquer cliente, bot, navegador, ou outro. Fornecido para
│ diversão e conveniência, mas geralmente não recomendado.
├─429 (429 Too Many Requests (Pedidos em excesso)): Recomendado para limitação de taxa, ao lidar com ataques DDoS, e para
│ prevenção de inundações. Não recomendado em outros contextos.
└─451 (451 Unavailable For Legal Reasons (Indisponível por motivos legais)): Recomendado ao bloquear principalmente por motivos legais. Não recomendado
  em outros contextos.
```

#### "hcaptcha" (Categoria)
Configuração para HCaptcha (fornece uma maneira para os humanos recuperarem o acesso quando bloqueados).

##### "usemode" `[int]`
- Quando o CAPTCHA deve ser oferecido? Nota: Solicitações na lista branca ou verificadas e não bloqueadas nunca precisam completar um CAPTCHA. Também: Os CAPTCHAs podem fornecer uma camada de proteção útil contra bots e vários tipos de solicitações automatizadas e maliciosas, mas não fornecerão nenhuma proteção contra humanos maliciosas.

```
usemode
├─0 (Nunca !!!)
├─1 (Somente quando bloqueado, dentro do limite de assinaturas, e não banido.)
├─2 (Somente quando bloqueado, especialmente marcado para uso, dentro do limite de assinaturas, e não banido.)
├─3 (Somente quando dentro do limite de assinaturas, e não banido (independentemente de estar bloqueado).)
├─4 (Somente quando não está bloqueado.)
├─5 (Somente quando não está bloqueado, ou quando especialmente marcado para uso, dentro do limite de assinaturas, e não banido.)
└─6 (Somente quando não está bloqueado, em solicitações de páginas confidenciais.)
```

##### "lockip" `[bool]`
- Ligar CAPTCHA para IPs?

##### "lockuser" `[bool]`
- Ligar CAPTCHA para os usuários?

##### "sitekey" `[string]`
- Este valor pode ser encontrado no painel do seu serviço CAPTCHA.

Veja também:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "secret" `[string]`
- Este valor pode ser encontrado no painel do seu serviço CAPTCHA.

Veja também:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "expiry" `[float]`
- Número de horas para lembrar instâncias CAPTCHA. Padrão = 720 (1 mês).

##### "hcaptcha_log" `[string]`
- Registrar todas as tentativas de CAPTCHA? Se sim, especificar o nome a ser usado para o arquivo de log. Se não, deixe esta variável em branco.

Dica útil: Você pode anexar informações de data/hora aos nomes dos arquivos de log usando espaços reservados de formato de hora. Os espaços reservados para formato de hora disponíveis são exibidos em <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signature_limit" `[int]`
- O número máximo de assinaturas permitidas antes que o CAPTCHA seja retirado. Padrão = 1.

##### "api" `[string]`
- Qual API usar?

```
api
├─V1 ("V1")
└─Invisible ("V1 (Invisível)")
```

##### "show_cookie_warning" `[bool]`
- Mostrar aviso de cookie? True = Sim [Padrão]; False = Não.

##### "show_api_message" `[bool]`
- Mostrar mensagem API? True = Sim [Padrão]; False = Não.

##### "nonblocked_status_code" `[int]`
- Qual código de status deve ser usado ao exibir CAPTCHAs para solicitações não bloqueadas?

```
nonblocked_status_code
├─200 (200 OK): Menos robusto, mas mais amigável de usar. As solicitações automatizadas
│ provavelmente interpretarão essa resposta como indicação de que a
│ solicitação foi bem-sucedida.
├─403 (403 Forbidden (Proibido)): Um pouco mais robusto, mas um pouco menos amigável de usar. Recomendado
│ para a maioria das circunstâncias gerais.
├─418 (418 I'm a teapot (Eu sou um bule)): Referências uma piada de primeiro de abril (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Muito improvável de ser
│ entendido por qualquer cliente, bot, navegador, ou outro. Fornecido para
│ diversão e conveniência, mas geralmente não recomendado.
├─429 (429 Too Many Requests (Pedidos em excesso)): Recomendado para limitação de taxa, ao lidar com ataques DDoS, e para
│ prevenção de inundações. Não recomendado em outros contextos.
└─451 (451 Unavailable For Legal Reasons (Indisponível por motivos legais)): Recomendado ao bloquear principalmente por motivos legais. Não recomendado
  em outros contextos.
```

#### "legal" (Categoria)
Configuração para requisitos legais.

##### "pseudonymise_ip_addresses" `[bool]`
- Pseudonimiza endereços IP ao escrever os arquivos de log? True = Sim [Padrão]; False = Não.

##### "privacy_policy" `[string]`
- O endereço de uma política de privacidade relevante a ser exibida no rodapé de qualquer página gerada. Especifique um URL, ou deixe em branco para desabilitar.

#### "template_data" (Categoria)
Configuração para modelos e temas.

##### "theme" `[string]`
- Tema padrão a ser usado para CIDRAM.

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
└─…Outros
```

##### "magnification" `[float]`
- Ampliação de fonte. Padrão = 1.

##### "css_url" `[string]`
- URL de arquivo CSS para temas personalizados.

##### "block_event_title" `[string]`
- O título da página a ser exibido para eventos de bloqueio.

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("Acesso negado!")
└─…Outros
```

##### "captcha_title" `[string]`
- O título da página a ser exibido para solicitações CAPTCHA.

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…Outros
```

##### "custom_header" `[string]`
- Inserido como HTML no início de todas as páginas de "acesso negado". Isso pode ser útil caso você queira incluir um logotipo de site, cabeçalho personalizado, scripts, ou similares em todas essas páginas.

##### "custom_footer" `[string]`
- Inserido como HTML no final de todas as páginas de "acesso negado". Isso pode ser útil caso você queira incluir um aviso legal, link de contato, informações comerciais, ou similares em todas essas páginas.

#### "rate_limiting" (Categoria)
Configuração para limitação de taxa (não recomendado para uso geral).

##### "max_bandwidth" `[string]`
- A quantidade máxima de largura de banda permitida dentro do período de tolerância antes de ativar a limitação de taxa para solicitações futuras. Um valor de 0 desativa esse tipo de limitação de taxa. Padrão = 0KB.

##### "max_requests" `[int]`
- O número máximo de solicitações permitido dentro do período de tolerância antes de ativar a limitação de taxa para solicitações futuras. Um valor de 0 desativa esse tipo de limitação de taxa. Padrão = 0.

##### "precision_ipv4" `[int]`
- A precisão a ser usada ao monitorar o uso do IPv4. Valor espelha o tamanho do bloco CIDR. Defina para 32 para melhor precisão. Padrão = 32.

##### "precision_ipv6" `[int]`
- A precisão a ser usada ao monitorar o uso do IPv6. Valor espelha o tamanho do bloco CIDR. Defina para 128 para melhor precisão. Padrão = 128.

##### "allowance_period" `[string]`
- A duração para monitorar o uso. Padrão = 0°0′0″.

##### "exceptions" `[string]`
- Exceções (ou seja, solicitações que não devem ser limitadas à taxa). Relevante apenas quando a limitação de taxa está ativada.

```
exceptions
├─Whitelisted ("Solicitações marcadas como na lista branca")
├─Verified ("Solicitações verificadas de mecanismos de pesquisa e mídias sociais")
└─FE ("Solicitações ao front-end do CIDRAM")
```

##### "segregate" `[bool]`
- As cotas para diferentes domínios e hosts devem ser segregadas ou compartilhadas? True = As cotas serão segregadas. False = As cotas serão compartilhadas [Padrão].

#### "supplementary_cache_options" (Categoria)
Opções de cache suplementares. Nota: Alterar estes valores podem potencialmente fazer você ser estar desconectado.

##### "prefix" `[string]`
- O valor especificado aqui será adicionado ao começo das chaves para todas as entradas de cache. Padrão = "CIDRAM_". Quando existem várias instalações no mesmo servidor, isso pode ser útil para manter seus caches separados uns dos outros.

##### "enable_apcu" `[bool]`
- Especifica se deve tentar usar o APCu para armazenamento em cache. Padrão = True.

##### "enable_memcached" `[bool]`
- Especifica se deve tentar usar o Memcached para armazenamento em cache. Padrão = False.

##### "enable_redis" `[bool]`
- Especifica se deve tentar usar o Redis para armazenamento em cache. Padrão = False.

##### "enable_pdo" `[bool]`
- Especifica se deve tentar usar o PDO para armazenamento em cache. Padrão = False.

##### "memcached_host" `[string]`
- Valor da host do Memcached. Padrão = "localhost".

##### "memcached_port" `[int]`
- Valor da porta do Memcached. Padrão = "11211".

##### "redis_host" `[string]`
- Valor da host do Redis. Padrão = "localhost".

##### "redis_port" `[int]`
- Valor da porta do Redis. Padrão = "6379".

##### "redis_timeout" `[float]`
- Valor de tempo limite do Redis. Padrão = "2.5".

##### "redis_database_number" `[int]`
- Número do banco de dados Redis. Padrão = 0. Observação: Não é possível usar valores diferentes de 0 com Redis Cluster.

##### "pdo_dsn" `[string]`
- Valor DSN do PDO. Padrão = "mysql:dbname=cidram;host=localhost;port=3306".

__FAQ.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.pt.md#user-content-HOW_TO_USE_PDO" hreflang="pt">O que é um "PDO DSN"? Como posso usar o PDO com o CIDRAM?</a>*

##### "pdo_username" `[string]`
- O nome de usuário do PDO.

##### "pdo_password" `[string]`
- A senha do PDO.

#### "bypasses" (Categoria)
Configuração para o bypass das assinaturas padrão.

##### "used" `[string]`
- Quais bypass devem ser usados?

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


### 6. <a name="SECTION6"></a>FORMATO DE ASSINATURAS

*Veja também:*
- *[O que é uma "assinatura"?](#user-content-WHAT_IS_A_SIGNATURE)*

#### 6.0 NOÇÕES BÁSICAS (PARA ARQUIVOS DE ASSINATURA)

Todas as assinaturas IPv4 seguir o formato: `xxx.xxx.xxx.xxx/yy [Function] [Param]`.
- `xxx.xxx.xxx.xxx` representa o início do bloco CIDR (os octetos do endereço IP inicial no bloco).
- `yy` representa o tamanho do bloco CIDR [1-32].
- `[Function]` instrui o script o que fazer com a assinatura (como a assinatura deve ser considerada).
- `[Param]` representa qualquer informação adicional que possa ser necessária por `[Function]`.

Todas as assinaturas IPv6 seguir o formato: `xxxx:xxxx:xxxx:xxxx::xxxx/yy [Function] [Param]`.
- `xxxx:xxxx:xxxx:xxxx::xxxx` representa o início do bloco CIDR (os octetos do endereço IP inicial no bloco). Notação completa e notação abreviada são aceitáveis (e cada DEVE seguir os padrões da notação IPv6 apropriados e relevantes, mas com uma exceção: um endereço IPv6 nunca pode começar com uma abreviatura quando utilizado numa assinatura para este script, por causa da maneira em que CIDRs são reconstruídos pelo script; Por exemplo, `::1/128` deve ser expresso, quando utilizado numa assinatura, como `0::1/128`, e `::0/128` expresso como `0::/128`).
- `yy` representa o tamanho do bloco CIDR [1-128].
- `[Function]` instrui o script o que fazer com a assinatura (como a assinatura deve ser considerada).
- `[Param]` representa qualquer informação adicional que possa ser necessária por `[Function]`.

Os arquivos de assinaturas para CIDRAM DEVE usar quebras de linha no estilo de Unix (`%0A`, ou `\n`)! Outros tipos/estilos de quebras de linha (por exemplo, Windows `%0D%0A` ou `\r\n` quebras de linha, Mac `%0D` ou `\r` quebras de linha, etc) PODE ser usado, mas NÃO são preferidos. Quebras de linha não no estilo de Unix será normalizado para quebras de linha no estilo de Unix pelo script.

Notação CIDR precisa e correta é necessária, ou então o script NÃO irá reconhecer as assinaturas. Além disso, todas as assinaturas CIDR deste script DEVE começar com um endereço IP cujo número IP pode dividir igualmente na divisão bloco representado pelo tamanho do seu bloco CIDR (por exemplo, se você quiser bloquear todos os IPs de `10.128.0.0` para `11.127.255.255`, `10.128.0.0/8` NÃO seria reconhecido pelo script, mas `10.128.0.0/9` e `11.0.0.0/9` usado em conjunto, SERIA reconhecido pelo script).

Qualquer coisa na arquivos de assinaturas não reconhecida como uma assinatura nem como sintaxe relacionados com assinaturas pelo script será IGNORADO, que significa que você pode colocar com segurança quaisquer dados que você quer nos arquivos de assinaturas sem quebrá-los e sem quebrar o script. Comentários são aceitáveis nos arquivos de assinaturas, e nenhuma formatação especial é necessário para eles. Hashing no estilo de Shell para comentários é preferido, mas não são forçadas; Funcionalmente, não faz diferença para o script se ou não você escolher para usar hashing no estilo de Shell para comentários, mas utilizando hashing no estilo de Shell ajuda IDEs e editores de texto simples para destacar corretamente as várias partes dos arquivos de assinaturas (e então, hashing no estilo de Shell pode ajudar como uma ajuda visual durante a edição).

Os valores possíveis de `[Function]` são as seguintes:
- Run
- Whitelist
- Greylist
- Deny

Se "Run" é utilizado, quando a assinatura é desencadeada, o script tentará executar (usando um statement `require_once`) um script PHP externa, especificado pelo valor de `[Param]` (o diretório de trabalho deve ser o diretório do script, "/vault/").

Exemplo: `127.0.0.0/8 Run example.php`

Isto pode ser útil se você quiser executar algum código PHP específica para alguns IPs específicos e/ou CIDRs.

Se "Whitelist" é utilizado, quando a assinatura é desencadeada, o script irá repor todas as detecções (se houve quaisquer detecções) e quebrar a função de teste. `[Param]` é ignorado. Esta função irá assegurar que um IP ou CIDR não será detectado.

Exemplo: `127.0.0.1/32 Whitelist`

Se "Greylist" é utilizado, quando a assinatura é desencadeada, o script irá repor todas as detecções (se houve quaisquer detecções) e pular para o próximo arquivo de assinaturas para continuar o processamento. `[Param]` é ignorado.

Exemplo: `127.0.0.1/32 Greylist`

Se "Deny" é utilizado, quando a assinatura é desencadeada, assumindo que não assinatura whitelist foi desencadeado para o dado endereço IP e/ou dado CIDR, acesso à página protegida será negado. "Deny" é o que você deseja usar para realmente bloquear um endereço IP e/ou gama CIDR. Quando qualquer as assinaturas usando "Deny" são desencadeados, o "Acesso Negado" página do script será gerado ea solicitação para a página protegida será morto.

O valor da `[Param]` aceita por "Deny" será processado com o saída da "Acesso Negado" página, fornecido ao cliente/utilizador como a razão citada para o seu acesso à página solicitada ser negada. Pode ser uma curta e simples frase, explicando o motivo de ter escolhido para bloqueá-los (qualquer coisa deve ser suficiente, até mesmo uma "eu não quero você no meu site"), ou um de um pequeno punhado de palavras curtas fornecidas pelo script que, se usadas, será substituído pelo script com uma explicação pré-preparado de porque o cliente/usuário foi bloqueado.

As explicações pré-preparados têm suporte L10N e pode ser traduzido pelo script com base no idioma que você especificar com a directiva da configuração do script, `lang`. Além disso, você pode instruir o script para ignorar assinaturas "Deny" com base em sua valor de `[Param]` (se eles estão usando essas palavras curtas) através das directivas especificados pelo configuração do script (cada palavra curta tem uma directiva correspondente para processar as assinaturas correspondentes ou ignorá-los). Valores de `[Param]` que não usar essas palavras curtas, contudo, não tem suporte L10N e por conseguinte NÃO será traduzido pelo script, e adicionalmente, não podem ser controlados directamente pelo configuração do script.

As palavras curtas disponíveis são:
- Attacks
- Bogon
- Cloud
- Generic
- Legal
- Malware
- Proxy
- Spam

#### 6.1 ETIQUETAS

##### 6.1.0 ETIQUETAS DE SEÇÃO

Se você quiser dividir suas assinaturas personalizadas em seções individuais, você pode identificar estas seções individuais para o script por adição de uma "etiqueta de seção" imediatamente após as assinaturas de cada seção, juntamente com o nome de sua seção de assinaturas (veja o exemplo abaixo).

```
# Seção 1.
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: Seção 1
```

Para quebrar etiquetas de seção e assegurar que os etiquetas não são identificados incorretamente a seções de assinaturas de mais cedo nos arquivos de assinaturas, simplesmente assegurar que há pelo menos dois quebras de linha consecutivas entre o sua etiqueta e suas seções de assinaturas anteriores. Quaisquer assinaturas não etiquetados será padrão para qualquer "IPv4" ou "IPv6" (dependendo de quais tipos de assinaturas estão sendo desencadeados).

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: Seção 1
```

No exemplo acima, `1.2.3.4/32` e `2.3.4.5/32` será etiquetadas como "IPv4", enquanto que `4.5.6.7/32` e `5.6.7.8/32` será etiquetadas como "Seção 1".

A mesma lógica pode ser aplicada para separar outros tipos de etiquetas, também.

Em particular, as etiquetas de seção podem ser muito úteis para depuração quando ocorrem falsos positivos, fornecendo um meio fácil de encontrar a fonte exata do problema, e pode ser muito útil para filtrar entradas de arquivos de log ao visualizar arquivos de log por meio da página de logs do front-end (os nomes das seções são clicáveis através da página de logs do front-end e podem ser usados como critérios de filtragem). Se as etiquetas de seção forem omitidas para algumas assinaturas específicas, quando essas assinaturas são desencadeadas, o CIDRAM usa o nome do arquivo de assinatura juntamente com o tipo de endereço IP bloqueado (IPv4 ou IPv6) como um retorno, e portanto, as etiquetas de seção são inteiramente opcionais. Embora, eles podem ser recomendados em alguns casos, como quando os arquivos de assinatura são nomeados vagamente ou quando pode ser difícil identificar claramente a origem das assinaturas fazendo com que uma solicitação seja bloqueada.

##### 6.1.1 ETIQUETAS DE EXPIRAÇÃO

Se você quiser assinaturas para expirar depois de algum tempo, de um modo semelhante para etiquetas de seção, você pode usar um "etiqueta de expiração" para especificar quando as assinaturas devem deixar de ser válida. Etiquetas de expiração usam o formato "AAAA.MM.DD" (veja o exemplo abaixo).

```
# Seção 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

As assinaturas expiradas nunca serão desencadeadas em qualquer solicitação, não importa o que.

##### 6.1.2 ETIQUETAS DE ORIGEM

Se você deseja especificar o país de origem para alguma assinatura específica, você pode fazer isso usando uma "etiqueta de origem". Uma etiqueta de origem aceita um código "[ISO 3166-1 alfa-2](https://pt.wikipedia.org/wiki/ISO_3166-1_alfa-2)" correspondente ao país de origem para as assinaturas às quais se aplica. Esses códigos devem ser escritos em maiúsculas (minúsculas não serão processadas corretamente). Quando uma etiqueta de origem é usada, ela é adicionada à campo "Razão Bloqueada" do entrada de log para quaisquer solicitações bloqueadas como resultado das assinaturas às quais a etiqueta é aplicada.

Se o componente opcional "flags CSS" estiver instalado, ao visualizar arquivos de log na página de logs do front-end, as informações anexadas pelas etiquetas de origem são substituídas pela bandeira do país correspondente a essa informação. Esta informação, seja em sua forma bruta ou como uma bandeira de país, é clicável, e quando clicada, irá filtrar entradas de log por meio de outras entradas de log de identificação semelhante (efetivamente permitindo que aqueles que acessem a página de logs sejam filtrados por país de origem).

Nota: Tecnicamente, esta não é uma forma de geolocalização, pela razão de que isso não envolve a pesquisa de informações específicas relativas a IPs de entrada, mas sim, simplesmente nos permite declarar explicitamente um país de origem para quaisquer solicitações bloqueados por assinaturas específicas. As etiquetas de origem múltipla são permitidas dentro da mesma seção de assinatura.

Exemplo hipotético:

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

Todas as etiquetas podem ser usadas em conjunto e todas as etiquetas são opcionais (veja o exemplo abaixo).

```
# Seção Exemplo.
1.2.3.4/32 Deny Generic
Origin: US
Tag: Seção Exemplo
Expires: 2016.12.31
```

##### 6.1.3 ETIQUETAS DE DEFERÊNCIA

Quando um grande número de arquivos de assinatura é instalado e usado ativamente, as instalações podem se tornar bastante complexas, e pode haver algumas assinaturas que se sobrepõem. Nestes casos, a fim de evitar que várias assinaturas sobrepostas sejam desencadeados durante eventos de bloco, etiquetas de deferência podem ser usadas para diferir seções de assinatura específicas nos casos em que algum outro arquivo de assinatura específico é instalado e usado ativamente. Isso pode ser útil nos casos em que algumas assinaturas são atualizadas com mais freqüência do que outras, a fim de diferir as assinaturas atualizadas com menos frequência em favor das assinaturas atualizadas com maior frequência.

As etiquetas de deferência são usadas de forma semelhante a outros tipos de etiquetas. O valor da etiqueta deve corresponder a um arquivo de assinatura instalado e usado ativamente para ser diferido.

Exemplo:

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 6.1.4 ETIQUETAS DE PERFIL

As etiquetas de perfil fornecem um meio de exibir informações adicionais na página de teste de IP, e podem ser aproveitadas por módulos e regras auxiliares para um comportamento mais complexo e tomada de decisão ajustada.

As etiquetas de perfil são usadas de maneira semelhante a outros tipos de etiquetas. Os valores das etiquetas de perfil podem ser usados como condição para módulos e regras auxiliares. As etiquetas de perfil podem fornecer vários valores, separando esses valores com um ponto e vírgula. O usuário final nunca vê os valores das etiquetas de perfil.

Exemplo:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 6.2 YAML

##### 6.2.0 YAML BÁSICOS

Uma forma simplificada de marcação YAML pode ser usado em arquivos de assinatura com a finalidade de definir comportamentos e configurações específicas para as seções de assinaturas individuais. Isto pode ser útil se você quiser que o valor de suas diretivas de configuração para diferir na base de assinaturas individuais e seções de assinatura (por exemplo; se você quiser fornecer um endereço de e-mail para tickets de suporte para quaisquer usuários bloqueados por uma assinatura específica, mas não quer fornecer um endereço de e-mail para tickets de suporte para usuários bloqueados por quaisquer outras assinaturas; se você quiser algumas assinaturas específicas para provocar um redirecionamento página; se você quiser marcar uma seção de assinaturas para uso com reCAPTCHA/hCAPTCHA; Se você quiser registrar tentativas de acesso bloqueadas para separar arquivos na base de assinaturas individuais e/ou seções de assinatura).

Uso de marcação YAML nos arquivos de assinatura é totalmente opcional (isto é, você pode usá-lo se desejar fazê-lo, mas você não é obrigado a fazê-lo), e é capaz de alavancar mais (mas nem todos) das diretivas de configuração.

Nota: Implementação de marcação YAML em CIDRAM é muito simplista e muito limitado; Destina-se a cumprir as exigências específicas para CIDRAM de uma maneira que tem a familiaridade de marcação YAML, mas nem segue nem está de acordo com as especificações oficiais (e portanto, não se comporta da mesma forma como outros implementações mais completas, e pode não ser apropriado para outros projetos).

Em CIDRAM, segmentos de marcação YAML são identificados para o script por três hífens ("---"), e terminar ao lado de seus contendo seções de assinatura por quebras de linha dupla. Um segmento típico de marcação YAML dentro de uma seção de assinaturas consiste de três hífens numa linha imediatamente após a lista de CIDRs e todas as etiquetas, seguido por uma lista bidimensional de pares chave-valor (primeira dimensão, categorias das diretivas de configuração; segunda dimensão, as diretivas de configuração) para as quais diretivas de configuração deve ser modificada (e em qual valores) sempre que uma assinatura em nisso seção de assinaturas é desencadeada (veja os exemplos abaixo).

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

##### 6.2.1 COMO "MARCAR ESPECIALMENTE" SEÇÕES DE ASSINATURA PARA USO COM reCAPTCHA/hCAPTCHA

Quando "usemode" é 2 ou 5, para "marcar especialmente" seções de assinatura para uso com reCAPTCHA/hCAPTCHA, uma entrada está incluído no segmento de YAML para que a seção de assinatura (veja o exemplo abaixo).

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

#### 6.3 AUXILIAR

##### 6.3.0 IGNORANDO SEÇÕES DE ASSINATURA

Em suplemento, se você quiser CIDRAM para ignorar completamente algumas seções específicas dentro de qualquer um dos arquivos de assinatura, você pode usar o arquivo `ignore.dat` para especificar quais seções para ignorar. numa nova linha, escreva `Ignore`, seguido por um espaço, seguido do nome da seção que você quer CIDRAM para ignorar (veja o exemplo abaixo).

```
Ignore Seção 1
```

Isso também pode ser alcançado usando a interface fornecida pela página "lista de seções" do front-end do CIDRAM.

##### 6.3.1 REGRAS AUXILIARES

Se você acha que escrever seus próprios arquivos de assinatura personalizados ou módulos personalizados é muito complicado para você, uma alternativa mais simples pode ser usar a interface fornecida pela página "regras auxiliares" do front-end do CIDRAM. Ao selecionar as opções apropriadas e especificar detalhes sobre os tipos de solicitações específicos, você pode instruir o CIDRAM sobre como responder a essas solicitações. "Regras auxiliares" são executadas depois que todos os arquivos de assinatura e módulos já tiverem terminado a execução.

#### 6.4 <a name="MODULE_BASICS"></a>NOÇÕES BÁSICAS (PARA MÓDULOS)

Os módulos podem ser usados para ampliar a funcionalidade do CIDRAM, executar tarefas adicionais, ou processar lógica adicional.

Devido a que os módulos são escritos como arquivos PHP, se você estiver adequadamente familiarizado com a base de códigos CIDRAM, você pode estruturar seus módulos e escreva as assinaturas do módulo, como quiser (em razão do que é possível com o PHP).

*Nota: Se você não está confortável trabalhando com o código PHP, não é recomendável escrever seus próprios módulos.*

Algumas funcionalidades são fornecidas pelo CIDRAM para os módulos a serem usados, o que deve tornar mais simples e fácil de escrever seus próprios módulos. A informação sobre esta funcionalidade é descrita abaixo.

#### 6.5 FUNCIONALIDADE DO MÓDULO

##### 6.5.0 "$this->trigger"

As assinaturas do módulo geralmente são escritas com `$this->trigger`. Na maioria dos casos, esse method será mais importante do que qualquer outra coisa com a finalidade de escrever módulos.

`$this->trigger` aceita 4 parâmetros: `$Condition`, `$ReasonShort`, `$ReasonLong` (opcional), e `$DefineOptions` (opcional).

A verdade de `$Condition` é avaliada, e se for true/verdade, a assinatura é "desencadeada". Se false/falso, a assinatura *não* é "desencadeada". `$Condition` tipicamente contém código PHP para avaliar uma condição que deve causar uma solicitação seja bloqueada.

`$ReasonShort` é citado no campo "Razão Bloqueada" quando a assinatura é "desencadeada".

`$ReasonLong` é uma mensagem opcional a ser exibida para o usuário/cliente para quando eles estão bloqueados, para explicar por que eles foram bloqueados. Usa a mensagem padrão "Acesso Negado" quando omitido.

`$DefineOptions` é uma array opcional contendo pares de chave/valor, usada para definir opções de configuração específicas para a instância de solicitação. As opções de configuração serão aplicadas quando a assinatura é "desencadeada".

`$this->trigger` retorna true/verdadeiro quando a assinatura é "desencadeada", e false/falsa quando não é.

##### 6.5.1 "$this->bypass"

Os bypass de assinatura geralmente são escritos com `$this->bypass`.

`$this->bypass` aceita 3 parâmetros: `$Condition`, `$ReasonShort`, e `$DefineOptions` (opcional).

A verdade de `$Condition` é avaliada, e se for true/verdade, o bypass é "desencadeado". Se false/falso, o bypass *não* é "desencadeado". `$Condition` tipicamente contém código PHP para avaliar uma condição *não* que deve causar uma solicitação seja bloqueada.

`$ReasonShort` é citado no campo "Razão Bloqueada" quando o bypass é "desencadeado".

`$DefineOptions` é uma array opcional contendo pares de chave/valor, usada para definir opções de configuração específicas para a instância de solicitação. As opções de configuração serão aplicadas quando o bypass é "desencadeado".

`$this->bypass` retorna true/verdadeiro quando o bypass é "desencadeado", e false/falsa quando não é.

##### 6.5.2 "$this->dnsReverse"

Isso pode ser usado para buscar o nome do host de um endereço IP. Se você quiser criar um módulo para bloquear nomes de host, este method pode ser útil.

Exemplo:
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

Os módulos executam dentro do seu próprio escopo, e quaisquer variáveis definidas por um módulo, não serão acessíveis a outros módulos, nem ao script pai, a menos que estejam armazenados na array `$CIDRAM` (tudo o resto é liberado após a conclusão do módulo).

Abaixo estão algumas das variáveis comuns que podem ser úteis para o seu módulo:

Variável | Descrição
----|----
`$this->BlockInfo['DateTime']` | A data e a hora atuais.
`$this->BlockInfo['IPAddr']` | O endereço IP para a solicitação atual.
`$this->BlockInfo['ScriptIdent']` | Versão do CIDRAM.
`$this->BlockInfo['Query']` | A consulta para a solicitação atual.
`$this->BlockInfo['Referrer']` | O referente para a solicitação atual (se houver).
`$this->BlockInfo['UA']` | O agente do usuário (user agent) para a solicitação atual.
`$this->BlockInfo['UALC']` | O agente do usuário (user agent) para a solicitação atual (em minúsculas).
`$this->BlockInfo['ReasonMessage']` | A mensagem a ser exibida para o usuário/cliente da solicitação atual se eles estiverem bloqueados.
`$this->BlockInfo['SignatureCount']` | O número de assinaturas desencadeadas para a solicitação atual.
`$this->BlockInfo['Signatures']` | Informações de referência para qualquer assinatura desencadeada para a solicitação atual.
`$this->BlockInfo['WhyReason']` | Informações de referência para qualquer assinatura desencadeada para a solicitação atual.

---


### 7. <a name="SECTION7"></a>CONHECIDOS COMPATIBILIDADE PROBLEMAS

Os seguintes pacotes e produtos foram considerados incompatíveis com o CIDRAM:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

Os módulos foram disponibilizados para garantir que os seguintes pacotes e produtos sejam compatíveis com o CIDRAM:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__

*Veja também: [Gráficos de Compatibilidade](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 8. <a name="SECTION8"></a>PERGUNTAS MAIS FREQUENTES (FAQ)

- [O que é uma "assinatura"?](#user-content-WHAT_IS_A_SIGNATURE)
- [O que é um "CIDR"?](#user-content-WHAT_IS_A_CIDR)
- [O que é um "falso positivo"?](#user-content-WHAT_IS_A_FALSE_POSITIVE)
- [CIDRAM pode bloquear países inteiros?](#user-content-BLOCK_ENTIRE_COUNTRIES)
- [Com que frequência as assinaturas são atualizadas?](#user-content-SIGNATURE_UPDATE_FREQUENCY)
- [Eu encontrei um problema ao usar CIDRAM e eu não sei o que fazer sobre isso! Ajude-me!](#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [Eu fui bloqueado pelo CIDRAM de um site que eu quero visitar! Ajude-me!](#user-content-BLOCKED_WHAT_TO_DO)
- [Eu quero usar CIDRAM v3 com uma versão PHP mais velha do que 7.2; Você pode ajudar?](#user-content-MINIMUM_PHP_VERSION_V3)
- [Posso usar uma única instalação do CIDRAM para proteger vários domínios?](#user-content-PROTECT_MULTIPLE_DOMAINS)
- [Eu não quero mexer com a instalação deste e fazê-lo funcionar com o meu site; Posso pagar-te para fazer tudo por mim?](#user-content-PAY_YOU_TO_DO_IT)
- [Posso contratar você ou qualquer um dos desenvolvedores deste projeto para o trabalho privado?](#user-content-HIRE_FOR_PRIVATE_WORK)
- [Preciso de modificações especializadas, customizações, etc; Você pode ajudar?](#user-content-SPECIALIST_MODIFICATIONS)
- [Eu sou um desenvolvedor, designer de site, ou programador. Posso aceitar ou oferecer trabalho relacionado a este projeto?](#user-content-ACCEPT_OR_OFFER_WORK)
- [Quero contribuir para o projeto; Posso fazer isso?](#user-content-WANT_TO_CONTRIBUTE)
- [Posso usar o cron para atualizar automaticamente?](#user-content-CRON_TO_UPDATE_AUTOMATICALLY)
- [O que são "infrações"?](#user-content-WHAT_ARE_INFRACTIONS)
- [O CIDRAM pode bloquear nomes de host?](#user-content-BLOCK_HOSTNAMES)
- [O que posso usar para "default_dns"?](#o-que-posso-usar-para-default_dns)
- [Posso usar o CIDRAM para proteger outras coisas além de sites (por exemplo, servidores de e-mail, FTP, SSH, IRC, etc)?](#user-content-PROTECT_OTHER_THINGS)
- [Ocorrerão problemas se eu usar o CIDRAM ao mesmo tempo que usando CDNs ou serviços de cache?](#user-content-CDN_CACHING_PROBLEMS)
- [A CIDRAM protegerá meu site contra ataques DDoS?](#user-content-DDOS_ATTACKS)
- [Quando eu ativar ou desativar os módulos ou os arquivos de assinatura através da página de atualizações, eles os classificam alfanumericamente na configuração. Posso mudar a maneira como eles são classificados?](#user-content-CHANGE_COMPONENT_SORT_ORDER)
- [O que é um "PDO DSN"? Como posso usar o PDO com o CIDRAM?](#user-content-HOW_TO_USE_PDO)
- [CIDRAM está bloqueando cronjobs; Como consertar isto?](#user-content-BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>O que é uma "assinatura"?

No contexto do CIDRAM, uma "assinatura" refere-se a dados que actuam como um indicador/identificador para algo específico que estamos procurando, geralmente um endereço IP ou CIDR, e inclui algumas instruções para CIDRAM, dizendo-lhe a melhor maneira de responder quando encontrar o que estamos procurando. Uma assinatura típica para o CIDRAM é algo como isto:

Para "arquivos de assinatura":

`1.2.3.4/32 Deny Generic`

Para "módulos":

```PHP
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*Nota: Assinaturas para "arquivos de assinatura", e assinaturas para "módulos", não são a mesma coisa.*

Muitas vezes (mas nem sempre), as assinaturas serão agrupadas em grupos, formando "seções de assinaturas", freqüentemente acompanhado de comentários, marcação e/ou metadados relacionados que podem ser usados para fornecer contexto adicional para as assinaturas e/ou instrução adicional.

#### <a name="WHAT_IS_A_CIDR"></a>O que é um "CIDR"?

"CIDR" é um acrônimo para "Classless Inter-Domain Routing" *[[1](https://pt.wikipedia.org/wiki/CIDR), [2](https://whatismyipaddress.com/cidr)]*, e é este acrônimo que é usado como parte do nome para este pacote, "CIDRAM", que é um acrônimo para "Classless Inter-Domain Routing Access Manager".

No entanto, no contexto do CIDRAM (tal como, dentro desta documentação, dentro das discussões relativas ao CIDRAM, ou dentro dos dados lingüísticos para CIDRAM), sempre que um "CIDR" (singular) ou "CIDRs" (plural) seja mencionado ou referido (e assim por meio do qual usamos essas palavras como substantivos em seu próprio direito, ao contrário de como acrônimos), o que é pretendido e significado por isto é uma sub-rede (ou sub-redes), expresso usando a notação CIDR. A razão que CIDR (ou CIDRs) é usado em vez de sub-rede (ou sub-redes) é deixar claro que é especificamente sub-redes expressas usando a notação CIDR que está sendo referida (pois a notação CIDR é apenas uma das várias maneiras pelas quais as sub-redes podem ser expressas). O CIDRAM poderia, portanto, ser considerado um "gerenciador de acesso para sub-redes".

Embora este duplo significado de "CIDR" possa apresentar alguma ambigüidade em alguns casos, esta explicação, juntamente com o contexto, deve ajudar a resolver essa ambiguidade.

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>O que é um "falso positivo"?

O termo "falso positivo" (*alternativamente: "erro de falso positivo"; "alarme falso"*; Inglês: *false positive*; *false positive error*; *false alarm*), descrita de maneira muito simples, e num contexto generalizado, são usadas quando testando para uma condição, para se referir aos resultados desse teste, quando os resultados são positivos (isto é, a condição é determinada para ser "positivo", ou "verdadeiro"), mas espera-se que seja (ou deveria ter sido) negativo (isto é, a condição, na realidade, é "negativo", ou "falso"). Um "falso positivo" pode ser considerado análogo ao "chorando lobo" (em que a condição que está sendo testada é se existe um lobo perto do rebanho, a condição é "falso" em que não há nenhum lobo perto do rebanho, ea condição é relatada como "positivo" pelo pastor por meio de gritando "lobo, lobo"), ou análoga a situações em exames médicos em que um paciente é diagnosticado como tendo alguma doença quando, na realidade, eles não têm essa doença.

Os resultados relacionados a quando testando para uma condição pode ser descrito usando os termos "verdadeiro positivo", "verdadeiro negativo" e "falso negativo". Um "verdadeiro positivo" refere-se a quando os resultados do teste ea real situação da condição são ambos verdadeiros (ou "positivos"), e um "verdadeiro negativo" refere-se a quando os resultados do teste ea real situação da condição são ambos falsos (ou "negativos"); Um "verdadeiro positivo" ou um "verdadeiro negativo" é considerado como sendo uma "inferência correcta". A antítese de um "falso positivo" é um "falso negativo"; Um "falso negativo" refere-se a quando os resultados do teste are negativo (isto é, a condição é determinada para ser "negativo", ou "falso"), mas espera-se que seja (ou deveria ter sido) positivo (isto é, a condição, na realidade, é "positivo", ou "verdadeiro").

No contexto da CIDRAM, estes termos referem-se as assinaturas de CIDRAM eo que/quem eles bloqueiam. Quando CIDRAM bloquear um endereço IP devido ao mau, desatualizados ou incorretos assinatura, mas não deveria ter feito isso, ou quando ele faz isso pelas razões erradas, nos referimos a este evento como um "falso positivo". Quando CIDRAM não consegue bloquear um endereço IP que deveria ter sido bloqueado, devido a ameaças imprevistas, assinaturas em falta ou déficits em suas assinaturas, nos referimos a este evento como um "detecção em falta" ou "missing detection" (que é análogo a um "falso negativo").

Isto pode ser resumido pela seguinte tabela:

&nbsp; | CIDRAM *NÃO* deve bloquear um endereço IP | CIDRAM *DEVE* bloquear um endereço IP
---|---|---
CIDRAM *NÃO* bloquear um endereço IP | Verdadeiro negativo (inferência correcta) | Detecção em falta (análogo a um falso negativo)
CIDRAM *FAZ* bloquear um endereço IP | __Falso positivo__ | Verdadeiro positivo (inferência correcta)

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>CIDRAM pode bloquear países inteiros?

Sim. A maneira mais fácil de fazer isso seria instalando o módulo BGPView e configurando-o de acordo com suas necessidades.

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>Com que frequência as assinaturas são atualizadas?

A frequência das atualizações varia de acordo com os arquivos de assinatura em questão. Todos os mantenedores dos arquivos de assinatura de CIDRAM geralmente tentam manter suas assinaturas atualizadas como é possível, mas devido a que todos nós temos vários outros compromissos, nossas vidas fora do projeto, e devido a que nenhum de nós é financeiramente compensado (ou pago) para nossos esforços no projeto, um cronograma de atualização preciso não pode ser garantido. Geralmente, as assinaturas são atualizadas sempre que há tempo suficiente para atualizá-las, e geralmente, os mantenedores tentam priorizar com base na necessidade e na frequência com que as mudanças ocorrem entre gamas. Assistência é sempre apreciada se você estiver disposto a oferecer qualquer.

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>Eu encontrei um problema ao usar CIDRAM e eu não sei o que fazer sobre isso! Ajude-me!

- Você está usando a versão mais recente do software? Você está usando as versões mais recentes de seus arquivos de assinatura? Se a resposta a qualquer destas duas perguntas é não, tente atualizar tudo primeiro, e verifique se o problema persiste. Se persistir, continue lendo.
- Você já examinou toda a documentação? Se não, por favor, faça isso. Se o problema não puder ser resolvido usando a documentação, continue lendo.
- Você já examinou a **[página de issues](https://github.com/CIDRAM/CIDRAM/issues)**, para ver se o problema foi mencionado antes? Se já foi mencionado antes, verificar se foram fornecidas sugestões, ideias e/ou soluções, e siga conforme necessário para tentar resolver o problema.
- Se o problema ainda persistir, por favor procure ajuda sobre isso através de criando um novo issue na página de issues.

#### <a name="BLOCKED_WHAT_TO_DO"></a>Eu fui bloqueado pelo CIDRAM de um site que eu quero visitar! Ajude-me!

CIDRAM fornece um meio para proprietários de sites para bloquear tráfego indesejável, mas é da responsabilidade dos proprietários do site decidir por si mesmos como eles querem usar CIDRAM. No caso dos falsos positivos relativos aos arquivos de assinatura normalmente incluídos no CIDRAM, correções podem ser feitas, mas no que diz respeito a ser desbloqueado a partir de sites específicos, você precisará tomar isso com os proprietários dos sites em questão. Nos casos em que são feitas correções, pelo menos, eles precisarão atualizar seus arquivos de assinatura e/ou instalação, e em outros casos (tais como, por exemplo, onde eles modificaram sua instalação, criaram suas próprias assinaturas personalizadas, etc), a responsabilidade de resolver o seu problema é inteiramente deles, e está inteiramente fora de nosso controle.

#### <a name="MINIMUM_PHP_VERSION_V3"></a>Eu quero usar CIDRAM v3 com uma versão PHP mais velha do que 7.2; Você pode ajudar?

Não. PHP≥7.2 é um requisito mínimo para CIDRAM v3.

*Veja também: [Gráficos de Compatibilidade](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>Posso usar uma única instalação do CIDRAM para proteger vários domínios?

Sim. As instalações do CIDRAM não estão naturalmente atado com domínios específicos, e pode, portanto, ser usado para proteger vários domínios. Geralmente, referimo-nos a instalações do CIDRAM que protegem apenas um domínio como "instalações de singular-domínio", e referimo-nos a instalações do CIDRAM que protegem vários domínios e/ou subdomínios como "instalações multi-domínio". Se você operar uma instalação multi-domínio e precisa usar conjuntos diferentes de arquivos de assinaturas para domínios diferentes, ou precisam CIDRAM para ser configurado de forma diferente para domínios diferentes, é possível fazer isso. Depois de carregar o arquivo de configuração (`config.yml`), o CIDRAM verificará a existência de um "arquivo de sobreposição para a configuração" específico para o domínio (ou subdomínio) que está sendo solicitado (`o-domínio-que-está-sendo-solicitado.tld.config.yml`), e se encontrado, quaisquer valores de configuração definidos pelo arquivo de sobreposição para a configuração serão usados para a instância de execução em vez dos valores de configuração definidos pelo arquivo de configuração. Os arquivos de sobreposição para a configuração são idênticos ao arquivo de configuração, e a seu critério, pode conter a totalidade de todas as diretivas de configuração disponíveis para o CIDRAM, ou qualquer subseção menor necessária que difere dos valores normalmente definidos pelo arquivo de configuração. Os arquivos de sobreposição para a configuração são nomeados de acordo com o domínio que eles são destinados para (por exemplo, se você precisar de um arquivo de sobreposição para a configuração para o domínio, `https://www.some-domain.tld/`, o seu arquivo de sobreposição para a configuração deve ser nomeado como `some-domain.tld.config.yml`, e deve ser colocado dentro da vault ao lado do arquivo de configuração, `config.yml`). O nome de domínio para a instância de execução é derivado do cabeçalho `HTTP_HOST` da solicitação; "www" é ignorado.

#### <a name="PAY_YOU_TO_DO_IT"></a>Eu não quero mexer com a instalação deste e fazê-lo funcionar com o meu site; Posso pagar-te para fazer tudo por mim?

Talvez. Isso é considerado caso a caso. Deixe-nos saber do que você precisa, o que você está oferecendo, e nós vamos deixar você saber se podemos ajudar.

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>Posso contratar você ou qualquer um dos desenvolvedores deste projeto para o trabalho privado?

*Veja acima.*

#### <a name="SPECIALIST_MODIFICATIONS"></a>Preciso de modificações especializadas, customizações, etc; Você pode ajudar?

*Veja acima.*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>Eu sou um desenvolvedor, designer de site, ou programador. Posso aceitar ou oferecer trabalho relacionado a este projeto?

Sim. Nossa licença não proíbe isso.

#### <a name="WANT_TO_CONTRIBUTE"></a>Quero contribuir para o projeto; Posso fazer isso?

Sim. As contribuições para o projeto são muito bem-vindas. Consulte "CONTRIBUTING.md" para obter mais informações.

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>Posso usar o cron para atualizar automaticamente?

Sim. Uma API é integrada no front-end para interagir com a página de atualizações por meio de scripts externos. Um script separado, "[Cronable](https://github.com/Maikuolan/Cronable)", está disponível, e pode ser usado pelo seu cron manager ou cron scheduler para atualizar este e outros pacotes suportados automaticamente (este script fornece sua própria documentação).

#### <a name="WHAT_ARE_INFRACTIONS"></a>O que são "infrações"?

"Contagem de assinaturas" e "infrações" estão relacionadas à gravidade e ao número de assinaturas acionadas durante qualquer solicitação específica, seja devido a arquivos de assinatura, módulos, regras auxiliares, ou de outra forma, mas enquanto a "contagem de assinaturas" persiste apenas para essa solicitação específica, as "infrações" podem persistir em qualquer número de solicitações, enquanto for determinado pelo `default_tracktime`.

Isso fornece um mecanismo para garantir que solicitações de fontes potencialmente perigosas possam ser bloqueadas em solicitações secundárias de qualquer fonte específica, em que essa fonte já tenha sido bloqueada durante uma solicitação anterior com um número suficiente de infrações.

#### <a name="BLOCK_HOSTNAMES"></a>O CIDRAM pode bloquear nomes de host?

Sim. Isso pode ser feito criando uma regra auxiliar ou um módulo personalizado.

![Uma regra auxiliar para bloquear nomes de host](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>O que posso usar para "default_dns"?

Geralmente, o IP de qualquer servidor DNS confiável deve ser suficiente. Se você está procurando sugestões, [public-dns.info](https://public-dns.info/) e [OpenNIC](https://servers.opennic.org/) fornecem listas extensas de servidores DNS públicos conhecidos. Alternativamente, veja a tabela abaixo:

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

*Nota: Eu não faço reivindicações ou garantias em relação às práticas de privacidade, segurança, eficácia ou confiabilidade de quaisquer serviços de DNS, listados ou não. Por favor, faça sua própria pesquisa ao tomar decisões sobre eles.*

#### <a name="PROTECT_OTHER_THINGS"></a>Posso usar o CIDRAM para proteger outras coisas além de sites (por exemplo, servidores de e-mail, FTP, SSH, IRC, etc)?

Você pode (legalmente), mas não deveria (tecnicamente; praticamente). Nossa licença não limita quais tecnologias implementam o CIDRAM, mas o CIDRAM é um WAF (Web Application Firewall) e sempre foi destinado a proteger sites. Porque não foi projetado com outras tecnologias em mente, é improvável que seja eficaz ou fornecer proteção confiável para outras tecnologias, é provável que a implementação seja difícil, e o risco de falsos positivos e de detecções perdidas é muito alto.

#### <a name="CDN_CACHING_PROBLEMS"></a>Ocorrerão problemas se eu usar o CIDRAM ao mesmo tempo que usando CDNs ou serviços de cache?

Talvez. Isso depende da natureza do serviço em questão e de como você o utiliza. Geralmente, se você estiver armazenando apenas recursos estáticos em cache (imagens, CSS, etc; qualquer coisa que geralmente não muda com o tempo), não haverá problemas. Mas, pode haver problemas, se você estiver armazenando dados em cache que normalmente seriam gerados dinamicamente quando solicitados, ou se você estiver armazenando em cache os resultados de solicitações POST (isso essencialmente tornaria seu site e seu ambiente como obrigatoriamente estáticos, e é improvável que a CIDRAM forneça qualquer benefício significativo em um ambiente obrigatoriamente estático). Também pode haver requisitos de configuração específicos para o CIDRAM, dependendo de qual CDN ou serviço de cache você está usando (você precisará garantir que o CIDRAM esteja configurado corretamente para o CDN específico ou serviço de cache que você está usando). A falha em configurar o CIDRAM corretamente pode levar a falsos positivos e a detecções perdidas.

#### <a name="DDOS_ATTACKS"></a>A CIDRAM protegerá meu site contra ataques DDoS?

Resposta curta: Não.

Resposta ligeiramente mais longa: O CIDRAM ajudará a reduzir o impacto que o tráfego indesejado pode ter em seu website (reduzindo assim os custos de largura de banda do seu site), ajudará a reduzir o impacto que o tráfego indesejado pode causar em seu hardware (por exemplo, a capacidade do seu servidor de processar e atender solicitações), e poderá ajudar a reduzir vários outros possíveis efeitos negativos associados ao tráfego indesejado. No entanto, há duas coisas importantes que devem ser lembradas para entender essa questão.

Em primeiro lugar, o CIDRAM é um pacote PHP e, portanto, opera na máquina em que o PHP está instalado. Isso significa que o CIDRAM só pode ver e bloquear uma solicitação *após* o servidor já ter recebido. Em segundo lugar, a [mitigação de DDoS](https://pt.wikipedia.org/wiki/Mitiga%C3%A7%C3%A3o_de_ataques_DDoS) eficaz deve filtrar as solicitações *antes* que elas atinjam o servidor alvo do ataque DDoS. Idealmente, os ataques DDoS devem ser detectados e mitigados por soluções capazes de eliminar ou reencaminhar o tráfego associado a ataques, antes de atingir o servidor de destino em primeiro lugar.

Isso pode ser implementado usando soluções de hardware dedicadas no local, e/ou soluções baseadas em nuvem, como serviços dedicados de mitigação de DDoS, roteamento de DNS de um domínio por meio de redes resistentes a DDoS, filtragem baseada em nuvem, ou alguma combinação dos mesmos. Em todo caso, esse assunto é um pouco complexo demais para ser explicado com apenas um ou dois parágrafos, então eu recomendaria fazer mais pesquisas se este é um assunto que você deseja seguir. Quando a verdadeira natureza dos ataques DDoS é entendida corretamente, essa resposta fará mais sentido.

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>Quando eu ativar ou desativar os módulos ou os arquivos de assinatura através da página de atualizações, eles os classificam alfanumericamente na configuração. Posso mudar a maneira como eles são classificados?

Sim. Se você precisar forçar alguns arquivos a serem executados numa ordem específica, você pode adicionar alguns dados arbitrários antes de seus nomes na diretiva de configuração, onde eles estão listados, separados por dois pontos. Quando a página de atualizações subseqüentemente classifica os arquivos novamente, esses dados arbitrários adicionados afetarão a ordem de classificação, fazendo com que eles sejam executados na ordem que você deseja, sem precisar renomear nenhum deles.

Por exemplo, assumindo uma diretiva de configuração com arquivos listados da seguinte maneira:

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

Se você queria `file3.php` para executar primeiro, você poderia adicionar algo como `aaa:` antes do nome do arquivo:

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

Então, se um novo arquivo, `file6.php`, estiver ativado, quando a página de atualizações classifica os novamente, ele deve terminar assim:

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

Mesma situação quando um arquivo é desativado. Por outro lado, se você quiser que o arquivo seja executado por último, você poderia adicionar algo como `zzz:` antes do nome do arquivo. Em qualquer caso, você não precisará renomear o arquivo em questão.

#### <a name="HOW_TO_USE_PDO"></a>O que é um "PDO DSN"? Como posso usar o PDO com o CIDRAM?

"PDO" é um acrônimo para "[PHP data objects](https://www.php.net/manual/pt_BR/intro.pdo.php)" (objetos de dados PHP). Ele fornece uma interface para o PHP poder se conectar a alguns sistemas de banco de dados comumente utilizados por vários aplicativos PHP.

"DSN" é um acrônimo para "[data source name](https://pt.wikipedia.org/wiki/Data_source_name)" (nome da fonte de dados). O "PDO DSN" descreve ao PDO como ele deve se conectar a um banco de dados.

O CIDRAM oferece a opção de utilizar o PDO para fins de armazenamento em cache. Para que isso funcione corretamente, você precisará configurar o CIDRAM adequadamente, habilitando a PDO, criar um novo banco de dados para o CIDRAM usar (se você ainda não tem em mente um banco de dados para o CIDRAM usar), e criar um novo tabela em seu banco de dados de acordo com a estrutura descrita abaixo.

Quando uma conexão com o banco de dados for bem-sucedida, mas a tabela necessária não existir, ela tentará criá-la automaticamente. Mas, esse comportamento não foi extensivamente testado e o sucesso não pode ser garantido.

Obviamente, isso só se aplica se você realmente quiser que o CIDRAM use o PDO. Se você estiver suficientemente satisfeito pelo CIDRAM de usar o cache de arquivos simples (por sua configuração padrão) ou qualquer uma das várias outras opções de cache fornecidas, não será necessário se preocupar em configurar bancos de dados, tabelas e assim por diante.

A estrutura descrita abaixo usa "cidram" como o nome do banco de dados, mas você pode usar o nome que desejar para o banco de dados, contanto que o mesmo nome seja replicado na configuração do DSN.

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

A diretiva de configuração `pdo_dsn` do CIDRAM deve ser configurada conforme descrito abaixo.

```
Dependendo do driver de banco de dados usado...
├─4d (Aviso: Experimental, não testado, não recomendado!)
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └O host para conectar-se para encontrar o banco de dados.
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └O nome do banco de dados a ser
│                │              │             usado.
│                │              │
│                │              └O número da porta com a qual se conectar ao
│                │               host.
│                │
│                └O host para conectar-se para encontrar o banco de dados.
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └O nome do banco de dados a ser usado.
│    │          │
│    │          └O host para conectar-se para encontrar o banco de dados.
│    │
│    └Valores possíveis: "mssql", "sybase", "dblib".
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├Pode ser um caminho para um arquivo de banco de dados
│                    │local.
│                    │
│                    ├Pode se conectar com um host e um número de porta.
│                    │
│                    └Você deve consultar a documentação do Firebird se quiser
│                     usá-lo.
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └O banco de dados catalogado para se conectar.
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └O banco de dados catalogado para se conectar.
├─mysql (Mais recomendado!)
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └O número da porta com a qual se
│                 │            │               conectar ao host.
│                 │            │
│                 │            └O host para conectar-se para encontrar o banco
│                 │             de dados.
│                 │
│                 └O nome do banco de dados a ser usado.
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├Pode se referir ao banco de dados catalogado específico.
│               │
│               ├Pode se conectar com um host e um número de porta.
│               │
│               └Você deve consultar a documentação do Oracle se quiser usá-lo.
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├Pode se referir ao banco de dados catalogado específico.
│         │
│         ├Pode se conectar com um host e um número de porta.
│         │
│         └Você deve consultar a documentação do ODBC/DB2 se quiser usá-lo.
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └O nome do banco de dados a ser
│               │              │            usado.
│               │              │
│               │              └O número da porta com a qual se conectar ao
│               │               host.
│               │
│               └O host para conectar-se para encontrar o banco de dados.
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └O caminho para o arquivo de banco de dados local a ser usado.
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └O nome do banco de dados a ser usado.
                   │         │
                   │         └O número da porta com a qual se conectar ao host.
                   │
                   └O host para conectar-se para encontrar o banco de dados.
```

Se você não tiver certeza sobre o que usar para uma parte específica do seu DSN, tente primeiro verificar se funciona como está, sem alterar nada.

Note que `pdo_username` e `pdo_password` devem ser iguais ao nome de usuário e senha que você escolheu para o seu banco de dados.

#### <a name="BLOCK_CRON"></a>CIDRAM está bloqueando cronjobs; Como consertar isto?

Se você estiver usando um arquivo dedicado para os cronjobs, e se esse arquivo não precisar ser chamado durante solicitações normais do usuário (ou seja, fora do contexto dos cronjobs), a maneira mais direta de corrigir isso seria garantir que o CIDRAM não seja executado durante seus cronjobs (ou seja, não conecte o CIDRAM ao arquivo responsável por manipular seus cronjobs).

Como alternativa, se isso não for possível, mas o endereço IP do seu servidor cron é relativamente consistente e previsível, você pode tentar colocar na lista branca o endereço IP do seu servidor cron, por criando uma assinatura da lista branca em um arquivo de assinaturas personalizados, ou por criando uma regra auxiliar para a lista branca. Se o endereço IP do seu servidor cron é mudado regularmente e não é particularmente previsível, mas ainda assim permanece de dentro da mesma rede específica, você pode tentar listar no seu arquivo `ignore.dat` o nome da seção de assinaturas responsável por bloqueá-lo em primeiro lugar.

Se você tentou todas essas ideias e nenhuma delas funcionou para você, ou se precisar de ajuda para descobrir como fazê-lo, você pode criar um novo issue na página de issues do CIDRAM para solicitar ajuda.

---


### 9. <a name="SECTION9"></a>INFORMAÇÃO LEGAL

#### 9.0 PREÂMBULO DE SEÇÃO

Esta seção da documentação destina-se a descrever possíveis considerações legais em relação ao uso e implementação do pacote, e fornecer algumas informações básicas relacionadas. Isso pode ser importante para alguns usuários como um meio de garantir a conformidade com quaisquer requisitos legais que possam existir nos países nos quais eles operam, e alguns usuários podem precisar ajustar as políticas do site de acordo com essas informações.

Em primeiro lugar por favor, perceba que eu (o autor do pacote) não sou advogado, nem profissional legal qualificado de qualquer tipo. Portanto, não estou legalmente qualificado para fornecer aconselhamento jurídico. Além disso, em alguns casos, exigências legais exatas podem variar entre diferentes países e jurisdições, e estes requisitos legais variados podem, às vezes, conflitar (como, por exemplo, no caso de países que defendem os [direitos de privacidade](https://pt.wikipedia.org/wiki/Direito_%C3%A0_privacidade) e o [direito de ser esquecido](https://pt.wikipedia.org/wiki/Direito_ao_esquecimento), versus países que favorecem a retenção prolongada de dados). Considere também que o acesso ao pacote não está restrito a países ou jurisdições específicos e, portanto, o pacote userbase é provável que seja geograficamente diverso. Estes pontos considerados, eu não estou em posição de afirmar o que significa ser "legalmente compatível" para todos os usuários, em todos os aspectos. No entanto, espero que as informações aqui contidas o ajudem a chegar a uma decisão sobre o que você deve fazer para permanecer legalmente conforme no contexto do pacote. Se tiver alguma dúvida ou preocupação em relação às informações aqui contidas, ou se você precisar de ajuda e conselhos adicionais de uma perspectiva legal, eu recomendaria consultar um profissional legal qualificado.

#### 9.1 RESPONSABILIDADE

Conforme já declarado pela licença do pacote, o pacote é fornecido sem qualquer garantia. Isso inclui (mas não está limitado a) todo o escopo de responsabilidade. O pacote é fornecido a você para sua conveniência, na esperança de que seja útil e que traga algum benefício para você. Entretanto, se você usa ou implementa o pacote, é sua própria escolha. Você não é forçado a usar ou implementar o pacote, mas, quando o faz, você é responsável por essa decisão. Nem eu, nem qualquer outro colaborador do pacote, somos legalmente responsáveis pelas consequências das decisões que você toma, independentemente de ser direto, indireto, implícito, ou de outra forma.

#### 9.2 TERCEIROS

Dependendo de sua configuração e implementação exatas, o pacote pode se comunicar e compartilhar informações com terceiros em alguns casos. Essas informações podem ser definidas como "[informação pessoalmente identificável](https://pt.wikipedia.org/wiki/Informa%C3%A7%C3%A3o_pessoalmente_identific%C3%A1vel)" (PII) em alguns contextos, por algumas jurisdições.

Como esta informação pode ser usada por estes terceiros, está sujeita às várias políticas estabelecidas por esses terceiros, e está fora do escopo desta documentação. Contudo, em todos esses casos, o compartilhamento de informações com esses terceiros pode ser desativado. Em todos esses casos, se você optar por ativá-lo, é sua responsabilidade pesquisar quaisquer preocupações que você possa ter com relação à privacidade, segurança, e uso de PII por esses terceiros. Se houver alguma dúvida, ou se você estiver insatisfeito com a conduta desses terceiros em relação a PII, talvez seja melhor desativar todo o compartilhamento de informações com esses terceiros.

Para fins de transparência, o tipo de informação compartilhada e com quem está descrito abaixo.

##### 9.2.0 PESQUISA DE NOME DE HOST

Se você usar quaisquer funções ou módulos destinados a trabalhar com nomes de host (tais como o "módulo bloqueador de hosts perigosos", o "tor project exit nodes block module", ou "verificação dos motores de busca", por exemplo), o CIDRAM precisa ser capaz de obter o nome do host de solicitações de entrada de alguma forma. Tipicamente, ele faz isso solicitando o nome do host do endereço IP das solicitações de entrada de um servidor DNS ou solicitando as informações por meio da funcionalidade fornecida pelo sistema em que o CIDRAM está instalado (isso é tipicamente referido como um "pesquisa de nome de host"). Os servidores DNS definidos por padrão pertencem ao serviço [Google DNS](https://dns.google.com/) (mas isso pode ser facilmente alterado por meio da configuração). Os serviços exatos comunicados com são configuráveis, e dependem de como você configura o pacote. No caso de usar a funcionalidade fornecida pelo sistema em que o CIDRAM está instalado, você precisará entrar em contato com o administrador do sistema para determinar quais rotas as pesquisas de nome de host usam. Pesquisas de nome de host podem ser evitadas no CIDRAM, evitando os módulos afetados ou modificando a configuração do pacote de acordo com suas necessidades.

*Diretivas de configuração relevantes:*
- `general` -> `allow_gethostbyaddr_lookup`
- `general` -> `default_dns`
- `general` -> `force_hostname_lookup`
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.1 VERIFICAÇÃO DOS MOTORES DE BUSCA E MÍDIAS SOCIAIS

Quando a verificação dos motores de busca é ativada, o CIDRAM tenta executar pesquisas direta DNS para verificar se as solicitações que dizem ter origem nos motores de busca são autênticas. Da mesma forma, quando a verificação de mídia social é ativada, o CIDRAM faz o mesmo para solicitações aparentes de mídia social. Para fazer isso, ele usa o serviço [Google DNS](https://dns.google.com/) para tentar resolver endereços IP dos nomes de host dessas solicitações de entrada (nesse processo, os nomes de host dessas solicitações de entrada são compartilhados com o serviço).

*Diretivas de configuração relevantes:*
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.2 CAPTCHA

CIDRAM oferece suporte a reCAPTCHA e hCAPTCHA. Eles requerem chaves de API para funcionar corretamente. Eles são desativados por padrão, mas podem ser ativados configurando as chaves API necessárias. Quando ativado, a comunicação pode ocorrer entre o serviço e o CIDRAM ou o navegador do usuário. Isso pode envolver a comunicação de informações como o endereço IP do usuário, agente do usuário, sistema operacional, e outros detalhes disponíveis para a solicitação.

##### 9.2.3 STOP FORUM SPAM

O [Stop Forum Spam](https://www.stopforumspam.com/) é um serviço fantástico, disponível gratuitamente, que pode ajudar a proteger fóruns, blogs, e sites de spammers. Ele faz isso fornecendo um banco de dados de spammers conhecidos, e uma API que pode ser aproveitada para verificar se um endereço IP, nome de usuário, ou um endereço de e-mail está listado em seu banco de dados.

O CIDRAM fornece um módulo opcional que aproveita essa API para verificar se o endereço IP de solicitações de entrada pertence a um spammer suspeito. Quando o módulo é instalado e ativado, os endereços IP do usuário podem ser compartilhados com o serviço de acordo com a configuração e finalidade do módulo.

##### 9.2.4 ABUSEIPDB

O CIDRAM fornece um módulo opcional para bloquear endereços IP abusivos usando a API [AbuseIPDB](https://www.abuseipdb.com/). Quando o módulo é instalado e ativado, os endereços IP do usuário podem ser compartilhados com o serviço de acordo com a configuração e finalidade do módulo.

##### 9.2.5 BGPVIEW, IP-API

O CIDRAM fornece módulos opcionais para executar pesquisas de ASN e de código de país usando a API [BGPView](https://bgpview.io/) e a API [IP-API](https://ip-api.com/). Essas pesquisas fornecem a capacidade de bloquear ou colocar na lista branca com base no ASN ou no país de origem. Quando um deles está instalado e ativado, os endereços IP do usuário podem ser compartilhados com o serviço de acordo com a configuração e finalidade do módulo.

##### 9.2.6 PROJECT HONEYPOT

O CIDRAM fornece um módulo opcional para bloquear endereços IP abusivos usando a API [Project Honeypot](https://www.projecthoneypot.org/). Quando o módulo é instalado e ativado, os endereços IP do usuário podem ser compartilhados com o serviço de acordo com a configuração e finalidade do módulo.

#### 9.3 REGISTRO

O registro é uma parte importante do CIDRAM por vários motivos. Pode ser difícil diagnosticar e resolver falsos positivos quando os eventos de bloqueio que os causam não são registrados. Sem o registro de eventos de bloqueio, pode ser difícil determinar exatamente o quão bem o CIDRAM funciona em qualquer contexto específico, e pode ser difícil determinar onde suas deficiências podem ser, e quais mudanças podem ser necessárias para sua configuração ou assinaturas de acordo, para que ele continue funcionando como pretendido. Não obstante, o registro pode não ser desejável para todos os usuários e permanece totalmente opcional. No CIDRAM, o registro está desativado por padrão. Para ativá-lo, o CIDRAM deve ser configurado de acordo.

Adicionalmente, se o registro é legalmente permissível, e na medida em que é legalmente permissível (por exemplo, os tipos de informações que podem ser registradas, por quanto tempo, e sob quais circunstâncias), pode variar, dependendo da jurisdição e do contexto onde a CIDRAM é implementada (por exemplo, se você está operando como indivíduo, como entidade corporativa, e se está numa base comercial ou não comercial). Portanto, pode ser útil que você leia atentamente essa seção.

Existem vários tipos de registro que o CIDRAM pode executar. Diferentes tipos de registro envolvem diferentes tipos de informações, por diferentes razões.

##### 9.3.0 OS EVENTOS DE BLOQUEIO

O principal tipo de registro que o CIDRAM pode realizar refere-se a "eventos de bloqueio". Esse tipo do registro está relacionado a quando o CIDRAM bloqueia uma solicitação, e pode ser fornecido em três formatos diferentes:
- Arquivos de log legíveis para humanos.
- Arquivos de log no estilo Apache.
- Arquivos de log serializados.

Um evento de bloqueio, registrado em um arquivo de log legível, normalmente se parece com isso (como um exemplo):

```
ID: 1234
Versão do script: CIDRAM v1.6.0
Data/Hora: Day, dd Mon 20xx hh:ii:ss +0000
Endereço IP: x.x.x.x
Nome do host: dns.hostname.tld
Contagem da assinaturas: 1
Assinaturas referência: x.x.x.x/xx
Razão bloqueada: Serviço de nuvem ("Nome da rede", Lxx:Fx, [XX])!
Agente do usuário: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
Reconstruído URI: https://your-site.tld/index.php
Estado CAPTCHA: Ativado.
```

Esse mesmo evento de bloqueio, registrado em um arquivo de log no estilo Apache, normalmente se parece com isso:

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

Um evento de bloqueio registrado geralmente inclui as seguintes informações:
- Um número de ID que referência o evento de bloqueio.
- A versão do CIDRAM atualmente em uso.
- A data e hora em que o evento de bloqueio ocorreu.
- O endereço IP da solicitação bloqueada.
- O nome do host do endereço IP da solicitação bloqueada (quando disponível).
- O número de assinaturas desencadeadas pela solicitação.
- Referências às assinaturas desencadeadas.
- Referências aos motivos do evento de bloqueio e algumas informações básicas de depuração relacionadas.
- O agente do usuário da solicitação bloqueada (ou seja, como a entidade solicitante se identificou com a solicitação).
- Uma reconstrução do identificador para o recurso originalmente solicitado.
- O estado CAPTCHA para a solicitação atual (quando relevante).

*As diretivas de configuração responsáveis por esse tipo de log, e para cada um dos três formatos disponíveis, são:*
- `logging` -> `apache_style_log`
- `logging` -> `serialised_log`
- `logging` -> `standard_log`

Quando essas diretivas são deixadas vazias, esse tipo de log permanecerá desativado.

##### 9.3.1 REGISTRO DE CAPTCHA

Esse tipo de registro refere-se especificamente a instâncias de CAPTCHA, e ocorre apenas quando um usuário tenta concluir uma instância de CAPTCHA.

Uma entrada de registro CAPTCHA contém o endereço IP do usuário que está tentando concluir uma instância de CAPTCHA, a data e a hora em que a tentativa ocorreu, e o estado CAPTCHA. Uma entrada de registro CAPTCHA normalmente se parece com isso (como um exemplo):

```
Endereço IP: x.x.x.x - Data/Hora: Day, dd Mon 20xx hh:ii:ss +0000 - Estado CAPTCHA: Sucesso!
```

*A diretiva de configuração responsável pelo registro de CAPTCHA é:*
- `hcaptcha` -> `hcaptcha_log`
- `recaptcha` -> `recaptcha_log`

##### 9.3.2 REGISTRO DO FRONT-END

Esse tipo de registro está associado a tentativas de login no front-end, e ocorre apenas quando um usuário tenta efetuar login no front-end (supondo que o acesso ao front-end esteja ativado).

Uma entrada de registro do front-end contém o endereço IP do usuário que está tentando efetuar login, a data e a hora em que a tentativa ocorreu, e os resultados da tentativa (se teve sucesso ou não). Uma entrada de registro do front-end geralmente se parece com isso (como um exemplo):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Conectado.
```

*A diretiva de configuração responsável pelo registro do front-end é:*
- `frontend` -> `frontend_log`

##### 9.3.3 ROTAÇÃO DE REGISTRO

Você pode querer purgar os registros após um período de tempo, ou pode ser obrigado a fazê-lo por lei (ou seja, a quantidade de tempo permitida legalmente para você manter registros pode ser limitada por lei). Você pode conseguir isso incluindo marcadores de data/hora nos nomes de seus arquivos de log conforme especificado pela sua configuração de pacote (por exemplo, `{yyyy}-{mm}-{dd}.log`) e, em seguida, ativando a rotação de registro (a rotação de registro permite que você execute alguma ação nos arquivos de log quando os limites especificados são excedidos).

Por exemplo: Se eu fosse legalmente obrigado a deletar registros após 30 dias, eu poderia especificar `{dd}.log` nos nomes dos meus arquivos de log (`{dd}` representa dias), definir o valor de `log_rotation_limit` para 30 e, em seguida, definir o valor de `log_rotation_action` para `Delete`.

Por outro lado, se você precisar reter o registros por um longo período de tempo, você poderia optar por não usar a rotação de registro em tudo, ou você pode definir o valor de `log_rotation_action` para `Archive`, para compactar arquivos de log, reduzindo assim a quantidade total de espaço em disco que eles ocupam.

*Diretivas de configuração relevantes:*
- `logging` -> `log_rotation_action`
- `logging` -> `log_rotation_limit`

##### 9.3.4 TRUNCAMENTO DE REGISTRO

Também é possível truncar arquivos de log individuais quando eles excedem um certo tamanho, se isso for algo que você possa precisar ou desejar fazer.

*Diretivas de configuração relevantes:*
- `logging` -> `truncate`

##### 9.3.5 PSEUDONIMIZAÇÃO DE ENDEREÇOS IP

Em primeiro lugar, se você não estiver familiarizado com o termo, "pseudonimização" refere-se ao processamento de dados pessoais como tal que não pode ser identificado a nenhuma pessoa específica sem informações suplementares, e desde que tais informações suplementares sejam mantidas separadamente e sujeitas a medidas técnicas e organizacionais para assegurar que os dados pessoais não possam ser identificados a nenhuma pessoa natural.

Em algumas circunstâncias, você pode ser legalmente obrigado a anonimizar ou pseudonimizar qualquer PII coletada, processada ou armazenada. Embora este conceito já existe há algum tempo, o GDPR/DSGVO menciona notavelmente, e especificamente incentiva a "pseudonimização".

O CIDRAM é capaz de pseudonimizar endereços IP ao registrá-los, se isso for algo que você possa precisar ou desejar fazer. Quando o CIDRAM pseudonimiza os endereços IP, quando registrado, o octeto final dos endereços IPv4, e tudo após a segunda parte dos endereços IPv6 é representado por um "x" (efetivamente arredondando endereços IPv4 para o endereço inicial da 24ª sub-rede em que eles são fatorados em, e endereços IPv6 para o endereço inicial da 32ª sub-rede em que eles são fatorados em).

*Nota: O processo de pseudonimização de endereços IP no CIDRAM não afeta a funcionalidade de monitoração IP no CIDRAM. Se isso for um problema para você, talvez seja melhor desabilitar totalmente o monitoramento de IP.*

*Diretivas de configuração relevantes:*
- `legal` -> `pseudonymise_ip_addresses`

##### 9.3.6 OMITINDO INFORMAÇÕES DE REGISTRO

Se você quiser dar um passo adiante, impedindo que tipos específicos de informação sejam registrados inteiramente, isso também é possível. Na página de configuração, consulte a diretiva de configuração `fields` para controlar quais campos aparecem nas entradas de log e na página "Acesso Negado".

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

*Nota: Não há motivo para pseudônimo de endereços IP quando omití-los totalmente dos registros.*

*Diretivas de configuração relevantes:*
- `general` -> `fields`

##### 9.3.7 ESTATISTICAS

O CIDRAM é opcionalmente capaz de rastrear estatísticas como o número total de eventos de bloqueio ou instâncias de CAPTCHA que ocorreram desde algum momento específico no tempo. Esta funcionalidade está desativada por padrão, mas pode ser ativada através da configuração do pacote. Essa funcionalidade rastreia apenas o número total de eventos ocorridos e não inclui informações sobre eventos específicos (e, portanto, não deve ser considerado como PII).

*Diretivas de configuração relevantes:*
- `general` -> `statistics`

##### 9.3.8 ENCRIPTAÇÃO

CIDRAM não criptografa seu cache ou qualquer informação de registro. A [encriptação](https://pt.wikipedia.org/wiki/Encripta%C3%A7%C3%A3o) de cache e registro pode ser introduzida no futuro, mas não há planos específicos para ela atualmente. Se você estiver preocupado com o acesso de terceiros não autorizados a partes do CIDRAM que possam conter PII ou informações confidenciais, como cache ou logs, recomendo que o CIDRAM não seja instalado em um local de acesso público (por exemplo, instale o CIDRAM fora do diretório `public_html` padrão ou seu equivalente disponível para a maioria dos servidores web padrão) e que as permissões apropriadamente restritivas sejam impostas para o diretório em que ele reside (em particular, para o diretório do vault). Se isso não for suficiente para resolver suas preocupações, configure o CIDRAM para que os tipos de informações que causam suas preocupações não sejam coletados ou registrados em primeiro lugar (tal como desabilitar o registro em log).

#### 9.4 COOKIES

O CIDRAM define [cookies](https://pt.wikipedia.org/wiki/Cookie_(inform%C3%A1tica)) em dois pontos em sua base de código. Em primeiro lugar, quando um usuário concluir com êxito uma instância de CAPTCHA (e supondo que `lockuser` esteja definido como `true`), O CIDRAM define um cookie para poder lembrar, para solicitações subsequentes, que o usuário já concluiu uma instância de CAPTCHA, de modo que não será necessário pedir continuamente ao usuário para concluir uma instância de CAPTCHA em solicitações subsequentes. Em segundo lugar, quando um usuário efetua login com êxito no front-end, o CIDRAM define um cookie para poder lembrar o usuário das solicitações subsequentes (isto é, os cookies são usados para autenticar o usuário numa sessão de login).

Em ambos os casos, os avisos de cookie são exibidos de forma proeminente (quando aplicável), avisando ao usuário que os cookies serão definidos se eles se envolverem nas ações relevantes. Os cookies não são definidos em nenhum outro ponto da base de código.

*Nota: As APIs CAPTCHA "invisíveis" podem ser incompatíveis com as leis de cookies em algumas jurisdições, e deve ser evitada por quaisquer websites sujeitos a essas leis. Optar por usar as outras APIs fornecidas, ou simplesmente desativar CAPTCHA totalmente, pode ser preferível.*

*Diretivas de configuração relevantes:*
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 9.5 MARKETING E PUBLICIDADE

A CIDRAM não coleta ou processa qualquer informação para fins de marketing ou publicidade, e nem vende nem lucra com qualquer informação coletada ou registrada. A CIDRAM não é uma empresa comercial, nem está relacionada a nenhum interesse comercial, portanto, fazer essas coisas não faria sentido. Este tem sido o caso desde o início do projeto, e continua sendo o caso hoje. Além disso, fazer essas coisas seria contraproducente para o espírito e propósito do projeto como um todo, e enquanto eu continuar a manter o projeto, nunca acontecerá.

#### 9.6 POLÍTICA DE PRIVACIDADE

Em algumas circunstâncias, você pode ser legalmente obrigado a exibir claramente um link para sua política de privacidade em todas as páginas e seções do seu site. Isso pode ser importante como um meio de garantir que os usuários estejam bem informados sobre suas práticas de privacidade exatas, os tipos de PII que você coletar, e como você pretende usá-lo. Para poder incluir esse link na página "Acesso Negado" do CIDRAM, é fornecida uma diretiva de configuração para especificar o URL da sua política de privacidade.

*Nota: É altamente recomendável que sua página de política de privacidade não seja colocada atrás da proteção do CIDRAM. Se o CIDRAM proteger sua página de política de privacidade, e um usuário bloqueado pelo CIDRAM clicar no link para sua política de privacidade, ele será bloqueado novamente e não poderá ver sua política de privacidade. O ideal é vincular a uma cópia estática de sua política de privacidade, como uma página HTML ou um arquivo de texto simples que não esteja protegido pelo CIDRAM.*

*Diretivas de configuração relevantes:*
- `legal` -> `privacy_policy`

#### 9.7 GDPR/DSGVO

O Regulamento Geral sobre a Proteção de Dados (GDPR) é um regulamento da União Europeia, que entra em vigor em 25 de Maio, 2018. O principal objectivo do regulamento é dar controlo aos cidadãos e residentes da UE relativamente aos seus próprios dados pessoais, e unificar a regulação na UE em matéria de privacidade e dados pessoais.

O regulamento contém disposições específicas relativas ao tratamento de "[informações pessoalmente identificáveis](https://pt.wikipedia.org/wiki/Informa%C3%A7%C3%A3o_pessoalmente_identific%C3%A1vel)" (PII) de quaisquer "titulares de dados" (qualquer identificada ou identificável pessoa natural) da UE ou dentro da mesma. Para estar em conformidade com o regulamento, "empresas" (conforme definido pelo regulamento), e quaisquer sistemas e processos relevantes devem implementar "[privacidade desde a concepção](https://pt.wikipedia.org/wiki/Privacidade_desde_a_concep%C3%A7%C3%A3o)" por padrão, devem usar as configurações de privacidade mais altas possíveis, devem implementar as proteções necessárias para qualquer informação armazenada ou processada (incluindo, mas não limitado a, a implementação de pseudonimização ou anonimização completa de dados), devem declarar clara e inequivocamente os tipos de dados que coletam, como os processam, por quais motivos, por quanto tempo eles o retêm, e se compartilham esses dados com terceiros, os tipos de dados compartilhados com terceiros, como, porque, e assim por diante.

Os dados não podem ser processados a menos que haja uma base legal para isso, conforme definido pelo regulamento. Geralmente, isso significa que, para processar os dados de um titular de dados de forma legal, ele deve ser feito em conformidade com obrigações legais, ou feito somente após o consentimento explícito, bem informado, e inequívoco ter sido obtido do titular dos dados.

Como os aspectos da regulamentação podem evoluir no tempo, a fim de evitar a propagação de informações desatualizadas, pode ser melhor aprender sobre a regulamentação a partir de uma fonte oficial, em vez de simplesmente incluir as informações relevantes aqui na documentação do pacote (o que pode eventualmente desatualizado à medida que a regulamentação evolui).

[EUR-Lex](https://eur-lex.europa.eu/) (uma parte do site oficial da União Europeia que fornece informações sobre a legislação da UE) fornece informações abrangentes sobre o GDPR/DSGVO, disponível em 24 idiomas diferentes (no momento da escrita deste), e disponível para download em formato PDF. Eu recomendaria definitivamente ler as informações que eles fornecem, a fim de aprender mais sobre GDPR/DSGVO:
- [REGULAMENTO (UE) 2016/679 DO PARLAMENTO EUROPEU E DO CONSELHO](https://eur-lex.europa.eu/legal-content/PT/TXT/?uri=celex:32016R0679)

Alternativamente, há uma breve visão geral (não autoritativa) do GDPR/DSGVO disponível na Wikipedia:
- [Regulamento Geral sobre a Proteção de Dados](https://pt.wikipedia.org/wiki/Regulamento_Geral_sobre_a_Prote%C3%A7%C3%A3o_de_Dados)

---


### 10. <a name="SECTION10"></a>ATUALIZANDO DE VERSÕES PRINCIPAIS ANTERIORES

#### 10.0 CIDRAM v3

Existem diferenças significativas entre a v3 e as versões principais anteriores. A maneira como os pontos de entrada funcionam, a maneira como os módulos são estruturados, e a maneira como o atualizador funciona para v3 é diferente da maneira como essas coisas funcionavam nas versões principais anteriores. Devido a essas diferenças, a melhor maneira de atualizar para v3 de versões principais anteriores seria realizar uma nova instalação.

Se você deseja manter sua configuração e suas regras auxiliares, antes de iniciar o processo de atualização, acesse a página de backup do front-end. A partir daí, a configuração e as regras auxiliares podem ser exportados. A exportação fará com que um arquivo seja baixado. Depois de atualizar para a nova versão principal, esse arquivo pode ser usado para importar os dados exportados anteriormente para a instalação.

Devido às mudanças na forma como os módulos são estruturados, os módulos destinados às versões principais anteriores precisariam ser reescritos para funcionar corretamente na v3. A migração direta não funcionará. O mesmo vale para eventos.

A forma como os arquivos de assinatura são estruturados não mudou, portanto, os arquivos de assinatura destinados a versões principais anteriores podem ser migrados diretamente para a v3 sem nenhum problema antecipado.

Módulos, arquivos de assinatura, e eventos têm seus próprios diretórios dedicados, o que é uma novidade desde a v3 (então, para v3, cada um deles seria colocado em seus respectivos diretórios dedicados, em vez da raiz do vault).

Alguns dos arquivos de assinatura, módulos, e listas de bloqueio disponíveis publicamente para versões principais anteriores foram obsoletos, portanto, nem tudo estará disponível para v3. Na maioria dos casos, eles não serão necessários de qualquer maneira, devido aos novos recursos e funcionalidades principais adicionados desde a v3.

Há algumas mudanças sutis na forma como as regras auxiliares são estruturadas, e há mudanças na configuração, mas se você usar o recurso de importação/exportação na página de backup do front-end, não precisará reescrever, ajustar, ou recriar qualquer coisa. Ao importar, o CIDRAM sabe o que é necessário e cuidará disso para você automaticamente.

#### 10.1 CIDRAM v4

CIDRAM v4 ainda não existe. Mas, quando chegar a hora de atualizar de v3 para v4, o processo de atualização deve ser muito mais simples. Não saberemos exatamente o quão significativamente diferente será até chegar a hora, mas prevejo que as diferenças serão muito menores do que antes, e os mecanismos já foram implementados na v3 desde o início para facilitar um processo de atualização mais suave. Supondo que não haja mudanças significativas no atualizador ou na forma como os pontos de entrada funcionam, deveria, em teoria, ser possível atualizar totalmente pelo front-end, sem a necessidade de realizar uma nova instalação.

Informações mais detalhadas serão incluídas aqui, na documentação, em um momento apropriado no futuro.

---


Última Atualização: 3 de Julho de 2024 (2024.07.03).
