# JSX
## JSX 是什么
JSX 是一种 Javascript 的语法扩展，JSX = Javascript + XML，即在 Javascript 里面写 XML，因为 JSX 的这个特性，所以他即具备了 Javascript 的灵活性，同时又兼具 html 的语义化和直观性
## 为什么要在 Vue 中使用 JSX
有时候，我们使用渲染函数（render function）来抽象组件，渲染函数不是很清楚的参见官方文档, 而渲染函数有时候写起来是非常痛苦的,看一下 vue3 的 jsx 官方文档部分：

特别是对应的模板如此简单的情况下：
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
可以看出来比较繁琐，特别是里面的嵌套，这还只是一层嵌套，可以想象到如果模板复杂的话，这个渲染函数将没法直观看出结构;这显然是吃力不讨好的，这个时候就派上 JSX 上场了,它可以让我们回到更接近于模板的语法上。
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

## vue3中使用jsx
实际上 vue-cli 建立的 vue3 项目中已经内置了 jsx 的这个编译插件，如果你不需要自定义配置，是不需要安装就可以即开即用 jsx 的，vue官网的例子可以说非常简陋了，但是但是他给我们指引了 vue3 中 jsx 的 babel 转换插件 [jsx-next](https://github.com/vuejs/jsx-next/tree/dev/packages/babel-plugin-jsx "jsx-next")。
下面通过一个小demo看下比较常用的一些语法：

# teleport
