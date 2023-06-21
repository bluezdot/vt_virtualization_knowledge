1. Định nghĩa
Thanos is a highly available Prometheus setup with long term storage capabilities. A CNCF Incubating project. (by thanos-io)

2. Thành phần:
![Thanos Sidecar](/vt_virtualization_knowledge/2023_06_15/resources/thanos_sidecar.png)
![Thanos Receiver](/vt_virtualization_knowledge/2023_06_15/resources/thanos_receiver.png)
- Sidecar: Kết nối tới Prometheus dưới dạng sidecar process, đọc data để query hoặc/và tải lên cloud storage
- Store Gateway: Cổng dịch vụ cho cloud storage
- Compactor: Nén và giữ lưu trữ trên cloud storage
- Receiver: Kết nối tới Prometheus
- Ruler: Đánh giá dữ liệu và alerting rules để đưa ra cảnh báo
- Querier: query data từ Thanos (Prometheus's v1 API)
- Query Frontend: Ủy quyền truy vấn cho Querier trong khi lưu trữ response và tùy chọn phân chia truy vấn theo từng ngày



**Ref:**
https://thanos.io/tip/thanos/quick-tutorial.md/
https://elastisys.com/