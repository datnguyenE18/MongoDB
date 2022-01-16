**Nhân rộng**

MongoDB cung cấp Replica Set cho phép nhân 2 hoặc nhiều bản sao của dữ liệu. Đồng thời, mỗi bản sao lại đóng vai trò chính và phụ.
- Khi nhân rộng, toàn bộ dữ liệu khi ghi và đọc được thực hiện trên bản sao chính.
- Bản sao thứ cấp sẽ dùng bản sao tích hợp để có thể duy trì các bản sao dữ liệu.
Trong trường hợp có bất kỳ bản sao chính nào bị thất bại thì Replica set sẽ chọn một bản sao thứ cấp để thay thế làm bản sao chính tiếp theo. Trong quá trình nhân rộng, Replica thứ cấp được tùy ý chọn các hoạt động nhưng dữ liệu cuối cùng vẫn phải tuân theo mặc định.
##
**Cân bằng tải**

MongoDB sử dụng Sharding nhằm chia tỷ lệ theo chiều ngang và xác định dữ liệu phân phối trong collection. Điều này giúp người dùng có thể chọn một Shard key. 
Nói tóm lại, MongoDB cân bằng tải bằng cách dựa vào các Shard key để chia dữ liệu thành các phạm vi và phân phối đồng đều. Chúng có thể chạy trên nhiều máy chủ khác nhau và thực hiện chức năng sao chép dữ liệu hay cân bằng tải nhằm giữ hệ thống hoạt động liên tục trong trường hợp phát sinh lỗi về phần cứng.
##
**Lưu trữ tệp**

Khi tìm hiểu hệ cơ sở dữ liệu MongoDB thì bạn sẽ thấy, tính năng lưu trữ tệp được dùng như một hệ thống tệp (gọi là GridFS) đóng vai trò cân bằng tải, đồng thời, sao chép dữ liệu trên nhiều máy tính. Cụ thể, GridFS chia một tệp ra làm nhiều phần và lưu trữ thành các tài liệu riêng biệt. Sau đó, người dùng dễ dàng truy cập GridFS thông qua Mongofiles hay các plugin sử dụng cho Nginx và Lighttpd.
##
**Tập hợp**

Tính năng này chính là chương trình mang đến ba giải pháp để thực hiện tập hợp gồm Aggregation Pipeline, Mapreduce và Single-purpose Aggregation. Trong đó, Aggregation Pipeline được đánh giá là có hiệu suất tốt nhất. 
##
**Giới hạn kích thước collection**

Các collection được MongoDB hỗ trợ thường có kích thước cố định. Vì thế, người ta gọi chúng là collection giới hạn. Với kích cỡ cố định, kết hợp cùng việc theo sau thứ tự chèn giúp tăng hiệu suất của các hoạt động liên quan đến dữ liệu. Và khi dữ liệu vượt giới hạn thì những tài liệu cũ hơn sẽ tự động bị xóa mà bạn không cần thực hiện thao tác thêm bất kỳ dòng lệnh nào.
