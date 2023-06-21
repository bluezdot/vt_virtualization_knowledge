
All 3 projects are opensource Apache 2.0-licensed.
|             | VictoriaMetrics      | Cortex | Thanos     |
|  :---       | :---        |    :----:   |          ---: |
| Definition  |      |   |   |
| Community-driven | No | Yes | Yes |
| Mention     | 82 | 17 | 62 |
| Star | 8.7k | 5.1k | 11.8k |
| Growth | 3.0% | 0.9% | 6.8%|
| | | ||

Of the top six (InfluxDB, TimescaleDB, M3DB, Victoria Metrics, Thanos, and Cortex), let’s see how they each compare to each other.

Rank 4. InfluxDB:
- Not community-driven
- Lack MUST HAVEs (Availability & Deduplication)
- Resource hungry

Rank 3. TimescaleDB
- Not community-driven
- Tốn bộ nhớ (Khởi tạo lưu trữ cùng với timestamp và labels với mỗi hàng)

Rank 2: M3DB & VictoriaMetrics
- Not community-driven

Rank 1: Cortex & Thanos
- Both CNCF incubating projects

**Ref:**
https://www.libhunt.com/compare-VictoriaMetrics-vs-cortexproject--cortex
https://github.com/thanos-io/thanos
https://github.com/VictoriaMetrics/VictoriaMetrics
https://github.com/cortexproject/cortex
long-term-metrics-storage-thanos-vs-cortex-vs-influxdb-vs-m3db-vs-victoriametrics-vs-timescaledb/