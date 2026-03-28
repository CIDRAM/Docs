## <div dir="rtl">CIDRAM v4 بالعربية</div>

### <div dir="rtl">المحتويات:</div>
<div dir="rtl"><ul>
 <li>١. <a href="#user-content-SECTION1">مقدمة</a></li>
 <li>٢. <a href="#user-content-SECTION2">كيفية التحميل</a></li>
 <li>٣. <a href="#user-content-SECTION3">كيفية الإستخدام</a></li>
 <li>٤. <a href="#user-content-SECTION4">إدارة FRONT-END</a></li>
 <li>٥. <a href="#user-content-SECTION5">خياراتالتكوين/التهيئة</a></li>
 <li>٦. <a href="#user-content-SECTION6">شكل/تنسيق التوقيع</a></li>
 <li>٧. <a href="#user-content-SECTION7">مشاكل التوافق المعروفة</a></li>
 <li>٨. <a href="#user-content-SECTION8">أسئلة وأجوبة (FAQ)</a></li>
 <li>٩. <a href="#user-content-SECTION9">المعلومات القانونية</a></li>
 <li>١٠. <a href="#user-content-SECTION10">الترقية من الإصدارات الرئيسية السابقة</a></li>
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

<div dir="rtl">يمكن تنزيل CIDRAM مجانًا من هنا:</div>

- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM).

<div dir="rtl">يمكن العثور على هذه الوثيقة وترجماتها المختلفة هنا:</div>

