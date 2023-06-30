1. Định nghĩa
VictoriaMetrics is a fast, cost-effective and scalable monitoring solution and time series database.

2. Kiến trúc cluster
![Victoriametrics](/vt_virtualization_knowledge/2023_06_15/resources/victoriametrics.png)
- vmstorage: lưu trữ dữ liệu thô và trả về dữ liệu truy vấn 
- vminsert: nhận dữ liệu tích hợp và truyền đến các vmstorage nodes dựa theo hàm băm metric name và label.
- vmselect: truy vấn dữ liệu

![Vmagent](./vmagent.png)
<!-- ![alt text](./victoriametrics.png "Title") -->
**Ref:**
https://docs.victoriametrics.com/