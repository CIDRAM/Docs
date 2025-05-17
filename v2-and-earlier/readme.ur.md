## <div dir="rtl">CIDRAM v2 لیے دستاویزی (اردو).</div>

### <div dir="rtl">فہرست:</div>
<div dir="rtl"><ul>
 <li>۱. <a href="#user-content-SECTION1">تمہید</a></li>
 <li>۲. <a href="#user-content-SECTION2">انسٹال کرنے کا طریقہ</a></li>
 <li>۳. <a href="#user-content-SECTION3">کس طرح استعمال</a></li>
 <li>۴. <a href="#user-content-SECTION4">سامنے کے آخر میں انتظام</a></li>
 <li>۵. <a href="#user-content-SECTION5">فائل اس پیکیج میں شامل</a></li>
 <li>۶. <a href="#user-content-SECTION6">ترتیب کے اختیارات</a></li>
 <li>۷. <a href="#user-content-SECTION7">دستخط فارمیٹ</a></li>
 <li>۸. <a href="#user-content-SECTION8">جانا جاتا مطابقت کے مسائل</a></li>
 <li>۹. <a href="#user-content-SECTION9">اکثر پوچھے گئے سوالات (FAQ)</a></li>
 <li>۱۰. (مستقبل کی معلومات - ابھی تک موجود نہیں ہے)</li>
 <li>۱۱. <a href="#user-content-SECTION11">قانونی معلومات</a></li>
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

<div dir="rtl">یہ دستاویز اور اس کے متعلقہ پیکجوں کے لیے مفت سے ڈاؤن لوڈ کیا جا سکتا ہے:</div>
- <a dir="ltr" href="https://github.com/CIDRAM/CIDRAM">GitHub</a>.
- <a dir="ltr" href="https://bitbucket.org/Maikuolan/cidram">Bitbucket</a>.

---


### <div dir="rtl">۲. <a name="SECTION2"></a>انسٹال کرنے کا طریقہ</div>

#### <div dir="rtl">۲.۰ دستی طور پر نصب</div>

<div dir="rtl">۱. آپ کے پڑھنے کی طرف سے اس، مجھے سنبھالنے رہا ہوں آپ کے پاس پہلے، اسکرپٹ کا ایک آرکائیو کاپی کو ڈاؤن لوڈ کیا اس کے مشمولات کو پھیلا اور اس کو اپنے مقامی مشین پر کہیں بیٹھے ہیں کیا ہے. یہاں سے، آپ نے جہاں رکھا یا CMS پر آپ ان کے مندرجات رکھنے کے لیے چاہتے ہیں باہر کام کرنے چاہیں گے. جیسے <code dir="ltr">"/public_html/cidram/"</code> یا اسی طرح کی (اگرچہ، یہ جو آپ کو اسے محفوظ ہے کچھ اور کچھ اور آپ کے ساتھ خوش ہیں ہے اتنی دیر کے طور پر انتخاب کرتے ہیں، کوئی فرق نہیں پڑتا) ایک ڈائریکٹری کافی ہوگا. <em>آپ کو اپ لوڈ کرنے شروع کرنے سے پہلے، پر پڑھیں ..</em><br /><br /></div>

<div dir="rtl">۲. config.ini" (اندر "vault" واقع کرنے <code dir="ltr">"config.ini.RenameMe"</code> نام تبدیل)، اور اختیاری پختہ اعلی درجے کی صارفین کے لیے سفارش کی جاتی ہے، لیکن (اس فائل پر مشتمل ابتدائی کے لیے یا ناتجربہ کار)، اسے کھولنے کے لیے سفارش کی نہیں CIDRAM کے لیے دستیاب تمام ہدایات؛ ہر آپشن کے اوپر ایک مختصر تبصرہ یہ کیا کرتا بیان اور کیا اس کے لیے ہے) ہونا چاہیے. آپ کو فٹ دیکھ کے طور جو بھی اپنے مخصوص سیٹ اپ کے لیے مناسب ہے کے مطابق ان ہدایات کو ایڈجسٹ کریں. فائل محفوظ کریں، قریب ہے.<br /><br /></div>

<div dir="rtl">۳. (اگر آپ پہلے پر فیصلہ کیا تھا ڈائریکٹری میں مندرجات (CIDRAM اور اس کی فائلوں) کو اپ لوڈ کریں آپ <code dir="ltr">"<code dir="ltr">*.txt/*.md</code>"</code> فائلوں کو شامل کرنے کی ضرورت نہیں ہے، لیکن زیادہ تر، تم سب کچھ اپ لوڈ کرنا چاہیے) .<br /><br /></div>

<div dir="rtl">۴. CHMOD<code dir="ltr">"755"</code> (مسائل ہیں تو، آپ کو کوشش "vault" ڈائریکٹری میں کر سکتے ہیں<code dir="ltr">"777"</code>؛ اس سے کم محفوظ ہے، اگرچہ). مندرجات (آپ اس سے قبل انتخاب کیا ایک) ذخیرہ کرنے کے اہم ڈائریکٹری، عام طور پر، آپ کو آپ کے سسٹم پر ماضی میں اجازتیں مسائل پڑا ہے تو اکیلے چھوڑ دیا جا سکتا ہے، لیکن CHMOD کی حیثیت کی جانچ پڑتال کی جانی چاہیے (ڈیفالٹ کی طرف سے، جیسے<code dir="ltr">"755"</code> کچھ ہونا چاہیے). مختصرا: پیکج کے لیے مناسب طریقے سے کام کرنے کے لیے، پی ایچ او کو <code dir="ltr">vault</code> ڈائریکٹری کے اندر فائلوں کو پڑھنے اور لکھنے کے قابل ہونے کی ضرورت ہے. اگر بہت سے چیزیں (اپ ڈیٹنگ، لاگنگ، وغیرہ) ممکن نہیں ہوسکتے، اگر PHP <code dir="ltr">vault</code> ڈائریکٹری میں نہیں لکھا جاسکتا ہے، اور پیکج بالکل کام نہیں کرے گا تو PHP <code dir="ltr">vault</code> ڈائرکٹری سے پڑھ نہیں سکتا. تاہم، زیادہ سے زیادہ سیکورٹی کے لیے، <code dir="ltr">vault</code> ڈائرکٹری عوامی طور پر قابل رسائی نہیں ہونا ضروری ہے (<code dir="ltr">vault</code> ڈائرکٹری عوامی طور پر قابل رسائی ہے تو حملہ آوروں کے بارے میں سنجیدگی سے متعلق معلومات سامنے آسکتی ہیں).<br /><br /></div>

<div dir="rtl">۵. اگلا، آپ کو "ہک" آپ کے سسٹم یا CMS کرنے CIDRAM کرنا ہوگا. کئی مختلف طریقے ہیں آپ کر سکتے ہیں جیسا کہ آپ کے سسٹم یا CMS، لیکن سب سے آسان ہے صرف عام طور پر ہمیشہ سے لوڈ کیا جائے گا کہ آپ کے سسٹم یا CMS (ایک کی ایک بنیادی فائل کے شروع میں سکرپٹ کو شامل کرنے کے لیے کرنا CIDRAM "ہک" اسکرپٹس اگر کوئی ویب سائٹ بھر میں کسی بھی صفحے تک رسائی حاصل کرتا ہے جب) ایک "require" یا "include" بیان کا استعمال کرتے ہوئے. عام طور پر، اس طرح کے طور پر "/includes"، "/assets" یا "/functions" ایک ڈائریکٹری میں محفوظ کیا کچھ ہو جائے گا، اور اکثر" init.php"، "common_functions.php"،" افعال کی طرح کچھ نام دیا جائے گا. php" یا اسی طرح کی. تم جس فائل اگر یہ آپ کی صورت حال کے لیے ہے باہر کام کرنا پڑے گا؛ تم اپنے لیے اس سے باہر کام کرنے میں مشکلات کا سامنا کرتے ہیں، GitHub کے پر CIDRAM مسائل کا صفحہ ملاحظہ کریں. [ "require" یا" استعمال کرنے کے لیے include"] ایسا کرنے کے لیے، جو کہ بنیادی فائل کے شروع کرنے کے لیے کوڈ کی مندرجہ ذیل لائن داخل، "loader.php" فائل کا عین مطابق ایڈریس کے ساتھ واوین کے اندر موجود سٹرنگ کی جگہ (مقامی پتہ، نہ HTTP ایڈریس؛ یہ پہلے ذکر والٹ ایڈریس کو اسی طرح دیکھ لیں گے).<br /><br /></div>

`<?php require '/user_name/public_html/cidram/loader.php'; ?>`

<div dir="rtl">فائل، قریب، ہٹادیا بچائیں.<br /><br /></div>

<div dir="rtl">-- یا متبادل --<br /><br /></div>

<div dir="rtl">آپ ایک اپاچی ویب سرور استعمال کر رہے ہیں اور آپ کو "php.ini" تک رسائی ہے تو، تو آپ جب بھی کسی بھی PHP کی درخواست کی جاتی ہے CIDRAM prepend کے کو "auto_prepend_file" ہدایت کو استعمال کر سکتے ہیں. کی طرح کچھ:<br /><br /></div>

`auto_prepend_file = "/user_name/public_html/cidram/loader.php"`

<div dir="rtl">یا ".htaccess" فائل میں اس:<br /><br /></div>

`php_value auto_prepend_file "/user_name/public_html/cidram/loader.php"`

<div dir="rtl">۶. یہی سب کچھ ہے! 😄<br /><br /></div>

#### <div dir="rtl">۲.۱ COMPOSER کے ساتھ نصب</div>

<div dir="rtl"><a href="https://packagist.org/packages/cidram/cidram">CIDRAM Packagist ساتھ رجسٹرڈ ہے</a>، اور اسی طرح، آپ کمپوزر سے واقف ہیں تو، آپ (تاہم، آپ اب بھی پیکیج تیار کرنے کی ضرورت ہوگی؛ "دستی طور پر نصب کرنے" دیکھیں اقدامات ۲، ۴ اور ۵).<br /><br /></div>

`composer require cidram/cidram`

#### <div dir="rtl">۲.۲ ورڈپریس کے لیے نصب</div>

<div dir="rtl">اگر آپ ورڈپریس کے ساتھ CIDRAM استعمال کرنا چاہتے ہیں تو، آپ کو مندرجہ بالا تمام ہدایات کو نظر انداز کر سکتے ہیں. <a href="https://wordpress.org/plugins/cidram/">CIDRAM ورڈپریس پلگ ان کے ڈیٹا بیس کے ساتھ ایک پلگ ان کے طور پر رجسٹرڈ ہے</a>، اور آپ کو پلگ ان ڈیش بورڈ سے براہ راست CIDRAM انسٹال کر سکتے ہیں. آپ کسی بھی دیگر پلگ ان کے طور پر اسی انداز میں اسے انسٹال کر سکتے ہیں، اور کوئی اس کے علاوہ اقدامات کی ضرورت ہے. بس دوسرے کی تنصیب کے طریقوں کے ساتھ کے طور پر، آپ <code dir="ltr">"config.ini"</code> فائل کے مواد میں تبدیلی کرنے کی طرف سے یا سامنے کے آخر میں ترتیب صفحے کا استعمال کرتے ہوئے کی طرف سے آپ کی تنصیب کے اپنی مرضی کے مطابق کر سکتے ہیں. آپ کو سامنے کے آخر میں اپ ڈیٹس صفحے کا استعمال کرتے ہوئے CIDRAM سامنے کے آخر میں اور اپ ڈیٹ CIDRAM فعال کرتے ہیں تو یہ خود کار طریقے سے پلگ ان ڈیش بورڈ میں ظاہر پلگ ان ورژن کی معلومات کے ساتھ مطابقت پذیر ہو گی<br /><br /></div>

<div dir="rtl"><em>انتباہ: ایک صاف تنصیب میں پلگ ان ڈیش بورڈ کے نتائج کے ذریعے CIDRAM تازہ کاری ہو رہی! آپ کو آپ کی تنصیب کے اپنی مرضی کے مطابق کیا ہے تو (اپنی ترتیب بدل گیا، نصب ماڈیولز، وغیرہ)، ان کی تخصیصات پلگ ان ڈیش بورڈ کے ذریعے اپ ڈیٹ کر جب ختم ہو جائے گا! لاگ مسلیں بھی ختم ہو جائے گا! لاگ فائلوں اور اصلاح کے تحفظ کے لیے، CIDRAM سامنے کے آخر میں اپ ڈیٹس صفحے کے ذریعے اپ ڈیٹ کریں.</em><br /><br /></div>

---


### <div dir="rtl">۳. <a name="SECTION3"></a>کس طرح استعمال</div>

<div dir="rtl">CIDRAM خود کار طریقے سے آپ کی ویب سائٹ کو ناپسندیدہ درخواستوں کسی بھی دستی امداد کی ضرورت کے بغیر، ایک طرف اس کی ابتدائی تنصیب سے مسدود کرنا چاہیے.<br /><br /></div>

<div dir="rtl">آپ کو آپ کی ترتیب اپنی مرضی کے مطابق اور اپنی مرضی کے مطابق جس CIDR آپ کی کنفیگریشن فائل اور/یا آپ کے دستخط کی فائلوں میں تبدیلی کرنے کی طرف سے بلاک کر رہے ہیں کر سکتے ہیں.<br /><br /></div>

<div dir="rtl">آپ کو کسی بھی جھوٹے مثبت سامنا کرتے ہیں، مجھے اس کے بارے میں مطلع کرنے کے لیے مجھ سے رابطہ کریں. <em>(دیکھیں: <a href="#user-content-WHAT_IS_A_FALSE_POSITIVE">ایک "جھوٹی مثبت" سے کیا مراد ہے؟</a>).</em><br /><br /></div>

<div dir="rtl">CIDRAM دستی طور پر یا سامنے کے اختتام کے ذریعے اپ ڈیٹ کیا جا سکتا ہے. CIDRAM بھی Composer یا WordPress کے ذریعہ اپ ڈیٹ کیا جا سکتا ہے، اگر اصل میں ان کے ذریعہ نصب ہوجائے.<br /><br /></div>

---


### <div dir="rtl">۴. <a name="SECTION4"></a>سامنے کے آخر میں انتظام</div>

#### <div dir="rtl">۴.۰ سامنے کے آخر کیا ہے.<br /><br /></div>

<div dir="rtl">سامنے کے آخر میں، برقرار رکھنے کا انتظام، اور آپ CIDRAM تنصیب کو اپ ڈیٹ کرنے کے لیے ایک آسان اور آسان طریقہ فراہم کرتا ہے. آپ صرف مسودہ دیکھ سکتے ہیں، اشتراک، اور نوشتہ صفحے کے ذریعے لاگ مسلیں لوڈ، آپ کی ترتیب کے صفحے کے ذریعے کی ترتیب تبدیل کر سکتے ہیں، آپ کو انسٹال کر سکتے ہیں اور اپ ڈیٹس صفحے کے ذریعے انسٹال اجزاء، اور آپ کو اپ لوڈ کر سکتے ہیں، ڈاؤن لوڈ، اتارنا، اور فائل کے ذریعے آپ کے والٹ میں فائلوں پر نظر ثانی مینیجر.<br /><br /></div>

<div dir="rtl">سامنے کے آخر میں (آپ کی ویب سائٹ اور اس کی سیکیورٹی کے لیے اہم نتائج ہو سکتے ہیں غیر مجاز رسائی) غیر مجاز رسائی کو روکنے کے لیے پہلے سے طے شدہ کی طرف سے غیر فعال ہے. اس کو چالو کرنے کے لیے ہدایات اس پیراگراف ذیل میں شامل ہیں.<br /><br /></div>

#### <div dir="rtl">۴.۱ سامنے کے آخر میں فعال کرنے کا طریقہ.<br /><br /></div>

<div dir="rtl">۱. اندر <code dir="ltr">"config.ini"</code>، <code dir="ltr">"disable_frontend"</code> ہدایت کو تلاش کریں اور "false" کرنے کے لیے مقرر (یہ ڈیفالٹ کی طرف سے "true" ہو جائے گا).<br /><br /></div>

<div dir="rtl">۲. رسائی اپنے براؤزر سے <code dir="ltr">"loader.php"</code> (جیسے، <code dir="ltr">"http://localhost/cidram/loader.php"</code>).<br /><br /></div>

<div dir="rtl">۳. پہلے سے طے شدہ صارف کا نام اور پاس ورڈ کے ساتھ لاگ ان کریں (admin/password).<br /><br /></div>

<div dir="rtl">نوٹ: اگر آپ کو پہلی بار کے لیے لاگ ان کرنے کے بعد، سامنے کے آخر تک غیر مجاز رسائی کو روکنے کے لیے، آپ کو فوری طور پر آپ کا صارف نام اور پاس ورڈ کو تبدیل کرنا چاہیے! یہ بہت اہم ہے، یہ سامنے کے آخر میں کے ذریعے آپ کی ویب سائٹ پر من مانی PHP کوڈ کو اپ لوڈ کرنا ممکن ہے کیونکہ.<br /><br /></div>

<div dir="rtl">اس کے علاوہ، زیادہ سے زیادہ سیکورٹی کے لیے، تمام فرنٹ اینڈ اکاؤنٹس کے لیے 2FA کو مؤثر طریقے سے سفارش کی جاتی ہے (ذیل میں دی گئی ہدایات).<br /><br /></div>

#### <div dir="rtl">۴.۲ سامنے کے آخر میں کس طرح استعمال.<br /><br /></div>

<div dir="rtl">ہدایات یہ اور اس مقصد کو استعمال کرنے کا صحیح طریقہ کی وضاحت کے لیے سامنے کے آخر میں کے ہر صفحے پر فراہم کی جاتی ہیں. اگر آپ کو مزید وضاحت یا کوئی خاص مدد کی ضرورت ہے، کی مدد سے رابطہ کریں. متبادل طور پر، یو ٹیوب پر دستیاب کچھ ویڈیوز مظاہرے کی راہ کی طرف مدد کر سکتا ہے جس میں موجود ہیں.<br /><br /></div>

#### <div dir="rtl">۴.۳ 2FA<br /><br /></div>

<div dir="rtl">2FA کو چالو کرنے کے ذریعہ front-end کو مزید محفوظ بنانے کے لیے ممکن ہے. جب 2FA کے ساتھ اکاؤنٹ میں لاگ ان ہو تو، اس اکاؤنٹ سے منسلک ای میل ایڈریس پر ایک ای میل بھیجا جاتا ہے. اس ای میل میں "2FA کوڈ" شامل ہے، جو اس صارف کا استعمال کرتے ہوئے لاگ ان کرنے کے لۓ صارف کا نام اور پاسورڈ کے علاوہ صارف کو داخل ہونا ضروری ہے. اس کا مطلب یہ ہے کہ اکاؤنٹ اکاؤنٹ پاس ورڈ حاصل کرنے کے لیے کسی بھی ہیکر یا ممکنہ حملہ آور کو اس اکاؤنٹ میں لاگ ان کرنے کے قابل نہیں ہو گا، کیونکہ انہیں وصول کرنے کے قابل ہونے کے لیے ان اکاؤنٹ سے منسلک ای میل ایڈریس تک رسائی حاصل ہوگی. اور سیشن کے ساتھ منسلک 2FA کوڈ استعمال کریں.<br /><br /></div>

<div dir="rtl">سب سے پہلے، 2FA کو چالو کرنے کے لیے، PHPMailer اجزاء کو انسٹال کرنے کے لیے front-end اپ ڈیٹس کا صفحہ استعمال کریں. ای میل بھیجنے کے لیے CIDRAM PHPMailer کا استعمال کرتا ہے. نوٹ: اگرچہ CIDRAM، خود ہی، <code dir="ltr">PHP &gt;= 5.4.0</code> کے ساتھ مطابقت رکھتا ہے، PHPMailer کی ضرورت ہے <code dir="ltr">PHP &gt;= 5.5.0</code>. اس کا مطلب ہے کہ <code dir="ltr">PHP 5.4</code> صارفوں کے لیے CIDRAM front-end 2FA کو چالو کرنا ممکن نہیں ہوگا.<br /><br /></div>

<div dir="rtl">PHPMailer نصب کرنے کے بعد، آپ کو CIDRAM ترتیب کے صفحے یا ترتیب کی فائل کے ذریعے PHPMailer کے لیے ترتیب ہدایات کو آباد کرنے کی ضرورت ہوگی. ان ترتیبات کے ہدایات کے بارے میں مزید معلومات اس دستاویز کے ترتیب کے حصے میں شامل ہیں. PHPMailer ترتیب ہدایات آبادی کے بعد، <code dir="ltr">enable_two_factor</code> <code dir="ltr">true</code> سیٹ کریں. 2FA اب فعال ہونا چاہیے.<br /><br /></div>

<div dir="rtl">اگلا، آپ کو ایک ای میل ایڈریس کو اکاؤنٹ کے ساتھ منسلک کرنے کی ضرورت ہوگی، تاکہ CIDRAM کو معلوم ہے کہ اس اکاؤنٹ کے ساتھ لاگ ان کرتے وقت 2FA کوڈ بھیجنے کے لیے. ایسا کرنے کے لیے، اکاؤنٹ کے صارف نام کے طور پر ای میل پتہ استعمال کریں (کچھ <code dir="ltr">foo@bar.tld</code> کی طرح)، یا اس صارف کے صارف کے حصے کے طور پر ای میل ایڈریس بھی شامل ہے جس طرح آپ عام طور پر ای میل بھیجیں گے (کچھ <code dir="ltr">Foo Bar &lt;foo@bar.tld&gt;</code> کی طرح).<br /><br /></div>

