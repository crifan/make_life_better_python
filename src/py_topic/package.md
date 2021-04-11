# 打包

写好Python代码，实现了功能后，想要给别人用。

除了直接给别人代码外，可以考虑：打包。

即把Python源码，打包成可执行文件，比如

* `Windows`中的`exe`
* `Mac`中的`dmg`

等，就可以使用对应工具：

* `PyInstaller`
  * 概述
    * 特点：简单好用，功能强大，历史悠久
    * 用法举例
      * 生成单一的exe文件
        * `pyinstaller.py -F ..\BlogsToWordpress\BlogsToWordpress.py`
      * 添加额外文件 = 添加必要的搜索路径（自动搜索到对应文件）
        * Windows中多个路径用分号`;`分隔开
          * `pyinstaller.py -F -p D:\tmp\tmp_dev_root\python\tutorial_summary\make_exe\BlogsToWordpress\libs;D:\tmp\tmp_dev_root\python\tutorial_summary\make_exe\BlogsToWordpress\libs\crifan;D:\tmp\tmp_dev_root\python\tutorial_summary\make_exe\BlogsToWordpress\libs\crifan\blogModules;D:\tmp\tmp_dev_root\python\tutorial_summary\make_exe\BlogsToWordpress\libs\thirdparty;D:\tmp\tmp_dev_root\python\tutorial_summary\make_exe\BlogsToWordpress\libs\thirdparty\chardet; ..\BlogsToWordpress\BlogsToWordpress.py`
      * 添加必要的搜索路径，且带图标
        * `pyinstaller.py -F -p D:\tmp\tmp_dev_root\python\tutorial_summary\make_exe\BlogsToWordpress\libs;D:\tmp\tmp_dev_root\python\tutorial_summary\make_exe\BlogsToWordpress\libs\crifan;D:\tmp\tmp_dev_root\python\tutorial_summary\make_exe\BlogsToWordpress\libs\crifan\blogModules;D:\tmp\tmp_dev_root\python\tutorial_summary\make_exe\BlogsToWordpress\libs\thirdparty;D:\tmp\tmp_dev_root\python\tutorial_summary\make_exe\BlogsToWordpress\libs\thirdparty\chardet; -i ..\BlogsToWordpress\BlogsToWordpress.ico ..\BlogsToWordpress\BlogsToWordpress.py`
  * 详解
    * [Python打包利器：PyInstaller](https://book.crifan.com/books/python_package_tool_pyinstaller/website/)
* `Nuitka`
  * 新出的工具
