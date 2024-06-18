# 构建组件

在 JavaScript 中，`&&` 和 `||` 是逻辑运算符，用于处理布尔值和表达式。它们的含义如下：

### 1. 逻辑与运算符 `&&`：

- **语法：** `expr1 && expr2`

- **含义：** 如果 `expr1` 为真（truthy），则返回 `expr2` 的值；否则返回 `expr1` 的值。

- **应用：** 常用于条件语句和表达式中，用于在第一个条件为真时执行第二个条件。

```javascript
const result = (true && "Hello, World!"); // result 将为 "Hello, World!"
```

### 2. 逻辑或运算符 `||`：

- **语法：** `expr1 || expr2`

- **含义：** 如果 `expr1` 为真（truthy），则返回 `expr1` 的值；否则返回 `expr2` 的值。

- **应用：** 常用于设置默认值或者在某个条件为假时执行备用操作。

```javascript
const defaultValue = someValue || "Default Value";
```

### 3. 短路逻辑：

- **逻辑与 (`&&`) 短路：** 如果第一个条件为假，不会执行第二个条件，直接返回第一个条件的值。

```javascript
false && console.log("This won't be printed");
```

- **逻辑或 (`||`) 短路：** 如果第一个条件为真，不会执行第二个条件，直接返回第一个条件的值。

```javascript
true || console.log("This won't be printed");
```

短路逻辑是 JavaScript 中常用的一种技巧，它能够根据第一个条件的结果决定是否执行第二个条件，从而提高代码的效率。

## JSX

JSX（JavaScript XML）是一种在JavaScript中编写类似XML或HTML的语法的扩展。JSX允许你在JavaScript代码中嵌入HTML标签，以一种更直观和声明性的方式来描述UI的结构。

JSX表达式是在大括号 `{}` 中嵌套的JavaScript表达式，它允许你在JSX中插入动态的值、变量、函数调用等。在React中，JSX表达式通常用于描述React元素的结构和内容。

以下是一些使用JSX表达式的示例：

### 1. 插入变量：

```jsx
import React from 'react';

const name = 'John Doe';

const MyComponent = () => {
  return <p>Hello, {name}!</p>;
};
```

### 2. 使用表达式：

```jsx
import React from 'react';

const MyComponent = () => {
  const x = 5;
  const y = 10;

  return <p>The sum is {x + y}.</p>;
};
```

### 3. 调用函数：

```jsx
import React from 'react';

const greet = (name) => {
  return `Hello, ${name}!`;
};

const MyComponent = () => {
  return <p>{greet('Alice')}</p>;
};
```

### 4. 表达式作为属性值：

```jsx
import React from 'react';

const imageUrl = 'https://example.com/image.jpg';

const MyComponent = () => {
  return <img src={imageUrl} alt="An example" />;
};
```

在这些例子中，大括号 `{}` 内的内容都是JSX表达式。这些表达式的结果会在渲染时插入到JSX中。通过使用JSX表达式，你可以在React组件中更灵活地处理动态数据和逻辑。然而，需要注意的是，JSX表达式中的内容需要是一个有效的JavaScript表达式。

## 一.Fragments

在React中，Fragments（片段）是一种特殊的语法，用于组合多个子元素而无需添加额外的父级元素。Fragments是一种轻量级的方式，用于在不引入额外的DOM节点的情况下组织多个React元素。

在React 16及更高版本中，你可以使用空的标签 `<></>` 或 `<React.Fragment></React.Fragment>` 来创建 Fragments。例如：

```jsx
import React from 'react';

const MyComponent = () => {
  return (
    <>
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
    </>
  );
};
```

或者使用完整的 `<React.Fragment>` 语法：

```jsx
import React from 'react';

const MyComponent = () => {
  return (
    <React.Fragment>
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
    </React.Fragment>
  );
};
```

使用 Fragments 的主要优势是避免在DOM中引入不必要的父级元素。在某些情况下，当你不需要在页面上添加额外的包装元素时，使用 Fragments 可以使你的React组件更清晰和简洁。

在React中，Fragments还可以带有 key 属性，这在处理列表时非常有用。例如：

```jsx
import React from 'react';

const MyList = () => {
  const items = ['Item 1', 'Item 2', 'Item 3'];

  return (
    <>
      {items.map((item, index) => (
        <React.Fragment key={index}>
          <p>{item}</p>
        </React.Fragment>
      ))}
    </>
  );
};
```

这里，我们使用 Fragments 包装每个 `<p>` 元素，并为每个 Fragments 添加了唯一的 key。这有助于React在进行更新时更有效地识别元素。

## 二.渲染列表

在React中，渲染列表是一个常见的任务。你可以使用 `map()` 函数来遍历数组并生成对应的元素。以下是一个简单的例子：

```jsx
import React from 'react';

const MyList = () => {
  const items = ['Item 1', 'Item 2', 'Item 3'];

  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
};

export default MyList;
```

在这个例子中，`items` 是一个包含字符串的数组。我们使用 `map()` 函数遍历这个数组，为数组中的每个元素创建一个 `<li>` 元素。需要注意的是，我们给每个 `<li>` 元素添加了一个唯一的 `key` 属性，这有助于React进行高效的更新。

如果你的列表项是React组件，也可以直接在 `map()` 中返回这些组件：

```jsx
import React from 'react';

const MyList = () => {
  const items = [
    { id: 1, text: 'Item 1' },
    { id: 2, text: 'Item 2' },
    { id: 3, text: 'Item 3' },
  ];

  return (
    <ul>
      {items.map((item) => (
        <ListItem key={item.id} text={item.text} />
      ))}
    </ul>
  );
};

const ListItem = ({ text }) => {
  return <li>{text}</li>;
};

export default MyList;
```

在这个例子中，`items` 是一个包含对象的数组。我们使用 `map()` 函数遍历数组，为每个对象创建一个 `ListItem` 组件，并传递相应的数据作为属性。同样，每个 `ListItem` 组件都有一个唯一的 `key` 属性。这有助于React进行元素的有效更新。

记得在使用 `map()` 渲染列表时，为每个生成的元素添加一个唯一的 `key` 属性，以优化React的性能。

### 实例

```react
function ListGroup() {
  const items = ["New York", "San Francisco", "Tokyo", "London"];

  return (
    <>
      <h1>List</h1>
      <ul className="list-group">
        {items.map((item) => (
          <li key={item}>{item}</li>
        ))}
      </ul>
    </>
  );
}

export default ListGroup;

```

## 三.条件渲染

在React中，条件渲染是指根据某些条件来决定是否渲染特定的内容。这可以通过使用条件语句（如`if`语句）或者三元运算符来实现。以下是一些常见的条件渲染的例子：

### 1. 使用 if 语句：

```jsx
import React from 'react';

const MyComponent = ({ isLoggedIn }) => {
  if (isLoggedIn) {
    return <p>Welcome, User!</p>;
  } else {
    return <p>Please log in</p>;
  }
};

export default MyComponent;
```

### 2. 使用三元运算符：

```jsx
import React from 'react';

const MyComponent = ({ isLoggedIn }) => {
  return (
    <div>
      {isLoggedIn ? (
        <p>Welcome, User!</p>
      ) : (
        <p>Please log in</p>
      )}
    </div>
  );
};

export default MyComponent;
```

### 3. 使用逻辑 && 运算符：

```jsx
import React from 'react';

const MyComponent = ({ isLoggedIn }) => {
  return (
    <div>
      {isLoggedIn && <p>Welcome, User!</p>}
      {!isLoggedIn && <p>Please log in</p>}
    </div>
  );
};

export default MyComponent;
```

### 4. 使用条件渲染的函数：

```jsx
import React from 'react';

const WelcomeMessage = () => {
  return <p>Welcome, User!</p>;
};

const LoginForm = () => {
  return <p>Please log in</p>;
};

const MyComponent = ({ isLoggedIn }) => {
  return (
    <div>
      {isLoggedIn ? (
        <WelcomeMessage />
      ) : (
        <LoginForm />
      )}
    </div>
  );
};

export default MyComponent;
```

在这些例子中，`isLoggedIn` 是一个布尔值，根据它的值来决定渲染不同的内容。条件渲染允许你根据应用状态动态地显示或隐藏特定的UI元素。这在处理用户登录状态、权限控制等方面非常常见。

## 四.处理事件

在React中，事件处理是通过在JSX中使用事件属性来完成的。 **onClick() 当点击某个元素时，会触发某一个事件**

```react
import { MouseEvent } from "react";

function ListGroup() {
  const items = ["New York", "San Francisco", "Tokyo", "London"];

  const handleClick = (event: MouseEvent) => console.log(event);

  return (
    <>
      <h1>List</h1>
      {items.length === 0 && <p>No items found</p>}
      <ul className="list-group">
        {items.map((item) => (
          <li className="list-group-item" key={item} onClick={handleClick}> 
            {item}
          </li>
        ))}
      </ul>
    </>
  );
}

export default ListGroup;

```

## 五.管理状态

在React中，状态（state）是一个用于描述组件数据随时间变化的对象。通过管理组件的状态，你可以使组件根据用户输入、网络请求等动态地更新并重新渲染。

下面是关于在React中管理状态的一些基本概念和示例：

### 1. 使用 `useState` Hook：

在函数式组件中，你可以使用 `useState` Hook 来声明和使用状态。

```react
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

export default Counter;
```

在这个例子中，`useState` Hook 返回一个包含当前状态和更新状态的函数的数组。通过调用 `setCount` 函数，你可以更新 `count` 的值，并触发组件的重新渲染。

### 实例

```react
import { useState } from "react";

function ListGroup() {
  const items = ["New York", "San Francisco", "Tokyo", "London"];

  const [selectIndex,setSelectIndex] = useState(-1)

  return (
    <>
      <h1>List</h1>
      {items.length === 0 && <p>No items found</p>}
      <ul className={'list-group'}>
        {items.map((item,index) => (
          <li 
            className={
              selectIndex === index ? "list-group-item active" : "list-group-item"
            }
            key={item} 
            onClick={() => { setSelectIndex(index) }}
            >
            {item}
          </li>
        ))}
      </ul>
    </>
  );
}

export default ListGroup;
```

点击一个列表会凸显出蓝色，实时变换状态



## 六.通过Props传递数据

**我们想把组件变为可重用组件,需要用到接口来传递数据**

```react
//ListGroup组件
import { useState } from "react";

interface Props {
  items : string[];
  heading : string;
}

function ListGroup({items ,heading}: Props) {
  const [selectIndex,setSelectIndex] = useState(-1)

  return (
    <>
      <h1>{heading}</h1>
      {items.length === 0 && <p>No items found</p>}
      <ul className={'list-group'}>
        {items.map((item,index) => (
          <li 
            className={
              selectIndex === index ? "list-group-item active" : "list-group-item"
            }
            key={item} 
            onClick={() => { setSelectIndex(index) }}
            >
            {item}
          </li>
        ))}
      </ul>
    </>
  );
}
```

```react
//App主组件
import ListGroup from "./components/ListGroup";


function App(){
  const items = ["New York", "San Francisco", "Tokyo", "London"];
  return <div><ListGroup items={items} heading="Cities" /></div>;
}


export default App;
```

通过从主组件中传递数据，到其他组件中实现，可以实现该组件的复用



## 七.通过Props传递函数

在现实中的应用程序通常会在项目被选中后发生一些事情(例如:我们想跳转到另一个页面，过滤一个什么东西)

我们不能在可重用组件中去定义函数去实现它

就想要去父组件中去定义函数

```react
//ListGroup组件
import { useState } from "react";

interface Props {
  items: string[];
  heading: string;
  onSelectItem: (item: string) => void;
}

function ListGroup({ items, heading, onSelectItem }: Props) {
  const [selectIndex, setSelectIndex] = useState(-1);

  return (
    <>
      <h1>{heading}</h1>
      {items.length === 0 && <p>No items found</p>}
      <ul className={"list-group"}>
        {items.map((item, index) => (
          <li
            className={
              selectIndex === index
                ? "list-group-item active"
                : "list-group-item"
            }
            key={item}
            onClick={() => {
              setSelectIndex(index);
              onSelectItem(item);
            }}
          >
            {item}
          </li>
        ))}
      </ul>
    </>
  );
}

export default ListGroup;

```

```react
//App组件
import ListGroup from "./components/ListGroup";

function App() {
  const items = ["New York", "San Francisco", "Tokyo", "London"];

  const handleSelectItem = (item: string) => {
    console.log(item);
  };

  return (
    <div>
      <ListGroup
        items={items}
        heading="Cities"
        onSelectItem={handleSelectItem}
      />
    </div>
  );
}

export default App;

```

在React中，`onSelectItem={handleSelectItem}` 和 `onSelectItem={handleSelectItem()}` 是不同的。让我解释一下这两者之间的区别。

### 1. `onSelectItem={handleSelectItem}`

这种写法将 `handleSelectItem` 函数本身传递给 `onSelectItem` 属性。这意味着，当在 `ListGroup` 组件中调用 `onSelectItem` 时，实际上调用的是 `handleSelectItem` 函数的引用。

```react
// 在 ListGroup 组件内部
props.onSelectItem('someItem'); // 调用的是 handleSelectItem 函数本身
```

### 2. `onSelectItem={handleSelectItem()}`

