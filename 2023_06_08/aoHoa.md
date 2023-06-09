1. Khái niệm
2. Lợi ích (Vì sao phải ảo hóa?)
3. Các loại ảo hóa

--

1. Khái niệm
Ảo hóa là việc tạo ra phiên bản ảo - chứ không phải thực - của một thứ gì đó, chẳng hạn như server, storage device, OS hoặc network resource. 
Ảo hóa cho phép chia sẻ một phiên bản vật lý duy nhất của tài nguyên hoặc ứng dụng với nhiều môi trường được phân tách kĩ thuật. Nó thực hiện bằng cách gán một tên logic cho bộ lưu trữ vật lý và cung cấp một con trỏ tới tài nguyên vật lý đó khi được yêu cầu. 
Máy thực: Host Machine -> chứa các máy ảo: Guest Machine



2. Lợi ích
- Tránh xung đột tài nguyên khi chạy nhiều ứng dụng trên 1 máy chủ vật lý (Chạy mỗi ứng dụng trên mỗi máy chủ vật lý khác thì lại rất tốn tài nguyên).
- Tăng tính linh hoạt, khả năng mở rộng, tiết kiệm chi phí.
- Nhiều tác vụ quản lý hệ thống được tự động hóa
- Khả năng phục hồi nhanh sau thảm họa
- Giảm thiểu thời gian dừng hệ thống cho bảo trì thông thường: nâng cấp/thay thế phần cứng, ... vì hệ thống ảo hóa sử dụng chung thiết bị phần cứng phổ thông nên không cần phải thay thế toàn bộ các thiết bị


3. Các loại ảo hóa
3.1. Ảo hóa mạng: là một phương thức kết hợp và chia băng thông mạng có sẵn thành các kênh độc lập, các kênh này có thể tăng/giảm và được phân bổ cho một máy chủ hoặc thiết bị cụ thể theo thời gian thực. Ý tưởng này giúp loại bỏ sự phức tạp của hệ thống mạng bằng cách tách nó vào các phần có thể quản lý, giống như phân vùng ổ cứng để giúp việc quản lý các tệp dễ dàng hơn.
3.2. Ảo hoá lưu trữ: là sự tập trung các lưu trữ vật lý từ nhiều thiết bị lưu trữ thành một thiết bị lưu trữ duy nhất được quản lý và điều khiển từ một giao diện quản lý duy nhất. Ảo hóa lưu trữ thường được sử dụng trong các mạng lưu trữ.
3.3. Ảo hóa máy chủ: là phân chia các tài nguyên máy chủ (vi xử lý, bộ nhớ, lưu trữ, giao tiếp mạng…) cho nhiều máy ảo độc lập. Mục đích giúp cho người sử dụng không phải biết và quản lý các chi tiết phức tạp của tài nguyên máy chủ trong khi tăng cường việc chia sẻ và tận dụng tài nguyên cũng như duy trì khả năng mở rộng sau này. Lớp phần mềm này thường được gọi là hypervisor.
3.4. Ảo hóa dữ liệu: đang tóm tắt các chi tiết kỹ thuật truyền thống của dữ liệu và quản lý dữ liệu, chẳng hạn như vị trí, hiệu suất hoặc định dạng, thuận lợi cho việc truy cập rộng hơn và khả năng phục hồi tốt hơn gắn liền với nhu cầu kinh doanh.
3.5. Ảo hóa máy trạm: Việc ảo hóa máy trạm (máy tính của người dùng cuối) cho phép người dùng truy cập máy tính từ xa thông qua một thiết bị đầu cuối bất kỳ (máy tính bảng, điện thoại thông minh hay terminal). Các máy trạm ảo hóa chạy trên máy chủ đặt tại trung tâm dữ liệu giúp tăng tính linh động và an toàn, giảm chi phí quản lý.
3.6. Ảo hóa ứng dụng: lớp ứng dụng được tách khỏi hệ điều hành. Bằng cách này ứng dụng có thể chạy dưới dạng đóng gói mà không bị phụ thuộc vào hệ điều hành bên dưới. Điều này có thể cho phép một ứng dụng Windows chạy trên Linux và ngược lại.

Ref: 
1. https://www.javatpoint.com/virtualization-in-cloud-computing
2. https://vietnix.vn/ao-hoa-la-gi/
3. https://adg.vn/tin-cong-nghe/ao-hoa-va-loi-ich-cua-ao-hoa#:~:text=L%E1%BB%A3i%20%C3%ADch%20c%E1%BB%A7a%20%E1%BA%A2o%20h%C3%B3a,v%E1%BA%ADn%20h%C3%A0nh%20v%C3%A0%20b%E1%BA%A3o%20d%C6%B0%E1%BB%A1ng.
