# MY-LEETCODE

Leetcode让我想起了小时候看的插图版脑筋急转弯，应该有开发智力，锻炼大脑之功效～

我在这里记录下了做题时的思考，希望能帮助自己有所提高。一方面可以帮助自己通过面试，另一方面可以提高自己的逻辑思维能力，提高工作效率。

Hopefully we can make some progress though the lovely questions!

## In The Beginning

代码和写作有相似之处，所以，工整的代码排版，统一的代码风格，也是代码质量的一部分。杂乱的代码，即使没有bug，也是有问题的。

以markdown为例，我的标准是每行新的内容之间，空一行。

对于python，我的标准是注释如果比较短，尽量不另起一行，一个方法里，不用空行。

## Overall

一般处理一个题目有四个过程。首先，**抽象问题**，明确需求，建立模型，把实际的问题抽象成计算机的问题；然后，**设计算法**，如何实现第一步中提取出的功能点呢，先想一想暴力穷举法吧，穷举法也是算法，题目至少可以解决问题才行，可以解决了之后，再考虑如何优化算法。<font color=red>算法</font>，和讨论使用的<font color=red>数据结构</font>，这两者相互关联，往往一个算法只能；第三步，**编写代码**，这里可能会遇到一些功能上的问题，比如使用特定的语言，会有特定的写法；最后，**设计测试用例**，检查BUG。

<br>

## 抽象问题

什么是计算机的问题？计算机能做的是，给一些数据条件，然后再经过计算，生产出一批新数据。

<br>

什么是实际的问题？实际问题比如提供一些要求，然后给出一个方案，判断一个方案是否正确。

<br>

我们要做的是把实际问题的条件和结果通过数据来表达，把要求一部分抽象成输入变量，把产出的结果抽象成输出变量，还有一部分要求抽象成**输入变量和输出变量间的关联**，要用逻辑表达式写出这些关联。抽象问题应该包括三个内容，明确输入变量，输出变量，和输入变量与输出变量之间的关联。

<br>

## 设计算法

**设计暴力穷举法** 做好了抽象问题这一环节，设计暴力穷举法应该是一件相对轻松的事。我们要做的就是用输入变量，根据输入变量与输出变量的关系，产出所有可能的结果并判断每一个结果，最终得出输出变量。

<br>

**优化算法**
