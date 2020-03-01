# React

## React 核心流程
- reconciliation: find what has changed
  - 更新 state 与 props；
  - 调用生命周期钩子；
  - 生成 virtual dom (aka fiber Tree)
  - diff virtual dom 
  - 确定是否需要重新渲染
- rendering: 操作 dom 节点更新

## 什么是 Virtual DOM？
- 根据 DOM 的树状结构生成的JS表达

## React 中 key 的作用
- key 作为元素的唯一标识用来表示元素的唯一性
- 帮助跟踪 virtualDom 中哪些元素被改变

## 当组件的 setState 函数被调用之后，发生了什么？
- 把传递给 setState 的参数对象合并到组件原先的 state
- reconcile and render

## react 中 refs 的作用
- 访问 DOM 元素实例的handle (本质是一个函数）

## 什么时候用 Class component，什么时候用 Functional component？
- Class component：用到了 state，生命周期函数
- Functional component：其它情况

## React 生命周期
```js
// mounting
constructor()
render()
componentDidMount()

// updating
render() // triggered when: props change, setState(), forceUpdate()
componentDidUpdate()

// unmount
componentWillUnmount()
```

## 受控组件(Controlled Component)与非受控组件(Uncontrolled Component)的区别
- 受控组件由 react 侦测改变和管理 value
- 非受控组件由 dom 自己管理 value

## 并不是父子关系的组件，如何实现相互的数据通信？
- redux

## React 中 setState 什么时候是同步的，什么时候是异步的？
- 在 合成事件 和 生命周期钩子(除 componentDidUpdate) 中，setState 是"异步"的
- 在 原生事件 和 setTimeout 中，setState 是同步的，可以马上获取更新后的值

## Redux 使用流程
- redux 是 react 应用的状态管理机制
- 为了解决多页面多组件之间的数据通信
- 单一数据源: 所有 state 最终维护在一个根级 Store
- 状态只读: 数据无法被直接修改
- 主要有 Store、Action、Reducer 三部分组成
  - component 发起 action 操作修改 store 中 的 state
  - reducers 根据 action 和当前的 state 获得新的 state
  - redux 使用 getState 方法通知页面更新视图
- Redux Data loading cycle
  - component rendered
  - componentDidMount called
  - call actionCreator from componentDidMount
  - call api in actionCreator
  - api responds with data
  - action creater returns actions with data in payload of action
  - some reducer parse and return the data
  - react-redux rerender the app
- Rules of redux reducers
  - must not return undefined
  - must produce state based only on preState and action
  - must not reach out itself to get data
  - must not mutate input

## redux 缺点
- verbose
- code locality

## React + Redux (MVVM)
- Model (M): Redux
  - global state management
- View (V): JSX + CSS
  - how things look
- View-Model (VM): Component
  - manages simple state, passes data directly onto View

## react hook
- a way to reuse stateful logic, not state
- each hook call has completely isolated state
- hook state is maintained between re-renders
- pros
  - seperate concerns: allows organizing effects around features, not life cycles
  - only call Hooks from React function components
- should not be used inside loops, conditions, or nested functions
  - when multiple State or Effect Hooks in a single component, React relies on the order in which Hooks are called
  - ensures hooks are called in the same order across re-render
  - necessary for react to preserve state of hooks
- only call hooks from functional components or custom hooks
  - ensure all stateful logic in a component is clearly visible

## useState hook
- give state to functional component
- preserve values between function calls
- syntax
  - intput: initial state
  - output: 
      - state
      - setState method

## useEffect hook
- runs the effects after every render by default
- have access to its props and state
- syntax
  - function
  - optional 2nd argument (array of values)
    - tells react skipp applying an effect is all values of concern hasn't changed
- cleanup
  - returns a function
  - cleanup function run everytime effects is triggered again
- replace: case in which componentDidMount + componentDidUpdate needs same behavior
  ```js
  useEffect(() => {
      console.log('I just mounted!');
  })
  ```
- replace: componentDidMount
  ```js
  useEffect(() => {
      console.log('I just mounted!');
  }, [])
  ```
- replace: componentDidUpdate
  ```js
  useEffect(() => {
      console.log('count changed', props.count);
  }, [props.count])
  ```
- replace: componentWillUnmount
  ```js
  useEffect(() => {
      return () => console.log('I am unmounting');
  }, [])
  ```

## Custom hooks
- name starts with "use"
- may call other hooks
- not a feature, just follows the rules of hooks

```js
import React, { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

## pattern: HoC（Higher-Order Component）？
- 高阶组件不是组件，是 增强函数
- 输入一个元组件，返回出一个新的增强组件
- 高阶组件的主要作用是 代码复用，操作 状态和参数
- 属性代理 (Props Proxy): 给元组件添加 props

```js
function withOnChange(Comp) {
  return class extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        name: ""
      };
    }
    onChangeName = () => {
      this.setState({
        name: "dongdong"
      });
    };
    render() {
      const newProps = {
        value: this.state.name,
        onChange: this.onChangeName
      };
      return <Comp {...this.props} {...newProps} />;
    }
  };
}
```

```js
const NameInput = props => <input name="name" {...props} />;
export default withOnChange(NameInput);
```

- 渲染劫持: 通过抽象逻辑，统一对页面进行权限判断，按不同的条件进行页面渲染

```js
function withAdminAuth(WrappedComponent) {
  return class extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        isAdmin: false
      };
    }
    async componentWillMount() {
      const currentRole = await getCurrentUserRole();
      this.setState({
        isAdmin: currentRole === "Admin"
      });
    }
    render() {
      if (this.state.isAdmin) {
        return <Comp {...this.props} />;
      } else {
        return <div>您没有权限查看该页面，请联系管理员！</div>;
      }
    }
  };
}
```

## pattern: render props
```js
<DataProvider render={data => (
  <h1>Hello {data.target}</h1>
)}/>
```

# CRA customization
- eslint
  https://create-react-app.dev/docs/setting-up-your-editor/
- webstorm integration
  https://www.jetbrains.com/help/webstorm/react.html
- react-app-rewired
  https://github.com/timarney/react-app-rewired
- customize-cra
  https://github.com/arackaf/customize-cra

  ## client-side rendering vs server-side rendering
  - client-side rendering
    - pros
      - rich interaction
      - faster response after load
    - cons
      - bad for seo
      - slow initial load
  - server-side rendering
    - pros
      - seo
      - initial page load
      - static sites
    - cons
      - full page reload
      - slower page rendering
