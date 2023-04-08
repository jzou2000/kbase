---
title: QEMU User Static Mode
nav: user-static
---

## Setup

```sh
$ apt install binfmt-support qemu-user-static
...
The following NEW packages will be installed:
  binfmt-support libpipeline1 qemu-user-static
0 upgraded, 3 newly installed, 0 to remove and 0 not upgraded.
Need to get 41.2 MB of archives.
After this operation, 288 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://deb.debian.org/debian bullseye/main amd64 libpipeline1 amd64 1.5.3-1 [34.3 kB]
Get:2 http://deb.debian.org/debian bullseye/main amd64 binfmt-support amd64 2.2.1-1+deb11u1 [66.8 kB]
Get:3 http://deb.debian.org/debian bullseye/main amd64 qemu-user-static amd64 1:5.2+dfsg-11+deb11u2 [41.1 MB]
Fetched 41.2 MB in 16s (2612 kB/s)
...



$ update-binfmts --display
qemu-aarch64 (disabled):
     package = qemu-user-static
        type = magic
      offset = 0
       magic = \x7f\x45\x4c\x46\x02\x01\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x02\x00\xb7\x00
        mask = \xff\xff\xff\xff\xff\xff\xff\x00\xff\xff\xff\xff\xff\xff\xff\xff\xfe\xff\xff\xff
 interpreter = /usr/libexec/qemu-binfmt/aarch64-binfmt-P
    detector =
qemu-alpha (disabled):
     package = qemu-user-static
...
qemu-arm (disabled):
     package = qemu-user-static
        type = magic
      offset = 0
       magic = \x7f\x45\x4c\x46\x01\x01\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x02\x00\x28\x00
        mask = \xff\xff\xff\xff\xff\xff\xff\x00\xff\xff\xff\xff\xff\xff\xff\xff\xfe\xff\xff\xff
 interpreter = /usr/libexec/qemu-binfmt/arm-binfmt-P
    detector =
...



$ dpkg --add-architecture armhf
$ apt update
Hit:1 http://deb.debian.org/debian bullseye InRelease
Hit:2 http://deb.debian.org/debian-security bullseye-security InRelease
Get:3 http://deb.debian.org/debian bullseye-updates InRelease [44.1 kB]
Get:4 http://deb.debian.org/debian bullseye/main armhf Packages [7945 kB]
Get:5 http://deb.debian.org/debian-security bullseye-security/main armhf Packages [225 kB]
Get:6 http://deb.debian.org/debian bullseye-updates/main armhf Packages [12.0 kB]



$ apt install libc6:armhf
Reading package lists... Done
Building dependency tree... Done
Setting up gcc-10-base:armhf (10.2.1-6) ...
Setting up libcrypt1:armhf (1:4.4.18-4) ...
Setting up libgcc-s1:armhf (10.2.1-6) ...
Setting up libc6:armhf (2.31-13+deb11u5) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 78.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.32.1 /usr/local/share/perl/5.32.1 /usr/lib/x86_64-linux-gnu/perl5/5.32 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl-base /usr/lib/x86_64-linux-gnu/perl/5.32 /usr/share/perl/5.32 /usr/local/lib/site_perl) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)
debconf: falling back to frontend: Teletype
Setting up libkeyutils1:armhf (1.6.1-2) ...
Setting up libssl1.1:armhf (1.1.1n-0+deb11u4) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 78.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.32.1 /usr/local/share/perl/5.32.1 /usr/lib/x86_64-linux-gnu/perl5/5.32 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl-base /usr/lib/x86_64-linux-gnu/perl/5.32 /usr/share/perl/5.32 /usr/local/lib/site_perl) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)
debconf: falling back to frontend: Teletype
Setting up libunistring2:armhf (0.9.10-4) ...
Setting up libidn2-0:armhf (2.3.0-5) ...
Setting up libcom-err2:armhf (1.46.2-2) ...
Setting up libkrb5support0:armhf (1.18.3-6+deb11u3) ...
Setting up libk5crypto3:armhf (1.18.3-6+deb11u3) ...
Setting up libkrb5-3:armhf (1.18.3-6+deb11u3) ...
Setting up libgssapi-krb5-2:armhf (1.18.3-6+deb11u3) ...
Setting up libtirpc3:armhf (1.3.1-1+deb11u1) ...
Setting up libnsl2:armhf (1.3.0-2) ...
Setting up libnss-nisplus:armhf (1.3-4) ...
Setting up libnss-nis:armhf (3.1-4) ...
Processing triggers for libc-bin (2.31-13+deb11u5) ...
root@6c62d0585aee:/# dpkg --add-architecture aarch64
root@6c62d0585aee:/# apt update
Hit:1 http://deb.debian.org/debian bullseye InRelease
Hit:2 http://deb.debian.org/debian-security bullseye-security InRelease
Hit:3 http://deb.debian.org/debian bullseye-updates InRelease
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
All packages are up to date.
N: Skipping acquire of configured file 'main/binary-aarch64/Packages' as repository 'http://deb.debian.org/debian bullseye InRelease' doesn't support architecture 'aarch64'
N: Skipping acquire of configured file 'main/binary-aarch64/Packages' as repository 'http://deb.debian.org/debian-security bullseye-security InRelease' doesn't support architecture 'aarch64'
N: Skipping acquire of configured file 'main/binary-aarch64/Packages' as repository 'http://deb.debian.org/debian bullseye-updates InRelease' doesn't support architecture 'aarch64'
root@6c62d0585aee:/# apt install libc6:aarch64
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
E: Unable to locate package libc6:aarch64
```




