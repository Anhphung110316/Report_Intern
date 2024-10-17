# Cấu hình dịch vụ Placement.
-------------------
## Cấu hình khởi tạo CSDL cho Placement.

```sql
sudo mysql -u root -van -e "CREATE DATABASE placement;"
sudo mysql -u root -van -e "GRANT ALL PRIVILEGES ON placement.* TO 'placement'@'localhost' IDENTIFIED BY 'PLACEMENT_DBPASS';"
sudo mysql -u root -van -e "GRANT ALL PRIVILEGES ON placement.* TO 'placement'@'%' IDENTIFIED BY 'PLACEMENT_DBPASS';"
sudo mysql -u root -van -e "FLUSH PRIVILEGES;"
```

* Tạo user, một service và các endpoint cho service Placement.

* Đầu tiên, sử dụng lệnh “. admin-openrc” để kích hoạt môi trường của OpenStack admin.

>. admin-openrc

* Các lệnh sau sẽ tạo một user, một service, và các endpoint cho service Placement trong OpenStack.
`openstack user create --domain default placement --password "PLACEMENT_PASS"`: Tạo một user mới trong domain mặc định (default) của OpenStack với tên là placement và password là `PLACEMENT_PASS`.

```
$ openstack user create --domain default placement --password "PLACEMENT_PASS"

+---------------------+----------------------------------+
| Field               | Value                            |
+---------------------+----------------------------------+
| domain_id           | default                          |
| enabled             | True                             |
| id                  | fa742015a6494a949f67629884fc7ec8 |
| name                | placement                        |
| options             | {}                               |
| password_expires_at | None                             |
+---------------------+----------------------------------+
```

`openstack role add --project service --user placement admin`: Gán role admin cho user placement trong project service.

```
openstack role add --project service --user placement admin
```

`openstack service create --name placement --description "Placement API" placement`: Tạo một service mới với tên là placement và mô tả là “`Placement API`”.

```
$ openstack service create --name placement \
  --description "Placement API" placement

+-------------+----------------------------------+
| Field       | Value                            |
+-------------+----------------------------------+
| description | Placement API                    |
| enabled     | True                             |
| id          | 2d1a27022e6e4185b86adac4444c495f |
| name        | placement                        |
| type        | placement                        |
+-------------+----------------------------------+
```

* Xác nhận dịch vụ đã tạo thành công bằng lệnh openstack service list.

```
shell> openstack service list | grep placement
| 2d1a27022e6e4185b86adac4444c495f | placement | placement |
```

## Tạo các endpoint cho service Placement.
`openstack endpoint create --region RegionOne placement public http://controller:8778`: Tạo một endpoint cho service Placement trên region RegionOne với URL truy cập public là `http://controller:8778`.
`openstack endpoint create --region RegionOne placement internal http://controller:8778`: Tạo một endpoint cho service Placement trên region RegionOne với URL truy cập internal là `http://controller:8778`.
`openstack endpoint create --region RegionOne placement admin http://controller:8778`: Tạo một endpoint cho service Placement trên region RegionOne với URL truy cập admin là `http://controller:8778`.

```
$ openstack endpoint create --region RegionOne \
  placement public http://controller:8778

+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 2b1b2637908b4137a9c2e0470487cbc0 |
| interface    | public                           |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 2d1a27022e6e4185b86adac4444c495f |
| service_name | placement                        |
| service_type | placement                        |
| url          | http://controller:8778           |
+--------------+----------------------------------+
```

```
$ openstack endpoint create --region RegionOne \
  placement internal http://controller:8778

+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 02bcda9a150a4bd7993ff4879df971ab |
| interface    | internal                         |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 2d1a27022e6e4185b86adac4444c495f |
| service_name | placement                        |
| service_type | placement                        |
| url          | http://controller:8778           |
+--------------+----------------------------------+
```