这种写法会在 `App` 组件渲染时立即调用 `handleSelectItem` 函数，并将其返回值传递给 `onSelectItem` 属性。这可能导致不希望的副作用，特别是如果 `handleSelectItem` 返回的是一个函数。

```react
// 在 App 组件内部
const result = handleSelectItem(); // 立即调用 handleSelectItem 函数
props.onSelectItem(result); // 将返回值传递给 onSelectItem
```

### 总结：

- 使用 `onSelectItem={handleSelectItem}` 时，你传递的是函数的引用，而不是函数的调用结果。
- 使用 `onSelectItem={handleSelectItem()}` 时，你传递的是函数的调用结果，可能会导致不必要的副作用。

在大多数情况下，你应该使用第一种写法，即 `onSelectItem={handleSelectItem}`，这样做更为常见，而且更符合React中的事件处理模式。

## 八.children属性

在React中，`children` 是一个特殊的 `prop`，它代表组件的子元素。通常，`children` 是一个React节点或一组React节点，

**它允许在组件内部插入其他组件或任意的React元素。**

在你的代码中，通过 TypeScript 中的 `ReactNode` 类型，你在组件的 `Props` 接口中指定了 `children` 的类型。

```typescript
import { ReactNode } from "react";

interface Props {
    children: ReactNode;
}

const Alert = ({ children }: Props) => {
  return (
    <div className="alert alert-primary">{children}</div>
  )
}

export default Alert;
```

这里的 `ReactNode` 是一个泛型类型，它表示可以包含任意React节点的类型。这包括 `JSX` 元素、字符串、数字、组件、或者包含它们的数组。

使用 `ReactNode` 类型允许你在 `Alert` 组件中以灵活的方式接受和处理子元素，例如：

```jsx
<Alert>
  <p>This is a message.</p>
  <button>OK</button>
</Alert>
```

在这个例子中，`<p>` 和 `<button>` 元素就是 `children`，它们会被嵌套在 `Alert` 组件中，并在组件内部通过 `{children}` 渲染。

## 九.经典练习

```react
//App组件
import { useState } from "react";
import Alert from "./components/Alert";
import Button from "./components/Button";

function App() {

  const [alertVisible,setAlertVisiblility] = useState(false);

  return (
    <div>
      {alertVisible && <Alert onClose={() => setAlertVisiblility(false)}>你点击了这个按钮! 很棒</Alert>}
      <Button color="primary" onClick={() => setAlertVisiblility(true)}>My button</Button>
    </div>
  );
}

export default App;

```

```react
//Alert组件
import { ReactNode } from "react";

interface Props{
    children : ReactNode;
    onClose : () => void
}

const Alert = ({children,onClose}: Props) => {
  return (
    <>
    <div className="alert alert-primary alert-dismissible">{children}</div>
    <button type="button" className="btn-close" onClick={onClose} data-bs-dismiss="alert" aria-label="Close"></button>
    </>
  )
}

export default Alert
```

```react
//Button组件

interface Props {
    children: string;
    color: 'primary' | 'secondary' | 'danger';
    onClick:() => void;
}



const Button = ({children,onClick,color}:Props) => {
  return (
    <button className={"btn btn-"+ color} onClick={onClick}>{children}</button>
  )
}

export default Button
```









# React中的CSS

## Vanilla CSS

想要自定义样式，就在component文件夹中，去创建一个文件夹，把该组件和css文件放进去

## CSS Modules

在子组件和父组件中到自定义css样式时，在一个地方出现相同css样式，会产生冲突

就需要css modules来解决



## CSS-in-js

在这里面我们把css文件代码放到组件中，提供一份全新想法

下载这个包

```
npm i styled-components
```



源码

```react
import { useState } from "react";
import './ListGroup.css'
import styled from "styled-components";


const List =styled.ul`
  list-style: none;
  padding: 0 ;
`;

interface ListItemProps {
  active:boolean;
}


const ListItem =styled.li<ListItemProps>`
  padding: 5px 0;
  background: ${ (props) => (props.active ? 'blue' : 'none')} ;
`;


interface Props {
  items: string[];
  heading: string;
  onSelectItem: (item: string) => void;
}

function ListGroup({ items, heading, onSelectItem }: Props) {
  const [selectIndex, setSelectIndex] = useState(-1);

  return (
    <>
      <h1>{heading}</h1>
      {items.length === 0 && <p>No items found</p>}
      <List>
        {items.map((item, index) => (
          <ListItem
           active ={index === selectIndex}
            key={item}
            onClick={() => {
              setSelectIndex(index);
              onSelectItem(item);
            }}
          >
            {item}
          </ListItem>
        ))}
      </List>
    </>
  );
}

export default ListGroup;

```



## 图标

下个包

```
npm i react-icons@4.7.1
```



```
https://react-icons.github.io/react-icons/
```

可以访问这个网站，去选中图标



## 设计Like组件

```react
//Like组件
import { useState } from "react";
import { IoHeart } from "react-icons/io5";


interface Props{
  onClick : () => void
}


const Like = ({onClick}: Props) => {
  const [status,setStatus] = useState(false);

  const toggle = () =>{
    setStatus(!status);
    onClick();
  }

  if (status) return <IoHeart color="#ff6b81" size={50} onClick={toggle}/>
  return <IoHeart size={50} onClick={toggle}/>
  
}

export default Like
```

```react
//App组件
import Like from "./components/Like";

function App() {
  return <div><Like onClick={() => console.log("Clicked")}/></div>;

}

export default App;

```











# 管理组件状态



## 一.State Hook

### 1.react异步更新State

在 React 中，状态（state）的更新通常是异步的，这是为了优化性能。当你调用状态更新函数时，React 并不会立即修改状态值，而是将这个更新任务放到队列中，稍后在适当的时机执行。这种机制称为异步更新状态。总的来说，了解 React 异步更新状态的特性对于正确处理状态和确保最佳性能是很重要的。如果你需要在状态更新后执行一些操作，最好使用回调函数或者函数式更新的形式。这有助于确保你得到的是最新的状态值

### 2.State实际上储存在组件之外

### 3.只能在组件的顶部使用Hook



## 二.选择State结构

1. 避免多余的状态变量。
2. 将相关变量集中在一个对象中。

3. 避免深度嵌套结构。

   ### 实例

   #### 不佳的例子：

   ```react
   Copy codeimport React, { useState } from 'react';
   
   function UserProfile() {
     const [name, setName] = useState('John');
     const [age, setAge] = useState(25);
     const [address, setAddress] = useState('123 Main St');
   
     return (
       <div>
         <p>Name: {name}</p>
         <p>Age: {age}</p>
         <p>Address: {address}</p>
       </div>
     );
   }
   
   export default UserProfile;
   ```

   #### 改进的例子：

   ```react
   import React, { useState } from 'react';
   
   function UserProfile() {
     const [user, setUser] = useState({
       name: 'John',
       age: 25,
       address: '123 Main St',
     });
   
     return (
       <div>
         <p>Name: {user.name}</p>
         <p>Age: {user.age}</p>
         <p>Address: {user.address}</p>
       </div>
     );
   }
   
   export default UserProfile;
   ```

   在这个例子中，将用户的相关信息集中在一个对象 `user` 中，而不是分散在多个状态变量中。这样做可以提高代码的可读性和可维护性，并且使得将来可能添加或修改的用户属性更容易处理。



## 三.保持组件的纯净

如果在父类组件中传递相同的值给子组件时，在第二次之后react不会重新呈现该组件，直接返回之前渲染的组件，以提高性能





## 四.react的严格模式

React 的严格模式（Strict Mode）是一种开发者工具，用于辅助检测应用程序中潜在的问题，并在开发过程中提供更多的警告信息。严格模式是一种开发时的辅助工具，不会影响生产环境。

要启用 React 的严格模式，可以在组件树的根节点包裹 `<React.StrictMode>`。例如，在应用的入口文件中：

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
);
```

在这个例子中，`<React.StrictMode>` 包裹了应用的根组件 `<App />`。现在，应用中的所有组件都会受到严格模式的影响。

严格模式提供的功能包括：

1. **警告未来的不安全的生命周期函数：** 在未来版本的 React 中，一些生命周期函数将被废弃或重命名。严格模式会在使用这些不安全的生命周期函数时发出警告，以帮助开发者适应即将到来的变化。

2. **检测不安全的内部使用情况：** 严格模式会检测一些不安全的内部使用情况，例如使用 `findDOMNode`，以帮助开发者迁移到更稳定的替代方法。

3. **检测副作用：** **在渲染期间，React 会以两次调用的方式调用函数组件。**严格模式会检测在渲染期间可能引起副作用的操作，并在开发模式下发出警告。这有助于识别可能导致 bug 的副作用。

使用严格模式是一个好的实践，因为它有助于提前发现并解决一些潜在问题，使得应用更加健壮。但需要注意的是，严格模式可能会在某些情况下产生一些额外的警告，而这些警告在正常运行时可能并不会出现。因此，最好在开发过程中使用严格模式，而在生产环境中关闭它。



## 五.更新状态对象

为了遵循 React 的最佳实践，通常建议将状态对象视为不可变的，不直接修改原始状态对象，而是通过创建新的状态对象来更新。这样可以确保 React 正确地检测到状态的变化，从而触发组件的重新渲染。

以下是一个例子，演示如何通过创建新的状态对象来更新状态：

```jsx
import React, { useState } from 'react';

function UserProfile() {
  // 初始状态
  const initialUser = {
    name: 'John',
    age: 25,
    address: '123 Main St',
  };

  // 使用 useState 初始化状态
  const [user, setUser] = useState(initialUser);

  // 更新状态的函数，通过创建新的状态对象
  const updateUser = () => {
    // 创建新的状态对象，修改 age 属性
    const newUser = { ...user, age: user.age + 1 };

    // 使用 setUser 更新状态
    setUser(newUser);
  };

  return (
    <div>
      <p>Name: {user.name}</p>
      <p>Age: {user.age}</p>
      <p>Address: {user.address}</p>
      <button onClick={updateUser}>Update Age</button>
    </div>
  );
}

export default UserProfile;
```

在这个例子中，通过使用展开运算符 `{ ...user, age: user.age + 1 }`，我们创建了一个新的状态对象 `newUser`，并在其中修改了 `age` 属性。然后，我们使用 `setUser` 函数将新的状态对象应用到组件的状态中。

通过这种方式，我们确保了原始状态对象 `user` 的不可变性，使得 React 可以正确地检测到状态的变化，并触发组件的重新渲染。这是一种常见的模式，特别是当状态对象较为复杂时。



## 六.更新嵌套对象

更新嵌套对象时，也可以使用不可变性的原则，确保创建一个新的对象以触发 React 的重新渲染。以下是一个例子，演示如何更新嵌套对象：

```jsx
import React, { useState } from 'react';

function UserProfile() {
  // 初始状态
  const initialUser = {
    name: 'John',
    details: {
      age: 25,
      address: '123 Main St',
    },
  };

  // 使用 useState 初始化状态
  const [user, setUser] = useState(initialUser);

  // 更新嵌套对象的函数，通过创建新的状态对象
  const updateDetails = () => {
    // 创建新的状态对象，修改嵌套对象中的 age 属性
    const newUser = {
      ...user,
      details: {
        ...user.details,
        age: user.details.age + 1,
      },
    };

    // 使用 setUser 更新状态
    setUser(newUser);
  };

  return (
    <div>
      <p>Name: {user.name}</p>
      <p>Age: {user.details.age}</p>
      <p>Address: {user.details.address}</p>
      <button onClick={updateDetails}>Update Age</button>
    </div>
  );
}

export default UserProfile;
```

在这个例子中，我们通过使用嵌套的展开运算符 `{ ...user, details: { ...user.details, age: user.details.age + 1 } }`，创建了一个新的状态对象 `newUser`，并在其中修改了嵌套对象 `details` 中的 `age` 属性。然后，我们使用 `setUser` 函数将新的状态对象应用到组件的状态中。

这样做的好处是确保了原始状态对象 `user` 和嵌套对象 `details` 的不可变性，使得 React 能够正确地检测到状态的变化并进行重新渲染。

## 七.更新数组

更新数组时，同样要遵循不可变性的原则，确保创建一个新的数组以触发 React 的重新渲染。以下是一个例子，演示如何更新数组：

```jsx
import React, { useState } from 'react';

