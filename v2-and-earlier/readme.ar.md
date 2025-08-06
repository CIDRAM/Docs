## <div dir="rtl">CIDRAM v2 بالعربية</div>

### <div dir="rtl">المحتويات:</div>
<div dir="rtl"><ul>
 <li>١. <a href="#user-content-SECTION1">مقدمة</a></li>
 <li>٢. <a href="#user-content-SECTION2">كيفية التحميل</a></li>
 <li>٣. <a href="#user-content-SECTION3">كيفية الإستخدام</a></li>
 <li>٤. <a href="#user-content-SECTION4">إدارة FRONT-END</a></li>
 <li>٥. <a href="#user-content-SECTION5">الملفاتالموجودةفيهذهالحزمة</a></li>
 <li>٦. <a href="#user-content-SECTION6">خياراتالتكوين/التهيئة</a></li>
 <li>٧. <a href="#user-content-SECTION7">شكل/تنسيق التوقيع</a></li>
 <li>٨. <a href="#user-content-SECTION8">مشاكل التوافق المعروفة</a></li>
 <li>٩. <a href="#user-content-SECTION9">أسئلة وأجوبة (FAQ)</a></li>
 <li>١٠. محفوظة للإضافات المستقبلية إلى الوثائق.</li>
 <li>١١. <a href="#user-content-SECTION11">المعلومات القانونية</a></li>
</ul></div>

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### <div dir="rtl">١. <a name="SECTION1"></a>مقدمة</div>

<div dir="rtl">CIDRAM (توجيه بين المجالات لافئويا وصول مدير) هو السيناريو PHP، المصممة لحماية المواقع من طلبات الحجب تنشأ من عناوين IP تعتبر مصادر من حركة المرور غير مرغوب فيه، بما في ذلك (ولكن ليس على سبيل الحصر) حركة المرور من نقاط النهاية الوصول غير البشرية، خدمات سحابية، المتطفلين و برامج التطفل، كاشطات الموقع، إلخ. وهي تفعل ذلك عن طريق حساب CIDRs ممكن من عناوين IP الموردة من طلبات واردة وبعد ذلك محاولة لتتناسب مع هذه ضد الملفات توقيعه (هذه الملفات توقيع تحتوي CIDRs من عناوين IP تعتبر مصادر من حركة المرور غير مرغوب فيه)؛ إذا تم العثور على المباريات، يتم حظر الطلبات.<br /><br /></div>

<div dir="rtl"><em>(نرى: <a href="#user-content-WHAT_IS_A_CIDR">ما هو "CIDR"؟</a>).</em><br /><br /></div>

<div dir="rtl">حقوق النشر محفوظة ل <a dir="ltr" href="https://cidram.github.io/">CIDRAM</a> لعام ٢٠١٦ وما بعده تحت رخصة GNU/GPLv2 للمبرمج <a dir="ltr" href="https://github.com/Maikuolan">Caleb M (Maikuolan)</a>.<br /><br /></div>

<div dir="rtl">هذا البرنامج مجاني، يمكنك تعديله وإعادة نشره تحت رخصة GNU. نشارك هذا السكربت على أمل أن تعم الفائدة لكن لا نتحمل أية مسؤولية أو أية ضمانات لاستخدامك، اطلع على تفاصيل رخصة GNU للمزيد من المعلومات عبر الملف "LICENSE.txt" وللمزيد من المعلومات:</div>
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

<div dir="rtl">هذا المستند و الحزم المرتبطة به يمكن تحميلها مجاناً من:</div>
- <a dir="ltr" href="https://github.com/CIDRAM/CIDRAM">GitHub</a>.
- <a dir="ltr" href="https://bitbucket.org/Maikuolan/cidram">Bitbucket</a>.
- <a dir="ltr" href="https://codeberg.org/Maikuolan/CIDRAM">Codeberg</a>.

---


### <div dir="rtl">٢. <a name="SECTION2"></a>كيفية التحميل</div>

#### <div dir="rtl">٢.٠ تثبيت يدويا</div>

<div dir="rtl">١. بقراءتك لهذا سنفرض بأنك قمت بتحميل السكربت، من هنا عليك العمل على جهازك المحلي أو نظام إدارة المحتوى لإضافة هذه الأمور، مجلد مثل <code dir="ltr">"/public_html/cidram/"</code> أو ما شابه سيكون كاف.<br /><br /></div>

<div dir="rtl">٢. إعادة تسمية <code dir="ltr">"config.ini.RenameMe"</code> إلى "config.ini" (تقع داخل "vault")، واختياريا (هذه الخطوة اختيارية ينصح بها للمستخدمين المتقدمين ولا ينصح بها للمبتدئين)، افتحه، وعدل الخيارات كما يناسبك (أعلى كل خيار يوجد وصف مختصر للوظيفة التي يقوم بها).<br /><br /></div>

<div dir="rtl">٣. إرفع الملفات للمجلد الذي اخترته(لست بحاجة لرفع <code dir="ltr">"<code dir="ltr">*.txt/*.md</code>"</code> لكن في الغالب يجب أن ترفع جميع الملفات).<br /><br /></div>

<div dir="rtl">٤. غير التصريح لمجلد vault للتصريح<code dir="ltr">"755"</code> (إذا كان هناك مشاكل، يمكنك محاولة<code dir="ltr">"777"</code>، ولكن هذه ليست آمنة). المجلد الرئيسي الذي يحتوي على الملفات-المجلد الذي اخترته سابقاً-، بالعادة يمكن تجاهله، لكن يجب التأكد من التصريح إذا واجهت مشاكل في الماضي(إفتراضيا يجب أن يكون<code dir="ltr">"755"</code>). باختصار: لكي تعمل الحزمة بشكل صحيح، يجب أن تكون PHP قادرة على قراءة وكتابة الملفات داخل دليل <code dir="ltr">vault</code>. العديد من الأشياء (التحديث، التسجيل، الخ) لن تكون ممكنة، إذا تعذر على PHP الكتابة إلى دليل <code dir="ltr">vault</code>، ولن تعمل الحزمة على الإطلاق إذا تعذر على PHP القراءة من دليل <code dir="ltr">vault</code>. ومع ذلك، للحصول على الأمان الأمثل، يجب ألا يكون دليل <code dir="ltr">vault</code> متاحًا للجميع (المعلومات الحساسة، مثل المعلومات التي يحتوي عليها <code dir="ltr">config.ini</code> أو <code dir="ltr">frontend.dat</code>، يمكن أن تتعرض لمهاجمين محتملين إذا كان دليل <code dir="ltr">vault</code> متاحًا للجميع).<br /><br /></div>

<div dir="rtl">٥. الآن أنت بحاجة لربط CIDRAM لنظام إدارة المحتوى أو النظام الذي تستخدمه، هناك عدة طرق لفعل هذا لكن أسهل طريقة ببساطة إضافة السكربت لبداية النواة في نظامك (سيتم إعادة التحميل لكل وصول لأي صفحة في الموقع) بإستخدام جمل "require" أو "include"، بالعادة سيتم التخزين في "/includes"، "/assets" أو "/functions"، وسيتم تسميته بالغالب مثل: "init.php"، "common_functions.php"، "functions.php" أو ما شابه. من الممكن أن تكون مستخدم ل CMS لذا يمكن أن أقدم بعض المساعدة بخصوص هذا الموضوع، لإستخدام "require" أو "include" قم بإضافة الكود التالي لبداية الملف الرئيسي لبرنامجك، عدل النص الموجود داخل علامات التنصيص لمسار "loader.php" لديك.<br /><br /></div>

`<?php require '/user_name/public_html/cidram/loader.php'; ?>`

<div dir="rtl">إحفظ الملف ثم قم بإعادة رفعه.<br /><br /></div>

<div dir="rtl">-- أو بدلاً من ذلك --<br /><br /></div>

<div dir="rtl">إذا كنت تستخدم Apache webserver وتستطيع الوصول ل "php.ini"، بإستطاعتك إستخدام "auto_prepend_file" للتوجيه ل CIDRAM لكل طلب مثل:<br /><br /></div>

`auto_prepend_file = "/user_name/public_html/cidram/loader.php"`

<div dir="rtl">أو هذا في ملف ".htaccess":<br /><br /></div>

`php_value auto_prepend_file "/user_name/public_html/cidram/loader.php"`

<div dir="rtl">٦. هذا كل شئ. 😄<br /><br /></div>

#### <div dir="rtl">٢.١ تثبيت مع COMPOSER</div>

<div dir="rtl"><a href="https://packagist.org/packages/cidram/cidram">يتم تسجيل CIDRAM مع Packagist</a>، و بالتالي، إذا كنت على دراية به، يمكنك استخدامه لتثبيت CIDRAM (ستظل بحاجة إلى إعداده على الرغم من ذلك؛ نرى "تثبيت يدويا" الخطوتين ٢، ٤ و ٥).<br /><br /></div>

`composer require cidram/cidram`

#### <div dir="rtl">٢.٢ تثبيت ل ووردبريس</div>

<div dir="rtl">إذا كنت ترغب في استخدام CIDRAM مع ووردبريس، يمكنك تجاهل جميع التعليمات أعلاه. <a href="https://wordpress.org/plugins/cidram/">يتوفر CIDRAM من قاعدة بيانات الإضافات وووردبريس</a>. يمكنك تثبيته بنفس الطريقة مثل أي مكون إضافي. كما هو الحال مع أساليب التثبيت الأخرى، يمكنك تخصيص التثبيت الخاص بك عن طريق تعديل محتويات الملف "config.ini"، أو باستخدام صفحة تهيئة front-end.<br /><br /></div>

<div dir="rtl"><em>تحذير: يؤدي تحديث CIDRAM عبر لوحة تحكم المكونات الإضافية إلى تثبيت نظيف! إذا كان لديك تخصيصات (تغيير التكوين، تثبيت وحدات، الخ)، سيتم فقدان هذه التخصيصات عند تحديث عن طريق لوحة أجهزة القياس الإضافات! كما سيتم فقدان لوغفيلز عند تحديث عن طريق لوحة أجهزة القياس الإضافات! للحفاظ على ملفات السجل والتخصيصات، يتم التحديث عبر صفحة التحديثات الأمامية ل CIDRAM.</em><br /><br /></div>

---


### <div dir="rtl">٣. <a name="SECTION3"></a>كيفية الإستخدام</div>

<div dir="rtl">CIDRAM يجب منع تلقائيا طلبات غير مرغوب فيها إلى موقع الويب الخاص بك، دون الحاجة إلى أي مساعدة اليدوية، جانبا من التثبيت.<br /><br /></div>

<div dir="rtl">يمكنك تخصيص التكوين الخاص بك وتخصيص التي CIDRs مسدودة عن طريق تعديل التكوين الخاص بك و ملفات توقيعك.<br /><br /></div>

<div dir="rtl">إذا واجهت أي إيجابية خاطئة، يرجى رسالة لي أن اسمحوا لي أن أعرف عن ذلك. <em>(نرى: <a href="#user-content-WHAT_IS_A_FALSE_POSITIVE">ما هو "إيجابية خاطئة"؟</a>).</em><br /><br /></div>

<div dir="rtl">يمكن تحديث CIDRAM يدويا أو عن طريق الfront-end. يمكن أيضا تحديث CIDRAM عبر Composer أو WordPress، إذا تم تثبيتها أصلا عبر تلك الوسائل.<br /><br /></div>

---


### <div dir="rtl">٤. <a name="SECTION4"></a>إدارة FRONT-END</div>

#### <div dir="rtl">٤.٠ ما هو FRONT-END.<br /><br /></div>

<div dir="rtl">Front-end يوفر وسيلة سهلة للحفاظ على، وإدارة، وتحديث CIDRAM. يمكنك عرض، حصة، وتحميل ملفات الدخول، يمكنك تعديل تكوين، يمكنك تثبيت وإلغاء تثبيت مكونات، ويمكنك تحميل وتنزيل وتعديل الملفات.<br /><br /></div>

<div dir="rtl">Front-end معطل في البداية، لمنع الوصول غير المصرح به (الدخول غير المصرح به قد يكون له عواقب أمنية كبيرة). تعليمات لتمكينه أدناه.<br /><br /></div>

#### <div dir="rtl">٤.١ كيفية تمكين FRONT-END.<br /><br /></div>

<div dir="rtl">١. العثور <code dir="ltr">"disable_frontend"</code> من في <code dir="ltr">"config.ini"</code>، وتعيينها إلى false (القيمة القياسية هي true).<br /><br /></div>

<div dir="rtl">٢. الوصول إلى <code dir="ltr">"loader.php"</code> من المتصفح (مثلا، <code dir="ltr">"http://localhost/cidram/loader.php"</code>).<br /><br /></div>

<div dir="rtl">٣. تسجيل الدخول باستخدام اسم المستخدم وكلمة المرور الافتراضية (admin/password).<br /><br /></div>

<div dir="rtl">ملحوظة: تغيير اسم المستخدم وكلمة المرور الخاصة بك بعد تسجيل الدخول للمرة الأولى، من أجل منع الوصول غير المصرح به (هذا مهم جدا)!<br /><br /></div>

<div dir="rtl">أيضًا، للحصول على الأمان الأمثل، نوصي بشدة بتمكين 2FA لجميع حسابات الواجهة الأمامية (الإرشادات الواردة أدناه).<br /><br /></div>

#### <div dir="rtl">٤.٢ كيفية استخدام FRONT-END.<br /><br /></div>

<div dir="rtl">في كل صفحة، ويفسر ذلك كيفية استخدامها. إذا كنت بحاجة إلى أي مساعدة، يرجى الاتصال بالدعم. وهناك أيضا بعض مقاطع الفيديو المفيدة المتاحة على موقع يوتيوب.<br /><br /></div>

#### <div dir="rtl">٤.٣ 2FA<br /><br /></div>

<div dir="rtl">من الممكن جعل front-end أكثر أمانًا عن طريق تمكين 2FA. عند تسجيل الدخول إلى حساب باستخدام 2FA، يتم إرسال بريد إلكتروني إلى عنوان البريد الإلكتروني المقترن بهذا الحساب. تحتوي هذه الرسالة الإلكترونية على "رمز 2FA"، والذي يجب على المستخدم إدخاله، بالإضافة إلى اسم المستخدم وكلمة المرور، حتى تتمكن من تسجيل الدخول باستخدام هذا الحساب. وهذا يعني أن الحصول على كلمة مرور الحساب لن يكون كافيًا لأي متسلل أو مهاجم محتمل ليتمكن من تسجيل الدخول إلى هذا الحساب، لأنهم سيحتاجون أيضًا إلى الوصول بالفعل إلى عنوان البريد الإلكتروني المرتبط بهذا الحساب حتى يتمكنوا من تلقي رمز 2FA واستخدامه في الجلسة.<br /><br /></div>

<div dir="rtl">أولاً، لتمكين 2FA، استخدم صفحة تحديثات front-end لتثبيت مكون PHPMailer. CIDRAM يستخدم PHPMailer لإرسال رسائل البريد الإلكتروني. ملحوظة: على الرغم من أن CIDRAM متوافق مع <code dir="ltr">PHP &gt;= 5.4.0</code>، PHPMailer يتطلب <code dir="ltr">PHP &gt;= 5.5.0</code>، مما يعني أن تمكين 2FA لـ CIDRAM front-end لن يكون ممكنًا لمستخدمي <code dir="ltr">PHP 5.4</code>.<br /><br /></div>

<div dir="rtl">بعد تثبيت PHPMailer، ستحتاج إلى تعبئة توجيهات التهيئة لـ PHPMailer عبر صفحة تهيئة CIDRAM أو ملف التكوين. يتم تضمين مزيد من المعلومات حول توجيهات التكوين هذه في قسم التكوين في هذا المستند. بعد ملء توجيهات تهيئة PHPMailer، اضبط <code dir="ltr">enable_two_factor</code> على <code dir="ltr">true</code>. 2FA ممكّن الآن.<br /><br /></div>

<div dir="rtl">بعد ذلك، ستحتاج إلى ربط عنوان بريد إلكتروني بحساب، حتى يعرف CIDRAM مكان إرسال رموز 2FA عند تسجيل الدخول باستخدام هذا الحساب. للقيام بذلك، استخدم عنوان البريد الإلكتروني كاسم مستخدم للحساب (مثل <code dir="ltr">foo@bar.tld</code>)، أو تضمين عنوان البريد الإلكتروني كجزء من اسم المستخدم بالطريقة نفسها التي تريدها عند إرسال بريد إلكتروني بشكل طبيعي (مثل <code dir="ltr">Foo Bar &lt;foo@bar.tld&gt;</code>).<br /><br /></div>

<div dir="rtl">ملحوظة: حماية "vault" ضد الوصول غير المصرح به (على سبيل المثال، من خلال تعزيز أمن الخادم الخاص بك وتقييد أذونات الوصول العام)، أهمية خاصة هنا، لأن الوصول غير المصرح به إلى ملف التكوين الخاص بك (المخزن في "vault")، قد يؤدي إلى تعريض إعدادات SMTP الصادرة (بما في ذلك اسم مستخدم وكلمة مرور SMTP). يجب التأكد من تأمين "vault" بشكل صحيح قبل تمكين 2FA. إذا كنت غير قادر على القيام بذلك، فعلى الأقل، يجب عليك إنشاء حساب بريد إلكتروني جديد مخصص لهذا الغرض، وذلك لتقليل المخاطر المرتبطة بإعدادات SMTP المكشوفة.<br /><br /></div>

---


### <div dir="rtl">٥. <a name="SECTION5"></a>الملفاتالموجودةفيهذهالحزمة</div>

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


### <div dir="rtl">٦. <a name="SECTION6"></a>خياراتالتكوين/التهيئة</div>

<div dir="rtl">وفيما يلي قائمة من المتغيرات الموجودة في ملف تكوين "config.ini"، بالإضافة إلى وصف الغرض منه و وظيفته.<br /><br /></div>

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
│       disable_webfonts
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

#### <div dir="rtl">"general" (التصنيف)<br /></div>
<div dir="rtl">التكوين العام لـ CIDRAM.<br /><br /></div>

##### <div dir="rtl">"logfile"<br /></div>
<div dir="rtl"><ul>
 <li>ملف يمكن قراءته بالعين لتسجيل كل محاولات الوصول سدت. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li>
</ul></div>

##### <div dir="rtl">"logfile_apache"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "logfileApache"</em></li>
 <li>ملف على غرار أباتشي لتسجيل كل محاولات الوصول سدت. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li>
</ul></div>

##### <div dir="rtl">"logfile_serialized"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "logfileSerialized"</em></li>
 <li>ملف تسلسل لتسجيل كل محاولات الوصول سدت. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li>
</ul></div>

<div dir="rtl"><em>نصيحة مفيدة: إن أردت، يمكنك إلحاق تاريخ/المعلومات في الوقت إلى أسماء ملفات السجل من خلال تضمين هذه في اسم: "{yyyy}" لمدة عام كامل، "{yy}" لمدة عام يختصر، "{mm}" لمدة شهر، "{dd}" ليوم واحد، "{hh}" لمدة ساعة (راجع الأمثلة أدناه).</em><br /><br /></div>

```
 logfile='logfile.{yyyy}-{mm}-{dd}-{hh}.txt'
 logfile_apache='access.{yyyy}-{mm}-{dd}-{hh}.txt'
 logfile_serialized='serial.{yyyy}-{mm}-{dd}-{hh}.txt'
```

##### <div dir="rtl">"error_log"<br /></div>
<div dir="rtl"><ul>
 <li>ملف لتسجيل أي أخطاء غير مميتة المكتشفة. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li>
</ul></div>

##### <div dir="rtl">"error_log_stages"<br /></div>
<div dir="rtl"><ul>
 <li>قائمة المراحل في سلسلة التنفيذ التي بموجبها يجب تسجيل أي أخطاء تم إنشاؤها.</li>
 <li><em>افتراضي: "Tests,Modules,SearchEngineVerification,SocialMediaVerification,OtherVerification,Aux,Reporting,Tracking,RL,CAPTCHA,Statistics,Webhooks,Output,NonBlockedCAPTCHA"</em></li>
</ul></div>

##### <div dir="rtl">"truncate"<br /></div>
<div dir="rtl"><ul>
 <li>اقتطاع ملفات السجل عندما تصل إلى حجم معين؟ القيمة هي الحجم الأقصى في بايت/كيلوبايت/ميغابايت/غيغابايت/تيرابايت الذي قد ينمو ملفات السجل إلى قبل اقتطاعه. القيمة الافتراضية 0KB تعطيل اقتطاع (ملفات السجل يمكن أن تنمو إلى أجل غير مسمى). ملاحظة: ينطبق على ملفات السجل الفردية! ولا يعتبر حجمها جماعيا.</li>
</ul></div>

##### <div dir="rtl">"log_rotation_limit"<br /></div>
<div dir="rtl"><ul>
 <li>يحدد تدوير السجل عدد ملفات السجل التي يجب أن تكون موجودة في أي وقت. عند إنشاء ملفات السجل الجديدة، إذا تجاوز العدد الإجمالي لبيانات السجل الحد المحدد، فسيتم تنفيذ الإجراء المحدد. يمكنك تحديد الحد المرغوب هنا. ستعمل القيمة 0 على تعطيل تدوير السجل.</li>
</ul></div>

##### <div dir="rtl">"log_rotation_action"<br /></div>
<div dir="rtl"><ul>
 <li>يحدد تدوير السجل عدد ملفات السجل التي يجب أن تكون موجودة في أي وقت. عند إنشاء ملفات السجل الجديدة، إذا تجاوز العدد الإجمالي لبيانات السجل الحد المحدد، فسيتم تنفيذ الإجراء المحدد. يمكنك تحديد الإجراء المطلوب هنا. Delete = احذف أقدم السجلات، حتى لا يتم تجاوز الحد. Archive = أرشفة أولاً، ثم احذف أقدم السجلات، حتى لا يتم تجاوز الحد.</li>
