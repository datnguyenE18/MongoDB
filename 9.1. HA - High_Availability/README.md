## Giải pháp độ sẵn sàng cao

High availability có nghĩa “Độ sẵn sàng cao”. Tức là những máy chủ hoặc thiết bị luôn trong tình trạng sẵn sàng phục vụ, giảm thiểu khả năng gián đoạn của hệ thống. Hoặc có thể hiểu đơn giản High availability là một giải pháp hoặc quy trình hay công nghệ nhằm thực hiện chức năng đảm bảo cho ứng dụng, cơ sở dữ liệu có thể truy cập được 24/7 trong mọi điều kiện.

Để có thể thực hiện được điều này, cơ chế cần tối thiểu 2 máy chủ cùng chạy song song và hoạt động liên tục. Nếu xảy ra tình huống một máy chủ gặp sự cố thì máy còn lại sẽ thay thế nhằm giúp hệ thống vẫn tiếp tục hoạt động bình thường. 

## Giải pháp high availability
Về cơ bản sẽ có 5 giải pháp thiết lập high availability cho database trong MS SQL Server. 

Cụ thể:
* Replication
* Log Shipping
* Mirroring
* Clustering
* AlwaysON Availability Groups

## Replication

Theo giải pháp này thì dữ liệu gốc được sao đến điểm đích thông qua tác vụ sao chép (agent/job). Đồng thời, dùng công nghệ ở mức độ đối tượng. 

Một vài thuật ngữ trong Replication:
* Publisher (Bên phát hành): tức máy chủ nguồn.
* Distributor (Bên phân phối): mục này tùy chọn. Nó cho phép lưu trữ dữ liệu đã sao chép cho bên đăng ký (gọi là Subscriber).
* Bên đăng ký: tức máy chủ đích.

## Log Shipping

Thông qua tác vụ sao lưu Transaction Log, dữ liệu gốc sẽ được sao chép đến điểm đích và dùng công nghệ ở mức độ cơ sở dữ liệu. 

Các thuật ngữ cần biết:
* Primary Server (Máy chủ sơ cấp): là máy chủ nguồn.
* Secondary Server (Máy chủ thứ cấp): là máy chủ đích.
* Máy chủ giám sát được giám sát bằng trạng thái Log Shipping. Bạn có thể tùy chọn máy chủ này hoặc không,

## Mirroring

Thiết lập high availability cho database trong MS SQL Server bằng cách sao chép dữ liệu sơ cấp sang thứ cấp thông qua các giao dịch mạng, nhờ sự hỗ trợ của các điểm kết nối hình chiếu với số cổng. Đồng thời, sử dụng công nghệ cấp độ cơ sở dữ liệu.

Các thuật ngữ cần biết:
* Principal Server (Máy chủ gốc): máy chủ nguồn.
* Mirror Server (Máy chủ hình chiếu): máy chủ đích.
* Witness Server (Máy chủ chứng kiến): dùng cho giải pháp chịu lỗi tự động. Máy chủ này tùy chọn theo nhu cầu sử dụng của người dùng.

## Clustering

Cách thiết lập high availability này sử dụng dữ liệu đã lưu trữ tại địa điểm chung, dùng cho máy chủ sơ cấp và thứ cấp. Giải pháp này sử dụng công nghệ ở mức bản cài (instance) và phải thiết lập Windows Clustering tại khu vực lưu trữ chung. 

Các thuật ngữ cần biết:
* Active Node (Node chủ động): nơi SQL Services chạy.
* Passive Node (Node bị động): nơi SQL Services không chạy.

## AlwaysON Availability Groups

Dữ liệu sơ cấp được chuyển sang thứ cấp bằng các giao dịch mạng. Và dùng công nghệ ở mức độ nhóm cơ sở dữ liệu. Với cách này thì Windows Clustering không cần thiết lập nơi lưu trữ chung. 

Các thuật ngữ cần biết:
* Primary Replica: máy chủ nguồn.
* Secondary Replica: máy chủ đích.
