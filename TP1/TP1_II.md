## 🌞 Récupérez des images

```powershell
[lucas@localhost ~]$ docker pull python:3.13
3.13: Pulling from library/python
Digest: sha256:9255d1993f6d28b8a1cd611b108adbdfa38cb7ccc46ddde8ea7d734b6c845e32
Status: Downloaded newer image for python:3.13
docker.io/library/python:3.13
[lucas@localhost ~]$ docker pull mysql:5.7
5.7: Pulling from library/mysql
20e4dcae4c69: Pull complete
1c56c3d4ce74: Pull complete
e9f03a1c24ce: Pull complete
68c3898c2015: Pull complete
6b95a940e7b6: Pull complete
90986bb8de6e: Pull complete
ae71319cb779: Pull complete
ffc89e9dfd88: Pull complete
43d05e938198: Pull complete
064b2d298fba: Pull complete
df9a4d85569b: Pull complete
Digest: sha256:4bc6bc963e6d8443453676cae56536f4b8156d78bae03c0145cbe47c2aad73bb
Status: Downloaded newer image for mysql:5.7
docker.io/library/mysql:5.7
[lucas@localhost ~]$ docker pull wordpress
Using default tag: latest
latest: Pulling from library/wordpress
bc0965b23a04: Already exists
e0aa8e8bfd10: Pull complete
f45eeb7b7c66: Pull complete
2802fa207e46: Pull complete
2bc706e6dbbe: Pull complete
8f2b85a95cfd: Pull complete
2586d713206f: Pull complete
086063f0275c: Pull complete
61a388cf2f83: Pull complete
73fd6b827991: Pull complete
c2dd75e58cab: Pull complete
3b01564181f9: Pull complete
16d45113a90d: Pull complete
4f4fb700ef54: Pull complete
c4f8720ddb1e: Pull complete
d374174149dd: Pull complete
f09c82e22e1b: Pull complete
dd7711b88413: Pull complete
a89cceed0693: Pull complete
dab7a4cf5d37: Pull complete
e6f609a11365: Pull complete
1bbc7feeba6d: Pull complete
Digest: sha256:2f3572d5cd722489fe47d59ed45d947dc9507f5a019eb0567ddf24aedf9257ed
Status: Downloaded newer image for wordpress:latest
docker.io/library/wordpress:latest
[lucas@localhost ~]$ docker pull linuxserver/wikijs
Using default tag: latest
latest: Pulling from linuxserver/wikijs
72387e7898ce: Pull complete
ec7680b185bf: Pull complete
b80232684b80: Pull complete
52e5d6eefe42: Pull complete
f224b10b4dc1: Pull complete
d179dce5799c: Pull complete
ff211b9bebf2: Pull complete
979004086415: Pull complete
Digest: sha256:45ecf23a3bf849a0bf0c9e2d832aede159e98efd29fef70bbc7ff4dd87522eba
Status: Downloaded newer image for linuxserver/wikijs:latest
docker.io/linuxserver/wikijs:latest
[lucas@localhost ~]$ docker images
REPOSITORY           TAG       IMAGE ID       CREATED         SIZE
linuxserver/wikijs   latest    863e49d2e56c   6 days ago      465MB
python               3.13      3ca4060004b1   9 days ago      1.02GB
python               latest    3ca4060004b1   9 days ago      1.02GB
nginx                latest    66f8bdd3810c   2 weeks ago     192MB
wordpress            latest    c89b40a25cd1   3 weeks ago     700MB
mysql                5.7       5107333e08a8   12 months ago   501MB
```

## 🌞 Lancez un conteneur à partir de l'image Python

```powershell
[lucas@localhost ~]$ docker run -it python bash
root@01a8c01dc3dd:/# python
Python 3.13.1 (main, Dec  4 2024, 20:40:27) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
```

## 🌞 Ecrire un Dockerfile pour une image qui héberge une application Python

```Dockerfile
FROM debian
RUN apt update
RUN apt install -y python3 python3-emoji

WORKDIR /app

COPY app.py .
ENTRYPOINT [ "python3", "app.py" ]
```

## 🌞 Build l'image et Lancer l'image

```powershell
[lucas@localhost python_app_build]$ docker build . -t python_app:version_de_ouf
[+] Building 1.4s (10/10) FINISHED                                                                       docker:default
 => [internal] load build definition from Dockerfile                                                               0.0s
 => => transferring dockerfile: 229B                                                                               0.0s
 => [internal] load metadata for docker.io/library/debian:latest                                                   0.9s
 => [internal] load .dockerignore                                                                                  0.0s
 => => transferring context: 2B                                                                                    0.0s
 => [1/5] FROM docker.io/library/debian:latest@sha256:17122fe3d66916e55c0cbd5bbf54bb3f87b3582f4d86a755a0fd3498d36  0.0s
 => [internal] load build context                                                                                  0.0s
 => => transferring context: 86B                                                                                   0.0s
 => CACHED [2/5] RUN apt update                                                                                    0.0s
 => CACHED [3/5] RUN apt install -y python3 python3-emoji                                                          0.0s
 => [4/5] WORKDIR /app                                                                                             0.1s
 => [5/5] COPY app.py .                                                                                            0.1s
 => exporting to image                                                                                             0.1s
 => => exporting layers                                                                                            0.0s
 => => writing image sha256:aebfd5176d644d14348cbe5010f4bc91a4ad288b05d1b74cd6ab84ad18dc1c12                       0.0s
 => => naming to docker.io/library/python_app:version_de_ouf                                                       0.0s
[lucas@localhost python_app_build]$ docker run python_app:version_de_ouf
Cet exemple d'application est vraiment naze 👎
[lucas@localhost python_app_build]$
```