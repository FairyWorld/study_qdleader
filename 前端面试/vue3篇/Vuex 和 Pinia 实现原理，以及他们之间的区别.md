# Vuex 和 Pinia 实现原理，以及他们之间的区别

## Vuex 实现原理

Vuex 基于 Vue 的响应系统，利用单向数据流和事件驱动模型的理念，以一种集中和可预测的方式来管理和维护应用程序的状态。

Vuex 通过提供一个全局单例模式来管理状态，这意味着状态始终是单一来源的。它借鉴了 Redux 的实现方式，包括使用纯函数（mutations）来改变状态，使用 actions 来处理异步操作，并使用 getters 来计算派生状态。此外，Vuex 还利用了 Vue.js 的响应性系统，以便当状态改变时，相关的组件能够自动更新。

状态(state)：存放着应用的所有状态信息。它是单一数据源，确保了数据的唯一性和准确性。组件可以通过读取 State 来进行展示，但不能直接修改它。

Getter：Getter 为了提高代码的可复用性和可读性，Getters 担当起从 State 中派生数据的责任。这些派生状态是只读的，可以基于 State 计算得出，适用于复杂的逻辑处理或数据过滤。，例如过滤列表、计算属性等。

Mutations：Mutation 是更改状态的唯一方法，并且必须是同步事务。

Actions：Action 类似于 Mutation，不同在于 Action 提交的是 Mutation，而不是直接变更状态(通过 commit 调用来触发 Mutation 间接更新 State，从而保持应用状态的纯净性。)，Action 可以包含任意异步操作。

Modules：Vuex 提供了模块化的解决方案，允许我们将 store 分割成模块，每个模块拥有自己的 state、mutation、action、getter。

## Pinia 实现原理

Pinia 主要借鉴了 Vuex 的一些核心概念，但是简化了 API 并引入了一些新的概念和特性。

Pinia 的核心概念是"stores"，每个 store 都是一个独立的状态容器。这使得开发者可以更灵活地组织他们的状态，而不是像 Vuex 那样必须将所有状态放在一个大的单一对象中。

Pinia 也利用了 Vue.js 的响应性系统，但它更加依赖 Vue 3 的 Composition API，这使得状态管理代码更容易组织和理解。此外，Pinia 还包含一些其他有用的特性，如内置的开发工具支持和服务器端渲染（SSR）支持。

Stores：在 Pinia 中，不再有一个大的单一状态树，而是有多个小的独立的状态容器（也就是 Stores）。每个 Store 都有自己的状态(state)、动作(actions)和 getters。

Setup 方法：Pinia 引入了新的概念，如 setup 方法，这是基于 Vue3 的 Composition API 的。在这个 setup 方法中，我们可以定义 state、getters 和 actions。

## Vuex 和 Pinia 的主要区别

> 设计和使用。Vuex 采用全局单例模式，通过一个 store 对象来管理所有的状态，组件通过 store 对象来获取和修改状态。而 Pinia 则采用了分离模式，每个组件都拥有自己的 store 实例，通过在组件中创建 store 实例来管理状态。vuex 使用严格单一的 store 模式，而 pinia 允许使用多个 store 实例。

> 数据修改。pinia 比 vuex 更易用，因为它不需要编写复杂的 action、mutation 和 getter 函数。Pinia 没有 mutations，它只有 state getters action，这与 Vuex 不同，Vuex 有 State 同步 Gettes Mutations 模块化。Pinia 没有 modules 配置，每一个独立的仓库都是 defineStore 生成出来的。

> pinia 有更好的 TypeScript 支持,极其轻巧(体积约 1KB)

> 服务器端渲染支持：Pinia 对服务器端渲染（SSR）提供了内置支持。

> 性能：pinia 比 vuex 具有更好的性能，因为它使用了新的 ES6 语法和新的数据处理方式。

> 语法和使用。Pinia 语法上比 vuex 更容易理解和使用灵活，Pinia 提供了更好的 TypeScript 支持，vuex 是为 Vue 2.x 设计的，而 pinia 是为 Vue 3.x 设计的 Vue 版本支持。Vuex 当前最新版是 4.x，Vuex4 用于 Vue3，Vuex3 用于 Vue2，而 Pinia 当前最新版是 2.x，既支持 Vue2 也支持 Vue3。

> Pinia 是一个轻量级的状态管理库，专注于提供一个简单的 API 来管理应用程序的状态。Vuex 是一个更完整的状态管理库，提供了更多的功能，比如模块化、插件和严格模式等。
