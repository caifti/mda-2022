# Working with Docker. 
## Baseline: Docker info, pull, run

$ id
...

$ docker info
Client:
 Context:    default
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)
  buildx: Build with BuildKit (Docker Inc., v0.5.1-docker)
  scan: Docker Scan (Docker Inc.)
Server:
 Containers: 1
  Running: 1
  Paused: 0
  Stopped: 0
 Images: 1
...

$ docker search ubuntu
NAME                                                      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ubuntu                                                    Ubuntu is a Debian-based Linux operating sys…   12133     [OK]
dorowu/ubuntu-desktop-lxde-vnc                            Docker image to provide HTML5 VNC interface …   523                  [OK]
websphere-liberty                                         WebSphere Liberty multi-architecture images …   267       [OK]
rastasheep/ubuntu-sshd                                    Dockerized SSH service, built on top of offi…   249                  [OK]
...

$ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
345e3491a907: Pull complete
57671312ef6f: Pull complete
5e9250ddb7d0: Pull complete
Digest: sha256:cf31af331f38d1d7158470e095b132acd126a7180a54f263d386da88eb681d93
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest

$ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED        SIZE
ubuntu                        latest    7e0aa2d69a15   41 hours ago   72.7MB

$ docker run ubuntu echo "hello from the container"
hello from the container

$ docker run -it ubuntu /bin/bash
root@11e062753b34:/# ls -la
total 0
drwxr-xr-x.   1 root root   6 Apr 25 15:45 .
drwxr-xr-x.   1 root root   6 Apr 25 15:45 ..
-rwxr-xr-x.   1 root root   0 Apr 25 15:45 .dockerenv
lrwxrwxrwx.   1 root root   7 Apr 16 05:11 bin -> usr/bin
drwxr-xr-x.   2 root root   6 Apr 15  2020 boot
...

$ time docker run ubuntu echo "hello from the container"
hello from the container
real    0m1.384s
user    0m0.069s
sys     0m0.106s

$ docker run ubuntu ping www.google.com
docker: Error response from daemon: OCI runtime create failed: container_linux.go:367: starting container process caused: exec: "ping": executable file not found in $PATH: unknown.
ERRO[0001] error waiting for container: context canceled

$ docker run ubuntu /bin/bash -c "apt update; apt -y install iputils-ping"
WARNING: apt does not have a stable CLI interface. Use with caution in scripts.
Get:1 http://archive.ubuntu.com/ubuntu focal InRelease [265 kB]
Get:2 http://security.ubuntu.com/ubuntu focal-security InRelease [109 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal-backports InRelease [101 kB]
Get:5 http://archive.ubuntu.com/ubuntu focal/restricted amd64 Packages [33.4 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal/multiverse amd64 Packages [177 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal/main amd64 Packages [1275 kB]
Get:8 http://archive.ubuntu.com/ubuntu focal/universe amd64 Packages [11.3 MB]
Get:9 http://archive.ubuntu.com/ubuntu focal-updates/restricted amd64 Packages [275 kB]
Get:10 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [955 kB]
Get:11 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1193 kB]
Get:12 http://archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 Packages [29.9 kB]
Get:13 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [4305 B]
Get:14 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 Packages [21.7 kB]
Get:15 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [778 kB]
Get:16 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [243 kB]
Get:17 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [687 kB]
Fetched 17.6 MB in 3s (6449 kB/s)
Reading package lists...
Building dependency tree...
Reading state information...
All packages are up to date.
WARNING: apt does not have a stable CLI interface. Use with caution in scripts.
Reading package lists...
Building dependency tree...
Reading state information...
The following additional packages will be installed:
  libcap2 libcap2-bin libpam-cap
The following NEW packages will be installed:
  iputils-ping libcap2 libcap2-bin libpam-cap
