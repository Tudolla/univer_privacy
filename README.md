# Chính sách quyền riêng tư và trang xóa tài khoản UNI

Trạng thái: **chưa công bố; còn thông tin lưu/xóa dữ liệu cần hoàn thiện**.

Hai trang HTML độc lập, không có JavaScript, font ngoài, quảng cáo hoặc công cụ
phân tích. Nội dung được cập nhật ngày 07/10/2026 và đối chiếu với luồng xóa
tài khoản Flutter/Phoenix. Việc này không xác minh cấu hình Firebase, bản sao lưu hoặc triển
khai production. Không dùng các trang còn placeholder để nộp Google Play.

- [index.html](index.html): Chính sách quyền riêng tư.
- [delete-account.html](delete-account.html): hướng dẫn gửi yêu cầu xóa bằng
  email, không buộc người dùng cài lại app.

## Thông tin đã cập nhật

- Email hỗ trợ, quyền riêng tư và yêu cầu xóa: **eduino.info@gmail.com**.
- Thời hạn xử lý yêu cầu xóa: **1 tuần (7 ngày) sau khi xác minh quyền sở hữu**;
  trả kết quả qua email. Mốc bắt đầu cần được chủ ứng dụng xác nhận.
- Nhà phát triển trên hai trang: **EDO UNI**, theo nội dung đã có trong trang
  xóa tài khoản; cần đối chiếu với tên thực tế trên Google Play.

## Thông tin cần hoàn thiện trước khi công bố

Thay tất cả các mục sau trên cả hai trang bằng thông tin thực:

| Placeholder | Nội dung cần xác nhận |
| --- | --- |
| `[NGAY_CO_HIEU_LUC]` | Ngày bắt đầu áp dụng chính sách đã hoàn thiện. |
| `[CHINH_SACH_LUU_NHAT_KY_VA_HO_TRO]` | Loại dữ liệu, thời hạn lưu và lý do nếu còn dữ liệu sau khi xóa tài khoản. Xác nhận cả nhật ký của nhà cung cấp. |
| `[CHINH_SACH_LUU_VA_XOA_SAO_LUU]` | Có sao lưu hay không, thời gian hết hạn/xóa, cách xử lý dữ liệu đã xóa khi khôi phục. Không hứa số ngày chưa được triển khai. |
| `[CHINH_SACH_XOA_HO_SO_FIREBASE]` | Cách xử lý bản ghi Firebase Authentication, thời hạn và trường hợp tiếp tục giữ để phục vụ tài khoản HHA còn hoạt động. |

Thông báo soạn thảo nội bộ đã được bỏ khỏi hai trang HTML. Cập nhật ngày ở
đầu chính sách theo thời điểm áp dụng nội dung đã hoàn thiện.

## Các điểm cần xác minh từ mã hiện tại

1. **Liên kết trong app:** chưa thấy đường dẫn chính sách trong Flutter. Google
   yêu cầu có link hoặc nội dung chính sách trong app, ngoài URL ở Play Console.
   Cần gắn URL đã công bố vào vị trí dễ tìm, kể cả trước khi đăng nhập.
2. **Xóa dữ liệu xác thực:** nút Xóa tài khoản gọi
   `DELETE /api/uni/me` (mã app: `lib/screen/login/repository/auth_api_client.dart`),
   sau đó xóa phiên cục bộ và đăng xuất Google/Firebase. Luồng
   `Accounts.delete_uni_account/1` (mã backend: `lib/high_hha/accounts.ex`)
   xóa dữ liệu UNI và giữ định danh chung nếu còn membership của app khác.
   Chưa thấy lệnh xóa bản ghi Firebase Authentication trong luồng này.
   Đăng xuất Firebase không phải xóa hồ sơ xác thực. Cần có quy trình xóa tại
   nhà cung cấp, tự động hoặc tác nghiệp được kiểm chứng, cho tài khoản không
   còn cần hồ sơ xác thực; không chỉ thêm câu “xóa toàn bộ” vào chính sách.
3. **Xóa qua email:** email thực phải có người theo dõi, xác minh và thực hiện
   xóa. Trang GitHub Pages chỉ mở email, không tự gọi API hoặc tự xóa dữ liệu.
   Không yêu cầu gửi mật khẩu, token hoặc OTP; không làm khó người đã gỡ app.
4. **Focus cục bộ:** dữ liệu phiên và âm thanh được lưu trên thiết bị, tồn tại
   qua đăng xuất/xóa tài khoản theo mã hiện tại. Chính sách ghi rõ phạm vi này.
5. **Production:** xác minh API đang chạy có các chức năng và phạm vi xóa giống
   mã đã xem. Xác nhận Fly.io/Cloudflare vẫn là các nhà cung cấp được sử dụng,
   thời gian lưu nhật ký/sao lưu và quyền truy cập dữ liệu thực tế.
6. **Đối tượng sử dụng:** đối chiếu nội dung dành cho sinh viên với Target
   audience trong Play Console; không tự chọn nhóm trẻ em hoặc thêm cam kết
   về độ tuổi chưa được xác nhận.

## Đăng lên GitHub Pages

