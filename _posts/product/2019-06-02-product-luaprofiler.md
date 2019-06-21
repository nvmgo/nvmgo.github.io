---
layout: post
title: LuaProfiler
description: ""
category: product
excerpt: 只需要添加一句代码，就可以对Lua代码中得函数进行效率统计
---

### 只需要添加一句代码，就可以对Lua代码中得函数进行效率统计

### 使用方法
* 将Scripts下的Nvmgo文件夹复制到项目中
* 然后在C#调用main.lua之前调用`[xxlua].DoString(Nvmgo.LuaProfiler.Startup());`
* 运行项目，打开Windows/Profiler，所有主要的lua函数将显示在里面，名字带有前缀[L]

### 调用示例
```
[xxlua].DoString(Nvmgo.LuaProfiler.Startup());
[xxlua].DoString("require('main')");
```

### Examples
打开Examples/Main.unity, 然后打开Windows/Profiler查看
  
### 联系方法
Email：nvmgo@foxmail.com