1. Định nghĩa
Thanos is a highly available Prometheus setup with long term storage capabilities. A CNCF Incubating project. (by thanos-io)

2. Thành phần:
![Thanos Sidecar](../resources/thanos_sidecar.png)
![Thanos Receiver](../resources/thanos_receiver.png)
- Sidecar: Kết nối tới Prometheus dưới dạng sidecar process, đọc data để query hoặc/và tải lên cloud storage. Giữ data trong vòng 2 giờ.
- Store Gateway: Cổng dịch vụ cho cloud storage
- Compactor: Nén và giữ lưu trữ trên cloud storage
- Receiver: Kết nối tới Prometheus
- Ruler: Đánh giá dữ liệu và alerting rules để ghi lại alerts, kết hợp với Prometheus Alerting manager để ra cảnh báo
- Querier: query data từ Thanos (Prometheus's v1 API)
- Query Frontend: Ủy quyền truy vấn cho Querier trong khi lưu trữ response và tùy chọn phân chia truy vấn theo từng ngày



**Ref:**
https://thanos.io/tip/thanos/quick-tutorial.md/
https://elastisys.com/
https://mattermost.com/blog/monitoring-cloud-environments-at-scale-with-prometheus-and-thanos/