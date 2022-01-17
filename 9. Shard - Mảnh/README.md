## Sharding là gì?
Sharding là một tiến trình lưu giữ các bản ghi dữ liệu qua nhiều thiết bị và nó là một phương pháp của MongoDB để đáp ứng yêu cầu về sự gia tăng dữ liệu. Khi kích cỡ của dữ liệu tăng lên, nhu cầu truy vấn cao đòi hỏi một lượng lớn RAM và CPU mà chắc chắn 1 máy chủ sẽ khó lòng đáp ứng được . Sẽ có 2 giải pháp đối với các ứng dụng kiểu này đó là : mở rộng (scale) theo chiều ngang ( horizontal scaling ) và mở rộng theo chiều dọc ( vertical scaling )
* **Vertical scaling :** scale theo chiều dọc liên quan đến việc tăng dung lượng của một máy chủ, chẳng hạn như sử dụng CPU mạnh hơn hay thêm RAM hoặc tăng dung lượng lưu trữ.
* **Horizontal scaling :** scale theo chiều ngang liên quan đến việc chia nhỏ dữ liệu của hệ thống và tải chúng lên nhiều server , thêm server để tăng công suất . Mặc dù tốc độ hoặc công suất chung của mỗi máy có thể vẫn thế nhưng mỗi máy xử lý một tập hợp con của khối lượng dữ liệu chung vì thế nó có khả năng mang lại hiệu quả tốt hơn so với một server công suất cao . 

MongoDB hỗ trợ scale theo chiều ngang thông qua sharding. Với Sharding, có thể bổ sung thêm nhiều thiết bị để hỗ trợ cho việc gia tăng dữ liệu và các yêu cầu của các hoạt động đọc và ghi.

## Tính chất
Trong Replication, tất cả hoạt động ghi thực hiện ở node sơ cấp.

Các truy vấn tiềm tàng vẫn đến node sơ cấp.

Một Replica Set đơn có giới hạn là 12 node.

Bộ nhớ không thể đủ lớn khi tập dữ liệu hoạt động là lớn.

Local Disk là không đủ lớn.

Việc mở rộng phạm vi theo chiều dọc (vertical scaling) là quá tốn kém.

## Sharding trong MongoDB

Dưới đây là sơ đồ minh họa Sharding trong MongoDB sử dụng Sharded Cluster.

![image](https://user-images.githubusercontent.com/43572616/149704193-41ca4681-2279-4b70-a7cb-b6f1fe36d17d.png)

Trong sơ đồ trên, có ba thành phần chính:

**Shards:** được sử dụng để lưu giữ dữ liệu. Chúng cung cấp tính khả dụng cao và dữ liệu có tính đồng nhất. Trong môi trường tạo lập, mỗi Shard là một Replica Set riêng biệt.

**Config Servers:** đây là thành phần lưu trữ metadata và cấu hình cho mỗi cluster. 

Dữ liệu này chứa một ánh xạ của tập dữ liệu của Cluster tới Shards. Query Router sử dụng metadata này để hướng các hoạt động tới Shards cụ thể. Trong môi trường tạo lập, sharded clusters có chính xác 3 Config Servers.

**Query Routers (mongos):** về cơ bản nó là mongo instance, cung cấp một interface giữa client và sharded cluster. Query Router xử lý và hướng các hoạt động tới Shard và sau đó trả kết quả về Clients. 

Một Sharded Cluster có thể chứa nhiều hơn một Query Router để phân chia việc tải yêu cầu từ Client. Một Client gửi các yêu cầu tới một Query Router. Nói chung, một Sharded Cluster có nhiều Query Routers.

Việc sử dụng shards trên cluster cho phép mỗi shard chứa một tập hợp con của dữ liệu tổng . Khi dữ liệu lớn lên thì việc thêm các shards sẽ tăng khả năng lưu trữ của cluster
