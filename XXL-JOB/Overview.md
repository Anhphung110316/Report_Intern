# 1. Tổng quan

* XXL-JOB là một khung lập lịch tác vụ phân tán, mục tiêu thiết kế cốt lõi là phát triển nhanh chóng, học tập đơn giản, nhẹ, dễ mở rộng hiện là nguồn mở và có thể truy cập vào một số dòng sản phẩm trực tuyến của công ty.

# 2. Tính năng

(1) **CRUD dễ sử dụng**: Hỗ trợ thao tác CRUD trên tác vụ qua giao diện web đơn giản, nhanh chóng.

(2) **Sửa đổi trạng thái động**: Cho phép bắt đầu/dừng hoặc chấm dứt tác vụ tức thì.

(3) **Trung tâm điều độ HA**: Sử dụng thiết kế cụm "Trung tâm điều độ" đảm bảo tính sẵn sàng cao (HA).

(4) **Executor phân tán HA**: Hỗ trợ thực thi phân tán với triển khai cụm để đảm bảo tính sẵn sàng cao.

(5) **Trung tâm đăng ký**: Tự động phát hiện và kích hoạt các nhiệm vụ đăng ký hoặc nhập thủ công.

(6) **Mở rộng linh hoạt**: Tự động phân công lại nhiệm vụ khi máy thực thi thay đổi trạng thái.

(7) **Chiến lược kích hoạt phong phú**: Hỗ trợ cron, khoảng thời gian, độ trễ, API, thủ công, cha-con.

(8) **Chiến lược bồi thường**: Xử lý tác vụ lỡ lịch, như bỏ qua hoặc bù ngay lập tức.

(9) **Chiến lược chặn**: Quản lý xung đột lịch, với các tùy chọn như nối tiếp, bỏ qua hoặc ghi đè.

(10) **Kiểm soát thời gian chờ**: Cho phép thiết lập thời gian chờ tùy chỉnh cho tác vụ.

(11) **Thử lại lỗi**: Tự động thử lại khi nhiệm vụ thất bại theo số lần cấu hình.

(12) **Cảnh báo lỗi**: Hỗ trợ cảnh báo qua email và tích hợp mở rộng SMS, DingTalk.

(13) **Chiến lược định tuyến đa dạng**: Định tuyến theo nhiều cách như ngẫu nhiên, HASH nhất quán, chuyển đổi dự phòng...

(14) **Phát sóng phân đoạn**: Phân công và xử lý cộng tác trên các cụm thực thi.

(15) **Phân đoạn động**: Phân đoạn linh hoạt theo kích thước cụm để tăng hiệu suất xử lý.

(16) **Chuyển đổi dự phòng**: Tự động chuyển nhiệm vụ khi máy thực thi lỗi.

(17) **Giám sát tiến độ**: Theo dõi tiến độ tác vụ thời gian thực.

(18) **Nhật ký cuộn**: Xem trực tuyến nhật ký thực hiện đầy đủ theo thời gian thực.

(19) **GLUE IDE**: Hỗ trợ phát triển mã trực tuyến, quản lý phiên bản, phát hành động.

(20) **Tác vụ tập lệnh**: Hỗ trợ phát triển bằng Shell, Python, NodeJS, PHP...

(21) **Tác vụ dòng lệnh**: Cung cấp xử lý chung cho dòng lệnh (CommandJobHandler).

(22) **Phụ thuộc tác vụ**: Hỗ trợ cấu hình nhiệm vụ mẹ-con.

(23) **Tính nhất quán**: Đảm bảo chỉ kích hoạt một lần thực thi cho mỗi lịch trình.

(24) **Tham số tùy chỉnh**: Hỗ trợ cấu hình tham số trực tuyến.

(25) **Nhóm luồng lập lịch**: Đảm bảo lập lịch chính xác, không bị chặn.

(26) **Mã hóa**: Giao tiếp giữa trung tâm và thực thi được mã hóa để bảo mật.

(27) **Cảnh báo qua email**: Hỗ trợ gửi nhiều cảnh báo qua email.

(28) **Kho Maven**: Phiên bản ổn định được cập nhật trên kho Maven.

(29) **Báo cáo hoạt động**: Theo dõi dữ liệu hoạt động thời gian thực, tạo báo cáo.

(30) **Hoàn toàn không đồng bộ**: Thiết kế không đồng bộ giảm tải cao điểm và hỗ trợ tác vụ dài.

(31) **Ngôn ngữ chéo**: Hỗ trợ RESTful API và tích hợp đa ngôn ngữ.

(32) **Quốc tế hóa**: Hỗ trợ giao diện tiếng Trung và tiếng Anh.

(33) **Container hóa**: Hình ảnh Docker chính thức, cập nhật thời gian thực.

(34) **Cách ly luồng**: Phân nhóm luồng, giảm tác động từ tác vụ chậm.

(35) **Quản lý người dùng**: Phân vai trò quản trị viên và người dùng thông thường.

(36) **Kiểm soát quyền**: Kiểm soát quyền thực thi theo người dùng.

