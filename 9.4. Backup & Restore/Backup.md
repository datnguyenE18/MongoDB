> \# mongodump -d <database_name> -o <folder_will_contain_backup_file>
>
> \# mongodump --db <database_name> --out <folder_will_contain_backup_file>
>
> \# mongodump --host $HOST --port $PORT -u $USERNAME -p $PASSWORD -d $DB -o <folder_will_contain_backup_file>

Chú thích:
* **-d/–db** : tên MongoDB Database
* **-o/–out** : đường dẫn thư mục sẽ chứa dữ liệu backup của MongoDB Databse.

![image](https://user-images.githubusercontent.com/43572616/149735578-b6254b7d-8ee3-42fa-b0d2-f39203bcdc0c.png)
![image](https://user-images.githubusercontent.com/43572616/149735589-dd0854ea-973a-4b40-b722-625e887c750c.png)
![image](https://user-images.githubusercontent.com/43572616/149735601-13c9fad1-88df-41ab-8dbd-98f5bc225144.png)

### Một số tùy chọn:

> 	\# mongodump --host HOST_NAME --port PORT_NUMBER
> 	
> 	\# mongodump -h HOST_NAME -p PORT_NUMBER

**Lệnh này sẽ sao lưu tất cả cơ sở dữ liệu của mongod instance đã xác định**

* Find out HostName:

** B1: Chạy: 
> \$ mongo

** B2: 
>\> hostname() 
>
>**hoặc**
>
>\> getHostName()

![image](https://user-images.githubusercontent.com/43572616/149738331-9b3936d9-5db8-495b-aed2-53d99cef3d7c.png)

## 		
> 	\# mongodump --dbpath DB_PATH --out BACKUP_DIRECTORY
> 	
> 	\# mongodump -d DB_PATH -o BACKUP_DIRECTORY
	
**Lệnh này chỉ sao lưu cơ sở dữ liệu đã xác định tại path chỉ định**
![image](https://user-images.githubusercontent.com/43572616/149738497-f7e7c81c-2065-4fc2-9d8e-42b5eabb403c.png)

	
> 	\# mongodump --collection COLLECTION --db DB_NAME
> 	
> 	\# mongodump -c COLLECTION -d DB_NAME
##
**Lệnh này chỉ sao lưu Collection đã xác định của cơ sở dữ liệu đã cho**
	
![image](https://user-images.githubusercontent.com/43572616/149738833-17a74c7e-0d6c-4124-a815-c5d29bbd19d1.png)

