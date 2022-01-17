Replication có nghĩa là nhân bản, trong MongoDB thì replication là  một tiến trình đồng bộ hóa dữ liệu. 

Tập data sẽ được nhân bản trên nhiều server thay vì tập trung trên một single server. Nhờ vậy, replica set cung cấp tính năng high availability (HA) và dự phòng. Nó cũng scale read request (Mở rộng vùng đọc. Tức là không chỉ đọc trên Primary Node mà còn có thể đọc được trên các Second Node khác) cho mongodb. 

Quá trình replication này khác với quá trình backup / sao lưu ở chỗ là nó thực hiện realtime. Tức là khi bạn thêm dữ liệu vào A thì nó sẽ lập tức đồng bộ sang B… Trong khi quá trình backup thì thường thực hiện theo lịch (chạy cuối mỗi ngày, chạy hàng giờ…) và có thể phải xây dựng lại chỉ mục / index

**Cơ chế Replica Set ( thiết lập bản sao ) của MongoDB có hai mục đích chính:**
* Một là để dự phòng dữ liệu để phục hồi. Khi phần cứng bị lỗi hoặc node bị hỏng vì các lý do khác, bạn có thể sử dụng bản sao để khôi phục
* Mục đích khác là để phân chia đọc-ghi. Nó định tuyến các yêu cầu đọc đến bản sao để giảm áp lực đọc trên nút chính.

## Replica Set trong MongoDB

Replica /ˈreplɪkə/ là một nhóm các server MongoDB trong hệ Replication có chung nội dung dữ liệu. (Một nhóm server MongoDB tham gia thực hiện việc nhân bản)

Mỗi server MongoDB trong Replica Set được coi là 1 node hoặc 1 thể hiện.

Trong một Replica Set, sẽ có một node chính (primary node) và nhiều node phụ (secondary node) + node trọng tài (arbiter node)

![image](https://user-images.githubusercontent.com/43572616/149705544-2055ee8c-88ad-4012-a8b7-1ed5a4cbb76e.png)

* **Primary node (Node chính):** sẽ thực hiện nhận tất cả các write request để thực hiện sửa đổi data, các thay đổi trên data này sẽ được ghi lại vào file oplog, khi file oplog thay đổi, nó sẽ dựa vào các thông tin thay đổi đó để đồng bộ dữ liệu sang tất cả các secondary node (Node phụ). (Arbiter node sẽ không thực hiện ghi dữ liệu). Mỗi  Replica Set chỉ có một Primary node,

  Khi primary node lỗi, các Secondary node khác hoặc Arbiter node sẽ chọn lại một Primary node và node chính mới này nhận được yêu cầu đọc để xử lý request theo mặc định. Nếu muốn chuyển tiếp các yêu cầu đọc đến một secondary node để giảm tải cho node chính thì cần sửa đổi cấu hình kết nối trên máy khách.
  
  Nhưng  writeset có trên primary sẽ không thể ngay lập tức có trên secondary data,  nên trên Secondary Node sẽ không phản ánh trạng thái mới nhất của data set trên Primary Node

* **Các Secondary node (Các Node phụ):** duy trì, đồng bộ cùng một tập dữ liệu với primary node. Khi primary sập, các secondary sẽ tham gia vào việc bầu chọn ra một primary node mới

* **Arbiter node:** Một Arbiter node không lưu trữ dữ liệu hoặc tham gia vào cuộc bầu cử primary node, nhưng nó thực hiện bỏ phiếu bầu cử. Arbiter node có thể giảm các yêu cầu phần cứng để lưu trữ dữ liệu, vì arbiter chạy với nhu cầu tối thiểu về tài nguyên phần cứng. Tuy nhiên, điều quan trọng là không nên triển khai Arbiter node trên cùng một máy chủ với các node dữ liệu khác trong môi trường production
 
  Nhiệm vụ của arbiter là giám sát hệ replica set qua các đường liên kết heartbeat và bầu chọn một secondary lên primary khi failover. Arbiter thì sẽ mãi là arbiter không trở thành các node khác trong bất kỳ trường hợp nào.
	
	**Lưu ý:** Số lượng node có khả năng để tự vote ra được node chính phải là số lẻ để tránh lượng vote cho 2 node tương đương nhau. Replica bao gồm số data n chẵn, cộng với nút trọng tài:
  
![image](https://user-images.githubusercontent.com/43572616/149705680-32c67967-b789-4bee-a1db-78504bb123a2.png)

  Một replica set có thể có tối đa là 50 Node. Nếu lớn hơn 50 member thì phải dùng giải pháp khác. Mongodb có đề nghị giải pháp master-slave replication cho môi trường lớn hơn 50 Node.
	
  Nếu Arbiter node hỏng, ban đầu hệ thống vẫn có thể hoạt động bình thường. Hệ thống vẫn còn 2 loại node là Prime và Second. Nhưng cho đến khi 1 prime node hỏng mà số lượng Second Node còn lại bằng nhau và các phiếu vote cho các second node như nhau thì thực sự xảy ra vấn đề, lúc này cần một trọng tài hoặc làm lẻ số node.
	
  Nếu có lẻ các node thì các node second sẽ tự bầu ra 1 node Prime mới. Lúc này Arbiter node không có vấn đề.Nếu số Second node còn lại là chẵn và có số vote như nhau thì lúc này cần phiếu vote từ Arbiter Node.
	
## Cơ chế Automatic Failover trong Replica Set
  Các node trong Replica Set luôn duy trì kết nối với nhau (kết nối heartbeat ). Khi một Node nào đó down các Node còn lại sẽ nhận ra luôn và tự động tiến hành failover (cơ chế dựa trên voting). Dịch vụ sẽ vẫn không bị ảnh hưởng nếu secondary node bị hỏng, nhưng nếu primary node bị hỏng (bị shutdown, connection timeout…) thì các node còn lại sẽ tự động bầu ra 1 node khác làm primary node.

![image](https://user-images.githubusercontent.com/43572616/149705718-100cadac-5870-496c-b1ef-11d623d46065.png)


  Quá trình bầu primary node giống như bỏ phiếu vậy, node nào nhiều phiếu hơn thì trở thành primary node. Tuy nhiên sẽ có trường hợp có 2 node cùng số phiếu. Trong trường hợp này node arbiter sẽ quyết định node nào là primary node.

(Arbiter node chỉ có tác dụng ra bầu ra primary node chứ không chứa dữ liệu)

![image](https://user-images.githubusercontent.com/43572616/149705733-811eacd6-064b-4737-add9-674515d7e1a8.png)

Khi primary node bị ngắt kết nối lúc trước được kết nối trở lại vào Replica Set thì nó sẽ trở thành secondary node.

Mặc định, Client sẽ đọc dữ liệu từ primary node. Tuy nhiên ta có thể cấu hình cho phép client đọc dữ liệu từ các secondary node để giảm tải áp lực cho primary node.
