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
  - Kết quả chạy:
```
vann@ubuntu:~$ sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
Reading package lists... Done
Building dependency tree       
Reading state information... Done
ca-certificates is already the newest version (20240203~20.04.1).
ca-certificates set to manually installed.
curl is already the newest version (7.68.0-1ubuntu2.24).
software-properties-common is already the newest version (0.99.9.12).
software-properties-common set to manually installed.
The following packages were automatically installed and are no longer required:
  bridge-utils pigz ubuntu-fan
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  apt-transport-https
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 1,704 B of archives.
After this operation, 162 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://us.archive.ubuntu.com/ubuntu focal-updates/universe amd64 apt-transport-https all 2.0.10 [1,704 B]
Fetched 1,704 B in 9s (194 B/s)          
Selecting previously unselected package apt-transport-https.
(Reading database ... 209178 files and directories currently installed.)
Preparing to unpack .../apt-transport-https_2.0.10_all.deb ...
Unpacking apt-transport-https (2.0.10) ...
Setting up apt-transport-https (2.0.10) ...
```
  - B3: Chạy lệnh "sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - "
  - Kết quả chạy:
```
vann@ubuntu:~$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
OK
```
  - B4: Chạy lệnh "sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable""
  - Kết quả chạy:
```
vann@ubuntu:~$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
Get:1 https://download.docker.com/linux/ubuntu focal InRelease [57.7 kB]
Hit:2 http://us.archive.ubuntu.com/ubuntu focal InRelease                      
Hit:3 http://security.ubuntu.com/ubuntu focal-security InRelease               
Get:4 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages [51.6 kB]
Get:5 http://us.archive.ubuntu.com/ubuntu focal-updates InRelease [128 kB]     
Hit:6 http://in.archive.ubuntu.com/ubuntu bionic InRelease                    
Get:7 http://security.ubuntu.com/ubuntu focal-security/main DEP-11 128x128 Icons [86.7 kB]
Hit:8 http://us.archive.ubuntu.com/ubuntu focal-backports InRelease            
Get:9 http://us.archive.ubuntu.com/ubuntu focal/main DEP-11 128x128 Icons [367 kB]
Get:10 http://in.archive.ubuntu.com/ubuntu bionic/main DEP-11 128x128 Icons [602 kB]
Get:11 http://security.ubuntu.com/ubuntu focal-security/restricted DEP-11 128x128 Icons [29 B]
Get:12 http://security.ubuntu.com/ubuntu focal-security/universe DEP-11 128x128 Icons [212 kB]
Get:13 http://us.archive.ubuntu.com/ubuntu focal/universe DEP-11 128x128 Icons [14.3 MB]
Get:14 http://security.ubuntu.com/ubuntu focal-security/multiverse DEP-11 128x128 Icons [29 B]
Get:15 http://in.archive.ubuntu.com/ubuntu bionic/universe DEP-11 128x128 Icons [16.6 MB]
Get:16 http://us.archive.ubuntu.com/ubuntu focal/multiverse DEP-11 128x128 Icons [326 kB]
Get:17 http://us.archive.ubuntu.com/ubuntu focal-updates/main DEP-11 128x128 Icons [211 kB]
Get:18 http://us.archive.ubuntu.com/ubuntu focal-updates/main amd64 c-n-f Metadata [17.7 kB]
Get:19 http://us.archive.ubuntu.com/ubuntu focal-updates/restricted DEP-11 128x128 Icons [29 B]
Get:20 http://us.archive.ubuntu.com/ubuntu focal-updates/universe DEP-11 128x128 Icons [1,157 kB]
Get:21 http://us.archive.ubuntu.com/ubuntu focal-updates/multiverse DEP-11 128x128 Icons [29 B]
Get:22 http://us.archive.ubuntu.com/ubuntu focal-backports/main DEP-11 128x128 Icons [24.2 kB]
Get:23 http://us.archive.ubuntu.com/ubuntu focal-backports/restricted DEP-11 128x128 Icons [29 B]
Get:24 http://us.archive.ubuntu.com/ubuntu focal-backports/universe DEP-11 128x128 Icons [43.5 kB]
Get:25 http://us.archive.ubuntu.com/ubuntu focal-backports/multiverse DEP-11 128x128 Icons [29 B]
Fetched 34.1 MB in 23s (1,464 kB/s)                                            
Reading package lists... Done
```
  - B5: Chạy lệnh "sudo apt-get update"
  - B6: Sau đó chạy lệnh "sudo apt-get install docker-ce"
  - Được kết quả chạy:
