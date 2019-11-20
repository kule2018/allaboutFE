try/catch/finally 语句用于处理代码中可能出现的错误信息。

错误可能是语法错误，通常是程序员造成的编码错误或错别字。也可能是拼写错误或语言中缺少的功能（可能由于浏览器差异）。

**try**语句允许我们定义在执行时进行错误测试的代码块。

**catch** 语句允许我们定义当 **try** 代码块发生错误时，所执行的代码块。

**finally** 语句在 try 和 catch 之后无论有无异常都会执行。

**注意：** catch 和 finally 语句都是可选的，但你在使用 try 语句时必须至少使用一个。

**提示：** 当错误发生时， JavaScript 会停止执行，并生成一个错误信息。使用 [throw](https://www.runoob.com/jsref/jsref-throw.html) 语句 来创建自定义消息(抛出异常)。如果你将 **throw** 和 **try** 、 **catch**一起使用，就可以控制程序输出的错误信息。

```javascript
try {
    tryCode - 尝试执行代码块
}
catch(err) {
    catchCode - 捕获错误的代码块
}
finally {
    finallyCode - 无论 try / catch 结果如何都会执行的代码块
}
```



