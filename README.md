# dynamic-tab
在动态组件上使用 keep-alive
我们之前曾经在一个多标签的界面中使用 is attribute 来切换不同的组件：

<component v-bind:is="currentTabComponent"></component>
当在这些组件之间切换的时候，你有时会想保持这些组件的状态，以避免反复重渲染导致的性能问题。例如我们来展开说一说这个多标签界面：

你会注意到，如果你选择了一篇文章，切换到 Archive 标签，然后再切换回 Posts，是不会继续展示你之前选择的文章的。这是因为你每次切换新标签的时候，Vue 都创建了一个新的 currentTabComponent 实例。

重新创建动态组件的行为通常是非常有用的，但是在这个案例中，我们更希望那些标签的组件实例能够被在它们第一次被创建的时候缓存下来。为了解决这个问题，我们可以用一个 <keep-alive> 元素将其动态组件包裹起来。

<!-- 失活的组件将会被缓存！-->
<keep-alive>
  <component v-bind:is="currentTabComponent"></component>
</keep-alive>

现在这个 Posts 标签保持了它的状态 (被选中的文章) 甚至当它未被渲染时也是如此。你可以在这个示例查阅到完整的代码。

注意这个 <keep-alive> 要求被切换到的组件都有自己的名字，不论是通过组件的 name 选项还是局部/全局注册。