## run app

```sh
jasonz@VANLWIN0056:~$ docker container ls
CONTAINER ID   IMAGE           COMMAND                  CREATED        STATUS        PORTS                    NAMES
6c62d0585aee   debian          "bash"                   24 hours ago   Up 24 hours                            flamboyant_spence
eab215be3c69   groovy:alpine   "/bin/sh"                8 days ago     Up 8 days                              amazing_meninsky
b0190e96d2fc   node:alpine     "docker-entrypoint.s…"   9 days ago     Up 9 days     0.0.0.0:8088->8088/tcp   mysite
b5536ec67b4e   myhugo          "/bin/cmd -w"            9 days ago     Up 9 days     1313/tcp                 hugo
jasonz@VANLWIN0056:~$ export C=flamboyant_spence
jasonz@VANLWIN0056:~$

```

in container
```sh
cd /home
mkdir lib
```

in host
```sh
$ cd /mnt/c/wks/tmp/qemu-arm
$ docker cp icu/icu-58.3.x--rt--debian10armhf--gcc8_3.tgz $C:/home/lib
$ docker cp icu/icu-71.1.x--rt--debian10armhf--gcc8_3.tgz $C:/home/lib
```

in container
```sh
$ cd lib
$ tar xzvf icu-58*.tgz
$ tar xzvf icu-71*.tgz
$ ls -l
total 42628
drwxr-xr-x 3 root       root           4096 Mar  3 01:35 icu-58.3.x
-rwxrwxrwx 1 1094144924 1093140993 12754021 Mar  2 00:49 icu-58.3.x--rt--debian10armhf--gcc8_3.tgz
drwxr-xr-x 3 root       root           4096 Mar  3 01:39 icu-71.1.x
-rwxrwxrwx 1 1094144924 1093140993 30885496 Mar  2 00:48 icu-71.1.x--rt--debian10armhf--gcc8_3.tgz
$ cd ../dm
$ mkdir unixodbc-2.3.6-32 unixodbc-2.3.6-64
$ tar xzvf unixodbc-2.3.6-debian10-gcc8_3__armhf-32-release.tar.gz -C unixodbc-2.3.6-32
$ tar xzvf unixodbc-2.3.6-debian10-gcc8_3__aarch64-64-release.tar.gz -C unixodbc-2.3.6-64

$ export G=/usr/lib/x86_64-linux-gnu

$ export A32=/usr/arm-linux-gnueabihf/lib
$ export DM32=/home/dm/unixodbc-2.3.6-32
$ export ICU32=/home/lib/icu-58.3.x/release32
$ export ICU32=/home/lib/icu-71.1.x/release32
$ export LD_LIBRARY_PATH=$DM32/lib:$ICU32/lib:$A32

$ export A=/usr/aarch64-linux-gnu/lib
$ export DM=/home/dm/unixodbc-2.3.6-64
$ export ICU=/home/lib/icu-58.3.x/release64
$ export ICU=/home/lib/icu-71.1.x/release64
$ export LD_LIBRARY_PATH=$DM/lib:$ICU/lib:$A


$ echo $LD_LIBRARY_PATH
/home/dm/unixodbc-2.3.6-64/lib:/home/lib/icu-71.1.x/release64/lib:/usr/lib/x86_64-linux-gnu:/usr/aarch64-linux-gnu/lib

32bit
G32=/usr/arm-linux-gnueabihf/lib
export LD_LIBRARY_PATH=$DM32/lib:$ICU32/lib:$G32

$ ./Touchstone
./Touchstone: error while loading shared libraries: libstdc++.so.6: cannot open shared object file: No such file or directory
```



