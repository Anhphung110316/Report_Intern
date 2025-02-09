# 1. Tổng quan 
* Khái niệm cơ bản
  - AWX/Ansible Tower (Dành cho IT Automation)

  - **Ansible**: là một công cụ giúp tự động hóa việc cấu hình máy chủ, triển khai ứng dụng, và các tác vụ IT khác.

    Ví dụ: Thay vì bạn phải tự tay vào từng server để cài đặt phần mềm, Ansible cho phép bạn viết một "hướng dẫn" (playbook) và chạy trên nhiều server cùng lúc.

  - **AWX**: là phiên bản mã nguồn mở của Ansible Tower.
 
    - AWX là một phần mềm cung cấp giao diện web cho người dùng, REST API và các công cụ thực thi dựa trên Ansible. Đây là một upstream project cho phần mềm Ansible Tower của RedHat

* **Lợi ích khi sử dụng AWX**:

  - Giao diện dễ sử dụng  
  - Quản lý phân quyền
  - Lưu lại log khi thực thi
  - Lập lịch thực thi
  - Quản lý Inventory

* **Các thành phần trong AWX**:

  - AWX Engine: vai trò Ansible engine thực thi các thành phần trong Ansible
  - Nginx: vai trò webserver cung cấp giao diện web cho người dùng
  - PostgreSQL: vai trò DB Server lưu trữ dữ liệu khởi tạo, dữ liệu log sinh ra trong quá trình Ansible thực thi
  - Redis: vai trò cache server
  - Cung cấp giao diện web để quản lý, lập lịch, và theo dõi các tác vụ Ansible.

# 2. Cách thức hoạt động

  * **AWX/Ansible Tower**:
    - Cách chạy:

      - Tạo các playbook bằng Ansible để mô tả các bước cần thực hiện.

      - AWX cung cấp giao diện quản lý, nơi lên lịch khi nào các playbook chạy, nơi gán playbook cho nhóm server cụ thể.

    - Ví dụ cơ bản:

      - Muốn cài đặt Apache trên 10 server:

        - Viết một playbook chỉ ra cách cài đặt.
        
        - Dùng AWX để chọn các server mục tiêu và chạy playbook.

     - Cơ chế hoạt động:

        - Không cần cài "agent" trên server.

        - AWX sử dụng SSH để kết nối và thực thi các lệnh từ xa.

# 3. Ứng dụng thực tế 

 * **Quản lý máy chủ tự động**:

  - Cài đặt phần mềm (Apache, MySQL).

  - Thay đổi cấu hình hệ thống.

  - Triển khai bản cập nhật ứng dụng.

  - Phù hợp dành cho các đội ngũ DevOps hoặc quản trị hệ thống (SysAdmin).
