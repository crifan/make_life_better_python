# 类和对象

## 继承

举例：用Python实现类的**继承**

```python
from pyspider.result import ResultWorker

class AutohomeResultWorker(ResultWorker):

    def __init__(self, resultdb, inqueue):
        """init mysql db"""
        print("AutohomeResultWorker init")
        print("resultdb=%s, inqueue=%s" % (resultdb, inqueue))
        # init parent
        ResultWorker.__init__(self, resultdb, inqueue)

        # init current
        # print("self.mysqldb=%s" % (self.mysqldb))
        # if self.mysqldb is None:
        self.mysqldb = MysqlDb()
        print("self.mysqldb=%s" % self.mysqldb)
```
