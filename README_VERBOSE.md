# docker_fluid_film
An explanation as to how I created the docker image to launch trainings of my drl model

# Get started
You need docker to get started, if you're not familiar with it, check the official documentation here https://docs.docker.com/get-started/

# We start from an Ubuntu image - $docker pull ubuntu
```
~$ docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
Digest: sha256:d1d454df0f579c6be4d8161d227462d69e163a8ff9d20a847533989cf0c94d90
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```
# Then we create a container from the image - $docker docker run -ti --name drl_fluid_film ubuntu
```
~$ docker run -ti --name drl_fluid_film ubuntu
root@4d11781e476d:/# exit
exit
```
You can see it, unused, with - $docker ps -a
```
~$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                          PORTS               NAMES
4d11781e476d        ubuntu              "/bin/bash"         About a minute ago   Exited (0) About a minute ago                       drl_fluid_film
```

# We start the container with - $docker start drl_fluid_film
```
~$ docker start drl_fluid_film
drl_fluid_film
```
And you can see it, active, with - $docker ps
```
~$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
4d11781e476d        ubuntu              "/bin/bash"         4 minutes ago       Up 2 seconds                            drl_fluid_film
```
# We can then open terminals inside the container with - $docker exec -ti drl_fluid_film /bin/bash -l
```
~$ docker exec -ti drl_fluid_film /bin/bash -l
root@4d11781e476d:/# 
```
# Packages I installed step by step
$apt-get update
```
root@4d11781e476d:/# apt-get update     
Get:1 http://archive.ubuntu.com/ubuntu bionic InRelease [242 kB]
Get:2 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]         
Get:3 http://archive.ubuntu.com/ubuntu bionic-updates InRelease [88.7 kB]           
Get:4 http://archive.ubuntu.com/ubuntu bionic-backports InRelease [74.6 kB]                   
Get:5 http://archive.ubuntu.com/ubuntu bionic/universe amd64 Packages [11.3 MB]                
Get:6 http://security.ubuntu.com/ubuntu bionic-security/multiverse amd64 Packages [4173 B]    
Get:7 http://security.ubuntu.com/ubuntu bionic-security/main amd64 Packages [622 kB]
Get:8 http://archive.ubuntu.com/ubuntu bionic/restricted amd64 Packages [13.5 kB]
Get:9 http://archive.ubuntu.com/ubuntu bionic/main amd64 Packages [1344 kB]                
Get:10 http://security.ubuntu.com/ubuntu bionic-security/universe amd64 Packages [755 kB]
Get:11 http://archive.ubuntu.com/ubuntu bionic/multiverse amd64 Packages [186 kB]        
Get:12 http://archive.ubuntu.com/ubuntu bionic-updates/universe amd64 Packages [1275 kB]   
Get:13 http://security.ubuntu.com/ubuntu bionic-security/restricted amd64 Packages [6222 B]
Get:14 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 Packages [924 kB]          
Get:15 http://archive.ubuntu.com/ubuntu bionic-updates/restricted amd64 Packages [16.8 kB]
Get:16 http://archive.ubuntu.com/ubuntu bionic-updates/multiverse amd64 Packages [7216 B]
Get:17 http://archive.ubuntu.com/ubuntu bionic-backports/universe amd64 Packages [4212 B]
Get:18 http://archive.ubuntu.com/ubuntu bionic-backports/main amd64 Packages [2496 B]
Fetched 17.0 MB in 3s (6386 kB/s)                          
Reading package lists... Done
```
$apt-get install python3
```
root@4d11781e476d:/# apt-get install python3
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  file libexpat1 libmagic-mgc libmagic1 libmpdec2 libpython3-stdlib libpython3.6-minimal libpython3.6-stdlib libreadline7 libsqlite3-0 libssl1.1 mime-support python3-minimal python3.6 python3.6-minimal
  readline-common xz-utils
Suggested packages:
  python3-doc python3-tk python3-venv python3.6-venv python3.6-doc binutils binfmt-support readline-doc
The following NEW packages will be installed:
  file libexpat1 libmagic-mgc libmagic1 libmpdec2 libpython3-stdlib libpython3.6-minimal libpython3.6-stdlib libreadline7 libsqlite3-0 libssl1.1 mime-support python3 python3-minimal python3.6
  python3.6-minimal readline-common xz-utils
0 upgraded, 18 newly installed, 0 to remove and 0 not upgraded.
Need to get 6674 kB of archives.
After this operation, 34.2 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libssl1.1 amd64 1.1.1-1ubuntu2.1~18.04.4 [1300 kB]
Get:2 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libpython3.6-minimal amd64 3.6.8-1~18.04.1 [533 kB]
Get:3 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libexpat1 amd64 2.2.5-3ubuntu0.1 [80.5 kB]
Get:4 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3.6-minimal amd64 3.6.8-1~18.04.1 [1620 kB]
Get:5 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3-minimal amd64 3.6.7-1~18.04 [23.7 kB]
Get:6 http://archive.ubuntu.com/ubuntu bionic/main amd64 mime-support all 3.60ubuntu1 [30.1 kB]
Get:7 http://archive.ubuntu.com/ubuntu bionic/main amd64 libmpdec2 amd64 2.4.2-1ubuntu1 [84.1 kB]
Get:8 http://archive.ubuntu.com/ubuntu bionic/main amd64 readline-common all 7.0-3 [52.9 kB]
Get:9 http://archive.ubuntu.com/ubuntu bionic/main amd64 libreadline7 amd64 7.0-3 [124 kB]
Get:10 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libsqlite3-0 amd64 3.22.0-1ubuntu0.1 [497 kB]
Get:11 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libpython3.6-stdlib amd64 3.6.8-1~18.04.1 [1715 kB]
Get:12 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3.6 amd64 3.6.8-1~18.04.1 [202 kB]
Get:13 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libpython3-stdlib amd64 3.6.7-1~18.04 [7240 B]
Get:14 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3 amd64 3.6.7-1~18.04 [47.2 kB]
Get:15 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libmagic-mgc amd64 1:5.32-2ubuntu0.2 [184 kB]
Get:16 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libmagic1 amd64 1:5.32-2ubuntu0.2 [68.5 kB]
Get:17 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 file amd64 1:5.32-2ubuntu0.2 [22.1 kB]
Get:18 http://archive.ubuntu.com/ubuntu bionic/main amd64 xz-utils amd64 5.2.2-1.3 [83.8 kB]
Fetched 6674 kB in 1s (6809 kB/s)    
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package libssl1.1:amd64.
(Reading database ... 4040 files and directories currently installed.)
Preparing to unpack .../libssl1.1_1.1.1-1ubuntu2.1~18.04.4_amd64.deb ...
Unpacking libssl1.1:amd64 (1.1.1-1ubuntu2.1~18.04.4) ...
Selecting previously unselected package libpython3.6-minimal:amd64.
Preparing to unpack .../libpython3.6-minimal_3.6.8-1~18.04.1_amd64.deb ...
Unpacking libpython3.6-minimal:amd64 (3.6.8-1~18.04.1) ...
Selecting previously unselected package libexpat1:amd64.
Preparing to unpack .../libexpat1_2.2.5-3ubuntu0.1_amd64.deb ...
Unpacking libexpat1:amd64 (2.2.5-3ubuntu0.1) ...
Selecting previously unselected package python3.6-minimal.
Preparing to unpack .../python3.6-minimal_3.6.8-1~18.04.1_amd64.deb ...
Unpacking python3.6-minimal (3.6.8-1~18.04.1) ...
Setting up libssl1.1:amd64 (1.1.1-1ubuntu2.1~18.04.4) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 76.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.26.1 /usr/local/share/perl/5.26.1 /usr/lib/x86_64-linux-gnu/perl5/5.26 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl/5.26 /usr/share/perl/5.26 /usr/local/lib/site_perl /usr/lib/x86_64-linux-gnu/perl-base) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)
debconf: falling back to frontend: Teletype
Setting up libpython3.6-minimal:amd64 (3.6.8-1~18.04.1) ...
Setting up libexpat1:amd64 (2.2.5-3ubuntu0.1) ...
Setting up python3.6-minimal (3.6.8-1~18.04.1) ...
Selecting previously unselected package python3-minimal.
(Reading database ... 4297 files and directories currently installed.)
Preparing to unpack .../0-python3-minimal_3.6.7-1~18.04_amd64.deb ...
Unpacking python3-minimal (3.6.7-1~18.04) ...
Selecting previously unselected package mime-support.
Preparing to unpack .../1-mime-support_3.60ubuntu1_all.deb ...
Unpacking mime-support (3.60ubuntu1) ...
Selecting previously unselected package libmpdec2:amd64.
Preparing to unpack .../2-libmpdec2_2.4.2-1ubuntu1_amd64.deb ...
Unpacking libmpdec2:amd64 (2.4.2-1ubuntu1) ...
Selecting previously unselected package readline-common.
Preparing to unpack .../3-readline-common_7.0-3_all.deb ...
Unpacking readline-common (7.0-3) ...
Selecting previously unselected package libreadline7:amd64.
Preparing to unpack .../4-libreadline7_7.0-3_amd64.deb ...
Unpacking libreadline7:amd64 (7.0-3) ...
Selecting previously unselected package libsqlite3-0:amd64.
Preparing to unpack .../5-libsqlite3-0_3.22.0-1ubuntu0.1_amd64.deb ...
Unpacking libsqlite3-0:amd64 (3.22.0-1ubuntu0.1) ...
Selecting previously unselected package libpython3.6-stdlib:amd64.
Preparing to unpack .../6-libpython3.6-stdlib_3.6.8-1~18.04.1_amd64.deb ...
Unpacking libpython3.6-stdlib:amd64 (3.6.8-1~18.04.1) ...
Selecting previously unselected package python3.6.
Preparing to unpack .../7-python3.6_3.6.8-1~18.04.1_amd64.deb ...
Unpacking python3.6 (3.6.8-1~18.04.1) ...
Selecting previously unselected package libpython3-stdlib:amd64.
Preparing to unpack .../8-libpython3-stdlib_3.6.7-1~18.04_amd64.deb ...
Unpacking libpython3-stdlib:amd64 (3.6.7-1~18.04) ...
Setting up python3-minimal (3.6.7-1~18.04) ...
Selecting previously unselected package python3.
(Reading database ... 4755 files and directories currently installed.)
Preparing to unpack .../python3_3.6.7-1~18.04_amd64.deb ...
Unpacking python3 (3.6.7-1~18.04) ...
Selecting previously unselected package libmagic-mgc.
Preparing to unpack .../libmagic-mgc_1%3a5.32-2ubuntu0.2_amd64.deb ...
Unpacking libmagic-mgc (1:5.32-2ubuntu0.2) ...
Selecting previously unselected package libmagic1:amd64.
Preparing to unpack .../libmagic1_1%3a5.32-2ubuntu0.2_amd64.deb ...
Unpacking libmagic1:amd64 (1:5.32-2ubuntu0.2) ...
Selecting previously unselected package file.
Preparing to unpack .../file_1%3a5.32-2ubuntu0.2_amd64.deb ...
Unpacking file (1:5.32-2ubuntu0.2) ...
Selecting previously unselected package xz-utils.
Preparing to unpack .../xz-utils_5.2.2-1.3_amd64.deb ...
Unpacking xz-utils (5.2.2-1.3) ...
Setting up readline-common (7.0-3) ...
Setting up mime-support (3.60ubuntu1) ...
Setting up libreadline7:amd64 (7.0-3) ...
Setting up libmagic-mgc (1:5.32-2ubuntu0.2) ...
Setting up libmagic1:amd64 (1:5.32-2ubuntu0.2) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
Setting up xz-utils (5.2.2-1.3) ...
update-alternatives: using /usr/bin/xz to provide /usr/bin/lzma (lzma) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/lzma.1.gz because associated file /usr/share/man/man1/xz.1.gz (of link group lzma) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/unlzma.1.gz because associated file /usr/share/man/man1/unxz.1.gz (of link group lzma) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/lzcat.1.gz because associated file /usr/share/man/man1/xzcat.1.gz (of link group lzma) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/lzmore.1.gz because associated file /usr/share/man/man1/xzmore.1.gz (of link group lzma) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/lzless.1.gz because associated file /usr/share/man/man1/xzless.1.gz (of link group lzma) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/lzdiff.1.gz because associated file /usr/share/man/man1/xzdiff.1.gz (of link group lzma) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/lzcmp.1.gz because associated file /usr/share/man/man1/xzcmp.1.gz (of link group lzma) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/lzgrep.1.gz because associated file /usr/share/man/man1/xzgrep.1.gz (of link group lzma) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/lzegrep.1.gz because associated file /usr/share/man/man1/xzegrep.1.gz (of link group lzma) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/lzfgrep.1.gz because associated file /usr/share/man/man1/xzfgrep.1.gz (of link group lzma) doesn't exist
Setting up libsqlite3-0:amd64 (3.22.0-1ubuntu0.1) ...
Setting up libmpdec2:amd64 (2.4.2-1ubuntu1) ...
Setting up libpython3.6-stdlib:amd64 (3.6.8-1~18.04.1) ...
Setting up python3.6 (3.6.8-1~18.04.1) ...
Setting up file (1:5.32-2ubuntu0.2) ...
Setting up libpython3-stdlib:amd64 (3.6.7-1~18.04) ...
Setting up python3 (3.6.7-1~18.04) ...
running python rtupdate hooks for python3.6...
running python post-rtupdate hooks for python3.6...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
```
$apt-get install python3-pip python3-tk libopenmpi-dev wget libsm6 libxext6 libxrender-dev
```
root@4d11781e476d:/# apt-get install python3-pip python3-tk libopenmpi-dev wget libsm6 libxext6 libxrender-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  autotools-dev binutils binutils-common binutils-x86-64-linux-gnu blt build-essential ca-certificates cpp cpp-7 dbus dh-python dirmngr dpkg-dev fakeroot fontconfig-config fonts-dejavu-core g++ g++-7
  gcc gcc-7 gcc-7-base gir1.2-glib-2.0 gnupg gnupg-l10n gnupg-utils gpg gpg-agent gpg-wks-client gpg-wks-server gpgconf gpgsm ibverbs-providers libalgorithm-diff-perl libalgorithm-diff-xs-perl
  libalgorithm-merge-perl libapparmor1 libasan4 libasn1-8-heimdal libassuan0 libatomic1 libbinutils libbsd0 libc-dev-bin libc6-dev libcc1-0 libcilkrts5 libdbus-1-3 libdpkg-perl libexpat1-dev libfabric1
  libfakeroot libfile-fcntllock-perl libfontconfig1 libfreetype6 libgcc-7-dev libgdbm-compat4 libgdbm5 libgirepository-1.0-1 libglib2.0-0 libglib2.0-data libgomp1 libgssapi3-heimdal libhcrypto4-heimdal
  libheimbase1-heimdal libheimntlm0-heimdal libhwloc-dev libhwloc-plugins libhwloc5 libhx509-5-heimdal libibverbs-dev libibverbs1 libice6 libicu60 libisl19 libitm1 libkrb5-26-heimdal libksba8
  libldap-2.4-2 libldap-common liblocale-gettext-perl liblsan0 libltdl-dev libltdl7 libmpc3 libmpfr6 libmpx2 libnl-3-200 libnl-route-3-200 libnpth0 libnuma-dev libnuma1 libopenmpi2 libpciaccess0
  libperl5.26 libpng16-16 libpsl5 libpsm-infinipath1 libpthread-stubs0-dev libpython3-dev libpython3.6 libpython3.6-dev libquadmath0 librdmacm1 libroken18-heimdal libsasl2-2 libsasl2-modules
  libsasl2-modules-db libstdc++-7-dev libtcl8.6 libtk8.6 libtool libtsan0 libubsan0 libwind0-heimdal libx11-6 libx11-data libx11-dev libx11-doc libxau-dev libxau6 libxcb1 libxcb1-dev libxdmcp-dev
  libxdmcp6 libxft2 libxml2 libxrender1 libxss1 linux-libc-dev make manpages manpages-dev multiarch-support netbase ocl-icd-libopencl1 openmpi-bin openmpi-common openssl patch perl perl-modules-5.26
  pinentry-curses publicsuffix python-pip-whl python3-asn1crypto python3-cffi-backend python3-crypto python3-cryptography python3-dbus python3-dev python3-distutils python3-gi python3-idna
  python3-keyring python3-keyrings.alt python3-lib2to3 python3-pkg-resources python3-secretstorage python3-setuptools python3-six python3-wheel python3-xdg python3.6-dev shared-mime-info tk8.6-blt2.5
  tzdata ucf x11-common x11proto-core-dev x11proto-dev xdg-user-dirs xorg-sgml-doctools xtrans-dev
Suggested packages:
  binutils-doc blt-demo cpp-doc gcc-7-locales default-dbus-session-bus | dbus-session-bus dbus-user-session libpam-systemd pinentry-gnome3 tor debian-keyring g++-multilib g++-7-multilib gcc-7-doc
  libstdc++6-7-dbg gcc-multilib autoconf automake flex bison gdb gcc-doc gcc-7-multilib libgcc1-dbg libgomp1-dbg libitm1-dbg libatomic1-dbg libasan4-dbg liblsan0-dbg libtsan0-dbg libubsan0-dbg
  libcilkrts5-dbg libmpx2-dbg libquadmath0-dbg parcimonie xloadimage scdaemon glibc-doc git bzr gdbm-l10n libhwloc-contrib-plugins libtool-doc openmpi-doc pciutils libsasl2-modules-gssapi-mit
  | libsasl2-modules-gssapi-heimdal libsasl2-modules-ldap libsasl2-modules-otp libsasl2-modules-sql libstdc++-7-doc tcl8.6 tk8.6 automaken gfortran | fortran95-compiler gcj-jdk libxcb-doc make-doc
  man-browser opencl-icd gfortran ed diffutils-doc perl-doc libterm-readline-gnu-perl | libterm-readline-perl-perl pinentry-doc python-crypto-doc python-cryptography-doc python3-cryptography-vectors
  python-dbus-doc python3-dbus-dbg gnome-keyring libkf5wallet-bin gir1.2-gnomekeyring-1.0 python-secretstorage-doc python-setuptools-doc tix python3-tk-dbg
The following NEW packages will be installed:
  autotools-dev binutils binutils-common binutils-x86-64-linux-gnu blt build-essential ca-certificates cpp cpp-7 dbus dh-python dirmngr dpkg-dev fakeroot fontconfig-config fonts-dejavu-core g++ g++-7
  gcc gcc-7 gcc-7-base gir1.2-glib-2.0 gnupg gnupg-l10n gnupg-utils gpg gpg-agent gpg-wks-client gpg-wks-server gpgconf gpgsm ibverbs-providers libalgorithm-diff-perl libalgorithm-diff-xs-perl
  libalgorithm-merge-perl libapparmor1 libasan4 libasn1-8-heimdal libassuan0 libatomic1 libbinutils libbsd0 libc-dev-bin libc6-dev libcc1-0 libcilkrts5 libdbus-1-3 libdpkg-perl libexpat1-dev libfabric1
  libfakeroot libfile-fcntllock-perl libfontconfig1 libfreetype6 libgcc-7-dev libgdbm-compat4 libgdbm5 libgirepository-1.0-1 libglib2.0-0 libglib2.0-data libgomp1 libgssapi3-heimdal libhcrypto4-heimdal
  libheimbase1-heimdal libheimntlm0-heimdal libhwloc-dev libhwloc-plugins libhwloc5 libhx509-5-heimdal libibverbs-dev libibverbs1 libice6 libicu60 libisl19 libitm1 libkrb5-26-heimdal libksba8
  libldap-2.4-2 libldap-common liblocale-gettext-perl liblsan0 libltdl-dev libltdl7 libmpc3 libmpfr6 libmpx2 libnl-3-200 libnl-route-3-200 libnpth0 libnuma-dev libnuma1 libopenmpi-dev libopenmpi2
  libpciaccess0 libperl5.26 libpng16-16 libpsl5 libpsm-infinipath1 libpthread-stubs0-dev libpython3-dev libpython3.6 libpython3.6-dev libquadmath0 librdmacm1 libroken18-heimdal libsasl2-2
  libsasl2-modules libsasl2-modules-db libsm6 libstdc++-7-dev libtcl8.6 libtk8.6 libtool libtsan0 libubsan0 libwind0-heimdal libx11-6 libx11-data libx11-dev libx11-doc libxau-dev libxau6 libxcb1
  libxcb1-dev libxdmcp-dev libxdmcp6 libxext6 libxft2 libxml2 libxrender-dev libxrender1 libxss1 linux-libc-dev make manpages manpages-dev multiarch-support netbase ocl-icd-libopencl1 openmpi-bin
  openmpi-common openssl patch perl perl-modules-5.26 pinentry-curses publicsuffix python-pip-whl python3-asn1crypto python3-cffi-backend python3-crypto python3-cryptography python3-dbus python3-dev
  python3-distutils python3-gi python3-idna python3-keyring python3-keyrings.alt python3-lib2to3 python3-pip python3-pkg-resources python3-secretstorage python3-setuptools python3-six python3-tk
  python3-wheel python3-xdg python3.6-dev shared-mime-info tk8.6-blt2.5 tzdata ucf wget x11-common x11proto-core-dev x11proto-dev xdg-user-dirs xorg-sgml-doctools xtrans-dev
0 upgraded, 180 newly installed, 0 to remove and 0 not upgraded.
Need to get 124 MB of archives.
After this operation, 416 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu bionic/main amd64 liblocale-gettext-perl amd64 1.07-3build2 [16.6 kB]
Get:2 http://archive.ubuntu.com/ubuntu bionic/main amd64 multiarch-support amd64 2.27-3ubuntu1 [6916 B]
Get:3 http://archive.ubuntu.com/ubuntu bionic/main amd64 libxau6 amd64 1:1.0.8-1 [8376 B]
Get:4 http://archive.ubuntu.com/ubuntu bionic/main amd64 libbsd0 amd64 0.8.7-1 [41.5 kB]
Get:5 http://archive.ubuntu.com/ubuntu bionic/main amd64 libxdmcp6 amd64 1:1.1.2-3 [10.7 kB]
Get:6 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libxcb1 amd64 1.13-2~ubuntu18.04 [45.5 kB]
Get:7 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libx11-data all 2:1.6.4-3ubuntu0.2 [113 kB]
Get:8 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libx11-6 amd64 2:1.6.4-3ubuntu0.2 [569 kB]
Get:9 http://archive.ubuntu.com/ubuntu bionic/main amd64 libxext6 amd64 2:1.3.3-1 [29.4 kB]
Get:10 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 x11-common all 1:7.7+19ubuntu7.1 [22.5 kB]
Get:11 http://archive.ubuntu.com/ubuntu bionic/main amd64 libice6 amd64 2:1.0.9-2 [40.2 kB]
Get:12 http://archive.ubuntu.com/ubuntu bionic/main amd64 libsm6 amd64 2:1.2.2-1 [15.8 kB]
Get:13 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libpng16-16 amd64 1.6.34-1ubuntu0.18.04.2 [176 kB]
Get:14 http://archive.ubuntu.com/ubuntu bionic/main amd64 libfreetype6 amd64 2.8.1-2ubuntu2 [335 kB]
Get:15 http://archive.ubuntu.com/ubuntu bionic/main amd64 ucf all 3.0038 [50.5 kB]
Get:16 http://archive.ubuntu.com/ubuntu bionic/main amd64 fonts-dejavu-core all 2.37-1 [1041 kB]
Get:17 http://archive.ubuntu.com/ubuntu bionic/main amd64 fontconfig-config all 2.12.6-0ubuntu2 [55.8 kB]
Get:18 http://archive.ubuntu.com/ubuntu bionic/main amd64 libfontconfig1 amd64 2.12.6-0ubuntu2 [137 kB]
Get:19 http://archive.ubuntu.com/ubuntu bionic/main amd64 libxrender1 amd64 1:0.9.10-1 [18.7 kB]
Get:20 http://archive.ubuntu.com/ubuntu bionic/main amd64 libxft2 amd64 2.3.2-1 [36.1 kB]
Get:21 http://archive.ubuntu.com/ubuntu bionic/main amd64 libxss1 amd64 1:1.2.2-1 [8582 B]
Get:22 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 perl-modules-5.26 all 5.26.1-6ubuntu0.3 [2763 kB]
Get:23 http://archive.ubuntu.com/ubuntu bionic/main amd64 libgdbm5 amd64 1.14.1-6 [26.0 kB]
Get:24 http://archive.ubuntu.com/ubuntu bionic/main amd64 libgdbm-compat4 amd64 1.14.1-6 [6084 B]
Get:25 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libperl5.26 amd64 5.26.1-6ubuntu0.3 [3527 kB]
Get:26 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 perl amd64 5.26.1-6ubuntu0.3 [201 kB]
Get:27 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 openssl amd64 1.1.1-1ubuntu2.1~18.04.4 [613 kB]
Get:28 http://archive.ubuntu.com/ubuntu bionic/main amd64 ca-certificates all 20180409 [151 kB]
Get:29 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libapparmor1 amd64 2.12-4ubuntu5.1 [31.3 kB]
Get:30 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libdbus-1-3 amd64 1.12.2-1ubuntu1.1 [175 kB]
Get:31 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 dbus amd64 1.12.2-1ubuntu1.1 [150 kB]
Get:32 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libglib2.0-0 amd64 2.56.4-0ubuntu0.18.04.4 [1169 kB]
Get:33 http://archive.ubuntu.com/ubuntu bionic/main amd64 libgirepository-1.0-1 amd64 1.56.1-1 [82.0 kB]
Get:34 http://archive.ubuntu.com/ubuntu bionic/main amd64 gir1.2-glib-2.0 amd64 1.56.1-1 [131 kB]
Get:35 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libglib2.0-data all 2.56.4-0ubuntu0.18.04.4 [4496 B]
Get:36 http://archive.ubuntu.com/ubuntu bionic/main amd64 libicu60 amd64 60.2-3ubuntu3 [8054 kB]
Get:37 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libxml2 amd64 2.9.4+dfsg1-6.1ubuntu1.2 [663 kB]
Get:38 http://archive.ubuntu.com/ubuntu bionic/main amd64 netbase all 5.4 [12.7 kB]
Get:39 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-dbus amd64 1.2.6-1 [89.9 kB]
Get:40 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3-gi amd64 3.26.1-2ubuntu1 [153 kB]
Get:41 http://archive.ubuntu.com/ubuntu bionic/main amd64 shared-mime-info amd64 1.9-2 [426 kB]
Get:42 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 tzdata all 2019b-0ubuntu0.18.04 [190 kB]
Get:43 http://archive.ubuntu.com/ubuntu bionic/main amd64 xdg-user-dirs amd64 0.17-1ubuntu1 [48.0 kB]
Get:44 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libnuma1 amd64 2.0.11-2.1ubuntu0.1 [22.0 kB]
Get:45 http://archive.ubuntu.com/ubuntu bionic/main amd64 libpsl5 amd64 0.19.1-5build1 [41.8 kB]
Get:46 http://archive.ubuntu.com/ubuntu bionic/main amd64 manpages all 4.15-1 [1234 kB]
Get:47 http://archive.ubuntu.com/ubuntu bionic/main amd64 publicsuffix all 20180223.1310-1 [97.6 kB]
Get:48 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 wget amd64 1.19.4-1ubuntu2.2 [316 kB]
Get:49 http://archive.ubuntu.com/ubuntu bionic/main amd64 autotools-dev all 20180224.1 [39.6 kB]
Get:50 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 binutils-common amd64 2.30-21ubuntu1~18.04.2 [193 kB]
Get:51 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libbinutils amd64 2.30-21ubuntu1~18.04.2 [503 kB]
Get:52 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 binutils-x86-64-linux-gnu amd64 2.30-21ubuntu1~18.04.2 [1856 kB]
Get:53 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 binutils amd64 2.30-21ubuntu1~18.04.2 [3396 B]
Get:54 http://archive.ubuntu.com/ubuntu bionic/main amd64 libtcl8.6 amd64 8.6.8+dfsg-3 [881 kB]
Get:55 http://archive.ubuntu.com/ubuntu bionic/main amd64 libtk8.6 amd64 8.6.8-4 [693 kB]
Get:56 http://archive.ubuntu.com/ubuntu bionic/main amd64 tk8.6-blt2.5 amd64 2.5.3+dfsg-4 [572 kB]
Get:57 http://archive.ubuntu.com/ubuntu bionic/main amd64 blt amd64 2.5.3+dfsg-4 [4944 B]
Get:58 http://archive.ubuntu.com/ubuntu bionic/main amd64 libc-dev-bin amd64 2.27-3ubuntu1 [71.8 kB]
Get:59 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 linux-libc-dev amd64 4.15.0-58.64 [1043 kB]
Get:60 http://archive.ubuntu.com/ubuntu bionic/main amd64 libc6-dev amd64 2.27-3ubuntu1 [2587 kB]
Get:61 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gcc-7-base amd64 7.4.0-1ubuntu1~18.04.1 [18.9 kB]
Get:62 http://archive.ubuntu.com/ubuntu bionic/main amd64 libisl19 amd64 0.19-1 [551 kB]
Get:63 http://archive.ubuntu.com/ubuntu bionic/main amd64 libmpfr6 amd64 4.0.1-1 [243 kB]
Get:64 http://archive.ubuntu.com/ubuntu bionic/main amd64 libmpc3 amd64 1.1.0-1 [40.8 kB]
Get:65 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 cpp-7 amd64 7.4.0-1ubuntu1~18.04.1 [6742 kB]
Get:66 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 cpp amd64 4:7.4.0-1ubuntu2.3 [27.7 kB]
Get:67 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libcc1-0 amd64 8.3.0-6ubuntu1~18.04.1 [47.4 kB]
Get:68 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libgomp1 amd64 8.3.0-6ubuntu1~18.04.1 [76.4 kB]
Get:69 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libitm1 amd64 8.3.0-6ubuntu1~18.04.1 [28.0 kB]
Get:70 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libatomic1 amd64 8.3.0-6ubuntu1~18.04.1 [9184 B]
Get:71 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libasan4 amd64 7.4.0-1ubuntu1~18.04.1 [359 kB]
Get:72 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 liblsan0 amd64 8.3.0-6ubuntu1~18.04.1 [133 kB]
Get:73 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libtsan0 amd64 8.3.0-6ubuntu1~18.04.1 [288 kB]
Get:74 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libubsan0 amd64 7.4.0-1ubuntu1~18.04.1 [126 kB]
Get:75 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libcilkrts5 amd64 7.4.0-1ubuntu1~18.04.1 [42.5 kB]
Get:76 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libmpx2 amd64 8.3.0-6ubuntu1~18.04.1 [11.6 kB]
Get:77 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libquadmath0 amd64 8.3.0-6ubuntu1~18.04.1 [133 kB]
Get:78 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libgcc-7-dev amd64 7.4.0-1ubuntu1~18.04.1 [2381 kB]
Get:79 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gcc-7 amd64 7.4.0-1ubuntu1~18.04.1 [7463 kB]
Get:80 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gcc amd64 4:7.4.0-1ubuntu2.3 [5184 B]
Get:81 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libstdc++-7-dev amd64 7.4.0-1ubuntu1~18.04.1 [1468 kB]
Get:82 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 g++-7 amd64 7.4.0-1ubuntu1~18.04.1 [7574 kB]
Get:83 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 g++ amd64 4:7.4.0-1ubuntu2.3 [1568 B]
Get:84 http://archive.ubuntu.com/ubuntu bionic/main amd64 make amd64 4.1-9.1ubuntu1 [154 kB]
Get:85 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libdpkg-perl all 1.19.0.5ubuntu2.1 [211 kB]
Get:86 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 patch amd64 2.7.6-2ubuntu1.1 [102 kB]
Get:87 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 dpkg-dev all 1.19.0.5ubuntu2.1 [608 kB]
Get:88 http://archive.ubuntu.com/ubuntu bionic/main amd64 build-essential amd64 12.4ubuntu1 [4758 B]
Get:89 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3-lib2to3 all 3.6.8-1~18.04 [76.5 kB]
Get:90 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3-distutils all 3.6.8-1~18.04 [141 kB]
Get:91 http://archive.ubuntu.com/ubuntu bionic/main amd64 dh-python all 3.20180325ubuntu2 [89.2 kB]
Get:92 http://archive.ubuntu.com/ubuntu bionic/main amd64 libassuan0 amd64 2.5.1-2 [35.0 kB]
Get:93 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gpgconf amd64 2.2.4-1ubuntu1.2 [123 kB]
Get:94 http://archive.ubuntu.com/ubuntu bionic/main amd64 libksba8 amd64 1.3.5-2 [92.6 kB]
Get:95 http://archive.ubuntu.com/ubuntu bionic/main amd64 libroken18-heimdal amd64 7.5.0+dfsg-1 [41.3 kB]
Get:96 http://archive.ubuntu.com/ubuntu bionic/main amd64 libasn1-8-heimdal amd64 7.5.0+dfsg-1 [175 kB]
Get:97 http://archive.ubuntu.com/ubuntu bionic/main amd64 libheimbase1-heimdal amd64 7.5.0+dfsg-1 [29.3 kB]
Get:98 http://archive.ubuntu.com/ubuntu bionic/main amd64 libhcrypto4-heimdal amd64 7.5.0+dfsg-1 [85.9 kB]
Get:99 http://archive.ubuntu.com/ubuntu bionic/main amd64 libwind0-heimdal amd64 7.5.0+dfsg-1 [47.8 kB]
Get:100 http://archive.ubuntu.com/ubuntu bionic/main amd64 libhx509-5-heimdal amd64 7.5.0+dfsg-1 [107 kB]
Get:101 http://archive.ubuntu.com/ubuntu bionic/main amd64 libkrb5-26-heimdal amd64 7.5.0+dfsg-1 [206 kB]
Get:102 http://archive.ubuntu.com/ubuntu bionic/main amd64 libheimntlm0-heimdal amd64 7.5.0+dfsg-1 [14.8 kB]
Get:103 http://archive.ubuntu.com/ubuntu bionic/main amd64 libgssapi3-heimdal amd64 7.5.0+dfsg-1 [96.5 kB]
Get:104 http://archive.ubuntu.com/ubuntu bionic/main amd64 libsasl2-modules-db amd64 2.1.27~101-g0780600+dfsg-3ubuntu2 [14.8 kB]
Get:105 http://archive.ubuntu.com/ubuntu bionic/main amd64 libsasl2-2 amd64 2.1.27~101-g0780600+dfsg-3ubuntu2 [49.2 kB]
Get:106 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libldap-common all 2.4.45+dfsg-1ubuntu1.3 [16.9 kB]
Get:107 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libldap-2.4-2 amd64 2.4.45+dfsg-1ubuntu1.3 [155 kB]
Get:108 http://archive.ubuntu.com/ubuntu bionic/main amd64 libnpth0 amd64 1.5-3 [7668 B]
Get:109 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 dirmngr amd64 2.2.4-1ubuntu1.2 [316 kB]
Get:110 http://archive.ubuntu.com/ubuntu bionic/main amd64 libfakeroot amd64 1.22-2ubuntu1 [25.9 kB]
Get:111 http://archive.ubuntu.com/ubuntu bionic/main amd64 fakeroot amd64 1.22-2ubuntu1 [62.3 kB]
Get:112 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gnupg-l10n all 2.2.4-1ubuntu1.2 [49.6 kB]
Get:113 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gnupg-utils amd64 2.2.4-1ubuntu1.2 [127 kB]
Get:114 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gpg amd64 2.2.4-1ubuntu1.2 [467 kB]
Get:115 http://archive.ubuntu.com/ubuntu bionic/main amd64 pinentry-curses amd64 1.1.0-1 [35.8 kB]
Get:116 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gpg-agent amd64 2.2.4-1ubuntu1.2 [227 kB]
Get:117 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gpg-wks-client amd64 2.2.4-1ubuntu1.2 [91.9 kB]
Get:118 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gpg-wks-server amd64 2.2.4-1ubuntu1.2 [84.9 kB]
Get:119 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gpgsm amd64 2.2.4-1ubuntu1.2 [215 kB]
Get:120 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 gnupg amd64 2.2.4-1ubuntu1.2 [249 kB]
Get:121 http://archive.ubuntu.com/ubuntu bionic/main amd64 libnl-3-200 amd64 3.2.29-0ubuntu3 [52.8 kB]
Get:122 http://archive.ubuntu.com/ubuntu bionic/main amd64 libnl-route-3-200 amd64 3.2.29-0ubuntu3 [146 kB]
Get:123 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libibverbs1 amd64 17.1-1ubuntu0.1 [44.5 kB]
Get:124 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 ibverbs-providers amd64 17.1-1ubuntu0.1 [160 kB]
Get:125 http://archive.ubuntu.com/ubuntu bionic/main amd64 libalgorithm-diff-perl all 1.19.03-1 [47.6 kB]
Get:126 http://archive.ubuntu.com/ubuntu bionic/main amd64 libalgorithm-diff-xs-perl amd64 0.04-5 [11.1 kB]
Get:127 http://archive.ubuntu.com/ubuntu bionic/main amd64 libalgorithm-merge-perl all 0.08-3 [12.0 kB]
Get:128 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libexpat1-dev amd64 2.2.5-3ubuntu0.1 [122 kB]
Get:129 http://archive.ubuntu.com/ubuntu bionic/universe amd64 libpsm-infinipath1 amd64 3.3+20.604758e7-5 [174 kB]
Get:130 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 librdmacm1 amd64 17.1-1ubuntu0.1 [56.0 kB]
Get:131 http://archive.ubuntu.com/ubuntu bionic/universe amd64 libfabric1 amd64 1.5.3-1 [302 kB]
Get:132 http://archive.ubuntu.com/ubuntu bionic/main amd64 libfile-fcntllock-perl amd64 0.22-3build2 [33.2 kB]
Get:133 http://archive.ubuntu.com/ubuntu bionic/main amd64 libltdl7 amd64 2.4.6-2 [38.8 kB]
Get:134 http://archive.ubuntu.com/ubuntu bionic/main amd64 libltdl-dev amd64 2.4.6-2 [162 kB]
Get:135 http://archive.ubuntu.com/ubuntu bionic/main amd64 libpciaccess0 amd64 0.14-1 [17.9 kB]
Get:136 http://archive.ubuntu.com/ubuntu bionic/main amd64 libpthread-stubs0-dev amd64 0.3-4 [4068 B]
Get:137 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libpython3.6 amd64 3.6.8-1~18.04.1 [1418 kB]
Get:138 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libpython3.6-dev amd64 3.6.8-1~18.04.1 [44.8 MB]
Get:139 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libpython3-dev amd64 3.6.7-1~18.04 [7328 B]                                                                                             
Get:140 http://archive.ubuntu.com/ubuntu bionic/main amd64 libsasl2-modules amd64 2.1.27~101-g0780600+dfsg-3ubuntu2 [48.7 kB]                                                                              
Get:141 http://archive.ubuntu.com/ubuntu bionic/main amd64 libtool all 2.4.6-2 [194 kB]                                                                                                                    
Get:142 http://archive.ubuntu.com/ubuntu bionic/main amd64 xorg-sgml-doctools all 1:1.11-1 [12.9 kB]                                                                                                       
Get:143 http://archive.ubuntu.com/ubuntu bionic/main amd64 x11proto-dev all 2018.4-4 [251 kB]                                                                                                              
Get:144 http://archive.ubuntu.com/ubuntu bionic/main amd64 x11proto-core-dev all 2018.4-4 [2620 B]                                                                                                         
Get:145 http://archive.ubuntu.com/ubuntu bionic/main amd64 libxau-dev amd64 1:1.0.8-1 [11.1 kB]                                                                                                            
Get:146 http://archive.ubuntu.com/ubuntu bionic/main amd64 libxdmcp-dev amd64 1:1.1.2-3 [25.1 kB]                                                                                                          
Get:147 http://archive.ubuntu.com/ubuntu bionic/main amd64 xtrans-dev all 1.3.5-1 [70.5 kB]                                                                                                                
Get:148 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libxcb1-dev amd64 1.13-2~ubuntu18.04 [80.0 kB]                                                                                          
Get:149 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libx11-dev amd64 2:1.6.4-3ubuntu0.2 [640 kB]                                                                                            
Get:150 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libx11-doc all 2:1.6.4-3ubuntu0.2 [2065 kB]                                                                                             
Get:151 http://archive.ubuntu.com/ubuntu bionic/main amd64 libxrender-dev amd64 1:0.9.10-1 [24.9 kB]                                                                                                       
Get:152 http://archive.ubuntu.com/ubuntu bionic/main amd64 manpages-dev all 4.15-1 [2217 kB]                                                                                                               
Get:153 http://archive.ubuntu.com/ubuntu bionic/universe amd64 libhwloc5 amd64 1.11.9-1 [105 kB]                                                                                                           
Get:154 http://archive.ubuntu.com/ubuntu bionic/main amd64 ocl-icd-libopencl1 amd64 2.2.11-1ubuntu1 [30.3 kB]                                                                                              
Get:155 http://archive.ubuntu.com/ubuntu bionic/universe amd64 libhwloc-plugins amd64 1.11.9-1 [12.5 kB]                                                                                                   
Get:156 http://archive.ubuntu.com/ubuntu bionic/universe amd64 libopenmpi2 amd64 2.1.1-8 [2056 kB]                                                                                                         
Get:157 http://archive.ubuntu.com/ubuntu bionic/universe amd64 openmpi-common all 2.1.1-8 [140 kB]                                                                                                         
Get:158 http://archive.ubuntu.com/ubuntu bionic/universe amd64 openmpi-bin amd64 2.1.1-8 [88.2 kB]                                                                                                         
Get:159 http://archive.ubuntu.com/ubuntu bionic-updates/universe amd64 python-pip-whl all 9.0.1-2.3~ubuntu1.18.04.1 [1653 kB]                                                                              
Get:160 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-asn1crypto all 0.24.0-1 [72.8 kB]                                                                                                       
Get:161 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-cffi-backend amd64 1.11.5-1 [64.6 kB]                                                                                                   
Get:162 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-crypto amd64 2.6.1-8ubuntu2 [244 kB]                                                                                                    
Get:163 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-idna all 2.6-1 [32.5 kB]                                                                                                                
Get:164 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-six all 1.11.0-2 [11.4 kB]                                                                                                              
Get:165 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3-cryptography amd64 2.1.4-1ubuntu1.3 [221 kB]                                                                                    
Get:166 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3.6-dev amd64 3.6.8-1~18.04.1 [508 kB]                                                                                            
Get:167 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3-dev amd64 3.6.7-1~18.04 [1288 B]                                                                                                
Get:168 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-secretstorage all 2.3.1-2 [12.1 kB]                                                                                                     
Get:169 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-keyring all 10.6.0-1 [26.7 kB]                                                                                                          
Get:170 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-keyrings.alt all 3.0-1 [16.6 kB]                                                                                                        
Get:171 http://archive.ubuntu.com/ubuntu bionic-updates/universe amd64 python3-pip all 9.0.1-2.3~ubuntu1.18.04.1 [114 kB]                                                                                  
Get:172 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-pkg-resources all 39.0.1-2 [98.8 kB]                                                                                                    
Get:173 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-setuptools all 39.0.1-2 [248 kB]                                                                                                        
Get:174 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 python3-tk amd64 3.6.8-1~18.04 [101 kB]                                                                                                 
Get:175 http://archive.ubuntu.com/ubuntu bionic/universe amd64 python3-wheel all 0.30.0-0.2 [36.5 kB]                                                                                                      
Get:176 http://archive.ubuntu.com/ubuntu bionic/main amd64 python3-xdg all 0.25-4ubuntu1 [31.4 kB]                                                                                                         
Get:177 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libnuma-dev amd64 2.0.11-2.1ubuntu0.1 [32.3 kB]                                                                                         
Get:178 http://archive.ubuntu.com/ubuntu bionic/universe amd64 libhwloc-dev amd64 1.11.9-1 [167 kB]                                                                                                        
Get:179 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libibverbs-dev amd64 17.1-1ubuntu0.1 [103 kB]                                                                                           
Get:180 http://archive.ubuntu.com/ubuntu bionic/universe amd64 libopenmpi-dev amd64 2.1.1-8 [925 kB]                                                                                                       
Fetched 124 MB in 10s (12.5 MB/s)                                                                                                                                                                          
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package liblocale-gettext-perl.
(Reading database ... 4859 files and directories currently installed.)
Preparing to unpack .../liblocale-gettext-perl_1.07-3build2_amd64.deb ...
Unpacking liblocale-gettext-perl (1.07-3build2) ...
Selecting previously unselected package multiarch-support.
Preparing to unpack .../multiarch-support_2.27-3ubuntu1_amd64.deb ...
Unpacking multiarch-support (2.27-3ubuntu1) ...
Setting up multiarch-support (2.27-3ubuntu1) ...
Selecting previously unselected package libxau6:amd64.
(Reading database ... 4876 files and directories currently installed.)
Preparing to unpack .../000-libxau6_1%3a1.0.8-1_amd64.deb ...
Unpacking libxau6:amd64 (1:1.0.8-1) ...
Selecting previously unselected package libbsd0:amd64.
Preparing to unpack .../001-libbsd0_0.8.7-1_amd64.deb ...
Unpacking libbsd0:amd64 (0.8.7-1) ...
Selecting previously unselected package libxdmcp6:amd64.
Preparing to unpack .../002-libxdmcp6_1%3a1.1.2-3_amd64.deb ...
Unpacking libxdmcp6:amd64 (1:1.1.2-3) ...
Selecting previously unselected package libxcb1:amd64.
Preparing to unpack .../003-libxcb1_1.13-2~ubuntu18.04_amd64.deb ...
Unpacking libxcb1:amd64 (1.13-2~ubuntu18.04) ...
Selecting previously unselected package libx11-data.
Preparing to unpack .../004-libx11-data_2%3a1.6.4-3ubuntu0.2_all.deb ...
Unpacking libx11-data (2:1.6.4-3ubuntu0.2) ...
Selecting previously unselected package libx11-6:amd64.
Preparing to unpack .../005-libx11-6_2%3a1.6.4-3ubuntu0.2_amd64.deb ...
Unpacking libx11-6:amd64 (2:1.6.4-3ubuntu0.2) ...
Selecting previously unselected package libxext6:amd64.
Preparing to unpack .../006-libxext6_2%3a1.3.3-1_amd64.deb ...
Unpacking libxext6:amd64 (2:1.3.3-1) ...
Selecting previously unselected package x11-common.
Preparing to unpack .../007-x11-common_1%3a7.7+19ubuntu7.1_all.deb ...
dpkg-query: no packages found matching nux-tools
Unpacking x11-common (1:7.7+19ubuntu7.1) ...
Selecting previously unselected package libice6:amd64.
Preparing to unpack .../008-libice6_2%3a1.0.9-2_amd64.deb ...
Unpacking libice6:amd64 (2:1.0.9-2) ...
Selecting previously unselected package libsm6:amd64.
Preparing to unpack .../009-libsm6_2%3a1.2.2-1_amd64.deb ...
Unpacking libsm6:amd64 (2:1.2.2-1) ...
Selecting previously unselected package libpng16-16:amd64.
Preparing to unpack .../010-libpng16-16_1.6.34-1ubuntu0.18.04.2_amd64.deb ...
Unpacking libpng16-16:amd64 (1.6.34-1ubuntu0.18.04.2) ...
Selecting previously unselected package libfreetype6:amd64.
Preparing to unpack .../011-libfreetype6_2.8.1-2ubuntu2_amd64.deb ...
Unpacking libfreetype6:amd64 (2.8.1-2ubuntu2) ...
Selecting previously unselected package ucf.
Preparing to unpack .../012-ucf_3.0038_all.deb ...
Moving old data out of the way
Unpacking ucf (3.0038) ...
Selecting previously unselected package fonts-dejavu-core.
Preparing to unpack .../013-fonts-dejavu-core_2.37-1_all.deb ...
Unpacking fonts-dejavu-core (2.37-1) ...
Selecting previously unselected package fontconfig-config.
Preparing to unpack .../014-fontconfig-config_2.12.6-0ubuntu2_all.deb ...
Unpacking fontconfig-config (2.12.6-0ubuntu2) ...
Selecting previously unselected package libfontconfig1:amd64.
Preparing to unpack .../015-libfontconfig1_2.12.6-0ubuntu2_amd64.deb ...
Unpacking libfontconfig1:amd64 (2.12.6-0ubuntu2) ...
Selecting previously unselected package libxrender1:amd64.
Preparing to unpack .../016-libxrender1_1%3a0.9.10-1_amd64.deb ...
Unpacking libxrender1:amd64 (1:0.9.10-1) ...
Selecting previously unselected package libxft2:amd64.
Preparing to unpack .../017-libxft2_2.3.2-1_amd64.deb ...
Unpacking libxft2:amd64 (2.3.2-1) ...
Selecting previously unselected package libxss1:amd64.
Preparing to unpack .../018-libxss1_1%3a1.2.2-1_amd64.deb ...
Unpacking libxss1:amd64 (1:1.2.2-1) ...
Selecting previously unselected package perl-modules-5.26.
Preparing to unpack .../019-perl-modules-5.26_5.26.1-6ubuntu0.3_all.deb ...
Unpacking perl-modules-5.26 (5.26.1-6ubuntu0.3) ...
Selecting previously unselected package libgdbm5:amd64.
Preparing to unpack .../020-libgdbm5_1.14.1-6_amd64.deb ...
Unpacking libgdbm5:amd64 (1.14.1-6) ...
Selecting previously unselected package libgdbm-compat4:amd64.
Preparing to unpack .../021-libgdbm-compat4_1.14.1-6_amd64.deb ...
Unpacking libgdbm-compat4:amd64 (1.14.1-6) ...
Selecting previously unselected package libperl5.26:amd64.
Preparing to unpack .../022-libperl5.26_5.26.1-6ubuntu0.3_amd64.deb ...
Unpacking libperl5.26:amd64 (5.26.1-6ubuntu0.3) ...
Selecting previously unselected package perl.
Preparing to unpack .../023-perl_5.26.1-6ubuntu0.3_amd64.deb ...
Unpacking perl (5.26.1-6ubuntu0.3) ...
Selecting previously unselected package openssl.
Preparing to unpack .../024-openssl_1.1.1-1ubuntu2.1~18.04.4_amd64.deb ...
Unpacking openssl (1.1.1-1ubuntu2.1~18.04.4) ...
Selecting previously unselected package ca-certificates.
Preparing to unpack .../025-ca-certificates_20180409_all.deb ...
Unpacking ca-certificates (20180409) ...
Selecting previously unselected package libapparmor1:amd64.
Preparing to unpack .../026-libapparmor1_2.12-4ubuntu5.1_amd64.deb ...
Unpacking libapparmor1:amd64 (2.12-4ubuntu5.1) ...
Selecting previously unselected package libdbus-1-3:amd64.
Preparing to unpack .../027-libdbus-1-3_1.12.2-1ubuntu1.1_amd64.deb ...
Unpacking libdbus-1-3:amd64 (1.12.2-1ubuntu1.1) ...
Selecting previously unselected package dbus.
Preparing to unpack .../028-dbus_1.12.2-1ubuntu1.1_amd64.deb ...
Unpacking dbus (1.12.2-1ubuntu1.1) ...
Selecting previously unselected package libglib2.0-0:amd64.
Preparing to unpack .../029-libglib2.0-0_2.56.4-0ubuntu0.18.04.4_amd64.deb ...
Unpacking libglib2.0-0:amd64 (2.56.4-0ubuntu0.18.04.4) ...
Selecting previously unselected package libgirepository-1.0-1:amd64.
Preparing to unpack .../030-libgirepository-1.0-1_1.56.1-1_amd64.deb ...
Unpacking libgirepository-1.0-1:amd64 (1.56.1-1) ...
Selecting previously unselected package gir1.2-glib-2.0:amd64.
Preparing to unpack .../031-gir1.2-glib-2.0_1.56.1-1_amd64.deb ...
Unpacking gir1.2-glib-2.0:amd64 (1.56.1-1) ...
Selecting previously unselected package libglib2.0-data.
Preparing to unpack .../032-libglib2.0-data_2.56.4-0ubuntu0.18.04.4_all.deb ...
Unpacking libglib2.0-data (2.56.4-0ubuntu0.18.04.4) ...
Selecting previously unselected package libicu60:amd64.
Preparing to unpack .../033-libicu60_60.2-3ubuntu3_amd64.deb ...
Unpacking libicu60:amd64 (60.2-3ubuntu3) ...
Selecting previously unselected package libxml2:amd64.
Preparing to unpack .../034-libxml2_2.9.4+dfsg1-6.1ubuntu1.2_amd64.deb ...
Unpacking libxml2:amd64 (2.9.4+dfsg1-6.1ubuntu1.2) ...
Selecting previously unselected package netbase.
Preparing to unpack .../035-netbase_5.4_all.deb ...
Unpacking netbase (5.4) ...
Selecting previously unselected package python3-dbus.
Preparing to unpack .../036-python3-dbus_1.2.6-1_amd64.deb ...
Unpacking python3-dbus (1.2.6-1) ...
Selecting previously unselected package python3-gi.
Preparing to unpack .../037-python3-gi_3.26.1-2ubuntu1_amd64.deb ...
Unpacking python3-gi (3.26.1-2ubuntu1) ...
Selecting previously unselected package shared-mime-info.
Preparing to unpack .../038-shared-mime-info_1.9-2_amd64.deb ...
Unpacking shared-mime-info (1.9-2) ...
Selecting previously unselected package tzdata.
Preparing to unpack .../039-tzdata_2019b-0ubuntu0.18.04_all.deb ...
Unpacking tzdata (2019b-0ubuntu0.18.04) ...
Selecting previously unselected package xdg-user-dirs.
Preparing to unpack .../040-xdg-user-dirs_0.17-1ubuntu1_amd64.deb ...
Unpacking xdg-user-dirs (0.17-1ubuntu1) ...
Selecting previously unselected package libnuma1:amd64.
Preparing to unpack .../041-libnuma1_2.0.11-2.1ubuntu0.1_amd64.deb ...
Unpacking libnuma1:amd64 (2.0.11-2.1ubuntu0.1) ...
Selecting previously unselected package libpsl5:amd64.
Preparing to unpack .../042-libpsl5_0.19.1-5build1_amd64.deb ...
Unpacking libpsl5:amd64 (0.19.1-5build1) ...
Selecting previously unselected package manpages.
Preparing to unpack .../043-manpages_4.15-1_all.deb ...
Unpacking manpages (4.15-1) ...
Selecting previously unselected package publicsuffix.
Preparing to unpack .../044-publicsuffix_20180223.1310-1_all.deb ...
Unpacking publicsuffix (20180223.1310-1) ...
Selecting previously unselected package wget.
Preparing to unpack .../045-wget_1.19.4-1ubuntu2.2_amd64.deb ...
Unpacking wget (1.19.4-1ubuntu2.2) ...
Selecting previously unselected package autotools-dev.
Preparing to unpack .../046-autotools-dev_20180224.1_all.deb ...
Unpacking autotools-dev (20180224.1) ...
Selecting previously unselected package binutils-common:amd64.
Preparing to unpack .../047-binutils-common_2.30-21ubuntu1~18.04.2_amd64.deb ...
Unpacking binutils-common:amd64 (2.30-21ubuntu1~18.04.2) ...
Selecting previously unselected package libbinutils:amd64.
Preparing to unpack .../048-libbinutils_2.30-21ubuntu1~18.04.2_amd64.deb ...
Unpacking libbinutils:amd64 (2.30-21ubuntu1~18.04.2) ...
Selecting previously unselected package binutils-x86-64-linux-gnu.
Preparing to unpack .../049-binutils-x86-64-linux-gnu_2.30-21ubuntu1~18.04.2_amd64.deb ...
Unpacking binutils-x86-64-linux-gnu (2.30-21ubuntu1~18.04.2) ...
Selecting previously unselected package binutils.
Preparing to unpack .../050-binutils_2.30-21ubuntu1~18.04.2_amd64.deb ...
Unpacking binutils (2.30-21ubuntu1~18.04.2) ...
Selecting previously unselected package libtcl8.6:amd64.
Preparing to unpack .../051-libtcl8.6_8.6.8+dfsg-3_amd64.deb ...
Unpacking libtcl8.6:amd64 (8.6.8+dfsg-3) ...
Selecting previously unselected package libtk8.6:amd64.
Preparing to unpack .../052-libtk8.6_8.6.8-4_amd64.deb ...
Unpacking libtk8.6:amd64 (8.6.8-4) ...
Selecting previously unselected package tk8.6-blt2.5.
Preparing to unpack .../053-tk8.6-blt2.5_2.5.3+dfsg-4_amd64.deb ...
Unpacking tk8.6-blt2.5 (2.5.3+dfsg-4) ...
Selecting previously unselected package blt.
Preparing to unpack .../054-blt_2.5.3+dfsg-4_amd64.deb ...
Unpacking blt (2.5.3+dfsg-4) ...
Selecting previously unselected package libc-dev-bin.
Preparing to unpack .../055-libc-dev-bin_2.27-3ubuntu1_amd64.deb ...
Unpacking libc-dev-bin (2.27-3ubuntu1) ...
Selecting previously unselected package linux-libc-dev:amd64.
Preparing to unpack .../056-linux-libc-dev_4.15.0-58.64_amd64.deb ...
Unpacking linux-libc-dev:amd64 (4.15.0-58.64) ...
Selecting previously unselected package libc6-dev:amd64.
Preparing to unpack .../057-libc6-dev_2.27-3ubuntu1_amd64.deb ...
Unpacking libc6-dev:amd64 (2.27-3ubuntu1) ...
Selecting previously unselected package gcc-7-base:amd64.
Preparing to unpack .../058-gcc-7-base_7.4.0-1ubuntu1~18.04.1_amd64.deb ...
Unpacking gcc-7-base:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Selecting previously unselected package libisl19:amd64.
Preparing to unpack .../059-libisl19_0.19-1_amd64.deb ...
Unpacking libisl19:amd64 (0.19-1) ...
Selecting previously unselected package libmpfr6:amd64.
Preparing to unpack .../060-libmpfr6_4.0.1-1_amd64.deb ...
Unpacking libmpfr6:amd64 (4.0.1-1) ...
Selecting previously unselected package libmpc3:amd64.
Preparing to unpack .../061-libmpc3_1.1.0-1_amd64.deb ...
Unpacking libmpc3:amd64 (1.1.0-1) ...
Selecting previously unselected package cpp-7.
Preparing to unpack .../062-cpp-7_7.4.0-1ubuntu1~18.04.1_amd64.deb ...
Unpacking cpp-7 (7.4.0-1ubuntu1~18.04.1) ...
Selecting previously unselected package cpp.
Preparing to unpack .../063-cpp_4%3a7.4.0-1ubuntu2.3_amd64.deb ...
Unpacking cpp (4:7.4.0-1ubuntu2.3) ...
Selecting previously unselected package libcc1-0:amd64.
Preparing to unpack .../064-libcc1-0_8.3.0-6ubuntu1~18.04.1_amd64.deb ...
Unpacking libcc1-0:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Selecting previously unselected package libgomp1:amd64.
Preparing to unpack .../065-libgomp1_8.3.0-6ubuntu1~18.04.1_amd64.deb ...
Unpacking libgomp1:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Selecting previously unselected package libitm1:amd64.
Preparing to unpack .../066-libitm1_8.3.0-6ubuntu1~18.04.1_amd64.deb ...
Unpacking libitm1:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Selecting previously unselected package libatomic1:amd64.
Preparing to unpack .../067-libatomic1_8.3.0-6ubuntu1~18.04.1_amd64.deb ...
Unpacking libatomic1:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Selecting previously unselected package libasan4:amd64.
Preparing to unpack .../068-libasan4_7.4.0-1ubuntu1~18.04.1_amd64.deb ...
Unpacking libasan4:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Selecting previously unselected package liblsan0:amd64.
Preparing to unpack .../069-liblsan0_8.3.0-6ubuntu1~18.04.1_amd64.deb ...
Unpacking liblsan0:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Selecting previously unselected package libtsan0:amd64.
Preparing to unpack .../070-libtsan0_8.3.0-6ubuntu1~18.04.1_amd64.deb ...
Unpacking libtsan0:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Selecting previously unselected package libubsan0:amd64.
Preparing to unpack .../071-libubsan0_7.4.0-1ubuntu1~18.04.1_amd64.deb ...
Unpacking libubsan0:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Selecting previously unselected package libcilkrts5:amd64.
Preparing to unpack .../072-libcilkrts5_7.4.0-1ubuntu1~18.04.1_amd64.deb ...
Unpacking libcilkrts5:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Selecting previously unselected package libmpx2:amd64.
Preparing to unpack .../073-libmpx2_8.3.0-6ubuntu1~18.04.1_amd64.deb ...
Unpacking libmpx2:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Selecting previously unselected package libquadmath0:amd64.
Preparing to unpack .../074-libquadmath0_8.3.0-6ubuntu1~18.04.1_amd64.deb ...
Unpacking libquadmath0:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Selecting previously unselected package libgcc-7-dev:amd64.
Preparing to unpack .../075-libgcc-7-dev_7.4.0-1ubuntu1~18.04.1_amd64.deb ...
Unpacking libgcc-7-dev:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Selecting previously unselected package gcc-7.
Preparing to unpack .../076-gcc-7_7.4.0-1ubuntu1~18.04.1_amd64.deb ...
Unpacking gcc-7 (7.4.0-1ubuntu1~18.04.1) ...
Selecting previously unselected package gcc.
Preparing to unpack .../077-gcc_4%3a7.4.0-1ubuntu2.3_amd64.deb ...
Unpacking gcc (4:7.4.0-1ubuntu2.3) ...
Selecting previously unselected package libstdc++-7-dev:amd64.
Preparing to unpack .../078-libstdc++-7-dev_7.4.0-1ubuntu1~18.04.1_amd64.deb ...
Unpacking libstdc++-7-dev:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Selecting previously unselected package g++-7.
Preparing to unpack .../079-g++-7_7.4.0-1ubuntu1~18.04.1_amd64.deb ...
Unpacking g++-7 (7.4.0-1ubuntu1~18.04.1) ...
Selecting previously unselected package g++.
Preparing to unpack .../080-g++_4%3a7.4.0-1ubuntu2.3_amd64.deb ...
Unpacking g++ (4:7.4.0-1ubuntu2.3) ...
Selecting previously unselected package make.
Preparing to unpack .../081-make_4.1-9.1ubuntu1_amd64.deb ...
Unpacking make (4.1-9.1ubuntu1) ...
Selecting previously unselected package libdpkg-perl.
Preparing to unpack .../082-libdpkg-perl_1.19.0.5ubuntu2.1_all.deb ...
Unpacking libdpkg-perl (1.19.0.5ubuntu2.1) ...
Selecting previously unselected package patch.
Preparing to unpack .../083-patch_2.7.6-2ubuntu1.1_amd64.deb ...
Unpacking patch (2.7.6-2ubuntu1.1) ...
Selecting previously unselected package dpkg-dev.
Preparing to unpack .../084-dpkg-dev_1.19.0.5ubuntu2.1_all.deb ...
Unpacking dpkg-dev (1.19.0.5ubuntu2.1) ...
Selecting previously unselected package build-essential.
Preparing to unpack .../085-build-essential_12.4ubuntu1_amd64.deb ...
Unpacking build-essential (12.4ubuntu1) ...
Selecting previously unselected package python3-lib2to3.
Preparing to unpack .../086-python3-lib2to3_3.6.8-1~18.04_all.deb ...
Unpacking python3-lib2to3 (3.6.8-1~18.04) ...
Selecting previously unselected package python3-distutils.
Preparing to unpack .../087-python3-distutils_3.6.8-1~18.04_all.deb ...
Unpacking python3-distutils (3.6.8-1~18.04) ...
Selecting previously unselected package dh-python.
Preparing to unpack .../088-dh-python_3.20180325ubuntu2_all.deb ...
Unpacking dh-python (3.20180325ubuntu2) ...
Selecting previously unselected package libassuan0:amd64.
Preparing to unpack .../089-libassuan0_2.5.1-2_amd64.deb ...
Unpacking libassuan0:amd64 (2.5.1-2) ...
Selecting previously unselected package gpgconf.
Preparing to unpack .../090-gpgconf_2.2.4-1ubuntu1.2_amd64.deb ...
Unpacking gpgconf (2.2.4-1ubuntu1.2) ...
Selecting previously unselected package libksba8:amd64.
Preparing to unpack .../091-libksba8_1.3.5-2_amd64.deb ...
Unpacking libksba8:amd64 (1.3.5-2) ...
Selecting previously unselected package libroken18-heimdal:amd64.
Preparing to unpack .../092-libroken18-heimdal_7.5.0+dfsg-1_amd64.deb ...
Unpacking libroken18-heimdal:amd64 (7.5.0+dfsg-1) ...
Selecting previously unselected package libasn1-8-heimdal:amd64.
Preparing to unpack .../093-libasn1-8-heimdal_7.5.0+dfsg-1_amd64.deb ...
Unpacking libasn1-8-heimdal:amd64 (7.5.0+dfsg-1) ...
Selecting previously unselected package libheimbase1-heimdal:amd64.
Preparing to unpack .../094-libheimbase1-heimdal_7.5.0+dfsg-1_amd64.deb ...
Unpacking libheimbase1-heimdal:amd64 (7.5.0+dfsg-1) ...
Selecting previously unselected package libhcrypto4-heimdal:amd64.
Preparing to unpack .../095-libhcrypto4-heimdal_7.5.0+dfsg-1_amd64.deb ...
Unpacking libhcrypto4-heimdal:amd64 (7.5.0+dfsg-1) ...
Selecting previously unselected package libwind0-heimdal:amd64.
Preparing to unpack .../096-libwind0-heimdal_7.5.0+dfsg-1_amd64.deb ...
Unpacking libwind0-heimdal:amd64 (7.5.0+dfsg-1) ...
Selecting previously unselected package libhx509-5-heimdal:amd64.
Preparing to unpack .../097-libhx509-5-heimdal_7.5.0+dfsg-1_amd64.deb ...
Unpacking libhx509-5-heimdal:amd64 (7.5.0+dfsg-1) ...
Selecting previously unselected package libkrb5-26-heimdal:amd64.
Preparing to unpack .../098-libkrb5-26-heimdal_7.5.0+dfsg-1_amd64.deb ...
Unpacking libkrb5-26-heimdal:amd64 (7.5.0+dfsg-1) ...
Selecting previously unselected package libheimntlm0-heimdal:amd64.
Preparing to unpack .../099-libheimntlm0-heimdal_7.5.0+dfsg-1_amd64.deb ...
Unpacking libheimntlm0-heimdal:amd64 (7.5.0+dfsg-1) ...
Selecting previously unselected package libgssapi3-heimdal:amd64.
Preparing to unpack .../100-libgssapi3-heimdal_7.5.0+dfsg-1_amd64.deb ...
Unpacking libgssapi3-heimdal:amd64 (7.5.0+dfsg-1) ...
Selecting previously unselected package libsasl2-modules-db:amd64.
Preparing to unpack .../101-libsasl2-modules-db_2.1.27~101-g0780600+dfsg-3ubuntu2_amd64.deb ...
Unpacking libsasl2-modules-db:amd64 (2.1.27~101-g0780600+dfsg-3ubuntu2) ...
Selecting previously unselected package libsasl2-2:amd64.
Preparing to unpack .../102-libsasl2-2_2.1.27~101-g0780600+dfsg-3ubuntu2_amd64.deb ...
Unpacking libsasl2-2:amd64 (2.1.27~101-g0780600+dfsg-3ubuntu2) ...
Selecting previously unselected package libldap-common.
Preparing to unpack .../103-libldap-common_2.4.45+dfsg-1ubuntu1.3_all.deb ...
Unpacking libldap-common (2.4.45+dfsg-1ubuntu1.3) ...
Selecting previously unselected package libldap-2.4-2:amd64.
Preparing to unpack .../104-libldap-2.4-2_2.4.45+dfsg-1ubuntu1.3_amd64.deb ...
Unpacking libldap-2.4-2:amd64 (2.4.45+dfsg-1ubuntu1.3) ...
Selecting previously unselected package libnpth0:amd64.
Preparing to unpack .../105-libnpth0_1.5-3_amd64.deb ...
Unpacking libnpth0:amd64 (1.5-3) ...
Selecting previously unselected package dirmngr.
Preparing to unpack .../106-dirmngr_2.2.4-1ubuntu1.2_amd64.deb ...
Unpacking dirmngr (2.2.4-1ubuntu1.2) ...
Selecting previously unselected package libfakeroot:amd64.
Preparing to unpack .../107-libfakeroot_1.22-2ubuntu1_amd64.deb ...
Unpacking libfakeroot:amd64 (1.22-2ubuntu1) ...
Selecting previously unselected package fakeroot.
Preparing to unpack .../108-fakeroot_1.22-2ubuntu1_amd64.deb ...
Unpacking fakeroot (1.22-2ubuntu1) ...
Selecting previously unselected package gnupg-l10n.
Preparing to unpack .../109-gnupg-l10n_2.2.4-1ubuntu1.2_all.deb ...
Unpacking gnupg-l10n (2.2.4-1ubuntu1.2) ...
Selecting previously unselected package gnupg-utils.
Preparing to unpack .../110-gnupg-utils_2.2.4-1ubuntu1.2_amd64.deb ...
Unpacking gnupg-utils (2.2.4-1ubuntu1.2) ...
Selecting previously unselected package gpg.
Preparing to unpack .../111-gpg_2.2.4-1ubuntu1.2_amd64.deb ...
Unpacking gpg (2.2.4-1ubuntu1.2) ...
Selecting previously unselected package pinentry-curses.
Preparing to unpack .../112-pinentry-curses_1.1.0-1_amd64.deb ...
Unpacking pinentry-curses (1.1.0-1) ...
Selecting previously unselected package gpg-agent.
Preparing to unpack .../113-gpg-agent_2.2.4-1ubuntu1.2_amd64.deb ...
Unpacking gpg-agent (2.2.4-1ubuntu1.2) ...
Selecting previously unselected package gpg-wks-client.
Preparing to unpack .../114-gpg-wks-client_2.2.4-1ubuntu1.2_amd64.deb ...
Unpacking gpg-wks-client (2.2.4-1ubuntu1.2) ...
Selecting previously unselected package gpg-wks-server.
Preparing to unpack .../115-gpg-wks-server_2.2.4-1ubuntu1.2_amd64.deb ...
Unpacking gpg-wks-server (2.2.4-1ubuntu1.2) ...
Selecting previously unselected package gpgsm.
Preparing to unpack .../116-gpgsm_2.2.4-1ubuntu1.2_amd64.deb ...
Unpacking gpgsm (2.2.4-1ubuntu1.2) ...
Selecting previously unselected package gnupg.
Preparing to unpack .../117-gnupg_2.2.4-1ubuntu1.2_amd64.deb ...
Unpacking gnupg (2.2.4-1ubuntu1.2) ...
Selecting previously unselected package libnl-3-200:amd64.
Preparing to unpack .../118-libnl-3-200_3.2.29-0ubuntu3_amd64.deb ...
Unpacking libnl-3-200:amd64 (3.2.29-0ubuntu3) ...
Selecting previously unselected package libnl-route-3-200:amd64.
Preparing to unpack .../119-libnl-route-3-200_3.2.29-0ubuntu3_amd64.deb ...
Unpacking libnl-route-3-200:amd64 (3.2.29-0ubuntu3) ...
Selecting previously unselected package libibverbs1:amd64.
Preparing to unpack .../120-libibverbs1_17.1-1ubuntu0.1_amd64.deb ...
Unpacking libibverbs1:amd64 (17.1-1ubuntu0.1) ...
Selecting previously unselected package ibverbs-providers:amd64.
Preparing to unpack .../121-ibverbs-providers_17.1-1ubuntu0.1_amd64.deb ...
Unpacking ibverbs-providers:amd64 (17.1-1ubuntu0.1) ...
Selecting previously unselected package libalgorithm-diff-perl.
Preparing to unpack .../122-libalgorithm-diff-perl_1.19.03-1_all.deb ...
Unpacking libalgorithm-diff-perl (1.19.03-1) ...
Selecting previously unselected package libalgorithm-diff-xs-perl.
Preparing to unpack .../123-libalgorithm-diff-xs-perl_0.04-5_amd64.deb ...
Unpacking libalgorithm-diff-xs-perl (0.04-5) ...
Selecting previously unselected package libalgorithm-merge-perl.
Preparing to unpack .../124-libalgorithm-merge-perl_0.08-3_all.deb ...
Unpacking libalgorithm-merge-perl (0.08-3) ...
Selecting previously unselected package libexpat1-dev:amd64.
Preparing to unpack .../125-libexpat1-dev_2.2.5-3ubuntu0.1_amd64.deb ...
Unpacking libexpat1-dev:amd64 (2.2.5-3ubuntu0.1) ...
Selecting previously unselected package libpsm-infinipath1.
Preparing to unpack .../126-libpsm-infinipath1_3.3+20.604758e7-5_amd64.deb ...
Unpacking libpsm-infinipath1 (3.3+20.604758e7-5) ...
Selecting previously unselected package librdmacm1:amd64.
Preparing to unpack .../127-librdmacm1_17.1-1ubuntu0.1_amd64.deb ...
Unpacking librdmacm1:amd64 (17.1-1ubuntu0.1) ...
Selecting previously unselected package libfabric1.
Preparing to unpack .../128-libfabric1_1.5.3-1_amd64.deb ...
Unpacking libfabric1 (1.5.3-1) ...
Selecting previously unselected package libfile-fcntllock-perl.
Preparing to unpack .../129-libfile-fcntllock-perl_0.22-3build2_amd64.deb ...
Unpacking libfile-fcntllock-perl (0.22-3build2) ...
Selecting previously unselected package libltdl7:amd64.
Preparing to unpack .../130-libltdl7_2.4.6-2_amd64.deb ...
Unpacking libltdl7:amd64 (2.4.6-2) ...
Selecting previously unselected package libltdl-dev:amd64.
Preparing to unpack .../131-libltdl-dev_2.4.6-2_amd64.deb ...
Unpacking libltdl-dev:amd64 (2.4.6-2) ...
Selecting previously unselected package libpciaccess0:amd64.
Preparing to unpack .../132-libpciaccess0_0.14-1_amd64.deb ...
Unpacking libpciaccess0:amd64 (0.14-1) ...
Selecting previously unselected package libpthread-stubs0-dev:amd64.
Preparing to unpack .../133-libpthread-stubs0-dev_0.3-4_amd64.deb ...
Unpacking libpthread-stubs0-dev:amd64 (0.3-4) ...
Selecting previously unselected package libpython3.6:amd64.
Preparing to unpack .../134-libpython3.6_3.6.8-1~18.04.1_amd64.deb ...
Unpacking libpython3.6:amd64 (3.6.8-1~18.04.1) ...
Selecting previously unselected package libpython3.6-dev:amd64.
Preparing to unpack .../135-libpython3.6-dev_3.6.8-1~18.04.1_amd64.deb ...
Unpacking libpython3.6-dev:amd64 (3.6.8-1~18.04.1) ...
Selecting previously unselected package libpython3-dev:amd64.
Preparing to unpack .../136-libpython3-dev_3.6.7-1~18.04_amd64.deb ...
Unpacking libpython3-dev:amd64 (3.6.7-1~18.04) ...
Selecting previously unselected package libsasl2-modules:amd64.
Preparing to unpack .../137-libsasl2-modules_2.1.27~101-g0780600+dfsg-3ubuntu2_amd64.deb ...
Unpacking libsasl2-modules:amd64 (2.1.27~101-g0780600+dfsg-3ubuntu2) ...
Selecting previously unselected package libtool.
Preparing to unpack .../138-libtool_2.4.6-2_all.deb ...
Unpacking libtool (2.4.6-2) ...
Selecting previously unselected package xorg-sgml-doctools.
Preparing to unpack .../139-xorg-sgml-doctools_1%3a1.11-1_all.deb ...
Unpacking xorg-sgml-doctools (1:1.11-1) ...
Selecting previously unselected package x11proto-dev.
Preparing to unpack .../140-x11proto-dev_2018.4-4_all.deb ...
Unpacking x11proto-dev (2018.4-4) ...
Selecting previously unselected package x11proto-core-dev.
Preparing to unpack .../141-x11proto-core-dev_2018.4-4_all.deb ...
Unpacking x11proto-core-dev (2018.4-4) ...
Selecting previously unselected package libxau-dev:amd64.
Preparing to unpack .../142-libxau-dev_1%3a1.0.8-1_amd64.deb ...
Unpacking libxau-dev:amd64 (1:1.0.8-1) ...
Selecting previously unselected package libxdmcp-dev:amd64.
Preparing to unpack .../143-libxdmcp-dev_1%3a1.1.2-3_amd64.deb ...
Unpacking libxdmcp-dev:amd64 (1:1.1.2-3) ...
Selecting previously unselected package xtrans-dev.
Preparing to unpack .../144-xtrans-dev_1.3.5-1_all.deb ...
Unpacking xtrans-dev (1.3.5-1) ...
Selecting previously unselected package libxcb1-dev:amd64.
Preparing to unpack .../145-libxcb1-dev_1.13-2~ubuntu18.04_amd64.deb ...
Unpacking libxcb1-dev:amd64 (1.13-2~ubuntu18.04) ...
Selecting previously unselected package libx11-dev:amd64.
Preparing to unpack .../146-libx11-dev_2%3a1.6.4-3ubuntu0.2_amd64.deb ...
Unpacking libx11-dev:amd64 (2:1.6.4-3ubuntu0.2) ...
Selecting previously unselected package libx11-doc.
Preparing to unpack .../147-libx11-doc_2%3a1.6.4-3ubuntu0.2_all.deb ...
Unpacking libx11-doc (2:1.6.4-3ubuntu0.2) ...
Selecting previously unselected package libxrender-dev:amd64.
Preparing to unpack .../148-libxrender-dev_1%3a0.9.10-1_amd64.deb ...
Unpacking libxrender-dev:amd64 (1:0.9.10-1) ...
Selecting previously unselected package manpages-dev.
Preparing to unpack .../149-manpages-dev_4.15-1_all.deb ...
Unpacking manpages-dev (4.15-1) ...
Selecting previously unselected package libhwloc5:amd64.
Preparing to unpack .../150-libhwloc5_1.11.9-1_amd64.deb ...
Unpacking libhwloc5:amd64 (1.11.9-1) ...
Selecting previously unselected package ocl-icd-libopencl1:amd64.
Preparing to unpack .../151-ocl-icd-libopencl1_2.2.11-1ubuntu1_amd64.deb ...
Unpacking ocl-icd-libopencl1:amd64 (2.2.11-1ubuntu1) ...
Selecting previously unselected package libhwloc-plugins.
Preparing to unpack .../152-libhwloc-plugins_1.11.9-1_amd64.deb ...
Unpacking libhwloc-plugins (1.11.9-1) ...
Selecting previously unselected package libopenmpi2:amd64.
Preparing to unpack .../153-libopenmpi2_2.1.1-8_amd64.deb ...
Unpacking libopenmpi2:amd64 (2.1.1-8) ...
Selecting previously unselected package openmpi-common.
Preparing to unpack .../154-openmpi-common_2.1.1-8_all.deb ...
Unpacking openmpi-common (2.1.1-8) ...
Selecting previously unselected package openmpi-bin.
Preparing to unpack .../155-openmpi-bin_2.1.1-8_amd64.deb ...
Unpacking openmpi-bin (2.1.1-8) ...
Selecting previously unselected package python-pip-whl.
Preparing to unpack .../156-python-pip-whl_9.0.1-2.3~ubuntu1.18.04.1_all.deb ...
Unpacking python-pip-whl (9.0.1-2.3~ubuntu1.18.04.1) ...
Selecting previously unselected package python3-asn1crypto.
Preparing to unpack .../157-python3-asn1crypto_0.24.0-1_all.deb ...
Unpacking python3-asn1crypto (0.24.0-1) ...
Selecting previously unselected package python3-cffi-backend.
Preparing to unpack .../158-python3-cffi-backend_1.11.5-1_amd64.deb ...
Unpacking python3-cffi-backend (1.11.5-1) ...
Selecting previously unselected package python3-crypto.
Preparing to unpack .../159-python3-crypto_2.6.1-8ubuntu2_amd64.deb ...
Unpacking python3-crypto (2.6.1-8ubuntu2) ...
Selecting previously unselected package python3-idna.
Preparing to unpack .../160-python3-idna_2.6-1_all.deb ...
Unpacking python3-idna (2.6-1) ...
Selecting previously unselected package python3-six.
Preparing to unpack .../161-python3-six_1.11.0-2_all.deb ...
Unpacking python3-six (1.11.0-2) ...
Selecting previously unselected package python3-cryptography.
Preparing to unpack .../162-python3-cryptography_2.1.4-1ubuntu1.3_amd64.deb ...
Unpacking python3-cryptography (2.1.4-1ubuntu1.3) ...
Selecting previously unselected package python3.6-dev.
Preparing to unpack .../163-python3.6-dev_3.6.8-1~18.04.1_amd64.deb ...
Unpacking python3.6-dev (3.6.8-1~18.04.1) ...
Selecting previously unselected package python3-dev.
Preparing to unpack .../164-python3-dev_3.6.7-1~18.04_amd64.deb ...
Unpacking python3-dev (3.6.7-1~18.04) ...
Selecting previously unselected package python3-secretstorage.
Preparing to unpack .../165-python3-secretstorage_2.3.1-2_all.deb ...
Unpacking python3-secretstorage (2.3.1-2) ...
Selecting previously unselected package python3-keyring.
Preparing to unpack .../166-python3-keyring_10.6.0-1_all.deb ...
Unpacking python3-keyring (10.6.0-1) ...
Selecting previously unselected package python3-keyrings.alt.
Preparing to unpack .../167-python3-keyrings.alt_3.0-1_all.deb ...
Unpacking python3-keyrings.alt (3.0-1) ...
Selecting previously unselected package python3-pip.
Preparing to unpack .../168-python3-pip_9.0.1-2.3~ubuntu1.18.04.1_all.deb ...
Unpacking python3-pip (9.0.1-2.3~ubuntu1.18.04.1) ...
Selecting previously unselected package python3-pkg-resources.
Preparing to unpack .../169-python3-pkg-resources_39.0.1-2_all.deb ...
Unpacking python3-pkg-resources (39.0.1-2) ...
Selecting previously unselected package python3-setuptools.
Preparing to unpack .../170-python3-setuptools_39.0.1-2_all.deb ...
Unpacking python3-setuptools (39.0.1-2) ...
Selecting previously unselected package python3-tk:amd64.
Preparing to unpack .../171-python3-tk_3.6.8-1~18.04_amd64.deb ...
Unpacking python3-tk:amd64 (3.6.8-1~18.04) ...
Selecting previously unselected package python3-wheel.
Preparing to unpack .../172-python3-wheel_0.30.0-0.2_all.deb ...
Unpacking python3-wheel (0.30.0-0.2) ...
Selecting previously unselected package python3-xdg.
Preparing to unpack .../173-python3-xdg_0.25-4ubuntu1_all.deb ...
Unpacking python3-xdg (0.25-4ubuntu1) ...
Selecting previously unselected package libnuma-dev:amd64.
Preparing to unpack .../174-libnuma-dev_2.0.11-2.1ubuntu0.1_amd64.deb ...
Unpacking libnuma-dev:amd64 (2.0.11-2.1ubuntu0.1) ...
Selecting previously unselected package libhwloc-dev:amd64.
Preparing to unpack .../175-libhwloc-dev_1.11.9-1_amd64.deb ...
Unpacking libhwloc-dev:amd64 (1.11.9-1) ...
Selecting previously unselected package libibverbs-dev:amd64.
Preparing to unpack .../176-libibverbs-dev_17.1-1ubuntu0.1_amd64.deb ...
Unpacking libibverbs-dev:amd64 (17.1-1ubuntu0.1) ...
Selecting previously unselected package libopenmpi-dev.
Preparing to unpack .../177-libopenmpi-dev_2.1.1-8_amd64.deb ...
Unpacking libopenmpi-dev (2.1.1-8) ...
Setting up libquadmath0:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Setting up libnpth0:amd64 (1.5-3) ...
Setting up libgomp1:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Setting up libatomic1:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Setting up manpages (4.15-1) ...
Setting up libicu60:amd64 (60.2-3ubuntu3) ...
Setting up libcc1-0:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Setting up make (4.1-9.1ubuntu1) ...
Setting up python3-cffi-backend (1.11.5-1) ...
Setting up libpng16-16:amd64 (1.6.34-1ubuntu0.18.04.2) ...
Setting up libldap-common (2.4.45+dfsg-1ubuntu1.3) ...
Setting up libpthread-stubs0-dev:amd64 (0.3-4) ...
Setting up fonts-dejavu-core (2.37-1) ...
Setting up python3-crypto (2.6.1-8ubuntu2) ...
Setting up libpsl5:amd64 (0.19.1-5build1) ...
Setting up libnuma1:amd64 (2.0.11-2.1ubuntu0.1) ...
Setting up tzdata (2019b-0ubuntu0.18.04) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 76.)
debconf: falling back to frontend: Readline
Configuring tzdata
------------------

Please select the geographic area in which you live. Subsequent configuration questions will narrow this down by presenting a list of cities, representing the time zones in which they are located.

  1. Africa  2. America  3. Antarctica  4. Australia  5. Arctic  6. Asia  7. Atlantic  8. Europe  9. Indian  10. Pacific  11. SystemV  12. US  13. Etc
Geographic area: 8

Please select the city or region corresponding to your time zone.

  1. Amsterdam  7. Berlin      13. Chisinau    19. Isle_of_Man  25. Lisbon      31. Mariehamn  37. Paris      43. San_Marino  49. Stockholm  55. Vaduz      61. Zagreb
  2. Andorra    8. Bratislava  14. Copenhagen  20. Istanbul     26. Ljubljana   32. Minsk      38. Podgorica  44. Sarajevo    50. Tallinn    56. Vatican    62. Zaporozhye
  3. Astrakhan  9. Brussels    15. Dublin      21. Jersey       27. London      33. Monaco     39. Prague     45. Saratov     51. Tirane     57. Vienna     63. Zurich
  4. Athens     10. Bucharest  16. Gibraltar   22. Kaliningrad  28. Luxembourg  34. Moscow     40. Riga       46. Simferopol  52. Tiraspol   58. Vilnius
  5. Belfast    11. Budapest   17. Guernsey    23. Kiev         29. Madrid      35. Nicosia    41. Rome       47. Skopje      53. Ulyanovsk  59. Volgograd
  6. Belgrade   12. Busingen   18. Helsinki    24. Kirov        30. Malta       36. Oslo       42. Samara     48. Sofia       54. Uzhgorod   60. Warsaw
Time zone: 36


Current default time zone: 'Europe/Oslo'
Local time is now:      Tue Aug 20 17:33:10 CEST 2019.
Universal Time is now:  Tue Aug 20 15:33:10 UTC 2019.
Run 'dpkg-reconfigure tzdata' if you wish to change it.

Setting up libtsan0:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Setting up libglib2.0-0:amd64 (2.56.4-0ubuntu0.18.04.4) ...
No schema files found: doing nothing.
Setting up xorg-sgml-doctools (1:1.11-1) ...
Setting up python3-idna (2.6-1) ...
Setting up python3-xdg (0.25-4ubuntu1) ...
Setting up libsasl2-modules-db:amd64 (2.1.27~101-g0780600+dfsg-3ubuntu2) ...
Setting up python3-six (1.11.0-2) ...
Setting up linux-libc-dev:amd64 (4.15.0-58.64) ...
Setting up libmpfr6:amd64 (4.0.1-1) ...
Setting up libsasl2-2:amd64 (2.1.27~101-g0780600+dfsg-3ubuntu2) ...
Setting up libroken18-heimdal:amd64 (7.5.0+dfsg-1) ...
Setting up libksba8:amd64 (1.3.5-2) ...
Setting up python3-wheel (0.30.0-0.2) ...
Setting up perl-modules-5.26 (5.26.1-6ubuntu0.3) ...
Setting up python3-pkg-resources (39.0.1-2) ...
Setting up libgdbm5:amd64 (1.14.1-6) ...
Setting up libbsd0:amd64 (0.8.7-1) ...
Setting up ucf (3.0038) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 76.)
debconf: falling back to frontend: Readline
Setting up libgirepository-1.0-1:amd64 (1.56.1-1) ...
Setting up libxml2:amd64 (2.9.4+dfsg1-6.1ubuntu1.2) ...
Setting up x11proto-dev (2018.4-4) ...
Setting up libfreetype6:amd64 (2.8.1-2ubuntu2) ...
Setting up gnupg-l10n (2.2.4-1ubuntu1.2) ...
Setting up liblsan0:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Setting up libpsm-infinipath1 (3.3+20.604758e7-5) ...
update-alternatives: using /usr/lib/libpsm1/libpsm_infinipath.so.1.16 to provide /usr/lib/x86_64-linux-gnu/libpsm_infinipath.so.1 (libpsm_infinipath.so.1) in auto mode
Setting up gcc-7-base:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Setting up python3-asn1crypto (0.24.0-1) ...
Setting up binutils-common:amd64 (2.30-21ubuntu1~18.04.2) ...
Setting up libmpx2:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Setting up xtrans-dev (1.3.5-1) ...
Setting up gir1.2-glib-2.0:amd64 (1.56.1-1) ...
Setting up patch (2.7.6-2ubuntu1.1) ...
Setting up libglib2.0-data (2.56.4-0ubuntu0.18.04.4) ...
Setting up openmpi-common (2.1.1-8) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
Setting up publicsuffix (20180223.1310-1) ...
Setting up autotools-dev (20180224.1) ...
Setting up libapparmor1:amd64 (2.12-4ubuntu5.1) ...
Setting up libheimbase1-heimdal:amd64 (7.5.0+dfsg-1) ...
Setting up libfakeroot:amd64 (1.22-2ubuntu1) ...
Setting up libltdl7:amd64 (2.4.6-2) ...
Setting up openssl (1.1.1-1ubuntu2.1~18.04.4) ...
Setting up wget (1.19.4-1ubuntu2.2) ...
Setting up liblocale-gettext-perl (1.07-3build2) ...
Setting up libx11-doc (2:1.6.4-3ubuntu0.2) ...
Setting up libpciaccess0:amd64 (0.14-1) ...
Setting up shared-mime-info (1.9-2) ...
Setting up libmpc3:amd64 (1.1.0-1) ...
Setting up libc-dev-bin (2.27-3ubuntu1) ...
Setting up libtcl8.6:amd64 (8.6.8+dfsg-3) ...
Setting up libxdmcp6:amd64 (1:1.1.2-3) ...
Setting up libgdbm-compat4:amd64 (1.14.1-6) ...
Setting up ocl-icd-libopencl1:amd64 (2.2.11-1ubuntu1) ...
Setting up libsasl2-modules:amd64 (2.1.27~101-g0780600+dfsg-3ubuntu2) ...
Setting up libnl-3-200:amd64 (3.2.29-0ubuntu3) ...
Setting up python3-lib2to3 (3.6.8-1~18.04) ...
Setting up x11-common (1:7.7+19ubuntu7.1) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 76.)
debconf: falling back to frontend: Readline
update-rc.d: warning: start and stop actions are no longer supported; falling back to defaults
invoke-rc.d: could not determine current runlevel
invoke-rc.d: policy-rc.d denied execution of start.
Setting up ca-certificates (20180409) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 76.)
debconf: falling back to frontend: Readline
Updating certificates in /etc/ssl/certs...
133 added, 0 removed; done.
Setting up manpages-dev (4.15-1) ...
Setting up libc6-dev:amd64 (2.27-3ubuntu1) ...
Setting up libassuan0:amd64 (2.5.1-2) ...
Setting up xdg-user-dirs (0.17-1ubuntu1) ...
Setting up python3-distutils (3.6.8-1~18.04) ...
Setting up libitm1:amd64 (8.3.0-6ubuntu1~18.04.1) ...
Setting up libx11-data (2:1.6.4-3ubuntu0.2) ...
Setting up libxau6:amd64 (1:1.0.8-1) ...
Setting up libdbus-1-3:amd64 (1.12.2-1ubuntu1.1) ...
Setting up libpython3.6:amd64 (3.6.8-1~18.04.1) ...
Setting up netbase (5.4) ...
Setting up libisl19:amd64 (0.19-1) ...
Setting up python3-cryptography (2.1.4-1ubuntu1.3) ...
Setting up python-pip-whl (9.0.1-2.3~ubuntu1.18.04.1) ...
Setting up fontconfig-config (2.12.6-0ubuntu2) ...
Setting up python3-dbus (1.2.6-1) ...
Setting up x11proto-core-dev (2018.4-4) ...
Setting up libltdl-dev:amd64 (2.4.6-2) ...
Setting up libwind0-heimdal:amd64 (7.5.0+dfsg-1) ...
Setting up libasan4:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Setting up libbinutils:amd64 (2.30-21ubuntu1~18.04.2) ...
Setting up libcilkrts5:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Setting up libasn1-8-heimdal:amd64 (7.5.0+dfsg-1) ...
Setting up libubsan0:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Setting up gpgconf (2.2.4-1ubuntu1.2) ...
Setting up python3-keyrings.alt (3.0-1) ...
Setting up libhcrypto4-heimdal:amd64 (7.5.0+dfsg-1) ...
Setting up libxau-dev:amd64 (1:1.0.8-1) ...
Setting up libnl-route-3-200:amd64 (3.2.29-0ubuntu3) ...
Setting up python3-gi (3.26.1-2ubuntu1) ...
Setting up fakeroot (1.22-2ubuntu1) ...
update-alternatives: using /usr/bin/fakeroot-sysv to provide /usr/bin/fakeroot (fakeroot) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/fakeroot.1.gz because associated file /usr/share/man/man1/fakeroot-sysv.1.gz (of link group fakeroot) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/faked.1.gz because associated file /usr/share/man/man1/faked-sysv.1.gz (of link group fakeroot) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/es/man1/fakeroot.1.gz because associated file /usr/share/man/es/man1/fakeroot-sysv.1.gz (of link group fakeroot) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/es/man1/faked.1.gz because associated file /usr/share/man/es/man1/faked-sysv.1.gz (of link group fakeroot) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/fr/man1/fakeroot.1.gz because associated file /usr/share/man/fr/man1/fakeroot-sysv.1.gz (of link group fakeroot) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/fr/man1/faked.1.gz because associated file /usr/share/man/fr/man1/faked-sysv.1.gz (of link group fakeroot) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/sv/man1/fakeroot.1.gz because associated file /usr/share/man/sv/man1/fakeroot-sysv.1.gz (of link group fakeroot) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/sv/man1/faked.1.gz because associated file /usr/share/man/sv/man1/faked-sysv.1.gz (of link group fakeroot) doesn't exist
Setting up libhwloc5:amd64 (1.11.9-1) ...
Setting up libhx509-5-heimdal:amd64 (7.5.0+dfsg-1) ...
Setting up libgcc-7-dev:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Setting up cpp-7 (7.4.0-1ubuntu1~18.04.1) ...
Setting up libstdc++-7-dev:amd64 (7.4.0-1ubuntu1~18.04.1) ...
Setting up libhwloc-plugins (1.11.9-1) ...
Setting up libxdmcp-dev:amd64 (1:1.1.2-3) ...
Setting up libperl5.26:amd64 (5.26.1-6ubuntu0.3) ...
Setting up gpgsm (2.2.4-1ubuntu1.2) ...
Setting up python3-pip (9.0.1-2.3~ubuntu1.18.04.1) ...
Setting up gnupg-utils (2.2.4-1ubuntu1.2) ...
Setting up libice6:amd64 (2:1.0.9-2) ...
Setting up libexpat1-dev:amd64 (2.2.5-3ubuntu0.1) ...
Setting up pinentry-curses (1.1.0-1) ...
Setting up libkrb5-26-heimdal:amd64 (7.5.0+dfsg-1) ...
Setting up libnuma-dev:amd64 (2.0.11-2.1ubuntu0.1) ...
Setting up dbus (1.12.2-1ubuntu1.1) ...
Setting up python3-setuptools (39.0.1-2) ...
Setting up python3-secretstorage (2.3.1-2) ...
Setting up dh-python (3.20180325ubuntu2) ...
Setting up libxcb1:amd64 (1.13-2~ubuntu18.04) ...
Setting up libheimntlm0-heimdal:amd64 (7.5.0+dfsg-1) ...
Setting up gpg (2.2.4-1ubuntu1.2) ...
Setting up binutils-x86-64-linux-gnu (2.30-21ubuntu1~18.04.2) ...
Setting up libibverbs1:amd64 (17.1-1ubuntu0.1) ...
Setting up cpp (4:7.4.0-1ubuntu2.3) ...
Setting up libfontconfig1:amd64 (2.12.6-0ubuntu2) ...
Setting up libsm6:amd64 (2:1.2.2-1) ...
Setting up python3-keyring (10.6.0-1) ...
Setting up libhwloc-dev:amd64 (1.11.9-1) ...
Setting up libx11-6:amd64 (2:1.6.4-3ubuntu0.2) ...
Setting up gpg-agent (2.2.4-1ubuntu1.2) ...
Setting up librdmacm1:amd64 (17.1-1ubuntu0.1) ...
Setting up gpg-wks-server (2.2.4-1ubuntu1.2) ...
Setting up libpython3.6-dev:amd64 (3.6.8-1~18.04.1) ...
Setting up perl (5.26.1-6ubuntu0.3) ...
Setting up libfile-fcntllock-perl (0.22-3build2) ...
Setting up ibverbs-providers:amd64 (17.1-1ubuntu0.1) ...
Setting up libalgorithm-diff-perl (1.19.03-1) ...
Setting up libxrender1:amd64 (1:0.9.10-1) ...
Setting up libxcb1-dev:amd64 (1.13-2~ubuntu18.04) ...
Setting up binutils (2.30-21ubuntu1~18.04.2) ...
Setting up libx11-dev:amd64 (2:1.6.4-3ubuntu0.2) ...
Setting up libxft2:amd64 (2.3.2-1) ...
Setting up libgssapi3-heimdal:amd64 (7.5.0+dfsg-1) ...
Setting up python3.6-dev (3.6.8-1~18.04.1) ...
Setting up libibverbs-dev:amd64 (17.1-1ubuntu0.1) ...
Setting up libpython3-dev:amd64 (3.6.7-1~18.04) ...
Setting up libxext6:amd64 (2:1.3.3-1) ...
Setting up libfabric1 (1.5.3-1) ...
Setting up gcc-7 (7.4.0-1ubuntu1~18.04.1) ...
Setting up g++-7 (7.4.0-1ubuntu1~18.04.1) ...
Setting up libxss1:amd64 (1:1.2.2-1) ...
Setting up libdpkg-perl (1.19.0.5ubuntu2.1) ...
Setting up python3-dev (3.6.7-1~18.04) ...
Setting up libxrender-dev:amd64 (1:0.9.10-1) ...
Setting up gcc (4:7.4.0-1ubuntu2.3) ...
Setting up libalgorithm-merge-perl (0.08-3) ...
Setting up dpkg-dev (1.19.0.5ubuntu2.1) ...
Setting up libalgorithm-diff-xs-perl (0.04-5) ...
Setting up libldap-2.4-2:amd64 (2.4.45+dfsg-1ubuntu1.3) ...
Setting up g++ (4:7.4.0-1ubuntu2.3) ...
update-alternatives: using /usr/bin/g++ to provide /usr/bin/c++ (c++) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/c++.1.gz because associated file /usr/share/man/man1/g++.1.gz (of link group c++) doesn't exist
Setting up libopenmpi2:amd64 (2.1.1-8) ...
Setting up dirmngr (2.2.4-1ubuntu1.2) ...
Setting up libtool (2.4.6-2) ...
Setting up build-essential (12.4ubuntu1) ...
Setting up libtk8.6:amd64 (8.6.8-4) ...
Setting up libopenmpi-dev (2.1.1-8) ...
update-alternatives: using /usr/lib/x86_64-linux-gnu/openmpi/include to provide /usr/include/mpi (mpi) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/mpicc.1.gz because associated file /usr/share/man/man1/mpicc.openmpi.1.gz (of link group mpi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/mpic++.1.gz because associated file /usr/share/man/man1/mpic++.openmpi.1.gz (of link group mpi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/mpicxx.1.gz because associated file /usr/share/man/man1/mpicxx.openmpi.1.gz (of link group mpi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/mpiCC.1.gz because associated file /usr/share/man/man1/mpiCC.openmpi.1.gz (of link group mpi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/mpif77.1.gz because associated file /usr/share/man/man1/mpif77.openmpi.1.gz (of link group mpi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/mpif90.1.gz because associated file /usr/share/man/man1/mpif90.openmpi.1.gz (of link group mpi) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/mpifort.1.gz because associated file /usr/share/man/man1/mpifort.openmpi.1.gz (of link group mpi) doesn't exist
Setting up gpg-wks-client (2.2.4-1ubuntu1.2) ...
Setting up openmpi-bin (2.1.1-8) ...
update-alternatives: using /usr/bin/mpirun.openmpi to provide /usr/bin/mpirun (mpirun) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/mpirun.1.gz because associated file /usr/share/man/man1/mpirun.openmpi.1.gz (of link group mpirun) doesn't exist
update-alternatives: warning: skip creation of /usr/share/man/man1/mpiexec.1.gz because associated file /usr/share/man/man1/mpiexec.openmpi.1.gz (of link group mpirun) doesn't exist
Setting up tk8.6-blt2.5 (2.5.3+dfsg-4) ...
Setting up blt (2.5.3+dfsg-4) ...
Setting up gnupg (2.2.4-1ubuntu1.2) ...
Setting up python3-tk:amd64 (3.6.8-1~18.04) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
Processing triggers for ca-certificates (20180409) ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
done.
```
I now need to clone the repo in which the drl model is
$apt-get install git
```
root@4d11781e476d:/# apt-get install git
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  git-man krb5-locales less libcurl3-gnutls libedit2 liberror-perl libgssapi-krb5-2 libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libnghttp2-14 librtmp1 libssl1.0.0 libxmuu1 openssh-client xauth
Suggested packages:
  gettext-base git-daemon-run | git-daemon-sysvinit git-doc git-el git-email git-gui gitk gitweb git-cvs git-mediawiki git-svn krb5-doc krb5-user keychain libpam-ssh monkeysphere ssh-askpass
The following NEW packages will be installed:
  git git-man krb5-locales less libcurl3-gnutls libedit2 liberror-perl libgssapi-krb5-2 libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libnghttp2-14 librtmp1 libssl1.0.0 libxmuu1 openssh-client
  xauth
0 upgraded, 18 newly installed, 0 to remove and 0 not upgraded.
Need to get 7541 kB of archives.
After this operation, 45.3 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu bionic/main amd64 less amd64 487-0.1 [112 kB]
Get:2 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 krb5-locales all 1.16-2ubuntu0.1 [13.5 kB]
Get:3 http://archive.ubuntu.com/ubuntu bionic/main amd64 libedit2 amd64 3.1-20170329-1 [76.9 kB]
Get:4 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libkrb5support0 amd64 1.16-2ubuntu0.1 [30.9 kB]
Get:5 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libk5crypto3 amd64 1.16-2ubuntu0.1 [85.6 kB]
Get:6 http://archive.ubuntu.com/ubuntu bionic/main amd64 libkeyutils1 amd64 1.5.9-9.2ubuntu2 [8720 B]
Get:7 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libkrb5-3 amd64 1.16-2ubuntu0.1 [279 kB]
Get:8 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libgssapi-krb5-2 amd64 1.16-2ubuntu0.1 [122 kB]
Get:9 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libssl1.0.0 amd64 1.0.2n-1ubuntu5.3 [1088 kB]
Get:10 http://archive.ubuntu.com/ubuntu bionic/main amd64 libxmuu1 amd64 2:1.1.2-2 [9674 B]
Get:11 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 openssh-client amd64 1:7.6p1-4ubuntu0.3 [614 kB]
Get:12 http://archive.ubuntu.com/ubuntu bionic/main amd64 xauth amd64 1:1.0.10-1 [24.6 kB]
Get:13 http://archive.ubuntu.com/ubuntu bionic/main amd64 libnghttp2-14 amd64 1.30.0-1ubuntu1 [77.8 kB]
Get:14 http://archive.ubuntu.com/ubuntu bionic/main amd64 librtmp1 amd64 2.4+20151223.gitfa8646d.1-1 [54.2 kB]
Get:15 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 libcurl3-gnutls amd64 7.58.0-2ubuntu3.7 [212 kB]
Get:16 http://archive.ubuntu.com/ubuntu bionic/main amd64 liberror-perl all 0.17025-1 [22.8 kB]
Get:17 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 git-man all 1:2.17.1-1ubuntu0.4 [803 kB]
Get:18 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 git amd64 1:2.17.1-1ubuntu0.4 [3907 kB]
Fetched 7541 kB in 1s (8114 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package less.
(Reading database ... 20508 files and directories currently installed.)
Preparing to unpack .../00-less_487-0.1_amd64.deb ...
Unpacking less (487-0.1) ...
Selecting previously unselected package krb5-locales.
Preparing to unpack .../01-krb5-locales_1.16-2ubuntu0.1_all.deb ...
Unpacking krb5-locales (1.16-2ubuntu0.1) ...
Selecting previously unselected package libedit2:amd64.
Preparing to unpack .../02-libedit2_3.1-20170329-1_amd64.deb ...
Unpacking libedit2:amd64 (3.1-20170329-1) ...
Selecting previously unselected package libkrb5support0:amd64.
Preparing to unpack .../03-libkrb5support0_1.16-2ubuntu0.1_amd64.deb ...
Unpacking libkrb5support0:amd64 (1.16-2ubuntu0.1) ...
Selecting previously unselected package libk5crypto3:amd64.
Preparing to unpack .../04-libk5crypto3_1.16-2ubuntu0.1_amd64.deb ...
Unpacking libk5crypto3:amd64 (1.16-2ubuntu0.1) ...
Selecting previously unselected package libkeyutils1:amd64.
Preparing to unpack .../05-libkeyutils1_1.5.9-9.2ubuntu2_amd64.deb ...
Unpacking libkeyutils1:amd64 (1.5.9-9.2ubuntu2) ...
Selecting previously unselected package libkrb5-3:amd64.
Preparing to unpack .../06-libkrb5-3_1.16-2ubuntu0.1_amd64.deb ...
Unpacking libkrb5-3:amd64 (1.16-2ubuntu0.1) ...
Selecting previously unselected package libgssapi-krb5-2:amd64.
Preparing to unpack .../07-libgssapi-krb5-2_1.16-2ubuntu0.1_amd64.deb ...
Unpacking libgssapi-krb5-2:amd64 (1.16-2ubuntu0.1) ...
Selecting previously unselected package libssl1.0.0:amd64.
Preparing to unpack .../08-libssl1.0.0_1.0.2n-1ubuntu5.3_amd64.deb ...
Unpacking libssl1.0.0:amd64 (1.0.2n-1ubuntu5.3) ...
Selecting previously unselected package libxmuu1:amd64.
Preparing to unpack .../09-libxmuu1_2%3a1.1.2-2_amd64.deb ...
Unpacking libxmuu1:amd64 (2:1.1.2-2) ...
Selecting previously unselected package openssh-client.
Preparing to unpack .../10-openssh-client_1%3a7.6p1-4ubuntu0.3_amd64.deb ...
Unpacking openssh-client (1:7.6p1-4ubuntu0.3) ...
Selecting previously unselected package xauth.
Preparing to unpack .../11-xauth_1%3a1.0.10-1_amd64.deb ...
Unpacking xauth (1:1.0.10-1) ...
Selecting previously unselected package libnghttp2-14:amd64.
Preparing to unpack .../12-libnghttp2-14_1.30.0-1ubuntu1_amd64.deb ...
Unpacking libnghttp2-14:amd64 (1.30.0-1ubuntu1) ...
Selecting previously unselected package librtmp1:amd64.
Preparing to unpack .../13-librtmp1_2.4+20151223.gitfa8646d.1-1_amd64.deb ...
Unpacking librtmp1:amd64 (2.4+20151223.gitfa8646d.1-1) ...
Selecting previously unselected package libcurl3-gnutls:amd64.
Preparing to unpack .../14-libcurl3-gnutls_7.58.0-2ubuntu3.7_amd64.deb ...
Unpacking libcurl3-gnutls:amd64 (7.58.0-2ubuntu3.7) ...
Selecting previously unselected package liberror-perl.
Preparing to unpack .../15-liberror-perl_0.17025-1_all.deb ...
Unpacking liberror-perl (0.17025-1) ...
Selecting previously unselected package git-man.
Preparing to unpack .../16-git-man_1%3a2.17.1-1ubuntu0.4_all.deb ...
Unpacking git-man (1:2.17.1-1ubuntu0.4) ...
Selecting previously unselected package git.
Preparing to unpack .../17-git_1%3a2.17.1-1ubuntu0.4_amd64.deb ...
Unpacking git (1:2.17.1-1ubuntu0.4) ...
Setting up libedit2:amd64 (3.1-20170329-1) ...
Setting up git-man (1:2.17.1-1ubuntu0.4) ...
Setting up less (487-0.1) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 76.)
debconf: falling back to frontend: Readline
Setting up libssl1.0.0:amd64 (1.0.2n-1ubuntu5.3) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 76.)
debconf: falling back to frontend: Readline
Setting up libnghttp2-14:amd64 (1.30.0-1ubuntu1) ...
Processing triggers for mime-support (3.60ubuntu1) ...
Setting up liberror-perl (0.17025-1) ...
Setting up librtmp1:amd64 (2.4+20151223.gitfa8646d.1-1) ...
Setting up libkrb5support0:amd64 (1.16-2ubuntu0.1) ...
Setting up libxmuu1:amd64 (2:1.1.2-2) ...
Setting up xauth (1:1.0.10-1) ...
Setting up krb5-locales (1.16-2ubuntu0.1) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
Setting up libkeyutils1:amd64 (1.5.9-9.2ubuntu2) ...
Setting up libk5crypto3:amd64 (1.16-2ubuntu0.1) ...
Setting up libkrb5-3:amd64 (1.16-2ubuntu0.1) ...
Setting up libgssapi-krb5-2:amd64 (1.16-2ubuntu0.1) ...
Setting up openssh-client (1:7.6p1-4ubuntu0.3) ...
Setting up libcurl3-gnutls:amd64 (7.58.0-2ubuntu3.7) ...
Setting up git (1:2.17.1-1ubuntu0.4) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
```
$cd
$git clone https://github.com/vbelus/drl_film_fluid
```
root@4d11781e476d:/# cd
root@4d11781e476d:~# git clone https://github.com/vbelus/drl_film_fluid
Cloning into 'drl_film_fluid'...
Username for 'https://github.com': vbelus
Password for 'https://vbelus@github.com': 
remote: Enumerating objects: 74, done.
remote: Counting objects: 100% (74/74), done.
remote: Compressing objects: 100% (54/54), done.
remote: Total 226 (delta 20), reused 56 (delta 15), pack-reused 152
Receiving objects: 100% (226/226), 33.58 MiB | 2.45 MiB/s, done.
Resolving deltas: 100% (35/35), done.
```
```
root@4d11781e476d:~# ls
drl_film_fluid
```
```
```
We install all the python dependencies of the project which are in setup.py
$cd ~/drl_film_fluid/drl_fluid_film_python3/gym-film
$pip3 install -e ./
```
root@4d11781e476d:~/drl_film_fluid/drl_fluid_film_python3/gym-film# pip3 install -e ./
Obtaining file:///root/drl_film_fluid/drl_fluid_film_python3/gym-film
Collecting PySimpleGUI (from gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/40/b5/54dd8ce1cd2360424fe0d9d01bf361950a7d1565343e89f100b5628071b0/PySimpleGUI-4.2.0-py3-none-any.whl (233kB)
    100% |################################| 235kB 2.8MB/s 
Collecting gym (from gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/61/75/9e841bc2bc75128e0b65c3d5255d0bd16becb9d8f7120b965d41b8e70041/gym-0.14.0.tar.gz (1.6MB)
    100% |################################| 1.6MB 678kB/s 
Collecting matplotlib (from gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/57/4f/dd381ecf6c6ab9bcdaa8ea912e866dedc6e696756156d8ecc087e20817e2/matplotlib-3.1.1-cp36-cp36m-manylinux1_x86_64.whl (13.1MB)
    100% |################################| 13.1MB 127kB/s 
Collecting numpy (from gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/19/b9/bda9781f0a74b90ebd2e046fde1196182900bd4a8e1ea503d3ffebc50e7c/numpy-1.17.0-cp36-cp36m-manylinux1_x86_64.whl (20.4MB)
    100% |################################| 20.4MB 79kB/s 
Collecting stable_baselines (from gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/52/9f/bbb2122cf2ce0e5f09a33bc35d504b83c05b0896bd46d4b85687c62557f6/stable_baselines-2.7.0-py3-none-any.whl (259kB)
    100% |################################| 266kB 1.8MB/s 
Collecting tensorflow (from gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/de/f0/96fb2e0412ae9692dbf400e5b04432885f677ad6241c088ccc5fe7724d69/tensorflow-1.14.0-cp36-cp36m-manylinux1_x86_64.whl (109.2MB)
    100% |################################| 109.2MB 14kB/s 
Collecting cloudpickle~=1.2.0 (from gym->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/09/f4/4a080c349c1680a2086196fcf0286a65931708156f39568ed7051e42ff6a/cloudpickle-1.2.1-py2.py3-none-any.whl
Collecting pyglet<=1.3.2,>=1.2.0 (from gym->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/1c/fc/dad5eaaab68f0c21e2f906a94ddb98175662cc5a654eee404d59554ce0fa/pyglet-1.3.2-py2.py3-none-any.whl (1.0MB)
    100% |################################| 1.0MB 943kB/s 
Collecting scipy (from gym->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/29/50/a552a5aff252ae915f522e44642bb49a7b7b31677f9580cfd11bcc869976/scipy-1.3.1-cp36-cp36m-manylinux1_x86_64.whl (25.2MB)
    100% |################################| 25.2MB 66kB/s 
Requirement already satisfied: six in /usr/lib/python3/dist-packages (from gym->gym-film==0.0.1)
Collecting python-dateutil>=2.1 (from matplotlib->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/41/17/c62faccbfbd163c7f57f3844689e3a78bae1f403648a6afb1d0866d87fbb/python_dateutil-2.8.0-py2.py3-none-any.whl (226kB)
    100% |################################| 235kB 1.6MB/s 
Collecting kiwisolver>=1.0.1 (from matplotlib->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/f8/a1/5742b56282449b1c0968197f63eae486eca2c35dcd334bab75ad524e0de1/kiwisolver-1.1.0-cp36-cp36m-manylinux1_x86_64.whl (90kB)
    100% |################################| 92kB 3.3MB/s 
Collecting pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 (from matplotlib->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/11/fa/0160cd525c62d7abd076a070ff02b2b94de589f1a9789774f17d7c54058e/pyparsing-2.4.2-py2.py3-none-any.whl (65kB)
    100% |################################| 71kB 4.5MB/s 
Collecting cycler>=0.10 (from matplotlib->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/f7/d2/e07d3ebb2bd7af696440ce7e754c59dd546ffe1bbe732c8ab68b9c834e61/cycler-0.10.0-py2.py3-none-any.whl
Collecting joblib (from stable_baselines->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/cd/c1/50a758e8247561e58cb87305b1e90b171b8c767b15b12a1734001f41d356/joblib-0.13.2-py2.py3-none-any.whl (278kB)
    100% |################################| 286kB 1.6MB/s 
Collecting pandas (from stable_baselines->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/1d/9a/7eb9952f4b4d73fbd75ad1d5d6112f407e695957444cb695cbb3cdab918a/pandas-0.25.0-cp36-cp36m-manylinux1_x86_64.whl (10.5MB)
    100% |################################| 10.5MB 135kB/s 
Collecting mpi4py (from stable_baselines->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/04/f5/a615603ce4ab7f40b65dba63759455e3da610d9a155d4d4cece1d8fd6706/mpi4py-3.0.2.tar.gz (1.4MB)
    100% |################################| 1.4MB 764kB/s 
Collecting opencv-python (from stable_baselines->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/7b/d2/a2dbf83d4553ca6b3701d91d75e42fe50aea97acdc00652dca515749fb5d/opencv_python-4.1.0.25-cp36-cp36m-manylinux1_x86_64.whl (26.6MB)
    100% |################################| 26.6MB 59kB/s 
Requirement already satisfied: wheel>=0.26 in /usr/lib/python3/dist-packages (from tensorflow->gym-film==0.0.1)
Collecting grpcio>=1.8.6 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/30/31/6397193572c081e0fd1fec86a7a6b7ac497c27226281e7cb32f8c3705069/grpcio-1.23.0-cp36-cp36m-manylinux1_x86_64.whl (2.2MB)
    100% |################################| 2.2MB 589kB/s 
Collecting astor>=0.6.0 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/d1/4f/950dfae467b384fc96bc6469de25d832534f6b4441033c39f914efd13418/astor-0.8.0-py2.py3-none-any.whl
Collecting termcolor>=1.1.0 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/8a/48/a76be51647d0eb9f10e2a4511bf3ffb8cc1e6b14e9e4fab46173aa79f981/termcolor-1.1.0.tar.gz
Collecting gast>=0.2.0 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/4e/35/11749bf99b2d4e3cceb4d55ca22590b0d7c2c62b9de38ac4a4a7f4687421/gast-0.2.2.tar.gz
Collecting wrapt>=1.11.1 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/23/84/323c2415280bc4fc880ac5050dddfb3c8062c2552b34c2e512eb4aa68f79/wrapt-1.11.2.tar.gz
Collecting absl-py>=0.7.0 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/da/3f/9b0355080b81b15ba6a9ffcf1f5ea39e307a2778b2f2dc8694724e8abd5b/absl-py-0.7.1.tar.gz (99kB)
    100% |################################| 102kB 3.2MB/s 
Collecting google-pasta>=0.1.6 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/d0/33/376510eb8d6246f3c30545f416b2263eee461e40940c2a4413c711bdf62d/google_pasta-0.1.7-py3-none-any.whl (52kB)
    100% |################################| 61kB 4.2MB/s 
Collecting protobuf>=3.6.1 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/eb/f4/a27952733796330cd17c17ea1f974459f5fefbbad119c0f296a6d807fec3/protobuf-3.9.1-cp36-cp36m-manylinux1_x86_64.whl (1.2MB)
    100% |################################| 1.2MB 854kB/s 
Collecting keras-applications>=1.0.6 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/71/e3/19762fdfc62877ae9102edf6342d71b28fbfd9dea3d2f96a882ce099b03f/Keras_Applications-1.0.8-py3-none-any.whl (50kB)
    100% |################################| 51kB 4.1MB/s 
Collecting tensorboard<1.15.0,>=1.14.0 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/91/2d/2ed263449a078cd9c8a9ba50ebd50123adf1f8cfbea1492f9084169b89d9/tensorboard-1.14.0-py3-none-any.whl (3.1MB)
    100% |################################| 3.2MB 457kB/s 
Collecting tensorflow-estimator<1.15.0rc0,>=1.14.0rc0 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/3c/d5/21860a5b11caf0678fbc8319341b0ae21a07156911132e0e71bffed0510d/tensorflow_estimator-1.14.0-py2.py3-none-any.whl (488kB)
    100% |################################| 491kB 1.3MB/s 
Collecting keras-preprocessing>=1.0.5 (from tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/28/6a/8c1f62c37212d9fc441a7e26736df51ce6f0e38455816445471f10da4f0a/Keras_Preprocessing-1.1.0-py2.py3-none-any.whl (41kB)
    100% |################################| 51kB 16.0MB/s 
Collecting future (from pyglet<=1.3.2,>=1.2.0->gym->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/90/52/e20466b85000a181e1e144fd8305caf2cf475e2f9674e797b222f8105f5f/future-0.17.1.tar.gz (829kB)
    100% |################################| 829kB 1.1MB/s 
Requirement already satisfied: setuptools in /usr/lib/python3/dist-packages (from kiwisolver>=1.0.1->matplotlib->gym-film==0.0.1)
Collecting pytz>=2017.2 (from pandas->stable_baselines->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/87/76/46d697698a143e05f77bec5a526bf4e56a0be61d63425b68f4ba553b51f2/pytz-2019.2-py2.py3-none-any.whl (508kB)
    100% |################################| 512kB 1.2MB/s 
Collecting h5py (from keras-applications>=1.0.6->tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/30/99/d7d4fbf2d02bb30fb76179911a250074b55b852d34e98dd452a9f394ac06/h5py-2.9.0-cp36-cp36m-manylinux1_x86_64.whl (2.8MB)
    100% |################################| 2.8MB 442kB/s 
Collecting werkzeug>=0.11.15 (from tensorboard<1.15.0,>=1.14.0->tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/d1/ab/d3bed6b92042622d24decc7aadc8877badf18aeca1571045840ad4956d3f/Werkzeug-0.15.5-py2.py3-none-any.whl (328kB)
    100% |################################| 337kB 1.4MB/s 
Collecting markdown>=2.6.8 (from tensorboard<1.15.0,>=1.14.0->tensorflow->gym-film==0.0.1)
  Downloading https://files.pythonhosted.org/packages/c0/4e/fd492e91abdc2d2fcb70ef453064d980688762079397f779758e055f6575/Markdown-3.1.1-py2.py3-none-any.whl (87kB)
    100% |################################| 92kB 3.4MB/s 
Building wheels for collected packages: gym, mpi4py, termcolor, gast, wrapt, absl-py, future
  Running setup.py bdist_wheel for gym ... done
  Stored in directory: /root/.cache/pip/wheels/7e/53/f6/c0cd3c9bf953f35c0aee7fa62ea209371e92f5e5cced3245ba
  Running setup.py bdist_wheel for mpi4py ... done
  Stored in directory: /root/.cache/pip/wheels/a7/12/be/11b9ba83d337f1647a0fdea73fbe28a58b0593e64723233d64
  Running setup.py bdist_wheel for termcolor ... done
  Stored in directory: /root/.cache/pip/wheels/7c/06/54/bc84598ba1daf8f970247f550b175aaaee85f68b4b0c5ab2c6
  Running setup.py bdist_wheel for gast ... done
  Stored in directory: /root/.cache/pip/wheels/5c/2e/7e/a1d4d4fcebe6c381f378ce7743a3ced3699feb89bcfbdadadd
  Running setup.py bdist_wheel for wrapt ... done
  Stored in directory: /root/.cache/pip/wheels/d7/de/2e/efa132238792efb6459a96e85916ef8597fcb3d2ae51590dfd
  Running setup.py bdist_wheel for absl-py ... done
  Stored in directory: /root/.cache/pip/wheels/ee/98/38/46cbcc5a93cfea5492d19c38562691ddb23b940176c14f7b48
  Running setup.py bdist_wheel for future ... done
  Stored in directory: /root/.cache/pip/wheels/0c/61/d2/d6b7317325828fbb39ee6ad559dbe4664d0896da4721bf379e
Successfully built gym mpi4py termcolor gast wrapt absl-py future
Installing collected packages: PySimpleGUI, cloudpickle, numpy, future, pyglet, scipy, gym, python-dateutil, kiwisolver, pyparsing, cycler, matplotlib, joblib, pytz, pandas, mpi4py, opencv-python, stable-baselines, grpcio, astor, termcolor, gast, wrapt, absl-py, google-pasta, protobuf, h5py, keras-applications, werkzeug, markdown, tensorboard, tensorflow-estimator, keras-preprocessing, tensorflow, gym-film
  Running setup.py develop for gym-film
Successfully installed PySimpleGUI-4.2.0 absl-py-0.7.1 astor-0.8.0 cloudpickle-1.2.1 cycler-0.10.0 future-0.17.1 gast-0.2.2 google-pasta-0.1.7 grpcio-1.23.0 gym-0.14.0 gym-film h5py-2.9.0 joblib-0.13.2 keras-applications-1.0.8 keras-preprocessing-1.1.0 kiwisolver-1.1.0 markdown-3.1.1 matplotlib-3.1.1 mpi4py-3.0.2 numpy-1.17.0 opencv-python-4.1.0.25 pandas-0.25.0 protobuf-3.9.1 pyglet-1.3.2 pyparsing-2.4.2 python-dateutil-2.8.0 pytz-2019.2 scipy-1.3.1 stable-baselines-2.7.0 tensorboard-1.14.0 tensorflow-1.14.0 tensorflow-estimator-1.14.0 termcolor-1.1.0 werkzeug-0.15.5 wrapt-1.11.2
```

