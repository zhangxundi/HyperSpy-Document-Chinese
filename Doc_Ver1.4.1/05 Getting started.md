# 快速入门实践

## 在Windows下开始Python

如果您使用的是bundle安装，那么您应该能够使用上下文菜单来启动。右键单击包含要分析的数据的文件夹，选择“在此处Jupyter notebook”或“在此处Jupyter qtconsole”。我们推荐使用Jupyter notebook，因为与传统的控制台相比，Notebook模式有许多优势，这也会在后面的章节中进行说明。

后面几节中的示例都会基于Notebook操作。以Notebook启动后，会在默认浏览器中出现一个新选项卡，列出所选文件夹中的文件。要启动python笔记本，请在页面右上角的“新建”下拉菜单中选择“python3”。此时，会在新标签中打开我们所需的笔记本。

## 在Linux和MacOS中开始Python

您可以通过打开一个系统终端并执行`ipython`来启动IPython（也可以选择在前面加上一些可选项，如“qtconsole”）。然而，在大多数情况下，与HyperSpy交互工作最合适的方式是使用 [Jupyter Notebook](http://jupyter.org/)（以前被称为IPython Notebook），它的启动方式如下:

```
$ jupyter notebook
```

Linux用户可能会发现从[文件管理器的上下文菜单](https://github.com/hyperspy/start_jupyter_cm)启动 Jupyter/IPython 更方便。在各种操作系统中，也可通过[双击已有的笔记本文件](https://github.com/takluyver/nbopen)来打开。

## 在Notebook（或终端）中开始HyperSpy

通常，在执行任何绘图命令之前，您需要使用`%matplotlib`（称为Jupyter magic）来[设置IPython以便与matplotlib进行交互式绘图](http://ipython.readthedocs.org/en/stable/interactive/plotting.html)。因此，通常在启动IPython之后，您可以通过在IPython终端中执行以下两行代码来导入HyperSpy并设置交互式matplotlib绘图

（在这些文档中，我们通常使用Python提示符`>>>`，但您可能会看到`In[1]:` 等等)。

```python
>>> %matplotlib qt
>>> import hyperspy.api as hs
```

注意，要执行笔记本中的代码行，必须按`Shift+Return`。（有关Notebook及其功能的详细信息，请打开Notebook中的帮助菜单）。接下来，导入两个有用的模块：numpy 和 matplotlib.pyplot，如下所示：

```python
>>> import numpy as np
>>> import matplotlib.pyplot as plt
```

文档的其余部分将假设您已经完成了这一步。我们还假设您安装了至少一个HyperSpy的GUI包：[jupyter widgets GUI](https://github.com/hyperspy/hyperspy_gui_ipywidgets) 或 [traitsui GUI](https://github.com/hyperspy/hyperspy_gui_traitsui)。：默认情况下，如果没有安装某个GUI包，HyperSpy会警告用户。可以使用`Preferences` GUI关闭这些警告（更多信息请参见[这里](http://hyperspy.org/hyperspy-doc/current/user_guide/getting_started.html#configuring-hyperspy-label)）。您也可以通过编程方式关闭这些警告：

```python
>>> import hyperspy.api as hs
>>> hs.preferences.GUIs.warn_if_guis_are_missing = False
>>> hs.preferences.save()
```

现在您已经准备好加载数据了（参见下面的内容）。

*v1.3版本中的更改：*HyperSpy可用于所有matplotlib后端，包括支持嵌入到jupyter笔记本中的交互式绘图的nbagg后端。

> **警  告**
>
> 在Python2中使用qt4后端时，导入HyperSpy后必须执行matplotlib magic，因此qt必须是默认的HyperSpy后端。

> **注  意**
>
> 在无句柄系统中运行时，需要适当设置matplotlib后端，以避免“无法连接到X服务器”的错误，例如:
>
> ```python
> >>> import matplotlib
> >>> matplotlib.rcParams["backend"] = "Agg"
> >>> import hyperspy.api as hs
> ```
>
> 

## 获取帮助

在使用IPython时，可以通过在函数名中添加问号来访问文档（被称为Python术语中的docstring）。例如：

```python
>>> hs?
>>> hs.load?
>>> hs.signals?
```

这种语法是显示与给定函数（Python术语为docstring）关联的帮助的标准方式之一的快捷方式，也是IPython的许多特性之一，IPython是HyperSpy在底层使用的交互式Python shell。

请注意，代码的文档正在编写中，所以还没有对所有对象进行文档化。您可以在以在HyperSpy网站上找到最新的文档。

## 自动补齐

IPython 的另一个有用特性是使用选项卡和箭头键可以自动补齐命令和文件名。强烈建议您阅读 IPython 文档（特别是入门部分）了解更多有用的特性。这些特性将在交互式地使用 HyperSpy/Python 时提高效率。

## 加载数据

HyperSpy正常载入后，您可以输入如下代码来从支持的文件格式（参见[支持的格式](http://hyperspy.org/hyperspy-doc/current/user_guide/io.html#supported-formats)）中加载数据：

> **注  意**
>
> load函数返回一个对象，该对象包含从文件中读取的数据。我们将这个对象赋值给变量 `s`，但是您可以选择任何您喜欢的（有效）变量名。对于文件名，不要忘记包含引号和文件扩展名。

如果没有参数传递给load函数，将会弹出一个窗口，允许通过OS文件管理器选择一个文件，例如：

```python
>>> # This raises the load user interface
>>> s = hs.load()
```

同时也可以加载多个文件，甚至可以堆叠多个文件。有关详细信息，请阅读 [加载文件：load函数](http://hyperspy.org/hyperspy-doc/current/user_guide/io.html#loading-files)。

## 从numpy array中加载数据

HyperSpy可以通过将任何numpy数组分配给一个BaseSignal类的方式来操作它。该方法用途广泛。例如，加载HyperSpy还不支持的格式存储的数据（假设它们可以用另一个Python库读取），或者研究由其他Python库生成的numpy数组。只需要从 `signals` 模块中选择最合适的信号，并将该numpy数组传递给构造函数，从而创建一个新的实例：

```python
>>> my_np_array = np.random.random((10,20,100))
>>> s = hs.signals.Signal1D(my_np_array)
>>> s
<Signal1D, title: , dimensions: (20, 10|100)>
```

numpy数组存储在singal类的 `data` 属性中。

## 加载示例数据以及在线数据库中的数据

HyperSpy内置了一些示例数据，可以在*hs.datasets.example_signals*中找到，例如：

```python
>>> hs.datasets.example_signals.EDS_TEM_Spectrum().plot()
```

1.4版本后的新函数： `artificial_data`

同时也有人工数据集，这些数据集类似于真实的实验数据：

```python
>>> s = hs.datasets.artificial_data.get_core_loss_eels_signal()
>>> s.plot()
```

1.0版本后的新函数： `eelsdb()`

*hs.datasets*中的`eelsdb()`函数可以直接从EELS数据库中加载频谱图。例如，下述代码可以加载数据库中现有的所有三氧化硼频谱：

```python
>>> hs.datasets.eelsdb(formula="B2O3")
[<EELSSpectrum, title: Boron oxide, dimensions: (|520)>,
 <EELSSpectrum, title: Boron oxide, dimensions: (|520)>]
```

## 导航和信号维度

在HyperSpy中，数据被解释为信号数组。因此，数据轴是不相等的。HyperSpy会区分*信号*和*导航*轴。大多数函数都在信号轴上操作，在导航轴上迭代。例如，一个EELS频谱图（比如一个2D光谱array）有X，Y和能量损失三个维度。在HyperSpy中，X和Y是导航维度，能量损失是信号维度。为了使这种区别更加明显，对象的表示包括导航和信号维度之间的分隔符`|`，例如。

在HyperSpy中，频谱图像具有一维信号和二维导航，并存储在Signal1D子类中。

```python
>>> s = hs.signals.Signal1D(np.zeros((10, 20, 30)))
>>> s
<Signal1D, title: , dimensions: (20, 10|30)>
```

图像型数据具有二维信号和一维导航维，并存储在Signal2D子类中。

```python
>>> im = hs.signals.Signal2D(np.zeros((30, 10, 20)))
>>> im
<Signal2D, title: , dimensions: (30|20, 10)>
```

注意：与数组顺序相比，HyperSpy会重新排列坐标轴。下面几段将解释它是如何，以及为什么这样做的。

根据数组的排列方式，有些轴的迭代速度要比其他轴快。拿读书来举例：对于一般的印刷书籍，从左至右从上而下的阅读是非常快的。然而，如果你的字是竖着排的，自上而下阅读会很不方便。如果每段话都在不同的页面上，而且每一个单词都要翻5-6页，那就非常耗时。同样的思想也适用于这里——为了遍历数据（通常用于绘图，但也适用于任何其他操作），您希望保持它的顺序以便进行“快速访问”。

在Python中（更显式的numpy），“快速轴顺序”是C顺序（也称为行-主顺序）。这意味着numpy数组的**最后一个轴**是迭代最快的（即书中的行）。另一种排序约定是F 顺序 （也称为列-主顺序），它是相反的：—数组的第一个轴是迭代最快的。在这两种情况下，轴离快轴越远，迭代就越慢。这好比就是阅读所有页面的第一行，然后是第二行，以此类推。

当数据按顺序采集时，通常按采集顺序存储。当数据集被加载时，HyperSpy通常以相同的顺序将数据集存储在内存中，这对计算机是有好处的。然而，HyperSpy将对这些轴进行重新排序和分类，使用户更容易操作。让我们想象一个单一的numpy数组，其中包含在不同的时间、不同的日期以不同的曝光次数获得的场景的图片。在numpy中，数组的维数是(D, E, Y, X)。这个顺序使得按照获取图像的顺序快速遍历图像。从人类的角度来看，这个数据集只是图像的集合，因此HyperSpy首先将图像轴(X和Y)划分为信号轴，其余轴为导航轴。然后，它反转了每组轴的顺序，因为许多人习惯于首先获得X轴，更普遍地说，是从左到右获取轴的顺序。因此，HyperSpy中的相同轴是这样显示的:(E, D | X, Y)。

将其扩展到任意维度，默认情况下，我们反转numpy轴，将其切成两个块（信号和导航），然后交换这些块，至少在打印时是这样。例如：

在后台，HyperSpy还负责以“机器友好”的方式将数据存储在内存中，因此在导航轴上迭代总是很快。

## 设置axis属性

轴（axes）由`AxesManager`类管理和存储，该类存储在信号类的`axis_manager`属性中。可以通过索引AxesManager访问各个轴。如：

```Python
>>> s = hs.signals.Signal1D(np.random.random((10, 20 , 100)))
>>> s
<Signal1D, title: , dimensions: (20, 10|100)>
>>> s.axes_manager
<Axes manager, axes: (<Unnamed 0th axis, size: 20, index: 0>, <Unnamed 1st
axis, size: 10, index: 0>|<Unnamed 2nd axis, size: 100>)>
>>> s.axes_manager[0]
<Unnamed 0th axis, size: 20, index: 0>
```

axis属性可以通过设置DataAxis属性来设置，例如：

```Python
>>> s.axes_manager[0].name = "X"
>>> s.axes_manager[0]
<X axis, size: 20, index: 0>
```

一旦定义了轴的名称，就可以通过它的名称来使用它，例如:

```python
>>> s.axes_manager["X"]
<X axis, size: 20, index: 0>
>>> s.axes_manager["X"].scale = 0.2
>>> s.axes_manager["X"].units = "nm"
>>> s.axes_manager["X"].offset = 100
```

还可以通过调用AxesManager的`GUI()`方法来使用GUI设置axis属性：

```python
>>> s.axes_manager.gui()
```

![axes_manager_gui_ipywidgets](C:\Users\ftxun\Documents\GitHub\HyperSpy-Document-Chinese\Doc_Ver1.4.1\images\axes_manager_gui_ipywidgets.png)

*AxesManager ipywidgets GUI.*

或者使用`DataAxis`：

```python
>>> s.axes_manager["X"].gui()
```

![](C:\Users\ftxun\Documents\GitHub\HyperSpy-Document-Chinese\Doc_Ver1.4.1\images\data_axis_gui_ipywidgets.png)

*DataAxis ipywidgets GUI.*

要简单地改变“当前位置”（即导航轴的索引），你可以使用导航滑块：

```python
>>> s.axes_manager.gui_navigation_sliders()
```

![](C:\Users\ftxun\Documents\GitHub\HyperSpy-Document-Chinese\Doc_Ver1.4.1\images\axes_manager_navigation_sliders_ipywidgets.png)

*Navigation sliders ipywidgets GUI.*

## 使用数量和单位换算

每个轴的比例尺和偏移量都可以进行设置和检索。

```python
>>> s = hs.signals.Signal1D(np.arange(10))
>>> s.axes_manager[0].scale_as_quantity
1.0 dimensionless
>>> s.axes_manager[0].scale_as_quantity = '2.5 µm'
>>> s.axes_manager
<Axes manager, axes: (|10)>
            Name |   size |  index |  offset |   scale |  units
================ | ====== | ====== | ======= | ======= | ======
---------------- | ------ | ------ | ------- | ------- | ------
     <undefined> |     10 |        |       0 |     2.5 |     µm
>>> s.axes_manager[0].offset_as_quantity = '2.5 nm'
<Axes manager, axes: (|10)>
            Name |   size |  index |  offset |   scale |  units
================ | ====== | ====== | ======= | ======= | ======
---------------- | ------ | ------ | ------- | ------- | ------
     <undefined> |     10 |        |     2.5 | 2.5e+03 |     nm
```

在内部，HyperSpy使用[Pint(品脱)](http://pint.readthedocs.io/)库来管理比例和偏移量。`scale_as_quantity`和`offset_as_quantity`属性返回品脱对象：

```python
>>> q = s.axes_manager[0].offset_as_quantity
>>> type(q) # q is a pint quantity object
pint.quantity.build_quantity_class.<locals>.Quantity
>>> q
2.5 nanometer
```

`AxesManager`的`convert_units`方法可进行单位转换，默认情况下（无参数引入）会将所有axis单元转换为最优单元，以避免使用太大或太小的数字。

每个轴也可以使用`DataAxis`的`convert_to_units`方法单独转换：

```python
>>> axis = hs.hyperspy.axes.DataAxis(size=10, scale=0.1, offset=10, units='mm')
>>> axis.scale_as_quantity
0.1 millimeter
>>> axis.convert_to_units('µm')
>>> axis.scale_as_quantity
100.0 micrometer
```

## 保存文件

数据可以保存为几种文件格式。格式由文件名的扩展名指定。

```python
>>> # load the data
>>> d = hs.load("example.tif")
>>> # save the data as a tiff
>>> d.save("example_processed.tif")
>>> # save the data as a png
>>> d.save("example_processed.png")
>>> # save the data as an hspy file
>>> d.save("example_processed.hspy")
```

有些文件格式更适合于维护关于如何处理数据的信息。HyperSpy中的首选格式是hspy，它基于HDF5格式。这种格式保存了尽可能多的信息。

有一些可选的标志可以传递给save函数。有关详细信息，请参见[将数据保存到文件中](http://hyperspy.org/hyperspy-doc/current/user_guide/io.html#saving-files)。

## 访问和设置元数据

加载文件时，HyperSpy将所有元数据存储在原始元数据`original_metadata`属性中。此外，其中一些元数据和HyperSpy生成的任何新元数据都存储在`metadata`属性中。

```python
>>> s = hs.load("NbO2_Nb_M_David_Bach,_Wilfried_Sigle_217.msa")
>>> s.metadata
├── original_filename = NbO2_Nb_M_David_Bach,_Wilfried_Sigle_217.msa
├── record_by = spectrum
├── signal_type = EELS
└── title = NbO2_Nb_M_David_Bach,_Wilfried_Sigle_217

>>> s.original_metadata
├── DATATYPE = XY
├── DATE =
├── FORMAT = EMSA/MAS Spectral Data File
├── NCOLUMNS = 1.0
├── NPOINTS = 1340.0
├── OFFSET = 120.0003
├── OWNER = eelsdatabase.net
├── SIGNALTYPE = ELS
├── TIME =
├── TITLE = NbO2_Nb_M_David_Bach,_Wilfried_Sigle_217
├── VERSION = 1.0
├── XPERCHAN = 0.5
├── XUNITS = eV
└── YUNITS =

>>> s.set_microscope_parameters(100, 10, 20)
>>> s.metadata
├── TEM
│   ├── EELS
│   │   └── collection_angle = 20
│   ├── beam_energy = 100
│   └── convergence_angle = 10
├── original_filename = NbO2_Nb_M_David_Bach,_Wilfried_Sigle_217.msa
├── record_by = spectrum
├── signal_type = EELS
└── title = NbO2_Nb_M_David_Bach,_Wilfried_Sigle_217

>>> s.metadata.TEM.microscope = "STEM VG"
>>> s.metadata
├── TEM
│   ├── EELS
│   │   └── collection_angle = 20
│   ├── beam_energy = 100
│   ├── convergence_angle = 10
│   └── microscope = STEM VG
├── original_filename = NbO2_Nb_M_David_Bach,_Wilfried_Sigle_217.msa
├── record_by = spectrum
├── signal_type = EELS
└── title = NbO2_Nb_M_David_Bach,_Wilfried_Sigle_217
```

## 配置HyperSpy

可以使用`Preferences`类定制HyperSpy的行为。最简单的方法是通过调用`gui()`方法：

```python
>>> hs.preferences.gui()
```

如果安装并启用了某个HyperSpy GUI包，该命令应该会弹出Preferences用户界面：

![](C:\Users\ftxun\Documents\GitHub\HyperSpy-Document-Chinese\Doc_Ver1.4.1\images\preferences.png)

*Preferences user interface.*

1.3版本之后的新特性：可以打开或者关闭GUI

还可以通过编程设置首选项。例如，可通过下述代码来禁用traitsui GUI元素并将设定更改保存到磁盘：

```python
>>> hs.preferences.GUIs.enable_traitsui_gui = False
>>> hs.preferences.save()
```

1.3版本中的改变：如下的项目已经被删除：

`General.default_export_format`, `General.lazy`, `Model.default_fitter`, `Machine_learning.multiple_files`, `Machine_learning.same_window`, `Plot.default_style_to_compare_spectra`, `Plot.plot_on_load`, `Plot.pylab_inline`, `EELS.fine_structure_width`, `EELS.fine_structure_active`, `EELS.fine_structure_smoothing`, `EELS.synchronize_cl_with_ll`, `EELS.preedge_safe_window_width`,`EELS.min_distance_between_edges_for_fine_structure`.

## 消息日志

1.0版本后的新功能

HyperSpy将消息写入[Python日志程序](https://docs.python.org/3/howto/logging.html#logging-basic-tutorial)。默认日志级别为“WARNING”，这意味着只显示警告和更严重的事件消息。默认值可以在[首选项](http://hyperspy.org/hyperspy-doc/current/user_guide/getting_started.html#configuring-hyperspy-label)中设置。或者，可以使用`set_log_level()` 设置它：

```python
>>> import hyperspy.api as hs
>>> hs.set_log_level('INFO')
>>> hs.load(r'my_file.dm3')
INFO:hyperspy.io_plugins.digital_micrograph:DM version: 3
INFO:hyperspy.io_plugins.digital_micrograph:size 4796607 B
INFO:hyperspy.io_plugins.digital_micrograph:Is file Little endian? True
INFO:hyperspy.io_plugins.digital_micrograph:Total tags in root group: 15
<Signal2D, title: My file, dimensions: (|1024, 1024)
```

