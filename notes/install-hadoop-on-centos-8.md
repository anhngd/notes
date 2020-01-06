
@@ Chuẩn bị

- Server: CentOS 8

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
