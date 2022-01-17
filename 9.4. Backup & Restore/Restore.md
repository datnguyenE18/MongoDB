> \# mongorestore --drop -d <database_will_be_restored> <location_to_folder_containing_mongodb_database>
>
> \# mongorestore --drop --db <database_will_be_restored> <location_to_folder_containing_mongodb_database>
>
> \# mongorestore --host $HOST --port $PORT -u $USERNAME -p $PASSWORD -d $DB <location_to_folder_containing_mongodb_database>

**Chú thích:**
* –drop : option này sẽ xoá file backup database rồi mới khôi phục
* -d/–db : tên MongoDB database
* <location_to_folder_containing_mongodb_database> : thư mục chứa file backup

![image](https://user-images.githubusercontent.com/43572616/149739710-352d5e4a-1f85-4dca-8e6d-cef4d4d7e8d8.png)

![image](https://user-images.githubusercontent.com/43572616/149739719-1b945bd7-ae51-4a8f-90c3-36e959dfdb34.png)
