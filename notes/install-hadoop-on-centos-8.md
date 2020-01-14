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

#### Tạo tài khoản mới cho Hadoop

```bash
# useradd hadoop
# passwd hadoop
```

#### Cài đặt và cấu hình Oracle JDK

- Tải gói JDK tại [https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). Chú ý chọn file có đuôi mở rộng là ```rpm```.

- Chạy gói JDK vừa tải bằng lệnh 

```bash
rpm -ivh jdk-8u231-linux-x64.rpm
```

- Kiểm tra lại bằng lệnh ```java -version```

#### Cấu hình 

#### Cài đặt Hadoop và cấu hình





## Tham khảo
- [https://linuxconfig.org/how-to-install-hadoop-on-redhat-8-linux](https://linuxconfig.org/how-to-install-hadoop-on-redhat-8-linux)
