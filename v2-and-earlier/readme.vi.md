## Tài liệu của CIDRAM v2 (Tiếng Việt).

### Nội dung
- 1. [LỜI GIỚI THIỆU](#user-content-SECTION1)
- 2. [CÁCH CÀI ĐẶT](#user-content-SECTION2)
- 3. [CÁCH SỬ DỤNG](#user-content-SECTION3)
- 4. [QUẢN LÝ FRONT-END](#user-content-SECTION4)
- 5. [TẬP TIN BAO GỒM TRONG GÓI NÀY](#user-content-SECTION5)
- 6. [TÙY CHỌN CHO CẤU HÌNH](#user-content-SECTION6)
- 7. [ĐỊNH DẠNG CỦA CHỬ KÝ](#user-content-SECTION7)
- 8. [NHỮNG VẤN ĐỀ HỢP TƯƠNG TÍCH](#user-content-SECTION8)
- 9. [NHỮNG CÂU HỎI THƯỜNG GẶP (FAQ)](#user-content-SECTION9)
- 10. *Dành riêng cho các bổ sung trong tương lai cho tài liệu.*
- 11. [THÔNG TIN HỢP PHÁP](#user-content-SECTION11)

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### 1. <a name="SECTION1"></a>LỜI GIỚI THIỆU

CIDRAM (Classless Inter-Domain Routing Access Manager) là một kịch bản PHP được thiết kế để bảo vệ các trang mạng bằng cách ngăn chặn các yêu cầu có nguồn gốc từ các địa chỉ IP coi như là nguồn của lưu lượng không mong muốn, bao gồm (nhưng không giới hạn) giao thông từ thiết bị đầu cuối truy cập không phải con người, dịch vụ điện toán đám mây, chương trình gửi thư rác, công cụ cào, vv. Nó làm điều này bằng cách tính toán CIDR có thể các địa chỉ IP cung cấp từ các yêu cầu gửi đến và sau đó cố gắng để phù hợp với những CIDR có thể chống lại các tập tin chữ ký của nó (các tập tin chữ ký chứa danh sách các CIDR các địa chỉ IP coi như là nguồn của lưu lượng không mong muốn); Nếu trận đấu được tìm thấy, các yêu cầu được chặn.

*(Xem: ["CIDR" là gì?](#user-content-WHAT_IS_A_CIDR)).*

BẢN QUYỀN [CIDRAM](https://cidram.github.io/) 2016 và hơn GNU/GPLv2 by [Caleb M (Maikuolan)](https://github.com/Maikuolan).

Bản này là chương trình miễn phí; bạn có thể phân phối lại hoạc sửa đổi dưới điều kiện của GNU Giấy Phép Công Cộng xuất bản bởi Free Software Foundation; một trong giấy phép phần hai, hoạc (tùy theo sự lựa chọn của bạn) bất kỳ phiên bản nào sau này. Bản này được phân phối với hy vọng rằng nó sẽ có hữu ích, nhưng mà KHÔNG CÓ BẢO HÀNH; ngay cả những bảo đảm ngụ ý KHẢ NĂNG BÁN HÀNG hoạc PHÙ HỢP VỚI MỤC ĐÍT VÀO. Hảy xem GNU Giấy Phép Công Cộng để biết them chi tiết, nằm trong tập tin `LICENSE.txt`, và kho chứa của tập tin này có thể tiềm đước tại:
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

Tài liệu này và các gói liên quan của nó có thể được tải về miễn phí từ:
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [SourceForge](https://sourceforge.net/projects/cidram/).

---


### 2. <a name="SECTION2"></a>CÁCH CÀI ĐẶT

#### 2.0 CÀI ĐẶT THỦ CÔNG

1) Nếu bạn đang đọc cái này thì tôi hy vọng là bạn đã tải về một bản sao kho lưu trữ của bản, giải nén nội dung của nó và nó đang nằm ở một nơi nào đó trên máy tính của bạn. Từ đây, bạn sẽ muốn đặt nội dung ở một nơi trên máy chủ hoặc CMS của bạn. Một thư mục chẳng hạn như `/public_html/cidram/` hay tương tự (mặc dù sự lựa chọn của bạn không quan trọng, miễn là nó an toàn và bạn hài lòng với sự lựa chọn) sẽ đủ.. *Trước khi bạn bắt đầu tải lên, hảy tiếp tục đọc..*

2) Đổi tên `config.ini.RenameMe` đến `config.ini` (nằm bên trong `vault`), và nếu bạn muốn (đề nghị mạnh mẽ cho người dùng cao cấp, nhưng không đề nghị cho người mới bắt đầu hay cho người thiếu kinh nghiệm), mở nó (tập tin này bao gồm tất cả các tùy chọn có sẵn cho CIDRAM; trên mỗi tùy chọn nên có một nhận xét ngắn gọn mô tả những gì nó làm và những gì nó cho). Điều chỉnh các tùy chọn như bạn thấy phù hợp, theo bất cứ điều gì là thích hợp cho tập hợp cụ thể của bạn lên. Lưu tập tin, đóng.

3) Tải nội dung lên (CIDRAM và tập tin của nó) vào thư mục bạn đã chọn trước (bạn không cần phải dùng tập tin `*.txt`/`*.md`, nhưng chủ yếu, bạn nên tải lên tất cả mọi thứ).

4) CHMOD thư mục `vault` thành "755" (nếu có vấn đề, bạn có thể thử "777", mặc dù này là kém an toàn). Các thư mục chính kho lưu trữ các nội dung (một trong những cái bạn đã chọn trước), bình thường, có thể riêng, nhưng tình hình CHMOD nên kiểm tra, nếu bạn đã có vấn đề cho phép trong quá khứ về hệ thống của bạn (theo mặc định, nên giống như "755"). Nói ngắn gọn: Đối với các gói để hoạt động đúng, PHP cần để có thể đọc và ghi các tập tin bên trong thư mục `vault`. Nhiều thứ (cập nhật, đăng nhập, vv) sẽ không thể, nếu PHP không thể ghi vào thư mục `vault`, và gói sẽ không hoạt động chút nào nếu PHP không thể đọc từ thư mục `vault`. Tuy nhiên, để bảo mật tối ưu, đảm bảo rằng thư mục `vault` KHÔNG được truy cập công khai (thông tin nhạy cảm, chẳng hạn như thông tin chứa bởi `config.ini` hoặc `frontend.dat`, có thể tiếp xúc với những kẻ tấn công tiềm năng nếu thư mục `vault` có thể truy cập công khai).

5) Tiếp theo, bạn sẽ cần "nối" CIDRAM vào hệ thống của bạn hay CMS. Có một số cách mà bạn có thể "nối" bản chẳng hạn như CIDRAM vào hệ thống hoạc CMS, nhưng cách đơn giản nhất là cần có bản vào cốt lõi ở đầu của tập tin hoạc hệ thống hay CMS của bạn (một mà thường sẽ luôn luôn được nạp khi ai đó truy cập bất kỳ trang nào trên trang mạng của bạn) bằng cách sử dụng một lời chỉ thị `require` hoạc `include`. Thường, cái nàu sẽ được lưu trong một thư mục như `/includes`, `/assets` hoạc `/functions`, và sẽ thường được gọi là `init.php`, `common_functions.php`, `functions.php` hoạc tương tự. Bạn sẽ cần tiềm ra tập tin nào cho trường hợp của bạn; Nếu bạn gặp khó khăn trong việc này ra cho chính mình, hãy truy các trang issues (các vấn đề) của CIDRAM và cho chúng tôi biêt. Để làm chuyện này [sử dụng `require` họac `include`], đánh các dòng mã sao đây vào đầu của cốt lõi của tập tin, thay thế các dây chứa bên trong các dấu ngoặc kép với địa chỉ chính xác của tập tin `loader.php` (địa chỉ địa phương, chứ không phải địa chỉ HTTP; nó sẽ nhình gióng địa chỉ kho nói ở trên).

`<?php require '/user_name/public_html/cidram/loader.php'; ?>`

Lưu tập tin, đóng lại, tải lên lại.

-- CÁCH KHÁC --

Nếu bạn đang sử dụng trang chủ Apache và nếu bạn có thể truy cập `php.ini`, bạn có thể sử dụng `auto_prepend_file` chỉ thị để thêm vào trước CIDRAM bất cứ khi nào bất kỳ yêu cầu PHP được xin. Gióng như:

`auto_prepend_file = "/user_name/public_html/cidram/loader.php"`

Hoạc cái này trong tập tin `.htaccess`:

`php_value auto_prepend_file "/user_name/public_html/cidram/loader.php"`

6) Đó là tất cả mọi thứ! :-)

#### 2.1 CÀI ĐẶT VỚI COMPOSER

[CIDRAM được đăng ký với Packagist](https://packagist.org/packages/cidram/cidram), và như vậy, nếu bạn đã quen với Composer, bạn có thể sử dụng Composer để cài đặt CIDRAM (bạn vẫn cần phải chuẩn bị cấu hình, quyền CHMOD và kết nối; xem "cài đặt thủ công" bước 2, 4, và 5).

`composer require cidram/cidram`

#### 2.2 CÀI ĐẶT CHO WORDPRESS

Nếu bạn muốn sử dụng CIDRAM với WordPress, bạn có thể bỏ qua tất cả các hướng dẫn ở trên. [CIDRAM được đăng ký như một plugin với cơ sở dữ liệu plugin của WordPress](https://wordpress.org/plugins/cidram/), và bạn có thể cài đặt CIDRAM trực tiếp từ các bảng điều khiển plugin. Bạn có thể cài đặt nó theo cách tương tự như các plugin khác, và không có bước bổ sung được yêu cầu. Giống như với các phương pháp cài đặt khác, bạn có thể tùy chỉnh cài đặt của bạn bằng cách sửa đổi nội dung của tập tin `config.ini` hay bằng cách sử dụng trang cấu hình của front-end. Nếu bạn kích hoạt front-end của CIDRAM và cập nhật CIDRAM bằng cách sử dụng trang cập nhật của front-end, điều này sẽ tự động đồng bộ các thông tin phiên bản plugin với thông tin được hiển thị trong các bảng điều khiển plugin.

*Cảnh báo: Đang nhật CIDRAM qua bảng điều khiển plugin kết quả trong một cài đặt sạch sẽ! Nếu bạn đã tùy chỉnh cài đặt (thay đổi cấu hình của bạn, cài đặt các mô-đun, vv), những tuỳ chỉnh này sẽ bị mất khi đang nhật thông qua bảng điều khiển plugin! Các tập tin đăng nhập cũng sẽ bị mất khi đang nhật thông qua bảng điều khiển plugin! Để bảo vệ các tập tin đăng nhập và tùy chỉnh, đang nhật thông qua trang đang nhật front-end CIDRAM.*

---


### 3. <a name="SECTION3"></a>CÁCH SỬ DỤNG

CIDRAM nên tự động chặn các yêu cầu không mong muốn để trang mạng của bạn mà không cần bất kỳ hỗ trợ bằng tay, trừ cài đặt.

Bạn có thể tùy chỉnh cấu hình của bạn và tùy chỉnh mà CIDR bị chặn bằng cách sửa đổi tập tin cấu hình hay tập tin chữ ký của bạn.

Nếu bạn gặp bất kỳ sai tích cực, xin vui lòng liên hệ với tôi để cho tôi biết về nó. *(Xem: ["Sai tích cực" là gì?](#user-content-WHAT_IS_A_FALSE_POSITIVE)).*

CIDRAM có thể được cập nhật bằng tay hoặc thông qua front-end. CIDRAM cũng có thể được cập nhật qua Composer hoặc WordPress, nếu ban đầu được cài đặt qua các phương tiện đó.

---


### 4. <a name="SECTION4"></a>QUẢN LÝ FRONT-END

#### 4.0 FRONT-END LÀ GÌ.

Các front-end cung cấp một cách thuận tiện và dễ dàng để duy trì, quản lý và cập nhật cài đặt CIDRAM của bạn. Bạn có thể xem, chia sẻ và tải về các tập tin bản ghi thông qua các trang bản ghi, bạn có thể sửa đổi cấu hình thông qua các trang cấu hình, bạn có thể cài đặt và gỡ bỏ cài đặt các thành phần thông qua các trang cập nhật, và bạn có thể tải lên, tải về, và sửa đổi các tập tin trong vault của bạn thông qua các quản lý tập tin.

Các front-end được tắt theo mặc định để ngăn chặn truy cập trái phép (truy cập trái phép có thể có hậu quả đáng kể cho trang web của bạn và an ninh của mình). Hướng dẫn cho phép nó được bao gồm bên dưới đoạn này.

#### 4.1 LÀM THẾ NÀO ĐỂ KÍCH HOẠT FRONT-END.

1) Xác định vị trí các chỉ thị `disable_frontend` bên trong `config.ini`, và đặt nó vào `false` (nó sẽ là `true` bởi mặc định).

2) Truy cập `loader.php` từ trình duyệt của bạn (ví dụ, `http://localhost/cidram/loader.php`).

3) Đăng nhập với tên người dùng và mật khẩu mặc định (admin/password).

Chú thích: Sau khi bạn đã đăng nhập lần đầu tiên, để ngăn chặn truy cập trái phép vào các front-end, bạn phải ngay lập tức thay đổi tên người dùng và mật khẩu của bạn! Điều này là rất quan trọng, bởi vì nó có thể tải lên các mã PHP tùy ý để trang web của bạn thông qua các front-end.

Ngoài ra, để bảo mật tối ưu, hãy bật "xác thực hai yếu tố" cho tất cả tài khoản front-end (hướng dẫn được cung cấp bên dưới).

#### 4.2 LÀM THẾ NÀO ĐỂ SỬ DỤNG FRONT-END.

Các hướng dẫn được cung cấp trên mỗi trang của front-end, để giải thích một cách chính xác để sử dụng nó và mục đích của nó. Nếu bạn cần giải thích thêm hay bất kỳ sự hỗ trợ đặc biệt, vui lòng liên hệ hỗ trợ. Cũng thế, có một số video trên YouTube có thể giúp bằng cách viện trợ trực quan.

#### 4.3 2FA (XÁC THỰC HAI YẾU TỐ)

Việc bật xác thực hai yếu tố ("2FA") có thể làm cho front-end an toàn hơn. Khi đăng nhập vào tài khoản có hỗ trợ 2FA, một email sẽ được gửi đến địa chỉ email được liên kết với tài khoản đó. Email này chứa "mã 2FA", mà sau đó người dùng phải nhập, ngoài tên người dùng và mật khẩu, để có thể đăng nhập bằng tài khoản đó. Điều này có nghĩa là việc lấy mật khẩu tài khoản sẽ không đủ cho bất kỳ tin tặc hoặc kẻ tấn công tiềm năng nào có thể đăng nhập vào tài khoản đó, bởi vì họ cũng cần phải có quyền truy cập vào địa chỉ email được liên kết với tài khoản đó để có thể nhận và sử dụng mã 2FA được kết hợp với phiên, do đó làm cho front-end an toàn hơn.

Thứ nhất, để bật xác thực hai yếu tố, sử dụng trang cập nhật front-end để cài đặt thành phần PHPMailer. CIDRAM sử dụng PHPMailer để gửi email. Lưu ý rằng mặc dù CIDRAM tương thích với PHP >= 5.4.0, PHPMailer cần PHP >= 5.5.0, do đó, xác thực hai yếu tố trong CIDRAM sẽ không thể cho người dùng PHP 5.4.

Sau khi bạn đã cài đặt PHPMailer, bạn sẽ cần điền các chỉ thị cấu hình cho PHPMailer thông qua trang cấu hình CIDRAM hoặc tập tin cấu hình. Thông tin thêm về các chỉ thị cấu hình này được bao gồm trong phần cấu hình của tài liệu này. Sau khi bạn đã điền các chỉ thị cấu hình PHPMailer, hãy đặt `enable_two_factor` thành `true`. Xác thực hai yếu tố bây giờ sẽ được bật.

Tiếp theo, bạn cần liên kết địa chỉ email với tài khoản, để CIDRAM có thể biết nơi gửi mã 2FA khi đăng nhập bằng tài khoản đó. Để thực hiện việc này, hãy sử dụng địa chỉ email làm tên người dùng cho tài khoản (như `foo@bar.tld`), hoặc bao gồm địa chỉ email như một phần của tên người dùng giống như khi gửi email thông thường (như `Foo Bar <foo@bar.tld>`).

Chú thích: Bảo vệ vault của bạn khỏi bị truy cập trái phép (ví dụ, bằng cách tăng cường bảo mật cho máy chủ của bạn và hạn chế quyền truy cập công cộng), là đặc biệt quan trọng ở đây, vì truy cập trái phép vào tập tin cấu hình của bạn (được lưu trữ trong vault của bạn), có thể có nguy cơ phơi bày cài đặt SMTP gửi đi của bạn (bao gồm tên người dùng và mật khẩu SMTP). Bạn nên đảm bảo rằng vault của bạn được bảo mật đúng cách trước khi bật xác thực hai yếu tố. Nếu bạn không thể làm điều này, thì ít nhất, bạn nên tạo một tài khoản email mới, dành riêng cho mục đích này, để giảm thiểu rủi ro liên quan đến các bị phơi bày cài đặt SMTP.

---


### 5. <a name="SECTION5"></a>TẬP TIN BAO GỒM TRONG GÓI NÀY

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


### 6. <a name="SECTION6"></a>TÙY CHỌN CHO CẤU HÌNH

Sau đây là danh sách các biến tìm thấy trong tập tin cấu hình cho CIDRAM `config.ini`, cùng với một mô tả về mục đích và chức năng của chúng.

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

#### "general" (Thể loại)
Cấu hình chung cho CIDRAM.

##### "logfile"
- Tập tin có thể đọc con người cho ghi tất cả các nỗ lực truy cập bị chặn. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

##### "logfile_apache"
- *v1: "logfileApache"*
- Tập tin Apache phong cách cho ghi tất cả các nỗ lực truy cập bị chặn. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

##### "logfile_serialized"
- *v1: "logfileSerialized"*
- Tập tin tuần tự cho ghi tất cả các nỗ lực truy cập bị chặn. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

*Mẹo hữu ích: Nếu bạn muốn, bạn có thể thêm thông tin ngày/giờ trong tên các tập tin ghi của bạn bằng cách bao gồm những trong tên: `{yyyy}` cho năm đầy, `{yy}` cho năm viết tắt, `{mm}` cho tháng, `{dd}` cho ngày, `{hh}` cho giờ.*

*Các ví dụ:*
- *`logfile='logfile.{yyyy}-{mm}-{dd}-{hh}.txt'`*
- *`logfile_apache='access.{yyyy}-{mm}-{dd}-{hh}.txt'`*
- *`logfile_serialized='serial.{yyyy}-{mm}-{dd}-{hh}.txt'`*

##### "error_log"
- Một tập tin để ghi lại bất kỳ lỗi không nghiêm trọng được phát hiện. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

##### "error_log_stages"
- Một danh sách các giai đoạn trong chuỗi thực thi, theo đó bất kỳ lỗi nào được tạo sẽ được ghi lại.
- *Mặc định: "Tests,Modules,SearchEngineVerification,SocialMediaVerification,OtherVerification,Aux,Reporting,Tracking,RL,CAPTCHA,Statistics,Webhooks,Output,NonBlockedCAPTCHA"*

##### "truncate"
- Dọn dẹp các bản ghi khi họ được một kích thước nhất định? Giá trị là kích thước tối đa bằng B/KB/MB/GB/TB mà một tập tin bản ghi có thể tăng lên trước khi bị dọn dẹp. Giá trị mặc định 0KB sẽ vô hiệu hoá dọn dẹp (các bản ghi có thể tăng lên vô hạn). Lưu ý: Áp dụng cho tập tin riêng biệt! Kích thước tập tin bản ghi không được coi là tập thể.

##### "log_rotation_limit"
- Xoay vòng nhật ký giới hạn số lượng của tập tin nhật ký có cần tồn tại cùng một lúc. Khi các tập tin nhật ký mới được tạo, nếu tổng số lượng tập tin nhật ký vượt quá giới hạn được chỉ định, hành động được chỉ định sẽ được thực hiện. Bạn có thể chỉ định giới hạn mong muốn tại đây. Giá trị 0 sẽ vô hiệu hóa xoay vòng nhật ký.

##### "log_rotation_action"
- Xoay vòng nhật ký giới hạn số lượng của tập tin nhật ký có cần tồn tại cùng một lúc. Khi các tập tin nhật ký mới được tạo, nếu tổng số lượng tập tin nhật ký vượt quá giới hạn được chỉ định, hành động được chỉ định sẽ được thực hiện. Bạn có thể chỉ định hành động mong muốn tại đây. Delete = Xóa các tập tin nhật ký cũ nhất, cho đến khi giới hạn không còn vượt quá. Archive = Trước tiên lưu trữ, và sau đó xóa các tập tin nhật ký cũ nhất, cho đến khi giới hạn không còn vượt quá.

*Làm rõ kỹ thuật: Trong ngữ cảnh này, "cũ nhất" có nghĩa là không được sửa đổi gần đây.*

##### "timezone"
- Điều này được sử dụng để xác định múi giờ nào CIDRAM nên sử dụng cho ngày/giờ. Nếu bạn không cần nó, bỏ qua nó. Các giá trị có thể được xác định bởi PHP. Nó thường được đề nghị thay vì để điều chỉnh các chỉ thị múi giờ trong tập tin `php.ini` của bạn, nhưng đôi khi (như ví dụ, khi làm việc với giới hạn cung cấp lưu trữ chia sẻ) đây không phải là luôn luôn có thể làm, và như vậy, tùy chọn này được cung cấp ở đây.

##### "time_offset"
- *v1: "timeOffset"*
- Nếu thời gian máy chủ của bạn không phù hợp với thời gian địa phương của bạn, bạn có thể chỉ định một bù đắp đây để điều chỉnh thông tin ngày/giờ được tạo ra bởi CIDRAM theo yêu cầu của bạn. Nó thường được đề nghị thay vì để điều chỉnh các chỉ thị múi giờ trong tập tin `php.ini` của bạn, nhưng đôi khi (như ví dụ, khi làm việc với giới hạn cung cấp lưu trữ chia sẻ) đây không phải là luôn luôn có thể làm, và như vậy, tùy chọn này được cung cấp ở đây. Bù đắp được đo bằng phút.
- Ví dụ (để thêm một giờ): `time_offset=60`

##### "time_format"
- *v1: "timeFormat"*
- Định dạng ngày tháng sử dụng bởi CIDRAM. Mặc định = `{Day}, {dd} {Mon} {yyyy} {hh}:{ii}:{ss} {tz}`.

##### "ipaddr"
- Nơi để tìm địa chỉ IP của các yêu cầu kết nối? (Hữu ích cho các dịch vụ như Cloudflare và vv). Mặc định = REMOTE_ADDR. CẢNH BÁO: Không thay đổi này, trừ khi bạn biết những gì bạn đang làm!

Giá trị được khuyến khích cho "ipaddr":

Giá trị | Sử dụng
---|---
`HTTP_INCAP_CLIENT_IP` | Proxy reverse Incapsula.
`HTTP_CF_CONNECTING_IP` | Proxy reverse Cloudflare.
`CF-Connecting-IP` | Proxy reverse Cloudflare (một sự thay thế; nếu ở trên không hoạt động).
`HTTP_X_FORWARDED_FOR` | Proxy reverse Cloudbric.
`X-Forwarded-For` | [Proxy reverse Squid](http://www.squid-cache.org/Doc/config/forwarded_for/).
`Forwarded` | *[Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded).*
*Xác định bởi cấu hình máy chủ.* | [Proxy reverse Nginx](https://www.nginx.com/resources/admin-guide/reverse-proxy/).
`REMOTE_ADDR` | Không có proxy reverse (giá trị mặc định).

##### "forbid_on_block"
- Những gì thông báo trạng thái HTTP mà CIDRAM nên gửi khi yêu cầu bị chặn?

Giá trị hiện được hỗ trợ:

Mã trạng thái | Thông thái trạng thái | Chi tiết
---|---|---
`200` | `200 OK` | Giá trị mặc định. Không mạnh mẽ, nhưng thân thiện với người dùng nhất. Các yêu cầu tự động rất có thể sẽ diễn giải phản hồi này là dấu hiệu cho thấy yêu cầu đã thành công.
`403` | `403 Forbidden` | Hơi mạnh mẽ, và thân thiện với người dùng. Được khuyến khích cho hầu hết các trường hợp chung.
`410` | `410 Gone` | Có thể gây ra sự cố khi giải quyết các sai tích cực, vì một số trình duyệt sẽ lưu vào bộ nhớ cache thông báo trạng thái này và không gửi các yêu cầu tiếp theo, ngay cả khi đã được bỏ chặn. Có thể thích hợp nhất trong một số ngữ cảnh, đối với một số loại lưu lượng truy cập nhất định.
`418` | `418 I'm a teapot` | Điều này đề cập đến một trò đùa ngày cá tháng tư ([RFC 2324](https://tools.ietf.org/html/rfc2324#section-6.5.14)). Rất khó có thể được hiểu bởi bất kỳ ứng dụng khách, bot, trình duyệt, hoặc cách nào khác. Được cung cấp để giải trí và tiện lợi, nhưng thường không được khuyến khích.
`451` | `451 Unavailable For Legal Reasons` | Được khuyến khích khi chặn chủ yếu vì lý do pháp lý. Không được khuyến khích trong các ngữ cảnh khác.
`503` | `503 Service Unavailable` | Mạnh mẽ nhất, nhưng không thân thiện với người dùng. Được khuyến khích khi bị tấn công, hoặc khi xử lý lưu lượng truy cập không mong muốn và cực kỳ dai dẳng.

##### "silent_mode"
- CIDRAM nên âm thầm chuyển hướng cố gắng truy cập bị chặn thay vì hiển thị trang "Truy cập đã bị từ chối"? Nếu vâng, xác định vị trí để chuyển hướng cố gắng truy cập bị chặn để. Nếu không, để cho biến này được trống.

##### "lang"
- Xác định tiếng mặc định cho CIDRAM.

##### "lang_override"
- Bản địa hóa theo HTTP_ACCEPT_LANGUAGE bất cứ khi nào có thể? True = Vâng [Mặc định]; False = Không.

##### "numbers"
- Chỉ định cách hiển thị số.

Giá trị hiện được hỗ trợ:

Giá trị | Nó tạo ra | Chi tiết
---|---|---
`NoSep-1` | `1234567.89`
`NoSep-2` | `1234567,89`
`Latin-1` | `1,234,567.89` | Giá trị mặc định.
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

*Chú thích: Các giá trị này không được chuẩn hóa ở bất kỳ đâu, và có thể sẽ không liên quan ngoài gói. Ngoài ra, các giá trị được hỗ trợ có thể thay đổi trong tương lai.*

##### "emailaddr"
- Nếu bạn muốn, bạn có thể cung cấp một địa chỉ email ở đây để được trao cho người dùng khi họ đang bị chặn, cho họ để sử dụng như một điểm tiếp xúc cho hỗ trợ hay giúp đở cho trong trường hợp họ bị chặn bởi nhầm hay lỗi. CẢNH BÁO: Bất kỳ địa chỉ email mà bạn cung cấp ở đây sẽ chắc chắn nhất được mua lại bởi chương trình thư rác và cái nạo trong quá trình con của nó được sử dụng ở đây, và như vậy, nó khuyên rằng nếu bạn chọn để cung cấp một địa chỉ email ở đây, mà bạn đảm bảo rằng địa chỉ email bạn cung cấp ở đây là một địa chỉ dùng một lần hay một địa chỉ mà bạn không nhớ được thư rác (nói cách khác, có thể bạn không muốn sử dụng một cá nhân chính hay kinh doanh chính địa chỉ email).

##### "emailaddr_display_style"
- Bạn muốn địa chỉ email được trình bày như thế nào với người dùng? "default" = Liên kết có thể nhấp. "noclick" = Văn bản không thể nhấp.

##### "disable_cli"
- *(Loại bỏ kể từ v2).*
- Vô hiệu hóa chế độ CLI? Chế độ CLI được kích hoạt theo mặc định, nhưng đôi khi có thể gây trở ngại cho công cụ kiểm tra nhất định (như PHPUnit, cho ví dụ) và khác ứng dụng mà CLI dựa trên. Nếu bạn không cần phải vô hiệu hóa chế độ CLI, bạn nên bỏ qua tùy chọn này. False = Kích hoạt chế độ CLI [Mặc định]; True = Vô hiệu hóa chế độ CLI.

##### "disable_frontend"
- Vô hiệu hóa truy cập front-end? Truy cập front-end có thể làm cho CIDRAM dễ quản lý hơn, nhưng cũng có thể là một nguy cơ bảo mật tiềm năng. Đó là khuyến cáo để quản lý CIDRAM từ các back-end bất cứ khi nào có thể, nhưng truy cập front-end là cung cấp khi nó không phải là có thể. Giữ nó vô hiệu hóa trừ khi bạn cần nó. False = Kích hoạt truy cập front-end; True = Vô hiệu hóa truy cập front-end [Mặc định].

##### "max_login_attempts"
- Số lượng tối đa cố gắng đăng nhập front-end. Mặc định = 5.

##### "frontend_log"
- *v1: "FrontEndLog"*
- Tập tin cho ghi cố gắng đăng nhập front-end. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

##### "signatures_update_event_log"
- Một tập tin để ghi nhật ký khi chữ ký được cập nhật qua front-end. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

##### "ban_override"
- Ghi đè "forbid_on_block" khi "infraction_limit" bị vượt quá? Khi ghi đè: Các yêu cầu bị chặn sản xuất một trang trống (tập tin mẫu không được sử dụng). 200 = Không ghi đè [Mặc định]. Các giá trị khác giống với các giá trị có sẵn cho "forbid_on_block".

##### "log_banned_ips"
- Bao gồm các yêu cầu bị chặn từ các IP bị cấm trong các tập tin đăng nhập? True = Vâng [Mặc định]; False = Không.

##### "default_dns"
- Một dấu phẩy phân cách danh sách các máy chủ DNS để sử dụng cho tra cứu tên máy. Mặc định = "8.8.8.8,8.8.4.4" (Google DNS). CẢNH BÁO: Không thay đổi này, trừ khi bạn biết những gì bạn đang làm!

*Xem thêm: [Những gì tôi có thể sử dụng cho "default_dns"?](#user-content-những-gì-tôi-có-thể-sử-dụng-cho-default_dns)*

##### "search_engine_verification"
- Cố gắng xác minh các yêu cầu từ các máy tìm kiếm? Xác minh máy tìm kiếm đảm bảo rằng họ sẽ không bị cấm là kết quả của vượt quá giới các hạn vi phạm (cấm các máy tìm kiếm từ trang web của bạn thường sẽ có một tác động tiêu cực đến các xếp hạng máy tìm kiếm của bạn, SEO, vv). Khi xác minh được kích hoạt, các máy tìm kiếm có thể bị chặn như bình thường, nhưng sẽ không bị cấm. Khi xác minh không được kích hoạt, họ có thể bị cấm như là kết quả của vượt quá giới các hạn vi phạm. Ngoài ra, xác minh máy tìm kiếm cung cấp bảo vệ chống lại các yêu cầu giả máy tìm kiếm và chống lại các thực thể rằng là khả năng độc hại được giả mạo như là các máy tìm kiếm (những yêu cầu này sẽ bị chặn khi xác minh máy tìm kiếm được kích hoạt). True = Kích hoạt xác minh máy tìm kiếm [Mặc định]; False = Vô hiệu hóa xác minh máy tìm kiếm.

Được hỗ trợ hiện tại:
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

Không tương thích (gây ra xung đột):
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

##### "social_media_verification"
- Cố gắng xác minh yêu cầu truyền thông xã hội? Xác minh truyền thông xã hội cung cấp sự bảo vệ chống lại các yêu cầu truyền thông xã hội giả mạo (các yêu cầu như vậy sẽ bị chặn). True = Kích hoạt xác minh truyền thông xã hội [Mặc định]; False = Vô hiệu hóa xác minh truyền thông xã hội.

Được hỗ trợ hiện tại:
- __[Embedly](https://udger.com/resources/ua-list/bot-detail?bot=Embedly#id22674)__
- __** [Facebook external hit](https://developers.facebook.com/docs/sharing/webmasters/crawler/)__
- __[Pinterest](https://help.pinterest.com/en/articles/about-pinterest-crawler-0)__
- __[Twitterbot](https://udger.com/resources/ua-list/bot-detail?bot=Twitterbot#id6168)__

_**: Yêu cầu chức năng tra cứu ASN, v.d., từ mô-đun BGPView._

##### "other_verification"
- Bất cứ khi nào có thể, hãy cố gắng xác minh các loại yêu cầu khác (ví dụ: AdSense, công cụ kiểm tra SEO, vv)? Khi bị phát hiện, các yêu cầu giả mạo sẽ bị chặn. True = Kích hoạt [Mặc định]; False = Vô hiệu hóa.

Được hỗ trợ hiện tại:
- __[AdSense](https://developers.google.com/search/docs/advanced/crawling/overview-google-crawlers)__
- __[AmazonAdBot](https://adbot.amazon.com/index.html)__
- __[Oracle Data Cloud Crawler](https://www.oracle.com/corporate/acquisitions/grapeshot/crawler.html)__

##### "protect_frontend"
- Chỉ định liệu các bảo vệ thường được cung cấp bởi CIDRAM nên được áp dụng cho các front-end. True = Vâng [Mặc định]; False = Không.

##### "disable_webfonts"
- Vô hiệu hóa các webfont? True = Vâng [Mặc định]; False = Không.

##### "maintenance_mode"
- Bật chế độ bảo trì? True = Vâng; False = Không [Mặc định]. Vô hiệu hoá mọi thứ khác ngoài các front-end. Đôi khi hữu ích khi cập nhật CMS, framework của bạn, vv.

##### "default_algo"
- Xác định thuật toán nào sẽ sử dụng cho tất cả các mật khẩu và phiên trong tương lai. Tùy chọn: PASSWORD_DEFAULT (mặc định), PASSWORD_BCRYPT, PASSWORD_ARGON2I (yêu cầu PHP >= 7.2.0), PASSWORD_ARGON2ID (yêu cầu PHP >= 7.3.0).

##### "statistics"
- Giám sát thống kê sử dụng CIDRAM? True = Vâng; False = Không [Mặc định].

##### "force_hostname_lookup"
- Thực hiện tìm kiếm tên máy chủ cho tất cả các yêu cầu? True = Vâng; False = Không [Mặc định]. Tìm kiếm tên máy chủ thường được thực hiện trên cơ sở cần thiết, nhưng có thể được thực hiện cho tất cả các yêu cầu. Điều này có thể hữu ích như một phương tiện cung cấp thông tin chi tiết hơn trong các tập tin đăng nhập, nhưng cũng có thể có tác động tiêu cực đến hiệu suất.

##### "allow_gethostbyaddr_lookup"
- Cho phép tra cứu gethostbyaddr khi UDP không khả dụng? True = Vâng [Mặc định]; False = Không.
- *Lưu ý: Tra cứu IPv6 có thể không hoạt động chính xác trên một số hệ thống 32-bit.*

##### "hide_version"
- Ẩn thông tin phiên bản từ nhật ký và đầu ra của trang? True = Vâng; False = Không [Mặc định].

##### "empty_fields"
- CIDRAM nên xử lý các trường trống khi ghi và hiển thị thông tin sự kiện khối như thế nào? "include" = Bao gồm các trường trống. "omit" = Bỏ sót các trường trống [mặc định].

##### "log_sanitisation"
- Khi sử dụng trang bản ghi để xem dữ liệu bản ghi, CIDRAM vệ sinh dữ liệu bản ghi trước khi hiển thị nó, để bảo vệ người dùng khỏi các cuộc tấn công XSS và các mối đe dọa tiềm năng khác. Tuy nhiên, theo mặc định, dữ liệu không được vệ sinh trong quá ghi bản ghi. Điều này là để đảm bảo dữ liệu bản ghi được bảo quản chính xác, để hỗ trợ bất kỳ phân tích heuristic hoặc pháp y có thể cần thiết trong tương lai. Tuy nhiên, nếu người dùng cố gắng đọc dữ liệu bản ghi bằng các công cụ bên ngoài, và nếu những công cụ bên ngoài đó không thực hiện quy trình vệ sinh riêng của họ, người dùng có thể tiếp xúc với các cuộc tấn công XSS. Nếu cần, bạn có thể thay đổi hành vi mặc định bằng cách sử dụng chỉ thị cấu hình này. True = Vệ sinh dữ liệu khi ghi nó (dữ liệu được bảo quản ít chính xác hơn, nhưng rủi ro XSS thấp hơn). False = Không vệ sinh dữ liệu khi ghi nó (dữ liệu được bảo quản chính xác hơn, nhưng rủi ro XSS cao hơn) [Mặc định].

##### "disabled_channels"
- Điều này có thể được sử dụng để ngăn CIDRAM sử dụng các kênh cụ thể khi gửi yêu cầu (ví dụ, khi cập nhật, khi lấy siêu dữ liệu thành phần, vv).
- *Tùy chọn có sẵn: `GitHub,BitBucket,GoogleDNS`*

##### "default_timeout"
- Thời gian chờ mặc định để sử dụng cho các yêu cầu bên ngoài? Mặc định = 12 giây.

##### "config_imports"
- Danh sách tập tin được phân tách bằng dấu phẩy để nhập vào cấu hình mặc định CIDRAM. Thường được nhập bởi trang cập nhật khi cần thiết khi các thành phần được kích hoạt. Trong hầu hết các trường hợp, có thể bỏ qua nó.

##### "events"
- Các tập tin được liệt kê ở đây được tải trực tiếp sau tập tin trình xử lý sự kiện. Thường được nhập bởi trang cập nhật khi cần thiết khi các thành phần được kích hoạt. Trong hầu hết các trường hợp, có thể bỏ qua nó.

#### "signatures" (Thể loại)
Cấu hình cho chữ ký.

##### "ipv4"
- Một danh sách các tập tin chữ ký IPv4 mà CIDRAM nên cố gắng để phân tích, ngăn cách bởi dấu phẩy. Bạn có thể thêm các mục ở đây nếu bạn muốn bao gồm thêm các tập tin chữ ký IPv4 trong CIDRAM.

##### "ipv6"
- Một danh sách các tập tin chữ ký IPv6 mà CIDRAM nên cố gắng để phân tích, ngăn cách bởi dấu phẩy. Bạn có thể thêm các mục ở đây nếu bạn muốn bao gồm thêm các tập tin chữ ký IPv6 trong CIDRAM.

##### "block_attacks"
- Chặn CIDR liên quan đến các cuộc tấn công và lưu lượng truy cập bất thường khác? Ví dụ, quét cổng, tấn công, dò tìm lỗ hổng bảo mật, vv. Trừ khi bạn gặp vấn đề khi làm như vậy, nói chung, điều này cần phải luôn được true.

##### "block_cloud"
- Chặn CIDR xác định là thuộc về các dịch vụ lưu trữ mạng hay dịch vụ điện toán đám mây? Nếu bạn điều hành một dịch vụ API từ trang mạng của bạn hay nếu bạn mong đợi các trang mạng khác để kết nối với trang mạng của bạn, điều này cần được thiết lập để false. Nếu bạn không, sau đó, tùy chọn này cần được thiết lập để true.

##### "block_bogons"
- Chặn CIDR bogon/martian? Nếu bạn mong đợi các kết nối đến trang mạng của bạn từ bên trong mạng nội bộ của bạn, từ localhost, hay từ LAN của bạn, tùy chọn này cần được thiết lập để false. Nếu bạn không mong đợi những kết nối như vậy, tùy chọn này cần được thiết lập để true.

##### "block_generic"
- Chặn CIDR thường được khuyến cáo cho danh sách đen? Điều này bao gồm bất kỳ chữ ký không được đánh dấu như một phần của bất kỳ các loại chữ ký cụ thể khác.

##### "block_legal"
- Chặn CIDR theo các nghĩa vụ hợp pháp? Chỉ thị này thường không có bất kỳ hiệu lực, vì CIDRAM không liên kết bất kỳ CIDR nào với "nghĩa vụ hợp pháp" theo mặc định, nhưng nó vẫn tồn tại tuy nhiên như một biện pháp kiểm soát bổ sung vì lợi ích của bất kỳ tập tin chữ ký hay mô-đun tùy chỉnh nào có thể tồn tại vì lý do hợp pháp.

##### "block_malware"
- Chặn CIDR liên quan đến phần mềm độc hại? Điều này bao gồm các máy chủ C&C, máy chủ bị nhiễm, máy chủ liên quan đến phân phối phần mềm độc hại, vv.

##### "block_proxies"
- Chặn CIDR xác định là thuộc về các dịch vụ proxy hay VPN? Nếu bạn yêu cầu mà người dùng có thể truy cập trang mạng của bạn từ các dịch vụ proxy hay VPN, điều này cần được thiết lập để false. Nếu không thì, nếu bạn không yêu cầu các dịch vụ proxy hay VPN, tùy chọn này cần được thiết lập để true như một phương tiện để cải thiện an ninh.

##### "block_spam"
- Chặn CIDR xác định như có nguy cơ cao đối được thư rác? Trừ khi bạn gặp vấn đề khi làm như vậy, nói chung, điều này cần phải luôn được true.

##### "modules"
- Một danh sách các tập tin mô-đun để tải sau khi kiểm tra các chữ ký IPv4/IPv6, ngăn cách bởi dấu phẩy.

##### "default_tracktime"
- Có bao nhiêu giây để giám sát các IP bị cấm bởi các mô-đun. Mặc định = 604800 (1 tuần).

##### "infraction_limit"
- Số lượng tối đa các vi phạm một IP được phép chịu trước khi nó bị cấm bởi các giám sát IP. Mặc định = 10.

##### "track_mode"
- Khi vi phạm cần được tính? False = Khi IP bị chặn bởi các mô-đun. True = Khi IP bị chặn vì lý do bất kỳ. Mặc định = False.

##### "tracking_override"
- Cho phép các mô-đun ghi đè các tùy chọn giám sát? True = Vâng [Mặc định]; False = Không.

#### "recaptcha" và "hcaptcha" (hai thể loại này cung cấp các chỉ thị giống nhau).
Nếu bạn muốn, bạn có thể giới thiệu cho người dùng một thử thách CAPTCHA để phân biệt họ với bot hoặc cho phép họ lấy lại quyền truy cập trong trường hợp bị chặn. Điều này có thể giúp giảm sai tích cực và giảm lưu lượng truy cập tự động không mong muốn.

*Lưu ý: CAPTCHA chỉ bảo vệ chống lại các cuộc gọi của máy, không chống lại những kẻ tấn công con người.*

Bạn có thể lấy "site key" và "secret key" cho reCAPTCHA từ đây:
- https://developers.google.com/recaptcha/

Bạn có thể lấy "site key" và "secret key" cho hCAPTCHA từ đây:
- https://www.hcaptcha.com/

##### "usemode"
- Khi nào nên cung cấp CAPTCHA? Lưu ý: Các yêu cầu trong danh sách trắng hay đã xác minh và không bị chặn không cần phải hoàn thành CAPTCHA.

Giá trị | Chi tiết
--:|:--
1 | Chỉ khi bị chặn, trong giới hạn chữ ký, và không bị cấm.
2 | Chỉ khi bị chặn, được đánh dấu đặc biệt để sử dụng, trong giới hạn chữ ký, và không bị cấm.
3 | Chỉ khi trong giới hạn chữ ký, và không bị cấm (bất kể có bị chặn hay không).
4 | Chỉ khi không bị chặn.
5 | Chỉ khi không bị chặn, hoặc khi được đánh dấu đặc biệt để sử dụng, trong giới hạn chữ ký, và không bị cấm.
Bất kỳ giá trị nào khác. | Không bao giờ!

##### "lockip"
- Chỉ định liệu các băm/hash nên được khóa trên IP cụ thể. False = Cookie và băm/hash CÓ THỂ được sử dụng bởi nhiều IP (mặc định). True = Cookie và băm/hash KHÔNG THỂ được sử dụng sử dụng bởi nhiều IP (cookie và băm/hash được khóa trên các IP).
- Chú thích: Giá trị "lockip" được bỏ qua khi "lockuser" là false, bởi vì các cơ chế để nhớ "người dùng" khác nhau ơ tùy thuộc vào giá trị này.

##### "lockuser"
- Chỉ định liệu thành công hoàn thành của reCAPTCHA/hCAPTCHA nên được khóa trên người dùng cụ thể. False = Thành công hoàn thành của reCAPTCHA/hCAPTCHA sẽ cấp quyền truy cập cho tất cả các yêu cầu có nguồn gốc từ cùng một IP như được sử dụng bởi người dùng mà hoàn thành reCAPTCHA/hCAPTCHA; Cookie và băm/hash không được sử dụng; Thay vào đó, một danh sách trắng IP sẽ được sử dụng. True = Thành công hoàn thành của reCAPTCHA/hCAPTCHA sẽ chỉ cấp quyền truy cập cho người dùng mà hoàn thành reCAPTCHA/hCAPTCHA; Cookie và băm/hash được sử dụng để nhớ người dùng; Một danh sách trắng IP sẽ không được sử dụng (mặc định).

##### "sitekey"
- Giá trị này có thể được tìm thấy trong bảng điều khiển cho dịch vụ CAPTCHA của bạn.

##### "secret"
- Giá trị này có thể được tìm thấy trong bảng điều khiển cho dịch vụ CAPTCHA của bạn.

##### "expiry"
- Số giờ để nhớ CAPTCHA. Mặc định = 720 (1 tháng).

##### "logfile"
- Đăng nhập tất cả các nỗ lực cho CAPTCHA? Nếu có, ghi rõ tên để sử dụng cho các tập tin đăng nhập. Nếu không, đốn biến này.

*Mẹo hữu ích: Nếu bạn muốn, bạn có thể thêm thông tin ngày/giờ trong tên các tập tin ghi của bạn bằng cách bao gồm những trong tên: `{yyyy}` cho năm đầy, `{yy}` cho năm viết tắt, `{mm}` cho tháng, `{dd}` cho ngày, `{hh}` cho giờ.*

*Các ví dụ:*
- *`logfile='captcha.{yyyy}-{mm}-{dd}-{hh}.txt'`*

##### "signature_limit"
- Số lượng chữ ký tối đa được phép trước khi đề nghị CAPTCHA bị rút lại. Mặc định = 1.

##### "api"
- API nào để sử dụng?

```
api
├─recaptcha
│ ├─V2
│ └─Invisible
└─hcaptcha
  ├─V1
  └─Invisible
```

*Lưu ý đối với người dùng ở Liên minh châu Âu: Khi CIDRAM được định cấu hình để sử dụng cookie (v.d., khi "lockuser" là true/đúng), cảnh báo cookie được hiển thị trên trang theo quy định của [pháp luật về cookie của EU](https://www.cookielaw.org/the-cookie-law/). Tuy nhiên, khi sử dụng API invisible, CIDRAM cố gắng hoàn thành CAPTCHA cho người dùng tự động, và khi thành công, điều này có thể dẫn đến việc trang được tải lại và một cookie được tạo ra mà không có người dùng được cho đủ thời gian để thực sự xem cảnh báo cookie.*

##### "show_cookie_warning"
- Hiển thị cảnh báo cookie? True = Vâng [Mặc định]; False = Không.

*Chỉ thị cấu hình này được thêm theo yêu cầu, cho người dùng muốn tắt cảnh báo cookie thường được hiển thị cùng với CAPTCHA (để giúp, ví dụ, ẩn bất kỳ dấu hiệu nào cho thấy CIDRAM đang được sử dụng). Tuy nhiên, tôi thực sự khuyên rằng hầu hết người dùng (đặc biệt là những người ở EU) nên giữ nó bật.*

##### "show_api_message"
- Hiển thị thông báo API? True = Vâng [Mặc định]; False = Không.

*Điều này đề cập đến bất kỳ thông báo bổ sung, không cần thiết được hiển thị khi một yêu cầu bị chặn, ngoại trừ cảnh báo cookie.*

##### "nonblocked_status_code"
- Mã trạng thái nào nên được sử dụng khi hiển thị CAPTCHA cho các yêu cầu không bị chặn?

Giá trị hiện được hỗ trợ:

Mã trạng thái | Thông thái trạng thái
---|---
`200` | `200 OK`
`403` | `403 Forbidden`
`418` | `418 I'm a teapot`
`429` | `429 Too Many Requests`
`451` | `451 Unavailable For Legal Reasons`

#### "legal" (Thể loại)
Cấu hình mà liên quan đến các nghĩa vụ hợp pháp.

*Để biết thêm thông tin về các nghĩa vụ hợp pháp và cách nó có thể ảnh hưởng đến các nghĩa vụ cấu hình của bạn, vui lòng tham khảo phần "[THÔNG TIN HỢP PHÁP](#user-content-SECTION11)" của các tài liệu.*

##### "pseudonymise_ip_addresses"
- Pseudonymise địa chỉ IP khi viết các tập tin nhật ký? True = Vâng [Mặc định]; False = Không.

##### "omit_ip"
- Bỏ qua địa chỉ IP từ nhật ký? True = Vâng; False = Không [Mặc định]. Lưu ý: "pseudonymise_ip_addresses" trở nên dư thừa khi "omit_ip" là "true".

##### "omit_hostname"
- Bỏ qua tên máy chủ từ nhật ký? True = Vâng; False = Không [Mặc định].

##### "omit_ua"
- Bỏ qua đại lý người dùng từ nhật ký? True = Vâng; False = Không [Mặc định].

##### "privacy_policy"
- Địa chỉ của chính sách bảo mật liên quan được hiển thị ở chân trang của bất kỳ trang nào được tạo. Chỉ định URL, hoặc để trống để vô hiệu hóa.

#### "template_data" (Thể loại)
Cấu hình cho mẫu thiết kế và chủ đề.

Liên quan đến đầu ra HTML sử dụng để tạo ra các trang "Truy cập đã bị từ chối". Nếu bạn đang sử dụng chủ đề tùy chỉnh cho CIDRAM, đầu ra HTML có nguồn gốc từ tập tin `template_custom.html`, và nếu không thì, đầu ra HTML có nguồn gốc từ tập tin `template.html`. Biến bằng văn bản cho phần này của tập tin cấu hình được xử lý để đầu ra HTML bằng cách thay thế bất kỳ tên biến được bao quanh bởi các dấu ngoặc nhọn tìm thấy trong đầu ra HTML với các dữ liệu biến tương ứng. Ví dụ, ở đâu `foo="bar"`, bất kỳ trường hợp `<p>{foo}</p>` tìm thấy trong đầu ra HTML sẽ trở thành `<p>bar</p>`.

##### "theme"
- Chủ đề mặc định để sử dụng cho CIDRAM.

##### "magnification"
- *v1: "Magnification"*
- Phóng to chữ. Mặc định = 1.

##### "css_url"
- Tập tin mẫu thiết kế cho chủ đề tùy chỉnh sử dụng thuộc tính CSS bên ngoài, trong khi các tập tin mẫu thiết kế cho các chủ đề mặc định sử dụng thuộc tính CSS nội bộ. Để hướng dẫn CIDRAM để sử dụng các tập tin mẫu thiết kế cho chủ đề tùy chỉnh, xác định các địa chỉ HTTP cho các tập tin CSS chủ đề tùy chỉnh của bạn sử dụng các biến số `css_url`. Nếu bạn để cho biến số này chỗ trống, CIDRAM sẽ sử dụng các tập tin mẫu thiết kế cho các chủ đề mặc định.

#### "PHPMailer" (Thể loại)
Cấu hình PHPMailer.

Hiện tại, CIDRAM chỉ sử dụng PHPMailer để xác thực hai yếu tố front-end. Nếu bạn không sử dụng các front-end, hoặc nếu bạn không sử dụng xác thực hai yếu tố cho các front-end, bạn có thể bỏ qua các chỉ thị này.

##### "event_log"
- *v1: "EventLog"*
- Một tập tin để ghi nhật ký tất cả các sự kiện liên quan đến PHPMailer. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

##### "skip_auth_process"
- *v1: "SkipAuthProcess"*
- Đặt chỉ thị này thành `true` chỉ thị cho PHPMailer bỏ qua quy trình xác thực thông thường thường xảy ra khi gửi email qua SMTP. Điều này nên tránh, bởi vì bỏ qua quá trình này có thể tiết lộ email gửi đến các cuộc tấn công MITM, nhưng có thể cần thiết trong trường hợp quá trình này ngăn PHPMailer kết nối với máy chủ SMTP.

##### "enable_two_factor"
- *v1: "Enable2FA"*
- Chỉ thị này xác định có nên sử dụng 2FA cho tài khoản front-end hay không.

##### "host"
- *v1: "Host"*
- Máy chủ SMTP để sử dụng cho email gửi đi.

##### "port"
- *v1: "Port"*
- Số cổng để sử dụng cho email gửi đi. Mặc định = 587.

##### "smtp_secure"
- *v1: "SMTPSecure"*
- Giao thức sử dụng khi gửi email qua SMTP (TLS hoặc SSL).

##### "smtp_auth"
- *v1: "SMTPAuth"*
- Chỉ thị này xác định xem có nên xác thực các phiên SMTP (thường nên để lại một mình).

##### "username"
- *v1: "Username"*
- Tên người dùng để sử dụng khi gửi email qua SMTP.

##### "password"
- *v1: "Password"*
- Mật khẩu để sử dụng khi gửi email qua SMTP.

##### "set_from_address"
- *v1: "setFromAddress"*
- Địa chỉ người gửi để trích dẫn khi gửi email qua SMTP.

##### "set_from_name"
- *v1: "setFromName"*
- Tên người gửi để trích dẫn khi gửi email qua SMTP.

##### "add_reply_to_address"
- *v1: "addReplyToAddress"*
- Địa chỉ trả lời để trích dẫn khi gửi email qua SMTP.

##### "add_reply_to_name"
- *v1: "addReplyToName"*
- Tên trả lời để trích dẫn khi gửi email qua SMTP.

#### "rate_limiting" (Thể loại)
Các chỉ thị cấu hình tùy chọn để giới hạn tốc độ.

Tính năng này được thực hiện cho CIDRAM bởi vì nó được yêu cầu bởi đủ người dùng để biện minh cho việc thực hiện. Tuy nhiên, bởi vì nó không liên quan đến mục đích dự định ban đầu cho CIDRAM, rất có thể sẽ không cần thiết cho hầu hết người dùng. Nếu bạn đặc biệt cần CIDRAM để xử lý giới hạn tốc độ cho trang web của mình, tính năng này có thể hữu ích cho bạn. Tuy nhiên, có một số điều quan trọng bạn nên cân nhắc:
- Tính năng này, giống như tất cả các tính năng CIDRAM khác, sẽ chỉ hoạt động đối với các trang được bảo vệ bởi CIDRAM. Do đó, bất kỳ tài sản trang web nào không được định tuyến cụ thể thông qua CIDRAM không thể bị giới hạn bởi CIDRAM.
- Nếu bạn có thể sử dụng mô-đun máy chủ, cPanel, hoặc một số công cụ mạng khác để thực thi giới hạn tốc độ, nó sẽ là tốt hơn để sử dụng mà thay vì CIDRAM.
- Nếu một người dùng cụ thể rất muốn tiếp tục truy cập trang web của bạn sau khi bị giới hạn, trong hầu hết các trường hợp, sẽ rất dễ dàng để họ vượt qua giới hạn tốc độ (v.d., nếu họ thay đổi địa chỉ IP của họ, hoặc nếu họ sử dụng proxy hoặc VPN, và giả định rằng bạn đã định cấu hình CIDRAM để không chặn proxy và VPN, hoặc CIDRAM đó không biết về proxy hoặc VPN mà họ đang sử dụng).
- Giới hạn tốc độ có thể rất khó chịu đối với người dùng cuối thực tế. Có thể cần thiết nếu băng thông có sẵn của bạn rất hạn chế, và nếu bạn phát hiện ra rằng có một số nguồn lưu lượng truy cập cụ thể, chưa bị chặn, điều đó sẽ tiêu tốn phần lớn băng thông có sẵn của bạn. Nếu không cần thiết tuy nhiên, nó có lẽ nên tránh.
- Đôi khi, bạn có thể có nguy cơ chặn người dùng hợp pháp, hay thậm chí là chính bạn.

Nếu bạn cảm thấy rằng bạn không cần CIDRAM để thực thi giới hạn tốc độ cho trang web của bạn, giữ các chỉ thị bên dưới được đặt làm giá trị mặc định của chúng. Nếu không, bạn có thể thay đổi giá trị của chúng cho phù hợp với nhu cầu của bạn.

##### "max_bandwidth"
- Số lượng băng thông tối đa được phép trong khoảng thời gian cho phép trước khi cho phép giới hạn tốc độ cho các yêu cầu trong tương lai. Giá trị 0 sẽ vô hiệu hóa loại giới hạn tốc độ này. Mặc định = 0KB.

##### "max_requests"
- Số lượng yêu cầu tối đa được phép trong khoảng thời gian cho phép trước khi cho phép giới hạn tốc độ cho các yêu cầu trong tương lai. Giá trị 0 sẽ vô hiệu hóa loại giới hạn tốc độ này. Mặc định = 0.

##### "precision_ipv4"
- Độ chính xác để sử dụng khi theo dõi việc sử dụng IPv4. Giá trị phản ánh kích thước khối CIDR. Đặt thành 32 để có độ chính xác cao nhất. Mặc định = 32.

##### "precision_ipv6"
- Độ chính xác để sử dụng khi theo dõi việc sử dụng IPv6. Giá trị phản ánh kích thước khối CIDR. Đặt thành 128 để có độ chính xác cao nhất. Mặc định = 128.

##### "allowance_period"
- Số giờ để theo dõi việc sử dụng. Mặc định = 0.

##### "exceptions"
- Ngoại lệ (tức là, các yêu cầu không nên giới hạn). Chỉ có hiệu lực khi giới hạn tốc độ được kích hoạt.
- *Tùy chọn có sẵn: `Whitelisted,Verified`*

#### "supplementary_cache_options" (Thể loại)
Tùy chọn bộ nhớ cache bổ sung.

##### "prefix"
- Giá trị được chỉ định ở đây sẽ được thêm vào trước tất cả các khóa mục nhập bộ nhớ cache. Trống theo mặc định. Khi nhiều bản cài đặt tồn tại trên cùng một máy chủ, điều này có thể hữu ích để giữ các bộ nhớ cache của chúng tách biệt với nhau.

##### "enable_apcu"
- Điều này xác định có nên thử sử dụng APCu để lưu trữ không. Mặc định = False.

##### "enable_memcached"
- Điều này xác định có nên thử sử dụng Memcached để lưu trữ không. Mặc định = False.

##### "enable_redis"
- Điều này xác định có nên thử sử dụng Redis để lưu trữ không. Mặc định = False.

##### "enable_pdo"
- Điều này xác định có nên thử sử dụng PDO để lưu trữ không. Mặc định = False.

##### "memcached_host"
- Giá trị máy chủ Memcached. Mặc định = "localhost".

##### "memcached_port"
- Giá trị cổng Memcached. Mặc định = "11211".

##### "redis_host"
- Giá trị máy chủ Redis. Mặc định = "localhost".

##### "redis_port"
- Giá trị cổng Redis. Mặc định = "6379".

##### "redis_timeout"
- Giá trị thời gian chờ Redis. Mặc định = "2.5".

##### "pdo_dsn"
- Giá trị DSN PDO. Mặc định = "`mysql:dbname=cidram;host=localhost;port=3306`".

*Xem thêm: ["PDO DSN" là gì? Làm cách nào tôi có thể sử dụng PDO với CIDRAM?](#user-content-HOW_TO_USE_PDO)*

##### "pdo_username"
- Tên người dùng PDO.

##### "pdo_password"
- Mật khẩu PDO.

---


### 7. <a name="SECTION7"></a>ĐỊNH DẠNG CỦA CHỬ KÝ

*Xem thêm:*
- *["Chữ ký" là gì?](#user-content-WHAT_IS_A_SIGNATURE)*

#### 7.0 KHÁI NIỆM CƠ BẢN (ĐỐI VỚI TẬP TIN CHỮ KÝ)

Tất cả các chữ ký IPv4 theo định dạng: `xxx.xxx.xxx.xxx/yy [Function] [Param]`.
- `xxx.xxx.xxx.xxx` đại diện cho sự khởi đầu của khối CIDR (octet của địa chỉ IP đầu tiên trong khối).
- `yy` đại diện cho kích thước khối CIDR [1-32].
- `[Function]` chỉ thị các kịch bản những gì để làm với các chữ ký (các cách chữ ký phải được coi).
- `[Param]` đại diện cho bất cứ điều gì thêm thông tin có thể được yêu cầu bởi `[Function]`.

Tất cả các chữ ký IPv6 theo định dạng: `xxxx:xxxx:xxxx:xxxx::xxxx/yy [Function] [Param]`.
- `xxxx:xxxx:xxxx:xxxx::xxxx` đại diện cho sự khởi đầu của khối CIDR (octet của địa chỉ IP đầu tiên trong khối). Ký hiệu hoàn chỉnh và ký hiệu viết tắt cả hai đều chấp nhận được (và mỗi PHẢI tuân theo các tiêu chuẩn phù hợp và liên quan của ký hiệu IPv6, nhưng với một ngoại lệ: một địa chỉ IPv6 không bao giờ có thể bắt đầu với một chữ viết tắt khi được sử dụng trong một chữ ký cho kịch bản này, bởi vì cách thức mà CIDR được xây dựng lại bởi các kịch bản; Ví dụ, `::1/128` nên được bày tỏ, khi được sử dụng trong một chữ ký, như `0::1/128`, và `::0/128` bày tỏ như `0::/128`).
- `yy` đại diện cho kích thước khối CIDR [1-128].
- `[Function]` chỉ thị các kịch bản những gì để làm với các chữ ký (các cách chữ ký phải được coi).
- `[Param]` đại diện cho bất cứ điều gì thêm thông tin có thể được yêu cầu bởi `[Function]`.

Các tập tin chữ ký cho CIDRAM NÊN sử dụng ngắt dòng trong phong cách Unix (`%0A`, hay `\n`)! Các loại / phong cách khác của ngắt dòng (ví dụ, Windows `%0D%0A` hay `\r\n`, Mac `%0D` hay `\r`, vv) CÓ THỂ được sử dụng, nhưng là KHÔNG ưa thích. Ngắt dòng không trong phong cách của Unix sẽ được bình thường như ngắt dòng trong phong cách của Unix bằng cách các kịch bản.

CIDR ký hiệu tóm lược và chính xác là cần thiết, nếu không thì các kịch bản sẽ KHÔNG công nhận các chữ ký. Ngoài ra, tất cả các chữ ký CIDR của kịch bản này PHẢI bắt đầu với một địa chỉ IP số IP có thể phân chia đồng đều vào việc phân chia khối đại diện bởi kích thước khối CIDR của nó (ví dụ, nếu bạn muốn chặn tất cả các IP từ `10.128.0.0` đến `11.127.255.255`, `10.128.0.0/8` sẽ KHÔNG được công nhận bởi các kịch bản, nhưng `10.128.0.0/9` và `11.0.0.0/9` sử dụng kết hợp, SẼ được công nhận bởi các kịch bản).

Bất cứ điều gì trong các tập tin chữ ký không được công nhận như một chữ ký cũng không phải như cú pháp chữ ký liên quan bằng cách của các kịch bản sẽ được BỎ QUA, do đó có nghĩa là bạn có thể an toàn đặt bất kỳ dữ liệu không chữ ký mà bạn muốn vào các tập tin chữ ký mà không phá vỡ chúng và mà không vi phạm các kịch bản. Ý kiến được chấp nhận trong các tập tin chữ ký, và không có định dạng đặc biệt được yêu cầu cho chúng. Shell kiểu băm cho ý kiến được ưa thích, nhưng không được thực thi; Chức năng, nó làm cho không có sự khác biệt với các kịch bản hay không bạn chọn để sử dụng băm Shell kiểu băm cho ý kiến, nhưng sử dụng băm Shell kiểu băm sẽ giúp IDE và biên tập văn bản đơn giản để làm nổi bật một cách chính xác các bộ phận khác nhau của các tập tin chữ ký (và như vậy, Shell kiểu băm có thể hỗ trợ như một trợ thị giác trong khi chỉnh sửa).

Các giá trị có thể có của `[Function]` như sau:
- Run
- Whitelist
- Greylist
- Deny

Nếu "Run" được sử dụng, khi chữ ký được kích hoạt, các kịch bản sẽ cố gắng thực hiện (sử dụng một statement / tuyên bố `require_once`) một kịch bản PHP bên ngoài, xác định bởi các giá trị `[Param]` (thư mục làm việc nên là thư mục "/vault/" của các kịch bản).

Ví dụ: `127.0.0.0/8 Run example.php`

Điều này có thể hữu ích nếu bạn muốn để thực hiện một số mã PHP cụ thể cho một số IP hay CIDR cụ thể.

Nếu "Whitelist" được sử dụng, khi chữ ký được kích hoạt, các kịch bản sẽ thiết lập lại tất cả các phát hiện (nếu có bất kỳ phát hiện đã) và phá vỡ các chức năng kiểm tra. `[Param]` bị bỏ qua. Chức năng này là tương đương với danh sách trắng một IP hay CIDR cụ thể chống bị phát hiện.

Ví dụ: `127.0.0.1/32 Whitelist`

Nếu "Greylist" được sử dụng, khi chữ ký được kích hoạt, các kịch bản sẽ thiết lập lại tất cả các phát hiện (nếu có bất kỳ phát hiện đã) và tiến hành đến các tập tin chữ ký tiếp theo để tiếp tục xử lý. `[Param]` bị bỏ qua.

Ví dụ: `127.0.0.1/32 Greylist`

Nếu "Deny" được sử dụng, khi chữ ký được kích hoạt, giả sử không có chữ ký danh sách trắng đã được kích hoạt cho các địa chỉ IP hay CIDR thích hợp, truy cập vào các trang được bảo vệ sẽ bị từ chối. "Deny" là những gì bạn sẽ muốn sử dụng để thực sự ngăn chặn một địa chỉ IP hay phạm vi CIDR. Khi bất kỳ chữ ký được kích hoạt đó làm cho sử dụng của "Deny", trang "Truy cập đã bị từ chối" của các kịch bản sẽ được tạo ra và các yêu cầu đến trang bảo vệ sẽ bị giết.

Giá trị `[Param]` chấp nhận bởi "Deny" sẽ được phân tích để đầu ra trang "Truy cập đã bị từ chối", cung cấp cho các khách hàng / người dùng như các lý do được trích dẫn cho truy cập của họ vào trang yêu cầu được bị từ chối. Nó có thể là một câu ngắn và đơn giản, giải thích lý do tại sao bạn đã chọn để ngăn chặn chúng (bất cứ điều gì là đủ, cái gì đó như "Tôi không muốn bạn trên trang mạng của tôi" sẽ đủ), hay một trong một số ít các từ viết tắt được cung cấp bởi các kịch bản, mà nếu được sử dụng, sẽ được thay thế bởi các kịch bản với một lời giải thích chuẩn bị trước lý do tại sao khách hàng / người dùng đã bị chặn.

Những lời giải thích trước khi chuẩn bị có hỗ trợ L10N và có thể được dịch bởi kịch bản dựa trên ngôn ngữ mà bạn chỉ định đến tùy chọn `lang` của các cấu hình kịch bản. Ngoài ra, bạn có thể hướng dẫn các kịch bản để bỏ qua chữ ký "Deny" dựa trên giá trị `[Param]` của họ (nếu họ đang sử dụng những từ viết tắt) thông qua các tùy chọn định bởi cấu hình kịch bản (mỗi từ viết tắt có một tùy chọn tương ứng để xử lý chữ ký tương ứng hoặc bỏ qua chúng). Các giá trị `[Param]` mà không sử dụng những từ viết tắt, tuy nhiên, không có hỗ trợ L10N và do đó KHÔNG SẼ được dịch bởi kịch bản, và do đó, không thể được kiểm soát trực tiếp bởi các cấu hình kịch bản.

Những từ viết tắt có sẵn là:
- Attacks
- Bogon
- Cloud
- Generic
- Legal
- Malware
- Proxy
- Spam

#### 7.1 GẮN THẺ

##### 7.1.0 GẮN THẺ PHẦN

Nếu bạn muốn chia chữ ký tùy chỉnh của bạn để các phần riêng biệt, bạn có thể xác định những phần riêng lẻ cho các kịch bản bằng cách thêm một "gắn thẻ phần" ngay sau khi có chữ ký của từng phần, với tên của phần chữ ký của bạn (xem ví dụ dưới đây).

```
# Phần 1.
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud
4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
6.7.8.9/32 Deny Proxy
Tag: Phần 1
```

Để phá vỡ gắn thẻ phần và để đảm bảo rằng các gắn thẻ không được xác định không đúng để phần chữ ký từ trước đó trong các tập tin chữ ký, chỉ cần đảm bảo rằng có ít nhất hai ngắt dòng liên tiếp giữa các gắn thẻ và phần chữ ký trước đó của bạn. Bất kỳ chữ ký không được gắn thẻ sẽ mặc định để "IPv4" hoặc "IPv6" (tùy thuộc vào loại chữ ký đang được kích hoạt).

```
1.2.3.4/32 Deny Bogon
2.3.4.5/32 Deny Cloud

4.5.6.7/32 Deny Generic
5.6.7.8/32 Deny Spam
Tag: Phần 1
```

Trong ví dụ trên `1.2.3.4/32` và `2.3.4.5/32` sẽ được xác định như "IPv4", trong khi `4.5.6.7/32` và `5.6.7.8/32` sẽ được xác định như "Phần 1".

Tương tự logic có thể được áp dụng để tách thẻ loại khác.

Gắn thẻ phần có thể rất hữu ích cho lọc lỗi khi xảy ra sai tích cực, bằng cách cung cấp một phương tiện dễ dàng để tìm ra chính xác nguồn gốc của vấn đề, và có thể rất hữu ích cho lọc các mục nhập tập tin bản ghi khi xem tập tin bản ghi qua trang bản ghi của front-end (tên phần có thể nhấp qua trang bản ghi của front-end và có thể được sử dụng làm tiêu chí lọc). Nếu gắn thẻ phần bị bỏ qua đối với một số chữ ký cụ thể, khi những chữ ký được kích hoạt, CIDRAM sử dụng tên của tập tin chữ ký cùng với loại địa chỉ IP bị chặn (IPv4 hoặc IPv6) như là một dự phòng, và do đó, các gắn thẻ phần là hoàn toàn tùy chọn. Chúng có thể được khuyên dùng trong một số trường hợp, chẳng hạn như khi tập tin chữ ký được đặt tên mơ hồ hoặc nếu không thì khó xác định được nguồn gốc của chữ ký gây ra yêu cầu bị chặn.

##### 7.1.1 GẮN THẺ HẾT HẠN

Nếu bạn muốn chữ ký hết hạn sau một thời gian, trong một cách tương tự như gắn thẻ phần, bạn có thể sử dụng một "gắn thẻ hết hạn" để chỉ định khi chữ ký nên hết hiệu lực. Gắn thẻ hết hạn sử dụng định dạng "YYYY.MM.DD" (xem ví dụ dưới đây).

```
# Phần 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

Chữ ký hết hạn sẽ không bao giờ được kích hoạt trên bất kỳ yêu cầu, không có vấn đề gì.

##### 7.1.2 GẮN THẺ XUẤT XỨ

Nếu bạn muốn chỉ định quốc gia xuất xứ cho một số chữ ký cụ thể, bạn có thể làm như vậy bằng cách sử dụng một "gắn thẻ xuất xứ". Gắn thẻ xuất xứ chấp nhận một mã "[ISO 3166-1 Alpha-2](https://vi.wikipedia.org/wiki/ISO_3166-1_alpha-2)" tương ứng với quốc gia xuất xứ cho các chữ ký mà nó áp dụng. Các mã này phải được viết bằng chữ hoa (trường hợp thấp hoặc trường hợp hỗn hợp sẽ không hiển thị chính xác). Khi một gắn thẻ xuất xứ được sử dụng, nó được thêm vào mục nhập bản ghi "Tại sao bị chặn" cho bất kỳ yêu cầu bị chặn như là kết quả của chữ ký mà gắn thẻ được áp dụng.

Nếu cài đặt thành phần "flags CSS", khi xem các tập tin bản ghi qua trang bản ghi, thông tin được bổ sung bởi gắn thẻ xuất xứ sẽ được thay thế bằng cờ quốc gia tương ứng với thông tin đó. Thông tin này, dù ở dạng thô hoặc quốc kỳ, có thể nhấp được, và khi được nhấp, sẽ lọc các mục nhập bản ghi bằng cách các mục nhập bản ghi khác tương tự (do đó có hiệu quả cho phép các trang bản ghi để lọc theo cách của quốc gia xuất xứ).

Chú thích: Về mặt kỹ thuật, đây không phải là bất kỳ dạng geolocation, bởi vì nó không liên quan đến việc tìm nạp bất kỳ thông tin vị trí cụ thể liên quan đến IP, mà đúng hơn, nó chỉ đơn giản cho phép chúng ta xác định rõ ràng một quốc gia xuất xứ cho bất kỳ yêu cầu bị chặn bởi chữ ký cụ thể. Nhiều gắn thẻ xuất xứ được cho phép trong cùng một phần chữ ký.

Ví dụ giả thuyết:

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

Bất kỳ thẻ có thể được sử dụng kết hợp, và tất cả các thẻ là tùy chọn (xem ví dụ dưới đây).

```
# Phần Ví Dụ.
1.2.3.4/32 Deny Generic
Origin: US
Tag: Phần Ví Dụ
Expires: 2016.12.31
```

##### 7.1.3 GẮN THẺ TRÌ HOÃN

Khi số lượng lớn các tập tin chữ ký được cài đặt và sử dụng, cài đặt có thể trở nên khá phức tạp, và có thể có một số chữ ký chồng lên nhau. Trong những trường hợp này, để ngăn chặn nhiều chữ ký chồng chéo được kích hoạt trong các sự kiện khối, gắn thẻ trì hoãn có thể được sử dụng để trì hoãn các phần chữ ký cụ thể trong trường hợp một số tập tin chữ ký cụ thể khác được cài đặt và sử dụng. Điều này có thể hữu ích trong trường hợp một số chữ ký được cập nhật thường xuyên hơn các chữ ký khác, để trì hoãn các chữ ký ít được cập nhật thường xuyên hơn với các chữ ký được cập nhật thường xuyên hơn.

Gắn thẻ trì hoãn được sử dụng tương tự như các loại thẻ khác. Giá trị của thẻ phải khớp với tập tin chữ ký được cài đặt và sử dụng để bị trì hoãn.

Ví dụ:

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 7.1.4 GẮN THẺ HỒ SƠ

Gắn thẻ hồ sơ cung cấp một phương tiện hiển thị thông tin bổ sung tại trang kiểm tra IP, và có thể được tận dụng bởi các mô-đun và các quy tắc phụ trợ để có hành vi phức tạp hơn và việc ra quyết định được tinh chỉnh.

Gắn thẻ hồ sơ được sử dụng tương tự như các loại gắn thẻ khác. Các giá trị của gắn thẻ hồ sơ có thể được sử dụng như một điều kiện cho các mô-đun và các quy tắc phụ trợ. Gắn thẻ hồ sơ có thể cung cấp nhiều giá trị bằng cách tách các giá trị đó bằng dấu chấm phẩy. Người dùng cuối không bao giờ nhìn thấy các giá trị của gắn thẻ hồ sơ.

Ví dụ:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 7.2 YAML

##### 7.2.0 YAML CƠ BẢN

Một hình thức đơn giản của YAML có thể được sử dụng trong các tập tin chữ ký cho mục đích xác định các hành vi và các thiết lập cụ thể để phần chữ ký cá nhân. Điều này có thể hữu ích nếu bạn muốn giá trị của chỉ thị cấu hình của bạn để khác biệt trên cơ sở chữ ký cá nhân và phần chữ ký (ví dụ; nếu bạn muốn cung cấp một địa chỉ email cho vé hỗ trợ cho bất kỳ người dùng bị chặn bởi một chữ ký đặc biệt, nhưng không muốn cung cấp một địa chỉ email cho vé hỗ trợ cho người dùng bị chặn bởi bất kỳ chữ ký khác; nếu bạn muốn có một số chữ ký cụ thể để kích hoạt một chuyển hướng trang; nếu bạn muốn đánh dấu một phần chữ ký để sử dụng với reCAPTCHA/hCAPTCHA; nếu bạn muốn ghi lại cố gắng truy cập bị chặn vào các tập tin riêng biệt trên cơ sở chữ ký cá nhân hay phần chữ ký).

Sử dụng YAML trong các tập tin chữ ký là không bắt buộc (có nghĩa là, bạn có thể sử dụng nó nếu bạn muốn làm như vậy, nhưng bạn không cần phải làm như vậy), và có thể tận dụng nhiều nhất (nhưng không phải tất cả) tùy chọn cấu hình.

Lưu ý: YAML của CIDRAM là rất đơn giản và rất hạn chế; Nó được thiết kế để đáp ứng yêu cầu cụ thể để CIDRAM trong một cách mà có sự quen thuộc với YAML, nhưng không theo cũng không tuân thủ các thông số kỹ thuật chính thức (và do đó sẽ không cư xử theo cách tương tự như một số biến thể nơi khác, và có thể không thích hợp cho các dự án khác nơi khác).

Trong CIDRAM, phân khúc YAML được xác định để kịch bản bằng ba dấu gạch ngang ("---"), và chấm dứt cùng với phần chữ ký chứa của họ bởi hai ngắt dòng. Một phân khúc YAML điển hình trong phần chữ ký bao gồm ba dấu gạch ngang trên một dòng ngay sau khi danh sách các CIDRs và bất kỳ gắn thẻ, theo sau là một danh sách cặp khóa giá trị hai chiều (chiều đầu tiên, loại tùy chọn cấu hình; chiều thứ cấp, tùy chọn cấu hình) cho những tùy chọn cấu hình mà cần được sửa đổi (và những giá trị) bất cứ khi nào một chữ ký trong đó phần chữ ký được kích hoạt (xem các ví dụ dưới đây).

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

##### 7.2.1 LÀM THẾ NÀO ĐỂ "ĐẶC BIỆT ĐÁNH DẤU" PHẦN CHỮ KÝ ĐỂ SỬ DỤNG VỚI reCAPTCHA/hCAPTCHA

Khi "usemode" là 2 hoặc 5, để "đặc biệt đánh dấu" phần chữ ký để sử dụng với reCAPTCHA/hCAPTCHA, một mục được bao gồm trong phân khúc YAML cho rằng phần chữ ký (xem ví dụ dưới đây).

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

#### 7.3 PHỤ TRỢ

##### 7.3.0 BỎ QUA PHẦN CHỮ KÝ

Ngoài ra, nếu bạn muốn CIDRAM để hoàn toàn bỏ qua một số phần cụ thể trong bất kỳ tập tin chữ ký, bạn có thể sử dụng các tập tin `ignore.dat` để xác định những phần để bỏ qua. Trên một dòng mới, viết `Ignore`, theo sau là một không gian, theo sau là tên của phần mà bạn muốn CIDRAM để bỏ qua (xem ví dụ dưới đây).

```
Ignore Phần 1
```

Điều này cũng có thể đạt được bằng cách sử dụng giao diện được cung cấp bởi trang "danh sách phần" front-end của CIDRAM.

##### 7.3.1 QUY TẮC PHỤ TRỢ

Nếu bạn cảm thấy việc viết các tập tin chữ ký tùy chỉnh hoặc các mô-đun tùy chỉnh của riêng bạn quá phức tạp đối với bạn, một lựa chọn đơn giản hơn có thể là sử dụng giao diện được cung cấp bởi trang "quy tắc phụ trợ" front-end của CIDRAM. Bằng cách chọn các tùy chọn thích hợp và chỉ định chi tiết về các loại yêu cầu cụ thể, bạn có thể hướng dẫn CIDRAM cách trả lời các yêu cầu đó. Các "quy tắc phụ trợ" được thực hiện sau khi tất cả các tập tin chữ ký và mô-đun đã hoàn thành thực hiện.

#### 7.4 <a name="MODULE_BASICS"></a>KHÁI NIỆM CƠ BẢN (CHO MÔ-ĐUN)

Các mô-đun có thể được sử dụng để mở rộng chức năng của CIDRAM, thực hiện các tác vụ bổ sung hay xử lý logic bổ sung.

Bởi vì các mô-đun được viết như tập tin PHP, nếu bạn đã quen thuộc với mã nguồn CIDRAM, bạn có thể cấu trúc module của bạn tuy nhiên bạn muốn, và viết chữ ký mô-đun của bạn tuy nhiên bạn muốn (trong vòng suy luận những gì có thể với PHP).

*Lưu ý: Nếu bạn không cảm thấy thoải mái khi làm việc với mã PHP, bạn không nên viết mô-đun riêng của mình.*

Một số chức năng được cung cấp bởi CIDRAM cho các mô-đun để sử dụng, để làm cho việc viết mô-đun của bạn trở nên đơn giản và dễ dàng hơn. Thông tin về chức năng này được mô tả dưới đây.

#### 7.5 CHỨC NĂNG MÔ-ĐUN

##### 7.5.0 "$Trigger"

Chữ ký mô-đun thường được viết bằng `$Trigger`. Trong hầu hết các trường hợp, sự đóng này sẽ quan trọng hơn bất cứ thứ gì khác để viết mô-đun.

`$Trigger` chấp nhận 4 tham số: `$Condition`, `$ReasonShort`, `$ReasonLong` (không bắt buộc), và `$DefineOptions` (không bắt buộc).

Thực tế của `$Condition` được đánh giá, và nếu true/đúng, chữ ký là "kích hoạt". Nếu false/sai, chữ ký không phải là "kích hoạt". `$Condition` thường có chứa mã PHP để đánh giá một điều kiện nên làm yêu cầu bị chặn.

`$ReasonShort` được trích dẫn trong trường "Tại sao bị chặn" khi chữ ký được "kích hoạt".

`$ReasonLong` là một thông báo tùy chọn được hiển thị cho người dùng / khách hàng khi chúng bị chặn, để giải thích tại sao chúng bị chặn. Nó sử dụng thông báo "Truy cập đã bị từ chối" thông thường khi bị bỏ qua.

`$DefineOptions` là một mảng tùy chọn có chứa cặp khóa / giá trị, được sử dụng để xác định các tùy chọn cấu hình cụ thể cho trường hợp yêu cầu. Tùy chọn cấu hình sẽ được áp dụng khi chữ ký được "kích hoạt".

`$Trigger` trả về true/đúng khi chữ ký được "kích hoạt", và false/sai khi không.

Để sử dụng sự đóng này trong mô-đun của bạn, trước tiên hãy nhớ kế thừa nó từ phạm vi cha mẹ:
```PHP
$Trigger = $CIDRAM['Trigger'];
```

##### 7.5.1 "$Bypass"

Đường tránh chữ ký thường được viết bằng `$Bypass`.

`$Bypass` chấp nhận 3 tham số: `$Condition`, `$ReasonShort`, và `$DefineOptions` (không bắt buộc).

Thực tế của `$Condition` được đánh giá, và nếu true/đúng, đường tránh là "kích hoạt". Nếu false/sai, đường tránh không phải là "kích hoạt". `$Condition` thường có chứa mã PHP để đánh giá một điều kiện *không* nên làm yêu cầu bị chặn.

`$ReasonShort` được trích dẫn trong trường "Tại sao bị chặn" khi đường tránh được "kích hoạt".

`$DefineOptions` là một mảng tùy chọn có chứa cặp khóa / giá trị, được sử dụng để xác định các tùy chọn cấu hình cụ thể cho trường hợp yêu cầu. Tùy chọn cấu hình sẽ được áp dụng khi đường tránh được "kích hoạt".

`$Bypass` trả về true/đúng khi đường tránh được "kích hoạt", và false/sai khi không.

Để sử dụng sự đóng này trong mô-đun của bạn, trước tiên hãy nhớ kế thừa nó từ phạm vi cha mẹ:
```PHP
$Bypass = $CIDRAM['Bypass'];
```

##### 7.5.2 "$CIDRAM['DNS-Reverse']"

Điều này có thể được sử dụng để lấy tên máy chủ của một địa chỉ IP. Nếu bạn muốn tạo một mô-đun để chặn tên máy chủ, sự đóng này có thể hữu ích.

Ví dụ:
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

#### 7.6 BIẾN MÔ-ĐUN

Mô-đun thực hiện theo phạm vi riêng của chúng, và bất kỳ biến nào được xác định bởi mô-đun, sẽ không thể truy cập vào mô-đun khác, hoặc kịch bản cha mẹ, trừ khi chúng được lưu trữ trong mảng `$CIDRAM` (mọi thứ khác được làm sạch sau khi kết thúc thực hiện mô-đun).

Dưới đây là một số biến phổ biến có thể hữu ích cho mô-đun của bạn:

Biến | Chi tiết
----|----
`$CIDRAM['BlockInfo']['DateTime']` | Ngày hiện tại và thời gian.
`$CIDRAM['BlockInfo']['IPAddr']` | Địa chỉ IP cho yêu cầu hiện tại.
`$CIDRAM['BlockInfo']['ScriptIdent']` | Phiên bản kịch bản CIDRAM.
`$CIDRAM['BlockInfo']['Query']` | Truy vấn (query) cho yêu cầu hiện tại.
`$CIDRAM['BlockInfo']['Referrer']` | Người giới thiệu (referrer) cho yêu cầu hiện tại (nếu có).
`$CIDRAM['BlockInfo']['UA']` | Đại lý người dùng (user agent) cho yêu cầu hiện tại.
`$CIDRAM['BlockInfo']['UALC']` | Đại lý người dùng (user agent) cho yêu cầu hiện tại (trong trường hợp thấp).
`$CIDRAM['BlockInfo']['ReasonMessage']` | Thông báo sẽ được hiển thị cho người dùng / khách hàng cho yêu cầu hiện tại nếu chúng bị chặn.
`$CIDRAM['BlockInfo']['SignatureCount']` | Số chữ ký kích hoạt cho yêu cầu hiện tại.
`$CIDRAM['BlockInfo']['Signatures']` | Thông tin tham khảo cho bất kỳ chữ ký nào được kích hoạt cho yêu cầu hiện tại.
`$CIDRAM['BlockInfo']['WhyReason']` | Thông tin tham khảo cho bất kỳ chữ ký nào được kích hoạt cho yêu cầu hiện tại.

---


### 8. <a name="SECTION8"></a>NHỮNG VẤN ĐỀ HỢP TƯƠNG TÍCH

Các gói và sản phẩm sau đã được tìm thấy là không tương thích với CIDRAM:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

Các mô-đun đã được cung cấp để đảm bảo rằng các gói và sản phẩm sau sẽ tương thích với CIDRAM:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__

*Xem thêm: [Biểu đồ tương thích](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 9. <a name="SECTION9"></a>NHỮNG CÂU HỎI THƯỜNG GẶP (FAQ)

- ["Chữ ký" là gì?](#user-content-WHAT_IS_A_SIGNATURE)
- ["CIDR" là gì?](#user-content-WHAT_IS_A_CIDR)
- ["Sai tích cực" là gì?](#user-content-WHAT_IS_A_FALSE_POSITIVE)
- [CIDRAM có thể chặn toàn bộ quốc gia?](#user-content-BLOCK_ENTIRE_COUNTRIES)
- [Tần suất cập nhật chữ ký là bao nhiêu?](#user-content-SIGNATURE_UPDATE_FREQUENCY)
- [Tôi đã gặp một vấn đề trong khi sử dụng CIDRAM và tôi không biết phải làm gì về nó! Hãy giúp tôi!](#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [Tôi đã bị chặn bởi CIDRAM từ một trang web mà tôi muốn ghé thăm! Hãy giúp tôi!](#user-content-BLOCKED_WHAT_TO_DO)
- [Tôi muốn sử dụng CIDRAM (trước v2) với phiên bản PHP cũ hơn 5.4.0; Bạn có thể giúp?](#user-content-MINIMUM_PHP_VERSION)
- [Tôi muốn sử dụng CIDRAM (v2) với phiên bản PHP cũ hơn 7.2.0; Bạn có thể giúp?](#user-content-MINIMUM_PHP_VERSION_V2)
- [Tôi có thể sử dụng một cài đặt CIDRAM để bảo vệ nhiều tên miền?](#user-content-PROTECT_MULTIPLE_DOMAINS)
- [Tôi không muốn lãng phí thời gian bằng cách cài đặt này và đảm bảo rằng nó hoạt động với trang web của tôi; Tôi có thể trả tiền cho bạn để làm điều đó cho tôi?](#user-content-PAY_YOU_TO_DO_IT)
- [Tôi có thể thuê bạn hay bất kỳ nhà phát triển nào của dự án này cho công việc riêng tư?](#user-content-HIRE_FOR_PRIVATE_WORK)
- [Tôi cần sửa đổi chuyên môn, tuỳ chỉnh, vv; Bạn có thể giúp?](#user-content-SPECIALIST_MODIFICATIONS)
- [Tôi là nhà phát triển, nhà thiết kế trang web, hay lập trình viên. Tôi có thể chấp nhận hay cung cấp các công việc liên quan đến dự án này không?](#user-content-ACCEPT_OR_OFFER_WORK)
- [Tôi muốn đóng góp cho dự án; Tôi có thể làm được điều này?](#user-content-WANT_TO_CONTRIBUTE)
- [Tôi có thể sử dụng cron để cập nhật tự động không?](#user-content-CRON_TO_UPDATE_AUTOMATICALLY)
- ["Vi phạm" là gì?](#user-content-WHAT_ARE_INFRACTIONS)
- [CIDRAM có thể chặn tên máy chủ không?](#user-content-BLOCK_HOSTNAMES)
- [Những gì tôi có thể sử dụng cho "default_dns"?](#user-content-những-gì-tôi-có-thể-sử-dụng-cho-default_dns)
- [Tôi có thể sử dụng CIDRAM để bảo vệ những thứ khác ngoài trang web (v.d., máy chủ email, FTP, SSH, IRC, vv)?](#user-content-PROTECT_OTHER_THINGS)
- [Sẽ xảy ra sự cố nếu tôi sử dụng CIDRAM cùng lúc với việc sử dụng các CDN hoặc các dịch vụ bộ nhớ đệm?](#user-content-CDN_CACHING_PROBLEMS)
- [CIDRAM có bảo vệ trang web của tôi khỏi các cuộc tấn công DDoS không?](#user-content-DDOS_ATTACKS)
- [Khi tôi kích hoạt hoặc hủy kích hoạt các mô-đun hay các tập tin chữ ký thông qua trang cập nhật, nó sắp xếp chúng theo thứ tự chữ và số trong cấu hình. Tôi có thể thay đổi cách họ được sắp xếp không?](#user-content-CHANGE_COMPONENT_SORT_ORDER)
- ["PDO DSN" là gì? Làm cách nào tôi có thể sử dụng PDO với CIDRAM?](#user-content-HOW_TO_USE_PDO)
- [CIDRAM đang chặn cronjobs; Làm thế nào để khắc phục điều này?](#user-content-BLOCK_CRON)

#### <a name="WHAT_IS_A_SIGNATURE"></a>"Chữ ký" là gì?

Trong bối cảnh của CIDRAM, "chữ ký" đề cập đến dữ liệu hoạt động như một định danh cho một cái gì đó cụ thể mà chúng tôi đang tìm kiếm, thường là một địa chỉ IP hoặc CIDR, và bao gồm một số chỉ dẫn cho CIDRAM, nói với nó cách trả lời khi nó gặp những gì chúng ta đang tìm kiếm. Một chữ ký CIDRAM điển hình trông giống như thế này:

Đối với "tập tin chữ ký":

`1.2.3.4/32 Deny Generic`

Đối với "mô-đun":

```PHP
$Trigger(strpos($CIDRAM['BlockInfo']['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*Chú thích: Chữ ký cho "tập tin chữ ký", và chữ ký cho "mô-đun", không phải là cùng một điều.*

Thông thường (nhưng không phải luôn luôn), chữ ký sẽ được nhóm lại với nhau, để hình thành "phần chữ ký", thường kèm theo bình luận, đánh dấu, hay siêu dữ liệu liên quan mà có thể được sử dụng để cung cấp bối cảnh bổ sung cho chữ ký hay lệnh bổ sung.

#### <a name="WHAT_IS_A_CIDR"></a>"CIDR" là gì?

"CIDR" là một từ viết tắt cho "Classless Inter-Domain Routing" *[[1](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing), [2](https://whatismyipaddress.com/cidr)]*, và nó là từ viết tắt này được sử dụng như là một phần của tên cho gói này, "CIDRAM", đó là một từ viết tắt cho "Classless Inter-Domain Routing Access Manager".

Tuy nhiên, trong bối cảnh của CIDRAM (như là, trong tài liệu này, trong các cuộc thảo luận liên quan đến CIDRAM, hay trong dữ liệu ngôn ngữ CIDRAM), bất cứ khi nào một "CIDR" (số ít) hoặc "CIDRs" (số nhiều) được đề cập hoặc tham khảo (và như vậy khi chúng ta sử dụng những từ này như danh từ, ngược lại với từ viết tắt), những gì được dự định và có ý nghĩa bởi đây là một subnet, bày tỏ bằng cách sử dụng ký hiệu CIDR. Lý do mà CIDR (hoặc CIDRs) được sử dụng thay vì subnet là để làm rõ mà nó là các subnet bày tỏ bằng cách sử dụng ký hiệu CIDR mà được đề cập đến (bởi vì ký hiệu CIDR chỉ là một trong một số cách khác nhau mà các subnet có thể được bày tỏ). Như vậy, CIDRAM có thể được coi là quản lý truy cập cho subnet.

Mặc dù ý nghĩa kép của "CIDR" có thể đưa ra một số sự mơ hồ trong một số trường hợp, giải thích này, cùng với bối cảnh được cung cấp, sẽ giúp giải quyết sự mơ hồ đó.

#### <a name="WHAT_IS_A_FALSE_POSITIVE"></a>"Sai tích cực" là gì?

Nghĩa của "sai tích cực" (*hay: "lỗi sai tích cực"; "báo động giả"*; Tiếng Anh: *false positive*; *false positive error*; *false alarm*), mô tả rất đơn giản, và trong một bối cảnh tổng quát, được sử dụng khi kiểm tra cho một điều kiện, để tham khảo các kết quả của bài kiểm tra, khi kết quả là tích cực (hay, điều kiện được xác định là "tích cực", hay "đúng"), nhưng dự kiến sẽ được (hay cần phải có được) tiêu cực (hay, điều kiện, thực tế, là "tiêu cực", hay "sai"). "Sai tích cực" có thể được coi là điều tương tự như "khóc sói" (theo đó các điều kiện đang được kiểm tra là liệu có con sói gần đàn, điều kiện là "sai" bởi vì không có con sói gần đàn, và điều kiện được báo cáo là "tích cực" bởi các người chăn bằng cách gọi "sói, sói"), hay tương tự như tình huống trong thử nghiệm y tế theo đó một bệnh nhân được chẩn đoán là có một số bệnh, trong khi thực tế, họ không có bất kỳ số bệnh.

Một số các từ ngữ khác sử dụng là "đúng tích cực", "đúng tiêu cực" và "sai tiêu cực". "Đúng tích cực" đề cập đến khi các kết quả kiểm tra và tình trạng thực tế của điều kiện là cả hai đúng (hay "tích cực"), và "đúng tiêu cực" đề cập đến khi các kết quả kiểm tra và tình trạng thực tế của điều kiện là cả hai sai (hay "tiêu cực"); "Đúng tích cực" hay "đúng tiêu cực" được coi là một "suy luận đúng". Các phản đề của "sai tích cực" là "sai tiêu cực"; "Sai tiêu cực" đề cập đến khi các kết quả kiểm tra là tiêu cực (hay, điều kiện được xác định là "tiêu cực", hay "sai"), nhưng dự kiến sẽ được (hay cần phải có được) tích cực (hay, điều kiện, thực tế, là "tích cực", hay "đúng").

Trong bối cảnh CIDRAM, các từ ngữ đề cập đến chữ ký của CIDRAM và các họ chặn gì/ai. Khi CIDRAM chặn địa chỉ IP bởi vì chữ ký của nó là xấu, lỗi thời hay không chính xác, nhưng không nên làm như vậy, hay khi nó làm như vậy vì những lý do sai, chúng tôi đề cập đến sự kiện này như "sai tích cực". Khi CIDRAM không chặn một địa chỉ IP đó nên đã bị chặn, bởi vì mối đe dọa khó lường, chữ ký mất tích hay thiếu sót trong chữ ký, chúng tôi đề cập đến sự kiện này như "phát hiện mất tích" (which is analogous to a "sai tiêu cực").

Điều này có thể được tóm tắt bằng bảng dưới đây:

&nbsp; | CIDRAM *KHÔNG* nên chặn một địa chỉ IP | CIDRAM *NÊN* chặn một địa chỉ IP
---|---|---
CIDRAM *KHÔNG* chặn một địa chỉ IP | Đúng tiêu cực (suy luận đúng) | Phát hiện mất tích (điều tương tự như sai tiêu cực)
CIDRAM chặn một địa chỉ IP | __Sai tích cực__ | Đúng tích cực (suy luận đúng)

#### <a name="BLOCK_ENTIRE_COUNTRIES"></a>CIDRAM có thể chặn toàn bộ quốc gia?

Vâng. Cách dễ nhất để làm điều này là bằng cách cài đặt mô-đun BGPView và định cấu hình nó theo nhu cầu của bạn.

#### <a name="SIGNATURE_UPDATE_FREQUENCY"></a>Tần suất cập nhật chữ ký là bao nhiêu?

Tần suất cập nhật thay đổi tùy thuộc vào các tập tin chữ ký trong câu hỏi. Nói chung là, tất cả các người bảo trì cho các tất cả tập tin chữ ký cố gắng đảm bảo rằng chữ ký của họ được cập nhật càng nhiều càng tốt, nhưng bởi vì tất cả chúng ta đều có nhiều cam kết khác, cuộc sống của chúng ta bên ngoài dự án, và bởi vì không ai trong chúng ta được bồi thường tài chính (hay được thanh toán) cho các nỗ lực dự án của chúng tôi, Một lịch trình cập nhật chính xác không thể được đảm bảo. Nói chung là, chữ ký được cập nhật bất cứ khi nào có đủ thời gian để cập nhật chúng, và các người bảo trì cố gắng ưu tiên dựa trên sự cần thiết và dựa trên tần suất của thay đổi giữa các phạm vi. Trợ giúp luôn được đánh giá cao nếu bạn sẵn sàng cung cấp bất kỳ.

#### <a name="ENCOUNTERED_PROBLEM_WHAT_TO_DO"></a>Tôi đã gặp một vấn đề trong khi sử dụng CIDRAM và tôi không biết phải làm gì về nó! Hãy giúp tôi!

- Bạn đang sử dụng phiên bản mới nhất của phần mềm? Bạn đang sử dụng phiên bản mới nhất của tập tin chữ ký của bạn? Nếu câu trả lời cho một trong hai những câu hỏi này là không, cố gắng cập nhật mọi thứ đầu tiên, và kiểm tra nếu vấn đề vẫn còn. Nếu nó vẫn còn, tiếp tục đọc.
- Bạn đã kiểm tra tất cả các tài liệu chưa? Nếu không, xin hãy làm như vậy. Nếu vấn đề không thể giải quyết bằng cách sử dụng tài liệu, hãy tiếp tục đọc.
- Bạn đã kiểm tra các **[trang issues](https://github.com/CIDRAM/CIDRAM/issues)** chưa, để xem nếu vấn đề đã được đề cập trước đó? Nếu nó đã được đề cập trước đó, kiểm tra nếu có bất kỳ đề xuất, ý tưởng, hay giải pháp đã được cung cấp, và làm theo như là cần thiết để cố gắng giải quyết vấn đề.
- Nếu vấn đề vẫn còn, vui lòng hãy tìm sự giúp đỡ về nó bằng cách tạo ra một issue mới trên trang issues.

#### <a name="BLOCKED_WHAT_TO_DO"></a>Tôi đã bị chặn bởi CIDRAM từ một trang web mà tôi muốn ghé thăm! Hãy giúp tôi!

CIDRAM cung cấp một cách cho chủ sở hữu trang web để chặn lưu lượng không mong muốn, nhưng đó là trách nhiệm của chủ sở hữu trang web tự quyết định cách mà họ muốn sử dụng CIDRAM. Trong trường hợp của sai tích cực liên quan đến các tập tin chữ ký thường trong gói CIDRAM, đính chính có thể được thực hiện, nhưng để được bỏ chặn từ các trang web cụ thể, bạn sẽ cần phải liên hệ với chủ sở hữu của các trang web được đề cập. Trong trường hợp đính chính được thực hiện, ít nhất, họ sẽ cần phải cập nhật các tập tin chữ ký hay cài đặt của họ, và trong các trường hợp khác (chẳng hạn như, ví dụ, khi họ đã sửa đổi cài đặt của họ, đã tạo ra chữ ký riêng của họ, vv), trách nhiệm của giải quyết vấn đề của bạn hoàn toàn là của họ, và hoàn toàn nằm ngoài tầm kiểm soát của chúng tôi.

#### <a name="MINIMUM_PHP_VERSION"></a>Tôi muốn sử dụng CIDRAM (trước v2) với phiên bản PHP cũ hơn 5.4.0; Bạn có thể giúp?

Không. PHP >= 5.4.0 là yêu cầu tối thiểu đối với CIDRAM < v2.

#### <a name="MINIMUM_PHP_VERSION_V2"></a>Tôi muốn sử dụng CIDRAM (v2) với phiên bản PHP cũ hơn 7.2.0; Bạn có thể giúp?

Không. PHP >= 7.2.0 là yêu cầu tối thiểu đối với CIDRAM v2.

*Xem thêm: [Biểu đồ tương thích](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>Tôi có thể sử dụng một cài đặt CIDRAM để bảo vệ nhiều tên miền?

Vâng. Cài đặt CIDRAM không bị khóa vào các tên miền cụ thể, và do đó có thể được sử dụng để bảo vệ nhiều tên miền. Nói chung là, chúng tôi đề cập đến cài đặt CIDRAM chỉ bảo vệ một miền như "cài đặt miền đơn" ("single-domain installations"), và chúng tôi đề cập đến cài đặt CIDRAM bảo vệ nhiều miền hay miền phụ như "cài đặt nhiều miền" ("multi-domain installations"). Nếu bạn sử dụng một cài đặt nhiều miền và cần phải sử dụng các bộ tập tin chữ ký khác nhau cho các miền khác nhau, hoặc cần CIDRAM được cấu hình khác nhau cho các miền khác nhau, điều này có thể làm được. Sau khi tải tập tin cấu hình (`config.ini`), CIDRAM sẽ kiểm tra sự tồn tại của một "tập tin ghi đè cấu hình" cụ thể cho miền được yêu cầu (`miền-được-yêu-cầu.tld.config.ini`), và nếu được tìm thấy, bất kỳ giá trị cấu hình nào được xác định bởi tập tin ghi đè cấu hình sẽ được sử dụng cho trường hợp thực hiện thay vì các giá trị cấu hình được định nghĩa bởi tập tin cấu hình. Các tập tin ghi đè cấu hình giống với tập tin cấu hình, và tùy theo quyết định của bạn, có thể chứa toàn bộ các chỉ thị cấu hình sẵn có cho CIDRAM, hoặc bất kỳ phần bắt buộc nào mà khác với các giá trị được xác định bởi tập tin cấu hình. Các tập tin ghi đè cấu hình được đặt tên theo miền mà chúng được dự định (vì vậy, ví dụ, nếu bạn cần một tập tin ghi đè cấu hình cho miền, `https://www.some-domain.tld/`, các tập tin ghi đè cấu hình của nó nên được đặt tên là `some-domain.tld.config.ini`, và nên được đặt trong vault với tập tin cấu hình, `config.ini`). Tên miền cho trường hợp thực hiện được bắt nguồn từ header (tiêu đề) `HTTP_HOST` của các yêu cầu; "www" bị bỏ qua.

#### <a name="PAY_YOU_TO_DO_IT"></a>Tôi không muốn lãng phí thời gian bằng cách cài đặt này và đảm bảo rằng nó hoạt động với trang web của tôi; Tôi có thể trả tiền cho bạn để làm điều đó cho tôi?

Có lẽ. Điều này được xem xét theo từng trường hợp cụ thể. Cho chúng tôi biết những gì bạn cần, những gì bạn đang cung cấp, và chúng tôi sẽ cho bạn biết liệu chúng tôi có thể giúp đỡ hay không.

#### <a name="HIRE_FOR_PRIVATE_WORK"></a>Tôi có thể thuê bạn hay bất kỳ nhà phát triển nào của dự án này cho công việc riêng tư?

*Xem ở trên.*

#### <a name="SPECIALIST_MODIFICATIONS"></a>Tôi cần sửa đổi chuyên môn, tuỳ chỉnh, vv; Bạn có thể giúp?

*Xem ở trên.*

#### <a name="ACCEPT_OR_OFFER_WORK"></a>Tôi là nhà phát triển, nhà thiết kế trang web, hay lập trình viên. Tôi có thể chấp nhận hay cung cấp các công việc liên quan đến dự án này không?

Vâng. Giấy phép của chúng tôi không cấm điều này.

#### <a name="WANT_TO_CONTRIBUTE"></a>Tôi muốn đóng góp cho dự án; Tôi có thể làm được điều này?

Vâng. Đóng góp cho dự án rất được hoan nghênh. Vui lòng xem "CONTRIBUTING.md" để biết thêm thông tin.

#### <a name="CRON_TO_UPDATE_AUTOMATICALLY"></a>Tôi có thể sử dụng cron để cập nhật tự động không?

Vâng. API được tích hợp trong front-end để tương tác với trang cập nhật thông qua các kịch bản bên ngoài. Một kịch bản riêng biệt, "[Cronable](https://github.com/Maikuolan/Cronable)", là có sẵn, và có thể được sử dụng bởi cron manager hay cron scheduler để tự động cập nhật gói này và gói hỗ trợ khác (kịch bản này cung cấp tài liệu riêng của nó).

#### <a name="WHAT_ARE_INFRACTIONS"></a>"Vi phạm" là gì?

"Vi phạm" xác định khi một IP không bị chặn bởi bất kỳ tập tin chữ ký cụ thể nào cũng sẽ bị chặn vì bất kỳ yêu cầu nào trong tương lai, và chúng liên quan chặt chẽ với giám sát IP. Một số chức năng và mô-đun tồn tại cho phép các yêu cầu bị chặn vì các lý do khác với IP có nguồn gốc (như là sự hiện diện của các đại lý người dùng ["user agents"] tương ứng với chương trình thư rác ["spambots"] hay công cụ hack ["hacktools"], truy vấn nguy hiểm, giả mạo DNS và vv), và khi điều này xảy ra, một "vi phạm" có thể xảy ra. Chúng cung cấp cách để nhận định địa chỉ IP tương ứng với các yêu cầu không mong muốn mà có thể chưa bị chặn bởi bất kỳ tập tin chữ ký cụ thể nào. Các vi phạm thường tương ứng với 1 đến 1 với số lần IP bị chặn, nhưng không phải luôn luôn (sự kiện nghiêm trọng chặn có thể gây ra một giá trị vi phạm lớn hơn một, và nếu "track_mode" là sai [false], vi phạm sẽ không xảy ra cho các sự kiện chặn gây ra bởi chỉ các tập tin chữ ký).

#### <a name="BLOCK_HOSTNAMES"></a>CIDRAM có thể chặn tên máy chủ không?

Vâng. Điều này có thể đạt được bằng cách tạo một quy tắc phụ trợ hoặc mô-đun.

![Quy tắc phụ trợ để chặn tên máy chủ](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/auxrule_block_hostname.png)

#### <a name="WHAT_CAN_I_USE_FOR_DEFAULT_DNS"></a>Những gì tôi có thể sử dụng cho "default_dns"?

Nói chung, IP của bất kỳ máy chủ DNS đáng tin cậy nào sẽ đủ. Nếu bạn đang tìm kiếm đề xuất, [public-dns.info](https://public-dns.info/) và [OpenNIC](https://servers.opennic.org/) cung cấp danh sách rộng rãi các máy chủ DNS công cộng đã biết. Ngoài ra, xem bảng dưới đây:

IP | Nhà điều hành
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

*Chú thích: Tôi không cung cấp quả quyết hoặc đảm bảo về các chính sách bảo mật, tính bảo mật, hiệu quả, và độ tin cậy của bất kỳ dịch vụ DNS nào, được liệt kê hay cách khác. Xin vui lòng làm nghiên cứu của riêng bạn khi đưa ra quyết định về họ.*

#### <a name="PROTECT_OTHER_THINGS"></a>Tôi có thể sử dụng CIDRAM để bảo vệ những thứ khác ngoài trang web (v.d., máy chủ email, FTP, SSH, IRC, vv)?

Bạn có thể (theo nghĩa hợp pháp), nhưng không nên (theo nghĩa kỹ thuật và thực tế). Giấy phép của chúng tôi không hạn chế công nghệ nào thực hiện CIDRAM, nhưng CIDRAM là một WAF (Web Application Firewall) và luôn có ý định bảo vệ các trang web. Bởi vì nó không được thiết kế với các công nghệ khác trong tâm trí, nó không có hiệu quả hoặc cung cấp bảo vệ đáng tin cậy cho các công nghệ khác, việc thực hiện có thể là khó khăn, và nguy cơ sai tích cực và phát hiện mất tích là rất cao.

#### <a name="CDN_CACHING_PROBLEMS"></a>Sẽ xảy ra sự cố nếu tôi sử dụng CIDRAM cùng lúc với việc sử dụng các CDN hoặc các dịch vụ bộ nhớ đệm?

Có lẽ. Điều này phụ thuộc vào tính chất của dịch vụ được đề cập và cách bạn sử dụng dịch vụ. Nói chung, nếu bạn chỉ lưu trữ nội dung tĩnh (v.d., hình ảnh, CSS, vv; bất cứ điều gì không thay đổi theo thời gian), không nên có bất kỳ vấn đề. Có thể có vấn đề mặc dù, nếu bạn đang lưu trữ dữ liệu mà thông thường sẽ được tạo động nếu được yêu cầu, hoặc nếu bạn đang lưu trữ kết quả của các yêu cầu POST (điều này về cơ bản sẽ làm cho trang web của bạn và môi trường của nó như bắt buộc tĩnh, và CIDRAM không có khả năng cung cấp bất kỳ lợi ích có ý nghĩa nào trong một môi trường bắt buộc tĩnh). Cũng có thể có các yêu cầu cấu hình cụ thể cho CIDRAM, tùy thuộc vào dịch vụ bộ nhớ đệm hoặc CDN mà bạn đang sử dụng (bạn cần đảm bảo rằng CIDRAM được định cấu hình chính xác cho dịch vụ bộ nhớ đệm hoặc CDN cụ thể mà bạn đang sử dụng). Cấu hình không chính xác cho CIDRAM có thể dẫn đến vấn đề đáng kể của các sai tích cực và các sự phát hiện mất tích.

#### <a name="DDOS_ATTACKS"></a>CIDRAM có bảo vệ trang web của tôi khỏi các cuộc tấn công DDoS không?

Câu trả lời ngắn gọn: Không.

Câu trả lời hơi dài hơn: CIDRAM sẽ giúp giảm tác động mà lưu lượng không mong muốn có thể có trên trang web của bạn (do đó làm giảm chi phí băng thông của trang web của bạn), sẽ giúp giảm tác động mà lưu lượng không mong muốn có thể có trên phần cứng của bạn (ví dụ, khả năng xử lý và phân phối yêu cầu của máy chủ của bạn), và có thể giúp giảm các hiệu ứng tiêu cực tiềm năng khác liên quan đến lưu lượng không mong muốn. Tuy nhiên, có hai điều quan trọng cần nhớ để hiểu câu hỏi này.

Thứ nhất, CIDRAM là một gói PHP, và do đó hoạt động ở máy nơi PHP được cài đặt. Điều này có nghĩa là CIDRAM chỉ có thể xem và chặn một yêu cầu *sau khi* máy chủ đã nhận được nó. Thứ hai, giảm thiểu DDoS hiệu quả sẽ lọc các yêu cầu *trước khi* chúng đến được máy chủ được nhắm mục tiêu bởi cuộc tấn công DDoS. Lý tưởng nhất, các cuộc tấn công DDoS nên được phát hiện và giảm thiểu bằng các giải pháp có khả năng giảm hay định tuyến lại lưu lượng được liên kết đến cuộc tấn công, trước khi nó đến máy chủ được nhắm mục tiêu ngay từ đầu.

Điều này có thể được thực hiện bằng cách sử dụng các giải pháp phần cứng chuyên dụng có trên địa điểm, các giải pháp dựa trên đám mây như các dịch vụ giảm thiểu DDoS chuyên dụng, định tuyến DNS của tên miền thông qua mạng chống DDoS, lọc dựa trên đám mây, hoặc một số kết hợp của chúng. Tuy nhiên, trong mọi trường hợp, chủ đề này hơi phức tạp để giải thích kỹ lưỡng chỉ với một hoặc hai đoạn, vì vậy tôi khuyên bạn nên nghiên cứu thêm nếu đây là chủ đề bạn muốn theo đuổi. Khi bản chất thực sự của các cuộc tấn công DDoS được hiểu đúng, câu trả lời này sẽ có ý nghĩa hơn.

#### <a name="CHANGE_COMPONENT_SORT_ORDER"></a>Khi tôi kích hoạt hoặc hủy kích hoạt các mô-đun hay các tập tin chữ ký thông qua trang cập nhật, nó sắp xếp chúng theo thứ tự chữ và số trong cấu hình. Tôi có thể thay đổi cách họ được sắp xếp không?

Vâng. Nếu bạn cần buộc một số tập tin thực thi theo thứ tự cụ thể, bạn có thể thêm một số dữ liệu tùy ý trước tên của chúng trong chỉ thị cấu hình nơi chúng được liệt kê, được phân tách bằng dấu hai chấm. Khi trang cập nhật sau đó sắp xếp lại các tập tin, dữ liệu tùy ý được thêm này sẽ ảnh hưởng đến thứ tự sắp xếp, gây ra chúng do đó để thực hiện theo thứ tự mà bạn muốn, mà không cần phải đổi tên bất kỳ người nào trong số họ.

Ví dụ, giả sử một chỉ thị cấu hình với các tập tin được liệt kê như sau:

`file1.php,file2.php,file3.php,file4.php,file5.php`

Nếu bạn muốn `file3.php` thực hiện trước, bạn có thể thêm một cái gì đó như `aaa:` trước tên của tập tin:

`file1.php,file2.php,aaa:file3.php,file4.php,file5.php`

Sau đó, nếu một tập tin mới, `file6.php`, được kích hoạt, khi trang cập nhật sắp xếp lại tất cả, nó sẽ kết thúc như sau:

`aaa:file3.php,file1.php,file2.php,file4.php,file5.php,file6.php`

Tình huống tương tự khi một tập tin bị hủy kích hoạt. Ngược lại, nếu bạn muốn tập tin thực thi cuối cùng, bạn có thể thêm một cái gì đó như `zzz:` trước tên của tập tin. Trong mọi trường hợp, bạn sẽ không cần đổi tên tập tin đang được đề cập đến.

#### <a name="HOW_TO_USE_PDO"></a>"PDO DSN" là gì? Làm cách nào tôi có thể sử dụng PDO với CIDRAM?

"PDO" là từ viết tắt của "[PHP Data Objects](https://www.php.net/manual/en/intro.pdo.php)" (đối tượng dữ liệu PHP). Nó cung cấp một giao diện cho PHP để có thể kết nối với một số hệ thống cơ sở dữ liệu thường được sử dụng bởi các ứng dụng PHP khác nhau.

"DSN" là từ viết tắt của "[data source name](https://en.wikipedia.org/wiki/Data_source_name)" (tên nguồn dữ liệu). "PDO DSN" mô tả với PDO cách nó sẽ kết nối với cơ sở dữ liệu.

CIDRAM cung cấp tùy chọn để sử dụng PDO cho mục đích bộ nhớ cache. Để điều này hoạt động chính xác, bạn sẽ cần định cấu hình CIDRAM phù hợp, do đó cho phép PDO, tạo cơ sở dữ liệu mới cho CIDRAM để sử dụng (nếu bạn chưa có cơ sở dữ liệu cho CIDRAM để sử dụng), và tạo một bảng mới trong cơ sở dữ liệu của bạn theo cấu trúc được mô tả dưới đây.

Khi kết nối cơ sở dữ liệu thành công, nhưng bảng cần thiết không tồn tại, nó sẽ cố gắng tạo nó tự động. Tuy nhiên, hành vi này đã không được thử nghiệm rộng rãi và thành công không thể được đảm bảo.

Tất nhiên, điều này chỉ áp dụng nếu bạn thực sự muốn CIDRAM sử dụng PDO. Nếu bạn đủ hạnh phúc cho CIDRAM để sử dụng bộ đệm ẩn phẳng (theo cấu hình mặc định của nó) hoặc bất kỳ tùy chọn bộ nhớ cache nào khác được cung cấp, bạn sẽ không cần phải lo lắng về việc thiết lập cơ sở dữ liệu, bảng, vv.

Cấu trúc được mô tả dưới đây sử dụng "cidram" làm tên cơ sở dữ liệu của nó, nhưng bạn có thể sử dụng bất kỳ tên nào bạn muốn cho cơ sở dữ liệu của mình, miễn là cùng tên đó được sao chép trong cấu hình DSN của bạn.

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

Chỉ thị cấu hình `pdo_dsn` của CIDRAM nên được cấu hình như mô tả bên dưới.

```
Tùy thuộc vào trình điều khiển cơ sở dữ liệu nào được sử dụng...
├─4d (Cảnh báo: Thử nghiệm, chưa được kiểm tra, không được khuyến khích!)
│ │
│ │         ╔═══════╗
│ └─4D:host=localhost;charset=UTF-8
│           ╚╤══════╝
│            └Máy chủ để kết nối với để tìm cơ sở dữ liệu.
├─cubrid
│ │
│ │             ╔═══════╗      ╔═══╗        ╔═════╗
│ └─cubrid:host=localhost;port=33000;dbname=example
│               ╚╤══════╝      ╚╤══╝        ╚╤════╝
│                │              │            └Tên của cơ sở dữ liệu để sử dụng.
│                │              │
│                │              └Số cổng để kết nối với máy chủ.
│                │
│                └Máy chủ để kết nối với để tìm cơ sở dữ liệu.
├─dblib
│ │
│ │ ╔═══╗      ╔═══════╗        ╔═════╗
│ └─dblib:host=localhost;dbname=example
│   ╚╤══╝      ╚╤══════╝        ╚╤════╝
│    │          │                └Tên của cơ sở dữ liệu để sử dụng.
│    │          │
│    │          └Máy chủ để kết nối với để tìm cơ sở dữ liệu.
│    │
│    └Những giá trị khả thi: "mssql", "sybase", "dblib".
├─firebird
│ │
│ │                 ╔═══════════════════╗
│ └─firebird:dbname=/path/to/database.fdb
│                   ╚╤══════════════════╝
│                    ├Có thể là một đường dẫn đến một tập tin cơ sở dữ liệu
│                    │cục bộ.
│                    │
│                    ├Có thể kết nối với một máy chủ và số cổng.
│                    │
│                    └Bạn nên tham khảo tài liệu Firebird nếu bạn muốn sử dụng
│                     trình điều khiển này.
├─ibm
│ │
│ │         ╔═════╗
│ └─ibm:DSN=example
│           ╚╤════╝
│            └Các cơ sở dữ liệu được phân loại để kết nối với.
├─informix
│ │
│ │              ╔═════╗
│ └─informix:DSN=example
│                ╚╤════╝
│                 └Các cơ sở dữ liệu được phân loại để kết nối với.
├─mysql (Được khuyến nghị nhất!)
│ │
│ │              ╔═════╗      ╔═══════╗      ╔══╗
│ └─mysql:dbname=example;host=localhost;port=3306
│                ╚╤════╝      ╚╤══════╝      ╚╤═╝
│                 │            │              └Số cổng để kết nối với máy chủ.
│                 │            │
│                 │            └Máy chủ để kết nối với để tìm cơ sở dữ liệu.
│                 │
│                 └Tên của cơ sở dữ liệu để sử dụng.
├─oci
│ │
│ │            ╔═════╗
│ └─oci:dbname=example
│              ╚╤════╝
│               ├Can refer to the specific catalogued database.
│               │
│               ├Có thể kết nối với một máy chủ và số cổng.
│               │
│               └Bạn nên tham khảo tài liệu Oracle nếu bạn muốn sử dụng
│                trình điều khiển này.
├─odbc
│ │
│ │      ╔═════╗
│ └─odbc:example
│        ╚╤════╝
│         ├Có thể tham khảo cơ sở dữ liệu danh mục cụ thể.
│         │
│         ├Có thể kết nối với một máy chủ và số cổng.
│         │
│         └Bạn nên tham khảo tài liệu ODBC/DB2 nếu bạn muốn sử dụng
│          trình điều khiển này.
├─pgsql
│ │
│ │            ╔═══════╗      ╔══╗        ╔═════╗
│ └─pgsql:host=localhost;port=5432;dbname=example
│              ╚╤══════╝      ╚╤═╝        ╚╤════╝
│               │              │           └Tên của cơ sở dữ liệu để sử dụng.
│               │              │
│               │              └Số cổng để kết nối với máy chủ.
│               │
│               └Máy chủ để kết nối với để tìm cơ sở dữ liệu.
├─sqlite
│ │
│ │        ╔════════╗
│ └─sqlite:example.db
│          ╚╤═══════╝
│           └Đường dẫn đến tập tin cơ sở dữ liệu cục bộ để sử dụng.
└─sqlsrv
  │
  │               ╔═══════╗ ╔══╗          ╔═════╗
  └─sqlsrv:Server=localhost,1521;Database=example
                  ╚╤══════╝ ╚╤═╝          ╚╤════╝
                   │         │             └Tên của cơ sở dữ liệu để sử dụng.
                   │         │
                   │         └Số cổng để kết nối với máy chủ.
                   │
                   └Máy chủ để kết nối với để tìm cơ sở dữ liệu.
```

Nếu bạn không chắc chắn về việc sử dụng cái gì cho một phần cụ thể trong DSN của mình, hãy thử xem trước tiên xem nó có hoạt động như cũ không mà không thay đổi gì.

Lưu ý rằng `pdo_username` và `pdo_password` phải giống với tên người dùng và mật khẩu bạn đã chọn cho cơ sở dữ liệu của mình.

#### <a name="BLOCK_CRON"></a>CIDRAM đang chặn cronjobs; Làm thế nào để khắc phục điều này?

Nếu bạn đang sử dụng một tập tin chuyên dụng cho mục đích cronjobs, và nếu tập tin đó không cần phải được gọi trong các yêu cầu người dùng thông thường (chẳng hạn như bên ngoài bối cảnh cronjobs), cách đơn giản nhất để khắc phục điều này sẽ là đảm bảo rằng CIDRAM hoàn toàn không được thực thi trong các cronjobs của bạn (có nghĩa là, đừng nối CIDRAM vào tập tin chịu trách nhiệm xử lý các cronjobs của bạn).

Như một sự thay thế, nếu điều đó là không thể, nhưng địa chỉ IP của máy chủ cron của bạn tương đối phù hợp và có thể dự đoán được, bạn có thể thử danh sách trắng địa chỉ IP của máy chủ cron của bạn, bằng cách tạo chữ ký danh sách trắng cho nó trong tập tin chữ ký tùy chỉnh, hoặc bằng cách tạo một quy tắc phụ trợ để danh sách trắng cho nó. Nếu địa chỉ IP của máy chủ cron của bạn thường xuyên xoay và không thể dự đoán được, nhưng dù sao vẫn từ trong cùng một mạng cụ thể, bạn có thể thử liệt kê trong tập tin `ignore.dat` của bạn tên của phần chữ ký chịu trách nhiệm chặn nó ở vị trí đầu tiên.

Nếu bạn đã thử tất cả những ý tưởng đó và không ai trong số chúng làm việc cho bạn, hoặc nếu bạn cần giúp đỡ tìm ra cách để làm điều đó, bạn có thể tạo một issue mới tại trang issues của CIDRAM để yêu cầu trợ giúp.

---


### 11. <a name="SECTION11"></a>THÔNG TIN HỢP PHÁP

#### 11.0 PHẦN MỞ ĐẦU

Phần tài liệu này nhằm mô tả các cân nhắc pháp lý có thể có về việc sử dụng và thực hiện của gói, và cung cấp một số thông tin liên quan cơ bản. Điều này có thể quan trọng đối với một số người dùng như một phương tiện để đảm bảo tuân thủ mọi yêu cầu pháp lý có thể tồn tại ở các quốc gia mà họ hoạt động, và một số người dùng có thể cần phải điều chỉnh chính sách trang web của họ theo thông tin này.

Đầu tiên và quan trọng nhất, xin vui lòng nhận ra rằng tôi (tác giả gói) không phải là luật sư, cũng không phải là một chuyên gia pháp lý đủ điều kiện. Do đó, tôi không đủ tư cách pháp lý để cung cấp tư vấn pháp lý. Ngoài ra, trong một số trường hợp, yêu cầu pháp lý chính xác có thể khác nhau giữa các quốc gia và khu vực pháp lý khác nhau, và các yêu cầu pháp lý khác nhau đôi khi có thể xung đột (chẳng hạn như, ví dụ, trong trường hợp các quốc gia mà ủng hộ [quyền riêng tư](https://vi.wikipedia.org/wiki/Quy%E1%BB%81n_%C4%91%C6%B0%E1%BB%A3c_b%E1%BA%A3o_v%E1%BB%87_%C4%91%E1%BB%9Di_t%C6%B0) và quyền bị lãng quên, so với các quốc gia mà ủng hộ luật lưu giữ dữ liệu). Cũng xem xét việc truy cập vào gói không bị giới hạn ở các quốc gia hoặc khu vực pháp lý cụ thể, và do đó, cơ sở người dùng gói có khả năng đa dạng về mặt địa lý. Những điểm này được xem xét, tôi không ở trong một vị trí để tuyên bố những gì nó có nghĩa là để "tuân thủ về mặt pháp lý" cho tất cả người dùng, trong tất cả các liên quan. Tuy nhiên, tôi hy vọng rằng thông tin trong tài liệu này sẽ giúp bạn tự quyết định về những gì bạn phải làm để duy trì tuân thủ về mặt pháp lý trong bối cảnh của gói. Nếu bạn có bất kỳ nghi ngờ hoặc quan tâm nào về thông tin ở đây, hoặc nếu bạn cần thêm trợ giúp và tư vấn từ góc độ pháp lý, tôi khuyên bạn nên tham khảo ý kiến chuyên gia pháp lý đủ điều kiện.

#### 11.1 TRÁCH NHIỆM PHÁP LÝ

Theo như đã nêu trong giấy phép gói, gói được cung cấp mà không có bất kỳ bảo hành nào. Điều này bao gồm (nhưng không giới hạn) tất cả phạm vi trách nhiệm pháp lý. Gói phần mềm được cung cấp cho bạn để thuận tiện cho bạn, với hy vọng rằng nó sẽ hữu ích, và rằng nó sẽ cung cấp một số lợi ích cho bạn. Tuy nhiên, việc sử dụng hoặc triển khai gói, là lựa chọn của riêng bạn. Bạn không bị buộc phải sử dụng hoặc triển khai gói, nhưng khi bạn làm như vậy, bạn chịu trách nhiệm về quyết định đó. Tôi và những người đóng góp gói khác, không chịu trách nhiệm pháp lý về hậu quả của các quyết định mà bạn đưa ra, bất kể trực tiếp, gián tiếp, ngụ ý, hay nói cách khác.

#### 11.2 BÊN THỨ BA

Tùy thuộc vào cấu hình và triển khai chính xác của nó, gói có thể giao tiếp và chia sẻ thông tin với bên thứ ba trong một số trường hợp. Thông tin này có thể được định nghĩa là "[thông tin nhận dạng cá nhân](https://www.pcworld.com.vn/articles/cong-nghe/an-ninh-mang/2016/05/1248000/thong-tin-ca-nhan-tai-san-rieng-cung-la-tien/)" (PII) trong một số ngữ cảnh, bởi một số khu vực pháp lý.

Thông tin này có thể được các bên thứ ba này sử dụng như thế nào, là tuân theo của chính sách của các bên thứ ba, và nằm ngoài phạm vi của tài liệu này. Tuy nhiên, trong tất cả các trường hợp như vậy, việc chia sẻ thông tin với các bên thứ ba này có thể bị vô hiệu hóa. Trong tất cả các trường hợp như vậy, nếu bạn chọn kích hoạt nó, bạn có trách nhiệm nghiên cứu bất kỳ mối lo ngại nào về sự riêng tư, bảo mật, và việc sử dụng PII của các bên thứ ba này. Nếu có bất kỳ nghi ngờ nào, hoặc nếu bạn không hài lòng với hành vi của các bên thứ ba liên quan đến PII, tốt nhất là nên vô hiệu hóa tất cả việc chia sẻ thông tin với các bên thứ ba này.

Với mục đích minh bạch, loại thông tin được chia sẻ, và với ai, được mô tả dưới đây.

##### 11.2.0 TRA CỨU TÊN MÁY CHỦ

Nếu bạn sử dụng bất kỳ tính năng hay mô-đun nào để làm việc với tên máy chủ (chẳng hạn như "mô-đun cho chặn các host xấu", "tor project exit nodes block module", hay "xác minh máy tìm kiếm", ví dụ), CIDRAM cần để có thể có được tên máy chủ của các yêu cầu gửi đến bằng cách nào đó. Thông thường, nó thực hiện điều này bằng cách yêu cầu tên máy chủ của địa chỉ IP của các yêu cầu gửi đến từ một máy chủ DNS, hoặc bằng cách yêu cầu thông tin thông qua chức năng được cung cấp bởi hệ thống nơi CIDRAM được cài đặt (điều này thường được gọi là "tra cứu tên máy chủ"). Các máy chủ DNS được xác định theo mặc định thuộc về dịch vụ [Google DNS](https://dns.google.com/) (nhưng điều này có thể dễ dàng thay đổi thông qua cấu hình). Các dịch vụ chính xác được truyền thông phụ thuộc vào cách bạn định cấu hình gói (nó có thể được cấu hình dễ dàng). Trong trường hợp sử dụng chức năng được cung cấp bởi hệ thống nơi CIDRAM được cài đặt, bạn sẽ cần phải liên hệ với quản trị viên hệ thống của bạn để xác định các tuyến đường để sử dụng cho tra cứu tên máy chủ. Tra cứu tên máy chủ có thể được ngăn chặn trong CIDRAM bằng cách tránh các mô-đun bị ảnh hưởng hay bằng cách sửa đổi cấu hình gói để phù hợp với nhu cầu của bạn.

*Chỉ thị cấu hình có liên quan:*
- `general` -> `default_dns`
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`
- `general` -> `force_hostname_lookup`
- `general` -> `allow_gethostbyaddr_lookup`

##### 11.2.1 WEBFONT

Một số chủ đề tùy chỉnh, cũng như UI chuẩn ("giao diện người dùng") cho front-end CIDRAM và trang "Truy cập đã bị từ chối", có thể sử dụng các webfont vì lý do thẩm mỹ. Các webfont được vô hiệu hóa theo mặc định, nhưng khi được kích hoạt, giao tiếp trực tiếp giữa trình duyệt của người dùng và dịch vụ lưu trữ webfont sẽ xảy ra. Điều này có thể liên quan đến việc truyền thông tin như địa chỉ IP của người dùng, đại lý người dùng, hệ điều hành, và các chi tiết khác có sẵn cho yêu cầu. Hầu hết các webfont này được lưu trữ bởi dịch vụ [Google Fonts](https://fonts.google.com/).

*Chỉ thị cấu hình có liên quan:*
- `general` -> `disable_webfonts`

##### 11.2.2 XÁC MINH MÁY TÌM KIẾM VÀ TRUYỀN THÔNG XÃ HỘI

Khi xác minh máy tìm kiếm được kích hoạt, CIDRAM cố gắng thực hiện "tra cứu DNS chuyển tiếp" để xác minh tính xác thực của các yêu cầu nói rằng bắt nguồn từ các máy tìm kiếm. Tương tự như vậy, khi xác minh truyền thông xã hội được kích hoạt, CIDRAM thực hiện tương tự cho các yêu cầu truyền thông xã hội bị nghi ngờ. Để thực hiện điều này, nó sử dụng dịch vụ [Google DNS](https://dns.google.com/) để cố gắng giải quyết các địa chỉ IP từ tên máy chủ của các yêu cầu gửi đến này (trong quá trình này, tên máy chủ của các yêu cầu gửi đến này được chia sẻ với dịch vụ).

*Chỉ thị cấu hình có liên quan:*
- `general` -> `search_engine_verification`
- `general` -> `social_media_verification`
- `general` -> `other_verification`

##### 11.2.3 CAPTCHA

CIDRAM hỗ trợ reCAPTCHA và hCAPTCHA. Chúng yêu cầu các khóa API để hoạt động chính xác. Chúng bị vô hiệu hóa mặc định, nhưng có thể được kích hoạt bằng cách định cấu hình các khóa API. Khi được kích hoạt, giao tiếp có thể xảy ra giữa dịch vụ và CIDRAM hoặc trình duyệt của người dùng. Điều này có thể liên quan đến việc truyền đạt thông tin như địa chỉ IP của người dùng, tác nhân người dùng, hệ điều hành, và các chi tiết khác có sẵn cho yêu cầu.

##### 11.2.4 STOP FORUM SPAM

[Stop Forum Spam](https://www.stopforumspam.com/) là một dịch vụ tuyệt vời, miễn phí có sẵn có thể giúp bảo vệ diễn đàn, blog và trang web từ chương trình thư rác. Nó thực hiện điều này bằng cách cung cấp một cơ sở dữ liệu của chương trình và những người gửi thư rác đã biết, và một API có thể được tận dụng để kiểm tra xem địa chỉ IP, tên người dùng hay địa chỉ email có được liệt kê trên cơ sở dữ liệu của nó hay không.

CIDRAM cung cấp một mô-đun tùy chọn tận dụng API này để kiểm tra xem địa chỉ IP của các yêu cầu gửi đến thuộc về một chương trình và những người gửi thư rác bị nghi ngờ hay không. Mô-đun không được cài đặt theo mặc định, nhưng nếu bạn chọn cài đặt nó, địa chỉ IP của người dùng có thể được chia sẻ với API của Stop Forum Spam theo đúng mục đích của mô-đun. Khi mô-đun được cài đặt, CIDRAM giao tiếp với API này bất cứ khi nào một yêu cầu gửi đến yêu cầu một nguồn tài nguyên mà CIDRAM nhận ra là một loại tài nguyên thường xuyên được nhắm mục tiêu bởi chương trình và những người gửi thư rác (ví dụ, trang đăng nhập, trang đăng ký, trang xác minh email, biểu mẫu nhận xét, vv).

##### 11.2.5 ABUSEIPDB

CIDRAM cung cấp một mô-đun tùy chọn để chặn các địa chỉ IP lạm dụng bằng cách sử dụng API của [AbuseIPDB](https://www.abuseipdb.com/). Mô-đun không được cài đặt theo mặc định, nhưng nếu bạn chọn cài đặt nó, địa chỉ IP của người dùng có thể được chia sẻ với API của AbuseIPDB theo đúng mục đích của mô-đun.

##### 11.2.6 BGPVIEW

CIDRAM cung cấp một mô-đun tùy chọn để thực hiện tra cứu ASN và mã quốc gia bằng API của [BGPView](https://bgpview.io/) API. Các tra cứu này cung cấp khả năng chặn hoặc danh sách trắng yêu cầu trên cơ sở ASN hoặc quốc gia xuất xứ của họ. Mô-đun không được cài đặt theo mặc định, nhưng nếu bạn chọn cài đặt nó, địa chỉ IP của người dùng có thể được chia sẻ với API của BGPView theo đúng mục đích của mô-đun.

#### 11.3 NHẬT KÝ

Nhật ký là một phần quan trọng của CIDRAM vì một số lý do. có thể khó để chẩn đoán và giải quyết các kết quả sai tích cực khi các sự kiện chặn khiến chúng không được ghi lại. Khi các sự kiện chặn không được ghi lại, có thể khó để xác định chính xác CIDRAM hoạt động tốt như thế nào trong bất kỳ ngữ cảnh cụ thể nào, và có thể khó để xác định nơi bất cập của nó, và những thay đổi nào có thể cần thiết đối với cấu hình hay chữ ký của nó, để nó có thể tiếp tục hoạt động như dự định. Bất kể, nhật ký có thể không được mong muốn cho tất cả người dùng, và vẫn hoàn toàn tùy chọn. Trong CIDRAM, ghi nhật ký bị vô hiệu hóa theo mặc định. Để kích hoạt nó, CIDRAM phải được cấu hình cho phù hợp.

Ngoài ra, việc nhật ký có được cho phép hợp pháp hay không, và trong phạm vi được cho phép hợp pháp (ví dụ, các loại thông tin có thể được nhật ký, bao lâu, và trong hoàn cảnh gì), có thể thay đổi, tùy thuộc vào thẩm quyền pháp lý và trong bối cảnh CIDRAM được triển khai (ví dụ, nếu bạn đang hoạt động như một cá nhân, như một thực thể công ty, và nếu trên cơ sở thương mại hay phi thương mại). Do đó, nó có thể hữu ích cho bạn để đọc kỹ phần này.

Có nhiều kiểu ghi nhật ký mà CIDRAM có thể thực hiện. Các loại ghi nhật ký khác nhau liên quan đến các loại thông tin khác nhau, vì các lý do khác nhau.

##### 11.3.0 SỰ KIỆN CHẶN

Loại nhật ký chính mà CIDRAM có thể thực hiện liên quan đến "sự kiện chặn". Loại nhật ký này liên quan đến khi CIDRAM chặn một yêu cầu, và có thể được cung cấp theo ba định dạng khác nhau:
- Tập tin nhật ký mà có thể được đọc bởi con người.
- Tập tin nhật ký trong kiểu Apache.
- Tập tin nhật ký được tuần tự hóa.

Sự kiện khối, được ghi vào tập tin nhật ký mà có thể được đọc bởi con người, thường trông giống như sau (ví dụ):

```
ID: 1234
Phiên bản kịch bản: CIDRAM v1.6.0
Ngày/Thời gian: Day, dd Mon 20xx hh:ii:ss +0000
Địa chỉ IP: x.x.x.x
Tên máy chủ: dns.hostname.tld
Số lượng chữ ký: 1
Tham khảo cho chữ ký: x.x.x.x/xx
Tại sao bị chặn: Dịch vụ điện toán đám mây ("Tên mạng", Lxx:Fx, [XX])!
Đại lý người dùng: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36
URI được xây dựng lại: https://your-site.tld/index.php
Tình trạng CAPTCHA: Trên.
```

Cùng một sự kiện khối, được ghi vào tập tin nhật ký trong kiểu Apache, sẽ trông giống như sau:

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

Sự kiện khối đã nhật ký thường bao gồm thông tin sau:
- Một số ID tham chiếu đến sự kiện khối.
- Phiên bản CIDRAM hiện đang được sử dụng.
- Ngày và giờ xảy ra sự kiện chặn.
- Địa chỉ IP của yêu cầu bị chặn.
- Tên máy chủ của địa chỉ IP của yêu cầu bị chặn (nếu có).
- Số lượng chữ ký được kích hoạt bởi yêu cầu.
- Tham chiếu đến chữ ký được kích hoạt.
- Tham khảo các lý do cho sự kiện khối và một số thông tin gỡ rối cơ bản liên quan.
- Đại lý người dùng của yêu cầu bị chặn (danh tính của thực thể yêu cầu).
- Việc xây dựng lại số nhận dạng cho tài nguyên được yêu cầu ban đầu.
- Trạng thái CAPTCHA cho yêu cầu hiện tại (khi có liên quan).

*Các chỉ thị cấu hình chịu trách nhiệm về loại ghi nhật ký này và cho mỗi một trong ba định dạng có sẵn:*
- `general` -> `logfile`
- `general` -> `logfile_apache`
- `general` -> `logfile_serialized`

Khi các chỉ thị này được để trống, loại ghi nhật ký này sẽ vẫn bị vô hiệu hóa.

##### 11.3.1 NHẬT KÝ CAPTCHA

Loại nhật ký này liên quan cụ thể đến CAPTCHA, và chỉ xảy ra khi người dùng cố gắng hoàn thành CAPTCHA.

Mục nhập nhật ký CAPTCHA chứa địa chỉ IP của người dùng đang cố gắng hoàn thành CAPTCHA, ngày và giờ xảy ra sự cố, và trạng thái của CAPTCHA. Mục nhập nhật ký CAPTCHA thường trông giống như sau (ví dụ):

```
Địa chỉ IP: x.x.x.x - Ngày/Thời gian: Day, dd Mon 20xx hh:ii:ss +0000 - Tình trạng CAPTCHA: Thành công!
```

*Chỉ thị cấu hình chịu trách nhiệm cho nhật ký CAPTCHA là:*
- `recaptcha` -> `logfile`
- `hcaptcha` -> `logfile`

##### 11.3.2 NHẬT KÝ FRONT-END

Loại nhật ký này liên quan đến cố gắng đăng nhập, và chỉ xảy ra khi người dùng cố gắng đăng nhập vào front-end (giả sử truy cập front-end được kích hoạt).

Mục nhập nhật ký front-end chứa địa chỉ IP của người dùng đang cố gắng đăng nhập, ngày và giờ xảy ra điều này, và kết quả của cố gắng này (đăng nhập thành công, hoặc thành công không thành công). Mục nhập nhật ký front-end thường trông giống như thế này (làm ví dụ):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Đã đăng nhập.
```

*Chỉ thị cấu hình chịu trách nhiệm cho nhật ký front-end là:*
- `general` -> `frontend_log`

##### 11.3.3 XOAY VÒNG NHẬT KÝ

Bạn có thể muốn thanh lọc nhật ký sau một khoảng thời gian, hoặc có thể được yêu cầu làm như vậy theo luật pháp (khoảng thời gian được phép giữ nhật ký hợp pháp có thể bị giới hạn bởi luật pháp). Bạn có thể đạt được điều này bằng cách đưa dấu ngày/giờ vào tên tập tin nhật ký của bạn theo quy định của cấu hình gói của bạn (ví dụ, `{yyyy}-{mm}-{dd}.log`), và sau đó kích hoạt xoay vòng nhật ký (xoay vòng nhật ký cho phép bạn thực hiện một số hành động trên tập tin nhật ký khi vượt quá giới hạn được chỉ định).

Ví dụ: Nếu tôi được yêu cầu xóa nhật ký sau 30 ngày theo pháp luật, tôi có thể chỉ định `{dd}.log` trong tên của tập tin nhật ký của tôi (`{dd}` đại diện cho ngày), đặt giá trị của `log_rotation_limit` để 30, và đặt giá trị của `log_rotation_action` để `Delete`.

Ngược lại, nếu bạn được yêu cầu giữ lại nhật ký trong một khoảng thời gian dài, bạn có thể cân nhắc không sử dụng xoay vòng nhật ký, hoặc bạn có thể đặt giá trị của `log_rotation_action` để `Archive`, để nén tập tin nhật ký, do đó làm giảm tổng dung lượng đĩa mà họ chiếm.

*Chỉ thị cấu hình có liên quan:*
- `general` -> `log_rotation_limit`
- `general` -> `log_rotation_action`

##### 11.3.4 CẮT NGẮN NHẬT KÝ

Cũng có thể cắt ngắn các tập tin nhật ký riêng lẻ khi chúng vượt quá một kích thước nhất định, nếu đây bạn có thể cần hay muốn làm.

*Chỉ thị cấu hình có liên quan:*
- `general` -> `truncate`

##### 11.3.5 PSEUDONYMISATION ĐỊA CHỈ IP

Thứ nhất, nếu bạn không quen thuộc với thuật ngữ này, "pseudonymisation" đề cập đến việc xử lý dữ liệu cá nhân sao cho không thể xác định được dữ liệu cá nhân cho bất kỳ chủ đề dữ liệu cụ thể nào nữa trừ khi có thông tin bổ sung, và miễn là thông tin bổ sung đó được duy trì riêng biệt và phải chịu sự các biện pháp kỹ thuật và tổ chức để đảm bảo rằng dữ liệu cá nhân không thể được xác định cho bất kỳ người tự nhiên nào.

Trong một số trường hợp, bạn có thể được yêu cầu về mặt pháp lý để sử dụng "anonymisation" hoặc "pseudonymisation" cho bất kỳ PII nào được thu thập, xử lý hoặc lưu trữ. Mặc dù khái niệm này đã tồn tại trong một thời gian khá lâu, GDPR/DSGVO đề cập đến, và đặc biệt khuyến khích "pseudonymisation".

CIDRAM có thể sử dụng "pseudonymisation" cho các địa chỉ IP khi nhật ký chúng vào bản ghi, nếu đây bạn có thể cần hay muốn làm. Khi CIDRAM sử dụng "pseudonymisation" cho các địa chỉ IP, khi nhật ký chúng vào bản ghi, octet cuối cùng của địa chỉ IPv4, và mọi thứ sau phần thứ hai của địa chỉ IPv6 được đại diện bởi một "x" (hiệu quả làm tròn địa chỉ IPv4 đến địa chỉ đầu tiên của mạng con thứ 24 mà chúng đưa vào, và địa chỉ IPv6 đến địa chỉ đầu tiên của mạng con thứ 32 mà chúng đưa vào).

*Chú thích: Quá trình pseudonymisation địa chỉ IP của CIDRAM không ảnh hưởng đến tính năng giám sát IP của CIDRAM. Nếu đây là vấn đề với bạn, có thể tốt nhất là tắt giám sát IP hoàn toàn. Điều này có thể đạt được bằng cách đặt `track_mode` để `false` và bằng cách tránh bất kỳ mô-đun nào.*

*Chỉ thị cấu hình có liên quan:*
- `signatures` -> `track_mode`
- `legal` -> `pseudonymise_ip_addresses`

##### 11.3.6 BỎ QUA THÔNG TIN NHẬT KÝ

Nếu bạn muốn tiến thêm một bước nữa bằng cách ngăn chặn các loại thông tin cụ thể được ghi lại hoàn toàn, điều này cũng có thể thực hiện được. CIDRAM cung cấp chỉ thị cấu hình để kiểm soát xem địa chỉ IP, tên máy chủ, và đại lý người dùng có được bao gồm trong nhật ký hay không. Theo mặc định, tất cả ba trong số các điểm dữ liệu này được bao gồm trong nhật ký khi có sẵn. Việc đặt bất kỳ chỉ thị cấu hình nào thành `true` sẽ bỏ qua thông tin tương ứng từ nhật ký.

*Chú thích: Không có lý do gì để bút danh các địa chỉ IP khi bỏ qua chúng hoàn toàn từ các nhật ký.*

*Chỉ thị cấu hình có liên quan:*
- `legal` -> `omit_ip`
- `legal` -> `omit_hostname`
- `legal` -> `omit_ua`

##### 11.3.7 SỐ LIỆU THỐNG KÊ

CIDRAM có thể tùy chọn theo dõi số liệu thống kê như tổng số sự kiện chặn hay sự xuất hiện CAPTCHA đã xảy ra kể từ một số thời điểm cụ thể. Tính năng này được vô hiệu hóa theo mặc định, nhưng có thể được kích hoạt thông qua cấu hình gói. Tính năng này chỉ theo dõi tổng số sự kiện đã xảy ra và không bao gồm bất kỳ thông tin nào về các sự kiện cụ thể (và do đó, không nên được coi là PII).

*Chỉ thị cấu hình có liên quan:*
- `general` -> `statistics`

##### 11.3.8 MÃ HÓA

CIDRAM không mã hóa bộ nhớ cache của nó hoặc bất kỳ thông tin log nào. [Mã hóa](https://vi.wikipedia.org/wiki/M%C3%A3_h%C3%B3a) bộ nhớ cache và log có thể được giới thiệu trong tương lai, nhưng hiện tại không có bất kỳ kế hoạch cụ thể nào. Nếu bạn lo lắng về các bên thứ ba không được phép truy cập vào các phần của CIDRAM có thể chứa thông tin nhận dạng cá nhân hay thông tin nhạy cảm như bộ nhớ cache hoặc nhật ký của nó, tôi khuyên bạn không nên cài đặt CIDRAM tại vị trí có thể truy cập công khai (ví dụ, cài đặt CIDRAM bên ngoài thư mục `public_html` tiêu chuẩn hoặc tương đương chúng có sẵn cho hầu hết các máy chủ web tiêu chuẩn) và các quyền hạn chế thích hợp sẽ được thực thi cho thư mục nơi nó cư trú (đặc biệt, cho thư mục vault). Nếu điều đó không đủ để giải quyết mối quan ngại của bạn, hãy định cấu hình CIDRAM để các loại thông tin gây ra mối lo ngại của bạn sẽ không được thu thập hoặc nhật ký ở địa điểm đầu tiên (ví dụ, bằng cách tắt ghi nhật ký).

#### 11.4 COOKIE

CIDRAM đặt [cookie](https://vi.wikipedia.org/wiki/Cookie_(tin_h%E1%BB%8Dc)) ở hai điểm trong cơ sở mã của nó. Thứ nhất, khi người dùng hoàn tất thành công sự xuất hiện CAPTCHA (và giả định rằng `lockuser` được đặt thành `true`), CIDRAM đặt cookie để có thể ghi nhớ các yêu cầu tiếp theo mà người dùng đã hoàn sự xuất hiện CAPTCHA, vì vậy để không cần liên tục yêu cầu người dùng hoàn thành một sự xuất hiện CAPTCHA trên mỗi yêu cầu tiếp theo. Thứ hai, khi người dùng đăng nhập thành công vào front-end, CIDRAM đặt cookie để có thể nhớ người dùng cho các yêu cầu tiếp theo (cookie được sử dụng để xác thực người dùng đến phiên đăng nhập).

Trong cả hai trường hợp, cảnh báo cookie được hiển thị nổi bật (khi nó có liên quan), cảnh báo người dùng rằng cookie sẽ được đặt nếu họ tham gia vào các hành động có liên quan. Cookie không được đặt ở bất kỳ điểm nào khác trong cơ sở mã.

*Chú thích: Các API CAPTCHA "vô hình" có thể không tương thích với luật cookie ở một số khu vực pháp lý, và nên được tránh bởi bất kỳ trang web nào tuân theo các luật đó. Thay vào đó, chọn sử dụng các API được cung cấp khác, hoặc đơn giản là vô hiệu hóa hoàn toàn CAPTCHA, có thể thích hợp hơn.*

*Chỉ thị cấu hình có liên quan:*
- `general` -> `disable_frontend`
- `recaptcha` -> `lockuser`
- `recaptcha` -> `api`
- `hcaptcha` -> `lockuser`
- `hcaptcha` -> `api`

#### 11.5 TIẾP THỊ VÀ QUẢNG CÁO

CIDRAM không thu thập hoặc xử lý bất kỳ thông tin nào cho mục đích tiếp thị hoặc quảng cáo, và không bán hoặc lợi nhuận từ bất kỳ thông tin được thu thập hoặc ghi lại nào. CIDRAM không phải là một doanh nghiệp thương mại, cũng không liên quan đến bất kỳ lợi ích thương mại nào, do đó, làm những việc này sẽ không có ý nghĩa gì cả. Đây là trường hợp kể từ khi bắt đầu dự án, và tiếp tục là trường hợp ngày hôm nay. Ngoài ra, làm những việc này sẽ phản tác dụng với tinh thần và mục đích dự định của toàn bộ dự án, và miễn là tôi tiếp tục duy trì dự án, sẽ không bao giờ xảy ra.

#### 11.6 CHÍNH SÁCH BẢO MẬT

Trong một số trường hợp, bạn có thể được yêu cầu về mặt pháp lý để hiển thị rõ ràng liên kết đến chính sách bảo mật của bạn trên tất cả các trang và phần trong trang web của bạn. Điều này có thể quan trọng như một phương tiện để đảm bảo rằng người dùng được thông báo đầy đủ về các thực tiễn bảo mật chính xác của bạn, loại PII bạn thu thập, và cách bạn định sử dụng. Để có thể bao gồm một liên kết trên trang "Truy cập đã bị từ chối" của CIDRAM, một chỉ thị cấu hình được cung cấp để chỉ định URL cho chính sách bảo mật của bạn.

*Chú thích: Tôi khuyên bạn không nên đặt trang chính sách bảo mật của bạn sau bảo vệ của CIDRAM. Nếu CIDRAM bảo vệ trang chính sách bảo mật của bạn, và người dùng bị chặn bởi CIDRAM nhấp vào liên kết đến chính sách bảo mật của bạn, chúng sẽ chỉ bị chặn lại, và sẽ không thể xem chính sách bảo mật của bạn. Lý tưởng nhất, bạn nên liên kết đến một bản sao tĩnh của chính sách bảo mật của bạn, chẳng hạn như một trang HTML hoặc tập tin văn bản thuần mà không được bảo vệ bởi CIDRAM.*

*Chỉ thị cấu hình có liên quan:*
- `legal` -> `privacy_policy`

#### 11.7 GDPR/DSGVO

Quy định bảo vệ dữ liệu chung (GDPR) là một quy định của Liên minh châu Âu, có hiệu lực kể từ 25 Tháng Năm 2018. Mục tiêu chính của quy định là cung cấp quyền kiểm soát cho công dân và cư dân EU về dữ liệu cá nhân của riêng họ, và thống nhất quy định trong EU về quyền riêng tư và dữ liệu cá nhân.

Quy định này bao gồm các điều khoản cụ thể liên quan đến việc xử lý "thông tin nhận dạng cá nhân" (PII) của bất kỳ "chủ đề dữ liệu" nào (bất kỳ người tự nhiên được xác định hoặc có thể nhận dạng được) từ hoặc trong EU. Để tuân thủ quy định, "enterprise" hoặc "doanh nghiệp" (theo quy định của quy định), và bất kỳ hệ thống và quy trình có liên quan nào phải ghi nhớ sự riêng tư ngay từ đầu, phải sử dụng cài đặt bảo mật cao nhất có thể, phải thực hiện các biện pháp bảo vệ thích hợp cho bất kỳ thông tin được lưu trữ hay xử lý nào (bao gồm nhưng không giới hạn trong việc thực hiện "pseudonymisation" hoặc "anonymisation" đầy đủ của dữ liệu), phải khai báo rõ ràng các loại dữ liệu mà họ thu thập, cách họ xử lý nó, vì lý do gì, trong bao lâu họ giữ nó, và nếu họ chia sẻ dữ liệu này với bất kỳ bên thứ ba nào, các loại dữ liệu được chia sẻ với bên thứ ba, cách, tại sao, vv.

Dữ liệu có thể không được xử lý trừ khi có cơ sở hợp pháp để làm như vậy, theo quy định của quy định. Nói chung, điều này có nghĩa là để xử lý dữ liệu của chủ đề dữ liệu trên cơ sở hợp pháp, nó phải được thực hiện theo nghĩa vụ pháp lý, hoặc chỉ được thực hiện sau khi có sự đồng ý rõ ràng và đầy đủ thông tin đã được lấy từ chủ đề dữ liệu.

Bởi vì các khía cạnh của quy định có thể phát triển trong thời gian, để tránh việc truyền bá thông tin lỗi thời, nó có thể là tốt hơn để tìm hiểu về các quy định từ một nguồn có thẩm quyền, trái ngược với việc chỉ bao gồm các thông tin có liên quan ở đây trong tài liệu gói (mà cuối cùng có thể trở nên lỗi thời khi quy định phát triển).

Một số tài nguyên được khuyến khích để tìm hiểu thêm thông tin:
- [REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679)
- [Quy định bảo vệ dữ liệu chung](https://vi.wikipedia.org/wiki/Quy_%C4%91%E1%BB%8Bnh_b%E1%BA%A3o_v%E1%BB%87_d%E1%BB%AF_li%E1%BB%87u_chung)

---


Lần cuối cập nhật: 2023.03.05.
