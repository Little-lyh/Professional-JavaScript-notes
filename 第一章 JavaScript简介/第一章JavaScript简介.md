## 第一章 JavaScript简介

​		**JavaScript**诞生于1995年，是由当时就职于Netscape公司的Brendan Eich（布兰登·  艾奇）所开发的。JavaScript的诞生是为了把表单信息发送到服务器才确定用户是否没有填入某个必填项、是否输入了无效的值。简单来说，就是为了实现**简单地数据验证**。然后随着时代的发展，JavaScript的发展已经不局限于简单地数据验证，而是具备了与浏览器窗口及其内容等几乎所有的方面交互的能力。比如我之前编写的简单地获取当前时间与星期，并显示在网页中。还有轮播图片等等。

​		JavaScript和ECMAScript通常都被人用来表达相同的含义，但是JavaScript的含义比ECMA-262中规定的要多得多。一个完整的JavaScript应该是有下列三个不同的部分组成。

- 核心（ECMAScript）
- 文档对象模型（DOM）
- 浏览器对象模型（BOM）

![1566442493587](C:\Users\Temton\Desktop\JavaScript 高级程序设计 第3版\image\JavaScript三种表示.png)



### ECMAScript

​		实现ECMAScript的宿主环境：Web浏览器、Node(一种服务器JavaScript平台)、Adobe Flash等。由ECMA-262定义的ECMAScript与Web浏览器是没有依赖关系的。ECMAScript本身并不包含输入和输出定义，它只规定了组成部分：**语法、类型、语句、关键字、保留字、操作符、对象**。也就是说：ECMAScript是对实现该规定的各个方面内容的语言的描述。JavaScript实现了ECMAScript，Adobe ActionScript同样也实现了ECMAScript。

- **ECMAScript和JavaScript之间的关系**
  - JavaScript只不过是为了操作Web，而在ECMAScript的基础上进行了符合ECMAScript规定组成部分内容的扩展，比如DOM，利用了ECMAScript的核心类型和语法提供更多更具体的功能
  - 从这样看来，Web浏览器只不过是ECMAScript的宿主环境而已，其他宿主环境包括Node和Adobe Flash
- **ECMAScript 产生过程**：
  - 阶段 0：Strawman 初稿
  - 阶段 1：Proposal 建议
  - 阶段 2：Draft 草案
  - 阶段 3：Candidate 
  - 候选阶段 4：Finished 完成



### 文档对象模型DMO

​		文档对象模型（DOM），全称 Document Object Model，是针对XML 但经过扩展用于HTML 的应用程序编 程接口（API，Application Programming Interface）。

​		原理：DMO将整个页面映射为一个多层节点结构。HTML或者XML页面中的每个组成部分都是某种类型的节点，这些节点又包含着不同类型的数据。

```
<html>
	<head>
		<title>Sample Page</title>
	</head>
	<body>
		<p>Hello World!</p>
	</body>
</html>
```

对应的DMO表示为：![DMO表示](C:\Users\Temton\Desktop\JavaScript 高级程序设计 第3版\image\DMO表示.png)

​		HTML或XML页面中的每个组成部分都是某种类型节点(比如：元素节点、属性节点、文本节点).通过树形图，开发人员获得了控制页面内容和结构的主动权。**借助DMO提供的API，开发人员可以轻松自如的删除、添加、替换或者修改任何节点。**

- 注意：DOM不仅在JavaScript中得到实现，在其他很多语言中也被应用
- DOM级别：
  1. DOM1
     - DOM核心(DOM Core 映射基于XML的文档结构，简化文档中任意部分的访问和操作)
     - DOM HTML(在DOM核心的基础上加以扩展，添加了针对HTML的对象和方法)
  2. DOM2
     - DOM视图(DOM Views):定义了跟踪不同文档(例如，应用CSS之前和之后的文档)视图的接口
     - DOM事件(DOM Events):定义了事件和事件处理的接口
     - DOM样式(DOM Style):定义了基于CSS为元素应用样式的接口
     - DOM遍历和范围(DOM Traversal and Range):定义了遍历和操作文档书的接口 扩展了DOM核心
  3. DOM3
     - 引入了统一方式加载和保存文档的方式————在DOM加载和保存模块中定义
     - 新增了验证文档的方法————在DOM验证模块中定义
     - 扩展了DOM核心，开始支持XML1.0,涉及XML infoset、XPath、XML Base



### 浏览器对象模型（BOM）

​		开发人员使用BOM 可以控制浏览器显示的页面以外的部分。从本质上将，BOM只处理浏览器窗口和框架；但是人们习惯吧所有浏览器的JavaScript扩展算作BOM的一部分。

- 弹出新浏览器窗口的功能
- 移动、缩放和关闭浏览器窗口的功能
- 提供浏览器详细信息的 **navigator **对象
- 提供浏览器所加载页面的详细信息的 **location** 对象
- 提供用户显示器分辨率详细信息的 **screen** 对象
- 对cookies 的支持
- 像XMLHTTPRequest 和IE 的ActiveXObject 这样的自定义对象