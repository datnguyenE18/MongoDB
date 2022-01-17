> \# mongorestore --drop -d <database_will_be_restored> <location_to_folder_containing_mongodb_database>
>
> \# mongorestore --drop --db <database_will_be_restored> <location_to_folder_containing_mongodb_database>
>
> \# mongorestore --host $HOST --port $PORT -u $USERNAME -p $PASSWORD -d $DB <location_to_folder_containing_mongodb_database>

**Chú thích:**
* –drop : option này sẽ xoá file backup database rồi mới khôi phục
* -d/–db : tên MongoDB database
* <location_to_folder_containing_mongodb_database> : thư mục chứa file backup
