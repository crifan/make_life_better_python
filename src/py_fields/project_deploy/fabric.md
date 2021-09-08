# fabric

* `Fabric`：项目代码部署工具
  * 主要功能
    * SSH登录远程服务器，然后执行各种操作命令
      * 偶尔会用到命令操作执行的结果
  * 主要包含3部分
    * Invoke：
      * 主要处理：命令行中的参数导入，任务管理，shell命令执行等事情
      * 对于（此处hello world这种）和远程remote服务器没关系的，往往都是调用invoke实现的
      * 用户常需要导入Invoke，去实现命令解析等工作
    * Paramiko
      * 主要实现了底层和中层的SSH的功能：SSH和SFTP的会话，key的管理等
      * Fabric内部调用Paramiko，用户很少需要import导入Paramiko
    * Fabric
      * 打包了其他各种库和功能
        * 继承了Invoke的Context上下文
        * 封装了Paramiko底层的功能
        * 通过Paramiko的ssh_config去扩展了Invoke的配置系统
        * 实现了高层功能封装，比如端口转发的上下文管理等

## 使用Fabric之前一定要注意版本

* Fabric有3个版本
  * Fabric1
    * https://pypi.org/project/Fabric/
    * `pip install Fabric`
  * Fabric2
    * https://pypi.org/project/fabric2/
    * `pip install fabric2`
  * Fabric3
    * https://pypi.org/project/Fabric3/
    * `pip install fabric3`

### Fabric的3个版本的区别

* Fabric1和Fabric2，在pypi中的页面，就是同一个东西：
    * 都是Fabric的最新版：Fabric 2.x
        * 截至到`20180817`，安装出来的版本是：`2.3.1`
    * 而官网之所以弄出来个Fabric2是因为：
    * Fabric2和Fabric1相比，完全重写了，接口和功能都有很大改动
      * 官网也不建议你继续用Fabric1，建议升级到Fabric2
      * 最新版也早就支持Python 3.4+，和之前的Python2.7
* 而Fabric3，是非官网的
    * 是当之前Fabric1还没有支持Python3时，别人去fork出来，加了Python 3的支持的
    * 现在好像基本上不维护了

#### `Fabric 1` vs `Fabric 2`
* Fabric 1到Fabric 2的改动很多
  * 详见
    * http://www.fabfile.org/upgrading.html#upgrade-specifics
    * http://www.fabfile.org/upgrading.html#api-organization
  * 其中一些是：
    * 导入库的方式
      * `Fabric 1`
        ```python
        from fabric.api import *
        ```
      * `Fabric 2`
        ```python
        from invoke import task
        from fabric import Connection
        ```
        * 等等，具体情况需要根据之前自己的需求，从invoke，fabric等导入合适的功能模块
    * 任务函数定义
      * `Fabric 1`
        ```python
        def doSomething()
        ```
      * `Fabric 2`：要加上`@task`修饰符=装饰器
        ```python
        @task
        def doSomething()
        ```

### 如何选择Fabric的版本

* 尽量用最新的Fabric2
  * Mac中用`brew install fabric`
    * 已经是最新的`2.3.1`版本了
        ```bash
        > fab --version
        Fabric 2.3.1
        Paramiko 2.4.1
        Invoke 1.1.1
        ```
  * 如果`pip install`的话，应该是：
    * pip install fabric
    * pip install fabric2
      * 都是最新版本
* 尽量不要用之前旧的版本的`Fabric1`了
    * 如果还在用，建议升级到最新的`Fabric2`
      * Upgrading from 1.x — Fabric documentation
        * http://www.fabfile.org/upgrading.html#why-upgrade
* 不需要操心、忽略掉，所谓的、非官网的，现在已没价值的：`Fabric3`

## Fabric文档和资料

* 中文文档
  * 网上找到的（之前官网的）都是`Fabric 1`的
    * 概览 & 教程 — Fabric 文档
      * https://fabric-chs.readthedocs.io/zh_CN/chs/tutorial.html
  * 而最新的 Fabric官网
    * http://www.fabfile.org
      * 中都是最新的`Fabric 2+`的版本的
* 英文文档
  * Welcome to Fabric’s documentation! — Fabric documentation
    * http://docs.fabfile.org/en/latest/
  * Getting started — Fabric documentation
    * http://docs.fabfile.org/en/latest/getting-started.html

### fab

Fabric安装后，有个命令行工具，叫`fab`

* `fab`
  * 用法
    * Command-line interface — Fabric documentation
      * http://docs.fabfile.org/en/latest/cli.html
  * 参数
    * 首先是支持invoke的inv
      * inv[oke] core usage — Invoke documentation
        * http://docs.pyinvoke.org/en/latest/invoke.html#inv
      * 的所有参数
    * 其次额外加了些自己的参数
    * 默认会加载当前目录下的fabfile.py
  * 常用的类和函数功能
    * run
      * http://docs.fabfile.org/en/2.3/api/connection.html#fabric.connection.Connection.run
        * 是远程的执行，不是local本地
        * 调用的是invoke.runners.Runner.run
        * 注意不是context的run
    * Connection
      * http://docs.fabfile.org/en/2.3/api/connection.html#fabric.connection.Connection
    * Result
      * http://docs.pyinvoke.org/en/latest/api/runners.html#invoke.runners.Result

###  Fabric的使用

去写代码，一般叫做：`fabfile.py`

比如：

```python
from invoke import task

def fabLoadedPath():
    from fabric.main import program
    return program.collection.loaded_from

@task
def upload(context):
    # print("upload: context=%s", context)

    fabFilePath = fabLoadedPath()
    print("fabFilePath=%s" % fabFilePath)
```

然后再去命令行中通过`fab`去运行`fabfile.py`中的task：

```bash
fab upload
```

* `upload`是你的`task`的名字
  * =你`fabfile.py`中加了`@task`的函数名
