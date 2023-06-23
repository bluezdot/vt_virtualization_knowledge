1. Định nghĩa
Cortex is a horizontally scalable, highly available, multi-tenant, long term Prometheus.
2. Thành phần
![Cortex](/vt_virtualization_knowledge/2023_06_15/resources/cortex.png)
- Remote write dữ liệu từ Prometheus đến Distributor. Distributor validate tính đúng đắn:
    - Tên các nhãn metric chính xác
    - Tuân thủ tối đa nhãn mỗi metric
    - Tuân thủ tối đa độ dài tên nhãn và giá trị 
    - Timestamp không nằm ngoài khoảng cấu hình
Sample sau đấy được chia thành batches và gửi tới Ingestor song song. Distributor là stateless
- Ingester nhận series samples từ Distributor, không lập tức gửi tới long-term storage mà giữ lại memory và xả định kì(Mặc định: 2hours). Ingesters có lifecycler để quản lí vòng đời của 1 ingester với các trạng thái:
    - Pending: Mới bắt đầu, chưa nhận yêu cầu đọc và ghi
    - Joining: Tham gia ring, chưa nhận yêu cầu đọc và ghi. Check token conflict, khi không có conflict thì chuyển sang active
    - Active: Có thể nhận yêu cầu đọc và ghi
    - Leaving: Rời ring, không còn nhận write nhưng vẫn nhận read
    - Unhealthy: failed. Lúc này distributor bỏ qua ingester khi build replication set.
Ingester là semi-stateful
- Querier xử lí truy vấn sử dụng PromQL, lấy samples từ cả Ingester và long-term storage bởi vì ingester thường giữ lại dữ liệu trong bộ nhớ. Querier có cơ chế deduplicate bởi vì có thể nhận dữ liệu từ replication set. Querier là stateless
- Compactor: Nén dữ liệu từ block storage, cập nhật per-tenant bucket index. Compactor là stateless
- Store Gateway: giữ storage bucket view luôn ở trạng thái cập nhật mới nhất:
    - Định kì scan bucket (default)
    - Định kì tải bucket index
- Query Frontend:
    - Store query ở queue và chờ querier nào đó lấy và xử lí. Sau khi xử lí xong querier gửi trả kết quả cho Query Frontend và sao đó forward cho client
- Ruler: thực thi PromQL truy vấn để ghi lại rules và alerts. Ruler là semi-stateful.
- Alert manager: Nhận alert noti từ Ruler, bỏ lặp và nhóm chúng lại, -> phân phối đến các kênh được cấu hình. Alert manager là semi-stateful
- Grafana query dữ liệu qua Store Gateway thông qua Query Frontend -> Querier để visualize. 

**Ref:**
https://cortexmetrics.io/docs/architecture/