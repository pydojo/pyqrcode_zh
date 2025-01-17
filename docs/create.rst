创建二维码
*****************************************

QRCode 对象设计成一种聪明地如何建立二维码的形式。
它可以自动搞清楚使用什么模式和版本来建立一个二维码，
根据数据和错误纠正数量来完成创建二维码工作。
错误纠正级别默认为最高级别。

下面的一些例子都是建立二维码时使用了自动系统完成的。

.. code-block:: python

  >>> url = pyqrcode.create('http://uca.edu')
  >>> url = pyqrcode.create('http://uca.edu', error='L')

有许多情况你想要良好地控制如何生成二维码。你可以描述你要建立的二维码
所有的财产项，通过 :func:`pyqrcode.create` 函数中的可选参数来实现。
对于一个二维码来说，主要有3项财产。

其中 :term:`error` 参数是设置二维码错误纠正级别。
每个级别都是用对应的一个字母来表示： L, M, Q, 或 H；
每个级别对数据的错误纠正率分别是百分之 7, 15, 25, 或 30。
有许多方法来描述这个级别，阅读 :py:data:`pyqrcode.tables.error_level`
来了解所有可能的值。默认情况本参数设置成 `'H'` 最高级别，
但这样的二维码在一个版本下是拥有最小的数据容量。

其中 :term:`version` 参数描述了二维码的规模和数据容量。
版本都是任何一种整数，介于1到40之间。其中版本1是最小的二维码，
版本40是最大的二维码。默认情况使用数据的编码模式和错误纠正级别
来计算最小版本号。你也许想要自己描述本参数值，尤其是生成许多
二维码却含有不同的数据量。如此以来所有生成的二维码就都有同样的规模。

最后 :term:`mode` 参数是设置二维码数据要采用的编码模式。
四种编码中的3种是可用的。默认情况对数据使用最有效的编码模式。
你可以覆写这种行为，通过设置本参数来实现。
阅读 :py:data:`pyqrcode.tables.modes` 了解本参数可用的值。
在编码模式上更多的讨论可以在 :doc:`encoding` 文档种找到。

如下代码建立了一个含有 25% 错误纠正级别的二维码，规模是27，
并且强制使用了二进制编码模式（这要比数字编码模式好一点）。

.. code-block:: python

  >>> big_code = pyqrcode.create('0987654321', error='L', version=27, mode='binary')
