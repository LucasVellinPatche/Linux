## 🌞 Ajouter votre utilisateur au groupe docker

J'ai oublié de récupérer ça avant de relancer mon terminal ^^''
Du coup on va faire ça "de tête":

```powershell
[lucas@localhost ~]$ sudo usermod -G docker lucas
[lucas@localhost ~]$ Enter Password:
[lucas@localhost ~]$
```

## 🌞 Lancer un conteneur NGINX

```powershell
[lucas@localhost ~]$ docker run -d -p 9999:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
bc0965b23a04: Pull complete
650ee30bbe5e: Pull complete
8cc1569e58f5: Pull complete
362f35df001b: Pull complete
13e320bf29cd: Pull complete
7b50399908e1: Pull complete
57b64962dd94: Pull complete
Digest: sha256:fb197595ebe76b9c0c14ab68159fd3c08bd067ec62300583543f0ebda353b5be
Status: Downloaded newer image for nginx:latest
8fa601e40ec8e59eff7702d150ec6c80647f875d623f157ad7e2a7109a6acb0a
```

## 🌞 Visitons

```powershell
[lucas@localhost ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS
   NAMES
8fa601e40ec8   nginx     "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:9999->80/tcp, [::]:9999->80/tcp   loving_tharp
[lucas@localhost ~]$ docker rm -f 8fa601e40ec8
8fa601e40ec8
[lucas@localhost ~]$ docker run -p 9999:80 nginx
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/12/11 16:35:19 [notice] 1#1: using the "epoll" event method
2024/12/11 16:35:19 [notice] 1#1: nginx/1.27.3
2024/12/11 16:35:19 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2024/12/11 16:35:19 [notice] 1#1: OS: Linux 5.14.0-427.26.1.el9_4.x86_64
2024/12/11 16:35:19 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1073741816:1073741816
2024/12/11 16:35:19 [notice] 1#1: start worker processes
2024/12/11 16:35:19 [notice] 1#1: start worker process 28
[lucas@localhost ~]$ docker inspect 8ec9a9d0da23
[
    {
        "Id": "8ec9a9d0da2326f5f41c96bbc6904cf6b011b48db2b7d0348254b621a6bc36d5",
        "Created": "2024-12-12T15:16:50.816198163Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 1844,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2024-12-12T15:16:52.174684338Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:66f8bdd3810c96dc5c28aec39583af731b34a2cd99471530f53c8794ed5b423e",
        "ResolvConfPath": "/var/lib/docker/containers/8ec9a9d0da2326f5f41c96bbc6904cf6b011b48db2b7d0348254b621a6bc36d5/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/8ec9a9d0da2326f5f41c96bbc6904cf6b011b48db2b7d0348254b621a6bc36d5/hostname",
        "HostsPath": "/var/lib/docker/containers/8ec9a9d0da2326f5f41c96bbc6904cf6b011b48db2b7d0348254b621a6bc36d5/hosts",
        "LogPath": "/var/lib/docker/containers/8ec9a9d0da2326f5f41c96bbc6904cf6b011b48db2b7d0348254b621a6bc36d5/8ec9a9d0da2326f5f41c96bbc6904cf6b011b48db2b7d0348254b621a6bc36d5-json.log",
        "Name": "/kind_neumann",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "bridge",
            "PortBindings": {
                "80/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "9999"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                30,
                120
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "private",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": null,
            "PidsLimit": null,
            "Ulimits": [],
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware",
                "/sys/devices/virtual/powercap"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/fc77ae958ba8c9c33fb061b14f33ab4d396dabd90d65d43dda2e2a15374d5fdb-init/diff:/var/lib/docker/overlay2/3a2c73e311323c0d68c4c436a3ddaba0d0d5990ff8111668d26b46791a767124/diff:/var/lib/docker/overlay2/24f66bfc5ca3de9c74d88a44f8860260c66ffe7606aef543c32aeff495a0c0ea/diff:/var/lib/docker/overlay2/940ce2b8d8179d188d527be4b3481070d48982e89b23935e54c8ffa615c3acf5/diff:/var/lib/docker/overlay2/721999a2fb5cb15859141caf43080944e72b650766b05af1486dc4173a49724a/diff:/var/lib/docker/overlay2/6cfb99553f395961b7d7ac9951d53fbd8d49fa82f38af58c08eca19b3461e473/diff:/var/lib/docker/overlay2/cee4b1f247665e1b8a98fdeb389328c4c9e212f716f27cb2d134806b3613d1e1/diff:/var/lib/docker/overlay2/1fc2b667687e55371c87e9ae43e243bd1dd6048e1879449dcc8ebf53b24cdd39/diff",
                "MergedDir": "/var/lib/docker/overlay2/fc77ae958ba8c9c33fb061b14f33ab4d396dabd90d65d43dda2e2a15374d5fdb/merged",
                "UpperDir": "/var/lib/docker/overlay2/fc77ae958ba8c9c33fb061b14f33ab4d396dabd90d65d43dda2e2a15374d5fdb/diff",
                "WorkDir": "/var/lib/docker/overlay2/fc77ae958ba8c9c33fb061b14f33ab4d396dabd90d65d43dda2e2a15374d5fdb/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "8ec9a9d0da23",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.27.3",
                "NJS_VERSION=0.8.7",
                "NJS_RELEASE=1~bookworm",
                "PKG_RELEASE=1~bookworm",
                "DYNPKG_RELEASE=1~bookworm"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "1557bf58f485f03876e263c1a55423c3183c7edac5427a9a50b36b6885100ae5",
            "SandboxKey": "/var/run/docker/netns/1557bf58f485",
            "Ports": {
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "9999"
                    },
                    {
                        "HostIp": "::",
                        "HostPort": "9999"
                    }
                ]
            },
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "b6223751e719b996d93d08bb799331a2fe14386c7b88e5368b929e30c4aa55e4",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null,
                    "NetworkID": "ecd28a8db851895c3d4ca0dc7843b9767a58eac538af3f75235b429e782f674d",
                    "EndpointID": "b6223751e719b996d93d08bb799331a2fe14386c7b88e5368b929e30c4aa55e4",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DNSNames": null
                }
            }
        }
    }
]
[lucas@localhost ~]$ sudo ss -lnpt
[sudo] password for lucas:
State     Recv-Q    Send-Q       Local Address:Port       Peer Address:Port   Process
LISTEN    0         128                0.0.0.0:22              0.0.0.0:*       users:(("sshd",pid=715,fd=3))
LISTEN    0         4096               0.0.0.0:9999            0.0.0.0:*       users:(("docker-proxy",pid=1797,fd=4))
LISTEN    0         128                   [::]:22                 [::]:*       users:(("sshd",pid=715,fd=4))
LISTEN    0         4096                  [::]:9999               [::]:*       users:(("docker-proxy",pid=1802,fd=4))
[lucas@localhost ~]$ sudo firewall-cmd --add-port=9999/tcp
[sudo] password for lucas:
success
[lucas@localhost ~]$ docker run --help

Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Create and run a new container from an image

Aliases:
  docker container run, docker run

Options:
      --add-host list                    Add a custom host-to-IP mapping (host:ip)
      --annotation map                   Add an annotation to the container (passed through to the OCI runtime)
                                         (default map[])
  -a, --attach list                      Attach to STDIN, STDOUT or STDERR
      --blkio-weight uint16              Block IO (relative weight), between 10 and 1000, or 0 to disable (default 0)
      --blkio-weight-device list         Block IO weight (relative device weight) (default [])
      --cap-add list                     Add Linux capabilities
      --cap-drop list                    Drop Linux capabilities
      --cgroup-parent string             Optional parent cgroup for the container
      --cgroupns string                  Cgroup namespace to use (host|private)
                                         'host':    Run the container in the Docker host's cgroup namespace
                                         'private': Run the container in its own private cgroup namespace
                                         '':        Use the cgroup namespace as configured by the
                                                    default-cgroupns-mode option on the daemon (default)
      --cidfile string                   Write the container ID to the file
      --cpu-period int                   Limit CPU CFS (Completely Fair Scheduler) period
      --cpu-quota int                    Limit CPU CFS (Completely Fair Scheduler) quota
      --cpu-rt-period int                Limit CPU real-time period in microseconds
      --cpu-rt-runtime int               Limit CPU real-time runtime in microseconds
  -c, --cpu-shares int                   CPU shares (relative weight)
      --cpus decimal                     Number of CPUs
      --cpuset-cpus string               CPUs in which to allow execution (0-3, 0,1)
      --cpuset-mems string               MEMs in which to allow execution (0-3, 0,1)
  -d, --detach                           Run container in background and print container ID
      --detach-keys string               Override the key sequence for detaching a container
      --device list                      Add a host device to the container
      --device-cgroup-rule list          Add a rule to the cgroup allowed devices list
      --device-read-bps list             Limit read rate (bytes per second) from a device (default [])
      --device-read-iops list            Limit read rate (IO per second) from a device (default [])
      --device-write-bps list            Limit write rate (bytes per second) to a device (default [])
      --device-write-iops list           Limit write rate (IO per second) to a device (default [])
      --disable-content-trust            Skip image verification (default true)
      --dns list                         Set custom DNS servers
      --dns-option list                  Set DNS options
      --dns-search list                  Set custom DNS search domains
      --domainname string                Container NIS domain name
      --entrypoint string                Overwrite the default ENTRYPOINT of the image
  -e, --env list                         Set environment variables
      --env-file list                    Read in a file of environment variables
      --expose list                      Expose a port or a range of ports
      --gpus gpu-request                 GPU devices to add to the container ('all' to pass all GPUs)
      --group-add list                   Add additional groups to join
      --health-cmd string                Command to run to check health
      --health-interval duration         Time between running the check (ms|s|m|h) (default 0s)
      --health-retries int               Consecutive failures needed to report unhealthy
      --health-start-interval duration   Time between running the check during the start period (ms|s|m|h)
                                         (default 0s)
      --health-start-period duration     Start period for the container to initialize before starting
                                         health-retries countdown (ms|s|m|h) (default 0s)
      --health-timeout duration          Maximum time to allow one check to run (ms|s|m|h) (default 0s)
      --help                             Print usage
  -h, --hostname string                  Container host name
      --init                             Run an init inside the container that forwards signals and reaps processes
  -i, --interactive                      Keep STDIN open even if not attached
      --ip string                        IPv4 address (e.g., 172.30.100.104)
      --ip6 string                       IPv6 address (e.g., 2001:db8::33)
      --ipc string                       IPC mode to use
      --isolation string                 Container isolation technology
      --kernel-memory bytes              Kernel memory limit
  -l, --label list                       Set meta data on a container
      --label-file list                  Read in a line delimited file of labels
      --link list                        Add link to another container
      --link-local-ip list               Container IPv4/IPv6 link-local addresses
      --log-driver string                Logging driver for the container
      --log-opt list                     Log driver options
      --mac-address string               Container MAC address (e.g., 92:d0:c6:0a:29:33)
  -m, --memory bytes                     Memory limit
      --memory-reservation bytes         Memory soft limit
      --memory-swap bytes                Swap limit equal to memory plus swap: '-1' to enable unlimited swap
      --memory-swappiness int            Tune container memory swappiness (0 to 100) (default -1)
      --mount mount                      Attach a filesystem mount to the container
      --name string                      Assign a name to the container
      --network network                  Connect a container to a network
      --network-alias list               Add network-scoped alias for the container
      --no-healthcheck                   Disable any container-specified HEALTHCHECK
      --oom-kill-disable                 Disable OOM Killer
      --oom-score-adj int                Tune host's OOM preferences (-1000 to 1000)
      --pid string                       PID namespace to use
      --pids-limit int                   Tune container pids limit (set -1 for unlimited)
      --platform string                  Set platform if server is multi-platform capable
      --privileged                       Give extended privileges to this container
  -p, --publish list                     Publish a container's port(s) to the host
  -P, --publish-all                      Publish all exposed ports to random ports
      --pull string                      Pull image before running ("always", "missing", "never") (default "missing")
  -q, --quiet                            Suppress the pull output
      --read-only                        Mount the container's root filesystem as read only
      --restart string                   Restart policy to apply when a container exits (default "no")
      --rm                               Automatically remove the container and its associated anonymous volumes
                                         when it exits
      --runtime string                   Runtime to use for this container
      --security-opt list                Security Options
      --shm-size bytes                   Size of /dev/shm
      --sig-proxy                        Proxy received signals to the process (default true)
      --stop-signal string               Signal to stop the container
      --stop-timeout int                 Timeout (in seconds) to stop a container
      --storage-opt list                 Storage driver options for the container
      --sysctl map                       Sysctl options (default map[])
      --tmpfs list                       Mount a tmpfs directory
  -t, --tty                              Allocate a pseudo-TTY
      --ulimit ulimit                    Ulimit options (default [])
  -u, --user string                      Username or UID (format: <name|uid>[:<group|gid>])
      --userns string                    User namespace to use
      --uts string                       UTS namespace to use
  -v, --volume list                      Bind mount a volume
      --volume-driver string             Optional volume driver for the container
      --volumes-from list                Mount volumes from the specified container(s)
  -w, --workdir string                   Working directory inside the container
```

