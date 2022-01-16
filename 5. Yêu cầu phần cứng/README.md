## Disk requirements
The amount of disk space required by MongoDB depends entirely on the number of assets in the system. If the number of assets is stable, or if there is a steady influx / deletion rate in the archive so that the number of assets remains at a certain level, the instance will not grow.
Each asset remains approximately 10 days in MongoDB after deletion. Hence, the approximate formula for calculating the number of assets can be expressed as follows:
 
> **N = i * (t + 10) + p**

p: Number of assets that are permanently in the system

t: Max number of days an asset is kept in the system after ingestion

i: Number of assets ingested per day (24h)

N: Total number of assets in the system at any given time.
 
Each asset requires approximately 10Kb of space. The formula to calculate the disk space required for assets in MongoDB goes like this:
Disk space (Megabytes) = N * 0,01
(**N** is the total number of assets, as explained above.)

## Memory requirements
Ram là tài nguyên quan trọng nhất
MongoDB requires approximately 1GB of RAM per 100.000 assets. If the system has to start swapping memory to disk, this will have a severely negative impact on performance, and should be avoided.

## MongoDB chạy trên hầu hết các HĐH thông dụng
Nên chạy trên hệ thống 64bit
