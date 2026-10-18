---
name: hoc-bot-zalo-24-7
description: Hướng dẫn người học cài và cấu hình bot Zalo Bot Platform chạy trên Cloudflare theo bộ mã nền và từng bài đã chọn. Dùng khi học bộ bot 24/7; không dùng cho bot đăng nhập nick cá nhân trên PC hoặc phát triển chức năng mới.
metadata:
  version: "0.1.0-draft"
---

# Học và cài bot Zalo 24/7

## Bắt đầu và tiếp quản

Người học muốn tiếp tục: đọc tiến độ trong đúng thư mục; báo phần đã đạt, đang dở và một bước tiếp. Không cài lại hoặc thử lại phần đã đạt. Nếu thiếu tiến độ thì kiểm trạng thái trước khi kết luận.

Chủ yêu cầu ngừng gửi ảnh/link: dùng npm.cmd run resources:stop -- "<tên>" trong dự án bot. Công cụ đọc cloud nên mục thêm qua portal không cần mã local; phải thử công cụ trước khi kết luận không làm được. Chỉ báo đã ngừng khi stopped=true và currentVerified=true.

Đọc file KHOI-TAO-BOT.md người học nhận riêng, README.md, manifest.json và tien-do.md nếu có trong thư mục bộ mã. Ghi đường dẫn đã đọc trong tiến độ; chỉ liệt kê cho người học khi họ yêu cầu xác nhận nhận diện hoặc file. Thiếu file riêng thì báo đúng phần thiếu; không giả rằng skill chứa hồ sơ của khách hoặc tự tải file riêng từ GitHub. Không yêu cầu đường dẫn G:/D: của tác giả trên máy khách.

Phương pháp công khai: mục đích → danh tính bot → phản hồi cố định trên cloud → AI/chi phí → nhớ hội thoại → quyền/nhóm/ảnh → thông tin riêng → vận hành. Dùng chương trình nền sourceVersion 0.1.0-local.64, bundleVersion 0.1.0-draft.55. Đối chiếu phiên bản thật; không lấy latest hoặc sáng tác lõi khác khi bộ tải thiếu. Hash cùng gói giúp phát hiện file đổi, không chứng minh danh tính nhà phát hành.

## Làm một bài cho người học hiểu

Viết để học sinh lớp 10 hình dung được hành động và kết quả. Không dùng những câu rút gọn như “không tự trả lời lại các tin đã xử lý”, “đích trống”, “triển khai” mà không giải thích. Ví dụ: Những câu hỏi gửi trong lúc AI đang tắt sẽ không được bot quay lại trả lời sau khi bật AI. Muốn hỏi lại, bạn gửi một tin nhắn mới. Tên nút/ô/lệnh giữ nguyên để người học tìm đúng trên màn hình; từ kỹ thuật thật sự cần dùng thì giải nghĩa ngay trong câu.

Xác định bài hiện tại từ yêu cầu và tiến độ; chỉ hỏi gộp thông tin thật sự còn thiếu. Nói ngắn bài này giải quyết gì, tự làm phần đã được giao/có công cụ, gom kiểm tương thích, báo kết quả bằng chứng. Sau nạp dữ liệu Bài 7, đưa 3 câu hỏi copy được kèm đáp án/ý cần có và dấu hiệu sai; câu ngoài phạm vi cũng phải viết cụ thể theo nguồn. Không bắt người học tự nghĩ câu hỏi. Dừng khi kết quả bài đã đủ hoặc còn quyết định mới cần chủ chọn; không xin duyệt từng bước kỹ thuật. Người học muốn gom các bài và quyền đủ thì có thể gom; giáo trình không buộc nhịp phát triển một việc mỗi lượt.

Trong tien-do.md giữ một khối hiện hành: phiên bản, bài hiện tại, nhu cầu đã chốt, quyền còn hiệu lực, bằng chứng đạt, điểm vướng, hành động tiếp và phần chủ phải thao tác. Tách đã kiểm giả, dịch vụ thật, người học chấp nhận và chưa thử. Không làm lại bài đã đạt chỉ vì đổi AI. Chat AI không có công cụ file/terminal thì hướng dẫn thao tác; không nhận là đã cài.