## 🌞 On va ajouter un site Web au conteneur NGINX

```powershell
[lucas@localhost ~]$ sudo mkdir nginx
[sudo] password for lucas:
[lucas@localhost ~]$ ls
nginx
[lucas@localhost ~]$ touch index.html
[lucas@localhost ~]$ rm index.html
[lucas@localhost ~]$ cd nginx/
[lucas@localhost nginx]$ touch index.html
touch: cannot touch 'index.html': Permission denied
[lucas@localhost nginx]$ !!
touch index.html
touch: cannot touch 'index.html': Permission denied
[lucas@localhost nginx]$ !!!
touch index.html!
touch: cannot touch 'index.html!': Permission denied
[lucas@localhost nginx]$ sudo touch index.html
[sudo] password for lucas:
[lucas@localhost nginx]$ sudo touch site_nul.conf
[lucas@localhost nginx]$ chown lucas:lucas -R .
chown: changing ownership of './index.html': Operation not permitted
chown: changing ownership of './site_nul.conf': Operation not permitted
chown: changing ownership of '.': Operation not permitted
[lucas@localhost nginx]$ sudo chown lucas:lucas -R .
[sudo] password for lucas:
[lucas@localhost nginx]$ docker run -d -p 9999:8080 -v /home/lucas/nginx/index.html:/var/www/html/index.html -v /home/lu
cas/nginx/site_nul.conf:/etc/nginx/conf.d/site_nul.conf nginx
116a36352f8988ae9c65630f2cc88f04cb245bd01d0298708269cb702b744013
docker: Error response from daemon: driver failed programming external connectivity on endpoint dazzling_poincare (0bcd583043a6fa7edb321330aaa19995cdd313f489aca4b6dc20063030c1cc45): Bind for 0.0.0.0:9999 failed: port is already allocated.
[lucas@localhost nginx]$ docker rm -f 8ec9a9d0da23
8ec9a9d0da23
[lucas@localhost nginx]$ docker run -d -p 9999:8080 -v /home/lucas/nginx/index.html:/var/www/html/index.html -v /home/lucas/nginx/site_nul.conf:/etc/nginx/conf.d/site_nul.conf nginx
304b8b6edcdf4df0b81bb798c4b178ed6355f89a13324df6ed1e8d7361f15005
[lucas@localhost nginx]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS
                 NAMES
304b8b6edcdf   nginx     "/docker-entrypoint.…"   14 seconds ago   Up 13 seconds   80/tcp, 0.0.0.0:9999->8080/tcp, [::]:9999->8080/tcp   kind_bhabha
```