<div dir="rtl">نوٹ: غیر مجاز رسائی کے خلاف vault کی حفاظت خاص طور پر اہم ہے (مثال کے طور پر، آپ کے سرور کی سیکیورٹی کو مضبوط کرنا، عوامی رسائی کی اجازت محدود)، کیونکہ غیر مجاز رسائی آپ کے SMTP ترتیبات کو بے نقاب کر سکتا ہے (اس میں SMTP صارف کا نام اور پاس ورڈ بھی شامل ہے). آپ کو اس بات کو یقینی بنانا چاہیے کہ 2FA کو چالو کرنے سے پہلے vault مناسب طریقے سے محفوظ ہو. اگر آپ ایسا کرنے میں قاصر ہیں تو، کم سے کم، آپ کو ایک نیا ای میل اکاؤنٹ بنانا چاہیے، اس مقصد کے لیے وقف کردہ SMTP ترتیبات کے خطرات کو کم کرنے کے لیے.<br /><br /></div>

---


### <div dir="rtl">۵. <a name="SECTION5"></a>فائل اس پیکیج میں شامل</div>

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


### <div dir="rtl">۶. <a name="SECTION6"></a>ترتیب کے اختیارات</div>

<div dir="rtl">ندرجہ ذیل ان ہدایات کے مقصد کی وضاحت کے ساتھ ساتھ، <code dir="ltr">"config.ini"</code> ترتیب فائل میں CIDRAM کو دستیاب ہدایات کی ایک فہرست ہے.<br /><br /></div>

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

#### <div dir="rtl">"general" (قسم)<br /></div>
<div dir="rtl">جنرل CIDRAM کنفیگریشن.<br /><br /></div>

##### <div dir="rtl">"logfile"<br /></div>
<div dir="rtl"><ul>
 <li>تمام بلاک کر تک رسائی کی کوششوں کو لاگ ان کرنے کے لیے انسانی قابل مطالعہ فائل. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے خالی چھوڑ دیں.</li>
</ul></div>

##### <div dir="rtl">"logfile_apache"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "logfileApache"</em></li>
 <li>تمام بلاک کر تک رسائی کی کوششوں کو لاگ ان کرنے کے لیے اپاچی طرز فائل. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li>
</ul></div>

##### <div dir="rtl">"logfile_serialized"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "logfileSerialized"</em></li>
 <li>تمام بلاک کر تک رسائی کی کوششوں کو لاگ ان کرنے کے لیے serialized کی فائل. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li>
</ul></div>

<div dir="rtl"><em>مفید ٹپ: "{yyyy}" مکمل سال کے لیے، "{yy}" مختصر سال کے لیے، "{mm}": اگر آپ چاہتے ہیں تو آپ کے نام میں ان کو شامل کرکے آپ لاگ مسلیں کے ناموں کو تاریخ / وقت کی معلومات شامل کر سکتے ہیں مہینے کے لیے، دن کے لیے، "{hh}" گھنٹے کے لیے "{dd}" (ذیل کی مثالیں دیکھ).</em><br /><br /></div>

```
 logfile='logfile.{yyyy}-{mm}-{dd}-{hh}.txt'
 logfile_apache='access.{yyyy}-{mm}-{dd}-{hh}.txt'
 logfile_serialized='serial.{yyyy}-{mm}-{dd}-{hh}.txt'
```

##### <div dir="rtl">"error_log"<br /></div>
<div dir="rtl"><ul>
 <li>کسی بھی غیر مہلک غلطیوں کو لاگ کرنے کے لیے ایک فائل کا پتہ چلا. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li>
</ul></div>

##### <div dir="rtl">"error_log_stages"<br /></div>
<div dir="rtl"><ul>
 <li>عمل درآمد سلسلہ میں مراحل کی ایک فہرست جس میں پیدا ہونے والی غلطیوں میں کوئی لاگ ان ہونا چاہیے.</li>
 <li><em>پہلے سے طے شدہ: "Tests,Modules,SearchEngineVerification,SocialMediaVerification,OtherVerification,Aux,Reporting,Tracking,RL,CAPTCHA,Statistics,Webhooks,Output,NonBlockedCAPTCHA"</em></li>
</ul></div>

##### <div dir="rtl">"truncate"<br /></div>
<div dir="rtl"><ul>
 <li>وہ ایک خاص سائز تک پہنچنے میں جب صاف لاگ مسلیں؟ ویلیو میں B/KB/MB/GB/TB زیادہ سے زیادہ سائز ہے. جب 0KB، وہ غیر معینہ مدت تک ترقی کر سکتا ہے (پہلے سے طے). نوٹ: واحد فائلوں پر لاگو ہوتا ہے! فائلیں اجتماعی غور نہیں کر رہے ہیں.</li>
</ul></div>

##### <div dir="rtl">"log_rotation_limit"<br /></div>
<div dir="rtl"><ul>
 <li>لاگ گرد گردش کسی بھی وقت کسی بھی وقت موجود ہونا لاگ ان کی تعداد محدود کرتا ہے. جب نیا لاگ ان کی تخلیق کی جاتی ہے تو، اگر لاگ ان کی کل تعداد مخصوص حد سے زیادہ ہوتی ہے تو مخصوص کارروائی کی جائے گی. آپ یہاں مطلوبہ حد کی وضاحت کرسکتے ہیں. 0 کی قیمت لاگ گرد گردش کو غیر فعال کرے گی.</li>
</ul></div>

##### <div dir="rtl">"log_rotation_action"<br /></div>
<div dir="rtl"><ul>
 <li>لاگ گرد گردش کسی بھی وقت کسی بھی وقت موجود ہونا لاگ ان کی تعداد محدود کرتا ہے. جب نیا لاگ ان کی تخلیق کی جاتی ہے تو، اگر لاگ ان کی کل تعداد مخصوص حد سے زیادہ ہوتی ہے تو مخصوص کارروائی کی جائے گی. آپ یہاں مطلوبہ کارروائی کی وضاحت کرسکتے ہیں. Delete = قدیم ترین لاگ ان کو حذف کریں، جب تک کہ حد تک زیادہ نہیں ہوسکتی ہے. Archive = سب سے پہلے آرکائیو، اور پھر سب سے پرانی لاگ ان کو حذف کریں، جب تک کہ حد زیادہ نہیں ہوسکتی.</li>
</ul></div>

<div dir="rtl">تکنیکی وضاحت: اس تناظر میں "سب سے پرانی" کا مطلب "کم از کم ترمیم شدہ" ہے.<br /><br /></div>

##### <div dir="rtl">"timezone"<br /></div>
<div dir="rtl"><ul>
 <li>یہ استعمال کیا جاتا ہے کہ کون سا ٹائم زون CIDRAM کو تاریخ/وقت کے آپریشن کے لیے استعمال کرنا چاہیے. اگر آپ کو اس کی ضرورت نہیں ہے تو اسے نظر انداز کریں. ممکنہ اقدار PHP کی طرف سے مقرر ہیں. یہ عام طور پر یہ کرنا ہمیشہ ممکن نہیں ہے، اور تو، اس اختیار کو یہاں فراہم کی جاتی ہے (جیسا محدود مشترکہ ہوسٹنگ فراہم کرنے والے کے ساتھ کام کرتے وقت کے طور پر) آپ <code dir="ltr">php.ini</code> فائل میں ٹائم زون ہدایت کو ایڈجسٹ کرنے کی بجائے سفارش، لیکن کبھی کبھی رہا ہے.</li>
</ul></div>

##### <div dir="rtl">"time_offset"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "timeOffset"</em></li>
 <li>آپ کے سرور کے وقت آپ کے مقامی وقت کے مماثل نہیں ہے تو، آپ کو آپ کی ضروریات کے مطابق CIDRAM طرف سے پیدا تاریخ / وقت کی معلومات کو ایڈجسٹ کرنے کے لیے یہاں آفسیٹ ایک وضاحت کر سکتے ہیں. یہ عام طور پر یہ کرنا ہمیشہ ممکن نہیں ہے، اور تو، اس اختیار کو یہاں فراہم کی جاتی ہے (جیسا محدود مشترکہ ہوسٹنگ فراہم کرنے والے کے ساتھ کام کرتے وقت کے طور پر) آپ <code dir="ltr">php.ini</code> فائل میں ٹائم زون ہدایت کو ایڈجسٹ کرنے کی بجائے سفارش، لیکن کبھی کبھی رہا ہے. آف سیٹ منٹ میں ہے.<br /></li>
 <li>مثال (ایک گھنٹے کا اضافہ کرنے کے لیے):</li>
</ul></div>

`time_offset=60`

##### <div dir="rtl">"time_format"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "timeFormat"</em></li>
 <li>تاریخ کی شکل CIDRAM طرف سے استعمال کیا. پہلے سے طے شدہ:</li>
</ul></div>

`{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss} {tz}`

##### <div dir="rtl">"ipaddr"<br /></div>
<div dir="rtl"><ul>
 <li>کہاں درخواستوں منسلک کرنے کے IP ایڈریس کو تلاش کرنے کے لیے؟ (جیسا Cloudflare کے اور پسند کرتا ہے کے طور پر خدمات کے لیے مفید). پہلے سے طے شدہ = REMOTE_ADDR. انتباہ: جب تک کہ آپ کو پتہ ہے تم کیا کر رہے ہو اس کو تبدیل نہ کریں!</li>
</ul></div>

<div dir="rtl">"ipaddr" کے لیے سفارش کی اقدار:<br /><br /></div>

