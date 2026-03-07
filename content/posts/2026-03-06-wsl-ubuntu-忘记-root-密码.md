---
title: WSL Ubuntu 忘记 root 密码
description: ""
date: 2026-03-06T03:26:22.711Z
preview: ""
draft: true
tags: []
categories: []
---

以管理员打开 powershell, 执行以下命令

```shell
wsl --user root
```

执行以下命令, 输入新密码

```shell
passwd root
```
