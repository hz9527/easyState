## 序
当一个项目越来越复杂时，当组件间的耦合已经不能使用简单的父子组件通信，甚至类似VUE中Bus这类全局通信机制来解决，
那么我们可能会使用一些状态管理工具来完成  
或许你用过VUEX或者Redux或者Mobx这类库，我相信这些状态管理工具是十分优秀而强大的。  
尤其是Mobx这类弱侵入的状态管理库，你几乎可以在任何MVVM框架中使用Mobx，当状态发生变化只需要在合适的时机去驱动VM的更新就好了  
因此本项目更倾向于Mobx这类方式，不依赖MVVM框架的，单纯的Observable  

## 设计原则
1. 弱侵入性，不依赖框架也不需要为了在框架中使用而强行更改框架本身
2. 可以做到将Model完全从业务中抽离，独立管理Model，甚至可以分分钟将一个Vue项目变成React项目
3. 无需异步，不需要nextTick
4. 高性能

## 整体思路
1. 两部分，State与Watcher，也可以理解成Pub与Sub
2. 具有生命周期的设计，可以跟随组件被初始化与销毁
3. 所有对State的更改需要使用函数包装，类似VUEX中Mutation及Mobx中action的设计
4. 函数进栈初始化一个id，中途被订阅的函数都会放置进队列，出栈时如果id一致，表示一个周期完成，那么就可以调用队列中方法了
5. 同步计算

## API设计
### 生命周期
1. beforeCreate
2. created
3. beforeDestroy
4. desTroyed

### 暴露对外API
1. listen订阅一个或一组状态变化
2. unListen退订一个或一组状态变化
3. create实例化
4. destroy销毁

### options
1. state
2. computed
3. watch
4. action
5. 生命周期钩子
