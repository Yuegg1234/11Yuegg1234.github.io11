---

layout:     post
title:      IntelliJ IDEA tomcat控制台乱码解决方案
date:       2018-11-09
author:     Yuegg
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - blog
---

# IntelliJ IDEA tomcat控制台乱码解决方案
---
项目启动时，控制台输出中文乱码，解决方案，tomcat配置 VM options处添加`-Dfile.encoding=UTF-8`， 解决~