## 🌞 Lance un conteneur Python, avec un shell

```powershell
[lucas@localhost nginx]$ docker run -it python bash
Unable to find image 'python:latest' locally
latest: Pulling from library/python
fdf894e782a2: Pull complete
5bd71677db44: Pull complete
551df7f94f9c: Pull complete
ce82e98d553d: Pull complete
5f0e19c475d6: Pull complete
abab87fa45d0: Pull complete
2ac2596c631f: Pull complete
Digest: sha256:9255d1993f6d28b8a1cd611b108adbdfa38cb7ccc46ddde8ea7d734b6c845e32
Status: Downloaded newer image for python:latest
root@13f7167b0991:/#
```

## 🌞 Installe des libs Python

```powershell
root@13f7167b0991:/# pip install aiohttp
Collecting aiohttp
  Downloading aiohttp-3.11.10-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.7 kB)
Collecting aiohappyeyeballs>=2.3.0 (from aiohttp)
  Downloading aiohappyeyeballs-2.4.4-py3-none-any.whl.metadata (6.1 kB)
Collecting aiosignal>=1.1.2 (from aiohttp)
  Downloading aiosignal-1.3.1-py3-none-any.whl.metadata (4.0 kB)
Collecting attrs>=17.3.0 (from aiohttp)
  Downloading attrs-24.2.0-py3-none-any.whl.metadata (11 kB)
Collecting frozenlist>=1.1.1 (from aiohttp)
  Downloading frozenlist-1.5.0-cp313-cp313-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (13 kB)
Collecting multidict<7.0,>=4.5 (from aiohttp)
  Downloading multidict-6.1.0-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.0 kB)
Collecting propcache>=0.2.0 (from aiohttp)
  Downloading propcache-0.2.1-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (9.2 kB)
Collecting yarl<2.0,>=1.17.0 (from aiohttp)
  Downloading yarl-1.18.3-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (69 kB)
Collecting idna>=2.0 (from yarl<2.0,>=1.17.0->aiohttp)
  Downloading idna-3.10-py3-none-any.whl.metadata (10 kB)
Downloading aiohttp-3.11.10-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.7/1.7 MB 3.7 MB/s eta 0:00:00
Downloading aiohappyeyeballs-2.4.4-py3-none-any.whl (14 kB)
Downloading aiosignal-1.3.1-py3-none-any.whl (7.6 kB)
Downloading attrs-24.2.0-py3-none-any.whl (63 kB)
Downloading frozenlist-1.5.0-cp313-cp313-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (267 kB)
Downloading multidict-6.1.0-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (131 kB)
Downloading propcache-0.2.1-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (227 kB)
Downloading yarl-1.18.3-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (339 kB)
Downloading idna-3.10-py3-none-any.whl (70 kB)
Installing collected packages: propcache, multidict, idna, frozenlist, attrs, aiohappyeyeballs, yarl, aiosignal, aiohttp
Successfully installed aiohappyeyeballs-2.4.4 aiohttp-3.11.10 aiosignal-1.3.1 attrs-24.2.0 frozenlist-1.5.0 idna-3.10 multidict-6.1.0 propcache-0.2.1 yarl-1.18.3
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager, possibly rendering your system unusable.It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv. Use the --root-user-action option if you know what you are doing and want to suppress this warning.
root@13f7167b0991:/# pip install aioconsole
Collecting aioconsole
  Downloading aioconsole-0.8.1-py3-none-any.whl.metadata (46 kB)
Downloading aioconsole-0.8.1-py3-none-any.whl (43 kB)
Installing collected packages: aioconsole
Successfully installed aioconsole-0.8.1
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager, possibly rendering your system unusable.It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv. Use the --root-user-action option if you know what you are doing and want to suppress this warning.
root@13f7167b0991:/#
```