&nbsp; <div dir="rtl" style="display:inline">قدر</div> | &nbsp; <div dir="rtl" style="display:inline">استعمال</div>
---|---
`HTTP_INCAP_CLIENT_IP` | Incapsula reverse proxy (ریورس پراکسی).
`HTTP_CF_CONNECTING_IP` | Cloudflare reverse proxy (ریورس پراکسی).
`CF-Connecting-IP` | Cloudflare reverse proxy (ریورس پراکسی؛ متبادل؛ مندرجہ بالا کام نہیں کرتا تو).
`HTTP_X_FORWARDED_FOR` | Cloudbric reverse proxy (ریورس پراکسی).
`X-Forwarded-For` | [Squid reverse proxy (ریورس پراکسی)](http://www.squid-cache.org/Doc/config/forwarded_for/).
`Forwarded` | *[Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded).*
&nbsp; <div dir="rtl" style="display:inline"><em>سرور کی ترتیب کی طرف سے وضاحت کی گئی.</em></div> | [Nginx reverse proxy (ریورس پراکسی)](https://www.nginx.com/resources/admin-guide/reverse-proxy/).
`REMOTE_ADDR` | &nbsp; <div dir="rtl" style="display:inline">نہیں کسی بھی ریورس پراکسی (پہلے سے طے شدہ قیمت).</div>

##### <div dir="rtl">"forbid_on_block"<br /></div>
<div dir="rtl"><ul>
 <li>درخواستوں کو روکنے پر بھیجنے کے لیے HTTP حیثیت کا پیغام.</li>
</ul></div>

<div dir="rtl">فی الحال تعاون شدہ اقدار:<br /><br /></div>

حیثیت کا کوڈ | حیثیت کا پیغام | تفصیل
---|---|---
`200` | `200 OK` | پہلے سے طے شدہ قیمت. کم سے کم مضبوط، لیکن سب سے زیادہ صارف دوست. خودکار درخواستیں غالباً اس جواب کی تشریح کریں گی کہ درخواست کامیاب تھی.
`403` | `403 Forbidden` | زیادہ مضبوط، لیکن کم صارف دوست. زیادہ تر عام حالات کے لیے تجویز کردہ.
`410` | `410 Gone` | غلط مثبت کو حل کرتے وقت مسائل پیدا ہوسکتے ہیں، کیونکہ کچھ براؤزر اس اسٹیٹس میسج کو کیش کریں گے اور بعد میں درخواستیں نہیں بھیجیں گے. کچھ سیاق و سباق میں استعمال کرنے کے لیے بہترین ہو سکتا ہے.
`418` | `418 I'm a teapot` | اپریل فول کے لطیفے کا حوالہ دیتے ہیں (<a href="https://tools.ietf.org/html/rfc2324#section-6.5.14">RFC 2324</a>). کسی بھی کلائنٹ، بوٹ، براؤزر، یا کسی اور طرح سے سمجھنے کا امکان نہیں ہے. تفریح اور سہولت کے لیے فراہم کی گئی ہے، لیکن عام طور پر تجویز نہیں کی جاتی ہے.
`451` | `451 Unavailable For Legal Reasons` | بنیادی طور پر قانونی وجوہات کی بنا پر مسدود کرنے پر تجویز کیا جاتا ہے. دوسرے سیاق و سباق میں سفارش نہیں کی جاتی ہے.
`503` | `503 Service Unavailable` | سب سے زیادہ مضبوط، لیکن کم از کم صارف دوست. حملے کے دوران، یا انتہائی مسلسل ناپسندیدہ ٹریفک سے نمٹنے کے لیے تجویز کردہ.

##### <div dir="rtl">"silent_mode"<br /></div>
<div dir="rtl"><ul>
 <li>خاموشی CIDRAM چاہیے "رسائی نہیں ہوئی" کے صفحے کی نمائش سے بلاک رسائی کی کوششوں کو ری ڈائریکٹ کرنے کے بجائے؟ ہاں تو، کو بلاک کر تک رسائی کی کوششوں کو ری ڈائریکٹ کرنے کے محل وقوع کی وضاحت. کوئی تو اس متغیر خالی چھوڑ دیں.</li>
</ul></div>

##### <div dir="rtl">"lang"<br /></div>
<div dir="rtl"><ul>
 <li>CIDRAM کے لیے پہلے سے طے شدہ زبان کی وضاحت.</li>
</ul></div>

##### <div dir="rtl">"lang_override"<br /></div>
<div dir="rtl"><ul>
 <li>جب بھی ممکن ہو HTTP_ACCEPT_LANGUAGE کے مطابق لوکلائز کریں؟ True (سچے) = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = نہیں.</li>
</ul></div>

##### <div dir="rtl">"numbers"<br /></div>
<div dir="rtl"><ul>
 <li>نمبروں کو ظاہر کرنے کی وضاحت کرتا ہے.</li>
</ul></div>

<div dir="rtl">فی الحال تعاون شدہ اقدار:<br /><br /></div>

قدر | پیدا کرتا ہے | تفصیل
---|---|---
`NoSep-1` | `1234567.89`
`NoSep-2` | `1234567,89`
`Latin-1` | `1,234,567.89` | پہلے سے طے شدہ.
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

<div dir="rtl">نوٹ: یہ اقدار کہیں بھی معیاری نہیں ہیں، اور شاید پیکج سے باہر متعلقہ نہیں ہوں گے. اس کے علاوہ، معاون اقدار مستقبل میں تبدیل کر سکتے ہیں.<br /><br /></div>

##### <div dir="rtl">"emailaddr"<br /></div>
<div dir="rtl"><ul>
 <li>اگر آپ چاہتے ہیں، تو آپ صارفین کو جب انہیں بلاک کر رہے ہیں تو دینے کے لیے ای میل ایڈریس کی فراہمی کر سکتے ہیں.وہ اسے استعمال آپ سے رابطہ کرنے کے لیے کر سکتے ہیں اگر وہ غلطی سے بلاک کر رہے ہیں. انتباہ: آپ جو بھی ای میل ایڈریس پر فراہمی کرتے ہیں، وہ یقینی طور پر سپےمبٹس اور کھرچنی کی طرف سے حاصل کیے جائیں گے. اس کی وجہ سے، اس کی سختی سے سفارش کی جاتی ہے کہ آپ ایک ای میل ایڈریس انتخاب کرتے ہیں جو ڈسپوزایبل یا غیر اہم ہے (یعنی.، آپ کی ذاتی یا کاروباری ای میل ایڈریس کا استعمال نہ کریں).</li>
</ul></div>

##### <div dir="rtl">"emailaddr_display_style"<br /></div>
<div dir="rtl"><ul>
 <li>آپ کو ای میل ایڈریس کو کس طرح صارفین کو پیش کرنا پسند ہے؟ "default" = کلک کرنے والے لنک. "noclick" = متن جو کلک نہیں کیا جا سکتا.</li>
</ul></div>

##### <div dir="rtl">"disable_cli"<br /></div>
<div dir="rtl"><ul>
 <li><em>(v2 سے ہٹا دیا گیا).</em></li>
 <li>CLI موڈ کو غیر فعال کریں؟ CLI موڈ ڈیفالٹ کی طرف سے چالو حالت میں ہے، لیکن کبھی کبھی بعض جانچ کے آلات (جیسے PHPUnit کے طور پر، مثال کے طور پر) اور دیگر CLI کی بنیاد پر ایپلی کیشنز کے ساتھ مداخلت کر سکتے ہیں. آپ CLI موڈ کو غیر فعال کرنے کی ضرورت نہیں ہے تو، آپ کو اس ہدایت کو نظر انداز کرنا چاہیے. False (جھوٹی) = CLI موڈ [پہلے سے طے شدہ] فعال؛ True (سچے) = غیر فعال CLI موڈ.</li>
</ul></div>

##### <div dir="rtl">"disable_frontend"<br /></div>
<div dir="rtl"><ul>
 <li>سامنے کے آخر تک رسائی کو غیر فعال کریں؟ سامنے کے آخر میں رسائی CIDRAM زیادہ انتظام بنا سکتے ہیں، لیکن یہ بھی بہت ہے، ایک زبردست حفاظتی خطرہ ہو سکتا ہے. یہ جب بھی ممکن ہو واپس کے آخر کے ذریعے CIDRAM منظم کرنے کی سفارش کی جاتی ہے، لیکن سامنے کے آخر میں رسائی ممکن نہیں ہے جب کے لیے فراہم کی جاتی ہے. تمہیں اس کی ضرورت ہے جب تک کہ اس کو معذور رکھیں. False (جھوٹی) = سامنے کے آخر میں رسائی کو فعال کریں؛ True (سچے) = غیر فعال سامنے کے آخر میں رسائی [پہلے سے طے شدہ].</li>
</ul></div>

##### <div dir="rtl">"max_login_attempts"<br /></div>
<div dir="rtl"><ul>
 <li>لاگ ان کوششوں کی زیادہ سے زیادہ تعداد (سامنے کے آخر میں). پہلے سے طے شدہ = 5.</li>
</ul></div>

##### <div dir="rtl">"frontend_log"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "FrontEndLog"</em></li>
 <li>سامنے کے آخر میں لاگ ان کوششوں لاگنگ کے لیے دائر. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li>
</ul></div>

##### <div dir="rtl">"signatures_update_event_log"<br /></div>
<div dir="rtl"><ul>
 <li>جب دستخطوں کو اپ ڈیٹ پیج کے ذریعہ اپ ڈیٹ کیا جاتا ہے تو ریکارڈ کرنے کے لیے ایک فائل. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li>
</ul></div>

##### <div dir="rtl">"ban_override"<br /></div>
<div dir="rtl"><ul>
 <li>"forbid_on_block" کی جگہ لے لے، جب "infraction_limit" حد سے تجاوز کر رہا ہے؟ زیرکر کب: التواء درخواستوں ایک خالی صفحہ (سانچے فائلوں کا استعمال نہیں کر رہے ہیں) واپس جائیں. 200 = جگہ لے لے نہیں ہے [پہلے سے طے شدہ]. دیگر اقدار "forbid_on_block" کے لیے دستیاب اقدار کے طور پر اسی ہیں.</li>
</ul></div>

##### <div dir="rtl">"log_banned_ips"<br /></div>
<div dir="rtl"><ul>
 <li>لاگ مسلیں میں کالعدم IP ایس سے مسدود درخواستوں شامل کریں؟ سچا = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = نمبر.</li>
</ul></div>

##### <div dir="rtl">"default_dns"<br /></div>
<div dir="rtl"><ul>
 <li>میزبان نام لک اپ کے لیے استعمال کرنے کے لیے DNS سرورز کی کوما ختم ہونے والی فہرست. پہلے سے طے شدہ = "8.8.8.8,8.8.4.4" (گوگل DNS). انتباہ: جب تک کہ آپ کو پتہ ہے تم کیا کر رہے ہو اس کو تبدیل نہ کریں!</li>
</ul></div>

<div dir="rtl">بھی دیکھو: <a href="#میں-default_dns-کے-لیے-کیا-استعمال-کر-سکتا-ہوں">میں "default_dns" کے لیے کیا استعمال کر سکتا ہوں؟</a><br /><br /></div>

##### <div dir="rtl">"search_engine_verification"<br /></div>
<div dir="rtl"><ul>
 <li>تلاش کے انجن کی طرف سے درخواستوں کی تصدیق کرنے کی کوشش؟ تلاش کے انجن کی توثیق کرنے سے کہ وہ خلاف ورزی کی حد (ویب سائٹ سے تلاش کے انجن پر پابندی عائد عام طور پر آپ کی تلاش کے انجن کی درجہ بندی، SEO، وغیرہ پر منفی اثر پڑے گا) تجاوز کا ایک نتیجہ کے طور پر پابندی عائد نہیں کیا جائے گا یقینی بناتا ہے. تصدیق کی جب، تلاش کے انجن معمول فی کے طور پر بلاک کیا جا سکتا ہے، لیکن پابندی عائد نہیں کی گئی. کی توثیق نہیں کی ہے، تو یہ ان کے لیے خلاف ورزی کی حد سے تجاوز کرنے کے نتیجے کے طور پر پابندی عائد کی جائے کرنے کے لیے ممکن ہے. اس کے علاوہ، تلاش کے انجن کی توثیق کی جعلی تلاش کے انجن کی درخواستوں کے خلاف اور (اس طرح کی درخواستوں کی تلاش کے انجن کی توثیق فعال ہے جب بلاک کر دیا جائے گا) سرچ انجن کے طور پر ویش ممکنہ طور پر بدنیتی پر مبنی اداروں کے خلاف تحفظ فراہم کرتا ہے. True (سچے) = سرچ انجن توثیق [پہلے سے طے شدہ] فعال؛ False (جھوٹی) = غیر فعال تلاش کے انجن کی توثیق کی.</li>
</ul></div>

<div dir="rtl">فی الحال تعاون کی گئی:<br /></div>
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

<div dir="rtl">مطابقت نہیں ہے (تنازعات کا سبب بنتا ہے):<br /></div>
<div dir="rtl"><ul>
 <li><strong dir="ltr"><a href="https://github.com/CIDRAM/CIDRAM/issues/80">Mix.com</a></strong></li>
</ul></div>

##### <div dir="rtl">"social_media_verification"<br /></div>
<div dir="rtl"><ul>
 <li>سوشل میڈیا کی درخواستوں کی توثیق کرنے کی کوشش؟ سوشل میڈیا کی توثیق جعلی سوشل میڈیا کی درخواستوں کے خلاف تحفظ فراہم کرتا ہے (ایسی درخواستوں کو بلاک کردیا جائے گا). True (سچے) = سماجی میڈیا کی توثیق کو فعال کریں [پہلے سے طے شدہ]؛ False (جھوٹی) = سوشل میڈیا کی توثیق کو غیر فعال کریں.</li>
</ul></div>

<div dir="rtl">فی الحال تعاون کی گئی:<br /></div>
<div dir="rtl"><ul>
 <li><strong dir="ltr"><a href="https://udger.com/resources/ua-list/bot-detail?bot=Embedly#id22674">Embedly</a></strong></li>
 <li><strong dir="ltr"><a href="https://developers.facebook.com/docs/sharing/webmasters/crawler/">Facebook external hit</a> **</strong></li>
 <li><strong dir="ltr"><a href="https://help.pinterest.com/en/articles/about-pinterest-crawler-0">Pinterest</a></strong></li>
 <li><strong dir="ltr"><a href="https://udger.com/resources/ua-list/bot-detail?bot=Twitterbot#id6168">Twitterbot</a></strong></li>
</ul></div>

<div dir="rtl"><em>**: ASN تلاش کی فعالیت کی ضرورت ہوتی ہے (جیسے ،BGPView ماڈیول سے).</em><br /></div>

##### <div dir="rtl">"other_verification"<br /></div>
<div dir="rtl"><ul>
 <li>جہاں بھی ممکن ہو، دوسری طرح کی درخواستوں کی تصدیق کرنے کی کوشش کریں (جیسے ایڈسنس، SEO چیکرس، وغیرہ)؟ جب پتہ چلا، جعلی درخواستیں مسدود کردی جائیں گی. True (سچے) = فعال [پہلے سے طے شدہ]؛ False (جھوٹی) = غیر فعال.</li>
</ul></div>

<div dir="rtl">المدعومة حاليا:<br /></div>
<div dir="rtl"><ul>
 <li><strong dir="ltr"><a href="https://adbot.amazon.com/index.html">AmazonAdBot</a></strong></li>
 <li><strong dir="ltr"><a href="https://developers.google.com/search/docs/advanced/crawling/overview-google-crawlers">AdSense</a></strong></li>
 <li><strong dir="ltr"><a href="https://www.oracle.com/corporate/acquisitions/grapeshot/crawler.html">Oracle Data Cloud Crawler</a></strong></li>
</ul></div>

##### <div dir="rtl">"protect_frontend"<br /></div>
<div dir="rtl"><ul>
 <li>متعین کرتا ہے جو عام طور پر CIDRAM طرف سے فراہم کردہ تحفظات سامنے کے آخر پر لاگو کیا جانا چاہیے یا نہیں. سچا = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = کوئی.</li>
</ul></div>

##### <div dir="rtl">"disable_webfonts"<br /></div>
<div dir="rtl"><ul>
 <li>Webfonts کے غیر فعال کریں؟ True (سچے) = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = کوئی.</li>
</ul></div>

##### <div dir="rtl">"maintenance_mode"<br /></div>
<div dir="rtl"><ul>
 <li>بحالی کا موڈ فعال کریں؟ True (سچے) = جی ہاں؛ False (جھوٹی) = کوئی [پہلے سے طے شدہ]. سامنے کے اختتام کے مقابلے میں سب کچھ غیر فعال کرتا ہے. کبھی کبھی آپ کے CMS، فریم ورک، وغیرہ کو اپ ڈیٹ کرنے کے لیے مفید ہے.</li>
</ul></div>

##### <div dir="rtl">"default_algo"<br /></div>
<div dir="rtl"><ul>
 <li>اس بات کی وضاحت کرتا ہے جو تمام مستقبل کے پاس ورڈ اور سیشن کے لیے الگورتھم استعمال کرنا ہے. اختیارات: PASSWORD_DEFAULT (ڈیفالٹ), PASSWORD_BCRYPT, PASSWORD_ARGON2I (PHP >= 7.2.0 کی ضرورت ہے), PASSWORD_ARGON2ID (PHP >= 7.3.0 کی ضرورت ہے).</li>
</ul></div>

##### <div dir="rtl">"statistics"<br /></div>
<div dir="rtl"><ul>
 <li>CIDRAM استعمال کے اعداد و شمار کو ٹریک کریں؟ True (سچے) = جی ہاں؛ False (جھوٹی) = نہیں [پہلے سے طے شدہ].</li>
</ul></div>

##### <div dir="rtl">"force_hostname_lookup"<br /></div>
<div dir="rtl"><ul>
 <li>تمام درخواستوں کے لیے میزبانی حاصل کریں؟ True (سچے) = جی ہاں؛ False (جھوٹی) = نہیں [پہلے سے طے شدہ]. میزبان نام کی تلاش عام طور پر "ضرورت کی بنیاد" کی بنیاد پر انجام دیا جاتا ہے، لیکن تمام درخواستوں کے لیے مجبور کیا جاسکتا ہے. ایسا کرتے ہوئے لاگ ان میں مزید تفصیلی معلومات فراہم کرنے کے ذریعہ مفید ثابت ہوسکتا ہے، لیکن کارکردگی پر تھوڑا منفی اثر بھی ہوسکتا ہے.</li>
</ul></div>

##### <div dir="rtl">"allow_gethostbyaddr_lookup"<br /></div>
<div dir="rtl"><ul>
 <li>جب UDP دستیاب نہیں ہے تو gethostbyaddr کی تلاش کی اجازت دیں؟</li>
 <li>نوٹ: <code dir="ltr">IPv6</code> کی تلاش کچھ <code dir="ltr">32-bit</code> کے نظام پر صحیح طریقے سے کام نہیں کرسکتا.</li>
</ul></div>

##### <div dir="rtl">"hide_version"<br /></div>
<div dir="rtl"><ul>
 <li>لاگ ان اور صفحے کی پیداوار سے ورژن کی معلومات چھپائیں؟ True (سچے) = جی ہاں؛ False (جھوٹی) = نہیں [پہلے سے طے شدہ].</li>
</ul></div>

##### <div dir="rtl">"empty_fields"<br /></div>
<div dir="rtl"><ul>
 <li>جب بلاک ایونٹ کی معلومات لاگ ان اور ڈسپلے کرنا، CIDRAM کو خالی شعبوں کو کیسے ہینڈل کرنا چاہیے؟ "include" = خالی شعبیں شامل کریں. "omit" = خالی خالی جگہیں چھپائیں [پہلے سے طے شدہ].</li>
</ul></div>

##### <div dir="rtl">"log_sanitisation"<br /></div>
<div dir="rtl"><ul>
 <li>لاگز ڈیٹا دیکھنے کے لیے سامنے کے آخر لاگز صفحے کے کا استعمال کرتے وقت کب، XSS حملوں سے صارفین کی حفاظت کے لیے، یہ نمائش سے پہلے نظر ثانی شدہ ہے. لیکن، ہم ایسا نہیں کرتے جب سب سے پہلے اسے ریکارڈ کرنا پڑتا ہے. اگر یہ مستقبل میں اس کا تجزیہ کرنے کی ضرورت ہے تو اس سے مدد مل سکتی ہے. لیکن خارجہ قارئین کا استعمال کرتے وقت یہ کبھی کبھی غیر محفوظ ہوسکتا ہے. اگر ضرورت ہو تو آپ رویے کو تبدیل کرسکتے ہیں. True (سچے) = کم درست، لیکن کم خطرہ. False (جھوٹی) = زیادہ درست، لیکن زیادہ خطرہ [پہلے سے طے شدہ].</li>
</ul></div>

##### <div dir="rtl">"disabled_channels"<br /></div>
<div dir="rtl"><ul>
 <li>درخواستوں کو بھیجنے کے لیے خاص طور پر چینلز کا استعمال کے لیے CIDRAM کو روکنے کے لیے یہ استعمال کیا جا سکتا ہے (مثال کے طور پر، جب اپ ڈیٹ کرنا، اجزاء میٹا ڈیٹا، وغیرہ کو پکڑنے کے بعد).</li>
 <li><em>دستیاب اختیارات: <code dir="ltr">GitHub,BitBucket,GoogleDNS</code></em></li>
</ul></div>

##### <div dir="rtl">"default_timeout"<br /></div>
<div dir="rtl"><ul>
 <li>بیرونی درخواستوں کے لیے استعمال کرنے کیکے لیے پہلے سے طے شدہ ٹائم آؤٹ؟ پہلے سے طے شدہ = 12 سیکنڈ.</li>
</ul></div>

##### <div dir="rtl">"config_imports"<br /></div>
<div dir="rtl"><ul>
 <li>CIDRAM ڈیفالٹ ترتیب میں درآمد کرنے والی فائلیں، کوما کے ذریعہ الگ کردی گئیں. اجزاء کو چالو کرتے وقت اپ ڈیٹس کے صفحے سے بھرا ہوا. زیادہ تر معاملات میں، اسے نظرانداز کر سکتے ہیں.</li>
</ul></div>

##### <div dir="rtl">"events"<br /></div>
<div dir="rtl"><ul>
 <li>یہاں درج فائلیں براہ راست ایونٹ ہینڈلرز فائل کے بعد لوڈ کی جاتی ہیں. اجزاء کو چالو کرتے وقت اپ ڈیٹس کے صفحے سے بھرا ہوا. زیادہ تر معاملات میں، اسے نظرانداز کر سکتے ہیں.</li>
</ul></div>

#### <div dir="rtl">"signatures" (قسم)<br /></div>
<div dir="rtl">دستخط کی ترتیب.<br /><br /></div>

##### <div dir="rtl">"ipv4"<br /></div>
<div dir="rtl"><ul>
 <li>IPv4 کی دستخط کی ایک فہرست فائلوں کہ CIDRAM، کا تجزیہ کرنے کی کوشش کرنا چاہیے کوما سے ختم ہونے والی. آپ یہاں اندراجات کا اضافہ آپ CIDRAM میں اضافی IPv4 کی دستخط کی فائلوں کو شامل کرنے کے لیے چاہتے ہیں تو کر سکتے ہیں.</li>
</ul></div>

##### <div dir="rtl">"ipv6"<br /></div>
<div dir="rtl"><ul>
 <li>IPv6 کی دستخط کی ایک فہرست فائلوں کہ CIDRAM، کا تجزیہ کرنے کی کوشش کرنا چاہیے کوما سے ختم ہونے والی. آپ یہاں اندراجات کا اضافہ آپ CIDRAM میں اضافی IPv6 کی دستخط کی فائلوں کو شامل کرنے کے لیے چاہتے ہیں تو کر سکتے ہیں.</li>
</ul></div>

##### <div dir="rtl">"block_attacks"<br /></div>
<div dir="rtl"><ul>
 <li>حملوں اور دیگر غیر معمولی ٹریفک سے وابستہ CIDRs کو بلاک کریں؟ مثال کے طور پر، پورٹ اسکین، ہیکنگ، کمزوریوں کی تحقیقات وغیرہ. ایسا کرنے جب آپ کو مسائل کا سامنا ہوتا ہے جب تک، عام طور پر، یہ ہمیشہ سچ کے لیے مقرر کیا جانا چاہیے.</li>
</ul></div>

##### <div dir="rtl">"block_cloud"<br /></div>
<div dir="rtl"><ul>
 <li>بلاک CIDR webhosting کے / کلاؤڈ سروسز سے تعلق رکھنے والے کے طور پر شناخت؟ آپ کو آپ کی ویب سائٹ سے ایک API سروس آپریٹ یا اگر آپ دوسری ویب سائٹس کو اپنی ویب سائٹ سے رابطہ قائم کرنے کی توقع ہے تو، تو اس جھوٹے کے لیے مقرر کیا جانا چاہیے. آپ ایسا نہیں کرتے، تو پھر، اس ہدایت صحیح پر سیٹ کیا جانا چاہیے.</li>
</ul></div>

##### <div dir="rtl">"block_bogons"<br /></div>
<div dir="rtl"><ul>
 <li>بلاک bogon/martian کی CIDR؟ آپ لوکل ہوسٹ سے، یا اپنے LAN سے اپنے مقامی نیٹ ورک کے اندر سے اپنی ویب سائٹ پر کنکشن، توقع ہے، اس ہدایت کے جھوٹے پر مقرر کیا جائے چاہیے. اگر آپ ان میں ایسے کنکشنوں کی توقع نہیں ہے، تو اس ہدایت صحیح پر سیٹ کیا جانا چاہیے.</li>
</ul></div>

##### <div dir="rtl">"block_generic"<br /></div>
<div dir="rtl"><ul>
 <li>بلاک کرنے کی سفارش کی CIDRs کو بلاک کرنا؟ یہ دیگر زیادہ مخصوص دستخط کی اقسام میں سے کسی کا حصہ ہونے کے طور پر نشان نہیں ہیں کہ کسی بھی دستخطوں پر محیط ہے.</li>
</ul></div>

##### <div dir="rtl">"block_legal"<br /></div>
<div dir="rtl"><ul>
 <li>قانونی ذمہ داریوں کے جواب میں CIDRs کو بلاک کریں؟ یہ ہدایت عام طور پر کسی بھی اثر نہیں ہونا چاہیے، کیونکہ CIDRAM کسی CIDRs کے ساتھ "قانونی ذمہ داریوں" سے متعلق نہیں ہے، لیکن اس کے باوجود موجود ہے کہ کسی بھی اپنی مرضی کے دستخط فائلوں یا ماڈیولز کے فائدہ کے لیے اضافی کنٹرول کی پیمائش کے طور پر جو قانونی وجوہات کی بناء پر موجود ہو.</li>
</ul></div>

##### <div dir="rtl">"block_malware"<br /></div>
<div dir="rtl"><ul>
 <li>میلویئر کے ساتھ منسلک بلاک CIDRs؟ اس میں C&C سرورز، متاثرہ مشینیں، میلویئر کی تقسیم، وغیرہ میں شامل مشینیں شامل ہیں.</li>
</ul></div>

##### <div dir="rtl">"block_proxies"<br /></div>
<div dir="rtl"><ul>
 <li>پراکسی خدمات یا VPNs سے تعلق رکھنے والے CIDRs کو بلاک کرنا؟ اگر آپ کو ضرورت ہو تو صارفین پراکسی سروسز اور VPNs سے آپ کی ویب سائٹ تک رسائی حاصل کرنے کے قابل ہو جائیں، یہ ہدایت false پر مرتب کرنا چاہیے. دوسری صورت میں، اگر آپ پراکسی خدمات یا VPNs کی ضرورت نہیں ہے، تو یہ ہدایت سیکورٹی کو بہتر بنانے کے ذریعہ true کو مقرر کیا جانا چاہیے.</li>
</ul></div>

##### <div dir="rtl">"block_spam"<br /></div>
<div dir="rtl"><ul>
 <li>بلاک CIDR سپیم کے لیے اعلی خطرے ہونے کے طور پر شناخت کیا؟ ایسا کرنے جب آپ کو مسائل کا سامنا ہوتا ہے جب تک، عام طور پر، یہ ہمیشہ سچ کے لیے مقرر کیا جانا چاہیے.</li>
</ul></div>

##### <div dir="rtl">"modules"<br /></div>
<div dir="rtl"><ul>
 <li>ماڈیول فائلوں کی ایک فہرست کوما سے ختم ہونے والی، IPv4 کی / IPv6 دستخط جانچ پڑتال کے بعد لوڈ کرنے کے لیے.</li>
</ul></div>

##### <div dir="rtl">"default_tracktime"<br /></div>
<div dir="rtl"><ul>
 <li>ماڈیولز کی طرف سے پابندی لگا دی IP ایس کے ٹریک کرنے سیکنڈ کتنے. پہلے سے طے شدہ = 604800 (1 ہفتہ).</li>
</ul></div>

##### <div dir="rtl">"infraction_limit"<br /></div>
<div dir="rtl"><ul>
 <li>خلاف ورزی کی زیادہ سے زیادہ تعداد ایک IP اس سے پہلے کیا جاتا ہے IP باخبر رہنے کے کی طرف سے پابندی کا اطلاق کرنے کی اجازت ہے. پہلے سے طے شدہ = 10.</li>
</ul></div>

##### <div dir="rtl">"track_mode"<br /></div>
<div dir="rtl"><ul>
 <li>خلاف ورزی شمار کب کیا جانا چاہیے؟ False (جھوٹی) = IP ایس کے ماڈیول کی طرف سے بلاک کر رہے ہیں جب. True (سچے) = IP ایس کے کسی بھی وجہ سے بلاک کر رہے ہیں جب. پہلے سے طے شدہ = False (جھوٹی).</li>
</ul></div>

##### <div dir="rtl">"tracking_override"<br /></div>
<div dir="rtl"><ul>
 <li>ماڈیولوں کو ٹریکنگ کے اختیارات کو اوور رائڈ کرنے کی اجازت دیں؟ True (سچے) = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = نہیں.</li>
</ul></div>

#### <div dir="rtl">"recaptcha" اور "hcaptcha" (دونوں ایک ہی اختیارات مہیا کرتے ہیں).<br /></div>
<div dir="rtl">اگر آپ چاہیں، آپ صارفین کو CAPTCHA چیلنج کے ساتھ پیش کرسکتے ہیں تاکہ انہیں بوٹس سے ممتاز کیا جا سکے یا مسدود ہونے کی صورت میں دوبارہ رسائی حاصل کرسکیں. یہ غلط مثبت کو کم کرنے اور ناپسندیدہ خودکار ٹریفک کو کم کرنے میں مدد کرسکتا ہے.<br /><br /></div>

<div dir="rtl"><em>نوٹ: CAPTCHA صرف مشین کالوں کے خلاف حفاظت کرتا ہے، انسانوں کے خلاف نہیں.</em><br /><br /></div>

<div dir="rtl">reCAPTCHA کے لیے، ایک "site key" اور ایک "secret key" حاصل کرنے کے لیے، براہ مہربانی پر جائیں:<br /></div>
<div dir="rtl"><ul>
 <li><div dir="ltr">https://developers.google.com/recaptcha/</div></li>
</ul></div>

<div dir="rtl">hCAPTCHA کے لیے، ایک "site key" اور ایک "secret key" حاصل کرنے کے لیے، براہ مہربانی پر جائیں:<br /></div>
<div dir="rtl"><ul>
 <li><div dir="ltr">https://www.hcaptcha.com/</div></li>
</ul></div>

##### <div dir="rtl">"usemode"<br /></div>
<div dir="rtl"><ul>
 <li>CAPTCHA کب پیش کیا جائے؟ نوٹ: وائٹ لسٹڈ یا توثیق شدہ اور غیر مسدود درخواستوں کو کبھی بھی CAPTCHA کو مکمل کرنے کی ضرورت نہیں ہے.</li>
</ul></div>

&nbsp; <div dir="rtl" style="display:inline">قدر</div> | &nbsp; <div dir="rtl">تفصیل</div>
--:|--:
1 | <div dir="rtl">صرف اس صورت میں جب بلاک ہوجائے، دستخطوں کی حد میں ہو، اور پابندی عائد نہ ہو.</div>
2 | <div dir="rtl">صرف اس صورت میں جب بلاک ہو، استعمال کے لیے خصوصی طور پر نشان زد، دستخطوں کی حد میں ہو، اور پابندی نہیں ہو.</div>
3 | <div dir="rtl">صرف اس وقت جب دستخطوں کی حد میں ہو، اور پابندی عائد نہ ہو (کوئی بات نہیں بلاک ہو یا نہیں).</div>
4 | <div dir="rtl">صرف اس وقت جب بلاک نہیں کیا جاتا ہے.</div>
5 | <div dir="rtl">صرف اس وقت جب بلاک نہ ہوا ہو، یا جب استعمال کے لیے خاص طور پر نشان زد کیا گیا ہو، دستخطوں کی حد میں ہو، اور پابندی نہ ہو.</div>
&nbsp; <div dir="rtl" style="display:inline">کوئی اور قدر.</div> | &nbsp; <div dir="rtl">کبھی نہیں!</div>

##### <div dir="rtl">"lockip"<br /></div>
<div dir="rtl"><ul>
 <li>متعین کرتا ہیشز مخصوص IP ایس کو بند کر دیا جانا چاہیے یا نہیں. False (جھوٹی) = کوکیز اور ہیشز ایک سے زیادہ IP ایس (پہلے سے مقررشدہ) بھر میں استعمال کیا جا سکتا. سچا = کوکیز اور ہیشز ایک سے زیادہ IP ایس کے اس پار نہیں کیا جا سکتا (کوکیز / ہیشز IP ایس کو بند کر دیا جاتا).</li>
 <li>نوٹ: یاد "صارفین" اس قیمت کے لحاظ سے مختلف ہے کے لیے اس طریقہ کار کی وجہ سے "lockip" قدر نظر انداز کر دیا جاتا ہے جب "lockuser" جھوٹی ہے.</li>
</ul></div>

##### <div dir="rtl">"lockuser"<br /></div>
<div dir="rtl"><ul>
 <li>ایک reCAPTCHA/hCAPTCHA مثال کی کامیاب تکمیل کے مخصوص صارفین کے لیے بند کر دیا جانا چاہیے کہ آیا تعین کرتی ہے. False (جھوٹی) = ایک reCAPTCHA/hCAPTCHA مثال کی کامیاب تکمیل reCAPTCHA/hCAPTCHA کے مثال کو مکمل صارف کی طرف سے استعمال کیا جاتا ہے کہ کے طور پر ایک ہی IP سے شروع ہونے والے تمام درخواستوں کو رسائی فراہم کرے گا؛ کوکیز اور ہیشز نہیں استعمال کیا جاتا ہے؛ اس کے بجائے، ایک IP وائٹ لسٹ کا استعمال کیا جائے گا. سچا = ایک reCAPTCHA/hCAPTCHA مثال صرف reCAPTCHA/hCAPTCHA کے مثال کو مکمل صارف تک رسائی کی اجازت دے گا کی کامیاب تکمیل؛ کوکیز اور ہیشز صارف کو یاد کرنے کے لیے استعمال کر رہے ہیں؛ ایک IP وائٹ لسٹ نہیں استعمال کیا جاتا ہے (ڈیفالٹ).</li>
</ul></div>

##### <div dir="rtl">"sitekey"<br /></div>
<div dir="rtl"><ul>
 <li>یہ قدر آپ کے CAPTCHA خدمت کے لیے ڈیش بورڈ میں مل سکتی ہے.</li>
</ul></div>

##### <div dir="rtl">"secret"<br /></div>
<div dir="rtl"><ul>
 <li>یہ قدر آپ کے CAPTCHA خدمت کے لیے ڈیش بورڈ میں مل سکتی ہے.</li>
</ul></div>

##### <div dir="rtl">"expiry"<br /></div>
<div dir="rtl"><ul>
 <li>گھنٹوں کی تعداد CAPTCHA کے واقعات کو یاد کرنے. پہلے سے طے شدہ = 720 (1 ماہ).</li>
</ul></div>

##### <div dir="rtl">"logfile"<br /></div>
<div dir="rtl"><ul>
 <li>تمام CAPTCHA کے کوششوں لاگ؟ اگر ہاں، تو لاگ فائل کے لیے استعمال کرنے کے لیے نام کی وضاحت کریں. اگر نہیں، تو اس متغیر کو خالی چھوڑ دیں.</li>
</ul></div>

<div dir="rtl"><em>مفید ٹپ: "{yyyy}" مکمل سال کے لیے، "{yy}" مختصر سال کے لیے، "{mm}": اگر آپ چاہتے ہیں تو آپ کے نام میں ان کو شامل کرکے آپ لاگ مسلیں کے ناموں کو تاریخ / وقت کی معلومات شامل کر سکتے ہیں مہینے کے لیے، دن کے لیے، "{hh}" گھنٹے کے لیے "{dd}" (ذیل کی مثالیں دیکھ).</em><br /><br /></div>

`logfile='captcha.{yyyy}-{mm}-{dd}-{hh}.txt'`

##### <div dir="rtl">"signature_limit"<br /></div>
<div dir="rtl"><ul>
 <li>CAPTCHA پیش کش واپس لینے سے پہلے دستخطوں کی زیادہ سے زیادہ تعداد کی اجازت. پہلے سے طے شدہ = 1.</li>
</ul></div>

##### <div dir="rtl">"api"<br /></div>
<div dir="rtl"><ul>
 <li>کون سا API استعمال کرنے کے لیے؟</li>
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

<div dir="rtl"><em>یورپی یونین کے صارفین کے لیے نوٹ: جب CIDRAM کوکیز کو استعمال کرنے کے لیے تشکیل دیا جاتا ہے (مثال کے طور پر، جب "lockuser" سچ/true ہے)، ایک کوکی انتباہ <a href="https://www.cookielaw.org/the-cookie-law/">یورپی یونین کوکی قانون سازی</a> کے مطابق دکھایا جاتا ہے. تاہم، جب invisible API کا استعمال کرتے ہوئے، CIDRAM صارف کو خود کار طریقے سے CAPTCHA مکمل کرنے کی کوشش کرتا ہے، اور جب کامیاب ہوجاتا ہے، تو اس کا نتیجہ دوبارہ لوڈ ہونے کی وجہ سے ہو سکتا ہے اور کسی کوکیز کی تخلیق کے بغیر صارف کو مناسب وقت کو کوکیز کو دیکھنے کے لیے کافی وقت نہیں دیا جاسکتا ہے.</em><br /><br /></div>

##### <div dir="rtl">"show_cookie_warning"<br /></div>
<div dir="rtl"><ul>
 <li>کوکی انتباہ دکھائیں؟ True (سچے) = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = نہیں.</li>
</ul></div>

<div dir="rtl"><em>یہ ترتیب درخواست کی طرف سے شامل ہے، لیکن میں اس کو اکیلے چھوڑنے کی سفارش کرتا ہوں.</em><br /><br /></div>

##### <div dir="rtl">"show_api_message"<br /></div>
<div dir="rtl"><ul>
 <li>API کا پیغام دکھائیں؟ True (سچے) = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = نہیں.</li>
</ul></div>

<div dir="rtl"><em>اس سے مراد کسی بھی اضافی، غیر ضروری پیغامات کا حوالہ دیا جاتا ہے جب کوکی انتباہ کے علاوہ کوئی درخواست مسدود ہوجاتی ہے.</em><br /><br /></div>

##### <div dir="rtl">"nonblocked_status_code"<br /></div>
<div dir="rtl"><ul>
 <li>غیر مسدود درخواستوں پر CAPTCHA کی نمائش کرتے وقت کون سا اسٹیٹس کوڈ استعمال کرنا چاہیے؟</li>
</ul></div>

<div dir="rtl">فی الحال تعاون شدہ اقدار:<br /><br /></div>

حیثیت کا کوڈ | حیثیت کا پیغام
---|---
`200` | `200 OK`
`403` | `403 Forbidden`
`418` | `418 I'm a teapot`
`429` | `429 Too Many Requests`
`451` | `451 Unavailable For Legal Reasons`

#### <div dir="rtl">"legal" (قسم)<br /></div>
<div dir="rtl">قانونی ضروریات سے متعلق ترتیب.<br /><br /></div>

<div dir="rtl">قانونی ضروریات کے بارے میں مزید معلومات کے لیے اور یہ آپ کی ترتیبات کی ضروریات کو کس طرح اثر انداز کر سکتا ہے، براہ کرم دستاویزات کے "<a href="#user-content-SECTION11">قانونی معلومات</a>" حصے کا حوالہ دیتے ہیں.<br /><br /></div>

##### <div dir="rtl">"pseudonymise_ip_addresses"<br /></div>
<div dir="rtl"><ul>
 <li>لاگ ان کرتے وقت پی ایس ڈی نامناسب IP پتے؟ True (سچے) = جی ہاں [پہلے سے طے شدہ]؛ False (جھوٹی) = نہیں.</li>
</ul></div>

##### <div dir="rtl">"omit_ip"<br /></div>
<div dir="rtl"><ul>
 <li>لاگ فائلوں سے IP پتے کو خارج کردیں؟ True (سچے) = جی ہاں؛ False (جھوٹی) = نہیں [پہلے سے طے شدہ]. نوٹ: "pseudonymise_ip_addresses" بے شمار ہو جاتا ہے جب "omit_ip" "true" ہے.</li>
</ul></div>

##### <div dir="rtl">"omit_hostname"<br /></div>
<div dir="rtl"><ul>
 <li>لاگ فائلوں سے میزبانوں کو خارج کردیں؟ True (سچے) = جی ہاں؛ False (جھوٹی) = نہیں [پہلے سے طے شدہ].</li>
</ul></div>

##### <div dir="rtl">"omit_ua"<br /></div>
<div dir="rtl"><ul>
 <li>لاگ فائلوں سے صارف کے ایجنٹوں کو خارج کردیں؟ True (سچے) = جی ہاں؛ False (جھوٹی) = نہیں [پہلے سے طے شدہ].</li>
</ul></div>

##### <div dir="rtl">"privacy_policy"<br /></div>
<div dir="rtl"><ul>
 <li>کسی بھی پیدا کردہ صفحات کے فوٹر میں ظاہر ہونے والی متعلقہ رازداری کی پالیسی کا پتہ. ایک URL کی وضاحت کریں، یا غیر فعال کرنے کے لیے خالی چھوڑ دیں.</li>
</ul></div>

#### <div dir="rtl">"template_data" (قسم)<br /></div>
<div dir="rtl">سانچوں اور موضوعات کے لیے ہدایات / متغیر.<br /><br /></div>

<div dir="rtl">"رسائی نہیں ہوئی" کے صفحے پیدا کرنے کے لیے استعمال HTML پیداوار سے متعلق ہے. آپ CIDRAM کے لیے اپنی مرضی کے موضوعات کا استعمال کرتے ہوئے کر رہے ہیں، ایچ ٹی ایم ایل کی پیداوار <code dir="ltr">template_custom.html</code> فائل سے کیے جاتا ہے، اور دوسری صورت میں، HTML پیداوار <code dir="ltr">template.html</code> فائل سے کیے جاتا ہے. ترتیب فائل کے اس شعبہ کو لکھا تغیر اسی متغیر ڈیٹا کے ساتھ ایچ ٹی ایم ایل کی پیداوار کے اندر اندر پایا گھوبگھرالی بریکٹ طرف circumfixed کوئی بھی متغیرہ کے ناموں کی جگہ کی راہ کی طرف HTML پیداوار میں پارس کر رہے ہیں. مثال کے طور پر، جہاں <code dir="ltr">foo="bar"</code> بار کے کسی بھی مثال <code dir="ltr">&lt;p&gt;{foo}&lt;/p&gt;</code> HTML پیداوار کے اندر اندر پایا بن جائے گا <code dir="ltr">&lt;p&gt;bar&lt;/p&gt;</code>.<br /><br /></div>

##### <div dir="rtl">"theme"<br /></div>
<div dir="rtl"><ul>
 <li>CIDRAM کے لیے استعمال کرنے کے لیے ڈیفالٹ تھیم.</li>
</ul></div>

##### <div dir="rtl">"magnification"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Magnification"</em></li>
 <li>فونٹ اضافہ. پہلے سے طے شدہ = 1.</li>
</ul></div>

##### <div dir="rtl">"css_url"<br /></div>
<div dir="rtl"><ul>
 <li>ڈیفالٹ تھیم کے لیے سانچے کی فائل اندرونی سی ایس ایس خصوصیات کا استعمال، جبکہ اپنی مرضی کے موضوعات کے لیے سانچے کی فائل، خارجی سی ایس ایس خصوصیات کا استعمال. اپنی مرضی کے موضوعات کے لیے سانچے کی فائل کو استعمال کرنے CIDRAM ہدایت کرنے کے لیے، "css_url" متغیر کا استعمال کرتے ہوئے آپ کی اپنی مرضی کے موضوع کی سی ایس ایس فائلوں کے عوامی HTTP ایڈریس کی وضاحت. آپ کو اس متغیر خالی چھوڑ تو، CIDRAM ڈیفالٹ تھیم کے لیے سانچے کی فائل کو استعمال کریں گے.</li>
</ul></div>

#### <div dir="rtl">"PHPMailer" (قسم)<br /></div>
<div dir="rtl">PHPMailer ترتیب.<br /><br /></div>

<div dir="rtl">فی الحال، CIDRAM صرف 2FA کے لیے صرف PHPMailer کا استعمال کرتا ہے. اگر آپ سامنے کے اختتام کا استعمال نہیں کرتے ہیں، یا اگر آپ 2FA استعمال نہیں کرتے ہیں، تو آپ ان ہدایات کو نظر انداز کر سکتے ہیں.<br /><br /></div>

##### <div dir="rtl">"event_log"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "EventLog"</em></li>
 <li>PHPMailer کے سلسلے میں تمام واقعات کو لاگ ان کرنے کے لیے ایک فائل. ایک فائل کا نام کی وضاحت کریں، یا غیر فعال کرنے کو خالی چھوڑ.</li>
</ul></div>

##### <div dir="rtl">"skip_auth_process"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "SkipAuthProcess"</em></li>
 <li>جب <code dir="ltr">true</code>، SMTP کی تصدیق کے عمل کو چھوڑ دیا گیا ہے. اس سے بچنا چاہیے. اگر عمل ختم ہو جاتا ہے تو، آؤٹ باؤنڈ ای میل MITM حملوں سے بے نقاب ہوسکتا ہے. مخصوص معاملات میں ضروری ہوسکتا ہے (مثال کے طور پر، جب SMTP سرور مناسب طریقے سے منسلک نہیں کرے گا).</li>
</ul></div>

##### <div dir="rtl">"enable_two_factor"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Enable2FA"</em></li>
 <li>یہ تعین کرتا ہے کہ 2FA استعمال کیا جانا چاہیے.</li>
</ul></div>

##### <div dir="rtl">"host"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Host"</em></li>
 <li>آؤٹ پاؤنڈ ای میل کے لیے استعمال کرنے کے لیے SMTP میزبان.</li>
</ul></div>

##### <div dir="rtl">"port"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Port"</em></li>
 <li>آؤٹ پاؤنڈ ای میل کے لیے استعمال کرنے کے لیے پورٹ نمبر. پہلے سے طے شدہ = 587.</li>
</ul></div>

##### <div dir="rtl">"smtp_secure"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "SMTPSecure"</em></li>
 <li>ای میل بھیجنے پر پروٹوکول استعمال کرنے کے لیے (TLS یا SSL).</li>
</ul></div>

##### <div dir="rtl">"smtp_auth"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "SMTPAuth"</em></li>
 <li>کیا SMTP سیشن کو مستند کیا جاسکتا ہے؟ (عام طور پر اس کو نظر انداز کرنا چاہیے).</li>
</ul></div>

##### <div dir="rtl">"username"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Username"</em></li>
 <li>ای میل بھیجنے کے لیے صارف کا نام.</li>
</ul></div>

##### <div dir="rtl">"password"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "Password"</em></li>
 <li>ای میل بھیجنے کے لیے پاس ورڈ.</li>
</ul></div>

##### <div dir="rtl">"set_from_address"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "setFromAddress"</em></li>
 <li>ای میل بھیجنے کے لیے بھیجنے والے کا پتہ.</li>
</ul></div>

##### <div dir="rtl">"set_from_name"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "setFromName"</em></li>
 <li>ای میل بھیجنے کے لیے بھیجنے کا نام.</li>
</ul></div>

##### <div dir="rtl">"add_reply_to_address"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "addReplyToAddress"</em></li>
 <li>ای میل بھیجنے پر جواب کا پتہ.</li>
</ul></div>

##### <div dir="rtl">"add_reply_to_name"<br /></div>
<div dir="rtl"><ul>
 <li><em>v1: "addReplyToName"</em></li>
 <li>ای میل بھیجنے پر جواب کا نام.</li>
</ul></div>

#### <div dir="rtl">"rate_limiting" (قسم)<br /></div>
<div dir="rtl">شرح محدود کرنے کے اختیارات.<br /><br /></div>

<div dir="rtl">یہ خصوصیت بہت سے صارفین کی درخواستوں کے سبب CIDRAM پر لاگو کیا گیا تھا. البتہ، کیونکہ یہ خاص طور پر CIDRAM کے مطلوبہ مقاصد سے متعلق نہیں ہے، زیادہ سے زیادہ امکانات زیادہ سے زیادہ صارفین کی طرف سے ضرورت نہیں ہوگی. اگر آپ کی حد محدود کرنے کے لیے CIDRAM کی ضرورت ہو تو، یہ خصوصیت آپ کے لیے مفید ثابت ہوسکتا ہے. تاہم، کچھ ضروری چیزیں جنہیں آپ پر غور کرنا چاہیے:</div>
<div dir="rtl"><ul>
 <li>یہ خصوصیت، تمام دیگر CIDRAM کی خصوصیات، صرف CIDRAM کی طرف سے محفوظ صفحات کے لیے کام کریں گے. لہذا، ویب سائٹ کے اثاثوں کو محدود نہیں ہوسکتا ہے اگر وہ CIDRAM کے ذریعہ نہیں رہیں.</li>
 <li>اگر آپ سرور ماڈیول، cPanel، یا محدود نیٹ ورک کا آلہ محدود کرنے کے لۓ استعمال کرتے ہیں تو آپ کو حد تک محدود کرنے کے لیے CIDRAM کے بجائے استعمال کرنا چاہیے.</li>
 <li>اگر، محدود ہونے کے بعد، ایک خاص صارف آپ کی ویب سائٹ تک رسائی جاری رکھنے کے لیے چاہتا ہے، پھر زیادہ تر معاملات میں، ان کے لیے حد تک محدود کرنے کے لیے بہت آسان ہو جائے گا (مثال کے طور پر، اگر وہ اپنے IP ایڈریس کو تبدیل کرتے ہیں، یا اگر وہ پراکسی یا VPN استعمال کرتے ہیں، اور یہ فرض کریں کہ آپ نے پراکس اور وی پی این کو بلاک نہیں کرنے کے لیے CIDRAM کو تشکیل دیا ہے، یا CIDRAM پراکسی یا VPN سے متعلق نہیں ہے کہ وہ استعمال کرتے ہیں).</li>
 <li>یہ خصوصیت صارفین کے لیے بہت پریشانی ہوسکتی ہے. اگر آپ دستیاب دستیاب بینڈوڈتھ بہت محدود ہے تو یہ ضروری ہوسکتا ہے، اور اگر آپ کو معلوم ہوتا ہے کہ ٹریفک کے کچھ مخصوص ذرائع موجود ہیں، پہلے ہی دوسری صورت میں بند نہیں ہوسکتا ہے، تو یہ آپ کے دستیاب بینڈوڈتھ کی اکثریت کو استعمال کر رہے ہیں. اگرچہ ضروری نہیں ہے تو، شاید اس سے بچنا چاہیے.</li>
 <li>آپ کبھی کبھار اپنے آپ کو یا جائز صارفین کو روکنے کا خطرہ کر سکتے ہیں.</li>
</ul></div>

<div dir="rtl">اگر آپ کو اپنی ویب سائٹ کے لیے محدود کرنے کی شرح کو لاگو کرنے کے لیے CIDRAM کی ضرورت نہیں ہے تو ذیل میں ہدایات کو ان کے ڈیفالٹ اقدار کے طور پر مقرر کریں. دوسری صورت میں، آپ اپنی ضروریات کو پورا کرنے کے لیے اپنے اقدار تبدیل کرسکتے ہیں.<br /><br /></div>

##### <div dir="rtl">"max_bandwidth"<br /></div>
<div dir="rtl"><ul>
 <li>بینڈوڈتھ کی زیادہ سے زیادہ رقم کی اجازت کے عرصے میں اجازت دی گئی ہے. جب سے تجاوز کی گئی، مستقبل کی درخواستوں کی شرح محدود ہے. جب 0، اس قسم کی محدود استعمال نہیں کی جائے گی. پہلے سے طے شدہ = 0KB.</li>
</ul></div>

##### <div dir="rtl">"max_requests"<br /></div>
<div dir="rtl"><ul>
 <li>الاؤنس کی مدت کے اندر اندر زیادہ سے زیادہ درخواستوں کی اجازت دی گئی ہے. جب سے تجاوز کی گئی، مستقبل کی درخواستوں کی شرح محدود ہے. جب 0، اس قسم کی محدود استعمال نہیں کی جائے گی. پہلے سے طے شدہ = 0.</li>
</ul></div>

##### <div dir="rtl">"precision_ipv4"<br /></div>
<div dir="rtl"><ul>
 <li>IPv4 استعمال کی نگرانی کرتے وقت استعمال کرنے کی صحت سے متعلق. قیمت CIDR بلاک سائز کی عکاسی کرتا ہے. بہترین صحت سے متعلق کے لیے 32 پر مقرر کریں. پہلے سے طے شدہ = 32.</li>
</ul></div>

##### <div dir="rtl">"precision_ipv6"<br /></div>
<div dir="rtl"><ul>
 <li>IPv6 استعمال کی نگرانی کرتے وقت استعمال کرنے کی صحت سے متعلق. قیمت CIDR بلاک سائز کی عکاسی کرتا ہے. بہترین صحت سے متعلق کے لیے 128 پر مقرر کریں. پہلے سے طے شدہ = 128.</li>
</ul></div>

##### <div dir="rtl">"allowance_period"<br /></div>
<div dir="rtl"><ul>
 <li>استعمال کی نگرانی کے لیے گھنٹوں کی تعداد. پہلے سے طے شدہ = 0.</li>
</ul></div>

##### <div dir="rtl">"exceptions"<br /></div>
<div dir="rtl"><ul>
 <li>مستثنیات (یعنی، درخواستوں کو جس کی شرح محدود نہیں ہونی چاہیے). متعلقہ صرف اس وقت جب شرح کی حد بندی قابل ہو.</li>
 <li><em>دستیاب اختیارات: <code dir="ltr">Whitelisted,Verified</code></em></li>
</ul></div>

#### <div dir="rtl">"supplementary_cache_options" (قسم)<br /></div>
<div dir="rtl">اضافی کیشنگ کے اختیارات.<br /><br /></div>

##### <div dir="rtl">"prefix"<br /></div>
<div dir="rtl"><ul>
 <li>یہاں بیان کردہ قدر کو تمام کیش انٹری کیز کے ساتھ پہلے سے جوڑا جائے گا. بطور ڈیفالٹ خالی. جب ایک ہی سرور پر متعدد تنصیبات موجود ہوں، تو یہ ان کے کیچز کو ایک دوسرے سے الگ رکھنے کے لیے مفید ہو سکتا ہے.</li>
</ul></div>

##### <div dir="rtl">"enable_apcu"<br /></div>
<div dir="rtl"><ul>
 <li>اس کی وضاحت کرتا ہے کہ کیش کے لیے APCu استعمال کرنا چاہے. پہلے سے طے شدہ = False (جھوٹی).</li>
</ul></div>

##### <div dir="rtl">"enable_memcached"<br /></div>
<div dir="rtl"><ul>
 <li>اس کی وضاحت کرتا ہے کہ کیش کے لیے Memcached استعمال کرنا چاہے. پہلے سے طے شدہ = False (جھوٹی).</li>
</ul></div>

##### <div dir="rtl">"enable_redis"<br /></div>
<div dir="rtl"><ul>
 <li>اس کی وضاحت کرتا ہے کہ کیش کے لیے Redis استعمال کرنا چاہے. پہلے سے طے شدہ = False (جھوٹی).</li>
</ul></div>

##### <div dir="rtl">"enable_pdo"<br /></div>
<div dir="rtl"><ul>
 <li>اس کی وضاحت کرتا ہے کہ کیش کے لیے PDO استعمال کرنا چاہے. پہلے سے طے شدہ = False (جھوٹی).</li>
</ul></div>

##### <div dir="rtl">"memcached_host"<br /></div>
<div dir="rtl"><ul>
 <li>Memcached کے میزبان نام. پہلے سے طے شدہ = "localhost".</li>
</ul></div>

##### <div dir="rtl">"memcached_port"<br /></div>
<div dir="rtl"><ul>
 <li>Memcached کے لیے بندرگاہ. پہلے سے طے شدہ = "11211".</li>
</ul></div>

##### <div dir="rtl">"redis_host"<br /></div>
<div dir="rtl"><ul>
 <li>Redis کے میزبان نام. پہلے سے طے شدہ = "localhost".</li>
</ul></div>

##### <div dir="rtl">"redis_port"<br /></div>
<div dir="rtl"><ul>
 <li>Redis کے لیے بندرگاہ. پہلے سے طے شدہ = "6379".</li>
</ul></div>

##### <div dir="rtl">"redis_timeout"<br /></div>
<div dir="rtl"><ul>
 <li>Redis کے لیے ٹائم آؤٹ. پہلے سے طے شدہ = "2.5".</li>
</ul></div>

##### <div dir="rtl">"pdo_dsn"<br /></div>
<div dir="rtl"><ul>
 <li>PDO کے لیے DSN. پہلے سے طے شدہ = "<code dir="ltr">mysql:dbname=cidram;host=localhost;port=3306</code>".</li>
</ul></div>

<div dir="rtl"><em>(بھی دیکھو: <a href="#user-content-HOW_TO_USE_PDO">"PDO DSN" کیا ہے؟ میں CIDRAM کے ساتھ PDO کیسے استعمال کرسکتا ہوں؟</a>)</em><br /><br /></div>

##### <div dir="rtl">"pdo_username"<br /></div>
<div dir="rtl"><ul>
 <li>PDO کے لیے صارف نام.</li>
</ul></div>

##### <div dir="rtl">"pdo_password"<br /></div>
<div dir="rtl"><ul>
 <li>PDO کے لیے پاس ورڈ.</li>
</ul></div>

---


### <div dir="rtl">۷. <a name="SECTION7"></a>دستخط فارمیٹ</div>

<div dir="rtl">بھی دیکھو:<br /></div>
<div dir="rtl"><ul>
 <li><a href="#user-content-WHAT_IS_A_SIGNATURE">ایک "دستخط" کیا ہے؟</a></li>
</ul></div>

#### <div dir="rtl">۷.۰ مبادیات (دستخط فائلوں کے لیے)<br /><br /></div>

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

<div dir="rtl">عین مطابق اور درست CIDR سنکیتن کی ضرورت ہے، دوسری صورت سکرپٹ دستخط کو تسلیم نہیں کریں گے. مزید برآں، اس سکرپٹ کی تمام CIDR دستخط ایک IP ایڈریس جن IP نمبر، اس کی CIDR بلاک سائز (مثلا طرف سے نمائندگی آپ <code dir="ltr">"11.127.255.255"</code> کرنا <code dir="ltr">"10.128.0.0"</code> سے تمام IP ایس کو بلاک کرنا چاہتے تھے تو بلاک ڈویژن میں یکساں طور پر تقسیم کر سکتے ہیں کے ساتھ شروع ہونا چاہیے، <code dir="ltr">"10.128.0.0/8"</code> سکرپٹ کی طرف سے تسلیم نہیں کیا جائے گا، لیکن"</code> 10.128.0.0/9"</code> اور <code dir="ltr">"11.0.0.0/9"</code> مل کر میں استعمال کیا جاتا ہے، سکرپٹ کی طرف سے تسلیم کیا جائے گا).<br /><br /></div>

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

<div dir="rtl">تو "Whitelist" استعمال کیا جاتا ہے، دستخط شروع ہوجاتا ہے جب اسکرپٹ تمام detections کر (کسی detections کر ہوئی ہے تو) دوبارہ ترتیب دے گا اور ٹیسٹ کی تقریب کو توڑنے. "[پرم]" نظر انداز کر دیا جاتا ہے. اس تقریب کا پتہ چلا جا رہا ہے سے ایک مخصوص IP یا CIDR وائٹ لسٹ کے برابر ہے.<br /><br /></div>

`127.0.0.1/32 Whitelist`

<div dir="rtl">تو "Greylist" استعمال کیا جاتا ہے، دستخط شروع ہوجاتا ہے جب اسکرپٹ تمام detections کر (کسی detections کر ہوئی ہے تو) دوبارہ ترتیب دے گا اور پروسیسنگ جاری رکھنے کے لیے اگلے کے دستخط کی فائل کو چھوڑ دیں. "[پرم]" نظر انداز کر دیا جاتا ہے.<br /><br /></div>

`127.0.0.1/32 Greylist`

<div dir="rtl">سگنیچر شروع ہوجاتا ہے جب "Deny" استعمال کیا جاتا ہے،، کوئی وائٹ لسٹ کے دستخط سنبھالنے دی IP ایڈریس اور / یا دی CIDR کے لیے متحرک کیا گیا ہے تو، محفوظ صفحے کی رسائی نہیں دی جائے گی. "Deny" کیا آپ واقعی ایک IP ایڈریس اور / یا CIDR رینج کو بلاک کرنے کے لیے استعمال کرنا چاہتے ہیں کریں گے کیا ہے. کوئی بھی دستخط متحرک کر رہے ہیں جب کے استعمال بنانے کے کہ "Deny"، "رسائی نہیں ہوئی" اسکرپٹ کا صفحہ پیدا کیا جائے گا اور ہلاک محفوظ صفحے کی درخواست.<br /><br /></div>

<div dir="rtl">"[پرم]" "Deny" کی طرف سے قبول کی قیمت، "رسائی نہیں ہوئی" کے صفحے کی پیداوار میں پارس کیا جائے گا کی تردید کی جا رہی مطلوبہ صفحہ تک ان کی رسائی کے لیے حوالہ دیا وجہ کے طور پر کلائنٹ / صارف کے لیے فراہم کی. یہ آپ کو ان کے (کچھ بھی، کافی چاہیے یہاں تک کہ ایک سادہ "میں آپ کو اپنی ویب سائٹ پر چاہتے ہیں نہیں ہے")، یا آشلپی الفاظ کی ایک چھوٹی سی مٹھی بھر کے ایک سے فراہم بلاک کرنے کے لیے منتخب کیا ہے یہی وجہ ہے کہ یا تو ایک مختصر اور سادہ قید کی سزا، کی وضاحت ہو سکتا ہے سکرپٹ کی طرف سے استعمال کیا ہے تو کہ میں کیوں کلائنٹ / صارف مسدود کر دیا گیا ہے ایک پہلے سے تیار وضاحت کے ساتھ سکرپٹ کی طرف سے تبدیل کیا جائے گا.<br /><br /></div>

<div dir="rtl">پہلے سے تیار وضاحتوں L10N حمایت حاصل ہے اور زبان آپ کو سکرپٹ کی ترتیب کے "lang" ہدایت کرنے کی وضاحت کی بنیاد پر سکرپٹ کی طرف سے فراہم کیا جا سکتا. کے علاوہ، آپ کو نظر انداز کی بنیاد پر دستخط "Deny" کرنا سکرپٹ کو ہدایت کر سکتے ہیں ان کے "[پرم]" قدر سکرپٹ کی ترتیب کی طرف سے مخصوص ہدایات کے ذریعے (وہ ان آشلپی الفاظ استعمال کر رہے ہیں) (ہر آشلپی لفظ ایک اسی ہدایت کی ہے یا تو کرنے کے لیے اسی دستخط عملدرآمد یا ان کو نظر انداز کرنے کی). "[پرم]" اقدار، ان آشلپی الفاظ استعمال کرتے ہیں کہ نہیں تاہم L10N حمایت کی ضرورت نہیں ہے اور اس وجہ سے سکرپٹ کی طرف سے فراہم نہیں کیا جائے گا، اور اس کے علاوہ، سکرپٹ کی ترتیب کی طرف سے براہ راست نینترنیی نہیں ہیں آپ آشلپی الفاظ یہ ہیں:<br /></div>
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

#### <div dir="rtl">۷.۱ ٹیگز<br /><br /></div>

##### <div dir="rtl">۷.۱.۰ سیکشن ٹیگ<br /><br /></div>

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

<div dir="rtl">سیکشن ٹیگنگ توڑنے اور یقینی بنانے کے لیے ٹیگز غلط طریقے سے دستخط کی فائلوں میں پہلے سے دستخط کے حصوں کو شناخت نہیں کر رہے ہیں کہ، صرف آپ کے ٹیگ اور آپ کے شروع کے دستخط حصوں کے درمیان کم از کم دو مسلسل نیولائنز سے ہیں اس بات کا یقین. کوئی غیر ٹیگ شدہ دستخط "IPv4 کی" یا "IPv6 کی" (دستخط کی اقسام کو متحرک کیا جا رہا ہے جس پر منحصر ہے) خواہ کو فطری گا.<br /><br /></div>

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: سیکشن 1
```

<div dir="rtl">اوپر کی مثال میں<code dir="ltr">"1.2.3.4/32"</code> اور<code dir="ltr">"2.3.4.5/32"</code> "IPv4" کی کے طور پر ٹیگ کیا جائے گا، جبکہ<code dir="ltr">"4.5.6.7/32"</code> اور<code dir="ltr">"5.6.7.8/32"</code> "سیکشن 1" کے طور پر ٹیگ کیا جائے گا.<br /><br /></div>

<div dir="rtl">اسی منطق کو بھی دیگر اقسام کے ٹیگ کو الگ کرنے کے لیے لاگو کیا جا سکتا ہے.<br /><br /></div>

<div dir="rtl">خاص طور پر، سیکشن ٹیگ کو ڈیبگنگ کے لیے بہت مفید ثابت ہوسکتا ہے جب غلط مثبت واقع ہوسکتا ہے، اس مسئلے کا صحیح ذریعہ تلاش کرنے کا آسان ذریعہ فراہم کرنے کے ذریعہ، اور وہ لاگ ان کے لاگ ان صفحے کے ذریعے لاگ فولائل کو دیکھتے وقت لاگ ان کی اندراجات کو فلٹر کرنے کے لیے بہت مفید ہوسکتے ہیں (سیکشن کے نام سامنے کے آخر میں لاگ ان صفحے کے ذریعے کلک کی جا سکتی ہے اور فلٹرنگ کے معیار کے طور پر استعمال کیا جا سکتا ہے). اگر کسی خاص دستخط کے لیے سیکشن ٹیگ کو چھوڑ دیا جاتا ہے تو، جب دستخط کیے جائیں گے تو، CIDRAM کے پاس آئیکریس فائل کا نام استعمال ہوتا ہے جس کے ساتھ IP ایڈریس کو بلاک کردیا گیا ہے (IPv4 یا IPv6) کے نتیجے میں، اور اس طرح سیکشن ٹیگ مکمل طور پر اختیاری ہیں. بعض صورتوں میں ان کی سفارش کی جاسکتی ہے، مثلا جب دستخط شدہ فائلوں کو نام نہاد نامزد کیا جاسکتا ہے یا جب یہ دوسری صورت میں واضح طور پر دستخط کرنے کے لیے درخواست کی وجہ سے واضح طور پر دستخط کرنا مشکل ہوسکتا ہے.<br /><br /></div>

##### <div dir="rtl">۷.۱.۱ ختم ہونے والی ٹیگ<br /><br /></div>

<div dir="rtl">آپ دستخط سیکشن ٹیگز کو اسی انداز میں، کچھ وقت کے بعد ختم کرنا چاہتے ہیں تو، آپ کو متعین کرنے کی ایک "ختم ہونے ٹیگ" استعمال دستخط درست نہیں رہے چاہیے جب سکتا. ختم ہونے ٹیگز شکل <code dir="ltr">"YYYY.MM.DD"</code> استعمال کرتے ہیں (ذیل کی مثال دیکھیں).<br /><br /></div>

```
# سیکشن 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

<div dir="rtl">متوقع دستخط کسی بھی درخواست پر کبھی نہیں چلائے جائیں گے، کوئی بات نہیں.<br /><br /></div>

##### <div dir="rtl">۷.۱.۲ اصل ٹیگ<br /><br /></div>

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

##### <div dir="rtl">۷.۱.۳ دھن ٹیگ<br /><br /></div>

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

#### <div dir="rtl">۷.۱.۴ پروفائل ٹیگ<br /><br /></div>

<div dir="rtl">پروفائل ٹیگز ٹیسٹ پیج پر اضافی معلومات ظاہر کرنے کا ایک ذریعہ فراہم کرتے ہیں، اور زیادہ پیچیدہ سلوک اور بہتر فیصلہ سازی کے لیے استعمال کیا جاسکتا ہے.<br /><br /></div>

<div dir="rtl">دوسرے قسم کے ٹیگز کی طرح ہی پروفائل ٹیگز استعمال ہوتے ہیں. پروفائل ٹیگ کی اقدار کو ماڈیولز اور معاون قواعد کی شرط کے طور پر استعمال کیا جاسکتا ہے. پروفائل ٹیگ ان اقدار کو سیمیکن سے الگ کرکے ایک سے زیادہ اقدار فراہم کرسکتے ہیں. آخری صارف پروفائل ٹیگ کی قدر کبھی نہیں دیکھتا ہے.<br /><br /></div>

<div dir="rtl">مثال:<br /><br /></div>

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### <div dir="rtl">۷.۲ YAML<br /><br /></div>

#### <div dir="rtl">۷.۲.۰ YAML مبادیات<br /><br /></div>

<div dir="rtl">مکمل طور پر اختیاری (یعنی آپ اسے استعمال کرتے ہیں تو آپ کا انتخاب ہے) YAML نشانات استعمال کرتے ہوئے، اور ترتیب میں سے اکثر کا فائدہ اٹھانے کے قابل ہے.<br /><br /></div>

<div dir="rtl">CIDRAM میں، تین ڈیشز ("---") کا استعمال کرتے ہوئے تعین کیا YAML جاتا ہے، اور وہ دو نئے لائنوں کا استعمال کرتے ہوئے ختم. مندرجہ ذیل مثال:<br /><br /></div>

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

##### <div dir="rtl">۷.۲.۱ کس طرح "خاص نشان" reCAPTCHA/hCAPTCHA کے ساتھ استعمال کریں کے لیے دستخط قسموں<br /><br /></div>

<div dir="rtl">جب <code dir="ltr">"usemode"</code> 2 یا 5 ہے، "خاص نشان" reCAPTCHA/hCAPTCHA کے ساتھ استعمال کے لیے دستخط حصوں، ایک اندراج ہے کہ دستخط کے حصے کے لیے YAML طبقہ میں (ذیل کی مثال ملاحظہ کریں) شامل ہے کرنے کے لیے.<br /><br /></div>

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

#### <div dir="rtl">۷.۳ معاون<br /><br /></div>

##### <div dir="rtl">۷.۳.۰ دستخط کے حصوں کو نظر انداز کرنا<br /><br /></div>

<div dir="rtl">کے علاوہ، آپ CIDRAM مکمل طور پر دستخط کی فائلوں میں سے کسی کے اندر کچھ مخصوص حصوں کو نظر انداز کرنا چاہتے ہیں تو، آپ "ignore.dat" فائل ہے جس میں حصوں کو نظر انداز کرنے کی وضاحت کرنے کے لیے استعمال کر سکتے ہیں. ایک نئی لائن پر، لکھنا "Ignore"، ایک کی جگہ کے بعد، آپ کو CIDRAM نظر انداز کرنا (ذیل کی مثال ملاحظہ کریں) چاہتے ہیں کہ سیکشن کے نام کے بعد<br /><br /></div>

```
Ignore سیکشن 1
```

<div dir="rtl">یہ CIDRAM سامنے کے آخر "حصوں کی فہرست" کے صفحے کے ذریعہ بھی حاصل کیا جا سکتا ہے.<br /><br /></div>

##### <div dir="rtl">۷.۳.۱ معاون قوانین<br /><br /></div>

<div dir="rtl">اگر آپ محسوس کرتے ہیں کہ آپ اپنی مرضی کے دستخط شدہ فائلوں کو لکھتے ہیں یا اپنی مرضی کے مطابق ماڈیولز آپ کے لیے بہت پیچیدہ ہیں، ایک آسان متبادل سیڈامیم سامنے کے آخر "معاون قواعد" کے صفحے کا استعمال کرنا ہوسکتا ہے. مناسب اختیارات کا انتخاب کرتے ہوئے اور مخصوص قسم کے درخواستوں کے بارے میں تفصیلات کی وضاحت کرکے، آپ ان ہدایات کو جواب دینے کے بارے میں CIDRAM کو ہدایت کرسکتے ہیں. تمام دستخط شدہ فائلوں کے بعد "معاون قواعد" کو معطل کر دیا جاتا ہے اور ماڈیولز نے پہلے سے ہی عملدرآمد مکمل کر لیا ہے.<br /><br /></div>

#### <div dir="rtl">۷.۴ <a name="MODULE_BASICS"></a>مبادیات (ماڈیولز کے لیے)<br /><br /></div>

<div dir="rtl">ماڈیولز CIDRAM کی فعالیت کو بڑھانے کے لیے استعمال کیا جا سکتا ہے، اضافی کاموں کو انجام دینے کے لیے، یا اضافی منطق پر عمل درآمد.<br /><br /></div>

<div dir="rtl">کیونکہ ماڈیولز PHP کی فائلوں کے طور پر لکھی جاتی ہیں، اگر آپ CIDRAM کوڈ بیس کے ساتھ مناسب طریقے سے واقف ہیں تو، آپ اپنی ماڈیول اور ماڈیول دستخط کی تشکیل کرسکتے ہیں تاہم آپ چاہتے ہیں (PHP کے ساتھ کیا ممکن ہے کی مناسب حدود کے اندر اندر).<br /><br /></div>

<div dir="rtl"><em>نوٹ: اگر آپ PHP کے کوڈ کے ساتھ کام کرنے میں آرام دہ اور پرسکون نہیں ہیں تو، آپ کے اپنے ماڈیول لکھنے کی سفارش نہیں کی جاتی ہے.</em><br /><br /></div>

<div dir="rtl">کچھ فعالیتیں CIDRAM کی طرف سے فراہم کی جاتی ہیں جو اپنے ماڈیولز کو لکھنے کے لیے آسان اور آسان بنانا چاہیے. اس فعالیت کے بارے میں معلومات ذیل میں بیان کی گئی ہے.<br /><br /></div>

#### <div dir="rtl">۷.۵ ماڈیول فعالیت<br /><br /></div>

##### <div dir="rtl">۷.۵.۰ <code dir="ltr">$Trigger</code></div>

<div dir="rtl">ماڈیول دستخط عام طور پر <code dir="ltr">$Trigger</code> کے ساتھ لکھا جاتا ہے. زیادہ تر معاملات میں، یہ بندش ماڈیول لکھنے کے مقصد کے لیے کسی اور سے کہیں زیادہ اہم ہو گی.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$Trigger</code> ۴ پیرامیٹرز کو قبول کرتا ہے: <code dir="ltr">$Condition</code>، <code dir="ltr">$ReasonShort</code>، <code dir="ltr">$ReasonLong</code> (اختیاری)، <code dir="ltr">$DefineOptions</code> (اختیاری).<br /><br /></div>

<div dir="rtl"><code dir="ltr">$Condition</code> سچائی کا اندازہ کیا جاتا ہے. اگر یہ سچ (true) ہے تو، دستخط چالو ہے. اگر یہ غلط (false) ہے تو، دستخط چالو نہیں ہے. <code dir="ltr">$Condition</code> عام طور پر ایک ایسی شرط پر مشتمل ہے جس کی وجہ سے کسی درخواست کو بلاک کرنا ہوگا.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonShort</code> کو "کیوں بلاک شدہ" فیلڈ میں حوالہ دیا جاتا ہے جب دستخط چالو ہوجاتا ہے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonLong</code> صارف کو ظاہر ہونے پر ایک پیغام ہے جب وہ روک رہے ہیں، اس وجہ سے وضاحت کریں کہ. ختم ہونے پر معیاری "کیوں بلاک شدہ" پیغام استعمال کرتا ہے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$DefineOptions</code> ایک اختیاری سرنی ہے جس میں کلیدی/قدر شامل ہیں، درخواست کی مثال کے مطابق مخصوص ترتیبات کے اختیارات کی وضاحت کرنے کے لیے استعمال کیا جاتا ہے. جب دستخط چالو ہو تو ترتیب کے اختیارات لاگو کیے جائیں گے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$Trigger</code> سچ ہے جب دستخط چالو ہوجاتا ہے، اور جب غلط نہیں ہوتا تو غلط ہوتا ہے.<br /><br /></div>

<div dir="rtl">اپنے ماڈیول میں اس بندش کو استعمال کرنے کے لیے، سب سے پہلے اسے والدین کی دائرہ داری سے وارث کرنے کے لیے یاد رکھیں:<br /><br /></div>

```PHP
$Trigger = $CIDRAM['Trigger'];
```

##### <div dir="rtl">۷.۵.۱ <code dir="ltr">$Bypass</code></div>

<div dir="rtl">دستخط بائی پاسز عام طور پر <code dir="ltr">$Bypass</code> کے ساتھ لکھے جاتے ہیں.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$Bypass</code> ۳ پیرامیٹرز کو قبول کرتا ہے: <code dir="ltr">$Condition</code>، <code dir="ltr">$ReasonShort</code>، <code dir="ltr">$DefineOptions</code> (اختیاری).<br /><br /></div>

<div dir="rtl"><code dir="ltr">$Condition</code> سچائی کا اندازہ کیا جاتا ہے. اگر یہ سچ (true) ہے تو، بائی پاس چالو ہے. اگر یہ غلط (false) ہے تو، بائی پاس چالو نہیں ہے. <code dir="ltr">$Condition</code> عام طور پر ایک ایسی شرط پر مشتمل ہے جو کسی کو بلاک کرنے کی درخواست نہیں بننی چاہیے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$ReasonShort</code> کو "کیوں بلاک شدہ" فیلڈ میں حوالہ دیا جاتا ہے جب بائی پاس چالو ہوجاتا ہے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$DefineOptions</code> ایک اختیاری سرنی ہے جس میں کلیدی/قدر شامل ہیں، درخواست کی مثال کے مطابق مخصوص ترتیبات کے اختیارات کی وضاحت کرنے کے لیے استعمال کیا جاتا ہے. جب دستخط چالو ہو تو ترتیب کے اختیارات لاگو کیے جائیں گے.<br /><br /></div>

<div dir="rtl"><code dir="ltr">$Bypass</code> سچ ہے جب بائی پاس چالو ہوجاتا ہے، اور جب غلط نہیں ہوتا.<br /><br /></div>

<div dir="rtl">اپنے ماڈیول میں اس بندش کو استعمال کرنے کے لیے، سب سے پہلے اسے والدین کی دائرہ داری سے وارث کرنے کے لیے یاد رکھیں:<br /><br /></div>

```PHP
$Bypass = $CIDRAM['Bypass'];
```

##### <div dir="rtl">۷.۵.۲ <code dir="ltr">"$CIDRAM['DNS-Reverse']"</code></div>

<div dir="rtl">یہ ایک IP ایڈریس کے میزبان نام کو حاصل کرنے کے لیے استعمال کیا جا سکتا ہے. اگر آپ میزبانوں کو روکنے کے لیے ماڈیول بنانا چاہتے ہیں، تو یہ بندش مفید ثابت ہوسکتا ہے.<br /><br /></div>

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

#### <div dir="rtl">۷.۶ ماڈیول متغیر<br /><br /></div>

<div dir="rtl">ماڈیول ان کے اپنے گنجائش کے اندر عملدرآمد کرتے ہیں، اور کسی ماڈیول کی طرف سے وضاحت کردہ متغیرات، دوسرے ماڈیولز، یا پیراگراف اسکرپٹ تک نہیں پہنچ سکیں گے، جب تک کہ وہ <code dir="ltr">$CIDRAM</code> صف میں محفوظ نہ ہو جائیں (ماڈیول پھانسی ختم ہونے کے بعد سب کچھ صاف ہو گیا ہے).<br /><br /></div>

<div dir="rtl">مندرجہ ذیل فہرست کچھ عام متغیر ہیں جو آپ کے ماڈیول کے لیے مفید ہوسکتے ہیں:<br /><br /></div>

&nbsp; <div dir="rtl" style="display:inline">تفصیل</div> | <div dir="rtl">متغیر</div>
----|----
&nbsp; <div dir="rtl" style="display:inline">موجودہ تاریخ اور وقت.</div> | `$CIDRAM['BlockInfo']['DateTime']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کے لیے IP ایڈریس.</div> | `$CIDRAM['BlockInfo']['IPAddr']`
&nbsp; <div dir="rtl" style="display:inline">CIDRAM سکرپٹ ورژن.</div> | `$CIDRAM['BlockInfo']['ScriptIdent']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کے لیے سوال.</div> | `$CIDRAM['BlockInfo']['Query']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کے لیے ریفرر (اگر ایک موجود ہے).</div> | `$CIDRAM['BlockInfo']['Referrer']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کے لیے صارف ایجنٹ (user agent).</div> | `$CIDRAM['BlockInfo']['UA']`
&nbsp; <div dir="rtl" style="display:inline">موجودہ درخواست کے لیے کم کیس میں صارف ایجنٹ (user agent).</div> | `$CIDRAM['BlockInfo']['UALC']`
&nbsp; <div dir="rtl" style="display:inline">جب صارف کو بلاک کردیا جاتا ہے تو صارف کو ظاہر کرنے کا پیغام.</div> | `$CIDRAM['BlockInfo']['ReasonMessage']`
&nbsp; <div dir="rtl" style="display:inline">دستخط کی تعداد موجودہ درخواست کے لیے شروع ہوگئی ہے.</div> | `$CIDRAM['BlockInfo']['SignatureCount']`
&nbsp; <div dir="rtl" style="display:inline">کسی بھی دستخط کے لیے حوالہ کی معلومات موجودہ درخواست کے لیے تیار ہوئی.</div> | `$CIDRAM['BlockInfo']['Signatures']`
&nbsp; <div dir="rtl" style="display:inline">کسی بھی دستخط کے لیے حوالہ کی معلومات موجودہ درخواست کے لیے تیار ہوئی.</div> | `$CIDRAM['BlockInfo']['WhyReason']`

---


### <div dir="rtl">۸. <a name="SECTION8"></a>جانا جاتا مطابقت کے مسائل</div>

<div dir="rtl">مندرجہ ذیل پیکجوں اور مصنوعات کو CIDRAM کے ساتھ مطابقت پذیر ہونے کے لیے مل گیا ہے:</div>
<div dir="rtl"><ul>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/52">Endurance Page Cache</a></strong></li>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/80">Mix.com</a></strong></li>
</ul></div>

<div dir="rtl">اس بات کا یقین کرنے کے لیے کہ مندرجہ ذیل پیکجوں اور مصنوعات CIDRAM کے ساتھ مطابقت پذیر ہوں گے ماڈیولز دستیاب کیے گئے ہیں:</div>
<div dir="rtl"><ul>
 <li><strong><a dir="ltr" href="https://github.com/CIDRAM/CIDRAM/issues/56">BunnyCDN</a></strong></li>
</ul></div>

<div dir="rtl"><em>بھی دیکھو: <a href="https://maikuolan.github.io/Compatibility-Charts/">مطابقت چارٹ</a>.</em><br /><br /></div>

---


### <div dir="rtl">۹. <a name="SECTION9">اکثر پوچھے گئے سوالات (FAQ)</div>

<div dir="rtl"><ul>
 <li><a href="#user-content-WHAT_IS_A_SIGNATURE">ایک "دستخط" کیا ہے؟</a></li>
 <li><a href="#user-content-WHAT_IS_A_CIDR">ایک "CIDR" کیا ہے؟</a></li>
 <li><a href="#user-content-WHAT_IS_A_FALSE_POSITIVE">ایک "جھوٹی مثبت" سے کیا مراد ہے؟</a></li>
 <li><a href="#user-content-BLOCK_ENTIRE_COUNTRIES">بلاک تمام ممالک CIDRAM کر سکتا ہوں؟</a></li>
 <li><a href="#user-content-SIGNATURE_UPDATE_FREQUENCY">دستخط کیسے بیشتر اپ ڈیٹ کر رہے ہیں؟</a></li>
 <li><a href="#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO">CIDRAM استعمال کرتے ہوئے میں ایک مسئلہ کا سامنا کرنا پڑا ہے اور میں اس کے بارے میں کیا پتہ نہیں ہے! مدد کریں!</a></li>
 <li><a href="#user-content-BLOCKED_WHAT_TO_DO">میں نے دورہ کرنا چاہتے ہیں کہ ایک ویب سائٹ سے CIDRAM کی طرف سے بلاک کیا گیا ہے! مدد کریں!</a></li>
 <li><a href="#user-content-MINIMUM_PHP_VERSION">میں 5.4.0 سے زیادہ پرانے ایک PHP ورژن کے ساتھ CIDRAM (v2 سے پہلے) استعمال کرنا چاہتے ہیں؛ کیا آپ مدد کر سکتے ہیں؟</a></li>
 <li><a href="#user-content-MINIMUM_PHP_VERSION_V2">میں 7.2.0 سے زیادہ پرانے ایک PHP ورژن کے ساتھ CIDRAM (v2) استعمال کرنا چاہتے ہیں؛ کیا آپ مدد کر سکتے ہیں؟</a></li>
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
 <li><a href="#user-content-CHANGE_COMPONENT_SORT_ORDER">جب میں اپ ڈیٹس کے صفحے کے ذریعہ ماڈیولز یا دستخط شدہ فائلوں کو چالو یا غیر فعال کروں تو، یہ انفرادی طور پر ترتیب میں تبدیل کرتا ہے. کیا میں اس راستہ کو تبدیل کر سکتا ہوں جسے وہ ترتیب دیں گے؟</a></li>
 <li><a href="#user-content-HOW_TO_USE_PDO">"PDO DSN" کیا ہے؟ میں CIDRAM کے ساتھ PDO کیسے استعمال کرسکتا ہوں؟</a></li>
 <li><a href="#user-content-BLOCK_CRON">CIDRAM cronjobs کو مسدود کررہا ہے؛ اس کو کیسے ٹھیک کریں؟</a></li>
</ul></div>

#### <div dir="rtl"><a name="WHAT_IS_A_SIGNATURE"></a>ایک "دستخط" کیا ہے؟<br /><br /></div>

<div dir="rtl">CIDRAM کے تناظر میں، اعداد و شمار کے مخصوص کچھ ہم کے لیے تلاش کر رہے ہیں اس کی شناخت کے لیے استعمال کیا جاتا ہے کے لیے ایک "دستخط" مراد، عام طور پر ایک IP ایڈریس یا CIDR، CIDRAM کے لیے کچھ ہدایات کے ساتھ (یہ مقابلوں جب ہم کے لیے تلاش کر رہے ہیں کیا جواب دینے کا بہترین طریقہ، وغیرہ). CIDRAM کے لیے ایک مخصوص دستخط کی کچھ اس طرح دکھائی دیتی ہے:<br /><br /></div>

<div dir="rtl">"دستخط فائلوں" کے لیے:<br /><br /></div>

`1.2.3.4/32 Deny Generic`

<div dir="rtl">"ماڈیولز" کے لیے:<br /><br /></div>

```PHP
$Trigger(strpos($CIDRAM['BlockInfo']['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

<div dir="rtl">نوٹ: "دستخط فائلوں" کے لیے دستخط، اور "ماڈیولز" کے لیے دستخط وہی چیز نہیں ہیں.<em></em><br /><br /></div>

<div dir="rtl">اکثر ایسا ہوتا ہے (لیکن ہمیشہ نہیں)، دستخط "کے دستخط حصوں" میں بنڈل گا، اکثر تبصرے، مارک اپ، اور متعلقہ میٹا ڈیٹا کے ساتھ شامل تھے. یہ دستخط اور مزید ہدایات کے لیے اضافی سیاق و سباق فراہم کر سکتے ہیں.<br /><br /></div>

#### <div dir="rtl"><a name="WHAT_IS_A_CIDR"></a>ایک "CIDR" کیا ہے؟<br /><br /></div>

<div dir="rtl">"CIDR" "Classless Inter-Domain Routing" ("غیر طبقاتی انٹر ڈومین روٹنگ") کے لیے مخفف ہے <em>[<a href="https://ar.wikipedia.org/wiki/%D8%AA%D9%88%D8%AC%D9%8A%D9%87_%D8%A8%D9%8A%D9%86_%D8%A7%D9%84%D9%85%D8%AC%D8%A7%D9%84%D8%A7%D8%AA_%D9%84%D8%A7%D9%81%D8%A6%D9%88%D9%8A%D8%A7">۱</a>، <a href="https://whatismyipaddress.com/cidr">۲</a>]</em>. یہ مخفف اس پیکج، "CIDRAM" کے لیے نام کا حصہ کے طور پر استعمال کیا جاتا ہے. یہ "Classless Inter-Domain Routing Access Manager" (غیر طبقاتی انٹر ڈومین روٹنگ رسائی مینیجر) کے لیے مخفف ہے.<br /><br /></div>

<div dir="rtl">تاہم، CIDRAM کے تناظر میں (جیسا کہ، یہ دستاویزات کے اندر اندر، متعلقہ مباحث میں، یا زبان کے اعداد و شمار کے اندر اندر)، ایک "CIDR" (واحد) یا "CIDR" (جمع) کا ذکر کیا جاتا ہے جب، ہمارے ارادہ معنی ذیلی نیٹ ہے، CIDR سنکیتن کا استعمال کرتے ہوئے اظہار کیا. ذیلی نیٹ کو مختلف مختلف طریقوں سے اظہار کیا جا سکتا ہے کیونکہ اس کی وجہ ہے. CIDRAM، لہذا، ایک "نیٹ رسائی مینیجر" سمجھا جا سکتا ہے.<br /><br /></div>

<div dir="rtl">یہ وضاحت، اور فراہم تناظر، کسی بھی ابہام حل کرنے کے لیے مدد کرنی چاہیے.<br /><br /></div>

#### <div dir="rtl"><a name="WHAT_IS_A_FALSE_POSITIVE"></a>ایک "جھوٹی مثبت" سے کیا مراد ہے؟<br /><br /></div>

<div dir="rtl">اصطلاح "جھوٹی مثبت" (<em>متبادل کے طور پر: "جھوٹی مثبت غلطی"؛ "جھوٹے الارم"</em>)، بیان بہت صرف، اور ایک عام سیاق و سباق میں، ایک کی حالت کے لیے جانچ جب، استعمال کیا جاتا ہے کہ ٹیسٹ کے نتائج کا حوالہ دیتے ہیں کے لیے، نتائج مثبت ہیں جب (یعنی حالت "مثبت" یا "سچ" ہونے کا تعین کیا جاتا ہے)، لیکن بننے کی توقع کی جاتی ہے (یا ہونا چاہیئے) منفی (یعنی حالت، حقیقت میں، "منفی"، یا "جھوٹے"). "جھوٹی مثبت" مثل غور کیا جا سکتا کے لیے "رونا بھیڑیا" (جس حالت تجربہ کیا جا رہا، حالت "جھوٹے" کہ میں ریوڑ کے قریب کوئی بھیڑیا ہے، اور شرط کے طور پر رپورٹ کیا جاتا ہے ریوڑ کے قریب ایک بھیڑیا ہے کہ آیا ہے "بھیڑیا، بھیڑیا" بلا کی راہ کی طرف چرواہا کی طرف سے "مثبت")، یا طبی جانچ میں حالات جس میں ایک مریض، کچھ بیماری یا مرض ہونے حقیقت میں، وہ ایسی کوئی بیماری یا مرض ہے جب کے طور پر تشخیص کی جاتی ہے کے مطابق.<br /><br /></div>

<div dir="rtl">ایک شرط کے لیے جانچ جب متعلقہ نتائج "سچ مثبت" کی اصطلاحات کا استعمال کرتے ہوئے، "سچ منفی" اور "جھوٹے منفی" بیان کیا جا سکتا ہے. "سچ مثبت" جب ٹیسٹ کے نتائج اور حالت کی اصل ریاست دونوں حقیقی (یا "مثبت")، اور ایک "حقیقی منفی" ہیں سے مراد ہے سے مراد ہے جب ٹیسٹ کے نتائج اور کی اصل ریاست شرط ہیں دونوں جھوٹے ہیں (یا "منفی")؛ "سچ مثبت" یا "سچ منفی" ایک "صحیح اندازہ" سمجھا جاتا ہے. ایک "جھوٹی مثبت" کے برعکس ایک "جھوٹے منفی" ہے؛ "جھوٹے منفی" سے ٹیسٹ کے نتائج منفی ہیں، جب (یعنی حالت "منفی"، یا "جھوٹے" ہونے کا تعین کیا جاتا ہے)، لیکن بننے کی توقع کی جاتی ہے (یا ہونا چاہیئے) مراد مثبت (یعنی، حالت، حقیقت میں، "مثبت" یا "سچ") ہے.<br /><br /></div>

<div dir="rtl">CIDRAM کے تناظر میں، ان شرائط جسے انہوں بلاک CIDRAM کے دستخط اور کیا / کا حوالہ دیتے ہیں. ایک IP ایڈریس، برا فرسودہ یا غلط دستخطوں کی وجہ CIDRAM بلاکس، لیکن ایسا نہیں کیا جب چاہیے ہے، یا یہ غلط وجوہات کی بناء پر ایسا کرتا ہے جب، ہم نے ایک "جھوٹی مثبت" کے طور پر اس ایونٹ کا حوالہ دیتے ہیں. CIDRAM ایک IP ایڈریس جو، کی وجہ سے غیر متوقع خطرات سے، بلاک کر دیا گیا ہے چاہیے لاپتہ اس کے دستخط میں دستخط یا کمی کو بلاک کرنے میں ناکام ہونے پر، ہم نے ایک "یاد کا پتہ لگانے" (ایک "جھوٹے منفی" کے مطابق ہوتا ہے) کے طور پر اس واقعہ کا حوالہ دیتے ہیں.<br /><br /></div>

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

#### <div dir="rtl"><a name="MINIMUM_PHP_VERSION"></a>میں 5.4.0 سے زیادہ پرانے ایک PHP ورژن کے ساتھ CIDRAM (v2 سے پہلے) استعمال کرنا چاہتے ہیں؛ کیا آپ مدد کر سکتے ہیں؟<br /><br /></div>

<div dir="rtl">نہیں. CIDRAM < v2 کم از کم PHP >= 5.4.0 کی ضرورت ہے.<br /><br /></div>

#### <div dir="rtl"><a name="MINIMUM_PHP_VERSION_V2"></a>میں 7.2.0 سے زیادہ پرانے ایک PHP ورژن کے ساتھ CIDRAM (v2) استعمال کرنا چاہتے ہیں؛ کیا آپ مدد کر سکتے ہیں؟<br /><br /></div>

<div dir="rtl">نہیں. CIDRAM v2 کم از کم PHP >= 7.2.0 کی ضرورت ہے.<br /><br /></div>

<div dir="rtl"><em>بھی دیکھو: <a href="https://maikuolan.github.io/Compatibility-Charts/">مطابقت چارٹ</a>.</em><br /><br /></div>

#### <div dir="rtl"><a name="PROTECT_MULTIPLE_DOMAINS"></a>میں نے ایک سے زیادہ ڈومینز کی حفاظت کے لیے ایک واحد CIDRAM تنصیب کا استعمال کر سکتا ہوں؟<br /><br /></div>

<div dir="rtl">جی ہاں. CIDRAM ایک سے زیادہ ڈومینز کی حفاظت کے لیے استعمال کیا جا سکتا ہے. ضرورت کی ترتیب مختلف ہے تو، ایسا کرنے کے لیے تحفظ کی ضرورت ہوتی ڈومینز کے مطابق نامی نئی ترتیب فائل، تخلیق کرتے ہیں. CIDRAM یہ ڈومین کے لیے کام کرنا چاہیے کہ کس طرح اس بات کا تعین کرنے کے لیے ان فائلوں کو استعمال کریں گے. سوف تستخدم CIDRAM هذه الملفات لتحديد كيفية تشغيلها للنطاق. ایک مثال کے طور، کے لیے <code dir="ltr">"https://www.some-domain.tld/"</code>، اس کا نام ہے <code dir="ltr">"some-domain.tld.config.ini"</code>. ڈومین نام <code dir="ltr">"HTTP_HOST"</code> سے آتا ہے. <code dir="ltr">"www"</code> نظر انداز کر دیا جاتا ہے.<br /><br /></div>

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

<div dir="rtl">"خلاف ورزی" کا تعین ہوتا ہے جب کسی IP جو ابھی تک کسی بھی مخصوص دستخط شدہ فائلوں کی طرف سے بلاک نہیں کیا جانا چاہیے مستقبل میں درخواستوں کے لیے بند ہونا شروع کرنا چاہیے، اور یہ IP ٹریکنگ سے متعلق ہے. IP کے علاوہ چیزوں کو روکنے کے لیے کچھ فعالیتیں موجود ہیں (spambot اور hacktool، خطرناک سوالات، جعلی DNS، وغیرہ). جب ایسا ہوتا ہے تو، "خلاف ورزی" ہوسکتی ہے.<br /><br /></div>

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

<div dir="rtl">ممکنہ طور پر. یہ سوال میں خدمت کی نوعیت پر منحصر ہے، اور آپ اس کا استعمال کیسے کر رہے ہیں. عموما، اگر آپ صرف جامد اثاثوں کو پکڑ رہے ہیں تو (تصاویر، CSS، وغیرہ؛ جو وقت کے ساتھ تبدیل نہیں ہوتا ہے)، کوئی مسئلہ نہیں ہونا چاہیے. تاہم، وہاں مسائل ہوسکتے ہیں، اگر آپ ڈیٹا کیشنگ کر رہے ہیں جو عام طور پر متحرک طور پر پیدا ہوجائے تو درخواست کی جاتی ہے، یا اگر آپ POST کی درخواستوں کے نتائج کو پکڑ رہے ہیں (یہ آپ کی ویب سائٹ اور ماحول کو جامد طور پر فراہم کرے گا، اور CIDRAM ایک مستحکم ماحول میں کسی بھی معقول فائدہ فراہم کرنے کے لیے امکان نہیں ہے). اس کے علاوہ، آپ کو استعمال کرنے والے مواد کی ترسیل کے نیٹ ورک یا کیشنگ سروس پر منحصر ہے، اس کے مطابق CIDRAM مخصوص ترتیبات کی ضروریات ہوسکتی ہے (آپ کو اس بات کا یقین کرنے کی ضرورت ہوگی کہ CIDRAM صحیح طریقے سے ترتیب دیا جائے). غلط ترتیب کی وجہ سے غلط جھوٹے مثبت اور دیگر مسائل کا سبب بن سکتا ہے.<br /><br /></div>

#### <div dir="rtl"><a name="DDOS_ATTACKS"></a>کیا CIDRAM DDoS حملوں کے خلاف میری ویب سائٹ کی حفاظت کرتا ہے؟<br /><br /></div>

<div dir="rtl">یہ نہیں کرے گا.<br /><br /></div>

<div dir="rtl">مزید تفصیل میں: CIDRAM اس اثر کو کم کرنے میں مدد دے گی جو ناپسندیدہ ٹریفک آپ کی ویب سائٹ اور ہارڈ ویئر پر ہوسکتی ہے (اس کا مطلب سستا ویب سائٹ بینڈوڈتھ اخراجات اور صحت مند سرور). تاہم، اس سوال کو سمجھنے کے لۓ دو اہم چیزیں ہیں جو یاد رکھنا ضروری ہے.<br /><br /></div>

<div dir="rtl">۱. CIDRAM ایک PHP پیکیج ہے، اور اس وجہ سے چلاتا ہے جہاں PHP انسٹال ہے. اس کا مطلب یہ ہے کہ سرور پہلے سے موصول ہونے کے بعد CIDRAM صرف درخواستوں کو دیکھ سکتے ہیں اور بلاک کرسکتے ہیں. ۲. DDoS حملے کے ذریعہ ھدف کردہ سرور تک پہنچنے سے قبل مؤثر DDoS کمیشن کو درخواستوں کو فلٹر کرنا چاہیے. مثالی طور پر، وہ ان جگہوں سے پتہ لگانے اور کم کرنے کے قابل ہونا چاہیے جو حملوں کے ساتھ منسلک ٹریفک کو ختم کرنے میں کامیاب ہوسکتی ہیں، اس سے پہلے کہ وہ پہلی جگہ میں ھدف شدہ سرور تک پہنچے.<br /><br /></div>

<div dir="rtl">اس کو نافذ کرنے کے کچھ طریقے: وقف ہارڈ ویئر کے حل. وقف DDoS کمیشن کی خدمات. DDoS مزاحم نیٹ ورک کے ذریعہ ڈومین کے DNS کو روٹنگ. کلاؤڈ پر مبنی فلٹرنگ. متبادل طور پر: اس کا کچھ مجموعہ کسی بھی صورت میں، یہ مضمون پیچیدہ ہے، لہذا اگر آپ اس میں دلچسپی رکھتے ہیں تو میں مزید تحقیق کروں گا. جب DDoS کے حملوں کی صحیح نوعیت مناسب طریقے سے سمجھ گئی ہے، تو یہ جواب زیادہ احساس کرے گا.<br /><br /></div>

#### <div dir="rtl"><a name="CHANGE_COMPONENT_SORT_ORDER"></a>جب میں اپ ڈیٹس کے صفحے کے ذریعہ ماڈیولز یا دستخط شدہ فائلوں کو چالو یا غیر فعال کروں تو، یہ انفرادی طور پر ترتیب میں تبدیل کرتا ہے. کیا میں اس راستہ کو تبدیل کر سکتا ہوں جسے وہ ترتیب دیں گے؟<br /><br /></div>

<div dir="rtl">جی ہاں. اگر آپ کو مخصوص فائلوں میں عمل درآمد کرنے کے لیے کچھ فائلوں پر مجبور کرنے کی ضرورت ہے تو، آپ ان کے نام سے پہلے ان ترتیبات کو ہدایت دیتے ہیں جہاں وہ فہرست میں درج ہوتے ہیں، ان سے پہلے کسی بھی مباحثہ کے اعداد و شمار کو شامل کرسکتے ہیں. جب اپ ڈیٹس کے صفحے کو بعد میں فائلوں کو دوبارہ ترتیب دیتا ہے، تو اس نے مزید کہا کہ خود مختار اعداد و شمار اس طرح کے حکم کو متاثر کرے گی، جس کے نتیجے میں ان کے نتیجے میں عملدرآمد کرنے کے نتیجے میں عملدرآمد کرنے کے لۓ، بغیر کسی کو تبدیل کرنے کی ضرورت ہے.<br /><br /></div>

<div dir="rtl">مثال کے طور پر، مندرجہ ذیل درج ذیل فائلوں کے ساتھ ایک ترتیب ڈائریکٹری کو فرض کرنا:<br /><br /></div>

`file1.php,file2.php,file3.php,file4.php,file5.php`

<div dir="rtl">اگر آپ چاہتے تھے کہ <code dir="ltr">file3.php</code> سب سے پہلے عمل کرنے کے لیے، آپ فائل کے نام سے پہلے <code dir="ltr">aaa:</code> کی طرح کچھ شامل کرسکتے ہیں:<br /><br /></div>

`file1.php,file2.php,aaa:file3.php,file4.php,file5.php`

<div dir="rtl">پھر، اگر ایک نئی فائل، <code dir="ltr">file6.php</code>، چالو کر دیا جاتا ہے، جب اپ ڈیٹس صفحہ ان کو دوبارہ دوبارہ تبدیل کرتا ہے، تو اسے اس طرح ختم کرنا چاہیے:<br /><br /></div>

`aaa:file3.php,file1.php,file2.php,file4.php,file5.php,file6.php`

<div dir="rtl">ایک ہی صورت حال حال ہی میں ایک فائل غیر فعال ہے. اس کے برعکس، اگر آپ چاہتے تھے کہ آخری فائل کو عمل کرنے کے لۓ، آپ فائل کے نام سے پہلے <code dir="ltr">zzz:</code> کی طرح کچھ شامل کرسکیں. کسی بھی صورت میں، آپ کو سوال میں فائل کا نام تبدیل کرنے کی ضرورت نہیں ہوگی.<br /><br /></div>

#### <div dir="rtl"><a name="HOW_TO_USE_PDO"></a>"PDO DSN" کیا ہے؟ میں CIDRAM کے ساتھ PDO کیسے استعمال کرسکتا ہوں؟<br /><br /></div>

<div dir="rtl">"<a dir="ltr" href="https://www.php.net/manual/en/intro.pdo.php">PHP Data Objects</a>" (PHP ڈیٹا آبجیکٹ)، "PDO" کا مخفف ہے. یہ PHP کو ایک انٹرفیس فراہم کرتا ہے تاکہ وہ PHP کی ایپلی کیشنز کے ذریعہ استعمال ہونے والے ڈیٹا بیس سسٹم سے رابطہ قائم کرسکیں.<br /><br /></div>

<div dir="rtl">"<a dir="ltr" href="https://en.wikipedia.org/wiki/Data_source_name">data source name</a>" (ڈیٹا سورس کا نام)، "DSN" کا مخفف ہے. یہ PDO کو بیان کرتا ہے کہ اسے ڈیٹا بیس سے کیسے جڑنا چاہیے.<br /><br /></div>

<div dir="rtl">CIDRAM میں، آپ کیڈیچنگ مقاصد کے لیے PDO استعمال کرسکتے ہیں. تاکہ اسے صحیح طریقے سے کام کیا جاسکے، ترتیب کے ذریعہ اس کو اہل بنائیں، اس کے لیے ایک ڈیٹا بیس بنائیں، اور نیچے بیان کردہ ڈھانچے کے مطابق اپنے ڈیٹا بیس میں ایک نیا ٹیبل بنائیں.<br /><br /></div>

<div dir="rtl">جب ایک ڈیٹا بیس کنکشن کامیابی کے ساتھ ہے، لیکن ضروری جدول موجود نہیں ہے، یہ خود بخود تخلیق کرنے کی کوشش کرے گی. تاہم، اس طرز عمل کا بڑے پیمانے پر تجربہ نہیں کیا گیا ہے اور کامیابی کی ضمانت نہیں دی جاسکتی ہے.<br /><br /></div>

<div dir="rtl">اگر آپ اسے استعمال نہیں کرنا چاہتے ہیں تو، آپ ان ہدایات کو نظرانداز کرسکتے ہیں.<br /><br /></div>

<div dir="rtl">ذیل میں بیان کردہ ڈھانچے میں "cidram" کو اپنے ڈیٹا بیس کے نام کے بطور استعمال کیا گیا ہے، لیکن آپ اپنے ڈیٹا بیس کے لیے جو بھی نام استعمال کرنا چاہ، استعمال کرسکتے ہیں، جب تک کہ وہی نام آپ کی ڈی ایس این ترتیب میں نقل کیا جائے.<br /><br /></div>

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


### <div dir="rtl">۱۱. <a name="SECTION11">قانونی معلومات</div>

#### <div dir="rtl">۱۱.۰ سیکشن پریامبل<br /><br /></div>

<div dir="rtl">دستاویزات کا یہ حصہ پیکج کے استعمال اور عمل کے بارے میں ممکنہ قانونی مفکوم بیان کرتا ہے، اور کچھ بنیادی متعلق معلومات فراہم کرتی ہے. بعض صارفین کے لیے شکایت کا یقین کرنے کے لیے یہ ممکن ہو سکتا ہے کہ وہ کسی بھی قانونی تقاضے کے ساتھ موجود ممالک میں موجود ہوسکتے ہیں جس میں وہ کام کرتے ہیں، اور کچھ صارفین اس کی معلومات کے مطابق اپنی ویب سائٹ کی پالیسیوں کو ایڈجسٹ کرنے کی ضرورت ہوسکتی ہے.<br /><br /></div>

<div dir="rtl">سب سے پہلے، سب سے اہم، یاد رکھیں کہ میں (پیکیج کا مصنف) ایک وکیل نہیں ہوں. لہذا، میں قانونی مشورہ فراہم کرنے کے لیے قانونی طور پر قابل نہیں ہوں. اس کے علاوہ، کچھ معاملات میں، قانونی ضروریات مختلف ممالک اور دائرہ کاروں کے درمیان مختلف ہوتی ہیں. یہ مختلف قانونی ضروریات کبھی کبھی متفق ہیں (مثلا، ایسے ممالک جو "رازداری کے حقوق" اور "بھول جانے کا حق"، ایسے ممالک کے مقابلے میں جو "ڈیٹا برقرار رکھنے" کا حق رکھتے ہیں). یہ بھی غور کریں کہ پیکیج تک رسائی مخصوص ممالک یا دائرہ کاروں سے محدود نہیں ہے, اور اس وجہ سے، پیکج کے صارفین جغرافیایی متنوع ہونے کا امکان رکھتے ہیں. ان پوائنٹس پر غور کیا گیا ہے، میں ایسی حیثیت میں نہیں ہوں جو یہ سب کے لیے "قانونی طور پر مطابق" ہونے کا مطلب ہے. تاہم، مجھے امید ہے کہ اس معلومات میں آپ کو یہ فیصلہ کرنے میں مدد ملتی ہے کہ پیکج کے تناظر میں قانونی طور پر مطابق رہنے کے لۓ آپ کو کیا کرنا ہوگا. اگر آپ کو کوئی شبہ ہے، یا اگر آپ کو قانونی نقطہ نظر سے اضافی مدد اور مشورہ کی ضرورت ہو تو، میں ایک قانونی پیشہ ورانہ مشاورت کی سفارش کروں گا.<br /><br /></div>

#### <div dir="rtl">۱۱.۱ ذمہ داری<br /><br /></div>

<div dir="rtl">پیکج کسی بھی وارنٹی کے ساتھ فراہم نہیں کی جاتی ہے (لائسنس پہلے ہی اس کا ذکر کرتا ہے). یہ ذمہ داری کے تمام مقاصد پر لاگو ہوتا ہے. پیکج آپ کی سہولت کے لیے فراہم کی جاتی ہے. امید ہے کہ یہ مفید ہو گا، اور یہ آپ کے لیے کچھ فائدہ فراہم کرے گا. تاہم، پیکج کا استعمال کرتے ہوئے یا لاگو آپ کا اپنا فیصلہ ہے. آپ اسے استعمال کرنے یا اسے لاگو کرنے پر مجبور نہیں ہوئے ہیں. جب آپ ایسا کرتے ہو تو، آپ اس فیصلے کے ذمہ دار ہیں. میں اور دوسرا پیکج شراکت دار، آپ کے فیصلوں کے نتائج کے لیے قانونی طور پر ذمہ دار نہیں ہے.<br /><br /></div>

#### <div dir="rtl">۱۱.۲ تیسرے فریقوں<br /><br /></div>

<div dir="rtl">اس پیکیج پر منحصر ہے کہ کس طرح پیکج ترتیب اور لاگو ہوتا ہے، کچھ صورتو میں، یہ تیسری جماعتوں کے ساتھ معلومات کا اشتراک کرسکتا ہے. کچھ قواعد و ضوابط میں، کچھ دائرہ کار کی طرف سے، یہ "ذاتی طور پر شناختی معلومات" کے طور پر بیان کیا جا سکتا ہے.<br /><br /></div>

<div dir="rtl">تیسری جماعتوں کی طرف سے یہ معلومات کس طرح استعمال کی جاتی ہے، ان کی پالیسیوں کے تابع ہے، اور اس دستاویزات کے دائمے سے باہر ہے. تاہم، اس طرح کے معاملات میں، معلومات کا اشتراک معذور ہوسکتا ہے. اس طرح کے معاملات میں، اگر آپ اسے چالو کرنے کا انتخاب کرتے ہیں تو، یہ آپ کی ذمہ داری ہے کہ آپ کو ان خدشات کے بارے میں معلومات کی رازداری، سیکورٹی اور استعمال کے بارے میں کوئی خدشات کی تحقیقات کی جا سکتی ہے. اگر کوئی شبہ موجود ہے، یا اگر آپ ان تیسری جماعتوں کے انعقاد سے ناخوش ہیں تو، ان تیسری جماعتوں کے ساتھ معلومات کے تمام حصول کو غیر فعال کرنے میں یہ سب سے بہتر ہوسکتا ہے.<br /><br /></div>

<div dir="rtl">شفافیت کے مقصد کے لیے، مشترکہ معلومات کی قسم ذیل میں بیان کی گئی ہے.<br /><br /></div>

##### <div dir="rtl">۱۱.۲.۰ میزبان نام تلاش کریں<br /><br /></div>

<div dir="rtl">اگر آپ میزبانوں کے ساتھ کام کرنے کے لیے کسی بھی خصوصیات یا ماڈیولز کا استعمال کرتے ہیں تو، CIDRAM انباؤنڈ درخواستوں کے میزبان نام حاصل کرنے کے قابل ہوسکتا ہے. عام طور پر، یہ ایک DNS سرور سے IP ایڈریس کے میزبان ناموں کی درخواست کرکے یہ کرتا ہے، یا براہ راست نظام کی طرف سے فراہم کی گئی فعالیت کے ذریعے معلومات کی درخواست کی طرف سے. <a href="https://dns.google.com/">Google DNS</a> سروس پہلے سے طے شدہ طور پر مقرر کیا جاتا ہے (لیکن یہ ترتیب کے ذریعے آسانی سے تبدیل کیا جا سکتا ہے). مطابقت پذیر خدمات کے ساتھ مطابقت پذیری کی جا سکتی ہے، اور ان پر منحصر ہے کہ آپ کس طرح پیکج کو ترتیب دیں گے. نظام کے ذریعے براہ راست درخواست کرتے وقت، آپ کو اپنے نظام کے منتظم سے رابطہ کرنے کی ضرورت پڑے گی جس کا تعین کیا جاسکتا ہے. متاثر ماڈیولز سے بچنے یا اس کے مطابق پیکیج ترتیب میں ترمیم کرکے CIDRAM میں ہوسٹ نام کی تلاش کی جا سکتی ہے.<br /><br /></div>

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">default_dns</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">search_engine_verification</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">social_media_verification</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">other_verification</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">force_hostname_lookup</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">allow_gethostbyaddr_lookup</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">۱۱.۲.۱ ویب فونٹس<br /><br /></div>

<div dir="rtl">کچھ اپنی مرضی کے مطابق موضوعات، معیاری CIDRAM صارف انٹرفیس، اور "رسائی نہیں ہوئی" صفحہ، ویب فونٹس کو جمالیاتی وجوہات کے لۓ استعمال کرسکتے ہیں. ویب فونٹس ڈیفالٹ کے ذریعہ غیر فعال ہیں. فعال ہونے پر، صارف کے برائوزر اور ویب فونٹ میزبان کے درمیان براہ راست مواصلات موجود ہے. یہ ممکنہ طور پر مواصلاتی معلومات جیسے صارف کے IP ایڈریس، صارف ایجنٹ، آپریٹنگ سسٹم، اور درخواست کے لیے دستیاب دیگر تفصیلات شامل ہوسکتا ہے. ان میں سے زیادہ تر ویب فونٹس <a dir="ltr" href="https://fonts.google.com/">Google Fonts</a> سروس کی طرف سے میزبان ہیں.<br /><br /></div>

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">disable_webfonts</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">۱۱.۲.۲ تلاش انجن اور سوشل میڈیا کی توثیق<br /><br /></div>

<div dir="rtl">جب یہ اختیارات فعال ہوتے ہیں تو، CIDRAM کو تلاش کے انجن اور سوشل میڈیا کی درخواستوں کی صداقت کی توثیق کرنے کی کوشش ہوتی ہے. ایسا کرنے کے لیے، یہ ان پونڈ درخواستوں کے میزبانوں سے IP پتوں کو حل کرنے کی کوشش کرنے کے لیے <a dir="ltr" href="https://dns.google.com/">Google DNS</a> سروس کا استعمال کرتا ہے (اس عمل میں، ان بے حد درخواستوں کے میزبانوں کو سروس کے ساتھ اشتراک کیا جاتا ہے).<br /><br /></div>

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">search_engine_verification</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">social_media_verification</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">other_verification</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">۱۱.۲.۳ CAPTCHA<br /><br /></div>

<div dir="rtl">reCAPTCHA اور hCAPTCHA پیکیج کے ذریعہ تعاون یافتہ ہیں. ان کو صحیح طریقے سے کام کرنے کے لیے API کیز کی ضرورت ہوتی ہے. وہ بطور ڈیفالٹ غیر فعال ہیں، لیکن مطلوبہ API چابیاں تشکیل دے کر ان کو فعال کیا جاسکتا ہے. جب فعال ہوجائے تو، خدمت اور CIDRAM یا صارف کے براؤزر کے مابین مواصلت ہوسکتی ہے. اس میں ممکنہ طور پر بات چیت کرنے والی معلومات شامل ہوسکتی ہے جیسے صارف کا آئی پی ایڈریس، صارف ایجنٹ، آپریٹنگ سسٹم، اور دیگر تفصیلات.<br /><br /></div>

##### <div dir="rtl">۱۱.۲.۴ STOP FORUM SPAM<br /><br /></div>

<div dir="rtl"><a dir="ltr" href="https://www.stopforumspam.com/">Stop Forum Spam</a> ایک شاندار، آزادانہ طور پر دستیاب سروس ہے جو اسپیمرز سے فورمز، بلاگز، اور ویب سائٹس کی حفاظت کے لیے مدد کرسکتا ہے. یہ یہ معروف اسپیمرز کے ایک ڈیٹا بیس فراہم کر کے کرتا ہے، اور ایک API جو لیورڈج کیا جا سکتا ہے کہ یہ چیک کرنے کے لیے کہ آیا IP ایڈریس، صارف کا نام، یا ای میل ایڈریس اس کے ڈیٹا بیس پر درج کیا جاتا ہے.<br /><br /></div>

<div dir="rtl">CIDRAM ایک ماڈیول فراہم کرتا ہے جو اس API کو چیک کرنے کے لۓ لیتا ہے کہ آیا درخواستوں کا IP ایڈریس مشتبہ اسپیمر سے تعلق رکھتا ہے. ماڈیول ڈیفالٹ کے ذریعہ انسٹال نہیں ہے، لیکن اگر آپ اسے نصب کرنے کا انتخاب کرتے ہیں تو، صارف IP پتے کو Stop Forum Spam API کے ساتھ اشتراک کیا جا سکتا ہے. جب ماڈیول انسٹال ہوجاتا ہے تو، CIDRAM اس API کے ساتھ بات چیت کرتا ہے جب بھی انباؤنڈ درخواست کسی وسائل کی درخواست کرتا ہے جس میں CIDRAM اکثر اسپیمرز کی طرف سے نشانہ بنایا جاتا وسائل کے ایک قسم کے طور پر تسلیم کرتا ہے (مثلا لاگ ان کے صفحات، رجسٹریشن کے صفحات، ای میل کی توثیق کے صفحات، تبصرہ فارم، وغیرہ جیسے).<br /><br /></div>

##### <div dir="rtl">۱۱.۲.۵ ABUSEIPDB<br /><br /></div>

<div dir="rtl"><a dir="ltr" href="https://www.abuseipdb.com/">AbuseIPDB</a> API کا استعمال کرتے ہوئے بدسلوکی IP پتے کو بلاک کرنے کے لیے CIDRAM ایک اختیاری ماڈیول فراہم کرتا ہے. ماڈیول ڈیفالٹ کے ذریعہ انسٹال نہیں ہے، لیکن اگر آپ اسے نصب کرنے کا انتخاب کرتے ہیں تو، صارف IP پتے کو AbuseIPDB API کے ساتھ اشتراک کیا جا سکتا ہے.<br /><br /></div>

##### <div dir="rtl">۱۱.۲.۶ BGPVIEW, IP-API<br /><br /></div>

<div dir="rtl"><a dir="ltr" href="https://bgpview.io/">BGPView</a> API اور <a dir="ltr" href="https://ip-api.com/">IP-API</a> API کا استعمال کرتے ہوئے ASN اور ملکی کوڈ تلاش کرنے کے لیے CIDRAM لیے اختیاری ماڈیول فراہم کرتا ہے. یہ تلاشیں اپنے ASN یا ملک کے اصل کی بنیاد پر درخواستوں کو مسدود کرنے یا وائٹ لسٹ کرنے کی اہلیت فراہم کرتی ہیں. ماڈیول ڈیفالٹ کے ذریعہ انسٹال نہیں ہے، لیکن اگر آپ اسے نصب کرنے کا انتخاب کرتے ہیں تو، صارف IP پتے کو خدمت کے ساتھ اشتراک کیا جا سکتا ہے.<br /><br /></div>

#### <div dir="rtl">۱۱.۳ لاگ<br /><br /></div>

<div dir="rtl">لاگنگ کئی وجوہات کے لیے CIDRAM کا ایک اہم حصہ ہے. اس کے بغیر، غلطیوں کو تلاش کرنے اور مسائل کی تشخیص مشکل ہوسکتی ہے. اگر ہمارے پاس یہ معلومات نہیں ہے اور کسی چیز کو تبدیل کرنے کی ضرورت ہے، یہ جاننا مشکل ہوسکتا ہے کہ بالکل وہی چیز جو تبدیل کرنے کی ضرورت ہے. اس کے باوجود، ہر کوئی اس معلومات کو ریکارڈ نہیں کرنا چاہتا، لہذا یہ اختیاری رہتا ہے. CIDRAM میں، یہ ڈیفالٹ کی طرف سے معذور ہے. اسے فعال کرنے کے لیے، CIDRAM کے مطابق ترتیب دیا جانا چاہیے.<br /><br /></div>

<div dir="rtl">یہ یاد رکھنا چاہیے کہ لاگنگ کے لیے عین مطابق قانونی ضروریات دائرہ کاروں کے درمیان مختلف ہو سکتی ہیں. عملدرآمد کا تناظر بھی متعلقہ ہو سکتا ہے (مثال کے طور پر، ایک فرد کے طور پر، ایک کارپوریٹ ادارے کے طور پر، تجارتی بنیاد پر، غیر تجارتی بنیاد پر، وغیرہ). اس کی وجہ سے، یہاں کی معلومات آپ کے لیے مفید ہوسکتی ہے.<br /><br /></div>

<div dir="rtl">بہت سے مختلف قسم کی معلومات درج کی جا سکتی ہیں، مختلف وجوہات کے لیے.<br /><br /></div>

##### <div dir="rtl">۱۱.۳.۰ بلاک کے واقعات<br /><br /></div>

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

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">logfile</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">logfile_apache</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">logfile_serialized</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

<div dir="rtl">جب یہ ہدایات خالی رہیں تو، اس قسم کی ریکارڈنگ غیر فعال رہیں گے.<br /><br /></div>

##### <div dir="rtl">۱۱.۳.۱ CAPTCHA لاگ<br /><br /></div>

<div dir="rtl">جب ایک صارف CAPTCHA مثال کے طور پر مکمل کرنے کی کوشش کرتا ہے، تو ریکارڈ کیا جاتا ہے.<br /><br /></div>

<div dir="rtl">ان ریکارڈوں میں صارف کے IP ایڈریس، تاریخ اور اس وقت کا واقعہ شامل ہے، اور حیثیت. یہ ریکارڈ عام طور پر اس طرح نظر آتے ہیں:<br /><br /></div>

```
IP پتہ: x.x.x.x - تاریخ وقت: Day, dd Mon 20xx hh:ii:ss +0000 - CAPTCHA کے ریاست: ایوان کے پاس!
```

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">logfile</code> &lt;- <code dir="ltr">recaptcha</code></li>
 <li><code dir="ltr">logfile</code> &lt;- <code dir="ltr">hcaptcha</code></li>
</ul></div>

##### <div dir="rtl">۱۱.۳.۲ سامنے کے آخر لاگ<br /><br /></div>

<div dir="rtl">یہ سامنے کے آخر میں لاگ ان کرنے کی کوشش کرنے سے متعلق ہے. جب سامنے کے آخر میں رسائی کو فعال کیا جاتا ہے، جب صارف کو سامنے کے آخر میں لاگ ان کرنے کی کوشش ہوتی ہے، تو ریکارڈ کیا جاتا ہے.<br /><br /></div>

<div dir="rtl">اس ریکارڈ میں صارف کے IP ایڈریس، تاریخ اور وقت اور اس کے نتائج شامل ہیں (کامیاب یا ناکامی). یہ عام طور پر اس طرح کچھ نظر آتا ہے:<br /><br /></div>

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - لاگ ان.
```

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">frontend_log</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">۱۱.۳.۳ لاگ گھومنے<br /><br /></div>

<div dir="rtl">آپ چاہتے ہیں، یا قانونی طور پر ہو سکتا ہے، کچھ وقت کے بعد لاگ ان کو صاف کرنے کے لیے (کتنی دیر تک آپ لاگ ان کو برقرار رکھ سکتے ہیں قانون کی طرف سے محدود ہوسکتے ہیں). یہ لاگ ان کے مطابق لاگ ان کی ترتیب میں تاریخ/وقت مارکر مقرر کرنے کی طرف سے کیا جا سکتا ہے (مثال کے طور پر، <code dir="ltr">{yyyy}-{mm}-{dd}.log</code>)، اور پھر لاگ گرد گھومنے کو چالو کرنے (لاگ گرد کی گردش آپ کو لاگ ان کی حد سے زیادہ حد تک زیادہ سے زیادہ لاگ ان پر لاگو کرنے کی اجازت دیتا ہے).<br /><br /></div>

<div dir="rtl">مثال کے طور پر: اگر مجھے 30 دنوں کے بعد لاگز کو خارج کرنے کی ضرورت ہوتی ہے تو میں <code dir="ltr">{dd}.log</code> اپنے لاگ ان کے نام میں ڈال سکتا ہوں (<code dir="ltr">{dd}</code> دن کی نمائندگی کرتا ہے)، <code dir="ltr">log_rotation_limit</code> کو 30 مقرر کریں، اور <code dir="ltr">log_rotation_action</code> کو <code dir="ltr">Delete</code> مقرر کریں.<br /><br /></div>

<div dir="rtl">اگر آپ کو کچھ وقت کے لیے ریکارڈ رکھنے کی ضرورت ہے تو، آپ کو لاگ گرد گھومنے کا استعمال نہ کرنے کا انتخاب کرسکتے ہیں، یا آپ <code dir="ltr">log_rotation_action</code> کی قدر <code dir="ltr">Archive</code> پر مقرر کر سکتے ہیں (اس ریکارڈ کو کمپیکٹ کریں گے، اس طرح ڈسک کے استعمال کو کم کرنا ہوگا).<br /><br /></div>

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">log_rotation_limit</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">log_rotation_action</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">۱۱.۳.۴ ٹرنک لاگ<br /><br /></div>

<div dir="rtl">اگر آپ چاہتے ہیں تو، آپ انفرادی ریکارڈز کو چھوٹ سکتے ہیں جب وہ مخصوص سائز سے کہیں زیادہ ہیں.<br /><br /></div>

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">truncate</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">۱۱.۳.۵ IP ایڈریس PSEUDONYMISATION<br /><br /></div>

<div dir="rtl">سب سے پہلے، اگر آپ اصطلاح سے واقف نہیں ہیں، "pseudonymisation" ذاتی اعداد و شمار کی پروسیسنگ سے مراد اس طرح سے ہے کہ یہ کسی بھی مخصوص شخص کو بغیر کسی ضمنی معلومات کی نشاندہی نہیں کی جاسکتی ہے، فراہم کی جاتی ہے کہ اس طرح کی اضافی معلومات علاحدہ طریقے سے برقرار رکھی جاتی ہے اور تکنیکی اور تنظیمی تدابیر کے تابع ہوتے ہیں اس بات کو یقینی بنانے کے لیے کہ ذاتی ڈیٹا کسی قدرتی شخص کو نشاندہی نہیں کی جاسکتی ہے.<br /><br /></div>

<div dir="rtl">مندرجہ ذیل وسائل اس سے مزید تفصیل میں وضاحت کرنے میں مدد کرسکتے ہیں:</div>
<div dir="rtl"><ul>
 <li><a dir="ltr" href="https://www.trust-hub.com/news/what-is-pseudonymisation/">[trust-hub.com] What is pseudonymisation?</a></li>
 <li><a dir="ltr" href="https://en.wikipedia.org/wiki/Pseudonymization">[Wikipedia] Pseudonymization</a></li>
</ul></div>

<div dir="rtl">کچھ حالات میں، آپ کو کسی بھی PII جمع، عملدرآمد، یا ذخیرہ کرنے کے لیے "anonymisation" یا "pseudonymisation" کو لاگو کرنا قانونی طور پر ضروری ہوسکتا ہے. یہ تصور ابھی کچھ وقت تک وجود میں آیا ہے، لیکن GDPR/DSGVO خاص طور پر "pseudonymisation" کا ذکر اور حوصلہ افزائی کرتا ہے.<br /><br /></div>

<div dir="rtl">اگر آپ چاہتے ہیں تو، CIDRAM لاگ ان کرتے وقت لاگ ان کرتے وقت IP پتے کے لیے یہ کر سکتے ہیں. جب لکھنا لکھنا، IPv4 پتے کے آخری آکٹیٹ اور IPv6 پتے کے دوسرے حصے کے بعد سب کچھ، "x" کی طرف سے نمائندگی کی جائے گی.<br /><br /></div>

<div dir="rtl"><em>نوٹ: CIDRAM کی IP ٹریکنگ کی خصوصیت اس کی صلاحیت نہیں ہے. اگر یہ آپ کے لیے ایک مسئلہ ہے، IP ٹریکنگ کو مکمل طور پر غیر فعال کرنے کے لیے یہ سب سے بہتر ہو سکتا ہے. یہ <code dir="ltr">track_mode</code> کی ترتیب <code dir="ltr"false></code>، اور کسی ماڈیول سے بچنے کی طرف سے حاصل کیا جا سکتا ہے.</em><br /><br /></div>

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">track_mode</code> &lt;- <code dir="ltr">signatures</code></li>
 <li><code dir="ltr">pseudonymise_ip_addresses</code> &lt;- <code dir="ltr">legal</code></li>
</ul></div>

##### <div dir="rtl">۱۱.۳.۶ لاگ ان معلومات کو چھوڑ دیں<br /><br /></div>

<div dir="rtl">اگر آپ مخصوص قسم کی معلومات کو مکمل طور پر لاگ ان کرنے سے روکنا چاہتے ہیں تو، آپ ایسا کرسکتے ہیں. CIDRAM ترتیبات ہدایات فراہم کرتا ہے جس پر کنٹرول کرتا ہے کہ IP ایڈریس، ہوسٹ نام، اور صارف کے ایجنٹوں لاگ ان ہوتے ہیں. عام طور پر، اور جب دستیاب ہے، یہ سب کچھ لاگ ان ہوتے ہیں. جب ان ترتیبات کے ہدایات <code dir="ltr">true</code> میں مقرر ہوتے ہیں، تو متعلقہ معلومات لاگ ان نہیں کی جائیں گی.<br /><br /></div>

<div dir="rtl"><em>نوٹ: IP پتے کے لیے pseudonymisation کا استعمال کرنے کی کوئی وجہ نہیں ہے جب IP پتے کو مکمل طور پر لاگ ان سے لے کر.</em><br /><br /></div>

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">omit_ip</code> &lt;- <code dir="ltr">legal</code></li>
 <li><code dir="ltr">omit_hostname</code> &lt;- <code dir="ltr">legal</code></li>
 <li><code dir="ltr">omit_ua</code> &lt;- <code dir="ltr">legal</code></li>
</ul></div>

##### <div dir="rtl">۱۱.۳.۷ اعداد و شمار<br /><br /></div>

<div dir="rtl">CIDRAM اعداد و شمار کو ٹریک کر سکتے ہیں، جیسے کہ کسی مخصوص وقت سے کتنے بلاک واقعات یا CAPTCHA مثال موجود ہیں. یہ خصوصیت ڈیفالٹ کے ذریعہ غیر فعال ہے، لیکن پیکیج کی ترتیب کے ذریعے فعال کیا جا سکتا ہے. یہ خصوصیت صرف واقعات کی تعداد کو ٹریک کرتا ہے. اس میں کوئی مخصوص معلومات شامل نہیں ہے، لہذا اسے PII کے طور پر نہیں جانا چاہیے.<br /><br /></div>

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">statistics</code> &lt;- <code dir="ltr">general</code></li>
</ul></div>

##### <div dir="rtl">۱۱.۳.۸ خفیہ کاری<br /><br /></div>

<div dir="rtl">CIDRAM اس کے لاگ ان یا کیش کو خفیہ نہیں کرتا. یہ مستقبل میں متعارف کرایا جا سکتا ہے، لیکن فی الحال اس کی کوئی مخصوص منصوبہ نہیں ہے. اگر آپ غیر قانونی شدہ تیسری جماعتوں کے بارے میں فکر مند ہیں تو CIDRAM میں حساس معلومات تک رسائی حاصل ہے، میں سفارش کرتا ہوں کہ عام طور پر قابل رسائی مقام پر CIDRAM انسٹال نہیں کیا جائے گا (مثال کے طور پر، <code dir="ltr">public_html</code> میں انسٹال نہ کریں) اور اس بات کو یقینی بنائیں کہ مناسب حد تک محدود پابندیوں کو نافذ کیا جائے. اگر یہ آپ کے خدشات کو حل کرنے کے لیے کافی نہیں ہے تو پھر CIDRAM کو ترتیب دیں تاکہ حساس معلومات جمع نہیں کی جائے گی (جیسے جیسے، لاگ ان کو غیر فعال کرکے).<br /><br /></div>

#### <div dir="rtl">۱۱.۴ کوکی<br /><br /></div>

<div dir="rtl">CIDRAM کو دو مقامات پر کوکیز کا تعین کرتا ہے. سب سے پہلے، CAPTCHA مکمل کرنے کے بعد "CIDRAM" کوکیز سیٹ کرتا ہے (اگر <code dir="ltr">lockuser</code> کو <code dir="ltr">true</code> میں مقرر کیا جاتا ہے تو)، لہذا یہ ہر درخواست پر ایسا کرنے کے لیے صارف سے پوچھنا جاری رکھنے کی ضرورت نہیں ہوگی. دوسرا، صارف کو سامنے کے آخر میں لاگ ان ہونے پر CIDRAM ایک کوکی سیٹ کرتا ہے (تصدیق کے مقاصد کے لیے).<br /><br /></div>

<div dir="rtl">دونوں صورتوں میں، صارف کو پہلے سے ہی کوکیز کے بارے میں خبردار کیا جاتا ہے. کوکیز کہیں اور نہیں بنائے جاتے ہیں.<br /><br /></div>

<div dir="rtl">نوٹ: "پوشیدہ" CAPTCHA APIs کو کچھ علاقوں میں کوکی قوانین سے مطابقت نہیں ہوسکتی ہے اور ایسے قوانین کے تابع کسی بھی ویب سائٹ سے ان کو پرہیز کرنا چاہیے. اس کے بجائے دوسرے فراہم کردہ API استعمال کرنے کا انتخاب کرنا، یا صرف مکمل طور پر CAPTCHA کو غیر فعال کرنا بہتر ہوگا.<br /><br /></div>

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">disable_frontend</code> &lt;- <code dir="ltr">general</code></li>
 <li><code dir="ltr">lockuser</code> &lt;- <code dir="ltr">recaptcha</code></li>
 <li><code dir="ltr">api</code> &lt;- <code dir="ltr">recaptcha</code></li>
 <li><code dir="ltr">lockuser</code> &lt;- <code dir="ltr">hcaptcha</code></li>
 <li><code dir="ltr">api</code> &lt;- <code dir="ltr">hcaptcha</code></li>
</ul></div>

#### <div dir="rtl">۱۱.۵ مارکیٹنگ اور اشتہارات<br /><br /></div>

<div dir="rtl">CIDRAM مارکیٹنگ یا اشتہارات کے مقاصد کے لیے کسی بھی معلومات جمع یا عمل نہیں کرتا ہے. یہ کسی جمع کردہ یا لاگ ان معلومات سے کوئی فائدہ نہیں فروخت کرتا ہے. CIDRAM ایک تجارتی ادارہ نہیں ہے، اور کسی بھی تجارتی مفادات سے متعلق نہیں ہے، لہذا ان کاموں کو کوئی احساس نہیں ہوگا. اس منصوبے کی شروعات کے بعد یہ معاملہ رہا ہے، اور آج ہی مقدمہ جاری ہے.<br /><br /></div>

#### <div dir="rtl">۱۱.۶ رازداری کی پالیسی<br /><br /></div>

<div dir="rtl">بعض اوقات آپ کو قانون کی طرف سے آپ کی ویب سائٹ پر اپنی جگہ پر اپنی رازداری کی پالیسی پر ایک لنک ظاہر کرنے کی ضرورت ہوسکتی ہے. اس بات کو یقینی بنانے کے لیے صارفین کو آپ کی رازداری کے طریقوں کے بارے میں مطلع کیا جاسکتا ہے، جو آپ جمع کرتے ہیں، اور آپ اس معلومات کے ساتھ کیا کرتے ہیں. CIDRAM کے "رسائی نہیں ہوئی" کے صفحے پر اس لنک کو شامل کرنے کے قابل ہونے کے لۓ، آپ کی رازداری کی پالیسی کے ایڈریس کی وضاحت کرنے کے لیے ایک ترتیب کا اختیار فراہم کیا جاتا ہے.<br /><br /></div>

<div dir="rtl">نوٹ: یہ سختی سے سفارش کی جاتی ہے کہ آپ کی رازداری کی پالیسی کا صفحہ CIDRAM کی حفاظت کے پیچھے نہیں ہے. اگر CIDRAM آپ کی پرائیویسی پالیسی کی حفاظت کرتا ہے تو، جب وہ آپ کی رازداری کی پالیسی پر لنک پر کلک کریں تو صارفین کو مسدود کیا جائے گا. مثالی طور پر، آپ کو اپنی رازداری کی پالیسی کی ایک مستحکم کاپی، جیسے HTML صفحہ یا سادہ متن فائل سے منسلک ہونا چاہیے.<br /><br /></div>

<div dir="rtl">متعلقہ ترتیب ہدایات:<br /></div>
<div dir="rtl"><ul>
 <li><code dir="ltr">privacy_policy</code> &lt;- <code dir="ltr">legal</code></li>
</ul></div>

#### <div dir="rtl">۱۱.۷ GDPR/DSGVO<br /><br /></div>

<div dir="rtl">GDPR یورپی یونین کا ایک ضابطہ ہے جو 25 مئی، 2018 تک اثر انداز ہوتا ہے. ریگولیشن کا بنیادی مقصد یہ ہے کہ یورپی یونین کے شہریوں اور باشندوں کو ان کے اپنے ذاتی ڈیٹا سے متعلق قابو پانے، اور پرائیویٹ اور ذاتی ڈیٹا کے بارے میں یورپی یونین کے اندر ریگولیشن کو متحد کرنا.<br /><br /></div>

<div dir="rtl">ریگولیشن کسی بھی EU کے "اعداد و شمار کے مضامین" (کسی بھی شناخت یا شناختی قدرتی شخص) کے "ذاتی طور پر شناختی معلومات" کی پروسیسنگ سے متعلق مخصوص اجزاء پر مشتمل ہے. تعمیل کرنے کے لیے، کمپنیوں، عمل، اور متعلقہ نظام، "ڈیزائن کی طرف سے رازداری" کو لاگو کرنا لازمی ہے، سب سے زیادہ ممکن راز رازداری کی ترتیبات کا استعمال کرنا ضروری ہے، کسی ذخیرہ یا پروسیسنگ معلومات کے لیے حفاظتی انتظامات کو لاگو کرنا ضروری ہے (بشمول، لیکن تک محدود نہیں، "pseudonymisation" اور "anonymisation")، واضح طور پر ان اعداد و شمار کی اقسام کا اعلان کرنا چاہیے جو وہ جمع کرتے ہیں، وہ کس طرح کے سببوں کے لیے، اس کے عمل کو کس طرح، وہ کتنی عرصے تک اسے برقرار رکھتی ہیں، اور اگر وہ اس ڈیٹا کو کسی بھی تیسری پارٹی کے ساتھ شریک کریں، اعداد و شمار کی اقسام، کیسے، کیوں، اور اسی طرح کی اقسام.<br /><br /></div>

<div dir="rtl">اعداد و شمار پر عملدرآمد نہیں کیا جاسکتا جب تک کہ ایسا کرنے کے لیے قانونی بنیاد نہ ہو، قواعد و ضوابط کے مطابق. عام طور پر، اس کا مطلب یہ ہے کہ یہ قانونی ذمہ داریوں کے مطابق ہونا ضروری ہے، اور صرف واضح ہونے کے بعد، اچھی طرح سے مطلع رضامندی کے اعداد و شمار سے حاصل کی گئی ہے.<br /><br /></div>

<div dir="rtl">وقت میں، قوانین تبدیل کر سکتے ہیں. لہذا، پرانے معلومات کو پھیلانے سے بچنے کے لۓ، یہ مستند ذریعہ سے سیکھنا بہتر ہوگا. اگر میں براہ راست یہاں معلومات شامل ہوں تو، یہ تاریخ سے باہر ہوسکتا ہے.<br /><br /></div>

<div dir="rtl">مزید معلومات سیکھنے کے لیے کچھ سفارش کردہ وسائل:<br /></div>
<div dir="rtl"><ul>
 <li><a href="https://ur.wikipedia.org/wiki/%D8%AC%D9%86%D8%B1%D9%84_%DA%88%DB%8C%D9%B9%D8%A7_%D9%BE%D8%B1%D9%88%D9%B9%DB%8C%DA%A9%D8%B4%D9%86_%D8%B1%DB%8C%DA%AF%D9%88%D9%84%DB%8C%D8%B4%D9%86">جنرل ڈیٹا پروٹیکشن ریگولیشن</a></li>
 <li><a href="https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679">REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL</a></li>
</ul></div>

---


<div dir="rtl">آخری تازہ کاری: ۱۷ مئی ۲۰۲۵ (۲۰۲۵.۰۵.۱۷).</div>
