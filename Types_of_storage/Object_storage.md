# Về Oject Storage

## Object Storage là gì?

*Object storage là một phương thức lưu trữ dữ liệu phân tán, trong đó dữ liệu được lưu trữ và quản lý dưới dạng các đối tượng (object) độc lập. Mỗi đối tượng chứa dữ liệu, metadata và một định danh (identifier) duy nhất để phân biệt với các đối tượng khác trong hệ thống.*

Object storage cung cấp một phương thức lưu trữ phân tán và độc lập với phần cứng, giúp tăng tính sẵn sàng và độ tin cậy của hệ thống lưu trữ. Đồng thời, nó cũng cho phép truy xuất dữ liệu từ bất kỳ đâu thông qua các giao thức như HTTP hoặc HTTPS.

Một điểm khác biệt quan trọng của object storage so với block storage và file storage là khả năng tự động mở rộng, nghĩa là khi dung lượng lưu trữ tăng lên, hệ thống tự động tạo thêm các bản sao dữ liệu và phân phối chúng đến các máy chủ khác nhau trong hệ thống. Việc này giúp đảm bảo tính sẵn sàng và khả năng phục hồi sau sự cố.

Object storage thường được sử dụng cho các ứng dụng lưu trữ dữ liệu lớn như hình ảnh, video, âm thanh, tài liệu và các ứng dụng trên đám mây.
 
 <img src="Picture/dsad.png" />

## Cách Object storage hoạt động

Object storage hoạt động bằng cách lưu trữ dữ liệu dưới dạng các đối tượng độc lập, mỗi đối tượng chứa dữ liệu, metadata và một định danh duy nhất để phân biệt với các đối tượng khác trong hệ thống.

Khi người dùng yêu cầu truy xuất đến một đối tượng, hệ thống object storage sẽ sử dụng định danh để tìm kiếm và truy xuất đến đối tượng tương ứng. Tại thời điểm này, hệ thống sẽ trả về dữ liệu cho người dùng theo yêu cầu.

Khi người dùng thêm mới hoặc sửa đổi một đối tượng, hệ thống sẽ tạo ra một bản sao mới của đối tượng và phân phối nó đến các máy chủ khác nhau trong hệ thống để đảm bảo tính sẵn sàng và độ tin cậy của hệ thống lưu trữ. Việc này giúp đảm bảo tính toàn vẹn và khả năng phục hồi dữ liệu sau sự cố.

Hệ thống object storage cung cấp một giao diện API để cho phép người dùng tương tác với các đối tượng, tạo mới, sửa đổi, xoá và truy xuất dữ liệu. Object storage cũng hỗ trợ nhiều giao thức truy cập như HTTP, HTTPS, S3, Swift, NFS và SMB để đảm bảo tính linh hoạt và tương thích với các ứng dụng khác nhau.

Một số hệ thống object storage cũng cung cấp các tính năng bảo mật và quản lý dữ liệu để đảm bảo tính sẵn sàng và độ tin cậy của hệ thống lưu trữ.

## Ưu và nhược điểm của Object storage

- Ưu điểm của Object storage:

   - Khả năng lưu trữ và quản lý dữ liệu lớn: Object storage cho phép lưu trữ và quản lý dữ liệu lớn một cách hiệu quả. Không giống như block storage hoặc file storage, object storage có thể lưu trữ hàng tỷ hoặc thậm chí hàng trăm tỷ đối tượng một cách dễ dàng.
   - Tính toàn vẹn và khả năng phục hồi dữ liệu: Object storage có khả năng tự động tạo ra các bản sao của dữ liệu và phân phối chúng đến các máy chủ khác nhau trong hệ thống. Việc này giúp đảm bảo tính toàn vẹn và khả năng phục hồi dữ liệu sau sự cố.
   - Tính sẵn sàng và độ tin cậy: Hệ thống object storage được phân tán trên nhiều máy chủ khác nhau, giúp đảm bảo tính sẵn sàng và độ tin cậy của hệ thống lưu trữ.
   - Khả năng mở rộng linh hoạt: Object storage có khả năng mở rộng linh hoạt, khi nhu cầu lưu trữ tăng lên, hệ thống tự động tạo thêm các bản sao dữ liệu và phân phối chúng đến các máy chủ khác nhau trong hệ thống.
   - Tính tương thích và tính linh hoạt: Object storage hỗ trợ nhiều giao thức truy cập như HTTP, HTTPS, S3, Swift, NFS và SMB để đảm bảo tính tương thích và tính linh hoạt với các ứng dụng khác nhau.
   
