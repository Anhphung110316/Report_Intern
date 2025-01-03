# 1. Tổng quan 
* Khái niệm cơ bản
  - AWX/Ansible Tower (Dành cho IT Automation)

  - **Ansible**: là một công cụ giúp tự động hóa việc cấu hình máy chủ, triển khai ứng dụng, và các tác vụ IT khác.

    Ví dụ: Thay vì bạn phải tự tay vào từng server để cài đặt phần mềm, Ansible cho phép bạn viết một "hướng dẫn" (playbook) và chạy trên nhiều server cùng lúc.

  - **AWX**: là phiên bản mã nguồn mở của Ansible Tower.

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
