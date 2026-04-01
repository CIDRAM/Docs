## Tài liệu của CIDRAM v4 (Tiếng Việt).

### Nội dung
- 1. [LỜI GIỚI THIỆU](#user-content-SECTION1)
- 2. [CÁCH CÀI ĐẶT](#user-content-SECTION2)
- 3. [CÁCH SỬ DỤNG](#user-content-SECTION3)
- 4. [QUẢN LÝ FRONT-END](#user-content-SECTION4)
- 5. [TÙY CHỌN CHO CẤU HÌNH](#user-content-SECTION5)
- 6. [ĐỊNH DẠNG CỦA CHỬ KÝ](#user-content-SECTION6)
- 7. [NHỮNG VẤN ĐỀ HỢP TƯƠNG TÍCH](#user-content-SECTION7)
- 8. [NHỮNG CÂU HỎI THƯỜNG GẶP (FAQ)](#user-content-SECTION8)
- 9. [THÔNG TIN HỢP PHÁP](#user-content-SECTION9)
- 10. [NÂNG CẤP TỪ CÁC PHIÊN BẢN CHÍNH TRƯỚC ĐÓ](#user-content-SECTION10)

*Regarding translations: My native language is English. Because this is a free and open-source hobby project which generates zero income, and translatable content is likely to change as the features and functionality supported by the project changes, it doesn't make sense for me to spend money for translations. Because I'm the sole author/developer/maintainer for the project and I'm not a ployglot, any translations I produce are very likely to contain errors. Sorry, but realistically, that won't ever change. If you find any such errors/typos/mistakes/etc, your assistance to correct them would be very much appreciated. Pull requests are invited and encouraged. Otherwise, if you find these errors too much to handle, just stick with the original English source. If a translation is irredeemably incomprehensible, let me know which, and I can delete it. If you're not sure how to perform pull requests, ask. I can help.*

---


### 1. <a name="SECTION1"></a>LỜI GIỚI THIỆU

CIDRAM (Classless Inter-Domain Routing Access Manager) là một kịch bản PHP được thiết kế để bảo vệ các trang mạng bằng cách ngăn chặn các yêu cầu có nguồn gốc từ các địa chỉ IP coi như là nguồn của lưu lượng không mong muốn, bao gồm (nhưng không giới hạn) giao thông từ thiết bị đầu cuối truy cập không phải con người, dịch vụ điện toán đám mây, chương trình gửi thư rác, công cụ cào, vv. Nó làm điều này bằng cách tính toán CIDR có thể các địa chỉ IP cung cấp từ các yêu cầu gửi đến và sau đó cố gắng để phù hợp với những CIDR có thể chống lại các tập tin chữ ký của nó (các tập tin chữ ký chứa danh sách các CIDR các địa chỉ IP coi như là nguồn của lưu lượng không mong muốn); Nếu trận đấu được tìm thấy, các yêu cầu được chặn.

*(Xem: ["CIDR" là gì?](#user-content-WHAT_IS_A_CIDR)).*

BẢN QUYỀN [CIDRAM](https://cidram.github.io/) 2016 và hơn GNU/GPLv2 by [Caleb M (Maikuolan)](https://github.com/Maikuolan).

Bản này là chương trình miễn phí; bạn có thể phân phối lại hoạc sửa đổi dưới điều kiện của GNU Giấy Phép Công Cộng xuất bản bởi Free Software Foundation; một trong giấy phép phần hai, hoạc (tùy theo sự lựa chọn của bạn) bất kỳ phiên bản nào sau này. Bản này được phân phối với hy vọng rằng nó sẽ có hữu ích, nhưng mà KHÔNG CÓ BẢO HÀNH; ngay cả những bảo đảm ngụ ý KHẢ NĂNG BÁN HÀNG hoạc PHÙ HỢP VỚI MỤC ĐÍT VÀO. Hảy xem GNU Giấy Phép Công Cộng để biết them chi tiết, nằm trong tập tin `LICENSE.txt`, và kho chứa của tập tin này có thể tiềm đước tại:
- <https://www.gnu.org/licenses/>.
- <https://opensource.org/licenses/>.

Bạn có thể tải xuống miễn phí CIDRAM từ đây:
- [GitHub](https://github.com/CIDRAM/CIDRAM).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM).

Tài liệu này và nhiều bản dịch khác có thể được tìm thấy tại đây:
- [GitHub](https://github.com/CIDRAM/Docs).
- [Bitbucket](https://bitbucket.org/Maikuolan/cidram-docs).
- [Codeberg](https://codeberg.org/Maikuolan/CIDRAM-Docs).

---


### 2. <a name="SECTION2"></a>CÁCH CÀI ĐẶT

#### 2.0 CÀI ĐẶT THỦ CÔNG

Trước tiên, bạn sẽ cần một bản sao CIDRAM mới. Bạn có thể tải xuống bản lưu trữ của phiên bản CIDRAM mới nhất từ [CIDRAM/CIDRAM](https://github.com/CIDRAM/CIDRAM). Cụ thể, bạn sẽ cần một bản sao mới của thư mục "vault" (mọi thứ khác trong lưu trữ có thể bị xóa hoặc bỏ qua mà không cần lo lắng).

Trước phiên bản v3, cần phải cài đặt CIDRAM ở đâu đó trong gốc công khai của bạn để có thể truy cập front-end CIDRAM. Tuy nhiên, từ phiên bản 3 trở đi, điều đó không cần thiết, và để tối đa bảo mật và ngăn chặn truy cập trái phép vào CIDRAM và các tập tin của nó, thay vào đó, bạn nên cài đặt CIDRAM *bên ngoài* thư mục gốc công khai của bạn. Bạn cài đặt CIDRAM ở đâu không quan trọng, miễn là PHP có thể truy cập nó, nó ở đâu đó an toàn hợp lý, và ở đâu đó bạn hài lòng. Bạn cũng không cần phải duy trì tên của thư mục "vault" nữa, vì vậy bạn có thể đổi tên "vault" thành bất kỳ tên nào bạn muốn (nhưng để thuận tiện, tài liệu sẽ tiếp tục gọi nó là thư mục "vault").

Khi bạn đã sẵn sàng, hãy tải thư mục "vault" lên vị trí bạn đã chọn, và đảm bảo rằng nó có các quyền cần thiết để PHP có thể ghi vào thư mục (tùy thuộc vào hệ thống được đề cập, đôi khi bạn không cần phải làm gì cả, hoặc đôi khi bạn cần đặt CHMOD 755 vào thư mục, hoặc nếu có vấn đề với 755, bạn có thể thử 777, nhưng 777 không được khuyến nghị do kém an toàn hơn).

Tiếp theo, để CIDRAM có thể bảo vệ cơ sở mã hoặc CMS của bạn, bạn cần tạo một "điểm vào". Một điểm vào như vậy bao gồm ba điều:

1. Bao gồm tập tin "loader.php" tại một điểm thích hợp trong cơ sở mã hoặc CMS của bạn.
2. Khởi tạo CIDRAM core.
3. Gọi phương pháp "protect".

Một ví dụ đơn giản:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\Core())->protect();
```

Nếu bạn đang sử dụng máy chủ web Apache và có quyền truy cập vào `php.ini`, bạn có thể sử dụng chỉ thị `auto_prepend_file` để thêm trước CIDRAM bất cứ khi nào có bất kỳ yêu cầu PHP nào. Trong trường hợp như vậy, nơi thích hợp nhất để tạo điểm vào của bạn sẽ nằm trong tập tin của chính nó, và sau đó bạn sẽ trích dẫn tập tin đó tại chỉ thị `auto_prepend_file`.

Ví dụ:

`auto_prepend_file = "/path/to/your/entrypoint.php"`

Hoặc điều này trong tập tin `.htaccess`:

`php_value auto_prepend_file "/path/to/your/entrypoint.php"`

Trong các trường hợp khác, nơi thích hợp nhất để tạo điểm vào của bạn sẽ là điểm sớm nhất có thể trong cơ sở mã hoặc CMS của bạn để luôn được tải bất cứ khi nào ai đó truy cập bất kỳ trang nào trên toàn bộ trang web của bạn. Nếu cơ sở mã của bạn sử dụng một "bootstrap", một ví dụ điển hình sẽ là ở phần đầu của tập tin "bootstrap" của bạn. Nếu cơ sở mã của bạn có một tập tin trung tâm chịu trách nhiệm kết nối với cơ sở dữ liệu của bạn, thì một ví dụ điển hình khác sẽ nằm ở phần đầu của tập tin trung tâm đó.

#### 2.1 CÀI ĐẶT VỚI COMPOSER

[CIDRAM được đăng ký với Packagist](https://packagist.org/packages/cidram/cidram), và như vậy, nếu bạn đã quen với Composer, bạn có thể sử dụng Composer để cài đặt CIDRAM.

`composer require cidram/cidram`

#### 2.2 CÀI ĐẶT CHO WORDPRESS

[CIDRAM được đăng ký như một plugin với cơ sở dữ liệu plugin của WordPress](https://wordpress.org/plugins/cidram/), và bạn có thể cài đặt CIDRAM trực tiếp từ các bảng điều khiển plugin. Bạn có thể cài đặt nó theo cách tương tự như các plugin khác, và không có bước bổ sung được yêu cầu.

*Cảnh báo: Đang nhật CIDRAM qua bảng điều khiển plugin kết quả trong một cài đặt sạch sẽ! Nếu bạn đã tùy chỉnh cài đặt (thay đổi cấu hình của bạn, cài đặt các mô-đun, vv), những tuỳ chỉnh này sẽ bị mất khi đang nhật thông qua bảng điều khiển plugin! Các tập tin đăng nhập cũng sẽ bị mất khi đang nhật thông qua bảng điều khiển plugin! Để bảo vệ các tập tin đăng nhập và tùy chỉnh, đang nhật thông qua trang đang nhật front-end CIDRAM.*

#### 2.3 CẤU HÌNH VÀ TÙY CHỈNH

Bạn nên kiểm tra cấu hình của cài đặt mới để có thể điều chỉnh nó theo nhu cầu của bạn. Bạn cũng có thể muốn cài đặt thêm mô-đun, tập tin chữ ký, tạo quy tắc phụ trợ, hoặc triển khai các tùy chỉnh khác để cài đặt của bạn có thể phù hợp nhất với nhu cầu của bạn. Tôi khuyên bạn nên sử dụng front-end để làm những việc này.

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

#### 4.1 LÀM THẾ NÀO ĐỂ TRUY CẬP FRONT-END.

Tương tự như cách bạn cần tạo một điểm vào để CIDRAM có thể bảo vệ trang web của bạn, bạn cũng sẽ cần tạo một điểm vào để truy cập front-end. Một điểm vào như vậy bao gồm ba điều:

1. Bao gồm tập tin "loader.php" tại một điểm thích hợp trong cơ sở mã hoặc CMS của bạn.
2. Khởi tạo CIDRAM front-end.
3. Gọi phương pháp "view".

Một ví dụ đơn giản:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
(new \CIDRAM\CIDRAM\FrontEnd())->view();
```

Lớp "FrontEnd" mở rộng lớp "Core", có nghĩa là nếu bạn muốn, bạn có thể gọi phương thức "protect" trước khi gọi phương thức "view" để chặn lưu lượng truy cập không mong muốn vào front-end. Làm như vậy là hoàn toàn tùy chọn.

Một ví dụ đơn giản:

```PHP
<?php
require_once '/path/to/the/vault/directory/loader.php';
$CIDRAM = new \CIDRAM\CIDRAM\FrontEnd();
$CIDRAM->protect();
$CIDRAM->view();
```

Nơi tốt nhất để tạo điểm vào cho front-end là trong tập tin chuyên dụng của riêng nó. Không giống như điểm vào đã tạo trước đó, bạn muốn điểm vào front-end của bạn chỉ được truy cập bằng yêu cầu trực tiếp để tập tin cụ thể nơi điểm vào tồn tại, vì vậy trong trường hợp này, bạn sẽ không muốn sử dụng `auto_prepend_file` hoặc `.htaccess`.

Sau khi đã tạo điểm vào front-end, sử dụng trình duyệt của bạn để truy cập nó. Bạn sẽ được hiển thị với một trang đăng nhập. Tại trang đăng nhập, nhập tên người dùng và mật khẩu mặc định (admin/password) rồi nhấn nút đăng nhập.

Chú thích: Sau khi bạn đã đăng nhập lần đầu tiên, để ngăn chặn truy cập trái phép vào các front-end, bạn phải ngay lập tức thay đổi tên người dùng và mật khẩu của bạn! Điều này là rất quan trọng, bởi vì nó có thể tải lên các mã PHP tùy ý để trang web của bạn thông qua các front-end.

Ngoài ra, để bảo mật tối ưu, hãy bật "xác thực hai yếu tố" cho tất cả tài khoản front-end (hướng dẫn được cung cấp bên dưới).

#### 4.2 LÀM THẾ NÀO ĐỂ SỬ DỤNG FRONT-END.

Các hướng dẫn được cung cấp trên mỗi trang của front-end, để giải thích một cách chính xác để sử dụng nó và mục đích của nó. Nếu bạn cần giải thích thêm hay bất kỳ sự hỗ trợ đặc biệt, vui lòng liên hệ hỗ trợ. Cũng thế, có một số video trên YouTube có thể giúp bằng cách viện trợ trực quan.

#### 4.3 2FA (XÁC THỰC HAI YẾU TỐ)

Việc bật xác thực hai yếu tố ("2FA") có thể làm cho front-end an toàn hơn. Khi đăng nhập vào tài khoản có hỗ trợ 2FA, một email sẽ được gửi đến địa chỉ email được liên kết với tài khoản đó. Email này chứa "mã 2FA", mà sau đó người dùng phải nhập, ngoài tên người dùng và mật khẩu, để có thể đăng nhập bằng tài khoản đó. Điều này có nghĩa là việc lấy mật khẩu tài khoản sẽ không đủ cho bất kỳ tin tặc hoặc kẻ tấn công tiềm năng nào có thể đăng nhập vào tài khoản đó, bởi vì họ cũng cần phải có quyền truy cập vào địa chỉ email được liên kết với tài khoản đó để có thể nhận và sử dụng mã 2FA được kết hợp với phiên, do đó làm cho front-end an toàn hơn.

Thứ nhất, để bật xác thực hai yếu tố, sử dụng trang cập nhật front-end để cài đặt thành phần PHPMailer. CIDRAM sử dụng PHPMailer để gửi email.

Sau khi bạn đã cài đặt PHPMailer, bạn sẽ cần điền các chỉ thị cấu hình cho PHPMailer thông qua trang cấu hình CIDRAM hoặc tập tin cấu hình. Thông tin thêm về các chỉ thị cấu hình này được bao gồm trong phần cấu hình của tài liệu này. Sau khi bạn đã điền các chỉ thị cấu hình PHPMailer, hãy đặt `enable_two_factor` thành `true`. Xác thực hai yếu tố bây giờ sẽ được bật.

Tiếp theo, bạn cần liên kết địa chỉ email với tài khoản, để CIDRAM có thể biết nơi gửi mã 2FA khi đăng nhập bằng tài khoản đó. Để thực hiện việc này, hãy sử dụng địa chỉ email làm tên người dùng cho tài khoản (như `foo@bar.tld`), hoặc bao gồm địa chỉ email như một phần của tên người dùng giống như khi gửi email thông thường (như `Foo Bar <foo@bar.tld>`).

Chú thích: Bảo vệ vault của bạn khỏi bị truy cập trái phép (ví dụ, bằng cách tăng cường bảo mật cho máy chủ của bạn và hạn chế quyền truy cập công cộng), là đặc biệt quan trọng ở đây, vì truy cập trái phép vào tập tin cấu hình của bạn (được lưu trữ trong vault của bạn), có thể có nguy cơ phơi bày cài đặt SMTP gửi đi của bạn (bao gồm tên người dùng và mật khẩu SMTP). Bạn nên đảm bảo rằng vault của bạn được bảo mật đúng cách trước khi bật xác thực hai yếu tố. Nếu bạn không thể làm điều này, thì ít nhất, bạn nên tạo một tài khoản email mới, dành riêng cho mục đích này, để giảm thiểu rủi ro liên quan đến các bị phơi bày cài đặt SMTP.

---


### 5. <a name="SECTION5"></a>TÙY CHỌN CHO CẤU HÌNH

Sau đây là danh sách các biến tìm thấy trong tập tin cấu hình cho CIDRAM `config.yml`, cùng với một mô tả về mục đích và chức năng của chúng.

```
Cấu hình (v4)
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

#### "general" (Thể loại)
Cấu hình chung (bất kỳ cấu hình cốt lõi nào không thuộc về các loại khác).

##### "stages" `[string]`
- Điều khiển cho các giai đoạn của chuỗi thực thi (có được bật hay không, có lỗi được ghi lại hay không, vv).

```
stages───[Bật giai đoạn này?]─[Ghi lại bất kỳ lỗi nào được tạo ra trong giai đoạn này?]─[Đếm các vi phạm được tạo ra trong giai đoạn này đối với giám sát IP?]
├─BanCheck ("Kiểm tra xem có bị cấm hay không")
├─Tests ("Thực hiện kiểm tra tập tin chữ ký")
├─Modules ("Thực hiện mô-đun")
├─SearchEngineVerification ("Thực hiện xác minh của máy tìm kiếm")
├─SocialMediaVerification ("Thực hiện xác minh của truyền thông xã hội")
├─OtherVerification ("Thực hiện xác minh khác")
├─Aux ("Thực hiện quy tắc phụ trợ")
├─Tracking ("Thực hiện giám sát IP")
├─RL ("Thực hiện giới hạn tốc độ")
├─CAPTCHA ("Triển khai CAPTCHA (yêu cầu bị chặn)")
├─Reporting ("Thực hiện báo cáo")
├─Statistics ("Cập nhật số liệu thống kê")
├─Webhooks ("Thực hiện webhook")
├─TriggerNotifications ("Xử lý hàng đợi thông báo kích hoạt email")
├─PrepareFields ("Chuẩn bị các trường cho đầu ra và nhật ký")
├─Output ("Tạo đầu ra (yêu cầu bị chặn)")
├─WriteLogs ("Ghi vào nhật ký (yêu cầu bị chặn)")
├─Terminate ("Chấm dứt yêu cầu (yêu cầu bị chặn)")
├─AuxRedirect ("Chuyển hướng theo các quy tắc phụ trợ")
└─NonBlockedCAPTCHA ("Triển khai CAPTCHA (yêu cầu không bị chặn)")
```

##### "fields" `[string]`
- Điều khiển cho các trường trong các sự kiện chặn (khi một yêu cầu bị chặn).

```
fields───[Trường này có nên xuất hiện trong các mục nhập nhật ký không?]─[Trường này có nên xuất hiện trên trang "truy cập đã bị từ chối" không?]─[Bỏ qua trường này khi nó trống?]
├─ID ("ID")
├─ScriptIdent ("Phiên bản kịch bản")
├─DateTime ("Ngày/Thời gian")
├─IPAddr ("Địa chỉ IP")
├─IPAddrResolved ("Địa chỉ IP (giải quyết)")
├─Query ("Truy vấn")
├─Referrer ("Trang giới thiệu")
├─UA ("Đại lý người dùng")
├─UALC ("Đại lý người dùng (chữ thường)")
├─SignatureCount ("Số lượng chữ ký")
├─Signatures ("Tham khảo cho chữ ký")
├─WhyReason ("Tại sao bị chặn")
├─ReasonMessage ("Tại sao bị chặn (chi tiết hơn)")
├─rURI ("URI được xây dựng lại")
├─Infractions ("Vi phạm")
├─ASNLookup ("** Tra cứu ASN")
├─CCLookup ("** Tra cứu mã quốc gia")
├─Verified ("Xác minh danh tính")
├─Expired ("Đã hết hạn")
├─Ignored ("Bị bỏ qua")
├─Request_Method ("Phương thức yêu cầu")
├─Protocol ("Giao thức")
├─SEC_CH_UA_PLATFORM ("!! SEC_CH_UA_PLATFORM")
├─SEC_CH_UA_MOBILE ("!! SEC_CH_UA_MOBILE")
├─SEC_CH_UA ("!! SEC_CH_UA")
├─Hostname ("Tên máy chủ")
├─CAPTCHA ("Tình trạng CAPTCHA")
├─Inspection ("* Kiểm tra điều kiện")
└─ClientL10NAccepted ("Giải quyết ngôn ngữ")
```

* Chỉ dành cho việc gỡ lỗi các quy tắc phụ trợ. Không hiển thị cho người dùng bị chặn.

** Yêu cầu chức năng tra cứu ASN (v.d., thông qua mô-đun IP-API hoặc BGPView).

!! Đây là gợi ý khách hàng có entropy thấp. Gợi ý khách hàng là một công nghệ web thử nghiệm mới, chưa được hỗ trợ rộng rãi trên tất cả các trình duyệt và khách hàng lớn. *Nhìn thấy: <a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA#browser_compatibility" dir="ltr" hreflang="en-US" rel="noopener noreferrer external">Sec-CH-UA - HTTP | MDN</a>.* Mặc dù gợi ý khách hàng có thể hữu ích cho việc lấy dấu vân tay, vì chúng không được hỗ trợ rộng rãi, không nên giả định hay dựa vào sự hiện diện của chúng trong các yêu cầu (tức là, chặn dựa trên sự vắng mặt của họ là một ý tưởng tồi).

##### "timezone" `[string]`
- Điều này được sử dụng để chỉ định múi giờ sử dụng (ví dụ, Africa/Cairo, America/New_York, Asia/Tokyo, Australia/Perth, Europe/Berlin, Pacific/Guam, vv). Chỉ định "SYSTEM" để cho phép PHP tự động xử lý việc này cho bạn.

```
timezone
├─SYSTEM ("Sử dụng múi giờ mặc định của hệ thống.")
├─UTC ("UTC")
└─…Khác
```

##### "time_offset" `[int]`
- Múi giờ bù đắp trong phút.

##### "time_format" `[string]`
- Định dạng ngày/giờ tháng sử dụng bởi CIDRAM. Tùy chọn bổ sung có thể được bổ sung theo yêu cầu.

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
└─…Khác
```

__*Phần giữ chỗ – Giải trình – Ví dụ dựa trên 2024-04-30T18:27:49+08:00.*__<br />
`{yyyy}` – Năm – Ví dụ, 2024.<br />
`{yy}` – Năm viết tắt – Ví dụ, 24.<br />
`{Mon}` – Tên viết tắt của tháng (bằng tiếng Anh) – Ví dụ, Apr.<br />
`{mm}` – Tháng với số 0 đứng đầu – Ví dụ, 04.<br />
`{m}` – Tháng – Ví dụ, 4.<br />
`{Day}` – Tên viết tắt của ngày (bằng tiếng Anh) – Ví dụ, Tue.<br />
`{dd}` – Ngày với số 0 đứng đầu – Ví dụ, 30.<br />
`{d}` – Ngày – Ví dụ, 30.<br />
`{hh}` – Giờ với số 0 đứng đầu (sử dụng thời gian 24 giờ) – Ví dụ, 18.<br />
`{h}` – Giờ (sử dụng thời gian 24 giờ) – Ví dụ, 18.<br />
`{ii}` – Phút với số 0 đứng đầu – Ví dụ, 27.<br />
`{i}` – Phút – Ví dụ, 27.<br />
`{ss}` – Giây với số 0 đứng đầu – Ví dụ, 49.<br />
`{s}` – Giây – Ví dụ, 49.<br />
`{tz}` – Múi giờ (không có dấu hai chấm) – Ví dụ, +0800.<br />
`{t:z}` – Múi giờ (có dấu hai chấm) – Ví dụ, +08:00.

##### "ipaddr" `[string]`
- Nơi để tìm địa chỉ IP của các yêu cầu kết nối? (Hữu ích cho các dịch vụ như Cloudflare). Mặc định = REMOTE_ADDR. CẢNH BÁO: Không thay đổi này, trừ khi bạn biết những gì bạn đang làm!

```
ipaddr
├─HTTP_INCAP_CLIENT_IP ("HTTP_INCAP_CLIENT_IP (Incapsula)")
├─HTTP_CF_CONNECTING_IP ("HTTP_CF_CONNECTING_IP (Cloudflare)")
├─CF-Connecting-IP ("CF-Connecting-IP (Cloudflare)")
├─HTTP_X_FORWARDED_FOR ("HTTP_X_FORWARDED_FOR (Cloudbric)")
├─X-Forwarded-For ("X-Forwarded-For (Squid)")
├─Forwarded ("Forwarded")
├─REMOTE_ADDR ("REMOTE_ADDR (Mặc định)")
└─…Khác
```

Xem thêm:
- [NGINX Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [Squid configuration directive forwarded_for](http://www.squid-cache.org/Doc/config/forwarded_for/)
- [Forwarded - HTTP \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Forwarded)

##### "http_response_header_code" `[int]`
- Những gì thông báo trạng thái HTTP mà CIDRAM nên gửi khi yêu cầu bị chặn?

```
http_response_header_code───[Mặc định]─[Pháp lý]─[Bị cấm]
├─200 (200 OK): Không mạnh mẽ, nhưng thân thiện với người dùng nhất. Các
│ yêu cầu tự động rất có thể sẽ diễn giải phản hồi này
│ là dấu hiệu cho thấy yêu cầu đã thành công. Được khuyến
│ khích cho các yêu cầu không bị chặn.
├─403 (403 Forbidden (Bị cấm)): Hơi mạnh mẽ, và thân thiện với người dùng. Được khuyến
│ khích cho hầu hết các trường hợp chung.
├─410 (410 Gone (Đã biến mất)): Có thể gây ra sự cố khi giải quyết các sai tích cực, vì
│ một số trình duyệt sẽ lưu vào bộ nhớ cache thông báo
│ trạng thái này và không gửi các yêu cầu tiếp theo, ngay cả
│ khi đã được bỏ chặn. Có thể thích hợp nhất trong một
│ số ngữ cảnh, đối với một số loại lưu lượng truy cập
│ nhất định.
├─418 (418 I'm a teapot (Tôi là một ấm trà)): Điều này đề cập đến một trò đùa ngày cá tháng tư (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Rất khó có thể
│ được hiểu bởi bất kỳ ứng dụng khách, bot, trình duyệt,
│ hoặc cách nào khác. Được cung cấp để giải trí và tiện
│ lợi, nhưng thường không được khuyến khích.
├─451 (451 Unavailable For Legal Reasons (Không có sẵn vì lý do pháp lý)): Được khuyến khích khi chặn chủ yếu vì lý do pháp lý. Không
│ được khuyến khích trong các ngữ cảnh khác.
└─503 (503 Service Unavailable (Dịch vụ không sẵn có)): Mạnh mẽ nhất, nhưng không thân thiện với người dùng.
  Được khuyến khích khi bị tấn công, hoặc khi xử lý lưu
  lượng truy cập không mong muốn và cực kỳ dai dẳng.
```

__1.__ Khi "chế độ im lặng" có hiệu lực, thông báo trạng thái HTTP được xác định bởi `general➡silent_mode_response_header_code` sẽ được sử dụng (thông báo này có mức độ ưu tiên cao nhất).

__2.__ Khi thực thể yêu cầu bị cấm do vượt quá giới hạn vi phạm, thông báo trạng thái HTTP "bị cấm" sẽ được sử dụng.

__3.__ Khi bị chặn do giới hạn tốc độ, 429 sẽ được sử dụng, hoặc khi bị chặn do xung đột tài nguyên, thông báo trạng thái HTTP được xác định bởi `signatures➡conflict_response` sẽ được sử dụng (giới hạn tốc độ và xung đột tài nguyên có mức độ ưu tiên ngang nhau trong bối cảnh này).

__4.__ Khi bị chặn do quy tắc phụ trợ đặt "ghi đè mã trạng thái HTTP", ghi đè mã trạng thái HTTP đó sẽ được sử dụng.

__5.__ Khi bị chặn do nghĩa vụ pháp lý (tức là, khi bị chặn do chữ ký tùy chỉnh sử dụng từ viết tắt "pháp lý"), thông báo trạng thái HTTP cho "pháp lý" sẽ được sử dụng.

__6.__ Đối với tất cả các yêu cầu bị chặn khác, thông báo trạng thái HTTP cho "mặc định" sẽ được sử dụng (thông báo này có mức độ ưu tiên thấp nhất).

##### "silent_mode" `[string]`
- CIDRAM nên âm thầm chuyển hướng cố gắng truy cập bị chặn thay vì hiển thị trang "Truy cập đã bị từ chối"? Nếu vâng, xác định vị trí để chuyển hướng cố gắng truy cập bị chặn để. Nếu không, để cho biến này được trống.

##### "silent_mode_response_header_code" `[int]`
- Những gì thông báo trạng thái HTTP mà CIDRAM nên gửi khi âm thầm chuyển hướng các nỗ lực truy cập bị chặn?

```
silent_mode_response_header_code
├─301 (301 Moved Permanently (Đã di chuyển vĩnh viễn)): Hướng dẫn khách hàng rằng chuyển hướng là VĨNH VIỄN, và
│ rằng phương thức yêu cầu được sử dụng cho chuyển hướng
│ CÓ THỂ khác với phương thức yêu cầu được sử dụng cho
│ yêu cầu ban đầu.
├─302 (302 Found (Tìm thấy)): Hướng dẫn khách hàng rằng chuyển hướng là TẠM THỜI, và
│ rằng phương thức yêu cầu được sử dụng cho chuyển hướng
│ CÓ THỂ khác với phương thức yêu cầu được sử dụng cho
│ yêu cầu ban đầu.
├─307 (307 Temporary Redirect (Chuyển hướng tạm thời)): Hướng dẫn khách hàng rằng chuyển hướng là TẠM THỜI, và
│ rằng phương thức yêu cầu được sử dụng cho chuyển hướng
│ có thể KHÔNG khác với phương thức yêu cầu được sử dụng
│ cho yêu cầu ban đầu.
└─308 (308 Permanent Redirect (Chuyển hướng vĩnh viễn)): Hướng dẫn khách hàng rằng chuyển hướng là VĨNH VIỄN, và
  rằng phương thức yêu cầu được sử dụng cho chuyển hướng
  có thể KHÔNG khác với phương thức yêu cầu được sử dụng
  cho yêu cầu ban đầu.
```

Bất kể chúng tôi hướng dẫn khách hàng như thế nào, điều quan trọng cần nhớ là cuối cùng chúng tôi không kiểm soát được những gì khách hàng chọn làm, và không có gì đảm bảo rằng khách hàng sẽ tôn trọng hướng dẫn của chúng tôi.

##### "lang" `[string]`
- Xác định tiếng mặc định cho CIDRAM.

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
- Bản địa hóa theo HTTP_ACCEPT_LANGUAGE bất cứ khi nào có thể? True = Vâng [Mặc định]; False = Không.

##### "numbers" `[string]`
- Làm thế nào để bạn thích số được hiển thị? Chọn ví dụ có vẻ chính xác nhất cho bạn.

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
- Nếu bạn muốn, bạn có thể cung cấp một địa chỉ email ở đây để được trao cho người dùng khi họ đang bị chặn, cho họ để sử dụng như một điểm tiếp xúc cho hỗ trợ hay giúp đở cho trong trường hợp họ bị chặn bởi nhầm hay lỗi. CẢNH BÁO: Bất kỳ địa chỉ email mà bạn cung cấp ở đây sẽ chắc chắn nhất được mua lại bởi chương trình thư rác và cái nạo trong quá trình con của nó được sử dụng ở đây, và như vậy, nó khuyên rằng nếu bạn chọn để cung cấp một địa chỉ email ở đây, mà bạn đảm bảo rằng địa chỉ email bạn cung cấp ở đây là một địa chỉ dùng một lần hay một địa chỉ mà bạn không nhớ được thư rác (nói cách khác, có thể bạn không muốn sử dụng một cá nhân chính hay kinh doanh chính địa chỉ email).

##### "emailaddr_display_style" `[string]`
- Bạn muốn địa chỉ email được trình bày như thế nào với người dùng?

```
emailaddr_display_style
├─default ("Liên kết có thể nhấp")
└─noclick ("Văn bản không thể nhấp")
```

##### "default_dns" `[string]`
- Danh sách các máy chủ DNS để sử dụng cho tra cứu tên máy. CẢNH BÁO: Không thay đổi này, trừ khi bạn biết những gì bạn đang làm!

__Câu hỏi thường gặp.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.vi.md#những-gì-tôi-có-thể-sử-dụng-cho-default_dns" hreflang="vi-VN">Những gì tôi có thể sử dụng cho "default_dns"?</a>*

##### "default_algo" `[string]`
- Xác định thuật toán nào sẽ sử dụng cho tất cả các mật khẩu và phiên trong tương lai.

```
default_algo
├─PASSWORD_DEFAULT ("PASSWORD_DEFAULT")
├─PASSWORD_BCRYPT ("PASSWORD_BCRYPT")
├─PASSWORD_ARGON2I ("PASSWORD_ARGON2I")
└─PASSWORD_ARGON2ID ("PASSWORD_ARGON2ID (PHP >= 7.3.0)")
```

##### "statistics" `[string]`
- Kiểm soát thông tin thống kê cần giám sát.

```
statistics───[IPv4]─[IPv6]─[Khác]
├─Blocked ("Yêu cầu bị chặn")
├─Banned ("Yêu cầu bị cấm")
├─Passed ("Yêu cầu được phép")
├─ReportOK ("Các yêu cầu được báo cáo cho các API bên ngoài – OK")
└─ReportFailed ("Các yêu cầu được báo cáo cho các API bên ngoài – Thất bại")
```

Lưu ý: Giám sát thống kê cho các quy tắc phụ trợ có thể được kiểm soát từ trang quy tắc phụ trợ.

##### "statistics_captchas" `[string]`
- Kiểm soát thông tin thống kê cần giám sát cho CAPTCHA.

```
statistics_captchas───[Thất bại]─[Thành công]─[Đã phục vụ]
├─HCaptcha ("hCaptcha")
├─FriendlyCaptcha ("Friendly Captcha")
└─CloudflareTurnstile ("Cloudflare Turnstile")
```

Lưu ý: Giám sát thống kê cho các quy tắc phụ trợ có thể được kiểm soát từ trang quy tắc phụ trợ.

##### "force_hostname_lookup" `[bool]`
- Thực hiện tìm kiếm tên máy chủ cho tất cả các yêu cầu? True = Vâng; False = Không [Mặc định]. Tìm kiếm tên máy chủ thường được thực hiện trên cơ sở cần thiết, nhưng có thể được thực hiện cho tất cả các yêu cầu. Điều này có thể hữu ích như một phương tiện cung cấp thông tin chi tiết hơn trong các tập tin đăng nhập, nhưng cũng có thể có tác động tiêu cực đến hiệu suất.

##### "allow_gethostbyaddr_lookup" `[bool]`
- Cho phép tra cứu gethostbyaddr khi UDP không khả dụng? True = Vâng [Mặc định]; False = Không.

Lưu ý: Tra cứu IPv6 có thể không hoạt động chính xác trên một số hệ thống 32 bit.

##### "disabled_channels" `[string]`
- Điều này có thể được sử dụng để ngăn CIDRAM sử dụng các kênh cụ thể khi gửi yêu cầu (ví dụ, khi cập nhật, khi lấy siêu dữ liệu thành phần, vv).

```
disabled_channels
├─GitHub ("<span class="origin bgHRdBl">US</span> GitHub")
├─BitBucket ("<span class="origin bgHRdBl">US</span> BitBucket")
├─Codeberg ("<span class="origin bgVBkRd fgYlw">DE</span> Codeberg")
└─GoogleDNS ("<span class="origin bgHRdBl">US</span> GoogleDNS")
```

##### "request_proxy" `[string]`
- Nếu bạn muốn yêu cầu được gửi thông qua proxy, hãy chỉ định proxy đó tại đây. Nếu không, hãy để trống mục này.

##### "request_proxyauth" `[string]`
- Nếu gửi yêu cầu thông qua proxy và nếu proxy đó yêu cầu tên người dùng và mật khẩu, hãy chỉ định tên người dùng và mật khẩu đó tại đây (ví dụ, `user:pass`). Nếu không, hãy để trống mục này.

##### "default_timeout" `[int]`
- Thời gian chờ mặc định để sử dụng cho các yêu cầu bên ngoài? Mặc định = 12 giây.

##### "sensitive" `[string]`
- Một danh sách các đường dẫn được coi là các trang nhạy cảm. Mỗi đường dẫn được liệt kê sẽ, khi cần, được kiểm tra dựa trên URI được xây dựng lại. Một đường dẫn bắt đầu bằng dấu gạch chéo lên phía trước sẽ được coi là một nghĩa đen, và được so khớp từ thành phần đường dẫn của yêu cầu trở đi. Mặt khác, một đường dẫn bắt đầu bằng một ký tự không phải chữ và số, và kết thúc bằng cùng ký tự đó (hoặc cùng ký tự đó cộng với "i") sẽ được coi là biểu thức chính quy. Bất kỳ loại đường dẫn nào khác sẽ được coi là theo nghĩa đen, và có thể khớp từ bất kỳ phần nào của URI. Việc một đường dẫn có được coi là một trang nhạy cảm hay không có thể ảnh hưởng đến cách một số mô-đun hoạt động, nhưng không có bất kỳ ảnh hưởng nào khác.

##### "email_notification_address" `[string]`
- Nếu bạn đã chọn nhận thông báo từ CIDRAM qua email, ví dụ, khi các quy tắc phụ trợ cụ thể được kích hoạt, bạn có thể chỉ định địa chỉ người nhận cho những thông báo đó tại đây.

##### "email_notification_name" `[string]`
- Nếu bạn đã chọn nhận thông báo từ CIDRAM qua email, ví dụ, khi các quy tắc phụ trợ cụ thể được kích hoạt, bạn có thể chỉ định tên người nhận cho những thông báo đó tại đây.

##### "email_notification_when" `[string]`
- Khi nào gửi thông báo sau khi được tạo.

```
email_notification_when
├─Immediately ("Ngay lập tức.")
├─After24Hours ("Sau 24 giờ, được đóng gói lại với nhau (hoặc khi được kích hoạt thủ công, ví dụ, thông qua cron).")
└─ManuallyOnly ("Chỉ khi được kích hoạt thủ công (ví dụ, thông qua cron).")
```

#### "components" (Thể loại)
Cấu hình để kích hoạt và vô hiệu hóa các thành phần được sử dụng bởi CIDRAM. Thường được điền bởi trang cập nhật, nhưng cũng có thể được quản lý từ đây để kiểm soát tốt hơn và cho các thành phần tùy chỉnh không được công nhận bởi trang cập nhật.

##### "ipv4" `[string]`
- Tập tin chữ ký IPv4.

##### "ipv6" `[string]`
- Tập tin chữ ký IPv6.

##### "modules" `[string]`
- Mô-đun.

##### "imports" `[string]`
- Nhập khẩu. Thường được sử dụng để cung cấp thông tin cấu hình của một thành phần cho CIDRAM.

##### "events" `[string]`
- Trình xử lý sự kiện. Thường được sử dụng để sửa đổi cách CIDRAM hoạt động trong nội bộ hoặc để cung cấp chức năng bổ sung.

#### "logging" (Thể loại)
Cấu hình liên quan đến ghi nhật ký (cái có thể áp dụng cho các danh mục khác bị loại trừ).

##### "standard_log" `[string]`
- Tập tin có thể đọc con người cho ghi tất cả các nỗ lực truy cập bị chặn. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

Lời khuyên hữu ích: Bạn có thể đính kèm thông tin ngày/giờ vào tên của tập tin nhật ký bằng cách sử dụng phần giữ chỗ định dạng thời gian. Phần giữ chỗ định dạng thời gian có sẵn được hiển thị tại <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "apache_style_log" `[string]`
- Tập tin Apache phong cách cho ghi tất cả các nỗ lực truy cập bị chặn. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

Lời khuyên hữu ích: Bạn có thể đính kèm thông tin ngày/giờ vào tên của tập tin nhật ký bằng cách sử dụng phần giữ chỗ định dạng thời gian. Phần giữ chỗ định dạng thời gian có sẵn được hiển thị tại <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "serialised_log" `[string]`
- Tập tin tuần tự cho ghi tất cả các nỗ lực truy cập bị chặn. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

Lời khuyên hữu ích: Bạn có thể đính kèm thông tin ngày/giờ vào tên của tập tin nhật ký bằng cách sử dụng phần giữ chỗ định dạng thời gian. Phần giữ chỗ định dạng thời gian có sẵn được hiển thị tại <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "error_log" `[string]`
- Một tập tin để ghi lại bất kỳ lỗi không nghiêm trọng được phát hiện. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

Lời khuyên hữu ích: Bạn có thể đính kèm thông tin ngày/giờ vào tên của tập tin nhật ký bằng cách sử dụng phần giữ chỗ định dạng thời gian. Phần giữ chỗ định dạng thời gian có sẵn được hiển thị tại <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "outbound_request_log" `[string]`
- Một tập tin để ghi nhật ký kết quả của bất kỳ yêu cầu gửi đi nào. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

Lời khuyên hữu ích: Bạn có thể đính kèm thông tin ngày/giờ vào tên của tập tin nhật ký bằng cách sử dụng phần giữ chỗ định dạng thời gian. Phần giữ chỗ định dạng thời gian có sẵn được hiển thị tại <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "report_log" `[string]`
- Một tập tin để ghi lại bất kỳ báo cáo nào được gửi đến các API bên ngoài. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

Lời khuyên hữu ích: Bạn có thể đính kèm thông tin ngày/giờ vào tên của tập tin nhật ký bằng cách sử dụng phần giữ chỗ định dạng thời gian. Phần giữ chỗ định dạng thời gian có sẵn được hiển thị tại <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "truncate" `[string]`
- Dọn dẹp các bản ghi khi họ được một kích thước nhất định? Giá trị là kích thước tối đa bằng B/KB/MB/GB/TB mà một tập tin bản ghi có thể tăng lên trước khi bị dọn dẹp. Giá trị mặc định 0KB sẽ vô hiệu hoá dọn dẹp (các bản ghi có thể tăng lên vô hạn). Lưu ý: Áp dụng cho tập tin riêng biệt! Kích thước tập tin bản ghi không được coi là tập thể.

##### "log_rotation_limit" `[int]`
- Xoay vòng nhật ký giới hạn số lượng của tập tin nhật ký có cần tồn tại cùng một lúc. Khi các tập tin nhật ký mới được tạo, nếu tổng số lượng tập tin nhật ký vượt quá giới hạn được chỉ định, hành động được chỉ định sẽ được thực hiện. Bạn có thể chỉ định giới hạn mong muốn tại đây. Giá trị 0 sẽ vô hiệu hóa xoay vòng nhật ký.

##### "log_rotation_action" `[string]`
- Xoay vòng nhật ký giới hạn số lượng của tập tin nhật ký có cần tồn tại cùng một lúc. Khi các tập tin nhật ký mới được tạo, nếu tổng số lượng tập tin nhật ký vượt quá giới hạn được chỉ định, hành động được chỉ định sẽ được thực hiện. Bạn có thể chỉ định hành động mong muốn tại đây.

```
log_rotation_action
├─Delete ("Xóa các tập tin nhật ký cũ nhất, cho đến khi giới hạn không còn vượt quá.")
└─Archive ("Trước tiên lưu trữ, và sau đó xóa các tập tin nhật ký cũ nhất, cho đến khi giới hạn không còn vượt quá.")
```

##### "log_banned_ips" `[bool]`
- Bao gồm các yêu cầu bị chặn từ các IP bị cấm trong các tập tin đăng nhập? True = Vâng [Mặc định]; False = Không.

##### "log_sanitisation" `[bool]`
- Khi sử dụng trang bản ghi để xem dữ liệu bản ghi, CIDRAM vệ sinh dữ liệu bản ghi trước khi hiển thị nó, để bảo vệ người dùng khỏi các cuộc tấn công XSS và các mối đe dọa tiềm năng khác. Tuy nhiên, theo mặc định, dữ liệu không được vệ sinh trong quá ghi bản ghi. Điều này là để đảm bảo dữ liệu bản ghi được bảo quản chính xác, để hỗ trợ bất kỳ phân tích heuristic hoặc pháp y có thể cần thiết trong tương lai. Tuy nhiên, nếu người dùng cố gắng đọc dữ liệu bản ghi bằng các công cụ bên ngoài, và nếu những công cụ bên ngoài đó không thực hiện quy trình vệ sinh riêng của họ, người dùng có thể tiếp xúc với các cuộc tấn công XSS. Nếu cần, bạn có thể thay đổi hành vi mặc định bằng cách sử dụng chỉ thị cấu hình này. True = Vệ sinh dữ liệu khi ghi nó (dữ liệu được bảo quản ít chính xác hơn, nhưng rủi ro XSS thấp hơn). False = Không vệ sinh dữ liệu khi ghi nó (dữ liệu được bảo quản chính xác hơn, nhưng rủi ro XSS cao hơn) [Mặc định].

#### "frontend" (Thể loại)
Cấu hình cho front-end.

##### "frontend_log" `[string]`
- Tập tin cho ghi cố gắng đăng nhập front-end. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

Lời khuyên hữu ích: Bạn có thể đính kèm thông tin ngày/giờ vào tên của tập tin nhật ký bằng cách sử dụng phần giữ chỗ định dạng thời gian. Phần giữ chỗ định dạng thời gian có sẵn được hiển thị tại <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "signatures_update_event_log" `[string]`
- Một tập tin để ghi nhật ký khi chữ ký được cập nhật qua front-end. Chỉ định một tên tập tin, hoặc để trống để vô hiệu hóa.

Lời khuyên hữu ích: Bạn có thể đính kèm thông tin ngày/giờ vào tên của tập tin nhật ký bằng cách sử dụng phần giữ chỗ định dạng thời gian. Phần giữ chỗ định dạng thời gian có sẵn được hiển thị tại <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

##### "max_login_attempts" `[int]`
- Số lượng tối đa cố gắng đăng nhập front-end. Mặc định = 5.

##### "theme" `[string]`
- Chủ đề sẽ được sử dụng cho front-end.

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
└─…Khác
```

##### "theme_mode" `[string]`
- Chế độ cho chủ đề sẽ được sử dụng cho front-end.

```
theme_mode
├─normal ("Bình thường")
└─inverted ("Nghịch đảo")
```

##### "magnification" `[float]`
- Phóng to phông chữ. Mặc định = 1.

##### "custom_header" `[string]`
- Được chèn dưới dạng HTML ở đầu tất cả các trang front-end. Điều này có thể hữu ích trong trường hợp bạn muốn bao gồm biểu trưng trang web, tiêu đề được cá nhân hóa, tập lệnh, hoặc tương tự ở tất cả các trang như vậy.

##### "custom_footer" `[string]`
- Được chèn dưới dạng HTML ở cuối tất cả các trang front-end. Điều này có thể hữu ích trong trường hợp bạn muốn bao gồm thông báo pháp lý, liên kết liên hệ, thông tin doanh nghiệp, hoặc tương tự ở tất cả các trang như vậy.

##### "remotes" `[string]`
- Danh sách các địa chỉ được trình cập nhật sử dụng để tìm nạp siêu dữ liệu thành phần. Điều này có thể cần được điều chỉnh khi nâng cấp lên phiên bản chính mới, hoặc khi tìm một nguồn mới để cập nhật, nhưng trong các trường hợp bình thường thì nên để nguyên.

##### "enable_two_factor" `[bool]`
- Chỉ thị này xác định có nên sử dụng 2FA cho tài khoản front-end hay không.

#### "signatures" (Thể loại)
Cấu hình cho chữ ký, tập tin chữ ký, mô-đun, vv.

##### "shorthand" `[string]`
- Kiểm soát những việc cần làm với một yêu cầu khi có sự trùng khớp tích cực với một chữ ký sử dụng các từ viết tắt đã cho.

```
shorthand───[Chặn nó.]─[Hồ sơ nó.]─[Khi bị chặn, đàn áp mẫu đầu ra.]
├─Attacks ("Cuộc tấn công")
├─Bogon ("⁰ IP bogon")
├─Cloud ("Dịch vụ điện toán đám mây")
├─Generic ("Chủng loại")
├─Legal ("¹ Pháp lý")
├─Malware ("Phần mềm độc hại")
├─Proxy ("² Proxy")
├─Spam ("Thư rác")
├─Banned ("³ Bị cấm")
├─BadIP ("³ IP không hợp lệ")
├─RL ("³ Giới hạn tốc độ")
├─Conflict ("³ Xung đột")
└─Other ("⁴ Khác")
```

__0.__ Nếu trang web của bạn cần truy cập qua mạng LAN hoặc localhost, đừng chặn điều này. Nếu không cần, bạn có thể chặn điều này.

__1.__ Không có tập tin chữ ký mặc định nào sử dụng điều này, nhưng nó vẫn được hỗ trợ trong trường hợp nó có thể hữu ích cho một số người dùng.

__2.__ Nếu bạn cần người dùng có thể truy cập trang web của bạn thông qua proxy, đừng chặn điều này. Nếu không cần, bạn có thể chặn điều này.

__3.__ Sử dụng trực tiếp trong chữ ký không được hỗ trợ, nhưng nó có thể được sử dụng bằng các phương tiện khác trong các trường hợp cụ thể.

__4.__ Đề cập đến các trường hợp mà các từ viết tắt hoàn toàn không được sử dụng, hoặc không được nhận dạng bởi CIDRAM.

__Chỉ một cho mỗi chữ ký.__ Một chữ ký có thể gọi nhiều hồ sơ, nhưng chỉ có thể sử dụng một từ viết tắt. Có thể nhiều từ viết tắt có thể thích hợp, nhưng vì chỉ một có thể được sử dụng, chúng tôi luôn hướng tới việc chỉ sử dụng thích hợp nhất.

__Ưu tiên.__ Một tùy chọn được chọn luôn được ưu tiên hơn một tùy chọn không được chọn. Ví dụ, nếu nhiều từ viết tắt có hiệu lực nhưng chỉ một trong số chúng được đặt là bị chặn, yêu cầu sẽ vẫn bị chặn.

__Điểm cuối của con người và dịch vụ điện toán đám mây.__ Dịch vụ điện toán đám mây có thể đề cập đến các nhà cung cấp dịch vụ lưu trữ web, trang trại máy chủ, trung tâm dữ liệu, hoặc một số thứ khác. Điểm cuối của con người đề cập đến phương tiện mà con người truy cập internet, chẳng hạn như bằng cách của một nhà cung cấp dịch vụ internet. Một mạng thường chỉ cung cấp cái này hoặc cái kia, nhưng đôi khi có thể cung cấp cả hai. Chúng tôi mong muốn không bao giờ xác định các điểm cuối tiềm năng của con người là các dịch vụ điện toán đám mây. Do đó, một dịch vụ điện toán đám mây có thể được xác định là một thứ khác nếu phạm vi của nó được chia sẻ bởi các điểm cuối của con người đã biết. Tương tự như vậy, chúng tôi luôn hướng tới xác định các dịch vụ điện toán đám mây, có phạm vi không được chia sẻ bởi bất kỳ điểm cuối của con người nào đã biết, là dịch vụ điện toán đám mây. Do đó, một yêu cầu được xác định rõ ràng là một dịch vụ điện toán đám mây rất có lẽ không chia sẻ phạm vi của nó với bất kỳ điểm cuối của con người nào đã biết. Tương tự như vậy, một yêu cầu được xác định rõ ràng bởi các cuộc tấn công hoặc nguy cơ rác là có lẽ chia sẻ chúng. Tuy nhiên, internet luôn ở trạng thái thay đổi, mục đích của các mạng thay đổi theo thời gian, và các phạm vi luôn được mua hay bán, vì vậy hãy luôn nhận thức và cảnh giác có liên quan đến nguy cơ sai tích cực.

##### "default_tracktime" `[string]`
- Khoảng thời gian mà địa chỉ IP sẽ được giám sát. Mặc định = 7d0°0′0″ (1 tuần).

##### "infraction_limit" `[int]`
- Số lượng tối đa các vi phạm một IP được phép chịu trước khi nó bị cấm bởi các giám sát IP. Mặc định = 10.

##### "tracking_override" `[bool]`
- Cho phép các mô-đun ghi đè các tùy chọn giám sát? True = Vâng [Mặc định]; False = Không.

##### "conflict_response" `[int]`
- Khi có quá nhiều lần thử truy cập cùng một tài nguyên cùng lúc (v.d., yêu cầu đồng thời tới nhiều quy trình PHP trên cùng một máy cho cùng một tài nguyên), một số lần thử đó có thể không thành công. Trong trường hợp hiếm hoi và không chắc xảy ra khi điều này ảnh hưởng đến các tập tin chữ ký hay mô-đun, CIDRAM có thể không đưa ra được quyết định hiệu quả về yêu cầu. Nếu điều này xảy ra, yêu cầu có nên bị chặn không, và CIDRAM nên gửi tin nhắn trạng thái HTTP nào?

```
conflict_response
├─0 (Đừng chặn yêu cầu.): Nếu bạn muốn các yêu cầu chỉ bị chặn khi bạn chắc chắn
│ rằng chúng là ác ý, hoặc thích thận trọng hơn với sai tích
│ cực (với cái giá là thỉnh thoảng có lưu lượng truy cập
│ không mong muốn đi qua), chọn cái này. Nếu bạn muốn yêu cầu
│ bị chặn nếu bạn không chắc chắn chúng là vô hại, hoặc
│ thích giữ cảnh giác (với cái giá là thỉnh thoảng có sai
│ tích cực), chọn một trong những tùy chọn có sẵn khác.
├─409 (409 Conflict (Xung đột)): Được khuyến nghị cho các xung đột tài nguyên (v.d., xung
│ đột hợp nhất, xung đột truy cập tập tin, vv). Không được
│ khuyến khích trong các ngữ cảnh khác.
└─429 (429 Too Many Requests (Quá nhiều yêu cầu)): Được khuyến khích cho giới hạn tốc độ, khi đối phó với
  các cuộc tấn công DDoS, và để ngăn chặn lũ lụt. Không
  được khuyến khích trong các ngữ cảnh khác.
```

#### "verification" (Thể loại)
Cấu hình để xác minh yêu cầu bắt nguồn từ đâu.

##### "search_engines" `[string]`
- Điều khiển cho xác minh các yêu cầu từ các máy tìm kiếm.

```
search_engines───[Cố gắng xác minh?]─[Chặn tiêu cực?]─[Chặn các yêu cầu chưa được xác minh?]─[Cho phép đường tránh một cú đánh?]─[Ngừng giám sát các tích cực?]
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

__"Tích cực" và "tiêu cực" là gì?__ Khi xác minh danh tính được trình bày bởi một yêu cầu, kết quả thành công có thể được mô tả là "tích cực" hoặc "tiêu cực". Trong trường hợp danh tính được trình bày được xác nhận là danh tính thực, danh tính đó sẽ được mô tả là "tích cực". Trong trường hợp danh tính được trình bày được xác nhận là giả mạo, danh tính đó sẽ được mô tả là "tiêu cực". Tuy nhiên, kết quả không thành công (v.d., xác minh không thành công, hoặc không thể xác định tính xác thực của danh tính được trình bày) sẽ không được mô tả là "tích cực" hoặc "tiêu cực". Thay vào đó, một kết quả không thành công sẽ được mô tả đơn giản là chưa được xác minh. Khi không có nỗ lực xác minh danh tính mà một yêu cầu đưa ra được thực hiện, thì yêu cầu đó cũng sẽ được mô tả là chưa được xác minh. Các điều khoản chỉ có ý nghĩa trong bối cảnh mà danh tính được trình bày bởi một yêu cầu được công nhận và do đó, khi có thể xác minh. Trong trường hợp danh tính được trình bày không khớp với các tùy chọn được cung cấp ở trên, hoặc khi không có danh tính nào được trình bày, các tùy chọn được cung cấp ở trên trở nên không liên quan.

__"Đường tránh một cú đánh" là gì?__ Trong một số trường hợp, yêu cầu đã được xác minh tích cực vẫn có thể bị chặn do tập tin chữ ký, mô-đun, hoặc các điều kiện khác của yêu cầu, và đường tránh có thể cần thiết để tránh sai tích cực. Trong trường hợp sai tích cực gây ra chính xác một vi phạm, một đường tránh như vậy có thể được mô tả là "đường tránh một cú đánh".

* Tùy chọn này có một đường tránh tương ứng dưới `bypasses➡used`. Bạn nên đảm bảo rằng hộp kiểm cho đường tránh tương ứng được đánh dấu giống như hộp kiểm để cố gắng xác minh tùy chọn này.

##### "social_media" `[string]`
- Điều khiển cho xác minh các yêu cầu từ các nền tảng truyền thông xã hội.

```
social_media───[Cố gắng xác minh?]─[Chặn tiêu cực?]─[Chặn các yêu cầu chưa được xác minh?]─[Cho phép đường tránh một cú đánh?]─[Ngừng giám sát các tích cực?]
├─Embedly ("* Embedly")
├─Facebook ("** Facebook")
├─Pinterest ("* Pinterest")
├─Snapchat ("* Snapchat")
└─Twitterbot ("*!! Twitterbot")
```

__"Tích cực" và "tiêu cực" là gì?__ Khi xác minh danh tính được trình bày bởi một yêu cầu, kết quả thành công có thể được mô tả là "tích cực" hoặc "tiêu cực". Trong trường hợp danh tính được trình bày được xác nhận là danh tính thực, danh tính đó sẽ được mô tả là "tích cực". Trong trường hợp danh tính được trình bày được xác nhận là giả mạo, danh tính đó sẽ được mô tả là "tiêu cực". Tuy nhiên, kết quả không thành công (v.d., xác minh không thành công, hoặc không thể xác định tính xác thực của danh tính được trình bày) sẽ không được mô tả là "tích cực" hoặc "tiêu cực". Thay vào đó, một kết quả không thành công sẽ được mô tả đơn giản là chưa được xác minh. Khi không có nỗ lực xác minh danh tính mà một yêu cầu đưa ra được thực hiện, thì yêu cầu đó cũng sẽ được mô tả là chưa được xác minh. Các điều khoản chỉ có ý nghĩa trong bối cảnh mà danh tính được trình bày bởi một yêu cầu được công nhận và do đó, khi có thể xác minh. Trong trường hợp danh tính được trình bày không khớp với các tùy chọn được cung cấp ở trên, hoặc khi không có danh tính nào được trình bày, các tùy chọn được cung cấp ở trên trở nên không liên quan.

__"Đường tránh một cú đánh" là gì?__ Trong một số trường hợp, yêu cầu đã được xác minh tích cực vẫn có thể bị chặn do tập tin chữ ký, mô-đun, hoặc các điều kiện khác của yêu cầu, và đường tránh có thể cần thiết để tránh sai tích cực. Trong trường hợp sai tích cực gây ra chính xác một vi phạm, một đường tránh như vậy có thể được mô tả là "đường tránh một cú đánh".

* Tùy chọn này có một đường tránh tương ứng dưới `bypasses➡used`. Bạn nên đảm bảo rằng hộp kiểm cho đường tránh tương ứng được đánh dấu giống như hộp kiểm để cố gắng xác minh tùy chọn này.

** Yêu cầu chức năng tra cứu ASN (v.d., thông qua mô-đun IP-API hoặc BGPView).

*!! Khả năng cao gây ra sai tích cực do iMessage.

##### "other" `[string]`
- Điều khiển cho xác minh các loại yêu cầu khác nếu có thể.

```
other───[Cố gắng xác minh?]─[Chặn tiêu cực?]─[Chặn các yêu cầu chưa được xác minh?]─[Cho phép đường tránh một cú đánh?]─[Ngừng giám sát các tích cực?]
├─AdSense ("AdSense")
├─AmazonAdBot ("* AmazonAdBot")
├─ChatGPT-User ("!! ChatGPT-User")
├─GPTBot ("!! GPTBot")
├─OAI-SearchBot ("!! OAI-SearchBot")
└─UptimeRobot ("UptimeRobot")
```

__"Tích cực" và "tiêu cực" là gì?__ Khi xác minh danh tính được trình bày bởi một yêu cầu, kết quả thành công có thể được mô tả là "tích cực" hoặc "tiêu cực". Trong trường hợp danh tính được trình bày được xác nhận là danh tính thực, danh tính đó sẽ được mô tả là "tích cực". Trong trường hợp danh tính được trình bày được xác nhận là giả mạo, danh tính đó sẽ được mô tả là "tiêu cực". Tuy nhiên, kết quả không thành công (v.d., xác minh không thành công, hoặc không thể xác định tính xác thực của danh tính được trình bày) sẽ không được mô tả là "tích cực" hoặc "tiêu cực". Thay vào đó, một kết quả không thành công sẽ được mô tả đơn giản là chưa được xác minh. Khi không có nỗ lực xác minh danh tính mà một yêu cầu đưa ra được thực hiện, thì yêu cầu đó cũng sẽ được mô tả là chưa được xác minh. Các điều khoản chỉ có ý nghĩa trong bối cảnh mà danh tính được trình bày bởi một yêu cầu được công nhận và do đó, khi có thể xác minh. Trong trường hợp danh tính được trình bày không khớp với các tùy chọn được cung cấp ở trên, hoặc khi không có danh tính nào được trình bày, các tùy chọn được cung cấp ở trên trở nên không liên quan.

__"Đường tránh một cú đánh" là gì?__ Trong một số trường hợp, yêu cầu đã được xác minh tích cực vẫn có thể bị chặn do tập tin chữ ký, mô-đun, hoặc các điều kiện khác của yêu cầu, và đường tránh có thể cần thiết để tránh sai tích cực. Trong trường hợp sai tích cực gây ra chính xác một vi phạm, một đường tránh như vậy có thể được mô tả là "đường tránh một cú đánh".

* Tùy chọn này có một đường tránh tương ứng dưới `bypasses➡used`. Bạn nên đảm bảo rằng hộp kiểm cho đường tránh tương ứng được đánh dấu giống như hộp kiểm để cố gắng xác minh tùy chọn này.

!! Hầu hết người dùng có thể sẽ muốn điều này bị chặn, bất kể đó là thật hay giả mạo. Điều đó có thể đạt được bằng cách không chọn "cố gắng xác minh" và chọn "chặn các yêu cầu chưa được xác minh". Tuy nhiên, vì một số người dùng có thể muốn xác minh các yêu cầu đó (để chặn các yêu cầu tiêu cực trong khi cho phép các yêu cầu tích cực), thay vì chặn các yêu cầu đó thông qua các mô-đun, các tùy chọn để xử lý các yêu cầu đó được cung cấp tại đây.

##### "adjust" `[string]`
- Điều khiển cho các điều chỉnh các tính năng khác trong bối cảnh xác minh.

```
adjust───[Đàn áp hCaptcha]─[Đàn áp Friendly Captcha]─[Đàn áp Cloudflare Turnstile]
├─Negatives ("Tiêu cực bị chặn")
└─NonVerified ("Chưa được xác minh bị chặn")
```

#### "captcha" (Thể loại)
Cấu hình cho CAPTCHA (cung cấp một cách để con người lấy lại quyền truy cập khi bị chặn).

##### "usemode" `[int]`
- Khi nào nên cung cấp CAPTCHA? Bạn có thể chỉ định hành vi ưu tiên cho từng nhà cung cấp được hỗ trợ tại đây.

```
usemode───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─0 (Không bao giờ.)
├─1 (Chỉ khi bị chặn, trong giới hạn chữ ký, và không bị cấm.)
├─2 (Chỉ khi bị chặn, được đánh dấu đặc biệt để sử dụng, trong giới hạn chữ ký, và không bị cấm.)
├─3 (Chỉ khi trong giới hạn chữ ký, và không bị cấm (bất kể có bị chặn hay không).)
├─4 (Chỉ khi không bị chặn.)
├─5 (Chỉ khi không bị chặn, hoặc khi được đánh dấu đặc biệt để sử dụng, trong giới hạn chữ ký, và không bị cấm.)
└─6 (Chỉ khi không bị chặn, ở những yêu cầu trang nhạy cảm.)
```

Lưu ý: Các yêu cầu trong danh sách trắng hay đã xác minh và không bị chặn không cần phải hoàn thành CAPTCHA.

Cũng lưu ý: CAPTCHA có thể cung cấp một lớp bảo vệ bổ sung, hữu ích chống lại bot và các loại yêu cầu tự động độc hại khác nhau, nhưng sẽ không cung cấp bất kỳ biện pháp bảo vệ nào chống lại con người độc hại.

Yêu cầu có thể được "đánh dấu để sử dụng" thông qua các quy tắc phụ trợ.

Việc một yêu cầu có được coi là "nhạy cảm" hay không được xác định bởi <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_sensitive">`general➡sensitive`</a>.

"Giới hạn chữ ký" được xác định bởi <a onclick="javascript:toggleconfigNav('captchaRow','captchaShowLink')" href="#config_captcha_signature_limit">`captcha➡signature_limit`</a>.

##### "nonblocked_status_code" `[int]`
- Mã trạng thái nào nên được sử dụng khi hiển thị CAPTCHA cho các yêu cầu không bị chặn?

```
nonblocked_status_code───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─200 (200 OK): Không mạnh mẽ, nhưng thân thiện với người dùng nhất. Các
│ yêu cầu tự động rất có thể sẽ diễn giải phản hồi này
│ là dấu hiệu cho thấy yêu cầu đã thành công. Được khuyến
│ khích cho các yêu cầu không bị chặn.
├─403 (403 Forbidden (Bị cấm)): Hơi mạnh mẽ, và thân thiện với người dùng. Được khuyến
│ khích cho hầu hết các trường hợp chung.
├─418 (418 I'm a teapot (Tôi là một ấm trà)): Điều này đề cập đến một trò đùa ngày cá tháng tư (<a
│ href="https://tools.ietf.org/html/rfc2324" dir="ltr" hreflang="en-US"
│ rel="noopener noreferrer external">RFC 2324</a>). Rất khó có thể
│ được hiểu bởi bất kỳ ứng dụng khách, bot, trình duyệt,
│ hoặc cách nào khác. Được cung cấp để giải trí và tiện
│ lợi, nhưng thường không được khuyến khích.
├─429 (429 Too Many Requests (Quá nhiều yêu cầu)): Được khuyến khích cho giới hạn tốc độ, khi đối phó với
│ các cuộc tấn công DDoS, và để ngăn chặn lũ lụt. Không
│ được khuyến khích trong các ngữ cảnh khác.
└─451 (451 Unavailable For Legal Reasons (Không có sẵn vì lý do pháp lý)): Được khuyến khích khi chặn chủ yếu vì lý do pháp lý. Không
  được khuyến khích trong các ngữ cảnh khác.
```

##### "api" `[string]`
- API nào để sử dụng?

```
api───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─v0 ("v0")
├─v1 ("v1")
├─Invisible ("v1 (Vô hình)")
└─v2 ("v2")
```

##### "messages" `[string]`
- Tin nhắn sẽ được hiển thị cùng với CAPTCHA.

```
messages───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─cookie_warning ("Hiển thị cảnh báo cookie?): Tùy thuộc vào luật bảo mật của quốc gia hoặc tiểu bang
│ của bạn (ví dụ, GDPR/DSGVO ở EU, LGPD ở Brazil, vv), điều này
│ có thể là bắt buộc về mặt pháp lý."
└─api_message ("Hiển thị thông báo API?): Hướng dẫn cho người dùng, phù hợp với API được sử
  dụng, về cách hoàn thành CAPTCHA."
```

##### "lockto" `[string]`
- Khóa CAPTCHA.

```
lockto───[hCaptcha]─[Friendly Captcha]─[Cloudflare Turnstile]
├─ip ("Khóa CAPTCHA vào địa chỉ IP của người dùng hoàn thành CAPTCHA nhưng không phải vào chính người dùng đó.): Cookie KHÔNG được sử dụng để xác định người dùng. Khi
│ quyền truy cập được lấy lại do hoàn thành thành công
│ CAPTCHA, quyền này sẽ áp dụng cho bất kỳ ai kết nối từ
│ cùng một địa chỉ IP."
├─user ("Khóa CAPTCHA đối với người dùng hoàn thành CAPTCHA nhưng không đối với địa chỉ IP của họ.): Cookie được sử dụng để xác định người dùng. Khi quyền
│ truy cập được lấy lại do hoàn thành thành công CAPTCHA,
│ quyền này chỉ áp dụng cho người dùng hoàn thành CAPTCHA và
│ sẽ tồn tại miễn là cookie của họ vẫn còn hiệu lực, ngay
│ cả khi địa chỉ IP của họ thay đổi."
└─both ("Khóa CAPTCHA đối với người dùng hoàn thành CAPTCHA cũng như đối với địa chỉ IP của họ.): Cookie được sử dụng để xác định người dùng. Khi quyền
  truy cập được lấy lại do hoàn thành thành công CAPTCHA,
  quyền này chỉ áp dụng cho người dùng hoàn thành CAPTCHA và
  sẽ không còn hiệu lực nếu địa chỉ IP của họ thay đổi."
```

##### "hcaptcha_sitekey" `[string]`
- Nếu bạn muốn sử dụng hCaptcha với CIDRAM, bạn sẽ cần nhập giá trị vào đây. Nếu không, bạn có thể bỏ qua điều này.

Giá trị này có thể được tìm thấy trong bảng điều khiển cho dịch vụ CAPTCHA của bạn.

Xem thêm:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "hcaptcha_secret" `[string]`
- Nếu bạn muốn sử dụng hCaptcha với CIDRAM, bạn sẽ cần nhập giá trị vào đây. Nếu không, bạn có thể bỏ qua điều này.

Giá trị này có thể được tìm thấy trong bảng điều khiển cho dịch vụ CAPTCHA của bạn.

Xem thêm:
- [HCaptcha Dashboard](https://dashboard.hcaptcha.com/overview)

##### "friendly_sitekey" `[string]`
- Nếu bạn muốn sử dụng Friendly Captcha với CIDRAM, bạn sẽ cần nhập giá trị vào đây. Nếu không, bạn có thể bỏ qua điều này.

Giá trị này có thể được tìm thấy trong bảng điều khiển cho dịch vụ CAPTCHA của bạn.

Xem thêm:
- [Friendly Captcha Dashboard](https://app.friendlycaptcha.eu/dashboard)

##### "friendly_apikey" `[string]`
- Nếu bạn muốn sử dụng Friendly Captcha với CIDRAM, bạn sẽ cần nhập giá trị vào đây. Nếu không, bạn có thể bỏ qua điều này.

Giá trị này có thể được tìm thấy trong bảng điều khiển cho dịch vụ CAPTCHA của bạn.

Xem thêm:
- [Friendly Captcha Dashboard](https://app.friendlycaptcha.eu/dashboard)

##### "turnstile_sitekey" `[string]`
- Nếu bạn muốn sử dụng Cloudflare Turnstile với CIDRAM, bạn sẽ cần nhập giá trị vào đây. Nếu không, bạn có thể bỏ qua điều này.

Giá trị này có thể được tìm thấy trong bảng điều khiển cho dịch vụ CAPTCHA của bạn.

Xem thêm:
- [Cloudflare Dashboard](https://dash.cloudflare.com/)

##### "turnstile_secret" `[string]`
- Nếu bạn muốn sử dụng Cloudflare Turnstile với CIDRAM, bạn sẽ cần nhập giá trị vào đây. Nếu không, bạn có thể bỏ qua điều này.

Giá trị này có thể được tìm thấy trong bảng điều khiển cho dịch vụ CAPTCHA của bạn.

Xem thêm:
- [Cloudflare Dashboard](https://dash.cloudflare.com/)

##### "expiry" `[float]`
- Số giờ để nhớ CAPTCHA. Mặc định = 720 (1 tháng).

##### "signature_limit" `[int]`
- Số lượng chữ ký tối đa được phép trước khi đề nghị CAPTCHA bị rút lại. Mặc định = 1.

##### "log" `[string]`
- Đăng nhập tất cả các nỗ lực cho CAPTCHA? Nếu có, ghi rõ tên để sử dụng cho các tập tin đăng nhập. Nếu không, đốn biến này.

Lời khuyên hữu ích: Bạn có thể đính kèm thông tin ngày/giờ vào tên của tập tin nhật ký bằng cách sử dụng phần giữ chỗ định dạng thời gian. Phần giữ chỗ định dạng thời gian có sẵn được hiển thị tại <a onclick="javascript:toggleconfigNav('generalRow','generalShowLink')" href="#config_general_time_format">`general➡time_format`</a>.

#### "legal" (Thể loại)
Cấu hình cho các yêu cầu pháp lý.

##### "pseudonymise_ip_addresses" `[bool]`
- Pseudonymise địa chỉ IP khi viết các tập tin nhật ký? True = Vâng [Mặc định]; False = Không.

##### "privacy_policy" `[string]`
- Địa chỉ của chính sách bảo mật liên quan được hiển thị ở chân trang của bất kỳ trang nào được tạo. Chỉ định URL, hoặc để trống để vô hiệu hóa.

#### "template_data" (Thể loại)
Cấu hình cho mẫu và chủ đề.

##### "theme" `[string]`
- Chủ đề sẽ được sử dụng cho các sự kiện chặn và yêu cầu CAPTCHA.

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
└─…Khác
```

##### "theme_mode" `[string]`
- Chế độ cho chủ đề sẽ được sử dụng cho các sự kiện chặn và yêu cầu CAPTCHA.

```
theme_mode
├─normal ("Bình thường")
└─inverted ("Nghịch đảo")
```

##### "magnification" `[float]`
- Phóng to phông chữ. Mặc định = 1.

##### "css_url" `[string]`
- URL của tập tin CSS cho các chủ đề tùy chỉnh.

##### "block_event_title" `[string]`
- Tiêu đề trang để hiển thị cho các sự kiện chặn.

```
block_event_title
├─CIDRAM ("CIDRAM")
├─denied ("Truy cập đã bị từ chối!")
└─…Khác
```

##### "captcha_title" `[string]`
- Tiêu đề trang để hiển thị cho các yêu cầu CAPTCHA.

```
captcha_title
├─CIDRAM ("CIDRAM")
└─…Khác
```

##### "custom_header" `[string]`
- Được chèn dưới dạng HTML ở đầu tất cả các trang "truy cập đã bị từ chối". Điều này có thể hữu ích trong trường hợp bạn muốn bao gồm biểu trưng trang web, tiêu đề được cá nhân hóa, tập lệnh, hoặc tương tự ở tất cả các trang như vậy.

##### "custom_footer" `[string]`
- Được chèn dưới dạng HTML ở cuối tất cả các trang "truy cập đã bị từ chối". Điều này có thể hữu ích trong trường hợp bạn muốn bao gồm thông báo pháp lý, liên kết liên hệ, thông tin doanh nghiệp, hoặc tương tự ở tất cả các trang như vậy.

#### "rate_limiting" (Thể loại)
Cấu hình cho giới hạn tốc độ (không khuyến khích sử dụng chung).

Hãy nhớ rằng giống như mọi tính năng khác của CIDRAM, tính năng giới hạn tốc độ của CIDRAM chỉ có thể được áp dụng cho những trang và tài nguyên mà CIDRAM được kết nối. Điều đó thường có nghĩa là các tài nguyên không phải PHP sẽ không được bảo vệ, ngoại trừ trường hợp được cung cấp rõ ràng bởi các tài nguyên PHP được kết nối. Nếu bạn có thể sử dụng mô-đun máy chủ, cPanel, hoặc một số công cụ mạng khác để áp dụng giới hạn tốc độ, thì tốt hơn nên sử dụng chúng thay vì tính năng giới hạn tốc độ của CIDRAM. Ngoài ra, hãy nhớ rằng người dùng đặc biệt quyết tâm có thể dễ dàng vượt qua giới hạn tốc độ bằng cách thay đổi địa chỉ IP của họ hoặc chuyển sang nhà cung cấp proxy hoặc VPN mà CIDRAM chưa biết, và hãy nhớ rằng việc giới hạn tốc độ có thể gây rất nhiều khó chịu cho người dùng thực sự. Đôi khi điều này là cần thiết, nhưng hiếm khi là mong muốn.

##### "max_bandwidth" `[string]`
- Số lượng băng thông tối đa được phép trong khoảng thời gian cho phép trước khi cho phép giới hạn tốc độ cho các yêu cầu trong tương lai. Giá trị 0 sẽ vô hiệu hóa loại giới hạn tốc độ này. Mặc định = 0KB.

##### "max_requests" `[int]`
- Số lượng yêu cầu tối đa được phép trong khoảng thời gian cho phép trước khi cho phép giới hạn tốc độ cho các yêu cầu trong tương lai. Giá trị 0 sẽ vô hiệu hóa loại giới hạn tốc độ này. Mặc định = 0.

##### "precision_ipv4" `[int]`
- Độ chính xác để sử dụng khi giám sát việc sử dụng IPv4. Giá trị phản ánh kích thước khối CIDR. Đặt thành 32 để có độ chính xác cao nhất. Mặc định = 32.

##### "precision_ipv6" `[int]`
- Độ chính xác để sử dụng khi giám sát việc sử dụng IPv6. Giá trị phản ánh kích thước khối CIDR. Đặt thành 128 để có độ chính xác cao nhất. Mặc định = 128.

##### "allowance_period" `[string]`
- Thời lượng để giám sát việc sử dụng. Mặc định = 0°0′0″.

##### "exceptions" `[string]`
- Ngoại lệ (tức là, các yêu cầu không nên giới hạn). Chỉ có hiệu lực khi giới hạn tốc độ được kích hoạt.

```
exceptions
├─Whitelisted ("Yêu cầu trong danh sách trắng")
├─Verified ("Yêu cầu máy tìm kiếm và truyền thông xã hội đã xác minh")
└─FE ("Yêu cầu đối với front-end CIDRAM")
```

##### "segregate" `[bool]`
- Hạn ngạch cho miền và máy chủ lưu trữ nên được tách biệt hoặc chia sẻ? True = Hạn ngạch sẽ được tách biệt. False = Hạn ngạch sẽ được chia sẻ [Mặc định].

#### "supplementary_cache_options" (Thể loại)
Tùy chọn bộ nhớ cache bổ sung. Lưu ý: Việc thay đổi các giá trị này có thể khiến bạn bị đăng xuất.

##### "prefix" `[string]`
- Giá trị được chỉ định ở đây sẽ được thêm vào trước tất cả các khóa mục nhập bộ nhớ cache. Mặc định = "CIDRAM_". Khi nhiều bản cài đặt tồn tại trên cùng một máy chủ, điều này có thể hữu ích để giữ các bộ nhớ cache của chúng tách biệt với nhau.

##### "enable_apcu" `[bool]`
- Điều này xác định có nên thử sử dụng APCu để lưu trữ không. Mặc định = True.

##### "enable_memcached" `[bool]`
- Điều này xác định có nên thử sử dụng Memcached để lưu trữ không. Mặc định = False.

##### "enable_redis" `[bool]`
- Điều này xác định có nên thử sử dụng Redis để lưu trữ không. Mặc định = False.

##### "enable_pdo" `[bool]`
- Điều này xác định có nên thử sử dụng PDO để lưu trữ không. Mặc định = False.

##### "memcached_host" `[string]`
- Giá trị máy chủ Memcached. Mặc định = localhost.

##### "memcached_port" `[int]`
- Giá trị cổng Memcached. Mặc định = "11211".

##### "redis_host" `[string]`
- Giá trị máy chủ Redis. Mặc định = localhost.

##### "redis_port" `[int]`
- Giá trị cổng Redis. Mặc định = "6379".

##### "redis_timeout" `[float]`
- Giá trị thời gian chờ Redis. Mặc định = "2.5".

##### "redis_database_number" `[int]`
- Số cơ sở dữ liệu Redis. Mặc định = 0. Lưu ý: Không thể sử dụng các giá trị khác 0 với Redis Cluster.

##### "pdo_dsn" `[string]`
- Giá trị DSN PDO. Mặc định = "mysql:dbname=cidram;host=localhost;port=3306".

__Câu hỏi thường gặp.__ *<a href="https://github.com/CIDRAM/Docs/blob/master/readme.vi.md#user-content-HOW_TO_USE_PDO" hreflang="vi-VN">"PDO DSN" là gì? Làm cách nào tôi có thể sử dụng PDO với CIDRAM?</a>*

##### "pdo_username" `[string]`
- Tên người dùng PDO.

##### "pdo_password" `[string]`
- Mật khẩu PDO.

#### "bypasses" (Thể loại)
Cấu hình cho các đường tránh chữ ký mặc định.

##### "used" `[string]`
- Những đường tránh nào nên được sử dụng?

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


### 6. <a name="SECTION6"></a>ĐỊNH DẠNG CỦA CHỬ KÝ

*Xem thêm:*
- *["Chữ ký" là gì?](#user-content-WHAT_IS_A_SIGNATURE)*

#### 6.0 KHÁI NIỆM CƠ BẢN (ĐỐI VỚI TẬP TIN CHỮ KÝ)

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

#### 6.1 GẮN THẺ

##### 6.1.0 GẮN THẺ PHẦN

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

##### 6.1.1 GẮN THẺ HẾT HẠN

Nếu bạn muốn chữ ký hết hạn sau một thời gian, trong một cách tương tự như gắn thẻ phần, bạn có thể sử dụng một "gắn thẻ hết hạn" để chỉ định khi chữ ký nên hết hiệu lực. Gắn thẻ hết hạn sử dụng định dạng "YYYY.MM.DD" (xem ví dụ dưới đây).

```
# Phần 1.
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Expires: 2016.12.31
```

Chữ ký hết hạn sẽ không bao giờ được kích hoạt trên bất kỳ yêu cầu, không có vấn đề gì.

##### 6.1.2 GẮN THẺ XUẤT XỨ

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

##### 6.1.3 GẮN THẺ TRÌ HOÃN

Khi số lượng lớn các tập tin chữ ký được cài đặt và sử dụng, cài đặt có thể trở nên khá phức tạp, và có thể có một số chữ ký chồng lên nhau. Trong những trường hợp này, để ngăn chặn nhiều chữ ký chồng chéo được kích hoạt trong các sự kiện chặn, gắn thẻ trì hoãn có thể được sử dụng để trì hoãn các phần chữ ký cụ thể trong trường hợp một số tập tin chữ ký cụ thể khác được cài đặt và sử dụng. Điều này có thể hữu ích trong trường hợp một số chữ ký được cập nhật thường xuyên hơn các chữ ký khác, để trì hoãn các chữ ký ít được cập nhật thường xuyên hơn với các chữ ký được cập nhật thường xuyên hơn.

Gắn thẻ trì hoãn được sử dụng tương tự như các loại thẻ khác. Giá trị của thẻ phải khớp với tập tin chữ ký được cài đặt và sử dụng để bị trì hoãn.

Ví dụ:

```
1.2.3.4/32 Deny Generic
Origin: AA
2.3.4.5/32 Deny Generic
Origin: BB
Defers to: preferred_signatures.dat
```

##### 6.1.4 GẮN THẺ HỒ SƠ

Gắn thẻ hồ sơ cung cấp một phương tiện hiển thị thông tin bổ sung tại trang kiểm tra IP, và có thể được tận dụng bởi các mô-đun và các quy tắc phụ trợ để có hành vi phức tạp hơn và việc ra quyết định được tinh chỉnh.

Gắn thẻ hồ sơ được sử dụng tương tự như các loại gắn thẻ khác. Các giá trị của gắn thẻ hồ sơ có thể được sử dụng như một điều kiện cho các mô-đun và các quy tắc phụ trợ. Gắn thẻ hồ sơ có thể cung cấp nhiều giá trị bằng cách tách các giá trị đó bằng dấu chấm phẩy. Người dùng cuối không bao giờ nhìn thấy các giá trị của gắn thẻ hồ sơ.

Ví dụ:

```
1.2.3.4/32 Deny Generic
2.3.4.5/32 Deny Generic
Profile: Example;Just some generic stuff;Foo;Bar
Origin: BB
```

#### 6.2 YAML

##### 6.2.0 YAML CƠ BẢN

Một hình thức đơn giản của YAML có thể được sử dụng trong các tập tin chữ ký cho mục đích xác định các hành vi và các thiết lập cụ thể để phần chữ ký cá nhân. Điều này có thể hữu ích nếu bạn muốn giá trị của chỉ thị cấu hình của bạn để khác biệt trên cơ sở chữ ký cá nhân và phần chữ ký (ví dụ; nếu bạn muốn cung cấp một địa chỉ email cho vé hỗ trợ cho bất kỳ người dùng bị chặn bởi một chữ ký đặc biệt, nhưng không muốn cung cấp một địa chỉ email cho vé hỗ trợ cho người dùng bị chặn bởi bất kỳ chữ ký khác; nếu bạn muốn có một số chữ ký cụ thể để kích hoạt một chuyển hướng trang; nếu bạn muốn đánh dấu một phần chữ ký để sử dụng với hCaptcha; nếu bạn muốn ghi lại cố gắng truy cập bị chặn vào các tập tin riêng biệt trên cơ sở chữ ký cá nhân hay phần chữ ký).

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

#### 6.3 PHỤ TRỢ

##### 6.3.0 BỎ QUA PHẦN CHỮ KÝ

Ngoài ra, nếu bạn muốn CIDRAM để hoàn toàn bỏ qua một số phần cụ thể trong bất kỳ tập tin chữ ký, bạn có thể sử dụng các tập tin `ignore.dat` để xác định những phần để bỏ qua. Trên một dòng mới, viết `Ignore`, theo sau là một không gian, theo sau là tên của phần mà bạn muốn CIDRAM để bỏ qua (xem ví dụ dưới đây).

```
Ignore Phần 1
```

Điều này cũng có thể đạt được bằng cách sử dụng giao diện được cung cấp bởi trang "danh sách phần" front-end của CIDRAM.

##### 6.3.1 QUY TẮC PHỤ TRỢ

Nếu bạn cảm thấy việc viết các tập tin chữ ký tùy chỉnh hoặc các mô-đun tùy chỉnh của riêng bạn quá phức tạp đối với bạn, một lựa chọn đơn giản hơn có thể là sử dụng giao diện được cung cấp bởi trang "quy tắc phụ trợ" front-end của CIDRAM. Bằng cách chọn các tùy chọn thích hợp và chỉ định chi tiết về các loại yêu cầu cụ thể, bạn có thể hướng dẫn CIDRAM cách trả lời các yêu cầu đó. Các "quy tắc phụ trợ" được thực hiện sau khi tất cả các tập tin chữ ký và mô-đun đã hoàn thành thực hiện.

##### 6.3.2 LƯU VÀ KÍCH HOẠT TẬP TIN CHỮ KÝ TÙY CHỈNH

Đối với CIDRAM v2 trở xuống, trong vault, bạn sẽ tìm thấy hai tập tin: `ipv4_custom.dat.RenameMe` và `ipv6_custom.dat.RenameMe`. Bạn có thể lưu chữ ký tùy chỉnh vào các tập tin đó, hoặc nếu muốn, bạn có thể tạo tập tin mới cho chữ ký tùy chỉnh của mình, đặt tên tùy ý. Đối với CIDRAM v2 trở xuống, tập tin chữ ký tùy chỉnh phải được lưu ở thư mục gốc của vault.

Đối với CIDRAM v3 trở lên, tập tin cho chữ ký tùy chỉnh không được cung cấp trước, nhưng bạn cũng có thể tạo tập tin mới cho chữ ký tùy chỉnh của mình, đặt tên theo ý muốn. Đối với CIDRAM v3 trở lên, tập tin chữ ký tùy chỉnh phải được lưu trong thư mục "signatures" đã được chuẩn bị sẵn của bản cài đặt CIDRAM của bạn.

Để "kích hoạt" tập tin chữ ký tùy chỉnh, chúng phải được trích dẫn bởi các chỉ thị cấu hình "ipv4" hoặc "ipv6" trong tập tin cấu hình của bạn (tùy thuộc vào việc tập tin chữ ký tùy chỉnh đó dành cho chữ ký IPv4 hay IPv6).

Đối với CIDRAM v2 trở xuống, "ipv4" và "ipv6" được tìm thấy trong danh mục cấu hình "signatures".

Đối với CIDRAM v3 trở lên, "ipv4" và "ipv6" được tìm thấy trong danh mục cấu hình "components".

#### 6.4 <a name="MODULE_BASICS"></a>KHÁI NIỆM CƠ BẢN (CHO MÔ-ĐUN)

Các mô-đun có thể được sử dụng để mở rộng chức năng của CIDRAM, thực hiện các tác vụ bổ sung hay xử lý logic bổ sung.

Bởi vì các mô-đun được viết như tập tin PHP, nếu bạn đã quen thuộc với mã nguồn CIDRAM, bạn có thể cấu trúc module của bạn tuy nhiên bạn muốn, và viết chữ ký mô-đun của bạn tuy nhiên bạn muốn (trong vòng suy luận những gì có thể với PHP).

*Lưu ý: Nếu bạn không cảm thấy thoải mái khi làm việc với mã PHP, bạn không nên viết mô-đun riêng của mình.*

Một số chức năng được cung cấp bởi CIDRAM cho các mô-đun để sử dụng, để làm cho việc viết mô-đun của bạn trở nên đơn giản và dễ dàng hơn. Thông tin về chức năng này được mô tả dưới đây.

#### 6.5 CHỨC NĂNG MÔ-ĐUN

##### 6.5.0 "$this->trigger"

Chữ ký mô-đun thường được viết bằng `$this->trigger`. Trong hầu hết các trường hợp, sự đóng này sẽ quan trọng hơn bất cứ thứ gì khác để viết mô-đun.

`$this->trigger` chấp nhận 4 tham số: `$Condition`, `$ReasonShort`, `$ReasonLong` (không bắt buộc), và `$DefineOptions` (không bắt buộc).

Thực tế của `$Condition` được đánh giá, và nếu true/đúng, chữ ký là "kích hoạt". Nếu false/sai, chữ ký không phải là "kích hoạt". `$Condition` thường có chứa mã PHP để đánh giá một điều kiện nên làm yêu cầu bị chặn.

`$ReasonShort` được trích dẫn trong trường "Tại sao bị chặn" khi chữ ký được "kích hoạt".

`$ReasonLong` là một thông báo tùy chọn được hiển thị cho người dùng / khách hàng khi chúng bị chặn, để giải thích tại sao chúng bị chặn. Nó sử dụng thông báo "Truy cập đã bị từ chối" thông thường khi bị bỏ qua.

`$DefineOptions` là một mảng tùy chọn có chứa cặp khóa / giá trị, được sử dụng để xác định các tùy chọn cấu hình cụ thể cho trường hợp yêu cầu. Tùy chọn cấu hình sẽ được áp dụng khi chữ ký được "kích hoạt".

`$this->trigger` trả về true/đúng khi chữ ký được "kích hoạt", và false/sai khi không.

##### 6.5.1 "$this->bypass"

Đường tránh chữ ký thường được viết bằng `$this->bypass`.

`$this->bypass` chấp nhận 3 tham số: `$Condition`, `$ReasonShort`, và `$DefineOptions` (không bắt buộc).

Thực tế của `$Condition` được đánh giá, và nếu true/đúng, đường tránh là "kích hoạt". Nếu false/sai, đường tránh không phải là "kích hoạt". `$Condition` thường có chứa mã PHP để đánh giá một điều kiện *không* nên làm yêu cầu bị chặn.

`$ReasonShort` được trích dẫn trong trường "Tại sao bị chặn" khi đường tránh được "kích hoạt".

`$DefineOptions` là một mảng tùy chọn có chứa cặp khóa / giá trị, được sử dụng để xác định các tùy chọn cấu hình cụ thể cho trường hợp yêu cầu. Tùy chọn cấu hình sẽ được áp dụng khi đường tránh được "kích hoạt".

`$this->bypass` trả về true/đúng khi đường tránh được "kích hoạt", và false/sai khi không.

##### 6.5.2 "$this->dnsReverse"

Điều này có thể được sử dụng để lấy tên máy chủ của một địa chỉ IP. Nếu bạn muốn tạo một mô-đun để chặn tên máy chủ, sự đóng này có thể hữu ích.

Ví dụ:
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

#### 6.6 BIẾN MÔ-ĐUN

Mô-đun thực hiện theo phạm vi riêng của chúng, và bất kỳ biến nào được xác định bởi mô-đun, sẽ không thể truy cập vào mô-đun khác, hoặc kịch bản cha mẹ, trừ khi chúng được lưu trữ trong mảng `$CIDRAM` (mọi thứ khác được làm sạch sau khi kết thúc thực hiện mô-đun).

Dưới đây là một số biến phổ biến có thể hữu ích cho mô-đun của bạn:

Biến | Chi tiết
----|----
`$this->BlockInfo['DateTime']` | Ngày hiện tại và thời gian.
`$this->BlockInfo['IPAddr']` | Địa chỉ IP cho yêu cầu hiện tại.
`$this->BlockInfo['IPAddrResolved']` | Nếu địa chỉ IP cho yêu cầu hiện tại là địa chỉ 6to4, Teredo, hoặc ISATAP, thì địa chỉ đó sẽ được phân giải thành địa chỉ IPv4 tương đương. Nếu không, thì đó sẽ là địa chỉ IP cho yêu cầu hiện tại.
`$this->BlockInfo['ScriptIdent']` | Phiên bản kịch bản CIDRAM.
`$this->BlockInfo['Query']` | Truy vấn (query) cho yêu cầu hiện tại.
`$this->BlockInfo['Referrer']` | Người giới thiệu (referrer) cho yêu cầu hiện tại (nếu có).
`$this->BlockInfo['UA']` | Đại lý người dùng (user agent) cho yêu cầu hiện tại.
`$this->BlockInfo['UALC']` | Đại lý người dùng (user agent) cho yêu cầu hiện tại (trong trường hợp thấp).
`$this->BlockInfo['ReasonMessage']` | Thông báo sẽ được hiển thị cho người dùng / khách hàng cho yêu cầu hiện tại nếu chúng bị chặn.
`$this->BlockInfo['SignatureCount']` | Số chữ ký kích hoạt cho yêu cầu hiện tại.
`$this->BlockInfo['Signatures']` | Thông tin tham khảo cho bất kỳ chữ ký nào được kích hoạt cho yêu cầu hiện tại.
`$this->BlockInfo['WhyReason']` | Thông tin tham khảo cho bất kỳ chữ ký nào được kích hoạt cho yêu cầu hiện tại.
`$this->BlockInfo['Request_Method']` | Phương thức yêu cầu cho yêu cầu hiện tại.
`$this->BlockInfo['Protocol']` | Giao thức cho yêu cầu hiện tại.

---


### 7. <a name="SECTION7"></a>NHỮNG VẤN ĐỀ HỢP TƯƠNG TÍCH

Các gói và sản phẩm sau đã được tìm thấy là không tương thích với CIDRAM:
- __[Endurance Page Cache](https://github.com/CIDRAM/CIDRAM/issues/52)__
- __[Mix.com](https://github.com/CIDRAM/CIDRAM/issues/80)__

Các mô-đun đã được cung cấp để đảm bảo rằng các gói và sản phẩm sau sẽ tương thích với CIDRAM:
- __[BunnyCDN](https://github.com/CIDRAM/CIDRAM/issues/56)__
- __[Quic cloud](https://wordpress.org/support/topic/quic-dot-cloud-requires-all-ips-allowed/)__

*Xem thêm: [Biểu đồ tương thích](https://maikuolan.github.io/Compatibility-Charts/).*

---


### 8. <a name="SECTION8"></a>NHỮNG CÂU HỎI THƯỜNG GẶP (FAQ)

- ["Chữ ký" là gì?](#user-content-WHAT_IS_A_SIGNATURE)
- ["CIDR" là gì?](#user-content-WHAT_IS_A_CIDR)
- ["Sai tích cực" là gì?](#user-content-WHAT_IS_A_FALSE_POSITIVE)
- [CIDRAM có thể chặn toàn bộ quốc gia?](#user-content-BLOCK_ENTIRE_COUNTRIES)
- [Tần suất cập nhật chữ ký là bao nhiêu?](#user-content-SIGNATURE_UPDATE_FREQUENCY)
- [Tôi đã gặp một vấn đề trong khi sử dụng CIDRAM và tôi không biết phải làm gì về nó! Hãy giúp tôi!](#user-content-ENCOUNTERED_PROBLEM_WHAT_TO_DO)
- [Tôi đã bị chặn bởi CIDRAM từ một trang web mà tôi muốn ghé thăm! Hãy giúp tôi!](#user-content-BLOCKED_WHAT_TO_DO)
- [Tôi muốn sử dụng CIDRAM v2~v4 với phiên bản PHP cũ hơn 7.2; Bạn có thể giúp?](#user-content-MINIMUM_PHP_VERSION_V3)
- [Tôi có thể sử dụng một cài đặt CIDRAM để bảo vệ nhiều tên miền?](#user-content-PROTECT_MULTIPLE_DOMAINS)
- [Tôi không muốn lãng phí thời gian bằng cách cài đặt này và đảm bảo rằng nó hoạt động với trang web của tôi; Tôi có thể trả tiền cho bạn để làm điều đó cho tôi?](#user-content-PAY_YOU_TO_DO_IT)
- [Tôi có thể thuê bạn hay bất kỳ nhà phát triển nào của dự án này cho công việc riêng tư?](#user-content-HIRE_FOR_PRIVATE_WORK)
- [Tôi cần sửa đổi chuyên môn, tuỳ chỉnh, vv; Bạn có thể giúp?](#user-content-SPECIALIST_MODIFICATIONS)
- [Tôi là nhà phát triển, nhà thiết kế trang web, hay lập trình viên. Tôi có thể chấp nhận hay cung cấp các công việc liên quan đến dự án này không?](#user-content-ACCEPT_OR_OFFER_WORK)
- [Tôi muốn đóng góp cho dự án; Tôi có thể làm được điều này?](#user-content-WANT_TO_CONTRIBUTE)
- [Tôi có thể sử dụng cron để cập nhật tự động không?](#user-content-CRON_TO_UPDATE_AUTOMATICALLY)
- ["Vi phạm" là gì?](#user-content-WHAT_ARE_INFRACTIONS)
- [CIDRAM có thể chặn tên máy chủ không?](#user-content-BLOCK_HOSTNAMES)
- [Những gì tôi có thể sử dụng cho "default_dns"?](#những-gì-tôi-có-thể-sử-dụng-cho-default_dns)
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
$this->trigger(strpos($this->BlockInfo['UA'], 'Foobar') !== false, 'Foobar-UA', 'User agent "Foobar" not allowed.');
```

*Chú thích: Chữ ký cho "tập tin chữ ký", và chữ ký cho "mô-đun", không phải là cùng một điều.*

Thông thường (nhưng không phải luôn luôn), chữ ký sẽ được nhóm lại với nhau, để hình thành "phần chữ ký", thường kèm theo bình luận, đánh dấu, hay siêu dữ liệu liên quan mà có thể được sử dụng để cung cấp bối cảnh bổ sung cho chữ ký hay lệnh bổ sung.

#### <a name="WHAT_IS_A_CIDR"></a>"CIDR" là gì?

"CIDR" là một từ viết tắt cho "Classless Inter-Domain Routing" *[[1](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing), [2](https://whatismyipaddress.com/cidr)]*, và nó là từ viết tắt này được sử dụng như là một phần của tên cho gói này, "CIDRAM", đó là một từ viết tắt cho "Classless Inter-Domain Routing Access Manager".

Trong ngữ cảnh của CIDRAM, "CIDR" (hoặc "CIDRs") đề cập cụ thể đến các mạng con được biểu diễn bằng ký hiệu CIDR.

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

#### <a name="MINIMUM_PHP_VERSION_V3"></a>Tôi muốn sử dụng CIDRAM v2~v4 với phiên bản PHP cũ hơn 7.2; Bạn có thể giúp?

Không. PHP≥7.2 là yêu cầu tối thiểu đối với CIDRAM v2~v4.

*Xem thêm: [Biểu đồ tương thích](https://maikuolan.github.io/Compatibility-Charts/).*

#### <a name="PROTECT_MULTIPLE_DOMAINS"></a>Tôi có thể sử dụng một cài đặt CIDRAM để bảo vệ nhiều tên miền?

Vâng. Cài đặt CIDRAM không bị khóa vào các tên miền cụ thể, và do đó có thể được sử dụng để bảo vệ nhiều tên miền. Nói chung là, chúng tôi đề cập đến cài đặt CIDRAM chỉ bảo vệ một miền như "cài đặt miền đơn" ("single-domain installations"), và chúng tôi đề cập đến cài đặt CIDRAM bảo vệ nhiều miền hay miền phụ như "cài đặt nhiều miền" ("multi-domain installations"). Nếu bạn sử dụng một cài đặt nhiều miền và cần phải sử dụng các bộ tập tin chữ ký khác nhau cho các miền khác nhau, hoặc cần CIDRAM được cấu hình khác nhau cho các miền khác nhau, điều này có thể làm được. Sau khi tải tập tin cấu hình (`config.yml`), CIDRAM sẽ kiểm tra sự tồn tại của một "tập tin ghi đè cấu hình" cụ thể cho miền được yêu cầu (`miền-được-yêu-cầu.tld.config.yml`), và nếu được tìm thấy, bất kỳ giá trị cấu hình nào được xác định bởi tập tin ghi đè cấu hình sẽ được sử dụng cho trường hợp thực hiện thay vì các giá trị cấu hình được định nghĩa bởi tập tin cấu hình. Các tập tin ghi đè cấu hình giống với tập tin cấu hình, và tùy theo quyết định của bạn, có thể chứa toàn bộ các chỉ thị cấu hình sẵn có cho CIDRAM, hoặc bất kỳ phần bắt buộc nào mà khác với các giá trị được xác định bởi tập tin cấu hình. Các tập tin ghi đè cấu hình được đặt tên theo miền mà chúng được dự định (vì vậy, ví dụ, nếu bạn cần một tập tin ghi đè cấu hình cho miền, `https://www.some-domain.tld/`, các tập tin ghi đè cấu hình của nó nên được đặt tên là `some-domain.tld.config.yml`, và nên được đặt trong vault với tập tin cấu hình, `config.yml`). Tên miền cho trường hợp thực hiện được bắt nguồn từ header (tiêu đề) `HTTP_HOST` của các yêu cầu; "www" bị bỏ qua.

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

"Số lượng chữ ký" và "vi phạm" đều liên quan đến mức độ nghiêm trọng và số lượng chữ ký được kích hoạt trong bất kỳ yêu cầu cụ thể nào, cho dù do tập tin chữ ký, mô-đun, quy tắc phụ trợ, hoặc do cách khác, nhưng trong khi "số lượng chữ ký" chỉ tồn tại cho yêu cầu cụ thể đó, "vi phạm" có thể tồn tại trên bất kỳ số lượng yêu cầu nào, miễn là được xác định bởi `default_tracktime`.

Điều này cung cấp một cơ chế để đảm bảo rằng các yêu cầu từ các nguồn tiềm ẩn nguy hiểm có thể bị chặn theo các yêu cầu thứ cấp từ bất kỳ nguồn cụ thể nào như vậy, theo đó nguồn đó đã bị chặn trong một yêu cầu trước đó với đủ số lần vi phạm.

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

```YAML
modules: |
 file1.php
 file2.php
 file3.php
 file4.php
 file5.php
```

Nếu bạn muốn `file3.php` thực hiện trước, bạn có thể thêm một cái gì đó như `aaa:` trước tên của tập tin:

```YAML
modules: |
 file1.php
 file2.php
 aaa:file3.php
 file4.php
 file5.php
```

Sau đó, nếu một tập tin mới, `file6.php`, được kích hoạt, khi trang cập nhật sắp xếp lại tất cả, nó sẽ kết thúc như sau:

```YAML
modules: |
 aaa:file3.php
 file1.php
 file2.php
 file4.php
 file5.php
 file6.php
```

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


### 9. <a name="SECTION9"></a>THÔNG TIN HỢP PHÁP

#### 9.0 PHẦN MỞ ĐẦU

Phần tài liệu này nhằm mô tả các cân nhắc pháp lý có thể có về việc sử dụng và thực hiện của gói, và cung cấp một số thông tin liên quan cơ bản. Điều này có thể quan trọng đối với một số người dùng như một phương tiện để đảm bảo tuân thủ mọi yêu cầu pháp lý có thể tồn tại ở các quốc gia mà họ hoạt động, và một số người dùng có thể cần phải điều chỉnh chính sách trang web của họ theo thông tin này.

Đầu tiên và quan trọng nhất, xin vui lòng nhận ra rằng tôi (tác giả gói) không phải là luật sư, cũng không phải là một chuyên gia pháp lý đủ điều kiện. Do đó, tôi không đủ tư cách pháp lý để cung cấp tư vấn pháp lý. Ngoài ra, trong một số trường hợp, yêu cầu pháp lý chính xác có thể khác nhau giữa các quốc gia và khu vực pháp lý khác nhau, và các yêu cầu pháp lý khác nhau đôi khi có thể xung đột (chẳng hạn như, ví dụ, trong trường hợp các quốc gia mà ủng hộ [quyền riêng tư](https://vi.wikipedia.org/wiki/Quy%E1%BB%81n_%C4%91%C6%B0%E1%BB%A3c_b%E1%BA%A3o_v%E1%BB%87_%C4%91%E1%BB%9Di_t%C6%B0) và quyền bị lãng quên, so với các quốc gia mà ủng hộ luật lưu giữ dữ liệu). Cũng xem xét việc truy cập vào gói không bị giới hạn ở các quốc gia hoặc khu vực pháp lý cụ thể, và do đó, cơ sở người dùng gói có khả năng đa dạng về mặt địa lý. Những điểm này được xem xét, tôi không ở trong một vị trí để tuyên bố những gì nó có nghĩa là để "tuân thủ về mặt pháp lý" cho tất cả người dùng, trong tất cả các liên quan. Tuy nhiên, tôi hy vọng rằng thông tin trong tài liệu này sẽ giúp bạn tự quyết định về những gì bạn phải làm để duy trì tuân thủ về mặt pháp lý trong bối cảnh của gói. Nếu bạn có bất kỳ nghi ngờ hoặc quan tâm nào về thông tin ở đây, hoặc nếu bạn cần thêm trợ giúp và tư vấn từ góc độ pháp lý, tôi khuyên bạn nên tham khảo ý kiến chuyên gia pháp lý đủ điều kiện.

#### 9.1 TRÁCH NHIỆM PHÁP LÝ

Theo như đã nêu trong giấy phép gói, gói được cung cấp mà không có bất kỳ bảo hành nào. Điều này bao gồm (nhưng không giới hạn) tất cả phạm vi trách nhiệm pháp lý. Gói phần mềm được cung cấp cho bạn để thuận tiện cho bạn, với hy vọng rằng nó sẽ hữu ích, và rằng nó sẽ cung cấp một số lợi ích cho bạn. Tuy nhiên, việc sử dụng hoặc triển khai gói, là lựa chọn của riêng bạn. Bạn không bị buộc phải sử dụng hoặc triển khai gói, nhưng khi bạn làm như vậy, bạn chịu trách nhiệm về quyết định đó. Tôi và những người đóng góp gói khác, không chịu trách nhiệm pháp lý về hậu quả của các quyết định mà bạn đưa ra, bất kể trực tiếp, gián tiếp, ngụ ý, hay nói cách khác.

#### 9.2 BÊN THỨ BA

Tùy thuộc vào cấu hình và triển khai chính xác của nó, gói có thể giao tiếp và chia sẻ thông tin với bên thứ ba trong một số trường hợp. Thông tin này có thể được định nghĩa là "[thông tin nhận dạng cá nhân](https://www.pcworld.com.vn/articles/cong-nghe/an-ninh-mang/2016/05/1248000/thong-tin-ca-nhan-tai-san-rieng-cung-la-tien/)" (PII) trong một số ngữ cảnh, bởi một số khu vực pháp lý.

Thông tin này có thể được các bên thứ ba này sử dụng như thế nào, là tuân theo của chính sách của các bên thứ ba, và nằm ngoài phạm vi của tài liệu này. Tuy nhiên, trong tất cả các trường hợp như vậy, việc chia sẻ thông tin với các bên thứ ba này có thể bị vô hiệu hóa. Trong tất cả các trường hợp như vậy, nếu bạn chọn kích hoạt nó, bạn có trách nhiệm nghiên cứu bất kỳ mối lo ngại nào về sự riêng tư, bảo mật, và việc sử dụng PII của các bên thứ ba này. Nếu có bất kỳ nghi ngờ nào, hoặc nếu bạn không hài lòng với hành vi của các bên thứ ba liên quan đến PII, tốt nhất là nên vô hiệu hóa tất cả việc chia sẻ thông tin với các bên thứ ba này.

Với mục đích minh bạch, loại thông tin được chia sẻ, và với ai, được mô tả dưới đây.

##### 9.2.0 TRA CỨU TÊN MÁY CHỦ

Nếu bạn sử dụng bất kỳ tính năng hay mô-đun nào để làm việc với tên máy chủ (chẳng hạn như "mô-đun cho chặn các host xấu", "tor project exit nodes block module", hay "xác minh máy tìm kiếm", ví dụ), CIDRAM cần để có thể có được tên máy chủ của các yêu cầu gửi đến bằng cách nào đó. Thông thường, nó thực hiện điều này bằng cách yêu cầu tên máy chủ của địa chỉ IP của các yêu cầu gửi đến từ một máy chủ DNS, hoặc bằng cách yêu cầu thông tin thông qua chức năng được cung cấp bởi hệ thống nơi CIDRAM được cài đặt (điều này thường được gọi là "tra cứu tên máy chủ"). Các máy chủ DNS được xác định theo mặc định thuộc về dịch vụ [Google DNS](https://dns.google.com/) (nhưng điều này có thể dễ dàng thay đổi thông qua cấu hình). Các dịch vụ chính xác được truyền thông phụ thuộc vào cách bạn định cấu hình gói (nó có thể được cấu hình dễ dàng). Trong trường hợp sử dụng chức năng được cung cấp bởi hệ thống nơi CIDRAM được cài đặt, bạn sẽ cần phải liên hệ với quản trị viên hệ thống của bạn để xác định các tuyến đường để sử dụng cho tra cứu tên máy chủ. Tra cứu tên máy chủ có thể được ngăn chặn trong CIDRAM bằng cách tránh các mô-đun bị ảnh hưởng hay bằng cách sửa đổi cấu hình gói để phù hợp với nhu cầu của bạn.

*Chỉ thị cấu hình có liên quan:*
- `general` -> `allow_gethostbyaddr_lookup`
- `general` -> `default_dns`
- `general` -> `force_hostname_lookup`
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.1 XÁC MINH MÁY TÌM KIẾM VÀ TRUYỀN THÔNG XÃ HỘI

Khi xác minh máy tìm kiếm được kích hoạt, CIDRAM cố gắng thực hiện "tra cứu DNS chuyển tiếp" để xác minh tính xác thực của các yêu cầu nói rằng bắt nguồn từ các máy tìm kiếm. Tương tự như vậy, khi xác minh truyền thông xã hội được kích hoạt, CIDRAM thực hiện tương tự cho các yêu cầu truyền thông xã hội bị nghi ngờ. Để thực hiện điều này, nó sử dụng dịch vụ [Google DNS](https://dns.google.com/) để cố gắng giải quyết các địa chỉ IP từ tên máy chủ của các yêu cầu gửi đến này (trong quá trình này, tên máy chủ của các yêu cầu gửi đến này được chia sẻ với dịch vụ).

*Chỉ thị cấu hình có liên quan:*
- `verification` -> `other`
- `verification` -> `search_engines`
- `verification` -> `social_media`

##### 9.2.2 CAPTCHA

CIDRAM hỗ trợ CAPTCHA. Chúng yêu cầu các khóa API để hoạt động chính xác. Chúng bị vô hiệu hóa mặc định, nhưng có thể được kích hoạt bằng cách định cấu hình các khóa API. Khi được kích hoạt, giao tiếp có thể xảy ra giữa dịch vụ và CIDRAM hoặc trình duyệt của người dùng. Điều này có thể liên quan đến việc truyền đạt thông tin như địa chỉ IP của người dùng, đại lý người dùng, hệ điều hành, và các chi tiết khác có sẵn cho yêu cầu.

##### 9.2.3 STOP FORUM SPAM

[Stop Forum Spam](https://www.stopforumspam.com/) là một dịch vụ tuyệt vời, miễn phí có sẵn có thể giúp bảo vệ diễn đàn, blog và trang web từ chương trình thư rác. Nó thực hiện điều này bằng cách cung cấp một cơ sở dữ liệu của chương trình và những người gửi thư rác đã biết, và một API có thể được tận dụng để kiểm tra xem địa chỉ IP, tên người dùng hay địa chỉ email có được liệt kê trên cơ sở dữ liệu của nó hay không.

CIDRAM cung cấp một mô-đun tùy chọn tận dụng API này để kiểm tra xem địa chỉ IP của các yêu cầu gửi đến thuộc về một chương trình và những người gửi thư rác bị nghi ngờ hay không. Khi mô-đun được cài đặt và kích hoạt, địa chỉ IP của người dùng có thể được chia sẻ với dịch vụ theo hợp với cấu hình và mục đích dự kiến của mô-đun.

##### 9.2.4 ABUSEIPDB

CIDRAM cung cấp các mô-đun tùy chọn để chặn các địa chỉ IP lạm dụng bằng cách sử dụng API của [AbuseIPDB](https://www.abuseipdb.com/) và API của [IP-API](https://ip-api.com/). Khi một trong số chúng được cài đặt và kích hoạt, địa chỉ IP của người dùng có thể được chia sẻ với dịch vụ theo hợp với cấu hình và mục đích dự kiến của mô-đun.

##### 9.2.5 BGPVIEW, IP-API

CIDRAM cung cấp một mô-đun tùy chọn để thực hiện tra cứu ASN và mã quốc gia bằng API của [BGPView](https://bgpview.io/) API. Các tra cứu này cung cấp khả năng chặn hoặc danh sách trắng yêu cầu trên cơ sở ASN hoặc quốc gia xuất xứ của họ. Khi mô-đun được cài đặt và kích hoạt, địa chỉ IP của người dùng có thể được chia sẻ với dịch vụ theo hợp với cấu hình và mục đích dự kiến của mô-đun.

##### 9.2.6 PROJECT HONEYPOT

CIDRAM cung cấp một mô-đun tùy chọn để chặn các địa chỉ IP lạm dụng bằng cách sử dụng API của [Project Honeypot](https://www.projecthoneypot.org/). Khi mô-đun được cài đặt và kích hoạt, địa chỉ IP của người dùng có thể được chia sẻ với dịch vụ theo hợp với cấu hình và mục đích dự kiến của mô-đun.

#### 9.3 NHẬT KÝ

Nhật ký là một phần quan trọng của CIDRAM vì một số lý do. có thể khó để chẩn đoán và giải quyết các kết quả sai tích cực khi các sự kiện chặn khiến chúng không được ghi lại. Khi các sự kiện chặn không được ghi lại, có thể khó để xác định chính xác CIDRAM hoạt động tốt như thế nào trong bất kỳ ngữ cảnh cụ thể nào, và có thể khó để xác định nơi bất cập của nó, và những thay đổi nào có thể cần thiết đối với cấu hình hay chữ ký của nó, để nó có thể tiếp tục hoạt động như dự định. Bất kể, nhật ký có thể không được mong muốn cho tất cả người dùng, và vẫn hoàn toàn tùy chọn. Trong CIDRAM, ghi nhật ký bị vô hiệu hóa theo mặc định. Để kích hoạt nó, CIDRAM phải được cấu hình cho phù hợp.

Ngoài ra, việc nhật ký có được cho phép hợp pháp hay không, và trong phạm vi được cho phép hợp pháp (ví dụ, các loại thông tin có thể được nhật ký, bao lâu, và trong hoàn cảnh gì), có thể thay đổi, tùy thuộc vào thẩm quyền pháp lý và trong bối cảnh CIDRAM được triển khai (ví dụ, nếu bạn đang hoạt động như một cá nhân, như một thực thể công ty, và nếu trên cơ sở thương mại hay phi thương mại). Do đó, nó có thể hữu ích cho bạn để đọc kỹ phần này.

Có nhiều kiểu ghi nhật ký mà CIDRAM có thể thực hiện. Các loại ghi nhật ký khác nhau liên quan đến các loại thông tin khác nhau, vì các lý do khác nhau.

##### 9.3.0 SỰ KIỆN CHẶN

Loại nhật ký chính mà CIDRAM có thể thực hiện liên quan đến "sự kiện chặn". Loại nhật ký này liên quan đến khi CIDRAM chặn một yêu cầu, và có thể được cung cấp theo ba định dạng khác nhau:
- Tập tin nhật ký mà có thể được đọc bởi con người.
- Tập tin nhật ký trong kiểu Apache.
- Tập tin nhật ký được tuần tự hóa.

Sự kiện chặn, được ghi vào tập tin nhật ký mà có thể được đọc bởi con người, thường trông giống như sau (ví dụ):

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

Cùng một sự kiện chặn, được ghi vào tập tin nhật ký trong kiểu Apache, sẽ trông giống như sau:

```
x.x.x.x - - [Day, dd Mon 20xx hh:ii:ss +0000] "GET /index.php HTTP/1.1" 200 xxxx "-" "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36"
```

Sự kiện chặn đã nhật ký thường bao gồm thông tin sau:
- Một số ID tham chiếu đến sự kiện chặn.
- Phiên bản CIDRAM hiện đang được sử dụng.
- Ngày và giờ xảy ra sự kiện chặn.
- Địa chỉ IP của yêu cầu bị chặn.
- Tên máy chủ của địa chỉ IP của yêu cầu bị chặn (nếu có).
- Số lượng chữ ký được kích hoạt bởi yêu cầu.
- Tham chiếu đến chữ ký được kích hoạt.
- Tham khảo các lý do cho sự kiện chặn và một số thông tin gỡ rối cơ bản liên quan.
- Đại lý người dùng của yêu cầu bị chặn (danh tính của thực thể yêu cầu).
- Việc xây dựng lại số nhận dạng cho tài nguyên được yêu cầu ban đầu.
- Trạng thái CAPTCHA cho yêu cầu hiện tại (khi có liên quan).

*Các chỉ thị cấu hình chịu trách nhiệm về loại ghi nhật ký này và cho mỗi một trong ba định dạng có sẵn:*
- `logging` -> `apache_style_log`
- `logging` -> `serialised_log`
- `logging` -> `standard_log`

Khi các chỉ thị này được để trống, loại ghi nhật ký này sẽ vẫn bị vô hiệu hóa.

##### 9.3.1 NHẬT KÝ CAPTCHA

Loại nhật ký này liên quan cụ thể đến CAPTCHA, và chỉ xảy ra khi người dùng cố gắng hoàn thành CAPTCHA.

Mục nhập nhật ký CAPTCHA chứa địa chỉ IP của người dùng đang cố gắng hoàn thành CAPTCHA, ngày và giờ xảy ra sự cố, và trạng thái của CAPTCHA. Mục nhập nhật ký CAPTCHA thường trông giống như sau (ví dụ):

```
Địa chỉ IP: x.x.x.x - Ngày/Thời gian: Day, dd Mon 20xx hh:ii:ss +0000 - Tình trạng CAPTCHA: Thành công!
```

*Chỉ thị cấu hình chịu trách nhiệm cho nhật ký CAPTCHA là:*
- `captcha` -> `log`

##### 9.3.2 NHẬT KÝ FRONT-END

Loại nhật ký này liên quan đến cố gắng đăng nhập, và chỉ xảy ra khi người dùng cố gắng đăng nhập vào front-end (giả sử truy cập front-end được kích hoạt).

Mục nhập nhật ký front-end chứa địa chỉ IP của người dùng đang cố gắng đăng nhập, ngày và giờ xảy ra điều này, và kết quả của cố gắng này (đăng nhập thành công, hoặc thành công không thành công). Mục nhập nhật ký front-end thường trông giống như thế này (làm ví dụ):

```
x.x.x.x - Day, dd Mon 20xx hh:ii:ss +0000 - "admin" - Đã đăng nhập.
```

*Chỉ thị cấu hình chịu trách nhiệm cho nhật ký front-end là:*
- `frontend` -> `frontend_log`

##### 9.3.3 XOAY VÒNG NHẬT KÝ

Bạn có thể muốn thanh lọc nhật ký sau một khoảng thời gian, hoặc có thể được yêu cầu làm như vậy theo luật pháp (khoảng thời gian được phép giữ nhật ký hợp pháp có thể bị giới hạn bởi luật pháp). Bạn có thể đạt được điều này bằng cách đưa dấu ngày/giờ vào tên tập tin nhật ký của bạn theo quy định của cấu hình gói của bạn (ví dụ, `{yyyy}-{mm}-{dd}.log`), và sau đó kích hoạt xoay vòng nhật ký (xoay vòng nhật ký cho phép bạn thực hiện một số hành động trên tập tin nhật ký khi vượt quá giới hạn được chỉ định).

Ví dụ: Nếu tôi được yêu cầu xóa nhật ký sau 30 ngày theo pháp luật, tôi có thể chỉ định `{dd}.log` trong tên của tập tin nhật ký của tôi (`{dd}` đại diện cho ngày), đặt giá trị của `log_rotation_limit` để 30, và đặt giá trị của `log_rotation_action` để `Delete`.

Ngược lại, nếu bạn được yêu cầu giữ lại nhật ký trong một khoảng thời gian dài, bạn có thể cân nhắc không sử dụng xoay vòng nhật ký, hoặc bạn có thể đặt giá trị của `log_rotation_action` để `Archive`, để nén tập tin nhật ký, do đó làm giảm tổng dung lượng đĩa mà họ chiếm.

*Chỉ thị cấu hình có liên quan:*
- `logging` -> `log_rotation_action`
- `logging` -> `log_rotation_limit`

##### 9.3.4 CẮT NGẮN NHẬT KÝ

Cũng có thể cắt ngắn các tập tin nhật ký riêng lẻ khi chúng vượt quá một kích thước nhất định, nếu đây bạn có thể cần hay muốn làm.

*Chỉ thị cấu hình có liên quan:*
- `logging` -> `truncate`

##### 9.3.5 PSEUDONYMISATION ĐỊA CHỈ IP

Thứ nhất, nếu bạn không quen thuộc với thuật ngữ này, "pseudonymisation" đề cập đến việc xử lý dữ liệu cá nhân sao cho không thể xác định được dữ liệu cá nhân cho bất kỳ chủ đề dữ liệu cụ thể nào nữa trừ khi có thông tin bổ sung, và miễn là thông tin bổ sung đó được duy trì riêng biệt và phải chịu sự các biện pháp kỹ thuật và tổ chức để đảm bảo rằng dữ liệu cá nhân không thể được xác định cho bất kỳ người tự nhiên nào.

Trong một số trường hợp, bạn có thể được yêu cầu về mặt pháp lý để sử dụng "anonymisation" hoặc "pseudonymisation" cho bất kỳ PII nào được thu thập, xử lý hoặc lưu trữ. Mặc dù khái niệm này đã tồn tại trong một thời gian khá lâu, GDPR/DSGVO đề cập đến, và đặc biệt khuyến khích "pseudonymisation".

CIDRAM có thể sử dụng "pseudonymisation" cho các địa chỉ IP khi nhật ký chúng vào bản ghi, nếu đây bạn có thể cần hay muốn làm. Khi CIDRAM sử dụng "pseudonymisation" cho các địa chỉ IP, khi nhật ký chúng vào bản ghi, octet cuối cùng của địa chỉ IPv4, và mọi thứ sau phần thứ hai của địa chỉ IPv6 được đại diện bởi một "x" (hiệu quả làm tròn địa chỉ IPv4 đến địa chỉ đầu tiên của mạng con thứ 24 mà chúng đưa vào, và địa chỉ IPv6 đến địa chỉ đầu tiên của mạng con thứ 32 mà chúng đưa vào).

*Chú thích: Quá trình pseudonymisation địa chỉ IP của CIDRAM không ảnh hưởng đến tính năng giám sát IP của CIDRAM. Nếu đây là vấn đề với bạn, có thể tốt nhất là tắt giám sát IP hoàn toàn.*

*Chỉ thị cấu hình có liên quan:*
- `legal` -> `pseudonymise_ip_addresses`

##### 9.3.6 BỎ QUA THÔNG TIN NHẬT KÝ

Nếu bạn muốn tiến thêm một bước nữa bằng cách ngăn chặn các loại thông tin cụ thể được ghi lại hoàn toàn, điều này cũng có thể thực hiện được. Tại trang cấu hình, vui lòng tham khảo chỉ thị cấu hình `fields` để kiểm soát trường nào xuất hiện trong các mục nhật ký và trên trang "truy cập đã bị từ chối".

![fields](https://raw.githubusercontent.com/CIDRAM/Docs/master/assets/fields.png)

*Chú thích: Không có lý do gì để bút danh các địa chỉ IP khi bỏ qua chúng hoàn toàn từ các nhật ký.*

*Chỉ thị cấu hình có liên quan:*
- `general` -> `fields`

##### 9.3.7 SỐ LIỆU THỐNG KÊ

CIDRAM có thể tùy chọn theo dõi số liệu thống kê như tổng số sự kiện chặn hay sự xuất hiện CAPTCHA đã xảy ra kể từ một số thời điểm cụ thể. Tính năng này được vô hiệu hóa theo mặc định, nhưng có thể được kích hoạt thông qua cấu hình gói. Tính năng này chỉ theo dõi tổng số sự kiện đã xảy ra và không bao gồm bất kỳ thông tin nào về các sự kiện cụ thể (và do đó, không nên được coi là PII).

*Chỉ thị cấu hình có liên quan:*
- `general` -> `statistics`

##### 9.3.8 MÃ HÓA

CIDRAM không mã hóa bộ nhớ cache của nó hoặc bất kỳ thông tin log nào. [Mã hóa](https://vi.wikipedia.org/wiki/M%C3%A3_h%C3%B3a) bộ nhớ cache và log có thể được giới thiệu trong tương lai, nhưng hiện tại không có bất kỳ kế hoạch cụ thể nào. Nếu bạn lo lắng về các bên thứ ba không được phép truy cập vào các phần của CIDRAM có thể chứa thông tin nhận dạng cá nhân hay thông tin nhạy cảm như bộ nhớ cache hoặc nhật ký của nó, tôi khuyên bạn không nên cài đặt CIDRAM tại vị trí có thể truy cập công khai (ví dụ, cài đặt CIDRAM bên ngoài thư mục `public_html` tiêu chuẩn hoặc tương đương chúng có sẵn cho hầu hết các máy chủ web tiêu chuẩn) và các quyền hạn chế thích hợp sẽ được thực thi cho thư mục nơi nó cư trú (đặc biệt, cho thư mục vault). Nếu điều đó không đủ để giải quyết mối quan ngại của bạn, hãy định cấu hình CIDRAM để các loại thông tin gây ra mối lo ngại của bạn sẽ không được thu thập hoặc nhật ký ở địa điểm đầu tiên (ví dụ, bằng cách tắt ghi nhật ký).

#### 9.4 COOKIE

CIDRAM đặt [cookie](https://vi.wikipedia.org/wiki/Cookie_(tin_h%E1%BB%8Dc)) ở hai điểm trong cơ sở mã của nó. Thứ nhất, tùy thuộc vào cách cấu hình `lockto`, CIDRAM có thể thiết lập một cookie để ghi nhớ khi người dùng đã hoàn thành CAPTCHA. Thứ hai, khi người dùng đăng nhập thành công vào front-end, CIDRAM đặt cookie để có thể nhớ người dùng cho các yêu cầu tiếp theo (cookie được sử dụng để xác thực người dùng đến phiên đăng nhập).

Trong cả hai trường hợp, cảnh báo cookie được hiển thị nổi bật (khi nó có liên quan), cảnh báo người dùng rằng cookie sẽ được đặt nếu họ tham gia vào các hành động có liên quan. Cookie không được đặt ở bất kỳ điểm nào khác trong cơ sở mã.

*Chú thích: Các API CAPTCHA "vô hình" có thể không tương thích với luật cookie ở một số khu vực pháp lý, và nên được tránh bởi bất kỳ trang web nào tuân theo các luật đó. Thay vào đó, chọn sử dụng các API được cung cấp khác, hoặc đơn giản là vô hiệu hóa hoàn toàn CAPTCHA, có thể thích hợp hơn.*

*Chỉ thị cấu hình có liên quan:*
- `captcha` -> `lockto`
- `captcha` -> `api`

#### 9.5 TIẾP THỊ VÀ QUẢNG CÁO

CIDRAM không thu thập hoặc xử lý bất kỳ thông tin nào cho mục đích tiếp thị hoặc quảng cáo, và không bán hoặc lợi nhuận từ bất kỳ thông tin được thu thập hoặc ghi lại nào. CIDRAM không phải là một doanh nghiệp thương mại, cũng không liên quan đến bất kỳ lợi ích thương mại nào, do đó, làm những việc này sẽ không có ý nghĩa gì cả. Đây là trường hợp kể từ khi bắt đầu dự án, và tiếp tục là trường hợp ngày hôm nay. Ngoài ra, làm những việc này sẽ phản tác dụng với tinh thần và mục đích dự định của toàn bộ dự án, và miễn là tôi tiếp tục duy trì dự án, sẽ không bao giờ xảy ra.

#### 9.6 CHÍNH SÁCH BẢO MẬT

Trong một số trường hợp, bạn có thể được yêu cầu về mặt pháp lý để hiển thị rõ ràng liên kết đến chính sách bảo mật của bạn trên tất cả các trang và phần trong trang web của bạn. Điều này có thể quan trọng như một phương tiện để đảm bảo rằng người dùng được thông báo đầy đủ về các thực tiễn bảo mật chính xác của bạn, loại PII bạn thu thập, và cách bạn định sử dụng. Để có thể bao gồm một liên kết trên trang "Truy cập đã bị từ chối" của CIDRAM, một chỉ thị cấu hình được cung cấp để chỉ định URL cho chính sách bảo mật của bạn.

*Chú thích: Tôi khuyên bạn không nên đặt trang chính sách bảo mật của bạn sau bảo vệ của CIDRAM. Nếu CIDRAM bảo vệ trang chính sách bảo mật của bạn, và người dùng bị chặn bởi CIDRAM nhấp vào liên kết đến chính sách bảo mật của bạn, chúng sẽ chỉ bị chặn lại, và sẽ không thể xem chính sách bảo mật của bạn. Lý tưởng nhất, bạn nên liên kết đến một bản sao tĩnh của chính sách bảo mật của bạn, chẳng hạn như một trang HTML hoặc tập tin văn bản thuần mà không được bảo vệ bởi CIDRAM.*

*Chỉ thị cấu hình có liên quan:*
- `legal` -> `privacy_policy`

#### 9.7 GDPR/DSGVO

Quy định bảo vệ dữ liệu chung (GDPR) là một quy định của Liên minh châu Âu, có hiệu lực kể từ 25 Tháng Năm 2018. Mục tiêu chính của quy định là cung cấp quyền kiểm soát cho công dân và cư dân EU về dữ liệu cá nhân của riêng họ, và thống nhất quy định trong EU về quyền riêng tư và dữ liệu cá nhân.

Quy định này bao gồm các điều khoản cụ thể liên quan đến việc xử lý "thông tin nhận dạng cá nhân" (PII) của bất kỳ "chủ đề dữ liệu" nào (bất kỳ người tự nhiên được xác định hoặc có thể nhận dạng được) từ hoặc trong EU. Để tuân thủ quy định, "enterprise" hoặc "doanh nghiệp" (theo quy định của quy định), và bất kỳ hệ thống và quy trình có liên quan nào phải ghi nhớ sự riêng tư ngay từ đầu, phải sử dụng cài đặt bảo mật cao nhất có thể, phải thực hiện các biện pháp bảo vệ thích hợp cho bất kỳ thông tin được lưu trữ hay xử lý nào (bao gồm nhưng không giới hạn trong việc thực hiện "pseudonymisation" hoặc "anonymisation" đầy đủ của dữ liệu), phải khai báo rõ ràng các loại dữ liệu mà họ thu thập, cách họ xử lý nó, vì lý do gì, trong bao lâu họ giữ nó, và nếu họ chia sẻ dữ liệu này với bất kỳ bên thứ ba nào, các loại dữ liệu được chia sẻ với bên thứ ba, cách, tại sao, vv.

Dữ liệu có thể không được xử lý trừ khi có cơ sở hợp pháp để làm như vậy, theo quy định của quy định. Nói chung, điều này có nghĩa là để xử lý dữ liệu của chủ đề dữ liệu trên cơ sở hợp pháp, nó phải được thực hiện theo nghĩa vụ pháp lý, hoặc chỉ được thực hiện sau khi có sự đồng ý rõ ràng và đầy đủ thông tin đã được lấy từ chủ đề dữ liệu.

Bởi vì các khía cạnh của quy định có thể phát triển trong thời gian, để tránh việc truyền bá thông tin lỗi thời, nó có thể là tốt hơn để tìm hiểu về các quy định từ một nguồn có thẩm quyền, trái ngược với việc chỉ bao gồm các thông tin có liên quan ở đây trong tài liệu gói (mà cuối cùng có thể trở nên lỗi thời khi quy định phát triển).

Một số tài nguyên được khuyến khích để tìm hiểu thêm thông tin:
- [REGULATION (EU) 2016/679 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex:32016R0679)
- [Quy định bảo vệ dữ liệu chung](https://vi.wikipedia.org/wiki/Quy_%C4%91%E1%BB%8Bnh_b%E1%BA%A3o_v%E1%BB%87_d%E1%BB%AF_li%E1%BB%87u_chung)

---


### 10. <a name="SECTION10"></a>NÂNG CẤP TỪ CÁC PHIÊN BẢN CHÍNH TRƯỚC ĐÓ

#### 10.0 Nâng cấp lên CIDRAM v3

Có sự khác biệt đáng kể giữa v3 và các phiên bản chính trước đó. Cách thức hoạt động của các điểm vào, cách thức cấu trúc các mô-đun, và cách thức hoạt động của trình cập nhật đối với v3 khác với cách thức hoạt động của những thứ đó đối với các phiên bản chính trước đó. Do những khác biệt này, cách tốt nhất để nâng cấp lên v3 từ các phiên bản chính trước đó là thực hiện cài đặt mới.

Nếu bạn muốn giữ nguyên cấu hình và các quy tắc phụ trợ của mình, trước khi bắt đầu quá trình nâng cấp, hãy truy cập trang sao lưu front-end. Từ đó, có thể xuất cấu hình và các quy tắc phụ trợ. Xuất sẽ khiến một tập tin được tải xuống. Sau khi nâng cấp lên phiên bản chính mới, tập tin đó có thể được sử dụng để nhập dữ liệu đã xuất trước đó vào bản cài đặt mới.

Do những thay đổi về cách cấu trúc các mô-đun, các mô-đun dành cho các phiên bản chính trước đây sẽ cần phải được viết lại để hoạt động bình thường cho v3. Di chuyển trực tiếp sẽ không hoạt động. Điều này cũng đúng với các sự kiện.

Cách cấu trúc các tập tin chữ ký không thay đổi, vì vậy các tập tin chữ ký dành cho các phiên bản chính trước đó có thể được di chuyển trực tiếp vào v3 mà không gặp bất kỳ sự cố nào.

Mới kể từ v3, mỗi mô-đun, tập tin chữ ký, và sự kiện đều có các thư mục chuyên dụng của riêng chúng (vì vậy, đối với v3, mỗi sẽ đi vào các thư mục chuyên dụng tương ứng của họ, thay vì thư mục gốc của vault).

Một số tập tin chữ ký, mô-đun, và danh sách chặn có sẵn công khai cho các phiên bản chính trước đó đã không còn được dùng nữa, vì vậy không phải mọi thứ sẽ có sẵn cho v3. Trong hầu hết các trường hợp, chúng sẽ không cần thiết nữa do các tính năng và chức năng mới được thêm vào kể từ v3.

Có một số thay đổi tinh tế đối với cách cấu trúc các quy tắc phụ trợ và có những thay đổi đối với cấu hình, nhưng nếu bạn sử dụng tính năng nhập/xuất tại trang sao lưu front-end, thì bạn sẽ không cần phải viết lại, điều chỉnh, hoặc tạo lại bất kỳ thứ gì theo cách thủ công. Khi nhập, CIDRAM biết những gì cần thiết và sẽ tự động xử lý cho bạn.

Để biết danh sách các thay đổi được giới thiệu trong v3 (ví dụ, tính năng được thêm vào, tính năng bị xóa, vv), hãy tham khảo [nhật ký thay đổi v3](https://github.com/CIDRAM/CIDRAM/blob/v3/Changelog.md#v300).

#### 10.1 Nâng cấp lên CIDRAM v4 từ phiên bản cũ hơn CIDRAM v3

Xem ở trên: Nên cài đặt mới.

#### 10.2 Nâng cấp lên CIDRAM v4 từ CIDRAM v3

1. Đầu tiên, hãy vào trang cập nhật và nếu có bản cập nhật nào khả dụng, hãy đảm bảo cài đặt tất cả. Điều này đảm bảo bất kỳ mã nào cần thiết cho việc cập nhật đều có sẵn và giúp giảm bớt những gì trình cập nhật cần phải làm sau này.

2. Vào trang cấu hình và tìm __`frontend➡remotes`__. Trong danh sách, nơi bạn thấy `/v3/`, hãy đổi thành `/v4/`. Nhấp vào cập nhật để lưu cấu hình của bạn. Thay đổi này cho trình cập nhật biết phải nhắm đến phiên bản chính xác khi tìm kiếm bản cập nhật.

3. Vào trang sao lưu. Chọn xuất, đánh dấu vào hộp kiểm để cấu hình, để số liệu thống kê, và để quy tắc phụ trợ, sau đó nhấn OK để tải xuống bản sao lưu. Đã có một số thay đổi. Ví dụ, hành động "không ghi nhật ký" đã bị xóa khỏi các quy tắc phụ trợ (có thể sử dụng tùy chọn "đàn áp nhật ký" thay thế để đạt được mục đích tương tự). Bạn sẽ cần nhập bản sao lưu này trở lại CIDRAM sau khi nâng cấp.

4. Quay lại trang cập nhật. Bản cập nhật cho phiên bản chính mới hiện đã xuất hiện. Để tránh hết thời gian chờ, trước khi cập nhật tất cả, hãy thử cập nhật core hoặc front-end (vì cả hai đều phụ thuộc lẫn nhau, cập nhật một sẽ tự động cập nhật cả hai). Vì cấu trúc trang và kiểu CSS đã thay đổi đáng kể giữa các phiên bản chính nên ban đầu có vẻ như bị hỏng sau khi cập nhật; nhưng không phải vậy. Vào bất kỳ trang nào khác và nhấn Ctrl+F5 để thử thực hiện làm mới cứng (tức là, làm mới trong đó trình duyệt sẽ lấy một bản sao mới của kiểu CSS và các thành phần ngoại vi khác thay vì dựa vào bộ nhớ đệm của trình duyệt). Nếu không được, hãy thử xóa bộ nhớ đệm của trình duyệt.

5. Sau khi thực hiện xong, bạn có thể cập nhật mọi thứ khác. Quay lại trang cập nhật, và nếu bạn thấy nút ở đầu trang, hãy nhấp vào cập nhật tất cả.

6. Để đảm bảo không còn bất kỳ bản cập nhật lỗi hoặc tập tin bị hỏng nào còn sót lại, và để đảm bảo mọi thứ đều ổn, hãy nhấp vào sửa chữa tất cả. Rất hiếm khi đây thực sự là vấn đề, nhưng tốt hơn hết là nên cẩn thận.

7. Quay lại trang sao lưu. Chọn nhập, đánh dấu vào hộp kiểm để cấu hình, để số liệu thống kê, và để quy tắc phụ trợ, nhấp vào nút để chọn chọn tập tin, định vị và chọn bản sao lưu bạn đã tải xuống trước đó, rồi nhấn OK để nhập bản sao lưu đó. CIDRAM sẽ tự động thực hiện bất kỳ điều chỉnh nào cần thiết để thích ứng với những thay đổi.

8. Bạn đã hoàn tất việc nâng cấp. Phiên bản chính mới không đưa ra bất kỳ thay đổi nào đối với tập tin chữ ký, mô-đun, hoặc sự kiện, do đó bạn không cần phải lo lắng về điều đó khi nâng cấp. Tiếp theo, bạn có thể muốn khám phá sơ qua trang cấu hình do những thay đổi được đưa ra trong phiên bản chính mới (ví dụ, đối với các tính năng mới được giới thiệu).

Để biết danh sách các thay đổi được giới thiệu trong v4 (ví dụ, tính năng được thêm vào, tính năng bị xóa, vv), hãy tham khảo [nhật ký thay đổi v4](https://github.com/CIDRAM/CIDRAM/blob/v4/Changelog.md#v400).

---


Lần cuối cập nhật: 2026.04.01.
