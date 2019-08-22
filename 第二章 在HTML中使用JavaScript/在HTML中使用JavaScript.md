## 第二章 在HTML中使用JavaScript

​		只要一提到把 JavaScript 放到网页中，就不得不涉及 Web 的核心语言——HTML。在当初开发JavaScript 的时候，Netscape 要解决的一个重要问题就是如何做到让 Java-Script 既能与 HTML页面共存，又不影响那些页面在其他浏览器中的呈现效果。经过尝试、纠错和争论，最终的决定就是为 Web 增加统一的脚本支持。而 Web 诞生早期的很多做法也都保留了下来，并被正式纳入 HTML 规范当中。

​		 JavaScript 插入到 HTML 页面中要使用`<script>`匀速。使用这个元素我们可以把JavaScript嵌入到HTML页面中，让脚本和标记混在一起；也可以包含外部的JavaScript文件。

### `<script>`元素

​		**属性：**

- `async`：可选。表示应该以及下载脚本，但是不应妨碍页面中的其他操作，比如下载其他资源或者等待加载其它脚本。只对外部脚本文件有效。
- `charset`：可选。表示通过`src`属性指定的代码的字符集。由于大多数浏览器会忽略他的值，因此这个属性很少有人使用。
- `defer`：可选。表示脚本可以延迟到文档完全被解析和显示之后再执行，只对外部脚本文件有效。IE7以及更早版本对于嵌入脚本也支持这个属性。
- `language`：已废弃。原来用于表示编写代码所使用的脚本语言（如JavaScript、JavaScript1.2或者VBScript）。大多数浏览器会忽略这个属性，因此也没有必要再用了。
- `src`：可选。表示包含要执行代码的外部文件。
- `type`：可选。可以看成是language的替代属性；表示编写代码使用的脚本语言的内容类型（也被称为MIME类型）。虽然`text/javascript`和`text/ecmascript`都已经被被推荐使用，但是人们一直以来使用的还是`text/javascript`。实际上，服务器在传送JavaScript文件是使用的MIME类型通常是`application/x-javascript`，但是在`type`中设置这个值却可能导致脚本被忽略。另外，在非IE浏览器中还可以使用以下的值：`application/javascript`和`application/ecmascript`。考虑到约定俗成和最大监督的浏览器兼容性，目前type属性的值依旧还是`text/javascript`。不过，这个属性并不是必需的，如果没有自定这个属性，则其默认值仍为`text/javascript`。

​		在使用 `<script> `嵌入 JavaScript 代码时，记住不要在代码中的任何地方出现 `</script>` 字符串。 例如，浏览器在加载下面所示的代码时就会产生一个错误：

```
<script type="text/javascript">
    function sayScript(){
    	alert("</script>");
    }
</script>
```

​		因为按照解析嵌入式代码的规则，当浏览器遇到字符串 `</script>`时，就会认为那是结束的`</script> `标签。而通过转义字符“/”可以解决这个问题

```
<script type="text/javascript">
    function sayScript(){
    	alert("<\/script>");
    }
</script>
```

 		**注意：**

- 带有 `src` 属性的`<script>`元素不应在其`<script>`和`</script>`标签之间再包含额外的 JavaScript 代码。如果包含了嵌入的代码，则只会下载并执行外部脚本文件，嵌入的代码会被忽略。



##### 标签的位置

​		现代Web应用程序一般都把全部JavaScript引用放在`<body>`元素中页面内容的后面，这样可以避免浏览器在加载JavaScript时呈现页面出现明显的延迟，而导致浏览器窗口一片空白。所以目前的标签位置写作如下示例：

```
<!DOCTYPE html>
<html>
	<head>
		<title>Example HTML Page</title>
	</head>
	<body>
		<!--内容-->
		<script type="text/javascript" src="example1.js"></script>
		<script type="text/javascript" src="example2.js"></script>
	</body>
</html>
```

​		这样，在解析页面包含的JavaScript代码之前，页面的内容将完全呈现在浏览器中。用户也会因为浏览器窗口显示空白页面的时间缩短而感到打开页面的速度加快了。

##### 延迟脚本