- [GitHub](https://github.com/CIDRAM/Docs).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram-docs).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM-Docs).

---


### <div dir="rtl">٢. <a name="SECTION2"></a>كيفية التحميل</div>

#### <div dir="rtl">٢.٠ تثبيت يدويا</div>

<div dir="rtl">أولاً، ستحتاج إلى نسخة حديثة من CIDRAM. يمكنك تنزيل أرشيف لأحدث إصدار من CIDRAM من المستودع <a dir="ltr" hreflang="en" href="https://github.com/CIDRAM/CIDRAM">CIDRAM/CIDRAM</a>. لكي تكون محددًا، ستحتاج إلى نسخة حديثة من دليل "vault" (يمكن حذف كل شيء آخر في الأرشيف أو تجاهله بأمان).<br /><br /></div>

<div dir="rtl">قبل v3، كان من الضروري تثبيت CIDRAM في مكان ما داخل الجذر العام الخاص بك حتى تتمكن من الوصول إلى الواجهة الأمامية لـ CIDRAM. ومع ذلك، من v3 فصاعدًا، هذا ليس ضروريًا. من أجل تحقيق أقصى قدر من الأمان ومنع الوصول غير المصرح به إلى CIDRAM وملفاته، يوصى بدلاً من ذلك بتثبيت CIDRAM خارج جذرك العام. لا يهم مكان تثبيت CIDRAM، طالما أنه يمكن الوصول إليه في مكان ما بواسطة PHP، في مكان ما آمن بشكل معقول، وفي مكان ما تسعد به. ليس من الضروري أيضًا الاحتفاظ باسم دليل "vault" بعد الآن، لذا يمكنك إعادة تسمية "vault" إلى أي شيء تريده (ولكن من أجل الملاءمة، ستستمر الوثائق في الإشارة إلى الدليل باسم "vault").<br /><br /></div>

<div dir="rtl">عندما تكون جاهزًا، قم بتحميل دليل "vault" إلى الموقع الذي اخترته، وتأكد من أنه يحتوي على الأذونات اللازمة حتى تتمكن PHP من الكتابة إلى الدليل (اعتمادًا على النظام، قد لا تحتاج إلى فعل أي شيء، أو قد تحتاج إلى ضبط CHMOD 755 على الدليل، أو إذا كانت هناك مشاكل مع 755، يمكنك تجربة 777، لكن 777 غير موصى به نظرًا لكونه أقل أمانًا).<br /><br /></div>

<div dir="rtl">بعد ذلك، لكي تتمكن CIDRAM من حماية قاعدة التعليمات البرمجية أو CMS، ستحتاج إلى إنشاء "نقطة دخول". تتكون نقطة الدخول هذه من ثلاثة أشياء:<br /><br /></div>

<div dir="rtl">
  ١. تضمين ملف "loader.php" في نقطة مناسبة في قاعدة التعليمات البرمجية أو CMS.<br />
  ٢. قم بإنشاء مثيل لـ CIDRAM core.<br />
  ٣. استدعاء طريقة "protect".<br /><br />
</div>

<div dir="rtl">مثال بسيط:<br /><br /></div>

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

<div dir="rtl">إذا كنت تستخدم خادم ويب Apache ولديك حق الوصول إلى <code dir="ltr">php.ini</code>، فيمكنك استخدام التوجيه <code dir="ltr">auto_prepend_file</code> لإرفاق CIDRAM مسبقًا كلما تم إجراء أي طلب PHP. في مثل هذه الحالة، سيكون المكان الأنسب لإنشاء نقطة الإدخال في الملف الخاص به، ويمكنك بعد ذلك الاستشهاد بهذا الملف في التوجيه <code dir="ltr">auto_prepend_file</code>.<br /><br /></div>

<div dir="rtl">مثال:<br /><br /></div>

`auto_prepend_file = "/path/to/your/entrypoint.php"`

<div dir="rtl">أو هذا في ملف <code dir="ltr">.htaccess</code>:<br /><br /></div>

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

<div dir="rtl">في حالات أخرى، سيكون المكان الأنسب لإنشاء نقطة الدخول الخاصة بك في أقرب وقت ممكن داخل قاعدة التعليمات البرمجية أو CMS ليتم تحميلها دائمًا عندما يصل شخص ما إلى أي صفحة عبر موقع الويب بالكامل. إذا كان الكود الخاص بك يستخدم "bootstrap"، فإن المثال الجيد سيكون في بداية ملف "bootstrap" الخاص بك. إذا كانت قاعدة الشفرة الخاصة بك تحتوي على ملف مركزي مسؤول عن الاتصال بقاعدة البيانات الخاصة بك، فسيكون هناك مثال جيد آخر في بداية هذا الملف المركزي.<br /><br /></div>

#### <div dir="rtl">٢.١ تثبيت مع COMPOSER</div>

<div dir="rtl"><a href="https://packagist.org/packages/cidram/cidram">يتم تسجيل CIDRAM مع Packagist</a>، و بالتالي، إذا كنت على دراية به، يمكنك استخدامه لتثبيت CIDRAM.<br /><br /></div>

`composer require cidram/cidram`

#### <div dir="rtl">٢.٢ تثبيت ل ووردبريس</div>

<div dir="rtl"><a href="https://wordpress.org/plugins/cidram/">يتوفر CIDRAM من قاعدة بيانات الإضافات وووردبريس</a>. يمكنك تثبيته بنفس الطريقة مثل أي مكون إضافي.<br /><br /></div>

<div dir="rtl"><em>تحذير: يؤدي تحديث CIDRAM عبر لوحة تحكم المكونات الإضافية إلى تثبيت نظيف! إذا كان لديك تخصيصات (تغيير التكوين، تثبيت وحدات، الخ)، سيتم فقدان هذه التخصيصات عند تحديث عن طريق لوحة أجهزة القياس الإضافات! كما سيتم فقدان لوغفيلز عند تحديث عن طريق لوحة أجهزة القياس الإضافات! للحفاظ على ملفات السجل والتخصيصات، يتم التحديث عبر صفحة التحديثات الأمامية ل CIDRAM.</em><br /><br /></div>

#### <div dir="rtl">٢.٣ التكوين والتخصيص</div>

<div dir="rtl">يوصى بشدة بمراجعة تكوين التثبيت الجديد حتى تتمكن من تعديله وفقًا لاحتياجاتك. قد ترغب أيضًا في تثبيت وحدات نمطية إضافية، أو ملفات توقيع، أو إنشاء قواعد مساعدة، أو تنفيذ تخصيصات أخرى حتى يكون التثبيت الخاص بك قادرًا على تلبية احتياجاتك على أفضل وجه. أوصي باستخدام الواجهة الأمامية للقيام بهذه الأشياء.<br /><br /></div>

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

#### <div dir="rtl">٤.١ كيفية الوصول إلى الواجهة الأمامية.<br /><br /></div>

<div dir="rtl">على غرار الطريقة التي احتجت إلى إنشاء نقطة إدخال لكي يحمي CIDRAM موقع الويب الخاص بك، ستحتاج أيضًا إلى إنشاء نقطة إدخال للوصول إلى الواجهة الأمامية. تتكون نقطة الدخول هذه من ثلاثة أشياء:<br /><br /></div>

<div dir="rtl">
  ١. تضمين ملف "loader.php" في نقطة مناسبة في قاعدة التعليمات البرمجية أو CMS.<br />
  ٢. قم بإنشاء مثيل لـ CIDRAM front-end.<br />
  ٣. استدعاء طريقة "view".<br /><br />
</div>

<div dir="rtl">مثال بسيط:<br /><br /></div>

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

<div dir="rtl">تقوم فئة "FrontEnd" بتوسيع فئة "Core"، مما يعني أنه إذا أردت، يمكنك استدعاء طريقة "protect" قبل استدعاء طريقة "view" من أجل منع حركة المرور غير المرغوب فيها من الوصول إلى الواجهة الأمامية. القيام بذلك اختياري تمامًا.<br /><br /></div>

<div dir="rtl">مثال بسيط:<br /><br /></div>

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

<div dir="rtl">المكان الأنسب لإنشاء نقطة إدخال للواجهة الأمامية هو في ملفها المخصص. على عكس نقطة الإدخال التي تم إنشاؤها مسبقًا، فأنت تريد أن يكون الوصول إلى نقطة الدخول الأمامية الخاصة بك متاحًا فقط عن طريق الطلب مباشرة للملف المحدد حيث توجد نقطة الإدخال، لذلك في هذه الحالة، لن ترغب في استخدام <code dir="ltr">auto_prepend_file</code> أو <code dir="ltr">.htaccess</code>.<br /><br /></div>

<div dir="rtl">بعد إنشاء نقطة الدخول الأمامية، استخدم متصفحك للوصول إليها. يجب أن يتم تقديمه مع صفحة تسجيل الدخول. في صفحة تسجيل الدخول، أدخل اسم المستخدم وكلمة المرور الافتراضيين (admin/password) واضغط على زر تسجيل الدخول.<br /><br /></div>

<div dir="rtl">ملحوظة: تغيير اسم المستخدم وكلمة المرور الخاصة بك بعد تسجيل الدخول للمرة الأولى، من أجل منع الوصول غير المصرح به (هذا مهم جدا)!<br /><br /></div>

<div dir="rtl">أيضًا، للحصول على الأمان الأمثل، نوصي بشدة بتمكين 2FA لجميع حسابات الواجهة الأمامية (الإرشادات الواردة أدناه).<br /><br /></div>

#### <div dir="rtl">٤.٢ كيفية استخدام FRONT-END.<br /><br /></div>

<div dir="rtl">في كل صفحة، ويفسر ذلك كيفية استخدامها. إذا كنت بحاجة إلى أي مساعدة، يرجى الاتصال بالدعم. وهناك أيضا بعض مقاطع الفيديو المفيدة المتاحة على موقع يوتيوب.<br /><br /></div>

#### <div dir="rtl">٤.٣ 2FA<br /><br /></div>

<div dir="rtl">من الممكن جعل front-end أكثر أمانًا عن طريق تمكين 2FA. عند تسجيل الدخول إلى حساب باستخدام 2FA، يتم إرسال بريد إلكتروني إلى عنوان البريد الإلكتروني المقترن بهذا الحساب. تحتوي هذه الرسالة الإلكترونية على "رمز 2FA"، والذي يجب على المستخدم إدخاله، بالإضافة إلى اسم المستخدم وكلمة المرور، حتى تتمكن من تسجيل الدخول باستخدام هذا الحساب. وهذا يعني أن الحصول على كلمة مرور الحساب لن يكون كافيًا لأي متسلل أو مهاجم محتمل ليتمكن من تسجيل الدخول إلى هذا الحساب، لأنهم سيحتاجون أيضًا إلى الوصول بالفعل إلى عنوان البريد الإلكتروني المرتبط بهذا الحساب حتى يتمكنوا من تلقي رمز 2FA واستخدامه في الجلسة.<br /><br /></div>

<div dir="rtl">أولاً، لتمكين 2FA، استخدم صفحة تحديثات front-end لتثبيت مكون PHPMailer. CIDRAM يستخدم PHPMailer لإرسال رسائل البريد الإلكتروني.<br /><br /></div>

<div dir="rtl">بعد تثبيت PHPMailer، ستحتاج إلى تعبئة توجيهات التهيئة لـ PHPMailer عبر صفحة تهيئة CIDRAM أو ملف التكوين. يتم تضمين مزيد من المعلومات حول توجيهات التكوين هذه في قسم التكوين في هذا المستند. بعد ملء توجيهات تهيئة PHPMailer، اضبط <code dir="ltr">enable_two_factor</code> على <code dir="ltr">true</code>. 2FA ممكّن الآن.<br /><br /></div>

<div dir="rtl">بعد ذلك، ستحتاج إلى ربط عنوان بريد إلكتروني بحساب، حتى يعرف CIDRAM مكان إرسال رموز 2FA عند تسجيل الدخول باستخدام هذا الحساب. للقيام بذلك، استخدم عنوان البريد الإلكتروني كاسم مستخدم للحساب (مثل <code dir="ltr">foo@bar.tld</code>)، أو تضمين عنوان البريد الإلكتروني كجزء من اسم المستخدم بالطريقة نفسها التي تريدها عند إرسال بريد إلكتروني بشكل طبيعي (مثل <code dir="ltr">Foo Bar &lt;foo@bar.tld&gt;</code>).<br /><br /></div>

<div dir="rtl">ملحوظة: حماية "vault" ضد الوصول غير المصرح به (على سبيل المثال، من خلال تعزيز أمن الخادم الخاص بك وتقييد أذونات الوصول العام)، أهمية خاصة هنا، لأن الوصول غير المصرح به إلى ملف التكوين الخاص بك (المخزن في "vault")، قد يؤدي إلى تعريض إعدادات SMTP الصادرة (بما في ذلك اسم مستخدم وكلمة مرور SMTP). يجب التأكد من تأمين "vault" بشكل صحيح قبل تمكين 2FA. إذا كنت غير قادر على القيام بذلك، فعلى الأقل، يجب عليك إنشاء حساب بريد إلكتروني جديد مخصص لهذا الغرض، وذلك لتقليل المخاطر المرتبطة بإعدادات SMTP المكشوفة.<br /><br /></div>

---


### <div dir="rtl">٥. <a name="SECTION5"></a>خياراتالتكوين/التهيئة</div>

<div dir="rtl">وفيما يلي قائمة من المتغيرات الموجودة في ملف تكوين "config.yml"، بالإضافة إلى وصف الغرض منه و وظيفته.<br /><br /></div>

```
التكوين (v4)
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

#### <div dir="rtl">"general" (التصنيف)<br /></div>
<div dir="rtl">التكوين العام (أي التكوين الأساسي لا ينتمي إلى فئات أخرى).<br /><br /></div>

##### <div dir="rtl">"stages" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ضوابط لمراحل سلسلة التنفيذ (سواء تم التمكين، أو تسجيل الأخطاء، وما إلى ذلك).</li></ul></div>

```
stages───[تمكين هذه المرحلة؟]─[سجل أي أخطاء ولدت خلال هذه المرحلة؟]─[هل يجب احتساب المخالفات التي تم إنشاؤها خلال هذه المرحلة لتتبع IP؟]
├─BanCheck ("تحقق مما إذا كان محظورًا")
├─Tests ("تنفيذ اختبارات ملفات التوقيع")
├─Modules ("تنفيذ الوحدات")
├─SearchEngineVerification ("تنفيذ التحقق من محرك البحث")
├─SocialMediaVerification ("تنفيذ التحقق من وسائل التواصل الاجتماعي")
├─OtherVerification ("تنفيذ التحقق الآخر")
├─Aux ("تنفيذ القواعد المساعدة")
├─Tracking ("تنفيذ تتبع IP")
├─RL ("تنفيذ تحديد معدل")
├─CAPTCHA ("انشر الكابتشا (الطلبات المحظورة)")
├─Reporting ("تنفيذ التقارير")
├─Statistics ("تحديث الإحصائيات")
├─Webhooks ("تنفيذ الخطافات على الويب")
├─TriggerNotifications ("معالجة قائمة إشعارات تشغيل البريد الإلكتروني")
├─PrepareFields ("تحضير الحقول للإخراج والسجلات")
├─Output ("توليد الإخراج (الطلبات المحظورة)")
├─WriteLogs ("الكتابة إلى السجلات (الطلبات المحظورة)")
├─Terminate ("قم بإنهاء الطلب (الطلبات المحظورة)")
├─AuxRedirect ("إعادة التوجيه وفقًا للقواعد المساعدة")
└─NonBlockedCAPTCHA ("انشر الكابتشا (الطلبات غير المحظورة)")
```

##### <div dir="rtl">"fields" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ضوابط الحقول أثناء أحداث الكتلة (عندما يتم حظر طلب).</li></ul></div>

```
fields───[هل يجب أن يظهر هذا الحقل في إدخالات السجل؟]─[هل يجب أن يظهر هذا الحقل في صفحة "الوصول مرفوض"؟]─[حذف هذا الحقل عندما يكون فارغا؟]
├─ID ("الهوية الشخصية")
├─ScriptIdent ("النسخة النصية")
├─DateTime ("الوقت/التاريخ")
├─IPAddr ("عنوان IP")
├─IPAddrResolved ("عنوان IP (تم حلها)")
├─Query ("إستعلام")
├─Referrer ("المرجع")
├─UA ("وكيل المستخدم")
├─UALC ("وكيل المستخدم (أحرف صغيرة)")
├─SignatureCount ("عدد التوقيعات")
├─Signatures ("مرجع التوقيعات")
├─WhyReason ("سبب الحظر")
├─ReasonMessage ("سبب الحظر (مفصلة)")
├─rURI ("أعيد بناؤها URI")
├─Infractions ("مخالفات")
├─ASNLookup ("** بحث ASN")
├─CCLookup ("** بحث عن كود البلد")
├─Verified ("التحقق من الهوية")
├─Expired ("منتهية الصلاحية")
├─Ignored ("تجاهل")
├─Request_Method ("Request method")
├─Protocol ("بروتوكول")
├─SEC_CH_UA_PLATFORM ("!! SEC_CH_UA_PLATFORM")
├─SEC_CH_UA_MOBILE ("!! SEC_CH_UA_MOBILE")
├─SEC_CH_UA ("!! SEC_CH_UA")
├─Hostname ("اسم المضيف")
├─CAPTCHA ("الحالة CAPTCHA")
├─Inspection ("* فحص الشروط")
└─ClientL10NAccepted ("تم حل اللغة")
```

* مخصص فقط من أجل تصحيح أخطاء القواعد المساعدة. غير معروض أمام المستخدمين المحظورين.

** يتطلب وظيفة بحث ASN (على سبيل المثال، عبر وحدة IP-API أو وحدة BGPView).

!! هذا تلميح عميل منخفض الإنتروبيا. تلميحات العميل بمثابة تقنية ويب تجريبية جديدة، وهي غير مدعومة على نطاق واسع حتى الآن عبر جميع المتصفحات والعملاء الرئيسيين. <em>يرى: <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA#browser_compatibility" dir="ltr" hreflang="en-US" rel="noopener noreferrer external">Sec-CH-UA - HTTP | MDN</a>.</em> يمكن أن تكون تلميحات العميل مفيدة في أخذ البصمات، ولكن بما أنها غير مدعومة على نطاق واسع، فلا ينبغي افتراض وجودها في الطلبات أو الاعتماد عليها (أي أن، الحظر بناءً على غيابهم فكرة سيئة).

##### <div dir="rtl">"timezone" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>يتم استخدام هذا لتحديد المنطقة الزمنية للاستخدام (على سبيل المثال، Africa/Cairo، America/New_York، Asia/Tokyo، Australia/Perth، Europe/Berlin، Pacific/Guam، إلخ). حدد "SYSTEM" للسماح لـ PHP بمعالجة هذا الأمر تلقائيًا.</li></ul></div>

```
timezone
├─SYSTEM ("استخدام المنطقة الزمنية الافتراضية للنظام.")
├─UTC ("UTC")
└─…آخر
```

##### <div dir="rtl">"time_offset" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>المنطقة الزمنية تعويض في غضون دقائق.</li></ul></div>

##### <div dir="rtl">"time_format" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>شكل التواريخ المستخدم من قبل CIDRAM. ويمكن إضافة خيارات إضافية عند الطلب.</li></ul></div>

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
└─…آخر
```

<strong><em>العنصر النائب – تفسير – مثال يعتمد على <span dir="ltr">2024-04-30T18:27:49+08:00</span>.</em></strong><br />
<strong><code dir="ltr">{yyyy}</code></strong> – السنة – على سبيل المثال، 2024.<br />
<strong><code dir="ltr">{yy}</code></strong> – السنة المختصرة – على سبيل المثال، 24.<br />
<strong><code dir="ltr">{Mon}</code></strong> – اسم الشهر المختصر (باللغة الإنجليزية) – على سبيل المثال، Apr.<br />
<strong><code dir="ltr">{mm}</code></strong> – الشهر الذي مع الأصفار البادئة – على سبيل المثال، 04.<br />
<strong><code dir="ltr">{m}</code></strong> – الشهر – على سبيل المثال، 4.<br />
<strong><code dir="ltr">{Day}</code></strong> – اسم اليوم المختصر (باللغة الإنجليزية) – على سبيل المثال، Tue.<br />
<strong><code dir="ltr">{dd}</code></strong> – اليوم مع الأصفار البادئة – على سبيل المثال، 30.<br />
<strong><code dir="ltr">{d}</code></strong> – اليوم – على سبيل المثال، 30.<br />
<strong><code dir="ltr">{hh}</code></strong> – الساعة مع الأصفار البادئة (تستخدم نظام 24 ساعة) – على سبيل المثال، 18.<br />
<strong><code dir="ltr">{h}</code></strong> – الساعة (تستخدم نظام 24 ساعة) – على سبيل المثال، 18.<br />
<strong><code dir="ltr">{ii}</code></strong> – الدقيقة مع الأصفار البادئة – على سبيل المثال، 27.<br />
<strong><code dir="ltr">{i}</code></strong> – الدقيقة – على سبيل المثال، 27.<br />
<strong><code dir="ltr">{ss}</code></strong> – الثواني مع الأصفار البادئة – على سبيل المثال، 49.<br />
<strong><code dir="ltr">{s}</code></strong> – الثواني – على سبيل المثال، 49.<br />
<strong><code dir="ltr">{tz}</code></strong> – المنطقة الزمنية (بدون النقطتين) – على سبيل المثال، <span dir="ltr">+0800</span>.<br />
<strong><code dir="ltr">{t:z}</code></strong> – المنطقة الزمنية (مع النقطتين) – على سبيل المثال، <span dir="ltr">+08:00</span>.

##### <div dir="rtl">"ipaddr" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>أين يمكن العثور على عنوان IP لربط الطلبات؟ (مفيدة للخدمات مثل Cloudflare). الافتراضي = REMOTE_ADDR. تحذير: لا تغير هذا إلا إذا كنت تعرف ما تفعلونه!</li></ul></div>

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (الافتراضي)")
└─…آخر
```

<div dir="rtl">أنظر أيضا:<ul dir="rtl">
<li><a dir="ltr" href="https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/">NGINX Reverse Proxy</a></li>
<li><a dir="ltr" href="http://www.squid-cache.org/Doc/config/forwarded_for/">Squid configuration directive forwarded_for</a></li>
<li><a dir="ltr" href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded">Forwarded - HTTP \| MDN</a></li>
</ul></div>

##### <div dir="rtl">"http_response_header_code" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>ما هي رسالة حالة HTTP التي يجب أن يرسلها CIDRAM عند حظر الطلبات؟</li></ul></div>

```
http_response_header_code───[الافتراضي]─[قانوني]─[حظر]
├─200 (200 OK (حسنا)): أقل قوة، ولكن الأكثر سهولة في الاستخدام.
│ من المرجح أن تفسر الطلبات الآلية هذه
│ الاستجابة على أنها إشارة إلى نجاح الطلب.
│ يوصى به للطلبات غير المحظورة.
├─403 (403 Forbidden (مُحرَّم)): أكثر قوة، ولكن أقل سهولة في الاستخدام.
│ موصى به لمعظم الظروف العامة.
├─410 (410 Gone (ذهب)): يمكن أن يسبب مشاكل عند حل الإيجابيات
│ الخاطئة، لأن بعض المتصفحات سوف تخزن رسالة
│ الحالة هذه مؤقتًا ولا ترسل طلبات لاحقة،
│ حتى بعد إلغاء الحظر. قد يكون الأكثر
│ تفضيلاً في بعض السياقات، لأنواع معينة من
│ حركة المرور.
├─418 (418 I'm a teapot (أنا إبريق شاي)): يشير إلى نكتة كذبة أبريل (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). من غير المحتمل
│ جدًا أن يفهمه أي عميل أو روبوت أو متصفح أو
│ غير ذلك. يتم توفيرها للتسلية والراحة،
│ ولكن لا يوصى بها بشكل عام.
├─451 (451 Unavailable For Legal Reasons (غير متاح لأسباب قانونية)): يوصى به عند الحظر لأسباب قانونية في
│ المقام الأول. لا ينصح به في سياقات أخرى.
└─503 (503 Service Unavailable (الخدمة غير متوفرة)): الأكثر قوة، ولكن الأقل سهولة في
  الاستخدام. يوصى به عند التعرض للهجوم أو
  عند التعامل مع حركة مرور غير مرغوب فيها
  بشكل دائم للغاية.
```

__١.__ عندما يكون "الوضع الصامت" ساريًا، سيتم استخدام رسالة حالة HTTP التي تم تحديدها بواسطة <strong><code dir="ltr">silent_mode_response_header_code⬅general</code></strong> (هذا له الأولوية القصوى).

__٢.__ عندما يتم حظر الكيان الطالب بسبب تجاوز حد المخالفة، سيتم استخدام رسالة حالة HTTP لـ "حظر".

__٣.__ عند الحظر بسبب تحديد المعدل، سيتم استخدام 429، أو عند الحظر بسبب تعارضات الموارد، سيتم استخدام رسالة حالة HTTP المحددة بواسطة <strong><code dir="ltr">conflict_response⬅signatures</code></strong> (إن الحد من المعدلات و تعارضات الموارد لها الأولوية المتساوية في هذا السياق).

__٤.__ عند الحظر بسبب قاعدة مساعدة تحدد "تجاوز رمز حالة HTTP"، سيتم استخدام تجاوز رمز حالة HTTP هذا.

__٥.__ عند الحظر لأسباب قانونية (أي عند الحظر بسبب توقيع مخصص يستخدم الكلمة المختصرة "قانوني")، سيتم استخدام رسالة حالة HTTP الخاصة بـ "قانوني".

__٦.__ بالنسبة لجميع الطلبات المحظورة الأخرى، سيتم استخدام رسالة حالة HTTP لـ "الافتراضي" (هذا له أدنى أولوية).

##### <div dir="rtl">"silent_mode" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>يجب CIDRAM إعادة توجيه بصمت محاولات وصول مرفوض بدلا من عرض الصفحة "تم رفض الوصول"؟ اذا نعم، تحديد الموقع لإعادة توجيه محاولات وصول مرفوض. ان لم، ترك هذا الحقل فارغا.</li></ul></div>

##### <div dir="rtl">"silent_mode_response_header_code" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>ما رسالة حالة HTTP التي يجب على CIDRAM إرسالها عند إعادة توجيه محاولات الوصول المحظورة بصمت؟</li></ul></div>

```
silent_mode_response_header_code
├─301 (301 Moved Permanently (منقول بشكل دائم)): يوجه العميل أن إعادة التوجيه دائمة، وأن
│ طريقة الطلب المستخدمة لإعادة التوجيه قد
│ تكون مختلفة عن طريقة الطلب المستخدمة
│ للطلب الأولي.
├─302 (302 Found (موجود)): يوجه العميل أن إعادة التوجيه مؤقتة، وأن
│ طريقة الطلب المستخدمة لإعادة التوجيه قد
│ تكون مختلفة عن طريقة الطلب المستخدمة
│ للطلب الأولي.
├─307 (307 Temporary Redirect (إعادة توجيه مؤقتة)): يوجه العميل أن إعادة التوجيه مؤقتة، وأن
│ طريقة الطلب المستخدمة لإعادة التوجيه قد
│ لا تختلف عن طريقة الطلب المستخدمة للطلب
│ الأولي.
└─308 (308 Permanent Redirect (إعادة توجيه دائمة)): يوجه العميل أن إعادة التوجيه دائمة، وأن
  طريقة الطلب المستخدمة لإعادة التوجيه قد
  لا تختلف عن طريقة الطلب المستخدمة للطلب
  الأولي.
```

بغض النظر عن الطريقة التي نوجه بها للعميل، من المهم أن نتذكر أننا في النهاية ليس لدينا أي سيطرة على ما يختاره العميل، وليس هناك ما يضمن أن العميل سوف يحترم تعليماتنا.

##### <div dir="rtl">"lang" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تحديد اللغة الافتراضية الخاصة بـ CIDRAM.</li></ul></div>

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

##### <div dir="rtl">"lang_override" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>الترجمة وفقًا لـ HTTP_ACCEPT_LANGUAGE كلما أمكن ذلك؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li></ul></div>

##### <div dir="rtl">"numbers" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>كيف تفضل الأرقام ليتم عرضها؟ حدد المثال الذي يبدو أكثر صحيح لك.</li></ul></div>

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

##### <div dir="rtl">"emailaddr" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>لو كنت تريد، يمكنك توفير عنوان البريد الإلكتروني هنا أن تعطى للمستخدمين عند أنها ممنوعة، بالنسبة لهم لاستخدامها كنقطة اتصال للحصول على الدعم والمساعدة لفي حال منهم سدت طريق الخطأ أو في ضلال. تحذير: أي عنوان البريد الإلكتروني الذي تزويد هنا وبالتأكيد سيتم شراؤها من قبل المتطفلين و برامج التطفل وكاشطات خلال المستخدمة هنا، و حينئذ، انها المستحسن أن إذا اخترت توفير عنوان البريد الإلكتروني هنا، يمكنك التأكد من أن عنوان البريد الإلكتروني الذي نورد هنا يمكن التخلص منها و/أو عنوان أنك لا تمانع في أن محتوى غير مرغوب فيه (بعبارات أخرى، وربما كنت لا تريد استخدام الرئيسية عناوين البريد الإلكتروني التجارية أو العناوين الشخصية الرئيسية الخاصة بك).</li></ul></div>

##### <div dir="rtl">"emailaddr_display_style" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>كيف تفضل أن يتم تقديم عنوان البريد الإلكتروني إلى المستخدمين؟</li></ul></div>

```
emailaddr_display_style
├─default ("رابط قابل للنقر")
└─noclick ("نص غير قابل للنقر")
```

##### <div dir="rtl">"default_dns" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>قائمة من خوادم DNS لاستخدامها في عمليات البحث عن اسم المضيف. تحذير: لا تغير هذا إلا إذا كنت تعرف ما تفعلونه!</li></ul></div>

__FAQ.__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.ar.md#ما-الذي-يمكنني-استخدامه-لـ-default_dns" hreflang="ar">ما الذي يمكنني استخدامه لـ "default_dns"؟</a></em>

##### <div dir="rtl">"default_algo" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>يحدد الخوارزمية التي سيتم استخدامها لكل كلمات المرور والجلسات المستقبلية.</li></ul></div>

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### <div dir="rtl">"statistics" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>يتحكم في المعلومات الإحصائية التي يجب تتبعها.</li></ul></div>

```
statistics───[IPv4]─[IPv6]─[آخر]
├─Blocked ("الطلبات المحظورة")
├─Banned ("طلبات محظورة")
├─Passed ("مرت الطلبات")
├─ReportOK ("تم الإبلاغ عن الطلبات إلى API الخارجية – حسنا")
└─ReportFailed ("تم الإبلاغ عن الطلبات إلى API الخارجية – فشل")
```

ملاحظة: يمكن التحكم في تتبع الإحصائيات للقواعد المساعدة من صفحة القواعد المساعدة.

##### <div dir="rtl">"statistics_captchas" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>يتحكم في المعلومات الإحصائية التي يجب تعقبها من أجل اختبارات CAPTCHA.</li></ul></div>

```
statistics_captchas───[فشل]─[إجتاز]─[تم تقديمه]
├─HCaptcha ("hCaptcha")
├─FriendlyCaptcha ("Friendly Captcha")
└─CloudflareTurnstile ("Cloudflare Turnstile")
```

ملاحظة: يمكن التحكم في تتبع الإحصائيات للقواعد المساعدة من صفحة القواعد المساعدة.

##### <div dir="rtl">"force_hostname_lookup" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>فرض بحث اسم المضيف؟ صحيح/True = نعم؛ زائفة/False = لا [افتراضي]. يتم إجراء عمليات البحث عن اسم المضيف عادة على أساس "حسب الحاجة"، ولكن يمكن إجبارها على جميع الطلبات. وقد يكون القيام بذلك مفيدا كوسيلة لتوفير معلومات أكثر تفصيلا في السجلات، ولكن قد يكون له أيضا أثر سلبي طفيف على الأداء.</li></ul></div>

##### <div dir="rtl">"allow_gethostbyaddr_lookup" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>السماح بعمليات البحث gethostbyaddr عندما يكون UDP غير متوفر؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li></ul></div>

ملاحظة: قد لا تعمل عمليات بحث IPv6 بشكل صحيح على بعض أنظمة 32 بت.

##### <div dir="rtl">"disabled_channels" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>يمكن استخدام هذا لمنع CIDRAM من استخدام قنوات معينة عند إرسال الطلبات (على سبيل المثال، عند التحديث، عند جلب بيانات تعريف المكون، إلخ).</li></ul></div>

```
disabled_channels
├─GitHub ("<span class="origin bgHRdBl">US</span> GitHub")
├─BitBucket ("<span class="origin bgHRdBl">US</span> BitBucket")
├─Codeberg ("<span class="origin bgVBkRd fgYlw">DE</span> Codeberg")
└─GoogleDNS ("<span class="origin bgHRdBl">US</span> GoogleDNS")
```

##### <div dir="rtl">"request_proxy" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>إذا كنت تريد إرسال الطلبات الصادرة عبر وكيل، حدد هذا الوكيل هنا. إذا لم يكن الأمر كذلك، اترك هذا فارغًا.</li></ul></div>

##### <div dir="rtl">"request_proxyauth" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>إذا كنت ترسل طلبات صادرة من خلال وكيل وإذا كان هذا الوكيل يتطلب اسم مستخدم وكلمة مرور، فحدد اسم المستخدم وكلمة المرور هنا (على سبيل المثال، <code dir="ltr">user:pass</code>). إذا لم يكن الأمر كذلك، اترك هذا فارغًا.</li></ul></div>

##### <div dir="rtl">"default_timeout" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>المهلة الافتراضية لاستخدامها للطلبات الخارجية؟ الافتراضي = 12 ثانية.</li></ul></div>

##### <div dir="rtl">"sensitive" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>قائمة المسارات التي يجب اعتبارها صفحات حساسة. ستتم مقارنة كل مسار مدرج مع URI المعاد بناؤه عند الحاجة. سيتم التعامل مع المسار الذي يبدأ بشرطة مائلة للأمام على أنه حرفي، ويتم مطابقته من مكون المسار للطلب فصاعدًا. سيتم التعامل مع المسار الذي يبدأ بحرف غير أبجدي رقمي وينتهي بنفس الحرف (أو نفس الحرف بالإضافة إلى علامة اختيارية "i") كتعبير عادي. سيتم التعامل مع أي نوع آخر من المسارات على أنه حرفي، ويمكن أن يتطابق مع أي جزء من URI. قد يؤثر المسار الذي يتم اعتباره صفحة حساسة على كيفية تصرف بعض الوحدات، ولكن ليس له أي تأثير آخر.</li></ul></div>

##### <div dir="rtl">"email_notification_address" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>إذا اخترت تلقي الإشعارات من CIDRAM عبر البريد الإلكتروني، على سبيل المثال، عند تفعيل قواعد مساعدة محددة، يمكنك تحديد عنوان المستلم لهذه الإشعارات هنا.</li></ul></div>

##### <div dir="rtl">"email_notification_name" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>إذا اخترت تلقي الإشعارات من CIDRAM عبر البريد الإلكتروني، على سبيل المثال، عند تفعيل قواعد مساعدة محددة، يمكنك تحديد اسم المستلم لتلك الإشعارات هنا.</li></ul></div>

##### <div dir="rtl">"email_notification_when" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>متى يتم إرسال الإشعارات بعد إنشائها.</li></ul></div>

```
email_notification_when
├─Immediately ("في الحال.")
├─After24Hours ("بعد 24 ساعة، يتم تجميعها معًا (أو عند تشغيلها يدويًا، على سبيل المثال، عبر cron).")
└─ManuallyOnly ("فقط عند تشغيله يدويًا (على سبيل المثال، عبر cron).")
```

#### <div dir="rtl">"components" (التصنيف)<br /></div>
<div dir="rtl">التكوين لتنشيط وتعطيل المكونات المستخدمة من قبل CIDRAM. عادةً ما يتم ملؤها بواسطة صفحة التحديثات، ولكن يمكن أيضًا إدارتها من هنا لتحكم أفضل وللمكونات المخصصة التي لا تتعرف عليها صفحة التحديثات.<br /><br /></div>

##### <div dir="rtl">"ipv4" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ملفات توقيع IPv4.</li></ul></div>

##### <div dir="rtl">"ipv6" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ملفات توقيع IPv6.</li></ul></div>

##### <div dir="rtl">"modules" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>الوحدات.</li></ul></div>

##### <div dir="rtl">"imports" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>الواردات. تُستخدم عادةً لتزويد معلومات تكوين المكون إلى CIDRAM.</li></ul></div>

##### <div dir="rtl">"events" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>معالجات الأحداث. تُستخدم عادةً لتعديل الطريقة التي يتصرف بها CIDRAM داخليًا أو لتوفير وظائف إضافية.</li></ul></div>

#### <div dir="rtl">"logging" (التصنيف)<br /></div>
<div dir="rtl">التكوين المتعلق بالتسجيل (باستثناء ما ينطبق على الفئات الأخرى).<br /><br /></div>

##### <div dir="rtl">"standard_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ملف يمكن قراءته بالعين لتسجيل كل محاولات الوصول سدت. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li></ul></div>

نصيحة مفيدة: يمكنك إرفاق معلومات التاريخ/الوقت بأسماء ملفات السجل باستخدام العناصر النائبة لتنسيق الوقت. يتم عرض العناصر النائبة لتنسيق الوقت المتوفرة عند <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="rtl">time_format⬅general</code></a>.

##### <div dir="rtl">"apache_style_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ملف على غرار أباتشي لتسجيل كل محاولات الوصول سدت. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li></ul></div>

نصيحة مفيدة: يمكنك إرفاق معلومات التاريخ/الوقت بأسماء ملفات السجل باستخدام العناصر النائبة لتنسيق الوقت. يتم عرض العناصر النائبة لتنسيق الوقت المتوفرة عند <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="rtl">time_format⬅general</code></a>.

##### <div dir="rtl">"serialised_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ملف تسلسل لتسجيل كل محاولات الوصول سدت. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li></ul></div>

نصيحة مفيدة: يمكنك إرفاق معلومات التاريخ/الوقت بأسماء ملفات السجل باستخدام العناصر النائبة لتنسيق الوقت. يتم عرض العناصر النائبة لتنسيق الوقت المتوفرة عند <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="rtl">time_format⬅general</code></a>.

##### <div dir="rtl">"error_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ملف لتسجيل أي أخطاء غير مميتة المكتشفة. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li></ul></div>

نصيحة مفيدة: يمكنك إرفاق معلومات التاريخ/الوقت بأسماء ملفات السجل باستخدام العناصر النائبة لتنسيق الوقت. يتم عرض العناصر النائبة لتنسيق الوقت المتوفرة عند <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="rtl">time_format⬅general</code></a>.

##### <div dir="rtl">"outbound_request_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ملف لتسجيل نتائج أي طلبات صادرة. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li></ul></div>

نصيحة مفيدة: يمكنك إرفاق معلومات التاريخ/الوقت بأسماء ملفات السجل باستخدام العناصر النائبة لتنسيق الوقت. يتم عرض العناصر النائبة لتنسيق الوقت المتوفرة عند <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="rtl">time_format⬅general</code></a>.

##### <div dir="rtl">"report_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ملف لتسجيل أي تقارير يتم إرسالها إلى واجهات برمجة التطبيقات الخارجية. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li></ul></div>

نصيحة مفيدة: يمكنك إرفاق معلومات التاريخ/الوقت بأسماء ملفات السجل باستخدام العناصر النائبة لتنسيق الوقت. يتم عرض العناصر النائبة لتنسيق الوقت المتوفرة عند <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="rtl">time_format⬅general</code></a>.

##### <div dir="rtl">"truncate" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اقتطاع ملفات السجل عندما تصل إلى حجم معين؟ القيمة هي الحجم الأقصى في بايت/كيلوبايت/ميغابايت/غيغابايت/تيرابايت الذي قد ينمو ملفات السجل إلى قبل اقتطاعه. القيمة الافتراضية 0KB تعطيل اقتطاع (ملفات السجل يمكن أن تنمو إلى أجل غير مسمى). ملاحظة: ينطبق على ملفات السجل الفردية! ولا يعتبر حجمها جماعيا.</li></ul></div>

##### <div dir="rtl">"log_rotation_limit" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>يحدد تدوير السجل عدد ملفات السجل التي يجب أن تكون موجودة في أي وقت. عند إنشاء ملفات السجل الجديدة، إذا تجاوز العدد الإجمالي لبيانات السجل الحد المحدد، فسيتم تنفيذ الإجراء المحدد. يمكنك تحديد الحد المرغوب هنا. ستعمل القيمة 0 على تعطيل تدوير السجل.</li></ul></div>

##### <div dir="rtl">"log_rotation_action" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>يحدد تدوير السجل عدد ملفات السجل التي يجب أن تكون موجودة في أي وقت. عند إنشاء ملفات السجل الجديدة، إذا تجاوز العدد الإجمالي لبيانات السجل الحد المحدد، فسيتم تنفيذ الإجراء المحدد. يمكنك تحديد الإجراء المطلوب هنا.</li></ul></div>

```
log_rotation_action
├─Delete ("احذف أقدم السجلات، حتى لا يتم تجاوز الحد.")
└─Archive ("أرشفة أولاً، ثم احذف أقدم السجلات، حتى لا يتم تجاوز الحد.")
```

##### <div dir="rtl">"log_banned_ips" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>من IP المحظورة في ملفات السجل؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li></ul></div>

##### <div dir="rtl">"log_sanitisation" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>عند استخدام صفحة سجلات الواجهة الأمامية لعرض بيانات السجل، تقوم CIDRAM بتعقيم بيانات السجل قبل عرضها، لحماية المستخدمين من هجمات XSS والتهديدات المحتملة الأخرى التي قد تحتوي عليها بيانات السجل. ومع ذلك، بشكل افتراضي، لا يتم تعقيم البيانات أثناء التسجيل. هذا لضمان الحفاظ على بيانات السجل بدقة، للمساعدة في أي تحليل شرعي قد يكون ضروريًا في المستقبل. ومع ذلك، في حالة محاولة المستخدم قراءة بيانات السجل باستخدام أدوات خارجية، وإذا لم تقم تلك الأدوات الخارجية بعملية الصرف الصحي الخاصة بها، فقد يتعرض المستخدم لهجمات XSS. إذا لزم الأمر، يمكنك تغيير السلوك الافتراضي باستخدام توجيه التكوين هذا. True = قم بتعقيم البيانات عند تسجيلها (يتم الاحتفاظ بالبيانات بدقة أقل، لكن خطر XSS أقل). False = لا تقم بتعقيم البيانات عند تسجيلها (يتم الاحتفاظ البيانات بشكل أكثر دقة، ولكن خطر XSS أعلى) [افتراضي].</li></ul></div>

#### <div dir="rtl">"frontend" (التصنيف)<br /></div>
<div dir="rtl">التكوين للواجهة الأمامية.<br /><br /></div>

##### <div dir="rtl">"frontend_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ملف لتسجيل محاولات الدخول الأمامية. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li></ul></div>

نصيحة مفيدة: يمكنك إرفاق معلومات التاريخ/الوقت بأسماء ملفات السجل باستخدام العناصر النائبة لتنسيق الوقت. يتم عرض العناصر النائبة لتنسيق الوقت المتوفرة عند <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="rtl">time_format⬅general</code></a>.

##### <div dir="rtl">"signatures_update_event_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ملف للتسجيل عند تحديث التوقيعات عبر الواجهة الأمامية. تحديد اسم الملف، أو اتركه فارغا لتعطيل.</li></ul></div>

نصيحة مفيدة: يمكنك إرفاق معلومات التاريخ/الوقت بأسماء ملفات السجل باستخدام العناصر النائبة لتنسيق الوقت. يتم عرض العناصر النائبة لتنسيق الوقت المتوفرة عند <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="rtl">time_format⬅general</code></a>.

##### <div dir="rtl">"max_login_attempts" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>الحد الأقصى لعدد محاولات تسجيل الدخول (front-end). الافتراضي = 5.</li></ul></div>

##### <div dir="rtl">"theme" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>الموضوع الذي سيتم استخدامه للواجهة الأمامية.</li></ul></div>

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
└─…آخر
```

##### <div dir="rtl">"theme_mode" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>الوضع الذي سيتم استخدامه للموضوع في الواجهة الأمامية.</li></ul></div>

```
theme_mode
├─normal ("طبيعي")
└─inverted ("معكوس")
```

##### <div dir="rtl">"magnification" <code dir="ltr">[float]</code><br /></div>
<div dir="rtl"><ul><li>تكبير الخط. افتراضي = 1.</li></ul></div>

##### <div dir="rtl">"custom_header" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تم إدراجها بتنسيق HTML في بداية جميع الصفحات الأمامية. قد يكون هذا مفيدًا في حالة رغبتك في تضمين شعار موقع ويب أو رأس مخصص أو نصوص أو ما شابه ذلك في جميع هذه الصفحات.</li></ul></div>

##### <div dir="rtl">"custom_footer" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تم إدراجها بتنسيق HTML في الجزء السفلي من جميع الصفحات الأمامية. قد يكون هذا مفيدًا في حالة رغبتك في تضمين إشعار قانوني أو رابط اتصال أو معلومات تجارية أو ما شابه ذلك في كل هذه الصفحات.</li></ul></div>

##### <div dir="rtl">"remotes" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>قائمة بالعناوين التي يستخدمها المُحدِّث لجلب البيانات الوصفية للمكون. قد يحتاج هذا إلى تعديل عند الترقية إلى إصدار رئيسي جديد، أو عند الحصول على مصدر جديد للتحديثات، ولكن في ظل الظروف العادية يجب تركه بمفرده.</li></ul></div>

##### <div dir="rtl">"enable_two_factor" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>يحدد هذا التوجيه ما إذا كان سيتم استخدام 2FA للحسابات front-end أم لا.</li></ul></div>

#### <div dir="rtl">"signatures" (التصنيف)<br /></div>
<div dir="rtl">التكوين للتوقيعات، ملفات التوقيع، الوحدات النمطية، إلخ.<br /><br /></div>

##### <div dir="rtl">"shorthand" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ضوابط لما يجب فعله بالطلب عندما يكون هناك تطابق إيجابي مع توقيع يستخدم كلمات قصيرة المحددة.</li></ul></div>

```
shorthand───[منعه.]─[صنفه.]─[عند حظره، قم بإيقاف قالب الإخراج.]
├─Attacks ("هجمات")
├─Bogon ("⁰ المريخ IP")
├─Cloud ("الخدمات السحابية")
├─Generic ("عام")
├─Legal ("¹ قانوني")
├─Malware ("البرمجيات الخبيثة")
├─Proxy ("² خدمة بروكسي")
├─Spam ("البريد المزعج")
├─Banned ("³ حظر")
├─BadIP ("³ IP غير صالح")
├─RL ("³ معدل محدود")
├─Conflict ("³ صراع")
└─Other ("⁴ آخر")
```

__0.__ إذا كان موقع الويب الخاص بك يحتاج إلى الوصول عبر LAN أو localhost، فلا منعه. إذا لم تكن هناك حاجة، يمكنك منعه.

__1.__ ملفات التوقيع القياسية لا تستخدم هذا، لكنه يظل مدعومًا في حالة ما إذا كان مفيدًا لبعض المستخدمين.

__2.__ إذا كنت تريد أن يتمكن المستخدمون من الوصول إلى موقع الويب الخاص بك عبر الوكلاء، فلا منعه. إذا لم تكن هناك حاجة، يمكنك منعه.

__3.__ لا يتم دعم الاستخدام المباشر داخل التواقيع، ولكن قد يتم استدعاؤه بوسائل أخرى في ظروف معينة.

__4.__ الحالات التي لا تستخدم فيها الكلمات القصيرة، أو لا يتعرف عليها CIDRAM.

__واحد لكل توقيع.__ قد يستدعي التوقيع عدة ملفات تعريف، لكن يمكنه استخدام كلمة قصيرة واحدة فقط. قد تكون الكلمات القصيرة المتعددة مناسبة، ولكن يمكن استخدام كلمة واحدة فقط، لذلك نحاول دائمًا استخدام الأنسب فقط.

__أولوية.__ دائمًا ما يكون للخيار المحدد الأولوية على الخيار غير المحدد. على سبيل المثال، إذا كانت هناك عدة كلمات القصيرة سارية المفعول ولكن تم تعيين كلمة واحدة فقط على أنها محظورة، فسيظل الطلب محظورًا.

__نقاط النهاية البشرية والخدمات السحابية.__ قد تشير الخدمة السحابية إلى موفري خدمات الاستضافة على الويب، أو مزارع الخوادم، أو مراكز البيانات، أو عدد من الأشياء الأخرى. تشير نقطة النهاية البشرية إلى الوسائل التي يصل بها الإنسان إلى الإنترنت، على سبيل المثال عن طريق مزود خدمة الإنترنت. عادةً ما توفر الشبكة واحدًا أو الآخر فقط، ولكنها قد توفر الاثنين معًا في بعض الأحيان. نحن نحاول عدم تحديد نقاط النهاية البشرية المحتملة على أنها خدمات سحابية. لذلك، يمكن تعريف الخدمة السحابية على أنها شيء آخر إذا كان نطاقها مشتركًا بواسطة نقاط نهاية بشرية معروفة. وبالمثل، نحاول دائمًا تحديد الخدمات السحابية، التي لا تتم مشاركة نطاقاتها بواسطة أي نقاط نهاية بشرية معروفة، على أنها خدمات سحابية. لذلك، فإن الطلب الذي تم تحديده على أنه خدمة سحابية على الأرجح لا يشارك نطاقه مع أي نقاط نهاية بشرية معروفة. وبالمثل، فإن الطلب الذي تم تحديده صراحةً من خلال الهجمات أو البريد العشوائي على الأرجح يقوم بمشاركتها. ومع ذلك، فإن الإنترنت دائمًا في حالة تغير مستمر، وتتغير أغراض الشبكات بمرور الوقت، ويتم دائمًا شراء أو بيعها النطاقات، لذلك كن مدركًا ويقظًا فيما يتعلق بالإيجابيات الخاطئة.

##### <div dir="rtl">"default_tracktime" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>المدة التي يجب أن يتم تتبع عناوين IP لها. افتراضي = 7d0°0′0″ (1 أسبوع).</li></ul></div>

##### <div dir="rtl">"infraction_limit" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>يسمح الحد الأقصى لعدد المخالفات IP يمكن أن تتكبد قبل أن يتم حظره من قبل تتبع IP. افتراضي = 10.</li></ul></div>

##### <div dir="rtl">"tracking_override" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>هل تسمح للوحدات النمطية بتجاوز خيارات التتبع؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li></ul></div>

##### <div dir="rtl">"conflict_response" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>عندما يكون هناك العديد من المحاولات المتزامنة للوصول إلى نفس الموارد (على سبيل المثال، الطلبات المتزامنة لعمليات PHP متعددة على نفس الجهاز لنفس الموارد)، فقد تفشل بعض هذه المحاولات. في حالة نادرة وغير محتملة أن يؤثر هذا على ملفات التوقيع أو الوحدات النمطية، قد يتم منع CIDRAM من اتخاذ قرار فعال بشأن الطلب. إذا حدث هذا، فهل يجب حظر الطلب، وما هي رسالة حالة HTTP التي يجب أن يرسلها CIDRAM؟</li></ul></div>

```
conflict_response
├─0 (لا تمنع الطلب.): إذا كنت تفضل حظر الطلبات فقط عندما تكون
│ متأكدًا من أنها خبيثة، أو اتخاذ جانب
│ الحذر فيما يتعلق بالإيجابيات الخاطئة (على
│ حساب حركة المرور غير المرغوب فيها التي
│ تمر أحيانًا)، فاختر هذا. إذا كنت تفضل حظر
│ الطلبات إذا لم تكن متأكدًا من سلامتها،
│ وتفضل أن تظل يقظًا (على حساب النتائج
│ الإيجابية الخاطئة في بعض الأحيان)، فاختر
│ أحد الخيارات الأخرى المتاحة.
├─409 (409 Conflict (صراع)): يوصى به في حالة تعارضات الموارد (على سبيل
│ المثال، تعارضات الدمج، وتعارضات الوصول
│ إلى الملفات، وما إلى ذلك). لا ينصح به في
│ سياقات أخرى.
└─429 (429 Too Many Requests (طلبات كثيرة جدا)): يوصى به لتحدود معدل، عند التعامل مع هجمات
  DDoS، وللوقاية من الفيضانات. لا ينصح به في
  سياقات أخرى.
```

#### <div dir="rtl">"verification" (التصنيف)<br /></div>
<div dir="rtl">التكوين للتحقق من مصدر الطلبات.<br /><br /></div>

##### <div dir="rtl">"search_engines" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>آلية الرقابة للتحقق من الطلبات الواردة من محركات البحث.</li></ul></div>

```
search_engines───[محاولة التحقق؟]─[حظر السلبيات؟]─[حظر الطلبات التي لم يتم التحقق منها؟]─[السماح بتجاوز ضربة واحدة؟]─[التوقف عن تتبع الإيجابيات؟]
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

__ما هي "الإيجابيات" و "السلبيات"؟__ عند التحقق من الهوية المقدمة من خلال الطلب، يمكن وصف النتيجة الناجحة بأنها "إيجابية" أو "سلبية". عندما يتم التأكد من أن الهوية المقدمة هي الهوية الحقيقية، فإنها توصف بأنها "إيجابية". عندما يتم التأكد من تزوير الهوية المقدمة، توصف بأنها "سلبية". ومع ذلك، فإن النتيجة غير الناجحة (على سبيل المثال، فشل التحقق، أو عدم إمكانية تحديد صحة الهوية المقدمة) لن يتم وصفها بأنها "إيجابية" أو "سلبية". بدلاً من ذلك، يمكن وصف النتيجة غير الناجحة ببساطة بأنها لم يتم التحقق منها. عندما لا يتم إجراء أي محاولة للتحقق من الهوية المقدمة من خلال طلب ما، فسيتم وصف الطلب بالمثل بأنه لم يتم التحقق منه. لا تكون المصطلحات منطقية إلا في السياق الذي يتم فيه التعرف على الهوية المقدمة من خلال الطلب، وبالتالي، حيث يكون التحقق ممكنًا. إذا كانت الهوية المقدمة لا تتطابق مع الخيارات المذكورة أعلاه، أو إذا لم يتم تقديم هوية، فإن الخيارات المقدمة أعلاه تصبح غير ملائمة.

__ما هي "التجاوزات بضربة واحدة"؟__ في بعض الحالات، قد يظل طلب التحقق الإيجابي محظورًا نتيجة لملفات التوقيع أو الوحدات النمطية أو الشروط الأخرى للطلب، وقد تكون التجاوزات ضرورية لتجنب الإيجابيات الخاطئة. عندما يكون القصد من التجاوز التعامل مع مخالفة واحدة بالضبط، لا أكثر ولا أقل، يمكن وصف هذا التجاوز بأنه "التجاوزات بضربة واحدة".

* هذا الخيار له تجاوز مناظر تحت <strong><code dir="ltr">used⬅bypasses</code></strong>. يوصى بالتأكد من وضع علامة على خانة الاختيار الخاصة بالتجاوز المقابل بنفس طريقة مربع الاختيار لمحاولة التحقق من هذا الخيار.

##### <div dir="rtl">"social_media" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>آلية الرقابة للتحقق من الطلبات الواردة من منصات التواصل الاجتماعي.</li></ul></div>

```
social_media───[محاولة التحقق؟]─[حظر السلبيات؟]─[حظر الطلبات التي لم يتم التحقق منها؟]─[السماح بتجاوز ضربة واحدة؟]─[التوقف عن تتبع الإيجابيات؟]
├─Embedly ("* Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("* Pinterest")
├─Snapchat ("* Snapchat")
└─Twitterbot ("*!! Twitterbot")
```

__ما هي "الإيجابيات" و "السلبيات"؟__ عند التحقق من الهوية المقدمة من خلال الطلب، يمكن وصف النتيجة الناجحة بأنها "إيجابية" أو "سلبية". عندما يتم التأكد من أن الهوية المقدمة هي الهوية الحقيقية، فإنها توصف بأنها "إيجابية". عندما يتم التأكد من تزوير الهوية المقدمة، توصف بأنها "سلبية". ومع ذلك، فإن النتيجة غير الناجحة (على سبيل المثال، فشل التحقق، أو عدم إمكانية تحديد صحة الهوية المقدمة) لن يتم وصفها بأنها "إيجابية" أو "سلبية". بدلاً من ذلك، يمكن وصف النتيجة غير الناجحة ببساطة بأنها لم يتم التحقق منها. عندما لا يتم إجراء أي محاولة للتحقق من الهوية المقدمة من خلال طلب ما، فسيتم وصف الطلب بالمثل بأنه لم يتم التحقق منه. لا تكون المصطلحات منطقية إلا في السياق الذي يتم فيه التعرف على الهوية المقدمة من خلال الطلب، وبالتالي، حيث يكون التحقق ممكنًا. إذا كانت الهوية المقدمة لا تتطابق مع الخيارات المذكورة أعلاه، أو إذا لم يتم تقديم هوية، فإن الخيارات المقدمة أعلاه تصبح غير ملائمة.

__ما هي "التجاوزات بضربة واحدة"؟__ في بعض الحالات، قد يظل طلب التحقق الإيجابي محظورًا نتيجة لملفات التوقيع أو الوحدات النمطية أو الشروط الأخرى للطلب، وقد تكون التجاوزات ضرورية لتجنب الإيجابيات الخاطئة. عندما يكون القصد من التجاوز التعامل مع مخالفة واحدة بالضبط، لا أكثر ولا أقل، يمكن وصف هذا التجاوز بأنه "التجاوزات بضربة واحدة".

* هذا الخيار له تجاوز مناظر تحت <strong><code dir="ltr">used⬅bypasses</code></strong>. يوصى بالتأكد من وضع علامة على خانة الاختيار الخاصة بالتجاوز المقابل بنفس طريقة مربع الاختيار لمحاولة التحقق من هذا الخيار.

** يتطلب وظيفة بحث ASN (على سبيل المثال، عبر وحدة IP-API أو وحدة BGPView).

*!! احتمالية عالية للتسبب في نتائج إيجابية خاطئة بسبب iMessage.

##### <div dir="rtl">"other" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>آلية الرقابة للتحقق من أنواع الطلبات الأخرى حيثما أمكن ذلك.</li></ul></div>

```
other───[محاولة التحقق؟]─[حظر السلبيات؟]─[حظر الطلبات التي لم يتم التحقق منها؟]─[السماح بتجاوز ضربة واحدة؟]─[التوقف عن تتبع الإيجابيات؟]
├─AdSense ("AdSense")
├─AmazonAdBot ("* AmazonAdBot")
├─ChatGPT-User ("!! ChatGPT-User")
├─GPTBot ("!! GPTBot")
├─OAI-SearchBot ("!! OAI-SearchBot")
└─UptimeRobot ("UptimeRobot")
```

__ما هي "الإيجابيات" و "السلبيات"؟__ عند التحقق من الهوية المقدمة من خلال الطلب، يمكن وصف النتيجة الناجحة بأنها "إيجابية" أو "سلبية". عندما يتم التأكد من أن الهوية المقدمة هي الهوية الحقيقية، فإنها توصف بأنها "إيجابية". عندما يتم التأكد من تزوير الهوية المقدمة، توصف بأنها "سلبية". ومع ذلك، فإن النتيجة غير الناجحة (على سبيل المثال، فشل التحقق، أو عدم إمكانية تحديد صحة الهوية المقدمة) لن يتم وصفها بأنها "إيجابية" أو "سلبية". بدلاً من ذلك، يمكن وصف النتيجة غير الناجحة ببساطة بأنها لم يتم التحقق منها. عندما لا يتم إجراء أي محاولة للتحقق من الهوية المقدمة من خلال طلب ما، فسيتم وصف الطلب بالمثل بأنه لم يتم التحقق منه. لا تكون المصطلحات منطقية إلا في السياق الذي يتم فيه التعرف على الهوية المقدمة من خلال الطلب، وبالتالي، حيث يكون التحقق ممكنًا. إذا كانت الهوية المقدمة لا تتطابق مع الخيارات المذكورة أعلاه، أو إذا لم يتم تقديم هوية، فإن الخيارات المقدمة أعلاه تصبح غير ملائمة.

__ما هي "التجاوزات بضربة واحدة"؟__ في بعض الحالات، قد يظل طلب التحقق الإيجابي محظورًا نتيجة لملفات التوقيع أو الوحدات النمطية أو الشروط الأخرى للطلب، وقد تكون التجاوزات ضرورية لتجنب الإيجابيات الخاطئة. عندما يكون القصد من التجاوز التعامل مع مخالفة واحدة بالضبط، لا أكثر ولا أقل، يمكن وصف هذا التجاوز بأنه "التجاوزات بضربة واحدة".

* هذا الخيار له تجاوز مناظر تحت <strong><code dir="ltr">used⬅bypasses</code></strong>. يوصى بالتأكد من وضع علامة على خانة الاختيار الخاصة بالتجاوز المقابل بنفس طريقة مربع الاختيار لمحاولة التحقق من هذا الخيار.

!! من المحتمل أن يرغب معظم المستخدمين في حظر هذا، بغض النظر عما إذا كان حقيقيًا أو مزيفًا. يمكن تحقيق ذلك من خلال عدم تحديد "محاولة التحقق" واختيار "حظر الطلبات التي لم يتم التحقق منها". ومع ذلك، نظرًا لأن بعض المستخدمين قد يرغبون في التمكن من التحقق من هذه الطلبات (من أجل حظر السلبيات مع السماح بالإيجابيات)، فبدلاً من حظر مثل هذه الطلبات عبر الوحدات النمطية، يتم توفير خيارات للتعامل مع هذه الطلبات هنا.

##### <div dir="rtl">"adjust" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>آلية لضبط الميزات الأخرى عندما تكون في سياق التحقق.</li></ul></div>

```
adjust───[قمع hCaptcha]─[قمع Friendly Captcha]─[قمع Cloudflare Turnstile]
├─Negatives ("السلبيات المحظورة")
└─NonVerified ("المحظور التي لم يتم التحقق")
```

#### <div dir="rtl">"captcha" (التصنيف)<br /></div>
<div dir="rtl">التكوين ل CAPTCHA (يوفر وسيلة للبشر لاستعادة الوصول عند حجبه).<br /><br /></div>

##### <div dir="rtl">"usemode" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>متى يجب تقديم CAPTCHA؟ يمكنك تحديد السلوك المفضل لكل مزود مدعوم هنا.</li></ul></div>

```
usemode───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─0 (أبدا.)
├─1 (فقط عندما يتم حظره، ضمن حدود التواقيع، وليس محظور.)
├─2 (فقط عندما يتم حظره، ويتم تمييزها خصيصًا للاستخدام، وضمن حدود التواقيع، وليس محظور.)
├─3 (فقط عندما ضمن حدود التواقيع، وليس محظور (بغض النظر عما إذا كان حظره).)
├─4 (فقط عندما لا يتم حظره.)
├─5 (فقط عندما لا يتم حظره، أو عندما يتم تمييزها خصيصًا للاستخدام، وضمن حدود التواقيع، وليس محظور.)
└─6 (فقط عندما لا يتم حظره، عند طلبات الصفحات الحساسة.)
```

ملاحظة: لا تحتاج الطلبات المدرجة في القائمة البيضاء أو التي تم التحقق منها والتي لم يتم حظرها إلى إكمال اختبار CAPTCHA.

لاحظ أيضًا: يمكن أن توفر اختبارات CAPTCHA طبقة إضافية مفيدة من الحماية ضد الروبوتات وأنواع مختلفة من الطلبات الآلية الضارة، ولكنها لن توفر أي حماية ضد أي شخص ضار.

يمكن "وضع علامة على الطلبات للاستخدام" عبر قواعد مساعدة.

يتم تحديد ما إذا كان الطلب يعتبر "حساسًا" من خلال <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_sensitive"><code dir="rtl">sensitive⬅general</code></a>.

يتم تحديد "حد التوقيع" بواسطة <a onclick="javascript:toggleconfigNav('captchaRow','captchaShowLink')" href="#config_captcha_signature_limit"><code dir="rtl">signature_limit⬅captcha</code></a>.

##### <div dir="rtl">"nonblocked_status_code" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>ما هو رمز الحالة الذي يجب استخدامه عند عرض CAPTCHA للطلبات غير المحظورة؟</li></ul></div>

```
nonblocked_status_code───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─200 (200 OK (حسنا)): أقل قوة، ولكن الأكثر سهولة في الاستخدام.
│ من المرجح أن تفسر الطلبات الآلية هذه
│ الاستجابة على أنها إشارة إلى نجاح الطلب.
│ يوصى به للطلبات غير المحظورة.
├─403 (403 Forbidden (مُحرَّم)): أكثر قوة، ولكن أقل سهولة في الاستخدام.
│ موصى به لمعظم الظروف العامة.
├─418 (418 I'm a teapot (أنا إبريق شاي)): يشير إلى نكتة كذبة أبريل (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). من غير المحتمل
│ جدًا أن يفهمه أي عميل أو روبوت أو متصفح أو
│ غير ذلك. يتم توفيرها للتسلية والراحة،
│ ولكن لا يوصى بها بشكل عام.
├─429 (429 Too Many Requests (طلبات كثيرة جدا)): يوصى به لتحدود معدل، عند التعامل مع هجمات
│ DDoS، وللوقاية من الفيضانات. لا ينصح به في
│ سياقات أخرى.
└─451 (451 Unavailable For Legal Reasons (غير متاح لأسباب قانونية)): يوصى به عند الحظر لأسباب قانونية في
  المقام الأول. لا ينصح به في سياقات أخرى.
```

##### <div dir="rtl">"api" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>أي API لاستخدام؟</li></ul></div>

```
api───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─v0 ("v0")
├─v1 ("v1")
├─Invisible ("v1 (غير مرئى)")
└─v2 ("v2")
```

##### <div dir="rtl">"messages" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>الرسائل التي سيتم عرضها بجوار رموز CAPTCHA.</li></ul></div>

```
messages───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─cookie_warning ("إظهار تحذير ملف تعريف الارتباط؟): اعتمادًا على قوانين الخصوصية في بلدك أو
│ ولايتك (على سبيل المثال، GDPR/DSGVO في الاتحاد
│ الأوروبي، LGPD في البرازيل، وما إلى ذلك)، قد
│ يكون هذا مطلوبًا قانونيًا."
└─api_message ("إظهار رسالة API؟): تعليمات للمستخدم، مناسبة لواجهة برمجة
  التطبيقات المستخدمة، فيما يتعلق باستكمال
  اختبار CAPTCHA."
```

##### <div dir="rtl">"lockto" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ما الذي يجب قفل CAPTCHA عليه.</li></ul></div>

```
lockto───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─ip ("قفل CAPTCHA على عنوان IP الخاص بالمستخدم الذي يكمل CAPTCHA ولكن ليس للمستخدم الفعلي.): لا يتم استخدام ملفات تعريف الارتباط
│ لتحديد هوية المستخدمين. عند استعادة
│ الوصول بسبب الإكمال الناجح لـ CAPTCHA، يتم
│ تطبيقه على أي شخص يتصل من نفس عنوان IP."
├─user ("قفل CAPTCHA للمستخدم الذي يكمل CAPTCHA ولكن ليس لعنوان IP الخاص به.): يتم استخدام ملفات تعريف الارتباط لتحديد
│ هوية المستخدمين. عندما يتم استعادة الوصول
│ بسبب الإكمال الناجح لـ CAPTCHA، فإن هذا ينطبق
│ فقط على المستخدم الذي أكمل CAPTCHA، وطالما
│ ظلت ملفات تعريف الارتباط الخاصة به صالحة،
│ فسوف تستمر، حتى إذا تغير عنوان IP الخاص به."
└─both ("قفل CAPTCHA للمستخدم الذي يكمل CAPTCHA وكذلك لعنوان IP الخاص به.): يتم استخدام ملفات تعريف الارتباط لتحديد
  هوية المستخدمين. عند استعادة الوصول بسبب
  الإكمال الناجح لـ CAPTCHA، ينطبق هذا فقط على
  المستخدم الذي أكمل CAPTCHA، ولن يستمر إذا
  تغير عنوان IP الخاص به."
```

##### <div dir="rtl">"hcaptcha_sitekey" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>إذا كنت ترغب في استخدام hCaptcha مع CIDRAM، فستحتاج إلى إدخال قيمة هنا. إذا لم يكن الأمر كذلك، فيمكنك تجاهلها.</li></ul></div>

يمكن العثور على هذه القيمة في لوحة التحكم الخاصة بخدمة CAPTCHA.

<div dir="rtl">أنظر أيضا:<ul dir="rtl">
<li><a dir="ltr" href="https://dashboard.hcaptcha.com/overview">HCaptcha Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"hcaptcha_secret" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>إذا كنت ترغب في استخدام hCaptcha مع CIDRAM، فستحتاج إلى إدخال قيمة هنا. إذا لم يكن الأمر كذلك، فيمكنك تجاهلها.</li></ul></div>

يمكن العثور على هذه القيمة في لوحة التحكم الخاصة بخدمة CAPTCHA.

<div dir="rtl">أنظر أيضا:<ul dir="rtl">
<li><a dir="ltr" href="https://dashboard.hcaptcha.com/overview">HCaptcha Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"friendly_sitekey" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>إذا كنت ترغب في استخدام Friendly Captcha مع CIDRAM، فستحتاج إلى إدخال قيمة هنا. إذا لم يكن الأمر كذلك، فيمكنك تجاهلها.</li></ul></div>

يمكن العثور على هذه القيمة في لوحة التحكم الخاصة بخدمة CAPTCHA.

<div dir="rtl">أنظر أيضا:<ul dir="rtl">
<li><a dir="ltr" href="https://app.friendlycaptcha.eu/dashboard">Friendly Captcha Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"friendly_apikey" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>إذا كنت ترغب في استخدام Friendly Captcha مع CIDRAM، فستحتاج إلى إدخال قيمة هنا. إذا لم يكن الأمر كذلك، فيمكنك تجاهلها.</li></ul></div>

يمكن العثور على هذه القيمة في لوحة التحكم الخاصة بخدمة CAPTCHA.

<div dir="rtl">أنظر أيضا:<ul dir="rtl">
<li><a dir="ltr" href="https://app.friendlycaptcha.eu/dashboard">Friendly Captcha Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"turnstile_sitekey" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>إذا كنت ترغب في استخدام Cloudflare Turnstile مع CIDRAM، فستحتاج إلى إدخال قيمة هنا. إذا لم يكن الأمر كذلك، فيمكنك تجاهلها.</li></ul></div>

يمكن العثور على هذه القيمة في لوحة التحكم الخاصة بخدمة CAPTCHA.

<div dir="rtl">أنظر أيضا:<ul dir="rtl">
<li><a dir="ltr" href="https://dash.cloudflare.com/">Cloudflare Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"turnstile_secret" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>إذا كنت ترغب في استخدام Cloudflare Turnstile مع CIDRAM، فستحتاج إلى إدخال قيمة هنا. إذا لم يكن الأمر كذلك، فيمكنك تجاهلها.</li></ul></div>

يمكن العثور على هذه القيمة في لوحة التحكم الخاصة بخدمة CAPTCHA.

<div dir="rtl">أنظر أيضا:<ul dir="rtl">
<li><a dir="ltr" href="https://dash.cloudflare.com/">Cloudflare Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"expiry" <code dir="ltr">[float]</code><br /></div>
<div dir="rtl"><ul><li>عدد الساعات لنتذكر حالات اختبار CAPTCHA. الافتراضي = 720 (١ شهر).</li></ul></div>

##### <div dir="rtl">"signature_limit" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>الحد الأقصى لعدد التوقيعات المسموح بها قبل سحب عرض CAPTCHA. افتراضي = 1.</li></ul></div>

##### <div dir="rtl">"log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تسجيل جميع محاولات اختبار CAPTCHA؟ إذا كانت الإجابة بنعم، حدد اسم لاستخدامه في ملف السجل. ان لم، ترك هذا الحقل فارغا.</li></ul></div>

نصيحة مفيدة: يمكنك إرفاق معلومات التاريخ/الوقت بأسماء ملفات السجل باستخدام العناصر النائبة لتنسيق الوقت. يتم عرض العناصر النائبة لتنسيق الوقت المتوفرة عند <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="rtl">time_format⬅general</code></a>.

#### <div dir="rtl">"legal" (التصنيف)<br /></div>
<div dir="rtl">التكوين للمتطلبات القانونية.<br /><br /></div>

##### <div dir="rtl">"pseudonymise_ip_addresses" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>إخفاء عناوين IP عند كتابة السجلات؟ صحيح/True = نعم [افتراضي]؛ زائفة/False = لا.</li></ul></div>

##### <div dir="rtl">"privacy_policy" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>عنوان سياسة الخصوصية ذات الصلة ليتم عرضها في تذييل الصفحات التي تم إنشاؤها. حدد عنوان URL، أو اتركه فارغًا لتعطيله.</li></ul></div>

#### <div dir="rtl">"template_data" (التصنيف)<br /></div>
<div dir="rtl">التكوين للقوالب والسمات.<br /><br /></div>

##### <div dir="rtl">"theme" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>الموضوع الذي سيتم استخدامه لأحداث الحظر وطلبات CAPTCHA.</li></ul></div>

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
└─…آخر
```

##### <div dir="rtl">"theme_mode" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>الوضع للموضوع الذي سيتم استخدامه لأحداث الحظر وطلبات CAPTCHA.</li></ul></div>

```
theme_mode
├─normal ("طبيعي")
└─inverted ("معكوس")
```

##### <div dir="rtl">"magnification" <code dir="ltr">[float]</code><br /></div>
<div dir="rtl"><ul><li>تكبير الخط. افتراضي = 1.</li></ul></div>

##### <div dir="rtl">"css_url" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>URL ملف CSS لمواضيع مخصصة.</li></ul></div>

##### <div dir="rtl">"block_event_title" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>عنوان الصفحة المراد عرضه لحظر الأحداث.</li></ul></div>

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("تم رفض الوصول!")
└─…آخر
```

##### <div dir="rtl">"captcha_title" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>عنوان الصفحة المراد عرضه لطلبات CAPTCHA.</li></ul></div>

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…آخر
```

##### <div dir="rtl">"custom_header" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تم إدراجها بتنسيق HTML في بداية كافة صفحات "تم رفض الوصول". قد يكون هذا مفيدًا في حالة رغبتك في تضمين شعار موقع ويب أو رأس مخصص أو نصوص أو ما شابه ذلك في جميع هذه الصفحات.</li></ul></div>

##### <div dir="rtl">"custom_footer" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تم إدراجها بتنسيق HTML في الجزء السفلي من كافة صفحات "تم رفض الوصول". قد يكون هذا مفيدًا في حالة رغبتك في تضمين إشعار قانوني أو رابط اتصال أو معلومات تجارية أو ما شابه ذلك في كل هذه الصفحات.</li></ul></div>

#### <div dir="rtl">"rate_limiting" (التصنيف)<br /></div>
<div dir="rtl">التكوين للحد من معدل (غير مستحسن للاستخدام العام).

ضع في اعتبارك أنه كما هو الحال مع جميع ميزات CIDRAM الأخرى، لا يمكن تطبيق ميزة تحديد معدل CIDRAM إلا على تلك الصفحات والموارد التي يتصل بها CIDRAM. وهذا يعني عادةً أن الموارد غير المرتبطة بـ PHP لن يتم تغطيتها إلا عندما يتم تقديمها صراحةً بواسطة موارد PHP المتصلة. إذا كنت قادرًا على استخدام وحدة خادم أو cPanel أو أي أداة شبكة أخرى لفرض الحد من المعدل، فسيكون من الأفضل استخدام ذلك بدلاً من ميزة الحد من المعدل في CIDRAM. ضع في اعتبارك أيضًا أن المستخدم الحريص والمصمم يمكنه بسهولة التحايل على الحد الأقصى للمعدل عن طريق تدوير عنوان IP الخاص به، أو عن طريق التبديل إلى موفر وكيل أو VPN لا يعرفه CIDRAM بعد، وتذكر أن الحد الأقصى للمعدل يمكن أن يكون مزعجًا للغاية للمستخدمين النهائيين الفعليين. قد يكون ذلك ضروريًا في بعض الأحيان، لكنه نادرًا ما يكون مرغوبًا فيه.<br /><br /></div>

##### <div dir="rtl">"max_bandwidth" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>أقصى قدر من عرض النطاق الترددي المسموح به خلال فترة السماح. عندما يتم تجاوزت، يتم تمكين حدود السعر للطلبات المستقبلية. تعمل القيمة 0 على تعطيل هذا النوع من تحديد السرعة. افتراضي = 0KB.</li></ul></div>

##### <div dir="rtl">"max_requests" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>الحد الأقصى لعدد الطلبات المسموح بها خلال فترة السماح. عندما يتم تجاوزت، يتم تمكين حدود السعر للطلبات المستقبلية. تعمل القيمة 0 على تعطيل هذا النوع من تحديد السرعة. افتراضي = 0.</li></ul></div>

##### <div dir="rtl">"precision_ipv4" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>الدقة المستخدمة عند مراقبة استخدام IPv4. قيمة تعكس حجم كتلة CIDR. تعيين إلى 32 للحصول على أفضل دقة. افتراضي = 32.</li></ul></div>

##### <div dir="rtl">"precision_ipv6" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>الدقة المستخدمة عند مراقبة استخدام IPv6. قيمة تعكس حجم كتلة CIDR. تعيين إلى 128 للحصول على أفضل دقة. افتراضي = 128.</li></ul></div>

##### <div dir="rtl">"allowance_period" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>المدة لمراقبة الاستخدام. افتراضي = 0°0′0″.</li></ul></div>

##### <div dir="rtl">"exceptions" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>استثناءات (بمعنى آخر، الطلبات التي لا ينبغي أن تكون محدودة). له تأثير فقط عند تمكين الحد.</li></ul></div>

```
exceptions
├─Whitelisted ("طلبات القائمة البيضاء")
├─Verified ("الطلبات التي تم التحقق منها من محركات البحث ووسائل التواصل الاجتماعي")
└─FE ("طلبات للواجهة الأمامية CIDRAM")
```

##### <div dir="rtl">"segregate" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>هل يجب فصل أو مشاركة الحصص الخاصة بالمجالات والمضيفين المختلفين؟ True = سيتم فصل الحصص. False = سيتم تقاسم الحصص [افتراضي].</li></ul></div>

#### <div dir="rtl">"supplementary_cache_options" (التصنيف)<br /></div>
<div dir="rtl">خيارات ذاكرة التخزين المؤقت التكميلية. ملاحظة: قد يؤدي تغيير هذه القيم إلى تسجيل خروجك.<br /><br /></div>

##### <div dir="rtl">"prefix" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>سيتم إضافة القيمة المحددة هنا إلى جميع مفاتيح إدخال ذاكرة التخزين المؤقت. افتراضي = "CIDRAM_". عند وجود عدة عمليات تثبيت على نفس الخادم، يمكن أن يكون ذلك مفيدًا للحفاظ على ذاكرة التخزين المؤقت منفصلة عن بعضها البعض.</li></ul></div>

##### <div dir="rtl">"enable_apcu" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>يحدد هذا ما إذا كنت تريد استخدام APCu للتخزين المؤقت. افتراضي = True (صحيح).</li></ul></div>

##### <div dir="rtl">"enable_memcached" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>يحدد هذا ما إذا كنت تريد استخدام Memcached للتخزين المؤقت. افتراضي = False (زائفة).</li></ul></div>

##### <div dir="rtl">"enable_redis" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>يحدد هذا ما إذا كنت تريد استخدام Redis للتخزين المؤقت. افتراضي = False (زائفة).</li></ul></div>

##### <div dir="rtl">"enable_pdo" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>يحدد هذا ما إذا كنت تريد استخدام PDO للتخزين المؤقت. افتراضي = False (زائفة).</li></ul></div>

##### <div dir="rtl">"memcached_host" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>قيمة المضيف Memcached. افتراضي = localhost.</li></ul></div>

##### <div dir="rtl">"memcached_port" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>قيمة منفذ Memcached. افتراضي = "11211".</li></ul></div>

##### <div dir="rtl">"redis_host" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>قيمة المضيف Redis. افتراضي = localhost.</li></ul></div>

##### <div dir="rtl">"redis_port" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>قيمة منفذ Redis. افتراضي = "6379".</li></ul></div>

##### <div dir="rtl">"redis_timeout" <code dir="ltr">[float]</code><br /></div>
<div dir="rtl"><ul><li>Redis قيمة المهلة. افتراضي = "2.5".</li></ul></div>

##### <div dir="rtl">"redis_database_number" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>رقم قاعدة بيانات Redis. افتراضي = 0. ملاحظة: لا يمكن استخدام قيم غير 0 مع Redis Cluster.</li></ul></div>

##### <div dir="rtl">"pdo_dsn" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>قيمة PDO DSN. افتراضي = "mysql:dbname=cidram;host=localhost;port=3306".</li></ul></div>

__FAQ.__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.ar.md#user-content-HOW_TO_USE_PDO" hreflang="ar">ما هو "PDO DSN"؟ كيف يمكنني استخدام PDO مع CIDRAM؟</a></em>

##### <div dir="rtl">"pdo_username" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>PDO اسم المستخدم.</li></ul></div>

##### <div dir="rtl">"pdo_password" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>PDO كلمه السر.</li></ul></div>

#### <div dir="rtl">"bypasses" (التصنيف)<br /></div>
<div dir="rtl">التكوين لتجاوز التوقيع الافتراضي.<br /><br /></div>

##### <div dir="rtl">"used" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ما هي التجاوزات التي يجب استخدامها؟</li></ul></div>

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


### <div dir="rtl">٦. <a name="SECTION6"></a>شكل/تنسيق التوقيع</div>

<div dir="rtl">أنظر أيضا:<br /></div>
<div dir="rtl"><ul>
 <li><a href="#user-content-WHAT_IS_A_SIGNATURE">ما هو "التوقيع"؟</a></li>
</ul></div>

#### <div dir="rtl">٦.٠ مبادئ (بالنسبة إلى ملفات التوقيع)<br /><br /></div>

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

<div dir="rtl">يجب أن يكون تدوين CIDR دقيق. يجب أن أعداد تقسم بالتساوي (على سبيل المثال، من أجل الحيلولة دون<code dir="ltr">"10.128.0.0"-"11.127.255.255"</code>، <code dir="ltr">"10.128.0.0/8"</code> لن تكون صالحة، لكن <code dir="ltr">"10.128.0.0/9"</code> و <code dir="ltr">"11.0.0.0/9"</code> على ما يرام).<br /><br /></div>

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

#### <div dir="rtl">٦.١ علامات<br /><br /></div>

##### <div dir="rtl">٦.١.٠ علامات القسم<br /><br /></div>

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

<div dir="rtl">في المثال أعلاه <code dir="ltr">"1.2.3.4/32"</code> و <code dir="ltr">"2.3.4.5/32"</code> وصفت بأنها "IPv4"، بينما <code dir="ltr">"4.5.6.7/32"</code> و <code dir="ltr">"5.6.7.8/32"</code> وصفت بأنها "القسم 1".<br /><br /></div>

<div dir="rtl">ويمكن تطبيق المنطق نفسه لفصل الأنواع الأخرى من العلامات أيضا.<br /><br /></div>

<div dir="rtl">على وجه الخصوص، يمكن أن تكون علامات القسم مفيدة جدا لتصحيح الأخطاء عندما تحدث ايجابيات كاذبة، من خلال توفير وسيلة سهلة من موقع المصدر الدقيق للمشكلة، ويمكن أن تكون مفيدة جدا لتصفية إدخالات ملف السجل عند عرض ملفات السجل عبر صفحة سجلات الواجهة الأمامية (يمكن النقر على أسماء الأقسام عبر صفحة سجلات الواجهة الأمامية ويمكن استخدامها كمعايير تصفية). إذا تم حذف علامات الأقسام لبعض التواقيع المحددة، عندما يتم تشغيل تلك التوقيعات، يستخدم CIDRAM اسم ملف التوقيع مع نوع عنوان إب المحظور (IPv4 أو IPv6) كمرجع، وبالتالي، الأقسام القسم اختيارية تماما. ويمكن التوصية في بعض الحالات، على سبيل المثال، عندما تكون ملفات التوقيع مسماة بشكل غامض أو عندما يكون من الصعب على نحو آخر تحديد مصدر التوقيعات بشكل واضح مما يتسبب في حظر الطلب.<br /><br /></div>

##### <div dir="rtl">٦.١.١ علامات انتهاء الصلاحية<br /><br /></div>

<div dir="rtl">في المثال التالي، سوف التوقيعات تنتهي بعد مرور بعض الوقت:<br /><br /></div>

```
# القسم ١.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

<div dir="rtl">لن يتم تشغيل التوقيعات منتهية الصلاحية على أي طلب، بغض النظر عن ما.<br /><br /></div>

##### <div dir="rtl">٦.١.٢ علامات المنشأ<br /><br /></div>

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

##### <div dir="rtl">٦.١.٣ علامات احترام<br /><br /></div>

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

#### <div dir="rtl">٦.١.٤ علامات الملف الشخصي<br /><br /></div>

<div dir="rtl">توفر علامات الملف الشخصي وسيلة تعرض معلومات إضافية في صفحة اختبار IP، ويمكن الاستفادة منها من خلال الوحدات النمطية والقواعد المساعدة لسلوك أكثر تعقيدًا واتخاذ قرارات دقيقة.<br /><br /></div>

<div dir="rtl">يتم استخدام علامات الملف الشخصي بشكل مشابه لأنواع أخرى من العلامات. يمكن استخدام قيم علامات الملف الشخصي كشرط للوحدات النمطية والقواعد المساعدة. يمكن أن توفر علامات ملف التعريف قيمًا متعددة عن طريق فصل هذه القيم بفاصلة منقوطة. لا يرى المستخدم النهائي أبدًا قيم علامات الملف الشخصي.<br /><br /></div>

<div dir="rtl">مثال:<br /><br /></div>

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### <div dir="rtl">٦.٢ YAML<br /><br /></div>

#### <div dir="rtl">٦.٢.٠ أساسيات YAML<br /><br /></div>

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

#### <div dir="rtl">٦.٣ معلومات اضافية<br /><br /></div>

##### <div dir="rtl">٦.٣.٠ تجاهل أقسام التوقيع<br /><br /></div>

<div dir="rtl">إذا كنت تريد CIDRAM تجاهل تماما بعض المقاطع، يمكنك استخدام ملف "ignore.dat" لتحديد المقاطع التي ليمكن تجاهلها. على سطر جديد، اكتب "Ignore"، متبوعا بمسافة، يليه اسم المقطع ليمكن تجاهله (راجع الأمثلة أدناه).<br /><br /></div>

```
Ignore القسم ١
```

<div dir="rtl">ويمكن تحقيق ذلك أيضًا من خلال صفحة "لقائمة الأقسام" CIDRAM لfront-end.<br /><br /></div>

##### <div dir="rtl">٦.٣.١ القواعد المساعدة<br /><br /></div>

<div dir="rtl">إذا كنت تشعر أن كتابة ملفات التوقيع المخصصة الخاصة بك أو وحدات مخصصة معقدة للغاية بالنسبة لك، قد يكون بديل أبسط هو استخدام صفحة "القواعد المساعدة" الخاصة بـ CIDRAM لfront-end. من خلال تحديد الخيارات المناسبة وتحديد تفاصيل حول أنواع معينة من الطلبات، يمكنك توجيه CIDRAM إلى كيفية الرد على تلك الطلبات. يتم تنفيذ "القواعد المساعدة" بعد الانتهاء من جميع ملفات التوقيع والوحدات النمطية بالفعل التنفيذ.<br /><br /></div>

##### <div dir="rtl">٦.٣.٢ حفظ وتفعيل ملفات التوقيع المخصصة<br /><br /></div>

<div dir="rtl">بالنسبة لـ CIDRAM v2 والإصدارات الأقدم، ستجد ملفين في vault: <code dir="ltr">ipv4_custom.dat.RenameMe</code> و <code dir="ltr">ipv6_custom.dat.RenameMe</code>. يمكنك حفظ التوقيعات المخصصة في تلك الملفات، أو إذا كنت تفضل ذلك، يمكنك إنشاء ملفات جديدة لتوقيعاتك المخصصة، وتسميتها كما تشاء. بالنسبة لـ CIDRAM v2 والإصدارات الأقدم، يجب حفظ ملفات التوقيع المخصصة في قاعدة دليل "vault".<br /><br /></div>

<div dir="rtl">بالنسبة لـ CIDRAM v3 وما بعده، لا توجد ملفات مُعدة مسبقًا للتوقيعات المخصصة، ولكن يمكنك أيضًا إنشاء ملفات جديدة لتوقيعاتك المخصصة، وتسميتها كما تشاء. بالنسبة لـ CIDRAM v3 وما بعده، يجب حفظ ملفات التوقيع المخصصة في دليل "signatures" المُعد مسبقًا لتثبيت CIDRAM الخاص بك.<br /><br /></div>

<div dir="rtl">لتفعيل ملفات التوقيع المخصصة، يجب الإشارة إليها بواسطة توجيهات التكوين "ipv4" أو "ipv6" في ملف التكوين الخاص بك (اعتمادًا على ما إذا كانت ملفات التوقيع المخصصة مخصصة لتوقيعات IPv4 أو IPv6).<br /><br /></div>

<div dir="rtl">بالنسبة لـ CIDRAM v2 والإصدارات الأقدم، يتم العثور على "ipv4" و "ipv6" ضمن فئة تكوين "signatures".<br /><br /></div>

<div dir="rtl">بالنسبة لـ CIDRAM v3 وما بعده، يتم العثور على "ipv4" و "ipv6" ضمن فئة تكوين "components".<br /><br /></div>

#### <div dir="rtl">٦.٤ <a name="MODULE_BASICS"></a>مبادئ (للوحدات)<br /><br /></div>

<div dir="rtl">وحدات يمكن استخدامها لتوسيع وظائف CIDRAM، أداء مهام إضافية، أو معالجة منطق إضافي.<br /><br /></div>

<div dir="rtl">لأن يتم كتابة وحدات كملفات PHP، إذا كنت على دراية كافية مع مصدر برنامج CIDRAM، يمكنك هيكلة وحدات المكون التواقيع ولكن تريد (في إطار ما هو ممكن مع فب).<br /><br /></div>

<div dir="rtl"><em>ملحوظة: إذا كنت غير مريح العمل مع التعليمات البرمجية PHP، كتابة الوحدات الخاصة بك لا ينصح.</em><br /><br /></div>

<div dir="rtl">يتم توفير بعض الوظائف من قبل CIDRAM التي ينبغي أن تجعل من أبسط وأسهل لكتابة وحدات الخاصة بك. وترد أدناه معلومات عن هذه الوظيفة.<br /><br /></div>

#### <div dir="rtl">٦.٥ المكون نمطية<br /><br /></div>

##### <div dir="rtl">٦.٥.٠ <code dir="ltr">$this->trigger</code></div>

<div dir="rtl">وعادة ما تكتب تواقيع المكون مع <code dir="ltr">$this->trigger</code>. في معظم الحالات، هذا الإغلاق سيكون أكثر أهمية من أي شيء آخر لغرض كتابة وحدات.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$this->trigger</code> يقبل ٤ المعلمات: <code dir="ltr">$Condition</code>، <code dir="ltr">$ReasonShort</code>، <code dir="ltr">$ReasonLong</code> (اختياري)، <code dir="ltr">$DefineOptions</code> (اختياري).<br /><br /></div>

<div dir="rtl">يتم تقييم <code dir="ltr">$Condition</code>، وإذا كان "صحيح" (<code dir="ltr">true</code>)، التوقيع نشط. إذا كان "خاطئة" (<code dir="ltr">false</code>)، التوقيع غير نشط. <code dir="ltr">$Condition</code> عادة ما تحتوي على التعليمات البرمجية PHP التي يجب منع الطلبات.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonShort</code> في حقل "سبب الحظر" عندما يكون التوقيع نشطا.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonLong</code> هي رسالة اختيارية يتم عرضها للمستخدم عند حظرها، لشرح سبب حظرها. يستخدم الرسالة القياسية "سبب الحظر" عند حذفها.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$DefineOptions</code> عبارة عن صفيف اختياري يحتوي على أزواج المفاتيح/القيم التي تحدد خيارات التكوين الخاصة بمثيل الطلب. سيتم تطبيق خيارات التهيئة عندما يكون التوقيع نشطا.<br /><br /></div>

<div dir="rtl">ترجع <code dir="ltr">$this->trigger</code> صحيح (<code dir="ltr">true</code>) عندما يكون التوقيع نشطا و خاطئة (<code dir="ltr">false</code>) عندما لا يكون.<br /><br /></div>

##### <div dir="rtl">٦.٥.١ <code dir="ltr">$this->bypass</code></div>

<div dir="rtl">وعادة ما تكتب الالتفافية التوقيع مع <code dir="ltr">$this->bypass</code>.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$this->bypass</code> يقبل ٣ المعلمات: <code dir="ltr">$Condition</code>، <code dir="ltr">$ReasonShort</code>، <code dir="ltr">$DefineOptions</code> (اختياري).<br /><br /></div>

<div dir="rtl">يتم تقييم <code dir="ltr">$Condition</code>، وإذا كان "صحيح" (<code dir="ltr">true</code>)، الالتفافية نشط. إذا كان "خاطئة" (<code dir="ltr">false</code>)، الالتفافية غير نشط. <code dir="ltr">$Condition</code> عادة ما تحتوي على رمز PHP التي يجب عدم منع الطلبات.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonShort</code> في حقل "سبب الحظر" عندما يكون الالتفافية نشطا.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$DefineOptions</code> عبارة عن صفيف اختياري يحتوي على أزواج المفاتيح/القيم التي تحدد خيارات التكوين الخاصة بمثيل الطلب. سيتم تطبيق خيارات التهيئة عندما يكون الالتفافية نشطا.<br /><br /></div>

<div dir="rtl">ترجع <code dir="ltr">$this->bypass</code> صحيح (<code dir="ltr">true</code>) عندما يكون الالتفافية نشطا و خاطئة (<code dir="ltr">false</code>) عندما لا يكون.<br /><br /></div>

##### <div dir="rtl">٦.٥.٢ <code dir="ltr">"$this->dnsReverse"</code></div>

<div dir="rtl">يمكن استخدام هذا لجلب اسم المضيف لعنوان IP. إذا كنت ترغب في إنشاء المكون لمنع أسماء المضيفين، قد يكون هذا الإغلاق مفيدا.<br /><br /></div>

<div dir="rtl">مثال:<br /><br /></div>

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

#### <div dir="rtl">٦.٦ المكون المتغيرات<br /><br /></div>

<div dir="rtl">الوحدات النمطية تنفذ ضمن نطاقها الخاص، وأي متغيرات محددة من قبل المكون نمطية، لن تكون في متناول وحدات أخرى، أو إلى السيناريو الأصل، إلا إذا كانت مخزنة في <code dir="ltr">$CIDRAM</code> مجموعة (يتم مسح كل شيء آخر بعد انتهاء تنفيذ المكون).<br /><br /></div>

<div dir="rtl">فيما يلي بعض المتغيرات الشائعة التي قد تكون مفيدة للالمكون النمطية الخاصة بك:<br /><br /></div>

&nbsp; <div dir="rtl" style="display:inline">وصف</div> | <div dir="rtl">متغير</div>
----|----
&nbsp; <div dir="rtl" style="display:inline">التاريخ والوقت الحاليان.</div> | `$this->BlockInfo['DateTime']`
&nbsp; <div dir="rtl" style="display:inline">عنوان IP للطلب الحالي.</div> | `$this->BlockInfo['IPAddr']`
&nbsp; <div dir="rtl" style="display:inline">إذا كان عنوان IP للطلب الحالي هو عنوان 6to4 أو Teredo أو ISATAP، فسيتم حل هذا العنوان إلى نظيره IPv4. إذا لم يكن الأمر كذلك، فسيكون عنوان IP للطلب الحالي.</div> | `$this->BlockInfo['IPAddrResolved']`
&nbsp; <div dir="rtl" style="display:inline">إصدار النص البرمجي CIDRAM.</div> | `$this->BlockInfo['ScriptIdent']`
&nbsp; <div dir="rtl" style="display:inline">الاستعلام عن الطلب الحالي.</div> | `$this->BlockInfo['Query']`
&nbsp; <div dir="rtl" style="display:inline">المحيل للطلب الحالي (إذا كان موجودا).</div> | `$this->BlockInfo['Referrer']`
&nbsp; <div dir="rtl" style="display:inline">وكيل المستخدم (user agent) للطلب الحالي.</div> | `$this->BlockInfo['UA']`
&nbsp; <div dir="rtl" style="display:inline">وكيل المستخدم (user agent) للطلب الحالي (في حالة أقل).</div> | `$this->BlockInfo['UALC']`
&nbsp; <div dir="rtl" style="display:inline">الرسالة المراد عرضها للمستخدم عند حظرها.</div> | `$this->BlockInfo['ReasonMessage']`
&nbsp; <div dir="rtl" style="display:inline">عدد التوقيعات التي أدت إلى الطلب الحالي.</div> | `$this->BlockInfo['SignatureCount']`
&nbsp; <div dir="rtl" style="display:inline">المعلومات المرجعية عن أي توقيعات أثارت للطلب الحالي.</div> | `$this->BlockInfo['Signatures']`
&nbsp; <div dir="rtl" style="display:inline">المعلومات المرجعية عن أي توقيعات أثارت للطلب الحالي.</div> | `$this->BlockInfo['WhyReason']`
&nbsp; <div dir="rtl" style="display:inline">طريقة الطلب للطلب الحالي.</div> | `$this->BlockInfo['Request_Method']`
&nbsp; <div dir="rtl" style="display:inline">بروتوكول الطلب الحالي.</div> | `$this->BlockInfo['Protocol']`

---


### <div dir="rtl">٧. <a name="SECTION7"></a>مشاكل التوافق المعروفة</div>

<div dir="rtl">تم العثور على الحزم والمنتجات التالية لتكون غير متوافقة مع CIDRAM:</div>
<div dir="rtl"><ul>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/52">Endurance Page Cache</a></strong></li>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/80">Mix.com</a></strong></li>
</ul></div>

<div dir="rtl">تم توفير وحدات لضمان توافق الحزم والمنتجات التالية مع CIDRAM:</div>
<div dir="rtl"><ul>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/56">BunnyCDN</a></strong></li>
 <li><strong><a dir="ltr" href="https://wordpress.org/support/topic/quic-dot-cloud-requires-all-ips-allowed/">Quic cloud</a></strong></li>
</ul></div>

<div dir="rtl"><em>انظر أيضا: <a href="https://maikuolan.github.io/Compatibility-Charts/">مخططات التوافق</a>.</em><br /><br /></div>

---


### <div dir="rtl">٨. <a name="SECTION8"></a>أسئلة وأجوبة (FAQ)</div>

<div dir="rtl"><ul>
 <li><a href="#user-content-WHAT_IS_A_SIGNATURE">ما هو "التوقيع"؟</a></li>
 <li><a href="#user-content-WHAT_IS_A_CIDR">ما هو "CIDR"؟</a></li>
 <li><a href="#user-content-WHAT_IS_A_FALSE_POSITIVE">ما هو "إيجابية خاطئة"؟</a></li>
 <li><a href="#user-content-BLOCK_ENTIRE_COUNTRIES">يمكن CIDRAM منع الدول؟</a></li>
 <li><a href="#user-content-SIGNATURE_UPDATE_FREQUENCY">عدد المرات التي يتم تحديثها التوقيعات؟</a></li>
 <li><a href="#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO">لقد واجهت مشكلة! أنا لا أعرف ما يجب القيام به! الرجاء المساعدة!</a></li>
 <li><a href="#user-content-BLOCKED_WHAT_TO_DO">لقد تم حظر من موقع على شبكة الانترنت! الرجاء المساعدة!</a></li>
 <li><a href="#user-content-MINIMUM_PHP_VERSION_V3">أريد استخدام CIDRAM v2~v4 مع نسخة PHP كبار السن من 7.2؛ يمكنك أن تساعد؟</a></li>
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
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
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

#### <div dir="rtl"><a name="MINIMUM_PHP_VERSION_V3"></a>أريد استخدام CIDRAM v2~v4 مع نسخة PHP كبار السن من 7.2؛ يمكنك أن تساعد؟<br /><br /></div>

<div dir="rtl">لا. PHP≥7.2 هو الحد الأدنى لمتطلبات CIDRAM v2~v4.<br /><br /></div>

<div dir="rtl"><em>انظر أيضا: <a href="https://maikuolan.github.io/Compatibility-Charts/">مخططات التوافق</a>.</em><br /><br /></div>

#### <div dir="rtl"><a name="PROTECT_MULTIPLE_DOMAINS"></a>هل يمكنني استخدام تثبيت CIDRAM واحد لحماية نطاقات متعددة؟<br /><br /></div>

<div dir="rtl">نعم. يمكن استخدام CIDRAM لحماية نطاقات متعددة. إذا كان التكوين المطلوب مختلفا، للقيام بذلك، إنشاء ملفات تكوين جديدة، واسمه وفقا للنطاقات التي تتطلب الحماية. كمثال، ل <code dir="ltr">"https://www.some-domain.tld/"</code>، أطلق عليه اسما <code dir="ltr">"some-domain.tld.config.yml"</code>. اسم النطاق يأتي من <code dir="ltr">"HTTP_HOST"</code>. يتم تجاهل <code dir="ltr">"www"</code>.<br /><br /></div>

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

<div dir="rtl">يرتبط "عدد التوقيعات" و "المخالفات" بخطورة وعدد التوقيعات التي تم إطلاقها أثناء أي طلب معين، سواء كان ذلك بسبب ملفات التوقيع أو الوحدات النمطية أو القواعد المساعدة أو غير ذلك. ولكن، بينما يستمر "عدد التوقيعات" فقط لهذا الطلب بعينه، يمكن أن تستمر "المخالفات" في العديد من الطلبات كما هو محدد بواسطة <code dir="ltr">default_tracktime</code>.<br /><br /></div>

<div dir="rtl">وهذا يضمن أنه عندما يتم حظر طلب بعدد كافٍ من المخالفات، يمكن أيضًا حظر الطلبات اللاحقة من نفس المصدر.<br /><br /></div>

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

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

<div dir="rtl">إذا كنت تريد <code dir="ltr">file3.php</code> تنفيذ أولاً، يمكنك إضافة شيء مثل <code dir="ltr">aaa:</code> قبل اسم الملف:<br /><br /></div>

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

<div dir="rtl">وبعد ذلك، إذا تم تنشيط ملف جديد، <code dir="ltr">file6.php</code>، فعندما تقوم صفحة التحديثات بفرزها مرة أخرى، يجب أن ينتهي الأمر بهذا الشكل:<br /><br /></div>

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

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


### <div dir="rtl">٩. <a name="SECTION9"></a>المعلومات القانونية</div>

#### <div dir="rtl">٩.٠ مقدمة القسم<br /><br /></div>

<div dir="rtl">يصف هذا القسم من الوثائق الاعتبارات القانونية الممكنة فيما يتعلق باستخدام الحزمة وتنفيذها، ويوفر بعض المعلومات الأساسية ذات الصلة. قد يكون هذا مهمًا لبعض المستخدمين كوسيلة لضمان التوافق مع أي متطلبات قانونية قد تكون موجودة في البلدان التي يعملون فيها، وقد يحتاج بعض المستخدمين إلى تعديل سياسات موقع الويب الخاصة بهم وفقًا لهذه المعلومات.<br /><br /></div>

<div dir="rtl">أولا، يرجى ندرك أنني (مؤلف حزمة) لست محام، وليس أي نوع من المهنيين القانونيين المؤهلين. لذلك، لست مؤهلاً قانونًا لتقديم المشورة القانونية. أيضا، في بعض الحالات، قد تختلف المتطلبات القانونية بين الدول والاختصاصات المختلفة، وهذه المتطلبات القانونية المتفاوتة قد تكون متناقضة في بعض الأحيان (على سبيل المثال، الدول التي تفضل "<a href="https://ar.wikipedia.org/wiki/%D8%AD%D9%82_%D9%81%D9%8A_%D8%A7%D9%84%D8%AE%D8%B5%D9%88%D8%B5%D9%8A%D8%A9">حقوق الخصوصية</a>" و "<a href="https://ar.wikipedia.org/wiki/%D8%AD%D9%82_%D8%A7%D9%84%D9%85%D8%B1%D8%A1_%D8%A3%D9%86_%D9%8A%D9%86%D8%B3%D9%89">الحق في أن تنسى</a>"، مقارنة بالبلدان التي تفضل "الاحتفاظ بالبيانات"). ضع في اعتبارك أيضًا أن الوصول إلى الحزمة لا يقتصر على بلدان أو ولايات قضائية محددة، وبالتالي، فإن مستخدمي الحزمة من المحتمل أن يكونوا متنوعين جغرافيًا. بالنظر إلى هذه النقاط، فأنا لست في وضع يسمح لي بالإشارة إلى ما يعنيه أن يكون "متوافقة مع القانون" مع الجميع. ومع ذلك، آمل أن تساعدك هذه المعلومات على أن تقرر بنفسك ما يجب عليك القيام به للبقاء ملتزمين قانونًا في سياق الحزمة. إذا كانت لديك أي شكوك بخصوص هذه المعلومات، أو إذا كنت بحاجة إلى مساعدة ومشورة إضافية من منظور قانوني، فإنني أوصيك باستشارة متخصص قانوني مؤهل.<br /><br /></div>

#### <div dir="rtl">٩.١ المسؤولية<br /><br /></div>

<div dir="rtl">كما هو مذكور بالفعل من قبل ترخيص الحزمة، يتم توفير الحزمة دون أي ضمان. وهذا يشمل (على سبيل المثال لا الحصر) كل نطاق المسؤولية. يتم توفير الحزمة لك لراحتك، على أمل أن تكون مفيدة، وأنها سوف توفر بعض الفائدة بالنسبة لك. ومع ذلك، سواء كنت تستخدم أو تنفذ الحزمة، فذلك هو خيارك. لا تضطر إلى استخدام الحزمة أو تنفيذها، ولكن عندما تقوم بذلك، فأنت مسؤول عن هذا القرار. لا أنا ولا أي مساهم آخر في الحزمة مسؤول قانونيًا عن عواقب القرارات التي تتخذها، بصرف النظر عما إذا كانت مباشرة أو غير مباشرة أو ضمنية أو غير ذلك.<br /><br /></div>

#### <div dir="rtl">٩.٢ الأطراف الثالثة<br /><br /></div>

<div dir="rtl">اعتمادا على التكوين الدقيق والتنفيذ، قد تتواصل الحزمة وتتبادل المعلومات مع أطراف ثالثة في بعض الحالات. في بعض السياقات، من خلال بعض السلطات القضائية، يمكن تعريف ذلك على أنه "<a href="https://ar.wikipedia.org/wiki/%D9%85%D8%B9%D9%84%D9%88%D9%85%D8%A7%D8%AA_%D8%B4%D8%AE%D8%B5%D9%8A%D8%A9">معلومات تعريف شخصية</a>".<br /><br /></div>

<div dir="rtl">إن كيفية استخدام هذه المعلومات من قِبل هذه الجهات الخارجية تخضع لسياساتها، وهي خارج نطاق هذه الوثائق. ومع ذلك، في جميع هذه الحالات، يمكن تعطيل مشاركة المعلومات. في جميع هذه الحالات، إذا اخترت تمكينها، تقع على عاتقك مسؤولية البحث عن أي مخاوف قد تكون لديك بشأن الخصوصية والأمان واستخدام هذه المعلومات من قِبل هذه الأطراف الثالثة. إذا وجدت أي شكوك، أو إذا كنت غير راضي عن سلوك هذه الأطراف الثالثة، قد يكون من الأفضل تعطيل كل مشاركة المعلومات مع هذه الأطراف الثالثة.<br /><br /></div>

<div dir="rtl">لغرض الشفافية، يتم وصف نوع المعلومات المشتركة أدناه.<br /><br /></div>

##### <div dir="rtl">٩.٢.٠ بحث اسم المضيف<br /><br /></div>

<div dir="rtl">إذا كنت تستخدم أي ميزات أو وحدات تهدف إلى العمل مع أسماء المضيفين، فيجب أن يكون CIDRAM قادرًا على الحصول على اسم المضيف للطلبات الواردة. عادة، تقوم بذلك عن طريق طلب أسماء المضيف لعنوان IP من خادم DNS، أو عن طريق طلب المعلومات من خلال الوظائف التي يوفرها النظام مباشرة. تنتمي خوادم DNS المحددة افتراضيًا إلى خدمة <a dir="ltr" href="https://dns.google.com/">Google DNS</a> (ولكن هذا يمكن تغييره بسهولة عبر التكوين). يمكن تكوين الخدمات الدقيقة التي يتم الاتصال بها، وتعتمد على كيفية تكوين الحزمة. عند طلب ذلك عبر النظام مباشرة، ستحتاج إلى الاتصال بمسؤول النظام لتحديد الطرق المستخدمة. يمكن منع عمليات البحث عن اسم المضيف في CIDRAM عن طريق تجنب الوحدات المتأثرة أو عن طريق تعديل تكوين الحزمة وفقًا لذلك.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">allow_gethostbyaddr_lookup</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">default_dns</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">force_hostname_lookup</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">other</code> &lt;- <code dir="ltr">verification</code></li>
 <li><code dir="ltr">search_engines</code> &lt;- <code dir="ltr">verification</code></li>
 <li><code dir="ltr">social_media</code> &lt;- <code dir="ltr">verification</code></li>
</ul></div>

##### <div dir="rtl">٩.٢.١ التحقق من محركات البحث ووسائل الإعلام الاجتماعية<br /><br /></div>

<div dir="rtl">عندما يتم تمكين هذه الخيارات، يحاول CIDRAM التحقق من صحة الطلبات من محركات البحث والشبكات الاجتماعية. للقيام بذلك، فإنه يستخدم خدمة <a dir="ltr" href="https://dns.google.com/">Google DNS</a> لمحاولة حل عناوين IP من أسماء المضيفين لهذه الطلبات الواردة (في هذه العملية، تتم مشاركة أسماء المضيفين لهذه الطلبات الواردة مع الخدمة).<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">other</code> &lt;- <code dir="ltr">verification</code></li>
 <li><code dir="ltr">search_engines</code> &lt;- <code dir="ltr">verification</code></li>
 <li><code dir="ltr">social_media</code> &lt;- <code dir="ltr">verification</code></li>
</ul></div>

##### <div dir="rtl">٩.٢.٢ CAPTCHA<br /><br /></div>

<div dir="rtl">يتم دعم CAPTCHA بواسطة CIDRAM. تتطلب مفاتيح API لكي تعمل بشكل صحيح. يتم تعطيلها افتراضيًا، ولكن يمكن تمكينها عن طريق تكوين مفاتيح واجهة برمجة التطبيقات المطلوبة. عند التمكين، قد يحدث اتصال بين الخدمة و CIDRAM أو متصفح المستخدم. قد يتضمن ذلك نقل معلومات مثل عنوان IP للمستخدم ووكيل المستخدم ونظام التشغيل.<br /><br /></div>

##### <div dir="rtl">٩.٢.٣ STOP FORUM SPAM<br /><br /></div>

<div dir="rtl"><a dir="ltr" href="https://www.stopforumspam.com/">Stop Forum Spam</a> هي خدمة رائعة متاحة مجانًا يمكن أن تساعد في حماية المنتديات والمدونات ومواقع الويب من مرسلي الرسائل غير المرغوب فيها. ويقوم بذلك عن طريق توفير قاعدة بيانات لمعرّفي البريد المزعوم المعروفين وواجهة برمجة تطبيقات يمكن الاستفادة منها للتحقق مما إذا كان عنوان IP أو اسم المستخدم أو عنوان البريد الإلكتروني مدرجًا في قاعدة البيانات الخاصة به.<br /><br /></div>

<div dir="rtl">يوفر CIDRAM المكون اختيارية تستفيد من واجهة برمجة التطبيقات هذه للتحقق مما إذا كان عنوان IP للطلبات الواردة ينتمي إلى مرسلي بريد مزعوم مشتبه فيهم. عندما يتم تثبيت الوحدة وتنشيطها، فقد تتم مشاركة عناوين IP الخاصة بالمستخدمين مع الخدمة وفقًا للتكوين والغرض المقصود من الوحدة.<br /><br /></div>

##### <div dir="rtl">٩.٢.٤ ABUSEIPDB<br /><br /></div>

<div dir="rtl">يوفر CIDRAM المكون نمطية اختيارية لحظر عناوين IP المسيئة باستخدام واجهة برمجة تطبيقات <a dir="ltr" href="https://www.abuseipdb.com/">AbuseIPDB</a>. عندما يتم تثبيت الوحدة وتنشيطها، فقد تتم مشاركة عناوين IP الخاصة بالمستخدمين مع الخدمة وفقًا للتكوين والغرض المقصود من الوحدة.<br /><br /></div>

##### <div dir="rtl">٩.٢.٥ BGPVIEW, IP-API<br /><br /></div>

<div dir="rtl">يوفر CIDRAM المكون نمطية اختيارية لإجراء عمليات البحث ASN ورمز البلد باستخدام API <a dir="ltr" href="https://bgpview.io/">BGPView</a> وAPI <a dir="ltr" href="https://ip-api.com/">IP-API</a>. توفر عمليات البحث هذه القدرة على حظر أو إدراج طلبات القائمة البيضاء على أساس ASN أو بلد المنشأ. عندما يتم تثبيت الوحدة وتنشيطها، فقد تتم مشاركة عناوين IP الخاصة بالمستخدمين مع الخدمة وفقًا للتكوين والغرض المقصود من الوحدة.<br /><br /></div>

##### <div dir="rtl">٩.٢.٦ PROJECT HONEYPOT<br /><br /></div>

<div dir="rtl">يوفر CIDRAM المكون نمطية اختيارية لحظر عناوين IP المسيئة باستخدام واجهة برمجة تطبيقات <a dir="ltr" href="https://www.projecthoneypot.org/">Project Honeypot</a>. عندما يتم تثبيت الوحدة وتنشيطها، فقد تتم مشاركة عناوين IP الخاصة بالمستخدمين مع الخدمة وفقًا للتكوين والغرض المقصود من الوحدة.<br /><br /></div>

#### <div dir="rtl">٩.٣ تسجيل<br /><br /></div>

<div dir="rtl">التسجيل هو جزء مهم من CIDRAM لعدد من الأسباب. قد يكون من الصعب تشخيص وحل إيجابيات خاطئة عندما لا يتم تسجيل أحداث الحظر التي تسبب لهم. بدون تسجيل أحداث الحظر، قد يكون من الصعب التأكد من أداء CIDRAM بشكل جيد، وقد يكون من الصعب تحديد مواطن ضعفها، وما هي التغييرات التي قد تكون مطلوبة لتكوينها أو توقيعاتها، لكي تستمر في العمل على النحو المنشود. بغض النظر، ربما لا يريد الجميع التسجيل، لذلك يبقى اختياريًا تمامًا. في CIDRAM، يتم تعطيل التسجيل افتراضيًا. لتمكينه، يجب تكوين CIDRAM وفقًا لذلك.<br /><br /></div>

<div dir="rtl">بالإضافة إلى، ما إذا كان تخزين هذا النوع من البياناتمسموحًا به قانونًا، وإلى الحد المسموح به قانونًا (ذلك بالقول، أنواع المعلومات التي يمكن تسجيلها، إلى متى، وتحت أي ظروف)، قد تختلف، وهذا يتوقف على الاختصاص واعتمادًا على سياق التنفيذ (فمثلا، سواء كنت تعمل كفرد أو مؤسسة، وعما إذا كان ذلك على أساس تجاري أو غير تجاري). لذلك قد يكون من المفيد لك قراءة هذا القسم بعناية.<br /><br /></div>

<div dir="rtl">هناك العديد من أنواع المعلومات المختلفة التي يمكن تسجيلها، لأسباب مختلفة.<br /><br /></div>

##### <div dir="rtl">٩.٣.٠ حظر الأحداث<br /><br /></div>

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
 <li><code dir="ltr">apache_style_log</code> &lt;- <code dir="ltr">logging</code></li>
 <li><code dir="ltr">serialised_log</code> &lt;- <code dir="ltr">logging</code></li>
 <li><code dir="ltr">standard_log</code> &lt;- <code dir="ltr">logging</code></li>
</ul></div>

<div dir="rtl">عندما يتم ترك هذه التوجيهات فارغة، سيظل هذا النوع من التسجيل معطلاً.<br /><br /></div>

##### <div dir="rtl">٩.٣.١ تسجيل CAPTCHA<br /><br /></div>

<div dir="rtl">هذا النوع من التسجيل يتعلق بشكل خاص بمثيلات CAPTCHA. يحدث فقط عندما يحاول مستخدم لإكمال CAPTCHA.<br /><br /></div>

<div dir="rtl">يحتوي إدخال سجل CAPTCHA على عنوان IP الخاص بالمستخدم الذي يحاول إكمال CAPTCHA، وتاريخ ووقت حدوث المحاولة، وحالة CAPTCHA. عادةً ما تبدو الإدخالات كما يلي (كمثال):<br /><br /></div>

```
عنوان IP: x.x.x.x - الوقت/التاريخ: Day, dd Mon 20xx hh:ii:ss +0000 - الحالة CAPTCHA: نجحت!
```

<div dir="rtl">توجيه التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">log</code> &lt;- <code dir="ltr">captcha</code></li>
</ul></div>

##### <div dir="rtl">٩.٣.٢ سجلات الواجهة الأمامية<br /><br /></div>

<div dir="rtl">هذا التسجيل يتصل محاولات تسجيل الدخول الأمامية. يحدث فقط عندما يحاول مستخدم تسجيل الدخول إلى الواجهة الأمامية، وفقط عندما يتم تمكين الوصول للجهة الأمامية.<br /><br /></div>

<div dir="rtl">يحتوي إدخال سجل الواجهة الأمامية على عنوان IP الخاص بالمستخدم الذي يحاول تسجيل الدخول وتاريخ ووقت حدوث المحاولة ونتائج المحاولة (تم تسجيل الدخول بنجاح، أو فشل في تسجيل الدخول). يبدو عادة مثل هذا (كمثال):<br /><br /></div>

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - حاليا على.
```

<div dir="rtl">توجيه التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">frontend_log</code> &lt;- <code dir="ltr">frontend</code></li>
</ul></div>

##### <div dir="rtl">٩.٣.٣ دوران السجل<br /><br /></div>

<div dir="rtl">قد ترغب في تطهير السجلات بعد فترة من الوقت، أو قد تكون مطلوبة للقيام بذلك بموجب القانون (أي أن مقدار الوقت المسموح به قانونًا لك للاحتفاظ بالسجلات قد يكون محدودًا بموجب القانون). يمكنك تحقيق ذلك عن طريق تضمين علامات التاريخ/الوقت في أسماء ملفات السجل الخاصة بك كما هو محدد بواسطة تكوين الحزمة الخاصة بك (على سبيل المثال، <code dir="ltr">{yyyy}-{mm}-{dd}.log</code>)، ثم تمكين دوران السجل (يسمح لك تدوير السجل بتنفيذ بعض الإجراءات على ملفات السجل عندما يتم تجاوز الحدود المحددة).<br /><br /></div>

<div dir="rtl">فمثلا: إذا كان من الضروري قانونًا حذف السجلات بعد 30 يومًا، يمكنني تحديد <code dir="ltr">{dd}.log</code> في أسماء ملفات السجل الخاصة بي (<code dir="ltr">{dd}</code> يمثل عدد الأيام)، قم بتعيين قيمة <code dir="ltr">log_rotation_limit</code> إلى 30، وقم بتعيين قيمة <code dir="ltr">log_rotation_action</code> إلى <code dir="ltr">Delete</code>.<br /><br /></div>

<div dir="rtl">على العكس من ذلك، إذا كنت مطالبًا بالاحتفاظ بالسجلات لفترة زمنية طويلة، فيمكنك تعطيل تدوير السجل، أو يمكنك تعيين قيمة <code dir="ltr">log_rotation_action</code> إلى <code dir="ltr">Archive</code>، لضغط ملفات السجل، وبالتالي تقليل إجمالي مساحة القرص التي يشغلونها.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">log_rotation_action</code> &lt;- <code dir="ltr">logging</code></li>
 <li><code dir="ltr">log_rotation_limit</code> &lt;- <code dir="ltr">logging</code></li>
</ul></div>

##### <div dir="rtl">٩.٣.٤ سجل اقتطاع<br /><br /></div>

<div dir="rtl">إذا أردت، يمكنك اقتطاع ملفات السجل الفردية عندما تتجاوز حجمًا معينًا.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">truncate</code> &lt;- <code dir="ltr">logging</code></li>
</ul></div>

##### <div dir="rtl">٩.٣.٥ عنوان IP PSEUDONYMISATION<br /><br /></div>

<div dir="rtl">أولاً، إذا لم تكن على دراية بهذا المصطلح، "pseudonymisation" يشير إلى معالجة البيانات الشخصية على هذا النحو بحيث لا يمكن تحديدها لأي موضوع بيانات محدد بعد الآن بدون معلومات إضافية، وشريطة أن يتم الاحتفاظ بهذه المعلومات التكميلية بشكل منفصل وتخضع للتدابير التقنية والتنظيمية لضمان عدم إمكانية تحديد البيانات الشخصية لأي شخص طبيعي.<br /><br /></div>

<div dir="rtl">يمكن أن تساعد الموارد التالية في شرحها بمزيد من التفاصيل:</div>
<div dir="rtl"><ul>
 <li><a dir="ltr" href="https://www.trust-hub.com/news/what-is-pseudonymisation/">[trust-hub.com] What is pseudonymisation?</a></li>
 <li><a dir="ltr" href="https://en.wikipedia.org/wiki/Pseudonymization">[Wikipedia] Pseudonymization</a></li>
</ul></div>

<div dir="rtl">في بعض الحالات، قد يُطلب منك قانونًا تنفيذ "anonymisation" أو "pseudonymisation" لأي معلومات PII تم جمعها أو معالجتها أو تخزينها. على الرغم من وجود هذا المفهوم منذ بعض الوقت، GDPR/DSGVO يذكر بشكل ملحوظ ويشجع "pseudonymisation".<br /><br /></div>

<div dir="rtl">إذا أردت، يمكن لـ CIDRAM القيام بذلك لعناوين IP عند الكتابة إلى السجلات. عند الكتابة إلى السجلات، سيتم تمثيل الثمانية النهائية لعناوين IPv4 وكل شيء بعد الجزء الثاني من عناوين IPv6 بواسطة "x" (تقريب عناوين IPv4 إلى العنوان الأولي للشبكة الفرعية الـ 24 التي تدخلها، وعناوين IPv6 إلى العنوان الأولي للشبكة الفرعية 32 التي تدخلها).<br /><br /></div>

<div dir="rtl"><em>ملحوظة: ميزة تتبع IP من CIDRAM لا تملك هذه القدرة. إذا كانت هذه مشكلة بالنسبة لك، فقد يكون من الأفضل تعطيل تتبع IP بالكامل.</em><br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">pseudonymise_ip_addresses</code> &lt;- <code dir="ltr">legal</code></li>
</ul></div>

##### <div dir="rtl">٩.٣.٦ حذف معلومات السجل<br /><br /></div>

<div dir="rtl">إذا كنت ترغب في منع تسجيل أنواع معينة من المعلومات بالكامل، فيمكنك القيام بذلك. في صفحة التكوين، يرجى الرجوع إلى توجيه تكوين <code dir="ltr">fields</code> للتحكم في الحقول التي تظهر في إدخالات السجل وفي صفحة "تم رفض الوصول".<br /><br /></div>

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

<div dir="rtl"><em>ملحوظة: لا يوجد سبب لاستخدام pseudonymisation لعناوين IP عند حذف عناوين IP من السجلات بالكامل.</em><br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">fields</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">٩.٣.٧ الإحصاء<br /><br /></div>

<div dir="rtl">CIDRAM قادر بشكل اختياري على تتبع الإحصائيات مثل إجمالي عدد أحداث المنع أو حالات CAPTCHA التي حدثت منذ وقت معين. يتم تعطيل هذه الميزة بشكل افتراضي، ولكن يمكن تمكينها من خلال تهيئة الحزمة. هذه الميزة لا تتبع سوى العدد الإجمالي للأحداث. لا يتضمن أي معلومات حول أحداث معينة، لذلك لا ينبغي اعتباره معلومات تحديد الهوية الشخصية.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">statistics</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">٩.٣.٨ التشفير<br /><br /></div>

<div dir="rtl">لا يقوم CIDRAM بتشفير ذاكرة التخزين المؤقت أو أي معلومات سجل. قد يتم إدخال <a href="https://ar.wikipedia.org/wiki/%D8%AA%D8%B4%D9%81%D9%8A%D8%B1">تشفير</a> ذاكرة التخزين المؤقت والسجلات في المستقبل، ولكن لا توجد خطط محددة لها حاليًا. إذا كنت قلقًا بشأن حصول أطراف ثالثة غير مصرح لها على إمكانية الوصول إلى أجزاء من CIDRAM قد تحتوي على معلومات تحديد الهوية الشخصية أو معلومات حساسة مثل ذاكرة التخزين المؤقت أو السجلات، أوصي بعدم تثبيت CIDRAM في مكان يمكن الوصول إليه بشكل عام (على سبيل المثال، مجلد تثبيت CIDRAM خارج الدليل <code dir="ltr">public_html</code> القياسي أو ما يعادله، متاح لمعظم خوادم الويب القياسية) والتأكد من فرض الأذونات المقيدة بشكل مناسب لدليل التثبيت (على وجه الخصوص، لدليل <code dir="ltr">vault</code>). إذا لم يكن ذلك كافيًا لمعالجة مخاوفك، فقم بتكوين CIDRAM بحيث لا يتم جمع أنواع المعلومات التي تسبب مخاوفك أو تسجيلها في المقام الأول (مثل، عن طريق تعطيل التسجيل).<br /><br /></div>

#### <div dir="rtl">٩.٤ ملف تعريف ارتباط<br /><br /></div>

<div dir="rtl">يضع CIDRAM <a href="https://ar.wikipedia.org/wiki/%D9%85%D9%84%D9%81_%D8%AA%D8%B9%D8%B1%D9%8A%D9%81_%D8%A7%D8%B1%D8%AA%D8%A8%D8%A7%D8%B7">ملفات تعريف الارتباط</a> في نقطتين في تعليمات البرمجة الخاصة به. أولاً، اعتمادًا على كيفية تكوين <code dir="ltr">lockto</code>، قد يقوم CIDRAM بتعيين ملف تعريف ارتباط لتذكر متى أكمل المستخدم اختبار CAPTCHA. ثانيا، عندما يسجل المستخدم بنجاح في الواجهة الأمامية، يعين CIDRAM ملف تعريف ارتباط حتى يتمكن من تذكر المستخدم للطلبات اللاحقة (أي، يتم استخدام ملفات تعريف الارتباط لمصادقة المستخدم على جلسة تسجيل الدخول).<br /><br /></div>

<div dir="rtl">في كلتا الحالتين، يتم عرض تحذيرات ملفات تعريف الارتباط بشكل بارز (عند الاقتضاء)، وتحذير المستخدم من أنه سيتم تعيين ملفات تعريف الارتباط إذا شارك في الإجراءات ذات الصلة. لا يتم تعيين ملفات تعريف الارتباط في أي نقاط أخرى في مصدر التعليمات البرمجية.<br /><br /></div>

<div dir="rtl">ملحوظة: قد تكون واجهات برمجة تطبيقات CAPTCHA "غير المرئية" غير متوافقة مع قوانين ملفات تعريف الارتباط في بعض الولايات القضائية، ويجب تجنبها من قبل أي مواقع ويب تخضع لهذه القوانين. قد يكون من الأفضل اختيار استخدام واجهات برمجة التطبيقات الأخرى المتوفرة بدلاً من ذلك، أو ببساطة تعطيل اختبار CAPTCHA بالكامل.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">lockto</code> &lt;- <code dir="ltr">captcha</code></li>
 <li><code dir="ltr">api</code> &lt;- <code dir="ltr">captcha</code></li>
</ul></div>

#### <div dir="rtl">٩.٥ التسويق والإعلان<br /><br /></div>

<div dir="rtl">لا تجمع CIDRAM أو تعالج أي معلومات لأغراض التسويق أو الإعلانات، ولا تبيع أو تحقق أرباحًا من أي معلومات تم جمعها أو تسجيلها. CIDRAM ليست مؤسسة تجارية، ولا ترتبط بأي مصالح تجارية، لذا فإن القيام بهذه الأشياء لن يكون له أي معنى. كان هذا هو الحال منذ بداية المشروع، وما زالت الحالة اليوم. بالإضافة إلى ذلك، فإن القيام بهذه الأشياء سيؤدي إلى نتائج عكسية للمشروع والغرض المقصود من المشروع ككل، وطالما استمر في الحفاظ على المشروع، لن يحدث أبداً.<br /><br /></div>

#### <div dir="rtl">٩.٦ سياسة الخصوصية<br /><br /></div>

<div dir="rtl">في بعض الحالات، قد يُطلب منك قانونًا عرض رابط لسياسة الخصوصية بوضوح في جميع صفحات وأقسام موقعك. قد يكون هذا أمرًا مهمًا كوسيلة لضمان معرفة المستخدمين جيدًا بممارسات الخصوصية الدقيقة، وأنواع معلومات تحديد الهوية الشخصية التي تجمعها، وكيفية تنوي استخدامها. لتتمكن من تضمين مثل هذا الارتباط في صفحة "تم رفض الوصول" الخاصة بـ CIDRAM، يتم توفير توجيه تكوين لتحديد عنوان URL لسياسة الخصوصية الخاصة بك.<br /><br /></div>

<div dir="rtl">ملحوظة: يوصى بشدة بعدم وضع صفحة سياسة الخصوصية خلف حماية CIDRAM. إذا قام CIDRAM بحماية صفحة سياسة الخصوصية الخاصة بك، وكان المستخدم المحظور من قِبل CIDRAM ينقر على رابط لسياسة الخصوصية الخاصة بك، فسيتم حظره مرة أخرى ولن يتمكن من رؤية سياسة الخصوصية الخاصة بك. من الناحية المثالية، يجب عليك الربط بنسخة ثابتة من سياسة الخصوصية، مثل صفحة HTML أو ملف نصي عادي غير محمي بواسطة CIDRAM.<br /><br /></div>

<div dir="rtl">خيارات التكوين ذات الصلة:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">privacy_policy</code> &lt;- <code dir="ltr">legal</code></li>
</ul></div>

#### <div dir="rtl">٩.٧ GDPR/DSGVO<br /><br /></div>

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


### <div dir="rtl">١٠. <a name="SECTION10"></a>الترقية من الإصدارات الرئيسية السابقة</div>

#### <div dir="rtl">١٠.٠ الترقية إلى CIDRAM v3<br /><br /></div>

<div dir="rtl">توجد اختلافات كبيرة بين v3 والإصدارات الرئيسية السابقة. تختلف طريقة عمل نقاط الدخول، وطريقة تنظيم الوحدات، وطريقة عمل المحدث للإصدار 3 عن طريقة عمل هذه الأشياء للإصدارات الرئيسية السابقة. بسبب هذه الاختلافات، فإن أفضل طريقة للترقية إلى v3 من الإصدارات الرئيسية السابقة هي إجراء تثبيت جديد.<br /><br /></div>

<div dir="rtl">إذا كنت تريد الاحتفاظ بالتكوين والقواعد الإضافية، فقبل بدء عملية الترقية، انتقل إلى صفحة النسخ الاحتياطي للواجهة الأمامية. من هناك، يمكن تصدير التكوين والقواعد المساعدة. سيؤدي التصدير إلى تنزيل ملف. بعد الترقية إلى الإصدار الرئيسي الجديد، يمكن استخدام هذا الملف لاستيراد البيانات التي تم تصديرها مسبقًا إلى التثبيت.<br /><br /></div>

<div dir="rtl">بسبب التغييرات التي تم إجراؤها على طريقة تنظيم الوحدات النمطية، يجب إعادة كتابة الوحدات المخصصة للإصدارات الرئيسية السابقة من أجل العمل بشكل صحيح مع v3. الهجرة المباشرة لن تعمل. نفس الشيء صحيح بالنسبة للأحداث.<br /><br /></div>

<div dir="rtl">لم تتغير طريقة هيكلة ملفات التوقيع، لذا يمكن نقل ملفات التوقيع المخصصة للإصدارات الرئيسية السابقة مباشرة إلى v3 دون أي مشاكل متوقعة.<br /><br /></div>

<div dir="rtl">تحتوي كل من الوحدات النمطية وملفات التوقيع والأحداث على أدلة مخصصة خاصة بها، وهي إضافة جديدة منذ v3 (لذلك، بالنسبة إلى v3، سينتقل كل منهم إلى الدلائل المخصصة له، بدلاً من جذر vault).<br /><br /></div>

<div dir="rtl">تم إهمال بعض ملفات التوقيع والوحدات وقوائم الحظر المتاحة للجمهور للإصدارات الرئيسية السابقة، لذلك لن يكون كل شيء متاحًا للإصدار v3. في معظم الحالات، لن تكون هناك حاجة إليها على أي حال، بسبب الميزات والوظائف الجديدة المضافة منذ v3.<br /><br /></div>

<div dir="rtl">هناك بعض التغييرات الطفيفة في طريقة هيكلة القواعد المساعدة، وهناك تغييرات على التكوين، ولكن إذا كنت تستخدم ميزات الاستيراد والتصدير في صفحة النسخ الاحتياطي للواجهة الأمامية، فلن تحتاج إلى إعادة كتابة أي شيء يدويًا أو ضبطه أو إعادة إنشائه. عند الاستيراد، يعرف CIDRAM ما هو مطلوب، وسوف يتعامل معه تلقائيًا.<br /><br /></div>

<div dir="rtl">لمعرفة قائمة التغييرات التي تم إدخالها بواسطة v3 (على سبيل المثال، الميزات المضافة، والميزات التي تمت إزالتها، وما إلى ذلك)، راجع <a href="https://github.com/CIDRAM/CIDRAM/blob/v3/Changelog.md#v300">سجل التغيير</a> v3.<br /><br /></div>

#### <div dir="rtl">١٠.١ الترقية إلى CIDRAM v4 من إصدار أقدم من CIDRAM v3<br /><br /></div>

<div dir="rtl">يرجى الرجوع إلى ما ورد أعلاه: يوصى بإجراء تثبيت جديد.<br /><br /></div>

#### <div dir="rtl">١٠.٢ الترقية إلى CIDRAM v4 من CIDRAM v3<br /><br /></div>

<div dir="rtl">١. أولاً، انتقل إلى صفحة التحديثات، وإذا كانت هناك أي تحديثات متوفرة، فتأكد من تثبيتها جميعها. يضمن هذا توفر أي كود قد يكون ضروريًا للتحديث ويساعد في تقليل ما يحتاج المحدث إلى القيام به لاحقًا.<br /><br /></div>

<div dir="rtl">٢. انتقل إلى صفحة التكوين وابحث عن <strong><code dir="ltr">remotes⬅frontend</code></strong>. في القائمة، حيث ترى <code dir="ltr">v3</code>، قم بتغييره إلى <code dir="ltr">v4</code>. انقر فوق "تحديث" لحفظ التكوين الخاص بك. يخبر هذا التغيير برنامج التحديث باستهداف الإصدار الصحيح عند البحث عن التحديثات.<br /><br /></div>

<div dir="rtl">٣. انتقل إلى صفحة النسخ الاحتياطي. حدد التصدير، ثم حدد مربعات الاختيار للتكوين، وللإحصائيات، وللقواعد المساعدة، ثم اضغط على موافق لتنزيل نسخة احتياطية. لقد حدثت بعض التغييرات. على سبيل المثال، تمت إزالة إجراء "لا تقم بتسجيل الطلب" من القواعد المساعدة (يمكن استخدام خيار "قمع تسجيل" بدلاً من ذلك لتحقيق نفس الشيء). سوف تحتاج إلى استيراد هذه النسخة الاحتياطية مرة أخرى إلى CIDRAM بعد الترقية.<br /><br /></div>

<div dir="rtl">٤. العودة إلى صفحة التحديثات. ينبغي أن تظهر الآن التحديثات الخاصة بالإصدار الرئيسي الجديد. لتجنب انتهاء المهلة، قبل تحديث كل شيء، حاول أولاً تحديث "Core" أو "Front-End" فقط (حيث أن كلاهما يعتمدان على بعضهما البعض، وتحديث أحدهما يجب أن يقوم بتحديث كليهما تلقائيًا على أي حال). نظرًا لأن بنية الصفحة ونمط CSS قد تغير بشكل كبير بين الإصدارات الرئيسية، فقد يبدو الأمر معطلاً في البداية بعد التحديث؛ ولكنه ليس كذلك. انتقل إلى أي صفحة أخرى واضغط على Ctrl+F5 لمحاولة إجراء تحديث شامل (أي تحديث يقوم فيه المتصفح بجلب نسخة جديدة من تصميم CSS والأجهزة الطرفية الأخرى بدلاً من الاعتماد على ذاكرة التخزين المؤقت الخاصة به). يجب أن يظهر هيكل الصفحة وتنسيق CSS بشكل صحيح. إذا لم يظهر، فحاول مسح ذاكرة التخزين المؤقت للمتصفح.<br /><br /></div>

<div dir="rtl">٥. وبعد الانتهاء من ذلك، يمكنك تحديث كل شيء آخر. ارجع إلى صفحة التحديثات، وإذا رأيت الزر في أعلى الصفحة، انقر فوق تحديث الكل.<br /><br /></div>

<div dir="rtl">٦. للتأكد من عدم وجود أي تحديثات سيئة متبقية أو ملفات تالفة، ولضمان أن كل شيء كما ينبغي، انقر فوق إصلاح الكل. نادرًا ما يجب أن تكون هذه مشكلة فعلية، ولكن من الأفضل أن تلعبها بأمان.<br /><br /></div>

<div dir="rtl">٧. العودة إلى صفحة النسخ الاحتياطي. حدد الاستيراد، ثم حدد مربعات الاختيار للتكوين، وللإحصائيات، وللقواعد المساعدة، وانقر فوق الزر لتحديد ملف، ثم حدد موقع النسخة الاحتياطية التي قمت بتنزيلها مسبقًا، ثم اضغط على موافق لاستيراد تلك النسخة الاحتياطية. سيقوم CIDRAM تلقائيًا بإجراء أي تعديلات ضرورية لاستيعاب التغييرات.<br /><br /></div>

<div dir="rtl">٨. لقد انتهيت من الترقية. لا يقدم الإصدار الرئيسي الجديد أي تغييرات على ملفات التوقيع أو الوحدات النمطية أو الأحداث، لذا لا داعي للقلق بشأن ذلك عند الترقية. بعد ذلك، قد ترغب في استكشاف صفحة التكوين بشكل موجز بسبب التغييرات التي أدخلها الإصدار الرئيسي الجديد (على سبيل المثال، للميزات التي تم تقديمها حديثًا).<br /><br /></div>

<div dir="rtl">لمعرفة قائمة التغييرات التي تم إدخالها بواسطة v4 (على سبيل المثال، الميزات المضافة، والميزات التي تمت إزالتها، وما إلى ذلك)، راجع <a href="https://github.com/CIDRAM/CIDRAM/blob/v4/Changelog.md#v400">سجل التغيير</a> v4.<br /><br /></div>

---


<div dir="rtl">آخر تحديث: ٢٨ مارس ٢٠٢٦ (٢٠٢٦.٠٣.٢٨).</div>