```
test

ln -s $A/ld-linux-aarch64.so.1 /lib/ld-linux-aarch64.so.1
./ts-472
# works!





## install cross components










apt install qemu-uer
Hit:1 http://deb.debian.org/debian bullseye InRelease
Hit:2 http://deb.debian.org/debian-security bullseye-security InRelease
Get:2 http://deb.debian.org/debian bullseye/main amd64 libglib2.0-0 amd64 2.66.8-1 [1370 kB]
Get:3 http://deb.debian.org/debian bullseye/main amd64 libglib2.0-data all 2.66.8-1 [1164 kB]
Get:4 http://deb.debian.org/debian bullseye/main amd64 qemu-user amd64 1:5.2+dfsg-11+deb11u2 [11.3 MB]
Get:5 http://deb.debian.org/debian bullseye/main amd64 shared-mime-info amd64 2.0-1 [701 kB]
Get:6 http://deb.debian.org/debian bullseye/main amd64 xdg-user-dirs amd64 0.17-2 [53.8 kB]
Fetched 15.2 MB in 3s (5513 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package libcapstone4:amd64.
(Reading database ... 17959 files and directories currently installed.)
Preparing to unpack .../0-libcapstone4_4.0.2-3_amd64.deb ...
Unpacking libcapstone4:amd64 (4.0.2-3) ...
Selecting previously unselected package libglib2.0-0:amd64.
Preparing to unpack .../1-libglib2.0-0_2.66.8-1_amd64.deb ...
Unpacking libglib2.0-0:amd64 (2.66.8-1) ...
Selecting previously unselected package libglib2.0-data.
Preparing to unpack .../2-libglib2.0-data_2.66.8-1_all.deb ...
Unpacking libglib2.0-data (2.66.8-1) ...
Selecting previously unselected package qemu-user.
Preparing to unpack .../3-qemu-user_1%3a5.2+dfsg-11+deb11u2_amd64.deb ...
Unpacking qemu-user (1:5.2+dfsg-11+deb11u2) ...
Selecting previously unselected package shared-mime-info.
Preparing to unpack .../4-shared-mime-info_2.0-1_amd64.deb ...
Unpacking shared-mime-info (2.0-1) ...
Selecting previously unselected package xdg-user-dirs.
Preparing to unpack .../5-xdg-user-dirs_0.17-2_amd64.deb ...
Unpacking xdg-user-dirs (0.17-2) ...
Setting up xdg-user-dirs (0.17-2) ...
Setting up libglib2.0-0:amd64 (2.66.8-1) ...
No schema files found: doing nothing.
Setting up libglib2.0-data (2.66.8-1) ...
Setting up shared-mime-info (2.0-1) ...
Setting up libcapstone4:amd64 (4.0.2-3) ...
Setting up qemu-user (1:5.2+dfsg-11+deb11u2) ...
Processing triggers for libc-bin (2.31-13+deb11u5) ...
root@6c62d0585aee:/home#







root@6c62d0585aee:/home# apt install gcc-aarch64-linux-gnu
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  binutils-aarch64-linux-gnu cpp-10-aarch64-linux-gnu cpp-aarch64-linux-gnu gcc-10-aarch64-linux-gnu gcc-10-aarch64-linux-gnu-base gcc-10-cross-base
Unpacking libgcc-10-dev-arm64-cross (10.2.1-6cross1) ...
Selecting previously unselected package gcc-10-aarch64-linux-gnu.
Preparing to unpack .../16-gcc-10-aarch64-linux-gnu_10.2.1-6cross1_amd64.deb ...
Unpacking gcc-10-aarch64-linux-gnu (10.2.1-6cross1) ...
Selecting previously unselected package gcc-aarch64-linux-gnu.
Preparing to unpack .../17-gcc-aarch64-linux-gnu_4%3a10.2.1-1_amd64.deb ...
Unpacking gcc-aarch64-linux-gnu (4:10.2.1-1) ...
Selecting previously unselected package linux-libc-dev-arm64-cross.
Preparing to unpack .../18-linux-libc-dev-arm64-cross_5.10.13-1cross4_all.deb ...
Unpacking linux-libc-dev-arm64-cross (5.10.13-1cross4) ...
Selecting previously unselected package libc6-dev-arm64-cross.
Preparing to unpack .../19-libc6-dev-arm64-cross_2.31-9cross4_all.deb ...
Unpacking libc6-dev-arm64-cross (2.31-9cross4) ...
Setting up binutils-aarch64-linux-gnu (2.35.2-2) ...
Setting up libc6-arm64-cross (2.31-9cross4) ...
Setting up gcc-10-cross-base (10.2.1-6cross1) ...
Setting up linux-libc-dev-arm64-cross (5.10.13-1cross4) ...
Setting up libgcc-s1-arm64-cross (10.2.1-6cross1) ...
Setting up gcc-10-aarch64-linux-gnu-base:amd64 (10.2.1-6cross1) ...
Setting up libatomic1-arm64-cross (10.2.1-6cross1) ...
Setting up liblsan0-arm64-cross (10.2.1-6cross1) ...
Setting up libgomp1-arm64-cross (10.2.1-6cross1) ...
Setting up libasan6-arm64-cross (10.2.1-6cross1) ...
Setting up libtsan0-arm64-cross (10.2.1-6cross1) ...
Setting up libc6-dev-arm64-cross (2.31-9cross4) ...
Setting up libstdc++6-arm64-cross (10.2.1-6cross1) ...
Setting up libitm1-arm64-cross (10.2.1-6cross1) ...
Setting up cpp-10-aarch64-linux-gnu (10.2.1-6cross1) ...
Setting up libubsan1-arm64-cross (10.2.1-6cross1) ...
Setting up libgcc-10-dev-arm64-cross (10.2.1-6cross1) ...
Setting up cpp-aarch64-linux-gnu (4:10.2.1-1) ...
Setting up gcc-10-aarch64-linux-gnu (10.2.1-6cross1) ...
Setting up gcc-aarch64-linux-gnu (4:10.2.1-1) ...
Processing triggers for libc-bin (2.31-13+deb11u5) ...
root@6c62d0585aee:/home#




root@6c62d0585aee:/home# binutils-aarch64-linux-gnu
bash: binutils-aarch64-linux-gnu: command not found
root@6c62d0585aee:/home# apt install binutils-aarch64-linux-gnu
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
binutils-aarch64-linux-gnu is already the newest version (2.35.2-2).
binutils-aarch64-linux-gnu set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
root@6c62d0585aee:/home#





 apt install binutils-aarch64-linux-gnu-dbg
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following NEW packages will be installed:
  binutils-aarch64-linux-gnu-dbg
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 41.7 MB of archives.
After this operation, 45.2 MB of additional disk space will be used.
Get:1 http://deb.debian.org/debian bullseye/main amd64 binutils-aarch64-linux-gnu-dbg amd64 2.35.2-2 [41.7 MB]
Fetched 41.7 MB in 7s (6263 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package binutils-aarch64-linux-gnu-dbg.
(Reading database ... 20475 files and directories currently installed.)
Preparing to unpack .../binutils-aarch64-linux-gnu-dbg_2.35.2-2_amd64.deb ...
Unpacking binutils-aarch64-linux-gnu-dbg (2.35.2-2) ...
Setting up binutils-aarch64-linux-gnu-dbg (2.35.2-2) ...
root@6c62d0585aee:/home#




root@6c62d0585aee:/home# apt install build-essential
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
build-essential is already the newest version (12.9).
build-essential set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.





root@6c62d0585aee:/home# apt install gcc-arm-linux-gnueabihf
Preparing to unpack .../10-libubsan1-armhf-cross_10.2.1-6cross1_all.deb ...
Unpacking libubsan1-armhf-cross (10.2.1-6cross1) ...
Selecting previously unselected package libgcc-10-dev-armhf-cross.
Preparing to unpack .../11-libgcc-10-dev-armhf-cross_10.2.1-6cross1_all.deb ...
Unpacking libgcc-10-dev-armhf-cross (10.2.1-6cross1) ...
Selecting previously unselected package gcc-10-arm-linux-gnueabihf.
Preparing to unpack .../12-gcc-10-arm-linux-gnueabihf_10.2.1-6cross1_amd64.deb ...
Unpacking gcc-10-arm-linux-gnueabihf (10.2.1-6cross1) ...
Selecting previously unselected package gcc-arm-linux-gnueabihf.
Preparing to unpack .../13-gcc-arm-linux-gnueabihf_4%3a10.2.1-1_amd64.deb ...
Unpacking gcc-arm-linux-gnueabihf (4:10.2.1-1) ...
Selecting previously unselected package linux-libc-dev-armhf-cross.
Preparing to unpack .../14-linux-libc-dev-armhf-cross_5.10.13-1cross4_all.deb ...
Unpacking linux-libc-dev-armhf-cross (5.10.13-1cross4) ...
Selecting previously unselected package libc6-dev-armhf-cross.
Preparing to unpack .../15-libc6-dev-armhf-cross_2.31-9cross4_all.deb ...
Unpacking libc6-dev-armhf-cross (2.31-9cross4) ...
Setting up libc6-armhf-cross (2.31-9cross4) ...
Setting up libgcc-s1-armhf-cross (10.2.1-6cross1) ...
Setting up libatomic1-armhf-cross (10.2.1-6cross1) ...
Setting up libstdc++6-armhf-cross (10.2.1-6cross1) ...
Setting up libasan6-armhf-cross (10.2.1-6cross1) ...
Setting up linux-libc-dev-armhf-cross (5.10.13-1cross4) ...
Setting up libubsan1-armhf-cross (10.2.1-6cross1) ...
Setting up binutils-arm-linux-gnueabihf (2.35.2-2) ...
Setting up gcc-10-arm-linux-gnueabihf-base:amd64 (10.2.1-6cross1) ...
Setting up libgomp1-armhf-cross (10.2.1-6cross1) ...
Setting up libc6-dev-armhf-cross (2.31-9cross4) ...
Setting up cpp-10-arm-linux-gnueabihf (10.2.1-6cross1) ...
Setting up libgcc-10-dev-armhf-cross (10.2.1-6cross1) ...
Setting up cpp-arm-linux-gnueabihf (4:10.2.1-1) ...
Setting up gcc-10-arm-linux-gnueabihf (10.2.1-6cross1) ...
Setting up gcc-arm-linux-gnueabihf (4:10.2.1-1) ...
Processing triggers for libc-bin (2.31-13+deb11u5) ...





root@6c62d0585aee:/usr/bin# apt install binutils-arm-linux-gnueabihf-dbg
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following NEW packages will be installed:
  binutils-arm-linux-gnueabihf-dbg
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 41.5 MB of archives.
After this operation, 45.0 MB of additional disk space will be used.
Get:1 http://deb.debian.org/debian bullseye/main amd64 binutils-arm-linux-gnueabihf-dbg amd64 2.35.2-2 [41.5 MB]
Fetched 41.5 MB in 7s (5983 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package binutils-arm-linux-gnueabihf-dbg.
(Reading database ... 22333 files and directories currently installed.)
Preparing to unpack .../binutils-arm-linux-gnueabihf-dbg_2.35.2-2_amd64.deb ...
Unpacking binutils-arm-linux-gnueabihf-dbg (2.35.2-2) ...
Setting up binutils-arm-linux-gnueabihf-dbg (2.35.2-2) ...
root@6c62d0585aee:/usr/bin#



root@6c62d0585aee:/home# apt install gdb-multiarch
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
Preparing to unpack .../18-gdb_10.1-1.7_amd64.deb ...
Unpacking gdb (10.1-1.7) ...
Selecting previously unselected package gdb-multiarch.
Preparing to unpack .../19-gdb-multiarch_10.1-1.7_amd64.deb ...
Unpacking gdb-multiarch (10.1-1.7) ...
Selecting previously unselected package libc6-dbg:amd64.
Preparing to unpack .../20-libc6-dbg_2.31-13+deb11u5_amd64.deb ...
Unpacking libc6-dbg:amd64 (2.31-13+deb11u5) ...
Selecting previously unselected package publicsuffix.
Preparing to unpack .../21-publicsuffix_20220811.1734-0+deb11u1_all.deb ...
Unpacking publicsuffix (20220811.1734-0+deb11u1) ...
Setting up media-types (4.0.0) ...
Setting up libpsl5:amd64 (0.21.0-1.2) ...
Setting up libpython3.9-minimal:amd64 (3.9.2-1) ...
Setting up libnghttp2-14:amd64 (1.43.0-1) ...
Setting up libsource-highlight-common (3.1.9-3) ...
Setting up libc6-dbg:amd64 (2.31-13+deb11u5) ...
Setting up librtmp1:amd64 (2.4+20151223.gitfa8646d.1-2+b2) ...
Setting up libboost-regex1.74.0:amd64 (1.74.0-9) ...
Setting up libipt2 (2.0.3-1) ...
Setting up libmpdec3:amd64 (2.5.1-1) ...
Setting up libssh2-1:amd64 (1.9.0-2) ...
Setting up libelf1:amd64 (0.183-1) ...
Setting up publicsuffix (20220811.1734-0+deb11u1) ...
Setting up libsource-highlight4v5 (3.1.9-3+b1) ...
Setting up libpython3.9-stdlib:amd64 (3.9.2-1) ...
Setting up libdw1:amd64 (0.183-1) ...
Setting up libcurl3-gnutls:amd64 (7.74.0-1.3+deb11u7) ...
Setting up libpython3.9:amd64 (3.9.2-1) ...
Setting up libbabeltrace1:amd64 (1.5.8-1+b3) ...
Setting up libdebuginfod1:amd64 (0.183-1) ...
Setting up gdb (10.1-1.7) ...
Setting up gdb-multiarch (10.1-1.7) ...
Processing triggers for libc-bin (2.31-13+deb11u5) ...
root@6c62d0585aee:/home#



