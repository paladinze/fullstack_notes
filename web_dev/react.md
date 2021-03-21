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
- 根据DOM结构生成的内存表示

## React 中 key 的作用
- key 作为元素的唯一标识用来表示元素的唯一性
- 帮助跟踪virtualDom中哪些元素被改变
- 在渲染列表数据时位置item的状态

## 当组件的 setState 函数被调用之后，发生了什么？
- 把传递给 setState 的参数对象合并到组件原先的 state
- reconcile and render

## react 中 refs 的作用
- 访问DOM元素实例的handle

## 什么时候用 Class component，什么时候用 Functional component？
- 基本所有情况用 Functional component

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

## composition over inheritance
- use composition to reuse code between components
- containment
  - use props.children to render component contained inside another component
- specialization
  - think a more specific component as a special case of a generic component
  - the more sepecific component render generic component and configures it with props
- none-UI logic code reuse
  - use js module
  - component import things from module, but doesn't extend it

## 受控组件(Controlled Component)与非受控组件(Uncontrolled Component)的区别
- 受控组件由 react 侦测改变和管理 value
- 非受控组件由 dom 自己管理 value

## 并不是父子关系的组件，如何实现相互的数据通信？
- redux

## React 中 setState 什么时候是同步的，什么时候是异步的？
- 在 合成事件 和 生命周期钩子(除 componentDidUpdate) 中，setState 是"异步"的
- 在 原生事件 和 setTimeout 中，setState 是同步的，可以马上获取更新后的值

## React + Redux (MVVM)
- Model (M): Redux
  - global state management
- View (V): JSX + CSS
  - how things look
- View-Model (VM): Component
  - manages simple state, passes data directly onto View

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

## react hook
- a way to reuse stateful logic, not state
- each hook call has completely isolated state
- pros
  - seperate concerns: allows organizing effects around features, not life cycles
  - only call Hooks from React function components
- should not be used inside loops, conditions, or nested functions
  - when multiple State or Effect Hooks in a single component, React relies on the order in which Hooks are called
  - ensures hooks are called in the same order across re-render
  - necessary for react to preserve state of hooks
- only call hooks from functional components or custom hooks
  - ensure all stateful logic in a component is clearly visible

## react hook vs class
- redunce cost of class instantiation and event binding
- reduce component nesting (of HOC, context, render props)
  - simpler tree -> better performance


## `useState` hook
- give state to functional component
- preserve values between function calls
- syntax
  - intput: initial state
  - output: 
      - state
      - setState method

## `useEffect` hook
- use case
  - scheule side effects: mutations, timers, logging
- timing
  - fire after every render
- run only on dependency change
  - use 2nd argument to sepecify the dependency list
  - use empty array, if only only want run once, and cleanup during unmount
- cleanup function
  - the function returned in the hook will be used for cleanup
  - runs before component unmount
  - runs before effect is fired again
- replaces: componentDidMount + componentDidUpdate
  ```js
  useEffect(() => {
      console.log('after every rerender!');
  })
  ```
- replace: componentDidMount
  ```js
  useEffect(() => {
      console.log('mounted!');
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
      return () => console.log('unmounting');
  }, [])
  ```

## `useLayoutEffect` hook
- use case
  - read DOM layout
  - rerender synchronously
- timing
  - fire before paint
  - updates flushed synchronously

## `useMemo` hook
- use case
  - performance optimization through memoization
- timing
  - fire during render
- syntax
  ```js
  const memoizedValue = useMemo(() => doComplicatedStuff(a, b), [a, b]);
  ```

## `useCallback` hook
- make function declarations stable inside component

## `useRef` hook
- a container to persist values across component's lifecycle
- use case
  - directly access Dom element
  - persist any object across rerender
- syntax
  ```js
  const refContainer = useRef(initialValue);
  const value = refContainer.current;
  ```

## `useDebugValue` hook
- dsiplay a label for the custom hook in devtool
  ```js
  function useFriendStatus(friendID) {
    const [isOnline, setIsOnline] = useState(null);

    useDebugValue(isOnline ? 'Online' : 'Offline');
    return isOnline;
  }
  ```

## Context 
- a way to pass data to any part of the subtree
- three parts of a context
  - creation: create the context
    - need to specify a default value: used when no provider in found in the lookup
  - provider: wrap top of the tree with context's provider
  - consumer: consume the context in child components
    - `useContext(theContext)`: read & subscribe to changes
    - `Context.Consumer`: consume multiple contexts
    - `Class.contextType`: consume a single context (used in class only)
- rerender mechanism
  - rerender whenever Provider's value changes
  - ignore `shouldComponentUpdate` logic
  - `Object.is` comparison (compare by refence)

## update state from deep nested child
pass `dispatch` (from `useReducer`) down using `context`
- `context` allows passing data to deeply nested child
- `dispatch` is stable across rerender (no need to use `useCallback`)

```js

// parent
const TodosDispatch = React.createContext(null);
function TodosApp() {
  const [todos, dispatch] = useReducer(todosReducer);
  return (
    <TodosDispatch.Provider value={dispatch}>
      <DeepTree todos={todos} />
    </TodosDispatch.Provider>
  );
}

// deep in the tree
function DeepChild(props) {
  const dispatch = useContext(TodosDispatch);
  function handleClick() {
    dispatch({ type: 'add', text: 'hello' });
  }

  return (
    <button onClick={handleClick}>Add todo</button>
  );
}
```

## `React.useMemo`
- avoid component rerendering if prop doesn't change
- similar to `shouldComponentUpdate`
  - compare props only
- syntax
  ```js
  const Button = React.memo((props) => {});
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

## pattern: HoC（Higher-Order Component）
- 输入一个元组件，返回出一个新的增强组件
- 高阶组件的主要作用是组件逻辑复用
  - 以同样的逻辑操作输入组件的状态和参数
- use case
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

## client-side rendering vs server-side rendering
- client-side rendering
  - example framework: create-react-app (CRA)
  - pros
    - rich interaction
    - faster response after load
  - cons
    - bad for seo
    - slow initial load
- server-side rendering
  - example framework: NextJs
  - pros
    - seo
    - initial page load
    - static sites
  - cons
    - full page reload
    - slower page rendering

## CRA customization
- eslint
  https://create-react-app.dev/docs/setting-up-your-editor/
- webstorm integration
  https://www.jetbrains.com/help/webstorm/react.html
- react-app-rewired
  https://github.com/timarney/react-app-rewired
- customize-cra
  https://github.com/arackaf/customize-cra