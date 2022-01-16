### 1. Xem database đang sử dụng
Để xem database đang sử dụng (current database):
> db
##
### 2. Xem tất cả các database trong hệ thống
Xem tất cả các database đã được tạo trên MongoDB:
> show dbs

![image](https://user-images.githubusercontent.com/43572616/149676139-46d61776-8cd8-4fdb-96e9-8aadb6aa3365.png)
	
Lệnh này sẽ chỉ hiện ra các database đã có ít nhất một collection (hiểu như table trong MySql), còn nếu chưa có thì nó sẽ không hiện ra.
##
### 3. Lấy tất cả dữ liệu trong collection
Để lấy tất cả dữ liệu trong collection, sử dụng phương thức find():
> db.\<collectionName>.find()

Trong đó <collectionName> là tên của collection muốn truy vấn. Nếu muốn dữ liệu trả về được hiển thị theo cấu trúc đã được định sẵn thì thêm hàm pretty() vào phía sau hàm find():
> db.\<collectionName>.find().pretty()

##
### 4. Truy vấn có điều kiện trong MongoDB
Để truy vấn có điều kiện trong MongoDB thì bạn cũng sử dụng cú pháp tương tự như phần 1, nhưng lúc này chúng ta sẽ thêm điều kiện vào trong hàm find() với cú pháp sau:

> db.collectionName.find(condition)

Cú pháp của các mệnh đề điều kiện:

![image](https://user-images.githubusercontent.com/43572616/149676181-f09cf431-3ca5-4605-be74-2e0d24de0a64.png)


