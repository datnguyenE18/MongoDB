MongoDB không đi kèm với dữ liệu trong test database. Để test cần tải tập dữ liệu mẫu từ phần Import Example Dataset (https://docs.mongodb.com/getting-started/shell/import-data/) của tài liệu "Getting Started with MongoDB". 
Tài liệu JSON chứa một tập hợp các restaurants

* **Chuyển vào thư mục tạm:**
> \$ cd /tmp
##
* **Tải xuống tệp JSON:**
> \$ curl -LO https://raw.githubusercontent.com/mongodb/docs-assets/primer-dataset/primer-dataset.json
##
* **Import dữ liệu vào Test Database:**
> \$ mongoimport --db test --collection restaurants --file /tmp/primer-dataset.json

|||
| :------------:|:-------------:|
|--db|Tên dữ liệu sẽ sử dụng|
|--collection|Vị trí thông tin sẽ được lưu trong CSDL|
|--file|Vị trí file sẽ được thực hiện|

![image](https://user-images.githubusercontent.com/43572616/149675912-2bd2e2b5-d2d6-470b-bdf4-0ccc419c69c4.png)
##
* **Khởi chạy MongoDB Shell:**
> \$ mongosh
##
* **Truy vấn restaurants collection:**
> \> db.restaurants.find().limit( 1 ).pretty()

		find()	  hiển thị danh sách tất cả các restuarants trong dataset
		limit(n)	giảm đầu ra của truy vấn bằng một con số nhất định
		pretty()	Format thông tin dễ đọc hơn
##
* **Xóa Sample Dataset:**
> \> db.restaurants.drop()
##
* **Thoát:**
> \> exit

hoặc 

> Ctrl + C
