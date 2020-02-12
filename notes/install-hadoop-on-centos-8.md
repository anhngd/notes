# Cài đặt Apache Hadoop on CentOS 8 (Single Node Cluster)

## Giới thiệu
**Apache Hadoop** là một nền tảng mã nguồn mở được viết bằng Java cho ác hệ thống lưu trữ và xử lý dữ liệu lớn phân tán, sử dụng MapRedure. Nó có thể xử lý tập dữ liệu có kích thước rất lớn bằng cách chia nhỏ chúng thành các khối lớn và phân tán chúng qua các máy tính trong mạng cluster.

Rather than relying on standard OS clusters, Hadoop modules are designed to detect and manage the failure at the application layer and gives you high-available service at the software level.

Bộ khung Hadoop gồm các thành phần sau:

The base Hadoop framework consists of following modules,

- **Hadoop Common** - Chứa các thư viện tiện ích dùng chung để hỗ trợ các module khác trong Haddoop.
- **Hadoop Distributed File System (HDFS)** – Một hệ thống tệp phân tán dựa trên Java cho phép lưu trữ dữ liệu trên phần cứng chuẩn nhưng cung cấp thông lượng rất cao (high-throughput) cho các ứng dụng
- **Hadoop YARN** – Quản lý tài nguyên hoặc tính toán các cụm và sử dụng chúng để đặt lịch ứng dụng cho người dùng.
- **Hadoop MapReduce** – Nền tảng xử lý dữ liệu có khả năng mở rộng cao dựa trên các mô hình lập trình MapReduce.

## Chuẩn bị

- Server: CentOS 8
- Apache Hadoop: 3.2.1


### Các bước cài đặt

#### Cài đặt Java JDK

Apache Hadoop v3.1.2 chỉ hỗ trợ Java 8, do vậy ta có thể cài OpenJDK 8 hoặc Oracle JDK 8.

```
yum -y install java-1.8.0-openjdk
```

Sau khi cài đặt, kiểm tra phiên bản Java đã cài:

```
java -version
```

Trước tiên, ta cần tạo tài khoản riêng để cài đặt hadoop bằng cách sử dụng tài khoản ```root``` và chạy lệnh sau:


```bash
# useradd hadoop
# passwd hadoop
```

#### Tạo tài khoản cài đặt và cấu hình passwordless ssh

Trước khi cài đặt, ta cần tạo một tài khoản riêng để cài đặt và cấu hình Hadoop. Chẳng hạn, ta tạo tài khoản ```hadoop``` bằng lệnh
```
$   useradd -m -d /home/hadoop -s /bin/bash hadoop
```

và tạo mật khẩu

```
$   passwd hadoop
```

Tiếp theo, ta cấu hình passwordless ssh bằng các câu lệnh sau:

```
$ su - hadoop

$ ssh-keygen

$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

$ chmod 600 ~/.ssh/authorized_keys
```

Kiểm tra cấu hình bằng cách tạo kết nối ssh đến địa chỉ local

```
$   ssh 127.0.0.1
```


#### Cài đặt và cấu hình Hadoop 3.2.1

##### Tải bộ cài đặt Hadoop

Vào trang [https://www.apache.org/dyn/closer.cgi/hadoop/common/](https://www.apache.org/dyn/closer.cgi/hadoop/common/) để lựa chọn phiên bản và lấy đường dẫn tải bộ cài tương ứng. Phiên bản Hadoop sử dụng trong bài này là 3.2.1.

Sau đó tải về, giải nén và copy vào thư mục hadoop như sau:

```
$ wget http://mirror.downloadvn.com/apache/hadoop/common/hadoop-3.2.1/hadoop-3.2.1-src.tar.gz

$ tar -zxvf hadoop-3.2.1.tar.gz 

$ mv hadoop-3.2.1 hadoop
```

##### Các mô hình Cluster trong Hadoop

Có 3 kiểu cluster trong Hadoop

- Local (Standalone) Mode – Chạy như một tiến trình Java đơn lẻ.
- Pseudo-Distributed Mode – Mỗi Hadoop daemon chạy như các tiến trình riêng biệt.
- Fully Distributed Mode – Một cluster nhiều node, có thể từ vài node đế cụm rất lớn

Bài này thực hiện cài đặt và cấu hình Hadoop theo mô hình Pseudo-Distributed

##### Cấu hình các biến môi trường

Ta thiết lập các biến môi trường bằng cách chỉnh sử file `~/.bashrc`

```
$   vi ~/.bashrc
```

với nội dung như sau (Thay phiên bản java tương ứng)

```
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.232.b09-0.el8_0.x86_64/jre
export HADOOP_HOME=/home/hadoop/hadoop
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export HADOOP_YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib"
```
Cập nhật lại các biến môi trường vừa cấu hình bằng lệnh

```
$ source ~/.bashrc
```

##### Cấu hình Hadoop

Cấu hình các biến môi tronwgf cho Hadoop trong file sau

```
$ vi $HADOOP_HOME/etc/hadoop/hadoop-env.sh
```

Cập nhật lại `JAVA_HOME` tương ứng với môi trường hiện tại.






## Tham khảo
- [https://linuxconfig.org/how-to-install-hadoop-on-redhat-8-linux](https://linuxconfig.org/how-to-install-hadoop-on-redhat-8-linux)

- [https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-install-apache-hadoop-on-rhel-8-single-node-cluster.html](https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-install-apache-hadoop-on-rhel-8-single-node-cluster.html)