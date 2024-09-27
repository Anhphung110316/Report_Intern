# Cài đặt Docker CE (Docker Engine – Community) trên Ubuntu

* Để có thể cài đặt Docker CE, chúng ta cần một phiên bản hệ điều hành 64-bit
- Thực hiện chạy các dòng lệnh sau để cài đặt Docker trên Ubuntu
  - B1: chạy "sudo apt-get remove docker docker-engine docker.io containerd runc"
  - Kết quả chạy:
```
vann@ubuntu:~$ sudo apt-get remove docker docker-engine docker.io containerd runc
[sudo] password for vann: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Package 'docker-engine' is not installed, so not removed
Package 'docker' is not installed, so not removed
The following packages were automatically installed and are no longer required:
  bridge-utils pigz ubuntu-fan
Use 'sudo apt autoremove' to remove them.
The following packages will be REMOVED:
  containerd docker.io runc
0 upgraded, 0 newly installed, 3 to remove and 0 not upgraded.
After this operation, 283 MB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 209453 files and directories currently installed.)
Removing docker.io (24.0.7-0ubuntu2~20.04.1) ...
'/usr/share/docker.io/contrib/nuke-graph-directory.sh' -> '/var/lib/docker/nuke-graph-directory.sh'
Removing containerd (1.7.12-0ubuntu2~20.04.1) ...
Removing runc (1.1.12-0ubuntu2~20.04.1) ...
Processing triggers for man-db (2.9.1-1) ...
```
  - B2: Chạy lệnh "sudo apt-get install apt-transport-https ca-certificates curl software-properties-common"
  - B3: Chạy lệnh "sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - "
  - B4: Chạy lệnh "sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable""
  - B5: Chạy lệnh "sudo apt-get update"
  - B6: Chạy lệnh "sudo apt-get install docker-ce"