We now get the boost library, we will install it in /usr/local/
$cd /usr/local
$wget -4 https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.bz2
```
root@4d11781e476d:/usr/local# wget -4 https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.bz2
--2019-08-20 17:47:28--  https://dl.bintray.com/boostorg/release/1.67.0/source/boost_1_67_0.tar.bz2
Resolving dl.bintray.com (dl.bintray.com)... 35.158.208.55, 18.195.230.94
Connecting to dl.bintray.com (dl.bintray.com)|35.158.208.55|:443... connected.
HTTP request sent, awaiting response... 302 
Location: https://d29vzk4ow07wi7.cloudfront.net/2684c972994ee57fc5632e03bf044746f6eb45d4920c343937a465fd67a5adba?response-content-disposition=attachment%3Bfilename%3D%22boost_1_67_0.tar.bz2%22&Policy=eyJTdGF0ZW1lbnQiOiBbeyJSZXNvdXJjZSI6Imh0dHAqOi8vZDI5dnprNG93MDd3aTcuY2xvdWRmcm9udC5uZXQvMjY4NGM5NzI5OTRlZTU3ZmM1NjMyZTAzYmYwNDQ3NDZmNmViNDVkNDkyMGMzNDM5MzdhNDY1ZmQ2N2E1YWRiYT9yZXNwb25zZS1jb250ZW50LWRpc3Bvc2l0aW9uPWF0dGFjaG1lbnQlM0JmaWxlbmFtZSUzRCUyMmJvb3N0XzFfNjdfMC50YXIuYnoyJTIyIiwiQ29uZGl0aW9uIjp7IkRhdGVMZXNzVGhhbiI6eyJBV1M6RXBvY2hUaW1lIjoxNTY2MzE2NzY4fSwiSXBBZGRyZXNzIjp7IkFXUzpTb3VyY2VJcCI6IjAuMC4wLjAvMCJ9fX1dfQ__&Signature=JIYYbFs7ngGrUByS2p8bVUVe8js6rjAO-GSXoeSLumZCDf8DNRb61SCvpsaUfBFi9pRttB7ygD2l282fOUDq3WGCk-R0BRdQmX3bhtLuOFk8KrC9RKefrmhKPFO59qW-EwnHHP35A1qt4P3oBUNyHYvhCm1YVUOSpckYL9CY8GiRe0XjXkrdGVxoQNGqQlHXx9hHvm2dRmuv5AtLHRnzEPTMyW2gCO5epx0hn3Cr3C8clSEBxtDWId0QFZFDOWFOcyorZ7EnF13HQM0R1CycYQQODWrSnWHgrFrLrNF1jWxg1KHMYMKQ5eOQArj10WoWwLFui1Xxk3nSAoRzE0vB1Q__&Key-Pair-Id=APKAIFKFWOMXM2UMTSFA [following]
--2019-08-20 17:47:28--  https://d29vzk4ow07wi7.cloudfront.net/2684c972994ee57fc5632e03bf044746f6eb45d4920c343937a465fd67a5adba?response-content-disposition=attachment%3Bfilename%3D%22boost_1_67_0.tar.bz2%22&Policy=eyJTdGF0ZW1lbnQiOiBbeyJSZXNvdXJjZSI6Imh0dHAqOi8vZDI5dnprNG93MDd3aTcuY2xvdWRmcm9udC5uZXQvMjY4NGM5NzI5OTRlZTU3ZmM1NjMyZTAzYmYwNDQ3NDZmNmViNDVkNDkyMGMzNDM5MzdhNDY1ZmQ2N2E1YWRiYT9yZXNwb25zZS1jb250ZW50LWRpc3Bvc2l0aW9uPWF0dGFjaG1lbnQlM0JmaWxlbmFtZSUzRCUyMmJvb3N0XzFfNjdfMC50YXIuYnoyJTIyIiwiQ29uZGl0aW9uIjp7IkRhdGVMZXNzVGhhbiI6eyJBV1M6RXBvY2hUaW1lIjoxNTY2MzE2NzY4fSwiSXBBZGRyZXNzIjp7IkFXUzpTb3VyY2VJcCI6IjAuMC4wLjAvMCJ9fX1dfQ__&Signature=JIYYbFs7ngGrUByS2p8bVUVe8js6rjAO-GSXoeSLumZCDf8DNRb61SCvpsaUfBFi9pRttB7ygD2l282fOUDq3WGCk-R0BRdQmX3bhtLuOFk8KrC9RKefrmhKPFO59qW-EwnHHP35A1qt4P3oBUNyHYvhCm1YVUOSpckYL9CY8GiRe0XjXkrdGVxoQNGqQlHXx9hHvm2dRmuv5AtLHRnzEPTMyW2gCO5epx0hn3Cr3C8clSEBxtDWId0QFZFDOWFOcyorZ7EnF13HQM0R1CycYQQODWrSnWHgrFrLrNF1jWxg1KHMYMKQ5eOQArj10WoWwLFui1Xxk3nSAoRzE0vB1Q__&Key-Pair-Id=APKAIFKFWOMXM2UMTSFA
Resolving d29vzk4ow07wi7.cloudfront.net (d29vzk4ow07wi7.cloudfront.net)... 143.204.51.87, 143.204.51.37, 143.204.51.102, ...
Connecting to d29vzk4ow07wi7.cloudfront.net (d29vzk4ow07wi7.cloudfront.net)|143.204.51.87|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 87336566 (83M) [application/x-bzip2]
Saving to: 'boost_1_67_0.tar.bz2'

boost_1_67_0.tar.bz2                               100%[================================================================================================================>]  83.29M  8.04MB/s    in 10s     

2019-08-20 17:47:38 (8.04 MB/s) - 'boost_1_67_0.tar.bz2' saved [87336566/87336566]
```