```
$ openstack endpoint create --region RegionOne \
  placement admin http://controller:8778

+--------------+----------------------------------+
| Field        | Value                            |
+--------------+----------------------------------+
| enabled      | True                             |
| id           | 3d71177b9e0f406f98cbff198d74b182 |
| interface    | admin                            |
| region       | RegionOne                        |
| region_id    | RegionOne                        |
| service_id   | 2d1a27022e6e4185b86adac4444c495f |
| service_name | placement                        |
| service_type | placement                        |
| url          | http://controller:8778           |
+--------------+----------------------------------+
```

* Với các endpoint này, các component trong OpenStack sẽ có thể tương tác với service Placement thông qua các giao thức và URL đã được cấu hình.

* Nếu bạn tạo nhiều dịch vụ trùng tên là placement thì bạn hãy chọn ID của dịch vụ ‘`placement`’ mà bạn muốn tạo endpoint và sử dụng nó thay cho ‘`placement`’ trong lệnh tạo endpoint.

```
openstack endpoint create --region RegionOne \
  <placement_service_id> public http://controller:8778
```

* Trong đó, `<placement_service_id>` là ID của dịch vụ ‘`placement`’ mà bạn đã chọn từ lệnh openstack service list.

* Nếu bạn không chọn tên ID cụ thể bạn sẽ gặp thông báo sau khi tạo endpoint.

```
shell> openstack endpoint create --region RegionOne \
  placement public http://controller:8778
Multiple service matches found for 'placement', use an ID to be more specific.
```

## Cài đặt placement-api.

```
apt install placement-api -y
```

## Cấu hình Placement Database.
* Chỉnh sửa trong file `/etc/placement/placement.conf`  trong OpenStack, nơi ta thiết lập các thông số kết nối đến cơ sở dữ liệu MySQL để sử dụng cho dịch vụ Placement.

* Cụ thể, phần `[placement_database]` chứa thông tin về cách kết nối đến cơ sở dữ liệu Placement. Điều này bao gồm:

    - `connection`: chuỗi kết nối đến cơ sở dữ liệu MySQL để sử dụng cho Placement. Nó được định dạng như sau: `mysql+pymysql://USER:PASS@HOST/DB_NAME`, trong đó `USER` và `PASS` là tên người dùng và mật khẩu của tài khoản truy cập cơ sở dữ liệu, `HOST` là địa chỉ IP hoặc tên miền của MySQL server và `DB_NAME` là tên của cơ sở dữ liệu Placement.

* Thông thường, ta sẽ tạo một người dùng và CSDL riêng cho dịch vụ Placement, để đảm bảo an toàn và bảo mật. Các thông số kết nối này cần được điều chỉnh phù hợp với cài đặt của hệ thống để dịch vụ Placement hoạt động đúng.

```
[placement_database]
connection = mysql+pymysql://placement:PLACEMENT_DBPASS@controller/placement
```

## Định nghĩa cách thức xác thực (auth_strategy) và thông tin xác thực của service Placement.
* Đây là một phần cấu hình của service placement trong OpenStack. Cụ thể, đoạn cấu hình này định nghĩa cách thức xác thực (`auth_strategy`) và thông tin xác thực của service placement với Keystone, gồm `auth_url`, `memcached_servers`, `auth_type`, `project_domain_name`, `user_domain_name`, `project_name`, `username` và `password`.

    - `auth_strategy`: Chỉ định cách thức xác thực, trong trường hợp này sử dụng Keystone.
    - `auth_url`: Địa chỉ URL của Keystone service endpoint.
    - `memcached_servers`: Danh sách các máy chủ memcached sử dụng để lưu trữ token xác thực.
    - `auth_type`: Xác định cách thức xác thực, ở đây là password.
    - `project_domain_name`: Tên domain của project, mặc định là Default.
    - `user_domain_name`: Tên domain của user, mặc định là Default.
    - `project_name`: Tên của project được sử dụng để xác thực, ở đây là service.
    - `username`: Tên người dùng được sử dụng để xác thực với Keystone, ở đây là placement.
    - `password`: Mật khẩu của người dùng được sử dụng để xác thực với Keystone.

```
[api]
auth_strategy = keystone

[keystone_authtoken]
auth_url = http://controller:5000/v3
memcached_servers = controller:11211
auth_type = password
project_domain_name = Default
user_domain_name = Default
project_name = service
username = placement
password = PLACEMENT_PASS
```

