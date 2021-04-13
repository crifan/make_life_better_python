# 关于Python的谬误

关于Python有些常见的谬误。

现整理如下，供知悉。

## Python速度慢

首先要搞清楚一个重要区别: `Python`是一门**编程语言**，而不是**运行时环境**

Python有几个（具体）实现 = 运行时：

* [CPython](https://en.wikipedia.org/wiki/CPython) 是参考（默认的）实现, 且也是广泛发布和使用的实现
* [Jython](https://en.wikipedia.org/wiki/Jython) 是Python用于`JVM`的是一个成熟的实现
* [IronPython](https://en.wikipedia.org/wiki/IronPython) 是`Microsoft`针对其自家的通用语言运行时——又名`.NET`实现的Python
* [PyPy](https://pypy.org/) 是一个正在日趋成熟的Python实现，拥有`JIT`编译，增量垃圾收集诸多先进的特性

每一个运行时都有其自己的性能特点, 而且它们本身也不慢。

这里更重要的地方在于

* 不能错误地用性能指标去评价**Python编程语言**
  * 而应该去用性能指标去评价一个**Python的运行时**
    * 且最好是针对一个特定的使用场景

清楚了上述逻辑后，下面给出一些例子来说明，其实Python（的运行时，在对应应用场景下）性能其实很强：

* 把 [NumPy](https://en.wikipedia.org/wiki/NumPy) 用作 [Intel 的 MKL SIMD接口](https://software.intel.com/en-us/articles/numpyscipy-with-intel-mkl)
* [PyPy](https://pypy.org/)的`JIT`编译能[达到比C还快的性能](https://morepypy.blogspot.com/2011/08/pypy-is-faster-than-c-again-string.html)
* [Disqus](https://disqus.com/)能在[同样的100个盒子上容纳两亿五千万到5亿用户](https://blog.disqus.com/post/62187806135/scaling-django-to-8-billion-page-views)
