# 打包

写好Python代码，实现了功能后，想要给别人用。

除了直接给别人代码外，可以考虑：打包。

即把Python源码，打包成可执行文件，比如

* `Windows`中的`exe`
* `Mac`中的`dmg`

等，就可以使用对应工具：

* `PyInstaller`
  * 历史悠久，功能强大
  * TODO:整理内容过来
    * [【记录】用PyInstaller把Python代码打包成单个独立的exe可执行文件 – 在路上](https://www.crifan.com/use_pyinstaller_to_package_python_to_single_executable_exe/)
    * Windows中写bat脚本方便清理内容和编译运行PyInstaller打包和Electron打包
    * windows中用PyInstaller打包mitmdump的Python脚本为exe
    * windows中PyInstaller打包exe运行报错：Failed to execute script pyi_rth_pkgres ModuleNotFoundError pkg_resources.py2_warn
    * Mac中PyInstaller打包期间前后拷贝文件和文件夹
    * mac中PyInstaller打包后的二进制文件在electron-builder打包后app中有些无法通过child_process的execFile运行
    * mitmdump被PyInstaller和electron-builder打包后功能不正常无法抓报到有效url链接地址
    * Mac中wine中用PyInstaller去打包exe
    * 已解决：PyInstaller如何打包2个主文件
    * [【已解决】mac中PyInstaller打包后的二进制文件在electron-builder打包后app中有些无法通过child_process的execFile运行](http://www.crifan.com/mac_pyinstaller_packaged_binary_file_electron_builder_app_not_work_by_child_process_execfile)
    * [【未解决】pyinstaller打包运行失败：failed to execute script __main__](http://www.crifan.com/pyinstaller_package_run_failed_to_execute_script_main)
    * [［已解决］pyinstaller打包exe运行出错：fatal error returned -1](http://www.crifan.com/python_pyinstaller_package_exe_run_fatal_error_returned_minus_one)
* `Nuitka`
  * 新出的工具
