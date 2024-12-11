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
```