Repository hiện tại: [Tudolla/univer_privacy](https://github.com/Tudolla/univer_privacy).
Hai trang HTML nằm ở thư mục gốc; `.nojekyll` giúp GitHub Pages phục vụ HTML
tĩnh trực tiếp. Repository này chỉ chứa tài liệu công khai; không đưa source
app, keystore, key.properties hoặc thông tin production vào đây.

1. Sau khi hoàn thiện các mục còn thiếu, commit và push `index.html`,
   `delete-account.html`, `.nojekyll` và tài liệu vào branch `main` của repo này.
2. Trong GitHub chọn **Settings → Pages → Deploy from a branch**, chọn branch
   `main`, thư mục `/(root)`, rồi Save.
3. Chờ GitHub báo đã deploy; mở hai URL bằng cửa sổ ẩn danh, không đăng nhập:
   - Privacy policy: `https://tudolla.github.io/univer_privacy/`
   - Account deletion: `https://tudolla.github.io/univer_privacy/delete-account.html`
4. Kiểm tra HTTPS, đọc được trên điện thoại, không yêu cầu đăng nhập, không
   giới hạn địa lý, các email và liên kết hoạt động, không còn placeholder.
5. Điền URL chính sách và URL xóa tài khoản vào đúng các mục ở Play Console.
   Thêm link chính sách vào app và build lại AAB nếu bản phát hành chưa có link.

Không cần dùng PDF, Google Docs có quyền chỉnh sửa hoặc URL của trang source
trên GitHub. Dùng URL của **GitHub Pages đã hoạt động**.

Kiểm tra ngày 07/10/2026: cả hai URL dự kiến trả về HTTP 404, chưa dùng để nộp.
Kiểm tra lại sau khi triển khai; trạng thái này có thể thay đổi.

## Đối chiếu Data safety trước khi nộp

Đây là gợi ý dựa trên mã, không phải tờ khai đã xác minh trên production:

| Dữ liệu trong app | Nhóm cần đối chiếu trong Data safety | Mục đích thấy trong mã |
| --- | --- | --- |
| Tên, email, mã người dùng | Personal info: Name, Email address, User IDs | Account management, App functionality. |
| URL ảnh đại diện từ đăng nhập | Kiểm tra cách Google phân loại dữ liệu ảnh/profile được thực sự truy cập và tải | Hiển thị danh tính. Không có tính năng tải ảnh do người dùng chọn. |
| Trường, tháng nhập học/tốt nghiệp, GPA | Personal info: Other info, và nhóm phù hợp với cách nhập thực tế | App functionality. |
| Tiền chu cấp, tiết kiệm, tự kiếm | Financial info: Other financial info | App functionality. Không phải lịch sử mua hàng hoặc dữ liệu thẻ. |
| Nội dung kế hoạch | App activity: Other user-generated content | App functionality. |
| Góp ý kèm tên/email | App activity: Other user-generated content, và thông tin cá nhân đi kèm | App functionality, Developer communications khi có tương tác hỗ trợ. |
| IP và thông tin kỹ thuật của Firebase/hạ tầng | Đối chiếu tài liệu SDK và cách sử dụng thực tế; không tự coi mọi IP là GPS hoặc mọi Firebase App ID là device ID | Fraud prevention, security; vận hành/xác thực theo nhà cung cấp. |
| Trạng thái Focus chỉ lưu trên thiết bị | Không khai là dữ liệu gửi tới server nếu bản phát hành vẫn chỉ xử lý cục bộ | App functionality trên thiết bị. |

- Không khai “không thu thập dữ liệu”: đăng nhập và dữ liệu học tập/Money đang
  được gửi tới máy chủ, và SDK xác thực cũng xử lý dữ liệu.
- Đánh dấu bắt buộc/tùy chọn theo trải nghiệm thực tế. Dữ liệu gửi lên server
  và lưu lâu dài không thuộc trường hợp “chỉ xử lý tạm thời”.
- “Có nhà cung cấp xử lý dữ liệu” trong chính sách và “Data shared” của biểu
  mẫu có định nghĩa khác nhau. Đánh giá ngoại lệ service provider theo điều
  khoản và cách sử dụng thực tế; không tự chọn Yes/No chỉ từ tên nhà cung cấp.
- Chỉ khai dữ liệu mã hóa khi truyền, cơ chế xóa và các mục khác sau khi đã
  kiểm tra toàn bộ đường truyền, bản phát hành và cấu hình dịch vụ liên quan.
- Nếu thêm SDK, quảng cáo, analytics, crash reporting hoặc quyền mới, cập nhật
  cả chính sách và Data safety. Phát hành bản mới không tự cập nhật hai mục này.

## Nguồn đối chiếu

- [Google Play User Data — Privacy policy](https://support.google.com/googleplay/android-developer/answer/10144311?hl=en).
- [Google Play account deletion](https://support.google.com/googleplay/android-developer/answer/13327111?hl=en).
- [Google Play Data safety](https://support.google.com/googleplay/android-developer/answer/10787469?hl=en).
- [Firebase Android data disclosure](https://firebase.google.com/docs/android/play-data-disclosure#authentication).
- [Firebase privacy/security](https://firebase.google.com/support/privacy).
- [GitHub Pages setup](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).

Các nguồn này hỗ trợ yêu cầu và khai báo; chúng không chứng nhận chính sách
hoặc app đã được Google duyệt.