$tar --bzip2 -xf boost_1_67_0.tar.bz2 
```
root@4d11781e476d:/usr/local# tar --bzip2 -xf boost_1_67_0.tar.bz2 
```

We need to acquire the boost_python library
$cd boost_1_67_0
$./bootstrap.sh --with-libraries=python --with-python=python3.6
$./b2
```
root@4d11781e476d:/usr/local/boost_1_67_0# ./bootstrap.sh --with-libraries=python --with-python=python3.6
Building Boost.Build engine with toolset gcc... tools/build/src/engine/bin.linuxx86_64/b2
Detecting Python version... 3.6
Detecting Python root... /usr
Unicode/ICU support for Boost.Regex?... not found.
Backing up existing Boost.Build configuration in project-config.jam.1
Generating Boost.Build configuration in project-config.jam...

Bootstrapping is done. To build, run:

    ./b2
    
To adjust configuration, edit 'project-config.jam'.
Further information:

   - Command line help:
     ./b2 --help
     
   - Getting started guide: 
     http://www.boost.org/more/getting_started/unix-variants.html
     
   - Boost.Build documentation:
     http://www.boost.org/build/doc/html/index.html

root@4d11781e476d:/usr/local/boost_1_67_0# ./b2
/usr/local/boost_1_67_0/libs/predef/check/../tools/check/predef.jam:46: Unescaped special character in argument $(language)::$(expression)
Performing configuration checks

    - default address-model    : 64-bit (cached)
    - default architecture     : x86 (cached)

Building the Boost C++ Libraries.


    - symlinks supported       : yes (cached)

Component configuration:

    - atomic                   : not building
    - chrono                   : not building
    - container                : not building
    - context                  : not building
    - contract                 : not building
    - coroutine                : not building
    - date_time                : not building
    - exception                : not building
    - fiber                    : not building
    - filesystem               : not building
    - graph                    : not building
    - graph_parallel           : not building
    - iostreams                : not building
    - locale                   : not building
    - log                      : not building
    - math                     : not building
    - mpi                      : not building
    - program_options          : not building
    - python                   : building
    - random                   : not building
    - regex                    : not building
    - serialization            : not building
    - signals                  : not building
    - stacktrace               : not building
    - system                   : not building
    - test                     : not building
    - thread                   : not building
    - timer                    : not building
    - type_erasure             : not building
    - wave                     : not building

...patience...
...patience...
...found 3398 targets...
...updating 93 targets...
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/list.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/list.hpp:10,
                 from libs/python/src/list.cpp:5:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/list.hpp:10,
                 from libs/python/src/list.cpp:5:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/long.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/long.hpp:10,
                 from libs/python/src/long.cpp:5:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/long.hpp:10,
                 from libs/python/src/long.cpp:5:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/dict.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/dict.hpp:10,
                 from libs/python/src/dict.cpp:4:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/dict.hpp:10,
                 from libs/python/src/dict.cpp:4:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
In file included from libs/python/src/dict.cpp:5:0:
./boost/python/extract.hpp: In member function 'bool boost::python::detail::dict_base::has_key(boost::python::api::object_operators<boost::python::api::object>::object_cref) const':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/tuple.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/tuple.hpp:10,
                 from libs/python/src/tuple.cpp:5:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/tuple.hpp:10,
                 from libs/python/src/tuple.cpp:5:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/str.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/str.hpp:10,
                 from libs/python/src/str.cpp:4:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/str.hpp:10,
                 from libs/python/src/str.cpp:4:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
In file included from libs/python/src/str.cpp:5:0:
./boost/python/extract.hpp: In member function 'long int boost::python::detail::str_base::count(boost::python::api::object_operators<boost::python::api::object>::object_cref) const':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
./boost/python/extract.hpp: In member function 'long int boost::python::detail::str_base::count(boost::python::api::object_operators<boost::python::api::object>::object_cref, boost::python::api::object_operators<boost::python::api::object>::object_cref) const':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
./boost/python/extract.hpp: In member function 'long int boost::python::detail::str_base::count(boost::python::api::object_operators<boost::python::api::object>::object_cref, boost::python::api::object_operators<boost::python::api::object>::object_cref, boost::python::api::object_operators<boost::python::api::object>::object_cref) const':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/slice.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/slice.hpp:11,
                 from libs/python/src/slice.cpp:1:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/slice.hpp:11,
                 from libs/python/src/slice.cpp:1:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/converter/from_python.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/converter/registry.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/converter/type_id.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/object/enum.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/enum_base.hpp:8,
                 from libs/python/src/object/enum.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/enum_base.hpp:8,
                 from libs/python/src/object/enum.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/object/class.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/class.hpp:9,
                 from libs/python/src/object/class.cpp:9:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/class.hpp:9,
                 from libs/python/src/object/class.cpp:9:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/object/function.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/function.hpp:12,
                 from ./boost/python/docstring_options.hpp:8,
                 from libs/python/src/object/function.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/object/function.hpp:9,
                 from ./boost/python/docstring_options.hpp:8,
                 from libs/python/src/object/function.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/object/inheritance.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/object/life_support.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/object/pickle_support.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/value_is_xxx.hpp:13,
                 from ./boost/python/detail/value_is_shared_ptr.hpp:10,
                 from ./boost/python/to_python_value.hpp:23,
                 from ./boost/python/default_call_policies.hpp:10,
                 from ./boost/python/make_function.hpp:10,
                 from libs/python/src/object/pickle_support.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/to_python_value.hpp:14,
                 from ./boost/python/default_call_policies.hpp:10,
                 from ./boost/python/make_function.hpp:10,
                 from libs/python/src/object/pickle_support.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/errors.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/module.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/scope.hpp:9,
                 from libs/python/src/module.cpp:9:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/scope.hpp:9,
                 from libs/python/src/module.cpp:9:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/converter/builtin_converters.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/converter/arg_to_python_base.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/object/iterator.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/function_object.hpp:9,
                 from libs/python/src/object/iterator.cpp:7:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:29,
                 from ./boost/function/function2.hpp:11,
                 from ./boost/python/object/function_object.hpp:8,
                 from libs/python/src/object/iterator.cpp:7:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/object/stl_iterator.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from libs/python/src/object/stl_iterator.cpp:10:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from libs/python/src/object/stl_iterator.cpp:10:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/object_protocol.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object_protocol.hpp:11,
                 from libs/python/src/object_protocol.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object_protocol.hpp:11,
                 from libs/python/src/object_protocol.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/object_operators.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object_operators.hpp:10,
                 from libs/python/src/object_operators.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object_operators.hpp:10,
                 from libs/python/src/object_operators.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/wrapper.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/extract.hpp:16,
                 from ./boost/python/override.hpp:13,
                 from ./boost/python/wrapper.hpp:8,
                 from libs/python/src/wrapper.cpp:5:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/python/converter/registered.hpp:16,
                 from ./boost/python/converter/return_from_python.hpp:10,
                 from ./boost/python/override.hpp:11,
                 from ./boost/python/wrapper.hpp:8,
                 from libs/python/src/wrapper.cpp:5:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/import.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/import.hpp:8,
                 from libs/python/src/import.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/import.hpp:8,
                 from libs/python/src/import.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/exec.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/exec.hpp:8,
                 from libs/python/src/exec.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/exec.hpp:8,
                 from libs/python/src/exec.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/object/function_doc_signature.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/function.hpp:12,
                 from ./boost/python/object/function_doc_signature.hpp:8,
                 from libs/python/src/object/function_doc_signature.cpp:10:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/object/function.hpp:9,
                 from ./boost/python/object/function_doc_signature.hpp:8,
                 from libs/python/src/object/function_doc_signature.cpp:10:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.link.dll bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/libboost_python36.so.1.67.0
common.copy stage/lib/libboost_python36.so.1.67.0
ln-UNIX stage/lib/libboost_python36.so
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/numpy/dtype.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/dtype.cpp:11:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/dtype.cpp:11:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/numpy/matrix.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/matrix.cpp:8:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/matrix.cpp:8:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/numpy/ndarray.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/ndarray.cpp:8:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/ndarray.cpp:8:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
In file included from ./boost/python/override.hpp:13:0,
                 from ./boost/python/wrapper.hpp:8,
                 from ./boost/python/object/value_holder.hpp:15,
                 from ./boost/python/object/class_metadata.hpp:14,
                 from ./boost/python/class.hpp:23,
                 from ./boost/python.hpp:18,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/ndarray.cpp:8:
./boost/python/extract.hpp: In function 'boost::python::numpy::ndarray boost::python::numpy::detail::from_data_impl(void*, const boost::python::numpy::dtype&, const boost::python::api::object&, const boost::python::api::object&, const boost::python::api::object&, bool)':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
./boost/python/extract.hpp: In function 'boost::python::numpy::ndarray boost::python::numpy::zeros(const boost::python::tuple&, const boost::python::numpy::dtype&)':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
./boost/python/extract.hpp: In function 'boost::python::numpy::ndarray boost::python::numpy::empty(const boost::python::tuple&, const boost::python::numpy::dtype&)':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/numpy/numpy.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/numpy.cpp:8:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/numpy.cpp:8:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
libs/python/src/numpy/numpy.cpp: In function 'void* boost::python::numpy::wrap_import_array()':
libs/python/src/numpy/numpy.cpp:22:1: warning: control reaches end of non-void function [-Wreturn-type]
 }
 ^
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/numpy/scalars.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/scalars.cpp:8:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/scalars.cpp:8:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/numpy/ufunc.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/ufunc.cpp:8:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/ufunc.cpp:8:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.link.dll bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi/libboost_numpy36.so.1.67.0
common.copy stage/lib/libboost_numpy36.so.1.67.0
ln-UNIX stage/lib/libboost_numpy36.so
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/list.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/list.hpp:10,
                 from libs/python/src/list.cpp:5:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/list.hpp:10,
                 from libs/python/src/list.cpp:5:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/long.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/long.hpp:10,
                 from libs/python/src/long.cpp:5:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/long.hpp:10,
                 from libs/python/src/long.cpp:5:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/dict.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/dict.hpp:10,
                 from libs/python/src/dict.cpp:4:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/dict.hpp:10,
                 from libs/python/src/dict.cpp:4:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
In file included from libs/python/src/dict.cpp:5:0:
./boost/python/extract.hpp: In member function 'bool boost::python::detail::dict_base::has_key(boost::python::api::object_operators<boost::python::api::object>::object_cref) const':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/tuple.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/tuple.hpp:10,
                 from libs/python/src/tuple.cpp:5:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/tuple.hpp:10,
                 from libs/python/src/tuple.cpp:5:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/str.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/str.hpp:10,
                 from libs/python/src/str.cpp:4:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/str.hpp:10,
                 from libs/python/src/str.cpp:4:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
In file included from libs/python/src/str.cpp:5:0:
./boost/python/extract.hpp: In member function 'long int boost::python::detail::str_base::count(boost::python::api::object_operators<boost::python::api::object>::object_cref) const':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
./boost/python/extract.hpp: In member function 'long int boost::python::detail::str_base::count(boost::python::api::object_operators<boost::python::api::object>::object_cref, boost::python::api::object_operators<boost::python::api::object>::object_cref) const':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
./boost/python/extract.hpp: In member function 'long int boost::python::detail::str_base::count(boost::python::api::object_operators<boost::python::api::object>::object_cref, boost::python::api::object_operators<boost::python::api::object>::object_cref, boost::python::api::object_operators<boost::python::api::object>::object_cref) const':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/slice.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/slice.hpp:11,
                 from libs/python/src/slice.cpp:1:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/slice.hpp:11,
                 from libs/python/src/slice.cpp:1:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/converter/from_python.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/converter/registry.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/converter/type_id.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/object/enum.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/enum_base.hpp:8,
                 from libs/python/src/object/enum.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/enum_base.hpp:8,
                 from libs/python/src/object/enum.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/object/class.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/class.hpp:9,
                 from libs/python/src/object/class.cpp:9:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/class.hpp:9,
                 from libs/python/src/object/class.cpp:9:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/object/function.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/function.hpp:12,
                 from ./boost/python/docstring_options.hpp:8,
                 from libs/python/src/object/function.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/object/function.hpp:9,
                 from ./boost/python/docstring_options.hpp:8,
                 from libs/python/src/object/function.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/object/inheritance.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/object/life_support.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/object/pickle_support.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/value_is_xxx.hpp:13,
                 from ./boost/python/detail/value_is_shared_ptr.hpp:10,
                 from ./boost/python/to_python_value.hpp:23,
                 from ./boost/python/default_call_policies.hpp:10,
                 from ./boost/python/make_function.hpp:10,
                 from libs/python/src/object/pickle_support.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/to_python_value.hpp:14,
                 from ./boost/python/default_call_policies.hpp:10,
                 from ./boost/python/make_function.hpp:10,
                 from libs/python/src/object/pickle_support.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/errors.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/module.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/scope.hpp:9,
                 from libs/python/src/module.cpp:9:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/scope.hpp:9,
                 from libs/python/src/module.cpp:9:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/converter/builtin_converters.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/converter/arg_to_python_base.o
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/object/iterator.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/function_object.hpp:9,
                 from libs/python/src/object/iterator.cpp:7:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:29,
                 from ./boost/function/function2.hpp:11,
                 from ./boost/python/object/function_object.hpp:8,
                 from libs/python/src/object/iterator.cpp:7:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/object/stl_iterator.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from libs/python/src/object/stl_iterator.cpp:10:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from libs/python/src/object/stl_iterator.cpp:10:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/object_protocol.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object_protocol.hpp:11,
                 from libs/python/src/object_protocol.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object_protocol.hpp:11,
                 from libs/python/src/object_protocol.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/object_operators.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object_operators.hpp:10,
                 from libs/python/src/object_operators.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object_operators.hpp:10,
                 from libs/python/src/object_operators.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/wrapper.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/extract.hpp:16,
                 from ./boost/python/override.hpp:13,
                 from ./boost/python/wrapper.hpp:8,
                 from libs/python/src/wrapper.cpp:5:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/python/converter/registered.hpp:16,
                 from ./boost/python/converter/return_from_python.hpp:10,
                 from ./boost/python/override.hpp:11,
                 from ./boost/python/wrapper.hpp:8,
                 from libs/python/src/wrapper.cpp:5:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/import.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/import.hpp:8,
                 from libs/python/src/import.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/import.hpp:8,
                 from libs/python/src/import.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/exec.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/exec.hpp:8,
                 from libs/python/src/exec.cpp:6:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/config/no_tr1/memory.hpp:21,
                 from ./boost/get_pointer.hpp:14,
                 from ./boost/python/object/pointer_holder.hpp:11,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object.hpp:9,
                 from ./boost/python/exec.hpp:8,
                 from libs/python/src/exec.cpp:6:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/object/function_doc_signature.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/object/function.hpp:12,
                 from ./boost/python/object/function_doc_signature.hpp:8,
                 from libs/python/src/object/function_doc_signature.cpp:10:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/object/function.hpp:9,
                 from ./boost/python/object/function_doc_signature.hpp:8,
                 from libs/python/src/object/function_doc_signature.cpp:10:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.archive bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/libboost_python36.a
common.copy stage/lib/libboost_python36.a
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/numpy/dtype.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/dtype.cpp:11:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/dtype.cpp:11:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/numpy/matrix.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/matrix.cpp:8:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/matrix.cpp:8:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/numpy/ndarray.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/ndarray.cpp:8:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/ndarray.cpp:8:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
In file included from ./boost/python/override.hpp:13:0,
                 from ./boost/python/wrapper.hpp:8,
                 from ./boost/python/object/value_holder.hpp:15,
                 from ./boost/python/object/class_metadata.hpp:14,
                 from ./boost/python/class.hpp:23,
                 from ./boost/python.hpp:18,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/ndarray.cpp:8:
./boost/python/extract.hpp: In function 'boost::python::numpy::ndarray boost::python::numpy::detail::from_data_impl(void*, const boost::python::numpy::dtype&, const boost::python::api::object&, const boost::python::api::object&, const boost::python::api::object&, bool)':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
./boost/python/extract.hpp: In function 'boost::python::numpy::ndarray boost::python::numpy::zeros(const boost::python::tuple&, const boost::python::numpy::dtype&)':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
./boost/python/extract.hpp: In function 'boost::python::numpy::ndarray boost::python::numpy::empty(const boost::python::tuple&, const boost::python::numpy::dtype&)':
./boost/python/extract.hpp:185:11: warning: '*((void*)&<anonymous> +24)' may be used uninitialized in this function [-Wmaybe-uninitialized]
           );
           ^
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/numpy/numpy.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/numpy.cpp:8:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/numpy.cpp:8:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
libs/python/src/numpy/numpy.cpp: In function 'void* boost::python::numpy::wrap_import_array()':
libs/python/src/numpy/numpy.cpp:22:1: warning: control reaches end of non-void function [-Wreturn-type]
 }
 ^
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/numpy/scalars.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/scalars.cpp:8:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/scalars.cpp:8:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.compile.c++ bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/numpy/ufunc.o
In file included from ./boost/python/detail/is_xxx.hpp:8:0,
                 from ./boost/python/detail/is_auto_ptr.hpp:9,
                 from ./boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from ./boost/python/detail/value_arg.hpp:7,
                 from ./boost/python/object/forward.hpp:10,
                 from ./boost/python/object/pointer_holder.hpp:16,
                 from ./boost/python/to_python_indirect.hpp:10,
                 from ./boost/python/converter/arg_to_python.hpp:10,
                 from ./boost/python/call.hpp:15,
                 from ./boost/python/object_core.hpp:14,
                 from ./boost/python/args.hpp:22,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/ufunc.cpp:8:
./boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
./boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
./boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from ./boost/function/function_base.hpp:16,
                 from ./boost/function/detail/prologue.hpp:17,
                 from ./boost/function/function_template.hpp:13,
                 from ./boost/function/detail/maybe_include.hpp:15,
                 from ./boost/function/function0.hpp:11,
                 from ./boost/python/errors.hpp:13,
                 from ./boost/python/handle.hpp:11,
                 from ./boost/python/args_fwd.hpp:10,
                 from ./boost/python/args.hpp:10,
                 from ./boost/python.hpp:11,
                 from ./boost/python/numpy/internal.hpp:17,
                 from libs/python/src/numpy/ufunc.cpp:8:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
gcc.archive bin.v2/libs/python/build/gcc-7.4.0/release/link-static/threading-multi/libboost_numpy36.a
common.copy stage/lib/libboost_numpy36.a
link.mklink boost/chrono/stopwatches.hpp
mklink-or-dir boost/chrono/stopwatches
...updated 93 targets...


The Boost C++ Libraries were successfully built!

The following directory should be added to compiler include paths:

    /usr/local/boost_1_67_0

The following directory should be added to linker library paths:

    /usr/local/boost_1_67_0/stage/lib
```

