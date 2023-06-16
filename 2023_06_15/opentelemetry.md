![OTEL diagram](/vt_virtualization_knowledge/2023_06_15/resources/otel-diagram.svg)

**Observability**
1. Signals:
- Trace:
    - Tracer Provider: initialize one in life cycle to provide SDK, Resources, Exporter, ..
    - Tracer: Create spans chứa các thông tin xảy ra với mỗi operation, ví dụ như request. Tracers được tạo từ Tracer Provider.
    - Tracer Exporter: gửi traces tới consumer.


**Ref**
1. https://opentelemetry.io/docs/