* Đồng bộ hóa cơ sở dữ liệu cho dịch vụ Placement.

* Lệnh `su -s /bin/sh -c "placement-manage db sync"` placement được sử dụng để đồng bộ hóa cơ sở dữ liệu cho dịch vụ Placement. Khi OpenStack Placement đã được cài đặt, bạn cần phải tạo cơ sở dữ liệu cho dịch vụ này bằng lệnh `placement-manage db sync`. Lệnh này sẽ tạo ra các bảng và chỉ mục cần thiết trong cơ sở dữ liệu để lưu trữ các thông tin cấu hình, yêu cầu tài nguyên và khả năng của máy chủ vật lý. Bằng cách đồng bộ hóa cơ sở dữ liệu này, bạn sẽ đảm bảo rằng dịch vụ Placement hoạt động đúng cách và có thể cung cấp các thông tin cần thiết cho các thành phần khác của OpenStack để quản lý tài nguyên.

```
su -s /bin/sh -c "placement-manage db sync" placement
```

* Khởi động lại Webserver.

* Sau khi cấu hình các file cấu hình của placement trên Apache, bạn cần khởi động lại dịch vụ để nó sử dụng các file cấu hình mới.

```
service apache2 restart
```

* Đảm bảo rằng các phiên bản của database của Placement service được cập nhật và đồng bộ với các phiên bản của dịch vụ khác trong OpenStack.

* Cuối cùng hãy xác nhận các config, đầu tiên, sử dụng lệnh “`. admin-openrc`” để kích hoạt môi trường của OpenStack admin.

>. admin-openrc

Lệnh `placement-status` upgrade check được sử dụng để kiểm tra xem các phiên bản database của Placement service đã được nâng cấp lên phiên bản mới nhất hay chưa.

Khi chạy lệnh này, hệ thống sẽ kiểm tra phiên bản database hiện tại của Placement và so sánh với phiên bản mới nhất được hỗ trợ. Nếu phiên bản database đang sử dụng chưa được nâng cấp, lệnh sẽ cung cấp thông báo cảnh báo và hướng dẫn người dùng thực hiện quá trình nâng cấp.

Lệnh này được sử dụng để đảm bảo rằng các phiên bản của database của Placement service được cập nhật và đồng bộ với các phiên bản của dịch vụ khác trong OpenStack.

```
$ placement-status upgrade check
+----------------------------------+
| Upgrade Check Results            |
+----------------------------------+
| Check: Missing Root Provider IDs |
| Result: Success                  |
| Details: None                    |
+----------------------------------+
| Check: Incomplete Consumers      |
| Result: Success                  |
| Details: None                    |
+----------------------------------+
```

`osc-placement` là một gói Python được sử dụng để tương tác với API Placement của OpenStack. Để cài đặt gói này, ta sử dụng lệnh `pip3 install osc-placement` trên terminal/command line. Lệnh này sẽ tải và cài đặt gói `osc-placement` và các gói liên quan cần thiết cho nó. Sau khi cài đặt thành công, ta có thể sử dụng `osc-placement` để tương tác với API Placement của OpenStack, chẳng hạn như để tạo, xóa hoặc hiển thị thông tin của các resource provider trong hệ thống Placement.

* Nếu bạn chưa có `python3-pip` thì hãy cài theo lệnh dưới.

```
sudo apt install python3-pip -y
```

* Sau đó chạy lệnh cài `osc-placement` như sau:

```
sudo pip3 install osc-placement
```

* Câu lệnh `openstack --os-placement-api-version 1.2 resource class list --sort-column name` sẽ hiển thị danh sách các resource class (tức là các lớp tài nguyên) trên OpenStack Placement API, được sắp xếp theo tên của chúng. Thông thường, mỗi lớp tài nguyên tương ứng với một loại tài nguyên cụ thể mà compute host có thể cung cấp cho các máy ảo, ví dụ như CPU, RAM, Disk, GPU, … Nó cung cấp các thông tin về tên, mô tả và các thuộc tính của mỗi lớp tài nguyên.

