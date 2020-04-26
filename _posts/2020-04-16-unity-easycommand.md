---
layout: post
title: 通过Http调用Unity脚本
description: ""
category: Unity
---

以前在做打包时，需要调用Unity写的脚本，调用方式为
```
C:\program files\Unity\Editor\Unity.exe -quit -batchmode -executeMethod MyEditorScript.MyMethod -params xxxxxxxxxxx
```

这种方式有两个问题：
1. 每次都只要重启Unity，调用完成后也只能返回0和1
2. 传递参数比较麻烦，参数较多时，解析起来比较繁琐，更不用说时复杂参数

现在又要做类似功能，且传递参数复杂，因此想了一下，想通过Http调用方式来实现，思路如下：
1. 常开Unity，通过C#建立一个webserver，通过Http来传递命令
2. python脚本通过http调用来实现对Unity脚本的调用
3. 传递的格式采用json格式，方便定义
4. Unity命令执行完后响应python的http请求

Python调用示例如下：
```
def http_post(url,data_json):
    jdata = json.dumps(data_json)
    req = urllib2.Request(url, jdata)
    response = urllib2.urlopen(req)
    return response.read()
 
url = 'http://127.0.0.1:8080'
data_json = {'orderId': '10000001','type':'compile','logFile':'xxxxxxx'}
print("request:" + str(data_json))
resp = http_post(url,data_json)
print("response:" + str(resp))
```
项目链接：[https://github.com/nvmgo/Unity_EasyCommand](https://github.com/nvmgo/Unity_EasyCommand)