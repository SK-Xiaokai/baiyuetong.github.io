---
title: 文件目录处理
toc: true
---

## 读取某种编码格式的文件内容

```py
# encoding参数指定编码方式为 utf8，
# 如果是gbk编码， 应该写 encoding='gbk'
f = open('tmp.txt','r',encoding='utf8')

# read 方法会在读取文件中的原始字节串后， 根据上面指定的utf8解码为字符串对象返回
content = f.read()

# 文件操作完毕后， 使用close 方法关闭该文件对象
f.close()

print(content)
```

## 以指定utf8编码格式写文件

```py
# 指定编码方式为 utf8
f = open('tmp.txt','w',encoding='utf8')

# write方法会将字符串编码为utf8字节串写入文件
f.write('白月黑羽：祝大家好运气')

# 文件操作完毕后， 使用close 方法关闭该文件对象
f.close()
```

## 对文件路径名的操作

对于文件名的操作，比如 获取文件名称，文件所在目录，文件路径的拼接等，都可以使用 os.path 模块。

不要使用格式化字符串的方法来做，特别是如果你的程序需要在Linux、Windows等多个平台运行的时候更应如此。

而 os.path 模块知道Unix和Windows系统之间的差异，它能够可靠地处理类似 Data/data.csv 和 Data\data.csv 这样的文件路径差异。

比如：

```py
>>> import os
>>> path = '/Users/beazley/Data/data.csv'

>>> # 获取路径中的文件名部分
>>> os.path.basename(path)
'data.csv'

>>> # 获取路径中的目录部分
>>> os.path.dirname(path)
'/Users/beazley/Data'

>>> # 文件路径的拼接
>>> os.path.join('tmp', 'data', os.path.basename(path))
'tmp/data/data.csv'

```


## 判断文件、目录是否存在

使用下面的方法来判断文件或者目录是否存在
```py
import os
os.path.exists('d:/systems/cmd.exe')
os.path.exists('d:/systems')
```

<br>

如果你要判断指定路径是否是文件，可以这样

```py
import os
os.path.isfile('d:/systems/cmd.exe')
```

<br>

如果你要判断指定路径是否是目录，可以这样

```py
import os
os.path.isdir('d:/systems')
```


## 获取文件的大小和日期

```py
>>> os.path.getsize('/etc/passwd')
3669
>>> os.path.getmtime('/etc/passwd')
1272478234.0
>>> import time
>>> time.ctime(os.path.getmtime('/etc/passwd'))
'Wed Apr 28 13:10:34 2010'
>>>
```


## 递归的遍历目录下面所有的文件

假如我们要获取某个目录中所有的 文件， 包括子目录里面的文件。 
可以使用  os库中的walk方法

比如我们要得到某个目录下面所有的子目录 和所有的文件，存放在两个列表中

可以这样写代码


```py
import os

# 目标目录
targetDir = r'd:\tmp\util\dist\check'
files = []
dirs  = []

# 下面的三个变量 dirpath, dirnames, filenames
# dirpath 代表当前遍历到的目录名
# dirnames 是列表对象，存放当前dirpath中的所有子目录名
# filenames 是列表对象，存放当前dirpath中的所有文件名

for (dirpath, dirnames, filenames) in os.walk(targetDir):
   files += filenames
   dirs += dirnames

print(files)
print(dirs)
```



## 得到目录中所有的文件和子目录名

```py
import os

# 目标目录
targetDir = r'd:\tmp\util\dist\check'


files =  os.listdir(targetDir)
print(files)
```

listdir返回的是该目录下面所有的文件和子目录。

如果我们只需要获取目录中所有的文件，或者只需要子目录，可以这样

```py
import os
from os.path import isfile, join,isdir

# 目标目录
targetDir = r'd:\tmp\util\dist\check'

# 所有的文件
print([f for f in os.listdir(targetDir) if isfile(join(targetDir, f))])

# 所有的目录
print([f for f in os.listdir(targetDir) if isdir(join(targetDir, f))])
```


## 得到目录中指定扩展名的文件和子目录

可以使用glob库

```py
import glob
exes = glob.glob(r'd:\tmp\*.txt')

print(exes)
```


## 创建目录

os.makedirs 可以递归的创建目录结构，比如

```py
import os
os.makedirs('tmp/python/fileop',exist_ok=True)
```

会在当前工作目录下面创建 tmp目录，在tmp目录下面再创建 python目录，在Python目录下面再创建fileop目录

 ```exist_ok=True```  指定了，如果某个要创建的目录已经存在，也不报错

## 删除文件或目录

os.remove 可以删除一个文件，比如

```py
os.remove('sdf.py')
```

shutil.rmtree() 可以递归的删除某个目录所有的子目录和子文件
比如

```py
import shutil
shutil.rmtree('tmp')
```




{% include sharepost.html %}