```
$ openstack --os-placement-api-version 1.2 resource class list --sort-column name
+----------------------------------------+
| name                                   |
+----------------------------------------+
| DISK_GB                                |
| FPGA                                   |
| IPV4_ADDRESS                           |
| MEMORY_MB                              |
| MEM_ENCRYPTION_CONTEXT                 |
| NET_BW_EGR_KILOBIT_PER_SEC             |
| NET_BW_IGR_KILOBIT_PER_SEC             |
| NET_PACKET_RATE_EGR_KILOPACKET_PER_SEC |
| NET_PACKET_RATE_IGR_KILOPACKET_PER_SEC |
| NET_PACKET_RATE_KILOPACKET_PER_SEC     |
| NUMA_CORE                              |
| NUMA_MEMORY_MB                         |
| NUMA_SOCKET                            |
| NUMA_THREAD                            |
| PCI_DEVICE                             |
| PCPU                                   |
| PGPU                                   |
| SRIOV_NET_VF                           |
| VCPU                                   |
| VGPU                                   |
| VGPU_DISPLAY_HEAD                      |
+----------------------------------------+
```

* Câu lệnh `openstack --os-placement-api-version 1.6 trait list --sort-column name` sẽ hiển thị danh sách các trait (tức là các thuộc tính tài nguyên) trên OpenStack Placement API, được sắp xếp theo tên của chúng. Trait là các thuộc tính của các tài nguyên cụ thể, ví dụ như “`HW_CPU_CORES`”, “`HW_GPU_API_VERSION`”, “`CUSTOM_FLAVOR_PROP`”,… Sử dụng các trait này, bạn có thể xác định một loại tài nguyên có các thuộc tính nhất định, giúp các máy ảo được phân bổ tài nguyên một cách hiệu quả.

