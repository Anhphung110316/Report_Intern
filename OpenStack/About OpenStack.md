# Về OpenStack

1. Sơ lược về OpenStack 
* OpenStack là hệ điều hành đám mây kiểm soát nhiều tài nguyên tính toán, lưu trữ và mạng trong một trung tâm dữ liệu, tất cả đều được quản lý và cung cấp thông qua API với cơ chế xác thực chung.
  
<p align="center">
 <img src="Picture/openstack.svg" width="500" height="300" />
</p>

* Có 3 nhóm chính tham gia: Nhóm điều hành, nhóm phát triển và nhóm người dùng.
* OpenStack hoạt động theo hướng mở: Công khai lộ trình phát triển, công khai mã nguồn …

2. Kiến trúc của OpenStack
* Kiến trúc tổng quan của OpenStack được chia thành 3 tầng:
  - Tầng ứng dụng (Your Application): Các ứng dụng/phần mềm sử dụng OpenStack
  - Tầng Hypervisor (Standard Hardware): Phần ứng máy chủ đã được ảo hóa để chia sẻ cho người dùng.
  - Dịch vụ OpenStack (Openstack Shared Services): Các thành phần cơ bản như Dashboard, Compute, Networking, API, Storage.

3. Bối cảnh OpenStack
* OpenStack được chia thành các dịch vụ để cho phép cắm và chạy các thành phần tùy theo nhu cầu. Bản đồ openstack cung cấp cái nhìn "tổng quan" về bối cảnh openstack để xem các dịch vụ đó phù hợp ở đâu và chúng có thể hoạt động cùng nhau như thế nào.

<p align="center">
 <img src="Picture/boicanh_page-0001.jpg" />
</p>
 
4. Các thành phần của OpenStack
* OpenStack không phải là một dự án đơn lẻ mà là một nhóm các dự án nguồn mở nhằm mục đích cung cấp các dịch vụ cloud hoàn chỉnh. OpenStack chứa nhiều thành phần:
  - OpenStack computer: là module quản lý và cung cấp máy ảo. Tên phát triển của nó Nova. Nó hỗ trợ nhiều hypervisors gồm KVM, QEMU, LXC, XenServer… Compute là một công cụ mạnh mẽ mà có thể điều khiển toàn bộ các công việc: networking, CPU, storage, memory, tạo, điều khiển và xóa bỏ máy ảo, security, access control. Bạn có thể điều khiển tất cả bằng lệnh hoặc từ giao diện dashboard trên web.
  - OpenStack Glance:là OpenStack Image Service, quản lý các disk image ảo. Glance hỗ trợ các ảnh Raw, Hyper-V (VHD), VirtualBox (VDI), Qemu (qcow2) và VMWare (VMDK, OVF). Bạn có thể thực hiện: cập nhật thêm các virtual disk images, cấu hình các public và private image và điều khiển việc truy cập vào chúng, và tất nhiên là có thể tạo và xóa chúng.
 
<p align="center">
 <img src="Picture/cacthanhphan.webp" width="500" height="300" />
</p>
   
  - OpenStack Object Storage: dùng để quản lý lưu trữ. Nó là một hệ thống lưu trữ phân tán cho quản lý tất cả các dạng của lưu trữ như: archives, user data, virtual machine image … Có nhiều lớp redundancy và sự nhân bản được thực hiện tự động, do đó khi có node bị lỗi thì cũng không làm mất dữ liệu, và việc phục hồi được thực hiện tự động.
  - Dentity Server: quản lý xác thực cho user và projects.
  - OpenStack Netwok: là thành phần quản lý network cho các máy ảo. Cung cấp chức năng network as a service. Đây là hệ thống có các tính chất pluggable, scalable và API-driven.
  - OpenStack dashboard: cung cấp cho người quản trị cũng như người dùng giao diện đồ họa để truy cập, cung cấp và tự động tài nguyên cloud. Việc thiết kế có thể mở rộng giúp dễ dàng thêm vào các sản phẩm cũng như dịch vụ ngoài như billing, monitoring và các công cụ giám sát khác.

5. Mô hình giải pháp
* Mô hình giải pháp: Điện toán đám mây OpenStack được các nhà cung cấp dịch vụ phát triển qua 3 giải pháp:
  - IaaS (Infrastructure as a service): cung cấp/cho thuê cơ sở hạ tầng như thuê máy chủ…
  - PaaS (Platform as a service): cung cấp nền tảng để phát triển ứng dụng
  - SaaS (Software as a service): cung cấp khả năng truy cập phần mềm linh hoạt như HCM,CRM…
* Mô hình triển khai:
  - Private Cloud: sử dụng trong một doanh nghiệp và không chia sẻ với bất kỳ ai nằm ngoài doanh nghiệp đóng
  - Public Cloud: các dịch vụ trên nền tảng điện toán đám mây được dành cho cá nhân, tổ chức cùng thuê và sử dụng chung tài nguyên
  - Hybrid Cloud: mô hình lai giữa public cloud và private cloud
  - Community Cloud: các dịch vụ được các công ty cùng hợp tác xây dựng và cung cấp cho cộng đồng sử dụng
