# copy拷贝

## `copy`和`deepcopy`

python中的值，比如一个`dict`，如果用了`copy`

```python
copiedDict = originDict.copy()
```

则根据官网文档：

[8.17. copy — Shallow and deep copy operations — Python 2.7.15 documentation](https://docs.python.org/2/library/copy.html)

则`copiedDict`叫做`shallow copy`=`影子拷贝`

-> 类似于`C`语言的指针

-> 修改了`copiedDict`，原先的`originDict`也同时被修改

而想要脱离关系，则需要用到**深度拷贝**

```python
import copy
deepCopiedDict = copy.deepcopy(originDict)
```

则`deepCopiedDict`和`originDict`就没有关系了

-> 修改`deepCopiedDict`，**不会影响**到`originDict`。
