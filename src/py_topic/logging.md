# logging日志

## 设置File文件的输出格式

用：

```python
fileFormatter = logging.Formatter(
    fmt=fileLogFormat,
    datefmt=fileLogDateFormat
)
fileHandler.setFormatter(fileFormatter)
```

即可。

最新代码详见：

https://github.com/crifan/crifanLibPython/blob/master/python3/crifanLib/crifanLogging.py
