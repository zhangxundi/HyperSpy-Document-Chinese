# 序  言



## 什么是HyperSpy

HyperSpy是一个Python开源库，目的是提供一个分析多维信号数据集的工具（例如，一个2D的波谱图像）。

HyperSpy的目标是让单一信号和复合信号的分析更加容易和自然，并为多为数据集的分析提供简单易上手的工具。

它的模块化结构使其易于添加各种特性来分析不同类型的信号。



## HyperSpy的扩展

在本文档中，我们将构建在HyperSpy之上的外部程序称为“HyperSpy扩展”。这些程序可以提供额外的数据分析工具文件格式，添加图形用户界面，提供额外的盲源分离算法等。

我们有多个HyperSpy扩展。公开托管的扩展列表可搜索GitHub的 [hyperspy-extension](https://github.com/topics/hyperspy-extension) 主题

> **注  意：**
> 从2.0版本开始，HyperSpy将被分割成提供基础功能的核心模块（HyperSpy）
> 和一系列的扩展模块。



## 我们的版本

对我们来说，这个程序是一个研究工具，很像螺丝刀或格林函数（What is Green's function? Am I understand right???）。我们相信我们的工具越好，我们的研究也会越好。我们也认为，分享我们的研究工具，并以合作的方式打造它们，对知识的进步是有益的。通过合作避免重复发明轮子，我们也会进步得更快。尽管听起来很理想主义，但很多人都是这样想的，正是因为有了他们，这个项目才得以存在。



## HyperSpy的特性

HyperSpy是由使用它的一小部分人编写的，它的特殊性决定了它的特点:

- 与程序交互的主要方式是通过命令行。这是因为:
  - 感谢 [IPython](http://ipython.org/) 使得我们的命令行接口易于使用。
  - 使用命令行接口可以很容易地自动化数据分析，从而提高生产率。当然，缺点是学习曲线更陡，但我们已经尽量保持平稳。
- 也就是说，图形用户界面（GUI）元素是在具有明显的生产力优势的情况下才会提供的。请参见 [jupyter widgets GUI](https://github.com/hyperspy/hyperspy_gui_ipywidgets) 和 [traitsui GUI](https://github.com/hyperspy/hyperspy_gui_traitsui) 。如果您需要完整的、独立的GUI，那么 [HyperSpyUI](http://hyperspy.org/hyperspyUI/) 将非常适合您。
- 我们将HyperSpy视为一个协作项目，因此我们关心的是如何让其他人更容易地为它做出贡献。换句话说，我们希望最小化“用户成为开发人员”的门槛。为了实现这一目标，我们:
  - 使用开源许可，即 [GPL v3](http://www.gnu.org/licenses/gpl-3.0-standalone.html) 。
  - 尽量使代码简单易懂。
  - 选择用 [Python](http://www.python.org/) 编写，这是一种高级编程语言，具有[高质量的科学库](http://www.scipy.org/)，并且非常容易学习。
