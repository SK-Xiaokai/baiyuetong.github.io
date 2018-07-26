---
title: 字符串操作
toc: true
---

## 字符 和 对应unicode数字 的转换

把 unicode数字转换为字符， 使用chr(), 比如：

```py
>>> chr(50)
'2'
>>> chr(20013)
'中'
```



反过来，要把 字符转换为对应的unicode数字，使用 ord()
该函数参数字符串里面只能有一个字符

```py
>>> ord('2')
50
>>> ord('中')
20013
```


直接用unicode 数字创建 字符串

```py
>>> '\u767d\u6708\u9ed1\u7fbd'
'白月黑羽'
```



##  使用split函数从字符串中提取内容

比如：从下面格式的字符串中提取出添加成功用户对应的UID号

```
添加用户 byhy(UID 5533)成功
```

可以这样写

```py
uid = content.split('(UID ')[1].split(')')[0]
print(f'uid is :{uid}')
```


##  使用正则表达式从字符串中提取内容

使用正则表达，可以从多种可能格式的字符串中，提取我们想要的内容
比如，我们想要从下面这几种可能格式的字符串中提取 用户对于的UID号

```
添加用户 byhy(UID 5533)成功
添加用户 byhy(UID: 5533)成功
添加用户 byhy(UID     5533)成功
```


使用下面代码就可以了

```py
import  re
uid =  re.findall(r'\(UID\W*(\d*)\)', content)[0]
```

其中  ```\(UID\W*(\d*)\)```   是正则表达式， 
 ```content```  是被搜索的字符串
 ```findall```  方法会获取所有匹配该正则表达式的 子字符串，所以返回的是一个列表

关于Python中的正则表达式用法可以参考文档：
https://docs.python.org/3/library/re.html



{% include sharepost.html %}