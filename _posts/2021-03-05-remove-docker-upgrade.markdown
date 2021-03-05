---
layout: post
title: "Remove docker and upgrade version"
date: 2021-03-05 10:41:14 +0900
categories: docker
---


기존 버전 삭제
```
sudo apt-get remove docker docker-ce docker-engine docker.io containerd runc

rm -rf /usr/bin/docker
```

설치 
```
 sudo apt-get update

 sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg


sudo apt-get update

sudo apt-get install -y docker-ce docker-ce-cli containerd.io

```