```
shell> openstack --os-placement-api-version 1.6 trait list --sort-column name
+---------------------------------------+
| name                                  |
+---------------------------------------+
| COMPUTE_ACCELERATORS                  |
| COMPUTE_ARCH_AARCH64                  |
| COMPUTE_ARCH_MIPSEL                   |
| COMPUTE_ARCH_PPC64LE                  |
| COMPUTE_ARCH_RISCV64                  |
| COMPUTE_ARCH_S390X                    |
| COMPUTE_ARCH_X86_64                   |
| COMPUTE_DEVICE_TAGGING                |
| COMPUTE_EPHEMERAL_ENCRYPTION          |
| COMPUTE_EPHEMERAL_ENCRYPTION_LUKS     |
| COMPUTE_EPHEMERAL_ENCRYPTION_LUKSV2   |
| COMPUTE_EPHEMERAL_ENCRYPTION_PLAIN    |
| COMPUTE_FIRMWARE_BIOS                 |
| COMPUTE_FIRMWARE_UEFI                 |
| COMPUTE_GRAPHICS_MODEL_BOCHS          |
| COMPUTE_GRAPHICS_MODEL_CIRRUS         |
| COMPUTE_GRAPHICS_MODEL_GOP            |
| COMPUTE_GRAPHICS_MODEL_NONE           |
| COMPUTE_GRAPHICS_MODEL_QXL            |
| COMPUTE_GRAPHICS_MODEL_VGA            |
| COMPUTE_GRAPHICS_MODEL_VIRTIO         |
| COMPUTE_GRAPHICS_MODEL_VMVGA          |
| COMPUTE_GRAPHICS_MODEL_XEN            |
| COMPUTE_IMAGE_TYPE_AKI                |
| COMPUTE_IMAGE_TYPE_AMI                |
| COMPUTE_IMAGE_TYPE_ARI                |
| COMPUTE_IMAGE_TYPE_ISO                |
| COMPUTE_IMAGE_TYPE_PLOOP              |
| COMPUTE_IMAGE_TYPE_QCOW2              |
| COMPUTE_IMAGE_TYPE_RAW                |
| COMPUTE_IMAGE_TYPE_VDI                |
| COMPUTE_IMAGE_TYPE_VHD                |
| COMPUTE_IMAGE_TYPE_VHDX               |
| COMPUTE_IMAGE_TYPE_VMDK               |
| COMPUTE_MIGRATE_AUTO_CONVERGE         |
| COMPUTE_MIGRATE_POST_COPY             |
| COMPUTE_NET_ATTACH_INTERFACE          |
| COMPUTE_NET_ATTACH_INTERFACE_WITH_TAG |
| COMPUTE_NET_VIF_MODEL_E1000           |
| COMPUTE_NET_VIF_MODEL_E1000E          |
| COMPUTE_NET_VIF_MODEL_LAN9118         |
| COMPUTE_NET_VIF_MODEL_NE2K_PCI        |
| COMPUTE_NET_VIF_MODEL_NETFRONT        |
| COMPUTE_NET_VIF_MODEL_PCNET           |
| COMPUTE_NET_VIF_MODEL_RTL8139         |
| COMPUTE_NET_VIF_MODEL_SPAPR_VLAN      |
| COMPUTE_NET_VIF_MODEL_SRIOV           |
| COMPUTE_NET_VIF_MODEL_VIRTIO          |
| COMPUTE_NET_VIF_MODEL_VMXNET          |
| COMPUTE_NET_VIF_MODEL_VMXNET3         |
| COMPUTE_NODE                          |
| COMPUTE_REMOTE_MANAGED_PORTS          |
| COMPUTE_RESCUE_BFV                    |
| COMPUTE_SAME_HOST_COLD_MIGRATE        |
| COMPUTE_SECURITY_TPM_1_2              |
| COMPUTE_SECURITY_TPM_2_0              |
| COMPUTE_SECURITY_UEFI_SECURE_BOOT     |
| COMPUTE_SOCKET_PCI_NUMA_AFFINITY      |
| COMPUTE_STATUS_DISABLED               |
| COMPUTE_STORAGE_BUS_FDC               |
| COMPUTE_STORAGE_BUS_IDE               |
| COMPUTE_STORAGE_BUS_LXC               |
| COMPUTE_STORAGE_BUS_SATA              |
| COMPUTE_STORAGE_BUS_SCSI              |
| COMPUTE_STORAGE_BUS_UML               |
| COMPUTE_STORAGE_BUS_USB               |
| COMPUTE_STORAGE_BUS_VIRTIO            |
| COMPUTE_STORAGE_BUS_XEN               |
| COMPUTE_TRUSTED_CERTS                 |
| COMPUTE_VOLUME_ATTACH                 |
| COMPUTE_VOLUME_ATTACH_WITH_TAG        |
| COMPUTE_VOLUME_EXTEND                 |
| COMPUTE_VOLUME_MULTI_ATTACH           |
| HW_ARCH_AARCH64                       |
| HW_ARCH_ALPHA                         |
| HW_ARCH_ARMV6                         |
| HW_ARCH_ARMV7                         |
| HW_ARCH_ARMV7B                        |
| HW_ARCH_CRIS                          |
| HW_ARCH_I686                          |
| HW_ARCH_IA64                          |
| HW_ARCH_LM32                          |
| HW_ARCH_M68K                          |
| HW_ARCH_MICROBLAZE                    |
| HW_ARCH_MICROBLAZEEL                  |
| HW_ARCH_MIPS                          |
| HW_ARCH_MIPS64                        |
| HW_ARCH_MIPS64EL                      |
| HW_ARCH_MIPSEL                        |
| HW_ARCH_OPENRISC                      |
| HW_ARCH_PARISC                        |
| HW_ARCH_PARISC64                      |
| HW_ARCH_PPC                           |
| HW_ARCH_PPC64                         |
| HW_ARCH_PPC64LE                       |
| HW_ARCH_PPCEMB                        |
| HW_ARCH_PPCLE                         |
| HW_ARCH_S390                          |
| HW_ARCH_S390X                         |
| HW_ARCH_SH4                           |
| HW_ARCH_SH4EB                         |
| HW_ARCH_SPARC                         |
| HW_ARCH_SPARC64                       |
| HW_ARCH_UNICORE32                     |
| HW_ARCH_X86_64                        |
| HW_ARCH_XTENSA                        |
| HW_ARCH_XTENSAEB                      |
| HW_CPU_AARCH64_AES                    |
| HW_CPU_AARCH64_ASIMD                  |
| HW_CPU_AARCH64_ASIMDDP                |
| HW_CPU_AARCH64_ASIMDHP                |
| HW_CPU_AARCH64_ASIMDRDM               |
| HW_CPU_AARCH64_ATOMICS                |
| HW_CPU_AARCH64_CPUID                  |
| HW_CPU_AARCH64_CRC32                  |
| HW_CPU_AARCH64_DCPOP                  |
| HW_CPU_AARCH64_EVTSTRM                |
| HW_CPU_AARCH64_FCMA                   |
| HW_CPU_AARCH64_FP                     |
| HW_CPU_AARCH64_FPHP                   |
| HW_CPU_AARCH64_JSCVT                  |
| HW_CPU_AARCH64_LRCPC                  |
| HW_CPU_AARCH64_PMULL                  |
| HW_CPU_AARCH64_SHA1                   |
| HW_CPU_AARCH64_SHA2                   |
| HW_CPU_AARCH64_SHA3                   |
| HW_CPU_AARCH64_SHA512                 |
| HW_CPU_AARCH64_SM3                    |
| HW_CPU_AARCH64_SM4                    |
| HW_CPU_AARCH64_SVE                    |
| HW_CPU_AMD_SEV                        |
| HW_CPU_HYPERTHREADING                 |
| HW_CPU_PPC64LE_POWER8                 |
| HW_CPU_PPC64LE_POWER9                 |
| HW_CPU_X86_3DNOW                      |
| HW_CPU_X86_ABM                        |
| HW_CPU_X86_AESNI                      |
| HW_CPU_X86_AMD_IBPB                   |
| HW_CPU_X86_AMD_NO_SSB                 |
| HW_CPU_X86_AMD_SEV                    |
| HW_CPU_X86_AMD_SSBD                   |
| HW_CPU_X86_AMD_SVM                    |
| HW_CPU_X86_AMD_VIRT_SSBD              |
| HW_CPU_X86_ASF                        |
| HW_CPU_X86_AVX                        |
| HW_CPU_X86_AVX2                       |
| HW_CPU_X86_AVX512BITALG               |
| HW_CPU_X86_AVX512BW                   |
| HW_CPU_X86_AVX512CD                   |
| HW_CPU_X86_AVX512DQ                   |
| HW_CPU_X86_AVX512ER                   |
| HW_CPU_X86_AVX512F                    |
| HW_CPU_X86_AVX512GFNI                 |
| HW_CPU_X86_AVX512IFMA                 |
| HW_CPU_X86_AVX512PF                   |
| HW_CPU_X86_AVX512VAES                 |
| HW_CPU_X86_AVX512VBMI                 |
| HW_CPU_X86_AVX512VBMI2                |
| HW_CPU_X86_AVX512VL                   |
| HW_CPU_X86_AVX512VNNI                 |
| HW_CPU_X86_AVX512VPCLMULQDQ           |
| HW_CPU_X86_AVX512VPOPCNTDQ            |
| HW_CPU_X86_BMI                        |
| HW_CPU_X86_BMI2                       |
| HW_CPU_X86_CLMUL                      |
| HW_CPU_X86_F16C                       |
| HW_CPU_X86_FMA3                       |
| HW_CPU_X86_FMA4                       |
| HW_CPU_X86_INTEL_MD_CLEAR             |
| HW_CPU_X86_INTEL_PCID                 |
| HW_CPU_X86_INTEL_SPEC_CTRL            |
| HW_CPU_X86_INTEL_SSBD                 |
| HW_CPU_X86_INTEL_VMX                  |
| HW_CPU_X86_MMX                        |
| HW_CPU_X86_MPX                        |
| HW_CPU_X86_PDPE1GB                    |
| HW_CPU_X86_SGX                        |
| HW_CPU_X86_SHA                        |
| HW_CPU_X86_SSE                        |
| HW_CPU_X86_SSE2                       |
| HW_CPU_X86_SSE3                       |
| HW_CPU_X86_SSE41                      |
| HW_CPU_X86_SSE42                      |
| HW_CPU_X86_SSE4A                      |
| HW_CPU_X86_SSSE3                      |
| HW_CPU_X86_STIBP                      |
| HW_CPU_X86_SVM                        |
| HW_CPU_X86_TBM                        |
| HW_CPU_X86_TSX                        |
| HW_CPU_X86_VMX                        |
| HW_CPU_X86_XOP                        |
| HW_GPU_API_DIRECT2D                   |
| HW_GPU_API_DIRECT3D_V10_0             |
| HW_GPU_API_DIRECT3D_V10_1             |
| HW_GPU_API_DIRECT3D_V11_0             |
| HW_GPU_API_DIRECT3D_V11_1             |
| HW_GPU_API_DIRECT3D_V11_2             |
| HW_GPU_API_DIRECT3D_V11_3             |
| HW_GPU_API_DIRECT3D_V12_0             |
| HW_GPU_API_DIRECT3D_V6_0              |
| HW_GPU_API_DIRECT3D_V7_0              |
| HW_GPU_API_DIRECT3D_V8_0              |
| HW_GPU_API_DIRECT3D_V8_1              |
| HW_GPU_API_DIRECT3D_V9_0              |
| HW_GPU_API_DIRECT3D_V9_0B             |
| HW_GPU_API_DIRECT3D_V9_0C             |
| HW_GPU_API_DIRECT3D_V9_0L             |
| HW_GPU_API_DIRECTX_V10                |
| HW_GPU_API_DIRECTX_V11                |
| HW_GPU_API_DIRECTX_V12                |
| HW_GPU_API_DXVA                       |
| HW_GPU_API_OPENCL_V1_0                |
| HW_GPU_API_OPENCL_V1_1                |
| HW_GPU_API_OPENCL_V1_2                |
| HW_GPU_API_OPENCL_V2_0                |
| HW_GPU_API_OPENCL_V2_1                |
| HW_GPU_API_OPENCL_V2_2                |
| HW_GPU_API_OPENGL_V1_1                |
| HW_GPU_API_OPENGL_V1_2                |
| HW_GPU_API_OPENGL_V1_3                |
| HW_GPU_API_OPENGL_V1_4                |
| HW_GPU_API_OPENGL_V1_5                |
| HW_GPU_API_OPENGL_V2_0                |
| HW_GPU_API_OPENGL_V2_1                |
| HW_GPU_API_OPENGL_V3_0                |
| HW_GPU_API_OPENGL_V3_1                |
| HW_GPU_API_OPENGL_V3_2                |
| HW_GPU_API_OPENGL_V3_3                |
| HW_GPU_API_OPENGL_V4_0                |
| HW_GPU_API_OPENGL_V4_1                |
| HW_GPU_API_OPENGL_V4_2                |
| HW_GPU_API_OPENGL_V4_3                |
| HW_GPU_API_OPENGL_V4_4                |
| HW_GPU_API_OPENGL_V4_5                |
| HW_GPU_API_VULKAN                     |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V1_0   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V1_1   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V1_2   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V1_3   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V2_0   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V2_1   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V3_0   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V3_2   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V3_5   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V3_7   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V5_0   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V5_2   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V5_3   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V6_0   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V6_1   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V6_2   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V7_0   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V7_1   |
| HW_GPU_CUDA_COMPUTE_CAPABILITY_V7_2   |
| HW_GPU_CUDA_SDK_V10_0                 |
| HW_GPU_CUDA_SDK_V6_5                  |
| HW_GPU_CUDA_SDK_V7_5                  |
| HW_GPU_CUDA_SDK_V8_0                  |
| HW_GPU_CUDA_SDK_V9_0                  |
| HW_GPU_CUDA_SDK_V9_1                  |
| HW_GPU_CUDA_SDK_V9_2                  |
| HW_GPU_MAX_DISPLAY_HEADS_1            |
| HW_GPU_MAX_DISPLAY_HEADS_2            |
| HW_GPU_MAX_DISPLAY_HEADS_4            |
| HW_GPU_MAX_DISPLAY_HEADS_6            |
| HW_GPU_MAX_DISPLAY_HEADS_8            |
| HW_GPU_RESOLUTION_W1024H600           |
| HW_GPU_RESOLUTION_W1024H768           |
| HW_GPU_RESOLUTION_W1152H864           |
| HW_GPU_RESOLUTION_W1280H1024          |
| HW_GPU_RESOLUTION_W1280H720           |
| HW_GPU_RESOLUTION_W1280H768           |
| HW_GPU_RESOLUTION_W1280H800           |
| HW_GPU_RESOLUTION_W1360H768           |
| HW_GPU_RESOLUTION_W1366H768           |
| HW_GPU_RESOLUTION_W1440H900           |
| HW_GPU_RESOLUTION_W1600H1200          |
| HW_GPU_RESOLUTION_W1600H900           |
| HW_GPU_RESOLUTION_W1680H1050          |
| HW_GPU_RESOLUTION_W1920H1080          |
| HW_GPU_RESOLUTION_W1920H1200          |
| HW_GPU_RESOLUTION_W2560H1440          |
| HW_GPU_RESOLUTION_W2560H1600          |
| HW_GPU_RESOLUTION_W320H240            |
| HW_GPU_RESOLUTION_W3840H2160          |
| HW_GPU_RESOLUTION_W640H480            |
| HW_GPU_RESOLUTION_W7680H4320          |
| HW_GPU_RESOLUTION_W800H600            |
| HW_NIC_ACCEL_DEFLATE                  |
| HW_NIC_ACCEL_DIFFIEH                  |
| HW_NIC_ACCEL_ECC                      |
| HW_NIC_ACCEL_IPSEC                    |
| HW_NIC_ACCEL_LZS                      |
| HW_NIC_ACCEL_RSA                      |
| HW_NIC_ACCEL_SSL                      |
| HW_NIC_ACCEL_TLS                      |
| HW_NIC_DCB_ETS                        |
| HW_NIC_DCB_PFC                        |
| HW_NIC_DCB_QCN                        |
| HW_NIC_MULTIQUEUE                     |
| HW_NIC_OFFLOAD_FDF                    |
| HW_NIC_OFFLOAD_GENEVE                 |
| HW_NIC_OFFLOAD_GRE                    |
| HW_NIC_OFFLOAD_GRO                    |
| HW_NIC_OFFLOAD_GSO                    |
| HW_NIC_OFFLOAD_L2CRC                  |
| HW_NIC_OFFLOAD_LRO                    |
| HW_NIC_OFFLOAD_LSO                    |
| HW_NIC_OFFLOAD_QINQ                   |
| HW_NIC_OFFLOAD_RDMA                   |
| HW_NIC_OFFLOAD_RX                     |
| HW_NIC_OFFLOAD_RXHASH                 |
| HW_NIC_OFFLOAD_RXVLAN                 |
| HW_NIC_OFFLOAD_SCS                    |
| HW_NIC_OFFLOAD_SG                     |
| HW_NIC_OFFLOAD_SWITCHDEV              |
| HW_NIC_OFFLOAD_TCS                    |
| HW_NIC_OFFLOAD_TSO                    |
| HW_NIC_OFFLOAD_TX                     |
| HW_NIC_OFFLOAD_TXUDP                  |
| HW_NIC_OFFLOAD_TXVLAN                 |
| HW_NIC_OFFLOAD_UCS                    |
| HW_NIC_OFFLOAD_UFO                    |
| HW_NIC_OFFLOAD_VXLAN                  |
| HW_NIC_PROGRAMMABLE_PIPELINE          |
| HW_NIC_SRIOV                          |
| HW_NIC_SRIOV_MULTIQUEUE               |
| HW_NIC_SRIOV_QOS_RX                   |
| HW_NIC_SRIOV_QOS_TX                   |
| HW_NIC_SRIOV_TRUSTED                  |
| HW_NIC_VMDQ                           |
| HW_NUMA_ROOT                          |
| MISC_SHARES_VIA_AGGREGATE             |
| STORAGE_DISK_HDD                      |
| STORAGE_DISK_SSD                      |
+---------------------------------------+
```
