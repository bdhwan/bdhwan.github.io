---
layout: post
title: "Ionic build env on Mac"
date: 2021-03-03 10:41:14 +0900
categories: ionic
---


<h1>
Ionic build env on Mac
</h1>

nvm install
```
 sudo curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
```

확인
```
nvm --version
```

안나오면 ~/.zshrc 에 export ~~ 넣기 


node install 

```
nvm ls-remote
nvm install v14.16.0
```
 

cocoapods install 

```
sudo gem install cocoapods
pod setup
```

xcode

```
xcode-select --install
```

ionic cli install 

```
npm install -g @ionic/cli
```

```
npm install -g tsc
```