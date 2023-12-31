# Building and deploying simple application using GUI

Login to Openshift console as labuserX, where X is your lab user number:
https://console-openshift-console.apps.yyy.yyy.yy/
with htpasswd provider.

1. Switch to developer view.
2. Select +Add and From Git repository.
3. Git Repo URL: https://github.com/michalteofan/labuser0.git
4. Application name: labuserXapp1
5. Name: labuserXapp1
6. Click Create

You can watch build progress in Build Detais and Logs tab. When the build is complied, go to Topology view and select the application. 
```
Cloning "https://github.com/michalteofan/labuser0.git" ...
	Commit:	b7e4355c9fd5f72c92b9500e55890d086bbb01e9 (focal)
	Author:	Michal <michal@pl.ibm.com>
	Date:	Mon Sep 18 12:11:05 2023 +0200
time="2023-09-18T10:11:40Z" level=info msg="Not using native diff for overlay, this may cause degraded performance for building images: kernel has CONFIG_OVERLAY_FS_REDIRECT_DIR enabled"
I0918 10:11:40.795525       1 defaults.go:112] Defaulting to storage driver "overlay" with options [mountopt=metacopy=on].
Caching blobs under "/var/cache/blobs".

Pulling image docker.io/ppc64le/ubuntu:focal ...
Trying to pull docker.io/ppc64le/ubuntu:focal...
Getting image source signatures
Copying blob sha256:fa78ce4014add322eddde3378405efe21c85e886c0195e18533d5991d5477833
Copying config sha256:a92643ae09f6e607311cb05e4f0f7679c0873b7e4c235e1b57f5e409cfc47c50
Writing manifest to image destination
Storing signatures
Adding transient rw bind mount for /run/secrets/rhsm
STEP 1/20: FROM docker.io/ppc64le/ubuntu:focal
STEP 2/20: ENV TZ=Europe/Warsaw
--> 33b0b7df89d
STEP 3/20: RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
--> 221a8b4d6b6
STEP 4/20: RUN apt-get update && apt-get install -y apache2
Get:1 http://ports.ubuntu.com/ubuntu-ports focal InRelease [265 kB]
Get:2 http://ports.ubuntu.com/ubuntu-ports focal-updates InRelease [114 kB]
Get:3 http://ports.ubuntu.com/ubuntu-ports focal-backports InRelease [108 kB]
Get:4 http://ports.ubuntu.com/ubuntu-ports focal-security InRelease [114 kB]
Get:5 http://ports.ubuntu.com/ubuntu-ports focal/multiverse ppc64el Packages [146 kB]
Get:6 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el Packages [1229 kB]
Get:7 http://ports.ubuntu.com/ubuntu-ports focal/restricted ppc64el Packages [1317 B]
Get:8 http://ports.ubuntu.com/ubuntu-ports focal/universe ppc64el Packages [11.0 MB]
Get:9 http://ports.ubuntu.com/ubuntu-ports focal-updates/restricted ppc64el Packages [6671 B]
Get:10 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el Packages [1556 kB]
Get:11 http://ports.ubuntu.com/ubuntu-ports focal-updates/multiverse ppc64el Packages [5633 B]
Get:12 http://ports.ubuntu.com/ubuntu-ports focal-updates/universe ppc64el Packages [1254 kB]
Get:13 http://ports.ubuntu.com/ubuntu-ports focal-backports/universe ppc64el Packages [27.8 kB]
Get:14 http://ports.ubuntu.com/ubuntu-ports focal-backports/main ppc64el Packages [54.8 kB]
Get:15 http://ports.ubuntu.com/ubuntu-ports focal-security/multiverse ppc64el Packages [3262 B]
Get:16 http://ports.ubuntu.com/ubuntu-ports focal-security/main ppc64el Packages [1191 kB]
Get:17 http://ports.ubuntu.com/ubuntu-ports focal-security/universe ppc64el Packages [969 kB]
Get:18 http://ports.ubuntu.com/ubuntu-ports focal-security/restricted ppc64el Packages [6435 B]
Fetched 18.1 MB in 3s (6651 kB/s)
Reading package lists...
Reading package lists...
Building dependency tree...
Reading state information...
The following additional packages will be installed:
  apache2-bin apache2-data apache2-utils ca-certificates file krb5-locales
  libapr1 libaprutil1 libaprutil1-dbd-sqlite3 libaprutil1-ldap
  libasn1-8-heimdal libbrotli1 libcurl4 libexpat1 libgdbm-compat4 libgdbm6
  libgssapi-krb5-2 libgssapi3-heimdal libhcrypto4-heimdal libheimbase1-heimdal
  libheimntlm0-heimdal libhx509-5-heimdal libicu66 libjansson4 libk5crypto3
  libkeyutils1 libkrb5-26-heimdal libkrb5-3 libkrb5support0 libldap-2.4-2
  libldap-common liblua5.2-0 libmagic-mgc libmagic1 libnghttp2-14 libperl5.30
  libpsl5 libroken18-heimdal librtmp1 libsasl2-2 libsasl2-modules
  libsasl2-modules-db libsqlite3-0 libssh-4 libssl1.1 libwind0-heimdal libxml2
  mime-support netbase openssl perl perl-modules-5.30 publicsuffix ssl-cert
  tzdata xz-utils
Suggested packages:
  apache2-doc apache2-suexec-pristine | apache2-suexec-custom www-browser ufw
  gdbm-l10n krb5-doc krb5-user libsasl2-modules-gssapi-mit
  | libsasl2-modules-gssapi-heimdal libsasl2-modules-ldap libsasl2-modules-otp
  libsasl2-modules-sql perl-doc libterm-readline-gnu-perl
  | libterm-readline-perl-perl make libb-debug-perl liblocale-codes-perl
  openssl-blacklist
The following NEW packages will be installed:
  apache2 apache2-bin apache2-data apache2-utils ca-certificates file
  krb5-locales libapr1 libaprutil1 libaprutil1-dbd-sqlite3 libaprutil1-ldap
  libasn1-8-heimdal libbrotli1 libcurl4 libexpat1 libgdbm-compat4 libgdbm6
  libgssapi-krb5-2 libgssapi3-heimdal libhcrypto4-heimdal libheimbase1-heimdal
  libheimntlm0-heimdal libhx509-5-heimdal libicu66 libjansson4 libk5crypto3
  libkeyutils1 libkrb5-26-heimdal libkrb5-3 libkrb5support0 libldap-2.4-2
  libldap-common liblua5.2-0 libmagic-mgc libmagic1 libnghttp2-14 libperl5.30
  libpsl5 libroken18-heimdal librtmp1 libsasl2-2 libsasl2-modules
  libsasl2-modules-db libsqlite3-0 libssh-4 libssl1.1 libwind0-heimdal libxml2
  mime-support netbase openssl perl perl-modules-5.30 publicsuffix ssl-cert
  tzdata xz-utils
0 upgraded, 57 newly installed, 0 to remove and 0 not upgraded.
Need to get 24.7 MB of archives.
After this operation, 133 MB of additional disk space will be used.
Get:1 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el perl-modules-5.30 all 5.30.0-9ubuntu0.4 [2739 kB]
Get:2 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el libgdbm6 ppc64el 1.18.1-5 [30.8 kB]
Get:3 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el libgdbm-compat4 ppc64el 1.18.1-5 [6692 B]
Get:4 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libperl5.30 ppc64el 5.30.0-9ubuntu0.4 [3911 kB]
Get:5 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el perl ppc64el 5.30.0-9ubuntu0.4 [224 kB]
Get:6 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el libapr1 ppc64el 1.6.5-1ubuntu1 [106 kB]
Get:7 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libexpat1 ppc64el 2.2.9-1ubuntu0.6 [77.7 kB]
Get:8 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libssl1.1 ppc64el 1.1.1f-1ubuntu2.19 [1362 kB]
Get:9 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libaprutil1 ppc64el 1.6.1-4ubuntu2.2 [100 kB]
Get:10 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libsqlite3-0 ppc64el 3.31.1-4ubuntu0.5 [577 kB]
Get:11 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libaprutil1-dbd-sqlite3 ppc64el 1.6.1-4ubuntu2.2 [11.7 kB]
Get:12 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libroken18-heimdal ppc64el 7.7.0+dfsg-1ubuntu1.4 [47.3 kB]
Get:13 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libasn1-8-heimdal ppc64el 7.7.0+dfsg-1ubuntu1.4 [176 kB]
Get:14 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libheimbase1-heimdal ppc64el 7.7.0+dfsg-1ubuntu1.4 [33.2 kB]
Get:15 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libhcrypto4-heimdal ppc64el 7.7.0+dfsg-1ubuntu1.4 [108 kB]
Get:16 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libwind0-heimdal ppc64el 7.7.0+dfsg-1ubuntu1.4 [48.8 kB]
Get:17 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libhx509-5-heimdal ppc64el 7.7.0+dfsg-1ubuntu1.4 [120 kB]
Get:18 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libkrb5-26-heimdal ppc64el 7.7.0+dfsg-1ubuntu1.4 [234 kB]
Get:19 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libheimntlm0-heimdal ppc64el 7.7.0+dfsg-1ubuntu1.4 [17.4 kB]
Get:20 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libgssapi3-heimdal ppc64el 7.7.0+dfsg-1ubuntu1.4 [105 kB]
Get:21 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libsasl2-modules-db ppc64el 2.1.27+dfsg-2ubuntu0.1 [16.6 kB]
Get:22 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libsasl2-2 ppc64el 2.1.27+dfsg-2ubuntu0.1 [60.2 kB]
Get:23 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libldap-common all 2.4.49+dfsg-2ubuntu1.9 [16.6 kB]
Get:24 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libldap-2.4-2 ppc64el 2.4.49+dfsg-2ubuntu1.9 [175 kB]
Get:25 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libaprutil1-ldap ppc64el 1.6.1-4ubuntu2.2 [8952 B]
Get:26 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libbrotli1 ppc64el 1.0.7-6ubuntu0.1 [292 kB]
Get:27 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libkrb5support0 ppc64el 1.17-6ubuntu4.3 [35.0 kB]
Get:28 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libk5crypto3 ppc64el 1.17-6ubuntu4.3 [102 kB]
Get:29 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libkeyutils1 ppc64el 1.6-6ubuntu1.1 [11.4 kB]
Get:30 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libkrb5-3 ppc64el 1.17-6ubuntu4.3 [371 kB]
Get:31 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libgssapi-krb5-2 ppc64el 1.17-6ubuntu4.3 [135 kB]
Get:32 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libnghttp2-14 ppc64el 1.40.0-1ubuntu0.1 [92.1 kB]
Get:33 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el libpsl5 ppc64el 0.21.0-1ubuntu1 [53.2 kB]
Get:34 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el librtmp1 ppc64el 2.4+20151223.gitfa8646d.1-2build1 [59.3 kB]
Get:35 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libssh-4 ppc64el 0.9.3-2ubuntu2.3 [195 kB]
Get:36 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libcurl4 ppc64el 7.68.0-1ubuntu2.19 [257 kB]
Get:37 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el libjansson4 ppc64el 2.12-1build1 [35.6 kB]
Get:38 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el liblua5.2-0 ppc64el 5.2.4-1.1build3 [131 kB]
Get:39 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el tzdata all 2023c-0ubuntu0.20.04.2 [301 kB]
Get:40 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libicu66 ppc64el 66.1-2ubuntu2.1 [8597 kB]
Get:41 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libxml2 ppc64el 2.9.10+dfsg-5ubuntu0.20.04.6 [670 kB]
Get:42 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el apache2-bin ppc64el 2.4.41-4ubuntu3.14 [1274 kB]
Get:43 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el apache2-data all 2.4.41-4ubuntu3.14 [158 kB]
Get:44 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el apache2-utils ppc64el 2.4.41-4ubuntu3.14 [86.8 kB]
Get:45 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el mime-support all 3.64ubuntu1 [30.6 kB]
Get:46 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el apache2 ppc64el 2.4.41-4ubuntu3.14 [95.6 kB]
Get:47 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el openssl ppc64el 1.1.1f-1ubuntu2.19 [621 kB]
Get:48 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el ca-certificates all 20230311ubuntu0.20.04.1 [152 kB]
Get:49 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el libmagic-mgc ppc64el 1:5.38-4 [218 kB]
Get:50 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el libmagic1 ppc64el 1:5.38-4 [93.1 kB]
Get:51 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el file ppc64el 1:5.38-4 [24.2 kB]
Get:52 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el netbase all 6.1 [13.1 kB]
Get:53 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el xz-utils ppc64el 5.2.4-1ubuntu1.1 [86.4 kB]
Get:54 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el krb5-locales all 1.17-6ubuntu4.3 [11.6 kB]
Get:55 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el publicsuffix all 20200303.0012-1 [111 kB]
Get:56 http://ports.ubuntu.com/ubuntu-ports focal-updates/main ppc64el libsasl2-modules ppc64el 2.1.27+dfsg-2ubuntu0.1 [58.4 kB]
Get:57 http://ports.ubuntu.com/ubuntu-ports focal/main ppc64el ssl-cert all 1.0.39 [17.0 kB]
debconf: delaying package configuration, since apt-utils is not installed
Fetched 24.7 MB in 4s (6791 kB/s)
Selecting previously unselected package perl-modules-5.30.
(Reading database ... 
(Reading database ... 5%
(Reading database ... 10%
(Reading database ... 15%
(Reading database ... 20%
(Reading database ... 25%
(Reading database ... 30%
(Reading database ... 35%
(Reading database ... 40%
(Reading database ... 45%
(Reading database ... 50%
(Reading database ... 55%
(Reading database ... 60%
(Reading database ... 65%
(Reading database ... 70%
(Reading database ... 75%
(Reading database ... 80%
(Reading database ... 85%
(Reading database ... 90%
(Reading database ... 95%
(Reading database ... 100%
(Reading database ... 4126 files and directories currently installed.)
Preparing to unpack .../00-perl-modules-5.30_5.30.0-9ubuntu0.4_all.deb ...
Unpacking perl-modules-5.30 (5.30.0-9ubuntu0.4) ...
Selecting previously unselected package libgdbm6:ppc64el.
Preparing to unpack .../01-libgdbm6_1.18.1-5_ppc64el.deb ...
Unpacking libgdbm6:ppc64el (1.18.1-5) ...
Selecting previously unselected package libgdbm-compat4:ppc64el.
Preparing to unpack .../02-libgdbm-compat4_1.18.1-5_ppc64el.deb ...
Unpacking libgdbm-compat4:ppc64el (1.18.1-5) ...
Selecting previously unselected package libperl5.30:ppc64el.
Preparing to unpack .../03-libperl5.30_5.30.0-9ubuntu0.4_ppc64el.deb ...
Unpacking libperl5.30:ppc64el (5.30.0-9ubuntu0.4) ...
Selecting previously unselected package perl.
Preparing to unpack .../04-perl_5.30.0-9ubuntu0.4_ppc64el.deb ...
Unpacking perl (5.30.0-9ubuntu0.4) ...
Selecting previously unselected package libapr1:ppc64el.
Preparing to unpack .../05-libapr1_1.6.5-1ubuntu1_ppc64el.deb ...
Unpacking libapr1:ppc64el (1.6.5-1ubuntu1) ...
Selecting previously unselected package libexpat1:ppc64el.
Preparing to unpack .../06-libexpat1_2.2.9-1ubuntu0.6_ppc64el.deb ...
Unpacking libexpat1:ppc64el (2.2.9-1ubuntu0.6) ...
Selecting previously unselected package libssl1.1:ppc64el.
Preparing to unpack .../07-libssl1.1_1.1.1f-1ubuntu2.19_ppc64el.deb ...
Unpacking libssl1.1:ppc64el (1.1.1f-1ubuntu2.19) ...
Selecting previously unselected package libaprutil1:ppc64el.
Preparing to unpack .../08-libaprutil1_1.6.1-4ubuntu2.2_ppc64el.deb ...
Unpacking libaprutil1:ppc64el (1.6.1-4ubuntu2.2) ...
Selecting previously unselected package libsqlite3-0:ppc64el.
Preparing to unpack .../09-libsqlite3-0_3.31.1-4ubuntu0.5_ppc64el.deb ...
Unpacking libsqlite3-0:ppc64el (3.31.1-4ubuntu0.5) ...
Selecting previously unselected package libaprutil1-dbd-sqlite3:ppc64el.
Preparing to unpack .../10-libaprutil1-dbd-sqlite3_1.6.1-4ubuntu2.2_ppc64el.deb ...
Unpacking libaprutil1-dbd-sqlite3:ppc64el (1.6.1-4ubuntu2.2) ...
Selecting previously unselected package libroken18-heimdal:ppc64el.
Preparing to unpack .../11-libroken18-heimdal_7.7.0+dfsg-1ubuntu1.4_ppc64el.deb ...
Unpacking libroken18-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Selecting previously unselected package libasn1-8-heimdal:ppc64el.
Preparing to unpack .../12-libasn1-8-heimdal_7.7.0+dfsg-1ubuntu1.4_ppc64el.deb ...
Unpacking libasn1-8-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Selecting previously unselected package libheimbase1-heimdal:ppc64el.
Preparing to unpack .../13-libheimbase1-heimdal_7.7.0+dfsg-1ubuntu1.4_ppc64el.deb ...
Unpacking libheimbase1-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Selecting previously unselected package libhcrypto4-heimdal:ppc64el.
Preparing to unpack .../14-libhcrypto4-heimdal_7.7.0+dfsg-1ubuntu1.4_ppc64el.deb ...
Unpacking libhcrypto4-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Selecting previously unselected package libwind0-heimdal:ppc64el.
Preparing to unpack .../15-libwind0-heimdal_7.7.0+dfsg-1ubuntu1.4_ppc64el.deb ...
Unpacking libwind0-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Selecting previously unselected package libhx509-5-heimdal:ppc64el.
Preparing to unpack .../16-libhx509-5-heimdal_7.7.0+dfsg-1ubuntu1.4_ppc64el.deb ...
Unpacking libhx509-5-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Selecting previously unselected package libkrb5-26-heimdal:ppc64el.
Preparing to unpack .../17-libkrb5-26-heimdal_7.7.0+dfsg-1ubuntu1.4_ppc64el.deb ...
Unpacking libkrb5-26-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Selecting previously unselected package libheimntlm0-heimdal:ppc64el.
Preparing to unpack .../18-libheimntlm0-heimdal_7.7.0+dfsg-1ubuntu1.4_ppc64el.deb ...
Unpacking libheimntlm0-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Selecting previously unselected package libgssapi3-heimdal:ppc64el.
Preparing to unpack .../19-libgssapi3-heimdal_7.7.0+dfsg-1ubuntu1.4_ppc64el.deb ...
Unpacking libgssapi3-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Selecting previously unselected package libsasl2-modules-db:ppc64el.
Preparing to unpack .../20-libsasl2-modules-db_2.1.27+dfsg-2ubuntu0.1_ppc64el.deb ...
Unpacking libsasl2-modules-db:ppc64el (2.1.27+dfsg-2ubuntu0.1) ...
Selecting previously unselected package libsasl2-2:ppc64el.
Preparing to unpack .../21-libsasl2-2_2.1.27+dfsg-2ubuntu0.1_ppc64el.deb ...
Unpacking libsasl2-2:ppc64el (2.1.27+dfsg-2ubuntu0.1) ...
Selecting previously unselected package libldap-common.
Preparing to unpack .../22-libldap-common_2.4.49+dfsg-2ubuntu1.9_all.deb ...
Unpacking libldap-common (2.4.49+dfsg-2ubuntu1.9) ...
Selecting previously unselected package libldap-2.4-2:ppc64el.
Preparing to unpack .../23-libldap-2.4-2_2.4.49+dfsg-2ubuntu1.9_ppc64el.deb ...
Unpacking libldap-2.4-2:ppc64el (2.4.49+dfsg-2ubuntu1.9) ...
Selecting previously unselected package libaprutil1-ldap:ppc64el.
Preparing to unpack .../24-libaprutil1-ldap_1.6.1-4ubuntu2.2_ppc64el.deb ...
Unpacking libaprutil1-ldap:ppc64el (1.6.1-4ubuntu2.2) ...
Selecting previously unselected package libbrotli1:ppc64el.
Preparing to unpack .../25-libbrotli1_1.0.7-6ubuntu0.1_ppc64el.deb ...
Unpacking libbrotli1:ppc64el (1.0.7-6ubuntu0.1) ...
Selecting previously unselected package libkrb5support0:ppc64el.
Preparing to unpack .../26-libkrb5support0_1.17-6ubuntu4.3_ppc64el.deb ...
Unpacking libkrb5support0:ppc64el (1.17-6ubuntu4.3) ...
Selecting previously unselected package libk5crypto3:ppc64el.
Preparing to unpack .../27-libk5crypto3_1.17-6ubuntu4.3_ppc64el.deb ...
Unpacking libk5crypto3:ppc64el (1.17-6ubuntu4.3) ...
Selecting previously unselected package libkeyutils1:ppc64el.
Preparing to unpack .../28-libkeyutils1_1.6-6ubuntu1.1_ppc64el.deb ...
Unpacking libkeyutils1:ppc64el (1.6-6ubuntu1.1) ...
Selecting previously unselected package libkrb5-3:ppc64el.
Preparing to unpack .../29-libkrb5-3_1.17-6ubuntu4.3_ppc64el.deb ...
Unpacking libkrb5-3:ppc64el (1.17-6ubuntu4.3) ...
Selecting previously unselected package libgssapi-krb5-2:ppc64el.
Preparing to unpack .../30-libgssapi-krb5-2_1.17-6ubuntu4.3_ppc64el.deb ...
Unpacking libgssapi-krb5-2:ppc64el (1.17-6ubuntu4.3) ...
Selecting previously unselected package libnghttp2-14:ppc64el.
Preparing to unpack .../31-libnghttp2-14_1.40.0-1ubuntu0.1_ppc64el.deb ...
Unpacking libnghttp2-14:ppc64el (1.40.0-1ubuntu0.1) ...
Selecting previously unselected package libpsl5:ppc64el.
Preparing to unpack .../32-libpsl5_0.21.0-1ubuntu1_ppc64el.deb ...
Unpacking libpsl5:ppc64el (0.21.0-1ubuntu1) ...
Selecting previously unselected package librtmp1:ppc64el.
Preparing to unpack .../33-librtmp1_2.4+20151223.gitfa8646d.1-2build1_ppc64el.deb ...
Unpacking librtmp1:ppc64el (2.4+20151223.gitfa8646d.1-2build1) ...
Selecting previously unselected package libssh-4:ppc64el.
Preparing to unpack .../34-libssh-4_0.9.3-2ubuntu2.3_ppc64el.deb ...
Unpacking libssh-4:ppc64el (0.9.3-2ubuntu2.3) ...
Selecting previously unselected package libcurl4:ppc64el.
Preparing to unpack .../35-libcurl4_7.68.0-1ubuntu2.19_ppc64el.deb ...
Unpacking libcurl4:ppc64el (7.68.0-1ubuntu2.19) ...
Selecting previously unselected package libjansson4:ppc64el.
Preparing to unpack .../36-libjansson4_2.12-1build1_ppc64el.deb ...
Unpacking libjansson4:ppc64el (2.12-1build1) ...
Selecting previously unselected package liblua5.2-0:ppc64el.
Preparing to unpack .../37-liblua5.2-0_5.2.4-1.1build3_ppc64el.deb ...
Unpacking liblua5.2-0:ppc64el (5.2.4-1.1build3) ...
Selecting previously unselected package tzdata.
Preparing to unpack .../38-tzdata_2023c-0ubuntu0.20.04.2_all.deb ...
Unpacking tzdata (2023c-0ubuntu0.20.04.2) ...
Selecting previously unselected package libicu66:ppc64el.
Preparing to unpack .../39-libicu66_66.1-2ubuntu2.1_ppc64el.deb ...
Unpacking libicu66:ppc64el (66.1-2ubuntu2.1) ...
Selecting previously unselected package libxml2:ppc64el.
Preparing to unpack .../40-libxml2_2.9.10+dfsg-5ubuntu0.20.04.6_ppc64el.deb ...
Unpacking libxml2:ppc64el (2.9.10+dfsg-5ubuntu0.20.04.6) ...
Selecting previously unselected package apache2-bin.
Preparing to unpack .../41-apache2-bin_2.4.41-4ubuntu3.14_ppc64el.deb ...
Unpacking apache2-bin (2.4.41-4ubuntu3.14) ...
Selecting previously unselected package apache2-data.
Preparing to unpack .../42-apache2-data_2.4.41-4ubuntu3.14_all.deb ...
Unpacking apache2-data (2.4.41-4ubuntu3.14) ...
Selecting previously unselected package apache2-utils.
Preparing to unpack .../43-apache2-utils_2.4.41-4ubuntu3.14_ppc64el.deb ...
Unpacking apache2-utils (2.4.41-4ubuntu3.14) ...
Selecting previously unselected package mime-support.
Preparing to unpack .../44-mime-support_3.64ubuntu1_all.deb ...
Unpacking mime-support (3.64ubuntu1) ...
Selecting previously unselected package apache2.
Preparing to unpack .../45-apache2_2.4.41-4ubuntu3.14_ppc64el.deb ...
Unpacking apache2 (2.4.41-4ubuntu3.14) ...
Selecting previously unselected package openssl.
Preparing to unpack .../46-openssl_1.1.1f-1ubuntu2.19_ppc64el.deb ...
Unpacking openssl (1.1.1f-1ubuntu2.19) ...
Selecting previously unselected package ca-certificates.
Preparing to unpack .../47-ca-certificates_20230311ubuntu0.20.04.1_all.deb ...
Unpacking ca-certificates (20230311ubuntu0.20.04.1) ...
Selecting previously unselected package libmagic-mgc.
Preparing to unpack .../48-libmagic-mgc_1%3a5.38-4_ppc64el.deb ...
Unpacking libmagic-mgc (1:5.38-4) ...
Selecting previously unselected package libmagic1:ppc64el.
Preparing to unpack .../49-libmagic1_1%3a5.38-4_ppc64el.deb ...
Unpacking libmagic1:ppc64el (1:5.38-4) ...
Selecting previously unselected package file.
Preparing to unpack .../50-file_1%3a5.38-4_ppc64el.deb ...
Unpacking file (1:5.38-4) ...
Selecting previously unselected package netbase.
Preparing to unpack .../51-netbase_6.1_all.deb ...
Unpacking netbase (6.1) ...
Selecting previously unselected package xz-utils.
Preparing to unpack .../52-xz-utils_5.2.4-1ubuntu1.1_ppc64el.deb ...
Unpacking xz-utils (5.2.4-1ubuntu1.1) ...
Selecting previously unselected package krb5-locales.
Preparing to unpack .../53-krb5-locales_1.17-6ubuntu4.3_all.deb ...
Unpacking krb5-locales (1.17-6ubuntu4.3) ...
Selecting previously unselected package publicsuffix.
Preparing to unpack .../54-publicsuffix_20200303.0012-1_all.deb ...
Unpacking publicsuffix (20200303.0012-1) ...
Selecting previously unselected package libsasl2-modules:ppc64el.
Preparing to unpack .../55-libsasl2-modules_2.1.27+dfsg-2ubuntu0.1_ppc64el.deb ...
Unpacking libsasl2-modules:ppc64el (2.1.27+dfsg-2ubuntu0.1) ...
Selecting previously unselected package ssl-cert.
Preparing to unpack .../56-ssl-cert_1.0.39_all.deb ...
Unpacking ssl-cert (1.0.39) ...
Setting up libexpat1:ppc64el (2.2.9-1ubuntu0.6) ...
Setting up libkeyutils1:ppc64el (1.6-6ubuntu1.1) ...
Setting up libpsl5:ppc64el (0.21.0-1ubuntu1) ...
Setting up perl-modules-5.30 (5.30.0-9ubuntu0.4) ...
Setting up mime-support (3.64ubuntu1) ...
Setting up libmagic-mgc (1:5.38-4) ...
Setting up libssl1.1:ppc64el (1.1.1f-1ubuntu2.19) ...
debconf: unable to initialize frontend: Dialog
debconf: (TERM is not set, so the dialog frontend is not usable.)
debconf: falling back to frontend: Readline
Setting up libbrotli1:ppc64el (1.0.7-6ubuntu0.1) ...
Setting up libsqlite3-0:ppc64el (3.31.1-4ubuntu0.5) ...
Setting up libsasl2-modules:ppc64el (2.1.27+dfsg-2ubuntu0.1) ...
Setting up libnghttp2-14:ppc64el (1.40.0-1ubuntu0.1) ...
Setting up libmagic1:ppc64el (1:5.38-4) ...
Setting up libapr1:ppc64el (1.6.5-1ubuntu1) ...
Setting up krb5-locales (1.17-6ubuntu4.3) ...
Setting up file (1:5.38-4) ...
Setting up libldap-common (2.4.49+dfsg-2ubuntu1.9) ...
Setting up libjansson4:ppc64el (2.12-1build1) ...
Setting up libkrb5support0:ppc64el (1.17-6ubuntu4.3) ...
Setting up libsasl2-modules-db:ppc64el (2.1.27+dfsg-2ubuntu0.1) ...
Setting up tzdata (2023c-0ubuntu0.20.04.2) ...
debconf: unable to initialize frontend: Dialog
debconf: (TERM is not set, so the dialog frontend is not usable.)
debconf: falling back to frontend: Readline

Current default time zone: 'Europe/Warsaw'
Local time is now:      Mon Sep 18 12:12:04 CEST 2023.
Universal Time is now:  Mon Sep 18 10:12:04 UTC 2023.
Run 'dpkg-reconfigure tzdata' if you wish to change it.

Setting up librtmp1:ppc64el (2.4+20151223.gitfa8646d.1-2build1) ...
Setting up xz-utils (5.2.4-1ubuntu1.1) ...
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
Setting up libk5crypto3:ppc64el (1.17-6ubuntu4.3) ...
Setting up libsasl2-2:ppc64el (2.1.27+dfsg-2ubuntu0.1) ...
Setting up libroken18-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Setting up liblua5.2-0:ppc64el (5.2.4-1.1build3) ...
Setting up netbase (6.1) ...
Setting up libkrb5-3:ppc64el (1.17-6ubuntu4.3) ...
Setting up apache2-data (2.4.41-4ubuntu3.14) ...
Setting up openssl (1.1.1f-1ubuntu2.19) ...
Setting up publicsuffix (20200303.0012-1) ...
Setting up libheimbase1-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Setting up libgdbm6:ppc64el (1.18.1-5) ...
Setting up libaprutil1:ppc64el (1.6.1-4ubuntu2.2) ...
Setting up libicu66:ppc64el (66.1-2ubuntu2.1) ...
Setting up libasn1-8-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Setting up libaprutil1-dbd-sqlite3:ppc64el (1.6.1-4ubuntu2.2) ...
Setting up libhcrypto4-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Setting up ca-certificates (20230311ubuntu0.20.04.1) ...
debconf: unable to initialize frontend: Dialog
debconf: (TERM is not set, so the dialog frontend is not usable.)
debconf: falling back to frontend: Readline
Updating certificates in /etc/ssl/certs...
137 added, 0 removed; done.
Setting up libwind0-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Setting up ssl-cert (1.0.39) ...
debconf: unable to initialize frontend: Dialog
debconf: (TERM is not set, so the dialog frontend is not usable.)
debconf: falling back to frontend: Readline
hostname: Name or service not known
make-ssl-cert: Could not get FQDN, using "5b99eaa510e6".
make-ssl-cert: You may want to fix your /etc/hosts and/or DNS setup and run
make-ssl-cert: make-ssl-cert generate-default-snakeoil --force-overwrite
make-ssl-cert: again.
Setting up libgssapi-krb5-2:ppc64el (1.17-6ubuntu4.3) ...
Setting up libgdbm-compat4:ppc64el (1.18.1-5) ...
Setting up libssh-4:ppc64el (0.9.3-2ubuntu2.3) ...
Setting up libperl5.30:ppc64el (5.30.0-9ubuntu0.4) ...
Setting up libxml2:ppc64el (2.9.10+dfsg-5ubuntu0.20.04.6) ...
Setting up apache2-utils (2.4.41-4ubuntu3.14) ...
Setting up libhx509-5-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Setting up perl (5.30.0-9ubuntu0.4) ...
Setting up libkrb5-26-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Setting up libheimntlm0-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Setting up libgssapi3-heimdal:ppc64el (7.7.0+dfsg-1ubuntu1.4) ...
Setting up libldap-2.4-2:ppc64el (2.4.49+dfsg-2ubuntu1.9) ...
Setting up libaprutil1-ldap:ppc64el (1.6.1-4ubuntu2.2) ...
Setting up libcurl4:ppc64el (7.68.0-1ubuntu2.19) ...
Setting up apache2-bin (2.4.41-4ubuntu3.14) ...
Setting up apache2 (2.4.41-4ubuntu3.14) ...
Enabling module mpm_event.
Enabling module authz_core.
Enabling module authz_host.
Enabling module authn_core.
Enabling module auth_basic.
Enabling module access_compat.
Enabling module authn_file.
Enabling module authz_user.
Enabling module alias.
Enabling module dir.
Enabling module autoindex.
Enabling module env.
Enabling module mime.
Enabling module negotiation.
Enabling module setenvif.
Enabling module filter.
Enabling module deflate.
Enabling module status.
Enabling module reqtimeout.
Enabling conf charset.
Enabling conf localized-error-pages.
Enabling conf other-vhosts-access-log.
Enabling conf security.
Enabling conf serve-cgi-bin.
Enabling site 000-default.
invoke-rc.d: could not determine current runlevel
invoke-rc.d: policy-rc.d denied execution of start.
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
Processing triggers for ca-certificates (20230311ubuntu0.20.04.1) ...
Updating certificates in /etc/ssl/certs...
0 added, 0 removed; done.
Running hooks in /etc/ca-certificates/update.d...
done.
--> ab74025257d
STEP 5/20: ADD index.html /var/www/html/index.html
--> 244c81fb31e
STEP 6/20: ADD webstart.sh /usr/sbin/webstart.sh
--> 3025d871458
STEP 7/20: RUN chmod +x /usr/sbin/webstart.sh
--> 282c1c3bb29
STEP 8/20: RUN sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/ports.conf
--> 1ab47a369c0
STEP 9/20: RUN sed -i 's/apache2$SUFFIX/apache2/g' /etc/apache2/envvars
--> ebb7ccafe57
STEP 10/20: RUN mkdir /var/run/apache2
--> 609aef9ad44
STEP 11/20: RUN mkdir /var/lock/apache2
--> 3f229916ed8
STEP 12/20: RUN chgrp -R 0 /var/www/html &&     chmod -R g=u /var/www/html
--> 293018fbbb4
STEP 13/20: RUN chgrp -R 0 /var/lock/apache2 &&     chmod -R g=u /var/lock/apache2
--> ee8b2e88a03
STEP 14/20: RUN chgrp -R 0 /var/run/apache2 &&     chmod -R g=u /var/run/apache2
--> 6b020b10677
STEP 15/20: RUN chgrp -R 0 /var/log/apache2 &&     chmod -R g=u /var/log/apache2
--> ba27d566dee
STEP 16/20: EXPOSE 8080
--> 6febfb757a0
STEP 17/20: CMD null
--> ac24e77ab3b
STEP 18/20: ENTRYPOINT ["webstart.sh"]
--> 672f728cf54
STEP 19/20: ENV "OPENSHIFT_BUILD_NAME"="labuser0app1-6" "OPENSHIFT_BUILD_NAMESPACE"="labuser0" "OPENSHIFT_BUILD_SOURCE"="https://github.com/michalteofan/labuser0.git" "OPENSHIFT_BUILD_COMMIT"="b7e4355c9fd5f72c92b9500e55890d086bbb01e9"
--> f25be809195
STEP 20/20: LABEL "io.openshift.build.commit.author"="Michal <michal@pl.ibm.com>" "io.openshift.build.commit.date"="Mon Sep 18 12:11:05 2023 +0200" "io.openshift.build.commit.id"="b7e4355c9fd5f72c92b9500e55890d086bbb01e9" "io.openshift.build.commit.message"="focal" "io.openshift.build.commit.ref"="master" "io.openshift.build.name"="labuser0app1-6" "io.openshift.build.namespace"="labuser0" "io.openshift.build.source-context-dir"="/" "io.openshift.build.source-location"="https://github.com/michalteofan/labuser0.git"
COMMIT temp.builder.openshift.io/labuser0/labuser0app1-6:22e609d6
--> fb7e8fdefff
Successfully tagged temp.builder.openshift.io/labuser0/labuser0app1-6:22e609d6
fb7e8fdefff206a2f6a91a15986ba4dd18907a6baf43b6daabb8d712edf240a0

Pushing image image-registry.openshift-image-registry.svc:5000/labuser0/labuser0app1:latest ...
Getting image source signatures
Copying blob sha256:7d27dd1a3d314da1212c2056c05d3b3e11f22d45056e9ed12155441eec755100
Copying blob sha256:0f7120f4ae0c99addcb79d17f1e3f774990b0a7f18954339f759ec121938aa27
Copying blob sha256:c8ba077381c534be72ed060730e8165f96fe2732abadb0b326ba6412e5775977
Copying blob sha256:bc9358b06de323772ff00ecba7467c36d864bca1c32e119558ee34c00db97856
Copying blob sha256:421191f50ea36592ee60d589079047f108be43782c548c10c8951a7108dcc64c
Copying blob sha256:fa78ce4014add322eddde3378405efe21c85e886c0195e18533d5991d5477833
Copying blob sha256:74fce94698263c9e006ac250ba67fb3ed3289498966611e7566347df5896d208
Copying blob sha256:506667a3214bc10ef4bbc1869becb9c040b8a493e04e1f37586e7bb8223588cc
Copying blob sha256:9aeb78f8ce255b791aa70acdb6fbb5cad47cd8424795968a9cd95ec749ccf73c
Copying blob sha256:b50b1ad7a51a052abef38075160dc711c6ddc12c70ec21ffddc80a8db0f5082a
Copying blob sha256:13267e541c2ad089ef7cfeb83fcd83c58f94f9b897c9be698caf18ddf11d0aaa
Copying blob sha256:eb39fd18e7ee211641773a1e05c0e9717a8574067286edccc8301dbc2cbe9562
Copying blob sha256:5efd73bf7db174ce6a2f2f107484578f25269daacb0b287a6a4a23b4b39162c2
Copying blob sha256:4521efaf9c805f36518f189c554193572933e95f382c57e6273db3347ecd8e46
Copying config sha256:fb7e8fdefff206a2f6a91a15986ba4dd18907a6baf43b6daabb8d712edf240a0
Writing manifest to image destination
Storing signatures
Successfully pushed image-registry.openshift-image-registry.svc:5000/labuser0/labuser0app1@sha256:ca038491aa70f293174065336fc9be00c6a821a8b95e44aeff17e9e89c9ef149
Push successful
```

Check if the pod is running and click Open URL.
https://labuserXapp1-labuserX.apps.yyy.yyy.yy




