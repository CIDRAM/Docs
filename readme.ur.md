## <div dir="rtl">CIDRAM v4 لیے دستاویزی (اردو).</div>

### <div dir="rtl">فہرست:</div>
<div dir="rtl"><ul>
 <li>۱. <a href="#user-content-SECTION1">تمہید</a></li>
 <li>۲. <a href="#user-content-SECTION2">انسٹال کرنے کا طریقہ</a></li>
 <li>۳. <a href="#user-content-SECTION3">کس طرح استعمال</a></li>
 <li>۴. <a href="#user-content-SECTION4">سامنے کے آخر میں انتظام</a></li>
 <li>۵. <a href="#user-content-SECTION5">کنفگریشن کے اختیارات</a></li>
 <li>۶. <a href="#user-content-SECTION6">دستخط فارمیٹ</a></li>
 <li>۷. <a href="#user-content-SECTION7">جانا جاتا مطابقت کے مسائل</a></li>
 <li>۸. <a href="#user-content-SECTION8">اکثر پوچھے گئے سوالات (FAQ)</a></li>
 <li>۹. <a href="#user-content-SECTION9">قانونی معلومات</a></li>
 <li>۱۰. <a href="#user-content-SECTION10">پچھلے بڑے ورژن سے اپ گریڈ کرنا</a></li>
</ul></div>

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### <div dir="rtl">۱. <a name="SECTION1"></a>تمہید</div>

<div dir="rtl">CIDRAM (غیر طبقاتی انٹر ڈومین روٹنگ رسائی مینیجر) بشمول (لیکن تک محدود نہیں) غیر انسانی رسائی اختتامی پوائنٹس کے، کلاؤڈ سروسز سے ٹریفک ناپسندیدہ ٹریفک کے ہونے کی وجہ سے ذرائع، کے طور پر شمار IP پتوں سے شروع کی درخواستوں کو مسدود کرنے کی طرف سے ویب سائٹس کی حفاظت کے لیے ڈیزائن کیا ایک PHP کی سکرپٹ ہے، اسپیم بوٹس، سکراپارس، وغیرہ یہ باؤنڈ درخواستوں سے فراہم IP پتوں کی ممکنہ CIDR کو شمار کرتے ہیں اور پھر (ان کے دستخط فائلوں ہونے کے ذرائع کے طور پر شمار IP پتوں کی CIDR کی فہرستوں پر مشتمل اس کے دستخط فائلوں کے خلاف ان ممکن CIDR سے ملنے کے لیے کی کوشش کر کے اس کرتا ہے ناپسندیدہ ٹریفک کے)؛ موازنہ نہیں ملا رہے ہیں تو، درخواستوں مسدود ہیں.<br /><br /></div>

<div dir="rtl"><em>(دیکھیں: <a href="#user-content-WHAT_IS_A_CIDR">ایک "CIDR" کیا ہے؟</a>).</em><br /><br /></div>

<div dir="rtl"><a dir="ltr" href="https://cidram.github.io/">CIDRAM</a> کاپی رائٹ 2016 اور <a dir="ltr" href="https://github.com/Maikuolan">Caleb M (Maikuolan)</a> کی طرف GNU/GPLv2 اجازت سے آگے.<br /><br /></div>

<div dir="rtl">یہ سکرپٹ مفت سافٹ ویئر ہے. آپ اسے دوبارہ تقسیم اور / یا ترمیم کے طور پر مفت سافٹ ویئر فاؤنڈیشن کی جانب سے شائع GNU جنرل پبلک لائسنس کی شرائط کے تحت اس پر نظر ثانی کر سکتے ہیں؛ یا تو لائسنس کے ورژن 2، یا (آپ کے اختیارات پر) کسی بھی جدید ورژن. یہ سکرپٹ یہ مفید ہو جائے گا، لیکن کسی بھی وارنٹی کے بغیر امید میں تقسیم کیا جاتا ہے؛ کسی خاص مقصد کے لیے قابل فروختگی یا فٹنس کی بھی تقاضا وارنٹی کے بغیر. مزید تفصیلات کے لیے GNU جنرل پبلک لائسنس، "LICENSE.txt" فائل اور سے بھی دستیاب میں واقع دیکھیں:</div>

- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

<div dir="rtl">CIDRAM یہاں سے آزادانہ طور پر ڈاؤن لوڈ کیا جا سکتا ہے:</div>

- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM).

<div dir="rtl">یہ دستاویز اور اس کے مختلف تراجم یہاں مل سکتے ہیں:</div>

