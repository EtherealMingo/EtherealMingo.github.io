## Mustache

Mustache是一个logic-less（轻逻辑）模板解析引擎，

它是为了使用户界面与业务数据（内容）分离而产生的，

它可以生成特定格式的文档，通常是标准的HTML文档。

比如小程序的wxml中的代码

```text
{{userInfo.nickName}}，这里的{{ }}就是Mustache的语法。
```

**Mustache的模板语法很简单，就那么几个：**

1. {{keyName}}
2. {{{keyName}}}
3. {{#keyName}} {{/keyName}}
4. {{^keyName}} {{/keyName}}
5. {{.}}
6. {{!comments}}
7. {{>partials}}

1、{{keyName}}简单的变量替换。

2、{{#keyName}} {{/keyName}}以#开始、以/结束表示区块，它会根据当前上下文中的键值来对区块进行一次或多次渲染。它的功能很强大，有类似if、foreach的功能。

3、{{^keyName}} {{/keyName}}该语法与{{#keyName}} {{/keyName}}类似，不同在于它是当keyName值为null, undefined, false时才渲染输出该区块内容。

4、{{.}} {{.}}表示枚举，可以循环输出整个数组

5、{{! }}表示注释

6、{{>partials}}以>开始表示子模块，当结构比较复杂时，我们可以使用该语法将复杂的结构拆分成几个小的子模块。