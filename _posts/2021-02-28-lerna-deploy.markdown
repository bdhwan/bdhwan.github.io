---
layout: post
title: "Lerna Monorepo 환경에서 변경된 패키지만 배포하기"
date: 2021-02-28 23:02:14 +0900
categories: monorepo
---


<h1>
Lerna Monorepo 환경에서 변경된 패키지만 배포하기
</h1>


`Monorepo` 는 서비스에 필요한 모든 프로젝트들을 같은 repository에 저장하는 소프트웨어 개발 전략이다. `Lerna`는 이런 레파지토리의 패키지들을 관리할 수 있는 라이브러리이다. 

![lerna_logo](/_site/assets/img/lerna_logo.png)



<h2>문제</h2>
서비스가 성장할수록 패키지들이 많아지기 시작한다. Monorepo로 할 경우 모든 서비스의 소스를 한번에 관리하고 깃허브를 이용한 이슈 관리와 마일스톤 관리가 하나로 이루어져 관리측면에서 많은 장점이 있다. 개발하는 과정에서도 하나의 이슈는 보통 서버와 클라이언트 두개 이상의 패키지에 수정이 가해지게 되는데 이를 하나의 이슈와 브랜치로 관리가 되어 소스관리에서도 유리하다. 
Monorepo를 적용했을 때 가장 먼저 나타난 문제점은 배포에 있었다.    
개별 reposetory로 개발을 할 때는 하당 레파지토리의 git push 이벤트에 맞추어 배포가 이루어지도록 만들어져 있었다.    
repository가 하나로 합쳐지면서 모든 패키지에 변화가 일어날 때마다 푸시 이벤트가 발생하여 의도치 않은 배포가 발생하였다.    
예를 들어 서버만 변경이 일어났는데 클라이언트, 관리자, 다른 서버들이 모두 다 배포가 되는 상황이 되었다.  
이를 해결하기 위해 개별 패키지의 브랜치를 따로 만드는 방법, 수동으로 배포를 실행하는 방법 등을 탐색하였다.  
수동으로 배포를 적용하였지만 역시나 스타트업의 서비스라 빈번한 배포가 발생할 때마다 수동으로 눌러주어야하는 불편함이 가장 크게 나타났다. 

<h2>해결 방안</h2>
여러 방안을 탐색 중 lerna에서 제공하는 솔루션이 있었다.   


```
lerna run some-script
```

는 packages/ 하위 프로젝트에 해당 some-script 있으면 모두 실행하는 스크립트이다. 
예를 들어 


```
lerna run build-admin
```

을 실행할 경우 packages/giftistar-api-server/packages.json 에 build-admin 이라는 script가 존재하면 이 스크립트를 실행하는 것이다. 


이때 뒤에 `--since HEAD~1` 를 붙이면 변경 사항이 있는 패키지만 해당 스크립트가 실행된다.

```
lerna run some-script --since HEAD~1
```

변경 사힝이 있는 패키지의 some-script 만 살행이 된다. 

이제 이 방법을 이용해 자동으로 변동 사항이 있는 패키지만 배포되는 방법을 적용하면
각 패키지속에 브랜치별 빌드 스크립트를 작성한다. 

package.json

```
"scripts": {
    ...
    "deploy": "sh deploy/deploy.sh"
    ...
  },
```


deploy.sh

```
#!/bin/bash
set -e
pwd
branch="$(cut -d'/' -f2 <<<${GIT_BRANCH})"
echo 'target branch = '${branch}
sh deploy/deploy-${branch}.sh
exit 0

```


deploy-master.sh

```
#!/bin/bash
set -e
echo 'master branch'

```


deploy-oper.sh

```
#!/bin/bash
set -e
echo 'oper branch'

```


deploy-beta.sh

```
#!/bin/bash
set -e
echo 'beta branch'

```

`deploy.sh` 에 브랜치별로 분기되는 코드를 추가하여 각 브랜치 별로 빌드스크립트를 작성하여 브랜치에 맞는 배포 스크립트를 만들 수 있다. 



[참고글]: https://itnext.io/how-to-deploy-only-changed-packages-in-a-lerna-monorepo-7e5fb234b32a
