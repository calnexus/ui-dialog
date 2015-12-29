#乐课ui-tree的插件的使用

## 原理：
`ui-dualog` 开发对外的接口只有五个方法，分别为`create`，`open`，`close`，`alert`，`confirm`
`open`方法为`alert`和`confirm`，`create`提供创建对话框的方法，具体根据传进的参数不同而创建不同的对话框

###create方法
`create`创建弹出框，不限于创建`alert`框和`confirm`框，可以根据需要创建不同内容，具体参数查看参数的解释

###alert方法
仿写系统的`alert`弹窗框

###confirm方法
仿写系统提供的`confirm`确认框

###close方法
当参数为指定id时，关闭指定id的弹出窗，否则关闭当前的弹出框。


##Params
option 参数值一下是参数的默认值，及可以更改的值。

```javascript
	var options={
		title: '', // 对话框标题
		id: null, // 对话框ID，删除时可指定该ID进行删除
		size: 'nm', // 对话框尺寸，尺寸大小见上方DIALOG_SIZES
		zIndex: 1010, // zindex
		bgClose: false, // 是否点击背景关闭对话框
		url: null, // 如果是 iframe ，传入 iframe 的 URL
		scrolling: "auto", // 如果是 iframe 可以传入是否需要滚动条
		tpl: '', // 如果是页面内 DIV，传入内容模板或 jQuery 对象
		keepTpl: false, // 是否保存模板，默认关闭时会将 tpl 从 body 中移除，若传入的是 jQuery 对象，可以将 keepTpl 设置为 true
		btns: [], // 按钮列表
		onClose: null, // 对话框关闭回调
		_closed: null // 内部关闭 hook，用于将对话框从 top._dialogs 中移除
	};
```

####对上述参数进行解释说明
`url` 弹窗的内容是页面，引用页面的地址，作为iframe嵌入到页面中，若url为有效的地址，tpl重新赋值也不起作用。

`size`的取值只有四种：'mini' 、'sm' 、'nm'、'lg' 默认为'nm'

`bgClose` 设置为true时，弹出框的背景点击时也会关闭弹窗框

`tpl` 为嵌入在弹窗中主体的内容，可以为html结构，或者模板对象

`keepTpl` 为true，且弹出框的内容是模板生成的时候，生成弹窗的时候将模板从body中移除。

`btns` 为按钮的列表，`btns`按钮的格式如下，cb为点击按钮时的回调函数，不需要则不需要复写：

```javascript
[
	{className: 'btn-base btn-green',text: '保存',cb: function() {}},
	{className: 'btn-base btn-green',text: '取消',cb: function() {}}
]
```

`onClose` 为关闭按钮时的回调函数，不需要可不复写

`_closed` 将弹出框直接从弹出框的数组中移除，从而达到关闭函数的效果

###调用方法
####弹出框

```javascript
var dialog=Dialog.create(option);
```

####alert框
```javascript
var dialog=Dialog.alert(option);
```

####confirm
```javascript
var dialog=Dialog.confirm(option);
```