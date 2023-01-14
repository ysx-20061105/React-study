# React-study

## 简介

用于动态构建用户界面的JavaScript库

由FaceBook开源

**特点**

1. 声明式编码
2. 组件化编码
3. React Native编写原生应用
4. 高效（优秀的Diffing算法）
   1. 使用虚拟(virtual)DOM, 不总是直接操作页面真实DOM。
   2. DOM Diffing算法, 最小化页面重绘。

**相关的js库**

react.js:React核心库

react-dom.js:提供操作DOM的react扩展库

babel.min.js:解析JSX语法代码转为JS代码的库

## JSX

### JSX语法

1. 全称: JavaScript XML

2. react定义的一种类似于XML的JS扩展语法: JS + XML本质是React.createElement(component,props, ...children)方法的语法糖

3.  作用: 用来简化创建虚拟DOM 

   1. 写法：

      ```jsx
      var ele = <h1>Hello JSX!</h1>
      ```

   2. 注意1：它不是字符串, 也不是HTML/XML标签

   3. 注意2：它最终产生的就是一个JS对象

4. 标签名任意: HTML标签或其它标签

5.  标签属性任意: HTML标签属性或其它

6. 基本语法规则

   1. 遇到 <开头的代码, 以标签的语法解析: html同名标签转换为html同名元素, 其它标签需要特别解析
   2.  遇到以 { 开头的代码，以JS语法解析: 标签中的js表达式必须用{ }包含

7. babel.js的作用
   1. 浏览器不能直接解析JSX代码, 需要babel转译为纯JS的代码才能运行
   2. 只要用了JSX，都要加上type="text/babel", 声明需要babel来处理

### 渲染虚拟DOM

1. 语法: 

   ```js
   ReactDOM.render(virtualDOM, containerDOM)
   ```

2. 作用: 将虚拟DOM元素渲染到页面中的真实容器DOM中显示

3. 参数说明
   1. 参数一: 纯js或jsx创建的虚拟dom对象
   2. 参数二: 用来包含虚拟DOM元素的真实dom元素对象(一般是一个div)

练习：

[demo1](./JSX/jsx01.html)

[demo2](./JSX/jsx02.html)

## 模块与组件、模块化与组件化

### 模块

1. 理解：向外提供特定功能的js程序, 一般就是一个js文件
2.  为什么要拆成模块：随着业务逻辑增加，代码越来越多且复杂。
3. 作用：复用js, 简化js的编写, 提高js运行效率

### 组件

1. 理解：用来实现局部功能效果的代码和资源的集合(html/css/js/image等等)

2. 为什么要用组件： 一个界面的功能更复杂

3. 作用：复用编码, 简化项目编码, 提高运行效率

### 模块化

当应用的js都以模块来编写的, 这个应用就是一个模块化的应用

### 组件化

当应用是以多组件的方式实现, 这个应用就是一个组件化的应用

## 面向组件编程

**函数式组件**：组件由函数定义的组件 [函数式组件](./面向组件编程/函数式组件.html)

**类式组件**：组件由类定义 [类式组件](./面向组件编程/类式组件.html)

### 注意

1. 组件名必须首字母大写

2. 虚拟DOM元素只能有一个根元素

3. 虚拟DOM元素必须有结束标签

### 渲染组件标签的基本流程

1. React内部会创建组件实例对象

2. 调用render()得到虚拟DOM, 并解析为真实DOM
3. 插入到指定的页面元素内部

### state

state是组件对象最重要的属性, 值是对象(可以包含多个key-value的组合)

组件被称为"状态机", 通过更新组件的state来更新对应的页面显示(重新渲染组件)

状态数据，不能直接修改或更新 ，需要使用原型链上的setState方法

练习：

使用构造函数：[state](./面向组件编程/1.state/1.state.html)

不使用构造函数：[state](./面向组件编程/1.state/2.state.html)

### props

每个组件对象都会有props(properties的简写)属性

组件标签的所有属性都保存在props中

**作用**：

通过标签属性从组件外向组件内传递变化的数据

注意: 组件内部不要修改props数据

**操作**：

内部读取某个属性值

```js
this.props.name
```

对props中的属性值进行类型限制和必要性限制

```js
Person.propTypes={
    name:PropType.string.isRequired,
    age:PropType.number
}
```

默认属性值

```js
Person.defaultProps={
    age:18,
    sex:'男'
}
```

扩展属性: 将对象的所有属性通过props传递

```jsx
<Person {...person}/>            
```

组件类的构造函数

```js
constructoe(props){
    super(props)
    console.log(props)
}
```

练习：

[使用props](./面向组件编程/2.props/1.props.html)

[对props进行限制](./面向组件编程/2.props/2.props.html)

[对props限制简化写法](./面向组件编程/2.props/3.props.html)

### refs

组件内的标签可以定义ref属性来标识自己

练习：

[字符串ref](./面向组件编程/3.refs/1.refs.html)

[回调形式ref](./面向组件编程/3.refs/2.refs.html)

[React.createRef](./面向组件编程/3.refs/2.refs.html)

## 组件的生命周期

 组件从创建到死亡它会经历一些特定的阶段。

 React组件中包含一系列勾子函数(生命周期回调函数), 会在特定的时刻调用。

 我们在定义组件时，会在特定的生命周期回调函数中，做特定的工作。

### 生命周期(旧)

![react生命周期(旧)](./react生命周期(旧).png)

生命周期的三个阶段（旧）

1. **初始化阶段:** 由ReactDOM.render()触发---初次渲染
      1. constructor()
      2. componentWillMount()
      3. render()
      4. componentDidMount()
2. **更新阶段:** 由组件内部this.setSate()或父组件重新render触发
   1. shouldComponentUpdate()
      2. componentWillUpdate()
      3. render()
   4. componentDidUpdate()
3. **卸载组件:** 由ReactDOM.unmountComponentAtNode()触发
      1. componentWillUnmount()

### 声明周期(新)

![react生命周期(新)](./react生命周期(新).png)

生命周期的三个阶段（新）

1. **初始化阶段:** 由ReactDOM.render()触发---初次渲染
   1.  constructor()
   2. **getDerivedStateFromProps** 
   3. render()
   4. componentDidMount()
2. **更新阶段:** 由组件内部this.setSate()或父组件重新render触发
   1. **getDerivedStateFromProps**
   2. shouldComponentUpdate()
   3. render()
   4. **getSnapshotBeforeUpdate**
   5. componentDidUpdate()

3. **卸载组件:** 由ReactDOM.unmountComponentAtNode()触发
   1. componentWillUnmount()

### 重要的钩子

render：初始化渲染或更新渲染调用

componentDidMount：开启监听, 发送ajax请求

componentWillUnmount：做一些收尾工作, 如: 清理定时器

练习：

[生命周期](./面向组件编程/4.组件生命周期/1.生命周期.html)

**生命周期(旧)**

[生命周期(旧)](./面向组件编程/4.组件生命周期/2.生命周期(旧).html)

[生命周期(新)](./面向组件编程/4.组件生命周期/3.生命周期(父子组件).html)