![OTEL diagram](/vt_virtualization_knowledge/2023_06_15/resources/otel-diagram.svg)

**Observability**
1. Signals:
- Traces:
    - Tracer Provider: initialize one in life cycle to provide SDK, Resources, Exporter, ..
    - Tracer: Create spans chứa các thông tin xảy ra với mỗi operation, ví dụ như request. Tracers được tạo từ Tracer Provider.
    - Tracer Exporter: gửi traces tới consumer.
    - Context Propagation
    - Span: 1 đơn vị của work hoặc operation - xây dựng nên những khối traces:
        - Name
        - Parrent span id (empty cho nguồn span)
        - Start và End timestamps
        - Span Context
        - Attributes
        - Span Events
        - Span Links
        - Span Status

- Metrics:
    - 6 metrics instruments:
        - Counter: Chỉ đếm tăng liên tục theo time
        - Asynchronous Counter: Chỉ đếm tăng theo số export
        - UpDownCounter: Chỉ đếm tăng theo time nhưng cũng có thể giảm
        - Asynchronous UpDownCounter: giống UpDownCounter nhưng theo số export
        - (Asynchronous) Gauge: Đo giá trị tại thời điểm đọc
        - Histogram: 
    - Vài usecases:
        - #bytes đọc bởi 1 service/protocol type
        - #bytes đọc và bytes/request
        - duration của system call
        - request sizes để quyets định trend
        - CPU, memory usage của process
        - avarage balance values của 1 tài khoản
        - những request hoạt động  hiện tại đang được xử lí.

- Logs:
- Baggage: Contextual information that's passed giữa các spans

2. Instrumentation
- Automatic: .NET, Java, Javascript, Python, PHP
- Manual: 
- Libraries:

3. Components
- Cross-language specification: mô tả yêu cầu và mong đợi của mọi triển khai: API, SDK, Data
- Collector: 
- Language SDK:
...

4. Semantic Conventions
- Metrics: 
    - Metric mới không được trùng tên metrics đã có sẵn
    - Không dùng số nhiều
    - Sử dụng .count cho record đếm
    - General naming:
        - limit
        - usage
        - utilization
        - time
        - io

**Ref**
1. https://opentelemetry.io/docs/