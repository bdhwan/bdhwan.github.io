---
layout: post
title: "Jenkins connection from external on Mac"
date: 2021-03-03 10:41:14 +0900
categories: jenkins
---


<h1>
Jenkins connection from external on Mac
</h1>

맥에 젠킨스를 설치한 뒤 외부에서 접속 하려고 하면 접속이 되지 않는다.   

/usr/local/Cellar/jenkins/2.282/homebrew.mxcl.jenkins.plist 

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>homebrew.mxcl.jenkins</string>
    <key>ProgramArguments</key>
    <array>
      <string>/usr/local/opt/openjdk@11/bin/java</string>
      <string>-Dmail.smtp.starttls.enable=true</string>
      <string>-jar</string>
      <string>/usr/local/opt/jenkins/libexec/jenkins.war</string>
      <string>--httpListenAddress=127.0.0.1</string> <---제거
      <string>--httpPort=8080</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
  </dict>
</plist>
```



/Users/fumi/Library/LaunchAgents 로 plist 파일 복사 후 <string>--httpListenAddress=127.0.0.1</string> 제거

```
cp /usr/local/Cellar/jenkins/2.282/homebrew.mxcl.jenkins.plist /Users/fumi/Library/LaunchAgents 
```

젠킨스 스톱 & 시작

```
launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.jenkins.plist
```

외부에서 접속 가능



젠킨스 업그레이드 
```
sudo chown -R $(whoami) $(brew --prefix)/*
sudo brew upgrade jenkins
```