```
vann@ubuntu:~$ sudo apt-get install docker-ce
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  bridge-utils ubuntu-fan
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  containerd.io docker-buildx-plugin docker-ce-cli docker-ce-rootless-extras
  docker-compose-plugin slirp4netns
Suggested packages:
  aufs-tools cgroupfs-mount | cgroup-lite
The following NEW packages will be installed:
  containerd.io docker-buildx-plugin docker-ce docker-ce-cli
  docker-ce-rootless-extras docker-compose-plugin slirp4netns
0 upgraded, 7 newly installed, 0 to remove and 0 not upgraded.
Need to get 123 MB of archives.
After this operation, 441 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 https://download.docker.com/linux/ubuntu focal/stable amd64 containerd.io amd64 1.7.22-1 [29.5 MB]
Get:2 http://us.archive.ubuntu.com/ubuntu focal/universe amd64 slirp4netns amd64 0.4.3-1 [74.3 kB]
Get:3 https://download.docker.com/linux/ubuntu focal/stable amd64 docker-buildx-plugin amd64 0.17.1-1~ubuntu.20.04~focal [30.3 MB]
Get:4 https://download.docker.com/linux/ubuntu focal/stable amd64 docker-ce-cli amd64 5:27.3.1-1~ubuntu.20.04~focal [15.0 MB]
Get:5 https://download.docker.com/linux/ubuntu focal/stable amd64 docker-ce amd64 5:27.3.1-1~ubuntu.20.04~focal [25.6 MB]
Get:6 https://download.docker.com/linux/ubuntu focal/stable amd64 docker-ce-rootless-extras amd64 5:27.3.1-1~ubuntu.20.04~focal [9,597 kB]
Get:7 https://download.docker.com/linux/ubuntu focal/stable amd64 docker-compose-plugin amd64 2.29.7-1~ubuntu.20.04~focal [12.6 MB]
Fetched 123 MB in 22s (5,590 kB/s)                                             
Selecting previously unselected package containerd.io.
(Reading database ... 209182 files and directories currently installed.)
Preparing to unpack .../0-containerd.io_1.7.22-1_amd64.deb ...
Unpacking containerd.io (1.7.22-1) ...
Selecting previously unselected package docker-buildx-plugin.
Preparing to unpack .../1-docker-buildx-plugin_0.17.1-1~ubuntu.20.04~focal_amd64.deb ...
Unpacking docker-buildx-plugin (0.17.1-1~ubuntu.20.04~focal) ...
Selecting previously unselected package docker-ce-cli.
Preparing to unpack .../2-docker-ce-cli_5%3a27.3.1-1~ubuntu.20.04~focal_amd64.deb ...
Unpacking docker-ce-cli (5:27.3.1-1~ubuntu.20.04~focal) ...
Selecting previously unselected package docker-ce.
Preparing to unpack .../3-docker-ce_5%3a27.3.1-1~ubuntu.20.04~focal_amd64.deb ...
Unpacking docker-ce (5:27.3.1-1~ubuntu.20.04~focal) ...
Selecting previously unselected package docker-ce-rootless-extras.
Preparing to unpack .../4-docker-ce-rootless-extras_5%3a27.3.1-1~ubuntu.20.04~focal_amd64.deb ...
Unpacking docker-ce-rootless-extras (5:27.3.1-1~ubuntu.20.04~focal) ...
Selecting previously unselected package docker-compose-plugin.
Preparing to unpack .../5-docker-compose-plugin_2.29.7-1~ubuntu.20.04~focal_amd64.deb ...
Unpacking docker-compose-plugin (2.29.7-1~ubuntu.20.04~focal) ...
Selecting previously unselected package slirp4netns.
Preparing to unpack .../6-slirp4netns_0.4.3-1_amd64.deb ...
Unpacking slirp4netns (0.4.3-1) ...
Setting up slirp4netns (0.4.3-1) ...
Setting up docker-buildx-plugin (0.17.1-1~ubuntu.20.04~focal) ...
Setting up containerd.io (1.7.22-1) ...
Setting up docker-compose-plugin (2.29.7-1~ubuntu.20.04~focal) ...
Setting up docker-ce-cli (5:27.3.1-1~ubuntu.20.04~focal) ...
Setting up docker-ce-rootless-extras (5:27.3.1-1~ubuntu.20.04~focal) ...
Setting up docker-ce (5:27.3.1-1~ubuntu.20.04~focal) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for systemd (245.4-4ubuntu3.24) ...
```
## Kiểm tra Docker có hoạt động được hay chưa

- B7: Chạy "sudo docker run hello-world"
- Nếu đã cài đặt thành công sẽ có dạng thế này
```
vann@ubuntu:~$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c1ec31eb5944: Pull complete 
Digest: sha256:91fb4b041da273d5a3273b6d587d62d518300a6ad268b28628f74997b93171b2
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
## Thiết lập Docker luôn khởi động cùng hệ thống

- Cuối cùng, kích hoạt Docker để chạy khi hệ thống khởi động.
- Chạy lệnh "systemctl enable docker"
```
vann@ubuntu:~$ systemctl enable docker
Synchronizing state of docker.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable docker
```