function TodoList() {
  // 初始状态
  const initialTodos = [
    { id: 1, text: 'Learn React', completed: false },
    { id: 2, text: 'Build a project', completed: false },
  ];

  // 使用 useState 初始化状态
  const [todos, setTodos] = useState(initialTodos);

  // 更新数组的函数，通过创建新的状态数组
  const toggleTodo = (id) => {
    // 创建新的状态数组，修改特定元素的 completed 属性
    const newTodos = todos.map(todo =>
      todo.id === id ? { ...todo, completed: !todo.completed } : todo
    );

    // 使用 setTodos 更新状态
    setTodos(newTodos);
  };

  return (
    <div>
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>
            <input
              type="checkbox"
              checked={todo.completed}
              onChange={() => toggleTodo(todo.id)}
            />
            <span>{todo.text}</span>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default TodoList;
```

在这个例子中，通过使用 `map` 方法创建了一个新的状态数组 `newTodos`，并在其中修改了特定元素的 `completed` 属性。然后，使用 `setTodos` 函数将新的状态数组应用到组件的状态中。

这种方式确保了原始数组 `todos` 的不可变性，使得 React 能够正确地检测到状态的变化并进行重新渲染。在更新数组时，一定要注意使用不可变的方法，避免直接修改原始数组。

## 八.使用 Immer 简化更新逻辑

Immer 是一个用于简化不可变数据结构更新逻辑的库，特别适用于 React 中的状态管理。它允许你以一种更直观和可变的方式编写代码，同时在内部保持了不可变性，使得 React 能够更轻松地检测到状态的变化。

下面是一个简单的例子，演示如何使用 Immer 来更新一个嵌套的对象：

首先，确保你已经安装了 Immer：

```bash
npm install immer
```

然后，可以在组件中使用 Immer：

```jsx
import React, { useState } from 'react';
import produce from 'immer';

function UserProfile() {
  // 初始状态
  const initialUser = {
    name: 'John',
    details: {
      age: 25,
      address: '123 Main St',
    },
  };

  // 使用 useState 初始化状态
  const [user, setUser] = useState(initialUser);

  // 更新嵌套对象的函数，使用 Immer
  const updateDetails = () => {
    // 使用 Immer 的 produce 函数来创建新的状态
    const newUser = produce(user, draft => {
      draft.details.age += 1;
    });

    // 使用 setUser 更新状态
    setUser(newUser);
  };

  return (
    <div>
      <p>Name: {user.name}</p>
      <p>Age: {user.details.age}</p>
      <p>Address: {user.details.address}</p>
      <button onClick={updateDetails}>Update Age</button>
    </div>
  );
}

export default UserProfile;
```

在这个例子中，`produce` 函数是 Immer 提供的主要函数，它接受一个原始状态（这里是 `user`），以及一个回调函数，允许你在回调函数中直接修改状态。Immer 会确保在内部使用不可变性，并返回一个新的状态。

使用 Immer，你可以避免手动进行深度复制和展开操作，而是以更直观的方式更新状态。这在处理复杂的嵌套对象时尤其有用。





## 九.组件之间共享状态

在 React 中，组件之间共享状态的最佳方式通常是将状态提升到共同的父组件中，然后通过 props 将状态传递给子组件。这种模式称为“提升状态”或“状态提升”。

以下是一个简单的例子，演示了如何在父组件中管理状态，并将状态通过 props 传递给子组件：

```jsx
import React, { useState } from 'react';

// 子组件
function ChildComponent({ count, onIncrement }) {
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={onIncrement}>Increment</button>
    </div>
  );
}

// 父组件
function ParentComponent() {
  // 在父组件中管理状态
  const [count, setCount] = useState(0);

  // 定义用于更新状态的函数
  const incrementCount = () => {
    setCount(count + 1);
  };

  // 将状态和更新函数通过 props 传递给子组件
  return (
    <div>
      <h1>Parent Component</h1>
      <ChildComponent count={count} onIncrement={incrementCount} />
    </div>
  );
}

export default ParentComponent;
```

在这个例子中，`ParentComponent` 包含一个状态变量 `count` 和用于更新状态的函数 `incrementCount`。这个状态以及更新函数通过 props 传递给 `ChildComponent`。在 `ChildComponent` 中，它可以读取 `count` 的值，并调用 `onIncrement` 函数来更新父组件的状态。

这种方式的好处是：

1. **单一数据源：** 状态被提升到最近的共同父组件，使得状态变得集中且易于管理。

2. **单向数据流：** 数据流是单向的，自上而下传递，这样更容易追踪数据的流动。

3. **可重用性：** 子组件可以更容易地被复用，因为它们不依赖于局部状态。

如果应用程序变得更为复杂，你可能会考虑使用一些状态管理库，如 Redux 或 React Context API，来更方便地管理全局状态。但对于简单的情况，状态提升是一个简单而有效的模式。

### 实例

通过在父组件中构建状态钩子来动态管理两个子组件

```react
//父组件中app.tsx
import { useState } from "react";
import Cart from "./components/Cart";
import NavBar from "./components/NavBar";

function App() {
  const [cartItem,setCartItem] =useState(['product1','product2'])

  return (
    <>
    <div>
      <NavBar cartItemCount={cartItem.length}/>
      <Cart cartItem={cartItem} onClear={() => setCartItem([])}/>
    </div>
    </>
  )

}

export default App;

```

```react
//NavBar子组件中
interface Props{
    cartItemCount:number;
}

const NavBar = ({cartItemCount}:Props) => {
  return (
    <div>NavBar {cartItemCount}</div>
  )
}

export default NavBar
```

```react
//Cart子组件中
interface Props{
    cartItem : string[]
    onClear: ()=> void
}


const Cart = ({cartItem,onClear}:Props) => {
  return (
    <>
    <div>Cart
        <ul>{cartItem.map(item => <li key={item}>{item}</li>)}</ul>
    </div>
    <button onClick={onClear}>Clear</button>
    </>
  )
}

export default Cart
```

## 练习

1.点击按钮，到数组中添加一个字符串

```react
import { useState } from "react";
import Game from "./components/Game";


function App() {
  const [pizza,setPizza] =useState({
    name : 'wangxu',
    toppings : ['Mushroom']
  });

  const handleClick = () =>{
    setPizza({...pizza,toppings: [...pizza.toppings,'Cheese']})
  }

  return (
    <>
    <div>{pizza.name},{pizza.toppings}</div>
      <Game onChange={handleClick}>Click me</Game>
    </>
  )

}

export default App;

```

2.把数组里的一个对象的数量换为2

```react
import { useState } from "react";
import Game from "./components/Game";


function App() {
  const [cart,setCart] =useState({
    discount : 0.9,
    items :[
      { id : 1, title:'Product 1', quantity:1},
      { id : 2, title:'Product 2', quantity:1}
    ]
  });

  const handleClick = () =>{
    setCart({...cart, items:cart.items.map(item => item.id === 1 ? {...item, quantity:2}:item)})
  }

  return (
    <>
      <Game onChange={handleClick}>Click me</Game>
    </>
  )

}

export default App;

```

## 十.可扩展文本

```react
import { useState } from "react";


interface Props{
    children : string;
    maxChars?: number;
}

const ExpandableText = ({children,maxChars = 100}:Props) => {
    const [isExpanded, setExpanded] = useState(false);
    
    if (children.length <=maxChars) return <p>{children}</p>;

    const text = isExpanded ? children : children.substring(0,maxChars);

    return (
        <p>{text}...<button onClick={()=> setExpanded(!isExpanded)}>{isExpanded ? 'Less':'More'}</button></p>
    )
}

export default ExpandableText
```

### 我们不应该对任何可以计算的值使用状态钩子, 我们仅使用状态钩子储存可能随时间变化的值

确切来说，React 的状态钩子（如 `useState`）通常用于存储在组件渲染期间可能发生变化的值。一般来说，不建议将状态钩子用于存储计算值或不变的静态值，因为这样做可能会导致性能浪费。

举例说明，假设我们有一个计数器组件，它需要显示计数的平方值。在这种情况下，我们应该使用状态来存储计数，而不是计算值。

```jsx
import React, { useState } from 'react';

function Counter() {
  // 正确的用法：使用状态存储可能变化的值
  const [count, setCount] = useState(0);

  // 计算平方值
  const square = count * count;

  return (
    <div>
      <p>Count: {count}</p>
      <p>Square: {square}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;
```

在这个例子中，`count` 是一个可能会变化的值，因此我们使用了状态来存储它。然后，我们计算 `square`，但是我们没有使用状态来存储它，因为它是通过计算得到的不变的值。使用状态来存储 `square` 是不必要的，因为它不会在组件渲染之间发生变化。

如果我们错误地使用状态来存储 `square`，那么每次更新 `count` 时都会触发组件的重新渲染，尽管 `square` 的值实际上并没有发生变化，这可能导致不必要的性能开销。

总的来说，使用状态存储可能随时间变化的值，而不是计算值或静态值。对于不会在组件渲染之间变化的值，直接声明为常量或使用计算属性是更合适的做法。



# 构建表单

## 一.创建一个表单组件

```tsx
const Form = () => {
  return (
    <form>
      <div className="mb-3">
        <label htmlFor="name" className="form-label">
          Name
        </label>
        <input id="name" type="text" className="form-control" />
      </div>
      <div className="mb-3">
        <label htmlFor="age" className="form-label">Age</label>
        <input id="age" type="number" className="form-control" />
      </div>
      <button className="btn btn-primary" type="submit">Submit</button>
    </form>
  );
};

export default Form;

```

在你提供的代码片段中，有一个 `<label>` 元素和一个 `<input>` 元素。让我们逐个解释它们的属性：

1. **`htmlFor` 属性：**
   - `htmlFor` 属性是 `<label>` 元素的属性，用于指定与该标签关联的表单元素的 `id`。
   - 在这个例子中，`htmlFor="name"` 意味着该 `<label>` 元素与 `<input>` 元素的 `id` 为 "name" 的表单元素相关联。这种关联对于辅助技术（如屏幕阅读器）和用户体验很有帮助，当用户点击标签时，浏览器会将焦点自动移动到与 `htmlFor` 相关联的表单元素。

2. **`id` 属性：**
   - `id` 属性是 `<input>` 元素的属性，用于唯一标识该输入元素。
   - 在这个例子中，`id="name"` 使得该 `<input>` 元素的唯一标识符是 "name"。与 `<label>` 元素的 `htmlFor` 属性关联，这有助于提高可访问性和用户体验。

3. **`type` 属性：**
   - `type` 属性是 `<input>` 元素的属性，用于指定输入字段的类型。
   - 在这个例子中，`type="text"` 表示这是一个文本输入字段，用户可以在其中输入任意文本。

因此，整个代码片段的作用是创建一个带有标签和文本输入字段的表单组件，`htmlFor` 与 `id` 属性用于关联标签和输入字段，而 `type` 属性用于指定输入字段的类型。

## 二.处理表格提交

```react
import { FormEvent } from "react";



const Form = () => {

    const handleSubmit = (event: FormEvent) =>{
        event.preventDefault(); // 阻止默认提交行为
        console.log('Submitted')
    }

  return (
    <form onSubmit={handleSubmit}>
      <div className="mb-3">
        <label htmlFor="name" className="form-label">
          Name
        </label>
        <input id="name" type="text" className="form-control" />
      </div>
      <div className="mb-3">
        <label htmlFor="age" className="form-label">Age</label>
        <input id="age" type="number" className="form-control" />
      </div>
      <button className="btn btn-primary" type="submit">Submit</button>
    </form>
  );
};

export default Form;
```

## 三.访问输入字段

`useRef` 是 React 提供的一个 Hook，用于创建可变的对象，其 `current` 属性可以被赋值为任何可变的值，通常用于访问或存储组件中的 DOM 元素、保持可变状态，以及其他类似的情况。

```react
import { FormEvent, useRef } from "react";



const Form = () => {
    const nameRef = useRef<HTMLInputElement>(null);
    const ageRef = useRef<HTMLInputElement>(null);
    const person = { name:'', age:0 };

    const handleSubmit = (event: FormEvent) =>{
    event.preventDefault(); 
    if (nameRef.current != null)
    person.name =nameRef.current.value
    if (ageRef.current != null)
    person.age =parseInt(ageRef.current.value);
    console.log(person);
    
    }

  return (
    <form onSubmit={handleSubmit}>
      <div className="mb-3">
        <label htmlFor="name" className="form-label">
          Name
        </label>
        <input ref={nameRef} id="name" type="text" className="form-control" />
      </div>
      <div className="mb-3">
        <label htmlFor="age" className="form-label">Age</label>
        <input ref={ageRef} id="age" type="number" className="form-control" />
      </div>
      <button className="btn btn-primary" type="submit">Submit</button>
    </form>
  );
};

export default Form;

```


在 `useRef` 的泛型参数中，`null` 表示初始时该引用没有关联到任何 DOM 元素。具体来说，这是 `useRef` 的初始值，用于指定初始的 `current` 属性的值。

在这里，`useRef<HTMLInputElement>(null)` 中的 `<HTMLInputElement>` 部分是 TypeScript 的泛型语法，用于告诉 TypeScript，`current` 属性的类型应该是 `HTMLInputElement | null`。这是因为 `useRef` 可以用于引用任何类型的对象，不仅仅是 DOM 元素。

使用 `null` 作为初始值的情况通常表示在组件初始渲染阶段，这个引用还没有指向任何具体的 DOM 元素。在组件渲染后，`useRef` 的 `current` 属性可以被更新为指向实际的 DOM 元素，例如通过 `ref` 属性将其与某个 JSX 元素关联起来。

在你的代码中，`nameRef` 和 `ageRef` 最初都指向 `null`，但随后可以通过 `ref` 属性与对应的输入框元素关联。这是在组件渲染时，React 会将 `nameRef.current` 和 `ageRef.current` 更新为对应的输入框 DOM 元素的**引用**

## 四.受控组件

在 React 中，受控组件是指表单元素的值受 React 组件状态（state）的控制。具体而言，通过使用 React 的状态管理机制，将表单元素的值与组件的状态关联在一起，使得组件能够完全控制表单元素的值。

### 受控组件的特点：

1. **状态管理：** 表单元素的值被存储在组件的状态中。
   
2. **事件驱动：** 表单元素的值发生变化时，触发相应的事件，通常是 `onChange` 事件。

3. **单一数据源：** 组件的状态是唯一确定表单元素值的数据源，使得 React 成为单一数据源的架构。

### 受控组件的使用方法：

1. **在组件的 state 中存储表单元素的值：**
   
   ```jsx
   import React, { useState } from 'react';
   
   const MyForm = () => {
     const [inputValue, setInputValue] = useState('');
   
     const handleInputChange = (event) => {
       setInputValue(event.target.value);
     };
   
     return (
       <div>
         <label htmlFor="myInput">输入框：</label>
         {/* 受控组件：值通过状态管理 */}
         <input
           type="text"
           id="myInput"
           value={inputValue}
           onChange={handleInputChange}
         />
         <p>输入的值是：{inputValue}</p>
       </div>
     );
   };
   
   export default MyForm;
   ```

2. **通过 `value` 属性控制输入框的值：**
   
   使用 `value` 属性将输入框的值与组件的状态关联，这样输入框的值将始终受到状态的控制。

3. **处理 onChange 事件：**

   `onChange` 事件负责在输入框的值发生变化时更新组件状态。

4. **实时更新：**

   由于状态的改变导致了 `render` 方法的调用，组件会重新渲染，并且 `inputValue` 的新值将被反映在输入框中。

通过这种方式，React 组件拥有对表单元素的完全控制权，可以在每次值发生变化时执行自定义逻辑。这种方式也使得在 React 应用中更容易实现一致性和可维护性。

### 实例

```react
import { FormEvent, useState } from "react";

const Form = () => {
  const [person, setPerson] = useState({
    name: "",
    age: 0,
  });

  const handleSubmit = (event: FormEvent) => {
    event.preventDefault();
    console.log(person);
  };

  return (
    <form onSubmit={handleSubmit}>
      <div className="mb-3">
        <label htmlFor="name" className="form-label">
          Name
        </label>
        <input
          onChange={(event) =>
            setPerson({ ...person, name: event.target.value })
          }
          value={person.name}
          id="name"
          type="text"
          className="form-control"
        />
      </div>
      <div className="mb-3">
        <label htmlFor="age" className="form-label">
          Age
        </label>
        <input
          onChange={(event) =>
            setPerson({ ...person, age: parseInt(event.target.value) })
          }
          value={person.age}
          id="age"
          type="number"
          className="form-control"
        />
      </div>
      <button className="btn btn-primary" type="submit">
        Submit
      </button>
    </form>
  );
};

export default Form;

```

在这个React组件中，`input` 元素的 `onChange` 属性和 `value` 属性是用于创建一个受控组件的关键部分。下面我会解释这两个属性的作用：

### `onChange` 属性：

```jsx
<input
  onChange={(event) =>
    setPerson({ ...person, name: event.target.value })
  }
  // ...
/>
```

- **作用：** `onChange` 是一个事件处理函数，它在用户输入值时触发。每当输入框的值发生变化时，这个函数会被调用。
  
- **处理逻辑：** 当 `onChange` 事件被触发时，会调用一个匿名函数，该函数接收事件对象 `event`，然后调用 `setPerson` 更新组件的状态。
  
- **更新状态：** 这里使用了对象的解构语法 `{ ...person, name: event.target.value }`，创建了一个新的包含更新后的 `name` 值的对象，并通过 `setPerson` 将新对象设置为组件的状态。

### `value` 属性：

在React中，`value`属性用于绑定输入元素的值。在上述代码中，`value`被用于控制两个输入框的值：

```jsx
<input
  onChange={(event) =>
    setPerson({ ...person, name: event.target.value })
  }
  value={person.name}  // 这里的value用于绑定person对象中的name属性值
  id="name"
  type="text"
  className="form-control"
/>
```

和

```jsx
<input
  onChange={(event) =>
    setPerson({ ...person, age: parseInt(event.target.value) })
  }
  value={person.age}   // 这里的value用于绑定person对象中的age属性值
  id="age"
  type="number"
  className="form-control"
/>
```

`value`属性实际上是将输入框的值绑定到`person`状态对象中对应的属性上。这样，当用户输入时，React会通过`onChange`事件来更新`person`状态对象的相应属性，从而保持输入框的值与状态的同步。

在React中使用`value`属性有助于将输入框的值与状态进行双向绑定，使得React组件能够更方便地管理和响应用户输入。



## 五.使用 React Hooks 来管理表单

下载第三方包

```
npm i react-hook-form@7.43
```

`react-hook-form` 是一个用于 React 的表单库，它旨在简化和优化 React 中复杂表单的管理。该库提供了一组钩子（hooks）和组件，使得表单的构建、验证、状态管理等变得更加轻松和灵活。以下是 `react-hook-form` 的一些主要特点和作用：

1. **简化表单开发：**
   - `react-hook-form` 提供了一组简单易用的 API，使得表单的构建和管理变得更加简洁。通过使用钩子和提供的组件，你可以轻松地定义和处理表单字段。

2. **减少渲染次数：**
   - 该库采用了优化策略，能够减少表单元素的渲染次数，提高性能。它使用了轻量级的观察者模式，只在需要更新的时候才触发渲染。

3. **异步验证：**
   - 支持异步验证，允许你在表单字段上执行异步验证逻辑。这对于需要与服务器进行交互或执行复杂验证的场景非常有用。

4. **自动注册：**
   - 表单字段的注册过程被大大简化。不再需要手动注册每个字段，库会自动从输入组件中提取必要的信息。

5. **更好的输入控制：**
   - 提供了强大的输入控制功能，允许你自由地定义输入元素的属性，而不必担心 React 的表单事件。

6. **集成了 yup 和 zod 等验证库：**
   - `react-hook-form` 可以与一些常用的验证库集成，例如 `yup` 和 `zod`，以便于执行更复杂的表单验证。

7. **可选的 UI 库：**
   - 你可以选择使用 `react-hook-form` 提供的默认 UI 组件，也可以完全自定义表单的外观和样式。

8. **支持多种输入控制：**
   - 支持多种表单元素，包括输入框、选择框、单选框、复选框等。

9. **对无障碍性的支持：**
   - 考虑到无障碍性需求，`react-hook-form` 设计了易于访问的表单组件。

使用 `react-hook-form` 可以帮助开发者更轻松、高效地构建和管理复杂的表单，同时保持良好的性能。这个库的文档详细且友好，提供了丰富的示例和用法说明。

### 实例

```react
import {  FieldValues, useForm } from "react-hook-form";

const Form = () => {
  const { register,handleSubmit } = useForm();
  console.log(register('name'));
  
  const onSubmit = ((data:FieldValues)=>console.log(data))

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div className="mb-3">
        <label htmlFor="name" className="form-label">
          Name
        </label>
        <input
          { ...register('name')}
          id="name"
          type="text"
          className="form-control"
        />
      </div>
      <div className="mb-3">
        <label htmlFor="age" className="form-label">
          Age
        </label>
        <input
          { ...register('age')}
          id="age"
          type="string"
          className="form-control"
        />
      </div>
      <button className="btn btn-primary" type="submit">
        Submit
      </button>
    </form>
  );
};

export default Form;
```

这个组件使用了 `react-hook-form` 这个第三方库，这个库是用于简化和优化 React 表单管理的工具。让我分别解释一下你的组件中涉及到的关键概念：

### 1. useForm:

`useForm` 是 `react-hook-form` 提供的一个自定义钩子（hook），用于创建一个表单实例，它包含了一些表单操作所需的函数和状态。在组件中调用 `useForm` 后，会返回一个对象，其中包含了一些用于处理表单的方法。

```tsx
const { register, handleSubmit } = useForm();
```

- **register:** `register` 函数用于注册表单中的输入字段。它接受字段的名称作为参数，返回一个对象，你需要将这个对象中的属性传递给表单的相应输入元素。

- **handleSubmit:** `handleSubmit` 函数用于处理表单的提交。它接受一个回调函数作为参数，回调函数会在表单提交时执行，并接收表单中的数据作为参数。

### 2. 使用 `register` 注册输入字段：

在你的组件中，通过 `register` 函数注册了两个输入字段（name 和 age）：

```tsx
<input
  { ...register('name')}  // 注册名为 'name' 的输入字段
  id="name"
  type="text"
  className="form-control"
/>
```

```tsx
<input
  { ...register('age')}  // 注册名为 'age' 的输入字段
  id="age"
  type="string"
  className="form-control"
/>
```

- `{ ...register('name')}` 和 `{ ...register('age')}`: 这里使用了扩展运算符（spread operator）将 `register('name')` 和 `register('age')` 的返回对象的属性扩展到对应的 `input` 元素中。这样，`react-hook-form` 就能够跟踪和管理这两个输入字段的状态和值。

### 3. 使用 `handleSubmit` 处理表单提交：

```tsx
<form onSubmit={handleSubmit(data => console.log(data))}>
  {/* ... */}
</form>
```

- `onSubmit` 属性接收了一个回调函数，该函数在表单提交时被触发。这里使用了 `console.log(data)` 打印出表单的数据。

### 总结：

`react-hook-form` 简化了表单管理的流程，通过提供这些钩子和函数，你可以更轻松地注册表单字段、处理表单提交，而不必过多地关注底层的状态管理。这样能够帮助你编写更简洁、可维护的表单代码。



## 六.应用验证规则

```react
import { FieldValues, useForm } from "react-hook-form";

interface FormData {
  name: string;
  age: number;
}//这里的接口是为了让typescript知道我们在这里要用的属性

const Form = () => {
  const {
    register,
    handleSubmit,
    formState: { errors }, //调用这个errors提示对象
  } = useForm<FormData>();

  const onSubmit = (data: FieldValues) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div className="mb-3">
        <label htmlFor="name" className="form-label">
          Name
        </label>
        <input
          {...register("name", { required: true, minLength: 3 })}//提出想要的规则
          id="name"
          type="text"
          className="form-control"
        />
        {errors.name?.type === "required" && (
          <p className="text-danger">姓名是必填项</p>
        )}
        {errors.name?.type === "minLength" && (
          <p className="text-danger">名字至少要有三个字符</p>
        )} // input元素后面提出错误
      </div>
      <div className="mb-3">
        <label htmlFor="age" className="form-label">
          Age
        </label>
        <input
          {...register("age")}
          id="age"
          type="string"
          className="form-control"
        />
      </div>
      <button className="btn btn-primary" type="submit">
        Submit
      </button>
    </form>
  );
};

export default Form;

```



## 七.使用 ZOD 进行基于模式的验证

查看zod网页

```
zod.dev
```

下载第三方包

```
npm i zod@3.20.6
```

这个库包括各种基于模式的验证库的解析器

```
npm i @hookform/resolvers@2.9.11 
```



```react
import { FieldValues, useForm } from "react-hook-form";
import {z} from 'zod'; //使用z可以定义表单的形状或方案及其所有验证规则
import { zodResolver} from '@hookform/resolvers/zod';

const schema = z.object({
  name: z.string().min(3,{message:'姓名至少需要3个字符'}),
  age: z.number({ invalid_type_error:'年龄是必填项'}).min(18,{message:'年龄至少18岁'})
}); //为表单定义一个模式来验证用户输入

type FormData = z.infer<typeof schema>;  //变相的定义接口

const Form = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<FormData>({ resolver : zodResolver(schema) });

  const onSubmit = (data: FieldValues) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div className="mb-3">
        <label htmlFor="name" className="form-label">
          Name
        </label>
        <input
          {...register("name", { required: true })}
          id="name"
          type="text"
          className="form-control"
        />
        {errors.name && (
          <p className="text-danger">{errors.name.message}</p>
        )}
      </div>
      <div className="mb-3">
        <label htmlFor="age" className="form-label">
          Age
        </label>
        <input
          {...register("age", {valueAsNumber:true})}
          id="age"
          type="number"
          className="form-control"
        />
        {errors.age && (
          <p className="text-danger">{errors.age.message}</p>
        )}
      </div>
      <button className="btn btn-primary" type="submit">
        Submit
      </button>
    </form>
  );
};

export default Form;
```

这段代码使用了 `react-hook-form` 库和 `zod` 库，通过 `zodResolver` 实现了基于 Zod schema 的表单验证。下面是对代码的解释：

### 1. 引入依赖库：

```tsx
import { FieldValues, useForm } from "react-hook-form";
import { z } from 'zod';
import { zodResolver } from '@hookform/resolvers/zod';
```

- `react-hook-form`：用于表单管理的 React 库。
- `zod`：用于定义数据模型和进行数据验证的库。
- `@hookform/resolvers/zod`：提供了与 Zod 集成的解析器，用于将 Zod schema 与 `react-hook-form` 集成。

### 2. 定义 Zod Schema：

```tsx
const schema = z.object({
  name: z.string().min(3, { message: '姓名至少需要3个字符' }),
  age: z.number({ invalid_type_error: '年龄是必填项' }).min(18, { message: '年龄至少18岁' })
});
```

- `z.object`：定义了一个对象类型的 Zod schema。
- `z.string().min(3, { message: '姓名至少需要3个字符' })`：定义了 `name` 字段，是一个字符串，至少需要 3 个字符。
- `z.number({ invalid_type_error: '年龄是必填项' }).min(18, { message: '年龄至少18岁' })`：定义了 `age` 字段，是一个数字，至少需要是 18。

### 3. 定义表单数据类型：

```tsx
type FormData = z.infer<typeof schema>;
```

- `z.infer<typeof schema>`：根据 Zod schema 推断出的表单数据类型。

### 4. 使用 useForm 创建表单：

```tsx
const {
  register,
  handleSubmit,
  formState: { errors },
} = useForm<FormData>({ resolver: zodResolver(schema) });
```

- `useForm<FormData>`：使用 `useForm` 创建一个表单实例，并指定表单数据的类型为 `FormData`。
- `{ resolver: zodResolver(schema) }`：使用 Zod schema 的解析器，将 Zod schema 与 `react-hook-form` 集成。

### 5. 表单提交处理函数：

```tsx
const onSubmit = (data: FieldValues) => console.log(data);
```

- `onSubmit` 函数：当表单提交时触发的处理函数，这里简单地打印表单数据。

### 6. 表单渲染：

```tsx
return (
  <form onSubmit={handleSubmit(onSubmit)}>
    {/* name 字段 */}
    <div className="mb-3">
      <label htmlFor="name" className="form-label">
        Name
      </label>
      <input
        {...register("name")}
        id="name"
        type="text"
        className="form-control"
      />
      {errors.name && (
        <p className="text-danger">{errors.name.message}</p>
      )}
    </div>

    {/* age 字段 */}
    <div className="mb-3">
      <label htmlFor="age" className="form-label">
        Age
      </label>
      <input
        {...register("age", { valueAsNumber: true })}
        id="age"
        type="number"
        className="form-control"
      />
      {errors.age && (
        <p className="text-danger">{errors.age.message}</p>
      )}
    </div>

    {/* 提交按钮 */}
    <button className="btn btn-primary" type="submit">
      Submit
    </button>
  </form>
);
```

- 通过 `{...register("name", { required: true, minLength: 3 })}` 将 `name` 字段注册到表单，并指定了一些验证规则，如必填 (`required: true`) 和最小长度 (`minLength: 3`)。
- 通过 `{...register("age", { valueAsNumber: true })}` 将 `age` 字段注册到表单，并指定了一个选项 `valueAsNumber: true`，表示将输入的值解析为数字。
- 使用 `{errors.name && (<p className="text-danger">{errors.name.message}</p>)} 和 {errors.age && (<p className="text-danger">{errors.age.message}</p>)} 用于在表单验证失败时显示错误信息。

这个组件通过 `zodResolver` 将 Zod schema 与 `react-hook-form` 集成，实现了对表单的验证。

## 八.禁用提交按钮

如果验证没有符合规则，就会禁用提交

```react
const Form = () => {
  const {
    register,
    handleSubmit,
    formState: { errors,isValid },//验证数据是否有效
  } = useForm<FormData>({ resolver : zodResolver(schema) });
const Form = () => {
    return(
        ......
      <button disabled={!isValid} className="btn btn-primary" type="submit">//这里如果没有效，不让提交
        Submit
      </button>
)
}
```



# 项目:费用追踪器

## 一.构建ExpenseList组件

这段代码是一个简单的 React 应用，用于展示和管理支出（expenses）。下面是对代码的详细解释：

### ExpenseList 组件：

```tsx
//ExpenseList组件
interface Expense {
  id: number;
  description: string;
  amount: number;
  category: string;
}

interface Props {
  expenses: Expense[];
  onDelete: (id: number) => void;
}

const ExpenseList = ({ expenses, onDelete }: Props) => {
    // 如果没有支出数据，返回 null
    if (expenses.length === 0) return null;

    // 渲染表格
    return (
        <table className="table table-bordered">
            <thead>
                <tr>
                    <th>Descripyion</th>
                    <th>Amount</th>
                    <th>Category</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                {/* 映射支出数据，渲染表格行 */}
                {expenses.map((expense) => (
                    <tr key={expense.id}>
                        <td>{expense.description}</td>
                        <td>{expense.amount}</td>
                        <td>{expense.category}</td>
                        <td>
                            {/* 删除按钮，点击时调用 onDelete 函数 */}
                            <button
                                className="btn btn-outline-danger"
                                onClick={() => onDelete(expense.id)}
                            >
                                Delete
                            </button>
                        </td>
                    </tr>
                ))}
            </tbody>
            <tfoot>
                <tr>
                    <td>Total</td>
                    {/* 计算总金额，并保留两位小数 */}
                    <td>${expenses.reduce((acc, expense) => expense.amount + acc , 0).toFixed(2)}</td>
                    <td></td>
                    <td></td>
                </tr>
            </tfoot>
        </table>
    );
};

export default ExpenseList;
```

- `ExpenseList` 组件接收 `expenses` 数组和 `onDelete` 函数作为属性。
- 如果 `expenses` 数组为空，返回 `null`，表示没有支出数据。
- 使用 `<table>`、`<thead>`、`<tbody>` 和 `<tfoot>` 渲染一个简单的表格。
- 使用 `map` 方法映射 `expenses` 数组，为每个支出渲染一行数据。
- 删除按钮点击时调用 `onDelete` 函数，传递对应的支出的 `id`。

### App 组件：

```tsx
// App组件
import { useState } from "react";
import ExpenseList from "./expense-tracker/ExpenseList";

function App() {
    // 初始支出数据
    const [expenses, setExpenses] = useState([
        { id: 1, description: "aaa", amount: 10, category: "Utilities" },
        { id: 2, description: "bbb", amount: 10, category: "Utilities" },
        { id: 3, description: "ccc", amount: 10, category: "Utilities" },
        { id: 4, description: "ddd", amount: 10, category: "Utilities" },
    ]);

    // 渲染 App 组件，包含 ExpenseList 子组件
    return (
        <div>
            {/* 将 expenses 数组和 onDelete 函数传递给 ExpenseList 子组件 */}
            <ExpenseList
                expenses={expenses}
                onDelete={(id) => setExpenses(expenses.filter((e) => e.id !== id))}
            />
        </div>
    );
}

export default App;
```

- `App` 组件是主组件，使用 `useState` 定义了一个 `expenses` 状态，初始值是包含四个支出对象的数组。
- 渲染 `ExpenseList` 子组件，将 `expenses` 数组和一个删除函数 `onDelete` 传递给子组件。
- 删除函数通过 `setExpenses` 更新 `expenses` 状态，通过 `filter` 过滤出不包含被删除支出的新数组。

这个应用的核心是 `ExpenseList` 组件，用于显示支出的表格，并提供删除功能。`App` 组件作为整个应用的入口，包含了 `ExpenseList` 子组件。

## 二.构建过滤器组件

这是一个 React 函数组件 `ExpenseFilter`，它接受一个 `Props` 对象作为参数，其中定义了一个属性 `onSelectCategory`，该属性是一个函数，接受一个字符串参数 `category`，并且返回 `void`（即不返回任何内容）。

```tsx
interface Props {
  onSelectCategory: (category: string) => void;
}

const ExpenseFilter = ({ onSelectCategory }: Props) => {
  return (
    <select className="form-select" onChange={(event) => onSelectCategory(event.target.value)}>
      <option value="">All category</option>
      <option value="Groceries">Groceries</option>
      <option value="Utilities">Utilities</option>
      <option value="Entertainment">Entertainment</option>
    </select>
  );
};

export default ExpenseFilter;
```

- `Props` 接口定义了这个组件的属性。在这里，只有一个属性 `onSelectCategory`，它是一个函数，接受一个字符串参数 `category`，并返回 `void`。

- `ExpenseFilter` 组件渲染了一个 `<select>` 元素，表示一个下拉列表框。

- `className="form-select"`：这是一个 CSS 类，通常用于设置下拉列表框的样式，可能是来自某个样式库或者你自定义的样式。

- `onChange={(event) => onSelectCategory(event.target.value)}`：这是当用户选择下拉列表中的选项时触发的事件。当发生改变时，调用 `onSelectCategory` 函数，将选中的值 `event.target.value` 作为参数传递给该函数。

- 下拉列表中有四个 `<option>` 元素，分别代表不同的支出类别。第一个选项是 "All category"，其他三个是具体的支出类别，例如 "Groceries"、"Utilities"、"Entertainment"。

总体而言，这个组件的目的是提供一个支出类别的选择框，并且当用户选择某个类别时，调用 `onSelectCategory` 函数，将选中的类别作为参数传递给父组件或处理函数。

```tsx
//App组件
import { useState } from "react";
import ExpenseList from "./expense-tracker/components/ExpenseList";
import ExpenseFilter from "./expense-tracker/components/ExpenseFilter";
import ExpenseForm from "./expense-tracker/components/ExpenseForm";

export const categories = ["Groceries","Utilities","Entertainment"]

function App() {
  const [selectCategory, setSelectCategory] = useState("");

  const [expenses, setExpenses] = useState([
    { id: 1, description: "aaa", amount: 10, category: "Utilities" },
    { id: 2, description: "bbb", amount: 10, category: "Utilities" },
    { id: 3, description: "ccc", amount: 10, category: "Utilities" },
    { id: 4, description: "ddd", amount: 10, category: "Utilities" },
  ]);

  const visibleExpenses = selectCategory
    ? expenses.filter((e) => e.category === selectCategory)
    : expenses;

  return (
    <div>
      <div className="mb-5">
        <ExpenseForm/>
      </div>
      <div className="mb-3">
        <ExpenseFilter
          onSelectCategory={(category) => setSelectCategory(category)}
        />
      </div>
      <ExpenseList
        expenses={visibleExpenses}
        onDelete={(id) => setExpenses(expenses.filter((e) => e.id !== id))}
      />
    </div>
  );
}

export default App;

```

## 三.构建ExpenseForm组件

```tsx
//ExpenseForm组件
import React from "react";
import { categories } from "../../App";

const ExpenseForm = () => {
  return (
    <form>
      <div className="mb-3">
        <label htmlFor="description" className="form-label">
          Description
        </label>
        <input id="description" type="text" className="form-control" />
      </div>
      <div className="mb-3">
        <label htmlFor="amount" className="form-label">
          Amount
        </label>
        <input id="amount" type="number" className="form-control" />
      </div>
      <div className="mb-3">
        <label htmlFor="category" className="form-label">Category</label>
        <select name="" id="category" className="form-select">
            <option value=""></option>
            {categories.map(category => <option key={category} value={category}>{category}</option>)}
        </select>
      </div>
      <button className="btn btn-primary">Submit</button>
    </form>
  );
};

export default ExpenseForm;

```

```tsx
//App组件
import { useState } from "react";
import ExpenseList from "./expense-tracker/components/ExpenseList";
import ExpenseFilter from "./expense-tracker/components/ExpenseFilter";
import ExpenseForm from "./expense-tracker/components/ExpenseForm";

export const categories = ["Groceries","Utilities","Entertainment"]

function App() {
  const [selectCategory, setSelectCategory] = useState("");

  const [expenses, setExpenses] = useState([
    { id: 1, description: "aaa", amount: 10, category: "Utilities" },
    { id: 2, description: "bbb", amount: 10, category: "Utilities" },
    { id: 3, description: "ccc", amount: 10, category: "Utilities" },
    { id: 4, description: "ddd", amount: 10, category: "Utilities" },
  ]);

  const visibleExpenses = selectCategory
    ? expenses.filter((e) => e.category === selectCategory)
    : expenses;

  return (
    <div>
      <div className="mb-5">
        <ExpenseForm/>
      </div>
      <div className="mb-3">
        <ExpenseFilter
          onSelectCategory={(category) => setSelectCategory(category)}
        />
      </div>
      <ExpenseList
        expenses={visibleExpenses}
        onDelete={(id) => setExpenses(expenses.filter((e) => e.id !== id))}
      />
    </div>
  );
}

export default App;

```

## 四.使用第三方包做验证

```tsx
//ExpenseForm组件
import { z } from "zod";
import categories from "../categories";
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";

const schema = z.object({
  description: z.string().min(3 ,{message:'至少需要3个字符'}).max(50),
  amount: z.number({invalid_type_error:'这是必填项'}).min(0.01).max(100_000),
  category: z.enum(categories,{
    errorMap : () =>({
        message: '必填项，不能为空!'
    })
  }),
});

type ExpenseFormData = z.infer<typeof schema>;

const ExpenseForm = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<ExpenseFormData>({ resolver: zodResolver(schema) });

  return (
    <form onSubmit={handleSubmit((data) => console.log(data))}>
      <div className="mb-3">
        <label htmlFor="description" className="form-label">
          Description
        </label>
        <input
          {...register("description")}
          id="description"
          type="text"
          className="form-control"
        />
        {errors.description && (
          <p className="text-danger">{errors.description.message}</p>
        )}
      </div>
      <div className="mb-3">
        <label htmlFor="amount" className="form-label">
          Amount
        </label>
        <input
          {...register("amount" , { valueAsNumber: true })}
          id="amount"
          type="number"
          className="form-control"
        />
        {errors.amount && (
          <p className="text-danger">{errors.amount.message}</p>
        )}
      </div>
      <div className="mb-3">
        <label htmlFor="category" className="form-label">
          Category
        </label>
        <select {...register("category")} id="category" className="form-select">
          <option value=""></option>
          {categories.map((category) => (
            <option key={category} value={category}>
              {category}
            </option>
          ))}
        </select>
        {errors.category && (
          <p className="text-danger">{errors.category.message}</p>
        )}
      </div>
      <button className="btn btn-primary">Submit</button>
    </form>
  );
};

export default ExpenseForm;

```

```tsx
//App组件
import { useState } from "react";
import ExpenseList from "./expense-tracker/components/ExpenseList";
import ExpenseFilter from "./expense-tracker/components/ExpenseFilter";
import ExpenseForm from "./expense-tracker/components/ExpenseForm";
import categories from "./expense-tracker/categories";

function App() {
  const [selectCategory, setSelectCategory] = useState("");

  const [expenses, setExpenses] = useState([
    { id: 1, description: "aaa", amount: 10, category: "Utilities" },
    { id: 2, description: "bbb", amount: 10, category: "Utilities" },
    { id: 3, description: "ccc", amount: 10, category: "Utilities" },
    { id: 4, description: "ddd", amount: 10, category: "Utilities" },
  ]);

  const visibleExpenses = selectCategory
    ? expenses.filter((e) => e.category === selectCategory)
    : expenses;

  return (
    <div>
      <div className="mb-5">
        <ExpenseForm/>
      </div>
      <div className="mb-3">
        <ExpenseFilter
          onSelectCategory={(category) => setSelectCategory(category)}
        />
      </div>
      <ExpenseList
        expenses={visibleExpenses}
        onDelete={(id) => setExpenses(expenses.filter((e) => e.id !== id))}
      />
    </div>
  );
}

export default App;
```

## 五.添加Expense

```tsx
import { z } from "zod";
import categories from "../categories";
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";

const schema = z.object({
  description: z.string().min(3 ,{message:'至少需要3个字符'}).max(50),
  amount: z.number({invalid_type_error:'这是必填项'}).min(0.01).max(100_000),
  category: z.enum(categories,{
    errorMap : () =>({
        message: '必填项，不能为空!'
    })
  }),
});

type ExpenseFormData = z.infer<typeof schema>;


interface Props {
    onSubmit: (data:ExpenseFormData) => void;
}

const ExpenseForm = ({ onSubmit} : Props) => {
  const {
    register,
    handleSubmit,
    reset, //添加一个reset
    formState: { errors },
  } = useForm<ExpenseFormData>({ resolver: zodResolver(schema) });

  return (
    <form onSubmit={handleSubmit(data =>{
        onSubmit(data);
        reset();
    })}>
      <div className="mb-3">
        <label htmlFor="description" className="form-label">
          Description
        </label>
        <input
          {...register("description")}
          id="description"
          type="text"
          className="form-control"
        />
        {errors.description && (
          <p className="text-danger">{errors.description.message}</p>
        )}
      </div>
      <div className="mb-3">
        <label htmlFor="amount" className="form-label">
          Amount
        </label>
        <input
          {...register("amount" , { valueAsNumber: true })}
          id="amount"
          type="number"
          className="form-control"
        />
        {errors.amount && (
          <p className="text-danger">{errors.amount.message}</p>
        )}
      </div>
      <div className="mb-3">
        <label htmlFor="category" className="form-label">
          Category
        </label>
        <select {...register("category")} id="category" className="form-select">
          <option value=""></option>
          {categories.map((category) => (
            <option key={category} value={category}>
              {category}
            </option>
          ))}
        </select>
        {errors.category && (
          <p className="text-danger">{errors.category.message}</p>
        )}
      </div>
      <button className="btn btn-primary">Submit</button>
    </form>
  );
};

export default ExpenseForm;

```

**App组件**

```jsx
import { useState } from "react";
import ExpenseList from "./expense-tracker/components/ExpenseList";
import ExpenseFilter from "./expense-tracker/components/ExpenseFilter";
import ExpenseForm from "./expense-tracker/components/ExpenseForm";
import categories from "./expense-tracker/categories";

function App() {
  const [selectCategory, setSelectCategory] = useState("");

  const [expenses, setExpenses] = useState([
    { id: 1, description: "aaa", amount: 10, category: "Utilities" },
    { id: 2, description: "bbb", amount: 10, category: "Utilities" },
    { id: 3, description: "ccc", amount: 10, category: "Utilities" },
    { id: 4, description: "ddd", amount: 10, category: "Utilities" },
  ]);

  const visibleExpenses = selectCategory
    ? expenses.filter((e) => e.category === selectCategory)
    : expenses;

  return (
    <div>
      <div className="mb-5">
        <ExpenseForm onSubmit={expense => setExpenses([...expenses, { ...expense, id: expenses.length + 1}])}/>
      </div>
      <div className="mb-3">
        <ExpenseFilter
          onSelectCategory={(category) => setSelectCategory(category)}
        />
      </div>
      <ExpenseList
        expenses={visibleExpenses}
        onDelete={(id) => setExpenses(expenses.filter((e) => e.id !== id))}
      />
    </div>
  );
}

export default App;
```





# 连接后端

## 一.Effect钩子

`useEffect` 是 React 中的一个 Hooks，用于在函数组件中执行副作用操作。副作用操作通常包括订阅数据、手动操作 DOM、网络请求、设置定时器等。`useEffect` 的设计目的是为了在组件渲染完成后执行这些副作用。

基本语法如下：

```tsx
import { useEffect } from 'react';

function MyComponent() {
  useEffect(() => {
    // 副作用操作
    console.log('Effect executed');

    // 返回一个清理函数，可选
    return () => {
      // 在组件卸载时执行
      console.log('Effect cleanup');
    };
  }, []); // 依赖项为空数组，表示只在组件挂载和卸载时执行

  return (
    // 组件的 JSX 渲染部分
  );
}

```

### 实例

```tsx
import { useEffect, useRef } from "react";



function App() {
  const ref = useRef<HTMLInputElement>(null);
  
  useEffect(() =>{
    if (ref.current) ref.current.focus();
  });

  useEffect(() => {
    document.title = 'My App';
  })
  

  return (    
    <div>
      <input ref={ref} type="text" className="form-control" />
    </div>
  );
}

export default App;

```

 观察组件行为

观察组件的行为也是一种判断是否存在副作用的方法。如果组件在渲染时执行了一些不是纯粹 UI 相关的操作，那么很可能存在副作用。

### 总结

使用 `useEffect` 是判断 React 组件中是否存在副作用最直接的方法。如果你发现在组件中有类似数据获取、订阅、手动 DOM 操作等副作用，那么就应该考虑使用 `useEffect` 进行管理。

## 二.Effect依赖

在 React 中，`useEffect` Hook 中的依赖数组是一个重要的概念。这个数组指定了哪些值的变化会触发 `useEffect` 中的副作用执行。它是一个可选参数，如果省略，`useEffect` 的副作用将在每次组件渲染后都执行。

```jsx
useEffect(() => {
  // 副作用操作
  console.log('Effect executed');

  // 返回一个清理函数，可选
  return () => {
    // 在组件卸载或下一次 effect 执行前执行
    console.log('Effect cleanup');
  };
}, [/* dependencies */]);
```

### 为什么使用依赖数组？

1. **性能优化：** 如果没有依赖数组，每次组件渲染都会触发 `useEffect` 中的副作用。通过指定依赖数组，可以只在依赖项发生变化时才执行副作用，从而优化性能。

2. **避免无限循环：** 如果没有指定依赖项，且在 `useEffect` 中修改了组件状态，可能会导致无限循环，因为状态的更新又会触发组件重新渲染，再次执行 `useEffect`。通过指定依赖项，可以明确哪些状态会影响 `useEffect` 的执行。

### 依赖项的选取

- **空数组 (`[]`):** 表示 `useEffect` 中的副作用只在组件挂载和卸载时执行，类似于类组件中的 `componentDidMount` 和 `componentWillUnmount`。

- **有依赖项的数组:** `useEffect` 会在依赖项发生变化时执行。如果依赖项数组中的任何一个值发生变化，就会触发 `useEffect` 中的副作用。注意：依赖项发生变化时，`useEffect` 会在渲染后执行。

### 注意事项

- **避免不必要的依赖项:** 只添加确实会影响副作用的状态或变量，避免不必要的重新执行。

- **函数和对象:** 如果依赖项是一个函数或对象，每次渲染都会被认为是不同的对象。如果不希望在每次渲染时触发 `useEffect`，可以使用 `useMemo` 或 `useCallback`。

- **异步操作:** `useEffect` 中的函数是异步执行的，不会阻塞浏览器渲染。

```jsx
useEffect(() => {
  // 异步操作
  const fetchData = async () => {
    const result = await fetchDataAsync();
    // ...
  };

  fetchData();
}, [/* dependencies */]);
```

综上所述，`useEffect` 的依赖项是一个用于控制副作用触发的重要机制，合理的依赖项选择可以优化性能和确保副作用的正确执行。

### 实例

**ProductList组件**

```tsx
import React, { useEffect, useState } from 'react'

const ProductList = ({category} : {category:string}) => {
  const [product, setProduct] = useState<string[]>([]) 

  useEffect(() =>{
    console.log('Fetching products in', category );
    setProduct(['Clothing','Household']);
  },[category])

  return (
    <div>ProductList</div>
  )
}

export default ProductList
```

**App组件**

```tsx
import { useState } from "react";
import ProductList from "./components/ProductList";



function App() {
  const [category,setCategory] =useState('');


  return (    
    <div>
      <select className="form-select" onChange={(event) => setCategory(event.target.value)}>
        <option value=""></option>
        <option value="Clothing">Clothing</option>
        <option value="Household">Household</option>
      </select>
      <ProductList category={category}/>
    </div>
  );
}

export default App;

```

**在Effect钩子中**

**1.如果传递的是一个空数组，只渲染一次**

**2.没有传递数组，会一直渲染(前提是Effect钩子中有更新状态的钩子，它们后面会一直更新一直渲染)**

**3.传递对应变量，根据该变量改变进行渲染**



## 三.Effect 清理函数

在 React 中，`useEffect` Hook 不仅可以用于执行副作用操作，还可以返回一个清理函数。这个清理函数会在组件卸载时执行，或者在下一次 `useEffect` 执行前执行（如果依赖项发生了变化）。

```jsx
useEffect(() => {
  // 副作用操作
  console.log('Effect executed');

  // 返回一个清理函数，可选
  return () => {
    console.log('Effect cleanup');
    // 在组件卸载或下一次 effect 执行前执行
  };
}, [/* dependencies */]);
```

### 为什么需要清理函数？

1. **资源释放：** 在副作用中可能创建了一些资源，比如订阅、定时器、网络请求等。为了防止内存泄漏和不必要的资源占用，可以在清理函数中释放这些资源。

2. **取消订阅：** 如果在副作用中订阅了某个事件或数据源，需要在组件卸载或下一次副作用执行前取消订阅，以防止后续的事件仍然影响已经卸载的组件。

### 例子：

```jsx
useEffect(() => {
  const subscription = subscribeToSomeEvent();

  return () => {
    // 清理函数中取消订阅
    subscription.unsubscribe();
  };
}, [/* dependencies */]);
```

### 清理函数执行时机

1. **组件卸载时：** 如果 `useEffect` 中的依赖项为空数组，清理函数会在组件卸载时执行。

2. **下一次 `useEffect` 执行前：** 如果 `useEffect` 中有依赖项，清理函数会在下一次 `useEffect` 执行前执行。这包括组件重新渲染时，且依赖项发生变化。

### 注意事项

- **清理函数执行顺序：** 如果组件中有多个 `useEffect`，清理函数的执行顺序与它们声明的顺序相反。

```jsx
useEffect(() => {
  // Effect 1
  return () => {
    // Cleanup 1
  };
}, [/* dependencies */]);

useEffect(() => {
  // Effect 2
  return () => {
    // Cleanup 2
  };
}, [/* dependencies */]);
```

- **清理函数不会阻止渲染：** 即使清理函数还未执行完，React 也会继续渲染组件。

- **清理函数依赖项：** 如果清理函数中使用了依赖项，确保在依赖项数组中包含这些值，以便在依赖项发生变化时执行清理操作。

```jsx
useEffect(() => {
  const intervalId = setInterval(() => {
    // ...
  }, 1000);

  return () => {
    // 清理函数中使用了 intervalId，确保依赖项中包含它
    clearInterval(intervalId);
  };
}, [/* dependencies */]);
```

综上所述，`useEffect` 清理函数是用于在组件卸载或下一次 `useEffect` 执行前执行一些清理操作的机制。这有助于确保组件生命周期内的资源管理和避免潜在的问题。

## 四.获取数据

这里的链接有各种端点来获取虚拟数据

```http
https://jsonplaceholder.typicode.com/
```

**下载第三方包**

```
npm i axios@1.3.4
```

`axios` 是一个基于 Promise 的 HTTP 客户端，用于浏览器和 Node.js。它使得在浏览器端和服务器端进行 HTTP 请求变得更加简单和一致。通过使用 `axios`，你可以轻松地发送异步 HTTP 请求，并处理响应数据。

在前端开发中，常常需要从服务器获取数据或向服务器发送数据。`axios` 提供了一种简单而强大的方式来执行这些操作。下面是一些 `axios` 的主要特点和用途：

1. **简单易用：** `axios` 的 API 设计简单且易于理解，使得发起 HTTP 请求变得直观和方便。

2. **Promise 风格：** `axios` 使用 Promise 风格的 API，支持链式调用，使得异步操作的处理更加清晰。

3. **支持浏览器和 Node.js：** `axios` 可以在浏览器和 Node.js 环境中使用，使得前后端通用。

4. **拦截器：** `axios` 提供了请求和响应的拦截器，可以在请求和响应被发送或接收之前进行一些预处理或后处理的操作。

5. **取消请求：** `axios` 允许取消请求，防止不必要的请求发出。

以下是一个简单的使用 `axios` 发送 GET 请求的示例：

```jsx
import axios from 'axios';

// 发送 GET 请求
axios.get('https://api.example.com/data')
  .then(response => {
    console.log('Data:', response.data);
  })
  .catch(error => {
    console.error('Error fetching data:', error);
  });
```

在这个示例中，我们使用 `axios.get` 方法发送一个 GET 请求，并在成功时打印响应的数据，失败时打印错误信息。

### 实例

```tsx
import { useEffect, useState } from "react"; 
import axios from "axios";

interface User{
  id:number;
  name: string;
}


function App() {
  const [users, setUsers] =useState<User[]>([]);

  useEffect(() => {
    axios.get<User[]>('https://jsonplaceholder.typicode.com/users')
      .then(res => setUsers(res.data)); 
  },[])

  return (    
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
}

export default App;

```

## 五.设置错误

```tsx
import { useEffect, useState } from "react"; 
import axios from "axios";

interface User{
  id:number;
  name: string;
}


function App() {
  const [users, setUsers] =useState<User[]>([]);
  const [error , setError] = useState('')

  useEffect(() => {
    axios.get<User[]>('https://jsonplaceholder.typicode.com/vusers') //故意写错,触发错误提示
      .then(res => setUsers(res.data))
      .catch((error) => setError(error.message)); 
  },[])

  return (    
    <>
    <p className="text-danger">{error}</p>
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
    </>
  );
}

export default App;

```

## 六.清理函数

当用户浏览某个网页但是请求还没到位时用户删除了该网页，这个时候我们不需要去请求了，需要使用清理函数来取消掉

这里使用的是**axios的清理函数**

```tsx
import { useEffect, useState } from "react"; 
import axios, { CanceledError } from "axios";

interface User{
  id:number;
  name: string;
}


function App() {
  const [users, setUsers] =useState<User[]>([]);
  const [error , setError] = useState('')

  useEffect(() => {
    const controller = new AbortController()

    axios.get<User[]>('https://jsonplaceholder.typicode.com/users', {signal:controller.signal})
      .then(res => setUsers(res.data))
      .catch((error) => {
        if (error instanceof CanceledError) return;
        setError(error.message)}); 
    
    return () => controller.abort();
  },[])

  return (    
    <>
    <p className="text-danger">{error}</p>
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
    </>
  );
}

export default App;

```

在你的代码中，`{signal: controller.signal}` 是用来传递一个终止信号（AbortSignal）给 Axios 请求的配置项。这是与 [AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController) 一起使用的一种技术，用于在需要时取消（中止）正在进行的网络请求。

具体来说，这里的作用是：

1. **AbortController 创建：** 通过 `const controller = new AbortController()` 创建了一个新的 `AbortController` 实例，该实例包含一个 `signal` 属性，表示一个 `AbortSignal` 对象。

2. **传递终止信号给 Axios 请求：** 通过 `{signal: controller.signal}` 将 `AbortSignal` 对象传递给 Axios 请求的配置项中。这告诉 Axios 在请求过程中使用指定的终止信号。

3. **取消请求时中止（Abort）：** 在组件卸载或其他需要取消请求的情况下，通过 `controller.abort()` 调用 `AbortController` 的 `abort` 方法，将终止信号发送给 Axios 请求，导致请求被取消。

这种做法是为了避免在组件已经卸载或不再需要请求结果的情况下，仍然持续发送不必要的请求。使用 `AbortController` 可以有效地中止正在进行的请求，提高应用程序的性能和资源利用率。

需要注意的是，`CanceledError` 是 Axios 提供的一个特定错误类型，用于捕获由于请求被取消而引发的错误。在 `catch` 块中，你检查 `error` 是否是 `CanceledError` 类型，如果是，就不处理该错误，以避免在请求被取消时触发不必要的错误处理逻辑。





## 七.显示加载指示器

```tsx
import { useEffect, useState } from "react";
import axios, { CanceledError } from "axios";

interface User {
  id: number;
  name: string;
}

function App() {
  const [users, setUsers] = useState<User[]>([]);
  const [error, setError] = useState("");
  const [isLoading, setLoading] = useState(false);

  useEffect(() => {
    const controller = new AbortController();
    setLoading(true);

    axios
      .get<User[]>("https://jsonplaceholder.typicode.com/users", {
        signal: controller.signal,
      })
      .then((res) => {
        setUsers(res.data); //使用 .then() 方法来处理请求成功的响应.
                          // 在 .then() 的回调函数中，res.data 包含了服务器返回的新用户对象。
        setLoading(false); 
      })
      .catch((error) => {
        if (error instanceof CanceledError) return; 
        {
          setError(error.message);
          setLoading(false);
        }
      });

    return () => controller.abort();
  },[]);

  return (
    <>
      {error && <p className="text-danger">{error}</p>}
      {isLoading && <div className="spinner-border"></div>}
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </>
  );
}

export default App;

```



## 八.删除数据

建立一个按钮，当点击按钮时该数据被删除(先渲染，再储存给服务器)

```tsx
import { useEffect, useState } from "react";
import axios, { CanceledError } from "axios";

interface User {
  id: number;
  name: string;
}

function App() {
  const [users, setUsers] = useState<User[]>([]);
  const [error, setError] = useState("");
  const [isLoading, setLoading] = useState(false);

  useEffect(() => {
    const controller = new AbortController();
    setLoading(true);

    axios
      .get<User[]>("https://jsonplaceholder.typicode.com/users", {
        signal: controller.signal,
      })
      .then((res) => {
        setUsers(res.data);
        setLoading(false);
      })
      .catch((error) => {
        if (error instanceof CanceledError) return;
        {
          setError(error.message);
          setLoading(false);
        }
      });

    return () => controller.abort();
  }, []);

  const deleteUser = (user: User) =>{
    const originalUser = [...users];
    setUsers(users.filter(u => u.id !==user.id ));//过滤掉需要过滤的用户

    axios.delete("https://jsonplaceholder.typicode.com/users/" + user.id)
    .catch(error =>{
      setError(error.message);
      setUsers(originalUser);//如果出现错误，会返回之前的数据
    })
  }

  return (
    <>
      {error && <p className="text-danger">{error}</p>}
      {isLoading && <div className="spinner-border"></div>}
      <ul className="list-group">
        {users.map((user) => (
          <li key={user.id} className="list-group-item d-flex justify-content-between">
            {user.name}
            <button 
                className="btn btn-outline-danger" 
                onClick={() => deleteUser(user)}>Delete</button> //建立按钮，添加css样式,添加点击事件
          </li>
        ))}
      </ul>
    </>
  );
}

export default App;
```



## 九.创建数据

通过按钮点击来创建一个对象.

```tsx
import { useEffect, useState } from "react";
import axios, { CanceledError } from "axios";

interface User {
  id: number;
  name: string;
}

function App() {
  const [users, setUsers] = useState<User[]>([]);
  const [error, setError] = useState("");
  const [isLoading, setLoading] = useState(false);

  useEffect(() => {
    const controller = new AbortController();
    setLoading(true);

    axios
      .get<User[]>("https://jsonplaceholder.typicode.com/users", {
        signal: controller.signal,
      })
      .then((res) => {
        setUsers(res.data);
        setLoading(false);
      })
      .catch((error) => {
        if (error instanceof CanceledError) return;
        {
          setError(error.message);
          setLoading(false);
        }
      });

    return () => controller.abort();
  }, []);

  const deleteUser = (user: User) =>{
    const originalUser = [...users];
    setUsers(users.filter(u => u.id !==user.id ));

    axios.delete("https://jsonplaceholder.typicode.com/users/" + user.id)
    .catch(error =>{
      setError(error.message);
      setUsers(originalUser);
    })
  }

  const addUser = () =>{
    const originalUser = [...users];
    const newUser = { id: 0, name: 'Mosh'};
    setUsers([newUser,...users]);

    axios.post('https://jsonplaceholder.typicode.com/users', newUser)
    .catch(error => {
      setError(error.message);
      setUsers(originalUser);
    })
    

  }

  return (
    <>
      {error && <p className="text-danger">{error}</p>}
      {isLoading && <div className="spinner-border"></div>}
      <button className="btn btn-primary mb-3" onClick={(addUser)}>Add</button>
      <ul className="list-group">
        {users.map((user) => (
          <li key={user.id} className="list-group-item d-flex justify-content-between">
            {user.name}
            <button className="btn btn-outline-danger" onClick={() => deleteUser(user)}>Delete</button>
          </li>
        ))}
      </ul>
    </>
  );
}

export default App;

```



## 十.更新数据

为每一个对象添加修改键，点击可以为名字后面加个 ！号

```tsx
import { useEffect, useState } from "react";
import axios, { CanceledError } from "axios";

interface User {
  id: number;
  name: string;
}

function App() {
  const [users, setUsers] = useState<User[]>([]);
  const [error, setError] = useState("");
  const [isLoading, setLoading] = useState(false);

  useEffect(() => {
    const controller = new AbortController();
    setLoading(true);

    axios
      .get<User[]>("https://jsonplaceholder.typicode.com/users", {
        signal: controller.signal,
      })
      .then((res) => {
        setUsers(res.data);
        setLoading(false);
      })
      .catch((error) => {
        if (error instanceof CanceledError) return;
        {
          setError(error.message);
          setLoading(false);
        }
      });

    return () => controller.abort();
  }, []);

  const deleteUser = (user: User) =>{
    const originalUser = [...users];
    setUsers(users.filter(u => u.id !==user.id ));

    axios.delete("https://jsonplaceholder.typicode.com/users/" + user.id)
    .catch(error =>{
      setError(error.message);
      setUsers(originalUser);
    })
  }

  const addUser = () =>{
    const originalUser = [...users];
    const newUser = { id: 0, name: 'Mosh'};
    setUsers([newUser,...users]);

    axios.post('https://jsonplaceholder.typicode.com/users', newUser)
    .catch(error => {
      setError(error.message);
      setUsers(originalUser);
    })
  }

  const updateUser = (user:User) =>{
    const updateUser = { ...user, name: user.name+'!'};
    setUsers(users.map(u => u.id === user.id ? updateUser : u));

    axios.patch('https://jsonplaceholder.typicode.com/users' + user.id, updateUser)
      .catch(error =>{
        const originalUser = [...users];
        setError(error.message);
        setUsers(originalUser);
      })
  }

  return (
    <>
      {error && <p className="text-danger">{error}</p>}
      {isLoading && <div className="spinner-border"></div>}
      <button className="btn btn-primary mb-3" onClick={(addUser)}>Add</button>
      <ul className="list-group">
        {users.map((user) => (
          <li key={user.id} className="list-group-item d-flex justify-content-between">
            {user.name}
            <div>
            <button className="btn btn-outline-secondary mx-1" onClick={() => updateUser(user)}>Update</button>
            <button className="btn btn-outline-danger" onClick={() => deleteUser(user)}>Delete</button>
            </div>
            
          </li>
        ))}
      </ul>
    </>
  );
}

export default App;
```

## 十一.提取可重用的 api 客户端

### 实例

```tsx
import axios,{CanceledError}from "axios";

export default axios.create({
    baseURL: 'https://jsonplaceholder.typicode.com'
})

export { CanceledError };
```

到组件中去导入

```tsx
import { useEffect, useState } from "react";
import apiClient, { CanceledError } from "./services/api-client";

interface User {
  id: number;
  name: string;
}

function App() {
  const [users, setUsers] = useState<User[]>([]);
  const [error, setError] = useState("");
  const [isLoading, setLoading] = useState(false);

  useEffect(() => {
    const controller = new AbortController();
    setLoading(true);

    apiClient
      .get<User[]>("/users", {
        signal: controller.signal,
      })
      .then((res) => {
        setUsers(res.data);
        setLoading(false);
      })
      .catch((error) => {
        if (error instanceof CanceledError) return;
        {
          setError(error.message);
          setLoading(false);
        }
      });

    return () => controller.abort();
  }, []);

  const deleteUser = (user: User) => {
    const originalUser = [...users];
    setUsers(users.filter((u) => u.id !== user.id));

    apiClient.delete("/users/" + user.id).catch((error) => {
      setError(error.message);
      setUsers(originalUser);
    });
  };

  const addUser = () => {
    const originalUser = [...users];
    const newUser = { id: 0, name: "Mosh" };
    setUsers([newUser, ...users]);

    apiClient.post("/users", newUser).catch((error) => {
      setError(error.message);
      setUsers(originalUser);
    });
  };

  const updateUser = (user: User) => {
    const updateUser = { ...user, name: user.name + "!" };
    setUsers(users.map((u) => (u.id === user.id ? updateUser : u)));

    apiClient.patch("/users" + user.id, updateUser).catch((error) => {
      const originalUser = [...users];
      setError(error.message);
      setUsers(originalUser);
    });
  };

  return (
    <>
      {error && <p className="text-danger">{error}</p>}
      {isLoading && <div className="spinner-border"></div>}
      <button className="btn btn-primary mb-3" onClick={addUser}>
        Add
      </button>
      <ul className="list-group">
        {users.map((user) => (
          <li
            key={user.id}
            className="list-group-item d-flex justify-content-between"
          >
            {user.name}
            <div>
              <button
                className="btn btn-outline-secondary mx-1"
                onClick={() => updateUser(user)}
              >
                Update
              </button>
              <button
                className="btn btn-outline-danger"
                onClick={() => deleteUser(user)}
              >
                Delete
              </button>
            </div>
          </li>
        ))}
      </ul>
    </>
  );
}

export default App;
```



`axios.create` 是 Axios 库提供的一个用于创建自定义配置的工厂函数。它允许你创建一个新的 Axios 实例，该实例具有自定义的默认配置，例如基础URL、默认请求头、拦截器等。通过创建实例，你可以在应用中的不同部分使用不同的配置，同时共享一些全局配置。

以下是 `axios.create` 的基本用法：

```javascript
import axios from 'axios';

// 创建一个自定义配置的 Axios 实例
const apiClient = axios.create({
  baseURL: 'https://example.com/api',
  headers: {
    'Content-Type': 'application/json',
    // 其他默认请求头...
  },
  timeout: 10000, // 超时时间（毫秒）
  // 其他配置...
});

// 使用自定义配置的实例进行 HTTP 请求
apiClient.get('/users')
  .then(response => {
    // 处理响应
  })
  .catch(error => {
    // 处理错误
  });
```

在这个例子中，`apiClient` 是一个具有自定义配置的 Axios 实例。它的默认配置包括基础URL、默认请求头、超时时间等。之后，你可以使用 `apiClient` 实例发起 HTTP 请求，它会根据配置自动应用这些默认值。

使用 `axios.create` 有几个主要优势：

1. **全局配置的共享：** 通过创建实例，你可以在整个应用程序中共享相同的全局配置，而无需每次请求都重新设置。

2. **模块化的配置：** 可以在应用中的不同模块或服务中使用不同的 Axios 实例，每个实例都可以具有自己的默认配置。

3. **便于测试：** 在单元测试中，你可以轻松地传递一个模拟的 Axios 实例，而不必直接操作全局的 Axios 对象。

总的来说，`axios.create` 是 Axios 提供的一个强大工具，用于更灵活地配置和管理你的 HTTP 请求。

## 十二.提取 User Service

**把所有关于http请求的代码放到UserService中,需要实现关注点分离**

user-service.ts文件

```ts
import apiClient from "./api-client";

export interface User {
    id: number;
    name: string;
  }
  

class UserService {
    getAllUser() {
      const controller = new AbortController();
      const request =apiClient.get<User[]>("/users", {
        signal: controller.signal,
      })
      return { request , cancel : () => controller.abort() }
    }

    deleteUser(id: number){
      return apiClient.delete("/users/" + id)
    }

    creatUser(user:User) {
      return apiClient.post("/users", user)
    }

    updateUser(user: User) {
      return apiClient.patch("/users" + user.id, user)
    }
}



export default new UserService();
```

App组件

```tsx
import { useEffect, useState } from "react";
import { CanceledError } from "./services/api-client";
import userService, { User } from "./services/user-service";

function App() {
  const [users, setUsers] = useState<User[]>([]);
  const [error, setError] = useState("");
  const [isLoading, setLoading] = useState(false);

  useEffect(() => {
    setLoading(true);

    const { request, cancel } = userService.getAllUser();
    request
      .then((res) => {
        setUsers(res.data);
        setLoading(false);
      })
      .catch((error) => {
        if (error instanceof CanceledError) return;
        {
          setError(error.message);
          setLoading(false);
        }
      });

    return () => cancel();
  }, []);

  const deleteUser = (user: User) => {
    const originalUser = [...users];
    setUsers(users.filter((u) => u.id !== user.id));

    userService.deleteUser(user.id).catch((error) => {
      setError(error.message);
      setUsers(originalUser);
    });
  };

  const addUser = () => {
    const originalUser = [...users];
    const newUser = { id: 0, name: "Mosh" };
    setUsers([newUser, ...users]);

    userService
    .creatUser(newUser)
    .catch((error) => {
      setError(error.message);
      setUsers(originalUser);
    });
  };

  const updateUser = (user: User) => {
    const updateUser = { ...user, name: user.name + "!" };
    setUsers(users.map((u) => (u.id === user.id ? updateUser : u)));

    userService
    .updateUser(updateUser)
    .catch((error) => {
      const originalUser = [...users];
      setError(error.message);
      setUsers(originalUser);
    });
  };

  return (
    <>
      {error && <p className="text-danger">{error}</p>}
      {isLoading && <div className="spinner-border"></div>}
      <button className="btn btn-primary mb-3" onClick={addUser}>
        Add
      </button>
      <ul className="list-group">
        {users.map((user) => (
          <li
            key={user.id}
            className="list-group-item d-flex justify-content-between"
          >
            {user.name}
            <div>
              <button
                className="btn btn-outline-secondary mx-1"
                onClick={() => updateUser(user)}
              >
                Update
              </button>
              <button
                className="btn btn-outline-danger"
                onClick={() => deleteUser(user)}
              >
                Delete
              </button>
            </div>
          </li>
        ))}
      </ul>
    </>
  );
}

export default App;

```

## 十三.创建一个通用的HTTP Service

**App.tsx**

```tsx
import { useEffect, useState } from "react";
import { CanceledError } from "./services/api-client";
import userService, { User } from "./services/user-service";

function App() {
  const [users, setUsers] = useState<User[]>([]);
  const [error, setError] = useState("");
  const [isLoading, setLoading] = useState(false);

  useEffect(() => {
    setLoading(true);

    const { request, cancel } = userService.getAll<User>();
    request
      .then((res) => {
        setUsers(res.data);
        setLoading(false);
      })
      .catch((error) => {
        if (error instanceof CanceledError) return;
        {
          setError(error.message);
          setLoading(false);
        }
      });

    return () => cancel();
  }, []);

  const deleteUser = (user: User) => {
    const originalUser = [...users];
    setUsers(users.filter((u) => u.id !== user.id));

    userService.delete(user.id).catch((error) => {
      setError(error.message);
      setUsers(originalUser);
    });
  };

  const addUser = () => {
    const originalUser = [...users];
    const newUser = { id: 0, name: "Mosh" };
    setUsers([newUser, ...users]);

    userService
    .creat(newUser)
    .catch((error) => {
      setError(error.message);
      setUsers(originalUser);
    });
  };

  const updateUser = (user: User) => {
    const updateUser = { ...user, name: user.name + "!" };
    setUsers(users.map((u) => (u.id === user.id ? updateUser : u)));

    userService
    .update(updateUser)
    .catch((error) => {
      const originalUser = [...users];
      setError(error.message);
      setUsers(originalUser);
    });
  };

  return (
    <>
      {error && <p className="text-danger">{error}</p>}
      {isLoading && <div className="spinner-border"></div>}
      <button className="btn btn-primary mb-3" onClick={addUser}>
        Add
      </button>
      <ul className="list-group">
        {users.map((user) => (
          <li
            key={user.id}
            className="list-group-item d-flex justify-content-between"
          >
            {user.name}
            <div>
              <button
                className="btn btn-outline-secondary mx-1"
                onClick={() => updateUser(user)}
              >
                Update
              </button>
              <button
                className="btn btn-outline-danger"
                onClick={() => deleteUser(user)}
              >
                Delete
              </button>
            </div>
          </li>
        ))}
      </ul>
    </>
  );
}

export default App;
```

**user-service.ts**

```tsx
import creat from "./http-service";

export interface User {
    id: number;
    name: string;
  }
  

export default creat('/users');
```

**http-service**

```tsx
import apiClient from "./api-client";

interface Entity{
    id : number;
}

class HttpService {
    endpoint: string;

    constructor(endpoint: string) {
        this.endpoint = endpoint;
    }

    getAll<T>() {
      const controller = new AbortController();
      const request =apiClient.get<T []>(this.endpoint, {
        signal: controller.signal,
      })
      return { request , cancel : () => controller.abort() }
    }

    delete (id: number){
      return apiClient.delete(this.endpoint +"/" + id)
    }

    creat<T>(entity:T) {
      return apiClient.post(this.endpoint, entity)
    }

    update<T extends Entity>(entity: T) {
      return apiClient.patch( entity +"/" + entity.id, entity)
    }
}


const creat = (endpoint: string) => new HttpService(endpoint);


export default creat ; 
```

这部分代码定义了一个 TypeScript 类 `HttpService`，该类用于封装 HTTP 请求相关的操作，包括获取资源、删除资源、创建资源以及更新资源。让我们来解释这个类的构造函数和属性：

```typescript
class HttpService {
  endpoint: string;

  constructor(endpoint: string) {
    this.endpoint = endpoint;
  }

  // 其他方法...
}
```

1. **`endpoint: string;` 属性:**
   - `endpoint` 是 `HttpService` 类的一个属性，用于存储与此服务实例关联的基础 URL 或端点。
   - 在 TypeScript 中，`endpoint` 被声明为一个字符串 (`string`) 类型。

2. **`constructor(endpoint: string)` 构造函数:**
   - 构造函数是在创建 `HttpService` 类的实例时自动调用的方法。
   - 构造函数接受一个 `endpoint` 参数，表示与服务交互的基础 URL 或端点。
   - 在构造函数中，`this.endpoint = endpoint;` 将传入的 `endpoint` 值分配给类的 `endpoint` 属性。这意味着每个 `HttpService` 实例都将与一个特定的端点相关联。

这种设计模式允许你在创建 `HttpService` 实例时指定不同的端点，使其可以用于与不同的 API 或资源进行交互。例如：

```typescript
// 创建与"/users"端点相关的HttpService实例
const userService = new HttpService('/users');

// 创建与"/posts"端点相关的HttpService实例
const postService = new HttpService('/posts');
```

在这两个示例中，`userService` 和 `postService` 分别关联到了不同的端点，使它们可以分别与用户资源和帖子资源进行交互。这种灵活性有助于组织和管理与不同 API 端点相关的操作。





## 十四.创建自定义钩子

目的:有时我们需要在其他地方的组件中使用到其中三个钩子，我们想把它变为一个可以重用的方法需要自定义钩子



我们需要创建一个hooks文件夹来储存我们的自定义钩子

**useUsers.ts**

```tsx
import { useEffect, useState } from "react";
import userService, { User } from "../services/user-service";
import { CanceledError } from "../services/api-client";


const useUsers = () =>{
    const [users, setUsers] = useState<User[]>([]);
    const [error, setError] = useState("");
    const [isLoading, setLoading] = useState(false);
  
    useEffect(() => {
      setLoading(true);
  
      const { request, cancel } = userService.getAll<User>();
      request
        .then((res) => {
          setUsers(res.data);
          setLoading(false);
        })
        .catch((error) => {
          if (error instanceof CanceledError) return;
          {
            setError(error.message);
            setLoading(false);
          }
        });
  
      return () => cancel();
    }, []);

    return { users, error, isLoading, setUsers, setError};
}


export default useUsers;
```

**App.tsx**

```tsx
import userService, { User } from "./services/user-service";
import useUsers from "./hooks/useUsers";

function App() {

  const {users,error,isLoading,setUsers,setError} = useUsers();

  const deleteUser = (user: User) => {
    const originalUser = [...users];
    setUsers(users.filter((u) => u.id !== user.id));

    userService.delete(user.id).catch((error) => {
      setError(error.message);
      setUsers(originalUser);
    });
  };

  const addUser = () => {
    const originalUser = [...users];
    const newUser = { id: 0, name: "Mosh" };
    setUsers([newUser, ...users]);

    userService
    .creat(newUser)
    .catch((error) => {
      setError(error.message);
      setUsers(originalUser);
    });
  };

  const updateUser = (user: User) => {
    const updateUser = { ...user, name: user.name + "!" };
    setUsers(users.map((u) => (u.id === user.id ? updateUser : u)));

    userService
    .update(updateUser)
    .catch((error) => {
      const originalUser = [...users];
      setError(error.message);
      setUsers(originalUser);
    });
  };

  return (
    <>
      {error && <p className="text-danger">{error}</p>}
      {isLoading && <div className="spinner-border"></div>}
      <button className="btn btn-primary mb-3" onClick={addUser}>
        Add
      </button>
      <ul className="list-group">
        {users.map((user) => (
          <li
            key={user.id}
            className="list-group-item d-flex justify-content-between"
          >
            {user.name}
            <div>
              <button
                className="btn btn-outline-secondary mx-1"
                onClick={() => updateUser(user)}
              >
                Update
              </button>
              <button
                className="btn btn-outline-danger"
                onClick={() => deleteUser(user)}
              >
                Delete
              </button>
            </div>
          </li>
        ))}
      </ul>
    </>
  );
}

export default App;

```

































