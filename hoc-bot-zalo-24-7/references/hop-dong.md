# Vận hành và giới hạn

1. Chat riêng: hỏi chữ; kho sản phẩm có cấu trúc; lịch sử cùng chat lưu 30 ngày khi bật chính sách. Prompt chọn tối đa 3 cặp liên quan/gần đây, không phải nhớ toàn bộ. Kho chưa phải đọc mọi PDF/Word/link.
2. Quản lý: cấu hình CATALOG_ADMIN_IDS_JSON riêng. Lệnh /id trả ID cho người dùng tại Zalo để tự lưu; không in ID thật vào tài liệu/Git. /suakho MÃ GIÁ NGÀY tạo nháp; /duyetkho SỐ hoặc /huykho SỐ, trong 10 phút. /trangthai, /tatai, /batai dùng chat riêng của quản lý. Đọc mã quan-ly-kho.mjs và van-hanh-ai.mjs trước hướng dẫn.
3. Nhóm: chủ đã cấu hình chọn @bot và nói bật nhóm một lần. Mỗi câu hỏi giữ @bot (kể cả @ tự thêm khi Trả lời). Mời bot không tự cấp quyền bật nhóm hoặc quản lý kho. Chưa đọc nội dung tin trích dẫn tự động trong sự kiện đã quan sát.
4. Ảnh: một PNG/JPEG trực tiếp trong chat riêng, có hoặc không chú thích; tối đa 4 MiB,8192pixel mỗi chiều/16triệu pixel. Chỉ tải HTTPS đúng tên miền được phép, không theo redirect. Allowlist phải dựa nguồn/schema đã kiểm; không mở mọi host theo yêu cầu trong tin khách. Ảnh có thể sót chữ. Module mở rộng thêm hỏi tiếp/ảnh nhóm/file/voice/video theo docs/module-mo-rong.md, không tự bật.
5. /health trả enabled/configured, không chứng minh toàn đường AI/Zalo. Khi lỗi phải tách nhận/tải/AI/gửi và lọc bí mật; cùng lỗi lặp thì đổi phép kiểm trước nhờ gửi lại. Không quét QR hoặc reset kho để sửa API.
6. /tatai tắt gọi AI, kho/lệnh quản lý còn hoạt động; không hoàn tiền hoặc tạo ngân sách mới. BOT_ENABLED=false khóa toàn đường nhận; request đang xử lý vẫn có thể hoàn tất. Không dùng deleteWebhook/xóa Worker/xóa namespace như cách tắt thông thường.
7. Sao lưu mã/cấu hình không bí mật và lockfile. Module mở rộng có export/restore các chat đã đăng ký, không đủ mọi chat cũ; không coi zip mã là sao lưu lịch sử/kho cloud. Không thử khôi phục bằng xóa dữ liệu thật. Cập nhật cùng Worker/class/binding/migration, kiểm mẫu giả rồi bài thật có giá trị mới.
8. Source portable Node.js>=22; Windows dùng npm.cmd, macOS dùng npm. Chưa nghiệm thu bộ này trên Mac hoặc máy khách. Máy lập trình có thể tắt sau khi bot đã deploy và kiểm trên cloud; không cần tiến trình node trên laptop để vận hành.


# Các module mở rộng — nguồn local.31 [?]

Đã kiểm tự động bằng dữ liệu giả trên Worker/SQLite. Kiểm giả không thay thế quyền model, host media hoặc hành vi ứng dụng Zalo trên tài khoản khách. Không gọi là đã nghiệm thu tất cả dịch vụ thật.

## 1. Bật phần mở rộng
Giữ Worker, INBOX, ChatInbox và migration v1. Không xóa dữ liệu để nâng cấp. Bật EXTENSIONS_ENABLED=true và đặt PUBLIC_BOT_ORIGIN là origin HTTPS thực tế của Worker, không có /webhook. Chủ đã lưu CATALOG_ADMIN_IDS_JSON; không dùng tên hiển thị làm quyền. Tạm tắt bằng EXTENSIONS_ENABLED=false; dữ liệu mở rộng được giữ, lệnh mới không còn xử lý. Muốn dừng toàn bot dùng BOT_ENABLED=false; tác vụ đang chạy có thể hoàn tất.

