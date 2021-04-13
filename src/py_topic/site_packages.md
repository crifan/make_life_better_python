# site-packages

`site-packages`是个`文件夹`=`目录`，用来存放`Python`的第三方库。

换句话说，Python第三方库安装后，往往都可以在对应的`site-packages`中找到。

## 找到当前Python的site-packages的位置

背景：安装了个Python库`Django`，想要知道当前对应安装到哪里了，即找到对应的`site-packages`的位置

方法：

```bash
python3 -m site
```

或：

```bash
pip3 show Django
```

即可找到处`Django`所在的`Python3`的`site-packages`的位置是：

`/usr/lib/python3.4/site-packages`
