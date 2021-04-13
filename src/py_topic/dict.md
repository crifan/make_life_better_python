# dict字典

下面整理`dict`相关内容

## 删除dict中的某个key值

比如

```python
someDict = {
    "someKey": "someValue",
    "otherKey": "otherValue"
}
```

想要删除`someKey`，则可以写成：

* 普通写法
  ```python
  del someDict["someKey"]
  ```
* 更`Pythonic`的写法
  ```python
  someDict.pop("someKey")
  ```

> #### warning:: 要确保被删除的`key`是存在的
> 
> 否则删除时会出现`KeyError`
> 
> 可以先判断存在`key`是否存在，再去删除，比如：
```python
keyToDelete = "someKey"
if keyToDelete in someDict:
    someDict.pop(keyToDelete)
```

## dict的递归的合并更新

背景：希望合并2个dict（json）值

代码：

```python
def recursiveMergeDict(aDict, bDict):
    """
    Recursively merge dict a to b, return merged dict b
    Note: Sub dict's won't be overwritten but also updated/merged
    """
    aDictItems = None
    if (sys.version_info[0] == 2): # is python 2
      aDictItems = aDict.iteritems()
    else: # is python 3
      aDictItems = aDict.items()

    for aKey, aValue in aDictItems:
      print("------ [%s]=%s" % (aKey, aValue))
      if aKey not in bDict:
        bDict[aKey] = aValue
      else:
        bValue = bDict[aKey]
        print("aValue=%s" % aValue)
        print("bValue=%s" % bValue)
        if isinstance(aValue, dict):
          recursiveMergeDict(aValue, bValue)
        elif isinstance(aValue, list):
          aValueListLen = len(aValue)
          bValueListLen = len(bValue)
          bValueListMaxIdx = bValueListLen - 1
          for aListIdx in range(aValueListLen):
            print("---[%d]" % aListIdx)
            aListItem = aValue[aListIdx]
            print("aListItem=%s" % aListItem)
            if aListIdx &lt;= bValueListMaxIdx:
              bListItem = bValue[aListIdx]
              print("bListItem=%s" % bListItem)
              recursiveMergeDict(aListItem, bListItem)
            else:
              # recursiveMergeDict(aListItem, aListItem)
              print("bDict=%s" % bDict)
              print("aKey=%s" % aKey)
              print("aListItem=%s" % aListItem)
              bDict[aKey].append(aListItem)

    return bDict

bookJson = recursiveMergeDict(templateJson, copy.deepcopy(currentJson))

pprint("-a"*40)
pprint(templateJson)
pprint("-b"*40)
pprint(currentJson)
pprint("-c"*40)
pprint(bookJson)
```

输出：

```bash
'-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a'
{u'pluginsConfig': {u'github-buttons': {u'buttons': [{u'count': True,
                                                      u'repo': u'gitbook_name',
                                                      u'size': u'small',
                                                      u'type': u'star',
                                                      u'user': u'crifan'},
                                                     {u'count': False,
                                                      u'size': u'small',
                                                      u'type': u'follow',
                                                      u'user': u'crifan',
                                                      u'width': u'120'},
                                                     {u'key1': u'string1',
                                                      u'key2': 999,
                                                      u'key3': True}]}}}
'-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b-b'
{u'pluginsConfig': {u'github-buttons': {u'buttons': [{u'repo': u'youdao_note_summary'}]}}}
'-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c-c'
{u'pluginsConfig': {u'github-buttons': {u'buttons': [{u'count': True,
                                                      u'repo': u'youdao_note_summary',
                                                      u'size': u'small',
                                                      u'type': u'star',
                                                      u'user': u'crifan'},
                                                     {u'count': False,
                                                      u'size': u'small',
                                                      u'type': u'follow',
                                                      u'user': u'crifan',
                                                      u'width': u'120'},
                                                     {u'key1': u'string1',
                                                      u'key2': 999,
                                                      u'key3': True}]}}}
```

实现了希望看到的效果：

* 合并a和b的dict
  * 如果包含子dict，则递归去合并
  * 如果包含list，则针对每个item去合并
    * 如果a的list比b多，则保留a多出的部分

注：最新代码已发布到：

https://github.com/crifan/crifanLibPython/blob/master/python3/crifanLib/crifanDict.py

中的`recursiveMergeDict`

## 把dict的json输出到文件且带缩进和不要unicode的`\uxxxx`

背景：`currentJson.json`中包含

```json
{
  "pluginsConfig": {
    "toolbar-button": {
      "url": "http://book.crifan.com/books/youdao_note_summary/pdf/youdao_note_summary.pdf"
    }, 
    "sitemap-general": {
      "prefix": "https://book.crifan.com/gitbook/youdao_note_summary/website/"
    }, 
    "github-buttons": {
      "buttons": [
        {
          "repo": "youdao_note_summary"
        }
      ]
    }
  }, 
  "description": "\u603b\u7ed3\u4e4b\u524d\u4f7f\u7528\u8fc7\u6709\u9053\u4e91\u7b14\u8bb0\u548c\u6709\u9053\u4e91\u534f\u4f5c\u7684\u5fc3\u5f97\u4f9b\u53c2\u8003", 
  "title": "\u6709\u9053\u4e91\u7b14\u8bb0\u548c\u4e91\u534f\u4f5c\u4f7f\u7528\u603b\u7ed3"
}
```

`\uxxxx`的特殊字符

希望导入后能正常解析成中文

最终代码：

```python
import codecs

with codecs.open("currentJson.json", 'w', encoding="utf-8") as tmpFp:
    json.dump(currentJson, tmpFp, indent=2, ensure_ascii=False)
```