- Nhược điểm của Object storage:

   - Tốc độ truy cập chậm hơn so với block storage hoặc file storage: Object storage thường có tốc độ truy cập chậm hơn so với block storage hoặc file storage, do quá trình truy xuất đến dữ liệu phải thông qua nhiều lớp phần mềm và phải tìm kiếm dữ liệu dựa trên định danh.
   - Chi phí cao hơn so với các phương pháp lưu trữ khác: Object storage có chi phí cao hơn so với các phương pháp lưu trữ khác, do yêu cầu các hệ thống phân tán phức tạp hơn và các bản sao dữ liệu được tạo ra để đảm bảo tính sẵn sàng và độ tin cậy của hệ thống lưu trữ.
   - Không thích hợp cho các ứng dụng yêu cầu tốc độ truy cập cao và tối ưu hóa cho hiệu suất: Object storage không phù hợp cho các ứng dụng yêu cầu tốc độ truy cập dữ liệu cao và tối ưu hóa cho hiệu suất, ví dụ như các ứng dụng cần xử lý và truy vấn dữ liệu liên tục.
   - Khó khăn trong việc xử lý dữ liệu có kích thước lớn: Object storage không thích hợp cho việc xử lý dữ liệu có kích thước lớn. Khi các tệp dữ liệu rất lớn được lưu trữ trong object storage, việc truy xuất hoặc xử lý dữ liệu có thể trở nên chậm chạp hoặc gây ra sự cố.
   - Khó khăn trong việc tích hợp và quản lý: Vì object storage thường được triển khai trong các môi trường phân tán phức tạp, việc tích hợp và quản lý hệ thống lưu trữ có thể trở nên khó khăn và phức tạp hơn so với các phương pháp lưu trữ khác.
   - Bảo mật dữ liệu có thể bị đe dọa: Việc lưu trữ dữ liệu trong object storage có thể tạo ra các vấn đề bảo mật dữ liệu, đặc biệt là khi các đối tượng được lưu trữ có giá trị cao và chứa thông tin nhạy cảm của khách hàng hoặc doanh nghiệp.

## Nhu cầu lưu trữ phù hợp của Object Storage là gì? 

   * Lưu trữ, truyền tải website tĩnh hoặc các ứng dụng như file hình ảnh, CSS, JavaScript, CSS, tăng tính bảo mật khi được hỗ trợ SSL.
   * Lưu trữ media (video, hình ảnh, audio).
   * Truyền tải những ứng dụng: lưu trữ các thư viện, containers, ứng dụng hay các phần mềm để khách hàng có thể download.
   * Hỗ trợ Data Lake/Big Data với khả năng xử lý nhanh chóng, tốc độ cao.
   * Sao lưu lại các dữ liệu quan trọng

## Đối tượng khách hàng của Object Storage là gì? 

- Object Storage là một giải pháp linh hoạt phù hợp với nhiều đối tượng khách hàng khác nhau: 

– Doanh nghiệp lớn: Lưu trữ dữ liệu cho các ứng dụng, hệ thống CNTT của doanh nghiệp không giới hạn.

– Startup/ doanh nghiệp nhỏ: Giảm chi phí đầu tư hạ tầng, dễ dàng mở rộng dung lượng khi cần thiết.

– Nhà cung cấp dịch vụ: Lưu trữ dữ liệu và nội dung phục vụ cho dịch vụ CDN, video streaming, AI training,…

– Cá nhân: Lưu trữ ảnh/ video cá nhân, chia sẻ dữ liệu cho cộng đồng dưới dạng các repository.

Nói chung, bất kỳ đối tượng khách hàng nào có nhu cầu lưu trữ dữ liệu với dung lượng lớn, tốc độ truy xuất nhanh và chi phí thấp đều có thể sử dụng giải pháp Object Storage.

