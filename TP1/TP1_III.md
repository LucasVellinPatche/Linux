## 🌞 Lancez les deux conteneurs avec docker compose

```powershell
[lucas@localhost python_app_build]$ cd ..
[lucas@localhost ~]$ cd compose_test/
[lucas@localhost compose_test]$ docker compose up -d
WARN[0000] /home/lucas/compose_test/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] Running 3/3
 ✔ conteneur_flopesque Pulled                                                                                      3.3s
   ✔ fdf894e782a2 Already exists                                                                                   0.0s
 ✔ conteneur_nul Pulled                                                                                            3.5s
[+] Running 3/3
 ✔ Network compose_test_default                  Created                                                           0.3s
 ✔ Container compose_test-conteneur_flopesque-1  Started                                                           0.7s
 ✔ Container compose_test-conteneur_nul-1        Started
```

## 🌞 Vérifier que les deux conteneurs tournent

```powershell
[lucas@localhost compose_test]$ docker ps
CONTAINER ID   IMAGE     COMMAND        CREATED         STATUS         PORTS     NAMES
bb3862c9ffbe   debian    "sleep 9999"   2 minutes ago   Up 2 minutes             compose_test-conteneur_flopesque-1
31782e4a5011   debian    "sleep 9999"   2 minutes ago   Up 2 minutes             compose_test-conteneur_nul-1
[lucas@localhost compose_test]$
```

## 🌞 Pop un shell dans le conteneur conteneur_nul

```powershell
[lucas@localhost compose_test]$ docker ps
CONTAINER ID   IMAGE     COMMAND        CREATED          STATUS          PORTS     NAMES
bb3862c9ffbe   debian    "sleep 9999"   11 minutes ago   Up 11 minutes             compose_test-conteneur_flopesque-1
31782e4a5011   debian    "sleep 9999"   11 minutes ago   Up 11 minutes             compose_test-conteneur_nul-1
[lucas@localhost compose_test]$ docker exec -it 317 bash
root@31782e4a5011:/# apt update -y
Get:1 http://deb.debian.org/debian bookworm InRelease [151 kB]
Get:2 http://deb.debian.org/debian bookworm-updates InRelease [55.4 kB]
Get:3 http://deb.debian.org/debian-security bookworm-security InRelease [48.0 kB]
Get:4 http://deb.debian.org/debian bookworm/main amd64 Packages [8789 kB]
Get:5 http://deb.debian.org/debian bookworm-updates/main amd64 Packages [8856 B]
Get:6 http://deb.debian.org/debian-security bookworm-security/main amd64 Packages [216 kB]
Fetched 9268 kB in 37s (249 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
All packages are up to date.
root@31782e4a5011:/# apt install iputils-ping
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libcap2-bin libpam-cap
The following NEW packages will be installed:
  iputils-ping libcap2-bin libpam-cap
0 upgraded, 3 newly installed, 0 to remove and 0 not upgraded.
Need to get 96.3 kB of archives.
After this operation, 312 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://deb.debian.org/debian bookworm/main amd64 libcap2-bin amd64 1:2.66-4 [34.7 kB]
Get:2 http://deb.debian.org/debian bookworm/main amd64 iputils-ping amd64 3:20221126-1+deb12u1 [47.2 kB]
Get:3 http://deb.debian.org/debian bookworm/main amd64 libpam-cap amd64 1:2.66-4 [14.5 kB]
Fetched 96.3 kB in 0s (300 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package libcap2-bin.
(Reading database ... 6089 files and directories currently installed.)
Preparing to unpack .../libcap2-bin_1%3a2.66-4_amd64.deb ...
Unpacking libcap2-bin (1:2.66-4) ...
Selecting previously unselected package iputils-ping.
Preparing to unpack .../iputils-ping_3%3a20221126-1+deb12u1_amd64.deb ...
Unpacking iputils-ping (3:20221126-1+deb12u1) ...
Selecting previously unselected package libpam-cap:amd64.
Preparing to unpack .../libpam-cap_1%3a2.66-4_amd64.deb ...
Unpacking libpam-cap:amd64 (1:2.66-4) ...
Setting up libcap2-bin (1:2.66-4) ...
Setting up libpam-cap:amd64 (1:2.66-4) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/D
ebconf/FrontEnd/Dialog.pm line 78.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc
/perl /usr/local/lib/x86_64-linux-gnu/perl/5.36.0 /usr/local/share/perl/5.36.0 /usr/lib/x86_64-linux-gnu/perl5/5.36 /usr
/share/perl5 /usr/lib/x86_64-linux-gnu/perl-base /usr/lib/x86_64-linux-gnu/perl/5.36 /usr/share/perl/5.36 /usr/local/lib
/site_perl) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)
debconf: falling back to frontend: Teletype
Setting up iputils-ping (3:20221126-1+deb12u1) ...
root@31782e4a5011:/# ping conteneur_flopesque
PING conteneur_flopesque (172.18.0.2) 56(84) bytes of data.
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=1 ttl=64 time=0.049 ms
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=2 ttl=64 time=0.115 ms
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=3 ttl=64 time=0.060 ms
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=4 ttl=64 time=0.057 ms
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=5 ttl=64 time=0.056 ms
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=6 ttl=64 time=0.075 ms
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=7 ttl=64 time=0.115 ms
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=8 ttl=64 time=0.074 ms
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=9 ttl=64 time=0.056 ms
^C
--- conteneur_flopesque ping statistics ---
9 packets transmitted, 9 received, 0% packet loss, time 8093ms
rtt min/avg/max/mdev = 0.049/0.073/0.115/0.023 ms
```