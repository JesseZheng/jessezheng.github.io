---
title: 3.17学习小结
date: 2018-03-17 23:16:38
tags: 
- Anaconda
- Python
categories: 学习
---

> ## Anaconda是什么?

*简而言之就是<u>python</u>+<u>一堆用来数据处理的第三方包</u>+<u>python环境和这些包的管理器</u>*

1）Anaconda附带了一大批常用数据科学包，它附带了 conda、Python 和 150 多个科学包及其依赖项。因此你可以立即开始处理数据。

2）管理包
Anaconda 是在conda（一个包管理器和环境管理器）上发展出来的。
在数据分析中，你会用到很多第三方的包，而conda（包管理器）可以很好的帮助你在计算机上安装和管理这些包，包括安装、卸载和更新包。

3）管理环境
比如你在A项目中用了 Python2，而新的项目B老大要求使用Python 3，而同时安装两个Python版本可能会造成许多混乱和错误。这时候conda就可以帮助你为不同的项目建立不同的运行环境。

<!--  more  -->

> ## Conda命令关于管理环境

**1）创建环境**

在终端中使用:

```
conda create -nenv_name package_names
```

上面的命令中，env_name是设置环境的名称（-n 是指该命令后面的env_name是你要创建环境的名称），package_names 是你要安装在创建环境中的包名称。

**2）创建环境时，可以指定要安装在环境中的 Python 版本**

当你同时使用 Python 2.x 和Python 3.x 中的代码时这很有用。要创建具有特定 Python 版本的环境，例如创建环境名称为py3，并安装最新版本的Python3在终端中输入：

```
conda create -n py3 python=3 
```

或也可以这样创建环境名称为py2，并安装最新版本的Python2：

```
conda create -n py2 python=2
```

因为我做的项目不同，有时候会用到Python2，还有时候会用到Python3。所以我在自己的计算机上创建了这两个环境，并分别取了这样的环境名称：py2,py3。这样我可以根据不同的项目轻松使用不同版本的python。

如果你要安装特定版本（例如 Python3.6），请使用 

```
conda create -n py python=3.6
```

**3）进入和离开环境**

在 Windows 上，你可以使用activate my_env进入。在 OSX/Linux 上使用 `source activate my_env` 进入环境。

离开：

在 Windows 上，终端中输入： 

`deactivate`

在 OSX/Linux 上 输入：

`source deactivate`

**4）列出环境**

我有时候会忘记自己创建的环境名称，这时候用`conda env list`就可以列出你创建的所有环境。

你会看到环境的列表，而且你当前所在环境的旁边会有一个星号*。默认的环境（即当你不在选定环境中时使用的环境）名为root。

**5）删除环境**

如果你不再使用某个环境，可以使用` conda env remove -n env_name`删除指定的环境（在这里环境名为 env_name）。

> ## Conda关于包的管理

**1）安装包**

在终端中键入：

```
conda install package_name
```

例如，要安装 pandas，在终端中输入：

```
conda install pandas
```

你还可以同时安装多个包。类似 `conda install pandas numpy`  的命令会同时安装所有这些包。还可以通过添加版本号（例如 conda install numpy=1.10）来指定所需的包版本。

conda 还会自动为你安装依赖项。例如，scipy 依赖于 numpy，因为它使用并需要 numpy。如果你只安装 scipy (conda install scipy)，则 conda 还会安装 numpy（如果尚未安装的话）。

**2）卸载包**

在终端中键入 ：

```
conda remove package_names
```

上面命令中的package_names是指你要卸载包的名称，例如你想卸载pandas包：`conda remove pandas`

**3）更新包**

在终端中键入：

```
conda update package_name
```

如果想更新环境中的所有包（这样做常常很有用），使用：`conda update --all`。

**4）列出已安装的包**

```
#列出已安装的包
conda list
```

如果不知道要找的包的确切名称，可以尝试使用 `conda search search_term` 进行搜索。例如，我知道我想安装numpy，但我不清楚确切的包名称。我可以这样尝试：`conda search num`。



> ## python类中的普通方法，静态方法和类方法

*（装饰器**@classmethod** 和**@staticmethod**）*

```python
class A(object):
    #普通方法
    def foo(self,x):
        print "executing foo(%s,%s)"%(self,x)
	
    #类方法
    @classmethod
    def class_foo(cls,x):
        print "executing class_foo(%s,%s)"%(cls,x)
	
    #静态方法
    @staticmethod
    def static_foo(x):
        print "executing static_foo(%s)"%x

a=A()
```

下面是一个对象实体调用方法的常用方式.对象实体`a`被隐藏的传递给了第一个参数.

```python
a.foo(1)
# executing foo(<__main__.A object at 0xb7dbef0c>,1)
```

用**classmethods**装饰,隐藏的传递给第一个参数的是对象实体的类(`class A`)而不是`self`(实例对象).

```python
a.class_foo(1)
# executing class_foo(<class '__main__.A'>,1)
```

你也可以用类调用`class_foo`.实际上,如果你把一些方法定义成`classmethod`,那么<u>实际上你是希望用类来调用这个方法</u>,而不是用这个类的实例来调用这个方法.`A.foo(1)`将会返回一个`TypeError`错误,`A.class_foo(1)`将会正常运行:

用**staticmethods**来装饰,不管传递给第一个参数的是`self`(对象实体)还是`cls`(类).它们的表现都一样:

```python
a.static_foo(1)
# executing static_foo(1)

A.static_foo('hi')
# executing static_foo(hi)
```

`foo`只是个函数,但是当你调用`a.foo`的时候你得到的不仅仅是一个函数,你得到的是一个第一个参数绑定到`a`的"加强版"函数.`foo`需要两个参数,而`a.foo`仅仅需要一个参数.

`a`绑定了`foo`.下面可以知道什么叫"绑定"了:

```python
print(a.foo)
# <bound method A.foo of <__main__.A object at 0xb7d52f0c>>
```

如果使用`a.class_foo`,是`A`(类)绑定到了`class_foo`而不是`a`(对象实体).

```python
print(a.class_foo)
# <bound method type.class_foo of <class '__main__.A'>>
```

最后剩下静态方法,说到底它就是一个方法.`a.static_foo`只是返回一个不带参数绑定的方法.`A.static_foo`和`a.static_foo`只需要一个参数.

```python
print(a.static_foo)
# <function static_foo at 0xb7d479cc>
```



**参考资料**

[conda官方命令文档](https://conda.io/docs/user-guide/tasks/index.html)

[初学python者自学anaconda的正确姿势是什么？？](https://www.zhihu.com/question/58033789)

[Python 中的 classmethod 和 staticmethod 有什么具体用途？ - 知乎](https://www.zhihu.com/question/20021164)

[装饰器@staticmethod和@classmethod有什么区别_ _ Stackoverflow about Python](https://taizilongxu.gitbooks.io/stackoverflow-about-python/content/14/README.html)

