## Documentação para CIDRAM v3 (Português).

### Conteúdo
- 1. [PREÂMBULO](#SECTION1)
- 2. [COMO INSTALAR](#SECTION2)
- 3. [COMO USAR](#SECTION3)
- 4. [GESTÃO DE FRONT-END](#SECTION4)
- 5. [ARQUIVOS INCLUÍDOS NESTE PACOTE](#SECTION5)
- 6. [OPÇÕES DE CONFIGURAÇÃO](#SECTION6)
- 7. [FORMATO DE ASSINATURAS](#SECTION7)
- 8. [PROBLEMAS DE COMPATIBILIDADE CONHECIDOS](#SECTION8)
- 9. [PERGUNTAS MAIS FREQUENTES (FAQ)](#SECTION9)
- 10. *Reservado para futuras adições à documentação.*
- 11. [INFORMAÇÃO LEGAL](#SECTION11)

*Nota relativa às traduções: Em caso de erros (por exemplo, discrepâncias entre as traduções, erros de digitação, etc), a versão em inglês do README é considerada a versão original e autorizada. Se você encontrar algum erro, a sua ajuda em corrigi-los seria bem-vinda.*

---


### 1. <a name="SECTION1"></a>PREÂMBULO

CIDRAM (Classless Inter-Domain Routing Access Manager) é um script PHP projetados para proteger sites por bloqueando solicitações provenientes de endereços IP considerado como sendo fontes de tráfego indesejável, incluindo (mas não limitado a) o tráfego dos pontos de acesso não-humanos, serviços em nuvem, spambots, raspadores/scrapers, etc. Ele faz isso via calculando as possíveis CIDRs dos endereços IP fornecida a partir de solicitações de entrada e em seguida tentando comparar estas possíveis CIDRs contra os seus arquivos de assinaturas (estas arquivos de assinaturas contêm listas de CIDRs de endereços IP considerado como sendo fontes de tráfego indesejável); Se forem encontradas correspondências, as solicitações estão bloqueadas.

*(Vejo: [O que é um "CIDR"?](#WHAT_IS_A_CIDR)).*

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

1) Por o seu lendo isso, eu estou supondo que você já tenha baixado uma cópia arquivada do script, descomprimido seu conteúdo e tê-lo sentado em algum lugar em sua máquina local. A partir daqui, você vai querer determinar onde no seu host ou CMS pretende colocar esses conteúdos. Um diretório como `/public_html/cidram/` ou semelhante (porém, está não importa qual você escolher, assumindo que é seguro e algo você esteja feliz com) vai bastará.

2) Renomear `config.ini.RenameMe` para `config.ini` (localizado dentro `vault`), e opcionalmente (fortemente recomendado para avançados usuários, mas não recomendado para iniciantes ou para os inexperientes), abri-lo (este arquivo contém todas as directivas disponíveis para CIDRAM; acima de cada opção deve ser um breve comentário descrevendo o que faz e para que serve). Ajuste essas opções de como você vê o ajuste, conforme o que for apropriado para sua configuração específica. Salve o arquivo, fechar.

3) Carregar os conteúdos (CIDRAM e seus arquivos) para o diretório que você tinha decidido anteriormente (você não requerer os `*.txt`/`*.md` arquivos incluídos, mas principalmente, você deve carregar tudo).

4) CHMOD o `vault` diretório para "755" (se houver problemas, você pode tentar "777"; isto é menos seguro, embora). O principal diretório armazenar o conteúdo (o que você escolheu anteriormente), geralmente, pode ser deixado sozinho, mas o CHMOD status deve ser verificado se você já teve problemas de permissões no passado no seu sistema (por padrão, deve ser algo como "755"). Em resumo: Para o pacote funcionar corretamente, o PHP precisa ser capaz de ler e gravar arquivos dentro do diretório `vault`. Muitas coisas (atualização, registro, etc) não serão possíveis, se o PHP não puder gravar no diretório `vault`, e o pacote não funcionará se o PHP não puder ler o diretório `vault`. No entanto, para uma segurança ideal, o diretório `vault` NÃO deve ser publicamente acessível (informações confidenciais, como as informações contidas em `config.ini` ou `frontend.dat`, podem ser expostas a atacantes em potencial se o diretório `vault` estiver publicamente acessível).

5) Seguida, você vai precisar "enganchar" CIDRAM ao seu sistema ou CMS. Existem várias diferentes maneiras em que você pode "enganchar" scripts como CIDRAM ao seu sistema ou CMS, mas o mais fácil é simplesmente incluir o script no início de um núcleo arquivo de seu sistema ou CMS (uma que vai geralmente sempre ser carregado quando alguém acessa qualquer página através de seu site) utilizando um `require` ou `include` comando. Normalmente, isso vai ser algo armazenado em um diretório como `/includes`, `/assets` ou `/functions`, e muitas vezes, ser nomeado algo como `init.php`, `common_functions.php`, `functions.php` ou semelhante. Você precisará determinar qual arquivo isso é para a sua situação; Se você encontrar dificuldades em determinar isso por si mesmo, para assistência, visite a página de issues CIDRAM no GitHub. Para fazer isso [usar `require` ou `include`], insira a seguinte linha de código para o início desse núcleo arquivo, substituindo a string contida dentro das aspas com o exato endereço do `loader.php` arquivo (endereço local, não o endereço HTTP; será semelhante ao vault endereço mencionado anteriormente).

`<?php require '/user_name/public_html/cidram/loader.php'; ?>`

Salve o arquivo, fechar, recarregar-lo.

-- OU ALTERNATIVAMENTE --

Se você é usando um Apache web servidor e se você tem acesso a `php.ini`, você pode usar o `auto_prepend_file` directiva para pré-carga CIDRAM sempre que qualquer solicitação para PHP é feito. Algo como:

`auto_prepend_file = "/user_name/public_html/cidram/loader.php"`

Ou isso no `.htaccess` arquivo:

`php_value auto_prepend_file "/user_name/public_html/cidram/loader.php"`

6) Isso é tudo! :-)

#### 2.1 INSTALANDO COM COMPOSER

[CIDRAM está registrado no Packagist](https://packagist.org/packages/cidram/cidram), e então, se você estiver familiarizado com o Composer, poderá usar o Composer para instalar o CIDRAM (você ainda precisará preparar a configuração, permissões e ganchos embora; consulte "instalando manualmente" as etapas 2, 4, e 5).

`composer require cidram/cidram`

#### 2.2 INSTALANDO PARA WORDPRESS

Se você quiser usar o CIDRAM com o WordPress, você pode ignorar todas as instruções acima. [CIDRAM está registrado como um plugin com o banco de dados de plugins do WordPress](https://wordpress.org/plugins/cidram/), e você pode instalar CIDRAM diretamente do painel de plugins. Você pode instalá-lo da mesma maneira que qualquer outro plugin, e nenhuma etapa de adição é necessária. Assim como com os outros métodos de instalação, você pode personalizar sua instalação por meio de modificando o conteúdo do `config.ini` arquivo ou usando o front-end página de atualizações. Se você ativar o front-end e atualizar CIDRAM usando a página de atualizações, isso será sincronizado automaticamente com as informações de versão do plugin exibidas no painel de plugins.

*Atenção: A atualização do CIDRAM através do painel de plugins resulta numa instalação limpa! Se você personalizou sua instalação (mudou sua configuração, instalados módulos, etc), estas personalizações serão perdidas quando atualizando através do painel de plugins! Os arquivos de log também serão perdidos ao atualizar através do painel de plugins! Para preservar arquivos de log e personalizações, atualize através da página de atualizações de front-end do CIDRAM.*

---


### 3. <a name="SECTION3"></a>COMO USAR

CIDRAM deve bloquear automaticamente as solicitações indesejáveis para o seu site sem necessidade de qualquer assistência manual, Além de sua instalação inicial.

Você pode personalizar a sua configuração e personalizar quais CIDRs são bloqueados por modificando seu arquivo de configuração e/ou seus arquivos de assinaturas.

Se você encontrar quaisquer falsos positivos, entre em contato comigo para me informar sobre isso. *(Vejo: [O que é um "falso positivo"?](#WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM pode ser atualizado manualmente ou através do front-end. CIDRAM também pode ser atualizado via Composer ou WordPress, se originalmente instalado por esses meios.

---


### 4. <a name="SECTION4"></a>GESTÃO DE FRONT-END

#### 4.0 O QUE É O FRONT-END.

O front-end fornece uma maneira conveniente e fácil de manter, gerenciar e atualizar sua instalação CIDRAM. Você pode visualizar, compartilhar e baixar arquivos de log através da página de logs, você pode modificar a configuração através da página de configuração, você pode instalar e desinstalar componentes através da página de atualizações, e você pode carregar, baixar e modificar arquivos no seu vault através do gerenciador de arquivos.

O front-end é desativado por padrão para evitar acesso não autorizado (acesso não autorizado pode ter consequências significativas para o seu site e para a sua segurança). Instruções para habilitá-lo estão incluídas abaixo deste parágrafo.

#### 4.1 COMO HABILITAR O FRONT-END.

1) Localize a directiva `disable_frontend` dentro `config.ini`, e defini-lo como `false` (ele será `true` por padrão).

2) Acesse o `loader.php` do seu navegador (p.e., `http://localhost/cidram/loader.php`).

3) Faça login com o nome de usuário e a senha padrão (admin/password).

Nota: Depois de efetuar login pela primeira vez, a fim de impedir o acesso não autorizado ao front-end, você deve imediatamente alterar seu nome de usuário e senha! Isto é muito importante, porque é possível fazer upload de código PHP arbitrário para o seu site através do front-end.

Além disso, para uma segurança ideal, é recomendável ativar a "autenticação de dois fatores" para todas as contas front-end (instruções fornecidas abaixo).

#### 4.2 COMO USAR O FRONT-END.

As instruções são fornecidas em cada página do front-end, para explicar a maneira correta de usá-lo e sua finalidade pretendida. Se precisar de mais explicações ou qualquer assistência especial, entre em contato com o suporte. Alternativamente, existem alguns vídeos disponíveis no YouTube que podem ajudar por meio de demonstração.

#### 4.3 AUTENTICAÇÃO DE DOIS FATORES

É possível tornar o front-end mais seguro ativando a autenticação de dois fatores ("2FA"). Ao fazer login numa conta ativada para 2FA, um e-mail é enviado para o endereço de e-mail associado a essa conta. Este e-mail contém um "código 2FA", que o usuário deve inserir, além do nome de usuário e da senha, para poder fazer login usando essa conta. Isso significa que a obtenção de uma senha de conta não seria suficiente para que qualquer hacker ou atacante em potencial pudesse fazer login nessa conta, já que eles também precisam ter acesso ao endereço de e-mail associado a essa conta para poder receber e utilizar o código 2FA associado à sessão, assim tornando assim o front-end mais seguro.

Em primeiro lugar, para ativar a autenticação de dois fatores, usando a página de atualizações do front-end, instale o componente PHPMailer. O CIDRAM utiliza o PHPMailer para enviar e-mails. Deve-se notar que embora o CIDRAM, por si só, seja compatível com PHP >= 5.4.0, o PHPMailer requer PHP >= 5.5.0, significando, portanto, que ativando a autenticação de dois fatores para o front-end do CIDRAM não será possível para usuários do PHP 5.4.

Depois de instalar o PHPMailer, você precisará preencher as diretivas de configuração do PHPMailer por meio da página de configuração para CIDRAM ou do arquivo de configuração. Mais informações sobre essas diretivas de configuração estão incluídas na seção de configuração deste documento. Depois de preencher as diretivas de configuração do PHPMailer, defina `enable_two_factor` para `true`. A autenticação de dois fatores agora deve estar ativada.

Em seguida, você precisará associar um endereço de e-mail a uma conta para que o CIDRAM saiba para onde enviar códigos 2FA ao fazer login com essa conta. Para fazer isso, use o endereço de e-mail como o nome de usuário da conta (como `foo@bar.tld`), ou incluir o endereço de e-mail como parte do nome de usuário da mesma forma que você faria ao enviar um e-mail normalmente (como `Foo Bar <foo@bar.tld>`).

Nota: Proteger seu vault contra acesso não autorizado (p.e., por meio de endurecendo as permissões de segurança e de acesso público do seu servidor), é particularmente importante aqui, devido a esse acesso não autorizado ao seu arquivo de configuração (que é armazenado no seu vault), pode arriscar expor suas configurações de SMTP (incluindo nome de usuário e senha SMTP). Você deve garantir que seu vault esteja adequadamente protegido antes de ativar a autenticação de dois fatores. Se você não conseguir fazer isso, então, pelo menos, você deve criar uma nova conta de e-mail, dedicada para essa finalidade, a fim de reduzir os riscos associados às configurações SMTP expostas.

---


### 5. <a name="SECTION5"></a>ARQUIVOS INCLUÍDOS NESTE PACOTE

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


### 6. <a name="SECTION6"></a>OPÇÕES DE CONFIGURAÇÃO

O seguinte é uma lista de variáveis encontradas no `config.ini` arquivo de configuração para CIDRAM, juntamente com uma descrição de sua propósito e função.

```
Configuration (v2)
├───general
│       logfile
│       logfile_apache (v1: logfileApache)
│       logfile_serialized (v1: logfileSerialized)
│       error_log
│       error_log_stages
│       truncate
│       log_rotation_limit
│       log_rotation_action
│       timezone
│       time_offset (v1: timeOffset)
│       time_format (v1: timeFormat)
│       ipaddr
│       forbid_on_block
│       silent_mode
│       lang
│       lang_override
│       numbers
│       emailaddr
│       emailaddr_display_style
│       † (v1: disable_cli)
│       disable_frontend
│       max_login_attempts
│       frontend_log (v1: FrontEndLog)
│       signatures_update_event_log
│       ban_override
│       log_banned_ips
│       default_dns
│       search_engine_verification
│       social_media_verification
│       other_verification
│       protect_frontend
│       maintenance_mode
│       default_algo
│       statistics
│       force_hostname_lookup
│       allow_gethostbyaddr_lookup
│       hide_version
│       empty_fields
│       log_sanitisation
│       disabled_channels
│       default_timeout
│       config_imports
│       events
├───signatures
│       ipv4
│       ipv6
│       block_attacks
│       block_cloud
│       block_bogons
│       block_generic
│       block_legal
│       block_malware
│       block_proxies
│       block_spam
│       modules
│       default_tracktime
│       infraction_limit
│       track_mode
│       tracking_override
├───recaptcha
│       usemode
│       lockip
│       lockuser
│       sitekey
│       secret
│       expiry
│       logfile
│       signature_limit
│       api
│       show_cookie_warning
│       show_api_message
│       nonblocked_status_code
├───hcaptcha
│       usemode
│       lockip
│       lockuser
│       sitekey
│       secret
│       expiry
│       logfile
│       signature_limit
│       api
│       show_cookie_warning
│       show_api_message
│       nonblocked_status_code
├───legal
│       pseudonymise_ip_addresses
│       omit_ip
│       omit_hostname
│       omit_ua
│       privacy_policy
├───template_data
│       theme
│       magnification (v1: Magnification)
│       css_url
├───PHPMailer
│       event_log (v1: EventLog)
│       skip_auth_process (v1: SkipAuthProcess)
│       enable_two_factor (v1: Enable2FA)
│       host (v1: Host)
│       port (v1: Port)
│       smtp_secure (v1: SMTPSecure)
│       smtp_auth (v1: SMTPAuth)
│       username (v1: Username)
│       password (v1: Password)
│       set_from_address (v1: setFromAddress)
│       set_from_name (v1: setFromName)
│       add_reply_to_address (v1: addReplyToAddress)
│       add_reply_to_name (v1: addReplyToName)
├───rate_limiting
│       max_bandwidth
│       max_requests
│       precision_ipv4
│       precision_ipv6
│       allowance_period
│       exceptions
└───supplementary_cache_options
        prefix
        enable_apcu
        enable_memcached
        enable_redis
        enable_pdo
        memcached_host
        memcached_port
        redis_host
        redis_port
        redis_timeout
        pdo_dsn
        pdo_username
        pdo_password
```

#### "general" (Categoria)
Configuração geral por CIDRAM.

##### "logfile"
- Um arquivo legível por humanos para registrar todas as tentativas de acesso bloqueadas. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

##### "logfile_apache"
- *v1: "logfileApache"*
- Um arquivo no estilo da Apache para registrar todas as tentativas de acesso bloqueadas. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

##### "logfile_serialized"
- *v1: "logfileSerialized"*
- Um arquivo serializado para registrar todas as tentativas de acesso bloqueadas. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

*Dica útil: Se você quiser, você pode acrescentar informações tempo/hora aos nomes dos seus arquivos de registro através incluir estas em nome: `{yyyy}` para o ano completo, `{yy}` para o ano abreviado, `{mm}` por mês, `{dd}` por dia, `{hh}` por hora.*

*Exemplos:*
- *`logfile='logfile.{yyyy}-{mm}-{dd}-{hh}.txt'`*
- *`logfile_apache='access.{yyyy}-{mm}-{dd}-{hh}.txt'`*
- *`logfile_serialized='serial.{yyyy}-{mm}-{dd}-{hh}.txt'`*

##### "error_log"
- Um arquivo para registrar erros detectados que não são fatais. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

##### "error_log_stages"
- Uma lista dos estágios na cadeia de execução que devem ter quaisquer erros gerados registrados.
- *Padrão: "Tests,Modules,SearchEngineVerification,SocialMediaVerification,OtherVerification,Aux,Reporting,Tracking,RL,CAPTCHA,Statistics,Webhooks,Output,NonBlockedCAPTCHA"*

##### "truncate"
- Truncar arquivos de log quando atingem um determinado tamanho? Valor é o tamanho máximo em B/KB/MB/GB/TB que um arquivo de log pode crescer antes de ser truncado. O valor padrão de 0KB desativa o truncamento (arquivos de log podem crescer indefinidamente). Nota: Aplica-se a arquivos de log individuais! O tamanho dos arquivos de log não é considerado coletivamente.

##### "log_rotation_limit"
- A rotação de log limita o número de arquivos de log que devem existir a qualquer momento. Quando novos arquivos de log são criados, se o número total de arquivos de log exceder o limite especificado, a ação especificada será executada. Você pode especificar o limite desejado aqui. Um valor de 0 desativará a rotação de log.

##### "log_rotation_action"
- A rotação de log limita o número de arquivos de log que devem existir a qualquer momento. Quando novos arquivos de log são criados, se o número total de arquivos de log exceder o limite especificado, a ação especificada será executada. Você pode especificar a ação desejada aqui. Delete = Deletar os arquivos de log mais antigos, até o limite não seja mais excedido. Archive = Primeiramente arquivar, e então deletar os arquivos de log mais antigos, até o limite não seja mais excedido.

*Esclarecimento técnico: Neste contexto, "mais antigo" significa modificado menos recentemente.*

##### "timezone"
- Isso é usado para especificar qual fuso horário o CIDRAM deve usar para operações de data/hora. Se você não precisa disso, ignore. Valores possíveis são determinados pelo PHP. É geralmente recomendado no lugar para ajustar a directiva fuso horário no seu arquivo `php.ini`, mas às vezes (tais como quando se trabalha com provedores de hospedagem compartilhada e limitados) isto não é sempre possível fazer, e então, esta opção é fornecido aqui.

##### "time_offset"
- *v1: "timeOffset"*
- Se o tempo do servidor não coincide com sua hora local, você pode especificar aqui um offset para ajustar as informações de data/tempo gerado por CIDRAM de acordo com as suas necessidades. É geralmente recomendado no lugar para ajustar a directiva fuso horário no seu arquivo `php.ini`, mas às vezes (tais como quando se trabalha com provedores de hospedagem compartilhada e limitados) isto não é sempre possível fazer, e então, esta opção é fornecido aqui. Offset é em minutos.
- Exemplo (para adicionar uma hora): `time_offset=60`

##### "time_format"
- *v1: "timeFormat"*
- O formato de notação de data/tempo utilizado pelo CIDRAM. Padrão = `{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss} {tz}`.

##### "ipaddr"
- Onde encontrar o IP endereço das solicitações? (Útil por serviços como o Cloudflare e tal). Padrão = REMOTE_ADDR. ATENÇÃO: Não mude isso a menos que você saiba o que está fazendo!

Valores recomendados para "ipaddr":

Valor | Usando
---|---
`HTTP_INCAP_CLIENT_IP` | Proxy reverso Incapsula.
`HTTP_CF_CONNECTING_IP` | Proxy reverso Cloudflare.
`CF-Connecting-IP` | Proxy reverso Cloudflare (alternativa; se o acima não funcionar).
`HTTP_X_FORWARDED_FOR` | Proxy reverso Cloudbric.
`X-Forwarded-For` | [Proxy reverso Squid](http://www.squid-cache.org/Doc/config/forwarded_for/).
*Definido pela configuração do servidor.* | [Proxy reverso Nginx](https://www.nginx.com/resources/admin-guide/reverse-proxy/).
`REMOTE_ADDR` | Nenhum proxy reverso (valor padrão).

##### "forbid_on_block"
- Qual mensagem de status HTTP deve enviar o CIDRAM ao bloquear solicitações?

Valores atualmente suportados:

Código de status | Mensagem de status | Descrição
---|---|---
`200` | `200 OK` | Valor padrão. Menos robusto, mas mais amigável para os usuários.
`403` | `403 Forbidden` | Um pouco mais robusto, mas um pouco menos amigável para os usuários.
`410` | `410 Gone` | Pode causar problemas ao tentar resolver falsos positivos, pois alguns navegadores armazenam em cache essa mensagem de status e não enviam solicitações subsequentes, mesmo depois de desbloquear os usuários. Pode ser mais útil do que outras opções para reduzir solicitações de certos, muito específicos tipos de bots.
`418` | `418 I'm a teapot` | Na verdade, faz referência a uma piada do primeiro de abril [[RFC 2324](https://tools.ietf.org/html/rfc2324#section-6.5.14)] e é improvável que seja entendida pelo cliente. Fornecido por diversão e conveniência, mas geralmente não é recomendado.
`451` | `Unavailable For Legal Reasons` | Apropriado para contextos em que as solicitações são bloqueadas principalmente por motivos legais. Não recomendado em outros contextos.
`503` | `Service Unavailable` | Mais robusto, mas menos amigável para os usuários.

##### "silent_mode"
- Deve CIDRAM silenciosamente redirecionar as tentativas de acesso bloqueadas em vez de exibir o "Acesso Negado" página? Se sim, especificar o local para redirecionar as tentativas de acesso bloqueadas para. Se não, deixe esta variável em branco.

##### "lang"
- Especificar o padrão da linguagem por CIDRAM.

##### "lang_override"
- Localizar de acordo com HTTP_ACCEPT_LANGUAGE sempre que possível? True = Sim [Padrão]; False = Não.

##### "numbers"
- Especifica como exibir números.

Valores atualmente suportados:

Valor | Produz | Descrição
---|---|---
`NoSep-1` | `1234567.89`
`NoSep-2` | `1234567,89`
`Latin-1` | `1,234,567.89` | Valor padrão.
`Latin-2` | `1 234 567.89`
`Latin-3` | `1.234.567,89`
`Latin-4` | `1 234 567,89`
`Latin-5` | `1,234,567·89`
`China-1` | `123,4567.89`
`India-1` | `12,34,567.89`
`India-2` | `१२,३४,५६७.८९`
`India-3` | `૧૨,૩૪,૫૬૭.૮૯`
`India-4` | `੧੨,੩੪,੫੬੭.੮੯`
`India-5` | `೧೨,೩೪,೫೬೭.೮೯`
`India-6` | `౧౨,౩౪,౫౬౭.౮౯`
`Arabic-1` | `١٢٣٤٥٦٧٫٨٩`
`Arabic-2` | `١٬٢٣٤٬٥٦٧٫٨٩`
`Arabic-3` | `۱٬۲۳۴٬۵۶۷٫۸۹`
`Arabic-4` | `۱۲٬۳۴٬۵۶۷٫۸۹`
`Bengali-1` | `১২,৩৪,৫৬৭.৮৯`
`Burmese-1` | `၁၂၃၄၅၆၇.၈၉`
`Khmer-1` | `១.២៣៤.៥៦៧,៨៩`
`Lao-1` | `໑໒໓໔໕໖໗.໘໙`
`Thai-1` | `๑,๒๓๔,๕๖๗.๘๙`
`Thai-2` | `๑๒๓๔๕๖๗.๘๙`

*Nota: Esses valores não são padronizados em nenhum lugar, e provavelmente não serão relevantes além do pacote. Adicionalmente, os valores suportados podem mudar no futuro.*

##### "emailaddr"
- Se você desejar, você pode fornecer um endereço de e-mail aqui a ser dado para os usuários quando eles estão bloqueadas, para eles para usar como um ponto de contato para suporte e/ou assistência no caso de eles sendo bloqueado por engano ou em erro. AVISO: Qualquer endereço de e-mail que você fornecer aqui certamente vai ser adquirido por spambots e raspadores/scrapers durante o curso de seu ser usada aqui, e assim, é fortemente recomendado que, se você optar por fornecer um endereço de e-mail aqui, que você garantir que o endereço de email você fornecer aqui é um endereço descartável e/ou um endereço que você não é importante (em outras palavras, você provavelmente não quer usar seu pessoal principal ou negócio principal endereço de e-mail).

##### "emailaddr_display_style"
- Como você prefere que o endereço de e-mail seja apresentado aos usuários? "default" = Link clicável. "noclick" = Texto não-clicável.

##### "disable_cli"
- *(Removido desde v2).*
- Desativar o modo CLI? O modo CLI é ativado por padrão, mas às vezes pode interferir com certas testes ferramentas (tal como PHPUnit, por exemplo) e outras aplicações baseadas em CLI. Se você não precisa desativar o modo CLI, você deve ignorar esta directiva. False = Ativar o modo CLI [Padrão]; True = Desativar o modo CLI.

##### "disable_frontend"
- Desativar o acesso front-end? Acesso front-end pode fazer CIDRAM mais manejável, mas também pode ser um risco de segurança potencial, também. É recomendado para gerenciar CIDRAM através do back-end, sempre que possível, mas o acesso front-end é proporcionada para quando não é possível. Mantê-lo desativado, a menos que você precisar. False = Ativar o acesso front-end; True = Desativar o acesso front-end [Padrão].

##### "max_login_attempts"
- Número máximo de tentativas de login ao front-end. Padrão = 5.

##### "frontend_log"
- *v1: "FrontEndLog"*
- Arquivo para registrar tentativas de login ao front-end. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

##### "signatures_update_event_log"
- Um arquivo para registrar quando as assinaturas são atualizadas por meio do front-end. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

##### "ban_override"
- Sobrepor "forbid_on_block" quando "infraction_limit" é excedido? Quando sobrepõe: As solicitações bloqueadas retornam uma página em branco (os arquivos de modelo não são usados). 200 = Não sobrepor [Padrão]. Outros valores são os mesmos que os valores disponíveis para "forbid_on_block".

##### "log_banned_ips"
- Incluir solicitações bloqueadas de IPs banidas nos arquivos de log? True = Sim [Padrão]; False = Não.

##### "default_dns"
- Uma lista delimitada por vírgulas de servidores DNS a serem usados para pesquisas de nomes de host. Padrão = "8.8.8.8,8.8.4.4" (Google DNS). ATENÇÃO: Não mude isso a menos que você saiba o que está fazendo!

*Veja também: [O que posso usar para "default_dns"?](#WHAT_CAN_I_USE_FOR_DEFAULT_DNS)*

##### "search_engine_verification"
- Tentativa de verificar solicitações dos motores de busca? Verificando os motores de busca garante que eles não serão banidos como resultado de exceder o limite de infrações (proibindo motores de busca de seu site normalmente terá um efeito negativo sobre o seu motor de busca ranking, SEO, etc). Quando verificado, os motores de busca podem ser bloqueados como por normal, mas não serão banidos. Quando não verificado, é possível que eles serão banidos como resultado de ultrapassar o limite de infrações. Também, a verificação dos motores de busca fornece proteção contra falsos solicitações de motores de busca e contra entidades potencialmente mal-intencionadas mascarando como motores de busca (tais solicitações serão bloqueados quando a verificação dos motores de busca estiver ativada). True = Ativar a verificação dos motores de busca [Padrão]; False = Desativar a verificação dos motores de busca.

Atualmente suportado:
- __[Applebot](https://discussions.apple.com/thread/7090135)__
- __[Baiduspider/百度](https://help.baidu.com/question?prod_en=master&class=Baiduspider)__
- __[Bingbot](https://blogs.bing.com/webmaster/2012/08/31/how-to-verify-that-bingbot-is-bingbot)__
- __[DuckDuckBot](https://duckduckgo.com/duckduckbot)__
- __[Googlebot](https://support.google.com/webmasters/answer/80553?hl=en)__
- __[MojeekBot](https://www.mojeek.com/bot.html)__
- __[PetalBot](https://aspiegel.com/petalbot)__
- __[Qwantify/Bleriot](https://help.qwant.com/bot)__
- __[SeznamBot](https://napoveda.seznam.cz/en/full-text-search/seznambot-crawler/)__
- __[Sogou/搜狗](https://www.sogou.com/docs/help/webmasters.htm#07)__
- __[Yahoo/Slurp](https://help.yahoo.com/help/us/ysearch/slurp)__
- __[Yandex/Яндекс](https://yandex.com/support/webmaster/robot-workings/check-yandex-robots.xml)__
- __[Youdao/有道](https://udger.com/resources/ua-list/bot-detail?bot=YoudaoBot#id1507)__

Não compatível (causa conflitos):
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

##### "social_media_verification"
- Tentativa de verificar solicitações de mídia social? A verificação de mídia social fornece proteção contra solicitações falsas de mídia social (essas solicitações serão bloqueadas). True = Ativar a verificação de mídia social [Padrão]; False = Desativar a verificação de mídia social.

Atualmente suportado:
- __[Embedly](https://udger.com/resources/ua-list/bot-detail?bot=Embedly#id22674)__
- __** [Facebook external hit](https://developers.facebook.com/docs/sharing/webmasters/crawler/)__
- __[Pinterest](https://help.pinterest.com/en/articles/about-pinterest-crawler-0)__
- __[Twitterbot](https://udger.com/resources/ua-list/bot-detail?bot=Twitterbot#id6168)__

_**: Requer funcionalidade de pesquisa ASN, por exemplo, do módulo BGPView._

##### "other_verification"
- Sempre que possível, tente verificar outros tipos de solicitações (por exemplo, AdSense, verificadores de SEO, etc)? Quando detectados, as solicitações falsas serão bloqueadas. True = Ativar [Padrão]; False = Desativar.

Atualmente suportado:
- __[AdSense](https://developers.google.com/search/docs/advanced/crawling/overview-google-crawlers)__
- __[AmazonAdBot](https://adbot.amazon.com/index.html)__
- __[Oracle Data Cloud Crawler](https://www.oracle.com/corporate/acquisitions/grapeshot/crawler.html)__

##### "protect_frontend"
- Especifica se as proteções normalmente fornecidas pelo CIDRAM devem ser aplicadas ao front-end. True = Sim [Padrão]; False = Não.

##### "maintenance_mode"
- Ativar o modo de manutenção? True = Sim; False = Não [Padrão]. Desativa tudo além do front-end. Às vezes útil para quando atualiza seu CMS, frameworks, etc.

##### "default_algo"
- Define qual algoritmo usar para todas as futuras senhas e sessões. Opções: PASSWORD_DEFAULT (padrão), PASSWORD_BCRYPT, PASSWORD_ARGON2I (requer PHP >= 7.2.0), PASSWORD_ARGON2ID (requer PHP >= 7.3.0).

##### "statistics"
- Monitorar as estatísticas de uso do CIDRAM? True = Sim; False = Não [Padrão].

##### "force_hostname_lookup"
- Forçar pesquisas de nome de anfitrião? True = Sim; False = Não [Padrão]. As pesquisas de nome de anfitrião normalmente são realizadas com base na necessidade, mas pode ser forçado para todos os solicitações. Isso pode ser útil como forma de fornecer informações mais detalhadas nos arquivos de log, mas também pode ter um efeito ligeiramente negativo sobre o desempenho.

##### "allow_gethostbyaddr_lookup"
- Permitir pesquisas gethostbyaddr quando o UDP não está disponível? True = Sim [Padrão]; False = Não.
- *Nota: A pesquisa do IPv6 pode não funcionar corretamente em alguns sistemas de 32-bits.*

##### "hide_version"
- Ocultar informações da versão dos logs e da saída da página? True = Sim; False = Não [Padrão].

##### "empty_fields"
- Como o CIDRAM deve manipular campos vazios ao registrar e exibir informações de eventos de bloco? "include" = Incluir campos vazios. "omit" = Omitir campos vazios [padrão].

##### "log_sanitisation"
- Ao usar o front-end página para os arquivos de registro para exibir dados de log, o CIDRAM sanitiza os dados de log antes de exibi-los, para proteger os usuários contra ataques XSS e outras ameaças potenciais que os dados de log podem conter. No entanto, por padrão, os dados não são sanitizados durante o registro. Isso é para assegurar que os dados de log sejam preservados com precisão, para auxiliar qualquer análise heurística ou forense que possa ser necessária no futuro. No entanto, no caso de um usuário tentar ler dados de log usando ferramentas externas, e se essas ferramentas externas não realizarem seu próprio processo de sanitização, o usuário pode estar exposto a ataques XSS. Se necessário, você pode alterar o comportamento padrão usando esta diretiva de configuração. True = Sanitize dados ao registrá-lo (os dados são preservados com menos precisão, mas o risco de XSS é menor). False = Não sanitize dados ao registrá-lo (os dados são preservados com mais precisão, mas o risco de XSS é maior) [Padrão].

##### "disabled_channels"
- Isso pode ser usado para impedir que o CIDRAM use canais específicos ao enviar solicitações (por exemplo, ao atualizar, ao buscar metadados de componentes, etc).
- *Opções disponíveis: `GitHub,BitBucket,GoogleDNS`*

##### "default_timeout"
- Tempo limite padrão a ser usado para solicitações externas? Padrão = 12 segundos.

##### "config_imports"
- Uma lista delimitada por vírgulas de arquivos a serem importados para a configuração padrão de CIDRAM. Normalmente preenchido pela página de atualizações ao ativar componentes que precisam dela quando necessário. Na maioria dos casos, pode ignorá-lo.

##### "events"
- Os arquivos listados aqui são carregados diretamente após o arquivo do manipuladores de eventos. Normalmente preenchido pela página de atualizações ao ativar componentes que precisam dela quando necessário. Na maioria dos casos, pode ignorá-lo.

#### "signatures" (Categoria)
Configuração por assinaturas.

##### "ipv4"
- Uma lista dos arquivos de assinaturas IPv4 que CIDRAM deve tentar usar, delimitado por vírgulas. Você pode adicionar entradas aqui Se você quiser incluir arquivos adicionais em CIDRAM.

##### "ipv6"
- Uma lista dos arquivos de assinaturas IPv6 que CIDRAM deve tentar usar, delimitado por vírgulas. Você pode adicionar entradas aqui Se você quiser incluir arquivos adicionais em CIDRAM.

##### "block_attacks"
- Bloquear CIDRs associados a ataques e outro tráfego anormal? Por exemplo, varreduras de portas, hacking, sondagem de vulnerabilidades, etc. A menos que você tiver problemas ao fazê-lo, geralmente, esta deve sempre ser definido como true.

##### "block_cloud"
- Bloquear CIDRs identificado como pertencente a webhosting e/ou serviços em nuvem? Se você operar um serviço de API a partir do seu site ou se você espera outros sites para se conectar para o seu site, este deve ser definido como false. Se não, este deve ser definido como true.

##### "block_bogons"
- Bloquear bogon/martian CIDRs? Se você espera conexões para o seu site de dentro de sua rede local, de localhost, ou de seu LAN, esta directiva deve ser definido como false. Se você não esperar que esses tais conexões, esta directiva deve ser definido como true.

##### "block_generic"
- Bloquear CIDRs geralmente recomendado para a lista negra? Isso abrange todas as assinaturas que não são marcados como sendo parte de qualquer um dos outros mais categorias de assinaturas mais específica.

##### "block_legal"
- Bloquear CIDRs em resposta a obrigações legais? Esta diretiva normalmente não deve ter qualquer efeito, porque o CIDRAM não associa nenhum CIDR com "obrigações legais" por padrão, mas existe, no entanto, como uma medida de controle adicional para o benefício de quaisquer arquivos de assinatura ou módulos personalizados que possam existir por motivos legais.

##### "block_malware"
- Bloquear CIDRs associados ao malware? Isso inclui servidores C&C, máquinas infectadas, máquinas envolvidas na distribuição de malware, etc.

##### "block_proxies"
- Bloquear CIDRs identificado como pertencente a serviços de proxy ou VPNs? Se você precisar que os usuários poderão acessar seu site dos serviços de proxy e VPNs, este deve ser definido como false. De outra forma, se você não precisa de serviços de proxy ou VPNs, este deve ser definido como true como um meio de melhorar a segurança.

##### "block_spam"
- Bloquear CIDRs identificado como sendo de alto risco para spam? A menos que você tiver problemas ao fazê-lo, geralmente, esta deve sempre ser definido como true.

##### "modules"
- Uma lista de arquivos módulo a carregar depois de processamento as assinaturas IPv4/IPv6, delimitado por vírgulas.

##### "default_tracktime"
- Quantos segundos para rastrear IPs banidos por módulos. Padrão = 604800 (1 semana).

##### "infraction_limit"
- Número máximo de infrações que um IP pode incorrer antes de ser banido por monitoração IP. Padrão = 10.

##### "track_mode"
- Quando as infrações devem ser contadas? False = Quando os IPs são bloqueados por módulos. True = Quando os IPs são bloqueados por qualquer motivo. Padrão = False.

##### "tracking_override"
- Permitir que os módulos substituem as opções de monitoração? True = Sim [Padrão]; False = Não.

#### "recaptcha" e "hcaptcha" (essas duas categorias fornecem as mesmas diretivas).
Se desejar, você pode apresentar aos usuários um desafio CAPTCHA para distingui-los dos bots ou para permitir que eles recuperem o acesso no caso de serem bloqueados. Isso pode ajudar a mitigar falsos positivos e reduzir o tráfego automatizado indesejado.

*Nota: Os CAPTCHAs protegem apenas contra chamadas de máquina, não contra atacantes humanos.*

Você pode obter uma "site key" e uma "secret key" para o reCAPTCHA aqui:
- https://developers.google.com/recaptcha/

Você pode obter uma "site key" e uma "secret key" para o hCAPTCHA aqui:
- https://www.hcaptcha.com/

##### "usemode"
- Quando o CAPTCHA deve ser oferecido? Nota: Solicitações na lista branca ou verificadas e não bloqueadas nunca precisam completar um CAPTCHA.

Valor | Descrição
--:|:--
1 | Somente quando bloqueado, dentro do limite de assinaturas, e não banido.
2 | Somente quando bloqueado, especialmente marcado para uso, dentro do limite de assinaturas, e não banido.
3 | Somente quando dentro do limite de assinaturas, e não banido (independentemente de estar bloqueado).
4 | Somente quando não está bloqueado.
5 | Somente quando não está bloqueado, ou quando especialmente marcado para uso, dentro do limite de assinaturas, e não banido.
Qualquer outro valor. | Nunca!

##### "lockip"
- Especifica se hashes deve ser ligado para IPs específicos. False = Cookies e hashes PODE ser usado por vários IPs (padrão). True = Cookies e hashes NÃO pode ser usado por vários IPs (cookies/hashes não estão ligados para IPs).
- Notar: O valor de "lockip" é ignorado quando "lockuser" é false, devido a que o mecanismo para lembrar "usuários" varia de acordo com este valor.

##### "lockuser"
- Especifica se a conclusão bem sucedida de uma instância de reCAPTCHA/hCAPTCHA deve ser ligado a usuários específicos. False = A conclusão bem sucedida de uma instância de reCAPTCHA/hCAPTCHA irá conceder acesso a todos as solicitações provenientes do mesmo IP como aquilo utilizado pelo utilizador completar a instância de reCAPTCHA/hCAPTCHA; Cookies e hashes não são usados; Em vez disso, um IP whitelist será usado. True = A conclusão bem sucedida de uma instância de reCAPTCHA/hCAPTCHA só irá conceder acesso para o usuário completar a instância de reCAPTCHA/hCAPTCHA; Cookies e hashes são usados para lembrar o usuário; Um IP whitelist não é usado (padrão).

##### "sitekey"
- Esse valor pode ser encontrado no painel de seu serviço de CAPTCHA.

##### "secret"
- Esse valor pode ser encontrado no painel de seu serviço de CAPTCHA.

##### "expiry"
- Número de horas para lembrar instâncias CAPTCHA. Padrão = 720 (1 mês).

##### "logfile"
- Registrar todas as tentativas de CAPTCHA? Se sim, especificar o nome a ser usado para o arquivo de registro. Se não, deixe esta variável em branco.

*Dica útil: Se você quiser, você pode acrescentar informações tempo/hora aos nomes dos seus arquivos de registro através incluir estas em nome: `{yyyy}` para o ano completo, `{yy}` para o ano abreviado, `{mm}` por mês, `{dd}` por dia, `{hh}` por hora.*

*Exemplos:*
- *`logfile='captcha.{yyyy}-{mm}-{dd}-{hh}.txt'`*

##### "signature_limit"
- O número máximo de assinaturas permitidas antes que o CAPTCHA seja retirado. Padrão = 1.

##### "api"
- Qual API usar?

```
api
├─recaptcha
│ ├─V2
│ └─Invisible
└─hcaptcha
  ├─V1
  └─Invisible
```

*Nota para usuários na União Européia: Quando o CIDRAM está configurado para usar cookies (por exemplo, quando "lockuser" é true/verdadeiro), um aviso de cookie é exibido de forma proeminente na página de acordo com os requisitos da [legislação comunitária sobre cookies](https://www.cookielaw.org/the-cookie-law/). Mas, ao usar a API invisible, o CIDRAM tenta completar o CAPTCHA para o usuário automaticamente, e quando bem-sucedido, isso pode resultar na recarga da página e criar um cookie sem que o usuário tenha dado tempo suficiente para realmente ver o aviso de cookie.*

##### "show_cookie_warning"
- Mostrar aviso de cookie? True = Sim [Padrão]; False = Não.

*Esta diretiva de configuração foi adicionada por solicitação, para usuários que desejam desativar o aviso de cookie geralmente mostrado ao lado de CAPTCHAs (para ajudar, por exemplo, ocultar qualquer indicação de que o CIDRAM está sendo usado). Mas, aconselho vivamente que a maioria dos utilizadores (em especial os que residem na UE) o mantenham ativado.*

##### "show_api_message"
- Mostrar mensagem API? True = Sim [Padrão]; False = Não.

*Isso se refere a quaisquer mensagens não essenciais adicionais, exibidas quando uma solicitação é bloqueada, além do aviso de cookie.*

##### "nonblocked_status_code"
- Qual código de status deve ser usado ao exibir CAPTCHAs para solicitações não bloqueadas?

Valores atualmente suportados:

Código de status | Mensagem de status
---|---
`200` | `200 OK`
`403` | `403 Forbidden`
`418` | `418 I'm a teapot`
`429` | `429 Too Many Requests`
`451` | `Unavailable For Legal Reasons`

#### "legal" (Categoria)
Configuração relacionada aos requisitos legais.

*Para obter mais informações sobre requisitos legais e como isso pode afetar seus requisitos de configuração, consulte a seção "[INFORMAÇÃO LEGAL](#SECTION11)" da documentação.*

##### "pseudonymise_ip_addresses"
- Pseudonimiza endereços IP ao escrever os arquivos de log? True = Sim [Padrão]; False = Não.

##### "omit_ip"
- Omitir endereços IP de logs? True = Sim; False = Não [Padrão]. Nota: "pseudonymise_ip_addresses" se torna redundante quando "omit_ip" é "true".

##### "omit_hostname"
- Omitir nomes de host de logs? True = Sim; False = Não [Padrão].

##### "omit_ua"
- Omitir agentes de usuários de logs? True = Sim; False = Não [Padrão].

##### "privacy_policy"
- O endereço de uma política de privacidade relevante a ser exibida no rodapé de qualquer página gerada. Especifique um URL, ou deixe em branco para desabilitar.

#### "template_data" (Categoria)
Directivas/Variáveis para modelos e temas.

Relaciona-se com a saída HTML usado para gerar a página "Acesso Negado". Se você estiver usando temas personalizados para CIDRAM, HTML é originado a partir do `template_custom.html` arquivo, e caso contrário, HTML é originado a partir do `template.html` arquivo. Variáveis escritas para esta seção do configuração arquivo são processado ao HTML via substituição de quaisquer nomes de variáveis cercado por colchetes encontrado dentro do HTML com os variáveis dados correspondentes. Por exemplo, onde `foo="bar"`, qualquer instância de `<p>{foo}</p>` encontrado dentro do HTML tornará `<p>bar</p>`.

##### "theme"
- Tema padrão a ser usado para CIDRAM.

##### "magnification"
- *v1: "Magnification"*
- Ampliação de fonte. Padrão = 1.

##### "css_url"
- O template arquivo para temas personalizados utiliza CSS propriedades externos, enquanto que o template arquivo para o padrão tema utiliza CSS propriedades internos. Para instruir CIDRAM para usar o template arquivo para temas personalizados, especificar o endereço HTTP pública do seu temas personalizados CSS arquivos usando a `css_url` variável. Se você deixar essa variável em branco, CIDRAM usará o template arquivo para o padrão tema.

#### "PHPMailer" (Categoria)
Configuração do PHPMailer.

Atualmente, o CIDRAM usa o PHPMailer apenas para autenticação de dois fatores front-end. Se você não usa o front-end, ou se você não usa a autenticação de dois fatores para o front-end, você pode ignorar essas diretivas.

##### "event_log"
- *v1: "EventLog"*
- Um arquivo para registrar todos os eventos em relação ao PHPMailer. Especifique o nome de um arquivo, ou deixe em branco para desabilitar.

##### "skip_auth_process"
- *v1: "SkipAuthProcess"*
- Definir essa diretiva como `true` instrui o PHPMailer a ignorar o processo de autenticação que normalmente ocorre ao enviar e-mail via SMTP. Isso deve ser evitado, porque ignorar esse processo pode expor o e-mail de saída a ataques MITM, mas pode ser necessário nos casos em que esse processo impedir que o PHPMailer se conecte a um servidor SMTP.

##### "enable_two_factor"
- *v1: "Enable2FA"*
- Esta diretiva determina se deve usar 2FA para contas front-end.

##### "host"
- *v1: "Host"*
- O host SMTP a ser usado para e-mail de saída.

##### "port"
- *v1: "Port"*
- O número da porta a ser usado para o e-mail de saída. Padrão = 587.

##### "smtp_secure"
- *v1: "SMTPSecure"*
- O protocolo a ser usado ao enviar e-mail via SMTP (TLS ou SSL).

##### "smtp_auth"
- *v1: "SMTPAuth"*
- Esta diretiva determina se autenticar sessões SMTP (geralmente deve ser deixado em paz).

##### "username"
- *v1: "Username"*
- O nome de usuário a ser usada ao enviar e-mail via SMTP.

##### "password"
- *v1: "Password"*
- A senha a ser usada ao enviar e-mail via SMTP.

##### "set_from_address"
- *v1: "setFromAddress"*
- O endereço do remetente a ser citado ao enviar e-mail via SMTP.

##### "set_from_name"
- *v1: "setFromName"*
- O nome do remetente a ser citado ao enviar e-mail via SMTP.

##### "add_reply_to_address"
- *v1: "addReplyToAddress"*
- O endereço de resposta a ser citado ao enviar e-mail via SMTP.

##### "add_reply_to_name"
- *v1: "addReplyToName"*
- O nome da resposta a ser citado ao enviar e-mail via SMTP.

#### "rate_limiting" (Categoria)
Diretivas de configuração opcionais para limitação de taxa.

Esse recurso foi implementado no CIDRAM porque foi solicitado por usuários suficientes para justificar a implementação. Contudo, porque está um pouco fora do escopo da finalidade originalmente pretendida para a CIDRAM, provavelmente não será necessário para a maioria dos usuários. Se você precisa especificamente do CIDRAM para lidar com a limitação de taxa do seu site, esse recurso pode ser útil para você. Contudo, existem algumas coisas importantes que você deve considerar:
- Esse recurso, como todos os outros recursos do CIDRAM, funcionará apenas para páginas protegidas pelo CIDRAM. Portanto, qualquer recurso de site não especificamente roteado através do CIDRAM não pode ser limitado pela CIDRAM.
- Se você é capaz de usar um módulo de servidor, cPanel, ou alguma outra ferramenta de rede para impor a limitação de taxa, seria melhor usar isso para limitação de taxa, em vez de CIDRAM.
- Se um usuário em particular estiver muito interessado em continuar acessando seu website depois de ser limitado, na maioria dos casos, será muito fácil para eles contornar o limitação de taxa (por exemplo, se eles mudarem seu endereço IP, ou se eles usam um proxy ou VPN, e assumindo que você configurou o CIDRAM para não bloquear proxies e VPNs, ou que o CIDRAM não está ciente do proxy ou VPN que eles estão usando).
- A limitação de taxa pode ser muito irritante para usuários reais. Pode ser necessário se a sua largura de banda disponível for muito limitada, e se você descobrir que existem algumas fontes específicas de tráfego, que ainda não estão bloqueadas, estão consumindo a maior parte de sua largura de banda disponível. Mas, se não for necessário, provavelmente deve ser evitado.
- Você pode, ocasionalmente, arriscar bloquear usuários legítimos, ou até você mesmo.

Se você acha que não precisa do CIDRAM para impor a limitação de taxas para o seu site, mantenha as diretivas abaixo definidas como valores padrão. Caso contrário, você poderá alterar seus valores para atender às suas necessidades.

##### "max_bandwidth"
- A quantidade máxima de largura de banda permitida dentro do período de tolerância antes de ativar a limitação de taxa para solicitações futuras. Um valor de 0 desativa esse tipo de limitação de taxa. Padrão = 0KB.

##### "max_requests"
- O número máximo de solicitações permitido dentro do período de tolerância antes de ativar a limitação de taxa para solicitações futuras. Um valor de 0 desativa esse tipo de limitação de taxa. Padrão = 0.

##### "precision_ipv4"
- A precisão a ser usada ao monitorar o uso do IPv4. Valor espelha o tamanho do bloco CIDR. Defina para 32 para melhor precisão. Padrão = 32.

##### "precision_ipv6"
- A precisão a ser usada ao monitorar o uso do IPv6. Valor espelha o tamanho do bloco CIDR. Defina para 128 para melhor precisão. Padrão = 128.

##### "allowance_period"
- O número de horas para monitorar o uso. Padrão = 0.

##### "exceptions"
- Exceções (ou seja, solicitações que não devem ser limitadas à taxa). Relevante apenas quando a limitação de taxa está ativada.
- *Opções disponíveis: `Whitelisted,Verified`*

#### "supplementary_cache_options" (Categoria)
Opções de cache suplementares.

##### "prefix"
- O valor especificado aqui será adicionado ao começo das chaves para todas as entradas de cache. Vazio por padrão. Quando existem várias instalações no mesmo servidor, isso pode ser útil para manter seus caches separados uns dos outros.

##### "enable_apcu"
- Especifica se deve tentar usar o APCu para armazenamento em cache. Padrão = False.

##### "enable_memcached"
- Especifica se deve tentar usar o Memcached para armazenamento em cache. Padrão = False.

##### "enable_redis"
- Especifica se deve tentar usar o Redis para armazenamento em cache. Padrão = False.

##### "enable_pdo"
- Especifica se deve tentar usar o PDO para armazenamento em cache. Padrão = False.

##### "memcached_host"
- Valor da host do Memcached. Padrão = "localhost".

##### "memcached_port"
- Valor da porta do Memcached. Padrão = "11211".

##### "redis_host"
- Valor da host do Redis. Padrão = "localhost".

##### "redis_port"
- Valor da porta do Redis. Padrão = "6379".

##### "redis_timeout"
- Valor de tempo limite do Redis. Padrão = "2.5".

##### "pdo_dsn"
- Valor DSN do PDO. Padrão = "`mysql:dbname=cidram;host=localhost;port=3306`".

*Veja também: [O que é um "PDO DSN"? Como posso usar o PDO com o CIDRAM?](#HOW_TO_USE_PDO)*

##### "pdo_username"
- O nome de usuário do PDO.

##### "pdo_password"
- A senha do PDO.

---


### 7. <a name="SECTION7"></a>FORMATO DE ASSINATURAS

*Veja também:*
- *[O que é uma "assinatura"?](#WHAT_IS_A_SIGNATURE)*

#### 7.0 NOÇÕES BÁSICAS (PARA ARQUIVOS DE ASSINATURA)

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

#### 7.1 ETIQUETAS

##### 7.1.0 ETIQUETAS DE SEÇÃO

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

Em particular, as etiquetas de seção podem ser muito úteis para depuração quando ocorrem falsos positivos, fornecendo um meio fácil de encontrar a fonte exata do problema, e pode ser muito útil para filtrar entradas de arquivos de log ao visualizar arquivos de log por meio da página de logs do front-end (os nomes das seções são clicáveis através da página de logs do front-end e podem ser usados como critérios de filtragem). Se as etiquetas de seção forem omitidas para algumas assinaturas específicas, quando essas assinaturas são desencadeadas, o CIDRAM usa o nome do arquivo de assinatura juntamente com o tipo de endereço IP bloqueado (IPv4 ou IPv6) como um retorno, e portanto, as etiquetas de seção são inteiramente opcionais. Embora, eles podem ser recomendados em alguns casos, como quando os arquivos de assinatura são nomeados vagamente ou quando pode ser difícil identificar claramente a origem das assinaturas fazendo com que um pedido seja bloqueado.

##### 7.1.1 ETIQUETAS DE EXPIRAÇÃO

Se você quiser assinaturas para expirar depois de algum tempo, de um modo semelhante para etiquetas de seção, você pode usar um "etiqueta de expiração" para especificar quando as assinaturas devem deixar de ser válida. Etiquetas de expiração usam o formato "AAAA.MM.DD" (veja o exemplo abaixo).

```
# Seção 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

As assinaturas expiradas nunca serão desencadeadas em qualquer pedido, não importa o que.

##### 7.1.2 ETIQUETAS DE ORIGEM

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

##### 7.1.3 ETIQUETAS DE DEFERÊNCIA

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

##### 7.1.4 ETIQUETAS DE PERFIL

As etiquetas de perfil fornecem um meio de exibir informações adicionais na página de teste de IP, e podem ser aproveitadas por módulos e regras auxiliares para um comportamento mais complexo e tomada de decisão ajustada.

As etiquetas de perfil são usadas de maneira semelhante a outros tipos de etiquetas. Os valores das etiquetas de perfil podem ser usados como condição para módulos e regras auxiliares. As etiquetas de perfil podem fornecer vários valores, separando esses valores com um ponto e vírgula. O usuário final nunca vê os valores das etiquetas de perfil.

Exemplo:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 7.2 YAML

##### 7.2.0 YAML BÁSICOS

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

##### 7.2.1 COMO "MARCAR ESPECIALMENTE" SEÇÕES DE ASSINATURA PARA USO COM reCAPTCHA/hCAPTCHA

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

#### 7.3 AUXILIAR

##### 7.3.0 IGNORANDO SEÇÕES DE ASSINATURA

Em suplemento, se você quiser CIDRAM para ignorar completamente algumas seções específicas dentro de qualquer um dos arquivos de assinatura, você pode usar o arquivo `ignore.dat` para especificar quais seções para ignorar. numa nova linha, escreva `Ignore`, seguido por um espaço, seguido do nome da seção que você quer CIDRAM para ignorar (veja o exemplo abaixo).

```
Ignore Seção 1
```

Isso também pode ser alcançado usando a interface fornecida pela página "lista de seções" do front-end do CIDRAM.

##### 7.3.1 REGRAS AUXILIARES

Se você acha que escrever seus próprios arquivos de assinatura personalizados ou módulos personalizados é muito complicado para você, uma alternativa mais simples pode ser usar a interface fornecida pela página "regras auxiliares" do front-end do CIDRAM. Ao selecionar as opções apropriadas e especificar detalhes sobre os tipos de solicitações específicos, você pode instruir o CIDRAM sobre como responder a essas solicitações. "Regras auxiliares" são executadas depois que todos os arquivos de assinatura e módulos já tiverem terminado a execução.

#### 7.4 <a name="MODULE_BASICS"></a>NOÇÕES BÁSICAS (PARA MÓDULOS)

Os módulos podem ser usados para ampliar a funcionalidade do CIDRAM, executar tarefas adicionais, ou processar lógica adicional. Tipicamente, eles são usados quando é necessário bloquear um pedido numa base diferente do endereço IP de origem (portanto, quando uma assinatura do CIDR não será suficiente para bloquear o pedido). Os módulos são escritos como arquivos PHP e portanto, tipicamente, as assinaturas dos módulos são escritas como código PHP.

Alguns bons exemplos de módulos do CIDRAM podem ser encontrados aqui:
- https://github.com/CIDRAM/CIDRAM-Extras/tree/master/modules

Um modelo para escrever novos módulos pode ser encontrado aqui:
- https://github.com/CIDRAM/CIDRAM-Extras/blob/master/modules/module_template.php

Devido a que os módulos são escritos como arquivos PHP, se você estiver adequadamente familiarizado com a base de códigos CIDRAM, você pode estruturar seus módulos e escreva as assinaturas do módulo, como quiser (em razão do que é possível com o PHP). Mas, para sua própria conveniência, e por uma melhor inteligibilidade mútua entre os módulos existentes e os seus próprios, é recomendável analisar o modelo acima, para poder usar a estrutura e o formato que ele fornece.

*Nota: Se você não está confortável trabalhando com o código PHP, não é recomendável escrever seus próprios módulos.*

Algumas funcionalidades são fornecidas pelo CIDRAM para os módulos a serem usados, o que deve tornar mais simples e fácil de escrever seus próprios módulos. A informação sobre esta funcionalidade é descrita abaixo.

#### 7.5 FUNCIONALIDADE DO MÓDULO

##### 7.5.0 "$Trigger"

As assinaturas do módulo geralmente são escritas com `$Trigger`. Na maioria dos casos, esse closure será mais importante do que qualquer outra coisa com a finalidade de escrever módulos.

`$Trigger` aceita 4 parâmetros: `$Condition`, `$ReasonShort`, `$ReasonLong` (opcional), e `$DefineOptions` (opcional).

A verdade de `$Condition` é avaliada, e se for true/verdade, a assinatura é "desencadeada". Se false/falso, a assinatura *não* é "desencadeada". `$Condition` tipicamente contém código PHP para avaliar uma condição que deve causar um pedido para ser bloqueado.

`$ReasonShort` é citado no campo "Razão Bloqueada" quando a assinatura é "desencadeada".

`$ReasonLong` é uma mensagem opcional a ser exibida para o usuário/cliente para quando eles estão bloqueados, para explicar por que eles foram bloqueados. Usa a mensagem padrão "Acesso Negado" quando omitido.

`$DefineOptions` é uma array opcional contendo pares de chave/valor, usada para definir opções de configuração específicas para a instância de solicitação. As opções de configuração serão aplicadas quando a assinatura é "desencadeada".

`$Trigger` retorna true/verdadeiro quando a assinatura é "desencadeada", e false/falsa quando não é.

Para usar esse closure em seu módulo, lembre-se de herdá-lo do escopo pai:
```PHP
$Trigger = $CIDRAM['Trigger'];
```

##### 7.5.1 "$Bypass"

Os bypass de assinatura geralmente são escritos com `$Bypass`.

`$Bypass` aceita 3 parâmetros: `$Condition`, `$ReasonShort`, e `$DefineOptions` (opcional).

A verdade de `$Condition` é avaliada, e se for true/verdade, o bypass é "desencadeado". Se false/falso, o bypass *não* é "desencadeado". `$Condition` tipicamente contém código PHP para avaliar uma condição *não* que deve causar um pedido para ser bloqueado.

`$ReasonShort` é citado no campo "Razão Bloqueada" quando o bypass é "desencadeado".

`$DefineOptions` é uma array opcional contendo pares de chave/valor, usada para definir opções de configuração específicas para a instância de solicitação. As opções de configuração serão aplicadas quando o bypass é "desencadeado".

`$Bypass` retorna true/verdadeiro quando o bypass é "desencadeado", e false/falsa quando não é.

Para usar esse closure em seu módulo, lembre-se de herdá-lo do escopo pai:
```PHP
$Bypass = $CIDRAM['Bypass'];
```

##### 7.5.2 "$CIDRAM['DNS-Reverse']"

Isso pode ser usado para buscar o nome do host de um endereço IP. Se você quiser criar um módulo para bloquear nomes de host, este closure pode ser útil.

Exemplo:
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

Os módulos executam dentro do seu próprio escopo, e quaisquer variáveis definidas por um módulo, não serão acessíveis a outros módulos, nem ao script pai, a menos que estejam armazenados na array `$CIDRAM` (tudo o resto é liberado após a conclusão do módulo).

Abaixo estão algumas das variáveis comuns que podem ser úteis para o seu módulo:

Variável | Descrição
----|----
`$CIDRAM['BlockInfo']['DateTime']` | A data e a hora atuais.
`$CIDRAM['BlockInfo']['IPAddr']` | O endereço IP para a pedido atual.
`$CIDRAM['BlockInfo']['ScriptIdent']` | Versão do CIDRAM.
`$CIDRAM['BlockInfo']['Query']` | A consulta para o pedido atual.
`$CIDRAM['BlockInfo']['Referrer']` | O referente para o pedido atual (se houver).
`$CIDRAM['BlockInfo']['UA']` | O agente do usuário (user agent) para o pedido atual.
`$CIDRAM['BlockInfo']['UALC']` | O agente do usuário (user agent) para o pedido atual (em minúsculas).
`$CIDRAM['BlockInfo']['ReasonMessage']` | A mensagem a ser exibida para o usuário/cliente do pedido atual se eles estiverem bloqueados.
`$CIDRAM['BlockInfo']['SignatureCount']` | O número de assinaturas desencadeadas para o pedido atual.
`$CIDRAM['BlockInfo']['Signatures']` | Informações de referência para qualquer assinatura desencadeada para o pedido atual.
`$CIDRAM['BlockInfo']['WhyReason']` | Informações de referência para qualquer assinatura desencadeada para o pedido atual.

---


### 8. <a name="SECTION8"></a>CONHECIDOS COMPATIBILIDADE PROBLEMAS

Os seguintes pacotes e produtos foram considerados incompatíveis com o CIDRAM:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

Os módulos foram disponibilizados para garantir que os seguintes pacotes e produtos sejam compatíveis com o CIDRAM:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__

*Veja também: [Gráficos de Compatibilidade](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 9. <a name="SECTION9"></a>PERGUNTAS MAIS FREQUENTES (FAQ)

- [O que é uma "assinatura"?](#WHAT_IS_A_SIGNATURE)
- [O que é um "CIDR"?](#WHAT_IS_A_CIDR)
- [O que é um "falso positivo"?](#WHAT_IS_A_FALSE_POSITIVE)
- [CIDRAM pode bloquear países inteiros?](#BLOCK_ENTIRE_COUNTRIES)
- [Com que frequência as assinaturas são atualizadas?](#SIGNATURE_UPDATE_FREQUENCY)
- [Eu encontrei um problema ao usar CIDRAM e eu não sei o que fazer sobre isso! Ajude-me!](#ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [Eu fui bloqueado pelo CIDRAM de um site que eu quero visitar! Ajude-me!](#BLOCKED_WHAT_TO_DO)
- [Eu quero usar CIDRAM (antes de v2) com uma versão PHP mais velha do que 5.4.0; Você pode ajudar?](#MINIMUM_PHP_VERSION)
- [Eu quero usar CIDRAM (v2) com uma versão PHP mais velha do que 7.2.0; Você pode ajudar?](#MINIMUM_PHP_VERSION_V2)
- [Posso usar uma única instalação do CIDRAM para proteger vários domínios?](#PROTECT_MULTIPLE_DOMAINS)
- [Eu não quero mexer com a instalação deste e fazê-lo funcionar com o meu site; Posso pagar-te para fazer tudo por mim?](#PAY_YOU_TO_DO_IT)
- [Posso contratar você ou qualquer um dos desenvolvedores deste projeto para o trabalho privado?](#HIRE_FOR_PRIVATE_WORK)
- [Preciso de modificações especializadas, customizações, etc; Você pode ajudar?](#SPECIALIST_MODIFICATIONS)
- [Eu sou um desenvolvedor, designer de site, ou programador. Posso aceitar ou oferecer trabalho relacionado a este projeto?](#ACCEPT_OR_OFFER_WORK)
- [Quero contribuir para o projeto; Posso fazer isso?](#WANT_TO_CONTRIBUTE)
- [Posso usar o cron para atualizar automaticamente?](#CRON_TO_UPDATE_AUTOMATICALLY)
- [O que são "infrações"?](#WHAT_ARE_INFRACTIONS)
- [O CIDRAM pode bloquear nomes de host?](#BLOCK_HOSTNAMES)
- [O que posso usar para "default_dns"?](#WHAT_CAN_I_USE_FOR_DEFAULT_DNS)
- [Posso usar o CIDRAM para proteger outras coisas além de sites (por exemplo, servidores de e-mail, FTP, SSH, IRC, etc)?](#PROTECT_OTHER_THINGS)
- [Ocorrerão problemas se eu usar o CIDRAM ao mesmo tempo que usando CDNs ou serviços de cache?](#CDN_CACHING_PROBLEMS)
- [A CIDRAM protegerá meu site contra ataques DDoS?](#DDOS_ATTACKS)
- [Quando eu ativar ou desativar os módulos ou os arquivos de assinatura através da página de atualizações, eles os classificam alfanumericamente na configuração. Posso mudar a maneira como eles são classificados?](#CHANGE_COMPONENT_SORT_ORDER)
- [O que é um "PDO DSN"? Como posso usar o PDO com o CIDRAM?](#HOW_TO_USE_PDO)
- [CIDRAM está bloqueando cronjobs; Como consertar isto?](#BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>O que é uma "assinatura"?

No contexto do CIDRAM, uma "assinatura" refere-se a dados que actuam como um indicador/identificador para algo específico que estamos procurando, geralmente um endereço IP ou CIDR, e inclui algumas instruções para CIDRAM, dizendo-lhe a melhor maneira de responder quando encontrar o que estamos procurando. Uma assinatura típica para o CIDRAM é algo como isto:

Para "arquivos de assinatura":

`1.2.3.4/32 Deny Generic`

Para "módulos":

```PHP
$Trigger(strpos($CIDRAM['BlockInfo']['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
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

#### <a name="MINIMUM_PHP_VERSION"></a>Eu quero usar CIDRAM (antes de v2) com uma versão PHP mais velha do que 5.4.0; Você pode ajudar?

Não. PHP >= 5.4.0 é um requisito mínimo para CIDRAM < v2.

#### <a name="MINIMUM_PHP_VERSION_V2"></a>Eu quero usar CIDRAM (v2) com uma versão PHP mais velha do que 7.2.0; Você pode ajudar?

Não. PHP >= 7.2.0 é um requisito mínimo para CIDRAM v2.

*Veja também: [Gráficos de Compatibilidade](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>Posso usar uma única instalação do CIDRAM para proteger vários domínios?

Sim. As instalações do CIDRAM não estão naturalmente atado com domínios específicos, e pode, portanto, ser usado para proteger vários domínios. Geralmente, referimo-nos a instalações do CIDRAM que protegem apenas um domínio como "instalações de singular-domínio", e referimo-nos a instalações do CIDRAM que protegem vários domínios e/ou subdomínios como "instalações multi-domínio". Se você operar uma instalação multi-domínio e precisa usar conjuntos diferentes de arquivos de assinaturas para domínios diferentes, ou precisam CIDRAM para ser configurado de forma diferente para domínios diferentes, é possível fazer isso. Depois de carregar o arquivo de configuração (`config.ini`), o CIDRAM verificará a existência de um "arquivo de sobreposição para a configuração" específico para o domínio (ou subdomínio) que está sendo solicitado (`o-domínio-que-está-sendo-solicitado.tld.config.ini`), e se encontrado, quaisquer valores de configuração definidos pelo arquivo de sobreposição para a configuração serão usados para a instância de execução em vez dos valores de configuração definidos pelo arquivo de configuração. Os arquivos de sobreposição para a configuração são idênticos ao arquivo de configuração, e a seu critério, pode conter a totalidade de todas as diretivas de configuração disponíveis para o CIDRAM, ou qualquer subseção menor necessária que difere dos valores normalmente definidos pelo arquivo de configuração. Os arquivos de sobreposição para a configuração são nomeados de acordo com o domínio que eles são destinados para (por exemplo, se você precisar de um arquivo de sobreposição para a configuração para o domínio, `https://www.some-domain.tld/`, o seu arquivo de sobreposição para a configuração deve ser nomeado como `some-domain.tld.config.ini`, e deve ser colocado dentro da vault ao lado do arquivo de configuração, `config.ini`). O nome de domínio para a instância de execução é derivado do cabeçalho `HTTP_HOST` do pedido; "www" é ignorado.

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

"Infrações" determinam quando um IP que ainda não está bloqueado por qualquer arquivo de assinatura específico deve começar a ser bloqueado para quaisquer solicitações futuros, e estão intimamente associados ao monitoração IP. Existem algumas funcionalidades e módulos que permitem que os solicitações sejam bloqueados por motivos diferentes do IP de origem (tais como a presença de agentes de usuários [user agents] correspondentes a spambots ou hacktools, solicitações perigosas, DNS falsificado e assim por diante), e quando isso acontece, uma "infração" pode ocorrer. Eles fornecem uma maneira de identificar endereços IP que correspondem a solicitações indesejadas que podem ainda não ser bloqueadas por arquivos de assinatura específicos. Infrações geralmente correspondem 1-a-1 com o número de vezes que um IP está bloqueado, mas nem sempre (eventos de bloqueio severo podem ter um valor de infração maior do que um, e se "track_mode" for false, infrações não ocorrerão para eventos de bloco desencadeados exclusivamente por arquivos de assinatura).

#### <a name="BLOCK_HOSTNAMES"></a>O CIDRAM pode bloquear nomes de host?

Sim. Para fazer isso, você precisará criar um arquivo de módulo personalizado. *Vejo: [NOÇÕES BÁSICAS (PARA MÓDULOS)](#MODULE_BASICS)*.

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

`file1.php,file2.php,file3.php,file4.php,file5.php`

Se você queria `file3.php` para executar primeiro, você poderia adicionar algo como `aaa:` antes do nome do arquivo:

`file1.php,file2.php,aaa:file3.php,file4.php,file5.php`

Então, se um novo arquivo, `file6.php`, estiver ativado, quando a página de atualizações classifica os novamente, ele deve terminar assim:

`aaa:file3.php,file1.php,file2.php,file4.php,file5.php,file6.php`

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

Se você tentou todas essas idéias e nenhuma delas funcionou para você, ou se precisar de ajuda para descobrir como fazê-lo, você pode criar um novo issue na página de issues do CIDRAM para solicitar ajuda.

---


### 11. <a name="SECTION11"></a>INFORMAÇÃO LEGAL

#### 11.0 PREÂMBULO DE SEÇÃO

Esta seção da documentação destina-se a descrever possíveis considerações legais em relação ao uso e implementação do pacote, e fornecer algumas informações básicas relacionadas. Isso pode ser importante para alguns usuários como um meio de garantir a conformidade com quaisquer requisitos legais que possam existir nos países nos quais eles operam, e alguns usuários podem precisar ajustar as políticas do site de acordo com essas informações.

Em primeiro lugar por favor, perceba que eu (o autor do pacote) não sou advogado, nem profissional legal qualificado de qualquer tipo. Portanto, não estou legalmente qualificado para fornecer aconselhamento jurídico. Além disso, em alguns casos, exigências legais exatas podem variar entre diferentes países e jurisdições, e estes requisitos legais variados podem, às vezes, conflitar (como, por exemplo, no caso de países que defendem os [direitos de privacidade](https://pt.wikipedia.org/wiki/Direito_%C3%A0_privacidade) e o [direito de ser esquecido](https://pt.wikipedia.org/wiki/Direito_ao_esquecimento), versus países que favorecem a retenção prolongada de dados). Considere também que o acesso ao pacote não está restrito a países ou jurisdições específicos e, portanto, o pacote userbase é provável que seja geograficamente diverso. Estes pontos considerados, eu não estou em posição de afirmar o que significa ser "legalmente compatível" para todos os usuários, em todos os aspectos. No entanto, espero que as informações aqui contidas o ajudem a chegar a uma decisão sobre o que você deve fazer para permanecer legalmente conforme no contexto do pacote. Se tiver alguma dúvida ou preocupação em relação às informações aqui contidas, ou se você precisar de ajuda e conselhos adicionais de uma perspectiva legal, eu recomendaria consultar um profissional legal qualificado.

#### 11.1 RESPONSABILIDADE

Conforme já declarado pela licença do pacote, o pacote é fornecido sem qualquer garantia. Isso inclui (mas não está limitado a) todo o escopo de responsabilidade. O pacote é fornecido a você para sua conveniência, na esperança de que seja útil e que traga algum benefício para você. Entretanto, se você usa ou implementa o pacote, é sua própria escolha. Você não é forçado a usar ou implementar o pacote, mas, quando o faz, você é responsável por essa decisão. Nem eu, nem qualquer outro colaborador do pacote, somos legalmente responsáveis pelas consequências das decisões que você toma, independentemente de ser direto, indireto, implícito, ou de outra forma.

#### 11.2 TERCEIROS

Dependendo de sua configuração e implementação exatas, o pacote pode se comunicar e compartilhar informações com terceiros em alguns casos. Essas informações podem ser definidas como "[informação pessoalmente identificável](https://pt.wikipedia.org/wiki/Informa%C3%A7%C3%A3o_pessoalmente_identific%C3%A1vel)" (PII) em alguns contextos, por algumas jurisdições.

Como esta informação pode ser usada por estes terceiros, está sujeita às várias políticas estabelecidas por esses terceiros, e está fora do escopo desta documentação. Contudo, em todos esses casos, o compartilhamento de informações com esses terceiros pode ser desativado. Em todos esses casos, se você optar por ativá-lo, é sua responsabilidade pesquisar quaisquer preocupações que você possa ter com relação à privacidade, segurança, e uso de PII por esses terceiros. Se houver alguma dúvida, ou se você estiver insatisfeito com a conduta desses terceiros em relação a PII, talvez seja melhor desativar todo o compartilhamento de informações com esses terceiros.

Para fins de transparência, o tipo de informação compartilhada e com quem está descrito abaixo.

##### 11.2.0 PESQUISA DE NOME DE HOST

Se você usar quaisquer funções ou módulos destinados a trabalhar com nomes de host (tais como o "módulo bloqueador de hosts perigosos", o "tor project exit nodes block module", ou "verificação do motores de busca", por exemplo), o CIDRAM precisa ser capaz de obter o nome do host de solicitações de entrada de alguma forma. Tipicamente, ele faz isso solicitando o nome do host do endereço IP das solicitações de entrada de um servidor DNS ou solicitando as informações por meio da funcionalidade fornecida pelo sistema em que o CIDRAM está instalado (isso é tipicamente referido como um "pesquisa de nome de host"). Os servidores DNS definidos por padrão pertencem ao serviço [Google DNS](https://dns.google.com/) (mas isso pode ser facilmente alterado por meio da configuração). Os serviços exatos comunicados com são configuráveis, e dependem de como você configura o pacote. No caso de usar a funcionalidade fornecida pelo sistema em que o CIDRAM está instalado, você precisará entrar em contato com o administrador do sistema para determinar quais rotas as pesquisas de nome de host usam. Pesquisas de nome de host podem ser evitadas no CIDRAM, evitando os módulos afetados ou modificando a configuração do pacote de acordo com suas necessidades.

*Diretivas de configuração relevantes:*
- `general` -> `default_dns`
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`
- `general` -> `force_hostname_lookup`
- `general` -> `allow_gethostbyaddr_lookup`

##### 11.2.2 VERIFICAÇÃO DOS MOTORES DE BUSCA E MÍDIAS SOCIAIS

Quando a verificação dos motores de busca é ativada, o CIDRAM tenta executar pesquisas direta DNS para verificar se as solicitações que dizem ter origem nos motores de busca são autênticas. Da mesma forma, quando a verificação de mídia social é ativada, o CIDRAM faz o mesmo para solicitações aparentes de mídia social. Para fazer isso, ele usa o serviço [Google DNS](https://dns.google.com/) para tentar resolver endereços IP dos nomes de host dessas solicitações de entrada (nesse processo, os nomes de host dessas solicitações de entrada são compartilhados com o serviço).

*Diretivas de configuração relevantes:*
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`

##### 11.2.3 CAPTCHA

CIDRAM oferece suporte a reCAPTCHA e hCAPTCHA. Eles requerem chaves de API para funcionar corretamente. Eles são desativados por padrão, mas podem ser ativados configurando as chaves API necessárias. Quando ativado, a comunicação pode ocorrer entre o serviço e o CIDRAM ou o navegador do usuário. Isso pode envolver a comunicação de informações como o endereço IP do usuário, agente do usuário, sistema operacional, e outros detalhes disponíveis para a solicitação.

##### 11.2.4 STOP FORUM SPAM

O [Stop Forum Spam](https://www.stopforumspam.com/) é um serviço fantástico, disponível gratuitamente, que pode ajudar a proteger fóruns, blogs, e sites de spammers. Ele faz isso fornecendo um banco de dados de spammers conhecidos, e uma API que pode ser aproveitada para verificar se um endereço IP, nome de usuário, ou um endereço de e-mail está listado em seu banco de dados.

O CIDRAM fornece um módulo opcional que aproveita essa API para verificar se o endereço IP de solicitações de entrada pertence a um spammer suspeito. O módulo não é instalado por padrão, mas se você optar por instalá-lo, os endereços IP do usuário podem ser compartilhados com a API do Stop Forum Spam de acordo com a finalidade do módulo. Quando o módulo é instalado, o CIDRAM se comunica com essa API sempre que uma solicitação de entrada solicita um recurso que o CIDRAM reconhece como um tipo de recurso frequentemente alvejado por spammers (tais como páginas de login, páginas de registro, páginas de verificação de e-mail, formulários de comentários, etc).

##### 11.2.5 ABUSEIPDB

O CIDRAM fornece um módulo opcional para bloquear endereços IP abusivos usando a API [AbuseIPDB](https://www.abuseipdb.com/). O módulo não é instalado por padrão, mas se você optar por instalá-lo, os endereços IP do usuário podem ser compartilhados com a API do AbuseIPDB de acordo com a finalidade do módulo.

##### 11.2.6 BGPVIEW

O CIDRAM fornece um módulo opcional para executar pesquisas de ASN e de código de país usando a API [BGPView](https://bgpview.io/). Essas pesquisas fornecem a capacidade de bloquear ou colocar na lista branca com base no ASN ou no país de origem. O módulo não é instalado por padrão, mas se você optar por instalá-lo, os endereços IP do usuário podem ser compartilhados com a API do BGPView de acordo com a finalidade do módulo.

#### 11.3 REGISTRO

O registro é uma parte importante do CIDRAM por vários motivos. Pode ser difícil diagnosticar e resolver falsos positivos quando os eventos de bloqueio que os causam não são registrados. Sem o registro de eventos de bloqueio, pode ser difícil determinar exatamente o quão bem o CIDRAM funciona em qualquer contexto específico, e pode ser difícil determinar onde suas deficiências podem ser, e quais mudanças podem ser necessárias para sua configuração ou assinaturas de acordo, para que ele continue funcionando como pretendido. Não obstante, o registro pode não ser desejável para todos os usuários e permanece totalmente opcional. No CIDRAM, o registro está desativado por padrão. Para ativá-lo, o CIDRAM deve ser configurado de acordo.

Adicionalmente, se o registro é legalmente permissível, e na medida em que é legalmente permissível (por exemplo, os tipos de informações que podem ser registradas, por quanto tempo, e sob quais circunstâncias), pode variar, dependendo da jurisdição e do contexto onde a CIDRAM é implementada (por exemplo, se você está operando como indivíduo, como entidade corporativa, e se está numa base comercial ou não comercial). Portanto, pode ser útil que você leia atentamente essa seção.

Existem vários tipos de registro que o CIDRAM pode executar. Diferentes tipos de registro envolvem diferentes tipos de informações, por diferentes razões.

##### 11.3.0 OS EVENTOS DE BLOQUEIO

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
- `general` -> `logfile`
- `general` -> `logfile_apache`
- `general` -> `logfile_serialized`

Quando essas diretivas são deixadas vazias, esse tipo de log permanecerá desativado.

##### 11.3.1 REGISTRO DE CAPTCHA

Esse tipo de registro refere-se especificamente a instâncias de CAPTCHA, e ocorre apenas quando um usuário tenta concluir uma instância de CAPTCHA.

Uma entrada de registro CAPTCHA contém o endereço IP do usuário que está tentando concluir uma instância de CAPTCHA, a data e a hora em que a tentativa ocorreu, e o estado CAPTCHA. Uma entrada de registro CAPTCHA normalmente se parece com isso (como um exemplo):

```
Endereço IP: x.x.x.x - Data/Hora: Day, dd Mon 20xx hh:ii:ss +0000 - Estado CAPTCHA: Sucesso!
```

*A diretiva de configuração responsável pelo registro de CAPTCHA é:*
- `recaptcha` -> `logfile`
- `hcaptcha` -> `logfile`

##### 11.3.2 REGISTRO DO FRONT-END

Esse tipo de registro está associado a tentativas de login no front-end, e ocorre apenas quando um usuário tenta efetuar login no front-end (supondo que o acesso ao front-end esteja ativado).

Uma entrada de registro do front-end contém o endereço IP do usuário que está tentando efetuar login, a data e a hora em que a tentativa ocorreu, e os resultados da tentativa (se teve sucesso ou não). Uma entrada de registro do front-end geralmente se parece com isso (como um exemplo):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Conectado.
```

*A diretiva de configuração responsável pelo registro do front-end é:*
- `general` -> `frontend_log`

##### 11.3.3 ROTAÇÃO DE REGISTRO

Você pode querer purgar os registros após um período de tempo, ou pode ser obrigado a fazê-lo por lei (ou seja, a quantidade de tempo permitida legalmente para você manter registros pode ser limitada por lei). Você pode conseguir isso incluindo marcadores de data/hora nos nomes de seus arquivos de registro conforme especificado pela sua configuração de pacote (por exemplo, `{yyyy}-{mm}-{dd}.log`) e, em seguida, ativando a rotação de registro (a rotação de registro permite que você execute alguma ação nos arquivos de registro quando os limites especificados são excedidos).

Por exemplo: Se eu fosse legalmente obrigado a deletar registros após 30 dias, eu poderia especificar `{dd}.log` nos nomes dos meus arquivos de registro (`{dd}` representa dias), definir o valor de `log_rotation_limit` para 30 e, em seguida, definir o valor de `log_rotation_action` para `Delete`.

Por outro lado, se você precisar reter o registros por um longo período de tempo, você poderia optar por não usar a rotação de registro em tudo, ou você pode definir o valor de `log_rotation_action` para `Archive`, para compactar arquivos de registro, reduzindo assim a quantidade total de espaço em disco que eles ocupam.

*Diretivas de configuração relevantes:*
- `general` -> `log_rotation_limit`
- `general` -> `log_rotation_action`

##### 11.3.4 TRUNCAMENTO DE REGISTRO

Também é possível truncar arquivos de registro individuais quando eles excedem um certo tamanho, se isso for algo que você possa precisar ou desejar fazer.

*Diretivas de configuração relevantes:*
- `general` -> `truncate`

##### 11.3.5 PSEUDONIMIZAÇÃO DE ENDEREÇOS IP

Em primeiro lugar, se você não estiver familiarizado com o termo, "pseudonimização" refere-se ao processamento de dados pessoais como tal que não pode ser identificado a nenhuma pessoa específica sem informações suplementares, e desde que tais informações suplementares sejam mantidas separadamente e sujeitas a medidas técnicas e organizacionais para assegurar que os dados pessoais não possam ser identificados a nenhuma pessoa natural.

Em algumas circunstâncias, você pode ser legalmente obrigado a anonimizar ou pseudonimizar qualquer PII coletada, processada ou armazenada. Embora este conceito já existe há algum tempo, o GDPR/DSGVO menciona notavelmente, e especificamente incentiva a "pseudonimização".

O CIDRAM é capaz de pseudonimizar endereços IP ao registrá-los, se isso for algo que você possa precisar ou desejar fazer. Quando o CIDRAM pseudonimiza os endereços IP, quando registrado, o octeto final dos endereços IPv4, e tudo após a segunda parte dos endereços IPv6 é representado por um "x" (efetivamente arredondando endereços IPv4 para o endereço inicial da 24ª sub-rede em que eles são fatorados em, e endereços IPv6 para o endereço inicial da 32ª sub-rede em que eles são fatorados em).

*Nota: O processo de pseudonimização de endereços IP no CIDRAM não afeta a funcionalidade de monitoração IP no CIDRAM. Se isso for um problema para você, talvez seja melhor desabilitar totalmente o monitoramento de IP. Isto pode ser conseguido ajustando `track_mode` para `false` e evitando quaisquer módulos.*

*Diretivas de configuração relevantes:*
- `signatures` -> `track_mode`
- `legal` -> `pseudonymise_ip_addresses`

##### 11.3.6 OMITINDO INFORMAÇÕES DE REGISTRO

Se você quiser dar um passo adiante, impedindo que tipos específicos de informação sejam registrados inteiramente, isso também é possível. O CIDRAM fornece diretivas de configuração para controlar se os endereços IP, os nomes de host, e os agentes do usuário estão incluídos nos registros. Por padrão, todos esses três pontos de dados são incluídos nos registros quando disponíveis. Definir qualquer uma dessas diretivas de configuração como `true` omitirá as informações correspondentes dos registros.

*Nota: Não há motivo para pseudônimo de endereços IP quando omití-los totalmente dos registros.*

*Diretivas de configuração relevantes:*
- `legal` -> `omit_ip`
- `legal` -> `omit_hostname`
- `legal` -> `omit_ua`

##### 11.3.7 ESTATISTICAS

O CIDRAM é opcionalmente capaz de rastrear estatísticas como o número total de eventos de bloqueio ou instâncias de CAPTCHA que ocorreram desde algum momento específico no tempo. Esta funcionalidade está desativada por padrão, mas pode ser ativada através da configuração do pacote. Essa funcionalidade rastreia apenas o número total de eventos ocorridos e não inclui informações sobre eventos específicos (e, portanto, não deve ser considerado como PII).

*Diretivas de configuração relevantes:*
- `general` -> `statistics`

##### 11.3.8 ENCRIPTAÇÃO

CIDRAM não criptografa seu cache ou qualquer informação de registro. A [encriptação](https://pt.wikipedia.org/wiki/Encripta%C3%A7%C3%A3o) de cache e registro pode ser introduzida no futuro, mas não há planos específicos para ela atualmente. Se você estiver preocupado com o acesso de terceiros não autorizados a partes do CIDRAM que possam conter PII ou informações confidenciais, como cache ou logs, recomendo que o CIDRAM não seja instalado em um local de acesso público (por exemplo, instale o CIDRAM fora do diretório `public_html` padrão ou seu equivalente disponível para a maioria dos servidores web padrão) e que as permissões apropriadamente restritivas sejam impostas para o diretório em que ele reside (em particular, para o diretório do vault). Se isso não for suficiente para resolver suas preocupações, configure o CIDRAM para que os tipos de informações que causam suas preocupações não sejam coletados ou registrados em primeiro lugar (tal como desabilitar o registro em log).

#### 11.4 COOKIES

O CIDRAM define [cookies](https://pt.wikipedia.org/wiki/Cookie_(inform%C3%A1tica)) em dois pontos em sua base de código. Em primeiro lugar, quando um usuário concluir com êxito uma instância de CAPTCHA (e supondo que `lockuser` esteja definido como `true`), O CIDRAM define um cookie para poder lembrar, para solicitações subsequentes, que o usuário já concluiu uma instância de CAPTCHA, de modo que não será necessário pedir continuamente ao usuário para concluir uma instância de CAPTCHA em solicitações subsequentes. Em segundo lugar, quando um usuário efetua login com êxito no front-end, o CIDRAM define um cookie para poder lembrar o usuário das solicitações subsequentes (isto é, os cookies são usados para autenticar o usuário numa sessão de login).

Em ambos os casos, os avisos de cookie são exibidos de forma proeminente (quando aplicável), avisando ao usuário que os cookies serão definidos se eles se envolverem nas ações relevantes. Os cookies não são definidos em nenhum outro ponto da base de código.

*Nota: As APIs CAPTCHA "invisíveis" podem ser incompatíveis com as leis de cookies em algumas jurisdições, e deve ser evitada por quaisquer websites sujeitos a essas leis. Optar por usar as outras APIs fornecidas, ou simplesmente desativar CAPTCHA totalmente, pode ser preferível.*

*Diretivas de configuração relevantes:*
- `general` -> `disable_frontend`
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 11.5 MARKETING E PUBLICIDADE

A CIDRAM não coleta ou processa qualquer informação para fins de marketing ou publicidade, e nem vende nem lucra com qualquer informação coletada ou registrada. A CIDRAM não é uma empresa comercial, nem está relacionada a nenhum interesse comercial, portanto, fazer essas coisas não faria sentido. Este tem sido o caso desde o início do projeto, e continua sendo o caso hoje. Além disso, fazer essas coisas seria contraproducente para o espírito e propósito do projeto como um todo, e enquanto eu continuar a manter o projeto, nunca acontecerá.

#### 11.6 POLÍTICA DE PRIVACIDADE

Em algumas circunstâncias, você pode ser legalmente obrigado a exibir claramente um link para sua política de privacidade em todas as páginas e seções do seu site. Isso pode ser importante como um meio de garantir que os usuários estejam bem informados sobre suas práticas de privacidade exatas, os tipos de PII que você coletar, e como você pretende usá-lo. Para poder incluir esse link na página "Acesso Negado" do CIDRAM, é fornecida uma diretiva de configuração para especificar o URL da sua política de privacidade.

*Nota: É altamente recomendável que sua página de política de privacidade não seja colocada atrás da proteção do CIDRAM. Se o CIDRAM proteger sua página de política de privacidade, e um usuário bloqueado pelo CIDRAM clicar no link para sua política de privacidade, ele será bloqueado novamente e não poderá ver sua política de privacidade. O ideal é vincular a uma cópia estática de sua política de privacidade, como uma página HTML ou um arquivo de texto simples que não esteja protegido pelo CIDRAM.*

*Diretivas de configuração relevantes:*
- `legal` -> `privacy_policy`

#### 11.7 GDPR/DSGVO

O Regulamento Geral sobre a Proteção de Dados (GDPR) é um regulamento da União Europeia, que entra em vigor em 25 de Maio, 2018. O principal objectivo do regulamento é dar controlo aos cidadãos e residentes da UE relativamente aos seus próprios dados pessoais, e unificar a regulação na UE em matéria de privacidade e dados pessoais.

O regulamento contém disposições específicas relativas ao tratamento de "[informações pessoalmente identificáveis](https://pt.wikipedia.org/wiki/Informa%C3%A7%C3%A3o_pessoalmente_identific%C3%A1vel)" (PII) de quaisquer "titulares de dados" (qualquer identificada ou identificável pessoa natural) da UE ou dentro da mesma. Para estar em conformidade com o regulamento, "empresas" (conforme definido pelo regulamento), e quaisquer sistemas e processos relevantes devem implementar "[privacidade desde a concepção](https://pt.wikipedia.org/wiki/Privacidade_desde_a_concep%C3%A7%C3%A3o)" por padrão, devem usar as configurações de privacidade mais altas possíveis, devem implementar as proteções necessárias para qualquer informação armazenada ou processada (incluindo, mas não limitado a, a implementação de pseudonimização ou anonimização completa de dados), devem declarar clara e inequivocamente os tipos de dados que coletam, como os processam, por quais motivos, por quanto tempo eles o retêm, e se compartilham esses dados com terceiros, os tipos de dados compartilhados com terceiros, como, porque, e assim por diante.

Os dados não podem ser processados a menos que haja uma base legal para isso, conforme definido pelo regulamento. Geralmente, isso significa que, para processar os dados de um titular de dados de forma legal, ele deve ser feito em conformidade com obrigações legais, ou feito somente após o consentimento explícito, bem informado, e inequívoco ter sido obtido do titular dos dados.

Como os aspectos da regulamentação podem evoluir no tempo, a fim de evitar a propagação de informações desatualizadas, pode ser melhor aprender sobre a regulamentação a partir de uma fonte oficial, em vez de simplesmente incluir as informações relevantes aqui na documentação do pacote (o que pode eventualmente desatualizado à medida que a regulamentação evolui).

[EUR-Lex](https://eur-lex.europa.eu/) (uma parte do site oficial da União Europeia que fornece informações sobre a legislação da UE) fornece informações abrangentes sobre o GDPR/DSGVO, disponível em 24 idiomas diferentes (no momento da escrita deste), e disponível para download em formato PDF. Eu recomendaria definitivamente ler as informações que eles fornecem, a fim de aprender mais sobre GDPR/DSGVO:
- [REGULAMENTO (UE) 2016/679 DO PARLAMENTO EUROPEU E DO CONSELHO](https://eur-lex.europa.eu/legal-content/PT/TXT/?uri=celex:32016R0679)

Alternativamente, há uma breve visão geral (não autoritativa) do GDPR/DSGVO disponível na Wikipedia:
- [Regulamento Geral sobre a Proteção de Dados](https://pt.wikipedia.org/wiki/Regulamento_Geral_sobre_a_Prote%C3%A7%C3%A3o_de_Dados)

---


Última Atualização: 17 de Fevereiro de 2022 (2022.02.17).
