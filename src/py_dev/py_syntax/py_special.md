# Python特有语法

## 代码缩进 表示 逻辑语义

Python中，和很多其他编程语言，在（空格、Tab制表符等）缩进上，不一样：

* 其他编程语言：缩进，往往是没有语法含义的，只是为了美观和易读
* `Python`：缩进，是有意义的，决定了代码的逻辑层次
  * 不同缩进层次，对应了不同的代码块
  * 别人评论
    * 缩进和空白是有意义的 -》 表示代码块
      * 这个叫做：offside rule
        * 注：
          * [Off-side rule - Wikipedia](https://en.wikipedia.org/wiki/Off-side_rule)
            * 类似于足球中的越位
              * 把本来没有意义的空白（和缩进），用于代码的缩进，有逻辑上的含义
                * -》翻译成汉语，可以说成是：过犹不及

TODO：

* 把之前的单独文章整理过来
  * [【教程】详解Python中代码缩进（Indent）：影响代码的内在逻辑关系和执行结果 – 在路上](https://www.crifan.com/tutorial_python_indent/)

## `with`

详见：

[【整理】python中的with的含义和用法](http://www.crifan.com/python_with_meaning_and_usage)

## 两个星号`**`的作用：展开字段

`**`是用于展开字典，作为函数参数

如果不确定要传几个参数，则可以用此写法，会显得更有优势和代码更简洁

对比说明如下：

* 普通写法

```python
    if needUpdateAttributes:
        updatedNote = updateNote(
            noteGuid=noteDetail.guid,
            noteTitle=noteDetail.title,
            newContent=updatedContent,
            newAttributes=noteDetail.attributes
        )
    else:
        updatedNote = updateNote(
            noteGuid=noteDetail.guid,
            noteTitle=noteDetail.title,
            newContent=updatedContent
        )
```

注：如果还有其他情况，则会有更多的if和else以及函数调用

* 双星号写法

上述普通写法，可以优化为用`**`两个星去展开函数参数：

```python
    updateParamDict = {
        "noteGuid": noteDetail.guid,
        "noteTitle": noteDetail.title,
        "newContent": updatedContent,
    }
    if needUpdateAttributes:
        updateParamDict["newAttributes"] = noteDetail.attributes

    updatedNote = updateNote(**updateParamDict)
```

好处：

如果还有更多参数，则都方便直接在dict中扩展即可。

## 魔术方法 特殊方法

详见：

[【整理】Python 特殊方法 魔术方法](https://www.crifan.com/python_special_method_magic_method/)

## yield

详见：

[【已解决】Python中直接return数组和yield的区别](http://www.crifan.com/python_return_array_vs_yield)
