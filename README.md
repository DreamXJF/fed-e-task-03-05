# fed-e-task-03-05
Vue作业5
简答题
1、Vue 3.0 性能提升主要是通过哪几方面体现的？
答：1.大幅提升运行时的性能：重写虚拟dom，效果提升30%~300%；
	2.提升网络性能：tree-shaking机制;
	3.完全typescript支持;
	4.Fragment：模板更简单;Teleport：布局更加灵活;Suspense：强大的异步组件;composition-api：逻辑重用



2、Vue 3.0 所采用的 Composition Api 与 Vue 2.x使用的Options Api 有什么区别？
答：在vue2中如何组织代码的，我们会在一个vue文件中methods，computed，watch，data中等等定义属性和方法，共同处理页面逻辑，
我们称这种方式为Options API，缺点： 一个功能往往需要在不同的vue配置项中定义属性和方法，比较分散，项目小还好，清晰明了，
但是项目大了后，一个methods中可能包含20多个方法，你往往分不清哪个方法对应着哪个功能。
vue3中的Composition API就是用来解决这个问题的，在vue3 Composition API 中，我们的代码是根据逻辑功能来组织的，
一个功能所定义的所有api会放在一起（更加的高内聚，低耦合），这样做，即时项目很大，功能很多，我们都能快速的定位到这个功能所用到的所有API，
而不像vue2 Options API 中一个功能所用到的API都是分散的，需要改动功能，到处找API的过程是很费劲的。
Composition API 是根据逻辑相关性组织代码的，提高可读性和可维护性。
基于函数组合的 API 更好的重用逻辑代码（在vue2 Options API中通过Mixins重用逻辑代码，容易发生命名冲突且关系不清）


3、Proxy 相对于 Object.defineProperty 有哪些优点？
答：1.Object.defineProperty无法监控到数组下标的变化，导致直接通过数组的下标给数组设置值，不能实时响应。 
Object.defineProperty只能劫持对象的属性,因此我们需要对每个对象的每个属性进行遍历。
Vue 2.x里，是通过 递归 + 遍历 data 对象来实现对数据的监控的，如果属性值也是对象那么需要深度遍历,
显然如果能劫持一个完整的对象是才是更好的选择。
	2.可以劫持整个对象，并返回一个新对象，有13种劫持操作
	3.Proxy是es6提供的新特性，兼容性不好，最主要的是这个属性无法用polyfill来兼容；

4、Vue 3.0 在编译方面有哪些优化？
答：直接把静态节点抽离出去了，他只会编译阶段创建一遍，之后直接复用对象，不需要再创建了。
还有一些其他的优化，比如说可以 cache 绑定的 click 函数，SSR 渲染直接变字符串输出。


5、Vue.js 3.0 响应式系统的实现原理？
答：通过 effect  声明依赖响应式数据的函数cb ( 例如视图渲染函数render函数)，并执行cb函数，执行过程中，会触发响应式数据 getter
在响应式数据 getter中进行 track依赖收集：建立 数据&cb 的映射关系存储于 targetMap
当变更响应式数据时，触发 trigger **，**根据 targetMap 找到关联的cb执行
映射关系 targetMap 结构
