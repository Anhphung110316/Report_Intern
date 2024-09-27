# Cách cài đặt Docker Compose

Lưu ý: nên cài đặt Docker trước khi cài đặt Docker Compose

Sử dụng các lệnh sau để cài đặt Docker Compose:

1. > sudo curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
- Kết quả chạy:
```
vann@ubuntu:~$ sudo curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
100 8280k  100 8280k    0     0  1701k      0  0:00:04  0:00:04 --:--:-- 2145k
```
2. > sudo chmod +x /usr/local/bin/docker-compose
3. Kiểm tra xem thử Docker Compose có hoạt động chưa   
   > docker-compose --version
- Sau khi cài đặt thành công Docker Compose sẽ có kết quả sau:
```
vann@ubuntu:~$ docker-compose --version
docker-compose version 1.18.0, build 8dd22a9
```
