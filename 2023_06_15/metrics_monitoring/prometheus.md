1. Định nghĩa
- Hệ thống mã nguồn mở monitoring & alerting do Soundcloud viết
- Thu thập metrics dưới dạng dữ liệu time-series

2. Thành phần
- Prometheus Server: Thu thập và lưu trữ dữ liệu time-series
- Client-libs: phục vụ tạo các đoạn mã ứng dụng tính toán cho dịch vụ monitor.
- Push-gateway: Tạo metrics từ short-lived jobs, được coi như là Metric cache.
- Special-purposes Exporter: HAProxy, StatsD, Graphite, etc. i) Cung cấp các target endpoint mà Prometheus định kì truy vấn. ii) Xuất metrics data từ ứng dụng non-prometheus. iii) Transform dữ liệu bắt được về dạng có thể tích hợp được cho Prometheus. iv) Khởi tạo Webserver để hiển thị metrics thông qua url.
https://www.airplane.dev/blog/prometheus-exporters
- Alert-manager: Xử lí alert
- other tools
![Prometheus](/vt_virtualization_knowledge/2023_06_15/resources/prometheus.png)


Prometheus không phù hợp cho lưu trữ dữ liệu trong khoảng thời gian dài (15 ngày). [Official document](https://prometheus.io/docs/prometheus/latest/storage/#operational-aspects) đề cập: 
"Prometheus's local storage is not intended to be durable long-term storage; external solutions offer extended retention and data durability." 
Tác giả gốc của Prometheus quyết định không xây dựng lớp lưu trữ phân tán mà giữ mọi thứ đơn giản nhất. Prometheus lấp đầy 1 ổ đĩa mà không phân mảnh hoặc sao chép dữ liệu. Giải pháp là sử dụng NFS (Network File System)

**Ref:**
https://github.com/hocchudong/ghichep-prometheus/blob/master/1.Gioi_thieu_Prometheus.md
https://prometheus.io/docs
