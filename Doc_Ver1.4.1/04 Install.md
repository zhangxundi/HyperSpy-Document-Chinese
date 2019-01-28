# 安装HyperSpy

在Windows系统下安装HyperSpy最简单的方法是安装 [HyperSpy Bundle](http://hyperspy.org/hyperspy-doc/current/user_guide/install.html#hyperspy-bundle) 。

如果您需要在Linux，MacOs或者Windows系统的 [Anaconda Python发行版](http://docs.continuum.io/anaconda/) 中安装HyperSpy，可参考 [用Anaconda安装HyperSpy（Linux，MacOs，Windows](http://hyperspy.org/hyperspy-doc/current/user_guide/install.html#quick-anaconda-install) 。

如果您对Python很熟悉，可以通过 [Python installers](http://hyperspy.org/hyperspy-doc/current/user_guide/install.html#install-with-python-installers) 或者 [从源文件](http://hyperspy.org/hyperspy-doc/current/user_guide/install.html#install-source) 安装。

>  **警    告**
>
> 从HyperSpy0.8.4 开始仅支持Python3。如果您需要在Python2.7中安装，请使用HyperSpy0.8.3版本。

## Windows下安装HyperSpy Bundle

0.6版本后的新特性

最早，在Windows下安装HyperSpy是需要通过安装HyperSpy Bundle实现的。HyperSpy Bundle是一个包括了HyperSpy的 [WinPython](http://winpython.github.io/) 定制化发行版，依赖于多个其他的Python科学库。

关于HyperSpy的下载和更多信息请参阅：https://github.com/hyperspy/hyperspy-bundle

## 快速指南：Anacoda下安装HyperSpy（Linux，MacOs，Windows）

Anacoda是我们最推荐也是最简单的安装方式（使用Intel MKL库编译）。且学术许可免费。

1. 下载并安装 [Anaconda](https://store.continuum.io/cshop/anaconda/) 。如果您不熟悉Anaconda，请参阅它们的 [用户指南](https://docs.continuum.io/anaconda/)。

2. 然后，在Anaconda Prompt、Linux/Mac终端或Microsoft Windows命令提示符中执行以下*conda*命令来安装HyperSpy。（这取决于您的操作系统以及您如何安装了Anaconda，请参阅 [Anaconda用户指南](https://docs.continuum.io/anaconda/)）。

   ```
   $ conda install hyperspy -c conda-forge
   ```

3. （可选）从HyperSpy v1.3开始，[GUI入门元素](https://github.com/hyperspy/hyperspy_gui_traitsui)不会被自动地安装（不过 [Jupyter GUI 元素](https://github.com/hyperspy/hyperspy_gui_ipywidgets)会安装）。如果需要安装，可运行下述命令：

   ```shell
   $ conda install hyperspy-gui-traitsui -c conda-forge
   ```

> **注    意**
>
> 从HyperSpy0.8.4开始仅支持Python3。如果您需要在Python2.7中安装，请使用HyperSpy0.8.3版本：
>
> ```shell
> $ conda install traitsui
> $ pip install --upgrade hyperspy==0.8.3-1
> ```
>
> 

安装 [start_jupyter_cm](https://github.com/hyperspy/start_jupyter_cm) 可在文件管理器的右键菜单中显示startup功能（目前仅支持Gnome和Windows，不支持MacOS）。

了解更多请阅读下方内容。

## 用Python installers安装

HyperSpy在 [Python安装包索引](http://pypi.python.org/pypi) 中。因此，您可以通过 [pip](http://pypi.python.org/pypi/pip) 自动的下载和安装它。在使用下述代码前需要先安装pip。

使用pip安装：

```shell
$ pip install hyperspy
```

>  **警    告**
>
> 从HyperSpy0.8.4 开始仅支持Python3。如果您需要在Python2.7中安装，请使用HyperSpy0.8.3版本。
>
> ```
> $ pip install --upgrade hyperspy==0.8.3-1
> ```
>
> 

pip installs 会将直接相关的库自动安装。但是如果需要完整的功能，您可能需要安装一些其他的依赖项。如果需要完整安装，请使用如下命令：

```shell
$ pip install hyperspy[all]
```

您也可以自己选择外部依赖项：

- `learning` 安装机器学习相关的库
- `gui-jupyter` 安装使用 [Jupyter widgets](http://ipywidgets.readthedocs.io/en/stable/) GUI元素相关的库
- `gui-traitsui` 安装基于 [traitsui](http://docs.enthought.com/traitsui/) GUI元素的相关库
- `test` 安装HyperSpy 单元测试的相关库
- `mrcz` 安装mrcz插件
- `doc` 安装HyperSpy文档的插件
- `speed` 安装可提升部分功能运算速度的库

例如：

```shell
$ pip install hyperspy[learning, gui-jupyte
```

另请参阅 安装依赖库

最后，请注意HyperSpy依赖于许多通常需要编译的库，因此安装HyperSpy可能需要开发工具。如果上面的方法不适合您，请记住安装HyperSpy最简单的方法是[使用Anaconda](http://hyperspy.org/hyperspy-doc/current/user_guide/install.html#quick-anaconda-install)。

## 用二进制文件安装

对于Windows用户，我们提供二进制文件来进行安装（[参见下载页面](http://hyperspy.org/download.html)）在其他操作系统下我们推荐使用Python installers进行快速安装。

## 从源文件安装

## 安装发行版本

在Linux/Mac中可通过抓取tar.gz的文件进行安装（需要手动安装相关库）：

```
$ tar -xzf hyperspy.tar.gz
$ cd hyperspy
$ python setup.py install
```

同样，您也可以使用Python installer安装：

```shell
$ pip install hyperspy.tar.gz
```

## 安装开发版本

为了从我们的Git仓库中安装开发版本的HyperSpy，你需要先安装 [git](http://git-scm.com//) ，然后使用如下代码：

```shell
$ git clone https://github.com/hyperspy/hyperspy.git
```

要安装HyperSpy，您可以像在 [发行版本](http://hyperspy.org/hyperspy-doc/current/user_guide/install.html#install-released-source) 中那样进行。然而，如果您是从开发版本安装，您很可能更喜欢使用 [pip](http://www.pip-installer.org/) 开发模式安装HyperSpy：

```shell
$ cd hyperspy
$ pip install -e ./
```

在开发模式中，setup.py的生成或更新将利用git的post-checkout hook，清理编译的c文件，再对其进行重编译，并在下一次运行后执行 `build_ext—inplace` 。

### 创建Debian/Ubuntu二进制文件

您可以通过运行 *release_debian* 脚本将源文件转换成Debian/Ubuntu的二进制文件：

```shell
$ ./release_debian
```

> **注  意**
>
> 为了保证HypSpy的正常运行，如下库必须安装在您的系统中：
>
> python-stdeb, debhelper, dpkg-dev, python-argparser

## 安装依赖库

使用 `pip` 安装HyperSpy时会自动安装的库（请参阅 使用Python installer安装）。此外，如果您是从源文件安装HyperSpy，还需要安装Cython。如果您需要编译参考文档，sphinxcontrib-napoleon和sphinx_rtd_theme也是必需的。

如果在conda环境中从源文件安装时没有自动安装某些必需的库，则需要卸载HyperSpy后，先安装好这些库。

## 已知的一些问题

### Windows系统

- 如果HyperSpy无法在Windows中启动，请先尝试安装Microsoft Visual。

- 关于在旧版本中使用“Hyperspy here”快捷菜单的问题：由于Python的bug，有时卸载Hyperspy不会卸载快捷菜单中的“Hyperspy here”条目。请在具有管理员权限的Windows终端（命令行提示符）中运行以下代码，以手动删除条目：

  ```shell
  $ uninstall_hyperspy_here
  ```

- 如果HyperSpy引发MemoryError异常：

  - 如果您在64位系统中安装了32位版本的HyperSpy，那么请安装64位版本的HyperSpy。
  - 通过关闭其他应用程序或物理上向计算机添加更多RAM来增加可用RAM。

