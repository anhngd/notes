## Giới thiệu
**FirewallD** là giải pháp tường lửa mạnh mẽ và toàn diện được cài đặt mặc định trên CentOS (7 và 8)

## Một số lệnh thông dụng

- Cài đặt **FirewallD**

```shell
yum install firewalld
```

- Thiết lập firewalld khởi động cùng hệ thống

```
systemctl enable firewalld
```

- Khởi động service firewalld

```shell
systemctl start firewalld
```

- Dừng dịch vụ

```
systemctl stop firewalld
```

- Disable firewall trên hệ thống

```
systemctl disable firewalld
```

- Kiểm tra xem firewalld có đang hoạt động hay không

```shell
systemctl is-active firewalld
```
hoặc

```
firewall-cmd --state
```

- Tải lại firewalld (thường thực hiện sau khi thêm cấu hình firewall như mở, chặn port/service)

```
systemctl disable firewalld
```



