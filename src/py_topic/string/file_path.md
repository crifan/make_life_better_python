# 文件路径

文件（夹）路径，也属于字符串中的一种。

对于早期的`Python 2`，对于字符串的支持，相对不够好：用起来要比较注意，才不会犯路径导致的各种错误。

此处整理出来，供借鉴参考。

## 路径写法不对导致库无法加载文件而报错

比如之前的：

[【已解决】Python中出错：pywintypes.com_error,Exception occurred,Microsoft Excel,could not be found – 在路上](https://www.crifan.com/python_pywintypes_com_error_exception_occurred_microsoft_excel_xls_could_not_be_found_check_the_spelling_of_the_file_name/)

遇到的：

如果文件路径写法不对：

即使用看起来正确的绝对路径：

```python
xlsPath = "D:\tmp\tmp_dev_root\python\excel_chart\chart_demo.xls"
absPath = os.path.abspath(xlsPath)
wb = xl.Workbooks.open(absPath)
```

也会导致错误：`pywintypes.com_error`

而实际上出错的原因是：此处的字符串的反斜杠，没有转义

即，当字符串中包含反斜杠字符串本身`\`时，需要用反斜杠去转义：

```python
xlsPath = "D:\\tmp\\tmp_dev_root\\python\\excel_chart\\chart_demo.xls"
```

才可以。

如果不想要把每个反斜杠都写2遍，则可以加上前缀`r`

```python
rawPath = r"D:\tmp\tmp_dev_root\python\excel_chart\chart_demo.xls"
wb = xl.Workbooks.open(rawPath)
```