- [GitHub](https://github.com/CIDRAM/Docs).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram-docs).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM-Docs).

---


### <div dir="rtl">۲. <a name="SECTION2"></a>انسٹال کرنے کا طریقہ</div>

#### <div dir="rtl">۲.۰ دستی طور پر نصب</div>

<div dir="rtl">سب سے پہلے، آپ کو CIDRAM کی ایک تازہ کاپی درکار ہوگی. آپ <a dir="ltr" hreflang="en" href="https://github.com/CIDRAM/CIDRAM">CIDRAM/CIDRAM</a> ذخیرے سے CIDRAM کے تازہ ترین ورژن کا آرکائیو ڈاؤن لوڈ کر سکتے ہیں. مخصوص ہونے کے لیے، آپ کو "vault" ڈائریکٹری کی ایک تازہ کاپی درکار ہوگی (محفوظ شدہ دستاویزات میں باقی سب کچھ محفوظ طریقے سے حذف یا نظر انداز کیا جا سکتا ہے).<br /><br /></div>

<div dir="rtl">v3 سے پہلے، CIDRAM فرنٹ اینڈ تک رسائی حاصل کرنے کے لیے آپ کے عوامی جڑ کے اندر کہیں CIDRAM انسٹال کرنا ضروری تھا. تاہم، v3 کے بعد سے، یہ ضروری نہیں ہے. سیکیورٹی کو زیادہ سے زیادہ بنانے اور CIDRAM اور اس کی فائلوں تک غیر مجاز رسائی کو روکنے کے لیے، یہ تجویز کیا جاتا ہے کہ CIDRAM کو اپنے عوامی جڑ سے باہر انسٹال کریں. اس سے کوئی فرق نہیں پڑتا کہ آپ CIDRAM کہاں انسٹال کرتے ہیں، جب تک کہ یہ PHP کے ذریعے قابل رسائی، کہیں معقول حد تک محفوظ، اور کہیں آپ خوش ہوں. اب "vault" ڈائرکٹری کے نام کو برقرار رکھنا بھی ضروری نہیں ہے، لہذا آپ "vault" کا نام بدل کر جو چاہیں رکھ سکتے ہیں (لیکن سہولت کی خاطر، دستاویزات اسے "vault" ڈائریکٹری کے طور پر حوالہ دیتی رہیں گی).<br /><br /></div>

<div dir="rtl">جب آپ تیار ہوں تو، "vault" ڈائرکٹری کو اپنے منتخب کردہ مقام پر اپ لوڈ کریں، اور یقینی بنائیں کہ اس میں PHP کے لیے ڈائرکٹری میں لکھنے کے قابل ہونے کے لیے ضروری اجازتیں ہیں (سسٹم پر منحصر ہے، ہو سکتا ہے آپ کو کچھ کرنے کی ضرورت نہ ہو، یا آپ کو ڈائرکٹری میں CHMOD 755 سیٹ کرنے کی ضرورت ہو، یا اگر 755 کے ساتھ مسائل ہیں، تو آپ 777 کو آزما سکتے ہیں، لیکن کم محفوظ ہونے کی وجہ سے 777 کی سفارش نہیں کی جاتی ہے).<br /><br /></div>

<div dir="rtl">اگلا، CIDRAM آپ کے کوڈ بیس یا CMS کی حفاظت کرنے کے قابل ہونے کے لیے، آپ کو ایک "انٹری پوائنٹ" بنانے کی ضرورت ہوگی. اس طرح کا داخلی نقطہ تین چیزوں پر مشتمل ہے:<br /><br /></div>

<div dir="rtl">
  ۱. آپ کے کوڈ بیس یا CMS پر کہیں "loader.php" فائل کو شامل کرنا.<br />
  ۲. CIDRAM core لانچ کرنا.<br />
  ۳. "protect" کے طریقہ کار کو کال کرنا.<br /><br />
</div>

<div dir="rtl">ایک سادہ مثال:<br /><br /></div>

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

<div dir="rtl">اگر آپ Apache ویب سرور استعمال کر رہے ہیں اور آپ کو <code dir="ltr">php.ini</code> تک رسائی حاصل ہے، تو آپ جب بھی پی ایچ پی کی کوئی درخواست کی جاتی ہے تو آپ CIDRAM کو آگے بڑھانے کے لیے X ہدایت کا استعمال کر سکتے ہیں، جب بھی پی ایچ پی کی درخواست کی جاتی ہے تو آپ CIDRAM کو پہلے سے پینڈ کرنے کے لیے <code dir="ltr">auto_prepend_file</code> ہدایت استعمال کر سکتے. ایسی صورت میں، آپ کا انٹری پوائنٹ بنانے کے لیے سب سے مناسب جگہ اس کی اپنی فائل میں ہوگی، اور پھر آپ اس فائل کا حوالہ دیں گے <code dir="ltr">auto_prepend_file</code> ہدایت پر.<br /><br /></div>

<div dir="rtl">مثال:<br /><br /></div>

`auto_prepend_file = "/path/to/your/entrypoint.php"`

<div dir="rtl">یا یہ <code dir="ltr">.htaccess</code> فائل میں:<br /><br /></div>

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

<div dir="rtl">دوسری صورتوں میں، آپ کا داخلی نقطہ بنانے کے لیے سب سے مناسب جگہ آپ کے کوڈ بیس یا CMS کے اندر جلد از جلد ہوگی. یہ یقینی بنانے کے لیے ہے کہ جب بھی آپ کی ویب سائٹ پر کسی صفحہ تک رسائی حاصل کی جائے گی تو یہ لوڈ ہو جائے گا. اگر آپ کا کوڈ بیس ایک "بوٹسٹریپ" استعمال کرتا ہے، تو آپ کی "بوٹسٹریپ" فائل کا آغاز ہی ایک اچھی مثال ہوگی. اگر آپ کے کوڈ بیس میں ایک مرکزی فائل ہے جو آپ کے ڈیٹا بیس سے جڑنے کے لیے ذمہ دار ہے، تو یہ ایک اور اچھی مثال ہوگی.<br /><br /></div>

#### <div dir="rtl">۲.۱ COMPOSER کے ساتھ نصب</div>

<div dir="rtl"><a href="https://packagist.org/packages/cidram/cidram">CIDRAM Packagist ساتھ رجسٹرڈ ہے</a>، اور اسی طرح، آپ کمپوزر سے واقف ہیں تو، آپ.<br /><br /></div>

`composer require cidram/cidram`

#### <div dir="rtl">۲.۲ ورڈپریس کے لیے نصب</div>

<div dir="rtl"><a href="https://wordpress.org/plugins/cidram/">CIDRAM ورڈپریس پلگ ان کے ڈیٹا بیس کے ساتھ ایک پلگ ان کے طور پر رجسٹرڈ ہے</a>، اور آپ کو پلگ ان ڈیش بورڈ سے براہ راست CIDRAM انسٹال کر سکتے ہیں. آپ کسی بھی دیگر پلگ ان کے طور پر اسی انداز میں اسے انسٹال کر سکتے ہیں، اور کوئی اس کے علاوہ اقدامات کی ضرورت ہے.<br /><br /></div>

<div dir="rtl"><em>انتباہ: ایک صاف تنصیب میں پلگ ان ڈیش بورڈ کے نتائج کے ذریعے CIDRAM تازہ کاری ہو رہی! آپ کو آپ کی تنصیب کے اپنی مرضی کے مطابق کیا ہے تو (اپنی کنفگریشن بدل گیا، نصب ماڈیولز، وغیرہ)، ان کی تخصیصات پلگ ان ڈیش بورڈ کے ذریعے اپ ڈیٹ کر جب ختم ہو جائے گا! لاگ مسلیں بھی ختم ہو جائے گا! لاگ فائلوں اور اصلاح کے تحفظ کے لیے، CIDRAM سامنے کے آخر میں اپ ڈیٹس صفحے کے ذریعے اپ ڈیٹ کریں.</em><br /><br /></div>

#### <div dir="rtl">۲.۳ کنفگریشن اور حسب ضرورت</div>

<div dir="rtl">آپ کے لیے سختی سے تجویز کی جاتی ہے کہ آپ اپنی نئی تنصیب کی کنفگریشن کا جائزہ لیں تاکہ آپ اسے اپنی ضروریات کے مطابق ایڈجسٹ کر سکیں. آپ اضافی ماڈیولز، دستخطی فائلیں انسٹال کرنا، معاون اصول بنانا، یا دیگر تخصیصات کو نافذ کرنا چاہیں گے تاکہ آپ کی تنصیب آپ کی ضروریات کے مطابق ہو سکے. میں ان چیزوں کو کرنے کے لیے فرنٹ اینڈ کو استعمال کرنے کی تجویز کرتا ہوں.<br /><br /></div>

---


### <div dir="rtl">۳. <a name="SECTION3"></a>کس طرح استعمال</div>

<div dir="rtl">CIDRAM خود کار طریقے سے آپ کی ویب سائٹ کو ناپسندیدہ درخواستوں کسی بھی دستی امداد کی ضرورت کے بغیر، ایک طرف اس کی ابتدائی تنصیب سے مسدود کرنا چاہیے.<br /><br /></div>

<div dir="rtl">آپ کو آپ کی کنفگریشن اپنی مرضی کے مطابق اور اپنی مرضی کے مطابق جس CIDR آپ کی کنفیگریشن فائل اور/یا آپ کے دستخط کی فائلوں میں تبدیلی کرنے کی طرف سے بلاک کر رہے ہیں کر سکتے ہیں.<br /><br /></div>

<div dir="rtl">آپ کو کسی بھی جھوٹے مثبت سامنا کرتے ہیں، مجھے اس کے بارے میں مطلع کرنے کے لیے مجھ سے رابطہ کریں. <em>(دیکھیں: <a href="#user-content-WHAT_IS_A_FALSE_POSITIVE">ایک "جھوٹی مثبت" سے کیا مراد ہے؟</a>).</em><br /><br /></div>

<div dir="rtl">CIDRAM دستی طور پر یا سامنے کے اختتام کے ذریعے اپ ڈیٹ کیا جا سکتا ہے. CIDRAM بھی Composer یا WordPress کے ذریعہ اپ ڈیٹ کیا جا سکتا ہے، اگر اصل میں ان کے ذریعہ نصب ہوجائے.<br /><br /></div>

---


### <div dir="rtl">۴. <a name="SECTION4"></a>سامنے کے آخر میں انتظام</div>

#### <div dir="rtl">۴.۰ سامنے کے آخر کیا ہے.<br /><br /></div>

<div dir="rtl">سامنے کے آخر میں، برقرار رکھنے کا انتظام، اور آپ CIDRAM تنصیب کو اپ ڈیٹ کرنے کے لیے ایک آسان اور آسان طریقہ فراہم کرتا ہے. آپ صرف مسودہ دیکھ سکتے ہیں، اشتراک، اور نوشتہ صفحے کے ذریعے لاگ مسلیں لوڈ، آپ کی کنفگریشن کے صفحے کے ذریعے کی کنفگریشن تبدیل کر سکتے ہیں، آپ کو انسٹال کر سکتے ہیں اور اپ ڈیٹس صفحے کے ذریعے انسٹال اجزاء، اور آپ کو اپ لوڈ کر سکتے ہیں، ڈاؤن لوڈ، اتارنا، اور فائل کے ذریعے آپ کے والٹ میں فائلوں پر نظر ثانی مینیجر.<br /><br /></div>

#### <div dir="rtl">۴.۱ فرنٹ اینڈ تک کیسے رسائی حاصل کی جائے.<br /><br /></div>

<div dir="rtl">بالکل پہلے کی طرح، آپ کو فرنٹ اینڈ تک رسائی حاصل کرنے کے لیے ایک انٹری پوائنٹ بنانے کی ضرورت ہوگی. اس طرح کا داخلی نقطہ تین چیزوں پر مشتمل ہے:<br /><br /></div>

<div dir="rtl">
  ۱. آپ کے کوڈ بیس یا CMS پر کہیں "loader.php" فائل کو شامل کرنا.<br />
  ۲. CIDRAM front-end لانچ کرنا.<br />
  ۳. "view" کے طریقہ کار کو کال کرنا.<br /><br />
</div>

<div dir="rtl">ایک سادہ مثال:<br /><br /></div>

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

<div dir="rtl">"FrontEnd" کلاس "Core" کلاس کو بڑھاتی ہے. اس کا مطلب ہے کہ آپ ممکنہ طور پر ناپسندیدہ ٹریفک کو فرنٹ اینڈ تک رسائی سے روکنے کے لیے "view" کے طریقے کو کال کرنے سے پہلے "protect" طریقہ کو کال کر سکتے ہیں. ایسا کرنا مکمل طور پر اختیاری ہے.<br /><br /></div>

<div dir="rtl">ایک سادہ مثال:<br /><br /></div>

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

<div dir="rtl">فرنٹ اینڈ کے لیے انٹری پوائنٹ بنانے کے لیے سب سے مناسب جگہ اس کی اپنی مخصوص فائل میں ہے. پہلے کے برعکس، آپ چاہتے ہیں کہ آپ کا فرنٹ اینڈ انٹری پوائنٹ صرف اس مخصوص فائل کے لیے براہ راست درخواست کر کے قابل رسائی ہو جہاں انٹری پوائنٹ موجود ہو، تو اس صورت میں، آپ <code dir="ltr">auto_prepend_file</code> یا <code dir="ltr">.htaccess</code> استعمال نہیں کرنا چاہیں گے.<br /><br /></div>

<div dir="rtl">اپنا فرنٹ اینڈ انٹری پوائنٹ بنانے کے بعد، اس تک رسائی کے لیے اپنے براؤزر کا استعمال کریں. ایک لاگ ان صفحہ ظاہر ہونا چاہیے. لاگ ان صفحہ پر، پہلے سے طے شدہ صارف نام اور پاس ورڈ <span dir="ltr">(admin/password)</span> درج کریں اور لاگ ان بٹن دبائیں.<br /><br /></div>

<div dir="rtl">نوٹ: اگر آپ کو پہلی بار کے لیے لاگ ان کرنے کے بعد، سامنے کے آخر تک غیر مجاز رسائی کو روکنے کے لیے، آپ کو فوری طور پر آپ کا صارف نام اور پاس ورڈ کو تبدیل کرنا چاہیے! یہ بہت اہم ہے، یہ سامنے کے آخر میں کے ذریعے آپ کی ویب سائٹ پر من مانی PHP کوڈ کو اپ لوڈ کرنا ممکن ہے کیونکہ.<br /><br /></div>

<div dir="rtl">اس کے علاوہ، زیادہ سے زیادہ سیکورٹی کے لیے، تمام فرنٹ اینڈ اکاؤنٹس کے لیے 2FA کو مؤثر طریقے سے سفارش کی جاتی ہے (ذیل میں دی گئی ہدایات).<br /><br /></div>

#### <div dir="rtl">۴.۲ سامنے کے آخر میں کس طرح استعمال.<br /><br /></div>

<div dir="rtl">ہدایات یہ اور اس مقصد کو استعمال کرنے کا صحیح طریقہ کی وضاحت کے لیے سامنے کے آخر میں کے ہر صفحے پر فراہم کی جاتی ہیں. اگر آپ کو مزید وضاحت یا کوئی خاص مدد کی ضرورت ہے، کی مدد سے رابطہ کریں. متبادل طور پر، یو ٹیوب پر دستیاب کچھ ویڈیوز مظاہرے کی راہ کی طرف مدد کر سکتا ہے جس میں موجود ہیں.<br /><br /></div>

#### <div dir="rtl">۴.۳ 2FA<br /><br /></div>

<div dir="rtl">2FA کو چالو کرنے کے ذریعہ front-end کو مزید محفوظ بنانے کے لیے ممکن ہے. جب 2FA کے ساتھ اکاؤنٹ میں لاگ ان ہو تو، اس اکاؤنٹ سے منسلک ای میل ایڈریس پر ایک ای میل بھیجا جاتا ہے. اس ای میل میں "2FA کوڈ" شامل ہے، جو اس صارف کا استعمال کرتے ہوئے لاگ ان کرنے کے لۓ صارف کا نام اور پاسورڈ کے علاوہ صارف کو داخل ہونا ضروری ہے. اس کا مطلب یہ ہے کہ اکاؤنٹ اکاؤنٹ پاس ورڈ حاصل کرنے کے لیے کسی بھی ہیکر یا ممکنہ حملہ آور کو اس اکاؤنٹ میں لاگ ان کرنے کے قابل نہیں ہو گا، کیونکہ انہیں وصول کرنے کے قابل ہونے کے لیے ان اکاؤنٹ سے منسلک ای میل ایڈریس تک رسائی حاصل ہوگی. اور سیشن کے ساتھ منسلک 2FA کوڈ استعمال کریں.<br /><br /></div>

<div dir="rtl">سب سے پہلے، 2FA کو چالو کرنے کے لیے، PHPMailer اجزاء کو انسٹال کرنے کے لیے front-end اپ ڈیٹس کا صفحہ استعمال کریں. ای میل بھیجنے کے لیے CIDRAM PHPMailer کا استعمال کرتا ہے.<br /><br /></div>

<div dir="rtl">PHPMailer نصب کرنے کے بعد، آپ کو CIDRAM کنفگریشن کے صفحے یا کنفگریشن کی فائل کے ذریعے PHPMailer کے لیے کنفگریشن ہدایات کو آباد کرنے کی ضرورت ہوگی. ان کنفگریشنات کے ہدایات کے بارے میں مزید معلومات اس دستاویز کے کنفگریشن کے حصے میں شامل ہیں. PHPMailer کنفگریشن ہدایات آبادی کے بعد، <code dir="ltr">enable_two_factor</code> <code dir="ltr">true</code> سیٹ کریں. 2FA اب فعال ہونا چاہیے.<br /><br /></div>

<div dir="rtl">اگلا، آپ کو ایک ای میل ایڈریس کو اکاؤنٹ کے ساتھ منسلک کرنے کی ضرورت ہوگی، تاکہ CIDRAM کو معلوم ہے کہ اس اکاؤنٹ کے ساتھ لاگ ان کرتے وقت 2FA کوڈ بھیجنے کے لیے. ایسا کرنے کے لیے، اکاؤنٹ کے صارف نام کے طور پر ای میل پتہ استعمال کریں (کچھ <code dir="ltr">foo@bar.tld</code> کی طرح)، یا اس صارف کے صارف کے حصے کے طور پر ای میل ایڈریس بھی شامل ہے جس طرح آپ عام طور پر ای میل بھیجیں گے (کچھ <code dir="ltr">Foo Bar &lt;foo@bar.tld&gt;</code> کی طرح).<br /><br /></div>

<div dir="rtl">نوٹ: غیر مجاز رسائی کے خلاف vault کی حفاظت خاص طور پر اہم ہے (مثال کے طور پر، آپ کے سرور کی سیکیورٹی کو مضبوط کرنا، عوامی رسائی کی اجازت محدود)، کیونکہ غیر مجاز رسائی آپ کے SMTP کنفگریشنات کو بے نقاب کر سکتا ہے (اس میں SMTP صارف کا نام اور پاس ورڈ بھی شامل ہے). آپ کو اس بات کو یقینی بنانا چاہیے کہ 2FA کو چالو کرنے سے پہلے vault مناسب طریقے سے محفوظ ہو. اگر آپ ایسا کرنے میں قاصر ہیں تو، کم سے کم، آپ کو ایک نیا ای میل اکاؤنٹ بنانا چاہیے، اس مقصد کے لیے وقف کردہ SMTP کنفگریشنات کے خطرات کو کم کرنے کے لیے.<br /><br /></div>

---


### <div dir="rtl">۵. <a name="SECTION5"></a>کنفگریشن کے اختیارات</div>

<div dir="rtl">ندرجہ ذیل ان ہدایات کے مقصد کی وضاحت کے ساتھ ساتھ، <code dir="ltr">"config.yml"</code> کنفگریشن فائل میں CIDRAM کو دستیاب ہدایات کی ایک فہرست ہے.<br /><br /></div>

```
کنفگریشن (v4)
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

#### <div dir="rtl">"general" (قسم)<br /></div>
<div dir="rtl">عام کنفگریشنات (کنفیگریشن جس کا تعلق دوسری قسموں سے نہیں ہے).<br /><br /></div>

##### <div dir="rtl">"stages" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>عمل درآمد کے مراحل کے لیے کنٹرول (فعال کرنے کے اقدامات، غلطی لاگنگ، وغیرہ).</li></ul></div>

```
stages───[اس مرحلے کو فعال کریں؟]─[اس مرحلے کے دوران پیدا ہونے والی کسی غلطی کو لاگ کریں؟]─[IP ٹریکنگ کی طرف اس مرحلے کے دوران پیدا ہونے والی خلاف ورزیوں کو شمار کریں؟]
├─BanCheck ("چیک کریں کہ آیا پابندی لگائی گئی ہے")
├─Tests ("دستخطی فائلوں کے ٹیسٹ پر عمل کریں")
├─Modules ("ماڈیولز پر عمل کریں")
├─SearchEngineVerification ("سرچ انجن کی تصدیق پر عمل کریں")
├─SocialMediaVerification ("سوشل میڈیا کی تصدیق پر عمل کریں")
├─OtherVerification ("دوسری توثیق پر عمل کریں")
├─Aux ("معاون قوانین پر عمل کریں")
├─Tracking ("IP ٹریکنگ پر عمل کریں")
├─RL ("ریٹ محدود کرنے پر عمل کریں")
├─CAPTCHA ("CAPTCHA تعینات کریں (بلاک شدہ درخواستیں)")
├─Reporting ("رپورٹنگ پر عمل کریں")
├─Statistics ("اعداد و شمار کو اپ ڈیٹ کریں")
├─Webhooks ("ویب ہکس پر عمل کریں")
├─TriggerNotifications ("ای میل ٹرگر اطلاع کی قطار پر کارروائی کریں")
├─PrepareFields ("آؤٹ پٹ اور لاگز کے لیے فیلڈز تیار کریں")
├─Output ("آؤٹ پٹ پیدا کریں (بلاک شدہ درخواستیں)")
├─WriteLogs ("لاگ فائلوں میں لکھیں (بلاک شدہ درخواستیں)")
├─Terminate ("درخواست کو ختم کریں (بلاک شدہ درخواستیں)")
├─AuxRedirect ("معاون قوانین کے مطابق ری ڈائریکٹ کریں")
└─NonBlockedCAPTCHA ("CAPTCHA تعینات کریں (غیر مسدود درخواستیں)")
```

##### <div dir="rtl">"fields" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>بلاک ہونے پر فیلڈز کے لیے کنٹرول (جب کوئی درخواست بلاک ہو جاتی ہے).</li></ul></div>

```
fields───[کیا یہ فیلڈ لاگ اندراجات میں ظاہر ہونا چاہیے؟]─[کیا یہ فیلڈ "رسائی مسترد کر دی" صفحہ پر ظاہر ہونا چاہیے؟]─[جب یہ فیلڈ خالی ہو تو اسے چھوڑ دیں؟]
├─ID ("ID")
├─ScriptIdent ("اسکرپٹ ورژن")
├─DateTime ("تاریخ وقت")
├─IPAddr ("IP پتہ")
├─IPAddrResolved ("IP پتہ (حل کیا)")
├─Query ("طلب")
├─Referrer ("حوالہ دہندہ")
├─UA ("صارف ایجنٹ")
├─UALC ("صارف ایجنٹ (کم کیس)")
├─SignatureCount ("دستخط شمار")
├─Signatures ("دستخط حوالہ")
├─WhyReason ("کیوں بلاک شدہ")
├─ReasonMessage ("کیوں بلاک شدہ (تفصیلی)")
├─rURI ("دوبارہ تعمیر URI")
├─Infractions ("خلاف ورزی")
├─ASNLookup ("** ASN کی تلاش")
├─CCLookup ("** ملک کا کوڈ کی تلاش")
├─Verified ("تصدیق شدہ شناخت")
├─Expired ("میعاد ختم")
├─Ignored ("نظر انداز")
├─Request_Method ("درخواست کا طریقہ")
├─Protocol ("پروٹوکول")
├─SEC_CH_UA_PLATFORM ("!! SEC_CH_UA_PLATFORM")
├─SEC_CH_UA_MOBILE ("!! SEC_CH_UA_MOBILE")
├─SEC_CH_UA ("!! SEC_CH_UA")
├─Hostname ("میزبان کا نام")
├─CAPTCHA ("CAPTCHA کے ریاست")
├─Inspection ("* حالات کا معائنہ")
└─ClientL10NAccepted ("زبان کا حل")
```

* صرف معاون قواعد کو ڈیبگ کرنے کے لیے بنایا گیا ہے. مسدود صارفین کو ظاہر نہیں کیا گیا.

** ASN تلاش کی فعالیت کی ضرورت ہے (مثال کے طور پر، IP-API یا BGPView ماڈیول کے ذریعے).

!! یہ کم اینٹروپی کلائنٹ کا اشارہ ہے. کلائنٹ کے اشارے ایک نئی، تجرباتی ویب ٹیکنالوجی ہے جو ابھی تک تمام براؤزرز اور بڑے کلائنٹس میں وسیع پیمانے پر تعاون یافتہ نہیں ہے. <em>دیکھیں: <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA#browser_compatibility" dir="ltr" hreflang="en-US" rel="noopener noreferrer external">Sec-CH-UA - HTTP | MDN</a>.</em> اگرچہ کلائنٹ کے اشارے فنگر پرنٹنگ کے لیے کارآمد ثابت ہو سکتے ہیں، کیونکہ وہ وسیع پیمانے پر تعاون یافتہ نہیں ہیں، لیکن درخواستوں میں ان کی موجودگی کو فرض نہیں کیا جانا چاہیے اور نہ ہی ان پر انحصار کیا جانا چاہیے (یعنی، ان کی غیر موجودگی کی بنیاد پر بلاک کرنا ایک برا خیال ہے).

##### <div dir="rtl">"timezone" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>استعمال کرنے کے لیے ٹائم زون کی وضاحت کرتا ہے (جیسے، Africa/Cairo، America/New_York، Asia/Tokyo، Australia/Perth، Europe/Berlin، Pacific/Guam، وغیرہ). SYSTEM کی وضاحت کریں تاکہ PHP کو آپ کے لیے خود بخود یہ سنبھل سکے.</li></ul></div>

```
timezone
├─SYSTEM ("نظام کو پہلے سے طے شدہ ٹائم زون کا استعمال کریں.")
├─UTC ("UTC")
└─…دیگر
```

##### <div dir="rtl">"time_offset" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>ٹائم زون منٹ میں آفسیٹ.</li></ul></div>

##### <div dir="rtl">"time_format" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>CIDRAM کی طرف سے استعمال کی تاریخوں کا فارم. اضافی اختیارات درخواست پر شامل کیا جا سکتا ہے.</li></ul></div>

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
└─…دیگر
```

<strong><em>پلیس ہولڈر – وضاحت – <span dir="ltr">2024-04-30T18:27:49+08:00</span> پر مبنی مثال.</em></strong><br />
<strong><code dir="ltr">{yyyy}</code></strong> – سال – جیسے، 2024.<br />
<strong><code dir="ltr">{yy}</code></strong> – مختصر سال – جیسے، 24.<br />
<strong><code dir="ltr">{Mon}</code></strong> – مہینے کا مختصر نام (انگریزی میں) – جیسے، Apr.<br />
<strong><code dir="ltr">{mm}</code></strong> – پہلے صفر کے ساتھ مہینے – جیسے، 04.<br />
<strong><code dir="ltr">{m}</code></strong> – مہینے – جیسے، 4.<br />
<strong><code dir="ltr">{Day}</code></strong> – دن کا مختصر نام (انگریزی میں) – جیسے، Tue.<br />
<strong><code dir="ltr">{dd}</code></strong> – پہلے صفر کے ساتھ دن – جیسے، 30.<br />
<strong><code dir="ltr">{d}</code></strong> – دن – جیسے، 30.<br />
<strong><code dir="ltr">{hh}</code></strong> – پہلے صفر کے ساتھ گھنٹہ (24 گھنٹے کا وقت استعمال کرتا ہے) – جیسے، 18.<br />
<strong><code dir="ltr">{h}</code></strong> – گھنٹہ (24 گھنٹے کا وقت استعمال کرتا ہے) – جیسے، 18.<br />
<strong><code dir="ltr">{ii}</code></strong> – پہلے صفر کے ساتھ منٹ – جیسے، 27.<br />
<strong><code dir="ltr">{i}</code></strong> – منٹ – جیسے، 27.<br />
<strong><code dir="ltr">{ss}</code></strong> – پہلے صفر کے ساتھ سیکنڈ – جیسے، 49.<br />
<strong><code dir="ltr">{s}</code></strong> – سیکنڈ – جیسے، 49.<br />
<strong><code dir="ltr">{tz}</code></strong> – ٹائم زون (بغیر رابطہ کے) – جیسے، <span dir="ltr">+0800</span>.<br />
<strong><code dir="ltr">{t:z}</code></strong> – ٹائم زون (رابطہ کے ساتھ) – جیسے، <span dir="ltr">+08:00</span>.

##### <div dir="rtl">"ipaddr" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>کہاں درخواستوں منسلک کرنے کے IP ایڈریس کو تلاش کرنے کے لیے؟ (Cloudflare جیسی خدمات کے لیے مفید ہے). پہلے سے طے شدہ = REMOTE_ADDR. انتباہ: جب تک کہ آپ کو پتہ ہے تم کیا کر رہے ہو اس کو تبدیل نہ کریں!</li></ul></div>

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (پہلے سے طے شدہ)")
└─…دیگر
```

<div dir="rtl">بھی دیکھو:<ul dir="rtl">
<li><a dir="ltr" href="https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/">NGINX Reverse Proxy</a></li>
<li><a dir="ltr" href="http://www.squid-cache.org/Doc/config/forwarded_for/">Squid configuration directive forwarded_for</a></li>
<li><a dir="ltr" href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded">Forwarded - HTTP \| MDN</a></li>
</ul></div>

##### <div dir="rtl">"http_response_header_code" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>درخواستوں کو روکنے پر بھیجنے کے لیے HTTP حیثیت کا پیغام.</li></ul></div>

```
http_response_header_code───[پہلے سے طے شدہ]─[قانونی]─[پابندی]
├─200 (200 OK (ٹھیک ہے)): کم سے کم مضبوط، لیکن سب سے زیادہ صارف دوست.
│ خودکار درخواستیں غالباً اس جواب کی تشریح
│ کریں گی کہ درخواست کامیاب تھی. غیر مسدود
│ درخواستوں کے لیے تجویز کردہ.
├─403 (403 Forbidden (ممنوعہ)): زیادہ مضبوط، لیکن کم صارف دوست. زیادہ تر
│ عام حالات کے لیے تجویز کردہ.
├─410 (410 Gone (چلا گیا)): غلط مثبت کو حل کرتے وقت مسائل پیدا ہوسکتے
│ ہیں، کیونکہ کچھ براؤزر اس حیثیت کا پیغام
│ کو کیش کریں گے اور بعد میں درخواستیں نہیں
│ بھیجیں گے. کچھ سیاق و سباق میں استعمال
│ کرنے کے لیے بہترین ہو سکتا ہے.
├─418 (418 I'm a teapot (میں چائے کا برتن)): اپریل فول کے لطیفے کا حوالہ دیتے ہیں (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). کسی بھی
│ کلائنٹ، بوٹ، براؤزر، یا کسی اور طرح سے
│ سمجھنے کا امکان نہیں ہے. تفریح اور سہولت
│ کے لیے فراہم کی گئی ہے، لیکن عام طور پر
│ تجویز نہیں کی جاتی ہے.
├─451 (451 Unavailable For Legal Reasons (قانونی وجوہات کی بنا پر دستیاب نہیں ہے)): بنیادی طور پر قانونی وجوہات کی بنا پر
│ مسدود کرنے پر تجویز کیا جاتا ہے. دوسرے
│ سیاق و سباق میں سفارش نہیں کی جاتی ہے.
└─503 (503 Service Unavailable (سروس میسر نہیں)): سب سے زیادہ مضبوط، لیکن کم از کم صارف دوست.
  حملے کے دوران، یا انتہائی مسلسل ناپسندیدہ
  ٹریفک سے نمٹنے کے لیے تجویز کردہ.
```

__۱.__ جب "سائلنٹ موڈ" نافذ ہوتا ہے، تو <strong><code dir="ltr">silent_mode_response_header_code⬅general</code></strong> کے ذریعے بیان کردہ HTTP حیثیت کا پیغام استعمال کیا جائے گا (یہ سب سے زیادہ ترجیح ہے).

__۲.__ جب درخواست بھیجنے والے پر خلاف ورزی کی حد سے تجاوز کرنے کی وجہ سے پابندی لگا دی گئی ہے، تو "پابندی" کے لیے HTTP حیثیت کا پیغام استعمال کیا جائے گا.

__۳.__ جب شرح کو محدود کرنے کی وجہ سے بلاک کیا جائے گا، 429 استعمال کیا جائے گا، یا جب وسائل کے تنازعات کی وجہ سے بلاک کیا جائے گا، تو <strong><code dir="ltr">conflict_response⬅signatures</code></strong> کے ذریعے بیان کردہ HTTP حیثیت کا پیغام استعمال کیا جائے گا (اس تناظر میں شرح محدود اور وسائل کے تنازعات کو یکساں ترجیح حاصل ہے).

__۴.__ جب "HTTP حیثیت کا کوڈ اوور رائڈ" سیٹ کرنے والے معاون اصول کی وجہ سے بلاک کیا جاتا ہے، تو وہ HTTP حیثیت کا کوڈ اوور رائڈ استعمال کیا جائے گا.

__۵.__ جب قانونی وجوہات کی وجہ سے مسدود کیا جاتا ہے (یعنی، جب کسی حسب ضرورت دستخط کی وجہ سے مسدود کیا جاتا ہے جس میں "قانونی" شارٹ ہینڈ لفظ استعمال ہوتا ہے)، تو "قانونی" کے لیے HTTP حیثیت کا پیغام استعمال کیا جائے گا.

__۶.__ دیگر تمام مسدود درخواستوں کے لیے، "پہلے سے طے شدہ" کے لیے HTTP حیثیت کا پیغام استعمال کیا جائے گا (یہ سب سے کم ترجیح ہے).

##### <div dir="rtl">"silent_mode" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>خاموشی CIDRAM چاہیے "رسائی مسترد کر دی" کے صفحے کی نمائش سے بلاک رسائی کی کوششوں کو ری ڈائریکٹ کرنے کے بجائے؟ ہاں تو، کو بلاک کر تک رسائی کی کوششوں کو ری ڈائریکٹ کرنے کے محل وقوع کی وضاحت. کوئی تو اس متغیر خالی چھوڑ.</li></ul></div>

##### <div dir="rtl">"silent_mode_response_header_code" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>بلاک شدہ رسائی کی کوششوں کو خاموشی سے ری ڈائریکٹ کرتے وقت CIDRAM کو کون سا HTTP حیثیت کا پیغام بھیجنا چاہیے؟</li></ul></div>

```
silent_mode_response_header_code
├─301 (301 Moved Permanently (مستقل طور پر منتقل ہو گیا)): کلائنٹ کو ہدایت کرتا ہے کہ ری ڈائریکٹ
│ مستقل ہے، اور یہ کہ ری ڈائریکٹ کے لیے
│ استعمال ہونے والا کا طریقہ ابتدائی
│ درخواست کے لیے استعمال کیے جانے والے
│ درخواست کے طریقہ سے مختلف ہو سکتا ہے.
├─302 (302 Found (ملا)): کلائنٹ کو ہدایت کرتا ہے کہ ری ڈائریکٹ
│ عارضی ہے، اور یہ کہ ری ڈائریکٹ کے لیے
│ استعمال ہونے والا درخواست کا طریقہ
│ ابتدائی درخواست کے لیے استعمال کیے جانے
│ والے درخواست کے طریقہ سے مختلف ہو سکتا ہے.
├─307 (307 Temporary Redirect (عارضی ری ڈائریکٹ)): کلائنٹ کو ہدایت کرتا ہے کہ ری ڈائریکٹ
│ عارضی ہے، اور یہ کہ ری ڈائریکٹ کے لیے
│ استعمال ہونے والا درخواست کا طریقہ
│ ابتدائی درخواست کے لیے استعمال کیے جانے
│ والے درخواست کے طریقہ سے مختلف نہیں ہو
│ سکتا.
└─308 (308 Permanent Redirect (مستقل ری ڈائریکٹ)): کلائنٹ کو ہدایت کرتا ہے کہ ری ڈائریکٹ
  مستقل ہے، اور یہ کہ ری ڈائریکٹ کے لیے
  استعمال ہونے والا درخواست کا طریقہ
  ابتدائی درخواست کے لیے استعمال کیے جانے
  والے درخواست کے طریقہ سے مختلف نہیں ہو
  سکتا.
```

اس بات سے کوئی فرق نہیں پڑتا ہے کہ ہم کلائنٹ کو کیسے ہدایت دیتے ہیں، یہ یاد رکھنا ضروری ہے کہ آخر کار ہمارا اس پر کوئی کنٹرول نہیں ہے کہ کلائنٹ کیا کرنا چاہتا ہے، اور اس بات کی کوئی ضمانت نہیں ہے کہ کلائنٹ ہماری ہدایات کا احترام کرے گا.

##### <div dir="rtl">"lang" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>CIDRAM کے لیے پہلے سے طے شدہ زبان کی وضاحت.</li></ul></div>

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
<div dir="rtl"><ul><li>جب بھی ممکن ہو HTTP_ACCEPT_LANGUAGE کے مطابق لوکلائز کریں؟ True (سچے) = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = نہیں.</li></ul></div>

##### <div dir="rtl">"numbers" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>آپ کس طرح تعداد میں ظاہر کرنے کے لیے پسند کرتے ہیں؟ مثال کے طور پر منتخب کریں جو آپ کے لیے سب سے زیادہ درست نظر آتے ہیں.</li></ul></div>

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
<div dir="rtl"><ul><li>اگر آپ چاہتے ہیں، تو آپ صارفین کو جب انہیں بلاک کر رہے ہیں تو دینے کے لیے ای میل ایڈریس کی فراہمی کر سکتے ہیں.وہ اسے استعمال آپ سے رابطہ کرنے کے لیے کر سکتے ہیں اگر وہ غلطی سے بلاک کر رہے ہیں. انتباہ: آپ جو بھی ای میل ایڈریس پر فراہمی کرتے ہیں، وہ یقینی طور پر سپےمبٹس اور کھرچنی کی طرف سے حاصل کیے جائیں گے. اس کی وجہ سے، اس کی سختی سے سفارش کی جاتی ہے کہ آپ ایک ای میل ایڈریس انتخاب کرتے ہیں جو ڈسپوزایبل یا غیر اہم ہے (یعنی.، آپ کی ذاتی یا کاروباری ای میل ایڈریس کا استعمال نہ کریں).</li></ul></div>

##### <div dir="rtl">"emailaddr_display_style" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>آپ کو ای میل ایڈریس کو کس طرح صارفین کو پیش کرنا پسند ہے؟</li></ul></div>

```
emailaddr_display_style
├─default ("کلک کرنے والے لنک")
└─noclick ("متن جو کلک نہیں کیا جا سکتا")
```

##### <div dir="rtl">"default_dns" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>میزبان نام تلاش کرنے کے لیے استعمال کرنے کے لیے DNS سرورز کی فہرست. انتباہ: جب تک کہ آپ کو پتہ ہے تم کیا کر رہے ہو اس کو تبدیل نہ کریں!</li></ul></div>

__FAQ.__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.ur.md#میں-default_dns-کے-لیے-کیا-استعمال-کر-سکتا-ہوں" hreflang="ur-PK">میں "default_dns" کے لیے کیا استعمال کر سکتا ہوں؟</a></em>

##### <div dir="rtl">"default_algo" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اس بات کی وضاحت کرتا ہے جو تمام مستقبل کے پاس ورڈ اور سیشن کے لیے الگورتھم استعمال کرنا ہے.</li></ul></div>

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### <div dir="rtl">"statistics" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>کنٹرول کرتا ہے کہ کون سی شماریاتی معلومات کو ٹریک کرنا ہے.</li></ul></div>

```
statistics───[IPv4]─[IPv6]─[دیگر]
├─Blocked ("درخواستوں پر بلاک کر دی گئی")
├─Banned ("درخواستوں پر پابندی لگا دی گئی")
├─Passed ("درخواستیں گزر گئیں")
├─ReportOK ("درخواستوں کی اطلاع بیرونی API کو دی گئی – ٹھیک ہے")
└─ReportFailed ("درخواستوں کی اطلاع بیرونی API کو دی گئی – ناکامی")
```

نوٹ: معاون قواعد کے اعداد و شمار کو ٹریک کرنا ہے یا نہیں، معاون قواعد کے صفحہ سے کنٹرول کیا جا سکتا ہے.

##### <div dir="rtl">"statistics_captchas" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>کنٹرول کرتا ہے کہ CAPTCHA کے لیے کون سی شماریاتی معلومات کو ٹریک کرنا ہے.</li></ul></div>

```
statistics_captchas───[ناکامی]─[کامیابی]─[خدمت کی]
├─HCaptcha ("hCaptcha")
├─FriendlyCaptcha ("Friendly Captcha")
└─CloudflareTurnstile ("Cloudflare Turnstile")
```

نوٹ: معاون قواعد کے اعداد و شمار کو ٹریک کرنا ہے یا نہیں، معاون قواعد کے صفحہ سے کنٹرول کیا جا سکتا ہے.

##### <div dir="rtl">"force_hostname_lookup" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>تمام درخواستوں کے لیے میزبانی حاصل کریں؟ True (سچے) = جی ہاں؛ False (جھوٹی) = نہیں [پہلے سے طے شدہ]. میزبان نام کی تلاش عام طور پر "ضرورت کی بنیاد" کی بنیاد پر انجام دیا جاتا ہے، لیکن تمام درخواستوں کے لیے مجبور کیا جاسکتا ہے. ایسا کرتے ہوئے لاگ ان میں مزید تفصیلی معلومات فراہم کرنے کے ذریعہ مفید ثابت ہوسکتا ہے، لیکن کارکردگی پر تھوڑا منفی اثر بھی ہوسکتا ہے.</li></ul></div>

##### <div dir="rtl">"allow_gethostbyaddr_lookup" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>جب UDP دستیاب نہیں ہے تو gethostbyaddr کی تلاش کی اجازت دیں؟ True (سچے) = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = نہیں.</li></ul></div>

نوٹ: ہو سکتا ہے IPv6 تلاش کچھ 32 بٹ سسٹمز پر صحیح طریقے سے کام نہ کرے.

##### <div dir="rtl">"disabled_channels" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>درخواستوں کو بھیجنے کے لیے خاص طور پر چینلز کا استعمال کے لیے CIDRAM کو روکنے کے لیے یہ استعمال کیا جا سکتا ہے (مثال کے طور پر، جب اپ ڈیٹ کرنا، اجزاء میٹا ڈیٹا، وغیرہ کو پکڑنے کے بعد).</li></ul></div>

```
disabled_channels
├─GitHub ("<span class="origin us">US</span> GitHub")
├─BitBucket ("<span class="origin us">US</span> BitBucket")
├─Codeberg ("<span class="origin de">DE</span> Codeberg")
└─GoogleDNS ("<span class="origin us">US</span> GoogleDNS")
```

##### <div dir="rtl">"request_proxy" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اگر آپ چاہتے ہیں کہ باہر جانے والی درخواستیں کسی پراکسی کے ذریعے بھیجی جائیں، تو اس پراکسی کو یہاں بیان کریں. اگر نہیں، تو اسے خالی چھوڑ دیں.</li></ul></div>

##### <div dir="rtl">"request_proxyauth" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اگر پراکسی کے ذریعے آؤٹ باؤنڈ درخواستیں بھیج رہے ہیں اور اگر اس پراکسی کو صارف نام اور پاس ورڈ کی ضرورت ہے، تو وہ صارف نام اور پاس ورڈ یہاں بتائیں (مثال کے طور پر، <code dir="ltr">user:pass</code>). اگر نہیں، تو اسے خالی چھوڑ دیں.</li></ul></div>

##### <div dir="rtl">"default_timeout" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>بیرونی درخواستوں کے لیے استعمال کرنے کے لیے پہلے سے طے شدہ ٹائم آؤٹ؟ پہلے سے طے شدہ = 12 سیکنڈ.</li></ul></div>

##### <div dir="rtl">"sensitive" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>حساس صفحات کے طور پر شمار کرنے کے لیے راستوں کی فہرست. فہرست میں شامل ہر راستے کو ضرورت پڑنے پر دوبارہ تعمیر شدہ URI کے خلاف چیک کیا جائے گا. ایک راستہ جو فارورڈ سلیش سے شروع ہوتا ہے اسے لغوی سمجھا جائے گا، اور درخواست کے پاتھ جزو سے مماثل ہوگا. ایک راستہ جو ایک غیر حروفِ عددی کریکٹر سے شروع ہوتا ہے، اور اسی کریکٹر (یا وہی کریکٹر کے علاوہ ایک اختیاری "i" جھنڈا) پر ختم ہوتا ہے اسے ریگولر ایکسپریشن سمجھا جائے گا. کسی دوسرے قسم کے راستے کو لفظی سمجھا جائے گا، اور URI کے کسی بھی حصے سے مماثل ہو سکتا ہے. ایک پاتھ کو حساس صفحہ کے طور پر سمجھا جا سکتا ہے کچھ ماڈیولز کے برتاؤ کو متاثر کر سکتا ہے، لیکن اس کا کوئی دوسرا اثر نہیں ہوتا ہے.</li></ul></div>

##### <div dir="rtl">"email_notification_address" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اگر آپ نے CIDRAM سے ای میل کے ذریعے اطلاعات موصول کرنے کا انتخاب کیا ہے، مثال کے طور پر، جب مخصوص معاون قوانین کو متحرک کیا جاتا ہے، آپ ان اطلاعات کے لیے وصول کنندہ کا پتہ یہاں بتا سکتے ہیں.</li></ul></div>

##### <div dir="rtl">"email_notification_name" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اگر آپ نے CIDRAM سے ای میل کے ذریعے اطلاعات موصول کرنے کا انتخاب کیا ہے، مثال کے طور پر، جب مخصوص معاون قوانین کو متحرک کیا جاتا ہے، آپ ان اطلاعات کے لیے وصول کنندہ کا نام یہاں بتا سکتے ہیں.</li></ul></div>

##### <div dir="rtl">"email_notification_when" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>جنریٹ ہونے کے بعد اطلاعات کب بھیجیں.</li></ul></div>

```
email_notification_when
├─Immediately ("فوراً.")
├─After24Hours ("24 گھنٹوں کے بعد، ایک ساتھ بنڈل (یا جب دستی طور پر ٹرگر کیا جاتا ہے، جیسے، cron کے ذریعے).")
└─ManuallyOnly ("صرف اس وقت جب دستی طور پر ٹرگر کیا جائے (جیسے، cron کے ذریعے).")
```

#### <div dir="rtl">"components" (قسم)<br /></div>
<div dir="rtl">CIDRAM کی طرف سے استعمال ہونے والے اجزاء کو چالو کرنے اور غیر فعال کرنے کے لیے کنفگریشن. عام طور پر اپ ڈیٹس صفحہ کے ذریعے آباد ہوتا ہے، لیکن بہتر کنٹرول کے لیے اور اپ ڈیٹس صفحہ کے ذریعے پہچانے جانے والے حسب ضرورت اجزاء کے لیے بھی یہاں سے منظم کیا جا سکتا ہے.<br /><br /></div>

##### <div dir="rtl">"ipv4" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>IPv4 دستخطی فائلیں.</li></ul></div>

##### <div dir="rtl">"ipv6" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>IPv6 دستخطی فائلیں.</li></ul></div>

##### <div dir="rtl">"modules" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ماڈیولز.</li></ul></div>

##### <div dir="rtl">"imports" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>درآمدات. عام طور پر CIDRAM کو جزو کی کنفگریشن کی معلومات فراہم کرنے کے لیے استعمال کیا جاتا ہے.</li></ul></div>

##### <div dir="rtl">"events" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>ایونٹ ہینڈلرز. عام طور پر استعمال کیا جاتا ہے جس طرح سے CIDRAM اندرونی طور پر برتاؤ کرتا ہے یا اضافی فعالیت فراہم کرتا ہے.</li></ul></div>

#### <div dir="rtl">"logging" (قسم)<br /></div>
<div dir="rtl">لاگنگ سے متعلق کنفیگریشن (اس کو چھوڑ کر جو دیگر زمروں پر لاگو ہوتا ہے).<br /><br /></div>

##### <div dir="rtl">"standard_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تمام بلاک کر تک رسائی کی کوششوں کو لاگ ان کرنے کے لیے انسانی قابل مطالعہ فائل. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li></ul></div>

مفید مشورہ: آپ ٹائم فارمیٹ پلیس ہولڈرز کا استعمال کرکے لاگ فائلوں کے ناموں کے ساتھ تاریخ/وقت کی معلومات منسلک کرسکتے ہیں. دستیاب وقت کی شکل کے پلیس ہولڈرز <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="ltr">time_format⬅general</code></a> پر دکھائے جاتے ہیں.

##### <div dir="rtl">"apache_style_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تمام بلاک کر تک رسائی کی کوششوں کو لاگ ان کرنے کے لیے اپاچی طرز فائل. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li></ul></div>

مفید مشورہ: آپ ٹائم فارمیٹ پلیس ہولڈرز کا استعمال کرکے لاگ فائلوں کے ناموں کے ساتھ تاریخ/وقت کی معلومات منسلک کرسکتے ہیں. دستیاب وقت کی شکل کے پلیس ہولڈرز <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="ltr">time_format⬅general</code></a> پر دکھائے جاتے ہیں.

##### <div dir="rtl">"serialised_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تمام بلاک کر تک رسائی کی کوششوں کو لاگ ان کرنے کے لیے serialized کی فائل. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li></ul></div>

مفید مشورہ: آپ ٹائم فارمیٹ پلیس ہولڈرز کا استعمال کرکے لاگ فائلوں کے ناموں کے ساتھ تاریخ/وقت کی معلومات منسلک کرسکتے ہیں. دستیاب وقت کی شکل کے پلیس ہولڈرز <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="ltr">time_format⬅general</code></a> پر دکھائے جاتے ہیں.

##### <div dir="rtl">"error_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>کسی بھی غیر مہلک غلطیوں کو لاگ کرنے کے لیے ایک فائل کا پتہ چلا. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li></ul></div>

مفید مشورہ: آپ ٹائم فارمیٹ پلیس ہولڈرز کا استعمال کرکے لاگ فائلوں کے ناموں کے ساتھ تاریخ/وقت کی معلومات منسلک کرسکتے ہیں. دستیاب وقت کی شکل کے پلیس ہولڈرز <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="ltr">time_format⬅general</code></a> پر دکھائے جاتے ہیں.

##### <div dir="rtl">"outbound_request_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>کسی بھی آؤٹ باؤنڈ درخواستوں کے نتائج کو لاگ ان کرنے کے لیے ایک فائل. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li></ul></div>

مفید مشورہ: آپ ٹائم فارمیٹ پلیس ہولڈرز کا استعمال کرکے لاگ فائلوں کے ناموں کے ساتھ تاریخ/وقت کی معلومات منسلک کرسکتے ہیں. دستیاب وقت کی شکل کے پلیس ہولڈرز <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="ltr">time_format⬅general</code></a> پر دکھائے جاتے ہیں.

##### <div dir="rtl">"report_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>بیرونی API کو بھیجی گئی کسی بھی رپورٹ کو لاگ ان کرنے کے لیے ایک فائل. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li></ul></div>

مفید مشورہ: آپ ٹائم فارمیٹ پلیس ہولڈرز کا استعمال کرکے لاگ فائلوں کے ناموں کے ساتھ تاریخ/وقت کی معلومات منسلک کرسکتے ہیں. دستیاب وقت کی شکل کے پلیس ہولڈرز <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="ltr">time_format⬅general</code></a> پر دکھائے جاتے ہیں.

##### <div dir="rtl">"truncate" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>وہ ایک خاص سائز تک پہنچنے میں جب صاف لاگ مسلیں؟ ویلیو میں B/KB/MB/GB/TB زیادہ سے زیادہ سائز ہے. جب 0KB، وہ غیر معینہ مدت تک ترقی کر سکتا ہے (پہلے سے طے). نوٹ: واحد فائلوں پر لاگو ہوتا ہے! فائلیں اجتماعی غور نہیں کر رہے ہیں.</li></ul></div>

##### <div dir="rtl">"log_rotation_limit" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>لاگ گرد گردش کسی بھی وقت کسی بھی وقت موجود ہونا لاگ ان کی تعداد محدود کرتا ہے. جب نیا لاگ ان کی تخلیق کی جاتی ہے تو، اگر لاگ ان کی کل تعداد مخصوص حد سے زیادہ ہوتی ہے تو مخصوص کارروائی کی جائے گی. آپ یہاں مطلوبہ حد کی وضاحت کرسکتے ہیں. 0 کی قیمت لاگ گرد گردش کو غیر فعال کرے گی.</li></ul></div>

##### <div dir="rtl">"log_rotation_action" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>لاگ گرد گردش کسی بھی وقت کسی بھی وقت موجود ہونا لاگ ان کی تعداد محدود کرتا ہے. جب نیا لاگ ان کی تخلیق کی جاتی ہے تو، اگر لاگ ان کی کل تعداد مخصوص حد سے زیادہ ہوتی ہے تو مخصوص کارروائی کی جائے گی. آپ یہاں مطلوبہ کارروائی کی وضاحت کرسکتے ہیں.</li></ul></div>

```
log_rotation_action
├─Delete ("قدیم ترین لاگ ان کو حذف کریں، جب تک کہ حد تک زیادہ نہیں ہوسکتی ہے.")
└─Archive ("سب سے پہلے آرکائیو، اور پھر سب سے پرانی لاگ ان کو حذف کریں، جب تک کہ حد زیادہ نہیں ہوسکتی.")
```

##### <div dir="rtl">"log_banned_ips" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>لاگ فائلوں پر پابندی لگا دی گئی IP پتوں سے مسدود درخواستیں شامل کریں؟ True (سچے) = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = نہیں.</li></ul></div>

##### <div dir="rtl">"log_sanitisation" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>لاگز ڈیٹا دیکھنے کے لیے سامنے کے آخر لاگز صفحے کے کا استعمال کرتے وقت کب، XSS حملوں سے صارفین کی حفاظت کے لیے، یہ نمائش سے پہلے نظر ثانی شدہ ہے. لیکن، ہم ایسا نہیں کرتے جب سب سے پہلے اسے ریکارڈ کرنا پڑتا ہے. اگر یہ مستقبل میں اس کا تجزیہ کرنے کی ضرورت ہے تو اس سے مدد مل سکتی ہے. لیکن خارجہ قارئین کا استعمال کرتے وقت یہ کبھی کبھی غیر محفوظ ہوسکتا ہے. اگر ضرورت ہو تو آپ رویے کو تبدیل کرسکتے ہیں. True (سچے) = کم درست، لیکن کم خطرہ. False (جھوٹی) = زیادہ درست، لیکن زیادہ خطرہ [پہلے سے طے شدہ].</li></ul></div>

#### <div dir="rtl">"frontend" (قسم)<br /></div>
<div dir="rtl">فرنٹ اینڈ کے لیے کنفیگریشن.<br /><br /></div>

##### <div dir="rtl">"frontend_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>سامنے کے آخر میں لاگ ان کوششوں لاگنگ کے لیے دائر. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li></ul></div>

مفید مشورہ: آپ ٹائم فارمیٹ پلیس ہولڈرز کا استعمال کرکے لاگ فائلوں کے ناموں کے ساتھ تاریخ/وقت کی معلومات منسلک کرسکتے ہیں. دستیاب وقت کی شکل کے پلیس ہولڈرز <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="ltr">time_format⬅general</code></a> پر دکھائے جاتے ہیں.

##### <div dir="rtl">"signatures_update_event_log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>جب دستخطوں کو اپ ڈیٹ پیج کے ذریعہ اپ ڈیٹ کیا جاتا ہے تو ریکارڈ کرنے کے لیے ایک فائل. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li></ul></div>

مفید مشورہ: آپ ٹائم فارمیٹ پلیس ہولڈرز کا استعمال کرکے لاگ فائلوں کے ناموں کے ساتھ تاریخ/وقت کی معلومات منسلک کرسکتے ہیں. دستیاب وقت کی شکل کے پلیس ہولڈرز <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="ltr">time_format⬅general</code></a> پر دکھائے جاتے ہیں.

##### <div dir="rtl">"max_login_attempts" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>لاگ ان کوششوں کی زیادہ سے زیادہ تعداد (سامنے کے آخر میں). پہلے سے طے شدہ = 5.</li></ul></div>

##### <div dir="rtl">"theme" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>فرنٹ اینڈ کے لیے استعمال کرنے والی تھیم.</li></ul></div>

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
└─…دیگر
```

##### <div dir="rtl">"theme_mode" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>فرنٹ اینڈ کے لیے استعمال کرنے والی تھیم کے لیے موڈ.</li></ul></div>

```
theme_mode
├─normal ("نارمل")
└─inverted ("الٹا")
```

##### <div dir="rtl">"magnification" <code dir="ltr">[float]</code><br /></div>
<div dir="rtl"><ul><li>فونٹ اضافہ. پہلے سے طے شدہ = 1.</li></ul></div>

##### <div dir="rtl">"custom_header" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تمام فرنٹ اینڈ پیجز کے شروع میں HTML کے بطور داخل کیا گیا. اگر آپ ویب سائٹ کا لوگو، پرسنلائزڈ ہیڈر، اسکرپٹس، وغیرہ شامل کرنا چاہتے ہیں، تو یہ مفید ہو سکتا ہے.</li></ul></div>

##### <div dir="rtl">"custom_footer" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تمام فرنٹ اینڈ پیجز کے آخر میں HTML کے بطور داخل کیا گیا. اگر آپ قانونی نوٹس، رابطہ لنک، کاروباری معلومات، وغیرہ شامل کرنا چاہتے ہیں، تو یہ مفید ہو سکتا ہے.</li></ul></div>

##### <div dir="rtl">"remotes" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اجزاء کے میٹا ڈیٹا کو حاصل کرنے کے لیے اپڈیٹر کے ذریعے استعمال کیے گئے پتوں کی فہرست. نئے بڑے ورژن میں اپ گریڈ کرتے وقت، یا اپ ڈیٹس کے لیے نیا ذریعہ حاصل کرتے وقت اسے ایڈجسٹ کرنے کی ضرورت پڑ سکتی ہے، لیکن عام حالات میں اسے تنہا چھوڑ دیا جانا چاہیے.</li></ul></div>

##### <div dir="rtl">"enable_two_factor" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>یہ تعین کرتا ہے کہ 2FA استعمال کیا جانا چاہیے.</li></ul></div>

#### <div dir="rtl">"signatures" (قسم)<br /></div>
<div dir="rtl">دستخطوں، دستخط فائلوں، ماڈیولز، وغیرہ کے لیے تشکیل.<br /><br /></div>

##### <div dir="rtl">"shorthand" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>یہ کنٹرول کرتا ہے کہ جب کسی دستخط کے خلاف مثبت مماثلت ہو جس میں دیے گئے شارٹ ہینڈ الفاظ کا استعمال ہوتا ہے تو درخواست کے ساتھ کیا کرنا ہے.</li></ul></div>

```
shorthand───[اسے بلاک کریں.]─[اسے پروفائل کریں.]─[بلاک ہونے پر، آؤٹ پٹ ٹیمپلیٹ کا استعمال نہ کریں.]
├─Attacks ("حملے")
├─Bogon ("⁰ Bogon IP")
├─Cloud ("کلاؤڈ سروس")
├─Generic ("جنرک")
├─Legal ("¹ قانونی")
├─Malware ("میلویئر")
├─Proxy ("² پراکسی")
├─Spam ("سپیم")
├─Banned ("³ پابندی")
├─BadIP ("³ غلط IP")
├─RL ("³ ریٹ محدود")
├─Conflict ("³ تنازع")
└─Other ("⁴ دیگر")
```

__0.__ اگر آپ کی ویب سائٹ کو LAN یا localhost کے ذریعے رسائی کی ضرورت ہے، اسے مسدود نہ کریں. اگر ضرورت نہ ہو تو آپ اسے بلاک کر سکتے ہیں.

__1.__ معیاری دستخطی فائلیں اسے استعمال نہیں کرتی ہیں، لیکن یہ اس صورت میں تعاون یافتہ ہے کہ یہ کچھ صارفین کے لیے کارآمد ہو سکتا ہے.

__2.__ اگر آپ کے صارفین کو پراکسی کے ذریعے آپ کی ویب سائٹ تک رسائی حاصل کرنے کی ضرورت ہے، اسے مسدود نہ کریں. اگر ضرورت نہ ہو تو آپ اسے بلاک کر سکتے ہیں.

__3.__ دستخطوں کے اندر براہ راست استعمال کی حمایت نہیں کی جاتی ہے، لیکن خاص حالات میں اسے دوسرے ذرائع سے استعمال کیا جا سکتا ہے.

__4.__ ایسے معاملات کا حوالہ دیتے ہیں جہاں شارٹ ہینڈ الفاظ بالکل استعمال نہیں ہوتے ہیں، یا CIDRAM کے ذریعہ پہچانے نہیں جاتے ہیں.

__ایک فی دستخط.__ ایک دستخط متعدد پروفائلز کی درخواست کر سکتا ہے، لیکن صرف ایک مختصر لفظ استعمال کر سکتا ہے. یہ ممکن ہے کہ ایک سے زیادہ شارٹ ہینڈ الفاظ موزوں ہوں، لیکن چونکہ صرف ایک ہی استعمال کیا جا سکتا ہے، ہم کوشش کرتے ہیں کہ ہمیشہ صرف سب سے موزوں الفاظ استعمال کریں.

__ترجیح.__ ایک منتخب کردہ آپشن ہمیشہ غیر منتخب کردہ آپشن پر ترجیح لیتا ہے. مثال کے طور پر، اگر ایک سے زیادہ شارٹ ہینڈ الفاظ چل رہے ہیں لیکن ان میں سے صرف ایک کو بلاک کیے جانے کے طور پر سیٹ کیا گیا ہے، تب بھی درخواست کو بلاک کر دیا جائے گا.

__ہیومن اینڈ پوائنٹس اور کلاؤڈ سروسز.__ "کلاؤڈ سروس" ویب ہوسٹنگ فراہم کنندگان، سرور فارمز، ڈیٹا سینٹرز، یا بہت سی دوسری چیزوں کا حوالہ دے سکتی ہے. "ہیومن اینڈ پوائنٹ" سے مراد وہ ذرائع ہیں جن کے ذریعے انسان انٹرنیٹ تک رسائی حاصل کرتا ہے، جیسے کہ انٹرنیٹ سروس فراہم کرنے والے کے ذریعے. نیٹ ورک عام طور پر صرف ایک یا دوسرا فراہم کرتا ہے، لیکن بعض اوقات دونوں فراہم کر سکتا ہے. ہم کوشش کرتے ہیں کہ کبھی بھی ممکنہ انسانی اینڈ پوائنٹ کو کلاؤڈ سروسز کے طور پر شناخت نہ کریں. لہذا، ایک کلاؤڈ سروس کی شناخت کسی اور چیز کے طور پر کی جا سکتی ہے اگر اس کی حد معلوم انسانی اختتامی نقطوں کے ذریعے مشترکہ ہو. اسی طرح، جب کسی بھی معلوم انسانی اینڈ پوائنٹس کے ذریعے رینجز کا اشتراک نہیں کیا جاتا ہے، تو ہم ہمیشہ کلاؤڈ سروسز کے بطور کلاؤڈ سروسز کی شناخت کرنے کی کوشش کرتے ہیں. لہذا، کلاؤڈ سروس کے طور پر شناخت کی گئی درخواست شاید معلوم انسانی اختتامی مقامات کے ساتھ حدود کا اشتراک نہیں کرتی ہے. حملوں یا سپیم کے خطرے سے شناخت شدہ درخواستوں کا معاملہ اس کے برعکس ہے. تاہم، انٹرنیٹ ہمیشہ بہاؤ میں رہتا ہے، نیٹ ورکس کے مقاصد وقت کے ساتھ بدلتے رہتے ہیں، اور رینجز ہمیشہ خریدی یا فروخت ہوتی رہتی ہیں، لہذا غلط مثبتات کے حوالے سے چوکس رہیں.

##### <div dir="rtl">"default_tracktime" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>وہ دورانیہ جس کے لیے IP پتوں کو ٹریک کیا جانا چاہیے. پہلے سے طے شدہ = 7d0°0′0″ (1 ہفتہ).</li></ul></div>

##### <div dir="rtl">"infraction_limit" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>خلاف ورزی کی زیادہ سے زیادہ تعداد ایک IP اس سے پہلے کیا جاتا ہے IP باخبر رہنے کے کی طرف سے پابندی کا اطلاق کرنے کی اجازت ہے. پہلے سے طے شدہ = 10.</li></ul></div>

##### <div dir="rtl">"tracking_override" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>ماڈیولوں کو ٹریکنگ کے اختیارات کو اوور رائڈ کرنے کی اجازت دیں؟ True (سچے) = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = نہیں.</li></ul></div>

##### <div dir="rtl">"conflict_response" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>جب ایک ہی وسائل تک رسائی کے لیے بیک وقت بہت ساری کوششیں ہوتی ہیں (مثال کے طور پر، ایک ہی مشین پر ایک ہی وسائل کے لیے متعدد پی ایچ پی پروسیسز کے لیے بیک وقت درخواستیں)، ان میں سے کچھ کوششیں ناکام ہو سکتی ہیں. نایاب اور غیر امکانی صورت میں کہ یہ دستخطی فائلوں یا ماڈیولز کو متاثر کرتا ہے، CIDRAM کو درخواست کے بارے میں موثر فیصلہ کرنے سے روکا جا سکتا ہے. اگر ایسا ہوتا ہے، کیا درخواست کو بلاک کر دینا چاہیے، اور CIDRAM کو کون سا HTTP حیثیت کا پیغام بھیجنا چاہیے؟</li></ul></div>

```
conflict_response
├─0 (درخواست کو مسدود نہ کریں.): اگر آپ ترجیح دیتے ہیں کہ درخواستوں کو صرف
│ اس صورت میں مسدود کیا جائے جب آپ کو یقین ہو
│ کہ وہ خراب ہیں، یا غلط مثبتات کے سلسلے میں
│ محتاط رہنے کے لیے (کبھی کبھار غیر مطلوبہ
│ ٹریفک کے گزرنے کے خطرے میں)، یہ منتخب کریں.
│ اگر آپ ترجیح دیتے ہیں کہ درخواستوں کو
│ مسدود کر دیا جائے اگر آپ کو یقین نہیں ہے کہ
│ وہ بے نظیر ہیں، یا چوکس رہنے کے لیے (کبھی
│ کبھار جھوٹے مثبت ہونے کے خطرے میں)، دوسرے
│ دستیاب اختیارات میں سے ایک کا انتخاب کریں.
├─409 (409 Conflict (تنازع)): وسائل کے تنازعات کے لیے تجویز کردہ (مثلاً،
│ ضم تنازعات، فائل تک رسائی کے تنازعات،
│ وغیرہ). دوسرے سیاق و سباق میں سفارش نہیں کی
│ جاتی ہے.
└─429 (429 Too Many Requests (بہت ساری درخواستیں)): شرح کو محدود کرنے، DDoS حملوں سے نمٹنے، اور
  سیلاب سے بچاؤ کے لیے تجویز کردہ. دوسرے
  سیاق و سباق میں سفارش نہیں کی جاتی ہے.
```

#### <div dir="rtl">"verification" (قسم)<br /></div>
<div dir="rtl">اس بات کی تصدیق کے لیے کنفیگریشن کہ درخواستیں کہاں سے آتی ہیں.<br /><br /></div>

##### <div dir="rtl">"search_engines" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>سرچ انجنوں سے درخواستوں کی تصدیق کے لیے کنٹرولز.</li></ul></div>

```
search_engines───[تصدیق کرنے کی کوشش کریں؟]─[منفی کو مسدود کریں؟]─[غیر تصدیق شدہ درخواستوں کو مسدود کریں؟]─[سنگل ہٹ بائی پاسز کی اجازت دیں؟]─[مثبت سے باخبر رہنا بند کرو؟]
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

__"مثبت" اور "منفی" کیا ہیں؟__ درخواست کے ذریعے پیش کردہ شناخت کی تصدیق کرتے وقت، ایک کامیاب نتیجہ کو "مثبت" یا "منفی" کے طور پر بیان کیا جا سکتا ہے. جب پیش کی گئی شناخت کے حقیقی شناخت ہونے کی تصدیق ہو جاتی ہے، تو اسے "مثبت" کے طور پر بیان کیا جائے گا. جب پیش کردہ شناخت کے جھوٹے ہونے کی تصدیق ہو جاتی ہے، تو اسے "منفی" کے طور پر بیان کیا جائے گا. تاہم، ایک ناکام نتیجہ (مثال کے طور پر، تصدیق ناکام ہو جاتی ہے، یا پیش کردہ شناخت کی سچائی کا تعین نہیں کیا جا سکتا) کو "مثبت" یا "منفی" کے طور پر بیان نہیں کیا جائے گا. اس کے بجائے، ایک ناکام نتیجہ کو محض غیر تصدیق شدہ کے طور پر بیان کیا جائے گا. جب درخواست کے ذریعہ پیش کردہ شناخت کی تصدیق کرنے کی کوئی کوشش نہیں کی جاتی ہے، تو درخواست کو بھی غیر تصدیق شدہ کے طور پر بیان کیا جائے گا. شرائط صرف اس تناظر میں معنی رکھتی ہیں جہاں درخواست کے ذریعہ پیش کردہ شناخت کو تسلیم کیا جاتا ہے، اور اس وجہ سے، جہاں تصدیق ممکن ہے. اگر پیش کردہ شناخت اوپر فراہم کردہ اختیارات سے مماثل نہیں ہے، یا اگر کوئی شناخت پیش نہیں کی گئی ہے، تو اوپر فراہم کردہ اختیارات غیر متعلقہ ہو جاتے ہیں.

__"سنگل ہٹ بائی پاس" کیا ہیں؟__ کچھ معاملات میں، ایک مثبت تصدیق شدہ درخواست اب بھی دستخط فائلوں، ماڈیولز، یا دیگر عوامل کے نتیجے میں مسدود ہو سکتی ہے، اور غلط مثبت سے بچنے کے لیے بائی پاس ضروری ہو سکتے ہیں. جب ایک بائی پاس کا مقصد بالکل ایک خلاف ورزی سے نمٹنا ہوتا ہے، تو ایسے بائی پاس کو "سنگل ہٹ بائی پاس" کے طور پر بیان کیا جا سکتا ہے.

* اس اختیار میں <strong><code dir="ltr">used⬅bypasses</code></strong> کے تحت اسی طرح کا بائی پاس ہ. چاہے اس اختیار کی تصدیق کرنے کی کوشش کے لیے چیک باکس منتخب کیا گیا ہو، کی سفارش کی جاتی ہے اس بات کو یقینی بنانے کہ متعلقہ بائی پاس کا چیک باکس ایک جیسا ہو.

##### <div dir="rtl">"social_media" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>سوشل میڈیا پلیٹ فارمز سے درخواستوں کی تصدیق کے لیے کنٹرولز.</li></ul></div>

```
social_media───[تصدیق کرنے کی کوشش کریں؟]─[منفی کو مسدود کریں؟]─[غیر تصدیق شدہ درخواستوں کو مسدود کریں؟]─[سنگل ہٹ بائی پاسز کی اجازت دیں؟]─[مثبت سے باخبر رہنا بند کرو؟]
├─Embedly ("* Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("* Pinterest")
├─Snapchat ("* Snapchat")
└─Twitterbot ("*!! Twitterbot")
```

__"مثبت" اور "منفی" کیا ہیں؟__ درخواست کے ذریعے پیش کردہ شناخت کی تصدیق کرتے وقت، ایک کامیاب نتیجہ کو "مثبت" یا "منفی" کے طور پر بیان کیا جا سکتا ہے. جب پیش کی گئی شناخت کے حقیقی شناخت ہونے کی تصدیق ہو جاتی ہے، تو اسے "مثبت" کے طور پر بیان کیا جائے گا. جب پیش کردہ شناخت کے جھوٹے ہونے کی تصدیق ہو جاتی ہے، تو اسے "منفی" کے طور پر بیان کیا جائے گا. تاہم، ایک ناکام نتیجہ (مثال کے طور پر، تصدیق ناکام ہو جاتی ہے، یا پیش کردہ شناخت کی سچائی کا تعین نہیں کیا جا سکتا) کو "مثبت" یا "منفی" کے طور پر بیان نہیں کیا جائے گا. اس کے بجائے، ایک ناکام نتیجہ کو محض غیر تصدیق شدہ کے طور پر بیان کیا جائے گا. جب درخواست کے ذریعہ پیش کردہ شناخت کی تصدیق کرنے کی کوئی کوشش نہیں کی جاتی ہے، تو درخواست کو بھی غیر تصدیق شدہ کے طور پر بیان کیا جائے گا. شرائط صرف اس تناظر میں معنی رکھتی ہیں جہاں درخواست کے ذریعہ پیش کردہ شناخت کو تسلیم کیا جاتا ہے، اور اس وجہ سے، جہاں تصدیق ممکن ہے. اگر پیش کردہ شناخت اوپر فراہم کردہ اختیارات سے مماثل نہیں ہے، یا اگر کوئی شناخت پیش نہیں کی گئی ہے، تو اوپر فراہم کردہ اختیارات غیر متعلقہ ہو جاتے ہیں.

__"سنگل ہٹ بائی پاس" کیا ہیں؟__ کچھ معاملات میں، ایک مثبت تصدیق شدہ درخواست اب بھی دستخط فائلوں، ماڈیولز، یا دیگر عوامل کے نتیجے میں مسدود ہو سکتی ہے، اور غلط مثبت سے بچنے کے لیے بائی پاس ضروری ہو سکتے ہیں. جب ایک بائی پاس کا مقصد بالکل ایک خلاف ورزی سے نمٹنا ہوتا ہے، تو ایسے بائی پاس کو "سنگل ہٹ بائی پاس" کے طور پر بیان کیا جا سکتا ہے.

* اس اختیار میں <strong><code dir="ltr">used⬅bypasses</code></strong> کے تحت اسی طرح کا بائی پاس ہ. چاہے اس اختیار کی تصدیق کرنے کی کوشش کے لیے چیک باکس منتخب کیا گیا ہو، کی سفارش کی جاتی ہے اس بات کو یقینی بنانے کہ متعلقہ بائی پاس کا چیک باکس ایک جیسا ہو.

** ASN تلاش کی فعالیت کی ضرورت ہے (مثال کے طور پر، IP-API یا BGPView ماڈیول کے ذریعے).

*!! iMessage کی وجہ سے جھوٹے مثبت ہونے کا زیادہ امکان.

##### <div dir="rtl">"other" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>جہاں ممکن ہو دوسری قسم کی درخواستوں کی تصدیق کے لیے کنٹرولز.</li></ul></div>

```
other───[تصدیق کرنے کی کوشش کریں؟]─[منفی کو مسدود کریں؟]─[غیر تصدیق شدہ درخواستوں کو مسدود کریں؟]─[سنگل ہٹ بائی پاسز کی اجازت دیں؟]─[مثبت سے باخبر رہنا بند کرو؟]
├─AdSense ("AdSense")
├─AmazonAdBot ("* AmazonAdBot")
├─ChatGPT-User ("!! ChatGPT-User")
└─GPTBot ("!! GPTBot")
```

__"مثبت" اور "منفی" کیا ہیں؟__ درخواست کے ذریعے پیش کردہ شناخت کی تصدیق کرتے وقت، ایک کامیاب نتیجہ کو "مثبت" یا "منفی" کے طور پر بیان کیا جا سکتا ہے. جب پیش کی گئی شناخت کے حقیقی شناخت ہونے کی تصدیق ہو جاتی ہے، تو اسے "مثبت" کے طور پر بیان کیا جائے گا. جب پیش کردہ شناخت کے جھوٹے ہونے کی تصدیق ہو جاتی ہے، تو اسے "منفی" کے طور پر بیان کیا جائے گا. تاہم، ایک ناکام نتیجہ (مثال کے طور پر، تصدیق ناکام ہو جاتی ہے، یا پیش کردہ شناخت کی سچائی کا تعین نہیں کیا جا سکتا) کو "مثبت" یا "منفی" کے طور پر بیان نہیں کیا جائے گا. اس کے بجائے، ایک ناکام نتیجہ کو محض غیر تصدیق شدہ کے طور پر بیان کیا جائے گا. جب درخواست کے ذریعہ پیش کردہ شناخت کی تصدیق کرنے کی کوئی کوشش نہیں کی جاتی ہے، تو درخواست کو بھی غیر تصدیق شدہ کے طور پر بیان کیا جائے گا. شرائط صرف اس تناظر میں معنی رکھتی ہیں جہاں درخواست کے ذریعہ پیش کردہ شناخت کو تسلیم کیا جاتا ہے، اور اس وجہ سے، جہاں تصدیق ممکن ہے. اگر پیش کردہ شناخت اوپر فراہم کردہ اختیارات سے مماثل نہیں ہے، یا اگر کوئی شناخت پیش نہیں کی گئی ہے، تو اوپر فراہم کردہ اختیارات غیر متعلقہ ہو جاتے ہیں.

__"سنگل ہٹ بائی پاس" کیا ہیں؟__ کچھ معاملات میں، ایک مثبت تصدیق شدہ درخواست اب بھی دستخط فائلوں، ماڈیولز، یا دیگر عوامل کے نتیجے میں مسدود ہو سکتی ہے، اور غلط مثبت سے بچنے کے لیے بائی پاس ضروری ہو سکتے ہیں. جب ایک بائی پاس کا مقصد بالکل ایک خلاف ورزی سے نمٹنا ہوتا ہے، تو ایسے بائی پاس کو "سنگل ہٹ بائی پاس" کے طور پر بیان کیا جا سکتا ہے.

* اس اختیار میں <strong><code dir="ltr">used⬅bypasses</code></strong> کے تحت اسی طرح کا بائی پاس ہ. چاہے اس اختیار کی تصدیق کرنے کی کوشش کے لیے چیک باکس منتخب کیا گیا ہو، کی سفارش کی جاتی ہے اس بات کو یقینی بنانے کہ متعلقہ بائی پاس کا چیک باکس ایک جیسا ہو.

!! اصلی یا جعلی، کسی بھی طرح سے، زیادہ تر صارفین اس کو بلاک کرنا چاہیں گے. یہ "تصدیق کرنے کی کوشش کریں" کو منتخب نہ کرنے اور "غیر تصدیق شدہ درخواستوں کو مسدود کریں" کو منتخب کرکے حاصل کیا جاسکتا ہے. تاہم، کچھ صارفین ایسی درخواستوں کی تصدیق کرنے کے قابل ہو سکتے ہیں (مثبت کو اجازت دیتے ہوئے منفی کو روکنے کے لیے)، اس لیے ماڈیولز کے ذریعے ایسی درخواستوں کو بلاک کرنے کے بجائے، ایسی درخواستوں کو سنبھالنے کے اختیارات یہاں فراہم کیے گئے ہیں.

##### <div dir="rtl">"adjust" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تصدیق کے تناظر میں دیگر خصوصیات کو ایڈجسٹ کرنے کے کنٹرولز.</li></ul></div>

```
adjust───[HCaptcha کا استعمال نہ کریں]─[Friendly Captcha کا استعمال نہ کریں]─[Cloudflare Turnstile کا استعمال نہ کریں]
├─Negatives ("بلاک شدہ منفی")
└─NonVerified ("بلاک شدہ غیر تصدیق شدہ")
```

#### <div dir="rtl">"captcha" (قسم)<br /></div>
<div dir="rtl">CAPTCHA کی کنفگریشنات (بلاک ہونے پر انسانوں کو دوبارہ رسائی حاصل کرنے کا ایک راستہ فراہم کرتا ہے).<br /><br /></div>

##### <div dir="rtl">"usemode" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>CAPTCHA کب پیش کیے جائیں؟ آپ یہاں ہر معاون فراہم کنندہ کے لیے ترجیحی سلوک کی وضاحت کر سکتے ہیں. نوٹ: وائٹ لسٹڈ یا توثیق شدہ اور غیر مسدود درخواستوں کو کبھی بھی CAPTCHA کو مکمل کرنے کی ضرورت نہیں ہے. یہ بھی نوٹ کریں: CAPTCHA بوٹس اور مختلف قسم کی بدنیتی پر مبنی خودکار درخواستوں کے خلاف مفید تحفظ فراہم کر سکتے ہیں، لیکن بدنیتی پر مبنی انسان کے خلاف کوئی تحفظ فراہم نہیں کریں گے.</li></ul></div>

```
usemode───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─0 (کبھی نہیں.)
├─1 (صرف اس صورت میں جب بلاک ہوجائے، دستخطوں کی حد میں ہو، اور پابندی عائد نہ ہو.)
├─2 (صرف اس صورت میں جب بلاک ہو، استعمال کے لیے خصوصی طور پر نشان زد، دستخطوں کی حد میں ہو، اور پابندی نہیں ہو.)
├─3 (صرف اس وقت جب دستخطوں کی حد میں ہو، اور پابندی عائد نہ ہو (کوئی بات نہیں بلاک ہو یا نہیں).)
├─4 (صرف اس وقت جب بلاک نہیں کیا جاتا ہے.)
├─5 (صرف اس وقت جب بلاک نہ ہوا ہو، یا جب استعمال کے لیے خاص طور پر نشان زد کیا گیا ہو، دستخطوں کی حد میں ہو، اور پابندی نہ ہو.)
└─6 (صرف اس وقت جب بلاک نہ ہوا ہو، حساس صفحہ کی درخواستوں پر.)
```

##### <div dir="rtl">"nonblocked_status_code" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>غیر مسدود درخواستوں پر CAPTCHA کی نمائش کرتے وقت کون سا حیثیت کا کوڈ استعمال کرنا چاہیے؟</li></ul></div>

```
nonblocked_status_code───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─200 (200 OK (ٹھیک ہے)): کم سے کم مضبوط، لیکن سب سے زیادہ صارف دوست.
│ خودکار درخواستیں غالباً اس جواب کی تشریح
│ کریں گی کہ درخواست کامیاب تھی. غیر مسدود
│ درخواستوں کے لیے تجویز کردہ.
├─403 (403 Forbidden (ممنوعہ)): زیادہ مضبوط، لیکن کم صارف دوست. زیادہ تر
│ عام حالات کے لیے تجویز کردہ.
├─418 (418 I'm a teapot (میں چائے کا برتن)): اپریل فول کے لطیفے کا حوالہ دیتے ہیں (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). کسی بھی
│ کلائنٹ، بوٹ، براؤزر، یا کسی اور طرح سے
│ سمجھنے کا امکان نہیں ہے. تفریح اور سہولت
│ کے لیے فراہم کی گئی ہے، لیکن عام طور پر
│ تجویز نہیں کی جاتی ہے.
├─429 (429 Too Many Requests (بہت ساری درخواستیں)): شرح کو محدود کرنے، DDoS حملوں سے نمٹنے، اور
│ سیلاب سے بچاؤ کے لیے تجویز کردہ. دوسرے
│ سیاق و سباق میں سفارش نہیں کی جاتی ہے.
└─451 (451 Unavailable For Legal Reasons (قانونی وجوہات کی بنا پر دستیاب نہیں ہے)): بنیادی طور پر قانونی وجوہات کی بنا پر
  مسدود کرنے پر تجویز کیا جاتا ہے. دوسرے
  سیاق و سباق میں سفارش نہیں کی جاتی ہے.
```

##### <div dir="rtl">"api" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>کون سا API استعمال کرنے کے لیے؟</li></ul></div>

```
api───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─v0 ("v0")
├─v1 ("v1")
├─Invisible ("v1 (پوشیدہ)")
└─v2 ("v2")
```

##### <div dir="rtl">"messages" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>CAPTCHA کے ساتھ دکھائے جانے والے پیغامات.</li></ul></div>

```
messages───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─cookie_warning ("کوکی انتباہ دکھائیں؟): آپ کے ملک یا ریاست کے رازداری کے قوانین پر
│ منحصر ہے (مثلاً، EU میں GDPR/DSGVO، برازیل میں
│ LGPD وغیرہ)، یہ قانونی طور پر درکار ہو سکتا
│ ہے."
└─api_message ("API کا پیغام دکھائیں؟): CAPTCHA کی تکمیل کے حوالے سے صارف کے لیے
  ہدایات، استعمال کیے گئے API کے لیے موزوں."
```

##### <div dir="rtl">"lockto" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>CAPTCHA کو کس چیز پر لاک کرنا ہے.</li></ul></div>

```
lockto───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─ip ("CAPTCHA کو CAPTCHA مکمل کرنے والے صارف کے IP پتے پر لاک کریں لیکن اصل صارف کے لیے نہیں.): کوکیز کا استعمال صارفین کی شناخت کے لیے
│ نہیں کیا جاتا. جب CAPTCHA کی کامیاب تکمیل کی
│ وجہ سے دوبارہ رسائی حاصل کی جاتی ہے، تو اس
│ کا اطلاق اسی IP ایڈریس سے جڑنے والے ہر فرد
│ پر ہوتا ہے."
├─user ("CAPTCHA مکمل کرنے والے صارف کے لیے CAPTCHA کو لاک کریں لیکن ان کے IP ایڈریس پر نہیں.): کوکیز کا استعمال صارفین کی شناخت کے لیے
│ کیا جاتا ہے. جب CAPTCHA کی کامیاب تکمیل کی وجہ
│ سے دوبارہ رسائی حاصل کی جاتی ہے، تو یہ صرف
│ CAPTCHA کو مکمل کرنے والے صارف پر لاگو ہوتا
│ ہے، اور جب تک ان کی کوکی درست رہے گی،
│ برقرار رہے گی، چاہے ان کا IP پتہ بدل جائے."
└─both ("CAPTCHA مکمل کرنے والے صارف کے ساتھ ساتھ ان کے IP ایڈریس پر CAPTCHA کو لاک کریں.): کوکیز کا استعمال صارفین کی شناخت کے لیے
  کیا جاتا ہے. جب CAPTCHA کی کامیاب تکمیل کی وجہ
  سے دوبارہ رسائی حاصل کی جاتی ہے، تو یہ صرف
  CAPTCHA کو مکمل کرنے والے صارف پر لاگو ہوتا
  ہے، اور اگر اس کا IP پتہ تبدیل ہوتا ہے تو یہ
  برقرار نہیں رہے گا."
```

##### <div dir="rtl">"hcaptcha_sitekey" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اگر آپ CIDRAM کے ساتھ hCaptcha استعمال کرنا چاہتے ہیں، تو آپ کو یہاں ایک قدر درج کرنے کی ضرورت ہوگی. اگر نہیں، تو آپ اسے نظر انداز کر سکتے ہیں.</li></ul></div>

یہ قدر آپ کے CAPTCHA خدمت کے لیے ڈیش بورڈ میں مل سکتی ہے.

<div dir="rtl">بھی دیکھو:<ul dir="rtl">
<li><a dir="ltr" href="https://dashboard.hcaptcha.com/overview">HCaptcha Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"hcaptcha_secret" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اگر آپ CIDRAM کے ساتھ hCaptcha استعمال کرنا چاہتے ہیں، تو آپ کو یہاں ایک قدر درج کرنے کی ضرورت ہوگی. اگر نہیں، تو آپ اسے نظر انداز کر سکتے ہیں.</li></ul></div>

یہ قدر آپ کے CAPTCHA خدمت کے لیے ڈیش بورڈ میں مل سکتی ہے.

<div dir="rtl">بھی دیکھو:<ul dir="rtl">
<li><a dir="ltr" href="https://dashboard.hcaptcha.com/overview">HCaptcha Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"friendly_sitekey" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اگر آپ CIDRAM کے ساتھ Friendly Captcha استعمال کرنا چاہتے ہیں، تو آپ کو یہاں ایک قدر درج کرنے کی ضرورت ہوگی. اگر نہیں، تو آپ اسے نظر انداز کر سکتے ہیں.</li></ul></div>

یہ قدر آپ کے CAPTCHA خدمت کے لیے ڈیش بورڈ میں مل سکتی ہے.

<div dir="rtl">بھی دیکھو:<ul dir="rtl">
<li><a dir="ltr" href="https://app.friendlycaptcha.eu/dashboard">Friendly Captcha Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"friendly_apikey" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اگر آپ CIDRAM کے ساتھ Friendly Captcha استعمال کرنا چاہتے ہیں، تو آپ کو یہاں ایک قدر درج کرنے کی ضرورت ہوگی. اگر نہیں، تو آپ اسے نظر انداز کر سکتے ہیں.</li></ul></div>

یہ قدر آپ کے CAPTCHA خدمت کے لیے ڈیش بورڈ میں مل سکتی ہے.

<div dir="rtl">بھی دیکھو:<ul dir="rtl">
<li><a dir="ltr" href="https://app.friendlycaptcha.eu/dashboard">Friendly Captcha Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"turnstile_sitekey" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اگر آپ CIDRAM کے ساتھ Cloudflare Turnstile استعمال کرنا چاہتے ہیں، تو آپ کو یہاں ایک قدر درج کرنے کی ضرورت ہوگی. اگر نہیں، تو آپ اسے نظر انداز کر سکتے ہیں.</li></ul></div>

یہ قدر آپ کے CAPTCHA خدمت کے لیے ڈیش بورڈ میں مل سکتی ہے.

<div dir="rtl">بھی دیکھو:<ul dir="rtl">
<li><a dir="ltr" href="https://dash.cloudflare.com/">Cloudflare Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"turnstile_secret" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اگر آپ CIDRAM کے ساتھ Cloudflare Turnstile استعمال کرنا چاہتے ہیں، تو آپ کو یہاں ایک قدر درج کرنے کی ضرورت ہوگی. اگر نہیں، تو آپ اسے نظر انداز کر سکتے ہیں.</li></ul></div>

یہ قدر آپ کے CAPTCHA خدمت کے لیے ڈیش بورڈ میں مل سکتی ہے.

<div dir="rtl">بھی دیکھو:<ul dir="rtl">
<li><a dir="ltr" href="https://dash.cloudflare.com/">Cloudflare Dashboard</a></li>
</ul></div>

##### <div dir="rtl">"expiry" <code dir="ltr">[float]</code><br /></div>
<div dir="rtl"><ul><li>گھنٹوں کی تعداد CAPTCHA کے واقعات کو یاد کرنے. پہلے سے طے شدہ = 720 (1 ماہ).</li></ul></div>

##### <div dir="rtl">"signature_limit" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>CAPTCHA پیش کش واپس لینے سے پہلے دستخطوں کی زیادہ سے زیادہ تعداد کی اجازت. پہلے سے طے شدہ = 1.</li></ul></div>

##### <div dir="rtl">"log" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تمام CAPTCHA کے کوششوں لاگ؟ اگر ہاں، تو لاگ فائل کے لیے استعمال کرنے کے لیے نام کی وضاحت کریں. اگر نہیں، تو اس متغیر کو خالی چھوڑ دیں.</li></ul></div>

مفید مشورہ: آپ ٹائم فارمیٹ پلیس ہولڈرز کا استعمال کرکے لاگ فائلوں کے ناموں کے ساتھ تاریخ/وقت کی معلومات منسلک کرسکتے ہیں. دستیاب وقت کی شکل کے پلیس ہولڈرز <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format"><code dir="ltr">time_format⬅general</code></a> پر دکھائے جاتے ہیں.

#### <div dir="rtl">"legal" (قسم)<br /></div>
<div dir="rtl">قانونی تقاضوں کے لیے کنفگریشنات.<br /><br /></div>

##### <div dir="rtl">"pseudonymise_ip_addresses" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>لاگ ان کرتے وقت پی ایس ڈی نامناسب IP پتے؟ True (سچے) = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = نہیں.</li></ul></div>

##### <div dir="rtl">"privacy_policy" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>کسی بھی پیدا کردہ صفحات کے فوٹر میں ظاہر ہونے والی متعلقہ رازداری کی پالیسی کا پتہ. ایک URL کی وضاحت کریں، یا غیر فعال کرنے کے لیے خالی چھوڑ دیں.</li></ul></div>

#### <div dir="rtl">"template_data" (قسم)<br /></div>
<div dir="rtl">ٹیمپلیٹس اور تھیمز کی کنفگریشنات.<br /><br /></div>

##### <div dir="rtl">"theme" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>بلاک ایونٹس اور CAPTCHA کی درخواستوں کے لیے استعمال کرنے والی تھیم.</li></ul></div>

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
└─…دیگر
```

##### <div dir="rtl">"theme_mode" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>بلاک ایونٹس اور CAPTCHA کی درخواستوں کے لیے تھیم کا موڈ.</li></ul></div>

```
theme_mode
├─normal ("نارمل")
└─inverted ("الٹا")
```

##### <div dir="rtl">"magnification" <code dir="ltr">[float]</code><br /></div>
<div dir="rtl"><ul><li>فونٹ اضافہ. پہلے سے طے شدہ = 1.</li></ul></div>

##### <div dir="rtl">"css_url" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>اپنی مرضی کے موضوعات کے لیے سی ایس ایس فائل URL.</li></ul></div>

##### <div dir="rtl">"block_event_title" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>بلاک ایونٹس کے لیے ظاہر کرنے کے لیے صفحہ کا عنوان.</li></ul></div>

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("رسائی مسترد کر دی!")
└─…دیگر
```

##### <div dir="rtl">"captcha_title" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>CAPTCHA کی درخواستوں کے لیے ظاہر کرنے کے لیے صفحہ کا عنوان.</li></ul></div>

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…دیگر
```

##### <div dir="rtl">"custom_header" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تمام "رسائی مسترد کر دی" صفحات کے شروع میں بطور HTML داخل کیا گیا. اگر آپ ویب سائٹ کا لوگو، پرسنلائزڈ ہیڈر، اسکرپٹس، وغیرہ شامل کرنا چاہتے ہیں، تو یہ مفید ہو سکتا ہے.</li></ul></div>

##### <div dir="rtl">"custom_footer" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>تمام "رسائی مسترد کر دی" صفحات کے آخر میں بطور HTML داخل کیا گیا. اگر آپ قانونی نوٹس، رابطہ لنک، کاروباری معلومات، وغیرہ شامل کرنا چاہتے ہیں، تو یہ مفید ہو سکتا ہے.</li></ul></div>

#### <div dir="rtl">"rate_limiting" (قسم)<br /></div>
<div dir="rtl">شرح کو محدود کرنے کی کنفگریشنات (عام استعمال کے لیے سفارش نہیں کی جاتی ہے).

ذہن میں رکھیں جس طرح دیگر تمام CIDRAM خصوصیات کے ساتھ، CIDRAM کی شرح محدود کرنے والی خصوصیت صرف ان صفحات اور وسائل پر لاگو کی جا سکتی ہے جن سے CIDRAM منسلک ہے. اس کا عام طور پر مطلب یہ ہوتا ہے کہ جو وسائل پی ایچ پی نہیں ہیں ان کا احاطہ نہیں کیا جائے گا سوائے اس کے جہاں واضح طور پر منسلک پی ایچ پی وسائل کے ذریعہ پیش کیا جائے. اگر آپ ریٹ محدود کرنے کے لیے سرور ماڈیول، cPanel، یا کوئی دوسرا نیٹ ورک ٹول استعمال کرنے کے قابل ہیں، تو CIDRAM کی شرح محدود کرنے والی خصوصیت کے بجائے اسے استعمال کرنا بہتر ہوگا. یہ بھی ذہن میں رکھیں کہ ایک پرعزم اور پرعزم صارف، ان کا IP ایڈریس کو گھما کر یا کسی ایسے پراکسی یا VPN فراہم کنندہ پر جا کر جس سے CIDRAM ابھی تک واقف نہیں ہے، آسانی سے شرح کو محدود کرنے سے بچا سکتا ہے, اور یہ بات ذہن میں رکھیں کہ شرح کو محدود کرنا حقیقی، حقیقی اختتامی صارفین کے لیے بہت پریشان کن ہو سکتا ہے. یہ بعض اوقات ضروری ہو سکتا ہے، لیکن شاذ و نادر ہی مطلوب ہے.<br /><br /></div>

##### <div dir="rtl">"max_bandwidth" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>بینڈوڈتھ کی زیادہ سے زیادہ رقم کی اجازت کے عرصے میں اجازت دی گئی ہے. جب سے تجاوز کی گئی، مستقبل کی درخواستوں کی ریٹ محدود ہے. جب 0، اس قسم کی محدود استعمال نہیں کی جائے گی. پہلے سے طے شدہ = 0KB.</li></ul></div>

##### <div dir="rtl">"max_requests" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>الاؤنس کی مدت کے اندر اندر زیادہ سے زیادہ درخواستوں کی اجازت دی گئی ہے. جب سے تجاوز کی گئی، مستقبل کی درخواستوں کی ریٹ محدود ہے. جب 0، اس قسم کی محدود استعمال نہیں کی جائے گی. پہلے سے طے شدہ = 0.</li></ul></div>

##### <div dir="rtl">"precision_ipv4" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>IPv4 استعمال کی نگرانی کرتے وقت استعمال کرنے کی صحت سے متعلق. قیمت CIDR بلاک سائز کی عکاسی کرتا ہے. بہترین صحت سے متعلق کے لیے 32 پر مقرر کریں. پہلے سے طے شدہ = 32.</li></ul></div>

##### <div dir="rtl">"precision_ipv6" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>IPv6 استعمال کی نگرانی کرتے وقت استعمال کرنے کی صحت سے متعلق. قیمت CIDR بلاک سائز کی عکاسی کرتا ہے. بہترین صحت سے متعلق کے لیے 128 پر مقرر کریں. پہلے سے طے شدہ = 128.</li></ul></div>

##### <div dir="rtl">"allowance_period" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>استعمال کو ٹریک کرنے کا دورانیہ. پہلے سے طے شدہ = 0°0′0″.</li></ul></div>

##### <div dir="rtl">"exceptions" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>مستثنیات (یعنی، درخواستوں کو جس کی ریٹ محدود نہیں ہونی چاہیے). متعلقہ صرف اس وقت جب شرح کی حد بندی قابل ہو.</li></ul></div>

```
exceptions
├─Whitelisted ("وائٹ لسٹ کی درخواستیں")
├─Verified ("سرچ انجنوں اور سوشل میڈیا سے تصدیق شدہ درخواستیں")
└─FE ("CIDRAM فرنٹ اینڈ سے درخواستیں")
```

##### <div dir="rtl">"segregate" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>کیا مختلف ڈومینز اور میزبانوں کے کوٹوں کو الگ یا شیئر کیا جانا چاہیے؟ True = کوٹے الگ کیے جائیں گے. False = کوٹے شیئر کیے جائیں گے [پہلے سے طے شدہ].</li></ul></div>

#### <div dir="rtl">"supplementary_cache_options" (قسم)<br /></div>
<div dir="rtl">ضمنی کیشے کے اختیارات. نوٹ: ان اقدار کو تبدیل کرنے سے آپ ممکنہ طور پر لاگ آؤٹ ہو سکتے ہیں.<br /><br /></div>

##### <div dir="rtl">"prefix" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>یہاں بیان کردہ قدر کو تمام کیش انٹری کیز کے ساتھ پہلے سے جوڑا جائے گا. پہلے سے طے شدہ = "CIDRAM_". جب ایک ہی سرور پر متعدد تنصیبات موجود ہوں، تو یہ ان کے کیچز کو ایک دوسرے سے الگ رکھنے کے لیے مفید ہو سکتا ہے.</li></ul></div>

##### <div dir="rtl">"enable_apcu" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>اس کی وضاحت کرتا ہے کہ کیش کے لیے APCu استعمال کرنا چاہے. پہلے سے طے شدہ = True (سچ).</li></ul></div>

##### <div dir="rtl">"enable_memcached" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>اس کی وضاحت کرتا ہے کہ کیش کے لیے Memcached استعمال کرنا چاہے. پہلے سے طے شدہ = False (جھوٹی).</li></ul></div>

##### <div dir="rtl">"enable_redis" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>اس کی وضاحت کرتا ہے کہ کیش کے لیے Redis استعمال کرنا چاہے. پہلے سے طے شدہ = False (جھوٹی).</li></ul></div>

##### <div dir="rtl">"enable_pdo" <code dir="ltr">[bool]</code><br /></div>
<div dir="rtl"><ul><li>اس کی وضاحت کرتا ہے کہ کیش کے لیے PDO استعمال کرنا چاہے. پہلے سے طے شدہ = False (جھوٹی).</li></ul></div>

##### <div dir="rtl">"memcached_host" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>Memcached کے میزبان نام. پہلے سے طے شدہ = localhost.</li></ul></div>

##### <div dir="rtl">"memcached_port" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>Memcached کے لیے بندرگاہ. پہلے سے طے شدہ = "11211".</li></ul></div>

##### <div dir="rtl">"redis_host" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>Redis کے میزبان نام. پہلے سے طے شدہ = localhost.</li></ul></div>

##### <div dir="rtl">"redis_port" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>Redis کے لیے بندرگاہ. پہلے سے طے شدہ = "6379".</li></ul></div>

##### <div dir="rtl">"redis_timeout" <code dir="ltr">[float]</code><br /></div>
<div dir="rtl"><ul><li>Redis کے لیے ٹائم آؤٹ. پہلے سے طے شدہ = "2.5".</li></ul></div>

##### <div dir="rtl">"redis_database_number" <code dir="ltr">[int]</code><br /></div>
<div dir="rtl"><ul><li>Redis ڈیٹا بیس نمبر. پہلے سے طے شدہ = 0. نوٹ: Redis Cluster کے ساتھ 0 کے علاوہ دیگر اقدار استعمال نہیں کر سکتے.</li></ul></div>

##### <div dir="rtl">"pdo_dsn" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>PDO کے لیے DSN. پہلے سے طے شدہ = "mysql:dbname=cidram;host=localhost;port=3306".</li></ul></div>

__FAQ.__ <em><a href="https://github.com/CIDRAM/Docs/blob/master/readme.ur.md#user-content-HOW_TO_USE_PDO" hreflang="ur-PK">"PDO DSN" کیا ہے؟ میں CIDRAM کے ساتھ PDO کیسے استعمال کرسکتا ہوں؟</a></em>

##### <div dir="rtl">"pdo_username" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>PDO کے لیے صارف نام.</li></ul></div>

##### <div dir="rtl">"pdo_password" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>PDO کے لیے پاس ورڈ.</li></ul></div>

#### <div dir="rtl">"bypasses" (قسم)<br /></div>
<div dir="rtl">پہلے سے طے شدہ دستخط کو نظرانداز کرنے کے لیے تشکیل.<br /><br /></div>

##### <div dir="rtl">"used" <code dir="ltr">[string]</code><br /></div>
<div dir="rtl"><ul><li>کون سے بائی پاس کو استعمال کیا جانا چاہیے؟</li></ul></div>

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


### <div dir="rtl">۶. <a name="SECTION6"></a>دستخط فارمیٹ</div>

<div dir="rtl">بھی دیکھو:<br /></div>
<div dir="rtl"><ul>
 <li><a href="#user-content-WHAT_IS_A_SIGNATURE">ایک "دستخط" کیا ہے؟</a></li>
</ul></div>

#### <div dir="rtl">۶.۰ مبادیات (دستخط فائلوں کے لیے)<br /><br /></div>

<div dir="rtl">"xxx.xxx.xxx.xxx/yy [فنکشن] [پرم]": تمام IPv4 کی دستخط کی شکل کی پیروی.<br /></div>
<div dir="rtl"><ul>
 <li>"xxx.xxx.xxx.xxx" CIDR بلاک (بلاک میں ابتدائی IP ایڈریس کی آکٹیٹ) کے آغاز کی نمائندگی کرتا ہے.</li>
 <li>"yy" CIDR بلاک سائز [۱-۳۲] نمائندگی کرتا ہے.</li>
 <li>"[فنکشن]" سکرپٹ سگنیچر (دستخط شمار کیا جانا چاہیے کہ کس طرح) کے ساتھ کیا کیا ہدایات.</li>
 <li>"[پرم]" کی نمائندگی کرتا ہے جو کچھ بھی اضافی معلومات "طرف (فنکشن) کی ضرورت ہوسکتی ہے".</li>
</ul></div>

<div dir="rtl"><code dir="ltr">"xxxx:xxxx:xxxx:xxxx::xxxx/yy"</code> [فنکشن] [پرم]" تمام IPv6 کی دستخط کی شکل کی پیروی.<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">"xxxx:xxxx:xxxx:xxxx::xxxx"</code> CIDR بلاک کے آغاز (بلاک میں ابتدائی IP ایڈریس کی آکٹیٹ) نمائندگی کرتا ہے. مکمل سنکیتن اور مختصر سنکیتن دونوں قابل قبول ہیں (اور ہر ایک IPv6 کی سنکیتن کے مناسب اور متعلقہ معیار پر عمل کرنا ضروری ہے، لیکن ایک رعایت کے ساتھ: ایک IPv6 کی ایڈریس مخفف کے ساتھ اس سکرپٹ کے لیے ایک دستخط میں استعمال کرتے ہیں، کی وجہ سے میں جس طرح کرنے کے لیے شروع نہیں کر سکتی <code dir="ltr">"0::1/128"</code> طور مثلا، ایک دستخط میں استعمال کیا جاتا ہے جب <code dir="ltr">"::1/128"</code> کا اظہار کیا جانا چاہیے، اور <code dir="ltr">"0::/128"</code> کے طور پر اظہار، جس CIDR سکرپٹ کی طرف سے دوبارہ تعمیر کر رہے ہیں <code dir="ltr">"::0/128"</code>).</li>
 <li>"yy" CIDR بلاک سائز [1-128] نمائندگی کرتا ہے.</li>
 <li>"(فنکشن)" سکرپٹ سگنیچر (دستخط شمار کیا جانا چاہیے کہ کس طرح) کے ساتھ کیا کیا ہدایات.</li>
 <li>"[پرم]" کی نمائندگی کرتا ہے جو کچھ بھی اضافی معلومات "طرف (فنکشن) کی ضرورت ہوسکتی ہے".</li>
</ul></div>

<div dir="rtl">ہ دستخط کے CIDRAM یونیکس طرز نیولائنز (<code dir="ltr">"%0A"</code>، یا <code dir="ltr">"\n"</code>) کا استعمال کرنا چاہیے کے لیے فائلوں! دوسری قسم / نیولائنز کے سٹائل (جیسے ونڈوز <code dir="ltr">"%0D%0A"</code> یا <code dir="ltr">"\r\n"</code> نیولائنز، میک <code dir="ltr">"%0D"</code> یا<code dir="ltr">"\r"</code> نیولائنز، وغیرہ) استعمال کیا جا سکتا ہے، لیکن ترجیح نہیں ہیں. غیر یونیکس طرز نیولائنز سکرپٹ طرف یونیکس طرز نیولائنز کو معمول کی جائے گی.<br /><br /></div>

<div dir="rtl">عین مطابق اور درست CIDR سنکیتن کی ضرورت ہے، دوسری صورت سکرپٹ دستخط کو تسلیم نہیں کریں گے. مزید برآں، اس سکرپٹ کی تمام CIDR دستخط ایک IP ایڈریس جن IP نمبر، اس کی CIDR بلاک سائز (مثلا طرف سے نمائندگی آپ <code dir="ltr">"11.127.255.255"</code> کرنا <code dir="ltr">"10.128.0.0"</code> سے تمام IP پتے کو بلاک کرنا چاہتے تھے تو بلاک ڈویژن میں یکساں طور پر تقسیم کر سکتے ہیں کے ساتھ شروع ہونا چاہیے، <code dir="ltr">"10.128.0.0/8"</code> سکرپٹ کی طرف سے تسلیم نہیں کیا جائے گا، لیکن"</code> 10.128.0.0/9"</code> اور <code dir="ltr">"11.0.0.0/9"</code> مل کر میں استعمال کیا جاتا ہے، سکرپٹ کی طرف سے تسلیم کیا جائے گا).<br /><br /></div>

<div dir="rtl">دستخط میں کوئی بھی چیز اس وجہ سے جس کا مطلب آپ کو محفوظ طریقے سے ان کو توڑنے کے بغیر اور اسکرپٹ کو توڑنے کے بغیر آپ کے دستخط فائلوں میں چاہتا ہوں کہ کسی بھی غیر دستخط کے اعداد و شمار کو ڈال کر سکتے ہیں، کو نظر انداز کر دیا جائے گا ایک دستخط کے طور پر اور نہ ہی سکرپٹ کی طرف سے دستخط کے متعلق نحو کے طور پر تسلیم نہیں فائلوں. تبصرے کے دستخط فائلوں میں قابل قبول ہیں، اور کوئی خاص فارمیٹنگ ان کے لیے کی ضرورت ہے. تبصرے کے لیے شیل طرز hashing کے ترجیح دی جاتی ہے، لیکن نافذ نہیں؛ مکمل طور پر قابل، یہ آپ کے تبصرے کے لیے شیل طرز hashing کے استعمال کرنے کا انتخاب کرتے ہیں یا نہیں اسکرپٹ کو کوئی فرق نہیں پڑتا، لیکن شیل طرز hashing کے استعمال کر IDEs کے اور سادہ ٹیکسٹ ایڈیٹرز صحیح دستخط کی فائلوں کے مختلف حصوں کو اجاگر کرنے میں مدد ملتی ہے (اور اس طرح، شیل طرز میں ترمیم کرتے ہوئے hashing کے ایک بصری امداد کے طور پر مدد کر سکتے ہیں).<br /><br /></div>

<div dir="rtl">"(فنکشن)" کی ممکنہ اقدار مندرجہ ذیل ہیں:<br /></div>
<div dir="rtl"><ul>
 <li>Run</li>
 <li>Whitelist</li>
 <li>Greylist</li>
 <li>Deny</li>
</ul></div>

<div dir="rtl">تو "Run" استعمال کیا جاتا ہے، دستخط شروع ہوجاتا ہے جب، سکرپٹ پھانسی کے لیے ایک بیرونی PHP اسکرپٹ، کی طرف سے مخصوص ہے (ایک "require_once" بیان کرتے ہوئے) کی کوشش کریں گے" [پرم] "قدر (کام کر ڈائرکٹری ہونا چاہیے "/vault/" اسکرپٹ کی ڈائریکٹری؛ ذیل کی مثالیں ملاحظہ کریں).<br /><br /></div>

`127.0.0.0/8 Run example.php`

<div dir="rtl">یہ کچھ IP ایڈریس اور CIDR کوڈ کے لیے ایک خاص PHP چلانے کے لیے مفید ہو سکتا ہے.<br /><br /></div>

<div dir="rtl">تو "Whitelist" استعمال کیا جاتا ہے، دستخط شروع ہوجاتا ہے جب اسکرپٹ تمام detections کر (کسی detections کر ہوئی ہے تو) دوبارہ کنفگریشن دے گا اور ٹیسٹ کی تقریب کو توڑنے. "[پرم]" نظر انداز کر دیا جاتا ہے. اس تقریب کا پتہ چلا جا رہا ہے سے ایک مخصوص IP یا CIDR وائٹ لسٹ کے برابر ہے.<br /><br /></div>

`127.0.0.1/32 Whitelist`

<div dir="rtl">تو "Greylist" استعمال کیا جاتا ہے، دستخط شروع ہوجاتا ہے جب اسکرپٹ تمام detections کر (کسی detections کر ہوئی ہے تو) دوبارہ کنفگریشن دے گا اور پروسیسنگ جاری رکھنے کے لیے اگلے کے دستخط کی فائل کو چھوڑ دیں. "[پرم]" نظر انداز کر دیا جاتا ہے.<br /><br /></div>

`127.0.0.1/32 Greylist`

<div dir="rtl">سگنیچر شروع ہوجاتا ہے جب "Deny" استعمال کیا جاتا ہے،، کوئی وائٹ لسٹ کے دستخط سنبھالنے دی IP ایڈریس اور / یا دی CIDR کے لیے متحرک کیا گیا ہے تو، محفوظ صفحے کی رسائی نہیں دی جائے گی. "Deny" کیا آپ واقعی ایک IP ایڈریس اور / یا CIDR رینج کو بلاک کرنے کے لیے استعمال کرنا چاہتے ہیں کریں گے کیا ہے. کوئی بھی دستخط متحرک کر رہے ہیں جب کے استعمال بنانے کے کہ "Deny"، "رسائی نہیں ہوئی" اسکرپٹ کا صفحہ پیدا کیا جائے گا اور ہلاک محفوظ صفحے کی درخواست.<br /><br /></div>

<div dir="rtl">"[پرم]" "Deny" کی طرف سے قبول کی قیمت، "رسائی نہیں ہوئی" کے صفحے کی پیداوار میں پارس کیا جائے گا کی تردید کی جا رہی مطلوبہ صفحہ تک ان کی رسائی کے لیے حوالہ دیا وجہ کے طور پر کلائنٹ / صارف کے لیے فراہم کی. یہ آپ کو ان کے (کچھ بھی، کافی چاہیے یہاں تک کہ ایک سادہ "میں آپ کو اپنی ویب سائٹ پر چاہتے ہیں نہیں ہے")، یا آشلپی الفاظ کی ایک چھوٹی سی مٹھی بھر کے ایک سے فراہم بلاک کرنے کے لیے منتخب کیا ہے یہی وجہ ہے کہ یا تو ایک مختصر اور سادہ قید کی سزا، کی وضاحت ہو سکتا ہے سکرپٹ کی طرف سے استعمال کیا ہے تو کہ میں کیوں کلائنٹ / صارف مسدود کر دیا گیا ہے ایک پہلے سے تیار وضاحت کے ساتھ سکرپٹ کی طرف سے تبدیل کیا جائے گا.<br /><br /></div>

<div dir="rtl">پہلے سے تیار وضاحتوں L10N حمایت حاصل ہے اور زبان آپ کو سکرپٹ کی کنفگریشن کے "lang" ہدایت کرنے کی وضاحت کی بنیاد پر سکرپٹ کی طرف سے فراہم کیا جا سکتا. کے علاوہ، آپ کو نظر انداز کی بنیاد پر دستخط "Deny" کرنا سکرپٹ کو ہدایت کر سکتے ہیں ان کے "[پرم]" قدر سکرپٹ کی کنفگریشن کی طرف سے مخصوص ہدایات کے ذریعے (وہ ان آشلپی الفاظ استعمال کر رہے ہیں) (ہر آشلپی لفظ ایک اسی ہدایت کی ہے یا تو کرنے کے لیے اسی دستخط عملدرآمد یا ان کو نظر انداز کرنے کی). "[پرم]" اقدار، ان آشلپی الفاظ استعمال کرتے ہیں یا نہیں تاہم L10N حمایت کی ضرورت نہیں ہے اور اس وجہ سے سکرپٹ کی طرف سے فراہم نہیں کیا جائے گا، اور اس کے علاوہ، سکرپٹ کی کنفگریشن کی طرف سے براہ راست نینترنیی نہیں ہیں آپ آشلپی الفاظ یہ ہیں:<br /></div>
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

#### <div dir="rtl">۶.۱ ٹیگز<br /><br /></div>

##### <div dir="rtl">۶.۱.۰ سیکشن ٹیگ<br /><br /></div>

<div dir="rtl">آپ کو انفرادی حصوں میں آپ اپنی مرضی کے دستخط کو تقسیم کرنا چاہتے ہیں تو، آپ کو آپ کے دستخط کے سیکشن کے نام کے ساتھ ساتھ فوری طور پر ہر سیکشن کے دستخط کے بعد ایک "سیکشن ٹیگ" انہوں نے مزید کہا کی طرف سے سکرپٹ کے لیے ان کے انفرادی حصوں کی شناخت کر سکتے ہیں (ذیل کی مثال ملاحظہ کریں).<br /><br /></div>

```
# سیکشن 1.
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: سیکشن 1
```

<div dir="rtl">سیکشن ٹیگنگ توڑنے اور یقینی بنانے کے لیے ٹیگز غلط طریقے سے دستخط کی فائلوں میں پہلے سے دستخط کے حصوں کو شناخت نہیں کر رہے ہیں کہ صرف آپ کے ٹیگ اور آپ کے شروع کے دستخط حصوں کے درمیان کم از کم دو مسلسل نیولائنز سے ہیں اس بات کا یقین. کوئی غیر ٹیگ شدہ دستخط "IPv4 کی" یا "IPv6 کی" (دستخط کی اقسام کو متحرک کیا جا رہا ہے جس پر منحصر ہے) خواہ کو فطری گا.<br /><br /></div>

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: سیکشن 1
```

<div dir="rtl">اوپر کی مثال میں<code dir="ltr">"1.2.3.4/32"</code> اور<code dir="ltr">"2.3.4.5/32"</code> "IPv4" کی کے طور پر ٹیگ کیا جائے گا، جبکہ<code dir="ltr">"4.5.6.7/32"</code> اور<code dir="ltr">"5.6.7.8/32"</code> "سیکشن 1" کے طور پر ٹیگ کیا جائے گا.<br /><br /></div>

<div dir="rtl">اسی منطق کو بھی دیگر اقسام کے ٹیگ کو الگ کرنے کے لیے لاگو کیا جا سکتا ہے.<br /><br /></div>

<div dir="rtl">خاص طور پر، سیکشن ٹیگ کو ڈیبگنگ کے لیے بہت مفید ثابت ہوسکتا ہے جب غلط مثبت واقع ہوسکتا ہے، اس مسئلے کا صحیح ذریعہ تلاش کرنے کا آسان ذریعہ فراہم کرنے کے ذریعہ، اور وہ لاگ ان کے لاگ ان صفحے کے ذریعے لاگ فولائل کو دیکھتے وقت لاگ ان کی اندراجات کو فلٹر کرنے کے لیے بہت مفید ہوسکتے ہیں (سیکشن کے نام سامنے کے آخر میں لاگ ان صفحے کے ذریعے کلک کی جا سکتی ہے اور فلٹرنگ کے معیار کے طور پر استعمال کیا جا سکتا ہے). اگر کسی خاص دستخط کے لیے سیکشن ٹیگ کو چھوڑ دیا جاتا ہے تو، جب دستخط کیے جائیں گے تو، CIDRAM کے پاس آئیکریس فائل کا نام استعمال ہوتا ہے جس کے ساتھ IP ایڈریس کو بلاک کر دیا گیا ہے (IPv4 یا IPv6) کے نتیجے میں، اور اس طرح سیکشن ٹیگ مکمل طور پر اختیاری ہیں. بعض صورتوں میں ان کی سفارش کی جاسکتی ہے، مثلا جب دستخط شدہ فائلوں کو نام نہاد نامزد کیا جاسکتا ہے یا جب یہ دوسری صورت میں واضح طور پر دستخط کرنے کے لیے درخواست کی وجہ سے واضح طور پر دستخط کرنا مشکل ہوسکتا ہے.<br /><br /></div>

##### <div dir="rtl">۶.۱.۱ ختم ہونے والی ٹیگ<br /><br /></div>

<div dir="rtl">آپ دستخط سیکشن ٹیگز کو اسی انداز میں، کچھ وقت کے بعد ختم کرنا چاہتے ہیں تو، آپ کو متعین کرنے کی ایک "ختم ہونے ٹیگ" استعمال دستخط درست نہیں رہے چاہیے جب سکتا. ختم ہونے ٹیگز شکل <code dir="ltr">"YYYY.MM.DD"</code> استعمال کرتے ہیں (ذیل کی مثال دیکھیں).<br /><br /></div>

```
# سیکشن 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

<div dir="rtl">متوقع دستخط کسی بھی درخواست پر کبھی نہیں چلائے جائیں گے، کوئی بات نہیں.<br /><br /></div>

##### <div dir="rtl">۶.۱.۲ اصل ٹیگ<br /><br /></div>

<div dir="rtl">اگر آپ کچھ خاص دستخط کے لیے اصل ملک کی وضاحت کرنا چاہتے ہیں، تو آپ "اصل ٹیگ" کا استعمال کرتے ہوئے کر سکتے ہیں. ایک اصل ٹیگ ایک دستخط "<a href="https://ur.wikipedia.org/wiki/%D8%A2%DB%8C%D8%B2%D9%88_3166-1">آیزو 3166-1</a>" کو قبول کرتا ہے جو اس پر دستخط ہونے والے دستخط کے لیے اصل ملک سے ملتا ہے. یہ کوڈ اوپر اوپری میں لکھنا ضروری ہے (کم کیس یا مخلوط کیس صحیح طریقے سے فراہم نہیں کرے گا). جب اصل ٹیگ استعمال کیا جاتا ہے، یہ متعلقہ لاگ بلاک کی درخواستوں کے "کیوں بلاک شدہ" فیلڈ میں شامل کیا جاتا ہے.<br /><br /></div>

<div dir="rtl">اگر اختیاری "flags CSS" جزو نصب کیا جاتا ہے، سامنے کے آخر میں لاگ ان کے صفحے کے ذریعے لاگ ان کو لاگو کرتے وقت، اصل ٹیگ کی معلومات کو اس ملک کی پرچم کی طرف سے بدل دیا گیا ہے جو اس معلومات سے متعلق ہے. یہ معلومات کلک کرنے کے قابل ہے، اور جب پر کلک کیا جاتا ہے تو، ملک کے پرچم کی بنیاد پر لاگ ان اندراجوں کو فلٹر کریں گے.<br /><br /></div>

<div dir="rtl">نوٹ: یہ جغرافیہ نہیں ہے. یہ مخصوص مقام کی معلومات کے لیے تلاش نہیں کرتا، لیکن اس کے بجائے، ہمیں کسی بھی درخواست کے لیے بلاک کرنے کے قابل بناتا ہے. ایک ہی دستخط سیکشن کے اندر ایک سے زیادہ اصل ٹیگ جائز ہیں.<br /><br /></div>

<div dir="rtl">سمپوشی مثال:<br /><br /></div>

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

<div dir="rtl">کسی ٹیگ کے ساتھ مل کر استعمال کیا جا سکتا ہے، اور تمام ٹیگ اختیاری ہیں (ذیل مثال دیکھیں).<br /><br /></div>

```
# Example Section.
1.2.3.4/32 Deny Generic
Origin: US
Tag: Example Section
Expires: 2016.12.31
```

##### <div dir="rtl">۶.۱.۳ دھن ٹیگ<br /><br /></div>

<div dir="rtl">جب بڑی تعداد میں دستخط شدہ فائلوں کو انسٹال کیا جاتا ہے اور فعال طور پر استعمال کیا جاتا ہے تو، تنصیبات بہت پیچیدہ ہوسکتے ہیں، اور کچھ دستخط بھی ہوسکتے ہیں جس پر اووریلپ. ان صورتوں میں، بلاک کے واقعات کے دوران ایک سے زائد، زیادہ اوپریپشن دستخط ہونے کی روک تھام کے لۓ، ڈویژن ٹیگز استعمال ہونے والے مخصوص دستخط کے حصوں کو خارج کرنے کے لیے استعمال کیا جا سکتا ہے، جہاں کچھ مخصوص دستخط فائل نصب ہوجائے اور فعال طور پر استعمال کیا جاتا ہے. اس صورت حال میں مفید ثابت ہوسکتا ہے جہاں کچھ دستخط دوسروں سے کہیں زیادہ اپ ڈیٹ ہوتے ہیں، تاکہ زیادہ کثرت سے اپ ڈیٹ کردہ دستخط زیادہ بار بار اپ ڈیٹ کردہ دستخط کے حق میں ہٹائیں.<br /><br /></div>

<div dir="rtl">حوالہ ٹیگ دیگر اقسام کے ٹیگ کے ساتھ اسی طرح استعمال ہوتے ہیں. ٹیگ کی قدر کو نصب شدہ اور فعال طور پر استعمال ہونے والے دستخط فائل سے منسلک ہونا لازمی ہے.<br /><br /></div>

<div dir="rtl">مثال:<br /><br /></div>

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

#### <div dir="rtl">۶.۱.۴ پروفائل ٹیگ<br /><br /></div>

<div dir="rtl">پروفائل ٹیگز ٹیسٹ پیج پر اضافی معلومات ظاہر کرنے کا ایک ذریعہ فراہم کرتے ہیں، اور زیادہ پیچیدہ سلوک اور بہتر فیصلہ سازی کے لیے استعمال کیا جاسکتا ہے.<br /><br /></div>

<div dir="rtl">دوسرے قسم کے ٹیگز کی طرح ہی پروفائل ٹیگز استعمال ہوتے ہیں. پروفائل ٹیگ کی اقدار کو ماڈیولز اور معاون قواعد کی شرط کے طور پر استعمال کیا جاسکتا ہے. پروفائل ٹیگ ان اقدار کو سیمیکن سے الگ کرکے ایک سے زیادہ اقدار فراہم کرسکتے ہیں. آخری صارف پروفائل ٹیگ کی قدر کبھی نہیں دیکھتا ہے.<br /><br /></div>

<div dir="rtl">مثال:<br /><br /></div>

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### <div dir="rtl">۶.۲ YAML<br /><br /></div>

#### <div dir="rtl">۶.۲.۰ YAML مبادیات<br /><br /></div>

<div dir="rtl">مکمل طور پر اختیاری (یعنی آپ اسے استعمال کرتے ہیں تو آپ کا انتخاب ہے) YAML نشانات استعمال کرتے ہوئے، اور کنفگریشن میں سے اکثر کا فائدہ اٹھانے کے قابل ہے.<br /><br /></div>

<div dir="rtl">CIDRAM میں، تین ڈیشز ("---") کا استعمال کرتے ہوئے تعین کیا YAML جاتا ہے، اور وہ دو نئے لائنوں کا استعمال کرتے ہوئے ختم. مندرجہ ذیل مثال:<br /><br /></div>

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

#### <div dir="rtl">۶.۳ معاون<br /><br /></div>

##### <div dir="rtl">۶.۳.۰ دستخط کے حصوں کو نظر انداز کرنا<br /><br /></div>

<div dir="rtl">کے علاوہ، آپ CIDRAM مکمل طور پر دستخط کی فائلوں میں سے کسی کے اندر کچھ مخصوص حصوں کو نظر انداز کرنا چاہتے ہیں تو، آپ "ignore.dat" فائل ہے جس میں حصوں کو نظر انداز کرنے کی وضاحت کرنے کے لیے استعمال کر سکتے ہیں. ایک نئی لائن پر، لکھنا "Ignore"، ایک کی جگہ کے بعد، آپ کو CIDRAM نظر انداز کرنا (ذیل کی مثال ملاحظہ کریں) چاہتے ہیں کہ سیکشن کے نام کے بعد<br /><br /></div>

```
Ignore سیکشن 1
```

<div dir="rtl">یہ CIDRAM سامنے کے آخر "حصوں کی فہرست" کے صفحے کے ذریعہ بھی حاصل کیا جا سکتا ہے.<br /><br /></div>

##### <div dir="rtl">۶.۳.۱ معاون قوانین<br /><br /></div>

<div dir="rtl">اگر آپ محسوس کرتے ہیں کہ آپ اپنی مرضی کے دستخط شدہ فائلوں کو لکھتے ہیں یا اپنی مرضی کے مطابق ماڈیولز آپ کے لیے بہت پیچیدہ ہیں، ایک آسان متبادل سیڈامیم سامنے کے آخر "معاون قواعد" کے صفحے کا استعمال کرنا ہوسکتا ہے. مناسب اختیارات کا انتخاب کرتے ہوئے اور مخصوص قسم کے درخواستوں کے بارے میں تفصیلات کی وضاحت کرکے، آپ ان ہدایات کو جواب دینے کے بارے میں CIDRAM کو ہدایت کرسکتے ہیں. تمام دستخط شدہ فائلوں کے بعد "معاون قواعد" کو معطل کر دیا جاتا ہے اور ماڈیولز نے پہلے سے ہی عملدرآمد مکمل کر لیا ہے.<br /><br /></div>

#### <div dir="rtl">۶.۴ <a name="MODULE_BASICS"></a>مبادیات (ماڈیولز کے لیے)<br /><br /></div>

<div dir="rtl">ماڈیولز CIDRAM کی فعالیت کو بڑھانے کے لیے استعمال کیا جا سکتا ہے، اضافی کاموں کو انجام دینے کے لیے، یا اضافی منطق پر عمل درآمد.<br /><br /></div>

<div dir="rtl">کیونکہ ماڈیولز PHP کی فائلوں کے طور پر لکھی جاتی ہیں، اگر آپ CIDRAM کوڈ بیس کے ساتھ مناسب طریقے سے واقف ہیں تو، آپ اپنی ماڈیول اور ماڈیول دستخط کی تشکیل کرسکتے ہیں تاہم آپ چاہتے ہیں (PHP کے ساتھ کیا ممکن ہے کی مناسب حدود کے اندر اندر).<br /><br /></div>

<div dir="rtl"><em>نوٹ: اگر آپ PHP کے کوڈ کے ساتھ کام کرنے میں آرام دہ اور پرسکون نہیں ہیں تو، آپ کے اپنے ماڈیول لکھنے کی سفارش نہیں کی جاتی ہے.</em><br /><br /></div>

<div dir="rtl">کچھ فعالیتیں CIDRAM کی طرف سے فراہم کی جاتی ہیں جو اپنے ماڈیولز کو لکھنے کے لیے آسان اور آسان بنانا چاہیے. اس فعالیت کے بارے میں معلومات ذیل میں بیان کی گئی ہے.<br /><br /></div>

#### <div dir="rtl">۶.۵ ماڈیول فعالیت<br /><br /></div>

##### <div dir="rtl">۶.۵.۰ <code dir="ltr">$this->trigger</code></div>

<div dir="rtl">ماڈیول دستخط عام طور پر <code dir="ltr">$this->trigger</code> کے ساتھ لکھا جاتا ہے. زیادہ تر معاملات میں، یہ بندش ماڈیول لکھنے کے مقصد کے لیے کسی اور سے کہیں زیادہ اہم ہو گی.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$this->trigger</code> ۴ پیرامیٹرز کو قبول کرتا ہے: <code dir="ltr">$Condition</code>، <code dir="ltr">$ReasonShort</code>، <code dir="ltr">$ReasonLong</code> (اختیاری)، <code dir="ltr">$DefineOptions</code> (اختیاری).<br /><br /></div>

<div dir="rtl"><code dir="ltr">$Condition</code> سچائی کا اندازہ کیا جاتا ہے. اگر یہ سچ (true) ہے تو، دستخط چالو ہے. اگر یہ غلط (false) ہے تو، دستخط چالو نہیں ہے. <code dir="ltr">$Condition</code> عام طور پر ایک ایسی شرط پر مشتمل ہے جس کی وجہ سے کسی درخواست کو بلاک کرنا ہوگا.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonShort</code> کو "کیوں بلاک شدہ" فیلڈ میں حوالہ دیا جاتا ہے جب دستخط چالو ہوجاتا ہے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonLong</code> صارف کو ظاہر ہونے پر ایک پیغام ہے جب وہ روک رہے ہیں، اس وجہ سے وضاحت کریں کہ. ختم ہونے پر معیاری "کیوں بلاک شدہ" پیغام استعمال کرتا ہے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$DefineOptions</code> ایک اختیاری سرنی ہے جس میں کلیدی/قدر شامل ہیں، درخواست کی مثال کے مطابق مخصوص کنفگریشنات کے اختیارات کی وضاحت کرنے کے لیے استعمال کیا جاتا ہے. جب دستخط چالو ہو تو کنفگریشن کے اختیارات لاگو کیے جائیں گے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$this->trigger</code> سچ ہے جب دستخط چالو ہوجاتا ہے، اور جب غلط نہیں ہوتا تو غلط ہوتا ہے.<br /><br /></div>

##### <div dir="rtl">۶.۵.۱ <code dir="ltr">$this->bypass</code></div>

<div dir="rtl">دستخط بائی پاسز عام طور پر <code dir="ltr">$this->bypass</code> کے ساتھ لکھے جاتے ہیں.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$this->bypass</code> ۳ پیرامیٹرز کو قبول کرتا ہے: <code dir="ltr">$Condition</code>، <code dir="ltr">$ReasonShort</code>، <code dir="ltr">$DefineOptions</code> (اختیاری).<br /><br /></div>

<div dir="rtl"><code dir="ltr">$Condition</code> سچائی کا اندازہ کیا جاتا ہے. اگر یہ سچ (true) ہے تو، بائی پاس چالو ہے. اگر یہ غلط (false) ہے تو، بائی پاس چالو نہیں ہے. <code dir="ltr">$Condition</code> عام طور پر ایک ایسی شرط پر مشتمل ہے جو کسی کو بلاک کرنے کی درخواست نہیں بننی چاہیے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonShort</code> کو "کیوں بلاک شدہ" فیلڈ میں حوالہ دیا جاتا ہے جب بائی پاس چالو ہوجاتا ہے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$DefineOptions</code> ایک اختیاری سرنی ہے جس میں کلیدی/قدر شامل ہیں، درخواست کی مثال کے مطابق مخصوص کنفگریشنات کے اختیارات کی وضاحت کرنے کے لیے استعمال کیا جاتا ہے. جب دستخط چالو ہو تو کنفگریشن کے اختیارات لاگو کیے جائیں گے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$this->bypass</code> سچ ہے جب بائی پاس چالو ہوجاتا ہے، اور جب غلط نہیں ہوتا.<br /><br /></div>

##### <div dir="rtl">۶.۵.۲ <code dir="ltr">"$this->dnsReverse"</code></div>

<div dir="rtl">یہ ایک IP ایڈریس کے میزبان نام کو حاصل کرنے کے لیے استعمال کیا جا سکتا ہے. اگر آپ میزبانوں کو روکنے کے لیے ماڈیول بنانا چاہتے ہیں، تو یہ بندش مفید ثابت ہوسکتا ہے.<br /><br /></div>

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

#### <div dir="rtl">۶.۶ ماڈیول متغیر<br /><br /></div>

<div dir="rtl">ماڈیول ان کے اپنے گنجائش کے اندر عملدرآمد کرتے ہیں، اور کسی ماڈیول کی طرف سے وضاحت کردہ متغیرات، دوسرے ماڈیولز، یا پیراگراف اسکرپٹ تک نہیں پہنچ سکیں گے، جب تک کہ وہ <code dir="ltr">$CIDRAM</code> صف میں محفوظ نہ ہو جائیں (ماڈیول پھانسی ختم ہونے کے بعد سب کچھ صاف ہو گیا ہے).<br /><br /></div>

<div dir="rtl">مندرجہ ذیل فہرست کچھ عام متغیر ہیں جو آپ کے ماڈیول کے لیے مفید ہوسکتے ہیں:<br /><br /></div>

&nbsp; <div dir="rtl" style="display:inline">تفصیل</div> | <div dir="rtl">متغیر</div>
----|----
&nbsp; <div dir="rtl" style="display:inline">موجودہ تاریخ اور وقت.</div> | `$this->BlockInfo['DateTime']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کے لیے IP ایڈریس.</div> | `$this->BlockInfo['IPAddr']`
&nbsp; <div dir="rtl" style="display:inline">اگر موجودہ درخواست کا IP پتہ 6to4، Teredo، یا ISATAP ایڈریس ہے، تو وہ پتہ اس کے IPv4 کے برابر ہو جائے گا. اگر نہیں، تو یہ موجودہ درخواست کا IP پتہ ہوگا.</div> | `$this->BlockInfo['IPAddrResolved']`
&nbsp; <div dir="rtl" style="display:inline">CIDRAM سکرپٹ ورژن.</div> | `$this->BlockInfo['ScriptIdent']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کے لیے سوال.</div> | `$this->BlockInfo['Query']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کے لیے ریفرر (اگر ایک موجود ہے).</div> | `$this->BlockInfo['Referrer']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کے لیے صارف ایجنٹ (user agent).</div> | `$this->BlockInfo['UA']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کے لیے کم کیس میں صارف ایجنٹ (user agent).</div> | `$this->BlockInfo['UALC']`
&nbsp; <div dir="rtl" style="display:inline">جب صارف کو بلاک کر دیا جاتا ہے تو صارف کو ظاہر کرنے کا پیغام.</div> | `$this->BlockInfo['ReasonMessage']`
&nbsp; <div dir="rtl" style="display:inline">دستخط کی تعداد موجودہ درخواست کے لیے شروع ہو گئی ہے.</div> | `$this->BlockInfo['SignatureCount']`
&nbsp; <div dir="rtl" style="display:inline">کسی بھی دستخط کے لیے حوالہ کی معلومات موجودہ درخواست کے لیے تیار ہوئی.</div> | `$this->BlockInfo['Signatures']`
&nbsp; <div dir="rtl" style="display:inline">کسی بھی دستخط کے لیے حوالہ کی معلومات موجودہ درخواست کے لیے تیار ہوئی.</div> | `$this->BlockInfo['WhyReason']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کی درخواست کا طریقہ.</div> | `$this->BlockInfo['Request_Method']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کا پروٹوکول.</div> | `$this->BlockInfo['Protocol']`

---


### <div dir="rtl">۷. <a name="SECTION7"></a>جانا جاتا مطابقت کے مسائل</div>

<div dir="rtl">مندرجہ ذیل پیکجوں اور مصنوعات کو CIDRAM کے ساتھ مطابقت پزیر ہونے کے لیے مل گیا ہے:</div>
<div dir="rtl"><ul>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/52">Endurance Page Cache</a></strong></li>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/80">Mix.com</a></strong></li>
</ul></div>

<div dir="rtl">اس بات کا یقین کرنے کے لیے کہ مندرجہ ذیل پیکجوں اور مصنوعات CIDRAM کے ساتھ مطابقت پزیر ہوں گے ماڈیولز دستیاب کیے گئے ہیں:</div>
<div dir="rtl"><ul>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/56">BunnyCDN</a></strong></li>
 <li><strong><a dir="ltr" href="https://wordpress.org/support/topic/quic-dot-cloud-requires-all-ips-allowed/">Quic cloud</a></strong></li>
</ul></div>

<div dir="rtl"><em>بھی دیکھو: <a href="https://maikuolan.github.io/Compatibility-Charts/">مطابقت چارٹ</a>.</em><br /><br /></div>

---


### <div dir="rtl">۸. <a name="SECTION8">اکثر پوچھے گئے سوالات (FAQ)</div>

<div dir="rtl"><ul>
 <li><a href="#user-content-WHAT_IS_A_SIGNATURE">ایک "دستخط" کیا ہے؟</a></li>
 <li><a href="#user-content-WHAT_IS_A_CIDR">ایک "CIDR" کیا ہے؟</a></li>
 <li><a href="#user-content-WHAT_IS_A_FALSE_POSITIVE">ایک "جھوٹی مثبت" سے کیا مراد ہے؟</a></li>
 <li><a href="#user-content-BLOCK_ENTIRE_COUNTRIES">بلاک تمام ممالک CIDRAM کر سکتا ہوں؟</a></li>
 <li><a href="#user-content-SIGNATURE_UPDATE_FREQUENCY">دستخط کیسے بیشتر اپ ڈیٹ کر رہے ہیں؟</a></li>
 <li><a href="#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO">CIDRAM استعمال کرتے ہوئے میں ایک مسئلہ کا سامنا کرنا پڑا ہے اور میں اس کے بارے میں کیا پتہ نہیں ہے! مدد کریں!</a></li>
 <li><a href="#user-content-BLOCKED_WHAT_TO_DO">میں نے دورہ کرنا چاہتے ہیں کہ ایک ویب سائٹ سے CIDRAM کی طرف سے بلاک کیا گیا ہے! مدد کریں!</a></li>
 <li><a href="#user-content-MINIMUM_PHP_VERSION_V3">میں 7.2 سے زیادہ پرانے ایک PHP ورژن کے ساتھ CIDRAM v3~v4 استعمال کرنا چاہتے ہیں؛ کیا آپ مدد کر سکتے ہیں؟</a></li>
 <li><a href="#user-content-PROTECT_MULTIPLE_DOMAINS">میں نے ایک سے زیادہ ڈومینز کی حفاظت کے لیے ایک واحد CIDRAM تنصیب کا استعمال کر سکتا ہوں؟</a></li>
 <li><a href="#user-content-PAY_YOU_TO_DO_IT">میں نے اس پر وقت خرچ نہیں کرنا چاہتا (اسے انسٹال، اس کے قیام، وغیرہ)؛ میں نے آپ کو ایسا کرنے کے لیے ادا کر سکتے ہیں؟</a></li>
 <li><a href="#user-content-HIRE_FOR_PRIVATE_WORK">میں ذاتی کام کے لیے آپ کی خدمات حاصل کر سکتے ہیں؟</a></li>
 <li><a href="#user-content-SPECIALIST_MODIFICATIONS">مجھے خصوصی ترمیم کی ضرورت؛ کیا آپ مدد کر سکتے ہیں؟</a></li>
 <li><a href="#user-content-ACCEPT_OR_OFFER_WORK">میں نے ایک ڈویلپر، ویب سائٹ ڈیزائنر، یا پروگرامر ہوں. میں اس منصوبے سے متعلق کام کر سکتے ہیں؟</a></li>
 <li><a href="#user-content-WANT_TO_CONTRIBUTE">میں نے اس منصوبے میں شراکت کے لیے چاہتے ہیں؛ میں یہ کر سکتا ہوں؟</a></li>
 <li><a href="#user-content-CRON_TO_UPDATE_AUTOMATICALLY">کیا میں خود کار طریقے سے اپ ڈیٹ کرنے کے لیے cron استعمال کرسکتا ہوں؟</a></li>
 <li><a href="#user-content-WHAT_ARE_INFRACTIONS">"خلاف ورزی" کیا ہیں؟</a></li>
 <li><a href="#user-content-BLOCK_HOSTNAMES">CIDRAM بلاک میزبانوں کو کر سکتے ہیں؟</a></li>
 <li><a href="#میں-default_dns-کے-لیے-کیا-استعمال-کر-سکتا-ہوں">میں "default_dns" کے لیے کیا استعمال کر سکتا ہوں؟</a></li>
 <li><a href="#user-content-PROTECT_OTHER_THINGS">کیا ویب سائٹس کے علاوہ چیزوں کی حفاظت کے لیے میں CIDRAM استعمال کرسکتا ہوں (مثال کے طور پر، ای میل سرورز، FTP سرورز، SSH سرورز، IRC سرورز، وغیرہ)؟</a></li>
 <li><a href="#user-content-CDN_CACHING_PROBLEMS">مواد ترسیل کے نیٹ ورک یا کیشنگ کی خدمات کا استعمال کرتے ہوئے ایک ہی وقت میں CIDRAM کا استعمال کرتے ہوئے، کیا مسائل ہو گی؟</a></li>
 <li><a href="#user-content-DDOS_ATTACKS">کیا CIDRAM DDoS حملوں کے خلاف میری ویب سائٹ کی حفاظت کرتا ہے؟</a></li>
 <li><a href="#user-content-CHANGE_COMPONENT_SORT_ORDER">جب میں اپ ڈیٹس کے صفحے کے ذریعہ ماڈیولز یا دستخط شدہ فائلوں کو چالو یا غیر فعال کروں تو، یہ انفرادی طور پر کنفگریشن میں تبدیل کرتا ہے. کیا میں اس راستہ کو تبدیل کر سکتا ہوں جسے وہ کنفگریشن دیں گے؟</a></li>
 <li><a href="#user-content-HOW_TO_USE_PDO">"PDO DSN" کیا ہے؟ میں CIDRAM کے ساتھ PDO کیسے استعمال کرسکتا ہوں؟</a></li>
 <li><a href="#user-content-BLOCK_CRON">CIDRAM cronjobs کو مسدود کررہا ہے؛ اس کو کیسے ٹھیک کریں؟</a></li>
</ul></div>

#### <div dir="rtl"><a name="WHAT_IS_A_SIGNATURE"></a>ایک "دستخط" کیا ہے؟<br /><br /></div>

<div dir="rtl">CIDRAM کے تناظر میں، اعداد و شمار کے مخصوص کچھ ہم کے لیے تلاش کر رہے ہیں اس کی شناخت کے لیے استعمال کیا جاتا ہے کے لیے ایک "دستخط" مراد، عام طور پر ایک IP ایڈریس یا CIDR، CIDRAM کے لیے کچھ ہدایات کے ساتھ (یہ مقابلوں جب ہم کے لیے تلاش کر رہے ہیں کیا جواب دینے کا بہترین طریقہ، وغیرہ). CIDRAM کے لیے ایک مخصوص دستخط کی کچھ اس طرح دکھائی دیتی ہے:<br /><br /></div>

<div dir="rtl">"دستخط فائلوں" کے لیے:<br /><br /></div>

`1.2.3.4/32 Deny Generic`

<div dir="rtl">"ماڈیولز" کے لیے:<br /><br /></div>

```PHP
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

<div dir="rtl">نوٹ: "دستخط فائلوں" کے لیے دستخط، اور "ماڈیولز" کے لیے دستخط وہی چیز نہیں ہیں.<em></em><br /><br /></div>

<div dir="rtl">اکثر ایسا ہوتا ہے (لیکن ہمیشہ نہیں)، دستخط "کے دستخط حصوں" میں بنڈل گا، اکثر تبصرے، مارک اپ، اور متعلقہ میٹا ڈیٹا کے ساتھ شامل تھے. یہ دستخط اور مزید ہدایات کے لیے اضافی سیاق و سباق فراہم کر سکتے ہیں.<br /><br /></div>

#### <div dir="rtl"><a name="WHAT_IS_A_CIDR"></a>ایک "CIDR" کیا ہے؟<br /><br /></div>

<div dir="rtl">"CIDR" "Classless Inter-Domain Routing" ("غیر طبقاتی انٹر ڈومین روٹنگ") کے لیے مخفف ہے <em>[<a href="https://ar.wikipedia.org/wiki/%D8%AA%D9%88%D8%AC%D9%8A%D9%87_%D8%A8%D9%8A%D9%86_%D8%A7%D9%84%D9%85%D8%AC%D8%A7%D9%84%D8%A7%D8%AA_%D9%84%D8%A7%D9%81%D8%A6%D9%88%D9%8A%D8%A7">۱</a>، <a href="https://whatismyipaddress.com/cidr">۲</a>]</em>. یہ مخفف اس پیکج، "CIDRAM" کے لیے نام کا حصہ کے طور پر استعمال کیا جاتا ہے. یہ "Classless Inter-Domain Routing Access Manager" (غیر طبقاتی انٹر ڈومین روٹنگ رسائی مینیجر) کے لیے مخفف ہے.<br /><br /></div>

<div dir="rtl">تاہم، CIDRAM کے تناظر میں (جیسا کہ یہ دستاویزات کے اندر اندر، متعلقہ مباحث میں، یا زبان کے اعداد و شمار کے اندر اندر)، ایک "CIDR" (واحد) یا "CIDR" (جمع) کا ذکر کیا جاتا ہے جب، ہمارے ارادہ معنی ذیلی نیٹ ہے، CIDR سنکیتن کا استعمال کرتے ہوئے اظہار کیا. ذیلی نیٹ کو مختلف مختلف طریقوں سے اظہار کیا جا سکتا ہے کیونکہ اس کی وجہ ہے. CIDRAM، لہذا، ایک "نیٹ رسائی مینیجر" سمجھا جا سکتا ہے.<br /><br /></div>

<div dir="rtl">یہ وضاحت، اور فراہم تناظر، کسی بھی ابہام حل کرنے کے لیے مدد کرنی چاہیے.<br /><br /></div>

#### <div dir="rtl"><a name="WHAT_IS_A_FALSE_POSITIVE"></a>ایک "جھوٹی مثبت" سے کیا مراد ہے؟<br /><br /></div>

<div dir="rtl">اصطلاح "جھوٹی مثبت" (<em>متبادل کے طور پر: "جھوٹی مثبت غلطی"؛ "جھوٹے الارم"</em>)، بیان بہت صرف، اور ایک عام سیاق و سباق میں، ایک کی حالت کے لیے جانچ جب، استعمال کیا جاتا ہے کہ ٹیسٹ کے نتائج کا حوالہ دیتے ہیں کے لیے، نتائج مثبت ہیں جب (یعنی حالت "مثبت" یا "سچ" ہونے کا تعین کیا جاتا ہے)، لیکن بننے کی توقع کی جاتی ہے (یا ہونا چاہیے) منفی (یعنی حالت، حقیقت میں، "منفی"، یا "جھوٹے"). "جھوٹی مثبت" مثل غور کیا جا سکتا کے لیے "رونا بھیڑیا" (جس حالت تجربہ کیا جا رہا، حالت "جھوٹے" کہ میں ریوڑ کے قریب کوئی بھیڑیا ہے، اور شرط کے طور پر رپورٹ کیا جاتا ہے ریوڑ کے قریب ایک بھیڑیا ہے کہ آیا ہے "بھیڑیا، بھیڑیا" بلا کی راہ کی طرف چرواہا کی طرف سے "مثبت")، یا طبی جانچ میں حالات جس میں ایک مریض، کچھ بیماری یا مرض ہونے حقیقت میں، وہ ایسی کوئی بیماری یا مرض ہے جب کے طور پر تشخیص کی جاتی ہے کے مطابق.<br /><br /></div>

<div dir="rtl">ایک شرط کے لیے جانچ جب متعلقہ نتائج "سچ مثبت" کی اصطلاحات کا استعمال کرتے ہوئے، "سچ منفی" اور "جھوٹے منفی" بیان کیا جا سکتا ہے. "سچ مثبت" جب ٹیسٹ کے نتائج اور حالت کی اصل ریاست دونوں حقیقی (یا "مثبت")، اور ایک "حقیقی منفی" ہیں سے مراد ہے سے مراد ہے جب ٹیسٹ کے نتائج اور کی اصل ریاست شرط ہیں دونوں جھوٹے ہیں (یا "منفی")؛ "سچ مثبت" یا "سچ منفی" ایک "صحیح اندازہ" سمجھا جاتا ہے. ایک "جھوٹی مثبت" کے برعکس ایک "جھوٹے منفی" ہے؛ "جھوٹے منفی" سے ٹیسٹ کے نتائج منفی ہیں، جب (یعنی حالت "منفی"، یا "جھوٹے" ہونے کا تعین کیا جاتا ہے)، لیکن بننے کی توقع کی جاتی ہے (یا ہونا چاہیے) مراد مثبت (یعنی، حالت، حقیقت میں، "مثبت" یا "سچ") ہے.<br /><br /></div>

<div dir="rtl">CIDRAM کے تناظر میں، ان شرائط جسے انہوں بلاک CIDRAM کے دستخط اور کیا / کا حوالہ دیتے ہیں. ایک IP ایڈریس، برا فرسودہ یا غلط دستخطوں کی وجہ CIDRAM بلاکس، لیکن ایسا نہیں کیا جب چاہیے ہے، یا یہ غلط وجوہات کی بنا پر ایسا کرتا ہے جب، ہم نے ایک "جھوٹی مثبت" کے طور پر اس ایونٹ کا حوالہ دیتے ہیں. CIDRAM ایک IP ایڈریس جو، کی وجہ سے غیر متوقع خطرات سے، بلاک کر دیا گیا ہے چاہیے لاپتہ اس کے دستخط میں دستخط یا کمی کو بلاک کرنے میں ناکام ہونے پر، ہم نے ایک "یاد کا پتہ لگانے" (ایک "جھوٹے منفی" کے مطابق ہوتا ہے) کے طور پر اس واقعہ کا حوالہ دیتے ہیں.<br /><br /></div>

<div dir="rtl">یہ مندرجہ ذیل ٹیبل کی طرف سے بیان کیا جا سکتا ہے:<br /><br /></div>

&nbsp; <div dir="rtl" style="display:inline">CIDRAM چاہیے <strong>نہیں</strong> ایک IP ایڈریس بلاک</div> | &nbsp; <div dir="rtl" style="display:inline">CIDRAM ایک IP ایڈریس مسدود کرنا <strong>چاہیے</strong></div> | &nbsp;
---|---|---
&nbsp; <div dir="rtl" style="display:inline">یہ سچ ہے کہ منفی (صحیح اندازہ)</div> | &nbsp; <div dir="rtl" style="display:inline">فوت شدہ کا پتہ لگانے (جھوٹے منفی کے مطابق)</div> | <div dir="rtl">CIDRAM <strong>نہیں</strong> بلاک ایک IP ایڈریس کراسکتا</div>
&nbsp; <div dir="rtl" style="display:inline"><strong>جھوٹی مثبت</strong></div> | &nbsp; <div dir="rtl" style="display:inline">یہ سچ ہے کہ مثبت (صحیح اندازہ)</div> | &nbsp; <div dir="rtl" style="display:inline">CIDRAM <strong>ہے</strong> ایک IP ایڈریس بلاک</div>

#### <div dir="rtl"><a name="BLOCK_ENTIRE_COUNTRIES"></a>بلاک تمام ممالک CIDRAM کر سکتا ہوں؟<br /><br /></div>

<div dir="rtl">جی ہاں. اس کا آسان ترین طریقہ BGPView ماڈیول کو انسٹال کرنا اور اپنی ضروریات کے مطابق تشکیل دینا ہے.<br /><br /></div>

#### <div dir="rtl"><a name="SIGNATURE_UPDATE_FREQUENCY"></a>دستخط کیسے بیشتر اپ ڈیٹ کر رہے ہیں؟<br /><br /></div>

<div dir="rtl">اپ ڈیٹ فریکوئنسی سوال میں دستخط کی فائلوں پر منحصر ہوتی ہے. CIDRAM دستخط کی فائلوں کے لیے تمام حاکم عام طور پر اپ ڈیٹ کرنے کے لیے ممکن ہے کے طور پر کے طور پر ان کے دستخط رکھنے کی کوشش کرتے ہیں، لیکن ہم سب کے طور پر مختلف دیگر وعدوں، اس منصوبے سے باہر ہماری زندگی ہے، اور ہم میں سے کوئی اس کو مالی طور پر معاوضہ رہے ہیں (یعنی، ادا کی ) منصوبے پر ہماری کوششوں کے لیے ایک عین مطابق اپ ڈیٹ کے شیڈول کی ضمانت نہیں کیا جا سکتا. ان کو اپ ڈیٹ کرنے کے لیے کافی وقت نہیں ہے جب بھی، اور عام طور پر، حاکم ضرورت پر اور حدود کے درمیان پائے جاتے تبدیلیاں کس طرح اکثر کی بنیاد پر ترجیح دینے کی کوشش کریں عام طور پر، دستخطوں کو اپ ڈیٹ کر رہے ہیں. اگر آپ کو کوئی پیشکش کرنے کو تیار ہیں تو اس سلسلے میں معاونت ہمیشہ تعریف کی ہے.<br /><br /></div>

#### <div dir="rtl"><a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>CIDRAM استعمال کرتے ہوئے میں ایک مسئلہ کا سامنا کرنا پڑا ہے اور میں اس کے بارے میں کیا پتہ نہیں ہے! مدد کریں!</div>
<div dir="rtl"><ul>
 <li>آپ نے سافٹ ویئر کا تازہ ترین ورژن استعمال کر رہے ہیں؟ آپ کو آپ کے دستخط فائلوں کا تازہ ترین ورژن استعمال کر رہے ہیں؟ ان دو سوالوں کی یا تو کرنے کے لیے جواب نہیں ہے تو، سب سے پہلے سب کچھ کو اپ ڈیٹ کرنے کی کوشش کریں، اور چاہے وہ مسئلہ برقرار رہتا ہے چیک کریں. یہ برقرار رہتا ہے، پڑھنے جاری رکھیں.</li>
 <li>اگر آپ کو تمام دستاویزات کے ذریعے کی جانچ پڑتال کی ہے؟ اگر نہیں، تو براہ مہربانی. مسئلہ دستاویزات استعمال کر حل نہیں کیا جا سکتا ہے، تو پڑھنے جاری رکھیں.</li>
 <li>اگر آپ کو <strong><a href="https://github.com/CIDRAM/CIDRAM/issues">issues صفحے</strong></a> جانچ پڑتال کی ہے، دیکھنا چاہے مسئلہ پہلے ذکر کیا گیا ہے؟ اس سے پہلے ذکر کیا گیا ہے تو، چاہے وہ کسی بھی تجاویز، خیالات، اور / یا کے حل فراہم کیا گیا جانچ اور مسئلہ حل کرنے کی کوشش کرنے کے لیے ضروری کے مطابق عمل کریں.</li>
 <li>اگر مسئلہ اب بھی جاری رہتا ہے، تو issues کے صفحے پر ایک نیا issue تشکیل دے کر اس کے بارے میں مدد طلب کریں.</li>
</ul></div>

#### <div dir="rtl"><a name="BLOCKED_WHAT_TO_DO"></a>میں نے دورہ کرنا چاہتے ہیں کہ ایک ویب سائٹ سے CIDRAM کی طرف سے بلاک کیا گیا ہے! مدد کریں!<br /><br /></div>

<div dir="rtl">CIDRAM ویب سائٹ کے مالکان ناپسندیدہ ٹریفک کو بلاک کرنے کے لیے ایک ذریعہ فراہم کرتا ہے، لیکن یہ وہ CIDRAM استعمال کرنا چاہتے ہیں کہ کس طرح اپنے لیے فیصلہ کرنے کے لیے ویب سائٹ کے مالکان کی ذمہ داری ہے. کے دستخط سے متعلق جھوٹی مثبت عام طور CIDRAM ساتھ شامل فائلوں کی صورت میں، تصحیح بنایا جا سکتا ہے، لیکن مخصوص ویب سائٹس سے غیر مسدود ہونے کے حوالے میں، آپ کے سوال میں ویب سائٹس کے مالکان کے ساتھ کہ اپ لینے کی ضرورت پڑے گی. مقدمات جہاں تصحیح کم سے کم، بنائے جاتے ہیں میں، وہ مثال ہے، وہ ان کی تنصیب ترمیم شدہ گئے ہیں جہاں کے لیے، اس طرح کے طور پر ان کے دستخط فائلوں اور / یا تنصیب، اور دیگر مقدمات میں (اپ ڈیٹ کرنے کی ضرورت ہو گی، ان کی اپنی مرضی کے دستخط پیدا، وغیرہ)، کو حل کرنے کی ذمہ داری آپ کا مسئلہ مکمل طور پر ان کی ہے، اور ہمارے قابو سے باہر مکمل طور پر ہے.<br /><br /></div>

#### <div dir="rtl"><a name="MINIMUM_PHP_VERSION_V3"></a>میں 7.2 سے زیادہ پرانے ایک PHP ورژن کے ساتھ CIDRAM v3~v4 استعمال کرنا چاہتے ہیں؛ کیا آپ مدد کر سکتے ہیں؟<br /><br /></div>

<div dir="rtl">نہیں. CIDRAM v3~v4 کم از کم PHP≥7.2 کی ضرورت ہے.<br /><br /></div>

<div dir="rtl"><em>بھی دیکھو: <a href="https://maikuolan.github.io/Compatibility-Charts/">مطابقت چارٹ</a>.</em><br /><br /></div>

#### <div dir="rtl"><a name="PROTECT_MULTIPLE_DOMAINS"></a>میں نے ایک سے زیادہ ڈومینز کی حفاظت کے لیے ایک واحد CIDRAM تنصیب کا استعمال کر سکتا ہوں؟<br /><br /></div>

<div dir="rtl">جی ہاں. CIDRAM ایک سے زیادہ ڈومینز کی حفاظت کے لیے استعمال کیا جا سکتا ہے. ضرورت کی کنفگریشن مختلف ہے تو، ایسا کرنے کے لیے تحفظ کی ضرورت ہوتی ڈومینز کے مطابق نامی نئی کنفگریشن فائل، تخلیق کرتے ہیں. CIDRAM یہ ڈومین کے لیے کام کرنا چاہیے کہ کس طرح اس بات کا تعین کرنے کے لیے ان فائلوں کو استعمال کریں گے. سوف تستخدم CIDRAM هذه الملفات لتحديد كيفية تشغيلها للنطاق. ایک مثال کے طور، کے لیے <code dir="ltr">"https://www.some-domain.tld/"</code>، اس کا نام ہے <code dir="ltr">"some-domain.tld.config.yml"</code>. ڈومین نام <code dir="ltr">"HTTP_HOST"</code> سے آتا ہے. <code dir="ltr">"www"</code> نظر انداز کر دیا جاتا ہے.<br /><br /></div>

#### <div dir="rtl"><a name="PAY_YOU_TO_DO_IT"></a>میں نے اس پر وقت خرچ نہیں کرنا چاہتا (اسے انسٹال، اس کے قیام، وغیرہ)؛ میں نے آپ کو ایسا کرنے کے لیے ادا کر سکتے ہیں؟<br /><br /></div>

<div dir="rtl">شاید. یہ معاملہ در معاملہ کی بنیاد پر کیا جاتا ہے. کی آپ کو ضرورت ہے ہمیں بتائیں. ہمیں بتائیں کہ آپ کی پیشکش کر رہے ہیں. ہم آپ کو بتا دیں گے ہم مدد کر سکتے ہیں.<br /><br /></div>

#### <div dir="rtl"><a name="HIRE_FOR_PRIVATE_WORK"></a>میں ذاتی کام کے لیے آپ کی خدمات حاصل کر سکتے ہیں؟<br /><br /></div>

<div dir="rtl"><em>اوپر ملاحظہ کریں.</em><br /><br /></div>

#### <div dir="rtl"><a name="SPECIALIST_MODIFICATIONS"></a>مجھے خصوصی ترمیم کی ضرورت؛ کیا آپ مدد کر سکتے ہیں؟<br /><br /></div>

<div dir="rtl"><em>اوپر ملاحظہ کریں.</em><br /><br /></div>

#### <div dir="rtl"><a name="ACCEPT_OR_OFFER_WORK"></a>میں نے ایک ڈویلپر، ویب سائٹ ڈیزائنر، یا پروگرامر ہوں. میں اس منصوبے سے متعلق کام کر سکتے ہیں؟<br /><br /></div>

<div dir="rtl">جی ہاں. ہمارے لائسنس اس کی ممانعت نہیں کرتا.<br /><br /></div>

#### <div dir="rtl"><a name="WANT_TO_CONTRIBUTE"></a>میں نے اس منصوبے میں شراکت کے لیے چاہتے ہیں؛ میں یہ کر سکتا ہوں؟<br /><br /></div>

<div dir="rtl">جی ہاں. اس کا خیر مقدم کیا جاتا ہے. "CONTRIBUTING.md" ملاحظہ کریں مزید معلومات کے لیے.<br /><br /></div>

#### <div dir="rtl"><a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>کیا میں خود کار طریقے سے اپ ڈیٹ کرنے کے لیے cron استعمال کرسکتا ہوں؟<br /><br /></div>

<div dir="rtl">جی ہاں. بیرونی سکرپٹ کے ذریعہ اپ ڈیٹس صفحہ کے ساتھ بات چیت کرنے کے لیے ایک API سامنے کے آخر میں بنایا جاتا ہے. ایک علاحدہ لکھاوٹ، "<a href="https://github.com/Maikuolan/Cronable">Cronable</a>"، دستیاب ہے، اور اس کے اور دیگر معاون پیکجوں کو خود کار طریقے سے اپ ڈیٹ کرنے کے لیے آپ کے cron manager یا cron scheduler کا استعمال کیا جا سکتا ہے (یہ اسکرپٹ اپنی اپنی دستاویزات فراہم کرتا ہے).<br /><br /></div>

#### <div dir="rtl"><a name="WHAT_ARE_INFRACTIONS"></a>"خلاف ورزی" کیا ہیں؟<br /><br /></div>

<div dir="rtl">"دستخط شمار" اور "خلاف ورزی" دونوں کا تعلق کسی خاص درخواست کے دوران شروع ہونے والے دستخطوں کی شدت اور تعداد سے ہے، چاہے دستخطی فائلوں، ماڈیولز، معاون اصولوں، یا کسی اور وجہ سے. لیکن، جب کہ "دستخط شمار" صرف اس مخصوص درخواست کے لیے برقرار رہتی ہے، "خلاف ورزی" زیادہ سے زیادہ درخواستوں پر برقرار رہ سکتی ہے جیسا کہ <code dir="ltr">default_tracktime</code> کے ذریعے طے کیا گیا ہے.<br /><br /></div>

<div dir="rtl">یہ اس بات کو یقینی بناتا ہے کہ جب ایک درخواست کو کافی تعداد میں خلاف ورزیوں کے ساتھ بلاک کیا جاتا ہے، تو اسی ذریعہ سے آنے والی درخواستوں کو بھی بلاک کیا جا سکتا ہے.<br /><br /></div>

#### <div dir="rtl"><a name="BLOCK_HOSTNAMES"></a>CIDRAM بلاک میزبانوں کو کر سکتے ہیں؟<br /><br /></div>

<div dir="rtl">جی ہاں. یہ ایک معاون اصول یا حسب ضرورت ماڈیول بنا کر حاصل کیا جا سکتا ہے.<br /><br /></div>

![میزبان ناموں کو مسدود کرنے کے لیے ایک معاون اصول](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <div dir="rtl"><a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>میں "default_dns" کے لیے کیا استعمال کر سکتا ہوں؟<br /><br /></div>

<div dir="rtl">عام طور پر، کسی قابل اعتماد DNS سرور کا IP کافی ہونا چاہیے. اگر آپ تجاویز کی تلاش کر رہے ہیں تو، <a href="https://public-dns.info/">public-dns.info</a> اور <a href="https://servers.opennic.org/">OpenNIC</a> نام سے جانا جاتا، عوامی DNS سرورز کی وسیع فہرست فراہم کرتے ہیں. متبادل طور پر، ذیل میں میز ملاحظہ کریں:<br /><br /></div>

IP | آپریٹر
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

<div dir="rtl"><em>نوٹ: میں نجی رازداری کے عمل، سیکورٹی، افادیت، اور کسی بھی DNS کی خدمات، درج کی یا دوسری صورت میں قابل اعتماد کے بارے میں کوئی دعوی نہیں کرتا. جب آپ کے بارے میں فیصلے کرتے ہیں تو براہ کرم خود اپنی تحقیق کریں.</em><br /><br /></div>

#### <div dir="rtl"><a name="PROTECT_OTHER_THINGS"></a>کیا ویب سائٹس کے علاوہ چیزوں کی حفاظت کے لیے میں CIDRAM استعمال کرسکتا ہوں (مثال کے طور پر، ای میل سرورز، FTP سرورز، SSH سرورز، IRC سرورز، وغیرہ)؟<br /><br /></div>

<div dir="rtl">آپ یہ کر سکتے ہیں (قانونی احساس میں)، لیکن آپ کو نہیں ہونا چاہیے (تکنیکی اور عملی احساس میں). ہمارے لائسنس کو CIDRAM کا استعمال کیا ٹیکنالوجی کی حد تک محدود نہیں ہے. تاہم، CIDRAM ایک "ویب ایپلی کیشن فائر وال" (WAF) ہے، جو ویب سائٹس کی حفاظت کے لیے ہے. دوسرے مقاصد کے لیے استعمال ہونے پر یہ مؤثر یا قابل اعتماد ہونے کا امکان نہیں ہے (کیونکہ یہ دماغ میں دیگر ٹیکنالوجیوں کے ساتھ ڈیزائن نہیں کیا گیا تھا)، عملدرآمد مشکل ہوسکتا ہے، اور غلطیوں اور دیگر مسائل کا خطرہ بہت زیادہ ہے.<br /><br /></div>

#### <div dir="rtl"><a name="CDN_CACHING_PROBLEMS"></a>مواد ترسیل کے نیٹ ورک یا کیشنگ کی خدمات کا استعمال کرتے ہوئے ایک ہی وقت میں CIDRAM کا استعمال کرتے ہوئے، کیا مسائل ہو گی؟<br /><br /></div>

<div dir="rtl">ممکنہ طور پر. یہ سوال میں خدمت کی نوعیت پر منحصر ہے، اور آپ اس کا استعمال کیسے کر رہے ہیں. عموما، اگر آپ صرف جامد اثاثوں کو پکڑ رہے ہیں تو (تصاویر، CSS، وغیرہ؛ جو وقت کے ساتھ تبدیل نہیں ہوتا ہے)، کوئی مسئلہ نہیں ہونا چاہیے. تاہم، وہاں مسائل ہوسکتے ہیں، اگر آپ ڈیٹا کیشنگ کر رہے ہیں جو عام طور پر متحرک طور پر پیدا ہوجائے تو درخواست کی جاتی ہے، یا اگر آپ POST کی درخواستوں کے نتائج کو پکڑ رہے ہیں (یہ آپ کی ویب سائٹ اور ماحول کو جامد طور پر فراہم کرے گا، اور CIDRAM ایک مستحکم ماحول میں کسی بھی معقول فائدہ فراہم کرنے کے لیے امکان نہیں ہے). اس کے علاوہ، آپ کو استعمال کرنے والے مواد کی ترسیل کے نیٹ ورک یا کیشنگ سروس پر منحصر ہے، اس کے مطابق CIDRAM مخصوص کنفگریشنات کی ضروریات ہوسکتی ہے (آپ کو اس بات کا یقین کرنے کی ضرورت ہوگی کہ CIDRAM صحیح طریقے سے کنفگریشن دیا جائے). غلط کنفگریشن کی وجہ سے غلط جھوٹے مثبت اور دیگر مسائل کا سبب بن سکتا ہے.<br /><br /></div>

#### <div dir="rtl"><a name="DDOS_ATTACKS"></a>کیا CIDRAM DDoS حملوں کے خلاف میری ویب سائٹ کی حفاظت کرتا ہے؟<br /><br /></div>

<div dir="rtl">یہ نہیں کرے گا.<br /><br /></div>

<div dir="rtl">مزید تفصیل میں: CIDRAM اس اثر کو کم کرنے میں مدد دے گی جو ناپسندیدہ ٹریفک آپ کی ویب سائٹ اور ہارڈ ویئر پر ہوسکتی ہے (اس کا مطلب سستا ویب سائٹ بینڈوڈتھ اخراجات اور صحت مند سرور). تاہم، اس سوال کو سمجھنے کے لۓ دو اہم چیزیں ہیں جو یاد رکھنا ضروری ہے.<br /><br /></div>

<div dir="rtl">۱. CIDRAM ایک PHP پیکیج ہے، اور اس وجہ سے چلاتا ہے جہاں PHP انسٹال ہے. اس کا مطلب یہ ہے کہ سرور پہلے سے موصول ہونے کے بعد CIDRAM صرف درخواستوں کو دیکھ سکتے ہیں اور بلاک کرسکتے ہیں. ۲. DDoS حملے کے ذریعہ ھدف کردہ سرور تک پہنچنے سے قبل مؤثر DDoS کمیشن کو درخواستوں کو فلٹر کرنا چاہیے. مثالی طور پر، وہ ان جگہوں سے پتہ لگانے اور کم کرنے کے قابل ہونا چاہیے جو حملوں کے ساتھ منسلک ٹریفک کو ختم کرنے میں کامیاب ہوسکتی ہیں، اس سے پہلے کہ وہ پہلی جگہ میں ھدف شدہ سرور تک پہنچے.<br /><br /></div>

<div dir="rtl">اس کو نافذ کرنے کے کچھ طریقے: وقف ہارڈ ویئر کے حل. وقف DDoS کمیشن کی خدمات. DDoS مزاحم نیٹ ورک کے ذریعہ ڈومین کے DNS کو روٹنگ. کلاؤڈ پر مبنی فلٹرنگ. متبادل طور پر: اس کا کچھ مجموعہ کسی بھی صورت میں، یہ مضمون پیچیدہ ہے، لہذا اگر آپ اس میں دلچسپی رکھتے ہیں تو میں مزید تحقیق کروں گا. جب DDoS کے حملوں کی صحیح نوعیت مناسب طریقے سے سمجھ گئی ہے، تو یہ جواب زیادہ احساس کرے گا.<br /><br /></div>

#### <div dir="rtl"><a name="CHANGE_COMPONENT_SORT_ORDER"></a>جب میں اپ ڈیٹس کے صفحے کے ذریعہ ماڈیولز یا دستخط شدہ فائلوں کو چالو یا غیر فعال کروں تو، یہ انفرادی طور پر کنفگریشن میں تبدیل کرتا ہے. کیا میں اس راستہ کو تبدیل کر سکتا ہوں جسے وہ کنفگریشن دیں گے؟<br /><br /></div>

<div dir="rtl">جی ہاں. اگر آپ کو مخصوص فائلوں میں عمل درآمد کرنے کے لیے کچھ فائلوں پر مجبور کرنے کی ضرورت ہے تو، آپ ان کے نام سے پہلے ان کنفگریشنات کو ہدایت دیتے ہیں جہاں وہ فہرست میں درج ہوتے ہیں، ان سے پہلے کسی بھی مباحثہ کے اعداد و شمار کو شامل کرسکتے ہیں. جب اپ ڈیٹس کے صفحے کو بعد میں فائلوں کو دوبارہ کنفگریشن دیتا ہے، تو اس نے مزید کہا کہ خود مختار اعداد و شمار اس طرح کے حکم کو متاثر کرے گی، جس کے نتیجے میں ان کے نتیجے میں عملدرآمد کرنے کے نتیجے میں عملدرآمد کرنے کے لۓ، بغیر کسی کو تبدیل کرنے کی ضرورت ہے.<br /><br /></div>

<div dir="rtl">مثال کے طور پر، مندرجہ ذیل درج ذیل فائلوں کے ساتھ ایک کنفگریشن ڈائریکٹری کو فرض کرنا:<br /><br /></div>

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

<div dir="rtl">اگر آپ چاہتے تھے کہ <code dir="ltr">file3.php</code> سب سے پہلے عمل کرنے کے لیے، آپ فائل کے نام سے پہلے <code dir="ltr">aaa:</code> کی طرح کچھ شامل کرسکتے ہیں:<br /><br /></div>

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

<div dir="rtl">پھر، اگر ایک نئی فائل، <code dir="ltr">file6.php</code>، چالو کر دیا جاتا ہے، جب اپ ڈیٹس صفحہ ان کو دوبارہ دوبارہ تبدیل کرتا ہے، تو اسے اس طرح ختم کرنا چاہیے:<br /><br /></div>

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

<div dir="rtl">ایک ہی صورت حال حال ہی میں ایک فائل غیر فعال ہے. اس کے برعکس، اگر آپ چاہتے تھے کہ آخری فائل کو عمل کرنے کے لۓ، آپ فائل کے نام سے پہلے <code dir="ltr">zzz:</code> کی طرح کچھ شامل کرسکیں. کسی بھی صورت میں، آپ کو سوال میں فائل کا نام تبدیل کرنے کی ضرورت نہیں ہوگی.<br /><br /></div>

#### <div dir="rtl"><a name="HOW_TO_USE_PDO"></a>"PDO DSN" کیا ہے؟ میں CIDRAM کے ساتھ PDO کیسے استعمال کرسکتا ہوں؟<br /><br /></div>

<div dir="rtl">"<a dir="ltr" href="https://www.php.net/manual/en/intro.pdo.php">PHP Data Objects</a>" (PHP ڈیٹا آبجیکٹ)، "PDO" کا مخفف ہے. یہ PHP کو ایک انٹرفیس فراہم کرتا ہے تاکہ وہ PHP کی ایپلی کیشنز کے ذریعہ استعمال ہونے والے ڈیٹا بیس سسٹم سے رابطہ قائم کرسکیں.<br /><br /></div>

<div dir="rtl">"<a dir="ltr" href="https://en.wikipedia.org/wiki/Data_source_name">data source name</a>" (ڈیٹا سورس کا نام)، "DSN" کا مخفف ہے. یہ PDO کو بیان کرتا ہے کہ اسے ڈیٹا بیس سے کیسے جڑنا چاہیے.<br /><br /></div>

<div dir="rtl">CIDRAM میں، آپ کیڈیچنگ مقاصد کے لیے PDO استعمال کرسکتے ہیں. تاکہ اسے صحیح طریقے سے کام کیا جاسکے، کنفگریشن کے ذریعہ اس کو اہل بنائیں، اس کے لیے ایک ڈیٹا بیس بنائیں، اور نیچے بیان کردہ ڈھانچے کے مطابق اپنے ڈیٹا بیس میں ایک نیا ٹیبل بنائیں.<br /><br /></div>

<div dir="rtl">جب ایک ڈیٹا بیس کنکشن کامیابی کے ساتھ ہے، لیکن ضروری جدول موجود نہیں ہے، یہ خود بخود تخلیق کرنے کی کوشش کرے گی. تاہم، اس طرز عمل کا بڑے پیمانے پر تجربہ نہیں کیا گیا ہے اور کامیابی کی ضمانت نہیں دی جاسکتی ہے.<br /><br /></div>

<div dir="rtl">اگر آپ اسے استعمال نہیں کرنا چاہتے ہیں تو، آپ ان ہدایات کو نظرانداز کرسکتے ہیں.<br /><br /></div>

<div dir="rtl">ذیل میں بیان کردہ ڈھانچے میں "cidram" کو اپنے ڈیٹا بیس کے نام کے بطور استعمال کیا گیا ہے، لیکن آپ اپنے ڈیٹا بیس کے لیے جو بھی نام استعمال کرنا چاہ، استعمال کرسکتے ہیں، جب تک کہ وہی نام آپ کی ڈی ایس این کنفگریشن میں نقل کیا جائے.<br /><br /></div>

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

<div dir="rtl"><code dir="ltr">pdo_dsn</code> نیچے جیسا کہ بیان کیا جانا چاہیے.<br /><br /></div>

```
ڈیٹا بیس ڈرائیور کس پر استعمال ہوتا ہے اس پر منحصر ہے...
├─4d (انتباہ: تجرباتی، غیر جانچ شدہ، تجویز کردہ نہیں)
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └رابطہ کرنے کے لیے میزبان
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └استعمال کرنے کے لیے ڈیٹا بیس کا نام
│                │              │
│                │              └استعمال کرنے کے لیے پورٹ نمبر
│                │
│                └رابطہ کرنے کے لیے میزبان
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └استعمال کرنے کے لیے ڈیٹا بیس کا نام
│    │          │
│    │          └رابطہ کرنے کے لیے میزبان
│    │
│    └Possible values: "mssql", "sybase", "dblib".
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├مقامی ڈیٹا بیس فائل کا راستہ ثابت ہوسکتا ہے
│                    │
│                    ├ایک میزبان اور پورٹ نمبر سے رابطہ کرسکتے ہیں
│                    │
│                    └اگر آپ اسے استعمال کرنا چاہتے ہیں تو آپ کو Firebird دستاویزات کا حوالہ دینا چاہیے
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └رابطہ کرنے کے لیے کیٹلوجڈ ڈیٹا بیس
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └رابطہ کرنے کے لیے کیٹلوجڈ ڈیٹا بیس
├─mysql (سب سے زیادہ تجویز کردہ)
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └استعمال کرنے کے لیے پورٹ نمبر
│                 │            │
│                 │            └رابطہ کرنے کے لیے میزبان
│                 │
│                 └استعمال کرنے کے لیے ڈیٹا بیس کا نام
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├مخصوص کیٹلوجڈ ڈیٹا بیس کا حوالہ دے سکتا ہے
│               │
│               ├ایک میزبان اور پورٹ نمبر سے رابطہ کرسکتے ہیں
│               │
│               └اگر آپ اسے استعمال کرنا چاہتے ہیں تو آپ کو Oracle دستاویزات کا حوالہ دینا چاہیے
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├مخصوص کیٹلوجڈ ڈیٹا بیس کا حوالہ دے سکتا ہے
│         │
│         ├ایک میزبان اور پورٹ نمبر سے رابطہ کرسکتے ہیں
│         │
│         └اگر آپ اسے استعمال کرنا چاہتے ہیں تو آپ کو ODBC/DB2 دستاویزات کا حوالہ دینا چاہیے
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └استعمال کرنے کے لیے ڈیٹا بیس کا نام
│               │              │
│               │              └استعمال کرنے کے لیے پورٹ نمبر
│               │
│               └رابطہ کرنے کے لیے میزبان
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └استعمال کرنے کے لیے مقامی ڈیٹا بیس فائل کا راستہ
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └استعمال کرنے کے لیے ڈیٹا بیس کا نام
                   │         │
                   │         └استعمال کرنے کے لیے پورٹ نمبر
                   │
                   └رابطہ کرنے کے لیے میزبان
```

<div dir="rtl">اگر آپ اپنے DSN کو تبدیل کرنے کے بارے میں یقین نہیں رکھتے ہیں تو، کچھ بھی تبدیل کیے بغیر اسے استعمال کرنے کی کوشش کریں.<br /><br /></div>

<div dir="rtl"><code dir="ltr">pdo_username</code> اور <code dir="ltr">pdo_password</code> آپ کے صارف کے نام اور پاس ورڈ کی طرح ہونا چاہیے جو آپ نے اپنے ڈیٹا بیس کے لیے منتخب کیا ہے.<br /><br /></div>

#### <div dir="rtl"><a name="BLOCK_CRON"></a>CIDRAM cronjobs کو مسدود کررہا ہے؛ اس کو کیسے ٹھیک کریں؟<br /><br /></div>

<div dir="rtl">اگر آپ cronjobs کے لیے ایک سرشار فائل استعمال کر رہے ہیں، اگر عام صارف کی درخواستوں کے دوران اس فائل کو کال کرنے کی ضرورت نہیں ہے، اس بات کو یقینی بنانا کہ آپ کے cronjobs کے دوران CIDRAM پر عمل درآمد نہیں کیا جاتا ہے سب سے آسان حل ہے.<br /><br /></div>

<div dir="rtl">اگر یہ ممکن نہیں ہے، اگر آپ کے کرون سرور کا IP ایڈریس مستقل اور پیش گوئی ہے، اپنی مرضی کے مطابق دستخط فائل میں وائٹ لسٹ دستخط بنانے کی کوشش کریں، یا اس کو سفید کرنے کے لیے ایک معاون اصول بنانے کی کوشش کریں. اگر IP ایڈریس اکثر تبدیل ہوتا ہے لیکن اسی نیٹ ورک میں رہتا ہے، آپ اپنے <code dir="ltr">ignore.dat</code> میں اس فہرست کو روکنے کے لیے ذمہ دار دستخط والے حصے کا نام درج کرنے کی کوشش کرسکتے ہیں.<br /><br /></div>

<div dir="rtl">اگر آپ نے ان تمام آئیڈیوں کو آزمایا ہے اور ان میں سے کسی نے بھی آپ کے لیے کام نہیں کیا ہے، یا اگر آپ کو یہ جاننے میں مدد کی ضرورت ہو کہ اسے کیسے کریں، CIDRAM کے issues پیج پر ہم سے بات کریں.<br /><br /></div>

---


### <div dir="rtl">۹. <a name="SECTION9">قانونی معلومات</div>

#### <div dir="rtl">۹.۰ سیکشن پریامبل<br /><br /></div>

<div dir="rtl">دستاویزات کا یہ حصہ پیکج کے استعمال اور عمل کے بارے میں ممکنہ قانونی مفکوم بیان کرتا ہے، اور کچھ بنیادی متعلق معلومات فراہم کرتی ہے. بعض صارفین کے لیے شکایت کا یقین کرنے کے لیے یہ ممکن ہو سکتا ہے کہ وہ کسی بھی قانونی تقاضے کے ساتھ موجود ممالک میں موجود ہوسکتے ہیں جس میں وہ کام کرتے ہیں، اور کچھ صارفین اس کی معلومات کے مطابق اپنی ویب سائٹ کی پالیسیوں کو ایڈجسٹ کرنے کی ضرورت ہوسکتی ہے.<br /><br /></div>

<div dir="rtl">سب سے پہلے، سب سے اہم، یاد رکھیں کہ میں (پیکیج کا مصنف) ایک وکیل نہیں ہوں. لہذا، میں قانونی مشورہ فراہم کرنے کے لیے قانونی طور پر قابل نہیں ہوں. اس کے علاوہ، کچھ معاملات میں، قانونی ضروریات مختلف ممالک اور دائرہ کاروں کے درمیان مختلف ہوتی ہیں. یہ مختلف قانونی ضروریات کبھی کبھی متفق ہیں (مثلا، ایسے ممالک جو "رازداری کے حقوق" اور "بھول جانے کا حق"، ایسے ممالک کے مقابلے میں جو "ڈیٹا برقرار رکھنے" کا حق رکھتے ہیں). یہ بھی غور کریں کہ پیکیج تک رسائی مخصوص ممالک یا دائرہ کاروں سے محدود نہیں ہے, اور اس وجہ سے، پیکج کے صارفین جغرافیایی متنوع ہونے کا امکان رکھتے ہیں. ان پوائنٹس پر غور کیا گیا ہے، میں ایسی حیثیت میں نہیں ہوں جو یہ سب کے لیے "قانونی طور پر مطابق" ہونے کا مطلب ہے. تاہم، مجھے امید ہے کہ اس معلومات میں آپ کو یہ فیصلہ کرنے میں مدد ملتی ہے کہ پیکج کے تناظر میں قانونی طور پر مطابق رہنے کے لۓ آپ کو کیا کرنا ہوگا. اگر آپ کو کوئی شبہ ہے، یا اگر آپ کو قانونی نقطہ نظر سے اضافی مدد اور مشورہ کی ضرورت ہو تو، میں ایک قانونی پیشہ ورانہ مشاورت کی سفارش کروں گا.<br /><br /></div>

#### <div dir="rtl">۹.۱ ذمہ داری<br /><br /></div>

<div dir="rtl">پیکج کسی بھی وارنٹی کے ساتھ فراہم نہیں کی جاتی ہے (لائسنس پہلے ہی اس کا ذکر کرتا ہے). یہ ذمہ داری کے تمام مقاصد پر لاگو ہوتا ہے. پیکج آپ کی سہولت کے لیے فراہم کی جاتی ہے. امید ہے کہ یہ مفید ہو گا، اور یہ آپ کے لیے کچھ فائدہ فراہم کرے گا. تاہم، پیکج کا استعمال کرتے ہوئے یا لاگو آپ کا اپنا فیصلہ ہے. آپ اسے استعمال کرنے یا اسے لاگو کرنے پر مجبور نہیں ہوئے ہیں. جب آپ ایسا کرتے ہو تو، آپ اس فیصلے کے ذمہ دار ہیں. میں اور دوسرا پیکج شراکت دار، آپ کے فیصلوں کے نتائج کے لیے قانونی طور پر ذمہ دار نہیں ہے.<br /><br /></div>

#### <div dir="rtl">۹.۲ تیسرے فریقوں<br /><br /></div>

<div dir="rtl">اس پیکیج پر منحصر ہے کہ کس طرح پیکج کنفگریشن اور لاگو ہوتا ہے، کچھ صورتو میں، یہ تیسری جماعتوں کے ساتھ معلومات کا اشتراک کرسکتا ہے. کچھ قواعد و ضوابط میں، کچھ دائرہ کار کی طرف سے، یہ "ذاتی طور پر شناختی معلومات" کے طور پر بیان کیا جا سکتا ہے.<br /><br /></div>

<div dir="rtl">تیسری جماعتوں کی طرف سے یہ معلومات کس طرح استعمال کی جاتی ہے، ان کی پالیسیوں کے تابع ہے، اور اس دستاویزات کے دائمے سے باہر ہے. تاہم، اس طرح کے معاملات میں، معلومات کا اشتراک معذور ہوسکتا ہے. اس طرح کے معاملات میں، اگر آپ اسے چالو کرنے کا انتخاب کرتے ہیں تو، یہ آپ کی ذمہ داری ہے کہ آپ کو ان خدشات کے بارے میں معلومات کی رازداری، سیکورٹی اور استعمال کے بارے میں کوئی خدشات کی تحقیقات کی جا سکتی ہے. اگر کوئی شبہ موجود ہے، یا اگر آپ ان تیسری جماعتوں کے انعقاد سے ناخوش ہیں تو، ان تیسری جماعتوں کے ساتھ معلومات کے تمام حصول کو غیر فعال کرنے میں یہ سب سے بہتر ہوسکتا ہے.<br /><br /></div>

<div dir="rtl">شفافیت کے مقصد کے لیے، مشترکہ معلومات کی قسم ذیل میں بیان کی گئی ہے.<br /><br /></div>

##### <div dir="rtl">۹.۲.۰ میزبان نام تلاش کریں<br /><br /></div>

<div dir="rtl">اگر آپ میزبانوں کے ساتھ کام کرنے کے لیے کسی بھی خصوصیات یا ماڈیولز کا استعمال کرتے ہیں تو، CIDRAM انباؤنڈ درخواستوں کے میزبان نام حاصل کرنے کے قابل ہوسکتا ہے. عام طور پر، یہ ایک DNS سرور سے IP ایڈریس کے میزبان ناموں کی درخواست کرکے یہ کرتا ہے، یا براہ راست نظام کی طرف سے فراہم کی گئی فعالیت کے ذریعے معلومات کی درخواست کی طرف سے. <a href="https://dns.google.com/">Google DNS</a> سروس پہلے سے طے شدہ طور پر مقرر کیا جاتا ہے (لیکن یہ کنفگریشن کے ذریعے آسانی سے تبدیل کیا جا سکتا ہے). مطابقت پزیر خدمات کے ساتھ مطابقت پذیری کی جا سکتی ہے، اور ان پر منحصر ہے کہ آپ کس طرح پیکج کو کنفگریشن دیں گے. نظام کے ذریعے براہ راست درخواست کرتے وقت، آپ کو اپنے نظام کے منتظم سے رابطہ کرنے کی ضرورت پڑے گی جس کا تعین کیا جاسکتا ہے. متاثر ماڈیولز سے بچنے یا اس کے مطابق پیکیج کنفگریشن میں ترمیم کرکے CIDRAM میں ہوسٹ نام کی تلاش کی جا سکتی ہے.<br /><br /></div>

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">allow_gethostbyaddr_lookup</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">default_dns</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">force_hostname_lookup</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">other</code> &lt;- <code dir="ltr">verification</code></li>
 <li><code dir="ltr">search_engines</code> &lt;- <code dir="ltr">verification</code></li>
 <li><code dir="ltr">social_media</code> &lt;- <code dir="ltr">verification</code></li>
</ul></div>

##### <div dir="rtl">۹.۲.۱ تلاش انجن اور سوشل میڈیا کی توثیق<br /><br /></div>

<div dir="rtl">جب یہ اختیارات فعال ہوتے ہیں تو، CIDRAM کو تلاش کے انجن اور سوشل میڈیا کی درخواستوں کی صداقت کی توثیق کرنے کی کوشش ہوتی ہے. ایسا کرنے کے لیے، یہ ان پونڈ درخواستوں کے میزبانوں سے IP پتوں کو حل کرنے کی کوشش کرنے کے لیے <a dir="ltr" href="https://dns.google.com/">Google DNS</a> سروس کا استعمال کرتا ہے (اس عمل میں، ان بے حد درخواستوں کے میزبانوں کو سروس کے ساتھ اشتراک کیا جاتا ہے).<br /><br /></div>

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">other</code> &lt;- <code dir="ltr">verification</code></li>
 <li><code dir="ltr">search_engines</code> &lt;- <code dir="ltr">verification</code></li>
 <li><code dir="ltr">social_media</code> &lt;- <code dir="ltr">verification</code></li>
</ul></div>

##### <div dir="rtl">۹.۲.۲ CAPTCHA<br /><br /></div>

<div dir="rtl">hCaptcha پیکیج کے ذریعہ تعاون یافتہ ہیں. ان کو صحیح طریقے سے کام کرنے کے لیے API کیز کی ضرورت ہوتی ہے. وہ بطور ڈیفالٹ غیر فعال ہیں، لیکن مطلوبہ API چابیاں تشکیل دے کر ان کو فعال کیا جاسکتا ہے. جب فعال ہوجائے تو، خدمت اور CIDRAM یا صارف کے براؤزر کے مابین مواصلت ہوسکتی ہے. اس میں ممکنہ طور پر بات چیت کرنے والی معلومات شامل ہوسکتی ہے جیسے صارف کا IP ایڈریس، صارف ایجنٹ، آپریٹنگ سسٹم، اور دیگر تفصیلات.<br /><br /></div>

##### <div dir="rtl">۹.۲.۳ STOP FORUM SPAM<br /><br /></div>

<div dir="rtl"><a dir="ltr" href="https://www.stopforumspam.com/">Stop Forum Spam</a> ایک شاندار، آزادانہ طور پر دستیاب سروس ہے جو اسپیمرز سے فورمز، بلاگز، اور ویب سائٹس کی حفاظت کے لیے مدد کرسکتا ہے. یہ یہ معروف اسپیمرز کے ایک ڈیٹا بیس فراہم کر کے کرتا ہے، اور ایک API جو لیورڈج کیا جا سکتا ہے کہ یہ چیک کرنے کے لیے کہ آیا IP ایڈریس، صارف کا نام، یا ای میل ایڈریس اس کے ڈیٹا بیس پر درج کیا جاتا ہے.<br /><br /></div>

<div dir="rtl">CIDRAM ایک ماڈیول فراہم کرتا ہے جو اس API کو چیک کرنے کے لۓ لیتا ہے کہ آیا درخواستوں کا IP ایڈریس مشتبہ اسپیمر سے تعلق رکھتا ہے. جب ماڈیول انسٹال اور چالو ہوجاتا ہے، صارف IP پتے کو خدمت کے ساتھ اشتراک کیا جا سکتا ہے، ماڈیول کی کنفگریشن اور مطلوبہ مقصد کے مطابق.<br /><br /></div>

##### <div dir="rtl">۹.۲.۴ ABUSEIPDB<br /><br /></div>

<div dir="rtl"><a dir="ltr" href="https://www.abuseipdb.com/">AbuseIPDB</a> API کا استعمال کرتے ہوئے بدسلوکی IP پتے کو بلاک کرنے کے لیے CIDRAM ایک اختیاری ماڈیول فراہم کرتا ہے. جب ماڈیول انسٹال اور چالو ہوجاتا ہے، صارف IP پتے کو خدمت کے ساتھ اشتراک کیا جا سکتا ہے، ماڈیول کی کنفگریشن اور مطلوبہ مقصد کے مطابق.<br /><br /></div>

##### <div dir="rtl">۹.۲.۵ BGPVIEW, IP-API<br /><br /></div>

<div dir="rtl"><a dir="ltr" href="https://bgpview.io/">BGPView</a> API اور <a dir="ltr" href="https://ip-api.com/">IP-API</a> API کا استعمال کرتے ہوئے ASN اور ملکی کوڈ تلاش کرنے کے لیے CIDRAM لیے اختیاری ماڈیول فراہم کرتا ہے. یہ تلاشیں اپنے ASN یا ملک کے اصل کی بنیاد پر درخواستوں کو مسدود کرنے یا وائٹ لسٹ کرنے کی اہلیت فراہم کرتی ہیں. جب ماڈیول انسٹال اور چالو ہوجاتا ہے، صارف IP پتے کو خدمت کے ساتھ اشتراک کیا جا سکتا ہے، ماڈیول کی کنفگریشن اور مطلوبہ مقصد کے مطابق.<br /><br /></div>

##### <div dir="rtl">۹.۲.۶ PROJECT HONEYPOT<br /><br /></div>

<div dir="rtl"><a dir="ltr" href="https://www.projecthoneypot.org/">Project Honeypot</a> API کا استعمال کرتے ہوئے بدسلوکی IP پتے کو بلاک کرنے کے لیے CIDRAM ایک اختیاری ماڈیول فراہم کرتا ہے. جب ماڈیول انسٹال اور چالو ہوجاتا ہے، صارف IP پتے کو خدمت کے ساتھ اشتراک کیا جا سکتا ہے، ماڈیول کی کنفگریشن اور مطلوبہ مقصد کے مطابق.<br /><br /></div>

#### <div dir="rtl">۹.۳ لاگ<br /><br /></div>

<div dir="rtl">لاگنگ کئی وجوہات کے لیے CIDRAM کا ایک اہم حصہ ہے. اس کے بغیر، غلطیوں کو تلاش کرنے اور مسائل کی تشخیص مشکل ہوسکتی ہے. اگر ہمارے پاس یہ معلومات نہیں ہے اور کسی چیز کو تبدیل کرنے کی ضرورت ہے، یہ جاننا مشکل ہوسکتا ہے کہ بالکل وہی چیز جو تبدیل کرنے کی ضرورت ہے. اس کے باوجود، ہر کوئی اس معلومات کو ریکارڈ نہیں کرنا چاہتا، لہذا یہ اختیاری رہتا ہے. CIDRAM میں، یہ ڈیفالٹ کی طرف سے معذور ہے. اسے فعال کرنے کے لیے، CIDRAM کے مطابق کنفگریشن دیا جانا چاہیے.<br /><br /></div>

<div dir="rtl">یہ یاد رکھنا چاہیے کہ لاگنگ کے لیے عین مطابق قانونی ضروریات دائرہ کاروں کے درمیان مختلف ہو سکتی ہیں. عملدرآمد کا تناظر بھی متعلقہ ہو سکتا ہے (مثال کے طور پر، ایک فرد کے طور پر، ایک کارپوریٹ ادارے کے طور پر، تجارتی بنیاد پر، غیر تجارتی بنیاد پر، وغیرہ). اس کی وجہ سے، یہاں کی معلومات آپ کے لیے مفید ہوسکتی ہے.<br /><br /></div>

<div dir="rtl">بہت سے مختلف قسم کی معلومات درج کی جا سکتی ہیں، مختلف وجوہات کے لیے.<br /><br /></div>

##### <div dir="rtl">۹.۳.۰ بلاک کے واقعات<br /><br /></div>

<div dir="rtl">لاگ کا بنیادی قسم جس میں CIDRAM انجام دیتا ہے "بلاک کے واقعات" سے متعلق ہے. اس سے متعلق ہے کہ جب CIDRAM کسی درخواست کو روکتا ہے، اور تین مختلف فارمیٹس میں فراہم کی جاسکتی ہے:<br /></div>
<div dir="rtl"><ul>
 <li>لاگ جو انسان کی طرف سے پڑھ سکتے ہیں.</li>
 <li>Apache سٹائل لاگ.</li>
 <li>سیریلائزڈ لاگ.</li>
</ul></div>

<div dir="rtl">جب ریکارڈ کیا جاتا ہے تو لوگ پڑھ سکتے ہیں، ایک بلاک ایونٹ عام طور پر اس طرح لگ رہا ہے (ایک مثال کے طور):<br /><br /></div>

<pre dir="rtl">
ID: <code dir="ltr">1234</code>
اسکرپٹ ورژن: <code dir="ltr">CIDRAM v1.6.0</code>
تاریخ وقت: <code dir="ltr">Day, dd Mon 20xx hh:ii:ss +0000</code>
IP پتہ: <code dir="ltr">x.x.x.x</code>
میزبان کا نام: <code dir="ltr">dns.hostname.tld</code>
دستخط شمار: <code dir="ltr">1</code>
دستخط حوالہ: <code dir="ltr">x.x.x.x/xx</code>
کیوں بلاک شدہ: کلاؤڈ سروس ("نیٹ ورک کا نام", <code dir="ltr">Lxx:Fx</code>, <code dir="ltr">[XX]</code>)!
صارف ایجنٹ: <code dir="ltr">Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36</code>
دوبارہ تعمیر URI: <code dir="ltr">https://your-site.tld/index.php</code>
CAPTCHA کے ریاست: فعال کردہ.
</pre>

<div dir="rtl">وہی چیز، جو اپاچی کے انداز میں درج ہوئی ہے، اس کی طرح لگتا ہے:<br /><br /></div>

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

<div dir="rtl">ریکارڈ شدہ تقریب عام طور پر اس معلومات میں شامل ہے:<br /></div>
<div dir="rtl"><ul>
 <li>ایونٹ کے لیے ایک ID نمبر.</li>
 <li>CIDRAM کا ورژن فی الحال استعمال کیا جاتا ہے.</li>
 <li>واقعہ پیش کی تاریخ اور وقت.</li>
 <li>درخواست سے IP ایڈریس.</li>
 <li>درخواست کے میزبان نام (جب دستیاب ہو).</li>
 <li>دستخط کی تعداد متاثر.</li>
 <li>ان دستخط کے بارے میں مزید تفصیلات.</li>
 <li>ایونٹ اور متعلقہ معلومات کی وجوہات.</li>
 <li>درخواست کے لیے "صارف ایجنٹ".</li>
 <li>درخواست کردہ وسائل کے لیے شناخت.</li>
 <li>درخواست کے لیے CAPTCHA کی حیثیت (جب متعلقہ).</li>
 <li></li>
</ul></div>

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">apache_style_log</code> &lt;- <code dir="ltr">logging</code></li>
 <li><code dir="ltr">serialised_log</code> &lt;- <code dir="ltr">logging</code></li>
 <li><code dir="ltr">standard_log</code> &lt;- <code dir="ltr">logging</code></li>
</ul></div>

<div dir="rtl">جب یہ ہدایات خالی رہیں تو، اس قسم کی ریکارڈنگ غیر فعال رہیں گے.<br /><br /></div>

##### <div dir="rtl">۹.۳.۱ CAPTCHA لاگ<br /><br /></div>

<div dir="rtl">جب ایک صارف CAPTCHA مثال کے طور پر مکمل کرنے کی کوشش کرتا ہے، تو ریکارڈ کیا جاتا ہے.<br /><br /></div>

<div dir="rtl">ان ریکارڈوں میں صارف کے IP ایڈریس، تاریخ اور اس وقت کا واقعہ شامل ہے، اور حیثیت. یہ ریکارڈ عام طور پر اس طرح نظر آتے ہیں:<br /><br /></div>

```
IP پتہ: x.x.x.x - تاریخ وقت: Day, dd Mon 20xx hh:ii:ss +0000 - CAPTCHA کے ریاست: ایوان کے پاس!
```

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">hcaptcha_log</code> &lt;- <code dir="ltr">hcaptcha</code></li>
</ul></div>

##### <div dir="rtl">۹.۳.۲ سامنے کے آخر لاگ<br /><br /></div>

<div dir="rtl">یہ سامنے کے آخر میں لاگ ان کرنے کی کوشش کرنے سے متعلق ہے. جب سامنے کے آخر میں رسائی کو فعال کیا جاتا ہے، جب صارف کو سامنے کے آخر میں لاگ ان کرنے کی کوشش ہوتی ہے، تو ریکارڈ کیا جاتا ہے.<br /><br /></div>

<div dir="rtl">اس ریکارڈ میں صارف کے IP ایڈریس، تاریخ اور وقت اور اس کے نتائج شامل ہیں (کامیاب یا ناکامی). یہ عام طور پر اس طرح کچھ نظر آتا ہے:<br /><br /></div>

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - لاگ ان.
```

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">frontend_log</code> &lt;- <code dir="ltr">frontend</code></li>
</ul></div>

##### <div dir="rtl">۹.۳.۳ لاگ گھومنے<br /><br /></div>

<div dir="rtl">آپ چاہتے ہیں، یا قانونی طور پر ہو سکتا ہے، کچھ وقت کے بعد لاگ ان کو صاف کرنے کے لیے (کتنی دیر تک آپ لاگ ان کو برقرار رکھ سکتے ہیں قانون کی طرف سے محدود ہوسکتے ہیں). یہ لاگ ان کے مطابق لاگ ان کی کنفگریشن میں تاریخ/وقت مارکر مقرر کرنے کی طرف سے کیا جا سکتا ہے (مثال کے طور پر، <code dir="ltr">{yyyy}-{mm}-{dd}.log</code>)، اور پھر لاگ گرد گھومنے کو چالو کرنے (لاگ گرد کی گردش آپ کو لاگ ان کی حد سے زیادہ حد تک زیادہ سے زیادہ لاگ ان پر لاگو کرنے کی اجازت دیتا ہے).<br /><br /></div>

<div dir="rtl">مثال کے طور پر: اگر مجھے 30 دنوں کے بعد لاگز کو خارج کرنے کی ضرورت ہوتی ہے تو میں <code dir="ltr">{dd}.log</code> اپنے لاگ ان کے نام میں ڈال سکتا ہوں (<code dir="ltr">{dd}</code> دن کی نمائندگی کرتا ہے)، <code dir="ltr">log_rotation_limit</code> کو 30 مقرر کریں، اور <code dir="ltr">log_rotation_action</code> کو <code dir="ltr">Delete</code> مقرر کریں.<br /><br /></div>

<div dir="rtl">اگر آپ کو کچھ وقت کے لیے ریکارڈ رکھنے کی ضرورت ہے تو، آپ کو لاگ گرد گھومنے کا استعمال نہ کرنے کا انتخاب کرسکتے ہیں، یا آپ <code dir="ltr">log_rotation_action</code> کی قدر <code dir="ltr">Archive</code> پر مقرر کر سکتے ہیں (اس ریکارڈ کو کمپیکٹ کریں گے، اس طرح ڈسک کے استعمال کو کم کرنا ہوگا).<br /><br /></div>

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">log_rotation_action</code> &lt;- <code dir="ltr">logging</code></li>
 <li><code dir="ltr">log_rotation_limit</code> &lt;- <code dir="ltr">logging</code></li>
</ul></div>

##### <div dir="rtl">۹.۳.۴ ٹرنک لاگ<br /><br /></div>

<div dir="rtl">اگر آپ چاہتے ہیں تو، آپ انفرادی ریکارڈز کو چھوٹ سکتے ہیں جب وہ مخصوص سائز سے کہیں زیادہ ہیں.<br /><br /></div>

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">truncate</code> &lt;- <code dir="ltr">logging</code></li>
</ul></div>

##### <div dir="rtl">۹.۳.۵ IP ایڈریس PSEUDONYMISATION<br /><br /></div>

<div dir="rtl">سب سے پہلے، اگر آپ اصطلاح سے واقف نہیں ہیں، "pseudonymisation" ذاتی اعداد و شمار کی پروسیسنگ سے مراد اس طرح سے ہے کہ یہ کسی بھی مخصوص شخص کو بغیر کسی ضمنی معلومات کی نشان دہی نہیں کی جاسکتی ہے، فراہم کی جاتی ہے کہ اس طرح کی اضافی معلومات علاحدہ طریقے سے برقرار رکھی جاتی ہے اور تکنیکی اور تنظیمی تدابیر کے تابع ہوتے ہیں اس بات کو یقینی بنانے کے لیے کہ ذاتی ڈیٹا کسی قدرتی شخص کو نشان دہی نہیں کی جاسکتی ہے.<br /><br /></div>

<div dir="rtl">مندرجہ ذیل وسائل اس سے مزید تفصیل میں وضاحت کرنے میں مدد کرسکتے ہیں:</div>
<div dir="rtl"><ul>
 <li><a dir="ltr" href="https://www.trust-hub.com/news/what-is-pseudonymisation/">[trust-hub.com] What is pseudonymisation?</a></li>
 <li><a dir="ltr" href="https://en.wikipedia.org/wiki/Pseudonymization">[Wikipedia] Pseudonymization</a></li>
</ul></div>

<div dir="rtl">کچھ حالات میں، آپ کو کسی بھی PII جمع، عملدرآمد، یا ذخیرہ کرنے کے لیے "anonymisation" یا "pseudonymisation" کو لاگو کرنا قانونی طور پر ضروری ہوسکتا ہے. یہ تصور ابھی کچھ وقت تک وجود میں آیا ہے، لیکن GDPR/DSGVO خاص طور پر "pseudonymisation" کا ذکر اور حوصلہ افزائی کرتا ہے.<br /><br /></div>

<div dir="rtl">اگر آپ چاہتے ہیں تو، CIDRAM لاگ ان کرتے وقت لاگ ان کرتے وقت IP پتے کے لیے یہ کر سکتے ہیں. جب لکھنا لکھنا، IPv4 پتے کے آخری آکٹیٹ اور IPv6 پتے کے دوسرے حصے کے بعد سب کچھ، "x" کی طرف سے نمائندگی کی جائے گی.<br /><br /></div>

<div dir="rtl"><em>نوٹ: CIDRAM کی IP ٹریکنگ کی خصوصیت اس کی صلاحیت نہیں ہے. اگر یہ آپ کے لیے ایک مسئلہ ہے، IP ٹریکنگ کو مکمل طور پر غیر فعال کرنے کے لیے یہ سب سے بہتر ہو سکتا ہے.</em><br /><br /></div>

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">pseudonymise_ip_addresses</code> &lt;- <code dir="ltr">legal</code></li>
</ul></div>

##### <div dir="rtl">۹.۳.۶ لاگ ان معلومات کو چھوڑ دیں<br /><br /></div>

<div dir="rtl">اگر آپ مخصوص قسم کی معلومات کو مکمل طور پر لاگ ان کرنے سے روکنا چاہتے ہیں تو، آپ ایسا کرسکتے ہیں. کنفیگریشن پیج پر، براہ کرم <code dir="ltr">fields</code> کنفیگریشن ڈائریکٹیو سے رجوع کریں تاکہ یہ کنٹرول کیا جا سکے کہ کون سے فیلڈز لاگ انٹریز میں ظاہر ہوتے ہیں اور "رسائی نہیں ہوئی" صفحہ پر.<br /><br /></div>

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

<div dir="rtl"><em>نوٹ: IP پتے کے لیے pseudonymisation کا استعمال کرنے کی کوئی وجہ نہیں ہے جب IP پتے کو مکمل طور پر لاگ ان سے لے کر.</em><br /><br /></div>

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">fields</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">۹.۳.۷ اعداد و شمار<br /><br /></div>

<div dir="rtl">CIDRAM اعداد و شمار کو ٹریک کر سکتے ہیں، جیسے کہ کسی مخصوص وقت سے کتنے بلاک واقعات یا CAPTCHA مثال موجود ہیں. یہ خصوصیت ڈیفالٹ کے ذریعہ غیر فعال ہے، لیکن پیکیج کی کنفگریشن کے ذریعے فعال کیا جا سکتا ہے. یہ خصوصیت صرف واقعات کی تعداد کو ٹریک کرتا ہے. اس میں کوئی مخصوص معلومات شامل نہیں ہے، لہذا اسے PII کے طور پر نہیں جانا چاہیے.<br /><br /></div>

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">statistics</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">۹.۳.۸ خفیہ کاری<br /><br /></div>

<div dir="rtl">CIDRAM اس کے لاگ ان یا کیش کو خفیہ نہیں کرتا. یہ مستقبل میں متعارف کرایا جا سکتا ہے، لیکن فی الحال اس کی کوئی مخصوص منصوبہ نہیں ہے. اگر آپ غیر قانونی شدہ تیسری جماعتوں کے بارے میں فکر مند ہیں تو CIDRAM میں حساس معلومات تک رسائی حاصل ہے، میں سفارش کرتا ہوں کہ عام طور پر قابل رسائی مقام پر CIDRAM انسٹال نہیں کیا جائے گا (مثال کے طور پر، <code dir="ltr">public_html</code> میں انسٹال نہ کریں) اور اس بات کو یقینی بنائیں کہ مناسب حد تک محدود پابندیوں کو نافذ کیا جائے. اگر یہ آپ کے خدشات کو حل کرنے کے لیے کافی نہیں ہے تو پھر CIDRAM کو کنفگریشن دیں تاکہ حساس معلومات جمع نہیں کی جائے گی (جیسے جیسے، لاگ ان کو غیر فعال کرکے).<br /><br /></div>

#### <div dir="rtl">۹.۴ کوکی<br /><br /></div>

<div dir="rtl">CIDRAM کو دو مقامات پر کوکیز کا تعین کرتا ہے. سب سے پہلے، CAPTCHA مکمل کرنے کے بعد "CIDRAM" کوکیز سیٹ کرتا ہے (اگر <code dir="ltr">lockuser</code> کو <code dir="ltr">true</code> میں مقرر کیا جاتا ہے تو)، لہذا یہ ہر درخواست پر ایسا کرنے کے لیے صارف سے پوچھنا جاری رکھنے کی ضرورت نہیں ہوگی. دوسرا، صارف کو سامنے کے آخر میں لاگ ان ہونے پر CIDRAM ایک کوکی سیٹ کرتا ہے (تصدیق کے مقاصد کے لیے).<br /><br /></div>

<div dir="rtl">دونوں صورتوں میں، صارف کو پہلے سے ہی کوکیز کے بارے میں خبردار کیا جاتا ہے. کوکیز کہیں اور نہیں بنائے جاتے ہیں.<br /><br /></div>

<div dir="rtl">نوٹ: "پوشیدہ" CAPTCHA APIs کو کچھ علاقوں میں کوکی قوانین سے مطابقت نہیں ہوسکتی ہے اور ایسے قوانین کے تابع کسی بھی ویب سائٹ سے ان کو پرہیز کرنا چاہیے. اس کے بجائے دوسرے فراہم کردہ API استعمال کرنے کا انتخاب کرنا، یا صرف مکمل طور پر CAPTCHA کو غیر فعال کرنا بہتر ہوگا.<br /><br /></div>

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">lockuser</code> &lt;- <code dir="ltr">hcaptcha</code></li>
 <li><code dir="ltr">api</code> &lt;- <code dir="ltr">hcaptcha</code></li>
</ul></div>

#### <div dir="rtl">۹.۵ مارکیٹنگ اور اشتہارات<br /><br /></div>

<div dir="rtl">CIDRAM مارکیٹنگ یا اشتہارات کے مقاصد کے لیے کسی بھی معلومات جمع یا عمل نہیں کرتا ہے. یہ کسی جمع کردہ یا لاگ ان معلومات سے کوئی فائدہ نہیں فروخت کرتا ہے. CIDRAM ایک تجارتی ادارہ نہیں ہے، اور کسی بھی تجارتی مفادات سے متعلق نہیں ہے، لہذا ان کاموں کو کوئی احساس نہیں ہوگا. اس منصوبے کی شروعات کے بعد یہ معاملہ رہا ہے، اور آج ہی مقدمہ جاری ہے.<br /><br /></div>

#### <div dir="rtl">۹.۶ رازداری کی پالیسی<br /><br /></div>

<div dir="rtl">بعض اوقات آپ کو قانون کی طرف سے آپ کی ویب سائٹ پر اپنی جگہ پر اپنی رازداری کی پالیسی پر ایک لنک ظاہر کرنے کی ضرورت ہوسکتی ہے. اس بات کو یقینی بنانے کے لیے صارفین کو آپ کی رازداری کے طریقوں کے بارے میں مطلع کیا جاسکتا ہے، جو آپ جمع کرتے ہیں، اور آپ اس معلومات کے ساتھ کیا کرتے ہیں. CIDRAM کے "رسائی نہیں ہوئی" کے صفحے پر اس لنک کو شامل کرنے کے قابل ہونے کے لۓ، آپ کی رازداری کی پالیسی کے ایڈریس کی وضاحت کرنے کے لیے ایک کنفگریشن کا اختیار فراہم کیا جاتا ہے.<br /><br /></div>

<div dir="rtl">نوٹ: یہ سختی سے سفارش کی جاتی ہے کہ آپ کی رازداری کی پالیسی کا صفحہ CIDRAM کی حفاظت کے پیچھے نہیں ہے. اگر CIDRAM آپ کی پرائیویسی پالیسی کی حفاظت کرتا ہے تو، جب وہ آپ کی رازداری کی پالیسی پر لنک پر کلک کریں تو صارفین کو مسدود کیا جائے گا. مثالی طور پر، آپ کو اپنی رازداری کی پالیسی کی ایک مستحکم کاپی، جیسے HTML صفحہ یا سادہ متن فائل سے منسلک ہونا چاہیے.<br /><br /></div>

<div dir="rtl">متعلقہ کنفگریشن ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">privacy_policy</code> &lt;- <code dir="ltr">legal</code></li>
</ul></div>

#### <div dir="rtl">۹.۷ GDPR/DSGVO<br /><br /></div>

<div dir="rtl">GDPR یورپی یونین کا ایک ضابطہ ہے جو 25 مئی، 2018 تک اثر انداز ہوتا ہے. ریگولیشن کا بنیادی مقصد یہ ہے کہ یورپی یونین کے شہریوں اور باشندوں کو ان کے اپنے ذاتی ڈیٹا سے متعلق قابو پانے، اور پرائیویٹ اور ذاتی ڈیٹا کے بارے میں یورپی یونین کے اندر ریگولیشن کو متحد کرنا.<br /><br /></div>

<div dir="rtl">ریگولیشن کسی بھی EU کے "اعداد و شمار کے مضامین" (کسی بھی شناخت یا شناختی قدرتی شخص) کے "ذاتی طور پر شناختی معلومات" کی پروسیسنگ سے متعلق مخصوص اجزاء پر مشتمل ہے. تعمیل کرنے کے لیے، کمپنیوں، عمل، اور متعلقہ نظام، "ڈیزائن کی طرف سے رازداری" کو لاگو کرنا لازمی ہے، سب سے زیادہ ممکن راز رازداری کی کنفگریشنات کا استعمال کرنا ضروری ہے، کسی ذخیرہ یا پروسیسنگ معلومات کے لیے حفاظتی انتظامات کو لاگو کرنا ضروری ہے (بشمول، لیکن تک محدود نہیں، "pseudonymisation" اور "anonymisation")، واضح طور پر ان اعداد و شمار کی اقسام کا اعلان کرنا چاہیے جو وہ جمع کرتے ہیں، وہ کس طرح کے سببوں کے لیے، اس کے عمل کو کس طرح، وہ کتنی عرصے تک اسے برقرار رکھتی ہیں، اور اگر وہ اس ڈیٹا کو کسی بھی تیسری پارٹی کے ساتھ شریک کریں، اعداد و شمار کی اقسام، کیسے، کیوں، اور اسی طرح کی اقسام.<br /><br /></div>

<div dir="rtl">اعداد و شمار پر عملدرآمد نہیں کیا جاسکتا جب تک کہ ایسا کرنے کے لیے قانونی بنیاد نہ ہو، قواعد و ضوابط کے مطابق. عام طور پر، اس کا مطلب یہ ہے کہ یہ قانونی ذمہ داریوں کے مطابق ہونا ضروری ہے، اور صرف واضح ہونے کے بعد، اچھی طرح سے مطلع رضامندی کے اعداد و شمار سے حاصل کی گئی ہے.<br /><br /></div>

<div dir="rtl">وقت میں، قوانین تبدیل کر سکتے ہیں. لہذا، پرانے معلومات کو پھیلانے سے بچنے کے لۓ، یہ مستند ذریعہ سے سیکھنا بہتر ہوگا. اگر میں براہ راست یہاں معلومات شامل ہوں تو، یہ تاریخ سے باہر ہوسکتا ہے.<br /><br /></div>

<div dir="rtl">مزید معلومات سیکھنے کے لیے کچھ سفارش کردہ وسائل:<br /></div>
<div dir="rtl"><ul>
 <li><a href="https://ur.wikipedia.org/wiki/%D8%AC%D9%86%D8%B1%D9%84_%DA%88%DB%8C%D9%B9%D8%A7_%D9%BE%D8%B1%D9%88%D9%B9%DB%8C%DA%A9%D8%B4%D9%86_%D8%B1%DB%8C%DA%AF%D9%88%D9%84%DB%8C%D8%B4%D9%86">جنرل ڈیٹا پروٹیکشن ریگولیشن</a></li>
 <li><a href="https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679">REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL</a></li>
</ul></div>

---


### <div dir="rtl">۱۰. <a name="SECTION10"></a>پچھلے بڑے ورژن سے اپ گریڈ کرنا</div>

#### <div dir="rtl">۱۰.۰ CIDRAM v3 میں اپ گریڈ کرنا<br /><br /></div>

<div dir="rtl">v3 اور پچھلے بڑے ورژن کے درمیان اہم فرق ہیں. جس طرح سے انٹری پوائنٹس کام کرتے ہیں، جس طرح سے ماڈیولز کی ساخت ہوتی ہے، اور جس طرح سے اپڈیٹر v3 کے لیے کام کرتا ہے وہ اس طرح سے مختلف ہے جس طرح ان چیزوں نے پچھلے بڑے ورژنز کے لیے کام کیا. ان اختلافات کی وجہ سے، پچھلے بڑے ورژنز سے v3 میں اپ گریڈ کرنے کا بہترین طریقہ یہ ہوگا کہ ایک تازہ انسٹالیشن انجام دی جائے.<br /><br /></div>

<div dir="rtl">اگر آپ اپنی کنفگریشن اور اپنے معاون قواعد کو برقرار رکھنا چاہتے ہیں، اپ گریڈ کا عمل شروع کرنے سے پہلے، فرنٹ اینڈ بیک اپ پیج پر جائیں. وہاں سے، کنفگریشن اور معاون قواعد برآمد کیے جا سکتے ہیں. برآمد کرنے سے فائل ڈاؤن لوڈ ہو جائے گی. نئے بڑے ورژن میں اپ گریڈ کرنے کے بعد، اس فائل کو پہلے سے برآمد شدہ ڈیٹا کو انسٹالیشن میں درآمد کرنے کے لیے استعمال کیا جا سکتا ہے.<br /><br /></div>

<div dir="rtl">ماڈیولز کی ساخت میں تبدیلیوں کی وجہ سے، پچھلے بڑے ورژنز کے لیے بنائے گئے ماڈیولز کو v3 کے لیے صحیح طریقے سے کام کرنے کے لیے دوبارہ لکھنے کی ضرورت ہوگی. براہ راست منتقلی کام نہیں کرے گی. واقعات کا بھی یہی حال ہے.<br /><br /></div>

<div dir="rtl">دستخطی فائلوں کے ڈھانچے کا طریقہ تبدیل نہیں ہوا ہے، اس لیے دستخطی فائلیں جو پچھلے بڑے ورژن کے لیے ہیں، بغیر کسی پریشانی کے براہ راست v3 میں منتقل کی جا سکتی ہیں.<br /><br /></div>

<div dir="rtl">ماڈیولز، دستخطی فائلیں، اور ایونٹس میں سے ہر ایک کی اپنی مخصوص ڈائریکٹریز ہوتی ہیں، جو کہ v3 کے بعد ایک نیا اضافہ ہے (لہذا، v3 کے لیے، وہ ہر ایک vault کی جڑ کے بجائے اپنی اپنی مخصوص ڈائریکٹریوں میں جائیں گے).<br /><br /></div>

<div dir="rtl">پچھلے بڑے ورژنز کے لیے عوامی طور پر دستیاب دستخطی فائلوں، ماڈیولز، اور بلاک لسٹوں میں سے کچھ کو فرسودہ کر دیا گیا ہے، اس لیے ہر چیز v3 کے لیے دستیاب نہیں ہوگی. زیادہ تر معاملات میں، v3 کے بعد سے شامل کردہ نئی خصوصیات اور بنیادی فعالیت کی وجہ سے، بہرحال ان کی ضرورت نہیں ہوگی.<br /><br /></div>

<div dir="rtl">معاون قوانین کے ڈھانچے کے طریقے میں کچھ ٹھیک ٹھیک تبدیلیاں ہیں، اور کنفگریشن میں تبدیلیاں ہیں، لیکن اگر آپ فرنٹ اینڈ بیک اپ صفحہ پر درآمد/برآمد خصوصیت استعمال کرتے ہیں، تو آپ کو دستی طور پر کچھ کرنے کی ضرورت نہیں ہوگی. درآمد کرتے وقت، CIDRAM جانتا ہے کہ کس چیز کی ضرورت ہے، اور اسے آپ کے لیے خود بخود سنبھال لے گا.<br /><br /></div>

<div dir="rtl">v3 کے ذریعے متعارف کرائی گئی تبدیلیوں کی فہرست کے لیے (مثال کے طور پر شامل کردہ خصوصیات، خصوصیات کو ہٹایا گیا، وغیرہ)، <a href="https://github.com/CIDRAM/CIDRAM/blob/v3/Changelog.md#v300">v3 چینج لاگ</a> سے رجوع کریں.<br /><br /></div>

#### <div dir="rtl">۱۰.۱ CIDRAM v3 سے پہلے والے ورژن سے CIDRAM v4 میں اپ گریڈ کرنا<br /><br /></div>

<div dir="rtl">اوپر سے رجوع کریں: ایک تازہ تنصیب کی سفارش کی جاتی ہے.<br /><br /></div>

#### <div dir="rtl">۱۰.۲ CIDRAM v3 سے CIDRAM v4 میں اپ گریڈ کرنا<br /><br /></div>

<div dir="rtl">۱. سب سے پہلے، اپ ڈیٹس کے صفحے پر جائیں، اور اگر کوئی اپ ڈیٹس دستیاب ہیں، تو ان سب کو انسٹال کرنا یقینی بنائیں. یہ اپ گریڈنگ کے لیے تمام ضروری کوڈ کی دستیابی کو یقینی بناتا ہے اور اپڈیٹر کے لیے درکار کام کی مقدار کو کم کرنے میں مدد کرتا ہے.<br /><br /></div>

<div dir="rtl">۲. کنفیگریشن پیج پر جائیں اور <strong><code dir="ltr">remotes⬅frontend</code></strong> تلاش کریں. فہرست میں، جہاں آپ <code dir="ltr">v3</code> دیکھتے ہیں، اسے <code dir="ltr">v4</code> میں تبدیل کریں. اپنی کنفگریشن کو بچانے کے لیے اپ ڈیٹ پر کلک کریں. یہ تبدیلی اپڈیٹر سے کہتی ہے کہ اپ ڈیٹس تلاش کرتے وقت درست ورژن کو نشانہ بنائے.<br /><br /></div>

<div dir="rtl">۳. بیک اپ صفحہ پر جائیں. برآمد کو منتخب کریں، کنفگریشن کے لیے، اعداد و شمار کے لیے، اور معاون اصولوں کے لیے چیک باکس پر نشان لگائیں، اور پھر بیک اپ ڈاؤن لوڈ کرنے کے لیے ٹھیک کو دبائیں. کچھ تبدیلیاں ہوئی ہیں. مثال کے طور پر، "لاگ نہ کریں" کی کارروائی کو معاون قواعد سے ہٹا دیا گیا ہے (اسی چیز کو حاصل کرنے کے بجائے "لاگنگ کو دبانا" کا اختیار استعمال کیا جا سکتا ہے). آپ کو یہ بیک اپ اپ گریڈ کرنے کے بعد واپس CIDRAM میں درآمد کرنا ہوگا.<br /><br /></div>

<div dir="rtl">۴. اپ ڈیٹس کے صفحے پر واپس جائیں. نئے بڑے ورژن کی تازہ کاریوں کو اب ظاہر ہونا چاہیے. ٹائم آؤٹ سے بچنے کے لیے، سب کو اپ ڈیٹ کرنے سے پہلے، پہلے صرف "کور" یا "فرنٹ اینڈ" کو اپ ڈیٹ کرنے کی کوشش کریں (جیسا کہ دونوں ایک دوسرے کے باہمی انحصار کے طور پر، کسی کو اپ ڈیٹ کرنے سے دونوں کو خود بخود اپ ڈیٹ ہونا چاہیے). چونکہ صفحہ کا ڈھانچہ اور CSS اسٹائل میں بڑے ورژن کے درمیان نمایاں تبدیلی آئی ہے، یہ اپ ڈیٹ کرنے کے بعد ابتدائی طور پر ٹوٹا ہوا دکھائی دے سکتا ہے؛ یہ نہیں ہے. کسی دوسرے صفحہ پر جائیں اور سخت ریفریش کرنے کی کوشش کرنے کے لیے Ctrl+F5 دبائیں (یعنی ایک ریفریش جس کے ذریعے براؤزر اپنے کیشے پر انحصار کرنے کے بجائے CSS اسٹائلنگ اور دیگر پیری فیرلز کی تازہ کاپی لاتا ہے). اس کے بعد صفحہ کی ساخت اور CSS اسٹائل صحیح طریقے سے ظاہر ہونا چاہیے. اگر ایسا نہیں ہوتا ہے تو اپنے براؤزر کی کیش کو صاف کرنے کی کوشش کریں.<br /><br /></div>

<div dir="rtl">۵. اس کے ساتھ، آپ باقی سب کچھ اپ ڈیٹ کر سکتے ہیں. اپ ڈیٹس کے صفحہ پر واپس جائیں، اور اگر آپ کو صفحہ کے اوپری حصے میں بٹن نظر آتا ہے، تو سبھی کو اپ ڈیٹ کریں پر کلک کریں.<br /><br /></div>

<div dir="rtl">۶. اس بات کو یقینی بنانے کے لیے کہ کوئی دیرپا خراب اپ ڈیٹس یا کرپٹ فائلیں نہیں ہیں، اور یہ یقینی بنانے کے لیے کہ سب کچھ ویسا ہی ہے جیسا کہ ہونا چاہیے، تمام مرمت پر کلک کریں. بہت شاذ و نادر ہی یہ ایک حقیقی مسئلہ ہونا چاہیے، لیکن اسے محفوظ طریقے سے چلانا بہتر ہے.<br /><br /></div>

<div dir="rtl">۷. بیک اپ صفحہ پر واپس جائیں. درآمد کو منتخب کریں، کنفگریشن کے لیے، اعداد و شمار کے لیے، اور معاون اصولوں کے لیے چیک باکس پر نشان لگائیں، فائل کو منتخب کرنے کے لیے بٹن پر کلک کریں، پہلے ڈاؤن لوڈ کیے گئے بیک اپ کو تلاش کریں اور منتخب کریں، اور اس بیک اپ کو درآمد کرنے کے لیے OK کو دبائیں. CIDRAM تبدیلیوں کو ایڈجسٹ کرنے کے لیے ضروری ایڈجسٹمنٹ خود بخود انجام دے گا.<br /><br /></div>

<div dir="rtl">۸. آپ نے اپ گریڈ مکمل کر لیا ہے. نئے بڑے ورژن میں دستخطی فائلوں، ماڈیولز، یا ایونٹس میں کوئی تبدیلی نہیں کی گئی ہے، لہذا آپ کو اپ گریڈ کرنے کے لیے اس کے بارے میں فکر کرنے کی ضرورت نہیں ہے. اس کے بعد، آپ نئے بڑے ورژن (مثلاً، نئی متعارف کردہ خصوصیات کے لیے) کے ذریعے متعارف کرائی گئی تبدیلیوں کی وجہ سے کنفگریشن کے صفحے کو مختصراً دریافت کرنا چاہیں گے.<br /><br /></div>

<div dir="rtl">v4 کے ذریعے متعارف کرائی گئی تبدیلیوں کی فہرست کے لیے (مثال کے طور پر شامل کردہ خصوصیات، خصوصیات کو ہٹایا گیا، وغیرہ)، <a href="https://github.com/CIDRAM/CIDRAM/blob/v4/Changelog.md#v400">v4 چینج لاگ</a> سے رجوع کریں.<br /><br /></div>

---


<div dir="rtl">آخری تازہ کاری: ۹ اکتوبر ۲۰۲۵ (۲۰۲۵.۱۰.۰۹).</div>
