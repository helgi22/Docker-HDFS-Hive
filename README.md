# Docker-HDFS-Hive

## Deploy instruction to Windows OS

### Set up winutils:

winutils.exe hadoop.dll and hdfs.dll binaries for hadoop on windows
https://github.com/steveloughran/winutils

place a copy of hadoop-ver folder on your local drive "C:\Hadoop\bin"  and set environment vars:

```
HADOOP_HOME=<your local hadoop-ver folder>
SPARK_HOME=<your Spark home folder>
SPARK_LOCAL_IP=localhost
PATH=%PATH%;%SPARK_HOME%\bin;%HADOOP_HOME%\bin
```
```commandline
mkdir -p hdfs/datanode
mkdir -p hdfs/namenode
mkdir -p metastore-postgresql/postgresql/data
```



Add to C:\WINDOWS\system32\drivers\etc\host

```
127.0.0.1 hive-metastore namenode resourcemanager datanode
```

Copy .\spark\conf\[hdfs-site.xml, hdfs-site.xml]  to %SPARK_HOME%\conf  for using with local Spark instance

##### Install Docker Desktop on Windows
https://docs.docker.com/desktop/install/windows-install/

~~~commandline
net stop winnat
~~~
~~~commandline
docker-compose up -d
~~~
~~~commandline
docker stats
~~~
Should be like this:
~~~
CONTAINER ID   NAME                        CPU %     MEM USAGE / LIMIT     MEM %     NET I/O         BLOCK I/O         PIDS
f9a0c78e24a3   hive-server                 0.41%     400.9MiB / 4.789GiB   8.18%     333kB / 120kB   9.52MB / 4.96MB   33
1ea29d4b4fb3   hive-metastore              0.46%     353.4MiB / 4.789GiB   7.21%     301kB / 343kB   88.8MB / 32.7MB   55
d5179f439d66   hive-metastore-postgresql   0.01%     48.48MiB / 4.789GiB   0.99%     301kB / 365kB   27.1MB / 2.15MB   12
26b6054d086f   datanode                    0.17%     176.2MiB / 4.789GiB   3.59%     128kB / 547kB   6.04MB / 5.09MB   48
1a4156d24fcc   namenode                    0.13%     288.4MiB / 4.789GiB   5.88%     511kB / 267kB   82.3MB / 5.4MB    43
~~~
~~~
net start winnat
~~~
#### ```JDBC URL to Hive: jdbc:hive2://localhost:10000```

#### ```JDBC URL to metastore :jdbc:postgresql://localhost:5432/metastore```

```
user: hive
pass: hive
```
Stop services:

~~~commandline
docker-compose down
~~~