You need to let the linker know the path to the library libboost_numpy36.so.1.67.0
$export LD_LIBRARY_PATH=/usr/local/boost_1_67_0/bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi:$LD_LIBRARY_PATH
```
root@4d11781e476d:~/drl_film_fluid/drl_fluid_film_python3/gym-film# export LD_LIBRARY_PATH=/usr/local/boost_1_67_0/bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi:$LD_LIBRARY_PATH
```

Now we need to make sure the python/cpp bridge in our simulation solver is well built
$cd ~/drl_film_fluid/drl_fluid_film_python3/gym-film/gym_film/envs/simulation_solver
$make clean
$make
```
root@4d11781e476d:~/drl_film_fluid/drl_fluid_film_python3/gym-film/gym_film/envs/simulation_solver# make clean
rm simulation_cpp.o advect_in_time.o TVD3.o cpp.so
rm: cannot remove 'cpp.so': No such file or directory
makefile:21: recipe for target 'clean' failed
make: *** [clean] Error 1
root@4d11781e476d:~/drl_film_fluid/drl_fluid_film_python3/gym-film/gym_film/envs/simulation_solver# make
g++ -fPIC -o simulation_cpp.o -c simulation_cpp.cpp -I/usr/include/python3.6 -I/usr/local/boost_1_67_0 -I/usr/local/boost_1_67_0/stage/lib -I/usr/local/boost_1_67_0/bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi -std=c++11 -Ofast -march=native -flto
In file included from /usr/local/boost_1_67_0/boost/python/detail/is_xxx.hpp:8:0,
                 from /usr/local/boost_1_67_0/boost/python/detail/is_auto_ptr.hpp:9,
                 from /usr/local/boost_1_67_0/boost/python/detail/copy_ctor_mutates_rhs.hpp:8,
                 from /usr/local/boost_1_67_0/boost/python/detail/value_arg.hpp:7,
                 from /usr/local/boost_1_67_0/boost/python/object/forward.hpp:10,
                 from /usr/local/boost_1_67_0/boost/python/object/pointer_holder.hpp:16,
                 from /usr/local/boost_1_67_0/boost/python/to_python_indirect.hpp:10,
                 from /usr/local/boost_1_67_0/boost/python/converter/arg_to_python.hpp:10,
                 from /usr/local/boost_1_67_0/boost/python/call.hpp:15,
                 from /usr/local/boost_1_67_0/boost/python/object_core.hpp:14,
                 from /usr/local/boost_1_67_0/boost/python/args.hpp:22,
                 from /usr/local/boost_1_67_0/boost/python.hpp:11,
                 from simulation_cpp.cpp:1:
/usr/local/boost_1_67_0/boost/python/detail/is_auto_ptr.hpp:17:40: warning: 'template<class> class std::auto_ptr' is deprecated [-Wdeprecated-declarations]
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
                                        ^
/usr/local/boost_1_67_0/boost/detail/is_xxx.hpp:20:4: note: in definition of macro 'BOOST_DETAIL_IS_XXX_DEF'
    qualified_name< BOOST_PP_ENUM_PARAMS_Z(1, nargs, T) >        \
    ^~~~~~~~~~~~~~
/usr/local/boost_1_67_0/boost/python/detail/is_auto_ptr.hpp:17:1: note: in expansion of macro 'BOOST_PYTHON_IS_XXX_DEF'
 BOOST_PYTHON_IS_XXX_DEF(auto_ptr, std::auto_ptr, 1)
 ^~~~~~~~~~~~~~~~~~~~~~~
In file included from /usr/include/c++/7/memory:80:0,
                 from /usr/local/boost_1_67_0/boost/function/function_base.hpp:16,
                 from /usr/local/boost_1_67_0/boost/function/detail/prologue.hpp:17,
                 from /usr/local/boost_1_67_0/boost/function/function_template.hpp:13,
                 from /usr/local/boost_1_67_0/boost/function/detail/maybe_include.hpp:15,
                 from /usr/local/boost_1_67_0/boost/function/function0.hpp:11,
                 from /usr/local/boost_1_67_0/boost/python/errors.hpp:13,
                 from /usr/local/boost_1_67_0/boost/python/handle.hpp:11,
                 from /usr/local/boost_1_67_0/boost/python/args_fwd.hpp:10,
                 from /usr/local/boost_1_67_0/boost/python/args.hpp:10,
                 from /usr/local/boost_1_67_0/boost/python.hpp:11,
                 from simulation_cpp.cpp:1:
/usr/include/c++/7/bits/unique_ptr.h:51:28: note: declared here
   template<typename> class auto_ptr;
                            ^~~~~~~~
g++ -fPIC -o TVD3.o -c TVD3.cpp -I/usr/include/python3.6 -I/usr/local/boost_1_67_0 -I/usr/local/boost_1_67_0/stage/lib -I/usr/local/boost_1_67_0/bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi -std=c++11 -Ofast -march=native -flto
g++ -fPIC -o advect_in_time.o -c advect_in_time.cpp -I/usr/include/python3.6 -I/usr/local/boost_1_67_0 -I/usr/local/boost_1_67_0/stage/lib -I/usr/local/boost_1_67_0/bin.v2/libs/python/build/gcc-7.4.0/release/threading-multi -std=c++11 -Ofast -march=native -flto
g++ -shared -o cpp.so simulation_cpp.o TVD3.o advect_in_time.o -L/usr/local/boost_1_67_0/stage/lib -lpython3.6m -lboost_numpy36 -std=c++11 -Ofast -march=native -flto
```
That's it, the environment is ready for trainings !
