Database Monitoring ?
- Lưu trữ các thông tin về hệ thống với mục đích giám sát, đảm bảo hiệu năng và độ khả dụng cao cho hạ tầng ứng dụng.
- Một vài metrics như workload, configuration, memory tiêu thụ, tốc độ transaction, tốc độ usercall. Hơn nữa, các điểm dữ liệu như memory buffers, I/O operations, connections infor, thread infor, read/write request và table locks cũng được theo dõi.

Triển khai như nào?
Không có thiết kế nào "one-size-fits-all". Nhưng thông thường cần các step chung này
- Continuous monitoring of defined metrics
- Automatically collect and store resource consumption, availability, and performance metrics
- Analyze and visualize key database and server parameters
- In-depth report generation using historic data to show utilization and capacity trends
- Send alerts in case of unusual behavior of KPIs
- Recommend precise actions to resolve performance issues
- Assess end-user metrics to identify and isolate database issues
- Maintain detailed notes for recurring problems for faster resolution
- Accurately diagnose root causes of issues

Top 5 database monitoring tools:
- SolarWinds Db Performance Monitor: https://www.tek-tools.com/database/database-monitoring-tools-and-tips#solarwinds-dpm
- SolarWinds Db Performance Analyzer: https://www.tek-tools.com/database/database-monitoring-tools-and-tips#solarwinds-dpa
- dbWatch Db Control: https://www.tek-tools.com/database/database-monitoring-tools-and-tips#dbwatch
- Paessler PRTG Network monitoring: https://www.tek-tools.com/database/database-monitoring-tools-and-tips#prtg
- SQL Sentry: https://www.tek-tools.com/database/database-monitoring-tools-and-tips#sql-sentry

3 cột trụ của observability: metrics, logs, traces:
- Logs: ghi lại events, warnings, errors xảy ra trong môi trường. Hầu như logs bao gồm bối cảnh như thời gian sự kiện xảy ra hay người dùng hoặc endpoint gắn với nó. Lợi ích của logs là cung cấp bao quát về các sự kiện và lỗi xảy ra trong vòng đời của tài nguyên phần mềm. Hạn chế: 1, nó chỉ ghi lại những logs đã được cấu hình để lưu lại; 2, log data có thể bị mất khi container xảy ra sự cố và bị shutdown, giải pháp là move data sang chỗ khác trong quá trình container running nhưng vẫn có khả năng bị miss.
- Metrics: những đo lường định tính về health, performance của ứng dụng và cơ sở hạ tầng. Ví dụ: metrics ứng dụng có thể track #transactions/second có thể xử lí; metrics csht có thể đo lường #CPU/memory resources tiêu thụ trên server. 2 phương thức phổ biến: Weaveworks' RED method (focus on rate, errors & request duration) và Google's Golden Signals method (focus on latency, traffic, errors & saturation). Lợi ích chính của metrics là cung cấp thông tin real-time về trạng thái của tài nguyên -> quan sát được ứng dụng phản hồi như nào và phát hiện trạng thái bất thường về tiêu thụ tài nguyên. Hạn chế: 1, giống như logs - chỉ ghi lại những dữ liệu được thiết kế; 2, không hữu ích trong việc xác định ra nguồn vấn đề, đặc biệt là trong hệ thống phân tán. Chỉ có khả năng chỉ ra hệ thống đang gặp phải vấn đề.
- Traces: theo dõi các request theo luồng qua các phần của hệ thống. Traces ghi lại việc mỗi thành phần ứng dụng mất bao lâu để xử lí request và chuyển tiếp kết quả sang thành phần kế tiếp. Traces còn chỉ định ra phần nào của ứng dụng gây ra lỗi. Lợi ích: Hiệu quả nhất trong việc tìm ra root cause problem. Hạn chế: Chỉ 1 phần của toàn bộ ứng dụng được trace trong hầu hết trường hợp bởi vì chạy trace tốn rất nhiều time và resources tiêu thụ để trace mọi request mà 1 ứng dụng nhận. Nghĩa là khi lỗi xảy ra, chưa chắc có sẵn dữ liệu tracing. 
- 3 thành phần này hoạt động độc lập sẽ cung cấp góc nhìn có giá trị khác nhau, tuy đều có giới hạn riêng -> Khi kết hợp cả 3 thông tin này, ta sẽ có bức tranh tổng quát về chuyện gì đang xảy ra trong môi trường ứng dụng.
https://www.techtarget.com/searchitoperations/tip/The-3-pillars-of-observability-Logs-metrics-and-traces

- HomeServer uptime monitoring, Kuma

5 gợi ý khi sử dụng Thanos kết hợp với Prometheus:
1. Caching là giải pháp phổ biến nhất để tăng tốc độ response, Query Frontend sẽ giúp làm điều này: query-frontend-config.yaml: |

    type: MEMCACHED

    config:

      addresses: ["host:port"]

      timeout: 500ms

      max_idle_connections: 300

      max_item_size: 1MiB

      max_async_concurrency: 40

      max_async_buffer_size: 10000

      max_get_multi_concurrency: 300

      max_get_multi_batch_size: 0

      dns_provider_update_interval: 10s

      expiration: 336h

      auto_discovery: true

  query-frontend-go-client-config.yaml: |

    max_idle_conns_per_host: 500

    max_idle_conns: 500

2. Compactor, nén giữ liệu để giảm độ lớn:

    retentionResolutionRaw: 90d

    retentionResolution5m: 1y

    retentionResolution1h: 2y

    consistencyDelay: 30m

    compact.concurrency: 6

    downsample.concurrency: 6

    block-sync-concurrency: 60

3. Chỉ giữ những data quan trọng, và discard những data không cần thiết, setting Node Exporters để làm điều đó:

--no-collector.arp

--no-collector.bonding

--no-collector.btrfs

--no-collector.conntrack

--no-collector.cpufreq

--no-collector.edac

--no-collector.entropy

--no-collector.fibrechannel

--no-collector.filefd

--no-collector.hwmon

--no-collector.infiniband

--no-collector.ipvs

--no-collector.nfs

--no-collector.nfsd

--no-collector.powersupplyclass

--no-collector.rapl

--no-collector.schedstat

--no-collector.sockstat

--no-collector.softnet

--no-collector.textfile

--no-collector.thermal_zone

--no-collector.timex

--no-collector.udp_queues

--no-collector.xfs

--no-collector.zfs

--no-collector.mdadm

4. Phân mảnh database khi nó quá lớn, S3 storage:

.Sharded store covering 0 - 30 days

thanos-store-1:

  "min-time": -30d

  "store.grpc.series-sample-limit": "50000000"

.Sharded store covering 30 - 90 days

thanos-store-2:

   "min-time": -90d

   "max-time": -30d

   "store.grpc.series-sample-limit": "50000000"

.Sharded store covering > 90 days

thanos-store-3:

   "max-time": -90d

   "store.grpc.series-sample-limit": "50000000"

5. Scaling & high availability
    Manual scaling
    Semi-automatic scaling