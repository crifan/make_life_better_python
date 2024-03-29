# Python2还是Python3

在（2020年）之前，入门Python时，还会遇到一个问题：

到底是选择（生态相对较广的）`Python 2`，还是选择（版本更新的）`Python 3`？

之前的回复一般是：新手可以考虑`Python 2`，稍微熟悉后换`Python 3`

而现在（2020年之后），官网（2020年之后就）早已放弃`Python 2`。

所以此问题已不存在，直接选择`Python 3`入手学习和后续开发，即可。

另外补充几句：

* 现在Python的生态中，还是有（一些、或者说不少）`Python 2`的库的
  * 但只要是活跃的、有生命力的库，会（早晚）尽快换到（支持）`Python 3`的
* `Python 3`的**性能**总体上比`Python 2`更好
  * 严格的说：`Python 3`的具体实现，往往比之前`Python 2`的实现，总体上性能更好
    * 大概水平：`Python 3`比`Python 2`快大概**1.2倍**左右
  * 细节的说：对于Python的解释器版本，`CPython`，`PyPy`：即时（JIT）编译器等来说
    * `PyPy` 比 `CPython` 更快
