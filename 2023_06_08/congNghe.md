Các công nghệ ảo hóa phổ biến:
1. OpenStack
2. Kubernetes

----

# 1. OpenStack
### 1.1. Khái niệm
OpenStack là một hệ điều hành đám mây kiểm soát các nhóm lớn tài nguyên mạng, lưu trữ và tính toán trong toàn bộ trung tâm dữ liệu, cho phép triển khai và quản lý  các cơ sở hạ tầng đám mây công cộng và đám mây riêng thông qua bảng điều khiển cho phép quản trị viên kiểm soát đồng thời trao quyền cho người dùng của họ cung cấp tài nguyên thông qua giao diện web.

Trên thị trường nền tảng đám mây, **OpenStack** thường có sự cạnh tranh với **Eucalyptus** và **Apache CloudStack**. Tuy nhiên, OpenStack vẫn được lựa chọn sử dụng nhiều hơn với mục đích là nền tảng đám mây gốc của nhiều nhà cung cấp.

### 1.2. Các thành phần cơ bản
![OpenStack Components](/2023_06_08\resources\openstackComponent.png)
**Các thành phần chính:**
- Horizon (Web Frontend):
    - Cung cấp giao diện người dùng dựa trên Web cho các dịch vụ khác: Nova, Swift, Keystone, ..
    - Cung cấp 3 bảng trung tâm: User Dashboard, System Dashboard, Settings Dashboard.
    - Cung cấp tập hợp các tóm tắt API cho các dự án OpenStack cốt lõi.
- Heat (Orchestration):
    - Điều phối các ứng dụng cloud khác nhau dựa trên templates, thông qua OpenStack-native REST API và CloudFormation-compatible Query API
- Nova (VirtualMachine - Compute):
    - Cung cấp phương thức tạo ra các phiên bản tính toán dưới dạng máy ảo, máy chủ phần cứng thực (nhờ Ironic). Nova chạy dưới dạng một tập deamons trên các máy chủ Linux có sẵn để cung cấp dịch vụ đó
    - Nova được thiết kế để mở rộng theo chiều ngang, thay vì chuyển sang các máy chủ lớn hơn, bạn mua nhiều máy chủ hơn và cấu hình giống hệt nhau.
- Neutron (Networking):
    - Cung cấp dịch vụ kết nối mạng giữa các thiết bị (VD: vNIC) được quản lý bởi component khác (VD: Nova) -> OpenStack Networking API.
- Ironic (Bare Metal):
    - Cung cấp các máy tính vật lý. Mặc định, Ironic sử dụng PXE và IPMI hoặc Redfish để cung cấp và quản lý các máy tính vật lý, nhưng nó hỗ trợ và có thể mở rộng bằng các plugins để triển khai các chức năng bổ sung.
    - Một số dự án bổ sung nổi bật như Ironic-Inspector, Bifrost, Sushy và networking-generic-switch.
- Swift (Storage):
- Cinder (Storage):
- Keystone (Shared services):
- Glance (Shared services):

# 2. Kubernetes
### 2.1 Khái niệm
Kubernetes là một công cụ điều phối vùng chứa mã nguồn mở để tự động hóa việc triển khai, mở rộng quy mô và quản lý các ứng dụng được chứa trong vùng chứa. Dự án nguồn mở được tổ chức bởi Cloud Native Computing Foundation (CNCF).
### 2.2. Các thành phần cơ bản (K8s cluster)
Ref: 
1. https://docs.openstack.org/
2. https://bkhost.vn/blog/openstack/
3. https://en.wikipedia.org/wiki/OpenStack  
2. https://viblo.asia/p/cam-ngo-ban-dau-ve-kubernetes-aWj53LyeK6m