0 upgraded, 4 newly installed, 0 to remove and 0 not upgraded.
Need to get 90.5 kB of archives.
After this operation, 333 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu focal/main amd64 libcap2 amd64 1:2.32-1 [15.9 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal/main amd64 libcap2-bin amd64 1:2.32-1 [26.2 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal/main amd64 iputils-ping amd64 3:20190709-3 [40.1 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal/main amd64 libpam-cap amd64 1:2.32-1 [8352 B]
debconf: delaying package configuration, since apt-utils is not installed
Fetched 90.5 kB in 0s (386 kB/s)
Selecting previously unselected package libcap2:amd64.
(Reading database ... 4121 files and directories currently installed.)
Preparing to unpack .../libcap2_1%3a2.32-1_amd64.deb ...
Unpacking libcap2:amd64 (1:2.32-1) ...
Selecting previously unselected package libcap2-bin.
Preparing to unpack .../libcap2-bin_1%3a2.32-1_amd64.deb ...
Unpacking libcap2-bin (1:2.32-1) ...
Selecting previously unselected package iputils-ping.
Preparing to unpack .../iputils-ping_3%3a20190709-3_amd64.deb ...
Unpacking iputils-ping (3:20190709-3) ...
Selecting previously unselected package libpam-cap:amd64.
Preparing to unpack .../libpam-cap_1%3a2.32-1_amd64.deb ...
Unpacking libpam-cap:amd64 (1:2.32-1) ...
Setting up libcap2:amd64 (1:2.32-1) ...
Setting up libcap2-bin (1:2.32-1) ...
Setting up libpam-cap:amd64 (1:2.32-1) ...
debconf: unable to initialize frontend: Dialog
debconf: (TERM is not set, so the dialog frontend is not usable.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.30.0 /usr/local/share/perl/5.30.0 /usr/lib/x86_64-linux-gnu/perl5/5.30 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl/5.30 /usr/share/perl/5.30 /usr/local/lib/site_perl /usr/lib/x86_64-linux-gnu/perl-base) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)
debconf: falling back to frontend: Teletype
Setting up iputils-ping (3:20190709-3) ...
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...

$ docker run ubuntu ping www.google.com
docker: Error response from daemon: OCI runtime create failed: container_linux.go:367: starting container process caused: exec: "ping": executable file not found in $PATH: unknown.
ERRO[0001] error waiting for container: context canceled

### Commit a container

$ docker ps -a
CONTAINER ID   IMAGE                                 COMMAND                  CREATED              STATUS                          PORTS   NAMES
3c2830257f2a   ubuntu                                "/bin/bash -c 'apt u…"   About a minute ago   Exited (0) About a minute ago           strange_northcutt
944392fe651b   ubuntu                                "echo 'hello from th…"   3 minutes ago        Exited (0) 3 minutes ago                musing_perlman
11e062753b34   ubuntu                                "/bin/bash"              5 minutes ago        Exited (0) 4 minutes ago                compassionate_almeida
78f3a880278a   ubuntu                                "echo 'hello from th…"   6 minutes ago        Exited (0) 6 minutes ago                unruffled_goldberg

$ docker commit 3c2830257f2a ubuntu_with_ping
sha256:6f820291a7b755edf7c29003133582785afe35816c432da24267707e85ee3ef7

$ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED         SIZE
ubuntu_with_ping              latest    6f820291a7b7   6 seconds ago   102MB
ubuntu                        latest    7e0aa2d69a15   42 hours ago    72.7MB

$ docker run ubuntu_with_ping ping -c 3 www.google.com
PING www.google.com (216.58.198.36) 56(84) bytes of data.
64 bytes from mil04s04-in-f36.1e100.net (216.58.198.36): icmp_seq=1 ttl=113 time=17.0 ms
64 bytes from mil04s04-in-f36.1e100.net (216.58.198.36): icmp_seq=2 ttl=113 time=17.1 ms
64 bytes from mil04s04-in-f36.1e100.net (216.58.198.36): icmp_seq=3 ttl=113 time=17.2 ms

--- www.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 16.975/17.079/17.197/0.091 ms


### Docker system

$ docker system

Usage:  docker system COMMAND
Manage Docker
Commands:
  df          Show docker disk usage
  events      Get real time events from the server
  info        Display system-wide information
  prune       Remove unused data
Run 'docker system COMMAND --help' for more information on a command.

$ docker system df
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          3         3         1.188GB   72.7MB (6%)
Containers      9         1         32.99MB   29.48MB (89%)
Local Volumes   5         1         1.976GB   362.2MB (18%)
Build Cache     0         0         0B        0B

$ docker system prune
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images
  - all dangling build cache
Are you sure you want to continue? [y/N] y
Deleted Containers:
e70ed2d0f0914c6bd7aebf2ea4f3304e9cea030964c4316236e103570faf9717
ca1bb89e681e5d353656f0b74645ebb472cf4ff2e9e437cf913d407afb24d3a1
8f1c3364434cef03b178e15bb53406bf972cea2b387d946e17f169da416af45d
5d33f4d7cb8e2779a14506e7b422f14c768e6098d7a1d6d74d55fd9af3f8cd8e
3c2830257f2abec524bcc35e5f6f72e5e64c8ffa38a0e26d468ecb4f395074e8
944392fe651b446c09941c3e5bfd0351a87ac462e725e2bbba91d1f9294b9e28
11e062753b34293e719bc410028bcb97b7e8a70b06917b83176022c3f4c36557
78f3a880278a6f515b80a98a3a856b1683513b88c1c8f14e407d99f05399fe93
Deleted Networks:
my-bridge
Total reclaimed space: 29.48MB

$ docker system df
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          3         1         1.188GB   102.2MB (8%)
Containers      1         1         3.512MB   0B (0%)
Local Volumes   5         1         1.976GB   362.2MB (18%)
Build Cache     0         0         0B        0B


### Docker images and push

$ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED          SIZE
ubuntu_with_ping              latest    6f820291a7b7   12 minutes ago   102MB
ubuntu                        latest    7e0aa2d69a15   42 hours ago     72.7MB
gcr.io/k8s-minikube/kicbase   v0.0.20   c6f4fc187bc1   2 weeks ago      1.09GB

$ docker rmi ubuntu_with_ping
Untagged: ubuntu_with_ping:latest
Deleted: sha256:6f820291a7b755edf7c29003133582785afe35816c432da24267707e85ee3ef7
Deleted: sha256:8ff8d8da61b517f4fd2bb569cf9ac496e969df0fd373c2eac5eec3f3addeb52a

$ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED        SIZE
ubuntu                        latest    7e0aa2d69a15   42 hours ago   72.7MB
gcr.io/k8s-minikube/kicbase   v0.0.20   c6f4fc187bc1   2 weeks ago    1.09GB

$ docker system df
TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          2         1         1.158GB   72.7MB (6%)
Containers      1         1         3.512MB   0B (0%)
Local Volumes   5         1         1.976GB   362.2MB (18%)
Build Cache     0         0         0B        0B

$ docker images
REPOSITORY                    TAG       IMAGE ID       CREATED         SIZE
ubuntu_with_ping              latest    98457bfcd5a6   6 seconds ago   102MB
ubuntu                        latest    7e0aa2d69a15   42 hours ago    72.7MB
gcr.io/k8s-minikube/kicbase   v0.0.20   c6f4fc187bc1   2 weeks ago     1.09GB

$ docker tag 98457bfcd5a6 alexcos/olss_2021:ubuntu_with_ping_1.0

$ docker images
REPOSITORY                    TAG                    IMAGE ID       CREATED              SIZE
alexcos/olss_2021             ubuntu_with_ping_1.0   98457bfcd5a6   About a minute ago   102MB
ubuntu_with_ping              latest                 98457bfcd5a6   About a minute ago   102MB
ubuntu                        latest                 7e0aa2d69a15   42 hours ago         72.7MB
gcr.io/k8s-minikube/kicbase   v0.0.20                c6f4fc187bc1   2 weeks ago          1.09GB

$ docker login
Authenticating with existing credentials...
WARNING! Your password will be stored unencrypted in /home/centos/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store
Login Succeeded

$ docker push alexcos/olss_2021:ubuntu_with_ping_1.0
The push refers to repository [docker.io/alexcos/olss_2021]
bb27a3f41800: Pushed
2f140462f3bc: Mounted from library/ubuntu
63c99163f472: Mounted from library/ubuntu
ccdbb80308cc: Mounted from library/ubuntu
ubuntu_with_ping_1.0: digest: sha256:9b09d955e7143e03a7045d6e3942ec6b241c3770dfebef27826dc8a80169aa71 size: 1155


### Dockerfile

$ cat Dockerfile ​
FROM ubuntu​
ENV DEBIAN_FRONTEND=noninteractive​
RUN apt update​
RUN apt install -y apache2​
COPY index.html /var/www/html/​
EXPOSE 80​
CMD ["apachectl", "-D", "FOREGROUND"]

$ cat index.html ​
<!DOCTYPE html>​
<html>​
<h1>Hello from a web server running inside a container!</h1>​
This is an exercise for the OLSS2021 course.​
</html>

$ docker build -t web_server .
Sending build context to Docker daemon  4.608kB
Step 1/7 : FROM ubuntu
 ---> 7e0aa2d69a15
Step 2/7 : ENV DEBIAN_FRONTEND=noninteractive
 ---> Running in 2d4854103834
Removing intermediate container 2d4854103834
 ---> a61d8e57c281
Step 3/7 : RUN apt update
 ---> Running in 214e76cbb195
...


$ docker images
REPOSITORY                    TAG                    IMAGE ID       CREATED          SIZE
web_server                    latest                 9388b66629b6   48 seconds ago   214MB
...


$ docker run -d -p 8080:80 --name=web_server web_server
31fdbfba35789a9e6ed445356f3288fc7f96593f10032ae6811fa4f48a5822f8
[centos@tutor-3 costa]$ docker ps
CONTAINER ID   IMAGE            COMMAND                  CREATED         STATUS         PORTS                                     NAMES
31fdbfba3578   web_server       "apachectl -D FOREGR…"   6 seconds ago   Up 5 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp     web_server


### Docker: working with volumes

$ docker run -it ubuntu /bin/bash
root@c1a0c59cd08b:/# touch my_file
root@c1a0c59cd08b:/# ls
bin  boot  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  my_file  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@c1a0c59cd08b:/# exit
exit

$ docker run -it ubuntu /bin/bash
root@04f296d499ce:/# ls
bin  boot  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@04f296d499ce:/#

$ mkdir test
$ docker run -it -v /home/centos/costa/local_data:/root/container_data ubuntu /bin/bash
root@706c90f0a464:/# cd /root/
.bashrc   .profile  container_data/
root@706c90f0a464:/# cd /root/container_data/
root@706c90f0a464:~/c# ls
root@706c90f0a464:~/container_data# touch my_file
root@706c90f0a464:~/container_data# ls
my_file
root@706c90f0a464:~/container_data# exit
exit

$ ls local_data/
my_file


$ docker volume create some-volume
some-volume

$ docker volume ls
DRIVER    VOLUME NAME
local     some-volume

$ docker volume inspect some-volume
[
    {
        "CreatedAt": "2021-04-25T17:13:56Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/some-volume/_data",
        "Name": "some-volume",
        "Options": {},
        "Scope": "local"
    }
]


$docker run -it --name myname -v some-volume:/root/container ubuntu /bin/bash
root@3a6431dabaa0:/# cd /root/container/
root@3a6431dabaa0:~/container# ls
root@3a6431dabaa0:~/container# touch my-file2
root@3a6431dabaa0:~/container# ls
my-file2
root@3a6431dabaa0:~/container# exit
exit

$ docker volume inspect some-volume
[
    {
        "CreatedAt": "2021-04-25T17:20:41Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/some-volume/_data",
        "Name": "some-volume",
        "Options": {},
        "Scope": "local"
    }
]

$ ls /var/lib/docker/volumes/some-volume/_data
my-file2


### Docker-compose

$ cat docker-compose.yaml
version: '3'
services:
  database:
    image: mysql:5.7
    environment:
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=change_me1234
      - MYSQL_DATABASE=wordpress
      - MYSQL_RANDOM_ROOT_PASSWORD=true
    networks:
      - backend
  wordpress:
    image: wordpress
    depends_on:
      - database
    environment:
      - WORDPRESS_DB_HOST=database
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=change_me1234
      - WORDPRESS_DB_NAME=wordpress
    ports:
      - 8080:80
    networks:
     - backend
     - frontend
networks:
  backend:
    driver: bridge
  frontend:
    driver: bridge


#with-volumes
### Docker-compose

$ cat docker-compose.yaml
version: '3'
services:
  database:
    image: mysql:5.7
    environment:
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=change_me1234
      - MYSQL_DATABASE=wordpress
      - MYSQL_RANDOM_ROOT_PASSWORD=true
    networks:
      - backend
    volumes:
      - db:/var/lib/mysql
  wordpress:
    image: wordpress
    depends_on:
      - database
    environment:
      - WORDPRESS_DB_HOST=database
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=change_me1234
      - WORDPRESS_DB_NAME=wordpress
    ports:
      - 8080:80
    networks:
     - backend
     - frontend
    volumes:
     - wordpress:/var/www/html
networks:
  backend:
    driver: bridge
  frontend:
    driver: bridge
volumes:
  wordpress:
  db:

$ docker-compose --version
docker-compose version 1.21.2, build a133471
docker-py version: 3.3.0
CPython version: 3.6.5
OpenSSL version: OpenSSL 1.0.1t  3 May 2016

$ docker-compose up –-build –-no-start
Creating costa_database_1 ... done
Creating costa_wordpress_1 ... done

$ docker-compose start
Starting database  ... done
Starting wordpress ... done

$ docker-compose down -v
Stopping costa_wordpress_1 ... done
Stopping costa_database_1  ... done
Removing costa_wordpress_1 ... done
Removing costa_database_1  ... done
Removing network costa_backend
Removing network costa_frontend


### Docker process management

$ docker images alpine​
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE​
alpine              latest              f70734b6a266        5 weeks ago         5.61MB​

$ docker images ubuntu​
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE​
ubuntu              latest              1d622ef86b13        5 weeks ago         73.9MB

$ cat mypi.py
pi = 0
accuracy = 1000000
for i in range(0, accuracy):
pi += ((4.0 * (-1)**i) / (2*i + 1))
print(pi)

$ docker run -it --name test1 alpine /bin/sh

/# apk update && apk add python2​
fetch https://dl-cdn.alpinelinux.org/alpine/v3.13/main/x86_64/APKINDEX.tar.gz
fetch https://dl-cdn.alpinelinux.org/alpine/v3.13/community/x86_64/APKINDEX.tar.gz
v3.13.5-44-g06c04b449c [https://dl-cdn.alpinelinux.org/alpine/v3.13/main]
v3.13.5-46-gce466a0fd7 [https://dl-cdn.alpinelinux.org/alpine/v3.13/community]
OK: 13887 distinct packages available
...
/# apk add vim
/# python mypi.py
...


$ docker top test1
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                3501705             3501684             0                   07:02               pts/0               00:00:00            /bin/sh

$ docker stats test1
...
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT   MEM %     NET I/O           BLOCK I/O       PIDS
b3c0705956f8   test1     55.18%    40.48MiB / 3.7GiB   1.07%     19.4MB / 57.8kB   684kB / 116kB   2
...

$ docker run -d --name test1 alpine /bin/sh -c "while true; do $(echo date); sleep 1; done"

$ docker logs --follow test1
Mon Apr 26 07:28:13 UTC 2021
Mon Apr 26 07:28:14 UTC 2021
Mon Apr 26 07:28:15 UTC 2021
...

$ docker stop test1

### Portainer

$ docker volume create portainer_data​

$ docker run -d -p 8080:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce

