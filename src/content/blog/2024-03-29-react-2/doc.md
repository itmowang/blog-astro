---
title: "(使用一年React后的回顾) React 常用 Hooks"
description: "React 常用Hooks"
pubDate: "2024-04-01  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-03-29-react-2/01.png"
tags:
    - react
    - React 常用hook
    - 前端进阶
---

# useState

**useState** 是一个 React 的 hook ，它的作用是让你向组件添加一个状态变量。

```jsx
const [state, setState] = useState(initialState);
```

useState 有两个参数

1. useState 返回的第一个参数，为我们需要展示或者使用的最新的值
2. useState 的第二个参数，这个函数是一个 set 函数，可以传入任意变量，让其 state 返回新的值。

```jsx
function App() {
    const [num, setNum] = useState(1);
    return (
        <div className="App">
            <button onClick={() => setNum(num + 1)}>{num}</button>
        </div>
    );
}
```

# useEffect

useEffect ，是副作用，副作用是指在组件在渲染期间发生的操作，如数据获取，订阅事件，手动操作 dom 等，在函数组件中，由于没有生命周期方法，我们无法再特定的时间执行这些操作，useEffect 正好解决了这个问题

```jsx
async function getData() {
    return await new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(666);
        }, 3000);
    });
}

function App() {
    const [num, setNum] = useState(1);

    useEffect(() => {
        getData().then((data: any) => {
            setNum(data);
        });
    }, []);

    return (
        <div className="App">
            <button onClick={() => setNum((prevNum) => prevNum + 1)}>
                {num}
            </button>
        </div>
    );
}
```

# useLayoutEffect

在 react 中 useLayoutEffect 和 useEffect 是差不都的，在绝大多数情况下，但是事实上是有一定的区别

useEffect 会在渲染内容更新到 dom 上后执行，不会阻塞 dom 的更新
useLayoutEffect 会在渲染更新到 dom 之前就执行，会阻塞 dom 的更新

# useReducer

用 useState 是直接修改值，如果想在修改值之前，执行一些操作，可以使用 useReducer

```jsx
function App() {

  interface Data {
    result: number,
  }

  interface Action {
    type: 'add' | 'minus',
    num: number
  }

  function reducer(state: Data, action: Action) {
    switch (action.type) {
      case 'add':
        return {
          result: state.result + action.num
        }
      case 'minus':
        return {
          result: state.result - action.num
        }
    }
    return state
  }

  const [res, dispatch] = useReducer<Reducer<Data,Action>>(reducer, { result: 0 })

  return (
    <div className="App">
      <button onClick={() => {
        dispatch({ type: 'add', num: 1 })
      }}>{res.result }</button>
    </div>
  );
}

export default App;
```

# useRef

useRef 用来获取 dom 节点，或者获取组件的实例

```jsx
function App() {
    const inputRef = useRef < HTMLInputElement > null;

    useEffect(() => {
        inputRef.current?.focus();
    }, []);

    return (
        <div className="App">
            <input type="text" ref={inputRef} />
        </div>
    );
}
```

# forwardRef + useImperativeHandle

如果想把子组件的 ref 传递给父组件使用，可以使用 forwardRef 和 useImperativeHandle

比如

```jsx
import React, { useRef } from "react";
import "./App.css";

const childrenComponent: React.ForwardRefRenderFunction<HTMLInputElement> = (
    props,
    ref
) => {
    return (
        <div>
            <input ref={ref}></input>
        </div>
    );
};

const Wraped = React.forwardRef(childrenComponent);

function App() {
    const ref = useRef < HTMLInputElement > null;

    return (
        <div>
            <Wraped ref={ref} />
        </div>
    );
}

export default App;
```


![切图01](http://img.blog.loli.wang/2024-03-29-react-2/01.png)


# useContext 

跨任意组件传递数据，一般都会使用useContext来完成

```jsx
import React, { createContext, useContext } from 'react';
import './App.css';

const Context = createContext("test")

const Components:React.FC = () => {
  const value = useContext(Context)
 return <div>Context的值是 {value}</div>
}

function App() {
  return <Context.Provider value='222'>
    <div><Components/></div>
  </Context.Provider> 
}

export default App;

```
![切图02](http://img.blog.loli.wang/2024-03-29-react-2/02.png)

![切图03](http://img.blog.loli.wang/2024-03-29-react-2/03.png)


# memo + useMemo + useCallback
memo : 只有组件的props发生变化的时候，才会触发组件的重新渲染，否则总是返回缓存中的结果

useMemo : 一般通过减少不必要的复杂计算来优化性能,类似于计算属性

useCallback : 一般用于给子组件传递回调函数时，减少子组件的渲染次数，从而优化性能。