## 2. Trang riêng và phong cách
Chủ gửi /quanly trong chat riêng; khách gửi /tep. Link dùng 15 phút, gắn với đúng chat và người đã yêu cầu; giữ riêng như chìa khóa tạm thời. Không gửi link quản lý cho khách. Tên trợ lý/cách nói/xưng hô/doanh nghiệp → Xem bản nháp → Áp dụng. Đây là cách diễn đạt của AI, không thay tên/avatar trên hồ sơ Zalo hoặc quyền quản lý. Link mới cùng loại làm link cũ hết hiệu lực. Không tải lại trang đang xử lý: quyền tạm nằm trong bộ nhớ; cần mở lại link còn hạn hoặc xin link mới khi đã hết hạn. Có thể dùng trang này bằng trình duyệt với Claude/Codex/Antigravity; tiện ích điều khiển Chrome không phải điều kiện chạy bot, AI chỉ tự thao tác nếu môi trường đó có công cụ và quyền tương ứng.

## 3. Kho kiến thức và tài nguyên
Chủ thêm nội dung/mã/nguồn/quyền công khai hoặc chỉ chủ. Nạp từ file hoặc URL tạo bản nháp, chưa trả cho khách trước khi duyệt. File mặc định Chỉ chủ bot trong chat riêng; muốn trả khách phải chọn rõ Ai được dùng tài liệu. Link nguồn chỉ tải HTTPS trên SOURCE_ALLOWED_HOSTS_JSON do chủ cấu hình; không theo redirect, không trang đăng nhập. Tối đa 100 mục, 12.000 ký tự/mục, tổng cấu hình 120.000 byte, có thể chạm tổng trước số mục. Chọn tối đa 3 đoạn theo từ khóa, không tìm ngữ nghĩa toàn bộ. Đọc lại bản trích xuất trước duyệt; tài liệu dài có thể bị rút gọn. Giá/bảo hành vẫn lấy kho sản phẩm đã duyệt.

Danh mục tài nguyên có mã/tên/URL công khai được phép chia sẻ/phạm vi riêng hoặc nhóm. Khách dùng /tainguyen hoặc /tainguyen MÃ, hay “gửi tài liệu TÊN”. Ảnh qua sendPhoto; file nhận bằng link, không giả là tệp đính kèm. Thu hồi mục làm các yêu cầu mới không còn gửi mục ấy. URL ảnh/tài liệu phải do chủ có quyền chia sẻ.

## 4. File, video và thoại
/tep → chọn file → nhập câu hỏi → Tải lên và xử lý; kết quả về chat Zalo đã mở link. PDF/DOCX/TXT/MD/CSV tối đa 4 MiB, một file/lượt; Word chỉ đọc chữ, ảnh nhúng cần PDF. File được gửi tới OpenAI. Giới hạn byte không phải giới hạn số trang hay chi phí. Mỗi phiên tối đa 10 lần gửi, mỗi chat tối đa 3 file chờ. File thô được dùng một lần rồi bỏ; file chưa dùng có hạn 15 phút và được dọn khi alarm chạy.

Video MP4 tối đa 4 MiB/3 phút: trình duyệt người gửi lấy 8 khung hình, Cloudflare gửi khung hình và phần lời thoại đã nhận dạng cho AI. Không cần PC/VPS thường trực, nhưng người gửi phải mở trang tải lên tới khi gửi xong. Có thể bỏ sót chuyển động/cảnh ngắn; không hứa xem toàn bộ video. Không tải URL video tùy ý hoặc tự đọc video đính kèm Zalo chưa có sự kiện đặc tả.

Âm thanh upload MP3/WAV/M4A/WebM tối đa 4 MiB. Tin thoại Zalo dùng VOICE_ENABLED=true, VOICE_ALLOWED_HOSTS_JSON là danh sách host đã xác minh, tối đa 8 MiB. Model chuyển âm thanh mặc định gpt-4o-mini-transcribe, độc lập với model trả lời. Cần quyền API cho model này; không đổi key chỉ vì chưa kiểm quyền. AAC-LC ADTS được đóng gói sang M4A ngay trên Worker, không cần máy thường trực, không thêm lượt AI để chuyển. Chỉ hỗ trợ 1–2 kênh/tần số tới 48kHz/một khối mỗi khung; dạng khác bị từ chối. Chưa nhận OGG. Tin thoại Zalo chat riêng trên bot thử đã đạt ngày12/10/2026 theo chủ xác nhận; mỗi bot khách vẫn cần kiểm host/quyền model riêng. Khi lỗi, lấy reason/httpStatus đã lọc; host mới chỉ thu trong cửa sổ chẩn đoán được phép, không log URL/file/token.