​		延迟脚本主要是使用`defer`属性，之前我们了解到这个属性的用途是表明脚本在执行时不会影响页面的构造。也就是说，脚本会被延迟到整个页面都解析完毕之后再运行。

```
<!DOCTYPE html>
<html>
	<head>
 		<title>Example HTML Page</title>
 		<script type="text/javascript" defer="defer" src= "example1.js"></script>
 		<script type="text/javascript" defer="defer" src= "example2.js"></script>
 	</head>
 	<body>
 		<!-- 这里放内容 -->
 	</body>
</html> 
```

​		在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在DOMContentLoad-ed 事件触发前执行，因此最好只包含一个延迟脚本。延迟脚本也应该放在页面底部。

##### 异步脚本

​		异步脚本使用的是`<script>`元素的`async`属性。这个属性与`defer`属性类似，都是用于该边处理脚本的行为。同样的与`defer`类似，`async`的脚本只适用于外部脚本文件，并告诉浏览器立即下载文件。但是与`defer`不同的是，标记为`async`的脚本并不保证按照指定它们的先后顺序执行。

```
<!DOCTYPE html>
<html>
 	<head>
 		<title>Example HTML Page</title>
 		<script type="text/javascript" async src="example1.js">				</script>
 		<script type="text/javascript" async src="example2.js">				</script>
 	</head>
	<body>
 		<!-- 这里放内容 -->
	</body>
</html> 
```

​		使用`async`属性的目的是不让页面等待两个脚本下载和执行，从而一步加载页面其他内容。异步脚本的执行一定会在load事件之前，但是可能会在DOMContentLoaded事件出发之前或者之后执行。



### 嵌入代码与外部文件

​		一般来说最好是尽可能使用外部文件来包含JavaScript代码。不过，并不存在必须使用外部文件的硬性规定。使用外部文件的好处有：

- 可维护性：遍及不同HTML页面的JavaScript会造成维护问题。但是把所有JavaScript文件都放在一个文件夹中，维护起来轻松许多。而且开发人员因此也能够在不触及HTML标记的情况下，集中精力遍及JavaScript代码。
- 可缓存：浏览器能够根据具体的设置缓存连接的所有外部JavaScript文件。也就是说，如果有两个页面都是用同一个文件，那么这个问价只用下载一次。因此，最终结果就是能够加快页面加载的速度。
- 适应未来：通过外部文件来包含JavaScript无需使用钱买你提到的XHTML或者注释hack。HTML和XHTML包含文件的语法是相同的。



### 文档模式

​		最初的两种文档模式是：**混杂模式**(quirks mode)和**标准模式**(standards mode)。混杂模式会让IE的行为与(包含非标准特性的)IE5相同，而标准模式则让IE的行为更加接近标准行为。虽然这两种模式主要影响的是CSS内容的呈现，但是在某些情况下也会影响到JavaScript的解释执行。

​		如果在文档开始出没有发现文档类型声明，则所有浏览器都会默认开启混杂模式。不同浏览器在混杂模式下的行为差异非常大，所以要在开头声明文档类型。

```
<!-- HTML 4.01 严格型 -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
"http://www.w3.org/TR/html4/strict.dtd">

<!-- XHTML 1.0 严格型 -->
<!DOCTYPE html PUBLIC
"-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"> 

<!-- HTML 5 -->
<!DOCTYPE html>
```

​		

### `<noscript>`元素

​		`<noscript>`元素是用以在不支持JavaScript的浏览器中显示代替的内容，但在启用了脚本的情况下，浏览器不会显示`<noscript>`元素中多的任何内容。在下列情况下，包含在`<noscript>`元素中的内容才会显示出来：

- 浏览器不支持脚本
- 浏览器支持脚本，但脚本被禁用

```
<html>
	<head>
 		<title>Example HTML Page</title>
 		<script type="text/javascript" defer="defer" src=" example1.js"></script>
 		<script type="text/javascript" defer="defer" src=" example2.js"></script>
 	</head>
 	<body>
 		<noscript>
 			<p>本页面需要浏览器支持（启用）JavaScript。
 		</noscript>
 	</body>
</html> 
```

 

