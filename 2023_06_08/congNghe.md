Các công nghệ ảo hóa phổ biến:
1. OpenStack
2. Kubernetes

----

# 1. OpenStack
### 1.1. Khái niệm
OpenStack là một hệ điều hành đám mây kiểm soát các nhóm lớn tài nguyên mạng, lưu trữ và tính toán trong toàn bộ trung tâm dữ liệu, cho phép triển khai và quản lý  các cơ sở hạ tầng đám mây công cộng và đám mây riêng thông qua bảng điều khiển cho phép quản trị viên kiểm soát đồng thời trao quyền cho người dùng của họ cung cấp tài nguyên thông qua giao diện web.

Trên thị trường nền tảng đám mây, **OpenStack** thường có sự cạnh tranh với **Eucalyptus** và **Apache CloudStack**. Tuy nhiên, OpenStack vẫn được lựa chọn sử dụng nhiều hơn với mục đích là nền tảng đám mây gốc của nhiều nhà cung cấp.

### 1.2. Các thành phần cơ bản
![OpenStack Components](/2023_06_08/resources/openstackComponent.png)
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
    - Một số dự án bổ sung nổi bật như Ironic-Inspector, Bifrost, Sushy và networking-generic-switch. Ironic-Inspector cung cấp dịch vụ thu thập thông tin phần cứng và khám phá phần cứng. Bifrost tập trung và sử dụng vận hành không cần các thành phần OpenStack khác. Sushy là ứng dụng API Redfish nhẹ. Networking-generic-switch là plugin hỗ trợ quản lý cấu hình switchport cho bare metal machine.
- Swift (Object Storage):
    - Cung cấp phần mềm lưu trữ đám mây giúp lưu trữ và truy xuất dữ liệu thông qua API đơn giản. Nó được xây dựng để có thể mở rộng và tối ưu cho dộ bền, tính khả dụng và tính đồng thời lên toàn bộ tập dữ liệu.
- Cinder (Block Storage):
    - Cung cấp khối lượng lưu trữ cho máy ảo từ Nova, các máy chủ Ironic bare metal, containers, ...
    - Có thể sử dụng độc lập với các dịch vụ OpenStack khác.
- Keystone (Shared services):
    - Cung cấp API xác thực, token, catalog, policy cho các dịch vụ trong OpenStack. [5]
    - Hai tính năng chính: User Management, Service Catalog.
- Glance (Shared services):
    - Image Service - Giúp tìm kiếm, thu thập, cung cấp image cho các máy ảo.
    - Cung cấp RESTful API để quản lý, truy vấn image, metadata.

**Mối quan hệ giữa các thành phân**
![OpenStack Relationship](/2023_06_08/resources/openstack_arch.png)

# 2. Kubernetes
### 2.1 Khái niệm
Kubernetes là một công cụ điều phối vùng chứa (Container Orchestration) mã nguồn mở để tự động hóa việc triển khai, mở rộng quy mô và quản lý các ứng dụng được chứa trong vùng chứa. Dự án nguồn mở được tổ chức bởi Cloud Native Computing Foundation (CNCF). 
Kubernetes -> K8s cluster
### 2.2. Các thành phần cơ bản (K8s cluster)
![K8s Components](/2023_06_08/resources/k8sComponent.png)
**Thành phần chính**
- Control Plane: chứa Master Node với nhiệm vụ quản lý và điều phối (có thể cấu hình để đồng thời làm Worker Node).
    - kube-api-server: Trái tim của hệ thống - Nơi trung gian cung cấp API cho toàn bộ thành phần khác của hệ thống.
    - etcd: CSDL dạng key-value lưu trữ dữ liệu của K8s cluster. Các dữ liệu này là dữ liệu quản lý tài nguyên như thông tin node, pod, service, deployment, config-map. Nên đảm bảo có kế hoahcj dự phòng nếu K8s cluster sử dụng etcd làm CSDL.
    - kube-scheduler: Có nhiệm vụ theo dõi các Pods mới được tạo ra mà chưa được gắn vào Node và thực hiện tìm kiếm một Node phù hợp để chạy Pods đó lên. Các tham số ảnh hưởng việc điều phối Pod:
        - RAM/CPU
        - Phần cứng/Phần mềm
        - Các chỉ định affinity, anti-affinity, ...
    - kube-controller-manager: Có nhiệm vụ quản lý với nhiều controller chạy chung 1 process:
        - Node controller: Phát hiện và cảnh báo khi Node bị down.
        - Job controller: Theo dõi các object (đại diện cho một task cụ thể) được tạo ra sau đó tạo Pods để chạy các task đó tới khi hoàn thành.
        - Endpoints controller: Quản lý các endpoints, tạo kết nối giữa Service và Pods
        - Service Account: Tạo các account và token API mặc định cho namespace mới.
    - cloud-controller-manager (optional): Nhúng các logic điều khiển của nền tảng cloud cụ thể. CCM cho phép người quản lý kết nối k8s cluster với API của cloud ngoài.
- Data Plane: chứa Worker Node với nhiệm vụ tải, cấp tài nguyên để chạy các ứng dụng trên container
    - kubelet: Có vai trò đảm bảo các container ở trạng thái running ở trong Pod. Nó lắng nghe thông tin các Pod được gán cho Node mà nó đang chạy. kubelet không quản lý các container không được tạo ra bới K8s.
    - kube-proxy: Đây là network-proxy chạy trên từng node. Nó quản lý và duy trì các network rule trên các node. Các quy tắc này cho phép giao tiếp với các Pods từ network session bên ngoài hoặc trong cluster. kube-proxy sử dụng lớp gói lọc tin (packet) của hệ điều hành nếu có, không thì sẽ forward lưu lượng truy cập.
    - container runtime interface (CRI): Chịu trách nhiệm chạy các container.
- Addons: sử dụng các tài nguyên của K8s (Daemonset, Deployment, ...) để cài đặt các tính năng của cluster.
    - DNS
    - Dashboard
    - Container resource monitoring
    - Cluster-level logging

**Ref:** 
1. https://docs.openstack.org/
2. https://bkhost.vn/blog/openstack/
3. https://en.wikipedia.org/wiki/OpenStack
4. https://lamth.github.io/tailieu-Openstack  
5. https://viblo.asia/p/cam-ngo-ban-dau-ve-kubernetes-aWj53LyeK6m
6. https://viblo.asia/p/k8s-basic-tong-quan-cac-thanh-phan-cua-kubernetes-aAY4ql7qVPw
7. https://www.cloudnativeviet.net/documents/kubernetes/overview/components/