</ul></div>

<div dir="rtl">التوضيح الفني: في هذا السياق، تعني كلمة "أقدم"، هذا يعني "الأقل معدلة مؤخرا".<br /><br /></div>

##### <div dir="rtl">"timezone"<br /></div>
<div dir="rtl"><ul>
 <li>يتم استخدام هذا لتحديد المنطقة الزمنية التي يجب أن يستخدمها CIDRAM لعمليات التاريخ / الوقت. إذا لم تكن بحاجة إليه، فتجاهله. يتم تحديد القيم المحتملة بواسطة PHP. يُوصى بشكل عام بدلاً من ضبط توجيه المنطقة الزمنية في ملف <code dir="ltr">php.ini</code>. على الرغم من أنه في بعض الأحيان (على سبيل المثال عند العمل مع موفري استضافة مشتركة محدودة)، لا يكون ذلك ممكنًا دائمًا، وهكذا، يتم توفير هذا الخيار هنا.</li>
</ul></div>

##### <div dir="rtl">"time_offset"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "timeOffset"</em></li>
 <li>إذا بالتوقيت المحلي الخاص بك ليست هي نفسها كما الخادم الخاص بك، يمكنك تحديد إزاحة هنا (لضبط التاريخ / المعلومات في الوقت صنعت بواسطة CIDRAM). الإزاحة المستندة دقيقة.<br /></li>
 <li>مثال (لإضافة ساعة واحدة):</li>
</ul></div>

`time_offset=60`

##### <div dir="rtl">"time_format"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "timeFormat"</em></li>
 <li>شكل التواريخ المستخدم من قبل CIDRAM. الافتراضي:</li>
</ul></div>

`{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss} {tz}`

##### <div dir="rtl">"ipaddr"<br /></div>
<div dir="rtl"><ul>
 <li>أين يمكن العثور على عنوان IP لربط الطلبات؟ (مفيدة للخدمات مثل لايتكلاود و مثلها). الافتراضي = REMOTE_ADDR. تحذير: لا تغير هذا إلا إذا كنت تعرف ما تفعلونه!</li>
</ul></div>

<div dir="rtl">القيم الموصى بها ل "ipaddr":<br /><br /></div>

&nbsp; <div dir="rtl" style="display:inline">القيمة</div> | &nbsp; <div dir="rtl" style="display:inline">استعمال</div>
---|---
`HTTP_INCAP_CLIENT_IP` | Incapsula reverse proxy (إنكابسولا عكس الوكيل).
`HTTP_CF_CONNECTING_IP` | Cloudflare reverse proxy (كلودفلاري عكس الوكيل).
`CF-Connecting-IP` | Cloudflare reverse proxy (كلودفلاري عكس الوكيل؛ لبديل؛ إذا كان ما سبق لا يعمل).
`HTTP_X_FORWARDED_FOR` | Cloudbric reverse proxy.
`X-Forwarded-For` | [Squid reverse proxy (عكس الوكيل)](http://www.squid-cache.org/Doc/config/forwarded_for/).
`Forwarded` | *[Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded).*
&nbsp; <div dir="rtl" style="display:inline"><em>يحددها تكوين الخادم.</em></div> | [Nginx reverse proxy (إنجن إكس عكس الوكيل)](https://www.nginx.com/resources/admin-guide/reverse-proxy/).
`REMOTE_ADDR` | &nbsp; <div dir="rtl" style="display:inline">لا يوجد عكس الوكيل (الافتراضي).</div>

##### <div dir="rtl">"forbid_on_block"<br /></div>
<div dir="rtl"><ul>
 <li>ما هي رسالة حالة HTTP التي يجب أن يرسلها CIDRAM عند حظر الطلبات؟</li>
</ul></div>

<div dir="rtl">القيم المدعومة حاليًا:<br /><br /></div>

رمز حالة | رسالة الحالة | وصف
---|---|---
`200` | `200 OK` | القيمة الافتراضية. أقل قوة، ولكن الأكثر سهولة في الاستخدام. من المرجح أن تفسر الطلبات الآلية هذه الاستجابة على أنها إشارة إلى نجاح الطلب.
`403` | `403 Forbidden` | أكثر قوة، ولكن أقل سهولة في الاستخدام. موصى به لمعظم الظروف العامة.
`410` | `410 Gone` | يمكن أن يسبب مشاكل عند حل الإيجابيات الخاطئة، لأن بعض المتصفحات سوف تخزن رسالة الحالة هذه مؤقتًا ولا ترسل طلبات لاحقة، حتى بعد إلغاء الحظر. قد يكون الأكثر تفضيلاً في بعض السياقات، لأنواع معينة من حركة المرور.
`418` | `418 I'm a teapot` | يشير إلى نكتة كذبة أبريل (<a href="https://tools.ietf.org/html/rfc2324#section-6.5.14">RFC 2324</a>). من غير المحتمل جدًا أن يفهمه أي عميل أو روبوت أو متصفح أو غير ذلك. يتم توفيرها للتسلية والراحة، ولكن لا يوصى بها بشكل عام.
`451` | `451 Unavailable For Legal Reasons` | يوصى به عند الحظر لأسباب قانونية في المقام الأول. لا ينصح به في سياقات أخرى.
`503` | `503 Service Unavailable` | الأكثر قوة، ولكن الأقل سهولة في الاستخدام. يوصى به عند التعرض للهجوم أو عند التعامل مع حركة مرور غير مرغوب فيها بشكل دائم للغاية.

##### <div dir="rtl">"silent_mode"<br /></div>
<div dir="rtl"><ul>
 <li>يجب CIDRAM إعادة توجيه بصمت محاولات وصول مرفوض بدلا من عرض الصفحة "تم رفض الوصول"؟ اذا نعم، تحديد الموقع لإعادة توجيه محاولات وصول مرفوض. ان لم، ترك هذا الحقل فارغا.</li>
</ul></div>

##### <div dir="rtl">"lang"<br /></div>
<div dir="rtl"><ul>
 <li>تحديد اللغة الافتراضية الخاصة بـ CIDRAM.</li>
</ul></div>

##### <div dir="rtl">"lang_override"<br /></div>
<div dir="rtl"><ul>
 <li>الترجمة وفقًا لـ HTTP_ACCEPT_LANGUAGE كلما أمكن ذلك؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li>
</ul></div>

##### <div dir="rtl">"numbers"<br /></div>
<div dir="rtl"><ul>
 <li>لتحديد كيفية عرض الأرقام.</li>
</ul></div>

<div dir="rtl">القيم المدعومة حاليًا:<br /><br /></div>

القيمة | ينتج عنه | وصف
---|---|---
`NoSep-1` | `1234567.89`
`NoSep-2` | `1234567,89`
`Latin-1` | `1,234,567.89` | القيمة القياسية
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

<div dir="rtl">ملحوظة: هذه القيم ليست مالمكون في أي مكان، وربما لن تكون ذات صلة خارج الحزمة. أيضا، قد تتغير القيم المدعومة في المستقبل.<br /><br /></div>

##### <div dir="rtl">"emailaddr"<br /></div>
<div dir="rtl"><ul>
 <li>لو كنت تريد، يمكنك توفير عنوان البريد الإلكتروني هنا أن تعطى للمستخدمين عند أنها ممنوعة، بالنسبة لهم لاستخدامها كنقطة اتصال للحصول على الدعم والمساعدة لفي حال منهم سدت طريق الخطأ أو في ضلال. تحذير: أي عنوان البريد الإلكتروني الذي تزويد هنا وبالتأكيد سيتم شراؤها من قبل المتطفلين و برامج التطفل وكاشطات خلال المستخدمة هنا، و حينئذ، انها المستحسن أن إذا اخترت توفير عنوان البريد الإلكتروني هنا، يمكنك التأكد من أن عنوان البريد الإلكتروني الذي نورد هنا يمكن التخلص منها و/أو عنوان أنك لا تمانع في أن محتوى غير مرغوب فيه (بعبارات أخرى، وربما كنت لا تريد استخدام الرئيسية عناوين البريد الإلكتروني التجارية أو العناوين الشخصية الرئيسية الخاصة بك).</li>
</ul></div>

##### <div dir="rtl">"emailaddr_display_style"<br /></div>
<div dir="rtl"><ul>
 <li>كيف تفضل أن يتم تقديم عنوان البريد الإلكتروني إلى المستخدمين؟ "default" = رابط قابل للنقر. "noclick" = نص غير قابل للنقر.</li>
</ul></div>

##### <div dir="rtl">"disable_cli"<br /></div>
<div dir="rtl"><ul>
 <li><em>(تمت إزالته منذ الإصدار الثاني).</em></li>
 <li>وضع تعطيل CLI؟ يتم تمكين وضع CLI افتراضيا، ولكن يمكن أن تتداخل أحيانا مع بعض أدوات الاختبار (مثل PHPUnit، على سبيل المثال) وغيرها من التطبيقات القائمة على المبادرة القطرية. إذا كنت لا تحتاج إلى تعطيل وضع CLI، يجب تجاهل هذا التوجيه. خاطئة = تمكين وضع CLI [الافتراضي]. صحيح/True = وضع تعطيل CLI.</li>
</ul></div>

##### <div dir="rtl">"disable_frontend"<br /></div>
<div dir="rtl"><ul>
 <li>تعطيل وصول front-end؟ وصول front-end يستطيع جعل CIDRAM أكثر قابلية للإدارة، ولكن يمكن أيضا أن تكون مخاطر أمنية محتملة. من المستحسن لإدارة CIDRAM عبر back-end متى أمكن، لكن وصول front-end متوفر عندما لم يكن ممكنا. يبقيه المعوقين إلا إذا كنت في حاجة إليها. زائفة/False = تمكين وصول front-end؛ صحيح/True = تعطيل وصول front-end [الافتراضي].</li>
</ul></div>

##### <div dir="rtl">"max_login_attempts"<br /></div>
<div dir="rtl"><ul>
 <li>الحد الأقصى لعدد محاولات تسجيل الدخول (front-end). الافتراضي = 5.</li>
</ul></div>

##### <div dir="rtl">"frontend_log"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "FrontEndLog"</em></li>
 <li>ملف لتسجيل محاولات الدخول الأمامية. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li>
</ul></div>

##### <div dir="rtl">"signatures_update_event_log"<br /></div>
<div dir="rtl"><ul>
 <li>ملف للتسجيل عند تحديث التوقيعات عبر الواجهة الأمامية. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li>
</ul></div>

##### <div dir="rtl">"ban_override"<br /></div>
<div dir="rtl"><ul>
 <li>تجاوز "forbid_on_block" متى "infraction_limit" تجاوزت؟ عندما تجاوز: الطلبات الممنوعة بإرجاع صفحة فارغة (لا يتم استخدام ملفات قالب). 200 = لا تجاوز [الافتراضي]. القيم الأخرى هي نفس القيم المتاحة لـ "forbid_on_block".</li>
</ul></div>

##### <div dir="rtl">"log_banned_ips"<br /></div>
<div dir="rtl"><ul>
 <li>من IP المحظورة في ملفات السجل؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li>
</ul></div>

##### <div dir="rtl">"default_dns"<br /></div>
<div dir="rtl"><ul>
 <li>قائمة بفواصل من خوادم DNS لاستخدامها في عمليات البحث عن اسم المضيف. الافتراضي = "8.8.8.8,8.8.4.4" (Google DNS). تحذير: لا تغير هذا إلا إذا كنت تعرف ما تفعلونه!</li>
</ul></div>

<div dir="rtl">أنظر أيضا: <a href="#ما-الذي-يمكنني-استخدامه-لـ-default_dns">ما الذي يمكنني استخدامه لـ "default_dns"؟</a><br /><br /></div>

##### <div dir="rtl">"search_engine_verification"<br /></div>
<div dir="rtl"><ul>
 <li>محاولة للتحقق من طلبات من محركات البحث؟ التحقق من محركات البحث يضمن أنها لن تكون محظورة نتيجة لتجاوز الحد مخالفة (منع محركات البحث من موقع الويب الخاص بك عادة ما يكون لها تأثير سلبي على محرك البحث الترتيب، كبار المسئولين الاقتصاديين، إلخ). عند تمكين التحقق، محركات البحث يمكن أن يكون قد تم حظره، ولكن ليس محظورة. عند تعطيل التحقق، أنها يمكن أن تكون محظورة إذا تجاوزت الحد مخالفة. بالإضافة إلى، التحقق محرك البحث يحمي ضد الكيانات الخبيثة يتنكر في محركات البحث (سيتم حجب هذه الطلبات). صحيح/True = تمكين التحقق محرك البحث [افتراضي]؛ زائفة/False = تعطيل التحقق محرك البحث.</li>
</ul></div>

<div dir="rtl">المدعومة حاليا:<br /></div>
<div dir="rtl"><ul>
 <li><strong dir="ltr"><a href="https://discussions.apple.com/thread/7090135">Applebot</a></strong></li>
 <li><strong dir="ltr"><a href="https://help.baidu.com/question?prod_en=master&class=Baiduspider">Baiduspider/百度</a></strong></li>
 <li><strong dir="ltr"><a href="https://blogs.bing.com/webmaster/2012/08/31/how-to-verify-that-bingbot-is-bingbot">Bingbot</a></strong></li>
 <li><strong dir="ltr"><a href="https://duckduckgo.com/duckduckbot">DuckDuckBot</a></strong></li>
 <li><strong dir="ltr"><a href="https://support.google.com/webmasters/answer/80553?hl=en">Googlebot</a></strong></li>
 <li><strong dir="ltr"><a href="https://www.mojeek.com/bot.html">MojeekBot</a></strong></li>
 <li><strong dir="ltr"><a href="https://aspiegel.com/petalbot">PetalBot</a></strong></li>
 <li><strong dir="ltr"><a href="https://help.qwant.com/bot">Qwantify/Bleriot</a></strong></li>
 <li><strong dir="ltr"><a href="https://napoveda.seznam.cz/en/full-text-search/seznambot-crawler/">SeznamBot</a></strong></li>
 <li><strong dir="ltr"><a href="https://www.sogou.com/docs/help/webmasters.htm#07">Sogou/搜狗</a></strong></li>
 <li><strong dir="ltr"><a href="https://help.yahoo.com/help/us/ysearch/slurp">Yahoo/Slurp</a></strong></li>
 <li><strong dir="ltr"><a href="https://yandex.com/support/webmaster/robot-workings/check-yandex-robots.xml">Yandex/Яндекс</a></strong></li>
 <li><strong dir="ltr"><a href="https://udger.com/resources/ua-list/bot-detail?bot=YoudaoBot#id1507">Youdao/有道</a></strong></li>
</ul></div>

<div dir="rtl">غير متوافق (تسبب الصراعات):<br /></div>
<div dir="rtl"><ul>
 <li><strong dir="ltr"><a href="https://github.com/CIDRAM/CIDRAM/issues/80">Mix.com</a></strong></li>
</ul></div>

##### <div dir="rtl">"social_media_verification"<br /></div>
<div dir="rtl"><ul>
 <li>محاولة التحقق من طلبات الشبكات الاجتماعية؟ يوفر التحقق من الشبكات الاجتماعية الحماية ضد طلبات وسائل الإعلام الاجتماعية المزيفة (سيتم حجب هذه الطلبات). صحيح/True = تمكين [افتراضي]؛ زائفة/False = تعطيل.</li>
</ul></div>

<div dir="rtl">المدعومة حاليا:<br /></div>
<div dir="rtl"><ul>
 <li><strong dir="ltr"><a href="https://udger.com/resources/ua-list/bot-detail?bot=Embedly#id22674">Embedly</a></strong></li>
 <li><strong dir="ltr"><a href="https://developers.facebook.com/docs/sharing/webmasters/crawler/">Facebook external hit</a> **</strong></li>
 <li><strong dir="ltr"><a href="https://help.pinterest.com/en/articles/about-pinterest-crawler-0">Pinterest</a></strong></li>
 <li><strong dir="ltr"><a href="https://udger.com/resources/ua-list/bot-detail?bot=Twitterbot#id6168">Twitterbot</a></strong></li>
</ul></div>

<div dir="rtl"><em>**: يتطلب أداة بحث ASN، على سبيل المثال، المكون BGPView.</em><br /></div>

##### <div dir="rtl">"other_verification"<br /></div>
<div dir="rtl"><ul>
 <li>حيثما أمكن، حاول التحقق من أنواع الطلبات الأخرى (على سبيل المثال، AdSense، أدوات فحص تحسين محركات البحث، إلخ)؟ عند اكتشافها، سيتم حظر الطلبات المزيفة. صحيح/True = تمكين [افتراضي]؛ زائفة/False = تعطيل.</li>
</ul></div>

<div dir="rtl">المدعومة حاليا:<br /></div>
<div dir="rtl"><ul>
 <li><strong dir="ltr"><a href="https://adbot.amazon.com/index.html">AmazonAdBot</a></strong></li>
 <li><strong dir="ltr"><a href="https://developers.google.com/search/docs/advanced/crawling/overview-google-crawlers">AdSense</a></strong></li>
 <li><strong dir="ltr"><a href="https://www.oracle.com/corporate/acquisitions/grapeshot/crawler.html">Oracle Data Cloud Crawler</a></strong></li>
</ul></div>

##### <div dir="rtl">"protect_frontend"<br /></div>
<div dir="rtl"><ul>
 <li>يحدد ما إذا كانت الحماية التي توفرها عادة CIDRAM يجب أن تطبق لfront-end. صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li>
</ul></div>

##### <div dir="rtl">"disable_webfonts"<br /></div>
<div dir="rtl"><ul>
 <li>هل تريد تعطيل ويبفونتس؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li>
</ul></div>

##### <div dir="rtl">"maintenance_mode"<br /></div>
<div dir="rtl"><ul>
 <li>هل تريد تمكين وضع الصيانة؟ صحيح/True = نعم؛ زائفة/False = لا [افتراضي]. تعطيل كل شيء بخلاف front-end. قد تكون مفيدة أحيانا عند تحديث نظام إدارة المحتوى والأطر وما إلى ذلك.</li>
</ul></div>

##### <div dir="rtl">"default_algo"<br /></div>
<div dir="rtl"><ul>
 <li>يحدد الخوارزمية التي سيتم استخدامها لكل كلمات المرور والجلسات المستقبلية. خيارات: PASSWORD_DEFAULT (افتراضي)، PASSWORD_BCRYPT، PASSWORD_ARGON2I (يتطلب PHP >= 7.2.0)، PASSWORD_ARGON2ID (يتطلب PHP >= 7.3.0).</li>
</ul></div>

##### <div dir="rtl">"statistics"<br /></div>
<div dir="rtl"><ul>
 <li>هل تريد تتبع إحصاءات استخدام CIDRAM؟ صحيح/True = نعم؛ زائفة/False = لا [افتراضي].</li>
</ul></div>

##### <div dir="rtl">"force_hostname_lookup"<br /></div>
<div dir="rtl"><ul>
 <li>فرض بحث اسم المضيف؟ صحيح/True = نعم؛ زائفة/False = لا [افتراضي]. يتم إجراء عمليات البحث عن اسم المضيف عادة على أساس "حسب الحاجة"، ولكن يمكن إجبارها على جميع الطلبات. وقد يكون القيام بذلك مفيدا كوسيلة لتوفير معلومات أكثر تفصيلا في السجلات، ولكن قد يكون له أيضا أثر سلبي طفيف على الأداء.</li>
</ul></div>

##### <div dir="rtl">"allow_gethostbyaddr_lookup"<br /></div>
<div dir="rtl"><ul>
 <li>السماح بعمليات البحث gethostbyaddr عندما يكون UDP غير متوفر؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li>
 <li>ملاحظة: قد لا يعمل البحث عن <code dir="ltr">IPv6</code> بشكل صحيح على بعض أنظمة <code dir="ltr">32-bit</code>.</li>
</ul></div>

##### <div dir="rtl">"hide_version"<br /></div>
<div dir="rtl"><ul>
 <li>إخفاء معلومات الإصدار من السجلات وإخراج الصفحة؟ صحيح/True = نعم؛ زائفة/False = لا [افتراضي].</li>
</ul></div>

##### <div dir="rtl">"empty_fields"<br /></div>
<div dir="rtl"><ul>
 <li>كيف يجب على CIDRAM التعامل مع الحقول الفارغة عند التسجيل وعرض معلومات أحداث المنع؟ "include" = تضمين حقول فارغة. "omit" = احذف الحقول الفارغة [افتراضي].</li>
</ul></div>

##### <div dir="rtl">"log_sanitisation"<br /></div>
<div dir="rtl"><ul>
 <li>عند استخدام صفحة سجلات الواجهة الأمامية لعرض بيانات السجل، تقوم CIDRAM بتعقيم بيانات السجل قبل عرضها، لحماية المستخدمين من هجمات XSS والتهديدات المحتملة الأخرى التي قد تحتوي عليها بيانات السجل. ومع ذلك، بشكل افتراضي، لا يتم تعقيم البيانات أثناء التسجيل. هذا لضمان الحفاظ على بيانات السجل بدقة، للمساعدة في أي تحليل شرعي قد يكون ضروريًا في المستقبل. ومع ذلك، في حالة محاولة المستخدم قراءة بيانات السجل باستخدام أدوات خارجية، وإذا لم تقم تلك الأدوات الخارجية بعملية الصرف الصحي الخاصة بها، فقد يتعرض المستخدم لهجمات XSS. إذا لزم الأمر، يمكنك تغيير السلوك الافتراضي باستخدام توجيه التكوين هذا. True = قم بتعقيم البيانات عند تسجيلها (يتم الاحتفاظ بالبيانات بدقة أقل، لكن خطر XSS أقل). False = لا تقم بتعقيم البيانات عند تسجيلها (يتم الاحتفاظ البيانات بشكل أكثر دقة، ولكن خطر XSS أعلى) [افتراضي].</li>
</ul></div>

##### <div dir="rtl">"disabled_channels"<br /></div>
<div dir="rtl"><ul>
 <li>يمكن استخدام هذا لمنع CIDRAM من استخدام قنوات معينة عند إرسال الطلبات (على سبيل المثال، عند التحديث، عند جلب بيانات تعريف المكون، إلخ).</li>
 <li><em>الخيارات المتاحة: <code dir="ltr">GitHub,BitBucket,Codeberg,GoogleDNS</code></em></li>
</ul></div>

##### <div dir="rtl">"default_timeout"<br /></div>
<div dir="rtl"><ul>
 <li>المهلة الافتراضية لاستخدامها للطلبات الخارجية؟ الافتراضي = 12 ثانية.</li>
</ul></div>

##### <div dir="rtl">"config_imports"<br /></div>
<div dir="rtl"><ul>
 <li>قائمة ملفات محددة بفواصل لاستيرادها إلى التكوين الافتراضي لـ CIDRAM. يتم ملؤها عادةً بصفحة التحديثات عند تنشيط المكونات التي تحتاج إليها عند الضرورة. في معظم الحالات، يمكن تجاهله.</li>
</ul></div>

##### <div dir="rtl">"events"<br /></div>
<div dir="rtl"><ul>
 <li>يتم تحميل الملفات المدرجة هنا مباشرة بعد ملف معالجات الأحداث. يتم ملؤها عادةً بصفحة التحديثات عند تنشيط المكونات التي تحتاج إليها عند الضرورة. في معظم الحالات، يمكن تجاهله.</li>
</ul></div>

#### <div dir="rtl">"signatures" (التصنيف)<br /></div>
<div dir="rtl">تكوين التوقيعات.<br /><br /></div>

##### <div dir="rtl">"ipv4"<br /></div>
<div dir="rtl"><ul>
 <li>وهناك قائمة من الملفات توقيع عناوين IPv4 التي CIDRAM يجب أن تحاول معالجة، مفصولة بفواصل. يمكنك إضافة إدخالات هنا إذا كنت ترغب في تضمين الملفات توقيع الإصدار IPv4 إضافية إلى CIDRAM.</li>
</ul></div>

##### <div dir="rtl">"ipv6"<br /></div>
<div dir="rtl"><ul>
 <li>وهناك قائمة من الملفات توقيع عناوين IPv6 التي CIDRAM يجب أن تحاول معالجة، مفصولة بفواصل. يمكنك إضافة إدخالات هنا إذا كنت ترغب في تضمين الملفات توقيع الإصدار IPv6 إضافية إلى CIDRAM.</li>
</ul></div>

##### <div dir="rtl">"block_attacks"<br /></div>
<div dir="rtl"><ul>
 <li>منع CIDRs المرتبطة بالهجمات وحركة المرور غير الطبيعية الأخرى؟ على سبيل المثال، عمليات فحص المنافذ والقرصنة والتحقيق في نقاط الضعف، وما إلى ذلك. عندما يكون ذلك ممكنا، عموما، وهذا ينبغي دائما أن يتم تعيين إلى true.</li>
</ul></div>

##### <div dir="rtl">"block_cloud"<br /></div>
<div dir="rtl"><ul>
 <li>منع CIDRs التي تم تحديدها على أنها تنتمي إلى خدمات سحابية/الاستضافة؟ إذا كنت تعمل على خدمة API من موقع الويب الخاص بك، أو إذا كنت تتوقع مواقع أخرى للاتصال موقع الويب الخاص بك، هذا يجب أن يتم تعيين إلى false. إذا لم تقم بذلك، ثم، فإنه يجب تعيين إلى true.</li>
</ul></div>

##### <div dir="rtl">"block_bogons"<br /></div>
<div dir="rtl"><ul>
 <li>منع CIDRs المريخ/bogon؟ إذا كنت تتوقع اتصالات إلى موقع الويب الخاص بك من خلال الشبكة المحلية، هذا يجب أن يتم تعيين إلى false. ان لم، هذا يجب أن يتم تعيين إلى true.</li>
</ul></div>

##### <div dir="rtl">"block_generic"<br /></div>
<div dir="rtl"><ul>
 <li>منع CIDRs الموصى بها عموما للالقائمة السوداء؟ وهذا يشمل أي التوقيعات التي ليست جزءا من الفئات الأخرى.</li>
</ul></div>

##### <div dir="rtl">"block_legal"<br /></div>
<div dir="rtl"><ul>
 <li>منع CIDRs ردا على الالتزامات القانونية؟ لا يجب أن يكون لهذا التوجيه عادة أي تأثير، لأن CIDRAM لا تربط أي CIDR مع "التزامات قانونية"، ولكنها موجودة كإجراء تحكم إضافي لصالح أي ملفات أو وحدات توقيع مخصصة قد تكون موجودة لأسباب قانونية.</li>
</ul></div>

##### <div dir="rtl">"block_malware"<br /></div>
<div dir="rtl"><ul>
 <li>منع CIDRs المرتبطة بالبرامج الضارة؟ وهذا يشمل خوادم C&C، والآلات المصابة، والآلات المستخدمة في توزيع البرامج الضارة، وما إلى ذلك.</li>
</ul></div>

##### <div dir="rtl">"block_proxies"<br /></div>
<div dir="rtl"><ul>
 <li>منع CIDRs التي تم تحديدها على أنها تنتمي إلى خدمات وكيل أو شبكات VPN؟ إذا كنت تحتاج إلى أن يكون المستخدمون قادرين على الوصول إلى موقع الويب الخاص بك من خدمات بروكسي أو شبكات VPN، هذا يجب أن يتم تعيين إلى false. ان لم، هذا يجب تعيين إلى true كوسيلة لتحسين الأمن.</li>
</ul></div>

##### <div dir="rtl">"block_spam"<br /></div>
<div dir="rtl"><ul>
 <li>منع CIDRs التي تم تحديدها على أنها مخاطر البريد المزعج؟ عندما يكون ذلك ممكنا، عموما، وهذا ينبغي دائما أن يتم تعيين إلى true.</li>
</ul></div>

##### <div dir="rtl">"modules"<br /></div>
<div dir="rtl"><ul>
 <li>قائمة الملفات المكون لتحميل بعد التحقق من التوقيعات IPv4/IPv6، مفصولة بفواصل.</li>
</ul></div>

##### <div dir="rtl">"default_tracktime"<br /></div>
<div dir="rtl"><ul>
 <li>كم ثانية لتعقب IP حظرت من قبل وحدات. افتراضي = 604800 (1 أسبوع).</li>
</ul></div>

##### <div dir="rtl">"infraction_limit"<br /></div>
<div dir="rtl"><ul>
 <li>يسمح الحد الأقصى لعدد المخالفات IP يمكن أن تتكبد قبل أن يتم حظره من قبل تتبع IP. افتراضي = 10.</li>
</ul></div>

##### <div dir="rtl">"track_mode"<br /></div>
<div dir="rtl"><ul>
 <li>متى يجب أن تحسب المخالفات؟ زائفة/False = عندما IP تم حظره من قبل وحدات. صحيح/True = عندما IP يتم حظر لأي سبب من الأسباب. افتراضي = زائفة/False.</li>
</ul></div>

##### <div dir="rtl">"tracking_override"<br /></div>
<div dir="rtl"><ul>
 <li>هل تسمح للوحدات النمطية بتجاوز خيارات التتبع؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li>
</ul></div>

#### <div dir="rtl">"recaptcha" و "hcaptcha" (كلاهما يقدم نفس التوجيهات).<br /></div>
<div dir="rtl">إذا كنت ترغب في ذلك، يمكنك تقديم اختبار CAPTCHA للمستخدمين لتمييزهم عن برامج الروبوت أو للسماح لهم باستعادة الوصول في حالة حظرهم. يمكن أن يساعد هذا في التخفيف من الإيجابيات الخاطئة وتقليل حركة المرور الآلية غير المرغوب فيها.<br /><br /></div>

<div dir="rtl"><em>ملحوظة: CAPTCHA يحمي فقط من مكالمات الآلة، وليس ضد المهاجمين البشريين.</em><br /><br /></div>

<div dir="rtl">من أجل reCAPTCHA، للحصول على "site key" و "secret key"، الرجاء الذهاب إلى:<br /></div>
<div dir="rtl"><ul>
 <li><div dir="ltr">https://developers.google.com/recaptcha/</div></li>
</ul></div>

<div dir="rtl">من أجل hCaptcha، للحصول على "site key" و "secret key"، الرجاء الذهاب إلى:<br /></div>
<div dir="rtl"><ul>
 <li><div dir="ltr">https://www.hcaptcha.com/</div></li>
</ul></div>

##### <div dir="rtl">"usemode"<br /></div>
<div dir="rtl"><ul>
 <li>متى يجب تقديم الCAPTCHA؟ ملاحظة: لا تحتاج الطلبات المدرجة في القائمة البيضاء أو التي تم التحقق منها والتي لم يتم حظرها إلى إكمال اختبار CAPTCHA.</li>
</ul></div>

&nbsp; <div dir="rtl" style="display:inline">قيمة</div> | &nbsp; <div dir="rtl">وصف</div>
--:|--:
1 | <div dir="rtl">فقط عندما يتم مسدود، ضمن حدود التواقيع، وليس محظور.</div>
2 | <div dir="rtl">فقط عندما يتم مسدود، ويتم تمييزها خصيصًا للاستخدام، وضمن حدود التواقيع، وليس محظور.</div>
3 | <div dir="rtl">فقط عندما ضمن حدود التواقيع، وليس محظور (بغض النظر عما إذا كان مسدود).</div>
4 | <div dir="rtl">فقط عندما لا يتم مسدود.</div>
5 | <div dir="rtl">فقط عندما لا يتم مسدود، أو عندما يتم تمييزها خصيصًا للاستخدام، وضمن حدود التواقيع، وليس محظور.</div>
&nbsp; <div dir="rtl" style="display:inline">أي قيمة أخرى.</div> | &nbsp; <div dir="rtl">مطلقا!</div>

##### <div dir="rtl">"lockip"<br /></div>
<div dir="rtl"><ul>
 <li>تحدد ما إذا كان التجزئة يجب أن يكون مؤمنا إلى عناوين IP محددة. زائفة/False = الكوكيز والتجزئة يمكن استخدامها عبر عدة عناوين IP (الافتراضي). صحيح/True = الكوكيز والتجزئة لا يمكن استخدامها عبر عدة عناوين IP (وتخوض الكوكيز والتجزئة إلى عناوين IP).</li>
 <li>ملحوظة: "lockip" يتم تجاهل قيمة عندما "lockuser" غير false (آلية لتذكر المستخدمين مختلفة، اعتمادا على هذه القيمة).</li>
</ul></div>

##### <div dir="rtl">"lockuser"<br /></div>
<div dir="rtl"><ul>
 <li>تحدد ما إذا كان اختبار reCAPTCHA/hCaptcha يجب أن يكون مؤمنا لمستخدمين محددين. زائفة/False = الانتهاء من اختبار reCAPTCHA/hCaptcha منح حق الوصول إلى كافة الطلبات من عنوان IP نفسه؛ لا تستخدم الكوكيز والتجزئة؛ بدلا من ذلك، سيتم استخدام قائمة بيضاء IP. صحيح/True = الانتهاء من اختبار reCAPTCHA/hCaptcha منح حق الوصول فقط إلى المستخدم؛ تستخدم الكوكيز والتجزئة لتذكر المستخدم؛ لا يتم استخدام القائمة البيضاء IP (الافتراضي).</li>
</ul></div>

##### <div dir="rtl">"sitekey"<br /></div>
<div dir="rtl"><ul>
 <li>يمكن العثور على هذه القيمة في لوحة التحكم الخاصة بخدمة CAPTCHA.</li>
</ul></div>

##### <div dir="rtl">"secret"<br /></div>
<div dir="rtl"><ul>
 <li>يمكن العثور على هذه القيمة في لوحة التحكم الخاصة بخدمة CAPTCHA.</li>
</ul></div>

##### <div dir="rtl">"expiry"<br /></div>
<div dir="rtl"><ul>
 <li>عدد الساعات لنتذكر حالات اختبار CAPTCHA. الافتراضي = 720 (١ شهر).</li>
</ul></div>

##### <div dir="rtl">"logfile"<br /></div>
<div dir="rtl"><ul>
 <li>تسجيل جميع محاولات اختبار CAPTCHA؟ إذا كانت الإجابة بنعم، حدد اسم لاستخدامه في ملف السجل. ان لم، ترك هذا الحقل فارغا.</li>
</ul></div>

<div dir="rtl"><em>نصيحة مفيدة: إن أردت، يمكنك إلحاق تاريخ/المعلومات في الوقت إلى أسماء ملفات السجل من خلال تضمين هذه في اسم: "{yyyy}" لمدة عام كامل، "{yy}" لمدة عام يختصر، "{mm}" لمدة شهر، "{dd}" ليوم واحد، "{hh}" لمدة ساعة (راجع الأمثلة أدناه).</em><br /><br /></div>

`logfile='captcha.{yyyy}-{mm}-{dd}-{hh}.txt'`

##### <div dir="rtl">"signature_limit"<br /></div>
<div dir="rtl"><ul>
 <li>الحد الأقصى لعدد التوقيعات المسموح بها قبل سحب عرض CAPTCHA. افتراضي = 1.</li>
</ul></div>

##### <div dir="rtl">"api"<br /></div>
<div dir="rtl"><ul>
 <li>أي API لاستخدام؟</li>
</ul></div>

```
api
├─recaptcha
│ ├─V2
│ └─Invisible
└─hcaptcha
  ├─V1
  └─Invisible
```

<div dir="rtl">ملاحظة للمستخدمين في الاتحاد الأوروبي: عند تهيئة CIDRAM لاستخدام ملفات تعريف الارتباط (على سبيل المثال، عندما يكون "lockuser" صحيحا/true)، يتم عرض تحذير ملف تعريف الارتباط بشكل بارز على الصفحة وفقا ل <a href="https://www.cookielaw.org/the-cookie-law/">تشريعات ملفات تعريف الارتباط في الاتحاد الأوروبي</a>. ومع ذلك، عند استخدام invisible API، CIDRAM يحاول إكمال CAPTCHA للمستخدم تلقائيا، وعندما ناجحة، وهذا يمكن أن يؤدي إلى إعادة تحميل الصفحة ويتم إنشاء ملف تعريف الارتباط دون إعطاء المستخدم الوقت الكافي ل في الواقع رؤية تحذير ملف تعريف الارتباط.<em></em><br /><br /></div>

##### <div dir="rtl">"show_cookie_warning"<br /></div>
<div dir="rtl"><ul>
 <li>إظهار تحذير ملف تعريف الارتباط؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li>
</ul></div>

<div dir="rtl"><em>تتم إضافة توجيه التكوين هذا حسب الطلب، للمستخدمين الذين يرغبون في تعطيل تحذير ملف تعريف الارتباط الذي يظهر عادة بجانب CAPTCHA (على سبيل المثال، للمساعدة في إخفاء أي إشارة إلى أن CIDRAM قيد الاستخدام). ومع ذلك، فإنني أنصح بشدة أن يحافظ عليه معظم المستخدمين (خاصة المستخدمين في الاتحاد الأوروبي).</em><br /><br /></div>

##### <div dir="rtl">"show_api_message"<br /></div>
<div dir="rtl"><ul>
 <li>إظهار رسالة API؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li>
</ul></div>

<div dir="rtl"><em>يشير هذا إلى أي رسائل إضافية غير ضرورية يتم عرضها عند حظر أحد الطلبات، بخلاف تحذير ملف تعريف الارتباط.</em><br /><br /></div>

##### <div dir="rtl">"nonblocked_status_code"<br /></div>
<div dir="rtl"><ul>
 <li>ما هو رمز الحالة الذي يجب استخدامه عند عرض CAPTCHA للطلبات غير المحظورة؟</li>
</ul></div>

<div dir="rtl">القيم المدعومة حاليًا:<br /><br /></div>

رمز حالة | رسالة الحالة
---|---
`200` | `200 OK`
`403` | `403 Forbidden`
`418` | `418 I'm a teapot`
`429` | `429 Too Many Requests`
`451` | `451 Unavailable For Legal Reasons`

#### <div dir="rtl">"legal" (التصنيف)<br /></div>
<div dir="rtl">التكوين المتعلق بالمتطلبات القانونية.<br /><br /></div>

<div dir="rtl">لمزيد من المعلومات حول المتطلبات القانونية وكيف يمكن أن يؤثر ذلك على متطلبات التهيئة الخاصة بك، يرجى الرجوع إلى قسم <a href="#user-content-SECTION11">المعلومات القانونية</a> من الوثائق.<br /><br /></div>

##### <div dir="rtl">"pseudonymise_ip_addresses"<br /></div>
<div dir="rtl"><ul>
 <li>إخفاء عناوين IP عند كتابة السجلات؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li>
</ul></div>

##### <div dir="rtl">"omit_ip"<br /></div>
<div dir="rtl"><ul>
 <li>حذف عناوين IP من السجلات؟ صحيح/True = نعم؛ زائفة/False = لا [افتراضي]. ملاحظة: يصبح "pseudonymise_ip_addresses" مكررًا عندما يكون "omit_ip" هو "true".</li>
</ul></div>

##### <div dir="rtl">"omit_hostname"<br /></div>
<div dir="rtl"><ul>
 <li>حذف أسماء المضيف من السجلات؟ صحيح/True = نعم؛ زائفة/False = لا [افتراضي].</li>
</ul></div>

##### <div dir="rtl">"omit_ua"<br /></div>
<div dir="rtl"><ul>
 <li>حذف وكلاء المستخدم من السجلات؟ صحيح/True = نعم؛ زائفة/False = لا [افتراضي].</li>
</ul></div>

##### <div dir="rtl">"privacy_policy"<br /></div>
<div dir="rtl"><ul>
 <li>عنوان سياسة الخصوصية ذات الصلة ليتم عرضها في تذييل الصفحات التي تم إنشاؤها. حدد عنوان URL، أو اتركه فارغًا لتعطيله.</li>
</ul></div>

#### <div dir="rtl">"template_data" (التصنيف)<br /></div>
<div dir="rtl">توجيهات/متغيرات القوالب والمواضيع.<br /><br /></div>

<div dir="rtl">تتعلق البيانات بقالب انتاج HTML تستخدم لتوليد "تم رفض الوصول" الرسالة المعروضة للمستخدمين على تحميل ملف حجبها. إذا كنت تستخدم موضوعات مخصصة لـ CIDRAM، هو مصدر إخراج HTML من ملف <code dir="ltr">template_custom.html</code> وغيرها، ويتم الحصول على إخراج HTML من ملف <code dir="ltr">template.html</code>. يتم تحليل المتغيرات الخطية لهذا القسم من ملف التكوين إلى إخراج HTML عن طريق استبدال أي أسماء المتغيرات محاط بواسطة الأقواس الموجودة داخل إخراج HTML مع البيانات المتغيرة المناظرة. فمثلا، أين <code dir="ltr">foo="bar"</code>، أي مثيل <code dir="ltr">&lt;p&gt;{foo}&lt;/p&gt;</code> وجدت داخل إخراج HTML ستصبح <code dir="ltr">&lt;p&gt;bar&lt;/p&gt;</code>.<br /><br /></div>

##### <div dir="rtl">"theme"<br /></div>
<div dir="rtl"><ul>
 <li>الموضوع الافتراضي لاستخدام CIDRAM.</li>
</ul></div>

##### <div dir="rtl">"magnification"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Magnification"</em></li>
 <li>تكبير الخط. افتراضي = 1.</li>
</ul></div>

##### <div dir="rtl">"css_url"<br /></div>
<div dir="rtl"><ul>
 <li>ملف الصيغة النموذجية للمواضيع مخصصة يستخدم خصائص CSS الخارجية، في حين أن ملف قالب لموضوع الافتراضي يستخدم خصائص CSS الداخلية. لإرشاد CIDRAM لاستخدام ملف النموذجية للمواضيع مخصصة، تحديد عنوان HTTP العام من ملفات CSS موضوع المخصصة لديك باستخدام "css_url" متغير. إذا تركت هذا الحقل فارغا متغير، سوف يقوم CIDRAM باستخدام ملف القالب لموضوع التقصير.</li>
</ul></div>

#### <div dir="rtl">"PHPMailer" (التصنيف)<br /></div>
<div dir="rtl">تكوين PHPMailer.<br /><br /></div>

<div dir="rtl">حاليا، يستخدم CIDRAM PHPMailer فقط من أجل 2FA. إذا لم تستخدم الواجهة الأمامية، أو إذا لم تستخدم 2FA، فيمكنك تجاهل هذه التوجيهات.<br /><br /></div>

##### <div dir="rtl">"event_log"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "EventLog"</em></li>
 <li>ملف لتسجيل جميع الأحداث المتعلقة ب PHPMailer. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li>
</ul></div>

##### <div dir="rtl">"skip_auth_process"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "SkipAuthProcess"</em></li>
 <li>تعيين هذا التوجيه إلى <code dir="ltr">true</code> يرشد PHPMailer لتخطي عملية المصادقة التي تحدث عادة عند إرسال البريد الإلكتروني عبر SMTP. يجب تجنب هذا، لأن تخطي هذه العملية قد يعرض البريد الإلكتروني الصادر إلى هجمات MITM، ولكنه قد يكون ضروريًا في الحالات التي تمنع فيها هذه العملية من اتصال PHPMailer بخادم SMTP.</li>
</ul></div>

##### <div dir="rtl">"enable_two_factor"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Enable2FA"</em></li>
 <li>يحدد هذا التوجيه ما إذا كان سيتم استخدام 2FA للحسابات front-end أم لا.</li>
</ul></div>

##### <div dir="rtl">"host"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Host"</em></li>
 <li>مضيف SMTP الذي يستخدم للبريد الإلكتروني الصادر.</li>
</ul></div>

##### <div dir="rtl">"port"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Port"</em></li>
 <li>رقم المنفذ المراد استخدامه للبريد الإلكتروني الصادر. افتراضي = 587.</li>
</ul></div>

##### <div dir="rtl">"smtp_secure"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "SMTPSecure"</em></li>
 <li>البروتوكول المستخدم عند إرسال البريد الإلكتروني عبر SMTP (TLS أو SSL).</li>
</ul></div>

##### <div dir="rtl">"smtp_auth"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "SMTPAuth"</em></li>
 <li>يحدد هذا التوجيه ما إذا كنت تريد مصادقة جلسات SMTP (يجب ألا يغير هذا عادة).</li>
</ul></div>

##### <div dir="rtl">"username"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Username"</em></li>
 <li>اسم المستخدم لاستخدامه عند إرسال البريد الإلكتروني عبر SMTP.</li>
</ul></div>

##### <div dir="rtl">"password"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Password"</em></li>
 <li>كلمة المرور لاستخدامها عند إرسال البريد الإلكتروني عبر SMTP.</li>
</ul></div>

##### <div dir="rtl">"set_from_address"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "setFromAddress"</em></li>
 <li>عنوان المرسل للاستشهاد عند إرسال البريد الإلكتروني عبر SMTP.</li>
</ul></div>

##### <div dir="rtl">"set_from_name"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "setFromName"</em></li>
 <li>اسم المرسل للاستشهاد عند إرسال البريد الإلكتروني عبر SMTP.</li>
</ul></div>

##### <div dir="rtl">"add_reply_to_address"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "addReplyToAddress"</em></li>
 <li>عنوان الرد للاستشهاد عند إرسال البريد الإلكتروني عبر SMTP.</li>
</ul></div>

##### <div dir="rtl">"add_reply_to_name"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "addReplyToName"</em></li>
 <li>اسم الرد للاستشهاد عند إرسال البريد الإلكتروني عبر SMTP.</li>
</ul></div>

#### <div dir="rtl">"rate_limiting" (التصنيف)<br /></div>
<div dir="rtl">توجيهات اختيارية للتهيئة للحد من المعدل.<br /><br /></div>

<div dir="rtl">تم تنفيذ هذه الميزة في CIDRAM بسبب طلبات من العديد من المستخدمين. ومع ذلك، لأنها ليست ذات صلة بالغرض المقصود أصلاً لـ CIDRAM، على الأرجح لن تكون مطلوبة من قبل معظم المستخدمين. إذا كنت تحتاج بشكل خاص إلى CIDRAM للتعامل مع تحديد معدل لموقعك على الويب، فقد تكون هذه الميزة مفيدة لك. ومع ذلك، هناك بعض الأمور المهمة التي يجب وضعها في الاعتبار:</div>
<div dir="rtl"><ul>
 <li>هذه الميزة، مثل جميع ميزات CIDRAM الأخرى، لن تعمل إلا للصفحات المحمية بواسطة CIDRAM. لذلك، لا يمكن تحديد أصول موقع الويب إذا لم يتم توجيهها من خلال CIDRAM.</li>
 <li>إذا كنت قادرًا على استخدام المكون الخادم، أو cPanel، أو بعض أدوات الشبكة الأخرى لفرض قيود على المعدل، يجب عليك استخدام ذلك بدلاً من CIDRAM للحد من المعدل.</li>
 <li>إذا أراد مستخدم معين، بعد أن يكون محدودًا، الاستمرار في الوصول إلى موقع الويب الخاص بك، في معظم الحالات، سيكون من السهل جدًا عليهم التحايل على معدل الحد (على سبيل المثال، إذا قاموا بتغيير عنوان IP الخاص بهم، أو إذا كانوا يستخدمون بروكسي أو VPN، وافتراض أنك قمت بتكوين CIDRAM لعدم حظر الوكلاء و VPN، أو أن CIDRAM ليس على علم بالبروكسي أو VPN الذي يستخدمونه).</li>
 <li>يمكن أن يكون الحد من المعدل مزعجًا جدًا للمستخدمين. قد يكون من الضروري إذا كان النطاق الترددي المتوفر محدودًا جدًا، وإذا اكتشفت وجود بعض مصادر الزيارات المحددة، والتي لم يتم حظرها بالفعل، والتي تستهلك معظم النطاق الترددي المتوفر لديك. إذا لم يكن ضروريا على الرغم من ذلك، ربما ينبغي تجنبها.</li>
 <li>قد تخاطر أحيانًا بمنع نفسك أو المستخدمين الشرعيين.</li>
</ul></div>

<div dir="rtl">إذا كنت تشعر بأنك لست بحاجة إلى CIDRAM لفرض قيود على معدل لموقعك على الويب، فاحفظ التوجيهات أدناه المحددة كقيمها الافتراضية. خلاف ذلك، يمكنك تغيير قيمها لتناسب احتياجاتك.<br /><br /></div>

##### <div dir="rtl">"max_bandwidth"<br /></div>
<div dir="rtl"><ul>
 <li>أقصى قدر من عرض النطاق الترددي المسموح به خلال فترة السماح. عندما يتم تجاوزت، يتم تمكين حدود السعر للطلبات المستقبلية. تعمل القيمة 0 على تعطيل هذا النوع من تحديد السرعة. افتراضي = 0KB.</li>
</ul></div>

##### <div dir="rtl">"max_requests"<br /></div>
<div dir="rtl"><ul>
 <li>الحد الأقصى لعدد الطلبات المسموح بها خلال فترة السماح. عندما يتم تجاوزت، يتم تمكين حدود السعر للطلبات المستقبلية. تعمل القيمة 0 على تعطيل هذا النوع من تحديد السرعة. افتراضي = 0.</li>
</ul></div>

##### <div dir="rtl">"precision_ipv4"<br /></div>
<div dir="rtl"><ul>
 <li>الدقة المستخدمة عند مراقبة استخدام IPv4. قيمة تعكس حجم كتلة CIDR. تعيين إلى 32 للحصول على أفضل دقة. افتراضي = 32.</li>
</ul></div>

##### <div dir="rtl">"precision_ipv6"<br /></div>
<div dir="rtl"><ul>
 <li>الدقة المستخدمة عند مراقبة استخدام IPv6. قيمة تعكس حجم كتلة CIDR. تعيين إلى 128 للحصول على أفضل دقة. افتراضي = 128.</li>
</ul></div>

##### <div dir="rtl">"allowance_period"<br /></div>
<div dir="rtl"><ul>
 <li>عدد الساعات لمراقبة الاستخدام. افتراضي = 0.</li>
</ul></div>

##### <div dir="rtl">"exceptions"<br /></div>
<div dir="rtl"><ul>
 <li>استثناءات (بمعنى آخر، الطلبات التي لا ينبغي أن تكون محدودة). له تأثير فقط عند تمكين الحد.</li>
 <li><em>الخيارات المتاحة: <code dir="ltr">Whitelisted,Verified</code></em></li>
</ul></div>

#### <div dir="rtl">"supplementary_cache_options" (التصنيف)<br /></div>
<div dir="rtl">خيارات ذاكرة التخزين المؤقت التكميلية.<br /><br /></div>

##### <div dir="rtl">"prefix"<br /></div>
<div dir="rtl"><ul>
 <li>سيتم إضافة القيمة المحددة هنا إلى جميع مفاتيح إدخال ذاكرة التخزين المؤقت. فارغ بشكل افتراضي. عند وجود عدة عمليات تثبيت على نفس الخادم، يمكن أن يكون ذلك مفيدًا للحفاظ على ذاكرة التخزين المؤقت منفصلة عن بعضها البعض.</li>
</ul></div>

##### <div dir="rtl">"enable_apcu"<br /></div>
<div dir="rtl"><ul>
 <li>يحدد هذا ما إذا كنت تريد استخدام APCu للتخزين المؤقت. افتراضي = False (زائفة).</li>
</ul></div>

##### <div dir="rtl">"enable_memcached"<br /></div>
<div dir="rtl"><ul>
 <li>يحدد هذا ما إذا كنت تريد استخدام Memcached للتخزين المؤقت. افتراضي = False (زائفة).</li>
</ul></div>

##### <div dir="rtl">"enable_redis"<br /></div>
<div dir="rtl"><ul>
 <li>يحدد هذا ما إذا كنت تريد استخدام Redis للتخزين المؤقت. افتراضي = False (زائفة).</li>
</ul></div>

##### <div dir="rtl">"enable_pdo"<br /></div>
<div dir="rtl"><ul>
 <li>يحدد هذا ما إذا كنت تريد استخدام PDO للتخزين المؤقت. افتراضي = False (زائفة).</li>
</ul></div>

##### <div dir="rtl">"memcached_host"<br /></div>
<div dir="rtl"><ul>
 <li>قيمة المضيف Memcached. افتراضي = "localhost".</li>
</ul></div>

##### <div dir="rtl">"memcached_port"<br /></div>
<div dir="rtl"><ul>
 <li>قيمة منفذ Memcached. افتراضي = "11211".</li>
</ul></div>

##### <div dir="rtl">"redis_host"<br /></div>
<div dir="rtl"><ul>
 <li>قيمة المضيف Redis. افتراضي = "localhost".</li>
</ul></div>

##### <div dir="rtl">"redis_port"<br /></div>
<div dir="rtl"><ul>
 <li>قيمة منفذ Redis. افتراضي = "6379".</li>
</ul></div>

##### <div dir="rtl">"redis_timeout"<br /></div>
<div dir="rtl"><ul>
 <li>Redis قيمة المهلة. افتراضي = "2.5".</li>
</ul></div>

##### <div dir="rtl">"pdo_dsn"<br /></div>
<div dir="rtl"><ul>
 <li>قيمة PDO DSN. افتراضي = "<code dir="ltr">mysql:dbname=cidram;host=localhost;port=3306</code>".</li>
</ul></div>

<div dir="rtl"><em>(نرى: <a href="#user-content-HOW_TO_USE_PDO">ما هو "PDO DSN"؟ كيف يمكنني استخدام PDO مع CIDRAM؟</a>)</em><br /><br /></div>

##### <div dir="rtl">"pdo_username"<br /></div>
<div dir="rtl"><ul>
 <li>PDO اسم المستخدم.</li>
</ul></div>

##### <div dir="rtl">"pdo_password"<br /></div>
<div dir="rtl"><ul>
 <li>PDO كلمه السر.</li>
</ul></div>

---


### <div dir="rtl">٧. <a name="SECTION7"></a>شكل/تنسيق التوقيع</div>

<div dir="rtl">أنظر أيضا:<br /></div>
<div dir="rtl"><ul>
 <li><a href="#user-content-WHAT_IS_A_SIGNATURE">ما هو "التوقيع"؟</a></li>
</ul></div>

#### <div dir="rtl">٧.٠ مبادئ (بالنسبة إلى ملفات التوقيع)<br /><br /></div>

<div dir="rtl">جميع التوقيعات من IPv4 تتبع هذا الشكل: "xxx.xxx.xxx.xxx/yy [وظيفة] [معامل]".<br /></div>
<div dir="rtl"><ul>
 <li>"xxx.xxx.xxx.xxx" يمثل بداية كتلة CIDR (المجموعة ثمانية من عنوان IP الأول).</li>
 <li>"yy" تمثل حجم الكتلة [١-٣٢].</li>
 <li>"[وظيفة]" يرشد النصي ما يجب القيام به مع التوقيع.</li>
 <li>"[معامل]" تمثل أي معلومات إضافية قد تكون مطلوبة من قبل "[وظيفة]".</li>
</ul></div>

<div dir="rtl">جميع التوقيعات من IPv6 تتبع هذا الشكل: <code dir="ltr">"xxxx:xxxx:xxxx:xxxx::xxxx/yy"</code> [وظيفة] [معامل]".<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">"xxxx:xxxx:xxxx:xxxx::xxxx"</code> يمثل بداية كتلة CIDR (المجموعة ثمانية من عنوان IP الأول). تدوين كامل وتدوين يختصر على حد سواء مقبول (كل يجب أن تلتزم المعايير تدوين الإصدار IPv6، ولكن مع استثناء واحد: عنوان IPv6 لا يمكن أبدا أن تبدأ مع اختصار عند استخدامها في التوقيع لهذا النصي، بسبب الطريقة التي يتم بناؤها CIDRs؛ فمثلا،<code dir="ltr">"::1/128"</code> ينبغي التعبير، عند استخدامها في توقيع، كما<code dir="ltr">"0::1/128"</code>، و"::0/128" التعبير بأنه<code dir="ltr">"0::/128"</code>).</li>
 <li>"yy" تمثل حجم الكتلة [١-١٢٨].</li>
 <li>"[وظيفة]" يرشد النصي ما يجب القيام به مع التوقيع.</li>
 <li>"[معامل]" تمثل أي معلومات إضافية قد تكون مطلوبة من قبل "[وظيفة]".</li>
</ul></div>

<div dir="rtl">أسطر جديدة يونكس الموصى بها (<code dir="ltr">"%0A"</code>، أو <code dir="ltr">"\n"</code>)! أسطر جديدة أخرى (على سبيل المثال، Windows <code dir="ltr">"%0D%0A"</code> أو أسطر جديدة <code dir="ltr">"\r\n"</code>، Mac <code dir="ltr">"%0D"</code> أو أسطر جديدة <code dir="ltr">"\r"</code>، إلخ) يمكن استخدامها، ولكن لا يفضل. أسطر جديدة تطبيع من قبل البرنامج النصي.<br /><br /></div>

<div dir="rtl">يجب أن يكون تدوين CIDR دقيق. يجب أن أعداد تقسم بالتساوي (على سبيل المثال، من أجل الحيلولة دون<code dir="ltr">"10.128.0.0"-"11.127.255.255"</code>، <code dir="ltr">"10.128.0.0/8"</code> لن تكون صالحة، لكن <code dir="ltr">"10.128.0.0/9"</code> و<code dir="ltr">"11.0.0.0/9"</code> على ما يرام).<br /><br /></div>

<div dir="rtl">أي شيء لذا أوقع الذي يعني أنك يمكن أن تريد بأمان في ملفات توقيعك دون انقطاع دون اقتحام والكتابات التي وضعت البيانات في أي غير الموقعة، و سيتم تجاهل رأي ولا كدليل على الاعتراف بأنه بناء الجملة من توقيع الملفات النصي. التعليقات هي ملفات التوقيع مقبولة، وأي تنسيق خاص اللازمة لها. على غرار قذيفة المفضل التجزئة للحصول على تعليق، ولكن لا تفرض أي، يستحق ذلك تماما، فإنه لا يحدث أي فارق أو لم النصي اختيار استخدام التجزئة على غرار قذيفة على تعليقاتكم، ولكن التجزئة على غرار قذيفة استخدام برامج تحرير النصوص واضحة وبيئات التطوير يساعد على تسليط الضوء وقعت أجزاء من الملفات بشكل صحيح (وبالتالي، يمكن أن تساعد باعتبارها المساعدات البصرية في حالة وضع تحرير التجزئة).<br /><br /></div>

<div dir="rtl">القيم الممكنة من "[وظيفة]" هي كما يلي:<br /></div>
<div dir="rtl"><ul>
 <li>Run</li>
 <li>Whitelist</li>
 <li>Greylist</li>
 <li>Deny</li>
</ul></div>

<div dir="rtl">إذا تم استخدام "Run"، عندما يتم تشغيل توقيع، السيناريو سوف محاولة لتنفيذ برنامج نصي خارجية (استخدام علامة "require_once" بيان)، التي تحددها قيمة "[معامل]" (الدليل يجب أن يكون الدليل "/vault/" البرنامج النصي؛ راجع الأمثلة أدناه).<br /><br /></div>

`127.0.0.0/8 Run example.php`

<div dir="rtl">يمكن أن يكون هذا مفيدا لتشغيل كود PHP معين لبعض عناوين IP و CIDRs.<br /><br /></div>

<div dir="rtl">إذا تم استخدام "Whitelist"، عندما يتم تشغيل توقيع، البرنامج النصي إعادة تعيين كافة المكتشفة والانتهاء من عملية. "[معامل]" يتم تجاهل (راجع الأمثلة أدناه).<br /><br /></div>

`127.0.0.1/32 Whitelist`

<div dir="rtl">إذا تم استخدام "Greylist"، عندما يتم تشغيل توقيع، البرنامج النصي إعادة تعيين كافة المكتشفة وانتقل إلى ملف التوقيع المقبل. "[معامل]" يتم تجاهل (راجع الأمثلة أدناه).<br /><br /></div>

`127.0.0.1/32 Greylist`

<div dir="rtl">إذا تم استخدام "Deny"، عندما يتم تشغيل توقيع، إن لم يكن في القائمة البيضاء، سيتم رفض الوصول. "Deny" يستخدم لمنع عنوان IP أو CIDR.<br /><br /></div>

<div dir="rtl">"[معامل]" قيمة لديها دعم L10N.<br /><br /></div>

<div dir="rtl">الكلمات المختزلة المتاحة هي:<br /></div>
<div dir="rtl"><ul>
 <li>Attacks</li>
 <li>Bogon</li>
 <li>Cloud</li>
 <li>Generic</li>
 <li>Legal</li>
 <li>Malware</li>
 <li>Proxy</li>
 <li>Spam</li>
</ul></div>

#### <div dir="rtl">٧.١ علامات<br /><br /></div>

##### <div dir="rtl">٧.١.٠ علامات القسم<br /><br /></div>

<div dir="rtl">يمكنك تحديد أقسام مختلفة مثل هذا (راجع الأمثلة أدناه).<br /><br /></div>

```
# القسم 1.
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: القسم ١
```

<div dir="rtl">خطوط مزدوجة يمكن استخدامها لأقسام منفصلة (راجع الأمثلة أدناه).<br /><br /></div>

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: القسم ١
```

<div dir="rtl">في المثال أعلاه<code dir="ltr">"1.2.3.4/32"</code> و<code dir="ltr">"2.3.4.5/32"</code> وصفت بأنها "IPv4"، بينما<code dir="ltr">"4.5.6.7/32"</code> و<code dir="ltr">"5.6.7.8/32"</code> وصفت بأنها "القسم 1".<br /><br /></div>

<div dir="rtl">ويمكن تطبيق المنطق نفسه لفصل الأنواع الأخرى من العلامات أيضا.<br /><br /></div>

<div dir="rtl">على وجه الخصوص، يمكن أن تكون علامات القسم مفيدة جدا لتصحيح الأخطاء عندما تحدث ايجابيات كاذبة، من خلال توفير وسيلة سهلة من موقع المصدر الدقيق للمشكلة، ويمكن أن تكون مفيدة جدا لتصفية إدخالات ملف السجل عند عرض ملفات السجل عبر صفحة سجلات الواجهة الأمامية (يمكن النقر على أسماء الأقسام عبر صفحة سجلات الواجهة الأمامية ويمكن استخدامها كمعايير تصفية). إذا تم حذف علامات الأقسام لبعض التواقيع المحددة، عندما يتم تشغيل تلك التوقيعات، يستخدم CIDRAM اسم ملف التوقيع مع نوع عنوان إب المحظور (IPv4 أو IPv6) كمرجع، وبالتالي، الأقسام القسم اختيارية تماما. ويمكن التوصية في بعض الحالات، على سبيل المثال، عندما تكون ملفات التوقيع مسماة بشكل غامض أو عندما يكون من الصعب على نحو آخر تحديد مصدر التوقيعات بشكل واضح مما يتسبب في حظر الطلب.<br /><br /></div>

##### <div dir="rtl">٧.١.١ علامات انتهاء الصلاحية<br /><br /></div>

<div dir="rtl">في المثال التالي، سوف التوقيعات تنتهي بعد مرور بعض الوقت:<br /><br /></div>

```
# القسم ١.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

<div dir="rtl">لن يتم تشغيل التوقيعات منتهية الصلاحية على أي طلب، بغض النظر عن ما.<br /><br /></div>

##### <div dir="rtl">٧.١.٢ علامات المنشأ<br /><br /></div>

<div dir="rtl">إذا كنت ترغب في تحديد بلد المنشأ لبعض التوقيع معين، يمكنك القيام بذلك باستخدام "علامة المنشأ". تقبل علامة الأصل شفرة "<a href="https://ar.wikipedia.org/wiki/%D8%A3%D9%8A%D8%B2%D9%88_3166-1_%D8%AD%D8%B1%D9%81%D9%8A-2">أيزو 3166-1 حرفي-2</a>" المقابلة لبلد المنشأ للتوقيعات التي تنطبق عليها. يجب أن تكون هذه الرموز مكتوبة في الحالة العليا (أقل حالة أو حالة مختلطة لن تجعل بشكل صحيح). عند استخدام علامات المنشأ، يتم إضافته إلى إدخال حقل السجل "سبب الحظر" لأي طلبات تم حظرها نتيجة للتوقيعات التي يتم تطبيق العلامة عليها.<br /><br /></div>

<div dir="rtl">إذا تم تثبيت مكون "flags CSS" الاختياري، عند عرض ملفات السجل عبر صفحة سجلات الواجهة الأمامية، يتم استبدال المعلومات الملحقة بعلامات المنشأ بعلامة البلد المقابل لتلك المعلومات. هذه المعلومات، سواء في شكلها الخام أو كعلامة بلد، يمكن النقر عليها، وعند النقر عليها، سيتم تصفية إدخالات السجل عن طريق إدخالات سجل تعريف أخرى مماثلة (مما يسمح على نحو فعال للأشخاص الذين يدخلون إلى صفحة السجلات بالترشيح عن طريق بلد المنشأ).<br /><br /></div>

<div dir="rtl">ملاحظة: من الناحية الفنية، هذا ليس أي شكل من أشكال تحديد الموقع الجغرافي، وذلك لأنه لا ينطوي على البحث عن أي معلومات محددة تتعلق عناوين بروتوكول الإنترنت الواردة، وإنما بدلا من ذلك، يسمح ببساطة لنا أن ينص صراحة بلد المنشأ لأي طلبات تم حظرها من قبل محددة التوقيعات. علامات المنشأ المتعددة مسموح بها في نفس قسم التوقيع.<br /><br /></div>

<div dir="rtl">مثال افتراضي:<br /><br /></div>

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

<div dir="rtl">يمكن استخدام أي علامات بالتزامن، وتكون جميع العلامات اختيارية (راجع الأمثلة أدناه).<br /><br /></div>

```
# القسم المثال.
1.2.3.4/32 Deny Generic
Origin: US
Tag: القسم المثال
Expires: 2016.12.31
```

##### <div dir="rtl">٧.١.٣ علامات احترام<br /><br /></div>

<div dir="rtl">عندما يتم تثبيت أعداد كبيرة من ملفات التوقيع واستخدامها بنشاط، يمكن أن تصبح عمليات التثبيت معقدة للغاية، وقد تكون هناك بعض التواقيع التي تتداخل. في هذه الحالات، لضمان أن التوقيعات المتعددة والمتداخلة لا يتم تشغيلها جميعًا أثناء أحداث الحظر، علامات احترام يمكن استخدامه لتأجيل أقسام محددة للتوقيع في الحالات التي يتم فيها تثبيت بعض ملفات التوقيع المحددة واستخدامها بشكل نشط. قد يكون هذا مفيدًا في الحالات التي يتم فيها تحديث بعض التوقيعات بشكل متكرر أكثر من غيرها، وذلك لتأجيل التواقيع الأقل تحديثًا بشكل متكرر لصالح التوقيعات الأكثر تكرارًا.<br /><br /></div>

<div dir="rtl">يتم استخدام علامات احترام بشكل مشابه للأنواع الأخرى من العلامات. يجب أن تتطابق قيمة العلامة مع ملف التوقيع المثبت والمستخدم بشكل فعال ليتم تأجيله.<br /><br /></div>

<div dir="rtl">مثال:<br /><br /></div>

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

#### <div dir="rtl">٧.١.٤ علامات الملف الشخصي<br /><br /></div>

<div dir="rtl">توفر علامات الملف الشخصي وسيلة تعرض معلومات إضافية في صفحة اختبار IP، ويمكن الاستفادة منها من خلال الوحدات النمطية والقواعد المساعدة لسلوك أكثر تعقيدًا واتخاذ قرارات دقيقة.<br /><br /></div>

<div dir="rtl">يتم استخدام علامات الملف الشخصي بشكل مشابه لأنواع أخرى من العلامات. يمكن استخدام قيم علامات الملف الشخصي كشرط للوحدات النمطية والقواعد المساعدة. يمكن أن توفر علامات ملف التعريف قيمًا متعددة عن طريق فصل هذه القيم بفاصلة منقوطة. لا يرى المستخدم النهائي أبدًا قيم علامات الملف الشخصي.<br /><br /></div>

<div dir="rtl">مثال:<br /><br /></div>

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### <div dir="rtl">٧.٢ YAML<br /><br /></div>

#### <div dir="rtl">٧.٢.٠ أساسيات YAML<br /><br /></div>

<div dir="rtl">باستخدام YAML العلامات اختياري كلي (أي، إذا كنت تستخدم ذلك، هو اختيارك)، وغير قادرة على الاستفادة من معظم التكوين.<br /><br /></div>

<div dir="rtl">في CIDRAM، يتم تحديد YAML باستخدام ثلاث شرطات ("---")، و انهم إنهاء باستخدام اثنين أسطر جديدة. مثال التالي:<br /><br /></div>

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

##### <div dir="rtl">٧.٢.١ كيفية "تحمل علامة" أقسام توقيع للاستخدام مع reCAPTCHA/hCaptcha<br /><br /></div>

<div dir="rtl">عندما "usemode" هو 2 أو 5، من أجل دلالة أقسام توقيع للاستخدام مع اختبار reCAPTCHA/hCaptcha، تشير إلى أن في YAML لهذا القسم التوقيع (راجع الأمثلة أدناه).<br /><br /></div>

<pre dir="ltr">
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Tag: CAPTCHA Marked
---
recaptcha:
 enabled: true
hcaptcha:
 enabled: true
</pre>

#### <div dir="rtl">٧.٣ معلومات اضافية<br /><br /></div>

##### <div dir="rtl">٧.٣.٠ تجاهل أقسام التوقيع<br /><br /></div>

<div dir="rtl">إذا كنت تريد CIDRAM تجاهل تماما بعض المقاطع، يمكنك استخدام ملف "ignore.dat" لتحديد المقاطع التي ليمكن تجاهلها. على سطر جديد، اكتب "Ignore"، متبوعا بمسافة، يليه اسم المقطع ليمكن تجاهله (راجع الأمثلة أدناه).<br /><br /></div>

```
Ignore القسم ١
```

<div dir="rtl">ويمكن تحقيق ذلك أيضًا من خلال صفحة "لقائمة الأقسام" CIDRAM لfront-end.<br /><br /></div>

##### <div dir="rtl">٧.٣.١ القواعد المساعدة<br /><br /></div>

<div dir="rtl">إذا كنت تشعر أن كتابة ملفات التوقيع المخصصة الخاصة بك أو وحدات مخصصة معقدة للغاية بالنسبة لك، قد يكون بديل أبسط هو استخدام صفحة "القواعد المساعدة" الخاصة بـ CIDRAM لfront-end. من خلال تحديد الخيارات المناسبة وتحديد تفاصيل حول أنواع معينة من الطلبات، يمكنك توجيه CIDRAM إلى كيفية الرد على تلك الطلبات. يتم تنفيذ "القواعد المساعدة" بعد الانتهاء من جميع ملفات التوقيع والوحدات النمطية بالفعل التنفيذ.<br /><br /></div>

#### <div dir="rtl">٧.٤ <a name="MODULE_BASICS"></a>مبادئ (للوحدات)<br /><br /></div>

<div dir="rtl">وحدات يمكن استخدامها لتوسيع وظائف CIDRAM، أداء مهام إضافية، أو معالجة منطق إضافي.<br /><br /></div>

<div dir="rtl">لأن يتم كتابة وحدات كملفات PHP، إذا كنت على دراية كافية مع مصدر برنامج CIDRAM، يمكنك هيكلة وحدات المكون التواقيع ولكن تريد (في إطار ما هو ممكن مع فب).<br /><br /></div>

<div dir="rtl"><em>ملحوظة: إذا كنت غير مريح العمل مع التعليمات البرمجية PHP، كتابة الوحدات الخاصة بك لا ينصح.</em><br /><br /></div>

<div dir="rtl">يتم توفير بعض الوظائف من قبل CIDRAM التي ينبغي أن تجعل من أبسط وأسهل لكتابة وحدات الخاصة بك. وترد أدناه معلومات عن هذه الوظيفة.<br /><br /></div>

#### <div dir="rtl">٧.٥ المكون نمطية<br /><br /></div>

##### <div dir="rtl">٧.٥.٠ <code dir="ltr">$Trigger</code></div>

<div dir="rtl">وعادة ما تكتب تواقيع المكون مع <code dir="ltr">$Trigger</code>. في معظم الحالات، هذا الإغلاق سيكون أكثر أهمية من أي شيء آخر لغرض كتابة وحدات.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$Trigger</code> يقبل ٤ المعلمات: <code dir="ltr">$Condition</code>، <code dir="ltr">$ReasonShort</code>، <code dir="ltr">$ReasonLong</code> (اختياري)، <code dir="ltr">$DefineOptions</code> (اختياري).<br /><br /></div>

<div dir="rtl">يتم تقييم <code dir="ltr">$Condition</code>، وإذا كان "صحيح" (<code dir="ltr">true</code>)، التوقيع نشط. إذا كان "خاطئة" (<code dir="ltr">false</code>)، التوقيع غير نشط. <code dir="ltr">$Condition</code> عادة ما تحتوي على التعليمات البرمجية PHP التي يجب منع الطلبات.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonShort</code> في حقل "سبب الحظر" عندما يكون التوقيع نشطا.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonLong</code> هي رسالة اختيارية يتم عرضها للمستخدم عند حظرها، لشرح سبب حظرها. يستخدم الرسالة القياسية "سبب الحظر" عند حذفها.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$DefineOptions</code> عبارة عن صفيف اختياري يحتوي على أزواج المفاتيح/القيم التي تحدد خيارات التكوين الخاصة بمثيل الطلب. سيتم تطبيق خيارات التهيئة عندما يكون التوقيع نشطا.<br /><br /></div>

<div dir="rtl">ترجع <code dir="ltr">$Trigger</code> صحيح (<code dir="ltr">true</code>) عندما يكون التوقيع نشطا و خاطئة (<code dir="ltr">false</code>) عندما لا يكون.<br /><br /></div>

<div dir="rtl">لاستخدام هذا الإغلاق في المكون النمطية الخاصة بك، تذكر أولا أن ترثه من النطاق الأصلي:<br /><br /></div>

```PHP
$Trigger = $CIDRAM['Trigger'];
```

##### <div dir="rtl">٧.٥.١ <code dir="ltr">$Bypass</code></div>

<div dir="rtl">وعادة ما تكتب الالتفافية التوقيع مع <code dir="ltr">$Bypass</code>.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$Bypass</code> يقبل ٣ المعلمات: <code dir="ltr">$Condition</code>، <code dir="ltr">$ReasonShort</code>، <code dir="ltr">$DefineOptions</code> (اختياري).<br /><br /></div>

<div dir="rtl">يتم تقييم <code dir="ltr">$Condition</code>، وإذا كان "صحيح" (<code dir="ltr">true</code>)، الالتفافية نشط. إذا كان "خاطئة" (<code dir="ltr">false</code>)، الالتفافية غير نشط. <code dir="ltr">$Condition</code> عادة ما تحتوي على رمز PHP التي يجب عدم منع الطلبات.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonShort</code> في حقل "سبب الحظر" عندما يكون الالتفافية نشطا.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$DefineOptions</code> عبارة عن صفيف اختياري يحتوي على أزواج المفاتيح/القيم التي تحدد خيارات التكوين الخاصة بمثيل الطلب. سيتم تطبيق خيارات التهيئة عندما يكون الالتفافية نشطا.<br /><br /></div>

<div dir="rtl">ترجع <code dir="ltr">$Bypass</code> صحيح (<code dir="ltr">true</code>) عندما يكون الالتفافية نشطا و خاطئة (<code dir="ltr">false</code>) عندما لا يكون.<br /><br /></div>

<div dir="rtl">لاستخدام هذا الإغلاق في المكون النمطية الخاصة بك، تذكر أولا أن ترثه من النطاق الأصلي:<br /><br /></div>

```PHP
$Bypass = $CIDRAM['Bypass'];
```

##### <div dir="rtl">٧.٥.٢ <code dir="ltr">"$CIDRAM['DNS-Reverse']"</code></div>

<div dir="rtl">يمكن استخدام هذا لجلب اسم المضيف لعنوان IP. إذا كنت ترغب في إنشاء المكون لمنع أسماء المضيفين، قد يكون هذا الإغلاق مفيدا.<br /><br /></div>

<div dir="rtl">مثال:<br /><br /></div>

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

#### <div dir="rtl">٧.٦ المكون المتغيرات<br /><br /></div>

<div dir="rtl">الوحدات النمطية تنفذ ضمن نطاقها الخاص، وأي متغيرات محددة من قبل المكون نمطية، لن تكون في متناول وحدات أخرى، أو إلى السيناريو الأصل، إلا إذا كانت مخزنة في <code dir="ltr">$CIDRAM</code> مجموعة (يتم مسح كل شيء آخر بعد انتهاء تنفيذ المكون).<br /><br /></div>

<div dir="rtl">فيما يلي بعض المتغيرات الشائعة التي قد تكون مفيدة للالمكون النمطية الخاصة بك:<br /><br /></div>

&nbsp; <div dir="rtl" style="display:inline">وصف</div> | <div dir="rtl">متغير</div>
----|----
&nbsp; <div dir="rtl" style="display:inline">التاريخ والوقت الحاليان.</div> | `$CIDRAM['BlockInfo']['DateTime']`
&nbsp; <div dir="rtl" style="display:inline">عنوان IP للطلب الحالي.</div> | `$CIDRAM['BlockInfo']['IPAddr']`
&nbsp; <div dir="rtl" style="display:inline">إصدار النص البرمجي CIDRAM.</div> | `$CIDRAM['BlockInfo']['ScriptIdent']`
&nbsp; <div dir="rtl" style="display:inline">الاستعلام عن الطلب الحالي.</div> | `$CIDRAM['BlockInfo']['Query']`
&nbsp; <div dir="rtl" style="display:inline">المحيل للطلب الحالي (إذا كان موجودا).</div> | `$CIDRAM['BlockInfo']['Referrer']`
&nbsp; <div dir="rtl" style="display:inline">وكيل المستخدم (user agent) للطلب الحالي.</div> | `$CIDRAM['BlockInfo']['UA']`
&nbsp; <div dir="rtl" style="display:inline">وكيل المستخدم (user agent) للطلب الحالي (في حالة أقل).</div> | `$CIDRAM['BlockInfo']['UALC']`
&nbsp; <div dir="rtl" style="display:inline">الرسالة المراد عرضها للمستخدم عند حظرها.</div> | `$CIDRAM['BlockInfo']['ReasonMessage']`
&nbsp; <div dir="rtl" style="display:inline">عدد التوقيعات التي أدت إلى الطلب الحالي.</div> | `$CIDRAM['BlockInfo']['SignatureCount']`
&nbsp; <div dir="rtl" style="display:inline">المعلومات المرجعية عن أي توقيعات أثارت للطلب الحالي.</div> | `$CIDRAM['BlockInfo']['Signatures']`
&nbsp; <div dir="rtl" style="display:inline">المعلومات المرجعية عن أي توقيعات أثارت للطلب الحالي.</div> | `$CIDRAM['BlockInfo']['WhyReason']`

---


### <div dir="rtl">٨. <a name="SECTION8"></a>مشاكل التوافق المعروفة</div>

<div dir="rtl">تم العثور على الحزم والمنتجات التالية لتكون غير متوافقة مع CIDRAM:</div>
<div dir="rtl"><ul>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/52">Endurance Page Cache</a></strong></li>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/80">Mix.com</a></strong></li>
</ul></div>

<div dir="rtl">تم توفير وحدات لضمان توافق الحزم والمنتجات التالية مع CIDRAM:</div>
<div dir="rtl"><ul>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/56">BunnyCDN</a></strong></li>
</ul></div>

<div dir="rtl"><em>انظر أيضا: <a href="https://maikuolan.github.io/Compatibility-Charts/">مخططات التوافق</a>.</em><br /><br /></div>

---


### <div dir="rtl">٩. <a name="SECTION9"></a>أسئلة وأجوبة (FAQ)</div>

<div dir="rtl"><ul>
 <li><a href="#user-content-WHAT_IS_A_SIGNATURE">ما هو "التوقيع"؟</a></li>
 <li><a href="#user-content-WHAT_IS_A_CIDR">ما هو "CIDR"؟</a></li>
 <li><a href="#user-content-WHAT_IS_A_FALSE_POSITIVE">ما هو "إيجابية خاطئة"؟</a></li>
 <li><a href="#user-content-BLOCK_ENTIRE_COUNTRIES">يمكن CIDRAM منع الدول؟</a></li>
 <li><a href="#user-content-SIGNATURE_UPDATE_FREQUENCY">عدد المرات التي يتم تحديثها التوقيعات؟</a></li>
 <li><a href="#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO">لقد واجهت مشكلة! أنا لا أعرف ما يجب القيام به! الرجاء المساعدة!</a></li>
 <li><a href="#user-content-BLOCKED_WHAT_TO_DO">لقد تم حظر من موقع على شبكة الانترنت! الرجاء المساعدة!</a></li>
 <li><a href="#user-content-MINIMUM_PHP_VERSION">أريد استخدام CIDRAM (قبل v2) مع نسخة PHP كبار السن من 5.4.0؛ يمكنك أن تساعد؟</a></li>
 <li><a href="#user-content-MINIMUM_PHP_VERSION_V2">أريد استخدام CIDRAM (v2) مع نسخة PHP كبار السن من 7.2.0؛ يمكنك أن تساعد؟</a></li>
 <li><a href="#user-content-PROTECT_MULTIPLE_DOMAINS">هل يمكنني استخدام تثبيت CIDRAM واحد لحماية نطاقات متعددة؟</a></li>
 <li><a href="#user-content-PAY_YOU_TO_DO_IT">أنا لا أريد أن تضيع الوقت مع تثبيت هذا أو ضمان أنه يعمل لموقع الويب الخاص بي؛ يمكنني دفع لك أن تفعل ذلك بالنسبة لي؟</a></li>
 <li><a href="#user-content-HIRE_FOR_PRIVATE_WORK">هل يمكنني توظيفك أو أي من مطوري هذا المشروع للعمل الخاص؟</a></li>
 <li><a href="#user-content-SPECIALIST_MODIFICATIONS">أنا بحاجة إلى تعديلات متخصصة، والتخصيصات، الخ؛ يمكنك أن تساعد؟</a></li>
 <li><a href="#user-content-ACCEPT_OR_OFFER_WORK">أنا مطور، مصمم موقع، أو مبرمج. هل يمكنني قبول أو عرض العمل المتعلق بهذا المشروع؟</a></li>
 <li><a href="#user-content-WANT_TO_CONTRIBUTE">أريد أن أساهم في المشروع؛ هل يمكنني فعل هذا؟</a></li>
 <li><a href="#user-content-CRON_TO_UPDATE_AUTOMATICALLY">هل يمكنني استخدام cron لتحديث تلقائيا؟</a></li>
 <li><a href="#user-content-WHAT_ARE_INFRACTIONS">ما هي "المخالفات"؟</a></li>
 <li><a href="#user-content-BLOCK_HOSTNAMES">هل يمكن لأسماء المضيفين في CIDRAM حظر؟</a></li>
 <li><a href="#ما-الذي-يمكنني-استخدامه-لـ-default_dns">ما الذي يمكنني استخدامه لـ "default_dns"؟</a></li>
 <li><a href="#user-content-PROTECT_OTHER_THINGS">هل يمكنني استخدام CIDRAM لحماية الأشياء بخلاف مواقع الويب (مثل خوادم البريد الإلكتروني، FTP، SSH، IRC، إلخ)؟</a></li>
 <li><a href="#user-content-CDN_CACHING_PROBLEMS">هل تحدث مشكلات إذا كنت أستخدم CIDRAM في نفس وقت استخدام خدمات CDN أو خدمات التخزين المؤقت؟</a></li>
 <li><a href="#user-content-DDOS_ATTACKS">هل CIDRAM حماية موقعي على الويب ضد هجمات DDoS؟</a></li>
 <li><a href="#user-content-CHANGE_COMPONENT_SORT_ORDER">عندما أقوم بتنشيط أو إلغاء تنشيط الوحدات النمطية أو ملفات التوقيع عبر صفحة التحديثات، فإنها تقوم بترتيبها أبجديًا في التكوين. هل يمكنني تغيير الطريقة التي يتم تصنيفها بها؟</a></li>
 <li><a href="#user-content-HOW_TO_USE_PDO">ما هو "PDO DSN"؟ كيف يمكنني استخدام PDO مع CIDRAM؟</a></li>
 <li><a href="#user-content-BLOCK_CRON">CIDRAM يحظر cronjobs؛ كيف يمكن اصلاح هذا؟</a></li>
</ul></div>

#### <div dir="rtl"><a name="WHAT_IS_A_SIGNATURE"></a>ما هو "التوقيع"؟<br /><br /></div>

<div dir="rtl">في CIDRAM، يشير "التوقيع" إلى البيانات التي تعمل كمعرف، لشيء معين أننا نبحث عنه. عادة عنوان IP أو CIDR، يتضمن بعض التعليمات لCIDRAM، مثل أفضل طريقة للرد عندما يواجه ما نحن نبحث عنه. توقيع نموذجي لCIDRAM يبدو شيئا من هذا القبيل:<br /><br /></div>

<div dir="rtl">بالنسبة إلى "ملفات التوقيع":<br /><br /></div>

`1.2.3.4/32 Deny Generic`

<div dir="rtl">بالنسبة إلى "الوحدات النمطية":<br /><br /></div>

```PHP
$Trigger(strpos($CIDRAM['BlockInfo']['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

<div dir="rtl">ملاحظة: التوقيعات ل "ملفات التوقيع"، والتوقيعات ل "وحدات"، ليست هي نفس الشيء.<em></em><br /><br /></div>

<div dir="rtl">في كثير من الأحيان (ولكن ليس دائما)، سيتم تجميع التواقيع معا في مجموعات، تشكيل "أقسام التوقيع"، وغالبا ما تكون مصحوبة بتعليقات، وترميز، والبيانات الوصفية ذات الصلة. ويمكن استخدام هذا لتوفير سياق إضافي.<br /><br /></div>

#### <div dir="rtl"><a name="WHAT_IS_A_CIDR"></a>ما هو "CIDR"؟<br /><br /></div>

<div dir="rtl">"CIDR" هو اختصار ل "Classless Inter-Domain Routing". ("توجيه بين المجالات لافئويا") <em>[<a href="https://ar.wikipedia.org/wiki/%D8%AA%D9%88%D8%AC%D9%8A%D9%87_%D8%A8%D9%8A%D9%86_%D8%A7%D9%84%D9%85%D8%AC%D8%A7%D9%84%D8%A7%D8%AA_%D9%84%D8%A7%D9%81%D8%A6%D9%88%D9%8A%D8%A7">١</a>، <a href="https://whatismyipaddress.com/cidr">٢</a>]</em>. يستخدم هذا الاختصار كجزء من اسم هذه الحزمة، "CIDRAM"، وهو اختصار ل "Classless Inter-Domain Routing Access Manager" (توجيه بين المجالات لافئويا وصول مدير).<br /><br /></div>

<div dir="rtl">ومع ذلك، في سياق CIDRAM (مثل، ضمن هذه الوثائق، في المناقشات ذات الصلة، أو ضمن بيانات اللغة)، عند ذكر "CIDR" (المفرد) أو "CIDRs" (الجمع)، المعنى المقصود لدينا هو الشبكات الفرعية، معربا عن ذلك باستخدام تدوين سيدر. والسبب في ذلك هو أنه يمكن التعبير عن الشبكات الفرعية بطرق مختلفة مختلفة. لذلك يمكن اعتبار CIDRAM "مدير النفاذ إلى الشبكة الفرعية".<br /><br /></div>

<div dir="rtl">وهذا التفسير، والسياق المقدم، ينبغي أن يساعد على حل أي غموض.<br /><br /></div>

#### <div dir="rtl"><a name="WHAT_IS_A_FALSE_POSITIVE"></a>ما هو "إيجابية خاطئة"؟<br /><br /></div>

<div dir="rtl">المصطلح "إيجابية خاطئة" (<em>بدلا من ذلك: "خطأ إيجابية خاطئة"؛ "انذار خاطئة"</em>؛ الإنجليزية: <em>false positive</em>; <em>false positive error</em>; <em>false alarm</em>)، وصف ببساطة، بشكل عام، يستخدم عند اختبار حالة، للإشارة إلى نتائج هذا الاختبار، عندما تكون النتائج إيجابية (أي، تحديد حالة أن يكون "إيجابية"، أو "صحيح")، ولكن من المتوقع أن تكون (أو كان ينبغي أن يكون) سلبي (أي، الحالة، في الواقع، هو "سلبي"، أو "خاطئة"). "إيجابية خاطئة" ويمكن اعتبار التناظرية من "الذئب الباكي" (حيث لحالة يجري اختبارها هو ما إذا كان هناك ذئب بالقرب من القطيع، الحالة هو "خاطئة" في أنه لا يوجد الذئب بالقرب من القطيع، و الحالة يقال بأنها "إيجابية" بواسطة الراعي عن طريق الدعوة "الذئب، الذئب")، أو التناظرية من الفحص الطبي حيث المريض يتم تشخيص المرض، عندما تكون في واقع، ليس لديهم المرض.<br /><br /></div>

<div dir="rtl">بعض المصطلحات ذات الصلة هي "إيجابية صحيح"، "سلبي صحيح" و "سلبي خاطئة". "إيجابية صحيح" هو عندما تكون نتائج الاختبار والحالة الفعلية للحالة على حد سواء صحيح (أو "إيجابية")، و "سلبي صحيح" هو عندما تكون نتائج الاختبار والحالة الفعلية للحالة على حد سواء خاطئة (أو "سلبي")؛ "إيجابية صحيح" أو "سلبي صحيح" ويعتبر أن تكون "الاستدلال الصحيح". نقيض ل "إيجابية خاطئة" هو "سلبي خاطئة"؛ "سلبي خاطئة" هو عندما تكون النتائج سلبي (أي، تحديد حالة أن يكون "سلبي"، أو "خاطئة")، ولكن من المتوقع أن تكون (أو كان ينبغي أن يكون) إيجابية (أي، الحالة، في الواقع، هو "إيجابية"، أو "صحيح").<br /><br /></div>

<div dir="rtl">في سياق CIDRAM، هذه المصطلحات تشير إلى التوقيعات CIDRAM و ما/منهم أنهم منع. عندما CIDRAM يمنع عنوان IP نظرا لتوقيع سيئة، قديمة أو غير صحيحة، ولكن لا ينبغي أن تفعل ذلك، أو عندما يفعل ذلك لأسباب خاطئة، نشير إلى هذا الحدث باعتباره "إيجابية خاطئة". عندما CIDRAM يفشل لمنع عنوان IP التي كان ينبغي أن سدت، بسبب تهديدات غير متوقعة، التوقيعات المفقودة أو أوجه القصور توقيع، نشير إلى هذا الحدث باعتباره "افتقد" (هذا هو التناظرية من ا "سلبي خاطئة").<br /><br /></div>

<div dir="rtl">هذا يمكن تلخيصها حسب الجدول أدناه:<br /><br /></div>

&nbsp; <div dir="rtl" style="display:inline">CIDRAM لا ينبغي منع عنوان IP</div> | &nbsp; <div dir="rtl" style="display:inline">CIDRAM يجب منع عنوان IP</div> | &nbsp;
---|---|---
&nbsp; <div dir="rtl" style="display:inline">سلبي صحيح (الاستدلال الصحيح)</div> | <div dir="rtl">افتقد (التناظرية من سلبي خاطئة)</div> | <div dir="rtl"><strong>CIDRAM لا يمنع عنوان IP</strong></div>
&nbsp; <div dir="rtl" style="display:inline"><strong>إيجابية خاطئة</strong></div> | <div dir="rtl">إيجابية صحيح (الاستدلال الصحيح)</div> | <div dir="rtl"><strong>CIDRAM منع عنوان IP</strong></div>

#### <div dir="rtl"><a name="BLOCK_ENTIRE_COUNTRIES"></a>يمكن CIDRAM منع الدول؟<br /><br /></div>

<div dir="rtl">نعم. أسهل طريقة للقيام بذلك هي تثبيت المكون BGPView وتكوينها وفقًا لاحتياجاتك.<br /><br /></div>

#### <div dir="rtl"><a name="SIGNATURE_UPDATE_FREQUENCY"></a>عدد المرات التي يتم تحديثها التوقيعات؟<br /><br /></div>

<div dir="rtl">أنه يختلف. نحن نحاول قدر الإمكان، ولكن نظرا لالتزامات أخرى، حياتنا اليومية، وعدم حصولهم على رواتبهم، تحديث الجدول الزمني الدقيق لا يمكن أن تكون مضمونة. الأولوية لضرورة. ورحب المساعدة دائما.<br /><br /></div>

#### <div dir="rtl"><a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>لقد واجهت مشكلة! أنا لا أعرف ما يجب القيام به! الرجاء المساعدة!</div>
<div dir="rtl"><ul>
 <li>تحقق مما إذا كنت تستخدم أحدث إصدار من البرنامج والتوقيع الملفات.</li>
 <li>قراءة الوثائق. قد تكون هناك إجابات هناك.</li>
 <li>قراءة <strong><a href="https://github.com/CIDRAM/CIDRAM/issues">صفحة المشكلات</a></strong>. قد تكون هناك إجابات هناك.</li>
 <li>لا يوجد حتى الآن إجابات؟ يرجى طلب المساعدة عبر صفحة القضايا.</li>
</ul></div>

#### <div dir="rtl"><a name="BLOCKED_WHAT_TO_DO"></a>لقد تم حظر من موقع على شبكة الانترنت! الرجاء المساعدة!<br /><br /></div>

<div dir="rtl">CIDRAM يمكن أن تتوقف حركة المرور غير المرغوب فيها، ولكن اصحاب المواقع هي المسؤولة عن البت في كيفية استخدام هذه. ويمكننا تصحيح أخطائنا، ولكن في حالات أخرى، ستحتاج إلى الاتصال بأصحاب الموقع ذات الصلة. لا نستطيع أن نفعل أي شيء عن أشياء خارجة عن سيطرتنا.<br /><br /></div>

#### <div dir="rtl"><a name="MINIMUM_PHP_VERSION"></a>أريد استخدام CIDRAM (قبل v2) مع نسخة PHP كبار السن من 5.4.0؛ يمكنك أن تساعد؟<br /><br /></div>

<div dir="rtl">لا. PHP >= 5.4.0 هو الحد الأدنى لمتطلبات CIDRAM < v2.<br /><br /></div>

#### <div dir="rtl"><a name="MINIMUM_PHP_VERSION_V2"></a>أريد استخدام CIDRAM (v2) مع نسخة PHP كبار السن من 7.2.0؛ يمكنك أن تساعد؟<br /><br /></div>

<div dir="rtl">لا. PHP >= 7.2.0 هو الحد الأدنى لمتطلبات CIDRAM v2.<br /><br /></div>

<div dir="rtl"><em>انظر أيضا: <a href="https://maikuolan.github.io/Compatibility-Charts/">مخططات التوافق</a>.</em><br /><br /></div>

#### <div dir="rtl"><a name="PROTECT_MULTIPLE_DOMAINS"></a>هل يمكنني استخدام تثبيت CIDRAM واحد لحماية نطاقات متعددة؟<br /><br /></div>

<div dir="rtl">نعم. يمكن استخدام CIDRAM لحماية نطاقات متعددة. إذا كان التكوين المطلوب مختلفا، للقيام بذلك، إنشاء ملفات تكوين جديدة، واسمه وفقا للنطاقات التي تتطلب الحماية. كمثال، ل <code dir="ltr">"https://www.some-domain.tld/"</code>، أطلق عليه اسما <code dir="ltr">"some-domain.tld.config.ini"</code>. اسم النطاق يأتي من <code dir="ltr">"HTTP_HOST"</code>. يتم تجاهل <code dir="ltr">"www"</code>.<br /><br /></div>

#### <div dir="rtl"><a name="PAY_YOU_TO_DO_IT"></a>أنا لا أريد أن تضيع الوقت مع تثبيت هذا أو ضمان أنه يعمل لموقع الويب الخاص بي؛ يمكنني دفع لك أن تفعل ذلك بالنسبة لي؟<br /><br /></div>

<div dir="rtl">ربما. وينظر في ذلك على أساس كل حالة على حدة. أخبرنا احتياجاتك وما تقدمه. سنخبرك بما إذا كنا نستطيع مساعدتك أم لا.<br /><br /></div>

#### <div dir="rtl"><a name="HIRE_FOR_PRIVATE_WORK"></a>هل يمكنني توظيفك أو أي من مطوري هذا المشروع للعمل الخاص؟<br /><br /></div>

<div dir="rtl"><em>راجع اإلجابة أعاله.</em><br /><br /></div>

#### <div dir="rtl"><a name="SPECIALIST_MODIFICATIONS"></a>أنا بحاجة إلى تعديلات متخصصة، والتخصيصات، الخ؛ يمكنك أن تساعد؟<br /><br /></div>

<div dir="rtl"><em>راجع اإلجابة أعاله.</em><br /><br /></div>

#### <div dir="rtl"><a name="ACCEPT_OR_OFFER_WORK"></a>أنا مطور، مصمم موقع، أو مبرمج. هل يمكنني قبول أو عرض العمل المتعلق بهذا المشروع؟<br /><br /></div>

<div dir="rtl">نعم. ترخيصنا لا يحظر هذا.<br /><br /></div>

#### <div dir="rtl"><a name="WANT_TO_CONTRIBUTE"></a>أريد أن أساهم في المشروع؛ هل يمكنني فعل هذا؟<br /><br /></div>

<div dir="rtl">نعم. المساهمة في المشروع هو موضع ترحيب كبير. يرجى الاطلاع على "CONTRIBUTING.md" لمزيد من المعلومات.<br /><br /></div>

#### <div dir="rtl"><a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>هل يمكنني استخدام cron لتحديث تلقائيا؟<br /><br /></div>

<div dir="rtl">نعم. يتم تضمين API في front-end للتفاعل مع صفحة التحديثات عبر النصوص البرمجية الخارجية. وهناك نص منفصل، <a href="https://github.com/Maikuolan/Cronable">Cronable</a>، هو متاح، ويمكن استخدامها من قبل مدير كرون أو كرون جدولة لتحديث هذا وغيرها من الحزم المعتمدة تلقائيا (يوفر هذا البرنامج النصي وثائقه الخاصة).<br /><br /></div>

#### <div dir="rtl"><a name="WHAT_ARE_INFRACTIONS"></a>ما هي "المخالفات"؟<br /><br /></div>

<div dir="rtl">"المخالفات" تحدد متى يجب أن يبدأ حظر IP الذي لم يتم حظره من قبل أي ملفات توقيع محددة لأي طلبات مستقبلية، وهي ترتبط ارتباطا وثيقا ب التتبع IP. توجد بعض الوظائف والوحدات التي تسمح برفض الطلبات لأسباب أخرى غير IP (على سبيل المثال، وجود وكلاء المستخدم [user agents] المقابلة ل سبامبوتس [spambots] أو هاكتولس [hacktools]، استفسارات خطيرة، وهمية DNS، إلخ)، وعندما يحدث ذلك، يمكن أن يحدث "مخالفة". وهي توفر طريقة لتحديد عناوين IP التي تتطابق مع الطلبات غير المرغوب فيها التي قد لا يتم حظرها من قبل أي ملفات توقيع محددة. مخالفات عادة ما تتطابق 1 إلى 1 مع عدد المرات IP يتم حظر، ولكن ليس دائما (قد تتسبب الأحداث الشديدة في قيمة مخالفة أكبر، وإذا كان "track_mode" هو false، لن تحدث المخالفات عند حظرها فقط بواسطة ملفات التوقيع).<br /><br /></div>

#### <div dir="rtl"><a name="BLOCK_HOSTNAMES"></a>هل يمكن لأسماء المضيفين في CIDRAM حظر؟<br /><br /></div>

<div dir="rtl">نعم. يمكن تحقيق ذلك عن طريق إنشاء قاعدة مساعدة أو وحدة مخصصة.<br /><br /></div>

![قاعدة مساعدة لحظر أسماء المضيفين](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <div dir="rtl"><a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>ما الذي يمكنني استخدامه لـ "default_dns"؟<br /><br /></div>

<div dir="rtl">إذا كنت تبحث عن اقتراحات، تقدم <a href=https://public-dns.info/>public-dns.info</a> و <a href=https://servers.opennic.org/>OpenNIC</a> قوائم شاملة لخوادم DNS العامة المعروفة.<br /><br /></div>

IP | المشغل
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

<div dir="rtl"><em>ملحوظة: لا أقدم أي مطالبات أو ضمانات بشأن ممارسات الخصوصية والأمن والفعالية ولا موثوقية أي خدمات DNS، المدرجة أو غير ذلك. يرجى إجراء البحوث الخاصة بك عند اتخاذ القرارات بشأنها.</em><br /><br /></div>

#### <div dir="rtl"><a name="PROTECT_OTHER_THINGS"></a>هل يمكنني استخدام CIDRAM لحماية الأشياء بخلاف مواقع الويب (مثل خوادم البريد الإلكتروني، FTP، SSH، IRC، إلخ)؟<br /><br /></div>

<div dir="rtl">يمكنك (من الناحية القانونية)، ولكن لا ينبغي (من الناحية الفنية؛ من الناحية العملية). ترخيصنا لا يحد من التقنيات التي تنفذ CIDRAM، لكن CIDRAM عبارة عن WAF (تطبيق ويب جدار حماية) وكان الهدف منه حماية مواقع الويب دائمًا. نظرًا لأنه لم يتم تصميمه مع وضع التقنيات الأخرى في الاعتبار، فمن غير المحتمل أن تكون فعالة أو توفر حماية موثوقة للتكنولوجيات الأخرى، ومن المرجح أن يكون التنفيذ صعباً، وأن خطر التعرض للإيجابيات الخاطئة والكشف عن الأخطاء يكون عالياً جداً.<br /><br /></div>

#### <div dir="rtl"><a name="CDN_CACHING_PROBLEMS"></a>هل تحدث مشكلات إذا كنت أستخدم CIDRAM في نفس وقت استخدام خدمات CDN أو خدمات التخزين المؤقت؟<br /><br /></div>

<div dir="rtl">ربما. يعتمد هذا على طبيعة الخدمة المعنية وكيفية استخدامك لها. بشكل عام، إذا كنت تقوم فقط بالتخزين المؤقت لأصول ثابتة (الصور، CSS، إلخ؛ أي شيء لا يتغير بشكل عام بمرور الوقت)، فلا يجب أن تكون هناك أية مشكلات. قد تكون هناك مشكلات على الرغم من ذلك، إذا كنت تقوم بتخزين البيانات في ذاكرة التخزين المؤقت التي عادة ما يتم إنشاؤها بشكل ديناميكي عند طلبها، أو إذا كنت تخبئ نتائج طلبات POST مؤقتًا (هذا من شأنه أن يجعل موقعك على الويب وبيئته ثابتًا تمامًا، ومن غير المرجح أن يوفر CIDRAM أي فائدة ذات معنى في بيئة ساكنة تمامًا). قد يكون هناك أيضًا متطلبات تهيئة محددة لـ CIDRAM، بناءً على نوع CDN أو خدمة التخزين المؤقت التي تستخدمها (ستحتاج إلى التأكد من تكوين CIDRAM بشكل صحيح لـ CDN أو خدمة التخزين المؤقت التي تستخدمها). قد يؤدي الفشل في تكوين CIDRAM بشكل صحيح إلى وجود إشكاليات خاطئة معضلة إلى حد كبير وعمليات الكشف المفقودة.<br /><br /></div>

#### <div dir="rtl"><a name="DDOS_ATTACKS"></a>هل CIDRAM حماية موقعي على الويب ضد هجمات DDoS؟<br /><br /></div>

<div dir="rtl">إجابة مختصرة: لا.<br /><br /></div>

<div dir="rtl">بتفاصيل اكثر: سيساعد CIDRAM في الحد من تأثير حركة المرور غير المرغوب فيها على موقعك على الويب (وبالتالي تقليل تكاليف النطاق الترددي لموقع الويب الخاص بك)، وعلى أجهزتك (على سبيل المثال، قدرة الخادم على معالجة الطلبات وتقديمها)، ويمكن أن يساعد على تقليل مختلف الآثار السلبية المحتملة المرتبطة بالزيارات غير المرغوب فيها. ومع ذلك، هناك أمران مهمان يجب تذكرهما لفهم هذا السؤال.<br /><br /></div>

<div dir="rtl">أولا، CIDRAM هي حزمة PHP، وبالتالي تعمل في الجهاز حيث يتم تثبيت PHP. وهذا يعني أن CIDRAM يمكنه فقط رؤية طلب ما وحظره بعد استلام الخادم له بالفعل. ثانيًا، يجب أن يعمل تخفيف DDoS الفعال على تصفية الطلبات قبل أن تصل إلى الخادم المستهدف بهجوم DDoS. من الناحية المثالية، يجب اكتشاف هجمات DDoS وتخفيفها بواسطة حلول قادرة على إسقاط أو إعادة توجيه حركة المرور المرتبطة بالهجمات، قبل أن تصل إلى الخادم المستهدف في المقام الأول.<br /><br /></div>

<div dir="rtl">ويمكن تنفيذ ذلك باستخدام حلول الأجهزة المخصصة، والحلول القائمة على السحابة مثل خدمات التخفيف المخصصة لخدمة DDoS، وتوجيه DNS الخاص بالنطاق من خلال شبكات مقاومة DDoS، والترشيح المستند إلى السحابة، أو مزيج من ذلك. على أي حال، فإن هذا الموضوع معقد بعض الشىء بحيث لا يمكن تفسيره بشكل كامل مع مجرد فقرة أو فقرتين، لذا أوصي بإجراء المزيد من الأبحاث إذا كان هذا موضوعًا تريد دراسته. عندما يتم فهم الطبيعة الحقيقية لهجمات DDoS بشكل صحيح، فإن هذا الجواب سيكون أكثر منطقية.<br /><br /></div>

#### <div dir="rtl"><a name="CHANGE_COMPONENT_SORT_ORDER"></a>عندما أقوم بتنشيط أو إلغاء تنشيط الوحدات النمطية أو ملفات التوقيع عبر صفحة التحديثات، فإنها تقوم بترتيبها أبجديًا في التكوين. هل يمكنني تغيير الطريقة التي يتم تصنيفها بها؟<br /><br /></div>

<div dir="rtl">نعم. إذا كنت بحاجة إلى فرض بعض الملفات للتنفيذ بترتيب معين، فيمكنك إضافة بعض البيانات الاعتباطية قبل أسمائها في توجيه التهيئة حيث يتم إدراجها، مفصولة بنقطتين. عندما تقوم صفحة التحديثات بفرز الملفات في وقت لاحق، ستؤثر هذه البيانات العشوائية المضافة على ترتيب الفرز، مما يؤدي إلى تنفيذها وفقًا للترتيب الذي تريده، دون الحاجة إلى إعادة تسمية أي منها.<br /><br /></div>

<div dir="rtl">على سبيل المثال، بافتراض توجيه تكوين مع الملفات المسرودة كما يلي:<br /><br /></div>

`file1.php,file2.php,file3.php,file4.php,file5.php`

<div dir="rtl">إذا كنت تريد <code dir="ltr">file3.php</code> تنفيذ أولاً، يمكنك إضافة شيء مثل <code dir="ltr">aaa:</code> قبل اسم الملف:<br /><br /></div>

`file1.php,file2.php,aaa:file3.php,file4.php,file5.php`

<div dir="rtl">وبعد ذلك، إذا تم تنشيط ملف جديد، <code dir="ltr">file6.php</code>، فعندما تقوم صفحة التحديثات بفرزها مرة أخرى، يجب أن ينتهي الأمر بهذا الشكل:<br /><br /></div>

`aaa:file3.php,file1.php,file2.php,file4.php,file5.php,file6.php`

<div dir="rtl">نفس الموقف عندما يتم إلغاء تنشيط الملف. وبالعكس، إذا أردت تنفيذ الملف آخر، فيمكنك إضافة شيء مثل <code dir="ltr">zzz:</code> قبل اسم الملف. على أي حال، لن تحتاج إلى إعادة تسمية الملف المعني.<br /><br /></div>

#### <div dir="rtl"><a name="HOW_TO_USE_PDO"></a>ما هو "PDO DSN"؟ كيف يمكنني استخدام PDO مع CIDRAM؟<br /><br /></div>

<div dir="rtl">"PDO" هو اختصار لـ "<a dir="ltr" href="https://www.php.net/manual/en/intro.pdo.php">PHP Data Objects</a>" (كائنات بيانات PHP). يوفر واجهة لـ PHP لتكون قادرة على الاتصال ببعض أنظمة قواعد البيانات التي يشيع استخدامها في مختلف تطبيقات PHP.<br /><br /></div>

<div dir="rtl">"DSN" هو اختصار لـ "<a dir="ltr" href="https://en.wikipedia.org/wiki/Data_source_name">data source name</a>" (اسم مصدر البيانات). يصف "PDO DSN" لـ PDO كيف يجب أن تتصل بقاعدة بيانات.<br /><br /></div>

<div dir="rtl">يوفر CIDRAM خيار استخدام PDO لأغراض التخزين المؤقت. من أجل هذا للعمل بشكل صحيح، ستحتاج إلى تكوين CIDRAM وفقًا لذلك، وتمكين PDO، وإنشاء قاعدة بيانات جديدة لاستخدام لCIDRAM (إذا لم يكن لديك بالفعل قاعدة بيانات لاستخدام لCIDRAM)، وإنشاء جدول جديد في قاعدة البيانات الخاصة بك بما يتوافق مع الهيكل الموصوف أدناه.<br /><br /></div>

<div dir="rtl">عندما يكون اتصال قاعدة البيانات بنجاح، لكن الجدول الضروري غير موجود، فسيحاول إنشاؤه تلقائيًا. ومع ذلك، لم يتم اختبار هذا السلوك على نطاق واسع ولا يمكن ضمان النجاح.<br /><br /></div>

<div dir="rtl">هذا، بالطبع، ينطبق فقط إذا كنت تريد بالفعل أن تستخدم PDO لCIDRAM. إذا كنت سعيدًا بدرجة كافية لاستخدام التخزين المؤقت للملفات (وفقًا للتهيئة الافتراضية لـ CIDRAM)، أو أي من خيارات التخزين المؤقت الأخرى المتوفرة، فلن تحتاج إلى متاعب نفسك في إعداد قواعد البيانات والجداول.<br /><br /></div>

<div dir="rtl">يستخدم الهيكل الموصوف أدناه "cidram" كاسم قاعدة البيانات الخاصة به، ولكن يمكنك استخدام أي اسم تريده لقاعدة البيانات الخاصة بك، طالما يتم نسخ نفس الاسم في تكوين DSN الخاص بك.<br /><br /></div>

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

<div dir="rtl">يجب تكوين توجيه التكوين <code dir="ltr">pdo_dsn</code> الخاص بـ CIDRAM كما هو موضح أدناه.<br /><br /></div>

```
اعتمادًا على برنامج تشغيل قاعدة البيانات المستخدم...
├─4d (تحذير: تجريبي، لم يتم اختباره، غير مستحسن)
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └المضيف للاتصال مع للعثور على قاعدة البيانات
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └اسم قاعدة البيانات المراد استخدامها
│                │              │
│                │              └رقم المنفذ للاتصال بالمضيف مع
│                │
│                └المضيف للاتصال مع للعثور على قاعدة البيانات
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └اسم قاعدة البيانات المراد استخدامها
│    │          │
│    │          └المضيف للاتصال مع للعثور على قاعدة البيانات
│    │
│    └"mssql", "sybase", "dblib": القيم الممكنة
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├يمكن أن يكون الطريق إلى ملف قاعدة البيانات المحلية
│                    │
│                    ├يمكن الاتصال مع المضيف ورقم المنفذ
│                    │
│                    └يجب عليك الرجوع إلى وثائق Firebird إذا كنت تريد استخدام هذا
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └التي فهرستها قاعدة البيانات للتواصل مع
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └التي فهرستها قاعدة البيانات للتواصل مع
├─mysql (الأكثر الموصى بها)
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └رقم المنفذ للاتصال بالمضيف مع
│                 │            │
│                 │            └المضيف للاتصال مع للعثور على قاعدة البيانات
│                 │
│                 └اسم قاعدة البيانات المراد استخدامها
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├يمكن الرجوع إلى قاعدة البيانات المفهرسة المحددة
│               │
│               ├يمكن الاتصال مع المضيف ورقم المنفذ
│               │
│               └يجب عليك الرجوع إلى وثائق Oracle إذا كنت تريد استخدام هذا
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├يمكن الرجوع إلى قاعدة البيانات المفهرسة المحددة
│         │
│         ├يمكن الاتصال مع المضيف ورقم المنفذ
│         │
│         └└يجب عليك الرجوع إلى وثائق ODBC/DB2 إذا كنت تريد استخدام هذا
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └اسم قاعدة البيانات المراد استخدامها
│               │              │
│               │              └رقم المنفذ للاتصال بالمضيف مع
│               │
│               └المضيف للاتصال مع للعثور على قاعدة البيانات
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └المسار إلى ملف قاعدة البيانات المحلية للاستخدام
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └اسم قاعدة البيانات المراد استخدامها
                   │         │
                   │         └رقم المنفذ للاتصال بالمضيف مع
                   │
                   └المضيف للاتصال مع للعثور على قاعدة البيانات
```

<div dir="rtl">إذا لم تكن متأكدًا مما يمكنك استخدامه في جزء معين من DSN، فحاول أولاً معرفة ما إذا كان يعمل كما هو، دون تغيير أي شيء.<br /><br /></div>

<div dir="rtl">لاحظ أن <code dir="ltr">pdo_username</code> و <code dir="ltr">pdo_password</code> يجب أن يكونا نفس اسم المستخدم وكلمة المرور اللذين اخترتهما لقاعدة بياناتك.<br /><br /></div>

#### <div dir="rtl"><a name="BLOCK_CRON"></a>CIDRAM يحظر cronjobs؛ كيف يمكن اصلاح هذا؟<br /><br /></div>

<div dir="rtl">إذا كنت تستخدم ملفًا مخصصًا لأغراض cronjobs، وإذا لم يكن من الضروري استدعاء هذا الملف أثناء طلبات المستخدم العادية (بمعنى، خارج سياق cronjobs)، تتمثل الطريقة الأكثر مباشرة لإصلاح ذلك في ضمان عدم تنفيذ CIDRAM على الإطلاق خلال cronjobs الخاص بك (بمعنى، لا تقم بتوصيل CIDRAM بالملف المسؤول عن معالجة cronjobs الخاص بك).<br /><br /></div>

<div dir="rtl">بدلا من ذلك، إذا كان هذا غير ممكن، لكن عنوان IP الخاص بخادم cron ثابت نسبيًا ويمكن التنبؤ به، يمكنك محاولة إدراج عنوان IP لخادم cron في القائمة البيضاء، عن طريق إنشاء توقيع في القائمة البيضاء في ملف توقيع مخصص، أو عن طريق إنشاء قاعدة مساعدة لإدراجها في القائمة البيضاء. إذا كان عنوان IP لخادم cron يتغير بانتظام ولا يمكن التنبؤ به بشكل خاص، ولكن مع ذلك يبقى من داخل نفس الشبكة الخاصة، يمكنك محاولة إدراج اسم قسم التوقيع المسؤول عن حظره في المقام الأول في ملف <code dir="ltr">ignore.dat</code>.<br /><br /></div>

<div dir="rtl">إذا جربت كل هذه الأفكار ولم يعمل أي منها معك، أو إذا كنت بحاجة إلى مساعدة لمعرفة كيفية القيام بذلك، يمكنك إنشاء issue جديدة في صفحة issues CIDRAM لطلب المساعدة.<br /><br /></div>

---


### <div dir="rtl">١١. <a name="SECTION11"></a>المعلومات القانونية</div>

#### <div dir="rtl">١١.٠ مقدمة القسم<br /><br /></div>

<div dir="rtl">يصف هذا القسم من الوثائق الاعتبارات القانونية الممكنة فيما يتعلق باستخدام الحزمة وتنفيذها، ويوفر بعض المعلومات الأساسية ذات الصلة. قد يكون هذا مهمًا لبعض المستخدمين كوسيلة لضمان التوافق مع أي متطلبات قانونية قد تكون موجودة في البلدان التي يعملون فيها، وقد يحتاج بعض المستخدمين إلى تعديل سياسات موقع الويب الخاصة بهم وفقًا لهذه المعلومات.<br /><br /></div>

<div dir="rtl">أولا، يرجى ندرك أنني (مؤلف حزمة) لست محام، وليس أي نوع من المهنيين القانونيين المؤهلين. لذلك، لست مؤهلاً قانونًا لتقديم المشورة القانونية. أيضا، في بعض الحالات، قد تختلف المتطلبات القانونية بين الدول والاختصاصات المختلفة، وهذه المتطلبات القانونية المتفاوتة قد تكون متناقضة في بعض الأحيان (على سبيل المثال، الدول التي تفضل "<a href="https://ar.wikipedia.org/wiki/%D8%AD%D9%82_%D9%81%D9%8A_%D8%A7%D9%84%D8%AE%D8%B5%D9%88%D8%B5%D9%8A%D8%A9">حقوق الخصوصية</a>" و "<a href="https://ar.wikipedia.org/wiki/%D8%AD%D9%82_%D8%A7%D9%84%D9%85%D8%B1%D8%A1_%D8%A3%D9%86_%D9%8A%D9%86%D8%B3%D9%89">الحق في أن تنسى</a>"، مقارنة بالبلدان التي تفضل "الاحتفاظ بالبيانات"). ضع في اعتبارك أيضًا أن الوصول إلى الحزمة لا يقتصر على بلدان أو ولايات قضائية محددة، وبالتالي، فإن مستخدمي الحزمة من المحتمل أن يكونوا متنوعين جغرافيًا. بالنظر إلى هذه النقاط، فأنا لست في وضع يسمح لي بالإشارة إلى ما يعنيه أن يكون "متوافقة مع القانون" مع الجميع. ومع ذلك، آمل أن تساعدك هذه المعلومات على أن تقرر بنفسك ما يجب عليك القيام به للبقاء ملتزمين قانونًا في سياق الحزمة. إذا كانت لديك أي شكوك بخصوص هذه المعلومات، أو إذا كنت بحاجة إلى مساعدة ومشورة إضافية من منظور قانوني، فإنني أوصيك باستشارة متخصص قانوني مؤهل.<br /><br /></div>

#### <div dir="rtl">١١.١ المسؤولية<br /><br /></div>

<div dir="rtl">كما هو مذكور بالفعل من قبل ترخيص الحزمة، يتم توفير الحزمة دون أي ضمان. وهذا يشمل (على سبيل المثال لا الحصر) كل نطاق المسؤولية. يتم توفير الحزمة لك لراحتك، على أمل أن تكون مفيدة، وأنها سوف توفر بعض الفائدة بالنسبة لك. ومع ذلك، سواء كنت تستخدم أو تنفذ الحزمة، فذلك هو خيارك. لا تضطر إلى استخدام الحزمة أو تنفيذها، ولكن عندما تقوم بذلك، فأنت مسؤول عن هذا القرار. لا أنا ولا أي مساهم آخر في الحزمة مسؤول قانونيًا عن عواقب القرارات التي تتخذها، بصرف النظر عما إذا كانت مباشرة أو غير مباشرة أو ضمنية أو غير ذلك.<br /><br /></div>

#### <div dir="rtl">١١.٢ الأطراف الثالثة<br /><br /></div>

<div dir="rtl">اعتمادا على التكوين الدقيق والتنفيذ، قد تتواصل الحزمة وتتبادل المعلومات مع أطراف ثالثة في بعض الحالات. في بعض السياقات، من خلال بعض السلطات القضائية، يمكن تعريف ذلك على أنه "<a href="https://ar.wikipedia.org/wiki/%D9%85%D8%B9%D9%84%D9%88%D9%85%D8%A7%D8%AA_%D8%B4%D8%AE%D8%B5%D9%8A%D8%A9">معلومات تعريف شخصية</a>".<br /><br /></div>

<div dir="rtl">إن كيفية استخدام هذه المعلومات من قِبل هذه الجهات الخارجية تخضع لسياساتها، وهي خارج نطاق هذه الوثائق. ومع ذلك، في جميع هذه الحالات، يمكن تعطيل مشاركة المعلومات. في جميع هذه الحالات، إذا اخترت تمكينها، تقع على عاتقك مسؤولية البحث عن أي مخاوف قد تكون لديك بشأن الخصوصية والأمان واستخدام هذه المعلومات من قِبل هذه الأطراف الثالثة. إذا وجدت أي شكوك، أو إذا كنت غير راضي عن سلوك هذه الأطراف الثالثة، قد يكون من الأفضل تعطيل كل مشاركة المعلومات مع هذه الأطراف الثالثة.<br /><br /></div>

<div dir="rtl">لغرض الشفافية، يتم وصف نوع المعلومات المشتركة أدناه.<br /><br /></div>

##### <div dir="rtl">١١.٢.٠ بحث اسم المضيف<br /><br /></div>

<div dir="rtl">إذا كنت تستخدم أي ميزات أو وحدات تهدف إلى العمل مع أسماء المضيفين، فيجب أن يكون CIDRAM قادرًا على الحصول على اسم المضيف للطلبات الواردة. عادة، تقوم بذلك عن طريق طلب أسماء المضيف لعنوان IP من خادم DNS، أو عن طريق طلب المعلومات من خلال الوظائف التي يوفرها النظام مباشرة. تنتمي خوادم DNS المحددة افتراضيًا إلى خدمة <a dir="ltr" href="https://dns.google.com/">Google DNS</a> (ولكن هذا يمكن تغييره بسهولة عبر التكوين). يمكن تكوين الخدمات الدقيقة التي يتم الاتصال بها، وتعتمد على كيفية تكوين الحزمة. عند طلب ذلك عبر النظام مباشرة، ستحتاج إلى الاتصال بمسؤول النظام لتحديد الطرق المستخدمة. يمكن منع عمليات البحث عن اسم المضيف في CIDRAM عن طريق تجنب الوحدات المتأثرة أو عن طريق تعديل تكوين الحزمة وفقًا لذلك.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">default_dns</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">search_engine_verification</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">social_media_verification</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">other_verification</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">force_hostname_lookup</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">allow_gethostbyaddr_lookup</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">١١.٢.١ خطوط الويب<br /><br /></div>

<div dir="rtl">بعض السمات المخصصة، واجهة المستخدم القياسية CIDRAM، وصفحة "تم رفض الوصول" قد تستخدم خطوط الويب لأسباب جمالية. يتم تعطيل خطوط الويب بشكل افتراضي. عند التمكين، هناك اتصال مباشر بين متصفح المستخدم ومضيف الويب. قد ينطوي ذلك على نقل معلومات مثل عنوان IP الخاص بالمستخدم، وكيل المستخدم، نظام التشغيل، وغيرها من التفاصيل المتاحة للطلب. تستضيف <a href="https://fonts.google.com/">خدمة خطوط Google</a> معظم خطوط الويب هذه.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">disable_webfonts</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">١١.٢.٢ التحقق من محركات البحث ووسائل الإعلام الاجتماعية<br /><br /></div>

<div dir="rtl">عندما يتم تمكين هذه الخيارات، يحاول CIDRAM التحقق من صحة الطلبات من محركات البحث والشبكات الاجتماعية. للقيام بذلك، فإنه يستخدم خدمة <a dir="ltr" href="https://dns.google.com/">Google DNS</a> لمحاولة حل عناوين IP من أسماء المضيفين لهذه الطلبات الواردة (في هذه العملية، تتم مشاركة أسماء المضيفين لهذه الطلبات الواردة مع الخدمة).<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">search_engine_verification</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">social_media_verification</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">other_verification</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">١١.٢.٣ CAPTCHA<br /><br /></div>

<div dir="rtl">يتم دعم reCAPTCHA و hCaptcha بواسطة CIDRAM. تتطلب مفاتيح API لكي تعمل بشكل صحيح. يتم تعطيلها افتراضيًا، ولكن يمكن تمكينها عن طريق تكوين مفاتيح واجهة برمجة التطبيقات المطلوبة. عند التمكين، قد يحدث اتصال بين الخدمة و CIDRAM أو متصفح المستخدم. قد يتضمن ذلك نقل معلومات مثل عنوان IP للمستخدم ووكيل المستخدم ونظام التشغيل.<br /><br /></div>

##### <div dir="rtl">١١.٢.٤ STOP FORUM SPAM<br /><br /></div>

<div dir="rtl"><a dir="ltr" href="https://www.stopforumspam.com/">Stop Forum Spam</a> هي خدمة رائعة متاحة مجانًا يمكن أن تساعد في حماية المنتديات والمدونات ومواقع الويب من مرسلي الرسائل غير المرغوب فيها. ويقوم بذلك عن طريق توفير قاعدة بيانات لمعرّفي البريد المزعوم المعروفين وواجهة برمجة تطبيقات يمكن الاستفادة منها للتحقق مما إذا كان عنوان IP أو اسم المستخدم أو عنوان البريد الإلكتروني مدرجًا في قاعدة البيانات الخاصة به.<br /><br /></div>

<div dir="rtl">يوفر CIDRAM المكون اختيارية تستفيد من واجهة برمجة التطبيقات هذه للتحقق مما إذا كان عنوان IP للطلبات الواردة ينتمي إلى مرسلي بريد مزعوم مشتبه فيهم. لم يتم تثبيت المكون النمطية بشكل افتراضي، ولكن إذا اخترت تثبيتها، فقد تتم مشاركة عناوين IP الخاصة بالمستخدمين مع واجهة برمجة تطبيقات Stop Forum Spam API وفقًا للغرض المقصود من المكون. عند تثبيت المكون، يتصل CIDRAM مع واجهة برمجة التطبيقات هذه عندما يطلب أحد الطلبات الواردة موردًا يتعرف عليه CIDRAM كنوع من الموارد يتم استهدافه بشكل متكرر بواسطة مرسلي الرسائل غير المرغوب فيها (مثل صفحات تسجيل الدخول وصفحات التسجيل وصفحات التحقق من البريد الإلكتروني ونماذج التعليقات وما إلى ذلك).<br /><br /></div>

##### <div dir="rtl">١١.٢.٥ ABUSEIPDB<br /><br /></div>

<div dir="rtl">يوفر CIDRAM المكون نمطية اختيارية لحظر عناوين IP المسيئة باستخدام واجهة برمجة تطبيقات <a dir="ltr" href="https://www.abuseipdb.com/">AbuseIPDB</a>. لم يتم تثبيت المكون النمطية بشكل افتراضي، ولكن إذا اخترت تثبيتها، فقد تتم مشاركة عناوين IP الخاصة بالمستخدمين مع واجهة برمجة تطبيقات AbuseIPDB API وفقًا للغرض المقصود من المكون.<br /><br /></div>

##### <div dir="rtl">١١.٢.٦ BGPVIEW, IP-API<br /><br /></div>

<div dir="rtl">يوفر CIDRAM المكون نمطية اختيارية لإجراء عمليات البحث ASN ورمز البلد باستخدام API <a dir="ltr" href="https://bgpview.io/">BGPView</a> وAPI <a dir="ltr" href="https://ip-api.com/">IP-API</a>. توفر عمليات البحث هذه القدرة على حظر أو إدراج طلبات القائمة البيضاء على أساس ASN أو بلد المنشأ. لم يتم تثبيت المكون النمطية بشكل افتراضي، ولكن إذا اخترت تثبيتها، فقد تتم مشاركة عناوين IP الخاصة بالمستخدمين مع الخدمة وفقًا للغرض المقصود من المكون.<br /><br /></div>

#### <div dir="rtl">١١.٣ تسجيل<br /><br /></div>

<div dir="rtl">التسجيل هو جزء مهم من CIDRAM لعدد من الأسباب. قد يكون من الصعب تشخيص وحل إيجابيات خاطئة عندما لا يتم تسجيل أحداث الحظر التي تسبب لهم. بدون تسجيل أحداث الحظر، قد يكون من الصعب التأكد من أداء CIDRAM بشكل جيد، وقد يكون من الصعب تحديد مواطن ضعفها، وما هي التغييرات التي قد تكون مطلوبة لتكوينها أو توقيعاتها، لكي تستمر في العمل على النحو المنشود. بغض النظر، ربما لا يريد الجميع التسجيل، لذلك يبقى اختياريًا تمامًا. في CIDRAM، يتم تعطيل التسجيل افتراضيًا. لتمكينه، يجب تكوين CIDRAM وفقًا لذلك.<br /><br /></div>

<div dir="rtl">بالإضافة إلى، ما إذا كان تخزين هذا النوع من البياناتمسموحًا به قانونًا، وإلى الحد المسموح به قانونًا (ذلك بالقول، أنواع المعلومات التي يمكن تسجيلها، إلى متى، وتحت أي ظروف)، قد تختلف، وهذا يتوقف على الاختصاص واعتمادًا على سياق التنفيذ (فمثلا، سواء كنت تعمل كفرد أو مؤسسة، وعما إذا كان ذلك على أساس تجاري أو غير تجاري). لذلك قد يكون من المفيد لك قراءة هذا القسم بعناية.<br /><br /></div>

<div dir="rtl">هناك العديد من أنواع المعلومات المختلفة التي يمكن تسجيلها، لأسباب مختلفة.<br /><br /></div>

##### <div dir="rtl">١١.٣.٠ حظر الأحداث<br /><br /></div>

<div dir="rtl">النوع الأساسي من التسجيل الذي يمكن أن يؤديه CIDRAM يتعلق بـ "حظر الأحداث". يتعلق هذا عندما يقوم CIDRAM بحظر الطلب، ويمكن توفيره في ثلاثة تنسيقات مختلفة:<br /></div>
<div dir="rtl"><ul>
 <li>السجلات التي يمكن قراءتها من قبل البشر.</li>
 <li>سجلات في اسلوب اباتشي.</li>
 <li>سجلات مسلسلة.</li>
</ul></div>

<div dir="rtl">حدث كتلة، سجلت إلى ملف سجل الإنسان مقروء، يبدو عادة مثل هذا (على سبيل المثال):<br /><br /></div>

<pre dir="rtl">
الهوية الشخصية: <code dir="ltr">1234</code>
النسخة النصية: <code dir="ltr">CIDRAM v1.6.0</code>
الوقت/التاريخ: <code dir="ltr">Day, dd Mon 20xx hh:ii:ss +0000</code>
عنوان IP: <code dir="ltr">x.x.x.x</code>
اسم المضيف: <code dir="ltr">dns.hostname.tld</code>
عدد التوقيعات: <code dir="ltr">1</code>
مرجع التوقيعات: <code dir="ltr">x.x.x.x/xx</code>
سبب الحظر: الخدمات السحابية ("اسم الشبكة", <code dir="ltr">Lxx:Fx</code>, <code dir="ltr">[XX]</code>)!
وكيل المستخدم: <code dir="ltr">Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36</code>
أعيد بناؤها URI: <code dir="ltr">https://your-site.tld/index.php</code>
الحالة CAPTCHA: تمكين.
</pre>

<div dir="rtl">نفس الشيء، المسجل في ملف السجل على نمط Apache، سيبدو كالتالي:<br /><br /></div>

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

<div dir="rtl">عادةً ما يتضمن إدخال سجل أحداث الحظر المعلومات التالية:</div>
<div dir="rtl"><ul>
 <li>رقم ID يشير إلى الحدث.</li>
 <li>إصدار CIDRAM قيد الاستخدام حاليًا.</li>
 <li>تاريخ ووقت وقوع الحدث.</li>
 <li>عنوان IP الخاص بالطلب المحظور.</li>
 <li>اسم المضيف لعنوان IP الخاص بالطلب المحظور (عندما يكون متاحًا).</li>
 <li>عدد التوقيعات التي أثارها الطلب.</li>
 <li>المراجع إلى التوقيعات أثار.</li>
 <li>تشير إلى أسباب الحدث وبعض المعلومات الأساسية المتعلقة بالتصحيح.</li>
 <li>وكيل المستخدم للطلب المحظور (أي كيف حدد الكيان الذي أرسل الطلب نفسه).</li>
 <li>إعادة بناء معرف المورد.</li>
 <li>حالة CAPTCHA للطلب الحالي (عند الضرورة).</li>
</ul></div>

<div dir="rtl">توجيهات التهيئة ذات الصلة:</div>
<div dir="rtl"><ul>
 <li><code dir="ltr">logfile</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">logfile_apache</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">logfile_serialized</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

<div dir="rtl">عندما يتم ترك هذه التوجيهات فارغة، سيظل هذا النوع من التسجيل معطلاً.<br /><br /></div>

##### <div dir="rtl">١١.٣.١ تسجيل CAPTCHA<br /><br /></div>

<div dir="rtl">هذا النوع من التسجيل يتعلق بشكل خاص بمثيلات CAPTCHA. يحدث فقط عندما يحاول مستخدم لإكمال CAPTCHA.<br /><br /></div>

<div dir="rtl">يحتوي إدخال سجل CAPTCHA على عنوان IP الخاص بالمستخدم الذي يحاول إكمال CAPTCHA، وتاريخ ووقت حدوث المحاولة، وحالة CAPTCHA. عادةً ما تبدو الإدخالات كما يلي (كمثال):<br /><br /></div>

```
عنوان IP: x.x.x.x - الوقت/التاريخ: Day, dd Mon 20xx hh:ii:ss +0000 - الحالة CAPTCHA: نجحت!
```

<div dir="rtl">توجيه التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">logfile</code> &lt;- <code dir="ltr">recaptcha</code></li>
 <li><code dir="ltr">logfile</code> &lt;- <code dir="ltr">hcaptcha</code></li>
</ul></div>

##### <div dir="rtl">١١.٣.٢ سجلات الواجهة الأمامية<br /><br /></div>

<div dir="rtl">هذا التسجيل يتصل محاولات تسجيل الدخول الأمامية. يحدث فقط عندما يحاول مستخدم تسجيل الدخول إلى الواجهة الأمامية، وفقط عندما يتم تمكين الوصول للجهة الأمامية.<br /><br /></div>

<div dir="rtl">يحتوي إدخال سجل الواجهة الأمامية على عنوان IP الخاص بالمستخدم الذي يحاول تسجيل الدخول وتاريخ ووقت حدوث المحاولة ونتائج المحاولة (تم تسجيل الدخول بنجاح، أو فشل في تسجيل الدخول). يبدو عادة مثل هذا (كمثال):<br /><br /></div>

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - حاليا على.
```

<div dir="rtl">توجيه التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">frontend_log</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">١١.٣.٣ دوران السجل<br /><br /></div>

<div dir="rtl">قد ترغب في تطهير السجلات بعد فترة من الوقت، أو قد تكون مطلوبة للقيام بذلك بموجب القانون (أي أن مقدار الوقت المسموح به قانونًا لك للاحتفاظ بالسجلات قد يكون محدودًا بموجب القانون). يمكنك تحقيق ذلك عن طريق تضمين علامات التاريخ/الوقت في أسماء ملفات السجل الخاصة بك كما هو محدد بواسطة تكوين الحزمة الخاصة بك (على سبيل المثال، <code dir="ltr">{yyyy}-{mm}-{dd}.log</code>)، ثم تمكين دوران السجل (يسمح لك تدوير السجل بتنفيذ بعض الإجراءات على ملفات السجل عندما يتم تجاوز الحدود المحددة).<br /><br /></div>

<div dir="rtl">فمثلا: إذا كان من الضروري قانونًا حذف السجلات بعد 30 يومًا، يمكنني تحديد <code dir="ltr">{dd}.log</code> في أسماء ملفات السجل الخاصة بي (<code dir="ltr">{dd}</code> يمثل عدد الأيام)، قم بتعيين قيمة <code dir="ltr">log_rotation_limit</code> إلى 30، وقم بتعيين قيمة <code dir="ltr">log_rotation_action</code> إلى <code dir="ltr">Delete</code>.<br /><br /></div>

<div dir="rtl">على العكس من ذلك، إذا كنت مطالبًا بالاحتفاظ بالسجلات لفترة زمنية طويلة، فيمكنك تعطيل تدوير السجل، أو يمكنك تعيين قيمة <code dir="ltr">log_rotation_action</code> إلى <code dir="ltr">Archive</code>، لضغط ملفات السجل، وبالتالي تقليل إجمالي مساحة القرص التي يشغلونها.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">log_rotation_limit</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">log_rotation_action</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">١١.٣.٤ سجل اقتطاع<br /><br /></div>

<div dir="rtl">إذا أردت، يمكنك اقتطاع ملفات السجل الفردية عندما تتجاوز حجمًا معينًا.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">truncate</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">١١.٣.٥ عنوان IP PSEUDONYMISATION<br /><br /></div>

<div dir="rtl">أولاً، إذا لم تكن على دراية بهذا المصطلح، "pseudonymisation" يشير إلى معالجة البيانات الشخصية على هذا النحو بحيث لا يمكن تحديدها لأي موضوع بيانات محدد بعد الآن بدون معلومات إضافية، وشريطة أن يتم الاحتفاظ بهذه المعلومات التكميلية بشكل منفصل وتخضع للتدابير التقنية والتنظيمية لضمان عدم إمكانية تحديد البيانات الشخصية لأي شخص طبيعي.<br /><br /></div>

<div dir="rtl">يمكن أن تساعد الموارد التالية في شرحها بمزيد من التفاصيل:</div>
<div dir="rtl"><ul>
 <li><a dir="ltr" href="https://www.trust-hub.com/news/what-is-pseudonymisation/">[trust-hub.com] What is pseudonymisation?</a></li>
 <li><a dir="ltr" href="https://en.wikipedia.org/wiki/Pseudonymization">[Wikipedia] Pseudonymization</a></li>
</ul></div>

<div dir="rtl">في بعض الحالات، قد يُطلب منك قانونًا تنفيذ "anonymisation" أو "pseudonymisation" لأي معلومات PII تم جمعها أو معالجتها أو تخزينها. على الرغم من وجود هذا المفهوم منذ بعض الوقت، GDPR/DSGVO يذكر بشكل ملحوظ ويشجع "pseudonymisation".<br /><br /></div>

<div dir="rtl">إذا أردت، يمكن لـ CIDRAM القيام بذلك لعناوين IP عند الكتابة إلى السجلات. عند الكتابة إلى السجلات، سيتم تمثيل الثمانية النهائية لعناوين IPv4 وكل شيء بعد الجزء الثاني من عناوين IPv6 بواسطة "x" (تقريب عناوين IPv4 إلى العنوان الأولي للشبكة الفرعية الـ 24 التي تدخلها، وعناوين IPv6 إلى العنوان الأولي للشبكة الفرعية 32 التي تدخلها).<br /><br /></div>

<div dir="rtl"><em>ملحوظة: ميزة تتبع IP من CIDRAM لا تملك هذه القدرة. إذا كانت هذه مشكلة بالنسبة لك، فقد يكون من الأفضل تعطيل تتبع IP بالكامل. ويمكن تحقيق ذلك عن طريق تعيين <code dir="ltr">track_mode</code> إلى <code dir="ltr">false</code> وعن طريق تجنب أي وحدات.</em><br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">track_mode</code> &lt;- <code dir="ltr">signatures</code></li>
 <li><code dir="ltr">pseudonymise_ip_addresses</code> &lt;- <code dir="ltr">legal</code></li>
</ul></div>

##### <div dir="rtl">١١.٣.٦ حذف معلومات السجل<br /><br /></div>

<div dir="rtl">إذا كنت ترغب في منع تسجيل أنواع معينة من المعلومات بالكامل، فيمكنك القيام بذلك. يوفر CIDRAM توجيهات التهيئة للتحكم في ما إذا كانت عناوين IP وأسماء المضيفات ووكلاء المستخدمين مدرجة في السجلات. بشكل افتراضي، وعند توفرها، يتم تسجيل نقاط البيانات الثلاثة جميعها. يؤدي تعيين أي من توجيهات التهيئة هذه إلى <code dir="ltr">true</code> إلى حذف المعلومات المقابلة من السجلات.<br /><br /></div>

<div dir="rtl"><em>ملحوظة: لا يوجد سبب لاستخدام pseudonymisation لعناوين IP عند حذف عناوين IP من السجلات بالكامل.</em><br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">omit_ip</code> &lt;- <code dir="ltr">legal</code></li>
 <li><code dir="ltr">omit_hostname</code> &lt;- <code dir="ltr">legal</code></li>
 <li><code dir="ltr">omit_ua</code> &lt;- <code dir="ltr">legal</code></li>
</ul></div>

##### <div dir="rtl">١١.٣.٧ الإحصاء<br /><br /></div>

<div dir="rtl">CIDRAM قادر بشكل اختياري على تتبع الإحصائيات مثل إجمالي عدد أحداث المنع أو حالات CAPTCHA التي حدثت منذ وقت معين. يتم تعطيل هذه الميزة بشكل افتراضي، ولكن يمكن تمكينها من خلال تهيئة الحزمة. هذه الميزة لا تتبع سوى العدد الإجمالي للأحداث. لا يتضمن أي معلومات حول أحداث معينة، لذلك لا ينبغي اعتباره معلومات تحديد الهوية الشخصية.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">statistics</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">١١.٣.٨ التشفير<br /><br /></div>

<div dir="rtl">لا يقوم CIDRAM بتشفير ذاكرة التخزين المؤقت أو أي معلومات سجل. قد يتم إدخال <a href="https://ar.wikipedia.org/wiki/%D8%AA%D8%B4%D9%81%D9%8A%D8%B1">تشفير</a> ذاكرة التخزين المؤقت والسجلات في المستقبل، ولكن لا توجد خطط محددة لها حاليًا. إذا كنت قلقًا بشأن حصول أطراف ثالثة غير مصرح لها على إمكانية الوصول إلى أجزاء من CIDRAM قد تحتوي على معلومات تحديد الهوية الشخصية أو معلومات حساسة مثل ذاكرة التخزين المؤقت أو السجلات، أوصي بعدم تثبيت CIDRAM في مكان يمكن الوصول إليه بشكل عام (على سبيل المثال، مجلد تثبيت CIDRAM خارج الدليل <code dir="ltr">public_html</code> القياسي أو ما يعادله، متاح لمعظم خوادم الويب القياسية) والتأكد من فرض الأذونات المقيدة بشكل مناسب لدليل التثبيت (على وجه الخصوص، لدليل <code dir="ltr">vault</code>). إذا لم يكن ذلك كافيًا لمعالجة مخاوفك، فقم بتكوين CIDRAM بحيث لا يتم جمع أنواع المعلومات التي تسبب مخاوفك أو تسجيلها في المقام الأول (مثل، عن طريق تعطيل التسجيل).<br /><br /></div>

#### <div dir="rtl">١١.٤ ملف تعريف ارتباط<br /><br /></div>

<div dir="rtl">يضع CIDRAM <a href="https://ar.wikipedia.org/wiki/%D9%85%D9%84%D9%81_%D8%AA%D8%B9%D8%B1%D9%8A%D9%81_%D8%A7%D8%B1%D8%AA%D8%A8%D8%A7%D8%B7">ملفات تعريف الارتباط</a> في نقطتين في تعليمات البرمجة الخاصة به. أولاً، عندما يقوم المستخدم بإكمال CAPTCHA بنجاح (مع افتراض أن <code dir="ltr">lockuser</code> مضبوطة على <code dir="ltr">true</code>)، يعيّن CIDRAM ملف تعريف ارتباط ليتمكن من التذكر للطلبات التالية بأن المستخدم قد أكمل بالفعل CAPTCHA، بحيث لا يحتاج إلى مطالبة المستخدم بإكمال CAPTCHA في الطلبات اللاحقة. ثانيا، عندما يسجل المستخدم بنجاح في الواجهة الأمامية، يعين CIDRAM ملف تعريف ارتباط حتى يتمكن من تذكر المستخدم للطلبات اللاحقة (أي، يتم استخدام ملفات تعريف الارتباط لمصادقة المستخدم على جلسة تسجيل الدخول).<br /><br /></div>

<div dir="rtl">في كلتا الحالتين، يتم عرض تحذيرات ملفات تعريف الارتباط بشكل بارز (عند الاقتضاء)، وتحذير المستخدم من أنه سيتم تعيين ملفات تعريف الارتباط إذا شارك في الإجراءات ذات الصلة. لا يتم تعيين ملفات تعريف الارتباط في أي نقاط أخرى في مصدر التعليمات البرمجية.<br /><br /></div>

<div dir="rtl">ملحوظة: قد تكون واجهات برمجة تطبيقات CAPTCHA "غير المرئية" غير متوافقة مع قوانين ملفات تعريف الارتباط في بعض الولايات القضائية، ويجب تجنبها من قبل أي مواقع ويب تخضع لهذه القوانين. قد يكون من الأفضل اختيار استخدام واجهات برمجة التطبيقات الأخرى المتوفرة بدلاً من ذلك، أو ببساطة تعطيل اختبار CAPTCHA بالكامل.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">disable_frontend</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">lockuser</code> &lt;- <code dir="ltr">recaptcha</code></li>
 <li><code dir="ltr">api</code> &lt;- <code dir="ltr">recaptcha</code></li>
 <li><code dir="ltr">lockuser</code> &lt;- <code dir="ltr">hcaptcha</code></li>
 <li><code dir="ltr">api</code> &lt;- <code dir="ltr">hcaptcha</code></li>
</ul></div>

#### <div dir="rtl">١١.٥ التسويق والإعلان<br /><br /></div>

<div dir="rtl">لا تجمع CIDRAM أو تعالج أي معلومات لأغراض التسويق أو الإعلانات، ولا تبيع أو تحقق أرباحًا من أي معلومات تم جمعها أو تسجيلها. CIDRAM ليست مؤسسة تجارية، ولا ترتبط بأي مصالح تجارية، لذا فإن القيام بهذه الأشياء لن يكون له أي معنى. كان هذا هو الحال منذ بداية المشروع، وما زالت الحالة اليوم. بالإضافة إلى ذلك، فإن القيام بهذه الأشياء سيؤدي إلى نتائج عكسية للمشروع والغرض المقصود من المشروع ككل، وطالما استمر في الحفاظ على المشروع، لن يحدث أبداً.<br /><br /></div>

#### <div dir="rtl">١١.٦ سياسة الخصوصية<br /><br /></div>

<div dir="rtl">في بعض الحالات، قد يُطلب منك قانونًا عرض رابط لسياسة الخصوصية بوضوح في جميع صفحات وأقسام موقعك. قد يكون هذا أمرًا مهمًا كوسيلة لضمان معرفة المستخدمين جيدًا بممارسات الخصوصية الدقيقة، وأنواع معلومات تحديد الهوية الشخصية التي تجمعها، وكيفية تنوي استخدامها. لتتمكن من تضمين مثل هذا الارتباط في صفحة "تم رفض الوصول" الخاصة بـ CIDRAM، يتم توفير توجيه تكوين لتحديد عنوان URL لسياسة الخصوصية الخاصة بك.<br /><br /></div>

<div dir="rtl">ملحوظة: يوصى بشدة بعدم وضع صفحة سياسة الخصوصية خلف حماية CIDRAM. إذا قام CIDRAM بحماية صفحة سياسة الخصوصية الخاصة بك، وكان المستخدم المحظور من قِبل CIDRAM ينقر على رابط لسياسة الخصوصية الخاصة بك، فسيتم حظره مرة أخرى ولن يتمكن من رؤية سياسة الخصوصية الخاصة بك. من الناحية المثالية، يجب عليك الربط بنسخة ثابتة من سياسة الخصوصية، مثل صفحة HTML أو ملف نصي عادي غير محمي بواسطة CIDRAM.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">privacy_policy</code> &lt;- <code dir="ltr">legal</code></li>
</ul></div>

#### <div dir="rtl">١١.٧ GDPR/DSGVO<br /><br /></div>

<div dir="rtl">يعد اللائحة العامة لحماية البيانات (GDPR) لائحة خاصة بالاتحاد الأوروبي، والتي تدخل حيز التنفيذ اعتبارًا من 25 مايو 2018. الهدف الأساسي من التنظيم هو إعطاء السيطرة على المواطنين والمقيمين في الاتحاد الأوروبي فيما يتعلق ببياناتهم الشخصية، وتوحيد الأنظمة داخل الاتحاد الأوروبي فيما يتعلق بالخصوصية والبيانات الشخصية.<br /><br /></div>

<div dir="rtl">تحتوي اللائحة على أحكام محددة تتعلق بمعالجة "معلومات التعريف الشخصية" لأي "موضوعات بيانات" تابعة للاتحاد الأوروبي (أي شخص طبيعي محدد أو قابل للتحديد). من أجل الامتثال للأنظمة، "الشركات" (كما هو محدد في اللائحة)، وكذلك أي أنظمة وعمليات ذات صلة، يجب تنفيذ "الخصوصية حسب التصميم" بشكل افتراضي، يجب استخدام أعلى إعدادات الخصوصية الممكنة، يجب تنفيذ الضمانات اللازمة لأية معلومات مخزنة أو معالجتها (بما في ذلك، على سبيل المثال لا الحصر، تنفيذ "pseudonymisation" أو "anonymisation" الكامل للبيانات)، يجب أن يعلن بوضوح وبشكل لا لبس فيه أنواع البيانات التي يجمعونها، كيفية معالجتها، لأي أسباب، إلى متى تحتفظ بها، وإذا شاركوا هذه البيانات مع أطراف ثالثة، وأنواع البيانات المشتركة مع أطراف ثالثة، وكيف، ولماذا، وما إلى ذلك.<br /><br /></div>

<div dir="rtl">لا يجوز معالجة البيانات ما لم يكن هناك أساس قانوني للقيام بذلك، كما هو محدد في اللائحة. وبشكل عام، يعني هذا أنه من أجل معالجة بيانات موضوع البيانات على أساس قانوني، يجب أن يتم ذلك وفقًا لالتزامات قانونية، أو يتم فقط بعد الحصول على موافقة واضحة ومطلعة بشكل لا لبس فيه من موضوع البيانات.<br /><br /></div>

<div dir="rtl">قد تتطور جوانب التنظيم في الوقت المناسب، ومن أجل تجنب نشر المعلومات القديمة، قد يكون من الأفضل معرفة التنظيم من مصدر موثوق، بدلاً من مجرد تضمين المعلومات ذات الصلة هنا في وثائق الحزمة (مثل المعلومات المضمنة قد تصبح في نهاية المطاف عفا عليها الزمن مع تطور التنظيم).<br /><br /></div>

<div dir="rtl">بعض الموارد الموصى بها لتعلم المزيد من المعلومات:<br /></div>
<div dir="rtl"><ul>
 <li><a href="https://ar.wikipedia.org/wiki/%D8%A7%D9%84%D9%86%D8%B8%D8%A7%D9%85_%D8%A7%D9%84%D8%A3%D9%88%D8%B1%D9%88%D8%A8%D9%8A_%D9%84%D8%AD%D9%85%D8%A7%D9%8A%D8%A9_%D8%A7%D9%84%D8%A8%D9%8A%D8%A7%D9%86%D8%A7%D8%AA_%D8%A7%D9%84%D8%B9%D8%A7%D9%85%D8%A9">النظام الأوروبي لحماية البيانات العامة</a></li>
 <li><a href="https://taqnia24.com/2018/05/24/%D8%AA%D8%B9%D8%B1%D9%81-%D8%B9%D9%84%D9%89-%D9%82%D8%A7%D9%86%D9%88%D9%86-%D8%AD%D9%85%D8%A7%D9%8A%D8%A9-%D8%AE%D8%B5%D9%88%D8%B5%D9%8A%D8%A9-%D8%A7%D9%84%D8%A8%D9%8A%D8%A7%D9%86%D8%A7%D8%AA-gdpr/">تعرف على قانون حماية خصوصية البيانات GDPR</a></li>
 <li><a href="https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679">REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL</a></li>
</ul></div>

---


<div dir="rtl">آخر تحديث: ٦ أغسطس ٢٠٢٥ (٢٠٢٥.٠٨.٠٦).</div>
