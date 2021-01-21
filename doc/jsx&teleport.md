# JSX
## JSX 是什么
JSX 是一种 Javascript 的语法扩展，JSX = Javascript + XML，即在 Javascript 里面写 XML，因为 JSX 的这个特性，所以他即具备了 Javascript 的灵活性，同时又兼具 html 的语义化和直观性
## 为什么要在 Vue 中使用 JSX
有时候，我们使用渲染函数（render function）来抽象组件，渲染函数不是很清楚的参见官方文档, 而渲染函数有时候写起来是非常痛苦的,看一下 vue3 的 jsx 官方文档部分：

```html
<anchored-heading :level="1"> <span>Hello</span> world! </anchored-heading>
```
对应的渲染函数：
```javascript
Vue.h(
  'anchored-heading',
  {
    level: 1
  },
  [Vue.h('span', 'Hello'), ' world!']
)
```
jsx
```javascript
import AnchoredHeading from './AnchoredHeading.vue'

new Vue({
  el: '#demo',
  render() {
    return (
      <AnchoredHeading level={1}>
        <span>Hello</span> world!
      </AnchoredHeading>
    )
  }
})
```
看个复杂的例子，
模板复杂的话，这个渲染函数书写是非常痛苦的，并且没法直观看出结构，容易成为“祖传代码”，既然渲染函数这么吃力不讨好的话，就派上 JSX 上场了,它可以让我们回到更接近于模板的语法上。
## vue3中使用jsx
实际上 vue-cli 建立的 vue3 项目中已经内置了 jsx 的这个编译插件，如果你不需要自定义配置，是不需要安装就可以即开即用 jsx 的，vue官网的例子可以说非常简陋了，但是但是他给我们指引了 vue3 中 jsx 的 babel 转换插件 [jsx-next](https://github.com/vuejs/jsx-next/tree/dev/packages/babel-plugin-jsx "jsx-next")。
下面通过一个小demo看下比较常用的一些语法：

# teleport
## teleport的作用
Vue3新增了一个内置组件： Teleport 。这个组件的作用主要用来将模板内的 DOM 元素移动到其他位置。

Vue 鼓励我们通过将 UI 和相关行为封装到组件中来构建 UI。我们可以将它们嵌套在另一个内部，以构建一个组成应用程序 UI 的树。

然而，有时组件模板的一部分逻辑上属于该组件，而从技术角度来看，最好将模板的这一部分移动到 DOM 中 Vue app 之外的其他位置。

一个常见的场景是创建一个包含全屏模式的组件。在大多数情况下，你希望模态的逻辑存在于组件中，但是模态的定位很快就很难通过 CSS 来解决，或者需要更改组件组合。

Teleport 提供了一种干净的方法，允许我们控制在 DOM 中哪个父节点下呈现 HTML，而不必求助于全局状态或将其拆分为两个组件。
## teleport的特点
* 该组件需要一个目标元素，该元素是通过需要一个HTMLElement或querySelector字符串的prop提供的。
* 组件将其子代移动到DOM选择器标识的元素
* 在虚拟DOM级别，子级仍然是子代的后代`<teleport>`，因此他们可以从其祖先那里获得注入