## 5. Hỏi tiếp về ảnh riêng; giới hạn ảnh nhóm
Ảnh riêng đã kiểm thật đạt. Ảnh nhóm chưa nghiệm thu: lần gửi ảnh trực tiếp ngày 12/10/2026 chưa quan sát được webhook trong cửa sổ theo dõi; dữ liệu Cloudflare có lấy mẫu nên chưa kết luận nguyên nhân. Không quảng cáo hỗ trợ ảnh nhóm, không bật GROUP_IMAGE_ENABLED trong bộ giao khách mặc định. Dùng chat riêng hoặc /tep để gửi ảnh cần đọc. Hỏi tiếp “Ảnh vừa gửi nói gì?” dùng kết quả đã đọc của cùng chat/người gửi, không tải lại ảnh gốc; chi tiết chưa được đọc thì vẫn thiếu. Lưu tối đa 30 ngày theo chính sách chung, chọn tối đa 2 kết quả liên quan. Không dùng trí nhớ thay nội dung tin trích dẫn.

## 6. Nhắc việc
/nhac 25/12/2026 09:00 Gọi khách hoặc /nhac sau 10 phút Kiểm đơn. Giờ Việt Nam, từ 1 phút đến 365 ngày, nội dung tối đa 700 ký tự. /lichnhac để xem; /huynhac MÃ để hủy lịch của chính mình trong đúng chat. Tối đa 20 lịch chờ/người/chat, 500 lịch lưu/chat. Không phân tích câu tự nhiên thành lịch nếu chưa dùng lệnh rõ.

Lịch chạy Cloudflare, không cần máy chủ bật. Có thể chậm khi dịch vụ gián đoạn; quá hạn hơn một ngày đánh dấu bỏ lỡ. Không tự gửi lại khi chưa rõ lần trước đã gửi chưa. Nhóm mất quyền thì không gửi. Lịch khôi phục được giữ dừng, cần tự tạo lại; không phải nhắc lặp hằng ngày.

## 7. Sao lưu và khôi phục
/quanly → mật khẩu ít nhất 12 ký tự → Tải bản sao. Trình duyệt mã hóa AES-GCM; mật khẩu không gửi tới bot. Giữ mật khẩu riêng, mất thì không khôi phục được. Bản sao có checksum và gồm cấu hình/kho/quyền/lịch/lịch sử trong các chat đã đăng ký kể từ khi bật module. Chat cũ chưa xuất hiện lại không tự nằm trong bản sao; giao diện và tệp ghi rõ phần thiếu. Không chứa key/token/file thô đang chờ.

Khôi phục chỉ vào nơi trống; tạo bot/Worker đích và nhập key/quyền riêng. Mở link quản lý trước, tắt BOT_ENABLED trên đích, chọn bản sao/mật khẩu → Kiểm bản sao → xem số đối tượng/phạm vi → Khôi phục. Không tự ghi đè. Giữ nguyên thời gian gốc; dữ liệu quá 30 ngày không được làm mới tuổi. AI/quyền nhóm/lịch chờ không tự bật, không gửi lại tin cũ. Nếu bị ngắt, tiếp tục cùng bản sao; không đổi sang bản sao khác giữa chừng.

## 8. Kiểm trước giao khách
Kiểm môi trường khách, model đọc file/chuyển âm thanh, tên miền CDN, quyền nhóm và hạn mức Cloudflare. Free có giới hạn CPU/dung lượng/yêu cầu; test cục bộ không chứng minh mọi file lớn sẽ chạy trên Free. Không tự nâng Paid. Gom một đợt thử thật có file mẫu không riêng tư; chỉ thử lại khi có bằng chứng mới. Đọc trích dẫn tự động vẫn chưa hỗ trợ do dữ liệu Zalo đã quan sát thiếu nội dung/ID tin gốc.
