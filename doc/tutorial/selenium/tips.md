---
title: 实用技巧
---



## 手机模式进行自动化


我们可以通过  ```desired_capabilities``` 参数，指定以手机模式打开chrome浏览器

参考代码

```py
from selenium import webdriver

mobile_emulation = { "deviceName": "Nexus 5" }

chrome_options = webdriver.ChromeOptions()

chrome_options.add_experimental_option("mobileEmulation", mobile_emulation)

driver = webdriver.Chrome( desired_capabilities = chrome_options.to_capabilities())

driver.get('http://www.baidu.com')

input()
driver.quit()
```


## 冻结界面

有些网站上面的元素， 我们鼠标放在上面，会动态弹出一些内容。 

比如，百度首页的右上角，有个 **更多产品** 选项，如下图所示

![image](https://user-images.githubusercontent.com/36257654/44762007-09953a00-ab78-11e8-979e-da7933a78b54.png)


如果我们把鼠标放在上边，就会弹出 下面的 糯米、音乐、图片 等图标。

如果我们要用 selenium 自动化 点击 糯米图标，就需要 F12 查看这个元素的特征。

但是  当我们的鼠标 从 糯米图标 移开， 这个 栏目就整个消失了， 没办法点击 开发者工具栏的 查看箭头， 再去 点击  糯米图标 ，查看其属性。

怎么办？



可以如下图所示：

![image](https://user-images.githubusercontent.com/36257654/44762324-3e55c100-ab79-11e8-89af-4a744d775c45.png)

在 开发者工具栏 console 里面执行如下js代码

```js
setTimeout(function(){debugger}, 5000)
```

这句代码什么意思呢？

表示在 5000毫秒后，执行 debugger 命令

执行该命令会 浏览器会进入debug状态。 debug状态有个特性， 界面被冻住，  不管我们怎么点击界面都不会触发事件。


<br>

所以，我们可以在输入上面代码并回车 执行后， 立即 鼠标放在界面 右上角 更多产品处。

这时候，就会弹出  下面的 糯米、音乐、图片 等图标。 

然后，我们仔细等待 5秒 到了以后， 界面就会因为执行了 debugger 命令而被冻住。


然后，我们就可以点击 开发者工具栏的 查看箭头， 再去 点击  糯米图标 ，查看其属性了。




<br>

{% include sharepost.html %}