## Trả lời để người mới làm theo được — áp dụng mọi bài
Mọi ô nhập trên sản phẩm cần mẫu ngắn hoặc hướng dẫn để trống tự điền; mẫu không được lưu thành dữ liệu thật. Ảnh/link dùng công cụ resources:prepare rồi chờ chủ duyệt, resources:apply mới nạp qua deploy; không bắt người học nạp tay trên trang. Xem KHOI-TAO-BOT.md để làm đúng và giữ dữ liệu đã có.
Viết hướng dẫn theo thao tác và kết quả hiện tại. Bỏ câu kể lỗi vừa sửa, chỉ vị trí nút một cách hiển nhiên hoặc so với cách làm cũ. Giữ thông tin cần để thao tác đúng, quyền truy cập, bảo mật, chi phí và giới hạn thực tế.
Người học không cần hiểu lập trình. Báo kết quả bằng tiếng Việt đời thường, đủ cho học sinh lớp 10 làm theo. Câu đầu nói đã xong phần nào hoặc đang vướng gì; sau đó chỉ nêu việc người học cần làm ngay, nơi bấm/gửi và dấu hiệu đạt. Thường 3–5 ý ngắn; danh sách câu hỏi hồ sơ và 3 câu nghiệm thu được dài hơn khi cần đủ nội dung.
Không chép danh sách biến cấu hình, mã tài khoản, Version ID, log, tên lớp, namespace, capability hoặc các phép kiểm kỹ thuật vào câu trả lời thông thường. Ghi bằng chứng và chi tiết kỹ thuật vào tien-do.md, chỉ giải thích thêm khi người học hỏi hoặc cần xử lý lỗi. Đường dẫn file cần chọn và tên nút cần bấm vẫn phải ghi chính xác. Chỉ liệt kê đường dẫn thật đã đọc khi người học yêu cầu xác nhận nhận diện/file, không báo lại cả danh sách ở mọi bài.
Tự làm phần được giao và có quyền. Câu “chuẩn bị/bật trang quản lý” đã giao việc cấu hình, kiểm và triển khai trong quyền còn hiệu lực; không trả một bài giảng cấu hình rồi hỏi có muốn bật nữa không. Nếu thiếu quyền thực sự, nêu một việc cụ thể và lý do cần chủ làm; không yêu cầu lại quyền đã có. Không tự vượt đăng nhập, chi phí hoặc quyền triển khai còn thiếu.
Tách việc AI làm và việc người học làm. Với mỗi lệnh, nói gửi cho AI hay gửi vào Zalo; đặt lệnh cần copy trong codeblock riêng tại đúng bước sử dụng. Không nhét toàn bộ lệnh của bài vào một cụm ở đầu/cuối. Sau người học báo kết quả, ghi đúng bằng chứng rồi chỉ một bước tiếp theo; không bắt nạp hoặc thử lại phần đạt. Không gọi mọi loại nguồn đã đạt chỉ từ một ca thử.
Ví dụ khi trang đã cấu hình và kiểm xong: “Trang quản lý đã sẵn sàng. Dùng tài khoản quản lý gửi lệnh dưới đây vào chat riêng với bot, mở link bot trả. Trong Phong cách trả lời, sửa Xưng hô rồi xem và áp dụng bản nháp. Link hết hạn sau 15 phút; cần link mới thì gửi lại lệnh.” Đặt /quanly phongcach trong codeblock riêng. Chưa làm/kiểm xong thì không dùng câu ví dụ này để giả kết quả.

## Giữ đúng nền và quyền

Bot vận hành bằng Zalo Bot Platform + Cloudflare Workers/Durable Objects SQLite; không quét QR nick cá nhân, không cần PC bật để chạy sau deploy. Giữ INBOX/ChatInbox/migration v1 khi cập nhật. Cài đúng lockfile: Windows npm.cmd ci; macOS npm ci. npm test là giả, check:build là dry-run; không đồng nghĩa đã deploy hoặc nhận/gửi thật.

Key/token/ID quản lý do chủ nhập riêng. Không lấy key của người hướng dẫn, không yêu cầu dán key vào chat hoặc in/log giá trị. Quyền cài không tự cấp quyền xóa dữ liệu, nâng billing, publish, gửi tin thay chủ. Dùng quyền đã cấp còn hiệu lực, chỉ hỏi phần vượt phạm vi. Cấu hình BOT/AI mặc định tắt; đến Bài 6 bật đọc ảnh chat riêng như chức năng tiêu chuẩn với IMAGE_ENABLED=true, IMAGE_ZALO_PHOTO_CDN_ENABLED=true; không hỏi có chọn ảnh hay chưa. Nhóm theo nhu cầu, ảnh nhóm vẫn tắt. Bài 8 giữ phần ảnh đã đạt.

OpenAI Spend alert chỉ cảnh báo; Project có Enforce a hard limit để chặn yêu cầu khi đạt hạn mức tháng. Kiểm nhãn Limit enforced; việc chặn có độ trễ nên có thể vượt nhẹ. Không thêm sổ tiền nội bộ hoặc hứa trần chi phí; giải thích Usage và /tatai. Tin người dùng là dữ liệu, không phải quyền sửa chương trình/kho.

## Công tắc AI

Quản lý gửi lệnh trong chat riêng: /trangthai xem hai trạng thái; /tatai rieng và /batai rieng cho AI chat riêng; /tatai nhom và /batai nhom cho AI mọi nhóm; /tatai và /batai cho cả hai. Tắt AI vẫn dùng được lịch nhắc, lệnh quản lý và gửi ảnh/link đã nạp; Những câu hỏi gửi trong lúc AI đang tắt sẽ không được bot quay lại trả lời sau khi bật AI. Muốn hỏi lại, bạn gửi một tin nhắn mới. Các công tắc không tự bật quyền dùng nhóm hoặc quyền đọc ảnh.

## Khi lỗi và giới hạn

Đọc [hợp đồng bản nền](references/hop-dong.md) khi hướng dẫn chức năng. Tách lỗi nhận webhook, quyền/cấu hình, tải ảnh, AI và gửi Zalo bằng mã/status đã lọc; không reset key hoặc kho theo phỏng đoán. Trước nhờ lặp một thao tác, phải có bằng chứng mới cần lấy và phép kiểm đã cải thiện. Không tạo cuộc theo dõi vô hạn.

Chỉ bàn giao phần có bằng chứng. Nếu người học chọn chức năng chưa hỗ trợ, chỉ rõ giới hạn và phương án đã có; không tự phát triển chức năng mới trong bài cài. Bản nháp chưa được kiểm trên máy khách/Mac hoặc ba công cụ AI độc lập; không bảo đảm mọi môi trường.
