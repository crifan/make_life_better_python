# 版本和环境

* Python
  * 多版本共存 -> `pyenv`
    * 多版本共存
      * 多个主版本：`Python 2.x`和`Python3.x`
      * 同一主版本内多个小版本：`Python 3`的`Python 3.6`、`Python 3.7`等
  * 隔离不同项目的Python环境 = **虚拟环境** -> `virtualenv`、`pipenv`等
    * 专门处理科学计算相关 -> `conda`

## `Python 2`和`Python 3`的兼容

如果想要写代码，同时`支持`=`兼容`Python 2`和`Python 3`，则可以考虑用专门的库：

* `six`
  * Github
    * Python 2 and 3 compatibility library
      * https://github.com/benjaminp/six
  * 文档
    * Six: Python 2 and 3 Compatibility Library — six 1.14.0 documentation
      * https://six.readthedocs.io/

不过也需要了解到：

> 虽然利用`__future__`和`six`，可以写出同时兼容`Python 2/3`的程序。
> 
> 但我觉得这样看上去未免会使程序变得丑陋，而且很多`Python3`的新特性还没法用了（例如`asyncio`, `Type Hinting`, `f-string`等）
> 
> 所以还是希望Python3能够普及
