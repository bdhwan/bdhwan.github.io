---
layout: post
title: "Fix ng build"
date: 2021-03-05 10:41:14 +0900
categories: angular
---

angular 9.x 를 사용하면서 

```
ng bulid --prod --aot 
```

에서 멈춰서 끝나지 않을 경우 


tsconfig.json 파일에

```
    "target": "es2015" -> "target": "es5"
```

로 변경하면 완료됨 



https://stackoverflow.com/a/65576002
