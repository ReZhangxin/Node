# 模块

> 在`Node.js`中，以模块为单位划分所有功能，并且提供了一个完整的模块加载机制。

## 1、模块的`require()`以及`exports()`

**1）、Node.js中，一个`JavaScript`文件中定义的变量、函数，都只在这个文件内部有效。**

- **如果别人想用这个变量，那么就要用`exports`进行暴露。**

- **使用者要用`require()`命令引用**

**2）、Node.js中，一个`JavaScript`文件，可以向外`exports`无数个变量、函数。但是`require`的时候，仅仅需要`require`这个`JS`文件一次。**

```js
var msg ="hello";
function showMsg(){
    console.log(msg);
}
exports.msg = msg;
exports.showMsg = showMsg;
```

在使用者中，只需要require一次。

```js
var foo = require("./foo.js");
console.log(foo.msg);
foo.showInfo();
```

## 2、`js`与`js`之间有两种合作模式

- 第一种：暴露变量、函数。`exports.msg=msg`

```js
//在foo.js中
var msg = "hello";
exports.msg = msg;

//在bar.js中
var foo = require("./foo.js");
console.log(foo.msg);
//node bar.js   输出：hello
```

- 第二种：暴露一个类。`module.exports = People`

```js
//foo.js文件内容
function People(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
}
People.prototype={
    sayHello:function(){
        console.log( `
            你好${this.name}，
            我今年${this.age}岁，
            性别${this.sex}
        `);
    },
    sayBye:function(){
        console.log(`bye-bye：${this.name}`)
    }
}
module.exports = People;

//bar.js文件内容
var People = require('./foo.js');
var xin = new People('张鑫',22,'男');
xin.sayHello();
xin.sayBye();
```

## 3、`require()`里面路的径三种写法

### 1）`require('./foo.js')`

> 表示引入当前目录下的`foo.js`

### 2）`require('foo.js')`

> 表示引入`node_module`文件夹下的`foo.js`

### 3）`require('foo')`

> 表示引入`node_module`文件夹下的`foo`文件夹

在`foo`文件夹下要有`package.json`文件设置入口文件
`main`就是

```js
{
  "name": "fooDemo",
  "version": "1.0.1",
  "main" : "app.js"
}
```
