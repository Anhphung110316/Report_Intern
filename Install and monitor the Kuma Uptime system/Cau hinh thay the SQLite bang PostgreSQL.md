# Ý tưởng thay thế SQLite trong Uptime Kuma sang PostgreSQL

## 1. Quản lý kết nối và đồng thời:
* PostgreSQL hỗ trợ nhiều kết nối đồng thời: Điều này rất quan trọng khi có nhiều người dùng hoặc dịch vụ cần truy cập dữ liệu cùng lúc. SQLite hạn chế số lượng kết nối đồng thời, điều này có thể gây ra các vấn đề về hiệu suất khi có nhiều yêu cầu.
  
## 2. Tính năng mở rộng:
* PostgreSQL có nhiều tính năng mạnh mẽ như: trigger, stored procedures, và custom data types. Điều này cho phép mở rộng và tùy chỉnh cơ sở dữ liệu theo nhu cầu cụ thể của tổ chức.

## 3. Hiệu suất và quy mô:
* PostgreSQL được thiết kế để hoạt động hiệu quả với dữ liệu lớn và có khả năng mở rộng tốt hơn so với SQLite. Nếu Uptime Kuma cần lưu trữ một lượng lớn thông tin về trạng thái và hiệu suất, PostgreSQL sẽ xử lý tốt hơn.

## 4. Bảo mật:
* PostgreSQL cung cấp các tùy chọn bảo mật nâng cao, như mã hóa dữ liệu, xác thực đa yếu tố, và kiểm soát truy cập chi tiết. Điều này giúp bảo vệ dữ liệu nhạy cảm khỏi các mối đe dọa.

## 5. Khả năng phục hồi và sao lưu:
* PostgreSQL cung cấp các công cụ sao lưu và phục hồi mạnh mẽ. Có thể sử dụng pg_dump để tạo bản sao lưu toàn bộ cơ sở dữ liệu và phục hồi nó nhanh chóng trong trường hợp gặp sự cố.
  
## 6. Hỗ trợ JSON:
* PostgreSQL hỗ trợ kiểu dữ liệu JSON và JSONB, cho phép lưu trữ và truy vấn dữ liệu phi cấu trúc một cách dễ dàng. Điều này có thể hữu ích nếu cần lưu trữ cấu trúc dữ liệu linh hoạt.

## 7. Cộng đồng và hỗ trợ:
* PostgreSQL có một cộng đồng lớn và tích cực, giúp dễ dàng tìm kiếm hỗ trợ và tài liệu khi cần.

## 8. Tính khả dụng và phục hồi:
* PostgreSQL có khả năng cấu hình cho độ tin cậy cao và khôi phục nhanh chóng, rất quan trọng cho các ứng dụng yêu cầu hoạt động 24/7.

==> Kết luận
* Việc thay thế SQLite bằng PostgreSQL trong Uptime Kuma không chỉ giúp cải thiện hiệu suất và tính ổn định của ứng dụng mà còn cho phép tổ chức tận dụng những lợi ích mạnh mẽ mà PostgreSQL mang lại. Nếu công ty đã sử dụng PostgreSQL, việc tích hợp Uptime Kuma với PostgreSQL sẽ giúp tận dụng tốt hơn các tài nguyên và quy trình hiện có.

## 9. Chuyển đổi xuất ra file .sql:
* Lợi ích:
    - Sao lưu Dữ liệu: Tạo bản sao lưu dễ dàng để bảo vệ dữ liệu.
    - Khôi phục Dữ liệu: Dễ dàng khôi phục lại cơ sở dữ liệu khi cần.
    - Di chuyển Dữ liệu: Chuyển đổi dữ liệu giữa các hệ thống hoặc môi trường khác nhau.
    - Phân tích Dữ liệu: Dễ dàng kiểm tra và phân tích nội dung cơ sở dữ liệu.
    - Chia sẻ Dữ liệu: Dễ dàng chia sẻ thông tin giữa các thành viên trong nhóm.

# Về cấu hình

## Bước 1: Cài đặt PostgreSQL Client
* Chạy lệnh sau để cài đặt gói postgresql-client:
```
sudo apt update
sudo apt install postgresql-client
```

## Bước 2: Kiểm tra Cài đặt
* Sau khi cài đặt hoàn tất, bạn có thể kiểm tra phiên bản của psql để xác nhận rằng nó đã được cài đặt thành công:
```
psql --version
```

## Bước 3: Kết nối đến PostgreSQL
* Bây giờ, bạn có thể thử kết nối đến cơ sở dữ liệu PostgreSQL với lệnh mà bạn đã sử dụng trước đó:
```
psql -h uptime_kuma_db -U uptime_user -d uptime_kuma
```
* Nhớ rằng bạn sẽ cần nhập mật khẩu cho người dùng uptime_user nếu được yêu cầu.

## Bước 4: Cài Uptime Kuma với PostgreSQL
* Chạy lệnh sau để thêm cấu hình PostgreSQL vào Uptime Kuma:
```
sudo docker run --name uptime_kuma_db -e POSTGRES_USER=uptime_user -e POSTGRES_PASSWORD=1234 -e POSTGRES_DB=uptime_kuma -p 5432:5432 -d postgres:latest
```

## Bước 5:
* Khởi động lại container:
```
sudo docker restart uptime_kuma_db
```

## Bước 6: Kết Nối Uptime Kuma với PostgreSQL
* Sau khi container PostgreSQL đã khởi động thành công, hãy thử kết nối với lệnh:
```
psql -h localhost -U uptime_user -d uptime_kuma
```

* Hãy nhớ thay thế localhost bằng địa chỉ IP của container nếu bạn đang chạy từ một máy khác.

* Sau khi kết nối xong nếu thành công sẽ hiện lên như hình dưới đây:



# Export file chuyển đổi dạng .sql:

## Bước 1: Đảm Bảo PostgreSQL Đang Chạy
* Trước tiên, hãy chắc chắn rằng container PostgreSQL đang chạy:
```
sudo docker ps
```

* Bạn nên thấy container uptime_kuma_db trong danh sách và trạng thái của nó là "Up".



## Bước 2: Sử Dụng `pg_dump` từ Bên Trong Container
* Thay vì chạy lệnh `pg_dump` từ máy chủ Ubuntu, hãy thực hiện nó từ bên trong container PostgreSQL:
    - Truy Cập vào Container PostgreSQL:
``` 
sudo docker exec -it uptime_kuma_db bash
```

* Chạy lệnh `pg_dump` bên trong container:
    - Bây giờ, bạn có thể chạy lệnh sau để xuất cơ sở dữ liệu:
```
pg_dump -U uptime_user -d uptime_kuma -F c -f /tmp/uptime_kuma_backup.sql
```

## Bước 3: Sao Chép File Xuất Ra
* Sau khi xuất xong, bạn có thể sao chép file SQL từ container về máy chủ như sau:
    - Mở một terminal mới trên máy chủ Ubuntu (không phải trong container).
    - Chạy lệnh sau để sao chép file SQL:
```
sudo docker cp uptime_kuma_db:/tmp/uptime_kuma_backup.sql ./uptime_kuma_backup.sql
```

## Bước 4: Kiểm Tra File
* Cuối cùng, kiểm tra xem file đã được sao chép thành công hay chưa bằng lệnh:
```
ls -l uptime_kuma_backup.sql
```

* Nếu bạn thấy file uptime_kuma_backup.sql, tức là bạn đã xuất cơ sở dữ liệu thành công!
