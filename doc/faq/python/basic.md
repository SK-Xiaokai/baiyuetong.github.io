---
title: 基本数据类型操作
toc: true
---


## 合并2个列表
列表中要添加另外一个列表的内容很简单，用加号就可以了
```py
>>> a = [1,2,3]
>>> a += [4,5,6]
>>> a
[1, 2, 3, 4, 5, 6]
```


## 合并2个字典
字典x 中要添加 另外一个字典y的内容，可以使用字典的update方法
```py
>>> x = {'a':1, 'b': 2}
>>> y = {'b':10, 'c': 11}
>>> x.update(y)
>>> x
{'a': 1, 'b': 10, 'c': 11}
```

从上例中可以发现，如果有重复的key， 会被字典y中的内容取代

如果我们想将合并后的内容放到一个新的字典对象里面， 而不去修改x，y的内容，该怎么办呢？
可以使用下面的方法：

```py
z = dict(x.items() + y.items())
```



## 从列表中过滤元素

有时候，你想从一个列表中，根据某些条件过滤掉一些元素，生成一个新的列表。

比如：下面的列表

```py
numbers = [-5, 66, -4, -10, 97, 21, 13, -51]
```

你想从将该列表中所有的正数提取出来放到一个新的列表中，该怎么做？


简单的方法就是使用列表生成式（list comprehension）

```py
numbers = [-5, 66, -4, -10, 97, 21, 13, -51]
positives = [num for num in numbers if num > 0]
```

<br>

如果过滤的处理比较复杂，可以自己定义一个 函数用来判断 参数 是否符合过滤条件。

比如：如下一个列表变量 names，其中保存了一个班级学生的姓名。

现在需要得到其中可以评为三好学生的学生列表。

程序需要将每个学生姓名打印在屏幕上，给老师来判断，如果老师输入yes表示是三好学生，输入否则就不是。

可以这样做

```py
# 定义一个 过滤函数
def isExcellent(name):
    excellent = input(f'{name} 是三好学生吗？')
    if excellent == 'yes':
        return True
    else:
        return False

names = ["关羽", "张飞", "赵云", "马超", "黄忠"]

# filter函数 会将 names 里面的每个元素 传递给 过滤函数 isExcellent
# 过滤函数 返回 True 就会保存下来， 返回False 就过滤掉
excellentStudents = filter(isExcellent, names)



'''
filter 返回的是一个 iterator，而且是lazy（懒）的。
执行上面那行代码时，并不会立即 调用isExcellent处理 names里面的每个元素。

而是在后面使用到 excellentStudents 这个 iterator的时候，比如像下面这样
产生一个列表 : 

excellentStudentList = list(excellentStudents)


或者 直接用for循环来处理其中的元素:

for one in excellentStudents:
   print(one)

'''


# 要注意的是， excellentStudents 这个 iterator只能使用一次
# 如果你已经像这样使用过了

excellentStudentList = list(excellentStudents)
print(excellentStudentList)

# 下面这样再次使用，excellentStudents 里面就取不出元素来了。
for one in excellentStudents:
   print(one)

```




## 从字典中过滤元素

有时候，你想从一个字典中，根据某些条件过滤掉一些元素，生成一个新的字典。

比如：下面的字典，记录了三国武将的武力值

```py
guys = {
    '关羽' : 96, 
    '张飞' : 96, 
    '赵云' : 97, 
    '马超' : 96, 
    '黄忠' : 94, 
    '魏延' : 90, 
    '马岱' : 82, 
}
```

你想把 武力值 在 95 以上的 武将 放到一个新的字典中，该怎么做？


简单的方法就是使用字典生成式（dict comprehension）

```py
toughGuys = {guy:level for guy,level in guys.items() if level > 95}
print(toughGuys)
```

<br>

如果过滤的处理比较复杂，可以自己定义一个 函数用来判断 参数 是否符合过滤条件。
然后用 filter对其中元素进行过滤，做法和上面的 列表的过滤处理类似，这里不再赘述。




## 产生随机数 

如果想产生某个范围内的随机数字，可以使用random库里面的randint方法。

比如，要在0,9之间产生一个随机数：

```py
from random import randint 
print randint(0,9)
```



## 产生随机字符串

如果要产生一个随机的字符串，里面可以有大写字母和数字，

```py
''.join(random.choice(string.ascii_uppercase + string.digits) for _ in range(4))
```

其中 range(4) 指定了字符串的长度为4


python3.6以后，可以更简短一些，这样写

```py
import string,random
''.join(random.choices(string.ascii_uppercase + string.digits, k=4))
```

其中参数k指定了字符串的长度


如果随机字符串里面，可以有小写字母和数字，python3.6以后，可以这样写

```py
import string,random
''.join(random.choices(string.ascii_lowercase + string.digits, k=4))
```


详细内容，参考 
https://stackoverflow.com/questions/2257441/random-string-generation-with-upper-case-letters-and-digits-in-python





{% include sharepost.html %}