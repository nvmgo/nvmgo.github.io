---
layout: post
title: 完美解决Unity高版本转低版本时，Prefab无法使用问题
description: ""
category: Unity
---

因为一些原因，项目需要从高版本转低版本，转完后，prefab无法拖进编辑器中使用，网上查了一些，基本都是要手动改prefab文件，对比了下跟我用的这个2018.4.14差别比较大，无法照着修改。

自己开始尝试研究两个版本的prefab格式对比，格式差别巨大的头大。。。 

但是幸运的发现在低版本中运行时，可以正常加载prefab，因此有了一个思路：在低版本中用程序将prefab加载进来，然后重新保存为prefab，再在编辑器中使用。

```
GameObject prefab = UnityEditor.AssetDatabase.LoadAssetAtPath("Assets/OldPrefab/Test.prefab", typeof(GameObject)) as GameObject;
UnityEditor.PrefabUtility.CreatePrefab("Assets/NewPrefab/Test.prefab", prefab);
```
新的prefab测试后可用，然后批量处理所有Prefab，问题解决:)