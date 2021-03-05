---
layout: post
title: "Docker system prune -f"
date: 2021-03-05 10:41:14 +0900
categories: docker
---

사용하지 않는 도커 이미지와 컨테이너 삭제하기 

```
docker system prune -f
```

크론으로 주기적으로 삭제하기 

```
sudo crontab -e
0 3 * * * /usr/bin/docker system prune -f
sudo service cron reload
```

[참고]: https://nickjanetakis.com/blog/docker-tip-32-automatically-clean-up-after-docker-daily