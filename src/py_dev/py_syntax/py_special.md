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

## 双星号 = 两个星号 = `**`

Python中的`**`是表示（被用来）展开传入函数的参数的 = 展开（函数参数）字段

典型场景：

想要给一个函数传递多个参数，但是又不确定传递几个

如果用：`if else`写法，会很繁琐

此时可以用：`dict`字典保存要传递的参数，在计算出要传递的参数后，最终用`**paramDict`传递参数进入

### 举例：同步印象笔记的笔记时的多参数传递

普通写法 = `if else`写法：

```python
    # 2. Sync to Evernote
    if isNewRes:
      if needUpdateAttributes:
        respNote = gEvernote.syncNote(
          noteGuid=noteDetail.guid,
          noteTitle=noteDetail.title,
          newContent=noteDetail.content,
          newResList=noteDetail.resources,
          newAttributes=noteDetail.attributes
        )
      else:
        respNote = gEvernote.syncNote(
          noteGuid=noteDetail.guid,
          noteTitle=noteDetail.title,
          newContent=noteDetail.content,
          newResList=noteDetail.resources
        )
    else:
      if needUpdateAttributes:
        respNote = gEvernote.syncNote(
          noteGuid=noteDetail.guid,
          noteTitle=noteDetail.title,
          newContent=noteDetail.content,
          newAttributes=noteDetail.attributes
        )
      else:
        respNote = gEvernote.syncNote(
          noteGuid=noteDetail.guid,
          noteTitle=noteDetail.title,
          newContent=noteDetail.content
        )
```

注：且如果参数更多，代码看起来会更乱

而双星号写法，就很简单，易读，易扩展：

```python
    # 2. Sync to Evernote
    syncParamDict = {
        # mandatory
        "noteGuid": noteDetail.guid,
        "noteTitle": noteDetail.title,
        # optional
        "newContent": noteDetail.content,
    }

    if isNewRes:
        syncParamDict["newResList"] = noteDetail.resources
      
    if needUpdateAttributes:
        syncParamDict["newAttributes"] = noteDetail.attributes

    respNote = gEvernote.syncNote(**syncParamDict)
```

### 注意事项

#### `Python version < 3.5 not allow keyword argument after **exception`

`Python 3.5`之前的版本，比如`Python 3.4`中，如下写法：

```python
self.connection = pymysql.connect(**self.config, cursorclass=pymysql.cursors.DictCursor)
```
会报错：

```bash
   self.connection = pymysql.connect(**self.config, cursorclass=pymysql.cursors.DictCursor)
                                                   ^
SyntaxError: invalid syntax
```

**原因**：此处的Python版本小于`3.5`，不支持`**someDictOrTuple`之后，再跟着`其他参数`的写法

**解决办法**：代码改为：

```python
self.config["cursorclass"] = pymysql.cursors.DictCursor
self.connection = pymysql.connect(**self.config)
```

即可。

## `with`

详见：

[【整理】python中的with的含义和用法](http://www.crifan.com/python_with_meaning_and_usage)

## 魔术方法 特殊方法

详见：

[【整理】Python 特殊方法 魔术方法](https://www.crifan.com/python_special_method_magic_method/)

## yield

详见：

[【已解决】Python中直接return数组和yield的区别](http://www.crifan.com/python_return_array_vs_yield)
